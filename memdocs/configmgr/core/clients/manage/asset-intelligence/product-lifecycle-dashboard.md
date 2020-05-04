---
title: Ürün yaşam döngüsü panosu
titleSuffix: Configuration Manager
description: Configuration Manager 'de ürün yaşam döngüsü panosundan Microsoft yaşam döngüsü Ilkesini görüntüleyin.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714244"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Microsoft yaşam döngüsü Ilkesini Configuration Manager yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sürüm 1806 ' den başlayarak, Microsoft yaşam döngüsü Ilkesini görüntülemek için Configuration Manager ürün yaşam döngüsü panosunu kullanabilirsiniz. Pano, Configuration Manager ile yönetilen cihazlarda yüklü Microsoft ürünleri için Microsoft yaşam döngüsü Ilkesinin durumunu gösterir. Ayrıca ortamınızdaki Microsoft ürünleriyle ilgili bilgiler, desteklenebilirlik State ve bitiş tarihlerini DESTEKDE sağlar. Her ürün için desteğin kullanılabilirliğini anlamak için panoyu kullanın. Bu bilgiler, geçerli destek sonuna ulaşılmadan önce kullandığınız Microsoft ürünlerini ne zaman güncelleştirebileceğini planlamanızı sağlar.  

Daha fazla bilgi için bkz. [Microsoft yaşam döngüsü ilkesi](https://support.microsoft.com/lifecycle).

Sürüm 1810 ' den başlayarak Pano, System Center 2012 Configuration Manager ve üzeri bilgilerini içerir.<!--1358702-->  



## <a name="prerequisites"></a>Önkoşullar 

 Ürün yaşam döngüsü panosundaki verileri görmek için aşağıdaki bileşenler gereklidir:  

- Configuration Manager konsolunu çalıştıran bilgisayarda Internet Explorer 9 veya üzeri bir sürümü yüklü olmalıdır.  

- Hizmet bağlantı noktası rolü yüklenmiş ve yapılandırılmış olmalıdır. Bu panodaki verilere yönelik güncelleştirmeleri almak için hizmet bağlantı noktasının çevrimiçi olması veya çevrimdışı olması durumunda düzenli olarak eşitlenmesi gerekir. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../../../servers/deploy/configure/about-the-service-connection-point.md).

- Panodaki köprü işlevselliği için bir raporlama hizmetleri noktası gereklidir. Pano SQL Server Reporting Services (SSRS) raporlarına bağlantı sağlar. Daha fazla bilgi için bkz. [raporlamaya giriş](../../../servers/manage/introduction-to-reporting.md).  

