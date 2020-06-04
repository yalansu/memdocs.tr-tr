---
title: Android Kurumsal cihazları için VPN yapılandırma
titleSuffix: Microsoft Intune
description: Uygulama koruma İlkesi kullanın TOC, Android kurumsal cihazlar için bir VPN yapılandırın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347351"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Android Kurumsal cihazları için VPN yapılandırma

Bu konu başlığı altında, Android kurumsal cihazlarda bir VPN istemcisiyle birlikte dağıtılabilecek bir uygulama yapılandırma ilkesinin nasıl oluşturulacağı açıklanmaktadır. Bu yapılandırma, seçilen uygulamaların şirket kaynaklarına erişmesi için ağ trafiğine izin verir.

> [!NOTE]
> Android platformu, seçili uygulamalardan biri açıldığında VPN istemci bağlantısının otomatik olarak tetiklemesini desteklememektedir. VPN bağlantısı önce el ile başlatılmalıdır, ya da [her zaman VPN](../configuration/vpn-settings-android-enterprise.md)'yi de kullanabilirsiniz.

Başarılı VPN erişimi elde etmek için bir yapılandırma ilkesi oluşturmanın ön gereksinimleri, seçilen VPN istemcisinin yönetilen uygulama yapılandırma profillerini desteklemeye yönelik özelliğini içerir. Şu anda, Intune uygulama yapılandırma ilkesini destekleyen VPN istemcileri şunları içerir:
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Palo Alto küresel bağlantı
- Pulse Secure
- SonicWall Mobile Connect

VPN uç noktasına yönelik kimlik doğrulama erişimi için istemci sertifikalarının kullanılması gerekiyorsa, uygulama yapılandırma ilkesi için gerekli değerleri doldurmaya yardımcı olmak üzere Sertifika profillerinin önceden oluşturulması gerekir.

> [!NOTE]
> Android kurumsal iş profili senaryoları hem SCEP hem de PKCS sertifikalarını destekleirken, Android kurumsal cihaz sahibi senaryoları Şu anda yalnızca SCEP sertifikalarını destekler. 

Uygulama başına VPN profili oluşturmak ve test etmek için temel akış aşağıdaki adımlardır:
1.  Altyapınız için uygun VPN istemci uygulamasını seçin.
2.  VPN bağlantısıyla kullanmak istediğiniz üretkenlik uygulamalarının uygulama paketi kimliklerini belirler.
3.  VPN bağlantısının kimlik doğrulama gereksinimlerini karşılamak için gereken tüm sertifika profillerini dağıtın. Başarılı dağıtımı doğruladığınızdan emin olun.
4.  VPN istemci uygulamasını dağıtın.
5.  Önceki adımlarda toplanan bilgileri kullanarak uygulama yapılandırma tabanlı VPN profilini hazırlayın.
6.  Yeni oluşturulan VPN profilini dağıtın.
7.  VPN istemci uygulamasının VPN sunucusu altyapınıza başarıyla bağlanıp bağlanmayacağını doğrulayın.
8.  Seçili üretkenlik uygulamalarınızdan gelen trafiğin, etkin olduğunda VPN 'yi başarıyla yeniden geçişli olduğunu doğrulayın.

## <a name="get-the-app-package-id"></a>Uygulama paketi KIMLIĞINI al

VPN erişimi vermek istediğiniz her uygulama için paket KIMLIĞINI belirler. Genel olarak kullanılabilir uygulamalar için, Google Play deposundaki her bir uygulama için paket kimliklerini almayı göz önünde bulundurun. Her uygulama için görünen URL paket KIMLIĞINI içerir. Örneğin, Microsoft Edge tarayıcısının Android sürümü için paket KIMLIĞI `com.microsoft.emmx` . Paket KIMLIĞI URL 'nin bir parçası olarak dahil edilir.

