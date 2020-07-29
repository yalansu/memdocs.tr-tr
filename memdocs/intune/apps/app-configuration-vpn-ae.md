---
title: Microsoft Intune 'de Android Kurumsal cihazları için bir VPN veya uygulama başına VPN yapılandırın | Microsoft Docs
titleSuffix: Microsoft Intune
description: Microsoft Intune ' de Android kurumsal cihazlara yönelik bir VPN veya uygulama başına VPN profili eklemek veya oluşturmak için bir uygulama yapılandırma ilkesi kullanın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262906"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Microsoft Intune 'de Android kurumsal cihazlarda VPN ve uygulama başına VPN ilkesi kullanın

Sanal özel ağlar (VPN), kullanıcıların, ana, otel, calarlar ve daha fazlası dahil olmak üzere kuruluş kaynaklarına uzaktan erişmesini sağlar. Microsoft Intune, bir uygulama yapılandırma ilkesi kullanarak Android kurumsal cihazlarda VPN istemci uygulamalarını yapılandırabilirsiniz. Ardından, bu ilkeyi kuruluşunuzdaki cihazlara VPN yapılandırmasıyla dağıtın.

Ayrıca, belirli uygulamalar tarafından kullanılan VPN ilkeleri de oluşturabilirsiniz. Bu özellik uygulama başına VPN olarak adlandırılır. Uygulama etkin olduğunda, VPN 'ye bağlanabilir ve VPN üzerinden kaynaklara erişebilir. Uygulama etkin olmadığında VPN kullanılmaz.

Bu özellik şu platformlarda geçerlidir:

- Android Kurumsal

VPN istemci uygulamanız için uygulama yapılandırma ilkesini oluşturmanın iki yolu vardır:

- Yapılandırma tasarımcısı
- JSON verileri

Bu makalede her iki seçeneği kullanarak uygulama başına VPN ve VPN uygulama yapılandırma ilkesi oluşturma işlemlerinin nasıl yapılacağı gösterilir.

> [!NOTE]
> VPN istemci yapılandırma parametrelerinin birçoğu benzerdir. Ancak, her uygulamanın benzersiz anahtar ve seçenekleri vardır. Sorularınız varsa VPN satıcınıza danışın.

## <a name="before-you-begin"></a>Başlamadan önce

- Bir uygulama açıldığında Android, VPN istemci bağlantısını otomatik olarak tetiklemez. VPN bağlantısının el ile başlatılması gerekir. Ya da bağlantıyı başlatmak için [Always on VPN](../configuration/vpn-settings-android-enterprise.md) kullanabilirsiniz.

- Aşağıdaki VPN istemcileri Intune uygulama yapılandırma ilkelerini destekler:

  - Cisco AnyConnect
  - Citrix SSO
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- Intune 'da VPN ilkesi oluşturduğunuzda, yapılandırmak için farklı anahtarlar seçersiniz. Bu anahtar adları farklı VPN istemci uygulamalarına göre farklılık gösterir. Bu nedenle, ortamınızdaki anahtar adları bu makaledeki örneklerden farklı olabilir.

- Yapılandırma Tasarımcısı ve JSON verileri, sertifika tabanlı kimlik doğrulamasını başarılı bir şekilde kullanabilir. VPN kimlik doğrulaması için istemci sertifikaları gerekiyorsa, VPN ilkesini oluşturmadan önce sertifika profillerini oluşturun. VPN uygulama yapılandırma ilkeleri, sertifika profillerindeki değerleri kullanır.

  Android kurumsal iş profili cihazları, SCEP ve PKCS sertifikalarını destekler. Android kurumsal tam olarak yönetilen, adanmış ve şirkete ait iş profili cihazları yalnızca SCEP sertifikalarını destekler. Daha fazla bilgi için bkz. [Microsoft Intune kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md).

## <a name="per-app-vpn-overview"></a>Uygulama başına VPN 'ye Genel Bakış

Uygulama başına VPN oluştururken ve test edilirken, temel akış aşağıdaki adımları içerir:

