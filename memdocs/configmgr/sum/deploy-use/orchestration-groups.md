---
title: Düzenleme grupları
titleSuffix: Configuration Manager
description: Düzenleme grupları oluşturun ve bunlara güncelleştirmeleri dağıtın.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b42a0260b347fb12444e8611e7ec02be38cc387
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088420"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Configuration Manager düzenleme grupları
<!--3098816-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sürüm 2002 ' den başlayarak, düzenleme grupları oluşturabilirsiniz. Cihazlara yazılım güncelleştirmelerinin dağıtımını daha iyi denetlemek için bir Orchestration grubu oluşturun. Birçok sunucu yöneticisi, belirli iş yükleri için güncelleştirmeleri dikkatle Yönetmeli ve arasındaki davranışları otomatikleştiremelidir.

Bir Orchestration grubu, cihazları bir yüzdeye, belirli bir sayıya veya açık bir sıraya göre güncelleştirme esnekliği sağlar. Ayrıca, cihazlar güncelleştirme dağıtımını çalıştırmadan önce ve sonra bir PowerShell betiği de çalıştırabilirsiniz.

Bir Orchestration grubunun üyeleri yalnızca sunucular değil Configuration Manager istemci olabilir. Düzenleme grubu kuralları, bir düzenleme grubu üyesi içeren herhangi bir koleksiyondaki tüm yazılım güncelleştirme dağıtımları için cihazlara uygulanır. Diğer dağıtım davranışları hala geçerlidir. Örneğin, bakım pencereleri ve dağıtım zamanlamaları.

> [!NOTE]
> Bu Configuration Manager sürümünde, düzenleme grupları bir yayın öncesi özelliktir. Etkinleştirmek için bkz. [yayın öncesi Özellikler](../../core/servers/manage/pre-release-features.md).  
>
> **Düzenleme grupları** özelliği, [sunucu grupları](service-a-server-group.md) özelliğinin evmidir. Düzenleme grubu Configuration Manager bir nesnedir.

## <a name="orchestration-group-usage-example"></a>Düzenleme grubu kullanım örneği

- Yazılım Güncelleştirme Yöneticisi olarak, kuruluşunuz için tüm güncelleştirmeleri yönetirsiniz.
- Tüm sunucular için bir büyük koleksiyonunuz ve tüm istemciler için bir büyük koleksiyon vardır. Tüm güncelleştirmeleri bu koleksiyonlara dağıtırsınız.
- SQL yöneticileri, SQL sunucularında yüklü olan tüm yazılımları denetlemek ister. Belirli bir sırada beş sunucuya yama yapmak ister. Güncel işlemleri, güncelleştirmeleri yüklemeden önce belirli hizmetleri el ile durdurmaktır ve ardından Hizmetleri daha sonra yeniden başlatın.
- Bir düzenleme grubu oluşturur ve beş SQL sunucusunu eklersiniz. SQL yöneticileri tarafından sunulan PowerShell betiklerini kullanarak, ön ve son betik da eklersiniz.
- Sonraki güncelleştirme çevrimi sırasında, yazılım güncelleştirmelerini oluşturup çok sayıda sunucu koleksiyonuna normal olarak dağıtırsınız. SQL yöneticileri dağıtımı çalıştırır ve düzenleme grubu sıra ve Hizmetleri otomatikleştirir.

## <a name="prerequisites"></a>Ön koşullar

### <a name="site-server-and-permission-prerequisites"></a>Site sunucusu ve izin önkoşulları
- Bu grupların tüm düzenleme gruplarını ve güncelleştirmelerini görmek için hesabınızın **tam yönetici**olması gerekir.
   - Düzenleme grupları için rol tabanlı yönetim Şu anda kullanılamıyor.
