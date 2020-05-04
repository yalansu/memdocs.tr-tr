---
title: Sınır gruplarına yönelik yordamlar
titleSuffix: Configuration Manager
description: Sınır gruplarını, sınır olarak adlandırılan ilgili ağ konumlarını mantıksal olarak düzenlemek için yapılandırın.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715798"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Configuration Manager için sınır gruplarını yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, sınır gruplarının nasıl yapılandırılacağı hakkında yordamlar içerir. Başlamadan önce, sınır grubu kavramlarını anladığınızdan emin olun. Daha fazla bilgi için bkz. [sınır grupları](boundary-groups.md).



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a>Sınır grubu oluşturma  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **sınır grupları** düğümünü seçin.  

2.  **Giriş** sekmesinde, **Oluştur** grubunda, **sınır grubu oluştur**' u seçin.  

3.  **Sınır grubu oluştur** iletişim kutusunda, **genel** sekmesinde, bu sınır grubu için bir **ad** belirtin. İsteğe bağlı olarak bir **Açıklama**ekleyin.  

4.  Yeni sınır grubunu kaydetmek için **Tamam** ' ı seçin veya sınır grubunu yapılandırmak için sonraki bölüme geçin.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a>Sınır grubu yapılandırma  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **sınır grupları** düğümünü seçin.  

2.  Değiştirmek istediğiniz sınır grubunu seçin ve Şeritteki **Özellikler** ' i seçin. Bu eylem Özellikler penceresi sınır grubunu açar.  

