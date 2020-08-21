---
title: Ortak yönetimi izleme
titleSuffix: Configuration Manager
description: Ortak yönetilen cihazlarla ilgili bilgileri gözden geçirmek için ortak yönetim panosunu kullanın.
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ac3bbb7c755be82b171f35442d2dbaf446dfea84
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695129"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Configuration Manager 'da ortak yönetimi izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Ortak yönetimi etkinleştirdikten sonra, aşağıdaki yöntemleri kullanarak ortak yönetim cihazlarını izleyin:

- [Ortak yönetim panosu](#co-management-dashboard)  

- [Dağıtım ilkeleri](#deployment-policies)

- [WMI cihaz verileri](#wmi-device-data)

## <a name="co-management-dashboard"></a>Ortak yönetim panosu

Bu Pano, ortamınızda birlikte yönetilen makineleri incelemenizi sağlar. Grafikler ilgilenilmesi gerekebilecek cihazları belirlemenize yardımcı olabilir.<!--1356648,1358980-->

Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **ortak yönetim** düğümünü seçin.

![Ortak yönetim panosunun ekran görüntüsü](media/co-management-dashboard.png)

### <a name="client-os-distribution"></a>İstemci işletim sistemi dağıtımı

Sürüme göre işletim sistemi başına istemci cihaz sayısını gösterir. Aşağıdaki gruplandırmaları kullanır:  

- Windows 7 & 8. x
- 1709 'den düşük Windows 10  
- Windows 10 1709 ve üzeri  

    > [!Tip]  
    > Windows 10, sürüm 1709 ve üzeri, ortak yönetim için bir önkoşuldur.  

Bu işletim sistemi grubundaki cihazların yüzdesini göstermek için bir grafik bölümünün üzerine gelin.

![İstemci işletim sistemi dağıtım kutucuğu](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status"></a>Ortak yönetim durumu

Kayıt işleminden aşağıdaki durumları içeren cihaz sayısını gösteren bir huni grafiği:
  
- Uygun cihazlar
- Zamanlanan  
- Kayıt başlatıldı  
- Kaydedildi  

![Ortak yönetim durumu (huni) kutucuğu](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Ortak yönetim kayıt durumu

Aşağıdaki kategorilerdeki cihaz durumunun dökümünü gösterir:

- Başarılı, karma Azure AD 'ye katılmış  
- Başarılı, Azure AD 'ye katılmış  
- Kaydetme, karma Azure AD 'ye katılmış  
- Hata, karma Azure AD 'ye katılmış  
- Hata, Azure AD 'ye katılmış  
- Bekleyen Kullanıcı oturumu açma  

    > [!NOTE]
    > Sürüm 1906 ' den başlayarak, bu bekleyen durumdaki cihaz sayısını azaltmak için, yeni bir ortak yönetilen cihaz artık Azure AD *cihaz* belirtecine göre Microsoft Intune hizmetine otomatik olarak kaydeder. Kullanıcının otomatik kayıt işleminin başlaması için cihazda oturum açmasını beklemesi gerekmez. Bu davranışı desteklemek için, cihazın Windows 10, sürüm 1803 veya sonraki bir sürümü çalıştırması gerekir.
    >
    > Cihaz belirteci başarısız olursa, kullanıcı belirteciyle önceki davranışa geri döner. Aşağıdaki girdi için **Comanagementhandler. log dosyasına** bakın: `Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Bu durumdaki cihazların listesine gitmek için kutucukta bir durum seçin.  

![Ortak yönetim kayıt durumu kutucuğu](media/co-management-dashboard/1358980-enrollment-status.png)

### <a name="workload-transition"></a>İş yükü geçişi

Kullanılabilir iş yükleri için Microsoft Intune geçiş yaptığınız cihazların sayısıyla bir çubuk grafik görüntüler.

İş yüklerinin listesi, Configuration Manager sürümüne göre farklılık gösterir. Daha fazla bilgi için bkz. [Intune 'a geçirilebilecek Iş yükleri](workloads.md).

İş yükü için geçiş yapılan cihaz sayısını göstermek için bir grafik bölümünün üzerine gelin.

![İş yükü geçiş çubuğu grafiği](media/co-management-dashboard/Workload-Transition.PNG)

### <a name="enrollment-errors"></a>Kayıt hataları

Bu tablo, cihazlardan kayıt hatalarının bir listesidir. Bu hatalar Windows 'un, çekirdek Windows işletim sisteminin veya Configuration Manager istemcisinin MDM bileşeninden gelebilir.

Yüzlerce olası hata vardır. Aşağıdaki tabloda en yaygın hatalar listelenmektedir.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Hata | Açıklama |
|---------|---------|
| 2147549183 (0x8000FFFF) | MDM kaydı henüz Azure AD 'de yapılandırılmadı, ya da kayıt URL 'SI beklenmiyordu.<br><br>[Windows 10 otomatik kayıt özelliğini etkinleştirme](/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Kullanıcı Lisansı hatalı durum engelliyor kayıt durumunda<br><br>[Kullanıcılara lisans atama](/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Intune 'a otomatik olarak kaydolmaya çalışırken, ancak Azure AD yapılandırması tam olarak uygulanmaz. Bu sorun, kısa bir süre sonra cihaz yeniden denendiğinden geçici olmalıdır. |
| 2149056554 (0x 8018002A)<br>&nbsp; | Kullanıcı işlemi iptal etti<br><br>MDM kaydı çok faktörlü kimlik doğrulaması gerektiriyorsa ve Kullanıcı desteklenen bir ikinci faktörle oturum açmadıysa, Windows, kaydolmak üzere kullanıcıya bir bildirim bildirimi görüntüler. Kullanıcı bildirim bildirimine yanıt vermezse, bu hata oluşur. Bu sorun, Configuration Manager yeniden deneneceği ve kullanıcıya sorulacak şekilde geçici olmalıdır. Kullanıcılar, Windows 'da oturum açtıklarında çok faktörlü kimlik doğrulaması kullanmalıdır. Ayrıca, bu davranışı beklemek için bunları eğitin ve istenirse işlem yapın. |
| 2149056532 (0x80180014)<br>MENROLL_E_DEVICENOTSUPPORTED | Mobil cihaz yönetimi desteklenmez. Cihaz kısıtlamalarını denetleyin. |
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Mobil cihaz yönetimi desteklenmez. Cihaz kısıtlamalarını denetleyin. |
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Sunucu, kullanıcının kimliğini doğrulayamadı<br><br> Kullanıcı için Azure AD belirteci yok. Kullanıcının Azure AD kimlik doğrulaması yapabilmesi için emin olun. |
| 2147942450 (0x 80070032)<br>&nbsp; | MDM otomatik kayıt yalnızca Windows RS3 ve üzeri sürümlerde desteklenir.<br><br>Cihazın ortak yönetim için [En düşük gereksinimleri](overview.md#windows-10) karşıladığından emin olun. |
| 3400073293 | ADAL Kullanıcı bölgesi hesabı yanıtı bilinmiyor<br><br>Azure AD yapılandırmanızı denetleyin ve kullanıcıların kimlik doğrulamasını başarıyla yapıp yapabilmeleri için emin olun. |
| 3399548929 | Kullanıcı oturumu açma gerekiyor<br><br>Bu sorun geçici olmalıdır. Kayıt görevi gerçekleşmeden önce Kullanıcı hızlı bir şekilde oturumu kapattığında oluşur. |
| 3400073236 | ADAL güvenlik belirteci isteği başarısız oldu.<br><br>Azure AD yapılandırmanızı denetleyin ve kullanıcıların kimlik doğrulamasını başarıyla yapıp yapabilmeleri için emin olun. |
| 2149122477 | Genel HTTP sorunu |
| 3400073247 | ADAL ile tümleşik Windows kimlik doğrulaması yalnızca Federal akışta desteklenir<br><br>[Hibrit Azure Active Directory JOIN Uygulamanızı planlayın](/azure/active-directory/devices/hybrid-azuread-join-plan) |
| 3399942148 | Sunucu veya proxy bulunamadı.<br><br>Bu sorun, istemci buluttan iletişim kuramıyorsa geçici olmalıdır. Devam ederse, istemcinin Azure ile tutarlı bir bağlantı olduğundan emin olun. | 
| 2149056532 | Belirli bir platform veya sürüm desteklenmiyor<br><br>Cihazın ortak yönetim için [En düşük gereksinimleri](overview.md#windows-10) karşıladığından emin olun. |
| 2147943568 | Öğe bulunamadı<br><br>Bu sorun geçici olmalıdır. Sorun devam ederse, Microsoft Desteği başvurun. |
| 2192179208 | Bu komutu işlemek için yeterli kullanılabilir bellek kaynağı yok.<br><br>Bu sorun geçici olmalıdır, istemci yeniden denenirse kendisini çözmelidir. |
| 3399614467 | ADAL yetkilendirmesi verme bu onaylama işlemi için başarısız oldu<br><br>Azure AD yapılandırmanızı denetleyin ve kullanıcıların kimlik doğrulamasını başarıyla yapıp yapabilmeleri için emin olun. |
| 2149056517 | Yönetim sunucusundan, DB erişim hatası gibi genel hata<br><br>Bu sorun geçici olmalıdır. Sorun devam ederse, Microsoft Desteği başvurun. |
| 2149134055 | WinHTTP adı çözülmedi<br><br>İstemci hizmetin adını çözümleyemiyor. DNS yapılandırmasını denetleyin. |
| 2149134050 | İnternet zaman aşımı<br><br>Bu sorun, istemci buluttan iletişim kuramıyorsa geçici olmalıdır. Devam ederse, istemcinin Azure ile tutarlı bir bağlantı olduğundan emin olun. |

Daha fazla bilgi için bkz. [MDM kayıt hatası değerleri](/windows/desktop/mdmreg/mdm-registration-constants).

## <a name="deployment-policies"></a>Dağıtım ilkeleri

**İzleme** çalışma alanının **dağıtımlar** düğümünde iki ilke oluşturulur. Bir ilke, pilot grubuna ve bir üretime yöneliktir. Bu ilkeler yalnızca Configuration Manager ilkeyi uyguladığı cihaz sayısını bildirir. Cihazların ortak yönetilebilmesi için bir gereksinim olan Intune 'A kaç cihaz kaydedildiğini düşünmez.

Üretim ilkesi (CoMgmtSettingsProd) **Tüm sistemler** koleksiyonuna yöneliktir. İşletim sistemi türünü ve sürümünü denetleyen bir uygulanabilirlik koşuluna sahiptir. İstemci bir sunucu işletim sistemi veya Windows 10 değilse, ilke uygulanmaz ve hiçbir işlem yapılmaz.

## <a name="wmi-device-data"></a>WMI cihaz verileri

Site sunucusundaki **Root\sms\ Site_ &lt; sitekodu>** ad alanında **SMS_Client_ComanagementState** WMI sınıfını sorgulayın. Ortak yönetim dağıtımınızın durumunu belirlemenize yardımcı olan Configuration Manager ' de özel koleksiyonlar oluşturabilirsiniz. Özel koleksiyonlar oluşturma hakkında daha fazla bilgi için bkz. [koleksiyonları oluşturma](../core/clients/manage/collections/create-collections.md).

WMI sınıfında aşağıdaki alanlar mevcuttur:

- **MachineID**: Configuration Manager istemcisi için benzersiz BIR cihaz kimliği

- **Mdmentopla:** cihazın MDM 'ye kayıtlı olup olmadığını belirtir

- **Yetkili**: cihazın kaydedildiği yetki

- **ComgmtPolicyPresent**: Configuration Manager ortak yönetim ilkesinin istemcide mevcut olup olmadığını belirtir. **Mdmentoplavalue** değeri ise `0` , cihaz istemcide her türlü ortak yönetim ilkesi varsa ortak yönetilmez.

Bir cihaz, **Mdmentoplafield** ve **ComgmtPolicyPresent** alanlarının her ikisi de değerine sahip olduğunda birlikte yönetilir `1` .