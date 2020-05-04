---
title: Bakım pencerelerini kullanma
titleSuffix: Configuration Manager
description: Configuration Manager ' deki istemcileri etkin bir şekilde yönetmek için Koleksiyonlar ve bakım pencerelerini kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714447"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Configuration Manager 'de bakım pencerelerini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bakım pencereleri Configuration Manager işlemlerin bir cihaz koleksiyonunda gerçekleştirilebilme süresini tanımlamanızı sağlar. Bakım pencerelerini, üretkenliği etkilemeyen dönemler sırasında istemci yapılandırma değişikliklerinin gerçekleşmesini sağlamaya yardımcı olmak için kullanırsınız. Configuration Manager sürüm 1806 ' den başlayarak, kullanıcılarınız bir sonraki bakım penceresinin **yazılım merkezindeki** **yükleme durumu** sekmesinden ne zaman olduğunu görebilirler. <!--1358131-->

 Aşağıdaki işlemler bakım pencerelerini destekler:  

- Yazılım dağıtımları  

- Yazılım güncelleştirme dağıtımları  

- Uyumluluk ayarları dağıtımı ve değerlendirmesi  

- İşletim sistemi dağıtımları  

- Görev sırası dağıtımları  

  Bakım pencerelerini başlangıç tarihi, başlangıç ve bitiş saati ve yinelenme düzeniyle yapılandırın. Bir pencerenin en uzun süresi 24 saatten az olmalıdır. Varsayılan olarak, dağıtıma neden olan bilgisayar yeniden başlatmalarının bakım penceresi dışında yapılmasına izin verilmez, ancak varsayılanı geçersiz kılabilirsiniz. Bakım pencereleri yalnızca dağıtım programının çalıştığı saati etkiler; Yerel olarak indirilmek ve çalıştırılmak üzere yapılandırılan uygulamalar, içeriği pencerenin dışında indirebilir.  

  Bir istemci bilgisayar, bakım penceresi olan bir cihaz koleksiyonunun üyesiyse, dağıtım programı yalnızca izin verilen en fazla çalışma süresi pencere için yapılandırılan süreyi aşmazsa çalışır. Program çalıştırılamazsa bir uyarı oluşturulur ve dağıtım, zamanlanmış olan ve yeterli süreyi içeren sonraki bakım penceresi sırasında yeniden çalıştırılır.  

## <a name="using-multiple-maintenance-windows"></a>Birden fazla bakım penceresi kullanma  
 Bir istemci bilgisayar, bakım pencereleri olan birden çok cihaz koleksiyonunun üyesiyse, bu kurallar geçerlidir:  

- Bakım pencereleri çakışmazsa, iki bağımsız bakım penceresi olarak kabul edilir.  

- Bakım pencereleri çakışırsa, her iki bakım penceresinin kapsadığı zaman dilimini çevreleyen tek bir bakım penceresi olarak kabul edilir. Örneğin, iki Windows, süre içindeki her saat 30 dakikadan çakışırsa, bakım penceresinin geçerlilik süresi 90 dakika olur.  

  Bir Kullanıcı, yazılım merkezi 'nden bir uygulama yüklemesi başlattığında uygulama, bakım pencerelerinden bağımsız olarak hemen yüklenir.  

  **Zorunlu** amacına sahip bir uygulama dağıtımı, Yazılım Merkezi’nde bir kullanıcı tarafından yapılandırılan iş dışı saatlerde yükleme süre sonuna ulaşırsa, uygulama yüklenir. 

### <a name="how-to-configure-maintenance-windows"></a>Bakım pencerelerini yapılandırma  

1.  Configuration Manager konsolunda, **varlıklar ve uyum**>  **Cihaz Koleksiyonları**' nı seçin.  

3.  **Cihaz Koleksiyonları** listesinde bir koleksiyon seçin. **Tüm sistemler** koleksiyonu için bakım pencereleri oluşturamazsınız.  

4.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

5.  **Koleksiyon adı\> Özellikler iletişim kutusunun bakım pencereleri sekmesinde, yeni simgesini &lt;** seçin. **Maintenance Windows** **New**  

6.  Yeni zamanlama iletişim kutusunu doldurun. ** &lt;\> **  

7.  **Bu zamanlamayı Uygula** açılır listesinden bir seçim yapın.  

8.  **Tamam** ' ı seçin ve ardından ** &lt;koleksiyon adı\> Özellikler** iletişim kutusunu kapatın.  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>PowerShell 'i kullanma

PowerShell, bakım pencerelerini yapılandırmak için kullanılabilir.  Daha fazla bilgi için bkz.

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
