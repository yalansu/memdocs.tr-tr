---
title: Windows PE’de BitLocker'ı önceden sağlama
titleSuffix: Configuration Manager
description: Configuration Manager 'de BitLocker 'ı önceden sağla görevi, işletim sistemi dağıtımından önce Windows Önyükleme Ortamı BitLocker 'ı mümkün bir şekilde sunar.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124952"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>Configuration Manager ile Windows PE 'de BitLocker 'ı önceden sağlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' deki **BitLocker 'ın ön sağlamasını** yap görev sırası adımı, işletim sistemi dağıtımından önce Windows önyükleme ortamı (Windows PE) Içinden BitLocker 'ı etkinleştirmenizi sağlar. Yalnızca kullanılan sürücü alanı şifrelendiği için ve şifreleme çok daha kısa sürer. Bu, biçimlendirilmiş birime rasgele oluşturulan bir açık koruyucu uygulanarak ve Windows kurulum süreci çalıştırılmadan önce birim şifrelenerek gerçekleştirilir. BitLocker’ın ön sağlamasını yapma özelliği Windows 8 ve Windows Server 2012 sürümleriyle sunulmuştur. Ancak, belirtilen bu adımları izlediğiniz sürece bir sabit sürücüde BitLocker’ın ön sağlamasını yapabilir ve Windows 7’yi yükleyebilirsiniz. Windows 7 Kurulumu tamamlandıktan sonra, Windows 7 BitLocker kontrol paneli açık koruyucu içeren BitLocker'ı desteklemediği için, bir BitLocker anahtar koruyucusu ayarlamanız gerekir. **BitLocker'ı Etkinleştir** adımını kullanarak veya manage-bde.exe komut satırı aracını kullanarak bir anahtar koruyucusu eklemeniz gerekir.  

 Genellikle, Windows 7 yükleyecek bir bilgisayarda başarıyla BitLocker'ın ön sağlamasını yapmak için aşağıdakileri yapmanız gerekir:  

- Bilgisayarı Windows PE'de yeniden başlatma  

  > [!IMPORTANT]  
  >  BitLocker'ın ön sağlamasını yapmak için Windows PE 4 veya daha yenisini içeren bir önyükleme görüntüsü kullanmanız gerekir. Configuration Manager ' deki desteklenen Windows PE sürümleri hakkında daha fazla bilgi için bkz. [dış bağımlılıklar Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- Sabit sürücüyü bölümleme ve biçimlendirme  

- 'deki  

- Belirli işletim sistemi ve ağ ayarlarıyla Windows 7 yükleme  

- BitLocker'a anahtar koruyucusu ekleme  

  Configuration Manager, bir sabit sürücüde BitLocker 'ın ön sağlamasını yapmak ve Windows 7 yüklemek için önerilen yöntem, yeni bir görev sırası oluşturmak ve **görev sırası oluşturma Sihirbazı**' nın **Yeni görev sırası oluştur** sayfasından **var olan bir görüntü paketini yüklemek** ' ı seçmeniz gerekir. Sihirbaz aşağıdaki tabloda listelenen görev sırası adımlarını oluşturur.  

> [!NOTE]  
>  Sihirbazdaki ayarları nasıl yapılandırdığınıza bağlı olarak, görev sırası ek adımlar içerebilir. Örneğin, sihirbazın **Durum Geçişi** sayfasında **Yakalanan Microsoft Windows ayarları** 'nı seçtiyseniz, **Windows Ayarlarını Yakala** adımı da olabilir.  

|Görev sırası adımı|Ayrıntılar|  
|------------------------|-------------|  
|BitLocker'ı Devre Dışı Bırak|Bu adım BitLocker şifrelemesi etkinse devre dışı bırakır. Daha fazla bilgi için, bkz. [Disable BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Bilgisayarı Windows PE'de Yeniden Başlatma|Bu adım görev sırasına atanan önyükleme görüntüsünü çalıştırarak bilgisayarı Windows PE'de yeniden başlatır. BitLocker'ın ön sağlamasını yapmak için Windows PE 4 veya daha yenisini içeren bir önyükleme görüntüsü kullanmanız gerekir. Daha fazla bilgi için, bkz. [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Diski Bölümle 0 - BIOS<br /><br /> Diski Bölümle 0 - UEFI|Bu adımlar hedef bilgisayardaki belirtilen sürücüyü BIOS veya UEFI'yi kullanarak biçimlendirir ve bölümler. Görev sırası hedef bilgisayarın UEFI modunda olduğunu algıladığında UEFI'yi kullanır. Daha fazla bilgi için, bkz. [Format and Partition Disk](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|'deki|Bu adım Windows PE'deyken bir sürücüde BitLocker'ı etkinleştirir. Yalnızca kullanılan sürücü alanı şifrelenir. Önceki adımda sürücüyü bölümleyip biçimlendirdiğiniz için, hiç veri yoktur ve şifreleme çok çabuk tamamlanır. Daha fazla bilgi için, bkz. [Pre-provision BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|İşletim Sistemini Uygula|Bu adım, hedef bilgisayarda işletim sistemini yüklemek için kullanılan yanıt dosyasını hazırlar ve OSDTargetSystemDrive görev sırası değişkenini işletim sistemi dosyalarının bulunduğu disk bölümünün sürücü harfine ayarlar. Yanıt dosyası ve değişken, Windows'u ve ConfigMgr'yi Kur adımı tarafından işletim sistemini yüklemek için kullanılır. Daha fazla bilgi için, bkz. [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Windows Ayarlarını Uygula|Bu adım Windows ayarlarını yanıt dosyasına ekler. Yanıt dosyası, Windows'u ve ConfigMgr'yi Kur adımı tarafından işletim sistemini yüklemek için kullanılır. Daha fazla bilgi için, bkz. [Apply Windows Settings](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Ağ Ayarlarını Uygula|Bu adım Ağ ayarlarını yanıt dosyasına ekler. Yanıt dosyası, Windows'u ve ConfigMgr'yi Kur adımı tarafından işletim sistemini yüklemek için kullanılır. Daha fazla bilgi için, bkz. [Apply Network Settings Step](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Aygıt Sürücülerini Uygula|Bu adım işletim sistemi dağıtımının parçası olarak sürücüleri eşler ve yükler. Daha fazla bilgi için, bkz. [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Windows'u ve ConfigMgr'yi Kur|Bu adım Windows PE'den yeni işletim sistemine geçişi gerçekleştirir. Bu görev sırası adımı herhangi bir işletim sistemi dağıtımının gerekli bir parçasıdır. Configuration Manager istemcisini yeni işletim sistemine yükleyerek görev dizisinin yeni işletim sisteminde yürütmeye devam etmesine hazırlar. Daha fazla bilgi için, bkz. [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|BitLocker'ı Etkinleştir|Bu adım sabit sürücüde BitLocker şifrelemesini etkinleştirir ve anahtar koruyucularını ayarlar. Sabit sürücünün BitLocker ile önceden sağlaması yapılmış olduğu için, bu adım çok çabuk tamamlanır. Windows 7 bir anahtar koruyucusu eklemenizi gerektirir. Bu adımı kullanmazsanız, anahtar koruyucusu ayarlamak için manage-bde.exe komut satırı aracını çalıştırabilirsiniz. Daha fazla bilgi için, bkz. [Enable BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
