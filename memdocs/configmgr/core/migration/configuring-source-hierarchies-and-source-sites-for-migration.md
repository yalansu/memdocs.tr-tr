---
title: Geçiş kaynağı hiyerarşileri
titleSuffix: Configuration Manager
description: Configuration Manager geçerli dal ortamınıza veri geçirebilmeniz için bir kaynak hiyerarşisini ve kaynak siteleri yapılandırın.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718927"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Güncel dala Configuration Manager geçiş için kaynak hiyerarşileri ve kaynak siteleri yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dal ortamınıza veri geçişini etkinleştirmek için, desteklenen bir Configuration Manager kaynak hiyerarşisi ve bu hiyerarşide geçirmek istediğiniz verileri içeren bir veya daha fazla kaynak sitesi yapılandırmanız gerekir.  

> [!NOTE]  
>  Geçiş işlemleri hedef hiyerarşide en üst düzey sitede çalıştırılır. Bir birincil alt siteye bağlı bir Configuration Manager konsolu kullandığınızda geçişi yapılandırırsanız, yapılandırmanın merkezi yönetim sitesine çoğaltılması için zaman vermeniz, başlatılması ve sonra durumu bağlı olduğunuz birincil siteye geri çoğaltılması gerekir.  

 Kaynak hiyerarşisini belirtmek ve ek kaynak siteler eklemek için aşağıdaki bölümlerdeki bilgileri ve yordamları kullanın. Bu yordamları tamamladıktan sonra, geçiş işleri oluşturabilir ve verileri kaynak hiyerarşisinden hedef hiyerarşiye geçirmeye başlayabilirsiniz.  

