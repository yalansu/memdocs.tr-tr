---
title: Masaüstü analizi için SSS
titleSuffix: Configuration Manager
description: Masaüstü analizi için sık sorulan sorular.
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 29f063da47dc26789493b2a83ad8e0cfa6885270
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693301"
---
# <a name="desktop-analytics-faq"></a>Desktop Analytics hakkında SSS

## <a name="prerequisites"></a>Önkoşullar

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a>Intune ile yönetilen cihazlarla bulut özellikli çözümlemeler kullanabilir miyim?

Bugün değil, [Öngörüler temelli cihaz yönetimi](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions)hakkında Microsoft Ignite 2019 duyurusuna bakın. Bu planlı çözüm, Cihaz Durumu ve Yükseltme Hazırlığı bir ardıldır.

Masaüstü Analizi iş akışından faydalanabilir müşterilerin büyük çoğunluğu Windows dağıtmak için Configuration Manager kullanır. Intune müşterilerinin analiz verilerinden ek Öngörüler elde eteceğimizi biliyoruz. Ayrıca, içgörüler ile de Öngörüler paylaşma yolları üzerinde çalışıyoruz.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>72 saat içinde ve Portal hala verileri işliyor, ne var?

Masaüstü analizlerini ilk kez ayarlarken, Configuration Manager ve Masaüstü Analizi portalındaki Raporlar, verilerin tamamını hemen göstermez. Hizmetin verileri işlemesi, 2-3 gün sürebilir. 72 saatten fazla olursa ve Portal hala veri işlemeye devam ediyorsa, şu adımları izleyin:

- Etkin cihazların düzgün yapılandırıldığını doğrulamak için, [bağlantı sistem durumu panosunu](monitor-connection-health.md)kullanın. Bu pano gerçek zamanlı olarak güncelleştirme yapmaz.
- Cihazların, masaüstü Analizi hizmetine Tanılama verileri göndermesini sağlayın. Daha fazla bilgi için bkz. [veri paylaşımını etkinleştirme](enable-data-sharing.md).
- Azure AD 'de [Azure AD uygulamaları](troubleshooting.md#bkmk_AzureADApps) sağlayın.
- Son yedi gün içinde kuruluşunuzla ilişkilendirdiğiniz cihazları denetleyin. [Masaüstü Analizi portalında](https://aka.ms/desktopanalytics), **bağlı hizmetler** bölmesine gidin. **Cihazları kaydet**' i seçin ve **son verileri görüntüleyin**

  > [!IMPORTANT]
  > **Son verileri görüntülemek** Için masaüstü Analizi seçeneği kullanım dışıdır. Bu eylem, daha sonraki bir masaüstü Analizi hizmeti sürümünde kaldırılacaktır. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

Cihazlar düzgün yapılandırıldıysa ve çalışma alanınızdaki verileri hala görmüyorsanız, [Microsoft destek 'e başvurun](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="connect-configuration-manager"></a>Configuration Manager’a bağlanma

### <a name="can-i-change-the-target-or-additional-collections"></a>Hedefi veya ek koleksiyonları değiştirebilir miyim?

Evet, aşağıdaki işlemi kullanın:

- Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri** düğümünü seçin. Masaüstü Analizi hizmetinizdeki ilişkili girdinin özelliklerini açın.

- **Masaüstü Analizi bağlantısı** sekmesinde, **hedef koleksiyonu** değiştirin veya ek koleksiyonları yönetin.

> [!IMPORTANT]  
> Configuration Manager, hedef koleksiyondaki cihazları yapılandırmak için bir ayar İlkesi kullanır. Bu ilke, cihazların Microsoft 'a veri göndermesini sağlamak için tanılama verileri ayarlarını içerir. Hedef koleksiyonun değiştirilmesi, artık hedef koleksiyonda olmayan cihazlarda ayarlar ilkesini geri almaz. Cihazların tanılama verilerini göndermeye devam etmesini istemiyorsanız, [cihazları yeniden yapılandırın](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Windows yükseltme

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Windows 'un yükseltebilir ve mimaride değişiklik yapabilir miyim?

Masaüstü analizi, yerinde yükseltmeleri en iyi şekilde destekleyecek şekilde tasarlanmıştır. Yerinde yükseltmeler 32 bitten 64 bitlik mimariye geçişleri desteklemez. Bu senaryodaki bilgisayarları geçirmeniz gerekiyorsa, yenileme senaryosunu kullanın. Bu senaryoda masaüstü Analizi öngörüleri hâlâ değerlidir, ancak yükseltmeye özgü Kılavuzu yoksayabilirsiniz.

Daha fazla bilgi için bkz. [var olan bir bilgisayarı yeni bir Windows sürümü Ile yenileme](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Windows 'U yükseltirken BIOS 'tan UEFı 'ye değişebilir miyim?

Evet. Daha fazla bilgi için bkz. [yerinde yükseltme SıRASıNDA BIOS 'TAN UEFI 'ye dönüştürme](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Masaüstü analizlerini Windows 10 LTSC ile kullanabilir miyim?

Masaüstü analizi, Windows 10 uzun süreli bakım kanalı (LTSC) cihazlarını desteklemez. Daha fazla bilgi için bkz. [hizmet olarak Windows 'a genel bakış](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Masaüstü Analizi portalından verilerin yenilenmesi için gereken süre miktarını azaltabilir miyim?

Masaüstü Analizi portalında iki tür veri bulunur: yönetici verileri ve Tanılama verileri. İsteğe bağlı yönetici verilerini yenilemek için, veri para birimi açılır öğesini açın ve **Değişiklikleri Uygula**' yı seçin. Bu eylem, çalışma alanlarınızdaki bekleyen yönetici değişikliklerinin bir kerelik olarak yenilenmesini hemen tetikler. Değişiklikler yayılır ve 15-60 dakika içinde genel kullanıma sunulmuştur. Zamanlama, çalışma alanınızın boyutuna ve bekleyen değişikliklerin kapsamına bağlıdır. 24 saatlik bir dönemde, en fazla altı kez bir isteğe bağlı veri yenilemesi isteyebilirsiniz.

İsteğe bağlı veri yenileme isteğinde olmasalar bile tüm veriler her gün otomatik olarak güncelleştirilir. Tanılama verilerinin talep üzerine yenilenmesini tetiklemenin bir yolu yoktur. Masaüstü analizinden farklı veri türleri hakkında daha fazla bilgi için bkz. [veri gecikmesi](troubleshooting.md#data-latency).

## <a name="privacy"></a>Gizlilik

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Masaüstü analizi, Microsoft Veri Yönetimi hizmetine doğrudan istemci bağlantısı olmadan kullanılabilir mi?

Hayır, tüm hizmet Windows Tanılama verileri tarafından desteklenir, bu da cihazların bu doğrudan bağlantıya sahip olmasını gerektirir.

### <a name="can-i-choose-the-data-center-location"></a>Veri merkezi konumunu seçebilir miyim?

Azure Log Analytics için: Evet, masaüstü analizlerini ayarlarken ve Log Analytics çalışma alanını oluşturduğunuzda.

Microsoft Veri Yönetimi hizmeti ve Analytics Azure depolaması için: Hayır, bu iki hizmet Birleşik Devletler barındırılır.

### <a name="where-is-my-organizations-data-stored"></a>Kuruluşumun verileri nerede depolanıyor?

Bilgisayarlarınızdaki Windows Tanılama verileri, Birleşik Devletler bulunan Microsoft tarafından yönetilen güvenli veri merkezlerinde şifrelenir, gönderilir ve işlenir. Microsoft, masaüstü analiziyle ilgili verilerin analizini Azure portal masaüstü analizi çözümü aracılığıyla sağlar. Masaüstü Analizi [Log Analytics kullanılabildiği](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all)birçok bölgede desteklenir. Uluslararası bir Azure bölgesi seçerseniz, tanılama verileriniz Birleşik Devletler Microsoft 'un güvenli veri merkezlerine gönderilir ve burada işlenir.

## <a name="existing-windows-analytics-customers"></a>Mevcut Windows Analytics müşterileri

> [!Important]  
> Windows Analytics hizmeti 31 Ocak 2020 itibariyle kullanımdan kaldırıldı.
>
> Daha fazla bilgi için bkz. [KB 4521815: Windows Analytics emekli on 31 ocak 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Güncelleştirme Uyumluluğu masaüstü analiziyle birlikte kullanabilir miyim?

Evet. Azure portal bugün [güncelleştirme uyumluluğu](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) kullanıyorsanız, şimdi ve 2020 Ocak ' den fazla devam edebilirsiniz.

Daha fazla bilgi için bkz. [KB 4521815: Windows Analytics emekli on 31 ocak 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Masaüstü Analizi 'nde kullanılamayan herhangi bir Windows Analytics özelliği var mı?

<!-- 3616924 -->
Evet, aşağıdaki Windows Analytics özellikleri devre dışı bırakıldı veya henüz masaüstü analizinden kullanılamıyor:

#### <a name="general"></a>Genel

- Configuration Manager gerektirmeyen senaryolar için destek. Örneğin, [Intune desteği](#bkmk_intune).
- Herhangi bir geçerli Windows lisansının lisans önkoşulu E3, E5
- Azure AD kiracısı başına birden çok çalışma alanı desteği
- Özel sorgular çalıştırma ve ham çözüm verilerini dışa aktarma özelliği
- Özel raporlar için veri modeli belgeleri

#### <a name="upgrade-readiness"></a>Yükseltme Hazırlığı

- Internet Explorer sitesi bulma verileri
- Office eklentisi öngörüleri (artık [Configuration Manager kullanılabilir](#bkmk_office))
- Geribildirim merkezi öngörüleri

#### <a name="update-compliance"></a>Güncelleştirme Uyumluluğu

- Iş Windows Update için destek
- Teslim Iyileştirme öngörüleri
- Windows 10 uzun süreli bakım kanalı (LTSC) için destek
- Windows Insider raporları
- Windows Defender durumu

> [!Note]
> Masaüstü analizine dahil olmayanlar da dahil olmak üzere tüm mevcut Güncelleştirme Uyumluluğu özellikleri, Azure portal [güncelleştirme uyumluluğu](/windows/deployment/update/update-compliance-get-started) çözümünde kullanılabilir durumda kalır.

#### <a name="device-health"></a>Cihaz Sistem Durumu

- Sürücü durumu
- Uygulama durumu (dağıtım planı dışında)
- Sık sık kilitlenen cihazlar veya sürücü kaynaklı kilitlenmeler
- Windows oturum açma durumu
- Windows Bilgi Koruması
- Windows Server desteği

## <a name="other"></a>Diğer

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a><a name="bkmk_office"></a>Office 365 ProPlus yükseltmelerim için masaüstü analizlerini kullanabilir miyim?

Hayır, masaüstü Analizi Windows 'a odaklanılmıştır. Microsoft, birçok müşteriyle birlikte çalışan yakın işbirliği sürümünde masaüstü analizi geliştirmiştir. Müşteri geri bildirimi, masaüstü analizinin Windows dağıtımlarını güvenle yönetme yeteneğini nasıl geliştirip geliştebilmesidir. Ayrıca, [office 365 ProPlus](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) 'ın Configuration Manager ve Intune 'da Office yönetim araçlarıyla daha yakından tümleştirileceği hakkında bilgi de ister. Microsoft bu alanlara yatırım yapmaya devam ederken masaüstü analizinden Windows senaryolarına odaklanmaya devam etmektedir.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Masaüstü analizi hakkında nasıl geri bildirim sağlayabilirim?

Masaüstü analizi hakkında görüşlerinizi paylaşmak için portalın üst kısmındaki **gülümseme Gönder** simgesini seçin. Microsoft 'un geri bildirimlerinizi daha iyi anlamasına yardımcı olmak için Gönderiminizle birlikte bir ekran görüntüsü ekleyin. Ayrıca, ürün önerilerini gönderebilir ve diğer fikirlerinizi [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805)üzerine getirebilirsiniz.

> [!Note]
> Gülümseme veya UserVoice gönder aracılığıyla özel bilgileri hiçbir şekilde paylaşmayın. Bu tür özel bilgiler, kiracı kimliğinizi veya ticari kimliğinizi içerir. Microsoft, gülümseme Gönder veya UserVoice kanalları aracılığıyla destek sağlamaz. Masaüstü Analizi çalışma alanınız hakkında yardım almak için, bir destek bileti açmak üzere gezinti menüsündeki **Yardım ve destek** bağlantısını seçin.
