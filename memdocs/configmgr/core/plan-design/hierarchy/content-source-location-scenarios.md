---
title: İçerik kaynağı konumu
titleSuffix: Configuration Manager
description: İstemcilerin yavaş bir ağda içerik bulmasını sağlayan Configuration Manager ayarları hakkında bilgi edinin.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720243"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Configuration Manager içerik kaynak konumu senaryoları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sürüm 1610 ' den önceki Configuration Manager, istemcilerin yavaş bir ağda olduklarında içeriği nasıl ve nerede bulacağınızı tanımlamak üzere birleştirilmiş çeşitli ayarlar destekliyordu. Olası birleşimler, istemcilerin kullandıkları içerik konumunu ve tercih edilen içerik kaynağı kullanılabilir olmadığında bir geri dönüş konumunu başarıyla kullanıp kullanamayacağını etkiler.  

> [!IMPORTANT]  
> **Sitelerinizde 1511, 1602 veya 1606 sürümü**çalışıyorsa, bu konudaki bilgiler altyapınıza yöneliktir. Ayrıca, bu Configuration Manager sürümleriyle ilişkili sınır gruplarına özgü bilgiler için [1511, 1602 ve 1606 sürümleri Için sınır grupları](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md) konusuna bakın.
>
> **Siteleriniz 1610 veya sonraki bir sürümü kullanıyorsa**, istemcilerinizin kullanılabilir içeriğe sahip dağıtım noktalarını nasıl bulduklarını anlamak için [site sınırları ve sınır Configuration Manager grupları tanımlama](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) bölümündeki bilgileri kullanın.





**Aşağıdaki üç ayar, istemcilerin içerik istemesi durumunda davranışını tanımlar:**

- **İçerik için geri dönüş kaynak konumuna Izin ver** (etkin veya etkin değil): Bu, bir dağıtım noktasının **sınır grupları** sekmesinde etkinleştirebilmeniz için bir seçenektir. Bu, istemcinin tercih edilen bir dağıtım noktasında mevcut olmadığında geri dönüş konumu olarak yapılandırılmış bir dağıtım noktası kullanmasına izin verir.  

  - **Ağ bağlantısı hızı Için dağıtım davranışı**: her dağıtım, dağıtım noktasıyla bağlantı yavaş olduğunda kullanmak için aşağıdaki davranışlardan biriyle yapılandırılır:  

    -   **İçeriği dağıtım noktasından indir ve yerel olarak çalıştır**  

    -   **İçerik indirmeyin**: Bu seçenek yalnızca bir istemci içerik almak için bir geri dönüş konumu kullandığında kullanılır.  

    Bir dağıtım noktasının bağlantı hızı, bir sınır grubunun **Başvurular** sekmesinde yapılandırılır ve bu sınır grubuna özeldir.  

  - **İsteğe bağlı paket dağıtımı** (tercih edilen dağıtım noktalarına): Bu paketin içeriğini bir paketin veya uygulamanın özelliklerinin **dağıtım ayarları** sekmesinde **tercih edilen dağıtım noktalarına dağıt** seçeneğini belirlediğinizde etkinleştirilir. Bu seçenek etkinleştirildiğinde, bir istemci o dağıtım noktasından bu içeriği istediğinde, içeriği henüz olmayan tercih edilen bir dağıtım noktasına otomatik olarak kopyalamak için Configuration Manager yönlendirir.  


 **Aşağıdaki gereksinimler tüm senaryolar için geçerlidir:**


-   İçerik, bir geri dönüş dağıtım noktasında kullanılabilir  

-   Dağıtım noktaları çevrimiçi ve erişilebilir  


## <a name="scenario-1"></a>Senaryo 1  
 Aşağıdaki yapılandırma mevcut olduğunda geçerlidir:  

-   **Tercih edilen dağıtım noktasında içerik mevcuttur**  

-   **Geri dönüşe Izin ver**: etkin değil  

-   **Yavaş ağ Için dağıtım davranışı**: herhangi bir yapılandırma  


**Ayrıntılar:** (isteğe bağlı paket dağıtımı için yapılandırma bu senaryoya uygun değildir.)  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir.  

2.  İstemciye yönetim noktasından içeriği içeren tercih edilen dağıtım noktalarına bir içerik konumu listesi döndürülür.  

3.  İstemci, içeriği listedeki tercih edilen bir dağıtım noktasından indirir.  

## <a name="scenario-2"></a>Senaryo 2  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik mevcuttur**  

-   **Geri dönüşe Izin ver**: etkin  

-   **Yavaş ağ Için dağıtım davranışı**: içeriği indirmeyin  


**Ayrıntılar:** (isteğe bağlı paket dağıtımı için yapılandırma bu senaryoya uygun değildir.)  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir. İstemci, isteğin geri dönüş dağıtım noktalarına izin verildiğini belirten bir bayrak içerir.  

