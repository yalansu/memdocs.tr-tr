---
title: Endpoint Protection istemci sık sorulan sorular
titleSuffix: Configuration Manager
description: Windows Defender ve Endpoint Protection hakkında sık sorulan soruların yanıtlarını alın.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b89f2dd9f60b43db5c4ce8956f843429b47bc62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724373"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Endpoint Protection istemci sık sorulan sorular

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Bu SSS, yönetilen bilgisayarlarına BT yöneticisi tarafından Windows Defender veya Endpoint Protection dağıtılan bilgisayar kullanıcıları içindir. Buradaki içerik diğer kötü amaçlı yazılımdan koruma yazılımlarına uygulanmayabilir. Microsoft System Center Endpoint Protection Windows 10 ' da Windows Defender 'ı yönetir. Ayrıca, Windows 10 ' dan önceki Endpoint Protection istemcisini bilgisayarlara dağıtabilir ve yönetebilir. Bu makalede Windows Defender açıklanıyor olsa da, bu bilgiler Endpoint Protection için de geçerlidir.  

-   [Virüsten koruma yazılımına ve casus yazılıma neden ihtiyacım var?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Bilgisayarıma kötü amaçlı yazılım bulaşıp bulaşmadığını nasıl anlarım?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Windows Defender 'ın sürümünü nasıl bulabilirim?](#how-can-i-find-the-version-of-windows-defender)
-   [Windows Defender veya Endpoint Protection bilgisayarımda kötü amaçlı yazılım algıladığında ne yapmalıyım?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [Virüs nedir?](#what-is-a-virus)  
-   [Casus yazılım nedir?](#what-is-spyware)  
-   [Virüsler, casus yazılım ve diğer olası zararlı yazılımlar arasındaki fark nedir?](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Virüsler, casus yazılımlar ve diğer olası istenmeyen yazılımlar nereden gelir?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Bilmeden kötü amaçlı yazılım alabilir miyim?](#can-i-get-malicious-software-without-knowing-it)  
-   [Yazılım yüklemeden önce lisans sözleşmelerini gözden geçirmek neden önemlidir?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Endpoint Protection ve Windows Defender arasındaki fark nedir?](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Windows Defender tanımlama bilgilerini neden algılamıyor?](#why-doesnt-windows-defender-detect-cookies)  
-   [Kötü amaçlı yazılımları nasıl önleyebilirim?](#how-can-i-prevent-malware)  
-   [Virüs ve casus yazılım tanımları nelerdir?](#what-are-virus-and-spyware-definitions)  
-   [Virüs ve casus yazılım tanımlarının güncelliğini nasıl korurum?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Windows Defender veya Endpoint Protection tarafından karantinaya alınan öğeler Nasıl yaparım? kaldırmak veya geri yüklemek mi istiyorsunuz?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [Gerçek zamanlı koruma nedir?](#what-is-real-time-protection)  
-   [Bilgisayarımda Windows Defender veya Endpoint Protection’ın çalıştığını nasıl anlarım?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Windows Defender veya Endpoint Protection uyarılarını ayarlama](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>Virüsten koruma yazılımına ve casus yazılıma neden ihtiyacım var?  

 Bilgisayarınızda kötü amaçlı yazılımlardan koruma yazılımının çalıştığından emin olmak önemlidir. Virüsler, casus yazılımlar veya istenmeyebilecek yazılımları içeren kötü amaçlı yazılımlar, İnternet'e bağlandığınız zaman kendilerini bilgisayarınıza yüklemeyi deneyebilirler. Ayrıca bir CD, DVD veya diğer çıkarılabilir medya kullanarak bir program yüklediğinizde bilgisayarınıza bulaşabilir. Kötü amaçlı yazılımlar yalnızca yüklendiğinde değil beklenmeyen zamanlarda çalışmak için de programlanabilir.  

 Windows Defender veya Endpoint Protection kötü amaçlı yazılımların bilgisayarınıza bulaşmasını önlemeye yardımcı olmak için üç yol sunar:  

-   **Gerçek zamanlı koruma kullanma** -gerçek zamanlı koruma, Windows Defender 'ın bilgisayarınızı her zaman izlemelerine ve virüsler, casus yazılım veya diğer istenmeyebilecek yazılımlar dahil kötü amaçlı yazılımlar kendilerini yüklemeyi veya bilgisayarınızda çalışmayı denediğinde sizi uyarmasını sağlar. Daha sonra Windows Defender yazılımı askıya alır ve yazılım ile ilgili önerisini uygulamanızı veya alternatif bir eylem gerçekleştirmenizi sağlar.

-   **Tarama seçenekleri** -bilgisayarınızı riske koyabilecek virüsler, casus yazılım ve diğer kötü amaçlı yazılımlar gibi olası tehditleri taramak Için Windows Defender 'ı kullanabilirsiniz. Düzenli olarak taramalar zamanlamak ve bir tarama sırasında algılanan kötü amaçlı yazılımları kaldırmak için de kullanabilirsiniz.  

-   **Microsoft etkin koruma hizmeti Community** -çevrimiçi Microsoft etkin koruma hizmeti topluluğu, henüz riskler için sınıflandırılmamış yazılımlara diğer kişilerin nasıl yanıt verdiğini görmenizi sağlar. Bu bilgileri bilgisayarınızda bu yazılıma izin verip vermemeye karar verirken kullanabilirsiniz. Aynı zamanda, katılırsanız, seçimleriniz diğer kişilerin ne yapacaklarına karar vermelerine yardımcı olmak üzere topluluk derecelendirmelerine eklenir.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Bilgisayarıma kötü amaçlı yazılım bulaşıp bulaşmadığını nasıl anlarım?  

 Aşağıdaki durumlarda bilgisayarınızda virüsler, casus yazılım veya diğer istenmeyebilecek yazılımları içeren kötü amaçlı yazılım çeşitleri olabilir:  

-   Web tarayıcınıza bilerek eklemediğiniz yeni araç çubukları, bağlantılar veya sık kullanılanlar fark ederseniz.  

-   Giriş sayfanız, fare imleciniz veya arama programınız beklenmedik bir şekilde değişirse.  

-   Bir arama motoru gibi belirli bir sitenin adresini yazıyorsanız ancak bildirimde bulunulmaksızın başka bir Web sitesine yönlendiriliyorsanız.  

-   Dosyalar bilgisayarınızdan otomatik olarak siliniyorsa.  

-   Bilgisayarınız diğer bilgisayarlara saldırmak için kullanılıyorsa.  

-   İnternet'te olmadığınız halde açılır reklamlar görüntüleniyorsa.  

-   Bilgisayarınız aniden normalden daha yavaş çalışmaya başladıysa. Tüm bilgisayar performans sorunları kötü amaçlı yazılımlardan kaynaklanmaz, ancak kötü amaçlı yazılımlar, özellikle casus yazılımlar, fark edilebilir bir değişikliğe neden olabilir.  

Hiç belirti görmeseniz bile bilgisayarınızda kötü amaçlı yazılımlar olabilir. Bu tür yazılımlar bilginiz veya izniniz olmadan siz ve bilgisayarınızla ilgili bilgiler toplayabilir. Gizliliğinizin ve bilgisayarınızın korunmasına yardımcı olmak için Windows Defender veya Endpoint Protection’ı her zaman çalıştırmalısınız.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Windows Defender 'ın sürümünü nasıl bulabilirim?
 Bilgisayarınızda çalışan Windows Defender sürümünü görüntülemek için Windows Defender 'ı açın ( **Başlat** ' a tıklayın ve ardından **Windows Defender**için arama yapın), **Ayarlar**' a tıklayın ve Windows Defender ayarlarının en altına kaydırarak **sürüm bilgilerini**bulun.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>Windows Defender veya Endpoint Protection bilgisayarımda kötü amaçlı yazılım algıladığında ne yapmalıyım?  

 Windows Defender bilgisayarınızda kötü amaçlı yazılım veya olası istenmeyen yazılımlar algılarsa (gerçek zamanlı koruma kullanarak bilgisayarınızı izlerken veya bir tarama çalıştırdıktan sonra), ekranınızın sağ alt köşesinde bir bildirim iletisi görüntüleyerek algılanan öğeyi size bildirir.  

 Bildirim iletisinde bir **Bilgisayarı temizle** düğmesi ve algılanan öğe hakkında ek bilgiler görüntülemenizi sağlayan **Ayrıntıları göster** bağlantısı bulunur. **Olası tehdit ayrıntıları** penceresini açmak ve algılanan öğe hakkında ek bilgileri görüntülemek için **Ayrıntıları göster** bağlantısına tıklayın. Artık öğeye hangi eylemin uygulanacağını seçebilir veya **Bilgisayarı temizle**’ye tıklayabilirsiniz. Algılanan öğeye uygulanacak eylemi saptarken yardıma gerek duyarsanız, size yol göstermesi için Windows Defender tarafından öğeye atanan uyarı düzeyini kullanın (daha fazla bilgi için bkz. Uyarı düzeylerini anlama).  

 Uyarı düzeyleri virüslere, casus yazılımlara ve diğer olası istenmeyen yazılımlara ne yanıt vereceğinizi seçmenize yardımcı olur. Windows Defender tüm virüsleri ve casus yazılımları kaldırmanızı önerecektir, ancak işaretlenen yazılımların tümü kötü amaçlı veya istenmeyen yazılım değildir. Aşağıdaki bilgiler, Windows Defender bilgisayarınızda olası istenmeyen yazılımlar saptarsa ne yapacağınıza karar vermenize yardımcı olabilir.  

 Uyarı düzeyine bağlı olarak, algılanan öğeye uygulamak üzere aşağıdaki eylemlerden birini seçebilirsiniz:  

- **Kaldır** -bu eylem, yazılımı bilgisayarınızdan kalıcı olarak siler.  

- **Karantinaya** alma-Bu eylem, yazılımın çalışması için yazılım tarafından karantinaya alınır. Windows Defender yazılımı karantinaya aldığında, bilgisayarınızda başka bir konuma taşır ve ardından siz bunu geri yüklemeyi veya bilgisayarınızdan kaldırmayı seçene kadar yazılımın çalıştırılmasını önler.  

- **Izin ver** -bu eylem, yazılımı Windows Defender izin verilenler listesine ekler ve bilgisayarınızda çalışmasına izin verir. Windows Defender, yazılımın gizliliğinizde veya bilgisayarınızda neden olabileceği riskler konusunda sizi uyarmayı durdurur.  

  Öğelerden biri, örneğin bir yazılım için **İzin Ver** ’i seçerseniz, Windows Defender yazılımın gizliliğinizde veya bilgisayarınızda neden olabileceği riskler konusunda sizi uyarmayı durdurur. Bu nedenle, yazılımı izin verilenler listenize eklemeden önce yazılıma ve yazılımın yayımcısına güvendiğinizden emin olun.  

### <a name="how-to-remove-potentially-harmful-software"></a>Zararlı olabilecek yazılımları kaldırma

Windows Defender’ın algıladığı tüm istenmeyen veya potansiyel olarak zararlı öğeleri hızlı bir şekilde ve kolayca kaldırmak için **Bilgisayarı temizle** seçeneğini kullanın.  

1.  Olası tehditler algılandıktan sonra Bildirimler alanında görüntülenen bildirim iletisini gördüğünüzde, **Bilgisayarı temizle**’ye tıklayın.  

2.  Windows Defender olası tehdidi (veya tehditleri) kaldırır ve bilgisayarınızı temizleme işlemi tamamlandığında size bildirir.  

3.  Algılanan tehditler hakkında daha fazla bilgi edinmek için **Geçmiş** sekmesine tıklayın ve ardından **Algılanan tüm öğeler**’i seçin.  

4.  Algılanan tüm öğeleri görmüyorsanız, **Ayrıntıları görüntüle**’ye tıklayın. Yönetici parolası veya onay istenirse parolayı yazın ya da eylemi onaylayın.

> [!NOTE]  
>  Bilgisayarı temizleme sırasında mümkün olduğunda, Windows Defender dosyaların tamamını değil, yalnızca virüslü bölümünü kaldırır.  

##  <a name="what-is-a-virus"></a>Virüs nedir?  
 Bilgisayar virüsleri, bilgisayar işlemlerine engel olmak, verileri kaydetmek, bozmak veya silmek ya da İnternet üzerinden diğer bilgisayarlara bulaşmak için özellikle tasarlanmış yazılım programlarıdır. Virüsler genellikle sistemi yavaşlatır ve başka sorunlara neden olur.  

##  <a name="what-is-spyware"></a> Casus yazılım nedir?  
 Casus yazılım izninizi almadan veya yeterli bildirim ya da denetim sağlamadan bilgisayarınızda kendi kendini yükleyebilen veya çalıştırabilen yazılımdır. Casus yazılım bilgisayarınıza bulaştıktan sonra belirti göstermeyebilir, ancak birçok kötü amaçlı veya istenmeyen program bilgisayarınızın nasıl çalıştığını etkileyebilir. Örneğin, casus yazılım çevrimiçi davranışlarınızı izleyebilir veya hakkınızda bilgi toplayabilir (sizi kişisel olarak tanımlayabilen bilgiler ve diğer hassas bilgiler dahil), bilgisayarınızdaki ayarları değiştirebilir veya bilgisayarınızın yavaş çalışmasına neden olabilir.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a> Virüsler, casus yazılım ve diğer zararlı yazılımlar arasındaki fark nedir?  
 Virüsler ve casus yazılımlar bilgisayarınıza bilginiz dışında yüklenir ve ikisi de izinsiz ve zararlı olma olasılığına sahiptir. Ayrıca bilgisayarınızdaki bilgileri ele geçirebilir ve bu bilgilere zarar verebilir veya bilgileri silebilirler. Her ikisi de bilgisayarınızın performansını olumsuz etkileyebilir.  

 Virüs ve casus yazılım arasındaki temel farklar bilgisayarınızdaki davranış biçimleridir. Virüsler, canlı organizmalar gibi, bir bilgisayara bulaşmak, çoğalmak ve ardından mümkün olduğunca çok bilgisayara bulaşmak ister. Ancak casus yazılım, bir Mole gibidir. Bu, bilgisayarınızda "gezinmek" ve mümkün olduğunca uzun süre kalmak ve bu sırada bilgisayarınız hakkında değerli bilgiler göndermek istiyor.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>Virüsler, casus yazılımlar ve diğer olası istenmeyen yazılımlar nereden gelir?  
 Virüsler gibi istenmeyen yazılımlar Web siteleri veya indirdiğiniz ya da bir CD, DVD, harici sabit disk veya bir cihaz kullanarak yüklediğiniz programlar tarafından yüklenebilir. Casus yazılımlar en yaygın olarak dosya paylaşımı, ekran koruyucular veya arama araç çubukları gibi ücretsiz yazılımlar aracılığıyla yüklenir.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a> Farkında olmadan kötü amaçlı yazılımdan etkilenebilir miyim?  
 Evet, bazı kötü amaçlı yazılımlar bir Web sayfasındaki katıştırılmış betik veya program aracılığıyla bir Web sitesinden yüklenebilir. Bazı kötü amaçlı yazılımlar yüklenmek için yardımınızı gerektirir. Bu yazılımlar indirilebilir bir dosyayı kabul etmenizi gerektiren Web açılır pencereleri veya ücretsiz yazılımlar kullanır. Ancak, Microsoft Windows®’u güncel tutar ve güvenlik ayarlarını azaltmazsanız, bulaşma riskini en aza indirebilirsiniz.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a> Yazılım yüklemeden önce lisans sözleşmelerini gözden geçirmek neden önemlidir?  
 Web sitelerini ziyaret ettiğinizde, sitenin sunduğu her şeyi otomatik olarak indirmeyi kabul etmeyin. Dosya paylaşım programları veya ekran koruyucuları gibi ücretsiz yazılımları yüklerseniz, lisans sözleşmesini dikkatlice okuyun. Şirketten reklamlar ve açılır pencereleri kabul etmenizi zorunlu tutan veya yazılımın belirli bilgileri yazılım yayımcısına göndereceğini belirten yan tümceleri arayın.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a> Endpoint Protection ve Windows Defender arasındaki fark nedir?  
 Endpoint Protection kötü amaçlı yazılımdan koruma yazılımıdır, yani virüsler, casus yazılım ve diğer istenmeyebilecek yazılımlar dahil çeşitli kötü amaçlı yazılımları algılamak ve bilgisayarınızı bunlara karşı korumak için tasarlanmıştır. Windows işletim sisteminizle otomatik olarak yüklenen Windows Defender, casus yazılımı algılayan ve durduran yazılımdır.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Windows Defender tanımlama bilgilerini neden algılamıyor?  
 Tanımlama bilgileri, Web sitelerinin siz ve tercihleriniz hakkında bilgi depolamak için bilgisayarınıza yerleştirdiği küçük metin dosyalarıdır. Web siteleri, size kişiselleştirilmiş bir deneyim sunmak ve Web sitesi kullanımı hakkında bilgi toplamak için tanımlama bilgilerini kullanır. Windows Defender, gizlilik veya bilgisayarınızın güvenliğine yönelik bir tehdit görmediğinden, tanımlama bilgilerini algılamaz. Çoğu Internet tarayıcı programı tanımlama bilgilerini engellemenize olanak tanır.  

##  <a name="how-can-i-prevent-malware"></a> Kötü amaçlı yazılımları nasıl önleyebilirim?  
 Günümüzde bilgisayar kullanıcıları için en önemli konulardan ikisi virüsler ve casus yazılımlardır. İki durumda da, bunlar bir sorun olabilir, ancak biraz planlamayla kendinizi kolayca savunabilirsiniz:  

-   Bilgisayarınızın yazılımını güncel tutun ve tüm düzeltme eklerini yüklemeyi unutmayın. İşletim sisteminizi düzenli olarak güncelleştirmeyi unutmayın.  

-   Virüsten koruma ve casus yazılımdan koruma yazılımınız Windows Defender’ın olası tehditlere karşı en yeni güncelleştirmeleri kullandığından emin olun (bkz. Virüs ve casus yazılım tanımlarının güncelliğini nasıl korurum?). Ayrıca her zaman Windows Defender’ın en yeni sürümünü kullandığınızdan emin olun.  

-   Yalnızca güvenilir kaynaklardan güncelleştirmeleri yükleyin. Windows işletim sistemleri için her zaman [Microsoft Update](https://go.microsoft.com/fwlink/?LinkID=96304) gidin (https://go.microsoft.com/fwlink/?LinkID=96304) ve diğer yazılımlar için şirketin veya onu oluşturan kişinin meşru Web sitelerini kullanın.  

-   Ek içeren bir e-posta aldıysanız ve kaynağından emin değilseniz, e-postayı hemen silmeniz gerekir. Bilinmeyen kaynaklardan uygulama veya dosya indirmeyin ve diğer kullanıcılarla Ticari dosyalar olduğunda dikkatli olun.  

-   Bir güvenlik duvarı yükleyin ve kullanın. Windows Güvenlik Duvarı'nı etkinleştirmeniz önerilir.  

##  <a name="what-are-virus-and-spyware-definitions"></a> Virüs ve casus yazılım tanımları nedir?  
 Windows Defender veya Endpoint Protection kullandığınızda, virüs ve casus yazılım tanımlarının güncel olması önemlidir. Tanımlar sürekli büyüyen bir olası yazılım tehditleri ansiklopedisi gibi davranan dosyalardır. Windows Defender veya Endpoint Protection algıladığı yazılımların virüs, casus yazılım veya diğer istenmeyebilecek yazılım olup olmadığını belirlemek ve ardından, olası risklere karşı sizi uyarmak için tanımları kullanır. Tanımları güncel tutmaya yardımcı olmak için, Windows Defender veya Endpoint Protection yeni tanımları kullanıma sunulduklarında otomatik olarak yüklemek için Microsoft Update ile çalışır. Windows Defender veya Endpoint Protection’ı taramadan önce güncelleştirilmiş tanımları çevrimiçi olarak denetlemek için de ayarlayabilirsiniz.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>Virüs ve casus yazılım tanımlarının güncelliğini nasıl korurum?  
 Virüs ve casus yazılım tanımları virüsler, casus yazılım ve diğer istenmeyebilecek yazılımlar dahil olmak üzere bir bilinen kötü amaçlı yazılımlar ansiklopedisi gibi davranan dosyalardır. Kötü amaçlı yazılımlar sürekli geliştirildiği için, Windows Defender veya Endpoint Protection yüklenmeye, çalıştırılmaya veya bilgisayarınızdaki ayarları değiştirmeye çalışan yazılımın bir virüs, casus yazılım veya istenmeyebilecek başka bir yazılım olup olmadığını belirlemek için güncel tanımları kullanır.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Zamanlanan taramalardan önce yeni tanımları otomatik olarak denetlemek için (önerilir)  

1.  Bildirim alanındaki simgeye tıklayarak veya **Başlat** menüsünden başlatarak Windows Defender veya Endpoint Protection istemcisini açın.  

2.  **Ayarlar**’a tıklayın ve ardından **Zamanlanan tarama**’ya tıklayın.  

3.  **Zamanlanan taramaları çalıştırmadan önce en yeni virüs ve casus yazılım tanımlarını denetle** onay kutusunun seçili olduğundan emin olun ve ardından **Değişiklikleri kaydet**’e tıklayın. Yönetici parolası veya onay istenirse parolayı yazın ya da eylemi onaylayın.  

### <a name="to-check-for-new-definitions-manually"></a>Yeni tanımları elle denetlemek için

 Windows Defender veya Endpoint Protection bilgisayarınızda virüs ve casus yazılım tanımlarını otomatik olarak güncelleştirir. Tanımlar yedi günden daha fazla süre boyunca güncellenmemişse (örneğin, bilgisayarınızı bir hafta boyunca açmadıysanız), Windows Defender veya Endpoint Protection, Tanımlarınızın güncel olmadığını size bildirir.  

1.  Bildirim alanındaki simgeye tıklayarak veya **Başlat** menüsünden başlatarak Windows Defender veya Endpoint Protection istemcisini açın.  

2.  Yeni tanımları elle denetlemek için, **Güncelleştir** sekmesine tıklayın ve ardından **Tanımları güncelleştir**’e tıklayın.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a> Windows Defender veya Endpoint Protection tarafından karantinaya alınan öğeleri nasıl kaldırabilirim veya geri yükleyebilirim?  

 Windows Defender veya Endpoint Protection yazılımı karantinaya aldığında, yazılımı bilgisayarınızda başka bir konuma taşır ve ardından siz bunu geri yüklemeyi veya bilgisayarınızdan kaldırmayı seçene kadar yazılımın çalıştırılmasını önler.  

 Bu yordamda bahsedilen tüm adımlar için, yönetici parolası veya onay istenirse parolayı yazın ya da onay sağlayın.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Windows Defender veya Endpoint Protection tarafından karantinaya alınan öğeleri kaldırma veya geri yükleme


1.  **Geçmiş** sekmesine tıklayın, **Karantinaya alınan öğeler**’i seçin ve ardından **Karantinaya alınan öğeler** seçeneğini belirleyin.  

2.  Tüm öğeleri görmek için **Ayrıntıları görüntüle** ’ye tıklayın.  

3.  Her bir öğeyi gözden geçirin ve ardından her biri için **Kaldır** veya **Geri yükle**’ye tıklayın. Karantinaya alınan tüm öğeleri bilgisayarınızdan kaldırmak istiyorsanız **Tümünü kaldır**’a tıklayın.  

##  <a name="what-is-real-time-protection"></a>Gerçek zamanlı koruma nedir?  

 Gerçek zamanlı koruma, Windows Defender’ın bilgisayarınızı sürekli olarak izleyerek virüsler ve casus yazılım gibi olası tehditler kendilerini yüklemeyi veya bilgisayarınızda çalışmayı denediğinde sizi uyarmasını sağlar. Bu özellik Windows Defender’ın bilgisayarınızın korunmasına yardımcı olması için önemli bir öğe olduğundan, gerçek zamanlı korumanın her zaman açık olduğundan emin olun. Gerçek zamanlı koruma devre dışı bırakılırsa, Windows Defender size bildirir ve bilgisayarınızın durumunu **riskli**olarak değiştirir.  

 Gerçek zamanlı koruma bir tehdit veya olası tehdit algıladığında, Windows Defender bir bildirim görüntüler. Artık aşağıdaki seçeneklerden birini belirtebilirsiniz:  

- Algılanan öğeyi kaldırmak için **Bilgisayarı temizle** ’ye tıklayın. Windows Defender, öğeyi bilgisayarınızdan otomatik olarak kaldırır.  

- Olası tehdit ayrıntıları penceresini görüntülemek için **Ayrıntıları göster** bağlantısına tıklayın ve ardından algılanan öğeye uygulanacak eylemi seçin.  

  Windows Defender’ın izlemesini istediğiniz yazılım ve ayarları seçebilirsiniz, ancak gerçek zamanlı korumayı açmanızı ve tüm gerçek zamanlı koruma seçeneklerini belirlemenizi öneririz. Aşağıdaki tabloda kullanılabilir seçenekler açıklanmaktadır.  

|||  
|-|-|  
|**Gerçek zamanlı koruma seçeneği**|**Amaç**|  
|Tüm indirmeleri tara|Bu seçenek Windows Internet Explorer ve Microsoft Outlook® Express aracılığıyla otomatik olarak indirilen dosyalar dahil ActiveX® denetimleri ve yazılım yükleme programları gibi indirilen dosya ve programları izler. Bu dosyalar tarayıcı tarafından indirilebilir, yüklenebilir veya çalıştırılabilir. Bu dosyalarda virüsler, casus yazılım ve diğer istenmeyebilecek yazılımlar dahil kötü amaçlı yazılımlar bulunabilir ve bunlar bilginiz dışında yüklenebilir.<br /><br /> Gerçek zamanlı koruma seçeneğini kullandığınızda, Windows Defender bilgisayarınızı sürekli olarak izler ve indirmiş olabileceğiniz herhangi bir kötü amaçlı dosya veya program için denetler. Bu izleme özelliği, Windows Defender’ın indirmek isteyebileceğiniz dosya ve programların denetlenmesini gerektirerek gözatma veya e-posta deneyiminizi yavaşlatmayı gerektirmeyeceği anlamına gelir.|  
|Bilgisayarınızdaki dosya ve program etkinliğini izleme|Bu seçenek bilgisayarınızda çalışmaya başlayan dosya ve programları izler ve gerçekleştirdikleri ve bunlar üzerinde gerçekleştirilen işlemler hakkında sizi uyarır. Kötü amaçlı yazılımlar bilginiz dışında kötü amaçlı veya istenmeyen yazılımları çalıştırmak için yüklediğiniz programlardaki güvenlik açıklarını kullanabileceğinden bu önemlidir. Örneğin, sık kullandığınız bir programı başlattığınızda, casus yazılım kendisini arka planda çalıştırabilir. Windows Defender, programlarınızı izler ve şüpheli etkinlik algılarsa sizi uyarır.|  
|Davranış izlemeyi etkinleştir|Bu seçenek, geleneksel virüsten koruma algılama yöntemleri tarafından algılanmayabilen şüpheli desenler için davranış koleksiyonlarını izler.|  
|Ağ Denetleme Sistemi'ni Etkinleştir|Bu seçenek bilgisayarınızı bilinen güvenlik açıklarına karşı korumaya yardımcı olur. Bu, bir güvenlik açığının süresi ve bir güncelleştirmenin uygulanması arasındaki süreyi azaltır.|  

### <a name="to-turn-off-real-time-protection"></a>Gerçek zamanlı korumayı devre dışı bırakma  

1.  **Ayarlar**’a tıklayın ve ardından **Gerçek zamanlı koruma**’ya tıklayın.  

2.  Devre dışı bırakmak istediğiniz gerçek zamanlı koruma seçeneklerini temizleyin ve ardından **Değişiklikleri kaydet**’e tıklayın. Yönetici parolası veya onay istenirse parolayı yazın ya da eylemi onaylayın.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>Bilgisayarımda Windows Defender veya Endpoint Protection’ın çalıştığını nasıl anlarım?  

 Bilgisayarınızda Windows Defender'ı yükledikten sonra ana pencereyi kapatabilir ve Windows Defender’ın arka planda sessizce çalışmasını sağlayabilirsiniz. Windows Defender bilgisayarınızda çalışmaya, bilgisayarınızı izlemeye ve tehditlere karşı korumanıza yardımcı olmaya devam eder.  

 Elbette, Windows Defender’ın çalıştığını bildirim alanında bildirim iletileri görüntülediğinde anlarsınız. Bu bildirimler sizi Windows Defender’ın algıladığı olası tehditler hakkında uyarır.  

 Ayrıca diğer uyarı bildirimlerini de alırsınız, örneğin, bir nedenden dolayı gerçek zamanlı koruma devre dışı bırakıldıysa, virüs ve casus yazılım tanımlarınızı belirli bir gün sayısı boyunca güncelleştirmediyseniz veya program için güncelleştirmeler kullanılabilir olduğunda. Windows Defender ayrıca bilgisayarınızı taradığını size bildirmek için kısaca bir bildirim görüntüler.  

> [!TIP]
> 
> Bildirim alanında Windows Defender simgesini görmüyorsanız, Windows Defender simgesi dahil olmak üzere gizli simgeleri göstermek için bildirim alanındaki oka tıklayın.  


 Simgenin rengi bilgisayarınızın geçerli durumuna bağlıdır:  

-   Yeşil, bilgisayarınızın durumunun "korunuyor" olduğunu gösterir.  

-   Sarı, bilgisayarınızın durumunun "potansiyel olarak korunmuyor" olduğunu gösterir.  

-   Kırmızı, bilgisayarınızın durumunun "riskli" olduğunu gösterir.  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a> Windows Defender veya Endpoint Protection uyarılarını nasıl ayarlarım?  
 Windows Defender bilgisayarınızda çalışırken virüsler, casus yazılım veya istenmeyebilecek yazılımlar algılarsa otomatik olarak sizi uyarır. Ayrıca Windows Defender’ı henüz analiz edilmemiş yazılımları çalıştırdığınızda sizi uyarması için ayarlayabilir ve yazılım bilgisayarınızda değişiklik yaptığında uyarılmayı seçebilirsiniz.  

### <a name="to-set-up-alerts"></a>Uyarıları ayarlamak için  

1.  **Ayarlar**’a tıklayın ve ardından **Gerçek zamanlı koruma**’ya tıklayın.  

2.  **Gerçek zamanlı korumayı etkinleştir (önerilir)** onay kutusunun seçili olduğundan emin olun.  

3.  Çalıştırmak istediğiniz gerçek zamanlı koruma seçeneklerinin yanındaki onay kutularını işaretleyin ve ardından **Değişiklikleri kaydet**’e tıklayın. Yönetici parolası veya onay istenirse parolayı yazın ya da eylemi onaylayın.  

### <a name="see-also"></a>Ayrıca bkz.  
 [Windows Defender veya Endpoint Protection istemcisi sorunlarını giderme](troubleshoot-endpoint-client.md)   

 [Endpoint Protection Istemci yardımı](endpoint-protection-client-help.md)
