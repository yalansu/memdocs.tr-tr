---
title: Configuration Manager’a bağlanma
titleSuffix: Configuration Manager
description: Configuration Manager masaüstü analiziyle bağlamak için nasıl yapılır Kılavuzu.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0835892788f86e9c246ed98d46658025fbc4180d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723722"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Masaüstü analiziyle Configuration Manager bağlama

Masaüstü Analizi Configuration Manager sıkı bir şekilde tümleşiktir. İlk olarak, en son özellikleri desteklemek için sitenin güncel olduğundan emin olun. Ardından Configuration Manager ' de masaüstü Analizi bağlantısını oluşturun. Son olarak, bağlantının sistem durumunu izleyin.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a>Siteyi Güncelleştir

İlk olarak, Configuration Manager sitenizin en az sürüm 1902 çalıştırdığından emin olun. Daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yüklemeyi](../core/servers/manage/install-in-console-updates.md).

Ayrıca, masaüstü analiziyle tümleştirmeyi desteklemek için 1902 güncelleştirme paketi (4500571) sürümünü yüklemeniz gerekir. Bu güncelleştirme hakkında daha fazla bilgi için bkz. [geçerli Configuration Manager dalı Için güncelleştirme paketi, sürüm 1902](https://support.microsoft.com/help/4500571).

1. Siteyi 1902 sürümüne yönelik güncelleştirme paketi ile güncelleştirin. Daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yüklemeyi](../core/servers/manage/install-in-console-updates.md).

2. İstemcileri güncelleştirin. Bu işlemi basitleştirmek için otomatik istemci yükseltmesini kullanmayı göz önünde bulundurun. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a>Hizmete bağlanma

> [!TIP]
> Sihirbazı başlatmadan önce, başlattıktan sonra sihirbazın dışında seçim yapmadan, adım 8 ' de bahsedilen hedef koleksiyonu oluşturun.

Configuration Manager masaüstü analizine bağlamak ve cihaz ayarlarını yapılandırmak için bu yordamı kullanın. Bu yordam, hiyerarşinizi bulut hizmetine eklemek için tek seferlik bir işlemdir.

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri** düğümünü seçin. Şeritte **Azure hizmetlerini yapılandır** ' ı seçin.

    > [!TIP]
    > Hizmete doğrudan **Masaüstü Analizi bakım** düğümünden bağlanın. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin ve **Masaüstü Analizi bakım** düğümünü seçin. *Yeni Masaüstü Analizi?* kutusunda, *Configuration Manager masaüstü Analizi hizmetine bağlamak*için ikinci bağlantıyı seçin.

2. Azure Hizmetleri Sihirbazı 'nın **Azure hizmetleri** sayfasında, aşağıdaki ayarları yapılandırın:

    - Configuration Manager nesne için bir **ad** belirtin.

    - Hizmeti tanımlamanızı sağlayacak isteğe bağlı bir **Açıklama** belirtin.

    - Kullanılabilir hizmetler listesinden **Masaüstü Analizi** ' ni seçin.

   **İleri**’yi seçin.

3. **Uygulama** sayfasında, uygun **Azure ortamını**seçin. Ardından Web uygulaması için **Araştır** ' ı seçin.

4. Bu hizmet için yeniden kullanmak istediğiniz mevcut bir uygulamanız varsa listeden seçin ve **Tamam**' ı seçin.

