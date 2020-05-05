---
title: Technical Preview 1610 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1610 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6402205ae694d719845492b1af37000a0b9335c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721475"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Configuration Manager için Technical Preview 1610 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*



Bu makalede, sürüm 1610 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Otomatik dağıtım kurallarında içerik boyutuna göre filtrele
Artık otomatik dağıtım kurallarında yazılım güncelleştirmeleri için içerik boyutuna filtre uygulayabilirsiniz. Örneğin, yalnızca MB 'tan küçük yazılım güncelleştirmelerini indirmek için **Içerik boyutu (KB)** filtresini **< 2048** olarak ayarlayabilirsiniz. Bu filtrenin kullanılması, büyük yazılım güncelleştirmelerinin, ağ bant genişliği sınırlı olduğunda Basitleştirilmiş Windows alt düzey bakımını daha iyi destekleyecek şekilde otomatik olarak indirilmesine engel olur. Ayrıntılar için bkz. [Configuration Manager ve Basitleştirilmiş Windows Bakımı alt düzey Işletim sistemleri](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>Içerik boyutu alanını yapılandırmak için
**Içerik boyutu (KB)** alanını yapılandırmak IÇIN, ADR oluştururken otomatik dağıtım kuralı oluşturma Sihirbazı ' nda **yazılım güncelleştirmeleri** sayfasına gidin veya var olan bir ADR Için Özellikler ' de **yazılım güncelleştirmeleri** sekmesine gidin.

