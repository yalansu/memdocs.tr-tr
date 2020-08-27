---
title: Microsoft Intune-Azure 'da Android cihazları için Microsoft Defender ATP Web korumasını yönetme | Microsoft Docs
description: Intune 'da Android için Microsoft Defender Gelişmiş tehdit koruması (Microsoft Defender ATP) Web koruması 'nı yapılandırın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49423d1d1b887aaf3ed3323ff36678bb7319b1ad
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909474"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Intune ile yönettiğiniz Android cihazlarda Microsoft Defender ATP 'yi yapılandırma

Microsoft Intune ve Microsoft Defender Gelişmiş tehdit koruması 'nı (ATP) tümleştirdiğinizde, Android cihazlarda Microsoft Defender ATP 'nin bazı ayarlarını değiştirmek için cihaz yapılandırma profillerini kullanabilirsiniz.

Öncesinde, [Intune 'Da Microsoft Defender ATP](../protect/advanced-threat-protection-configure.md) 'Yi başarıyla yapılandırmanız ve Android cihazları MICROSOFT Defender ATP 'ye eklemek zorundasınız.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Android çalıştıran cihazlarda web korumasını yapılandırma

Varsayılan olarak, Android için Microsoft Defender ATP, Web Koruması özelliğini içerir ve sunar. [Web koruması](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) , cihazların Web tehditlerine karşı güvenliğini sağlamaya ve kullanıcıların kimlik avı saldırılarına karşı korunmasına yardımcı olur.

Varsayılan olarak etkinleştirildiğinde, bazı Android cihazlarda bu korumanın devre dışı bırakılması için geçerli nedenler vardır. Örneğin, yalnızca Microsoft Defender ATP uygulama tarama özelliğini kullanmayı veya zararlı URL 'Leri tararken Web korumasının VPN 'nizi kullanmasını engellemek için seçeneğini kullanabilirsiniz.

Intune, Web koruması özelliğinin tamamını veya bir kısmını kapatmayı destekler. Kullandığınız yöntem ve devre dışı bırakabilecek yetenekler, Android cihazının Intune 'a nasıl kaydedildiği üzerine bağlıdır:

- **Android Cihaz Yöneticisi**: Web koruması özelliğinin tamamını devre dışı bırakmak veya yalnızca VPN kullanımını devre dışı bırakmak için CIHAZDA özel OMA-URI ayarları ayarlamak için bir yapılandırma profili kullanın. Android cihazları için özel ayarlar hakkında genel bilgi için bkz. [özel ayarlar](../configuration/custom-settings-android.md).

- **Android kurumsal iş profili**: Web korumasını devre dışı bırakmak için bir uygulama yapılandırma profili ve *yapılandırma Tasarımcısı* kullanın. Bu yöntem ve kayıt türü tüm Web koruması yeteneklerini devre dışı bırakmayı destekler, ancak yalnızca VPN kullanımını devre dışı bırakmayı desteklemez. Uygulama yapılandırma ilkeleri hakkında genel bilgi için bkz. [yapılandırma tasarımcısını kullanma](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Cihazlarda web koruması 'nı yapılandırmak için, uygulanabilir yapılandırmayı oluşturup dağıtmak üzere aşağıdaki yordamları kullanın.

### <a name="disable-web-protection-for-android-device-administrator"></a>Android Cihaz Yöneticisi için Web korumasını devre dışı bırak

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. Aşağıdaki ayarları girin:

   - **Platform**: **Android cihaz yöneticisini** seçin
   - **Profil**: **özel** ' i seçin

   **Oluştur**’u seçin.

4. **Temel bilgiler**için aşağıdaki ayrıntıları girin:

   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, *Microsoft Defender ATP Web koruması Için Android özel profili*
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır, ancak önerilir.

5. **Yapılandırma ayarları**' nı seçin, **Ekle**' yi seçin.

   Dağıtmak istediğiniz yapılandırma için ayarları belirtin:

   - **Web korumasını devre dışı bırak**:
     - **Ad**: Bu OMA-URI ayarı için benzersiz bir ad girin, böylece kolayca bulabilirsiniz. Örneğin, *Microsoft Defender ATP Web korumasını devre dışı bırakın*
     - **Açıklama**: (isteğe bağlı) ayara genel bir bakış sunan bir açıklama ve diğer önemli ayrıntıları girin.
     - **OMA-URI**: girin **./Vendor/MSFT/savunma Deratp/antisızdırma**
     - **Veri türü**: açılan eklentiyi kullanın ve **tamsayı** ' ı seçin
     - **Değer**: VPN tabanlı tarama dahil olmak üzere Web korumasını devre dışı bırakmak için **0** girin.
       > [!NOTE]
       > Web koruması için varsayılan olan Web korumasını etkinleştirmek üzere **1** girin.

   - **Yalnızca Web Koruması tarafından VPN kullanımını devre dışı bırak**:
     - **Ad**: Bu OMA-URI ayarı için benzersiz bir ad girin, böylece kolayca bulabilirsiniz. Örneğin, *Microsoft Defender ATP Web KORUMASı VPN 'Yi devre dışı bırak*
     - **Açıklama**: (isteğe bağlı) ayara genel bir bakış sunan bir açıklama ve diğer önemli ayrıntıları girin.
     - **OMA-URI**: girin **./Vendor/MSFT/savunma Deratp/VPN**
     - **Veri türü**: açılan eklentiyi kullanın ve **tamsayı** ' ı seçin
     - **Değer**: VPN tabanlı taramayı devre dışı bırakmak için **0** girin.
       > [!NOTE]
       > Web koruması için varsayılan olan Web korumasını etkinleştirmek üzere **1** girin.

   **Ekle** ' yı seçerek OMA-URI ayarları yapılandırmasını kaydedin ve devam etmek için **İleri** ' yi seçin.

6. **Atamalar**' da, bu profili alacak grupları belirtin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

7. **İnceleme ve oluşturma**' da Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Android kurumsal iş profili için Web korumasını devre dışı bırak

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Ekle**' yi seçin ve ardından yönetilen cihazlar ' ı seçin.

3. **Temel bilgiler**için aşağıdaki ayrıntıları girin:

   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, *Microsoft Defender ATP Web koruması Için Android uygulama yapılandırması*.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır, ancak önerilir.
   - **Platform**: **Android Enterprise** seçin
   - **Profil türü**: **yalnızca iş profilini** seçin
   - **Hedeflenen uygulama**: **Uygulama Seç**' e tıklayın.

4. **İlişkili uygulamada**, **Defender ATP**öğesini bulup seçin ve ardından İleri ' yi **seçin**  >  **Next**.

5. **Ayarlar**' da, **yapılandırma ayarları biçimi**için açılan açılan ayarı kullanın, **yapılandırma tasarımcısını kullan**' ı seçin ve ardından **Ekle**' ye tıklayın. JSON Düzenleyicisi açılır.

6. **Web koruması**' nı bulup seçin ve ardından **Ayarlar** sayfasına dönmek için **Tamam** ' ı seçin.

7. **Yapılandırma değeri**için, Web korumasını devre dışı bırakmak için **0** girin.

   > [!NOTE]
   > Web koruması için varsayılan olan Web korumasını etkinleştirmek üzere **1** girin.

   Devam etmek için **İleri** seçeneğini belirleyin.

8. **Atamalar**' da, bu profili alacak grupları belirtin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

9. **İnceleme ve oluşturma**' da Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

## <a name="next-steps"></a>Sonraki adımlar

- [Risk düzeyleri için uyumluluğu izleme](../protect/advanced-threat-protection-monitor.md)
- [Cihazların sorunlarını gidermek için ATPs güvenlik açığı yönetimi ile güvenlik görevlerini kullanma](../protect/atp-manage-vulnerabilities.md)

Microsoft Defender ATP belgelerinden daha fazla bilgi edinin:

- [Microsoft Defender ATP koşullu erişimi](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP risk panosu](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)