![Uygulama paketi KIMLIĞINI bulma örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

Iş kolu (LOB) uygulamaları için satıcınıza veya uygulama geliştirme ekibinize ilgili paket KIMLIĞINI sağlamasını isteyin.

## <a name="certificates"></a>Sertifikalar

Bu konu başlığında, VPN bağlantınızın sertifika tabanlı kimlik doğrulamasını kullandığını ve istemci kimlik doğrulamasının başarılı olması için gereken zincirdeki tüm sertifikaları başarıyla dağıttığımız varsayılmaktadır. Genellikle, bu istemci sertifikası, tüm ara sertifikalar ve kök sertifika olacaktır.
Android Enterprise için sertifika dağıtımı hakkında daha fazla bilgi için, konusunu inceleyerek [Microsoft Intune kimlik doğrulaması için sertifikaları kullanın](../protect/certificates-configure.md).

İstemci kimlik doğrulama sertifikası profiliniz dağıtıldıktan sonra, VPN uygulama yapılandırma ilkesini oluşturmak için bu profille ilgili bazı ayrıntılara ihtiyacınız vardır.
Uygulama yapılandırma profilleri oluşturma konusunda bilgi sahibi değilseniz, [yönetilen Android Kurumsal cihazları için uygulama yapılandırma Ilkeleri ekleme](../apps/app-configuration-policies-use-android.md)konusuna bakın.
 

## <a name="build-the-vpn-profile"></a>VPN profili oluşturma

VPN uygulamanız için uygulama yapılandırma ilkesini oluşturmanın iki yolu vardır. **Yapılandırma tasarımcısını** veya **JSON verileri** seçeneğini kullanabilirsiniz. Tüm gerekli VPN ayarlarının **yapılandırma Tasarımcısı** yönteminde kullanılamadığı durumlarda **JSON verileri** seçeneği gereklidir. Destek için JSON seçeneğinin gerekli olduğunu belirlerseniz VPN satıcınıza başvurun. Bu konu başlığında her iki yöntemin da örnekleri gösterilecektir. Hem **JSON verileri** hem de **yapılandırma Tasarımcısı** yöntemlerinde sertifika tabanlı kimlik doğrulamasını başarıyla ekleyebilirsiniz. **JSON veri** yöntemini kullanırken, gerekli profil değerlerini ayıklamak için **yapılandırma tasarımcısını** kullanarak başlayabilirsiniz.

> [!NOTE]
> VPN istemci yapılandırma parametrelerinin birçoğu benzerdir, ancak her uygulamanın benzersiz anahtarları ve seçenekleri vardır. Sorular ortaya çıkarsa VPN satıcınıza danışın. 

## <a name="use-the-configuration-designer-flow"></a>Yapılandırma Tasarımcısı akışını kullanma

1.  **Yönetilen cihazlar**için yeni bir uygulama yapılandırma ilkesi ekleyerek başlayın.
2.  Uygun bir ad girin.
3.  Platform olarak **Android Enterprise** ' ı seçin.
4.  Sertifika tabanlı kimlik doğrulaması gerekliyse **yalnızca Iş profili** veya **cihaz sahibi yalnızca** profil türü olarak seçin. **Çalışma sahibi ve cihaz sahibi profili** sertifika tabanlı kimlik doğrulamasıyla uyumlu değil.
5.  Hedeflenen uygulama için, dağıttığınız VPN istemcisini seçin; Bu örnekte, önceden dağıtılan Cisco AnyConnect VPN istemcisini kullanıyoruz

  ![Uygulama yapılandırma ilkesi oluşturma örneği-temel bilgiler.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. Sonraki sayfada yapılandırma ayarları açılır öğesini kullanın ve **yapılandırma tasarımcısını kullan** seçeneğini belirleyin.

  ![Yapılandırma Tasarımcısı Flow-Settings kullanımı örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. Yapılandırma anahtarlarının listesini açmak için **Ekle** ' ye tıklayın.
8.  Seçtiğiniz yapılandırma için gereken tüm yapılandırma anahtarlarını seçin. Bu örnekte, sertifika tabanlı kimlik doğrulaması ve uygulama başına VPN gibi AnyConnect VPN için ayarlamak üzere en az bir liste kullanıyoruz.
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. **Bağlantı adı**, **ana bilgisayar**ve **protokol** anahtarları için uygun değerleri girin.

  ![Yapılandırma Tasarımcısı Flow-yapılandırma anahtarı seçimini kullanma örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > Bu anahtarların adları, ilkeyi oluşturduğunuz VPN Istemci uygulamasına bağlı olarak farklılık gösterebilir.

10. Daha önce, **uygulama BAŞıNA VPN Izin verilen uygulamalar** anahtarında topladığınız uygulama paketi kimliklerini girin.

  ![Yapılandırma Tasarımcısı Flow-App Package kimliklerini kullanma örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. **Anahtarlık sertifikası diğer adı** (isteğe bağlı) anahtarında **değer türünü** **dizeden** **sertifikaya**değiştirin, bu, VPN kimlik doğrulamasıyla kullanılacak doğru istemci sertifikası profilini seçmenizi sağlar.

  ![Yapılandırma Tasarımcısı Flow-güncelleştirme Anahtarlık sertifikası diğer adını kullanma örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. Sonraki sayfada, uygun kapsam etiketlerini seçin.
13. Sonraki sayfada, uygulama yapılandırma ilkesini dağıtmak istediğiniz uygun grupları girin.
14. İlkenin oluşturulmasını ve dağıtımını gerçekleştirmek için **Oluştur** ' u seçin.

  ![Yapılandırma Tasarımcısı Flow-Review kullanımı örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>JSON akışını kullanma

Geçici bir profil oluşturun:
1.  **Yönetilen cihazlar**için yeni bir uygulama yapılandırma ilkesi ekleyerek başlayın.
2.  Uygun bir ad girin (Bu profil kaydedilmeyecektir çünkü bu profilin kullanılması geçicidir).
3.  Platform olarak **Android Enterprise** ' ı seçin.
4.  Hedeflenen uygulama için, dağıttığınız VPN istemcisini seçin.
5.  Sertifika tabanlı kimlik doğrulaması gerekliyse **yalnızca Iş profili** veya **cihaz sahibi yalnızca** profil türü olarak seçin. **Çalışma sahibi ve cihaz sahibi profili** sertifika tabanlı kimlik doğrulamasıyla uyumlu değil.

  ![JSON Flow temel bilgileri kullanımı örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  Sonraki sayfada **yapılandırma ayarları** açılır öğesini kullanın ve **yapılandırma tasarımcısını kullan**seçeneğini belirleyin.

  ![JSON Flow-yapılandırma ayarları biçimi kullanma örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  Yapılandırma anahtarlarının listesini açmak için **Ekle** ' ye tıklayın.
8.  **Değer türü** **dize**olan anahtarlardan birini seçin ve **Tamam**' a tıklayın.

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  Bundan sonra **değer türünü** **dizeden** **sertifikaya**değiştirin. Bu, VPN kimlik doğrulamasıyla kullanılacak doğru istemci sertifikası profilini seçmenizi sağlar.

  ![JSON Flow bağlantı adını kullanma örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. **Değer türünü** hemen **dizeye**doğru olarak değiştirin. **Yapılandırma değerinin** biçim belirtecine değiştiği unutulmamalıdır `{{cert:GUID}}` .
11. Sertifikanın belirteç temsilini seçin ve metin düzenleyici gibi alternatif bir konuma kopyalayın.

  ![JSON Flow-yapılandırma değerini kullanma örneği.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. Oluşturulmakta olan profili at – önceki adımların tek amacı sertifika belirtecini belirlemektir.

### <a name="create-the-vpn-profile"></a>VPN profili oluşturma

1.  **Yönetilen cihazlar**için yeni bir uygulama yapılandırma profili ekleyerek başlayın.
2.  Uygun bir ad girin.
3.  Platform olarak **Android Enterprise** ' ı seçin.
4.  Hedeflenen uygulama için, dağıttığınız VPN istemcisini seçin.
5.  Sertifika tabanlı kimlik doğrulaması gerekliyse **yalnızca Iş profili** veya **cihaz sahibi yalnızca** profil türü olarak seçin. **Çalışma sahibi ve cihaz sahibi profili** sertifika tabanlı kimlik doğrulamasıyla uyumlu değil.
6.  **Yapılandırma ayarları açılır öğesini** kullanın ve **JSON verisi gir**seçeneğini belirleyin.
7.  JSON 'u doğrudan düzenleyebilir veya tercih ediyorsanız **JSON şablonu indir** düğmesini kullanarak şablonu dilediğiniz bir dış düzenleyicide değiştirin. İçerme JSON 'u geçersiz olarak işlerken **Akıllı Tırnakları**kullanma seçeneğine sahip metin düzenleyicilerle dikkatli olun.

  ![JSON akışını kullanma örneği-JSON düzenleme.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  Kullandığınız yöntemden bağımsız olarak, istenen yapılandırma için gereken değerleri doldurduktan sonra, tüm JSON içindeki "STRING_VALUE" veya STRING_VALUE değeri ile kalan tüm ayarların kaldırılması gerekir.

#### <a name="example-json-for-f5-access-vpn"></a>F5 Access VPN için örnek JSON

Aşağıda, F5 Access VPN için JSON verilerinin bir örneği verilmiştir.

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

## <a name="summary"></a>Özet

Android kurumsal kayıtlı cihazlar için bir uygulama yapılandırma ilkesi kullanmak, platformda doğrudan destek yokluğunda uygulama başına VPN davranışından yararlanmanızı sağlar. 

## <a name="additional-information"></a>Ek bilgiler

İlgili bilgiler için aşağıdaki konulara bakın:
- [Yönetilen Android Kurumsal cihazları için uygulama yapılandırma ilkeleri ekleme](../apps/app-configuration-policies-use-android.md)
- [Intune 'da VPN yapılandırmak için Android kurumsal cihaz ayarları](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Sonraki adımlar

- [Intune 'da VPN sunucularına bağlanmak için VPN profilleri oluşturma](../configuration/vpn-settings-configure.md)
