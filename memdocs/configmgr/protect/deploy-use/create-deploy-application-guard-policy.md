---
title: Application Guard ilkelerini yönetme
titleSuffix: Configuration Manager
description: Windows Defender Application Guard ilkeleri oluşturma ve dağıtma hakkında bilgi edinin
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 241e7ed9a2195e178cc1aac2ee2a146eea60b093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721748"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Windows Defender Application Guard ilkesi oluşturma ve dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*
<!-- 1351960 -->  
Configuration Manager Endpoint Protection 'ı kullanarak [Windows Defender Application Guard (Application Guard)](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) ilkeleri oluşturabilir ve dağıtabilirsiniz. Bu ilkeler, güvenilir olmayan Web sitelerini, işletim sisteminin diğer bölümleri tarafından erişilemeyen güvenli bir yalıtılmış kapsayıcıda açarak kullanıcılarınızı korumanıza yardımcı olur.

## <a name="prerequisites"></a>Önkoşullar

Windows Defender Application Guard İlkesi oluşturup dağıtmak için Windows 10 Fall oluşturucunun (1709) güncelleştirmesini kullanmanız gerekir. İlkeyi dağıttığınız Windows 10 cihazlarının bir ağ yalıtımı ilkesiyle yapılandırılması gerekir. Daha fazla bilgi için bkz. [Windows Defender Application Guard 'a genel bakış](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>İlke oluşturma ve kullanılabilir ayarlara gözatmaya yönelik

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**' i seçin.
2. **Varlıklar ve uyum** çalışma alanında,**Windows Defender Application Guard****Endpoint Protection** >  **genel bakış** > ' ı seçin.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **Windows Defender Application Guard İlkesi Oluştur**' a tıklayın.
4. [Makaleyi](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) başvuru olarak kullanarak, kullanılabilir ayarlara gözatıp yapılandırabilmeniz gerekir. Configuration Manager, belirli ilke ayarlarını ayarlamanıza izin verir:
   - [Konak etkileşim ayarları](#bkmk_HIS)
   - [Uygulama davranışı](#bkmk_ABS)
   - [Dosya yönetimi](#bkmk_FM)
5. **Ağ tanımı** sayfasında, kurumsal kimlik ' i belirtin ve kurumsal ağ sınırınızı tanımlayın.

    > [!NOTE]
    > Windows 10 bilgisayarları, istemcide yalnızca bir ağ yalıtımı listesini depolar. İki farklı türde ağ yalıtımı listesi oluşturabilir ve bunları istemciye dağıtabilirsiniz:
    >
    >  - bir Windows Information Protection 'den
    >  - bir Windows Defender Application Guard 'dan
    >
    > Her iki ilkeyi de dağıtırsanız, bu ağ yalıtımı listelerinin eşleşmesi gerekir. Aynı istemciyle eşleşmeyen listeler dağıtırsanız, dağıtım başarısız olur. Daha fazla bilgi için [Windows Information Protection belgelerine](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)bakın.

6. İşiniz bittiğinde Sihirbazı doldurun ve ilkeyi bir veya daha fazla Windows 10 1709 cihazına dağıtın.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a>Konak etkileşim ayarları

Konak cihazlar ve Application Guard kapsayıcısı arasındaki etkileşimleri yapılandırır. Sürüm 1802 ' den Configuration Manager önce, uygulama davranışı ve ana bilgisayar etkileşimi **Ayarlar** sekmesinin altında.

- **Pano** -Configuration Manager 1802 ' dan önceki ayarlar altında
  - İzin verilen içerik türü
    - Metin
    - Görüntüler
- **Yazdırma**
  - XPS 'ye yazdırmayı etkinleştir
  - PDF 'ye yazdırmayı etkinleştir
  - Yerel yazıcılara yazdırmayı etkinleştir
  - Ağ yazıcılarına yazdırmayı etkinleştir
- **Grafikler:** (Configuration Manager sürüm 1802 ' den başlayarak)
  - Sanal grafik işlemci erişimi
- **Dosyalar:** (Configuration Manager sürüm 1802 ' den başlayarak)
  - İndirilen dosyaları konağa Kaydet

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a>Uygulama davranışı ayarları

Uygulama koruyucusu oturumu içinde uygulama davranışını yapılandırır. Sürüm 1802 ' den Configuration Manager önce, uygulama davranışı ve ana bilgisayar etkileşimi **Ayarlar** sekmesinin altında.

- **İçeriði**
  - Kurumsal siteler, üçüncü taraf eklentiler gibi kurumsal olmayan içerikleri yükleyebilir.
- **Farklı**
  - Kullanıcı tarafından oluşturulan tarayıcı verilerini koruma
  - Yalıtılmış Application Guard oturumunda güvenlik olaylarını denetleme

### <a name="file-management"></a><a name="bkmk_FM"></a>Dosya yönetimi
<!--3555858-->
Configuration Manager sürüm 1906 ' den başlayarak, kullanıcıların normalde Application Guard 'da açık olan dosyalara güvenmesini sağlayan bir ilke ayarı vardır. Başarılı bir şekilde tamamlandıktan sonra dosyalar Application Guard yerine konak cihazında açılır. Application Guard ilkeleri hakkında daha fazla bilgi için bkz. [Windows Defender Application Guard ilke ayarlarını yapılandırma](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard).

- **Kullanıcıların Windows Defender Application Guard 'da açılan dosyalara güvenmesine Izin ver** -kullanıcının dosyaları güvenilir olarak işaretlemesini etkinleştirin. Bir dosya güvenilir olduğunda, uygulama koruyucusu yerine konakta açılır. Windows 10 sürüm 1809 veya üzeri istemciler için geçerlidir.
  - **Yasaklanmış:** Kullanıcıların dosyaları güvenilir (varsayılan) olarak işaretlemesini izin verme.
  - **Virüsten koruma tarafından denetlenen dosya:** Virüsten koruma denetiminden sonra kullanıcıların dosyaları güvenilir olarak işaretlemesini sağlar.
  - **Tüm dosyalar:** Kullanıcıların herhangi bir dosyayı güvenilir olarak işaretlememesini sağlar.

Dosya yönetimini etkinleştirdiğinizde, istemcinin DCMReporting. log dosyasına kaydedilen hataları görebilirsiniz. Aşağıdaki hatalar genellikle etkisizdir. <!--4619457-->

- Uyumlu cihazlarda:
  - FileTrustCriteria_condition bulunamadı
- Uyumlu olmayan cihazlarda:
  - FileTrustCriteria_condition bulunamadı
  - FileTrustCriteria_condition haritada bulunamadı
  - FileTrustCriteria_condition Özet içinde bulunamadı

Application Guard ayarlarını düzenlemek için **varlıklar ve uyum** çalışma alanındaki **Endpoint Protection** ' ı genişletin ve ardından **Windows Defender Application Guard** düğümüne tıklayın. Düzenlemek istediğiniz ilkeye sağ tıklayıp **Özellikler**' i seçin.

## <a name="next-steps"></a>Sonraki adımlar

Windows Defender Application Guard hakkında daha fazla bilgi için: [Windows Defender Application Guard 'A genel bakış](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Windows Defender Application Guard SSS](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).