Aşağıdaki ayarları yapılandırın:  
- [Sınır Ekle veya Kaldır](#bkmk_add)  
- [Site atamasını yapılandırma ve site sistemi sunucularını seçme](#bkmk_references)  
- [Geri dönüş davranışını yapılandırma](#bkmk_bg-fallback)  
- [Sınır grubu seçeneklerini yapılandırma](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a>Sınır Ekle veya Kaldır

Sınır grubu Özellikler penceresi, bu sınır grubunun üyesi olan sınırları değiştirmek için **genel** sekmesini kullanın:  

- Sınır eklemek için **Ekle**' yi seçin. Sınır Ekle penceresinde bir veya daha fazla sınırın onay kutusunu seçin ve **Tamam**' ı seçin.  

- Sınırları kaldırmak için listedeki sınırı seçin ve **Kaldır**' ı seçin.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a>Site atamasını yapılandırma ve site sistemi sunucularını seçme

Site atamasını ve ilişkili site sistemi sunucu yapılandırmasını değiştirmek için Özellikler penceresi sınır grubundaki **Başvurular** sekmesine geçin.  

- Bu sınır grubunu site ataması için istemciler tarafından kullanılmak üzere etkinleştirmek için, **site ataması için bu sınır grubunu kullan**' ı seçin. Sonra **atanan site** açılan listesinden bir site seçin. Daha fazla bilgi için bkz. [site ataması](boundary-groups.md#site-assignment).  

- Kullanılabilir site sistemi sunucularını bu sınır grubuyla ilişkilendirmek için, **Ekle**' yi seçin. Site sistemleri Ekle penceresi yalnızca desteklenen site sistem rollerine sahip olan sunucuları listeler. Bir veya daha fazla sunucunun onay kutusunu seçin ve **Tamam**' ı seçin. Bu sınır grubu için ilişkili site sistemi sunucuları olarak ekler.  

    > [!NOTE]  
    >  Hiyerarşideki herhangi bir siteden kullanılabilir site sistemlerinin herhangi bir birleşimini seçebilirsiniz. Seçilen site sistemleri, bu sınır grubunun üyesi olan her sınırın özelliklerindeki **site sistemleri** sekmesinde listelenir.  

- Bu sınır grubundan bir sunucuyu kaldırmak için sunucuyu seçip **Kaldır**' ı seçin.  

    > [!NOTE]  
    >  Site sistemlerini ilişkilendirirken bu sınır grubunun kullanımını durdurmak için, ilişkili site sistemi sunucuları olarak listelenen tüm sunucuları kaldırın.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a>Geri dönüş davranışını yapılandırma

Geri dönüş davranışını yapılandırmak için Özellikler penceresi sınır grubunda **ilişkiler** sekmesine geçin.  

- Başka bir sınır grubuyla ilişki oluşturmak için:  

  - **Add (Ekle)** seçeneğini belirleyin. Geri dönüş sınır grupları penceresinde yapılandırılacak sınır grubunu seçin.  

  - Aşağıdaki site sistem rolleri için bir geri dönüş süresi ayarlayın:  
    - Dağıtım noktası  
    - Yazılım güncelleştirme noktası  
    - Yönetim noktası  

      > [!Note]  
      > Örneğin, şube ofis sınır grubu için Özellikler penceresi açarsınız. Geri dönüş sınır grupları penceresinde, ana ofis sınır grubunu seçersiniz. Dağıtım noktası geri dönüş süresini olarak `20`ayarlayın. Bu yapılandırmayı kaydettiğinizde, şube ofisi sınır grubundaki istemciler 20 dakika sonra ana ofis sınır grubundaki dağıtım noktalarından içerik aramaya başlar.  

  - Belirli bir sınır grubuna geri dönüş yapılmasını engellemek için, sınır grubunu seçin ve ardından site sistemi rolü türü için **hiçbir şekilde geri dönüş** ' ı seçin. Bu eylem, *varsayılan site sınır grubunu*içerebilir.  

- Var olan bir ilişkinin yapılandırmasını değiştirmek için, listeden sınır grubunu seçin ve **Değiştir**' i seçin. Bu eylem yalnızca bu sınır grubu için geri dönüş Sınır Grupları penceresini açar.  
 
- Bir ilişkiyi kaldırmak için listedeki sınır grubunu seçin ve **Kaldır**' ı seçin.  

Daha fazla bilgi için bkz. [geri dönüş](boundary-groups.md#fallback). 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a>Sınır grubu seçeneklerini yapılandırma
<!--1356193-->
Sürüm 1806 ' den başlayarak, bu sınır grubundaki istemcilerin ek seçeneklerini yapılandırmak için **Seçenekler** sekmesine geçin. Daha fazla bilgi için bkz. [eş İndirmeleri Için sınır grubu seçenekleri](boundary-groups.md#bkmk_bgoptions).

- **Bu sınır grubunda eş indirmelere Izin ver**: Bu seçenek varsayılan olarak etkindir. Yönetim noktası, istemcilere eş kaynakları içeren içerik konumlarının bir listesini sağlar.  

    - **Eş Indirmeleri sırasında yalnızca aynı alt ağdaki eşleri kullanın**: Bu ayar yukarıdaki birine bağımlıdır. Bu seçeneği etkinleştirirseniz, yönetim noktası yalnızca istemciyle aynı alt ağda bulunan içerik konumu listesi eş kaynaklarını içerir.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a>Otomatik site ataması için bir geri dönüş sitesi yapılandırma  

İstemcileri atanmış bir site içeren bir sınır grubunda değilse, yüklendiklerinde bu siteye atayın.

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2.  Şeridin **giriş** sekmesinde, **siteler** grubunda, **Hiyerarşi ayarları**' nı seçin.  

3.  **Genel** sekmesinde **bir geri dönüş sitesi kullanmak**için onay kutusunu seçin. Ardından **geri dönüş sitesi** açılan listesinden bir site seçin.  

4.  Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  

Daha fazla bilgi için bkz. [site ataması](boundary-groups.md#site-assignment).


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a>Tercih edilen yönetim noktalarının kullanımını etkinleştir  

Daha fazla bilgi için bkz. [tercih edilen yönetim noktaları](boundary-groups.md#bkmk_preferred).

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **siteler** grubunda, **Hiyerarşi ayarları**' nı seçin.  

3. **Genel** sekmesinde, **istemciler sınır gruplarında belirtilen yönetim noktalarını kullanmayı tercih eder**' i seçin.  

4. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  

