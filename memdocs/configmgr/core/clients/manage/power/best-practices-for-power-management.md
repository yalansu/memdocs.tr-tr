---
title: Güç yönetimi için öneriler
titleSuffix: Configuration Manager
description: Configuration Manager 'de güç yönetimi için Microsoft önerilerini öğrenin.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715266"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Configuration Manager 'de güç yönetimi için öneriler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager 'de güç yönetimi için aşağıdaki önerileri kullanın.  

## <a name="monitor-at-a-representative-time"></a>Temsili bir zamanda izleyin

Güç yönetiminin izleme aşaması, kuruluşunuzdaki bilgisayarlardan aşağıdaki bilgileri sağlar:

- Güç tüketimi
- Etkinlik
- Güç yönetimi özellikleri
- Çevre etkisi

Cihazları izlemek için temsili bir süre seçin. Örneğin, genel bir tatil sırasında izleme, bilgisayar güç kullanımı üzerinde gerçekçi bir rapor sağlamaz.

## <a name="create-a-control-collection"></a>Denetim koleksiyonu oluşturma

Bilgisayarlara güç planları uygulamanın etkilerini izlemenize yardımcı olmak üzere iki bilgisayar koleksiyonu oluşturun. İlk koleksiyon, güç ayarlarını uygulamak istediğiniz bilgisayarların çoğunluğunu içermelidir. *Denetim koleksiyonu* kalan bilgisayarları içermelidir. Gerekli güç yönetimi planını ilk koleksiyona uygulayın. Ardından, iki koleksiyon arasındaki etkiyi karşılaştırmak için raporları çalıştırın.  

## <a name="run-reports-before-you-apply-a-plan"></a>Bir planı uygulamadan önce raporları çalıştırma

Bir bilgisayar koleksiyonuna bir güç yönetimi planı uygulamadan önce, **güç ayarları** raporunu çalıştırın. Koleksiyondaki bilgisayarlarda zaten yapılandırılmış güç yönetimi ayarlarını anlamanıza yardımcı olması için bu raporu kullanın. Bilgisayarlara yeni güç yönetimi ayarlarını mevcut ayarları incelemeden uygularsanız, bu durum güç tüketimini artırabilir.  

## <a name="exclude-servers"></a>Sunucuları hariç tut

Windows Server çalıştıran bilgisayarlar için güç yönetimi desteklenmez. Bir koleksiyona sunucu ekleyin ve güç yönetimi dışında bırakın.  

> [!NOTE]
> Configuration Manager, Windows Server 'ın güç yönetimini desteklemese de, analiz ve raporlama için güç kullanım verilerini toplar.

## <a name="exclude-other-computers"></a>Diğer bilgisayarları Dışla

Güç yönetimi ile yönetmek istemediğiniz bilgisayarlarınız varsa, bu bilgisayarları bir dışlama koleksiyonuna ekleyin.  

Güç yönetiminin aşağıdaki bilgisayar türlerini dışlamak isteyebilirsiniz:

- Açık kalması gereken bilgisayarlar.  

- Kullanıcıların uzaktan bağlanması gereken bilgisayarlar.  

- Güç yönetimini kullanmıyorum bilgisayarlar.  

- Dağıtım noktası site sistemi rolüne sahip bilgisayarlar.  

- Bilgisayar ve izleyicinin her zaman açık olması gereken bilgi noktası bilgisayarları, bilgi ekranları veya izleme konsolları gibi ortak bilgisayarlar.  

Daha fazla bilgi için bkz. [güç yönetimini yapılandırma](configuring-power-management.md).  

## <a name="apply-power-plans-to-a-test-collection"></a>Güç planlarını bir test koleksiyonuna Uygula

Güç planını daha büyük bir bilgisayar koleksiyonuna uygulamadan önce her zaman bir bilgisayar sınama koleksiyonuna güç yönetim planı uygulamanın etkisini sınayın.  

Bir bilgisayarı güç yönetimi dışında çıkardığınız zaman, tüm güç ayarları özgün değerlerine döndürülür. Bireysel güç ayarlarını özgün değerlerine döndüremezsiniz.  

## <a name="apply-power-plan-settings-individually"></a>Güç planı ayarlarını tek tek uygulama

Bir sonraki birini uygulamadan önce her bir güç ayarını uygulamanın etkisini izleyin. Bu işlem her bir ayarın gerekli etkiye sahip olduğundan emin olur. Güç planı ayarları hakkında daha fazla bilgi için bkz. [kullanılabilir güç yönetimi planı ayarları](create-and-apply-power-plans.md#BKMK_Plans).  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Bilgisayarları birden çok güç planı için düzenli olarak izleyin

Güç yönetimi birden çok güç planı uygulanmış bilgisayarları görüntüleyen bir rapor içerir: **birden çok güç planına sahip bilgisayarlar**.

Bir bilgisayar, her biri farklı güç planları uygulayan birden fazla koleksiyonun üyesiyse aşağıdaki davranışlar geçerlidir:  

- **Güç planı**: bir bilgisayara güç ayarları için birden çok değer uygularsanız, en az kısıtlayıcı değeri kullanır.  

- **Uyandırma zamanı**: masaüstü bilgisayara birden çok uyandırma süresi uygularsanız, gece yarısı için en yakın süreyi kullanır.  

Daha fazla bilgi için bkz. [birden çok güç planına sahip bilgisayarlar](monitor-and-plan-for-power-management.md#BKMK_Multiple).  

## <a name="save-or-export-power-management-information"></a>Güç yönetimi bilgilerini kaydetme veya dışarı aktarma

İzleme ve uyumluluk aşamaları sırasında raporları çalıştırdığınızda sonuçları kaydedin veya dışarı aktarın. Daha sonra verileri daha sonra Configuration Manager için verileri daha sonra karşılaştırmaya karşı tutun.  

Configuration Manager, site veritabanında aşağıdaki güç yönetimi bilgilerini tutar:

- Günlük raporlar tarafından kullanılan güç yönetimi bilgileri: 31 gün

- Aylık raporlar tarafından kullanılan güç yönetimi bilgileri: 13 ay
