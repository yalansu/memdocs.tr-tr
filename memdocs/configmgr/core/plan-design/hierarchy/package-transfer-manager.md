---
title: Paket Aktarma Yöneticisi
titleSuffix: Configuration Manager
description: Configuration Manager ' deki Paket Aktarma Yöneticisi 'nin bir site sunucusundan uzak dağıtım noktalarına içerik aktarma şeklini anlayın.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722455"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Paket Aktarma Yöneticisi Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager bir sitede, Paket Aktarma Yöneticisi, bir site sunucusu bilgisayarından bir sitedeki uzak dağıtım noktalarına içerik aktarımını yöneten SMS_Executive hizmetinin bir bileşenidir. (Uzak dağıtım noktası, site sunucusu bilgisayarında bulunmayan bir bilgisayardır.) Paket Aktarma Yöneticisi Yönetici tarafından yapılandırmayı desteklemez, ancak nasıl çalıştığını anlamak İçerik Yönetimi altyapınızı planlamaya yardımcı olabilir. Ayrıca içerik dağıtımı ile ilgili sorunları çözmenize yardımcı olabilir.


Bir sitedeki bir veya daha fazla uzak dağıtım noktasına içerik dağıttığınızda, **Dağıtım Yöneticisi** bir içerik aktarma işi oluşturur. Daha sonra, birincil ve ikincil site sunucularında Paket Aktarma Yöneticisi 'ne içeriği uzak dağıtım noktalarına aktarmaya bildirir.

 Paket Aktarma Yöneticisi, eylemlerini site sunucusundaki **pkgxfermgr. log** dosyasında günlüğe kaydeder. Günlük dosyası, Paket Aktarma Yöneticisi 'nin etkinliklerini görüntüleyebileceğiniz tek konumdur.  

> [!NOTE]  
>  Configuration Manager önceki sürümlerinde, dağıtım Yöneticisi içeriğin uzak dağıtım noktasına aktarımını yönetir. Dağıtım Yöneticisi ayrıca siteler arasında içerik aktarımını yönetir. Configuration Manager, dağıtım Yöneticisi iki site arasında içerik aktarımını yönetmeye devam eder. Ancak, Paket Aktarma Yöneticisi artık büyük sayıda dağıtım noktasına içerik aktarımını yönetir. Bu, hem siteler hem de bir sitedeki dağıtım noktaları arasındaki içerik dağıtımının genel performansını artırmaya yardımcı olur.  

İçeriği standart bir dağıtım noktasına aktarmak için, Paket Aktarma Yöneticisi, Configuration Manager önceki sürümlerinde çalışan dağıtım Yöneticisi ile aynı şekilde çalışır. Diğer bir deyişle, dosyaların her bir uzak dağıtım noktasına aktarımını etkin bir şekilde yönetir. Ancak, bir çekme dağıtım noktasına içerik dağıtmak için, Paket Aktarma Yöneticisi, çekme dağıtım noktasını içeriğin kullanılabilir olduğunu bildirir. Çekme dağıtım noktası daha sonra aktarım sürecini devralır.  

Aşağıdaki bilgiler, Paket Aktarma Yöneticisi 'nin standart dağıtım noktalarına içerik aktarımını nasıl yönettiğini ve çekme dağıtım noktaları olarak yapılandırılmış dağıtım noktalarını nasıl yönettiğini açıklar:
1.  **Yönetici, bir sitedeki bir veya daha fazla dağıtım noktasına içerik dağıtır.**  

    -   **Standart dağıtım noktası:** Dağıtım Yöneticisi bu içerik için bir içerik aktarma işi oluşturur.  

    -   **Çekme dağıtım noktası:** Dağıtım Yöneticisi bu içerik için bir içerik aktarma işi oluşturur.  

2.  **Dağıtım Yöneticisi ön denetimleri çalıştırır.**  

    -   **Standart dağıtım noktası:** Dağıtım Yöneticisi, her dağıtım noktasının içeriği almaya hazırlandığından emin olmak için temel bir denetim çalıştırır. Bu denetim sonrasında, dağıtım Yöneticisi, Paket Aktarma Yöneticisi 'ne içeriğin dağıtım noktasına aktarımını başlatmasını bildirir.  

    -   **Çekme dağıtım noktası:** Dağıtım Yöneticisi, Paket Aktarma Yöneticisi 'ni başlatır, daha sonra çekme dağıtım noktasına yeni bir içerik aktarma işi olduğunu bildirir. Dağıtım Yöneticisi, her istek temelli dağıtım noktası kendi içerik aktarımlarını yönettiğinden, çekme dağıtım noktaları olan uzak dağıtım noktalarının durumunu denetlemez.  

