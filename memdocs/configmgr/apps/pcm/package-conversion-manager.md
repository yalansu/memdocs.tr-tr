---
title: Paket Dönüştürme Yöneticisi
titleSuffix: Configuration Manager
description: Paketleri Configuration Manager ' deki uygulamalara dönüştürmek için Paket Dönüştürme Yöneticisi hakkında bilgi edinin.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709918"
---
# <a name="package-conversion-manager"></a>Paket Dönüştürme Yöneticisi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1357861-->

Sürüm 1806 ' den başlayarak, Paket Dönüştürme Yöneticisi eski Configuration Manager paketleri uygulamalara dönüştürmenize yardımcı olur. Uygulamalar, bağımlılıklar, gereksinim kuralları, algılama yöntemleri ve Kullanıcı cihaz benzeşimi gibi ek avantajlara sahiptir.

> [!Tip]  
> Bu özellik ilk olarak sürüm 1806 ' de [yayın öncesi özelliği](../../core/servers/manage/pre-release-features.md)olarak sunulmuştur. Sürüm 1810 ' den başlayarak, bu özellik artık yayın öncesi bir özellik değildir.  


Bir Configuration Manager uygulama, istemci cihazlarına dağıttığınız dosya ve programları içerir. Ancak, eski paketlerin ve programların aksine, bir uygulama ek kullanıcı merkezli işlevsellik sağlar. Örneğin, bir uygulama bir yazılım paketinin, sanal bir uygulama paketinin veya mobil cihazlar için uygulamanın bir sürümünün yerel yüklemesi için dağıtım türleri içerebilir.

