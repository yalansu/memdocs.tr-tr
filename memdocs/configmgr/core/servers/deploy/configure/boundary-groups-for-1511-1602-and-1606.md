---
title: 1511, 1602 ve 1606 için sınır grupları
titleSuffix: Configuration Manager
description: Sınır gruplarını 1511, 1602 ve 1606 Configuration Manager sürümleriyle birlikte kullanın.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721111"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Configuration Manager sürüm 1511, 1602 ve 1606 için sınır grupları

*Uygulama hedefi: Configuration Manager (geçerli dal)*
<!-- This topic drops from TOC with the release of version 1706 -->

Bu konudaki bilgiler 1511, 1602 ve 1606 Configuration Manager sürümler ile sınır gruplarını kullanmaya özgüdür.
Sürüm 1610 veya sonraki bir sürümü kullanıyorsanız, yeniden tasarlanan sınır gruplarının nasıl kullanılacağı hakkında bilgi için bkz. [sınır gruplarını yapılandırma](boundary-groups.md) .  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a>Sınır grupları  
 İlgili ağ konumlarını (sınırlar) mantıksal olarak gruplandırarak altyapınızı yönetmeyi kolaylaştırmak için sınır grupları oluşturabilirsiniz. Sınır gruplarını kullanabilmeniz için önce sınır gruplarına sınır atamanız gerekir. İstemciler sınır grubu yapılandırmasını aşağıdaki amaçlarla kullanır:  

-   Otomatik site ataması  

-   İçeriğin konumu  

-   Tercih edilen yönetim noktaları

    Tercih edilen yönetim noktalarını kullanacaksanız, bu seçeneği hiyerarşi için etkinleştirmeniz ve sınır grubu yapılandırmasının içinden olmaması gerekir. Bu konunun ilerleyen kısımlarında *tercih edilen yönetim noktalarının kullanımını etkinleştirmek için* bölümüne bakın.  

Sınır gruplarını ayarlarken, sınır grubuna bir veya daha fazla sınır eklersiniz. Daha sonra bu sınırlar üzerinde bulunan istemciler tarafından kullanılacak ek ayarları yapılandırırsınız.  

#### <a name="to-create-a-boundary-group"></a>Sınır grubu oluşturmak için  

1.  Configuration Manager konsolunda, **Yönetim**  >  **hiyerarşisi yapılandırması**  >   **sınır grupları**' nı seçin.  

2.  **Giriş** sekmesinde, **Oluştur** grubunda, **sınır grubu oluştur**' u seçin.  

3.  **Sınır grubu oluştur** iletişim kutusunda, **genel** sekmesini seçin ve ardından bu sınır grubu için bir **ad** girin.  

4.  Yeni sınır grubunu kaydetmek için **Tamam ' ı** seçin.  

#### <a name="to-set-up-a-boundary-group"></a>Sınır grubu ayarlamak için  

1.  Configuration Manager konsolunda, **Yönetim**  >  **hiyerarşisi yapılandırması**  >   **sınır grupları**' nı seçin.  

2.  Değiştirmek istediğiniz sınır grubunu seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

4.  Sınır grubunun **Özellikler** iletişim kutusunda, bu sınır grubunun üyesi olan sınırları değiştirmek için **genel** sekmesini seçin:  

    -   Sınır eklemek için **Ekle**' yi seçin, bir veya daha fazla sınırın onay kutusunu işaretleyin ve ardından **Tamam**' ı seçin.  

    -   Sınırları kaldırmak için, sınırı seçin ve ardından **Kaldır**' ı seçin.  

5.  Site atamasını ve ilişkili site sistemi sunucu yapılandırmasını değiştirmek için **Başvurular** sekmesini seçin:  

    -   Bu sınır grubunu site ataması için istemciler tarafından kullanılmak üzere etkinleştirmek için, **site ataması için bu sınır grubunu kullan**onay kutusunu işaretleyin ve ardından **atanan site** açılan kutusundan bir site seçin.  

    -   Bu sınır grubuyla ilişkili kullanılabilir site sistemi sunucularını ayarlamak için:  

    1.  **Ekle**' yi seçin ve ardından bir veya daha fazla sunucunun onay kutusunu işaretleyin. Sunucular bu sınır grubu için ilişkili site sistemi sunucuları olarak eklenir. Yalnızca desteklenen site sistem rolü yüklenmiş sunucular kullanılabilir.  

        > [!NOTE]  
        >  Hiyerarşideki herhangi bir siteden kullanılabilir site sistemlerinin herhangi bir birleşimini seçebilirsiniz. Seçilen site sistemleri, bu sınır grubunun üyesi olan her sınırın özelliklerindeki **Site Sistemleri** sekmesinde listelenir.  

    2.  Bu sınır grubundan bir sunucuyu kaldırmak için sunucuyu seçin ve ardından **Kaldır**' ı seçin.  

        > [!NOTE]  
        >  Site sistemlerini ilişkilendirirken bu sınır grubunun kullanımını durdurmak için, ilişkili site sistemi sunucuları olarak listelenen tüm sunucuları kaldırmanız gerekir.  

    3.  Bu sınır grubu için bir site sistemi sunucusunun ağ bağlantı hızını değiştirmek için sunucuyu seçin ve **Bağlantıyı Değiştir**' i seçin.  

         Varsayılan olarak, her site sisteminin bağlantı hızı **hızlıdır**, ancak hızı **yavaş**olarak değiştirebilirsiniz. Bir dağıtımın ağ bağlantı hızı ve yapılandırması, bir istemcinin sunucudan içerik indirip indiremeyeceğini belirler.  