2.  Yönetim noktasından istemciye, içeriğin bulunduğu tercih edilen dağıtım noktalarını ve geri dönüş dağıtım noktalarını içeren bir içerik konumu listesi döndürülür.  

3.  İstemci, içeriği listedeki tercih edilen bir dağıtım noktasından indirir.  

## <a name="scenario-3"></a>3. Senaryo  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik mevcuttur**  

-   **Geri dönüşe Izin ver**: etkin  

-   **Yavaş ağ Için dağıtım davranışı**: içeriği indirme ve yükleme  


**Ayrıntılar:** (isteğe bağlı paket dağıtımı için yapılandırma bu senaryoya uygun değildir.)  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir. İstemci, isteğin geri dönüş dağıtım noktalarına izin verildiğini belirten bir bayrak içerir.  

2.  Yönetim noktasından istemciye, içeriğin bulunduğu tercih edilen dağıtım noktalarını ve geri dönüş dağıtım noktalarını içeren bir içerik konumu listesi döndürülür.  

3.  İstemci, içeriği listedeki tercih edilen bir dağıtım noktasından indirir.  

## <a name="scenario-4"></a>4. Senaryo  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik yok**  

-   **Bu paketin içeriğini tercih edilen dağıtım noktalarına dağıt** etkin değil  

-   **Geri dönüşe Izin ver**: etkin değil  

-   **Yavaş ağ Için dağıtım davranışı**: herhangi bir yapılandırma  


**Bilgileri**  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir.  

2.  İstemciye, yönetim noktasından içeriğe sahip olan tercih edilen dağıtım noktalarına sahip bir içerik konumu listesi döndürülür. Listede tercih edilen dağıtım noktası yok.  

3.  İstemci, ileti **içeriği kullanılabilir değil** ve yeniden deneme moduna geçtiğinde başarısız olur. Her saat yeni bir içerik isteği başlatılır.  

## <a name="scenario-5"></a>Senaryo 5  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik yok**  

-   **Bu paketin içeriğini tercih edilen dağıtım noktalarına dağıt** etkin değil  

-   **Geri dönüşe Izin ver**: etkin  

-   **Yavaş ağ Için dağıtım davranışı**: içeriği indirmeyin  


**Bilgileri**  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir. İstemci, isteğin geri dönüş dağıtım noktalarına izin verildiğini belirten bir bayrak içerir.  

2.  Yönetim noktasından istemciye, içeriğin bulunduğu tercih edilen dağıtım noktalarını ve geri dönüş dağıtım noktalarını içeren bir içerik konumu listesi döndürülür. İçeriğe sahip bir tercih edilen dağıtım noktası yok, ancak en az bir geri dönüş dağıtım noktası içeriğe sahip.  

3.  İstemci bir geri dönüş dağıtım noktası kullandığında için dağıtım özelliği **içeriği indirme** (istemciler içeriği almaya geri dönzaman kullanılır) olarak ayarlandığı için içerik indirilmez. İstemci, ileti **içeriği kullanılabilir değil** ve yeniden deneme moduna geçtiğinde başarısız olur. İstemci her saat yeni bir içerik isteği yapar.  

## <a name="scenario-6"></a>Senaryo 6  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik yok**  

-   **Bu paketin içeriğini tercih edilen dağıtım noktalarına dağıt** etkin değil  

-   **Geri dönüşe Izin ver**: etkin  

-   **Yavaş ağ Için dağıtım davranışı**: içeriği indirme ve yükleme  


**Bilgileri**  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir. İstemci, isteğin geri dönüş dağıtım noktalarının etkinleştirildiğini belirten bir bayrak içerir.  

2.  Yönetim noktasından istemciye, içeriğin bulunduğu tercih edilen dağıtım noktalarını ve geri dönüş dağıtım noktalarını içeren bir içerik konumu listesi döndürülür. İçeriğe sahip bir tercih edilen dağıtım noktası yoktur, ancak içeriği olan en az bir geri dönüş dağıtım noktası yoktur.  

3.  İstemci, bir geri dönüş dağıtım noktası kullandığında bu içerik, **Içerik indirmek ve yüklemek**üzere ayarlandığı için dağıtım özelliği listedeki bir geri dönüş dağıtım noktasından indirilir.  

## <a name="scenario-7"></a>Senaryo 7  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik yok**  

-   **Bu paketin içeriğini tercih edilen dağıtım noktalarına dağıt** etkin  

-   **Geri dönüşe Izin ver**: etkin değil  

-   **Yavaş ağ Için dağıtım davranışı**: herhangi bir yapılandırma  


**Bilgileri**  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir.  

2.  İstemciye, yönetim noktasından içeriğe sahip olan tercih edilen dağıtım noktalarına sahip bir içerik konumu listesi döndürülür. İçeriğe sahip bir tercih edilen dağıtım noktası yok.  