3.  **Paket Aktarma Yöneticisi içerik aktarmaya hazırlar.**  

    -   **Standart dağıtım noktası:** Paket Aktarma Yöneticisi, belirtilen her uzak dağıtım noktasının tek örnekli içerik deposunu inceler. Bunun amacı, zaten o dağıtım noktasındaki dosyaları belirlemektir. Ardından, Paket Aktarma Yöneticisi, yalnızca henüz mevcut olmayan dosyaları aktarmak için kuyruğa alınır.  

        > [!NOTE]  
        >  Dağıtım noktasındaki her dosyayı dağıtım noktasına kopyalamak için, dosyalar dağıtım noktasının tek örnek deposunda zaten mevcut olsa bile, içerik için yeniden **Dağıt** eylemini kullanın.  

    -   **Çekme dağıtım noktası:** Dağıtım içindeki her çekme dağıtım noktası için, Paket Aktarma Yöneticisi, içeriğin kullanılabilir olup olmadığını doğrulamak için çekme dağıtım noktaları kaynak dağıtım noktalarını denetler.  

        -   İçerik en az bir kaynak dağıtım noktasında kullanılabilir olduğunda, Paket Aktarma Yöneticisi, söz konusu çekme dağıtım noktasına bir bildirim gönderir. Bildirim, dağıtım noktasını içerik aktarma işlemini başlatmak için yönlendirir. Bildirim dosya adlarını ve boyutları, öznitelikleri ve karma değerleri içerir.  

        -   İçerik henüz kullanılabilir olmadığında, Paket Aktarma Yöneticisi dağıtım noktasına bir bildirim göndermez. Bunun yerine, içerik kullanılabilir olana kadar 20 dakikada bir kontrolü tekrarlar. Ardından, içerik kullanılabilir olduğunda, Paket Aktarma Yöneticisi bu istek temelli dağıtım noktasına bildirim gönderir.  

        > [!NOTE]  
        >  Dağıtım noktasındaki her dosyayı dağıtım noktasına kopyalamak için çekme dağıtım noktası için, dosyalar çekme dağıtım noktasının tek örnek deposunda zaten mevcut olsa bile, içerik için yeniden **Dağıt** eylemini kullanın.  

4.  **İçerik aktarmaya başlar.**  

    -   **Standart dağıtım noktası:** Paket Aktarma Yöneticisi, dosyaları her bir uzak dağıtım noktasına kopyalar. Standart dağıtım noktasına aktarım sırasında:  

        -   Varsayılan olarak, Paket Aktarma Yöneticisi üç benzersiz paketi eşzamanlı olarak işleyebilir ve bunları paralel olarak beş dağıtım noktasına dağıtabilir. Toplu olarak, bunlara **eşzamanlı dağıtım ayarları**denir. Eşzamanlı dağıtımı ayarlamak için, her sitenin **yazılım dağıtım bileşeni özelliklerinde** **genel** sekmesine gidin.  

        -   Paket Aktarma Yöneticisi, içerik bu dağıtım noktasına aktarılırken her bir dağıtım noktasının zamanlama ve ağ bant genişliği yapılandırmasını kullanır. Bu ayarları yapılandırmak için, her bir uzak dağıtım noktasının **özelliklerinde** , **zamanlama** ve **oran limitleri** sekmelerine gidin. Daha fazla bilgi için bkz. [Configuration Manager içeriği ve içerik altyapısını yönetme](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Çekme dağıtım noktası:** Çekme dağıtım noktası bir bildirim dosyası aldığında, dağıtım noktası, içeriği aktarma işlemini başlatır. Aktarım işlemi her çekme dağıtım noktasında bağımsız olarak çalışır:  

        1.   Çekme dağılımı, içerik dağıtımında, kendi tek örnek deposunda bulunmayan dosyaları tanımlar ve bu içeriği kaynak dağıtım noktalarından birinden indirmeye hazırlar.  

        2.   Daha sonra, çekme dağıtım noktası, içeriği kullanılabilir olan bir kaynak dağıtım noktası bulana kadar, kaynak dağıtım noktalarının her birini sırayla denetler. Çekme dağıtım noktası, içeriğe sahip bir kaynak dağıtım noktasını belirlediğinde, bu içeriğin indirilmeye başlar.  

        > [!NOTE]  
        >  Çekme dağıtım noktası tarafından içerik indirme işlemi, Configuration Manager istemcileri tarafından kullanılan ile aynıdır. Çekme dağıtım noktası tarafından içerik aktarımı için eşzamanlı aktarım ayarları kullanılmaz. Standart dağıtım noktaları için yapılandırdığınız zamanlama ve azaltma seçenekleri her ikisi de kullanılmaz.  

5.  **İçerik aktarımı tamamlanır.**  

    -   **Standart dağıtım noktası:** Paket Aktarma Yöneticisi, dosyaları belirlenen her bir uzak dağıtım noktasına aktarmayı tamamladıktan sonra, dağıtım noktasındaki içeriğin karmasını doğrular. Daha sonra dağıtım Yöneticisi 'Ne dağıtımın tamamlandığını bildirir.  

    -   **Çekme dağıtım noktası:** Çekme dağıtım noktası içerik indirmeyi tamamladıktan sonra, dağıtım noktası içeriğin karmasını doğrular. Sonra, başarılı olduğunu belirtmek için site yönetim noktasına bir durum iletisi gönderir. 60 dakikadan sonra bu durum alınmaz, Paket Aktarma Yöneticisi yeniden uyku modundan çıkar. Çekme dağıtım noktasının içeriği indirip indirmediğini onaylamak için çekme dağıtım noktasını denetler. İçerik indirme işlemi devam ediyorsa, Paket Aktarma Yöneticisi, çekme dağıtım noktasını yeniden kontrol etmeden önce başka bir 60 dakika boyunca uyku moduna geçer. Çekme dağıtım noktası içerik aktarımını tamamlayana kadar bu döngü devam eder.  