6.  Sınır grubu özelliklerini kapatmak ve yapılandırmayı kaydetmek için **Tamam** ' ı seçin.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Bir içerik dağıtım sunucusunu veya yönetim noktasını bir sınır grubuyla ilişkilendirmek için  

1.  Configuration Manager konsolunda, **Yönetim**  >  **hiyerarşisi yapılandırması**  >   **sınır grupları**' nı seçin.  

2.  Değiştirmek istediğiniz sınır grubunu seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

4.  Sınır grubunun **Özellikler** iletişim kutusunda, **Başvurular** sekmesini seçin.  

5.  **Site sistemi sunucularını Seç**altında **Ekle**' yi seçin, bu sınır grubuyla ilişkilendirmek istediğiniz site sistem sunucularının onay kutularını işaretleyin ve ardından **Tamam**' ı seçin.  

6.  İletişim kutusunu kapatmak ve sınır grubu yapılandırmasını kaydetmek için **Tamam** ' ı seçin.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Tercih edilen yönetim noktalarının kullanımını etkinleştirmek için  

1.  Configuration Manager konsolunda, **Yönetim**  >  **Site yapılandırması**  >  **siteler**' i seçin ve ardından **giriş** sekmesinde **Hiyerarşi ayarları**' nı seçin.  

2.  **Hiyerarşi ayarları**'nın **genel** sekmesinde **istemciler sınır gruplarında belirtilen yönetim noktalarını kullanmayı tercih eder**' i seçin.  

3.  İletişim kutusunu kapatmak ve yapılandırmayı kaydetmek için **Tamam** ' ı seçin.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Otomatik site ataması için bir geri dönüş sitesi ayarlamak için  

1. Configuration Manager konsolunda, **Yönetim**  >  **Site yapılandırması**  >   **siteler**' i seçin.  

2. **Giriş** sekmesinde, **siteler** grubunda, **Hiyerarşi ayarları**' nı seçin.  

3. **Genel** sekmesinde **bir geri dönüş sitesi kullan**onay kutusunu Işaretleyin ve ardından **geri dönüş sitesi** açılan listesinden bir site seçin.  

4. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  

   Aşağıdaki bölümlerde sınır grubu yapılandırmaları hakkında daha ayrıntılı bilgiler verilmiştir.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a>Site ataması hakkında  
 Her bir sınır grubunu istemciler için atanan bir site ile ayarlayabilirsiniz.  

-   Otomatik site ataması kullanan yeni yüklenmiş bir istemci, istemcinin geçerli ağ konumunu içeren bir sınır grubunun atanan sitesine katılır.  

-   Bir siteye atanmış olan istemci, istemci ağ konumunu değiştirdiğinde site atamasını değiştirmez. Örneğin, istemci farklı bir site ataması bulunan bir sınır grubundaki bir sınır tarafından temsil edilen yeni bir ağ konumuna gezinse, istemcinin atanan sitesi değişmeden kalır.  

-   Active Directory Sistem Keşfi yeni bir kaynak keşfettiğinde, keşfedilen kaynağın ağ bilgileri sınır gruplarındaki sınırlara göre değerlendirilir. Bu işlem yeni kaynağı, client push yükleme yöntemi tarafından kullanılmak üzere atanmış bir siteyle ilişkilendirir.  

-   Sınır, farklı atanmış sitelere sahip birden fazla sınır grubunun üyesi olduğunda, istemciler sitelerden birini rastgele seçer.  

-   Sınır grubunun atanan sitesindeki değişiklikler yalnızca yeni site atama eylemlerine uygulanır. Daha önce bir siteye atanan istemciler, bir sınır grubunun yapılandırmasındaki değişikliklere (veya kendi ağ konumlarına) göre site atamasını yeniden değerlendirmez.  