5. Çoğu durumda, Bu sihirbazla masaüstü Analizi bağlantısı için bir uygulama oluşturabilirsiniz. **Oluştur**’u seçin.<!-- 3572123 -->

    > [!TIP]
    > Uygulamayı bu sihirbazdan oluşturamıyoruz, uygulamayı Azure AD 'de el ile oluşturabilir ve ardından Configuration Manager içeri aktarabilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager için uygulama oluşturma ve içeri aktarma](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. **Sunucu uygulaması oluştur** penceresinde aşağıdaki ayarları yapılandırın:

    - **Uygulama adı**: Azure AD 'de uygulama için kolay bir ad.

    - **Giriş sayfası URL 'si**: bu değer Configuration Manager tarafından kullanılmaz, ancak Azure AD tarafından gerekli değildir. Varsayılan olarak bu `https://ConfigMgrService` değerine ayarlanır.

    - **Uygulama kimliği URI 'si**: Bu DEĞERIN Azure AD kiracınızda benzersiz olması gerekir. Hizmete erişim istemek için Configuration Manager istemcisi tarafından kullanılan erişim simgesindeki. Varsayılan olarak bu `https://ConfigMgrService` değerine ayarlanır.

    - **Gizli anahtar geçerlilik süresi**: açılan listeden **1 yıl** veya **2 yıl** seçeneklerinden birini belirleyin. Bir yıl, varsayılan değerdir.

    **Oturum aç '** ı seçin. Azure 'da başarıyla kimlik doğrulamasından geçtikten sonra, sayfada başvuru için **Azure AD kiracı adı** gösterilir.

    > [!NOTE]
    > Bu adımı **genel yönetici**olarak doldurun. Bu kimlik bilgileri Configuration Manager tarafından kaydedilmez. Bu kişi Configuration Manager izinleri gerektirmez ve Azure Hizmetleri Sihirbazı 'Nı çalıştıran aynı hesapla aynı olmalıdır.

    Azure AD 'de Web uygulaması oluşturmak için **Tamam** ' ı seçin ve sunucu uygulaması oluştur iletişim kutusunu kapatın. Sunucu uygulaması iletişim kutusunda **Tamam**' ı seçin. Ardından, Azure hizmetleri sihirbazının uygulama sayfasında **İleri** ' yi seçin.

