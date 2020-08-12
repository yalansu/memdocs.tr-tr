---
title: Ağ üzerinden OSD için PXE kullanın
titleSuffix: Configuration Manager
description: Bir bilgisayarın işletim sistemini yenilemek veya yeni bir Windows sürümünü yeni bir bilgisayara yüklemek için PXE tarafından başlatılan IŞLETIM sistemi dağıtımlarını kullanın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d2d467a053689edad1dcf62fa9bb140d5f259d9
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124627"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager ile ağ üzerinden Windows dağıtmak için PXE kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Önyükleme yürütme ortamı (PXE) tarafından başlatılan işletim SISTEMI Configuration Manager dağıtımları, istemcilerin ağ üzerinden işletim sistemleri istemesini ve dağıtmasını sağlar. Bu dağıtım yönteminde, işletim sistemi görüntüsünü ve önyükleme görüntülerini PXE 'yi destekleyen bir dağıtım noktasına gönderirsiniz.

> [!NOTE]
> Yalnızca x64 BIOS bilgisayarları hedefleyen bir işletim sistemi dağıtımı oluşturduğunuzda hem x64 önyükleme görüntüsü hem de x86 önyükleme görüntüsünün dağıtım noktasında kullanılabilir olması gerekir.

PXE tarafından başlatılan işletim sistemi dağıtımlarını aşağıdaki senaryolarda kullanabilirsiniz:

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)

İşletim sistemi dağıtım senaryolarından birindeki adımları doldurun ve ardından bu makaledeki bölümleri kullanarak PXE tarafından başlatılan dağıtımları hazırlayın.

> [!WARNING]
> PXE dağıtımlarını kullanır ve ilk önyükleme aygıtı olarak ağ bağdaştırıcısı ile cihaz donanımını yapılandırırsanız, bu cihazlar Kullanıcı etkileşimi olmadan bir işletim sistemi dağıtımı görev sırasını otomatik olarak başlatabilir. [Dağıtım doğrulaması](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) bu yapılandırmayı yönetmez. Bu yapılandırma işlemi basitleştirecek ve kullanıcı etkileşimini azaltmasına karşın, yanlışlıkla yeniden görüntü için cihazı daha fazla riske koyar.

