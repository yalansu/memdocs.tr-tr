---
title: Yazılım güncelleştirmelerine giriş
titleSuffix: Configuration Manager
description: Configuration Manager 'de yazılım güncelleştirmelerinin temellerini öğrenin.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: bd384edafd6464073b33a593a56bc88ba2fb0b87
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906758"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Configuration Manager yazılım güncelleştirmelerine giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager yazılım güncelleştirmeleri, kuruluştaki istemci bilgisayarlara yapılan yazılım güncelleştirmelerini izleme ve uygulamaya yönelik karmaşık görevi yönetmeye yardımcı olabilecek bir dizi araç ve kaynak sağlar. İşletme verimliliğini sürdürmek, güvenlik sorunlarının üstesinden gelmek ve ağ altyapısının kararlılığını korumak için etkili bir yazılım güncelleştirme yönetimi işlemi gereklidir. Ancak, teknolojinin değişen yapısı ve yeni güvenlik tehditlerinin sürekli ortaya çıkması nedeniyle, etkili yazılım güncelleştirme yönetimi tutarlı ve sürekli bir ilgi gerektirir.  

Ortamınızdaki yazılım güncelleştirmelerini nasıl dağıtabileceğinizi gösteren örnek bir senaryo için bkz. [güvenlik yazılımı güncelleştirmelerini dağıtmak Için örnek senaryo](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a>Yazılım güncelleştirmeleri eşitlemesi  
 Configuration Manager yazılım güncelleştirmeleri eşitlemesi, yazılım güncelleştirmeleri meta verilerini almak için Microsoft Update bağlanır. Üst düzey site (merkezi yönetim sitesi veya tek başına birincil site) bir zamanlamaya göre Microsoft Update eşitlenir veya Configuration Manager konsolundan eşitlemeyi el ile başlatabilirsiniz. Configuration Manager, en üst düzey sitede yazılım güncelleştirmeleri eşitlemesini bitirdiğinde, varsa alt sitelerde yazılım güncelleştirmeleri eşitlemesi başlar. Her birincil sitede veya ikincil sitede eşitleme tamamlandığında, istemci bilgisayarlara yazılım güncelleştirme noktalarının konumunu sağlayan, site genelinde bir ilke oluşturulur.  

> [!NOTE]  
>  Yazılım güncelleştirmeleri istemci ayarlarında varsayılan seçenek olarak etkindir. Ancak, yazılım güncelleştirmelerini bir koleksiyonda veya varsayılan ayarlarda devre dışı bırakmak için **İstemcilerde yazılım güncelleştirmelerini etkinleştir** istemci ayarını **Hayır** yaparsanız yazılım güncelleştirme noktalarının konumu ilişkili istemcilere gönderilmez. Ayrıntılar için bkz. [yazılım güncelleştirmeleri istemci ayarları](../../core/clients/deploy/about-client-settings.md#software-updates).  

 İstemci bu ilkeyi aldıktan sonra, yazılım güncelleştirmelerinin uyumluluğu için bir tarama başlatır ve bilgileri Windows Yönetim Araçları'na (WMI) yazar. Bu uyumluluk bilgileri daha sonra yönetim noktasına, oradan da site sunucusuna gönderilir. Uyumluluk denetimi hakkında daha fazla bilgi için bu konudaki [Software updates compliance assessment](#BKMK_SUMCompliance) bölümüne bakın.  

 Birincil siteye birden çok yazılım güncelleştirme noktası yükleyebilirsiniz. Yüklediğiniz ilk yazılım güncelleştirme noktası eşitleme kaynağı olarak yapılandırılır. Bu, Configuration Manager hiyerarşinizde bulunmayan Microsoft Update veya WSUS sunucusundan eşitlenir. Sitedeki diğer yazılım güncelleştirme noktaları bu ilk yazılım güncelleştirme noktasını eşitleme kaynağı olarak kullanır.  

> [!NOTE]  
>  Yazılım güncelleştirmelerini eşitleme işlemi üst düzey sitede tamamlandığında, yazılım güncelleştirmelerinin meta verileri veritabanı çoğaltması kullanılarak alt sitelere çoğaltılır. Bir Configuration Manager konsolunu alt siteye bağladığınızda, Configuration Manager yazılım güncelleştirmeleri meta verilerini görüntüler. Ancak, sitede bir yazılım güncelleştirme noktası yükleyip yapılandırana kadar istemciler yazılım güncelleştirmeleri uyumluluğunu taramayacaktır, istemciler uyumluluk bilgilerini Configuration Manager olarak raporlamaz ve yazılım güncelleştirmelerini başarıyla dağıtamazsınız.  

### <a name="synchronization-on-the-top-level-site"></a>Üst düzey sitede eşitleme  
 Üst düzey sitede yazılım güncelleştirmeleri eşitleme işlemi, Yazılım Güncelleştirme Noktası Bileşeni özelliklerinde belirttiğiniz ölçütleri karşılayan yazılım güncelleştirmeleri meta verilerini Microsoft Update'ten alır. Bu ölçütler yalnızca üst düzey sitede yapılandırılır.  

> [!NOTE]  
>  Eşitleme kaynağı olarak Microsoft güncelleştirmeleri yerine Configuration Manager hiyerarşisinde olmayan mevcut bir WSUS sunucusunu belirtebilirsiniz.  

 Aşağıdaki listede, üst düzey sitede eşitleme işlemi için temel adımlar açıklanmıştır:  

1.  Yazılım güncelleştirmelerini eşitleme başlar.  

2.  WSUS Eşitleme Yöneticisi, yazılım güncelleştirme noktasında çalışan WSUS'a Microsoft Update ile eşitleme başlatma isteği gönderir.  

3.  Yazılım güncelleştirmelerinin meta verisi Microsoft Update'ten eşitlenir ve tüm değişiklikler WSUS veritabanına eklenir veya güncelleştirilir.  

4.  WSUS eşitlemeyi tamamladığında, WSUS Eşitleme Yöneticisi yazılım güncelleştirme meta verilerini WSUS veritabanından Configuration Manager veritabanına eşitler ve son eşitlemeden sonra yapılan değişiklikler site veritabanına eklenir veya güncelleştirilir. Yazılım güncelleştirmeleri meta verisi site veritabanına yapılandırma öğesi olarak depolanır.  

5.  Yazılım güncelleştirmeleri yapılandırma öğeleri, veritabanı çoğaltması kullanılarak alt sitelere gönderilir.  

6.  Eşitleme başarıyla tamamlandığında, WSUS Eşitleme Yöneticisi durum iletisi 6702'yi oluşturur.  

7.  WSUS Eşitleme Yöneticisi tüm alt sitelere eşitleme isteği gönderir.  

8.  WSUS Eşitleme Yöneticisi, sitedeki diğer yazılım güncelleştirme noktalarında çalışan WSUS'a birer birer istek gönderir. Diğer yazılım güncelleştirme noktalarındaki WSUS sunucuları, sitedeki varsayılan yazılım güncelleştirme noktasında çalışan WSUS'un çoğaltmaları olacak şekilde yapılandırılır.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Alt birincil ve ikincil sitelerde eşitleme  
 Üst düzey sitede yazılım güncelleştirmelerini eşitleme işlemi sırasında, yazılım güncelleştirmeleri yapılandırma öğeleri veritabanı çoğaltması kullanılarak alt sitelere çoğaltılır. İşlemin sonunda, üst düzey site alt siteye bir eşitleme isteği gönderir ve alt site WSUS eşitlemesini başlatır. Aşağıdaki listede, alt birincil sitede veya ikincil sitede eşitleme işlemi için temel adımlar verilmiştir:  

1.  WSUS Eşitleme Yöneticisi üst düzey siteden bir eşitleme isteği alır.  

2.  Yazılım güncelleştirmelerini eşitleme başlar.  

3.  WSUS Eşitleme Yöneticisi, yazılım güncelleştirme noktasında çalışan WSUS'a eşitleme başlatma isteğinde bulunur.  

4.  Alt sitedeki yazılım güncelleştirme noktasında çalışan WSUS, yazılım güncelleştirmeleri meta verilerini üst sitedeki yazılım güncelleştirme noktasında çalışan WSUS'tan eşitler.  

5.  Eşitleme başarıyla tamamlandığında, WSUS Eşitleme Yöneticisi durum iletisi 6702'yi oluşturur.  

6.  WSUS Eşitleme Yöneticisi birincil siteden tüm alt ikincil sitelere eşitleme isteği gönderir. İkincil site üst birincil siteyle yazılım güncelleştirmelerini eşitlemeye başlar. İkincil site, üst sitede çalışan WSUS'un çoğaltması olarak yapılandırılır.  

7.  WSUS Eşitleme Yöneticisi, sitedeki diğer yazılım güncelleştirme noktalarında çalışan WSUS'a birer birer istek gönderir. Diğer yazılım güncelleştirme noktalarındaki WSUS sunucuları, sitedeki varsayılan yazılım güncelleştirme noktasında çalışan WSUS'un çoğaltmaları olacak şekilde yapılandırılır.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Configuration Manager ' de istemci bilgisayarlara yazılım güncelleştirmeleri dağıtmadan önce, istemci bilgisayarlarda yazılım güncelleştirmeleri uyumluluğu için bir tarama başlatın. Her yazılım güncelleştirmesi için o güncelleştirmenin uyumluluk durumunu içeren bir durum iletisi oluşturulur. Durum iletileri topluca yönetim noktasına ve oradan site sunucusuna gönderilir, burada uyumluluk durumu site veritabanına eklenir. Yazılım güncelleştirmeleri için uyumluluk durumu Configuration Manager konsolunda görüntülenir. Güncelleştirme gerektiren bilgisayarlara yazılım güncelleştirmeleri dağıtabilir ve yükleyebilirsiniz. Aşağıdaki bölümlerde, uyum durumlarıyla ilgili bilgiler verilmiş ve yazılım güncelleştirmeleri uyumluluğunu tarama işlemi açıklanmıştır.  

### <a name="software-updates-compliance-states"></a>Yazılım güncelleştirmeleri uyumluluk durumları  
 Aşağıda, yazılım güncelleştirmeleri için Configuration Manager konsolunda görüntülenen her uyumluluk durumu listelenmiştir ve açıklanmaktadır.  

-   **Gerekli**  

     Yazılım güncelleştirmesinin istemci bilgisayarda uygulanabilir ve gerekli olduğunu belirtir. Yazılım güncelleştirmesinin durumu **Gerekli**olduğunda aşağıdaki koşullardan herhangi biri geçerli olabilir:  

    -   Yazılım güncelleştirmesi istemci bilgisayara dağıtılmadı.  

    -   Yazılım güncelleştirmesi istemci bilgisayara yüklendi. Ancak, en son durum iletisi henüz site sunucusundaki veritabanına eklenmedi. Yükleme tamamlandıktan sonra, istemci bilgisayar güncelleştirmeyi yeniden tarar. İstemci güncelleştirilen durumu yönetim noktasına gönderene ve sonra o da güncelleştirilen durumu site sunucusuna iletene kadar iki dakikalık bir gecikme olabilir.  

    -   Yazılım güncelleştirmesi istemci bilgisayara yüklendi. Ancak, güncelleştirmenin tamamlanabilmesi için yazılım güncelleştirme yüklemesi bilgisayarın yeniden başlatılmasını gerektirir.  

    -   Yazılım güncelleştirmesi istemci bilgisayara dağıtıldı ancak henüz yüklenmedi.  

-   **Gerekli Değil**  

     Yazılım güncelleştirmesinin istemci bilgisayarda uygulanamadığını belirtir. Bu nedenle, yazılım güncelleştirmesi gerekli değildir.  

-   **Yüklendi**  

     Yazılım güncelleştirmesinin istemci bilgisayarda uygulanabildiğini ve istemci bilgisayarda yazılım güncelleştirmesinin zaten yüklü olduğunu belirtir.  

-   **Bilinmiyor**  

     Site sunucusunun, genellikle aşağıdakilerden biri nedeniyle istemci bilgisayardan durum iletisi almadığını belirtir:  

    -   İstemci bilgisayar yazılım güncelleştirmeleri uyumluluğunu başarıyla taramadı.  

    -   İstemci bilgisayarda tarama başarıyla tamamlandı. Ancak, muhtemelen durum iletisi biriktirme listesi nedeniyle site sunucusunda durum iletisi henüz işlenmedi.  

    -   İstemci bilgisayarda tarama başarıyla tamamlandı, ancak durum iletisi alt siteden alınmadı.  

    -   İstemci bilgisayarda tarama başarıyla tamamlandı, ancak durum iletisi dosyası bir şekilde bozuktu ve işlenemedi.  

### <a name="scan-for-software-updates-compliance-process"></a>Yazılım güncelleştirmeleri uyumluluk işlemi taraması  
 Yazılım güncelleştirme noktası yüklenip eşitlendiğinde, istemci bilgisayarlara yazılım güncelleştirmelerinin site için etkinleştirildiğini Configuration Manager bildiren, site genelinde bir makine ilkesi oluşturulur. İstemci makine ilkesini aldığında, izleyen iki saat içinde rastgele başlayacak şekilde bir uyumluluk değerlendirmesi taraması zamanlanır. Tarama başlatıldığında Yazılım Güncelleştirmeleri İstemci Aracısı işlemi tarama geçmişini temizler, tarama için kullanılması gereken WSUS sunucusunu bulma isteği gönderir ve yerel Grup İlkesini WSUS sunucu konumu ile güncelleştirir.  

> [!NOTE]  
>  İnternet tabanlı istemciler WSUS sunucusuna SSL kullanarak bağlanmalıdır.  

 Windows Update Aracısı'na (WUA) bir tarama isteği geçirilir. WUA ardından, yerel ilkede listelenen WSUS sunucusu konumuna bağlanır, WSUS sunucusunda eşitlenmiş ola yazılım güncelleştirmeleri meta verilerini alır ve istemci bilgisayarını güncelleştirmeler için tarar. Bir Yazılım Güncelleştirmeleri İstemci Aracısı işlemi, uyumluluk taramasının tamamlandığını algılar ve son taramadan sonra uyumluluk durumunda değişiklik olan her bir yazılım güncelleştirmesi için durum mesajları oluşturur. Durum mesajları, 15 dakikada bir toplu halde yönetim noktasına gönderilir. Yönetim noktası ardından durum mesajlarını site sunucusuna iletir, burada, durum mesajları site sunucusu veritabanına yerleştirilir.  

 Yazılım güncelleştirmeleri uyumluluğu için ilk tarama sonrasında, tarama, yapılandırılan tarama zamanlamasında başlatılır. Ancak, istemci, Yaşam Süresi (TTL) değerinde belirtilen zaman çerçevesinde yazılım güncelleştirmeleri uyumluluğun taradıysa, istemci, yerel olarak depolanan yazılım güncelleştirmeleri meta verilerini kullanır. Son tarama TTL dışında olduğunda, istemcinin, yazılım güncelleştirme noktasında çalıştırılan WSUS'a bağlanması ve istemcide depolanan yazılım güncelleştirme meta verilerini güncelleştirmesi gerekir.  

 Tarama zamanlaması dahil, yazılım güncelleştirmeleri uyumluluk taraması aşağıdaki şekillerde başlatılabilir:  

-   **Yazılım güncelleştirmeleri tarama zamanlaması**: Yazılım güncelleştirmeleri uyumluluk taraması, Yazılım Güncelleştirmeleri İstemci Aracısı ayarlarında yapılandırılan tarama zamanlamasında başlar. Yazılım güncelleştirmeleri istemci ayarlarının nasıl yapılandırılacağı hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri istemci ayarları](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Configuration Manager Özellikler eylemi**: Kullanıcı, **Yazılım Güncelleştirmeleri Tarama Döngüsü** veya **Yazılım Güncelleştirmeleri Dağıtım Değerlendirme Döngüsü** eylemini, istemci bilgisayarında **Configuration Manager Özellikler** iletişim kutusundaki **Eylem** sekmesinde başlatabilir.  

-   **Dağıtım yeniden değerlendirme zamanlaması**: Dağıtım değerlendirmesi ve yazılım güncelleştirmeleri uyumluluk taraması, Yazılım Güncelleştirmeleri İstemci Aracısı ayarlarında yapılandırılan dağıtım yeniden değerlendirme zamanlamasında başlar. Yazılım güncelleştirmeleri istemci ayarları hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri istemci ayarları](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Güncelleştirme dosyalarını indirmeden önce**: Bir istemci bilgisayarı, gerekli yeni bir dağıtım için bir atama ilkesi aldığında, Yazılım Güncelleştirmeleri İstemci Aracısı, yazılım güncelleştirme dosyalarını yerel istemci önbelleğine indirir. Yazılım güncelleştirme dosyalarını indirmeden önce, istemci aracısı, yazılım güncelleştirmesinin hala gerekli olduğunu doğrulamak amacıyla bir tarama başlatır.  

-   **Yazılım güncelleştirmesi yüklemesinden önce**: Yazılım güncelleştirme yüklemesinden hemen önce, Yazılım Güncelleştirmeleri İstemci Aracısı, yazılım güncelleştirmelerinin hala gerekli olduğunu doğrulamak amacıyla bir tarama başlatır.  

-   **Yazılım güncelleştirmesi yüklemesinden sonra**: Bir yazılım güncelleştirme yüklemesi tamamlandıktan hemen sonra, Yazılım Güncelleştirme İstemci Aracısı, yazılım güncelleştirmelerinin artık gerekli olmadığını doğrulamak için bir tarama başlatır ve yazılım güncelleştirmesinin yüklendiğini belirten yeni bir durum mesajı oluşturur. Yükleme tamamlandığında, ancak bir yeniden başlatma gerekli olduğunda, durum mesajı, istemci bilgisayarının bir yeniden başlatma beklediğini belirtir.  

-   **Sistem yeniden başlatıldıktan sonra**: Bir istemci bilgisayarı, yazılım güncelleştirme yüklemesinin tamamlanması için bir sistem yeniden başlatması beklediğinde, Yazılım Güncelleştirmeleri İstemci aracısı, yeniden başlatma sonrasında, yazılım güncelleştirmesinin artık gerekli olmadığını doğrulamak için bir tarama başlatır ve yazılım güncelleştirmesinin yüklendiğini belirten bir durum mesajı oluşturur.  

#### <a name="time-to-live-value"></a>Yaşam süresi değeri  
 Yazılım güncelleştirme uyumluluğu taraması için gerekli yazılım güncelleştirmeleri meta verileri, yerel istemci bilgisayarında depolanır ve varsayılan olarak, 24 saate kadar ilgilidir. Bu değer, Yaşam Süresi (TTL) olarak bilinir.  

#### <a name="scan-for-software-updates-compliance-types"></a>Yazılım güncelleştirmeleri uyumluluk taraması türleri  
 İstemci, yazılım güncelleştirmeleri uyumluluğunun başlatıldığı tarama şekline bağlı olarak, bir çevrimiçi veya çevrimdışı tarama ve zorlanmış veya zorunlu kılınmayan bir tarama kullanarak yazılım güncelleştirmeleri uyumluğunu tarar. Aşağıda, taramanın başlatılması için hangi yöntemlerin çevrimiçi veya çevrimdışı olduğunu ve taramanın zorlanıp zorlanmadığını ve ne olduğu açıklanmaktadır.  

-   **Yazılım güncelleştirmeleri Tarama zamanlaması** (zorunlu olmayan çevrimiçi tarama)  

     Yapılandırılan tarama zamanlamasında, istemci, yalnızca son tarama TTL dışında olduğu zaman yazılım güncelleştirmeleri meta verilerini almak için yazılım güncelleştirme noktasında çalıştırılan WSUS'ye bağlanır.  

-   **Yazılım güncelleştirmeleri tarama çevrimi** veya **yazılım güncelleştirmeleri dağıtım değerlendirme çevrimi** (zorlamalı çevrimiçi tarama)  

     İstemci bilgisayarı, yazılım güncelleştirmeleri uyumluğunu taramadan önce, yazılım güncelleştirmeleri meta verilerini almak üzere daima yazılım güncelleştirme noktasında çalıştırılan WSUS'ye bağlanır. Tarama tamamlandıktan sonra, TTL sayacı yeniden ayarlanır. Örneğin, TTL 24 saat ise, bir kullanıcı, yazılım güncelleştirmeleri uyumluluğu taraması başlattıktan sonra, TTL 24 saate yeniden ayarlanır.  

-   **Dağıtım yeniden değerlendirme zamanlaması** (zorunlu olmayan çevrimiçi tarama)  

     Yapılandırılan dağıtım yeniden değerlendirmesi zamanlamasında, istemci, yalnızca son tarama TTL dışında olduğu zaman yazılım güncelleştirmeleri meta verilerini almak için yazılım güncelleştirme noktasında çalıştırılan WSUS'ye bağlanır.  

-   **Güncelleştirme dosyalarını Indirmeden önce** (zorunlu olmayan çevrimiçi tarama)  

     İstemcinin gerekli dağıtımlarda güncelleştirme dosyalarını indirebilmesinden önce, istemci, yalnızca son tarama TTL dışında olduğu zaman yazılım güncelleştirmeleri meta verilerini almak üzere yazılım güncelleştirme noktasında çalıştırılan WSUS'ye bağlanır.  

-   **Yazılım güncelleştirme yüklemesinden önce** (zorunlu olmayan çevrimiçi tarama)  

     İstemci gerekli dağıtımlarda güncelleştirme dosyalarını indirmeden önce, istemci, yalnızca son tarama TTL dışında olduğu zaman yazılım güncelleştirmeleri meta verilerini almak üzere yazılım güncelleştirme noktasında çalıştırılan WSUS'ye bağlanır.  

-   **Yazılım güncelleştirme yüklemesinden sonra** (çevrimdışı tarama zorlandı)  

     Bir yazılım güncelleştirmesi yüklendikten sonra Yazılım Günceleştirmeleri İstemci Aracısı, yerel meta verileri kullanarak yeni bir tarama başlatır. İstemci, yazılım güncelleştirmeleri meta verilerini almak için, yazılım güncelleştirme noktasında çalıştırılan WSUS'ye hiçbir zaman bağlanmaz.  

-   **Sistem yeniden başlatıldıktan sonra** (zorla çevrimdışı tarama)  

     Bir yazılım güncelleştirmesi yüklendikten ve bilgisayar yeniden başlatıldıktan sonra, Yazılım Günceleştirmeleri İstemci Aracısı, yerel meta verileri kullanarak yeni bir tarama başlatır. İstemci, yazılım güncelleştirmeleri meta verilerini almak için, yazılım güncelleştirme noktasında çalıştırılan WSUS'ye hiçbir zaman bağlanmaz.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a>Yazılım güncelleştirmesi dağıtım paketleri  
 Bir yazılım güncelleştirme dağıtım paketi, paylaşılan bir ağ klasörüne yazılım güncelleştirmelerini indirmek ve yazılım güncelleştirme kaynak dosyalarını, dağıtımda tanımlı dağıtım noktalarında ve site sunucularındaki içerik kitaplığına kopyalamak için kullanılan araçtır. Güncelleştirmeleri İndirme Sihirbazını kullanarak, yazılım güncelleştirmelerini indirebilirsiniz ve dağıtmadan önce onları dağıtım paketlerine ekleyebilirsiniz. Bu sihirbaz, dağıtım noktalarındaki yazılım güncelleştirmelerini sağlamanızı ve yazılım güncelleştirmelerini istemcilere dağıtmadan önce dağıtım işleminin bu kısmının başarılı olduğunu doğrulamanızı sağlar.  

 İndirilen yazılım güncelleştirmelerini, Yazılım Güncelleştirmelerini Dağıtma Sihirbazı ile dağıttığınızda, dağıtım işlemi otomatik olarak, yazılım güncelleştirmelerini içeren dağıtım paketini kullanır. İndirilen yazılım güncelleştirmeleri dağıtıldığında, Yazılım Güncelleştirmelerini Dağıtma Sihirbazı'nda yeni veya var olan bir dağıtım paketi belirtmeniz gerekir ve ardından sihirbaz tamamlandığında yazılım güncelleştirmeleri indirilir.  

> [!IMPORTANT]  
>  Dağıtım paketi kaynak dosyaları için paylaşılan ağ klasörünü, onu sihirbazda belirtmeden önce el ile oluşturmanız gerekir. Her bir dağıtım paketinin farklı bir paylaşılan ağ klasörü kullanması gerekir.  

> [!IMPORTANT]  
>  SMS Sağlayıcısı bilgisayar hesabının ve yazılım güncelleştirmelerini indiren yönetim kullanıcısının, paket kaynağına **Yazma** izinleri olması gerekir. Bir saldırganın paket kaynağında yazılım güncelleştirme kaynak dosyalarıyla oynama riskini azaltmak için, paket kaynağına erişimi kısıtlayın.  

 Yeni bir dağıtım paketi oluşturulduğunda, herhangi bir yazılım güncelleştirmesi indirilmeden önce içerik sürümü 1 olarak ayarlanır. Paket kullanılarak yazılım güncelleştirmesi dosyaları indirildiğinde içerik sürümü 2’ye yükseltilir. Bu nedenle tüm dağıtım paketleri 2 içerik sürümüyle başlar. Bir dağıtım paketinde içerik her değiştirildiğinde içerik sürümü 1’e yükseltilir. Daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

 İstemciler, bir dağıtımda yazılım güncelleştirmelerini, dağıtım paketinden bağımsız olarak, kullanılabilir yazılım güncelleştirmelerine sahip herhangi bir dağıtım noktası kullanarak yükler. Etkin bir dağıtım için bir dağıtım paketi silinse bile, istemciler, her bir güncelleştirme en az bir adet başka dağıtım paketine indirildiği ve istemciden erişilebilecek bir dağıtım noktasında kullanılabilir olduğu müddetçe, yazılım güncelleştirmelerini yine de yükleyebilir. Bir yazılım güncelleştirmesi içeren son dağıtım paketi silindiğinde, istemci bilgisayarları, güncelleştirme bir dağıtım paketine yeniden indirilene kadar yazılım güncelleştirmesini alamaz. Güncelleştirme dosyaları herhangi bir dağıtım paketinde olmadığında, yazılım güncelleştirmeleri Configuration Manager konsolunda kırmızı bir ok ile görünür. Dağıtımlar, bu durumda herhangi bir güncelleştirme içeriyorlarsa çift kırmızı okla belirir.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a>Yazılım güncelleştirmesi dağıtım iş akışları  
 Ortamınızda yazılım güncelleştirmeleri dağıtmak için iki ana senaryo vardır, el ile dağıtım ve otomatik dağıtım. Genellikle, istemci bilgisayarları için bir temel çizgisi oluşturmak için yazılım güncelleştirmelerini el ile yüklersiniz ve ardından yazılım güncelleştirmelerini istemcilerde otomatik dağıtım kullanarak yönetirsiniz. Aşağıdaki bölümlerde, yazılım güncelleştirmelerinin el ile ve otomatik dağıtımı iş akışı için bir özet sağlanmaktadır.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Yazılım güncelleştirmelerinin el ile dağıtımı  
 Yazılım güncelleştirmelerinin el ile dağıtımı, Configuration Manager konsolunda yazılım güncelleştirmeleri seçme ve dağıtım işlemini el ile başlatma işlemidir. Genellikle bu dağıtım yöntemini, devam eden aylık yazılım güncelleştirme dağıtımlarını yöneten otomatik dağıtım kuralları oluşturmadan önce, istemci bilgisayarlarını gerekli yazılım güncelleştirmeleri hakkında güncel tutmak için ve bant dışı yazılım güncelleştirme gereksinimlerini dağıtmak için kullanırsınız. Aşağıdaki listede, yazılım güncelleştirmelerinin el ile dağıtımı için genel iş akışı sağlanmaktadır:  

1.  Belirli gereklilikler kullanan yazılım güncelleştirmeleri için filtre. Örneğin, 50'den fazla istemci bilgisayarında gerekli tüm güvenlik veya kritik yazılım güncelleştirmelerini alan kriterler sağlayabilirsiniz.  

2.  Yazılım güncelleştirmelerini içeren bir yazılım güncelleştirme grubu oluşturun.  

3.  Yazılım güncelleştirmeleri için içeriği, yazılım güncelleştirme grubu içine indirin.  

4.  Yazılım güncelleştirme grubunu el ile dağıtın.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Yazılım güncelleştirmelerinin otomatik dağıtımı  
 Otomatik yazılım güncelleştirmeleri dağıtımı bir otomatik dağıtım kuralı (ADR) kullanılarak yapılandırılır. Genellikle bu dağıtım yöntemini, aylık yazılım güncelleştirmeleriniz (genelde Patch Tuesday olarak bilinir) ve tanım güncelleştirmelerini yönetmek için kullanırsınız. Kuralı çalıştığında, yazılım güncelleştirmeleri yazılım güncelleştirme grubundan kaldırılır (varolan bir grup kullanılıyorsa), belirtilen bir ölçütü karşılayan yazılım güncelleştirmeleri (örneğin, geçen hafta yayımlanan tüm güvenlik yazılım güncelleştirmeleri) bir yazılım güncelleştirme grubuna eklenir, yazılım güncelleştirmeleri için içerik dosyaları indirilir ve dağıtım noktalarına kopyalanır, ardından da yazılım güncelleştirmeleri hedef koleksiyonundaki istemci bilgisayarlara dağıtılır. Aşağıdaki listede, yazılım güncelleştirmelerinin otomatik dağıtımı için genel iş akışı sağlanmaktadır:  

1. Aşağıdaki gibi dağıtım ayarlarını belirten bir ADR oluşturun:  

   -   Hedef koleksiyon  

   -   Hedef koleksiyondaki istemci bilgisayarlar için dağıtımı etkinleştirmek mi yoksa yazılım güncelleştirme uyumluluğu hakkında rapor vermek mi istediğinize karar verin  

   -   Yazılım güncelleştirmeleri kriterleri  

   -   Değerlendirme ve dağıtım zamanlamaları  

   -   Kullanıcı deneyimleri  

   -   İndirme özellikleri  

2. Yazılım güncelleştirmeleri bir yazılım güncelleştirme grubuna eklenir.  

3. Yazılım güncelleştirme grubu, belirtilmişse, hedef koleksiyondaki istemci bilgisayarlarına dağıtılır.  

   Ortamınızda hangi dağıtım stratejisinin kullanılacağını belirlemeniz gerekir. Örneğin, ADR’yi ve test istemcilerinin bir hedef koleksiyonunu oluşturabilirsiniz. Yazılım güncelleştirmelerinin test grubuna yüklendiğini doğruladıktan sonra, kurala yeni bir dağıtım ekleyebilir veya var olan dağıtımdaki koleksiyonu, daha büyük bir istemci grubu içeren bir hedef koleksiyonla değiştirebilirsiniz. ADR’lerle oluşturulan yazılım güncelleştirme nesneleri etkileşimlidir.  

- ADR kullanılarak dağıtılmış yazılım güncelleştirmeleri, hedef koleksiyona eklenen yeni istemcilere otomatik olarak dağıtılır.  

- Bir yazılım güncelleştirme grubuna eklenen yeni yazılım güncelleştirmeleri, hedef koleksiyondaki istemcilere otomatik olarak dağıtılır.  

- ADR için dağıtımları istediğiniz zaman etkinleştirebilir veya devre dışı bırakabilirsiniz.  

  Bir ADR oluşturduktan sonra kurala başka dağıtımlar ekleyebilirsiniz. Bu destek, farklı koleksiyonlara farklı güncelleştirmeler dağıtma karmaşıklığını yönetmenize yardımcı olabilir. Her yeni dağıtım, tüm işlevlere ve dağıtım izleme deneyimine sahiptir ve eklediğiniz her yeni dağıtım:  

- ADR ilk kez çalıştırıldığında oluşturulan güncelleştirme grubunu ve paketi kullanır  

- Farklı bir koleksiyon belirtebilir  

- Aşağıdaki benzersiz dağıtım özelliklerini destekler:  

  -   Etkinleştirme zamanı  

  -   Son tarih  

  -   Son kullanıcı deneyimini gizle veya göster  

  -   Bu dağıtım için ayrı uyarılar  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a>Yazılım güncelleştirmesi dağıtım işlemi  
 Yazılım güncelleştirmelerini dağıttıktan sonra veya bir otomatik dağıtım kuralı çalıştırılıp yazılım güncelleştirmelerini dağıttığında, site için makine ilkesine bir dağıtım atama ilkesi eklenir. Yazılım güncelleştirmeleri, indirme konumundan, İnternetten veya paylaşılan ağ klasöründen, paket kaynağına indirilir. Yazılım güncelleştirmeleri, paket kaynağından site sunucusundaki içerik kitaplığına kopyalanır ve ardından dağıtım noktasındaki içerik kitaplığına kopyalanır.  

 Hedef koleksiyondaki istemci bir bilgisayar dağıtım için makine ilkesini alırsa, Yazılım Güncelleştirme İstemci Aracısı bir değerlendirme taraması başlatır. İstemci Aracısı, gerekli yazılım güncelleştirmelerinin içeriğini dağıtım için **Yazılım kullanılabilir zaman** ayarında yerel istemci önbelleğine yükler ve ardından yazılım güncelleştirmeleri yüklenmeye hazırdır. İsteğe bağlı dağıtımlardaki (yükleme sonra tarihi olmayan dağıtımlar) yazılım güncelleştirmeleri, kullanıcı yüklemeyi elle başlatana kadar yüklenmez.  

 Yapılandırılan son tarih geçtiğinde Yazılım Güncelleştirme İstemci Aracısı yazılım güncelleştirmelerinin hâlâ gerekli olduğunu doğrulamak üzere bir tarama yapar. Ardından istemci bilgisayardaki yerel önbelleği kontrol edere, yazılım güncelleştirme kaynak dosyalarının hâlâ mevcut olduğunu doğrular. Son olarak, istemci yazılım güncelleştirmelerini yükler. İçerik, başka bir dağıtıma yer açmak için istemci önbelleğinden silinmişse, istemci yazılım güncelleştirmelerini dağıtım noktasından istemci önbelleğine yeniden yükler. Yazılım güncelleştirmeleri, yapılandırılan maksimum istemci önbellek boyutundan bağımsız olarak, daima istemci önbelleğine yüklenir. Yükleme tamamlandığında, istemci aracısı yazılım güncelleştirmelerine artık ihtiyaç duyulmadığını doğrular ve ardından yönetim noktasına yazılım güncelleştirmelerinin artık istemciye yüklü olduğunu belirtmek üzere bir durum iletisi gönderir.  

### <a name="required-system-restart"></a>Gerekli sistem yeniden başlatması  
 Varsayılan olarak, yazılım güncelleştirmeleri gerekli bir dağıtımdan istemci bir bilgisayara yüklenirse ve yüklemenin tamamlanması için sistemin yeniden başlatılması gerekliyse sistem yeniden başlatılması gerçekleştirilir. Son tarihten önce yüklenen yazılım güncelleştirmelerinde, bilgisayar başka bir nedenle daha önce yeniden başlatılmadığı sürece, otomatik sistem yeniden başlatması son tarihe kadar ertelenir. Sistem yeniden başlatması, sunucular ve çalışma istasyonları için gizlenebilir. Bu ayarlar, Yazılım Güncelleştirmelerini Dağıt Sihirbazının veya Otomatik Güncelleştirme Kuralı Oluştur Sihirbazının **Kullanıcı Deneyimi** sayfasında yapılandırılır.  

### <a name="deployment-reevaluation-cycle"></a>Dağıtım yeniden değerlendirme döngüsü  
 Varsayılan olarak, istemci bilgisayarlar 7 günde bir dağıtım yeniden değerlendirme döngüsü başlatır. Bu değerlendirme döngüsü sırasında, istemci bilgisayar önceden dağıtılan ve yüklenen yazılım güncelleştirmelerini tarar. Kayıp yazılım güncelleştirmeleri varsa, yazılım güncelleştirmeleri yerel önbellekten yeniden yüklenir. Yerel önbellekte artık yazılım güncelleştirmesi mevcut değilse, dağıtım noktasından indirilir ve ardından yüklenir. Yeniden değerlendirme zamanlamasını site için istemci ayarlarındaki **Yazılım Güncelleştirmeleri** sayfasında yapılandırabilirsiniz.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a>Yazma filtreleri kullanan Windows Embedded cihazları için destek  
 Yazma filtresi etkinleştirilmiş Windows Katıştırılmış aygıtlara yazılım güncelleştirmesi dağıtırken, dağıtma sırasında aygıtta yazma filtresini devre dışı bırakıp bırakmamayı belirtebilir ve ardından dağıtım sonrasında aygıtı yeniden başlatabilirsiniz. Yazma filtresi devre dışı bırakılmamışsa, yazılım geçici bir katmana dağıtılır ve başka bir dağıtım değişikliklerin kalıcı olmasını zorlamazsa, yazılım aygıt yeniden başlatıldığında artık yüklü olmaz.  

> [!NOTE]  
>  Windows Katıştırılmış aygıtına bir yazılım güncelleştirmesi dağıttığınızda, aygıtın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun. Bu, yazma filtresinin ne zaman devre dışı ve etkin olduğunu ve aygıtın ne zaman yeniden başlatılacağını yönetmenizi sağlar.  

 Yazma filtresi davranışın denetleyen kullanıcı deneyimi ayarı, **Değişiklikleri son tarihte veya bakım pencerelerinde yürüt (yeniden başlatma gerektirir)** adlı bir onay kutusudur.  

 Yazma filtrelerini kullanan katıştırılmış cihazları Configuration Manager nasıl yönettiği hakkında daha fazla bilgi için bkz. [Windows Embedded cihazlarına istemci dağıtımını planlama](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Configuration Manager'da yazılım güncelleştirmelerini genişletme  
 Microsoft Update kullanılamayan yazılım güncelleştirmelerini yönetmek için System Center Updates Publisher kullanın. Yazılım güncelleştirmelerini güncelleştirme sunucusuna yayımladıktan ve Configuration Manager yazılım güncelleştirmelerini eşitledikten sonra, yazılım güncelleştirmelerini Configuration Manager istemcilerine dağıtabilirsiniz. Updates Publisher hakkında daha fazla bilgi için bkz. [Updates publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

## <a name="next-steps"></a>Sonraki adımlar
[Yazılım güncelleştirmelerini planlama](../plan-design/plan-for-software-updates.md)
