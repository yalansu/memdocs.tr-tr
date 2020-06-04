---
title: Windows 'da istemcileri yükseltme
titleSuffix: Configuration Manager
description: Configuration Manager Windows bilgisayarlarda istemcileri yükseltin.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b0a69b07a3be633434203f93b0724cec4ea88a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347159"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Configuration Manager 'da Windows bilgisayarlar için istemcileri yükseltme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İstemci yükleme yöntemlerini veya otomatik istemci yükseltme özelliğini kullanarak Windows bilgisayarlarda Configuration Manager istemcisini yükseltin. Aşağıdaki istemci yükleme yöntemleri Windows bilgisayarlardaki istemci yazılımını yükseltmek için geçerli yöntemlerdir:  

- Grup ilkesi yüklemesi  

- Oturum açma betiği yüklemesi  

- El ile yükleme  

- Yüklemeyi yükseltme  

Daha fazla bilgi için bkz. [Windows bilgisayarlarına istemci dağıtma](../../deploy/deploy-clients-to-windows-computers.md).

Dışlama koleksiyonu belirterek istemcileri yükseltmeden hariç tutun. Daha fazla bilgi için bkz. [istemcileri yükseltmeden dışlama](exclude-clients-windows.md). Dışlanan istemciler hala CCMSETUP 'ı indirir ve çalıştırır, ancak yükseltmez.

> [!TIP]  
> Sunucu altyapınızı Configuration Manager önceki bir sürümünden yükseltiyorsanız, Configuration Manager istemcilerini yükseltmeden önce sunucu yükseltmelerini doldurun. Bu işlem, tüm geçerli dal güncelleştirmelerini yüklemeyi içerir. En son geçerli dal güncelleştirmesi istemcinin en son sürümünü içerir. Tüm Configuration Manager güncelleştirmelerini yükledikten sonra istemcileri yükseltin.