- Varlık yönetim bilgileri eşitleme noktası yapılandırılmalı ve eşitlenmelidir. Pano, varlık yönetim bilgileri kataloğunu ürün başlıkları için meta veriler olarak kullanır. Meta veriler hiyerarşinizdeki envanter verileriyle karşılaştırılır. Daha fazla bilgi için [Configuration Manager varlık yönetim bilgilerini yapılandırma](configuring-asset-intelligence.md)konusuna bakın.  
  - Varlık yönetim bilgileri hizmet noktasını ilk kez yapılandırıyorsanız [varlık yönetim bilgileri donanım envanteri sınıflarını](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)etkinleştirdiğinizden emin olun. Yaşam döngüsü panosu, bu varlık yönetim bilgileri donanım envanteri sınıflarına bağlıdır. Pano, istemcileri için taranana ve donanım envanteri döndürdüğü sürece verileri göstermez.  
  - Bu panodaki genişletilmiş güvenlik güncelleştirmeleri (ESU) hakkındaki bilgileri görüntülemek için donanım envanteri sınıfı **yazılım lisanslama ürününü varlık yönetim bilgileri (SoftwareLicensingProduct)** etkinleştirin. Daha fazla bilgi için bkz. [varlık yönetim bilgileri donanım envanteri sınıflarını etkinleştirme](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Ürün yaşam döngüsü panosunu kullanma

Site Yönetilen cihazlardan toplanan envanter verilerine bağlı olarak, Pano tüm geçerli ürünlerle ilgili bilgileri görüntüler. Ancak, işletim sistemleri ve SQL Server için görünen bilgiler aşağıdaki sürümlerle sınırlıdır:

- Windows Server 2008 ve üzeri
- Windows XP ve üzeri
- SQL Server 2008 ve üzeri

Configuration Manager konsolundaki yaşam döngüsü panosuna erişmek için **varlıklar ve uyum** çalışma alanına gidin, **varlık yönetim bilgileri**' i genişletin ve **ürün yaşam döngüsü** düğümünü seçin.

> [!NOTE]  
> Panodaki veriler Configuration Manager konsolunun bağlandığı siteyi temel alır. Konsol üst katman sitenize bağlanırsa, tüm hiyerarşinin verilerini görürsünüz. Bir alt birincil siteye bağlanıldığında yalnızca o sitedeki veriler görüntülenir.

### <a name="product-lifecycle-dashboard"></a>Ürün yaşam döngüsü panosu

![Konsolundaki ürün yaşam döngüsü panosunun ekran görüntüsü](media/product-lifecycle-dashboard.png)

**Ürün kategorisi** listesinden aşağıdaki seçeneklerden birini seçerek görünümü değiştirin:  
- **Tümü**: tüm ürünleri birlikte görüntüleyin  
- **Windows istemcisi**: Windows istemci işletim sistemi sürümlerini görüntüle  
- **Windows Server**: Windows Server işletim sistemi sürümlerini görüntüleme  
- **Veritabanı**: SQL Server sürümlerini görüntüle  
- **Configuration Manager**: sürüm 1810 ' den başlayarak Configuration Manager sürümlerini görüntüleyin 
- **Microsoft Office**: sürüm 1902 ' den başlayarak Office 2003 ' nin yüklü sürümlerine yönelik bilgileri Office 2016 ile görüntüleyin <!--3556026-->

Pano aşağıdaki kutucuklara sahiptir:  

- Son **kullanım ömrü geçmiş ilk beş ürün**: bu kutucuk, ortamınızda bulunan ürünlerin son kullanım ömrünü aşan birleştirilmiş bir veri görünümüdür. Graph, işletim sistemleri ve SQL Server ürünleri için destek yaşam döngüsüne kıyasla süresi geçen yüklü yazılımları gösterir.  

- **Hayata geç en son beş ürün**: bu kutucuk, ortamınızda bulunan ve sonraki 18 ay içinde yaşam süresi yaklaşan ürünlerin birleştirilmiş bir veri görünümüdür. Grafik, işletim sistemleri ve SQL Server ürünleri için destek yaşam döngüsüne kıyasla 18 aylık son kullanım süresi içinde yüklü yazılımları gösterir.  

- **Yüklü ürünler Için yaşam döngüsü verileri**: bu kutucuk, bir ürün geçişlerinin süresi dolma süresi dolduğunda oluşan genel bir fikir sunar. Grafik, ürünün yüklendiği istemci sayısının, destek kullanılabilirliği durumunun ve izlenecek sonraki adımlar hakkında daha fazla bilgi edinmek için bir bağlantının dökümünü sağlar. Aşağıdaki bilgiler grafiğe dahildir:     
    - Kalan destek süresi
    - Ortamdaki sayı 
    - Temel destek bitiş tarihi
    - Genişletilmiş Destek bitiş tarihi
    - Sonraki adımlar  

> [!IMPORTANT]  
> Bu panoda gösterilen bilgiler kolaylık sağlaması için sağlanır ve yalnızca şirket içinde dahili olarak kullanılabilir. Uyumluluğu doğrulamak için bu bilgilere yalnızca güvenmemelisiniz. [Microsoft yaşam döngüsü ilkesini](https://support.microsoft.com/lifecycle)ziyaret ederek destek bilgilerinin kullanılabilirliğiyle birlikte size sunulan bilgilerin doğruluğunu doğruladığınızdan emin olun.  



## <a name="reporting"></a>Raporlama

Ek raporlar da kullanılabilir. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar**' ı genişletin. Aşağıdaki yeni raporlar **varlık yönetim bilgileri**kategorisi altına eklenir:  

- **Yaşam döngüsü 01A-belirli bir yazılım ürünü olan bilgisayarlar**: belirtilen bir ürünün algılandığı bilgisayarların listesini görüntüleyin.  

- **Yaşam döngüsü 02A-kuruluştaki süresi geçen bir ürüne sahip olan makinelerin listesi**: süresi dolmamış ürünleri olan bilgisayarları görüntüleyin. Bu raporu ürün adına göre filtreleyebilirsiniz.

- **Yaşam döngüsü 03A-kuruluşta bulunan süresi biten ürünlerin listesi**: ortamınızda süresi geçen yaşam döngüsü tarihleri olan ürünlerin ayrıntılarını görüntüleyin.  

- **Yaşam döngüsü 04A-genel ürün yaşam döngüsüne genel bakış**: ürün yaşam döngüsünün listesini görüntüleyin. Listeyi ürün adına ve günlere göre zaman aşımına göre filtreleyin.  

- **Yaşam döngüsü 05A-ürün yaşam döngüsü panosu**: sürüm 1810 ' den başlayarak bu rapor, konsol içi pano olarak benzer bilgiler içerir. Ortamınızdaki ürünlerin sayısını ve kalan destek günlerini görüntülemek için bir kategori seçin.  

Daha fazla bilgi için bkz. [rapor listesi](../../../servers/manage/list-of-reports.md#asset-intelligence).<!--SCCMDocs issue 997-->  