Sürüm 2006 ' den başlayarak, PXE tabanlı görev dizileri bulut tabanlı içeriği indirebilir. PXE 'yi destekleyen dağıtım noktası hala önyükleme görüntüsünü gerektirir ve cihazın yönetim noktasına bir intranet bağlantısı olması gerekir. Daha sonra içerik etkinleştirilmiş bir bulut yönetimi ağ geçidi (CMG) veya bulut dağıtım noktasından ek içerik alabilir.<!--6209223--> Daha fazla bilgi için bkz. [bulut tabanlı Içerik desteği](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="configure-distribution-points-for-pxe"></a><a name="BKMK_Configure"></a>PXE için dağıtım noktalarını yapılandırma

PXE önyükleme istekleri yapan istemcileri Configuration Manager işletim sistemlerini dağıtmak için, PXE isteklerini kabul etmek üzere bir veya daha fazla dağıtım noktası yapılandırın. Ardından dağıtım noktası PXE önyükleme isteklerine yanıt verir ve uygun dağıtım eylemini belirler. Daha fazla bilgi için, bkz. [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

> [!NOTE]
> Birden çok alt ağı desteklemek için tek bir PXE 'yi destekleyen dağıtım noktası yapılandırdığınızda, DHCP seçeneklerinin kullanılması desteklenmez. Ağın, istemci PXE isteklerini PXE 'yi destekleyen dağıtım noktalarına iletmesine izin vermek için, yönlendiricilerde IP Yardımcıları yapılandırın.

Sürüm 1810 ' de, aynı zamanda bir DHCP sunucusu çalıştıran sunucularda WDS olmadan PXE Yanıtlayıcı 'yı kullanmak desteklenmez.

Sürüm 1902 ' den başlayarak, bir dağıtım noktasında Windows dağıtım hizmeti olmadan bir PXE Yanıtlayıcı 'yı etkinleştirdiğinizde, artık DHCP hizmetiyle aynı sunucuda olabilir.<!--3734270, SCCMDocs-pr #3416--> Bu yapılandırmayı desteklemek için aşağıdaki ayarları ekleyin:

- **Donotlistenondhcpport** DWORD değerini `1` Şu kayıt defteri anahtarında olacak şekilde ayarlayın: `HKLM\Software\Microsoft\SMS\DP` .
- DHCP seçeneğini 60 olarak ayarlayın `PXEClient` .
- Sunucuda SCCMPXE ve DHCP hizmetlerini yeniden başlatın.

## <a name="prepare-a-pxe-enabled-boot-image"></a>PXE'yi destekleyen bir önyükleme görüntüsü hazırlama

Bir işletim sistemini dağıtmak üzere PXE kullanmak için, hem x86 hem de x64 PXE 'yi destekleyen önyükleme görüntülerini bir veya daha fazla PXE 'yi destekleyen dağıtım noktasına dağıtın.

- Bir önyükleme görüntüsünde PXE 'yi etkinleştirmek için, önyükleme görüntüsü özelliklerindeki **veri kaynağı** sekmesinden **Bu önyükleme görüntüsünü PXE 'yi destekleyen dağıtım noktasından dağıt** ' ı seçin.

- Önyükleme görüntüsünün özelliklerini değiştirdiğinizde önyükleme görüntüsünü güncelleştirme ve dağıtım noktalarına yeniden dağıtma. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## <a name="manage-duplicate-hardware-identifiers"></a>Yinelenen donanım tanımlayıcılarını yönetme

Configuration Manager, yinelenen SMBıOS öznitelikleri varsa veya paylaşılan bir ağ bağdaştırıcısı kullanıyorsanız, birden çok bilgisayarı aynı cihaz olarak tanıyabilir. Hiyerarşi ayarlarında yinelenen donanım tanımlayıcılarını yöneterek bu sorunları azaltabilirsiniz. Daha fazla bilgi için bkz. [yinelenen donanım tanımlayıcılarını yönetme](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> PXE dağıtımları için bir dışlama listesi oluşturma

> [!NOTE]
> Bazı durumlarda, [yinelenen donanım tanımlayıcılarını yönetme](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) işlemi daha kolay olabilir.<!-- SCCMDocs issue 802 -->
>
> Her birinin davranışları bazı senaryolarda farklı sonuçlara neden olabilir. Dışlama listesi hiçbir şekilde, listelenen MAC adresiyle bir istemciyi hiçbir şekilde önetmez.
>
> Yinelenen KIMLIK listesi, bir istemcinin görev sırası ilkesini bulmak için MAC adresini kullanmaz. SMBıOS KIMLIĞIYLE eşleşiyorsa veya bilinmeyen makineler için bir görev sırası ilkesi varsa, istemci hala önyüklenir.

İşletim sistemlerini PXE ile dağıtırken, her dağıtım noktasında bir dışlama listesi oluşturabilirsiniz. Dağıtım noktasının yoksayılmasını istediğiniz bilgisayarların dışlama listesine MAC adreslerini ekleyin. Listelenen bilgisayarlar Configuration Manager PXE dağıtımı için kullanılan dağıtım görev dizilerini almaz.

1. PXE 'yi destekleyen dağıtım noktasında bir metin dosyası oluşturun. Örneğin, dosyayı **pxeExceptions.txt**olarak adlandırın.

1. Dosyayı düzenlemek için Not Defteri gibi bir düz metin düzenleyicisi kullanın. PXE 'yi destekleyen dağıtım noktasının yoksayması gereken bilgisayarların MAC adreslerini ekleyin. MAC adresi değerlerini virgüllerle ayırın ve her adresi ayrı bir satıra girin. Örnek: `01:23:45:67:89:ab`

1. Metin dosyasını PXE 'yi destekleyen dağıtım noktasına kaydedin. Bunu, sunucudaki herhangi bir konuma kaydedebilirsiniz.

1. PXE 'yi destekleyen dağıtım noktasındaki kayıt defterini düzenleyin. Aşağıdaki kayıt defteri yoluna gidin: `HKLM\Software\Microsoft\SMS\DP` . Bir **MACIgnoreListFile** dize değeri oluşturun. PXE 'yi destekleyen dağıtım noktasındaki metin dosyasının tam yolunu ekleyin.

    > [!WARNING]
    > Kayıt Defteri Düzenleyicisi 'Ni yanlış kullanırsanız, Windows 'u yeniden yüklemenizi gerektirebilecek önemli sorunlara neden olabilirsiniz. Microsoft, kayıt defteri Düzenleyicisi 'nin yanlış kullanılması sonucunda oluşan sorunları çözebileceğinizi garanti edemez. Kayıt Defteri Düzenleyicisi'ni kullanım riski size aittir.

1. Bu kayıt defteri değişikliğini yaptıktan sonra WDS hizmetini veya PXE Yanıtlayıcı hizmetini yeniden başlatın. Sunucuyu yeniden başlatmanız gerekmez.<!--512129-->

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>RamDisk TFTP blok boyutu ve pencere boyutu

PXE 'yi destekleyen dağıtım noktaları için RamDisk TFTP bloğunu ve pencere boyutlarını özelleştirebilirsiniz. Ağınızı özelleştirdiyseniz, büyük bir blok veya pencere boyutu, önyükleme görüntüsü indirmenin zaman aşımı hatası vererek başarısız olmasına neden olabilir. RamDisk TFTP blok ve pencere boyutu özelleştirmeleri, PXE kullanırken belirli ağ gereksinimlerinizi karşılayacak şekilde TFTP trafiğini iyileştirmenize olanak tanır. Yapılandırmanın en verimli olduğunu belirlemek için, özelleştirilmiş ayarları ortamınızda test edin. Daha fazla bilgi için bkz. [PXE 'yi destekleyen dağıtım noktalarında RAMDISK TFTP blok boyutunu ve pencere boyutunu özelleştirme](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma

PXE tarafından başlatılan bir işletim sistemi dağıtımını kullanmak için dağıtımı, işletim sistemini PXE önyükleme istekleri için kullanılabilir hale getirmek üzere yapılandırın. Dağıtım özelliklerindeki **dağıtım ayarları** sekmesinde kullanılabilir işletim sistemlerini yapılandırın. **Aşağıdakiler için kullanılabilir yap** ayarı için, aşağıdaki seçeneklerden birini seçin:

- İstemcileri, medyayı ve PXE 'yi Configuration Manager

- Yalnızca medya ve PXE

- Yalnızca medya ve PXE (gizli)

## <a name="option-82-during-pxe-dhcp-handshake"></a>PXE DHCP el sıkışması sırasında 82 seçeneği

Sürüm 1906 ' den başlayarak, PXE DHCP el sıkışması sırasında WDS olmadan PXE yanıtlayıcısının 82 seçeneğini destekler Configuration Manager. Seçenek 82 ' ye ihtiyacınız varsa, PXE Yanıtlayıcı 'yı WDS olmadan kullandığınızdan emin olun. Configuration Manager WDS ile 82 seçeneğini desteklemez.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Görev dizisini dağıtma

İşletim sistemini bir hedef koleksiyona dağıtın. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md). İşletim sistemlerini PXE kullanarak dağıttığınızda dağıtımın gerekli veya kullanılabilir olup olmadığını yapılandırabilirsiniz.

- **Gerekli dağıtım**: gerekli dağıtımlar, herhangi bir Kullanıcı MÜDAHALESI olmadan PXE kullanır. Kullanıcı PXE önyüklemesini atlayamaz. Ancak, dağıtım noktası yanıt vermeden önce Kullanıcı PXE önyüklemesini iptal ederse işletim sistemi dağıtılmaz.

- **Kullanılabilir dağıtım**: kullanılabilir dağıtımlar, kullanıcının hedef bilgisayarda mevcut olmasını gerektirir. PXE önyükleme işlemine devam etmek için kullanıcının **F12** tuşuna basması gerekir. Bir Kullanıcı **F12**tuşuna basması için yoksa, bilgisayar geçerli işletim sisteminde veya bir sonraki kullanılabilir önyükleme aygıtından önyüklenir.

Bir Configuration Manager koleksiyonuna veya bir bilgisayara atanan son PXE dağıtımının durumunu temizleyerek gerekli bir PXE dağıtımını yeniden dağıtabilirsiniz. **Gereklı PXE dağıtımlarını temizle** eylemi hakkında daha fazla bilgi için bkz. [istemcileri yönetme](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) veya [koleksiyonları yönetme](../../core/clients/manage/collections/manage-collections.md#bkmk_device). Bu eylem, o dağıtımın durumunu sıfırlar ve gereken en son dağıtımları yeniden yükler.

> [!IMPORTANT]
> PXE protokolü güvenli değil. Sitenize yetkisiz erişimi engellemek için PXE sunucusunun ve PXE istemcisinin bir veri merkezinde olduğu gibi fiziksel olarak güvenli bir ağda bulunduğundan emin olun.

## <a name="how-the-boot-image-is-selected-for-pxe"></a>PXE için önyükleme görüntüsünün nasıl seçildiği

İstemci PXE ile önyüklendiğinde, Configuration Manager istemciye, kullanılacak bir önyükleme görüntüsü sağlar. Configuration Manager, bir önyükleme görüntüsünü tam mimari eşleşmesi ile kullanır. Tam mimarisine sahip bir önyükleme görüntüsü yoksa Configuration Manager, uyumlu bir mimariye sahip bir önyükleme görüntüsü kullanır.

Aşağıdaki listede PXE ile önyüklemesi yapılacak istemciler için bir önyükleme görüntüsünün nasıl seçilme hakkındaki ayrıntılar verilmektedir:  

1. Configuration Manager, önyükleme yapmaya çalışan istemcinin MAC adresiyle veya SMBıOS ile eşleşen sistem kaydı için site veritabanına bakar.  

    > [!NOTE]  
    > Bir siteye atanan bir bilgisayar, farklı bir site için PXE 'de önyükleniyorsa, ilkeler bilgisayar için görünür değildir. Örneğin, bir istemci sitesine zaten atanmışsa, B sitesinin yönetim noktası ve dağıtım noktası A sitesindeki ilkelere erişemez. İstemci başarıyla PXE önyüklemesi yapmaz.  

2. Configuration Manager adım 1 ' de bulunan sistem kaydına dağıtılan görev dizilerini arar.  

3. 2. adımda bulunan görev dizileri listesinde, önyüklemeye çalışan istemcinin mimarisiyle eşleşen bir önyükleme görüntüsünü arar Configuration Manager. Aynı mimariye sahip bir önyükleme görüntüsü bulunursa, bu önyükleme görüntüsü kullanılır.  

    Birden fazla önyükleme görüntüsü bulursa, *en yüksek* veya en son görev SıRASı dağıtım kimliğini kullanır. Çok siteli bir hiyerarşi söz konusu olduğunda, bu dize karşılaştırmasına göre *daha yüksek* bir site öncelik kazanır. Örneğin, her ikisi de eşleştirildiği takdirde, site ZZZ 'den eski bir yıla ait dağıtım site AAA 'dan dün dağıtımı üzerinde seçilir.<!-- SCCMDocs issue 877 -->  

4. Aynı mimariye sahip bir önyükleme görüntüsü bulunmazsa Configuration Manager istemcinin mimarisiyle uyumlu bir önyükleme görüntüsü arar. 2. adımda bulunan görev dizileri listesine bakar. Örneğin, 64 bitlik bir BIOS/MBR istemcisi, 32 bit ve 64 bit önyükleme görüntüleriyle uyumludur. 32 bitlik bir BIOS/MBR istemcisi yalnızca 32 bit önyükleme görüntüleriyle uyumludur. UEFı istemcileri yalnızca eşleşen mimarisiyle uyumludur. 64 bitlik bir UEFı istemcisi yalnızca 64 bit önyükleme görüntüleriyle uyumludur ve bir 32-bit UEFı istemcisi yalnızca 32 bit önyükleme görüntüleriyle uyumludur.

## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemi dağıtımı için kullanıcı deneyimleri](../understand/user-experience.md#pxe)