> [!NOTE]
> Yükseltme sırasında site istemcilerini yeniden atamayı planlıyorsanız, `SMSSITECODE` Client. msi özelliğini kullanarak yeni siteyi belirtin. İçin değerini kullanıyorsanız `AUTO` `SMSSITECODE` , ayrıca öğesini de belirtin `SITEREASSIGN=TRUE` . Bu özellik, yükseltme sırasında otomatik site yeniden atamaya izin verir. Daha fazla bilgi için bkz. [istemci yükleme özellikleri-SMSSITEKODU](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a>Otomatik istemci yükseltme hakkında

Siteyi, istemcileri otomatik olarak en son Configuration Manager sürümüne yükseltecek şekilde yapılandırın. Configuration Manager atanan bir istemcinin sürümünü, hiyerarşi sürümünden daha önce belirlediğinde, istemciyi otomatik olarak yükseltir. Bu senaryo, bir Configuration Manager sitesine atamaya çalıştığında istemciyi en son sürüme yükseltmeyi içerir.  

Aşağıdaki senaryolarda bir istemci otomatik olarak yükseltilebilir:  

- İstemci sürümü, hiyerarşide kullanılan sürümden daha eski.  

- Merkezi yönetim sitesindeki (CAS) istemcide bir dil paketi yüklüdür ve var olan istemci yoktur.  

- Hiyerarşideki bir istemci önkoşulu, istemcide yüklü olandan farklı bir sürümdür.  

- İstemci yüklemesi dosyalarının biri veya birkaçı farklı bir sürümdür.  

> [!NOTE]  
> Hiyerarşinizdeki Configuration Manager istemcisinin farklı sürümlerini tanımlamak için, **site-Istemci bilgileri**rapor klasöründe **istemci sürümlerine göre Configuration Manager istemcilerinin rapor sayısını** kullanın.  

Configuration Manager, varsayılan olarak bir yükseltme paketi oluşturur. Paket, hiyerarşideki tüm dağıtım noktalarına otomatik olarak gönderilir. CA 'larda istemci paketinde değişiklik yaparsanız, Configuration Manager paketi otomatik olarak güncelleştirir ve yeniden dağıtır. Bir istemci dil paketi eklediğinizde örnek bir değişiklik olur. Otomatik istemci yükseltmesini etkinleştirirseniz, her istemci yeni istemci dili paketini otomatik olarak yüklenir.

Hiyerarşiniz genelinde otomatik istemci yükseltmesini etkinleştirin. Bu yapılandırma, istemcilerinizi daha az çabayla güncel tutar.  

Configuration Manager site sistemlerinizi de istemci olarak yönetiyorsanız, bunları otomatik yükseltme işleminin bir parçası olarak dahil edilip edilmeyeceğini saptayın. İstemci yükseltmesinde tüm sunucuları veya belirli bir koleksiyonu dışlayabilirsiniz. Bazı Configuration Manager site rolleri istemci çerçevesini paylaşır. Örneğin, yönetim noktası ve çekme dağıtım noktası. Siteyi güncelleştirdiğinizde bu roller yükseltilir, bu nedenle bu sunuculardaki istemci sürümü aynı anda güncelleştirilir.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a>Otomatik istemci yükseltmesini yapılandırma

CA 'larda otomatik istemci yükseltmesini yapılandırmak için aşağıdaki yordamı kullanın. Bu yapılandırma hiyerarşinizdeki tüm istemciler için geçerlidir.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

1. Şeridin **giriş** sekmesinde, **siteler** grubunda, **Hiyerarşi ayarları**' nı seçin.  

1. **Istemci yükseltme** sekmesine geçin. üretim istemcisinin sürümünü ve tarihini gözden geçirin. İstemcilerinizi yükseltmek için kullanmak istediğiniz sürüm olduğundan emin olun. Tahmin ettiğiniz istemci sürümü değilse, ön üretim istemcisini üretime yükseltmeniz gerekebilir. Daha fazla bilgi için bkz. [bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](test-client-upgrades.md).  

1. **Üretim istemcisini kullanarak hiyerarşideki tüm Istemcileri Yükselt '** i seçin. Onaylamak için **Tamam**’ı seçin.  

1. İstemci yükseltmelerinin sunuculara uygulanmasını istemiyorsanız **sunucuları yükseltme**' yi seçin.  

1. Cihazların istemciyi yükseltmesi gereken gün sayısını belirtin. Cihaz ilkeyi aldıktan sonra, bu gün sayısı içinde rastgele bir aralıkta istemciyi yükseltir. Bu davranış, çok sayıda istemcinin eşzamanlı olarak yükseltilmesini önler.

    > [!NOTE]
    > İstemciyi yükseltmek için bir bilgisayarın çalışıyor olması gerekir. Bir bilgisayar, yükseltmeyi almak üzere zamanlandığında çalışmıyorsa, Yükseltme gerçekleşmez. Bilgisayar açıldığında ve ilke aldığında, yükseltmeyi izin verilen gün sayısı içinde rastgele bir süre boyunca zamanlar. Bu durum, Yükseltilecek gün sayısı sona erdiğinde, bilgisayarın açıldıktan sonra 24 saat içinde yükseltmeyi zaman içinde zamanlar.
    >
    > Bu davranış nedeniyle, düzenli olarak kapatılmış olan bilgisayarlar, rastgele zamanlanmış yükseltme zamanı normal çalışma saatleri içinde değilse beklenenden daha uzun sürebilir.

1. İstemcileri yükseltmeden hariç tutmak için, **belirtilen istemcileri yükseltmeden hariç**tut ' u seçin ve dışlanacak koleksiyonu belirtin. Daha fazla bilgi için bkz. [istemcileri yükseltmeden hariç tutma](exclude-clients-windows.md).

1. Sitenin istemci yükleme paketini [önceden hazırlanmış içerik](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)için etkinleştirdiğiniz dağıtım noktalarına kopyalamasını istiyorsanız, **istemci yükleme paketini önceden hazırlanan içerik için etkinleştirilen dağıtım noktalarına otomatik olarak dağıt**seçeneğini belirleyin.  

1. Ayarları kaydetmek ve hiyerarşi ayarları özelliklerini kapatmak için **Tamam** ' ı seçin.

İstemciler bir dahaki sefere ilkeyi indirdiklerinde bu ayarları alırlar.

> [!NOTE]
> İstemci yükseltmeleri, yapılandırdığınız tüm Configuration Manager bakım pencerelerini dikkate almaz. Execmgr thread yalnızca bir bakım penceresi sırasında istemci Kurulum önyükleme programını (CCMSetup. exe) çalıştırır. Cihaz, yazma filtresiyle bir Windows sürümü çalıştırıyorsa, CCMSetup aynı anda indirme ve yüklemeyi dener. Aksi takdirde, CCMSetup içeriğin indirileceği rastgele bir zaman alır. İçeriği indirdikten ve yerel ilkeyi derledikten sonra, Execmgr bir sonraki bakım penceresi sırasında istemci yükseltmesini zamanlar.<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>Sonraki adımlar

İstemcileri yükseltmek için alternatif yöntemler için bkz. [Windows bilgisayarlarına istemci dağıtma](../../deploy/deploy-clients-to-windows-computers.md).

Belirli istemcileri otomatik yükseltmeden hariç tutun. Daha fazla bilgi için bkz. [istemcileri yükseltmeden dışlama](exclude-clients-windows.md).