7. **Tanılama verileri** sayfasında, aşağıdaki ayarları yapılandırın:

    - **TICARI kimlik**: Bu değer, kuruluşunuzun kimliğiyle otomatik olarak doldurulur. Aksi takdirde, proxy sunucunuzun devam etmeden önce tüm gerekli [uç noktalara](enable-data-sharing.md#endpoints) izin verecek şekilde yapılandırıldığından emin olun. Alternatif olarak, [Masaüstü Analizi portalından](monitor-connection-health.md#bkmk_ViewCommercialID)ticari kimliğinizi el ile alın.

    - **Windows 10 tanılama veri düzeyi**: en az **temel**seçin. [Tanılama veri düzeylerine](enable-data-sharing.md#diagnostic-data-levels) bakın
  
    - **Tanılama verilerinde cihaz adına Izin ver**: **Etkinleştir** ' i seçin

        > [!NOTE]
        > Windows 10 sürüm 1803 ' den başlayarak, cihaz adı varsayılan olarak Microsoft 'a gönderilmez. Cihaz adını göndermezseniz, masaüstü analizlerinin "Unknown" olarak görünmesi gerekir. Bu davranış, cihazları belirlemeyi ve değerlendirmeyi zorlaştırır.

   **İleri**’yi seçin. **Kullanılabilir işlevsellik** sayfasında, önceki sayfadan gelen Tanılama verileri ayarları Ile kullanılabilen masaüstü Analizi işlevleri gösterilmektedir. Devam etmek için **İleri ' yi** veya değişiklik yapmak için **geri** 'yi seçin.

    ![Azure hizmetleri sihirbazında örnek kullanılabilir Işlevsellik sayfası](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. **Koleksiyonlar** sayfasında, aşağıdaki ayarları yapılandırın:

    - **Görünen ad**: Masaüstü Analizi portalı bu adı kullanarak bu Configuration Manager bağlantıyı görüntüler. Farklı hiyerarşiler arasında ayrım yapmak ve ayrı Hiyerarşilerden koleksiyonları tanımlamak için kullanın. Ortamınızdaki birden fazla hiyerarşiyi kolayca ayırt etmek için terimleri kullanın, örneğin: *Test Laboratuvarı* veya *üretimi*.

    - **Hedef koleksiyon**: Bu koleksiyon, ticari kimliğiniz ve tanılama veri ayarlarınızla Configuration Manager yapılandırdığı tüm cihazları içerir. Bu, Configuration Manager masaüstü Analizi hizmetine bağlanan cihazların eksiksiz kümesidir.

    - **Hedef koleksiyondaki cihazlar giden iletişim için Kullanıcı tarafından kimliği doğrulanmış bir proxy kullanır**: varsayılan olarak bu değer **Hayır**' dır. Ortamınızda gerekliyse, **Evet**olarak ayarlayın.

    - **Masaüstü analiziyle eşitlenmek üzere belirli koleksiyonlar seçin**: **hedef koleksiyon** hiyerarşinizden ek koleksiyonlar eklemek için **Ekle** ' yi seçin. Bu koleksiyonlar, dağıtım planlarıyla gruplamak için masaüstü Analizi portalında kullanılabilir. Pilot ve pilot dışlama koleksiyonlarını eklediğinizden emin olun.  <!-- 4097528 -->

        > [!TIP]
        > Koleksiyonları Seç penceresi yalnızca **hedef koleksiyonla**sınırlanan koleksiyonları görüntüler.
        >
        > Aşağıdaki örnekte, hedef koleksiyonunuz olarak CollectionA ' yı seçersiniz. Daha sonra ek koleksiyonlar eklediğinizde, CollectionA, CollectionB ve CollectionC ' yi görürsünüz. CollectionD ekleyemezsiniz.
        >
        > - CollectionA: **Tüm sistemler** koleksiyonuyla sınırlıdır
        >     - CollectionB: CollectionA ile sınırlı
        >         - CollectionC: CollectionB ile sınırlı
        > - CollectionD: **Tüm sistemler** koleksiyonuyla sınırlı
        >
        > Dağıtım planlarıyla gruplandırmak üzere masaüstü Analizi portalında bulunan koleksiyonları yönetmek için, Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri** düğümünü seçin. **Masaüstü Analizi Azure hizmeti** ile ilişkili girişi seçin ve **Masaüstü Analizi koleksiyonu** sayfasında ayarlarınızı güncelleştirin.

        > [!IMPORTANT]
        > Bu koleksiyonlar, üyelik değişiklikleri olarak eşitlemeye devam eder. Örneğin, hedef koleksiyonunuz bir Windows 7 üyelik kuralıyla bir koleksiyon kullanır. Bu cihazlar Windows 10 ' a yükseltile, ve Configuration Manager koleksiyon üyeliğini değerlendirirken, bu cihazlar koleksiyon ve Masaüstü analizinden çıkar.

9. Sihirbazı tamamlayın.

Configuration Manager, hedef koleksiyondaki cihazları yapılandırmak için bir ayar ilkesi oluşturur. Bu ilke, cihazların Microsoft 'a veri göndermesini sağlamak için tanılama verileri ayarlarını içerir. Varsayılan olarak, istemciler ilkeyi her saat güncelleştirir. Yeni ayarları aldıktan sonra, verilerin masaüstü analizinden kullanılabilmesi birkaç saat daha olabilir.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a>Bağlantı durumunu izleme

Masaüstü analizi için cihazlarınızın yapılandırmasını izleyin. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **Masaüstü Analizi bakım** düğümünü genişletin ve **bağlantı sistem durumu** panosunu seçin.

Daha fazla bilgi için bkz. [bağlantı durumunu izleme](monitor-connection-health.md).

Configuration Manager, bağlantı oluşturma 60 dakika içinde koleksiyonlarınızı eşitler. Masaüstü Analizi portalında,**genel pilot**' a gidin ve Configuration Manager cihaz koleksiyonlarınızı görüntüleyin.

> [!NOTE]
> Masaüstü analizine Configuration Manager bağlantısı, hizmet bağlantı noktası üzerine bağımlıdır. Bu site sistemi rolündeki değişiklikler, bulut hizmetiyle eşitlemeyi etkileyebilir. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

## <a name="next-steps"></a>Sonraki adımlar

Cihazları masaüstü Analizi 'ne kaydetmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Cihazları kaydetme](enroll-devices.md)
