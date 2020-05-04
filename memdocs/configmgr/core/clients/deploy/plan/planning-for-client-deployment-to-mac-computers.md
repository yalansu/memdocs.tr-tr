---
title: Mac bilgisayarlara istemci dağıtımını planlama
titleSuffix: Configuration Manager
description: Configuration Manager 'da Mac bilgisayarlara istemci dağıtımını planlayın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713229"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Configuration Manager 'da Mac bilgisayarlara istemci dağıtımını planlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcisini, Mac OS X işletim sistemini çalıştıran Mac bilgisayarlara yükleyebilir ve aşağıdaki yönetim özelliklerini kullanabilirsiniz:  

- **Donanım envanteri**  

   Mac bilgisayarlarda donanım ve yüklü uygulamalar hakkında bilgi toplamak için Configuration Manager donanım envanterini kullanabilirsiniz. Bu bilgiler daha sonra Configuration Manager konsolundaki Kaynak Gezgini görüntülenebilir ve koleksiyonlar, sorgular ve raporlar oluşturmak için kullanılır. Daha fazla bilgi için bkz. [donanım envanterini görüntülemek için kaynak Gezgini kullanma](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager, Mac bilgisayarlardan aşağıdaki donanım bilgilerini toplar:  

  -   İşlemci  

  -   Bilgisayar Sistemi  

  -   Disk sürücüsü  

  -   Disk bölümü  

  -   Ağ bağdaştırıcısı  

  -   İşletim Sistemi  

  -   Hizmet  

  -   İşleme  

  -   Yüklü yazılım  

  -   Bilgisayar Sistemi Ürünü  

  -   USB denetleyicisi  

  -   USB cihazı  

  -   CDROM sürücüsü  

  -   Video denetleyicisi  

  -   Masaüstü Izleyicisi  

  -   Taşınabilir pil  

  -   Fiziksel Bellek  

  -   Yazıcı  

  > [!IMPORTANT]  
  >  Donanım envanteri sırasında Mac bilgisayarlardan toplanan donanım bilgilerini genişletemezsiniz.  

- **Uyumluluk ayarları**  

   Configuration Manager uyumluluk ayarlarını kullanarak Mac OS X tercih (. plist) ayarlarının uyumluluğunu görüntüleyebilir ve düzeltebilirsiniz. Örneğin, Safari Web tarayıcısında giriş sayfası için ayarları uygulayabilir veya Apple güvenlik duvarının etkinleştirildiğinden emin olabilirsiniz. Ayrıca, MAC OS X 'teki ayarları izlemek ve düzeltmek için kabuk komut dosyalarını da kullanabilirsiniz.  

- **Uygulama yönetimi**  

   Configuration Manager, Mac bilgisayarlara yazılım dağıtabilir. Mac bilgisayarlara aşağıdaki yazılım biçimlerini dağıtabilirsiniz:  

  -   Apple disk görüntüsü (. DMG  

  -   Meta paket dosyası (. MPKG  

  -   Mac OS X Installer paketi (. PAKET  

  -   Mac OS X uygulaması (. UYGULAMANıZDA  

  Mac bilgisayarlara Configuration Manager istemcisini yüklediğinizde, Windows tabanlı bilgisayarlarda Configuration Manager istemcisi tarafından desteklenen aşağıdaki yönetim özelliklerini kullanamazsınız:  

- Client push yüklemesi  

- İşletim sistemi dağıtımı  

- Yazılım güncelleştirmeleri  

  > [!NOTE]  
  >  Mac bilgisayarlara gerekli Mac OS X yazılım güncelleştirmelerini dağıtmak için Configuration Manager uygulama yönetimini kullanabilirsiniz. Ayrıca, bilgisayarların gerekli yazılım güncelleştirmelerine sahip olduğundan emin olmak için uyumluluk ayarlarını kullanabilirsiniz.  

- Bakım pencereleri  

- Uzaktan denetim  

- Güç yönetimi  

- İstemci durumu istemci denetimi ve düzeltmesi  

  Configuration Manager Mac istemcisinin nasıl yükleneceği ve yapılandırılacağı hakkında daha fazla bilgi için bkz. Mac ['e istemci dağıtma](../../../../core/clients/deploy/deploy-clients-to-macs.md).
