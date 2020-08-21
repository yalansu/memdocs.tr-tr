---
title: Kullanım dışı bırakılan özellikler
titleSuffix: Configuration Manager
description: Configuration Manager artık desteklemediği özellikler hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 29b5dd8fdceb803de77aff9adbd0614d1e201b18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694278"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Configuration Manager için kaldırılan ve kullanım dışı bırakılan özellikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, kullanım dışı bırakılan veya Configuration Manager desteğinden kaldırılan özellikler listelenir. Kullanım dışı bırakılan özellikler gelecekteki bir güncelleştirmede kaldırılacaktır. Bu gelecekteki değişiklikler Configuration Manager kullanımını etkileyebilir.  

Bu bilgiler gelecek sürümlerde değiştirilebilir. Kullanım dışı bırakılmış her Configuration Manager özelliğini içermeyebilir.

## <a name="deprecated-features"></a>Kullanım dışı bırakılan özellikler

Aşağıdaki özellikler kullanım dışıdır. Artık bunları kullanmaya devam edebilirsiniz, ancak Microsoft bu desteği daha sonra bitirmek için planlar.

|Özellik|İlk duyurulan kullanımdan kaldırma|Destek &nbsp; kaldırıldı|
|-----------|---|--------------|
|Azure 'dan içerik paylaşmaya yönelik uygulama değişti. İçerik etkinleştirilmiş bir bulut yönetimi ağ geçidi kullanın. Gelecekte geleneksel bir bulut dağıtım noktası oluşturamayacak.|Şubat 2019|TBD<sup>[Note 1](#bkmk_note1)</sup>|
|Bulut yönetimi ağ geçidi ve bulut dağıtım noktası için Azure 'a klasik hizmet dağıtımı. Daha fazla bilgi için [plan for CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)konusuna bakın.|Kasım 2018|TBD<sup>[Note 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> Note 1: destek TBD

Belirli bir zaman çerçevesi belirlenir (TBD). Microsoft, yeni süreç veya özelliğe değiştirmenizi önerir, ancak yakın bir işlem için kullanım dışı olan işlemleri veya özelliği kullanmaya devam edebilirsiniz.

## <a name="unsupported-and-removed-features"></a>Desteklenmeyen ve kaldırılan özellikler

Aşağıdaki özellikler artık desteklenmiyor. Bazı durumlarda, bunlar üründe artık yoktur.

