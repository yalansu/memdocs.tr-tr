---
title: Bakım görevleri
titleSuffix: Configuration Manager
description: Configuration Manager siteleri ve hiyerarşileri için hangi bakım görevlerinin gerçekleştirileceğini ve bunların ne zaman gerçekleştirileceğini anlayın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0a71fc2f09e967944adfc4266e25eb20acfb9fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713733"
---
# <a name="maintenance-tasks-for-configuration-manager"></a>Configuration Manager için bakım görevleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager siteleri ve hiyerarşileri, hizmetleri verimli ve sürekli olarak sağlamak için düzenli bakım ve izleme gerektirir. Düzenli bakım, donanım, yazılım ve Configuration Manager veritabanının doğru ve verimli bir şekilde çalışmaya devam etmesini sağlar. En iyi performans, başarısızlık riskini büyük ölçüde azaltır.  

 Configuration Manager durumunu izlemek için uyarıları ayarlamak ve durum sistemini kullanmak için bkz. [Configuration Manager için uyarıları ve durum sistemini kullanma](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

## <a name="maintenance-tasks"></a><a name="bkmk_MTs"></a>Bakım görevleri

 Doğru site işlemlerini sağlamak için düzenli bakım önemlidir. Bakım tarihlerini, bakımını yapan kişileri ve görevlerle ilgili tüm bakım açıklamalarını belgelemek için bir bakım günlüğü tutun. Sitenizi sürdürmek için günlük veya haftalık Bakımı göz önünde bulundurun. Bazı görevler farklı bir zamanlama gerektirebilir. Yaygın bakım, şirket ilkeleriniz ile uyumluluğu sürdürmek için hem yerleşik bakım görevlerini hem de hesap bakımı gibi diğer görevleri içerebilir.  

 Farklı bakım görevlerinin ne zaman planlanacağını planlamaya yardımcı olması için aşağıdaki bilgileri kılavuz olarak kullanın. Bu listeleri bir başlangıç noktası olarak kullanın ve ihtiyacınız olabilecek görevleri ekleyin.  

### <a name="daily-tasks"></a>Günlük Görevler
Aşağıdakiler, günlük bir zamanlamaya göre düşünebileceğiniz bakım görevleridir:  

- Günlük olarak çalıştırılmak üzere zamanlanmış önceden tanımlanmış bakım görevlerinin başarıyla çalıştığını denetleyin.  

- Configuration Manager veritabanının durumunu denetleyin.  

- Site sunucusu durumunu kontrol edin.  

- Dosya biriktirme listeleri için Configuration Manager site sistemi gelen kutularını kontrol edin.  

- Site sistemlerinin durumunu denetleyin.  

- Site sistemlerindeki işletim sistemi olay günlüklerini denetleyin.  

- Site veritabanı bilgisayarından SQL Server hata günlüğünü kontrol edin.  

- Sistem performansını denetleyin.  

- Configuration Manager uyarılarını denetleyin.  

### <a name="weekly-tasks"></a>Haftalık Görevler

Aşağıdakiler, haftalık bir zamanlamaya göre düşünebileceğiniz bakım görevleridir:  

- Haftalık olarak çalışmak üzere zamanlanmış önceden tanımlanmış bakım görevlerinin başarıyla çalıştığını denetleyin.  

- Site sistemlerinden gereksiz dosyaları silin.  

- Gerekirse Son Kullanıcı raporları oluşturun ve dağıtın.  

- Uygulama, güvenlik ve sistem olay günlüklerini yedekleyin ve temizleyin.  

- Site veritabanının boyutunu kontrol edin ve site veritabanı sunucusunda site veritabanının büyüyebilmesi için yeterli kullanılabilir disk alanı olduğunu doğrulayın.  

- SQL Server bakım planınıza göre site veritabanında veritabanı bakımı SQL Server.  

- Tüm site sistemlerinde kullanılabilir disk alanını denetleyin.  

- Tüm site sistemlerinde disk birleştirme araçları 'nı çalıştırın.  

### <a name="periodic-tasks"></a>Düzenli görevler

Günlük veya haftalık bakım gerektirmeyen bazı görevler, genel site sistem durumunu sağlamak açısından önemlidir. Bu görevler ayrıca güvenlik ve olağanüstü durum kurtarma planlarının güncel olmasını da sağlar. Aşağıdakiler, günlük veya haftalık görevlerden daha düzenli bir zamanlama için düşünebileceğiniz bakım görevleridir:  

- Hesap ve parolaları güvenlik planınıza göre gerekliyse değiştirin.  

- Zamanlanmış bakım görevlerinin yapılandırılmış site ayarlarına bağlı olarak doğru ve etkili bir şekilde zamanlandığını denetlemek için bakım planını gözden geçirin.  

- Gerekli değişiklikler için Configuration Manager hiyerarşi tasarımını gözden geçirin.  

- Site işlemlerini etkileyen değişikliklerin yapıldığından emin olmak için ağ performansını denetleyin.  

- Site işlemlerini etkileyen Active Directory ayarlarının değiştirilmediğini denetleyin. Örneğin, Active Directory sitelere atanmış olan ve Configuration Manager site için sınır olarak kullanılan alt ağların değiştirilmediğini denetleyin.  

- Gerekli değişiklikler için olağanüstü durum kurtarma planınızı gözden geçirin.  

- Site Sunucusunu Yedekle bakım görevinin oluşturduğu en son yedeklemenin yedekleme kopyasını kullanarak, bir test laboratuvarında olağanüstü durum kurtarma planına uygun bir site kurtarması yapın.

- Herhangi bir hata veya kullanılabilir donanım güncelleştirmesi için donanımı denetleyin.  

- Sitenin genel durumunu kontrol edin.  

## <a name="maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a>Site veritabanınızın işletimsel durumunu koruyun

 Configuration Manager siteniz ve hiyerarşiniz, zamanladığınız ve ayarladığınız görevleri yaparken, site bileşenleri sürekli olarak verileri Configuration Manager veritabanına ekler. Veri miktarı arttıkça, veritabanı performansı ve veritabanı reddi boş depolama alanı. Artık ihtiyacınız olmayan eski verileri kaldırmak için site bakım görevlerini ayarlayabilirsiniz.  

 Configuration Manager, Configuration Manager veritabanının sistem durumunu korumak için kullanabileceğiniz, önceden tanımlanmış bakım görevleri sağlar. Tüm bakım görevleri, varsayılan olarak her bir sitede kullanılamaz. Bazıları olmadığı sürece birkaç görev etkindir ve tümü ayarlayabileceğiniz bir zamanlamayı destekler.  

 Çoğu bakım görevi, Configuration Manager veritabanından düzenli olarak güncel olmayan verileri kaldırır. Gereksiz verileri kaldırarak veritabanının boyutunu azaltmak, veritabanının ve hiyerarşinin verimliliğini artıran performansı ve veritabanının bütünlüğünü geliştirir. **Dizinleri yeniden oluştur**gibi diğer görevler veritabanı verimliliğini korumanıza yardımcı olur. **Site sunucusu yedekle** görevi gibi diğer görevler olağanüstü durum kurtarmaya hazırlanmanıza yardımcı olur.  

> [!IMPORTANT]
> Verileri silen herhangi bir görevin zamanlamasını planlarken, bu verilerin hiyerarşi genelinde kullanımını göz önünde bulundurun. Bir sitede veri silen bir görev çalıştırıldığında, bilgiler Configuration Manager veritabanından kaldırılır ve bu değişiklik hiyerarşideki tüm sitelere çoğaltılır. Bu silme, bu verilere dayanan diğer görevleri etkileyebilir. Örneğin, merkezi yönetim sitesinde, istemci olmayan bilgisayarları tanımlamak için her ay bir kez çalışacak şekilde bulmayı ayarlayabilirsiniz. Configuration Manager istemcisini, bulmanın iki haftası dahilinde bu bilgisayarlara yüklemeyi planlarsınız. Ancak, hiyerarşideki bir sitede, bir yönetici, eski bulma verilerini sil görevini her yedi günde bir çalışacak şekilde ayarlar. Sonuç, istemci olmayan bilgisayarların bulunduklarında yedi gün sonra Configuration Manager veritabanından silinir. Merkezi yönetim sitesine döndüğünüzde, Configuration Manager istemcisini bu yeni bilgisayarlara 10. günde yüklemeye hazırlarsınız. Ancak, eski bulma verilerini Sil görevi son zamanlarda yedi gün veya daha eski olan silinen veriler içerdiğinden, son bulunan bilgisayarlar artık veritabanında kullanılamaz.

Bir Configuration Manager sitesini yükledikten sonra, kullanılabilir bakım görevlerini inceleyin ve işlemlerinizin gerektirdiği görevleri etkinleştirin. Her görevin varsayılan zamanlamasını gözden geçirin ve gerektiğinde, bakım görevinin hiyerarşinize ve ortamınıza uyacak şekilde ince ayar yapmak için zamanlamayı ayarlayın. Her görevin varsayılan zamanlaması birçok ortama uygun olsa da, sitelerinizin ve veritabanınızın performansını izleyin ve dağıtımınızın verimliliğini artırmak için görevleri hassas bir şekilde ayarlamayı beklemeniz gerekir. Site ve veritabanı performansını düzenli aralıklarla gözden geçirmeyi ve bakım görevlerini ve bunların zamanlamalarını bu verimliliği korumak için yeniden yapılandırmayı planlayın.  

## <a name="set-up-maintenance-tasks"></a>Bakım görevlerini ayarlama

 Her Configuration Manager sitesi, site veritabanının işletimsel verimliliğini korumaya yardımcı olan bakım görevlerini destekler. Varsayılan olarak, her sitede birkaç bakım görevi etkinleştirilmiştir ve tüm görevler bağımsız zamanlamaları destekler. Bakım görevleri her site için ayrı ayrı ayarlanır ve bu sitedeki veritabanına uygulanır. Ancak, **eski bulma verilerini sil**gibi bazı görevler, bir hiyerarşideki tüm sitelerde kullanılabilir olan bilgileri etkiler.  

 Yalnızca bir sitede ayarlayabileceğiniz bakım görevleri Configuration Manager konsolunda görüntülenir. Site türüne göre bakım görevlerinin tüm listesi için, bkz. [Configuration Manager için bakım görevleri başvurusu](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Bakım görevlerinin ortak ayarlarını ayarlamanıza yardımcı olması için aşağıdaki yordamı kullanın.  

### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1906"></a><a name="bkmk_MTs1906"></a>Configuration Manager sürüm 1906 için bakım görevlerini ayarlamak için
<!--3555894-->
Sürüm 1906 ' den başlayarak, site sunucusu bakım görevleri artık bir site sunucusunun Ayrıntılar görünümündeki kendi sekmesinden görüntülenebilir, düzenlenebilir ve izlenebilir. Daha önceki Configuration Manager sürümlerde yaptığınız gibi **Ayarlar** grubunda **Site Bakımı** ' nı seçerek bakım görevlerini düzenleyebilirsiniz.

1. Configuration Manager konsolunda, **Yönetim** > **Site yapılandırması** >**siteler**' e gidin.
1. Listenizden bir site seçin ve ardından ayrıntı panelinde **bakım görevleri** sekmesine tıklayın.
1. Yalnızca seçili sitede bulunan görevler görüntülenir. Bakım görevlerinden birine sağ tıklayın ve aşağıdaki seçeneklerden birini belirleyin:
   - **Etkinleştirin** -görevi açın.
   - **Devre dışı bırak** -görevi kapat.
   - **Düzenle** -görev zamanlamasını veya özelliklerini düzenleyin.

![Site sunucusunun ayrıntı görünümündeki bakım görevlerinin sekmesi](./media/3555894-maintenance-tasks.png)

**Bakım görevleri** sekmesi, şunları gibi bilgiler sağlar:

- Görev etkinse
- Görev zamanlaması
- Son başlangıç zamanı
- Son tamamlanma zamanı
- Görev başarıyla tamamlanırsa
 
### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1902-and-prior"></a>Configuration Manager sürüm 1902 ve öncesi için bakım görevlerini ayarlamak için

1. Configuration Manager konsolunda, **Yönetim** > **Site yapılandırması** >**siteler**' e gidin.
2. Kurmak istediğiniz bakım görevinin bulunduğu siteyi seçin.  
3. **Giriş** sekmesinde, **Ayarlar** grubunda, **Site Bakımı**' nı seçin ve ardından ayarlamak istediğiniz bakım görevini seçin. Yalnızca seçili sitede bulunan görevler görüntülenir.

4. Görevi ayarlamak için **Düzenle**' yi seçin. **Bu görevi etkinleştir** onay kutusunun işaretli olduğundan emin olun ve görevin ne zaman çalışacağını bir zamanlama ayarlayın. Görev, eski verileri de silerse, görev çalıştırıldığında veritabanından Silinecek verilerin yaşını ayarlayın. Görev **özelliklerini**kapatmak için **Tamam ' ı** seçin.

   > [!NOTE]  
   > **Eski durum Iletilerini Sil**için, durum filtre kurallarını ayarlarken silinecek veri yaşını ayarlarsınız.  

5. Görev özelliklerini düzenlemeden görevi etkinleştirmek veya devre dışı bırakmak için **Etkinleştir** veya **devre dışı bırak** düğmesini seçin. Düğme etiketi, görevin geçerli yapılandırmasına bağlı olarak değişir.  
6. Bakım görevlerini tamamladığınızda, yordamı tamamladıktan sonra **Tamam** ' ı seçin.

## <a name="next-steps"></a>Sonraki adımlar

[Bakım görevleri için başvuru](reference-for-maintenance-tasks.md)