İstemci site ataması hakkında daha fazla bilgi için bkz. [istemcileri bir siteye atama](../../../../core/clients/deploy/assign-clients-to-a-site.md)içindeki [bilgisayarlar Için otomatik site atamasını kullanma](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) .  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a>İçerik konumu hakkında  
 Her bir sınır grubunu bir veya daha fazla dağıtım noktasıyla ve durum geçiş noktalarıyla ayarlayabilir ve aynı dağıtım noktalarını ve durum geçiş noktalarını birden çok sınır grubuyla ilişkilendirebilirsiniz.  

-   **Yazılım dağıtımı sırasında**istemciler, dağıtım içeriği için bir konum ister. Configuration Manager, istemcinin geçerli ağ konumunu içeren her bir sınır grubuyla ilişkili olan dağıtım noktalarının listesini istemciye gönderir.  

-   **İşletim sistemi dağıtımı sırasında**istemciler, durum geçiş bilgilerini göndermek veya almak için bir konum ister. Configuration Manager, istemcinin geçerli ağ konumunu içeren her bir sınır grubuyla ilişkili olan durum geçiş noktalarının listesini istemciye gönderir.  

Bu davranış, istemcinin içerik veya durum geçiş bilgilerinin aktarılacağı en yakın sunucuyu seçmesini sağlar.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Tercih edilen yönetim noktaları hakkında  
 Tercih edilen yönetim noktaları, istemcinin geçerli ağ konumuyla (sınır) ilişkili bir yönetim noktasını tanımlamasına olanak tanır.  

-   İstemci, tercih edilen bir yönetim noktasını, atanmış sitesinden tercih edilen olarak ayarlanmamış olan bir yönetim noktası kullanmadan önce kullanmayı dener.  

-   Bu seçeneği kullanmak için, hiyerarşi için etkinleştirmeniz ve tek tek birincil sitelerde sınır gruplarını, ilgili sınır grubunun ilişkili sınırlarıyla ilişkilendirilmesi gereken yönetim noktalarını içerecek şekilde ayarlamanız gerekir  

-   Tercih edilen yönetim noktaları ayarlandığında ve bir istemci, yönetim noktaları listesini düzenlediğinde, istemci, tercih edilen yönetim noktalarını, istemcinin atanan sitesindeki tüm yönetim noktalarını içeren atanmış yönetim noktaları listesinin üst kısmına koyar.  

> [!NOTE]  
>  Bir istemci dolaşımda olduğu gibi, bir dizüstü bilgisayar bir uzak ofis konumuna gitse ve ağ konumunu değiştirdiğinde, atanan sitesinden (tercih edilen yönetim noktalarını içeren) bir yönetim noktası kullanmayı denemeden önce yeni konumunda yerel siteden bir yönetim noktası (veya proxy yönetim noktası) kullanabilir.  Daha fazla bilgi için bkz. [İstemcilerin site kaynaklarını ve Configuration Manager hizmetleri nasıl bulduklarını anlama](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) .  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a>Çakışan sınırlar hakkında  
 Configuration Manager, içerik konumu için çakışan sınır yapılandırmalarının destekler:  

-   **İstemci içerik istediğinde**ve istemci ağ konumu birden fazla sınır grubuna aitse, Configuration Manager istemciye, içeriğe sahip olan tüm dağıtım noktalarının bir listesini gönderir.  

-   **İstemci, durum geçiş bilgilerini göndermek veya almak için bir sunucu istediğinde**ve istemci ağ konumu birden fazla sınır grubuna aitse, Configuration Manager istemciye istemcinin geçerli ağ konumunu içeren bir sınır grubuyla ilişkilendirilmiş tüm durum geçiş noktalarının listesini gönderir.  

Bu davranış, istemcinin içerik veya durum geçiş bilgilerinin aktarılacağı en yakın sunucuyu seçmesini sağlar.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a>Ağ bağlantısı hızı hakkında  
 Bir sınır grubundaki her site sistemi sunucusu için ağ bağlantı hızını ayarlayabilirsiniz. Bu ayar, bu sınır grubunun yapılandırmasına bağlı olarak bir site sistemine bağlanan istemciler için geçerlidir. Aynı site sistemi sunucusu için farklı sınır gruplarında farklı bir bağlantı hızı ayarlanabilir.  

 Varsayılan olarak, ağ bağlantı hızı **hızlı**olarak ayarlanır, ancak **yavaş**olarak değiştirebilirsiniz. Ağ bağlantı hızı ve dağıtım yapılandırması, istemci ilişkili bir sınır grubındayken bir istemcinin bir dağıtım noktasından içerik indirip indiremeyeceğini kontrol edebilir.  

 Ağ bağlantısı hızı yapılandırmasının istemcilerin içerik alma şeklini nasıl etkilediği hakkında daha fazla bilgi için bkz. [içerik kaynak konumu senaryoları](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
