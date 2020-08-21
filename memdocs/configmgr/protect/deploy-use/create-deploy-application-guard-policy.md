---
title: Application Guard ilkelerini yönetme
titleSuffix: Configuration Manager
description: Microsoft Defender Application Guard ilkeleri oluşturma ve dağıtma hakkında bilgi edinin
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3fb7559f624afdb16ef228c61331387c163fbd54
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697118"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>Microsoft Defender Application Guard ilkesi oluşturma ve dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*
<!-- 1351960 -->  
Configuration Manager Endpoint Protection 'ı kullanarak [Microsoft Defender Application Guard (Application Guard)](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview) ilkeleri oluşturabilir ve dağıtabilirsiniz. Bu ilkeler, güvenilir olmayan Web sitelerini, işletim sisteminin diğer bölümleri tarafından erişilemeyen güvenli bir yalıtılmış kapsayıcıda açarak kullanıcılarınızı korumanıza yardımcı olur.

## <a name="prerequisites"></a>Ön koşullar

Bir Microsoft Defender Application Guard İlkesi oluşturup dağıtmak için, Windows 10 Fall oluşturucunun güncelleştirmesini (1709) kullanmanız gerekir. İlkeyi dağıttığınız Windows 10 cihazlarının bir [ağ yalıtımı ilkesiyle](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings)yapılandırılması gerekir. Daha fazla bilgi için bkz. [Microsoft Defender Application Guard 'a genel bakış](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>İlke oluşturma ve kullanılabilir ayarlara gözatmaya yönelik

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**' i seçin.
2. **Varlıklar ve uyum** çalışma alanında, **Overview**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**Endpoint Protection genel bakış ' ı seçin.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **Windows Defender Application Guard İlkesi Oluştur**' a tıklayın.
4. [Makaleyi](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard) başvuru olarak kullanarak, kullanılabilir ayarlara gözatıp yapılandırabilmeniz gerekir. Configuration Manager, belirli ilke ayarlarını ayarlamanıza izin verir:
   - [Konak etkileşim ayarları](#bkmk_HIS)
   - [Uygulama davranışı](#bkmk_ABS)
   - [Dosya yönetimi](#bkmk_FM)
5. **Ağ tanımı** sayfasında, kurumsal kimlik ' i belirtin ve kurumsal ağ sınırınızı tanımlayın.

    > [!NOTE]
    > Windows 10 bilgisayarları, istemcide yalnızca bir ağ yalıtımı listesini depolar. İki farklı türde ağ yalıtımı listesi oluşturabilir ve bunları istemciye dağıtabilirsiniz:
    >
    >  - bir Windows Information Protection 'den
    >  - Bunlardan biri Microsoft Defender Application Guard
    >
    > Her iki ilkeyi de dağıtırsanız, bu ağ yalıtımı listelerinin eşleşmesi gerekir. Aynı istemciyle eşleşmeyen listeler dağıtırsanız, dağıtım başarısız olur. Daha fazla bilgi için [Windows Information Protection belgelerine](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)bakın.

6. İşiniz bittiğinde Sihirbazı doldurun ve ilkeyi bir veya daha fazla Windows 10 1709 cihazına dağıtın.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> Konak etkileşim ayarları

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

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> Uygulama davranışı ayarları

Uygulama koruyucusu oturumu içinde uygulama davranışını yapılandırır. Sürüm 1802 ' den Configuration Manager önce, uygulama davranışı ve ana bilgisayar etkileşimi **Ayarlar** sekmesinin altında.

- **İçeriði**
  - Kurumsal siteler, üçüncü taraf eklentiler gibi kurumsal olmayan içerikleri yükleyebilir.
- **Farklı**
  - Kullanıcı tarafından oluşturulan tarayıcı verilerini koruma
  - Yalıtılmış Application Guard oturumunda güvenlik olaylarını denetleme

### <a name="file-management"></a><a name="bkmk_FM"></a> Dosya yönetimi
<!--3555858-->
Configuration Manager sürüm 1906 ' den başlayarak, kullanıcıların normalde Application Guard 'da açık olan dosyalara güvenmesini sağlayan bir ilke ayarı vardır. Başarılı bir şekilde tamamlandıktan sonra dosyalar Application Guard yerine konak cihazında açılır. Application Guard ilkeleri hakkında daha fazla bilgi için bkz. [Microsoft Defender Application Guard ilke ayarlarını yapılandırma](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard).

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

## <a name="known-issues"></a>Bilinen sorunlar

Windows 10, sürüm 2004 çalıştıran cihazlar, Microsoft Defender Application Guard dosya güven ölçütleri için uyumluluk raporlaması 'ndaki sorunları gösterecektir. Bu sorun, bazı alt sınıfların `MDM_WindowsDefenderApplicationGuard_Settings01` Windows 10, sürüm 2004 ' de WMI sınıfından kaldırıldığı için oluşur. Diğer tüm Microsoft Defender Application Guard ayarları uygulanmaya devam eder, yalnızca dosya güven ölçütleri başarısız olur. Şu anda, hatayı atlamak için geçici çözüm yoktur. <!--7099444,5946790-->

## <a name="next-steps"></a>Sonraki adımlar

Microsoft Defender Application Guard hakkında daha fazla bilgi için bkz.
 - [Microsoft Defender Application Guard 'a genel bakış](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).
- [Microsoft Defender Application Guard SSS](/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard).