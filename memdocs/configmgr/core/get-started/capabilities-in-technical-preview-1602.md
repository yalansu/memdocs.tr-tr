---
title: Technical Preview 1602 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1602 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 64d01598f3d5feb162898761645ac84b1c73b175
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074478"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Configuration Manager için Technical Preview 1602 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1602 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).  

 Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a>Mobil cihaz yönetimi geliştirmeleri  

### <a name="ios-activation-lock"></a>iOS Etkinleştirme Kilidi  
 Configuration Manager, iOS 7,1 ve üzeri cihazlar için iPhone 'Umu bul uygulamasının bir özelliği olan iOS Etkinleştirme Kilidi yönetmenize yardımcı olabilir. Bir cihazda iPhone’umu Bul uygulaması kullanıldığında Etkinleştirme Kilidi otomatik olarak etkinleştirilir. Bu özellik etkinleştirildikten sonra şunların yapılabilmesi için Apple kimliği ve parolasının girilmesi gerekir:  

- iPhone’umu Bul özelliğini kapatma  

- Cihazı silme  

- Cihazı yeniden etkinleştirme  

  Configuration Manager, iOS 7,1 ve üstünü çalıştıran hem denetimli hem de denetlenen cihazların Etkinleştirme Kilidi durumunu isteyebilir. Intune, denetlenen cihazlar için Etkinleştirme Kilidi atlama kodunu alabilir ve doğrudan cihaza gönderebilir.  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a>Sürüm 1602 ' de yazılım merkezi geliştirmeleri  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Yazılım Merkezi 'nden bılgısayar makinesi ve kullanıcı ilkesini yenileme  
 Yazılım Merkezi 'nin**bilgisayar bakım** **sayfasına,** > bilgisayar Configuration Manager makine ve kullanıcı ilkesini yenilemeye neden olan yeni bir seçenek, **eşitleme ilkesi** eklenmiştir.  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a>Windows 10 Bakımı geliştirmeleri  
 1602 Technical Preview sürümünde Windows 10 bakımı için aşağıdaki iyileştirmeler ekledik:  

-   Bakım planları için yeni filtre seçenekleri.  Artık **dil**, **gerekli**ve **başlık**için filtre uygulayabilirsiniz. Yalnızca belirtilen ölçütleri karşılayan yükseltmeler ilişkili dağıtıma eklenecektir.  

-   Yazılım güncelleştirmeleri eşitlemesi için **yükseltmeler** sınıflandırması ' nı SEÇTIĞINIZDE, WSUS [Düzeltme 3095113](https://support.microsoft.com/kb/3095113) ' nin, yazılım güncelleştirmelerini başarıyla eşitlemek Için ve Windows 10 hizmetinin düzgün çalışması için gerekli olduğunu bildiren bir uyarı iletişim kutusu görüntülenir.  İletişim kutusunda Düzeltme için Bilgi Bankası makalesine gidebilirsiniz.  

-   Kullanılabilir Windows 10 yükseltmeleri artık yalnızca Configuration Manager konsolunun **Windows 10 Bakımı** \ **tüm Windows 10 güncelleştirmeleri** düğümünde görüntülenir. Bu güncelleştirmeler artık **yazılım güncelleştirmeleri** \ **tüm yazılım güncelleştirmeleri** düğümünde görüntülenmez.  

-   Windows 10 yükseltme paketi Başlatan son kullanıcılara, işletim sistemlerini yükselteceğimizi bildirmek üzere bir iletişim kutusu istenir.  