-   [Geçiş için bir kaynak hiyerarşisi belirtin](#BKBM_ConfigSrcHierarchy)  

-   [Kaynak hiyerarşisinin ek kaynak sitelerini tanımla](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a>Geçiş için bir kaynak hiyerarşisi belirtin  
 Hedef hiyerarşinize veri geçirmek için, geçirmek istediğiniz verileri içeren desteklenen bir kaynak hiyerarşisi belirtmeniz gerekir. Varsayılan olarak, bu hiyerarşinin en üst düzey sitesi, kaynak hiyerarşisinin kaynak sitesi haline gelir. Configuration Manager 2007 hiyerarşisinden geçiş yaparsanız, ilk kaynak sitesinden veriler toplandıktan sonra geçiş için ek kaynak siteler ayarlayabilirsiniz. Bir System Center 2012 Configuration Manager veya Configuration Manager geçerli dal hiyerarşisinden geçiş yaparsanız, kaynak hiyerarşisinden veri geçirmek için ek kaynak siteler ayarlamanız gerekmez. Bunun nedeni, Configuration Manager sürümlerinin kaynak hiyerarşinin en üst düzey sitesinde bulunan paylaşılan bir veritabanını kullanması. Paylaşılan veritabanı, geçirebileceğiniz tüm bilgileri içerir.  

 Geçiş için bir kaynak hiyerarşisi belirtmek ve bir Configuration Manager 2007 hiyerarşisindeki ek kaynak siteleri belirlemek için aşağıdaki yordamları kullanın.  

 Bu yordamı, hedef hiyerarşisine bağlı bir Configuration Manager konsoluyla çalıştırın:  

### <a name="to-configure-a-source-hierarchy"></a>Kaynak hiyerarşisini yapılandırmak için   

1. Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2. **Yönetim** çalışma alanında, **Geçiş**'i genişletin ve **Kaynak Hiyerarşisi**'ni tıklatın.  

3. **Giriş** sekmesinde, **geçiş** grubunda, **kaynak hiyerarşisini belirt**' e tıklayın.  

4. Kaynak hiyerarşisini **belirtin** iletişim kutusunda, **kaynak hiyerarşisi**için **Yeni kaynak hiyerarşisi**' ni seçin.  

5. **Üst düzey Configuration Manager site sunucusu**için, desteklenen bir kaynak hiyerarşinin en üst düzey sitesinin adını veya IP adresini girin.  

6. Aşağıdaki izinlere sahip kaynak site erişim hesaplarını belirtin:  

   - Kaynak site hesabı: kaynak hiyerarşisindeki belirtilen en üst düzey site için SMS sağlayıcısı için **Oku** izni. Dağıtım noktası Paylaşımı ve yükseltmeleri, kaynak hiyerarşisindeki site için **değiştirme** ve **silme** izinleri gerektirir.

   - Kaynak site veritabanı hesabı: kaynak hiyerarşisindeki belirtilen en üst düzey site için SQL Server veritabanı için **okuma** ve **yürütme** izni.  

     Bilgisayar hesabının kullanımını belirtirseniz Configuration Manager, hedef hiyerarşinin en üst düzey sitesinin bilgisayar hesabını kullanır. Bu seçenek için, bu hesabın, kaynak hiyerarşinin en üst düzey sitesinin bulunduğu etki alanındaki **Dağıtılmış com kullanıcıları** güvenlik grubunun bir üyesi olduğundan emin olun.  

7. Kaynak ve hedef hiyerarşileri arasında dağıtım noktaları paylaşmak için **kaynak site sunucusu için dağıtım noktası paylaşımını etkinleştir** onay kutusunu seçin. Dağıtım noktası paylaşımını Şu anda etkinleştirmezseniz, veri toplama işlemi tamamlandıktan sonra kaynak sitenin kimlik bilgilerini düzenleyerek bunu yapabilirsiniz.  

8. Yapılandırmayı kaydetmek için **Tamam** ' ı tıklatın. Bu, **veri toplama durumu** iletişim kutusunu açar ve veri toplama otomatik olarak başlar.  

9. Veri toplama tamamlandığında, **veri toplama durumu** iletişim kutusunu kapatmak ve yapılandırmayı gerçekleştirmek için **Kapat** ' a tıklayın.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a>Kaynak hiyerarşisinin ek kaynak sitelerini tanımla  
 Desteklenen bir kaynak hiyerarşisini yapılandırdığınızda, bu hiyerarşinin en üst düzey sitesi otomatik olarak bir kaynak site olarak yapılandırılır ve veriler bu siteden otomatik olarak toplanır. Gerçekleştirebileceğiniz sonraki eylem, kaynak hiyerarşisi tarafından çalıştırılan Configuration Manager sürümüne bağlıdır:  

-   Configuration Manager 2007 kaynak hiyerarşisi için, ilk kaynak site için veri toplama işlemi bittikten sonra, bu ilk kaynak siteden geçişe başlayabilir veya kaynak hiyerarşisinden ek kaynak siteleri ayarlayabilirsiniz. Yalnızca bir alt siteden kullanılabilir olan verileri geçirmek için, Configuration Manager 2007 hiyerarşisi için ek kaynak siteleri ayarlayın. Örneğin, kaynak hiyerarşisindeki bir alt sitede oluşturulduğunda geçirmek istediğiniz içerikle ilgili verileri toplamak üzere ek kaynak siteler yapılandırabilir ve kaynak hiyerarşisinin en üst sitesinde kullanılamaz.  

-   Bir System Center 2012 Configuration Manager veya Configuration Manager geçerli dal kaynak hiyerarşisi için ek kaynak siteleri yapılandırmanız gerekmez. Bunun nedeni, Configuration Manager sürümlerinin kaynak hiyerarşinin en üst düzey sitesinde bulunan paylaşılan bir veritabanını kullanması. Paylaşılan veritabanı, kaynak hiyerarşisindeki tüm sitelerden geçirebileceğiniz tüm bilgileri içerir. Bu, geçirebileceğiniz verileri kaynak hiyerarşisinin en üst düzey sitesinden kullanılabilir hale getirir.  

Configuration Manager 2007 kaynak hiyerarşisi için ek kaynak siteleri yapılandırdığınızda, kaynak hiyerarşinin en üstündeki ek kaynak siteleri en alta yapılandırmanız gerekir. Alt sitelerini kaynak siteler olarak yapılandırmadan önce bir üst siteyi kaynak site olarak yapılandırmanız gerekir.  

Configuration Manager 2007 kaynak hiyerarşisi için ek kaynak siteleri yapılandırmak üzere aşağıdaki yordamı kullanın:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Kaynak hiyerarşisindeki ek kaynak siteleri belirlemek için 

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında, **Geçiş**'i genişletin ve **Kaynak Hiyerarşisi**'ni tıklatın.  

3.  Kaynak site olarak yapılandırmak istediğiniz siteyi seçin.  

4.  **Giriş** sekmesinde, **Kaynak Site** grubunda, **Yapılandır**'ı tıklatın.  

5.  Kaynak **site kimlik bilgileri** iletişim kutusunda, kaynak site erişim hesapları için, aşağıdaki izinlere sahip hesapları belirtin:  

    -   Kaynak site hesabı: kaynak hiyerarşisindeki belirtilen en üst düzey site için SMS sağlayıcısı için **Oku** izni. Dağıtım noktası Paylaşımı ve yükseltmeleri, kaynak hiyerarşisindeki site için **değiştirme** ve **silme** izinleri gerektirir.  

    -   Kaynak site veritabanı hesabı: kaynak hiyerarşisindeki belirtilen en üst düzey site için SQL Server veritabanı için **okuma** ve **yürütme** izni.  

    Bilgisayar hesabının kullanımını belirtirseniz Configuration Manager, hedef hiyerarşinin en üst düzey sitesinin bilgisayar hesabını kullanır. Bu seçenek için, bu hesabın, kaynak hiyerarşinin en üst düzey sitesinin bulunduğu etki alanındaki **Dağıtılmış com kullanıcıları** güvenlik grubunun bir üyesi olduğundan emin olun.  

6.  Kaynak ve hedef hiyerarşileri arasında dağıtım noktaları paylaşmak için **kaynak site sunucusu için dağıtım noktası paylaşımını etkinleştir** onay kutusunu seçin. Dağıtım noktası paylaşımını Şu anda etkinleştirmezseniz, veri toplama işlemi tamamlandıktan sonra kaynak sitenin kimlik bilgilerini düzenleyerek bunu yapabilirsiniz.  

7. Yapılandırmayı kaydetmek için **Tamam** ' ı tıklatın. Bu, **veri toplama durumu** iletişim kutusunu açar ve veri toplama otomatik olarak başlar.  

8.  Veri toplama tamamlandığında, yapılandırmayı gerçekleştirmek için **Kapat** ' a tıklayın.  