Daha fazla bilgi için aşağıdaki makalelere bakın: 
- [Uygulama yönetimine giriş](../understand/introduction-to-application-management.md)  
- [Paketler ve programlar](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Daha önce Package Conversion Manager 'ın daha eski bir sürümünü yüklediyseniz, önce sitenizi yükseltmeden önce bu sürümü kaldırın. Bu tümleşik sürüm yükleme gerektirmez, ancak var olan sürümlerle çakışabilir.  

Paket Dönüştürme Yöneticisi 'nin Bu tümleşik sürümü, Configuration Manager geçerli şube sitesindeki paketler üzerinde çalışmaktadır. Tek başına bir araç değildir. Configuration Manager eski bir sürümünde paketler ve programlarınız varsa, önce paketleri geçerli şube sitenize geçirin. Daha fazla bilgi için bkz. [hiyerarşiler arasında veri geçirme](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager sürüm 1902 aşağıdaki geliştirmeleri içerir:
- Zamanlanan paket analizi varsayılan olarak 7 günde bir çalışır
- Paketleri çözümlemek ve dönüştürmek için PowerShell cmdlet 'leri
- Genel hata düzeltmeleri ve geliştirmeleri



## <a name="planning"></a>Planlama

Paketleri uygulamalara dönüştürmeye başlamadan önce, önce bir plan geliştirin. Aşağıdaki işlem örnek bir plandır:

- [Ayrıntılı paket dönüştürme planı tanımlama](#bkmk_define)  

- [Paketleri dönüştürme için seçin ve hazırlayın](#bkmk_prepare)  

- [Test paketlerini seçin](#bkmk_test)  

- [Paketleri analiz edin, araştırın ve dönüştürün](#bkmk_analyze)  

- [Uygulamaları test etme ve dağıtma](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a>Ayrıntılı paket dönüştürme planı tanımlama

Bu bölümde, iki örnek paket dönüştürme planı açıklanmaktadır:  

- [Yüksek kaynak test ortamı](#bkmk_define-high): üretim ortamınızı tamamen çoğaltmak için kaynaklar, izinler ve mimari içeren bir test ortamınız vardır.  

- [Sınırlı kaynak test ortamı](#bkmk_define-limited): üretim ortamınızı tamamen çoğaltan bir test ortamınız yok.  

Bu planları ortamınıza özgü diğer sorunlar için gereken şekilde ayarlayın.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a>Yüksek kaynak sınama ortamı için örnek plan

Test ortamınızda, üretim ortamınıza benzer kaynaklar, izinler ve mimari bulunur. Tüm paketlerinizi etkili bir şekilde çözümlemek ve dönüştürmek için test ortamını kullanın ve ardından tüm Configuration Manager uygulamalarınızı test edin. Bu işi tamamladıktan sonra üretim ortamına aktarın. 

Paket dönüştürme planınız aşağıdaki adımlara benzer olabilir:  

1.  Dönüştürmek istediğiniz paketleri seçin.  

2.  Paketleri test ortamınıza dönüştürmek için geçirin.  

3.  Paketleri dönüştürme için hazırlayın.  

4.  Test paketlerini seçin.  

5.  Test paketlerini çözümleyin, araştırın ve dönüştürün.  

6.  Dönüştürülen uygulamaları test edin.  

7.  Kalan (test olmayan) paketleri çözümleyin ve dönüştürün.  

8.  Uygulamaları test ortamından dışarı aktarın. Bunları üretim ortamınıza içeri aktarın.  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a>Sınırlı kaynak sınama ortamı için örnek plan

Test ortamınız, üretim ortamınıza benzer kaynak, izin ve mimariye sahip değildir. Paketlerinizi analiz edebilir, test edebilir ve dönüştüremezsiniz. Bu senaryoda, yalnızca test paketlerinizi çözümleyin, araştırın, dönüştürün ve test edin. Ardından, geri kalan paketleri analiz etmek ve dönüştürmek için üretim ortamına geçirin. 

Paket dönüştürme planınız aşağıdaki adımlara benzer olabilir:

1.  Dönüştürmek istediğiniz paketleri seçin.  

2.  Test paketlerini seçin.  

3.  Test paketlerini test ortamınıza geçirin.  

4.  Test paketlerini dönüştürme için hazırlayın.  

5.  Test paketlerini çözümleyin, araştırın ve dönüştürün.  

6.  Dönüştürülen uygulamaları test edin.  

7.  Test uygulamalarını test ortamından dışarı aktarın. Ardından bunları üretim ortamınıza içeri aktarın.  

8.  Kalan paketleri üretim ortamına geçirin ve dönüştürme için hazırlayın.  

9.  Üretim ortamında kalan paketleri çözümleyin, araştırın ve dönüştürün.  

10. Kalan uygulamaları üretim ortamında yayınlayın.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a>Paketleri dönüştürme için seçin ve hazırlayın

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a>Dönüştürmek istediğiniz paketleri seçin

Tüm paketlerin uygulamalara dönüştürülmesi uygun değildir. Paketleri dönüştürmeye başlamadan önce, dönüştürülmeyecek paketleri tanımla. 

Uygulamalara dönüştürme için en iyi paket türleri, kullanıcıya yönelik yazılımları içerir, örneğin:  

- Windows Installer dosyaları (. msi ve. msu)  

- Microsoft Application Virtualization (App-V) programları  

- Windows yürütülebilir dosyaları (. exe)  

Paketler olarak en iyi şekilde tutulan ve uygulamalara dönüştürülmeyen paket türleri şunlardır:

- Sistem bakım araçları. Örneğin, betikler veya yedekleme yardımcı programları.  

- Desteklemeyen yazılımın paketleri.

> [!Tip]  
> Uygulamalara dönüştürme için uygun olmayan paketleri tanımladıktan sonra, Configuration Manager konsolundaki ayrı bir klasöre taşıyın. Configuration Manager konsolunda bir paket klasörü oluşturmak için:  
> - **Paketler** düğümüne sağ tıklayın.  
> - **Klasörler**' i seçin ve ardından **klasör oluştur**' u seçin.  
> - Klasör adını girin, örneğin `Not Converted`.  
> - **Tamam**'a tıklayın.  

#### <a name="prepare-the-packages-for-conversion"></a>Paketleri dönüştürme için hazırlama

Dönüştürmek istediğiniz her paket için aşağıdaki koşullara uydıklarından emin olun:  

- Kaynak dosyalarının konumu, örneğin `\\Server\Share\File`tam bir UNC yoludur.  

- Windows Installer dosyalar yalnızca bir benzersiz ürün kodu kullanır.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a>Test paketlerini seçin

Mümkünse, test paketleri grubunuz aşağıdaki ölçütlere uyan paketleri içermelidir:  

- **Otomatik**hazırlık durumuna sahip en az bir test paketi.  

- Hazır olma durumu **el ile**olan en az bir test paketi.  

İdeal olarak, test paketleriniz çekirdek paketler olmalıdır, örneğin:  

- İyi bildiğiniz paketler.  

- Kuruluşunuz için en önemli olan paketler.  

- En kolay test edebileceğiniz paketler.  

Test için uygun olan paketleri belirler. Sonra Configuration Manager konsolundaki ayrı bir klasöre taşıyın.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a>Paketleri analiz edin, araştırın ve dönüştürün

#### <a name="analyze-packages"></a>Paketleri çözümle

Tek bir paketi veya küçük bir grubu çözümlemek için Configuration Manager konsolunda tümleşik Paket Dönüştürme Yöneticisi ' ni kullanın. Daha fazla bilgi için bkz. [paketleri çözümleme ve dönüştürme](how-to-analyze-and-convert.md).  

> [!NOTE]  
> **İzleme** çalışma alanındaki **paket dönüştürme durumu** düğümüne bakın. Analiz ve dönüştürme işlemleriyle ilgili özet bilgiler görüntüler.  

#### <a name="investigate-analysis-results"></a>Analiz sonuçlarını araştır

Test paketlerini analiz ettikten sonra, hazırlık durumu **el ile** veya **hata**olan paketleri araştırın. Bu duruma sahip oldukları nedenleri saptayın. **El ile** veya **hata** hazırlık durumunun bazı yaygın nedenleri şunlardır:

- Paket, bir uygulama dağıtım türünde bir algılama yöntemi oluşturmak için gereken bilgileri içermez.  

- Paket, koleksiyonları genel koşullara ve gereksinimlere dönüştürmek için gereken bilgileri içermez.  

- Pakette birden fazla program var.  

- Paket, uygulamaya dönüştürmemiş başka bir pakete bağımlıdır.  

Daha fazla bilgi için aşağıdaki kaynakları kullanın:  

- [Paket Dönüştürme Yöneticisi hata iletileri Için Teknik başvurudaki](error-messages.md) hata iletilerini ve düzeltmeleri gözden geçirin  

- **PCMtrace. log** günlük dosyasını gözden geçirin  

- [Paket Dönüştürme Yöneticisi sorunlarını giderme](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>Paketleri Dönüştür

Paketlerin nasıl dönüştürüleceği hakkında daha fazla bilgi için bkz. [paketleri çözümleme ve dönüştürme](how-to-analyze-and-convert.md).

> [!NOTE]  
> **İzleme** çalışma alanındaki **paket dönüştürme durumu** düğümüne bakın. Analiz ve dönüştürme işlemleriyle ilgili özet bilgiler görüntüler.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a>Uygulamaları test etme ve dağıtma

Uygulamaları, test ortamınızda veya üretim ortamınızda, ayrıntılı paket dönüştürme planınıza göre test edin.



## <a name="recommendations"></a>Öneriler

- **İzleme** çalışma alanındaki **paket dönüştürme durumu** düğümünü kullanın. Analiz ve dönüştürme işlemleriyle ilgili özet bilgiler görüntüler.  

- Paketinizdeki sarmalayıcılar olarak bilinen programları araştırın. İşlevlerini eşdeğer Configuration Manager işlevselliğine dönüştürmek için Paket Dönüştürme Yöneticisi eklentisini kullanın.  

- Bir üretim ortamında dağıtmadan önce, dönüştürülmüş her uygulamayı iyice test edin.  



## <a name="next-steps"></a>Sonraki adımlar

[Paketleri analiz etme ve dönüştürme](how-to-analyze-and-convert.md)
