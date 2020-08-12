---
title: VDI istemcilerini yönetme
titleSuffix: Configuration Manager
description: Bir sanal masaüstü altyapısında (VDı) Configuration Manager istemcilerini yönetin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6df9238cd81f14a64a42c45136c778357acb89c4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126959"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Bir sanal masaüstü altyapısında (VDı) Configuration Manager istemcilerini yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, aşağıdaki sanal masaüstü altyapısı (VDı) senaryolarında Configuration Manager istemcisinin yüklenmesini destekler:

- **Kişisel sanal makineler**: sanal makıne (VM), oturumlar arasında kullanıcı verilerini ve ayarları korur.

- **Uzak Masaüstü Hizmetleri oturumlar**: merkezi sunucuda birden çok eş zamanlı istemci oturumu barındırın. Kullanıcılar bir oturuma bağlanır ve bu sunucuda uygulamaları çalıştırır.

- **Havuza alınmış sanal makineler**: VM, oturumlar arasında kalıcı olmaz. Bir Kullanıcı bir oturumu kapattığında, sanal ortam tüm verileri ve ayarları atar. Havuza alınmış sanal makineler Uzak Masaüstü Hizmetleri kullanamıyoruz yararlı olur. Örneğin, gerekli bir uygulama, istemci oturumlarını barındıran Windows Server üzerinde çalıştırılamaz.

- **Windows sanal masaüstü**: Microsoft Azure üzerinde çalışan bir masaüstü ve uygulama sanallaştırma hizmeti. Sürüm 1906 ' den başlayarak, Azure 'da Windows çalıştıran bu sanal cihazları yönetmek için Configuration Manager kullanın.

## <a name="personal-vms"></a>Kişisel VM 'Ler

Configuration Manager, kişisel sanal makinelere fiziksel bir bilgisayarla aynı şekilde davranır. Configuration Manager istemcisini VM görüntüsüne veya onu hazırladıktan sonra önyükleyebilirsiniz.

Daha fazla bilgi için bkz. [sanallaştırma ortamları desteği](../../../plan-design/configs/support-for-virtualization-environments.md).

## <a name="remote-desktop-services"></a>Uzak Masaüstü Hizmetleri

Tek tek uzak masaüstü oturumları için Configuration Manager istemcisini yüklemeyin. Uzak Masaüstü Hizmetleri barındıran sunucuya bir kez yükler. Uzak Masaüstü Hizmetleri sunucusunda tüm Configuration Manager istemci özelliklerini kullanabilirsiniz.

Daha fazla bilgi için bkz. [Uzak Masaüstü Hizmetleri hoş geldiniz](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/welcome-to-rds).

## <a name="pooled-vms"></a>Havuza alınmış VM 'Ler

Havuza alınmış bir sanal makinenin yetkisini aldığınızda, Configuration Manager tarafından yapılan değişiklikler kaybedilir.

VM yalnızca kısa bir süre boyunca çalışır durumda olabileceğinden, bazı Configuration Manager Özellikler ilgili verileri döndürmeyebilir. Örneğin, donanım envanteri, yazılım envanteri ve yazılım kullanım ölçümü. Havuza alınmış VM 'yi envanter görevlerinden dışlayarak göz önünde bulundurun.

## <a name="windows-virtual-desktop"></a>Windows Sanal Masaüstü

Daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemleri](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="other-considerations"></a>Diğer önemli noktalar

Sanallaştırma, aynı fiziksel bilgisayarda birden çok Configuration Manager istemcisini çalıştırmayı desteklediğinden, çok sayıda istemci işlemi zamanlanmış eylemler için yerleşik rastgele gecikmeye sahiptir. Örneğin, donanım ve yazılım envanteri, kötü amaçlı yazılımdan taramalar, yazılım yüklemeleri ve yazılım güncelleştirme taramaları. Bu gecikme, Configuration Manager istemcisini çalıştıran birden çok VM 'ye sahip bir sunucu için CPU işleme ve veri aktarımını dağıtmaya yardımcı olur.

Hizmet verme modundaki Windows Embedded istemcileri hariç, sanallaştırılmış ortamlarda bulunmayan Configuration Manager istemcileri de bu rastgele gecikmeyi kullanır. Bu davranış, ağ bant genişliğinden en üst seviyeye kaçınmaya yardımcı olur. Ayrıca, yönetim noktası ve site sunucusu gibi site sistemlerindeki CPU işlemlerini azaltır. Gecikme aralığı Configuration Manager özelliğine göre farklılık gösterir. Örneğin, bkz. [istemci ayarları hakkında-son tarih rastgele seçimini devre dışı bırak](../about-client-settings.md#disable-deadline-randomization).

Birden çok kullanıcı oturumunu destekleyen sanal ortamlarda istemci performansına Configuration Manager yardımcı olması için, varsayılan olarak kullanıcı ilkesini devre dışı bırakır. Sürüm 1910 ' den başlayarak, bu senaryoda kullanıcı ilkesini etkinleştirebilirsiniz. Daha fazla bilgi için bkz. [istemci ayarları hakkında-birden çok Kullanıcı oturumu için Kullanıcı Ilkesini etkinleştirme](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions).