- **Düzenleme grupları** özelliğini etkinleştirin. Daha fazla bilgi için bkz. [isteğe bağlı özellikleri etkinleştirme](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
   - **Düzenleme gruplarını**etkinleştirdiğinizde, site **sunucu grupları** özelliğini devre dışı bırakır. Bu davranış, iki özellik arasındaki çakışmaları önler.

### <a name="client-prerequisites"></a>İstemci önkoşulları

- Hedef cihazları Configuration Manager istemcisinin en son sürümüne yükseltin.
- Bir Orchestration grubunun üyeleri aynı siteye atanmalıdır.
- Cihazlar birden fazla düzenleme grubunda olamaz.
   - Yeni Üyeler eklenirken bir düzenleme grubunda zaten bulunan cihazların seçimi kaldırılacak.


## <a name="limitations"></a>Sınırlamalar

- En fazla 1000 düzenleme grubu üyesine sahip olabilirsiniz.
- Düzenleme grupları birlikte çalışabilirlik modunda çalışmaz. Daha fazla bilgi için bkz. [Configuration Manager farklı sürümleri arasında birlikte çalışabilirlik](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed). <!--6389000-->
- Yazılım Merkezi 'nden kullanıcılar tarafından güncelleştirmeler başlatılmışsa, düzenleme atlanır. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>Sunucu grupları, düzenleme gruplarına otomatik olarak güncelleştirilir

**Düzenleme grupları** özelliği, [sunucu grupları](service-a-server-group.md) özelliğinin evmidir. Configuration Manager sürüm 2002 veya üstünü yüklediğinizde ve sunucu grupları etkin olduğunda, sunucu gruplarınız otomatik olarak düzenleme gruplarına taşınır.

## <a name="create-an-orchestration-group"></a>Düzenleme grubu oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Orchestration grubu** düğümünü seçin.

1. Şeritte düzenleme grubu oluştur ' **u seçerek** **düzenleme grubu oluşturma Sihirbazı 'nı**açın.

1. **Genel** sayfasında, düzenleme grubunuza bir **ad** ve Isteğe bağlı olarak bir **Açıklama**verin. Aşağıdaki öğeler için değerlerinizi belirtin:
   - **Düzenleme grubu zaman aşımı (dakika cinsinden)**: tüm grup üyelerinin güncelleştirme yüklemesini tamamlaması için geçen süre üst sınırı.
   - **Düzenleme grubu üye zaman aşımı (dakika cinsinden)**: güncelleştirme yüklemesini gerçekleştirmek için gruptaki tek bir cihaz için zaman sınırı.

1. **Üye seçimi** sayfasında, önce **site kodunu**belirtin. Sonra bu düzenleme grubunun üyesi olarak cihaz kaynakları eklemek için **Ekle** ' yi seçin. Cihazları ada göre **arayın** ve ardından **ekleyin** . Ayrıca, **koleksiyonda ara '** yı kullanarak aramanızı tek bir koleksiyona filtreleyebilirsiniz.  Seçili kaynaklar listesine cihaz eklemeyi bitirdiğinizde **Tamam ' ı** seçin.
   - Grup için kaynak seçerken yalnızca geçerli istemciler gösterilir. Site kodunun doğrulanması, istemcinin yüklü olması ve kaynakların yinelenmemesi için denetimler yapılır.

1. **Kural seçimi** sayfasında, aşağıdaki seçeneklerden birini seçin:

   - **Makinelerin bir yüzdesinin aynı anda güncelleştirilmesine Izin verin**, ardından bu yüzde için bir sayı seçin veya girin. Düzenleme grubunun boyutuyla ilgili daha fazla esneklik sağlamak için bu ayarı kullanın. Örneğin, düzenleme grubunuz 50 cihaz içerir ve bu değeri 10 olarak ayarlayabilirsiniz. Yazılım güncelleştirme dağıtımı sırasında, Configuration Manager dağıtımı aynı anda beş cihazın çalıştırmasına izin verir. Daha sonra Orchestration grubunun boyutunu 100 cihaz olarak artırdıysanız, 10 cihaz aynı anda güncelleştirme yapılır.

   - **Bir dizi makinenin aynı anda güncelleştirilmesine Izin verin**, ardından bu belirli sayı için bir sayı seçin veya girin. Düzenleme grubunun genel boyutu ne olursa olsun, her zaman belirli sayıda cihaza sınırlamak için bu ayarı kullanın.

   - **Bakım sırasını belirtin**ve ardından seçilen kaynakları uygun sırada sıralayın. Cihazların yazılım güncelleştirme dağıtımını Çalıştırma sırasını açıkça tanımlamak için bu ayarı kullanın.

1. **Ön betik** sayfasında, dağıtım *çalıştırılmadan önce* her cihazda çalıştırılacak bir PowerShell betiği girin. Betik, `0` başarılı veya `3010` yeniden başlatma ile başarılı için bir değer döndürmelidir.

1. **Betik sonrası** sayfasında, dağıtım çalıştıktan *sonra* her cihazda çalıştırılacak bir PowerShell betiği girin ve gerekirse bir yeniden başlatma gerçekleşir. Davranış, PreScript ile aynı şekilde aynıdır.

1. Sihirbazı tamamlayın.

> [!WARNING]
> Önceki betiklerin ve betikleri düzenleme grupları için kullanılmadan önce test edilmiş olduğundan emin olun. Betiklerin ve son betiklerin zaman aşımı değildir ve düzenleme grubu üye zaman aşımına ulaşılana kadar çalışır.

## <a name="view-orchestration-groups-and-members"></a>Düzenleme gruplarını ve üyelerini görüntüle

**Varlıklar ve uyum** çalışma alanından **Orchestration grubu** düğümünü seçin. Üyeleri görüntülemek için bir düzenleme grubu seçin ve şeritte **üyeleri göster** ' i seçin. Düğümlerin kullanılabilir sütunları hakkında daha fazla bilgi için bkz. [izleme düzenleme grupları ve üyeleri](#bkmk_orch_monitor).

## <a name="edit-or-delete-an-orchestration-group"></a>Orchestration grubunu düzenleme veya silme

Orchestration grubunu silmek için, seçin ve ardından Şeritteki veya sağ tıklama menüsünde **Sil** ' e tıklayın. Bir Orchestration grubunu düzenlemek için, seçin ve ardından Şeritteki **Özellikler** 'e veya sağ tıklama menüsünden Özellikler 'e tıklayın. Aşağıdaki sekmelerden ayarları değiştirin:

   - **Genel**: 
      - **Ad**: Orchestration grubunuzun adı
      - **Açıklama**: Orchestration grubu açıklaması (isteğe bağlı)
      - **Düzenleme grubu zaman aşımı (dakika cinsinden)**: tüm grup üyelerinin güncelleştirme yüklemesini tamamlaması için geçen süre üst sınırı.
      - **Düzenleme grubu üye zaman aşımı (dakika cinsinden)**: güncelleştirme yüklemesini gerçekleştirmek için gruptaki tek bir cihaz için zaman sınırı.

  - **Üye seçimi**:
     - **Site kodu**: Orchestration grubu için site kodu.
     - **Üyeler**: Orchestration grubuna yönelik ek cihazları seçmek için **Ekle** ' ye tıklayın. Seçili cihazı kaldırmak için **Kaldır** ' a tıklayın.

   - **Kural seçimi**:
      - **Makinelerin bir yüzdesinin aynı anda güncelleştirilmesine Izin verin**, ardından bu yüzde için bir sayı seçin veya girin. Düzenleme grubunun boyutuyla ilgili daha fazla esneklik sağlamak için bu ayarı kullanın. Örneğin, düzenleme grubunuz 50 cihaz içerir ve bu değeri 10 olarak ayarlayabilirsiniz. Yazılım güncelleştirme dağıtımı sırasında, Configuration Manager dağıtımı aynı anda beş cihazın çalıştırmasına izin verir. Daha sonra Orchestration grubunun boyutunu 100 cihaz olarak artırdıysanız, 10 cihaz aynı anda güncelleştirme yapılır.
      - **Bir dizi makinenin aynı anda güncelleştirilmesine Izin verin**, ardından bu belirli sayı için bir sayı seçin veya girin. Düzenleme grubunun genel boyutu ne olursa olsun, her zaman belirli sayıda cihaza sınırlamak için bu ayarı kullanın.
      - **Bakım sırasını belirtin**: seçili kaynakları uygun sırada sıralayın. Cihazların yazılım güncelleştirme dağıtımını Çalıştırma sırasını açıkça tanımlamak için bu ayarı kullanın.

   - **Ön betik**: 
       - Dağıtım çalışmadan *önce* her cihazda çalışan bir PowerShell betiği girin. Betik, `0` başarılı veya `3010` yeniden başlatma ile başarılı için bir değer döndürmelidir.
       
   - **Betik sonrası**:
      - Dağıtım çalıştıktan *sonra* her cihazda çalıştırılacak bir PowerShell betiği girin ve gerekirse bir yeniden başlatma gerçekleşir. Betik, `0` başarılı veya `3010` yeniden başlatma ile başarılı için bir değer döndürmelidir.
  
   > [!WARNING]
   > Önceki betiklerin ve betikleri düzenleme grupları için kullanılmadan önce test edilmiş olduğundan emin olun. Betiklerin ve son betiklerin zaman aşımı değildir ve düzenleme grubu üye zaman aşımına ulaşılana kadar çalışır.


## <a name="start-orchestration"></a>Düzenleme Başlat

1. [Yazılım güncelleştirmelerini](deploy-software-updates.md) düzenleme grubunun üyelerini içeren bir koleksiyona dağıtın.

1. Düzenleme, gruptaki herhangi bir istemci son tarihte veya bakım penceresi sırasında herhangi bir yazılım güncelleştirmesini yüklemeye çalıştığında başlar. Bu, tüm grup için başlar ve cihazların düzenleme grubu kurallarını izleyerek güncelleştirilmesini sağlar.
1. Orchestration **grubunu düzenleme grubu** düğümünden seçerek el ile başlatabilir, sonra şeritten düzenlemeyi **Başlat** ' ı veya sağ tıklama menüsünü seçebilirsiniz.
1. Bir düzenleme grubu *başarısız* durumdaysa:
   1. Orchestration 'un neden başarısız olduğunu saptayın ve sorunları çözün.
   1. [Grup üyelerinin düzenleme durumunu sıfırlayın](#bkmk_reset).
   1. Düzenleme **grubu** düğümünden düzenleme işlemini yeniden başlatmak Için düzenlemeye **başla** düğmesine tıklayın.
   [![Düzenleme Başlat](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - Düzenleme grupları yalnızca yazılım güncelleştirme dağıtımları için geçerlidir. Diğer dağıtımlar için uygulanamazlar.
> - Bir Orchestration grubu üyesine sağ tıklayıp **düzenleme grubu üyesini Sıfırla**' yı seçebilirsiniz. Bu sayede düzenleme işlemini yeniden çalıştırabilirsiniz.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a>Düzenleme gruplarını izleme

**Varlıklar ve uyum** çalışma alanından **Orchestration grubu** düğümünü seçin. Gruplar hakkında bilgi almak için aşağıdaki sütunlardan birini ekleyin:

- **Orchestration adı**: Orchestration grubunuzun adı.
- **Site kodu**: Grup için site kodu.
- **Düzenleme türü**: aşağıdaki türlerden biridir:
   - Sayı
   - Yüzde
   - Sequence

- **Orchestration değeri**: aynı anda bir kilit alabileceğiniz üye sayısı veya üye yüzdesi. **Orchestration değeri** yalnızca **Orchestration türü** *sayı* ya da *yüzde*olduğunda doldurulur.  
- **Düzenleme durumu**: düzenleme sırasında devam ediyor. Devam ederken boşta.
- **Düzenleme başlangıç zamanı**: Orchestration 'un başladığı tarih ve saat.
- **Geçerli sıra numarası**: Grup düzenleme 'nin hangi üyesinin etkin olduğunu gösterir. Bu sayı, üyenin **sıra numarasına** karşılık gelir.  
- **Düzenleme zaman aşımı (dakika cinsinden)**: Grup oluşturulurken **genel** sayfada ayarlanan **düzenleme grubu zaman aşımı süresi (dakika cinsinden)** veya grup düzenlenirken **genel** sekmesi.
- **Düzenleme grubu üye zaman aşımı (dakika cinsinden)**: Grup oluşturulurken **genel** sayfada ayarlanan **düzenleme grubu üye zaman aşımı süresi (dakika cinsinden)** veya grup düzenlenirken **genel** sekme değeri.
- **Orchestration grup kimliği**: grubun KIMLIĞI, kimlik günlüklerde ve veritabanında kullanılır.
- **Orchestration grubu BENZERSIZ kimliği**: grubun benzersiz kimliği, benzersiz kimlik ise günlüklerde ve veritabanında kullanılır.

## <a name="monitor-orchestration-group-members"></a>Düzenleme grubu üyelerini izleme

**Düzenleme grubu** düğümünde bir düzenleme grubu seçin. Şeritte **üyeleri göster**' i seçin. Grubun üyelerini ve bunların düzenleme durumlarını görebilirsiniz. Üyeler hakkında bilgi almak için aşağıdaki sütunlardan birini ekleyin:

- **Ad**: düzenleme grubu üyesinin cihaz adı
- **Geçerli durum**: size üye cihazın durumunu verir.
   - Düzenleme sırasında **devam ediyor** .
   - **Bekliyor**: istemcinin, güncelleştirmeleri yüklemeye yönelik kilidi beklediği anlamına gelir.
   - Düzenleme tamamlandığında veya çalışmadığı zaman **boşta kalır** .
- **Durum kodu**: Orchestration grubu üyesine sağ tıklayıp **düzenleme grubu üyesini Sıfırla**' yı seçebilirsiniz. Bu sıfırlama, düzenleme işlemini yeniden çalıştırmanıza olanak sağlar. Durumlar şunları içerir: 
   - Boş
   - Bekliyor, cihaz kendi cihazını bekliyor
   - Devam eden, güncelleştirme yükleme
   - Başarısız
   - Yeniden başlatma bekleniyor
- **Kilit alınma süresi**: kilitleri, ilkesi temel alınarak istemci tarafından istenir. İstemci bir kilit aldıktan sonra, üzerinde düzenleme tetiklenir.  
-**Son durum raporlanan süre**: üyenin bir durumu bildirdiği zaman.
- **Sıra numarası**: güncelleştirme yükleme sırasındaki istemci konumu.
- **Site kodu**: üyenin site kodu.
- **Istemci etkinliği**: istemcinin etkin veya devre dışı olduğunu bildirir.
- **Birincil**kullanıcılar: cihaz Için birincil kullanıcı.
- **Istemci türü**: istemcinin ne tür bir cihaz olduğunu.
- **Şu anda oturum açmış olan Kullanıcı**: cihazda Şu anda oturum açmış olan kullanıcı.
- **OG ID**: üyenin ait olduğu düzenleme grubunun kimliği.
- **OG BENZERSIZ kimliği**: üyenin ait olduğu Orchestration grubunun benzersiz kimliği.
- **Kaynak kimliği**: CIHAZıN kaynak kimliği.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a>Bir grup üyesinin düzenleme durumunu sıfırlayın

Bir grup üyesinde düzenleme *işlemini* yeniden çalıştırmak istiyorsanız, onun durumunu veya *başarısız*gibi temizleyebilirsiniz. Durumu temizlemek için, düzenleme grubu üyesine sağ tıklayın ve **düzenleme grubu üyesini Sıfırla**' yı seçin. Ayrıca şeritten **düzenleme grubu üyesini Sıfırla** ' ya tıklayabilirsiniz. Durumu sıfırlamadan önce, neden başarısız olduğunu görmek ve bulunan sorunları düzeltmek için istemcisini denetlemeniz gerekir.
   [![Düzenleme grubu üyesini Sıfırla](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>Günlük dosyaları

İzleme ve sorun gidermeye yardımcı olması için site sunucusunda aşağıdaki günlük dosyalarını kullanın:

### <a name="site-server"></a>Site sunucusu

- **Policypv. log**: sitenin düzenleme grubunu istemcilere hedeflediğini gösterir.
- **SMS_OrchestrationGroup. log**: Orchestration grubunun davranışlarını gösterir.

### <a name="client"></a>İstemci

- **MaintenanceCoordinator. log**: kilit alma, güncelleştirme yükleme, ön betik sonrası ve kilit bırakma işlemini gösterir.
- **UpdateDeployment. log**: güncelleştirme yükleme işlemini gösterir.
- **Policyagent. log**: istemcinin bir düzenleme grubunda olup olmadığını denetler.

## <a name="next-steps"></a>Sonraki adımlar

[Yazılım güncelleştirmelerini dağıtma](deploy-software-updates.md)