1. VPN istemci uygulamasını seçin. [Başlamadan önce](#before-you-begin) (Bu makalede) desteklenen uygulamaları listeler.
2. VPN bağlantısını kullanacak uygulamaların uygulama paketi kimliklerini alın. [Uygulama PAKETI kimliğini alma](#get-the-app-package-id) (Bu makalede) size nasıl yapılacağını gösterir.
3. VPN bağlantısının kimliğini doğrulamak için sertifikalar kullanıyorsanız, VPN ilkesini dağıtmadan önce sertifika profillerini oluşturun ve dağıtın. Sertifika profillerinin başarılı bir şekilde dağıttığınızdan emin olun. Daha fazla bilgi için bkz. [Microsoft Intune kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md).
4. [VPN istemci uygulamasını](apps-add-android-for-work.md) Intune 'a ekleyin ve uygulamayı kullanıcılarınıza ve cihazlarınıza dağıtın.
5. VPN uygulama yapılandırma ilkesini oluşturun. İlkedeki uygulama paketi kimliklerini ve sertifika bilgilerini kullanın.
6. Yeni VPN ilkesini dağıtın.
7. VPN istemci uygulamasının VPN sunucunuza başarıyla bağlandığını doğrulayın.
8. Uygulama etkin olduğunda, uygulamanızdan gelen trafiğin VPN üzerinden başarılı bir şekilde gitdiğini doğrulayın.

## <a name="get-the-app-package-id"></a>Uygulama paketi KIMLIĞINI al

VPN kullanacak her uygulama için paket KIMLIĞINI alın. Genel kullanıma açık uygulamalar için, Google Play deposundaki uygulama paketi KIMLIĞINI alabilirsiniz. Her uygulama için görünen URL paket KIMLIĞINI içerir.

Aşağıdaki örnekte, Microsoft Edge tarayıcı uygulamasının paket KIMLIĞI `com.microsoft.emmx` . Paket KIMLIĞI URL 'nin bir parçasıdır:

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Google Play deposundaki URL 'de uygulama paketi KIMLIĞINI alın.":::

Iş kolu (LOB) uygulamaları için, satıcı veya uygulama geliştiricisinden paket KIMLIĞINI alın.

## <a name="certificates"></a>Sertifikalar

Bu makalede, VPN bağlantınızın sertifika tabanlı kimlik doğrulaması kullandığı varsayılmaktadır. Ayrıca, istemcilerin başarıyla kimlik doğrulaması yapması için gereken zincirdeki tüm sertifikaları başarıyla dağıttığınızı varsayar. Genellikle, bu sertifika zinciri istemci sertifikasını, tüm ara sertifikaları ve kök sertifikayı içerir.

Sertifikalar hakkında daha fazla bilgi için bkz. [Microsoft Intune kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md).

İstemci kimlik doğrulama sertifikası profiliniz dağıtıldığında, sertifika profilinde bir sertifika belirteci oluşturur. Bu belirteç, VPN uygulama yapılandırma ilkesini oluşturmak için kullanılır.

Uygulama yapılandırma ilkeleri oluşturma konusunda bilgi sahibi değilseniz, bkz. [yönetilen Android Kurumsal cihazları için uygulama yapılandırma Ilkeleri ekleme](app-configuration-policies-use-android.md).

## <a name="use-the-configuration-designer"></a>Yapılandırma tasarımcısını kullanma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen cihazlar**ekleme ' yi seçin.
3. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **uygulama yapılandırma ilkesidir: Android kurumsal iş profili cihazları Için Cisco AnyConnect VPN ilkesi**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: **Android kurumsal**' i seçin.
    - **Profil türü**: seçenekleriniz:
      - **Tüm profil türleri**: Bu seçenek Kullanıcı adı ve parola kimlik doğrulamasını destekler. Sertifika tabanlı kimlik doğrulaması kullanıyorsanız, bu seçeneği kullanmayın.
      - **Yalnızca tam olarak yönetilen, adanmış ve şirkete ait iş profili**: Bu seçenek sertifika tabanlı kimlik doğrulamayı ve Kullanıcı adı ve parola kimlik doğrulamasını destekler.
      - **Yalnızca Iş profili**: Bu seçenek sertifika tabanlı kimlik doğrulamayı ve Kullanıcı adı ve parola kimlik doğrulamasını destekler.
    - **Hedeflenen uygulama**: daha önce EKLEMIŞ olduğunuz VPN istemci uygulamasını seçin. Aşağıdaki örnekte, Cisco AnyConnect VPN istemci uygulaması kullanılır:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Microsoft Intune 'de VPN veya uygulama başına VPN yapılandırmak için bir uygulama yapılandırma ilkesi oluşturma":::

4. **İleri**’yi seçin.
5. **Ayarlar**' da, aşağıdaki özellikleri girin:

    - **Yapılandırma ayarları biçimi**: **yapılandırma tasarımcısını kullan**' ı seçin:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="Yapılandırma Tasarımcısı 'Nı kullanarak Microsoft Intune bir uygulama yapılandırması VPN ilkesi oluşturun-örnek.":::

    - **Ekle**: yapılandırma anahtarlarının listesini gösterir. Yapılandırmanız için gereken tüm yapılandırma anahtarlarını seçin > Tamam ' **ı**seçin.

      Aşağıdaki örnekte, sertifika tabanlı kimlik doğrulaması ve uygulama başına VPN de dahil olmak üzere, AnyConnect VPN için en az bir liste seçtik:
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="Yapılandırma Tasarımcısı-örnek kullanarak Microsoft Intune bir VPN uygulama yapılandırma ilkesine yapılandırma anahtarları ekleyin.":::

    - **Yapılandırma değeri**: seçtiğiniz yapılandırma anahtarlarının değerlerini girin. Anahtar adlarının, kullanmakta olduğunuz VPN Istemci uygulamasına bağlı olarak değişebileceğini unutmayın. Örneğimizde seçili anahtarlar:

      - **Uygulama BAŞıNA VPN Izin verilen uygulamalar**: daha önce topladığınız uygulama paketi kimliklerini girin. Örnek:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="Yapılandırma Tasarımcısı örneğini kullanarak Microsoft Intune bir VPN uygulama yapılandırma ilkesine izin verilen uygulama paketi kimliklerini girin.":::

      - **Anahtarlık sertifikası diğer adı** (isteğe bağlı): **dizeden** **sertifika**olarak **değer türünü** değiştirin. VPN kimlik doğrulamasıyla kullanılacak istemci sertifikası profilini seçin. Örnek:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="Yapılandırma Tasarımcısı örneğini kullanarak Microsoft Intune bir VPN uygulama yapılandırma ilkesinde anahtar zinciri istemci sertifikası diğer adını değiştirin.":::

      - **Protokol**: VPN 'in **SSL** veya **IPSec** tünel protokolünü seçin.
      - **Bağlantı adı**: VPN bağlantısı için Kullanıcı dostu bir ad girin. Kullanıcılar bu bağlantı adını cihazlarında görür. Örneğin, `ContosoVPN` girin.
      - **Ana bilgisayar**: Ana BILGISAYAR adı URL 'sini, yayın uç yönlendiricisine girin. Örneğin, `vpn.contoso.com` girin.

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="Yapılandırma tasarımcısını kullanarak Microsoft Intune bir VPN uygulama yapılandırma ilkesinde protokol, bağlantı adı ve ana bilgisayar adı örnekleri":::

6. **İleri**’yi seçin.
7. **Atamalar**' da, VPN uygulama yapılandırma ilkesini atamak için grupları seçin.

    **İleri**’yi seçin.

8. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve ilke gruplarınıza dağıtılır. İlke ayrıca uygulama yapılandırma ilkeleri listesinde gösterilir.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="Microsoft Intune örneğinde yapılandırma Tasarımcısı akışını kullanarak uygulama yapılandırma ilkesini gözden geçirin.":::

## <a name="use-json"></a>JSON kullanma

**Yapılandırma tasarımcısında**kullanılan tüm VPN ayarlarını bilmiyorsanız veya bilmiyorsanız bu seçeneği kullanın. Yardıma ihtiyacınız varsa VPN satıcınıza başvurun.

### <a name="get-the-certificate-token"></a>Sertifika belirtecini al

Bu adımlarda geçici bir ilke oluşturun. İlke kaydedilmez. Amaç, sertifika belirtecini kopyalayamaktır. Bu belirteci, JSON kullanarak VPN ilkesi oluştururken kullanacaksınız (sonraki bölüm).

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen cihazlar**Ekle ' yi seçin.
2. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: herhangi bir ad girin. Bu ilke geçicidir ve kaydedilmez.
    - **Platform**: **Android kurumsal**' i seçin.
    - **Profil türü**: **yalnızca iş profilini**seçin.
    - **Hedeflenen uygulama**: daha önce EKLEMIŞ olduğunuz VPN istemci uygulamasını seçin.

3. **İleri**’yi seçin.
4. **Ayarlar**' da, aşağıdaki özellikleri girin:

    - **Yapılandırma ayarları biçimi**: **yapılandırma tasarımcısını kullan**' ı seçin.
    - **Ekle**: yapılandırma anahtarlarının listesini gösterir. **Dize** **değer türünde** bir anahtar seçin. **Tamam**’ı seçin.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="Yapılandırma Tasarımcısı 'nda Microsoft Intune VPN uygulama yapılandırma ilkesinde dize değer türü olan bir anahtar seçin":::

5. **Değer türünü** **dizeden** **sertifikaya**değiştirin. Bu adım VPN 'in kimliğini doğrulayan doğru istemci sertifikası profilini seçmenizi sağlar:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="Microsoft Intune örnekteki bir VPN uygulama yapılandırma ilkesinde bağlantı adını değiştirme":::

6. **Değer türünü** hemen **dizeye**doğru olarak değiştirin. **Yapılandırma değeri** bir belirteç olarak değişir `{{cert:GUID}}` :

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="Yapılandırma değeri Microsoft Intune içindeki bir VPN uygulama yapılandırma ilkesinde sertifika belirtecini gösterir":::

7. Bu sertifika belirtecini kopyalayıp metin Düzenleyicisi gibi başka bir dosyaya yapıştırın.

8. Bu ilkeyi atın. Kaydetme. Tek amaç, sertifika belirtecini kopyalayıp yapıştırmaktır.

### <a name="create-the-vpn-policy-using-json"></a>JSON kullanarak VPN ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen cihazlar**Ekle ' yi seçin.

2. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **uygulama yapılandırma ilkesidir: tüm şirketteki Android kurumsal iş profili cihazları IÇIN JSON Cisco AnyConnect VPN ilkesi**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: **Android kurumsal**' i seçin.
    - **Profil türü**: seçenekleriniz:
      - **Tüm profil türleri**: Bu seçenek Kullanıcı adı ve parola kimlik doğrulamasını destekler. Sertifika tabanlı kimlik doğrulaması kullanıyorsanız, bu seçeneği kullanmayın.
      - **Yalnızca tam olarak yönetilen, adanmış ve şirkete ait iş profili**: Bu seçenek sertifika tabanlı kimlik doğrulamayı ve Kullanıcı adı ve parola kimlik doğrulamasını destekler.
      - **Yalnızca Iş profili**: Bu seçenek sertifika tabanlı kimlik doğrulamayı ve Kullanıcı adı ve parola kimlik doğrulamasını destekler.
    - **Hedeflenen uygulama**: daha önce EKLEMIŞ olduğunuz VPN istemci uygulamasını seçin. 

3. **İleri**’yi seçin.
4. **Ayarlar**' da, aşağıdaki özellikleri girin:

    - **Yapılandırma ayarları biçimi**: **JSON verisi gir**' i seçin. JSON 'ı doğrudan düzenleyebilirsiniz.
    - **JSON şablonunu indirin**: Bu seçeneği, şablonu indirmek ve herhangi bir harici düzenleyicide güncelleştirmek için kullanın. Geçersiz JSON oluşturduklarında **Akıllı Tırnakları**kullanan metin düzenleyicilerle dikkatli olun.

    Yapılandırmanız için gereken değerleri girdikten sonra, veya içeren tüm ayarları kaldırın `"STRING_VALUE"` `STRING_VALUE` .

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="JSON akışını kullanma örneği-JSON düzenleme.":::

5. **İleri**’yi seçin.
6. **Atamalar**' da, VPN uygulama yapılandırma ilkesini atamak için grupları seçin.

    **İleri**’yi seçin.

7. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve ilke gruplarınıza dağıtılır. İlke ayrıca uygulama yapılandırma ilkeleri listesinde gösterilir.

#### <a name="json-example-for-f5-access-vpn"></a>F5 Access VPN için JSON örneği

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>Ek bilgiler

- [Yönetilen Android Kurumsal cihazları için uygulama yapılandırma ilkeleri ekleme](app-configuration-policies-use-android.md)
- [Intune 'da VPN yapılandırmak için Android kurumsal cihaz ayarları](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Sonraki adımlar

- [Intune 'da VPN sunucularına bağlanmak için VPN profilleri oluşturma](../configuration/vpn-settings-configure.md)