![İçerik boyutu alanı](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Gerekli yazılım iletişim kutuları için geliştirilmiş işlevsellik
Bir kullanıcı gerekli yazılımları aldığında, **yeniden anımsat ve bana anımsat:** ayarı aşağıdaki açılan değer listesinden seçim yapabilir:
- Daha sonra: bildirimlerin, Istemci Aracısı ayarlarında yapılandırılan bildirim ayarlarına göre zamanlandığını belirtir.
- Sabit zaman: bildirimin seçilen zamandan sonra yeniden görüntülenmek üzere zamanlanacağını belirtir. Örneğin, bir kullanıcı 30 dakika seçerse, bildirim 30 dakika içinde yeniden görüntülenir.

![Istemci Aracısı ayarlarındaki bilgisayar Aracısı sayfası](media/computeragentsettings.png)

En fazla erteleme zamanı, her zaman dağıtım zaman çizelgesinde Istemci Aracısı ayarlarında yapılandırılan bildirim değerlerine göre belirlenir. Örneğin, **dağıtım son tarihi 24 saatten fazlaysa, bilgisayar Aracısı sayfasında kullanıcıları her zaman (saat)** , 10 saat için de uyar ve iletişim kutusu başlatıldığında son tarihten önce 24 saatten fazla olursa, kullanıcıya, 10 saatten daha fazla bir erteleme seçeneği sunulur. Son Tarih yaklaşırsa iletişim kutusunda, dağıtım zaman çizelgesinin her bir bileşeni için ilgili Istemci Aracısı ayarları ile tutarlı olan daha az seçenek gösterilecektir.

Ek olarak, bir işletim sistemini dağıtan görev dizisi gibi yüksek riskli bir dağıtım için son kullanıcı bildirim deneyimi artık daha zorlayıcıdır. Geçici bir görev çubuğu bildirimi yerine, kullanıcıya kritik yazılım bakımının gerekli olduğu her bildirimde bulunulduğundan, kullanıcının bilgisayarında aşağıdaki gibi bir iletişim kutusu görüntülenir:

![Gerekli yazılım iletişim kutusu](media/requiredsoftwaredialog.png)


Daha fazla bilgi için:
- [Yüksek riskli dağıtımları yönetme ayarları](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [İstemci ayarlarını yapılandırma](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Önceden onaylanmış uygulama isteklerini Reddet

Yönetici olarak, artık önceden onaylanmış bir uygulama isteğini reddedebilirsiniz. Reddetme sonrasında, bu uygulamayı yüklemek için daha sonra kullanıcılar bir isteği yeniden göndermelidir. Reddetme, uygulamayı kaldırmaz; Bunun yerine, söz konusu uygulamaya yönelik tüm yeni istekleri yeniden onaylamayı zorlar. Daha önce, uygulama isteği reddetme yalnızca onaylanmamış uygulama istekleri için kullanılabilir.

#### <a name="try-it-out"></a>Deneyin
Bir uygulama tarafından onaylanan isteği reddetmek için:

1. Configuration Manager konsolunda, onay gerektiren [bir uygulama oluşturun ve dağıtın](../../apps/deploy-use/create-applications.md) .
2. İstemci bilgisayarda, yazılım merkezi 'ni açın ve uygulama için bir istek gönderebilirsiniz.
3. Configuration Manager konsolunda, uygulama isteğini onaylayın.
4. Onaylanan uygulama isteğini reddetme: Configuration Manager konsolunda, **yazılım kitaplığı** > **'na genel bakış** > **uygulama yönetimi** > **onay istekleri** ' ne gidin ve reddetmek istediğiniz uygulama isteğini seçin.  Şeritte **Reddet**' e tıklayın.

## <a name="exclude-clients-from-automatic-upgrade"></a>İstemcileri otomatik yükseltmeden hariç tut
Technical Preview 1610, bir istemci koleksiyonunun güncelleştirilmiş istemci sürümlerini otomatik olarak yüklemesini hariç tutmak için kullanabileceğiniz yeni bir ayar sunar.  Bu, otomatik yükseltme ve yazılım güncelleştirme tabanlı yükseltme, oturum açma betikleri ve Grup İlkesi gibi diğer yöntemler için de geçerlidir. Bu, istemciyi yükseltirken daha fazla dikkatli gereksinim duyulan bir bilgisayar koleksiyonu için kullanılabilir. Dışlanan bir koleksiyonda bulunan bir istemci, güncelleştirilmiş istemci yazılımını yüklemek için istekleri yoksayar.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Otomatik yükseltmeden dışlama yapılandırma
Otomatik yükseltme dışlamalarını yapılandırmak için:
1. Configuration Manager konsolunda, **yönetim > site yapılandırması > siteler**altındaki **Hiyerarşi ayarları** ' nı açın ve ardından **istemci yükseltme** sekmesini seçin.
2. **Belirtilen istemcileri yükseltmeden hariç tut**onay kutusunu seçin ve ardından **dışlama koleksiyonu**için dışlamak istediğiniz koleksiyonu seçin. Yalnızca dışlama için tek bir koleksiyon seçebilirsiniz.
3. **Tamam** ' a tıklayarak yapılandırmayı kapatın ve kaydedin. Ardından, istemciler ilkeyi güncelleştirdikten sonra, dışlanan koleksiyondaki istemciler artık güncelleştirmeleri istemci yazılımına otomatik olarak yüklemez.

   ![Otomatik yükseltme dışlama ayarları](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Kullanıcı arabirimi istemcilerin herhangi bir yöntem aracılığıyla yükseltilmeyeceğini bilse de, bu ayarları geçersiz kılmak için kullanabileceğiniz iki yöntem vardır. İstemci gönderme yüklemesi ve bir el ile istemci yüklemesi bu yapılandırmayı geçersiz kılmak için kullanılabilir. Daha ayrıntılı bilgi için aşağıdaki bölüme bakın.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Dışlanan bir koleksiyonda bulunan bir istemciyi yükseltme
Bu nedenle, bir koleksiyon dışlanmak üzere yapılandırıldığında, bu koleksiyonun üyeleri yalnızca kendi istemci yazılımlarını, dışlamayı geçersiz kılan iki yöntemden biriyle yükseltmiş olabilir:
- **Client Push yüklemesi** – dışlanan bir koleksiyonda bulunan bir istemciyi yükseltmek için istemci gönderme yüklemesi ' ni kullanabilirsiniz. Bu, yöneticinin amacı olduğu kabul edildiği için izin verilir ve tüm koleksiyonu dışlamadan kaldırmadan istemcileri yükseltmenizi sağlar.       
- **El ile istemci yüklemesi** : CCMSetup ile aşağıdaki komut satırı anahtarını kullandığınızda, dışlanan bir koleksiyonda bulunan istemcileri el ile yükseltebilirsiniz: ***/ignoreskipupgrade***

  Dışlanan koleksiyonun üyesi olan bir istemciyi el ile yükseltmeye çalışırsanız ve bu anahtarı kullanmıyorsanız, istemci yeni istemci yazılımını yüklemez. Daha fazla bilgi için bkz. [Configuration Manager Istemcilerini El Ile nasıl yüklenir](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

İstemci yükleme yöntemleri hakkında daha fazla bilgi için bkz. [Windows bilgisayarlarına istemci dağıtma](../clients/deploy/deploy-clients-to-windows-computers.md).

## <a name="windows-defender-configuration-settings"></a>Windows Defender yapılandırma ayarları

Artık Configuration Manager konsolundaki yapılandırma öğelerini kullanarak Intune 'a kayıtlı Windows 10 bilgisayarlarında Windows Defender istemci ayarlarını yapılandırabilirsiniz.

Özellikle, aşağıdaki Windows Defender ayarlarını yapılandırabilirsiniz:
- Gerçek zamanlı izlemeye izin ver
- Davranış izlemeye izin ver
- Ağ Denetleme Sistemi'ni Etkinleştir
- Tüm indirmeleri tara
- Betik taramaya izin ver
- Dosya ve program etkinliğini izle
  - İzlenen dosyalar
- Çözümlenen kötü amaçlı yazılımın izleneceği gün sayısı
- İstemci UI erişimine izin ver
- Sistem taraması zamanla
  - Zamanlanan gün
  - Zamanlanan saat
- Günlük hızlı tarama zamanla
  - Zamanlanan saat
- Tarama taraması arşiv dosyaları sırasında CPU kullanımını sınırla%
- E-posta iletilerini tara
- Çıkarılabilir sürücüleri tara
- Eşlenen sürücüleri Tara
- Ağ paylaşımlarından açılan dosyaları tara
- İmza güncelleştirme aralığı
- Bulut korumasına izin ver
- Kullanıcılara örnek iste
- İstenmeyebilecek uygulama algılama
- Dışlanan dosyalar/klasörler
- Dışlanan dosya uzantıları
- Dışlanan süreçler

> [!NOTE]
> Bu ayarlar, yalnızca Windows 10 Kasım Güncelleştirmesi (1511) ve üstünü çalıştıran istemci bilgisayarlarda yapılandırılabilir.

### <a name="try-it-out"></a>Deneyin!

1. Configuration Manager konsolunda, **varlıklar ve uyum** > **genel bakış** > **Uyumluluk ayarları** > **yapılandırma öğeleri**' ne gidin ve yeni bir **yapılandırma öğesi**oluşturun.
2. Bir ad girin ve **Configuration Manager istemcisi olmadan yönetilen cihazlar Için ayarlar** altında **Windows 8.1 ve Windows 10** ' u seçin ve **İleri**' ye tıklayın.
3. **Desteklenen platformlar** sayfasında **tüm windows 10 (64-bit)** ve **tüm Windows 10 (32-bit)** ' ın seçili olduğundan emin olun ve ardından **İleri**' ye tıklayın.
4. **Windows Defender** ayar grubunu seçin ve ardından **İleri**' ye tıklayın.
5. Bu sayfada istenen ayarları yapılandırın ve ardından **İleri**' ye tıklayın.
6. Sihirbazı tamamlayın.
7. Bu yapılandırma öğesini bir yapılandırma temeline ekleyin ve bu temeli Windows 10 Kasım Güncelleştirmesi (1511) veya üstünü çalıştıran bilgisayarlara dağıtın.

> [!NOTE]
> Yapılandırma temelini dağıttığınızda **uyumsuz ayarları Düzelt** onay kutusunun işaretli olup olmadığını unutmayın.

## <a name="request-policy-sync-from-administrator-console"></a>Yönetici konsolundan ilke eşitlemesi iste

Artık Configuration Manager konsolundan bir mobil cihaz için bir ilke eşitlemesi isteyebilirsiniz, bu da cihazın kendisinden eşitleme isteğinde bulunabilir. Eşitleme isteği durum bilgileri, **uzak eşitleme durumu**adlı cihaz görünümlerinde yeni bir sütun olarak kullanılabilir. Durum, her mobil cihazın **Özellikler** Iletişim kutusunun **bulgu verileri** bölümünde de görüntülenir.

### <a name="try-it-out"></a>Deneyin!

1. Configuration Manager konsolunda, **varlıklar ve uyum** > **genel bakış** > cihazlar ' a gidin.
2. **Uzak cihaz eylemleri** menüsünde, **eşitleme isteği gönder**' i seçin.

Eşitleme beş ila on dakika sürebilir. İlkedeki değişiklikler cihazla eşitlenir. Eşitleme isteğinin durumunu **cihazlar** görünümündeki **uzak eşitleme durumu** sütununda veya cihazın **Özellikler** iletişim kutusunda izleyebilirsiniz.

## <a name="additional-security-role-support"></a>Ek güvenlik rolü desteği

Tam yöneticiye ek olarak, aşağıdaki yerleşik güvenlik rolleri artık, **önceden tanımlanmış cihazlar**, **iOS kayıt profilleri**ve **Windows kayıt profilleri**dahil olmak üzere, **şirkete ait tüm cihazlar** düğümündeki öğelere tam erişime sahiptir:
- **Varlık Yöneticisi**
- **Şirket kaynağı Erişim Yöneticisi**

Configuration Manager konsolunun bu bölümlerine salt okuma erişimi, **salt okunurdur analist** rolüne hala verilir.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Windows 10 VPN profilleri için koşullu erişim

Artık, Configuration Manager konsolunda oluşturulan Windows 10 VPN profilleri aracılığıyla VPN erişimine sahip olmak için Azure Active Directory 'e kayıtlı Windows 10 cihazlarının uyumlu olmasını isteyebilirsiniz. Bu, VPN profili Sihirbazı 'ndaki **kimlik doğrulama yöntemi** sayfasında ve WINDOWS 10 VPN PROFILLERI için VPN profili özellikleri ' nde **Bu VPN bağlantısı Için koşullu erişimi etkinleştir** onay kutusu üzerinden yapılabilir. Ayrıca, profil için koşullu erişimi etkinleştirirseniz, çoklu oturum açma kimlik doğrulaması için ayrı bir sertifika belirtebilirsiniz.

## <a name="see-also"></a>Ayrıca Bkz.
[Configuration Manager için teknik önizleme](../../core/get-started/technical-preview.md)