3.  İstemci, ileti **içeriği kullanılabilir değil** ve yeniden deneme moduna geçtiğinde başarısız olur. Her saat yeni bir içerik isteği yapılır.  

4.  Yönetim noktası, bir dağıtım Yöneticisi 'nin içeriği içerik isteği yapan istemcinin tercih edilen tüm dağıtım noktalarına dağıtması için bir tetikleyici oluşturur.  

5.  Dağıtım Yöneticisi, içeriği tercih edilen tüm dağıtım noktalarına dağıtır. Çoğu durumda, içerik, tercih edilen dağıtım noktalarına bir saat içinde başarıyla dağıtılır.  

6.  İstemci tarafından yönetim noktasına yeni bir içerik isteği başlatılır.  

7.  İstemciye, yönetim noktasından içeriğe sahip olan tercih edilen dağıtım noktalarına sahip bir içerik konumu listesi döndürülür. İstemci, içeriği listedeki tercih edilen bir dağıtım noktasından indirir.  

## <a name="scenario-8"></a>Senaryo 8  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik yok**  

-   **Bu paketin içeriğini tercih edilen dağıtım noktalarına dağıt** etkin  

-   **Geri dönüşe Izin ver**: etkin  

-   **Yavaş ağ Için dağıtım davranışı**: içeriği indirmeyin  


**Bilgileri**  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir. İstemci, isteğin geri dönüş dağıtım noktalarına izin verildiğini belirten bir bayrak içerir.  

2.  Yönetim noktasından istemciye, içeriğin bulunduğu tercih edilen dağıtım noktalarını ve geri dönüş dağıtım noktalarını içeren bir içerik konumu listesi döndürülür. İçeriğe sahip bir tercih edilen dağıtım noktası yok, ancak en az bir geri dönüş dağıtım noktası içeriğe sahip.  

3.  İstemci, bir geri dönüş dağıtım noktası kullandığında için dağıtım özelliği **indirilmez**olarak ayarlandığı için içerik indirilmez. İstemci, ileti **içeriği kullanılabilir değil** ve yeniden deneme moduna geçtiğinde başarısız olur. İstemci her saat yeni bir içerik isteği yapar.  

4.  Yönetim noktası, bir dağıtım Yöneticisi 'nin içeriği içerik isteği yapan istemcinin tercih edilen tüm dağıtım noktalarına dağıtması için bir tetikleyici oluşturur.  

5.  Dağıtım Yöneticisi, içeriği tercih edilen tüm dağıtım noktalarına dağıtır. Çoğu durumda, içerik, tercih edilen dağıtım noktalarına bir saat içinde başarıyla dağıtılır.  

6.  İstemci tarafından yönetim noktasına yeni bir içerik isteği başlatılır.  

7.  İstemciye, yönetim noktasından içeriğe sahip olan tercih edilen dağıtım noktalarına sahip bir içerik konumu listesi döndürülür.  

8.  İstemci, içeriği listedeki tercih edilen bir dağıtım noktasından indirir.  

## <a name="scenario-9"></a>Senaryo 9  
 Aşağıdaki konfigürasyonlar mevcuttur:  

-   **Tercih edilen dağıtım noktasında içerik yok**  

-   **Bu paketin içeriğini tercih edilen dağıtım noktalarına dağıt** etkin  

-   **Geri dönüşe Izin ver**: etkin  

-   **Yavaş ağ Için dağıtım davranışı**: içeriği indirme ve yükleme  


**Bilgileri**  

1.  İstemci, yönetim noktasına bir içerik isteği gönderir. İstemci, isteğin geri dönüş dağıtım noktalarına izin verildiğini belirten bir bayrak içerir.  

2.  Yönetim noktasından istemciye, içeriğin bulunduğu tercih edilen dağıtım noktalarını ve geri dönüş dağıtım noktalarını içeren bir içerik konumu listesi döndürülür. İçeriğe sahip bir tercih edilen dağıtım noktası yok, ancak en az bir geri dönüş dağıtım noktası içeriğe sahip.  

3.  İstemci, bir geri dönüş dağıtım noktası kullandığında bu içerik, **Içerik indirmek ve yüklemek**üzere ayarlandığı için dağıtım özelliği listedeki bir geri dönüş dağıtım noktasından indirilir. Bu dağıtım ayarı, bu konumdan içerik almak için bir geri dönüş içerik konumu kullanması gereken bir istemciyi sağlar.  

4.  Yönetim noktası, bir dağıtım Yöneticisi 'nin içeriği içerik isteği yapan istemcinin tercih edilen tüm dağıtım noktalarına dağıtması için bir tetikleyici oluşturur.  

5.  Dağıtım Yöneticisi, içeriği bir geri dönüş dağıtım noktası kullanmadan ek istemcilerin içeriği elde etmesini sağlayan tüm tercih edilen dağıtım noktalarına dağıtır.  
