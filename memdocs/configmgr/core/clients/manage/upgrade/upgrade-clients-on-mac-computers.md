---
title: MacOS istemcilerini yükseltme
titleSuffix: Configuration Manager
description: Mac bilgisayarlarda Configuration Manager istemcisini yükseltin.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715007"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Configuration Manager Mac bilgisayarlarda istemcileri yükseltme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Mac bilgisayarlara yönelik istemciyi Configuration Manager bir uygulama kullanarak yükseltmek için bu makaledeki üst düzey adımları izleyin. Mac istemci yükleme dosyasını da indirebilir, paylaşılan bir ağ konumuna veya Mac bilgisayardaki yerel bir klasöre kopyalayabilir ve ardından kullanıcıların yüklemeyi el ile çalıştırmasını sağlayabilirsiniz.  

> [!NOTE]  
> Bu adımları uygulamadan önce Mac bilgisayarınızın önkoşulları karşıladığından emin olun. Bkz. [Mac bilgisayarlar Için desteklenen işletim sistemleri](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>En son Mac istemcisini indirin

Configuration Manager Mac istemcisi Configuration Manager yükleme medyasında sağlanmaz. Microsoft Download Center 'dan indirin, [Microsoft uç nokta Configuration Manager-macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850). Mac istemcisi yükleme dosyaları **ConfigmgrMacClient. msi**adlı bir Windows Installer dosyasında bulunur.  

## <a name="create-the-mac-client-installation-file"></a>Mac istemcisi yükleme dosyasını oluşturma

Windows çalıştıran bir bilgisayarda **ConfigmgrMacClient. msi**' yi çalıştırın. Bu yükleyici, **macclient. dmg**adlı Mac istemci yükleme dosyasının paketlerini kaldırır. Varsayılan olarak, bu dosyayı şu klasörde bulabilirsiniz: **C:\Program Files\Microsoft\System Center for Mac client Configuration Manager**.  

## <a name="extract-the-client-installation-files"></a>İstemci yükleme dosyalarını Ayıkla

**Macclient. dmg** 'Yi bir Mac bilgisayara kopyalayın. MacOS 'a macclient. dmg dosyasını bağlayın ve sonra içeriği Mac bilgisayardaki bir klasöre kopyalayın.  

## <a name="create-a-cmmac-file"></a>. Cmmac dosyası oluşturma

1. Mac istemci yükleme dosyalarının **Araçlar** klasörünü açın. İstemci yükleme paketinden bir. cmmac dosyası oluşturmak için **CMAppUtil** aracını kullanın. Bu dosyayı Configuration Manager uygulamasını oluşturmak için kullanacaksınız.  

2. Yeni **CMClient. pkg. cmmac** dosyasını, Configuration Manager konsolunu çalıştıran bilgisayar için kullanılabilir bir ağ konumuna kopyalayın.  

    Daha fazla bilgi için bkz. [Mac bilgisayarlara yönelik uygulamalar oluşturmak ve dağıtmak Için ek yordamlar](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="create-and-deploy-the-app"></a>Uygulama oluşturma ve dağıtma

1. Configuration Manager konsolunda, **CMClient. pkg. cmmac** dosyasından [bir uygulama oluşturun](../../../../apps/get-started/creating-mac-computer-applications.md) .  

2. [Bu uygulamayı](../../../../apps/deploy-use/deploy-applications.md) hiyerarşinizdeki Mac bilgisayarlara dağıtın.  

## <a name="install-the-updated-client"></a>Güncelleştirilmiş istemciyi yükler

Mac bilgisayarlarda var olan Configuration Manager istemcisi, kullanıcıdan bir güncelleştirmenin yükleneceğine ilişkin bir güncelleştirme olduğunu sorar. Kullanıcılar istemciyi yükledikten sonra Mac bilgisayarını yeniden başlatmaları gerekir.  

Bilgisayar yeniden başlatıldıktan sonra, yeni bir kullanıcı sertifikası istemek için **bilgisayar kayıt** Sihirbazı otomatik olarak çalıştırılır.

Configuration Manager kaydı kullanmıyorsanız ancak istemci sertifikasını Configuration Manager bağımsız olarak yüklerseniz, bkz. [istemcileri var olan bir sertifikayı kullanacak şekilde yapılandırma](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a>İstemcileri mevcut bir sertifikayı kullanacak şekilde yapılandırma

Bilgisayar kayıt Sihirbazı 'Nın çalışmasını engellemek ve yükseltilen istemciyi var olan bir istemci sertifikasını kullanmak üzere yapılandırmak için bu yordamı kullanın.  

1. Configuration Manager konsolunda, **Mac OS X**türünde [bir yapılandırma öğesi oluşturun](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) .  

1. Bu yapılandırma öğesine **Komut Dosyası**ayar türüyle bir ayar ekleyin.  

1. Aşağıdaki komut dosyasını ayara ekleyin:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Yapılandırma öğesini bir [yapılandırma temeline](../../../../compliance/deploy-use/create-configuration-baselines.md)ekleyin. Sonra [Yapılandırma temelini](../../../../compliance/deploy-use/deploy-configuration-baselines.md) Configuration Manager ' den bağımsız olarak bir sertifika yükleyen tüm Mac bilgisayarlarına dağıtın.  
