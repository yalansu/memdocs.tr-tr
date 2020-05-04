---
title: Hiyerarşi bakım aracı
titleSuffix: Configuration Manager
description: Hiyerarşi bakım aracının ne yaptığını ve bunu nasıl kullanabileceğini anlayın. Komut satırı seçenekleri başvurusunu içerir.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712445"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Configuration Manager için hiyerarşi bakım aracı (Preinst. exe)

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hiyerarşi Bakımı Aracı (Preinst. exe), hiyerarşi Yöneticisi hizmeti çalışırken komutları Configuration Manager hiyerarşi yöneticisine geçirir. Hiyerarşi Bakımı Aracı, bir Configuration Manager sitesi yüklediğinizde otomatik olarak yüklenir. Preinst \\ &lt;. exe dosyasını site sunucusundaki *SiteServerName*> \ SMS_&lt;*sitekodu*\x64\00000409 paylaşılan klasöründe bulabilirsiniz.  

 Hiyerarşi Bakımı aracını aşağıdaki senaryolarda kullanabilirsiniz:  

-   Güvenli anahtar değişimi gerektiğinde, siteler arasındaki ilk ortak anahtar değişimini elle gerçekleştirmeniz gerektiği durumlar vardır. Daha fazla bilgi için bu konuda [Ortak Anahtarları Siteler Arasında Elle Değiştirme](#BKMK_ManuallyExchangeKeys) bölümüne bakın.  

-   Artık kullanılamayan bir hedef siteye yönelik olan aktif işleri kaldırmak için.  

-   Kurulumu kullanarak siteyi kaldıramıyorsanız Configuration Manager konsolundan bir site sunucusunu silmek için. Örneğin, siteyi kaldırmak için öncelikle kurulum 'U çalıştırmadan bir Configuration Manager sitesini fiziksel olarak kaldırırsanız site bilgileri üst sitenin veritabanında olmaya devam eder ve üst site alt siteyle iletişim kurmayı denemeye devam eder. Bu sorunu çözmek için Hiyerarşi Bakımı aracını çalıştırmanız ve alt siteyi üst sitenin veritabanından elle silmeniz gerekir.  

-   Hizmetleri tek tek durdurmak zorunda kalmadan bir sitedeki tüm Configuration Manager hizmetlerini durdurmak için.  

-   Bir siteyi kurtarırken birden çok alt siteye ait ortak anahtarları kurtarılan siteye dağıtmak için CHILDKEYS seçeneğini kullanabilirsiniz.  

Hiyerarşi Bakımı aracını çalıştırmak için geçerli kullanıcının yerel bilgisayarda yönetici ayrıcalıkları olmalıdır. Ayrıca, kullanıcıya açık olarak Site - Yönetme güvenlik hakkı verilmiş olmalıdır; kullanıcının bu izne sahip bir grubun üyesi olma yoluyla bu hakkı devralması yeterli değildir.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Hiyerarşi Bakımı Aracı Komut Satırı Seçenekleri  
Hiyerarşi Bakımı Aracını kullanırken onu merkezi yönetim sitesinde, birincil sitede veya ikincil site sunucusunda yerel olarak çalıştırmalısınız.  

Hiyerarşi Bakımı aracını çalıştırdığınızda şu sözdizimini kullanmanız gerekir: Preinst. exe/&lt;seçeneği.\> Aşağıdakiler komut satırı seçenekleridir.  

 **/Deljob &lt; *sitekodu* > ** -geçerli siteden belirtilen hedef siteye olan tüm işleri veya komutları silmek için bir sitede bu seçeneği kullanın.  

 **/DELSITE &lt; *ChildSiteCodeToRemove* > ** -alt siteler için verileri üst sitenin site veritabanından silmek için bir üst sitede bu seçeneği kullanın. Genellikle, site bir site sunucusu bilgisayarından kaldırılmadan önce o bilgisayar kullanımdan alındığında bu seçenek kullanılır.  

> [!NOTE]  
>  /DELSITE seçeneği, ChildSiteCodeToRemove parametresi ile belirtilen bilgisayardaki siteyi kaldırmaz. Bu seçenek yalnızca Configuration Manager site veritabanından site bilgilerini kaldırır.  

**/Dump &lt; *sitekodu* > ** -site denetim görüntülerini sitenin yüklendiği sürücünün kök klasörüne yazmak için yerel site sunucusunda bu seçeneği kullanın. Belirli bir site denetim görüntüsünü klasöre yazabilir veya hiyerarşideki tüm site denetim dosyalarını yazabilirsiniz.  

-   /Dump &lt; *sitekodu*> site denetim görüntüsünü yalnızca belirtilen site için yazar.  

-   /DUMP tüm sitelerin site denetim dosyalarını yazar.  

Görüntü, site denetim dosyasının Configuration Manager sitesi veritabanında depolanan ikili gösterimidir. Dökümü alınan site denetim dosyası görüntüsü, bekleyen fark görüntülerine ek olarak temel görüntünün toplamıdır.  

Hiyerarşi bakım aracı ile bir site denetim dosyası görüntüsünü dökümünü aldıktan sonra dosya adı sitectrl_&lt;*sitekodu*>. CT0 biçimindedir biçimindedir.  

**/STOPSITE** -siteyi kısmen sıfırlayan Configuration Manager site Bileşen Yöneticisi hizmetine yönelik bir kapalı döngüsünü başlatmak için yerel site sunucusunda bu seçeneği kullanın. Bu oturum açma işlemi çalıştırıldığında, site sunucusu ve uzak site sistemleri üzerinde bazı Configuration Manager hizmetleri durdurulur. Bu hizmetler yeniden yüklenmek üzere işaretlenir. Bu kapatma döngüsünün sonucu olarak, hizmetler yeniden yüklendiğinde bazı parolalar otomatik olarak değiştirilir.  

> [!NOTE]  
>  Site Bileşen Yöneticisinin kapatma, yeniden yükleme ve parola değişiklikleri kaydını görmek istiyorsanız bu komut satırı seçeneğini kullanmadan önce bu bileşenin günlüğünü etkinleştirin.  

Kapatma döngüsü başlatıldıktan sonra, yanıt vermeyen tüm bileşenleri veya bilgisayarları atlayarak otomatik olarak ilerler. Bununla birlikte, Site Bileşen Yöneticisi hizmeti kapatma döngüsü sırasında uzak site sistemine erişemiyorsa Site Bileşen Yöneticisi hizmeti yeniden başlatıldığında uzak site sisteminde yüklü olan bileşenler yeniden yüklenir. Site Bileşen Yöneticisi hizmeti yeniden başlatıldığında, yeniden başlatılması işaretlenmiş tüm hizmetleri yeniden yüklemeyi başarılı olana dek üst üste dener.  

Hizmet Yöneticisi'ni kullanarak Site Bileşen Yöneticisi hizmetini yeniden başlatabilirsiniz. Hizmet yeniden başlatıldıktan sonra, etkilenen tüm hizmetler kaldırılır, yeniden yüklenir ve yeniden başlatılır. Kapatma döngüsü başlatmak için /STOPSITE seçeneğini kullandıktan ve Site Bileşen Yöneticisi hizmeti yeniden başlatıldıktan sonra, yeniden yükleme döngülerinden kaçınamazsınız.  

**/KEYFORPARENT** - Bir sitenin ortak anahtarını üst bir siteye dağıtmak için sitede bu seçeneği kullanın.  

/Keyforparent seçeneği, sitenin &lt; *sitekodu*> dosyasına ortak anahtarını koyar. CT4, Program Files sürücüsünün kökünde. Preinst. exe dosyasını bu seçenekle çalıştırdıktan sonra, &lt; *sitekodu*> el ile kopyalayın. CT4 dosyasını üst sitenin. ..\ınboxes\hmanman Box klasörüne (HMAN. box\pubkey değil).  

**/KEYFORCHILD** - Bir sitenin ortak anahtarını bir alt siteye dağıtmak için sitede bu seçeneği kullanın.  

/Keyforchild seçeneği, sitenin &lt; *sitekodu*> dosyasına ortak anahtarını koyar. CT5, Program Files sürücüsünün kökünde. Preinst. exe dosyasını bu seçenekle çalıştırdıktan sonra, &lt; *sitekodu*> el ile kopyalayın. CT5 dosyasını alt sitenin. ..\ınboxes\hmanman Box klasörüne (HMAN. box\pubkey değil).  

**/CHILDKEYS** - Bu seçeneği kurtarmakta olduğunuz bir sitenin alt sitelerinde kullanabilirsiniz. Birden çok alt sitedeki ortak anahtarları kurtarılan siteye dağıtmak için bu seçeneği kullanın.  

/Childkeys seçeneği, seçeneğini çalıştırdığınız siteden anahtarı ve bu sitelerin alt siteleri ortak anahtarlarını &lt; *sitekodu*> dosyasına koyar. CT6.  

Preinst. exe dosyasını bu seçenekle çalıştırdıktan sonra, &lt; *sitekodu*> el ile kopyalayın. CT6 dosyasını kurtarılan sitenin. ..\Inboxes\hman.exe klasörüne (HMAN. box\pubkey değil) kopyalayın.  

**/PARENTKEYS** - Bu seçeneği kurtarmakta olduğunu bir sitenin üst sitesinde kullanabilirsiniz. Tüm üst sitelerdeki ortak anahtarları kurtarılan siteye dağıtmak için bu seçeneği kullanın.  

/PARENTKEYS seçeneği, seçeneğini çalıştırdığınız siteden ve bu sitenin üzerindeki her bir üst sitedeki anahtarlar &lt;sitekodu\>' na konuma koyar. CT7.  

Preinst. exe dosyasını bu seçenekle çalıştırdıktan sonra, &lt; *sitekodu*> el ile kopyalayın. CT7 dosyasını kurtarılan sitenin. ..\Inboxes\hman.exe klasörüne (HMAN. box\pubkey değil) kopyalayın.  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a>Siteler arasında el ile ortak anahtarları değiştirme  
Varsayılan olarak, Configuration Manager siteleri için **güvenli anahtar değişimi iste** seçeneği etkinleştirilmiştir. Güvenli anahtar değişimi gerektiğinde, siteler arasındaki ilk ortak anahtar değişimini elle gerçekleştirmeniz gereken iki durum vardır:  

-   Active Directory şeması Configuration Manager için genişletilmemişse  

-   Configuration Manager siteler site verilerini Active Directory yayımmıyor  

Her sitenin ortak anahtarını dışarı aktarmak için Hiyerarşi Bakımı aracını kullanabilirsiniz. Bunlar dışarı aktarıldıktan sonra, anahtarları siteler arasında elle değiştirmeniz gerekir.  

> [!NOTE]  
>  Ortak anahtarlar elle değiştirildikten sonra, birincil sitenin yeni ortak anahtarı işlediğinden emin olmak için site yapılandırma değişikliklerini ve site bilgilerinin Active Directory Etki Alanı Hizmetlerine yayımlanmasını kaydeden üst site sunucusundaki **hman.log** günlük dosyasını inceleyebilirsiniz.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Alt site ortak anahtarını üst siteye elle aktarmak için  

1.  Alt sitede oturum açmışken bir komut istemi açın ve **Preinst.exe** dosyasının konumuna gidin.  

2.  Alt sitenin ortak anahtarını dışarı aktarmak için aşağıdakileri yazın: **Preinst/keyforparent**  

3.  /Keyforparent seçeneği, alt sitenin ortak anahtarını ** &lt;site kodunda\>koyar. **Sistem sürücüsünün kökünde bulunan CT4 dosyası.  

4.  **Site kodunu\> &lt; CT4** dosyasını üst sitenin ** &lt;Install Directory\>\Inboxes\hman.exe klasörüne taşıyın** .  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Üst site ortak anahtarını alt siteye elle aktarmak için  

1.  Üst sitede oturum açmışken bir komut istemi açın ve **Preinst.exe** dosyasının konumuna gidin.  

2.  Üst sitenin ortak anahtarını dışarı aktarmak için şunu yazın: **Preinst/keyforchild**.  

3.  /Keyforchild seçeneği, üst sitenin ortak anahtarını ** &lt;site kodunda\>koyar. **Sistem sürücüsünün kökünde bulunan CT5 dosyası.  

4.  **Site kodunu\> &lt; CT5** dosyasını alt sitedeki ** &lt;install Directory\>\Inboxes\hman.exe dizinine ekleyin** .  