|Özellik|İlk duyurulan kullanımdan kaldırma|Destek &nbsp; kaldırıldı|  
|-----------|---|--------------|  
| Cihaz kaydı ve güvenlik güncelleştirmeleri için **son verileri görüntülemek** üzere masaüstü Analizi seçeneği.<!-- 7080949 --> Daha fazla bilgi için bkz. [veri gecikmesi](../../../../desktop-analytics/troubleshooting.md#data-latency).|Mayıs 2020|Temmuz 2020|
| Windows Analytics ve Yükseltme Hazırlığı tümleştirme. Daha fazla bilgi için bkz. [KB 4521815: Windows Analytics emekli on 31 ocak 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | 14 Ekim 2019 | 31 Ocak 2020 |
| Koşullu erişim uyumluluk ilkeleri için cihaz sistem durumu kanıtlama değerlendirmesi <!--1235616 aka 3608202--> Daha fazla bilgi için bkz. [karma MDM 'ye ne oldu](../../../../mdm/understand/what-happened-to-hybrid.md).| 3 Temmuz 2019 | Sürüm 1910 |
| Configuration Manager Şirket Portalı uygulaması | 21 Mayıs 2019 | Sürüm 1910 |
| Uygulama Kataloğu, her iki site sistem rolü de dahil: Uygulama Kataloğu web sitesi noktası ve Web hizmet noktası. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | 21 Mayıs 2019 | Sürüm 1910 |
|Configuration Manager 'de Iş için Windows Hello ayarları ile sertifika tabanlı kimlik doğrulaması<br>Daha fazla bilgi için bkz. [iş Için Windows Hello ayarları](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|Aralık 2017|Sürüm 1910|
|Mac ve Linux için System Center Endpoint Protection<br>Daha fazla bilgi için bkz. [Destek Web günlüğü gönderisinin sonu](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).|Ekim 2018|31 Aralık 2018|
|Şirket içi koşullu erişim<br>Daha fazla bilgi için bkz. [karma MDM 'ye ne oldu](../../../../mdm/understand/what-happened-to-hybrid.md).|30 Ocak 2019|1 Eylül 2019|
|Karma mobil cihaz yönetimi (MDM)<br>Daha fazla bilgi için bkz. [karma MDM 'ye ne oldu](../../../../mdm/understand/what-happened-to-hybrid.md).<br><br>1902 Intune hizmet sürümünden itibaren, 2019 Şubat sonunda, yeni müşteriler yeni bir karma bağlantı oluşturamaz.<!--Intune feature 2683117-->|14 Ağustos 2018|1 Eylül 2019|
|Güvenlik Içeriği Otomasyon Protokolü (SCAP) uzantıları. <!--3607889--><br>Önceki sertifikalı sürüm, [Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=48741)' nde hala kullanılabilir.|Eylül 2018|Sürüm 1810|
|Uygulama Kataloğu web sitesi noktası için **Silverlight Kullanıcı deneyimi** artık desteklenmiyor. Kullanıcıların yeni yazılım merkezini kullanması gerekir. Daha fazla bilgi için bkz. [Software Center 'ı yapılandırma](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|11 Ağustos 2017| Sürüm 1806|
|Yazılım Merkezi 'nin önceki sürümü.<br><br>Yeni Yazılım Merkezi hakkında daha fazla bilgi için bkz. [uygulama yönetimini planlayın ve yapılandırın](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex).|13 Aralık 2016|Sürüm 1802|
|Configuration Manager ile sanal sabit disklerin (VHD) yönetimi. <br><br>Bu kullanımdan kaldırma, yeni bir VHD oluşturma veya bir görev dizisi kullanarak bir VHD 'yi yönetme veya Configuration Manager konsolundan sanal sabit diskler düğümünün kaldırılması seçeneklerini içerir. <br><br>Mevcut VHD 'ler silinmez, ancak artık Configuration Manager konsolu içinden erişilemez.  |6 Ocak 2017 |Sürüm 1710|
|Görev dizileri: <br /> -Diski dinamik diske Dönüştür <br /> -Dağıtım araçları 'nı yükler |18 Kasım 2016|Sürüm 1710|
|Yükseltme değerlendirme aracı<br><br>Yükseltme değerlendirme aracı hem Configuration Manager hem de uygulama uyumluluk araç seti 'ne (sahne) 6. x öğesine bağlıdır. SAHNE 'nin son sürümü Windows 10 v1511 ADK 'de gönderilmiştir. Işlem yapmak için daha fazla güncelleştirme olmadığından, yükseltme değerlendirmesi aracı için destek kullanımdan kaldırılmıştır. 12 Eylül 2016 ' de [UIAT için indirme sayfasına](https://www.microsoft.com/software-download/windows10) kullanımdan kaldırma bildirimi eklendi. | 12 Eylül 2016  | 11 Temmuz 2017 |
|Ağ Yükü Dengeleme (NLB) kümesiyle yazılım güncelleştirme noktaları | 27 Şubat 2016 | Sürüm 1702 |
|Görev dizileri: <br /> -OSDPreserveDriveLetter  <br /><br /> Bir işletim sistemi dağıtımı sırasında, varsayılan olarak Windows Kurulumu artık kullanılacak en iyi sürücü harfini (genellikle C:) ' i belirler. Kullanmak için farklı bir sürücü belirtmek istiyorsanız, Işletim sistemini Uygula görev dizisi adımında konumu değiştirebilirsiniz. **Bu işletim sistemi ayarını uygulamak istediğiniz konumu seçin** bölümüne gidin. **Belirli bir mantıksal sürücü harfi** seçin ve kullanmak istediğiniz sürücüyü seçin. |20 Haziran 2016 |Sürüm 1606 |
|Ağ Erişim Koruması (NAP)-System Center 2012 ' de bulunur Configuration Manager|10 Temmuz 2015|Sürüm 1511|  
|Bant dışı yönetim-System Center 2012 ' de bulundu Configuration Manager|16 Ekim 2015|Sürüm 1511|

### <a name="features-removed-in-version-1511"></a>Sürüm 1511 ' de kaldırılan özellikler

Aşağıdaki bölümlerde sürüm 1511 ile kaldırılan özellikler için ek ayrıntılar yer alır:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> Bant dışı yönetim  

Configuration Manager, Configuration Manager konsolunun içinden AMT tabanlı bilgisayarlar için yerel destek kaldırılmıştır.  

- [Configuration Manager Için ıNTEL SCS eklentisini](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)kullandığınızda AMT tabanlı bilgisayarlar tam olarak yönetilmeye devam eder. Eklenti, AMT 'yi yönetmek için en son yeteneklere erişmenizi sağlar. bu değişiklikler, Configuration Manager bu değişiklikleri birleştirebilene kadar sunulan sınırlamaları ortadan kaldırır.  

- System Center 2012 Configuration Manager bant dışı yönetim bu değişiklikten etkilenmez.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> Ağ erişim koruması

Configuration Manager ağ erişim koruması desteğini kaldırdı. Özellik Windows Server 2012 R2 'de kullanımdan kaldırılmıştır ve Windows 10 ' dan kaldırılmıştır.  

Ağ erişimi koruması alternatifleri için [Ağ İlkesi ve Erişim Hizmetlerine Genel Bakış](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)) konusundaki *Devre dışı bırakılan işlevsellik* bölümüne bakın.

## <a name="see-also"></a>Ayrıca bkz.

- [Kaldırılan ve kullanım dışı bırakılan](removed-and-deprecated.md)
- [Microsoft Desteği yaşam döngüsü](https://support.microsoft.com/lifecycle)
- [Configuration Manager güncel dal sürümleri için destek](../../../servers/manage/current-branch-versions-supported.md)