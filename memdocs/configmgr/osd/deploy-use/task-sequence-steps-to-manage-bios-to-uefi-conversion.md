---
title: BIOS’tan UEFI’ye dönüştürmeyi yönetmek için görev sırası adımları
titleSuffix: Configuration Manager
description: Bir işletim sistemi dağıtımı görev dizisini, UEFı 'ye geçiş için bir FAT32 bölümü hazırlamak üzere nasıl özelleştireceğinizi öğrenin.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079374"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>BIOS’tan UEFI’ye dönüştürmeyi yönetmek için görev sırası adımları
Windows 10, UEFı özellikli cihazlar gerektiren birçok yeni güvenlik özelliği sunar. UEFı 'yi destekleyen, ancak eski BIOS kullanan modern Windows bilgisayarlarınıza sahip olabilirsiniz. Bir cihazı UEFı 'ye dönüştürmek, her bir BILGISAYARA gitmeniz, sabit diski yeniden bölümlemeniz ve bellenimi yeniden yapılandırmanız gerekiyordu. Configuration Manager görev dizilerini kullanarak, BIOS 'tan UEFı dönüştürmesi için bir sabit sürücü hazırlayabilir, yerinde yükseltme işleminin bir parçası olarak BIOS 'tan UEFı 'ye dönüştürebilir ve donanım envanterinin bir parçası olarak UEFı bilgilerini toplayabilirsiniz.

## <a name="hardware-inventory-collects-uefi-information"></a>Donanım envanteri, UEFı bilgilerini toplar
Sürüm 1702 ' den başlayarak, bir bilgisayarın UEFı modunda başlatılıp başlatılmayacağını belirlemenize yardımcı olmak üzere yeni bir donanım envanteri sınıfı (**SMS_Firmware**) ve özelliği (**UEFI**) kullanılabilir. Bir bilgisayar UEFı modunda başlatıldığında, **UEFI** özelliği **true**olarak ayarlanır. Bu, varsayılan olarak donanım envanterinde etkinleştirilmiştir. Donanım envanteri hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>BIOS için sabit sürücüyü UEFı dönüştürmeye hazırlamak üzere özel bir görev dizisi oluşturma
Configuration Manager sürüm 1610 ' den başlayarak, şimdi **Bilgisayarı yeniden Başlat** ADıMıNıN, UEFI 'ye geçiş için sabit SÜRÜCÜDEKI bir FAT32 bölümünü hazırlayabilmesi Için TSUEFIDrive adlı bir işletim sistemi dağıtımı görev dizisini özelleştirebilirsiniz. Aşağıdaki yordam, BIOS 'TAN UEFı 'ye dönüştürme için sabit sürücüyü hazırlamak üzere görev dizisi adımlarını nasıl oluşturabileceğiniz hakkında bir örnek sağlar.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>UEFı 'ye dönüştürme için FAT32 bölümünü hazırlamak için:
Bir işletim sistemini yüklemek için var olan bir görev dizisinde, BIOS 'TAN UEFı dönüştürmesi yapmak için gereken adımları içeren yeni bir grup ekleyeceksiniz.

1. Dosya ve ayarları yakalama adımlarında ve işletim sistemini yüklemek için olan adımlardan önce yeni bir görev dizisi grubu oluşturun. Örneğin, **BIOS-UEFI**adlı **yakalama dosyaları ve ayarlar** grubundan sonra bir grup oluşturun.
2. Yeni grubun **Seçenekler** sekmesinde, **_SMSTSBootUEFI** **true** **değerine eşit olmayan** bir koşul olarak yeni bir görev dizisi değişkeni ekleyin. Bu, bir bilgisayar zaten UEFı modunda olduğunda gruptaki adımların çalıştırılmasını önler.

   ![BIOS 'TAN UEFı grubuna](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Yeni Grup altında **Bilgisayarı yeniden Başlat** görev sırası adımını ekleyin. **Yeniden başlatma işleminden sonra ne çalıştırılacağını belirtin**bölümünde, BILGISAYARı Windows PE 'de başlatmak için **Bu görev dizisine atanan önyükleme görüntüsünü** seçin.  
4. **Seçenekler** sekmesinde, **_SMSTSInWinPE eşitse**bir koşul olarak bir görev dizisi değişkeni ekleyin. Bu, bilgisayar zaten Windows PE 'de ise bu adımın çalışmasını önler.

   ![Bilgisayarı yeniden Başlat adımı](../../core/get-started/media/restart-in-windows-pe.png)
5. Yazılım yazılımını BIOS 'tan UEFı 'ye dönüştürecek OEM aracını başlatmak için bir adım ekleyin. Bu, tipik olarak bir komut satırı Çalıştır görev dizisi adımını bir komut satırı ile **ÇALıŞTıRARAK** OEM aracını başlatır.
6. Sabit sürücüyü bölümlemek ve biçimlendirmek için disk Biçimlendir ve bölümle disk görev dizisi adımını ekleyin. Adımda şunları yapın:
   1. İşletim sistemi yüklenmeden önce UEFı 'ye dönüştürülecek FAT32 bölümünü oluşturun. **Disk türü**için **GPT** 'yi seçin.
    ![Diski Biçimlendir ve bölümle adımı](../media/format-and-partition-disk.png)
   2. FAT32 bölümünün özelliklerine gidin. **Değişken** alanına **Tsuefidrive** girin. Görev dizisi bu değişkeni algıladığında, bilgisayar yeniden başlatılmadan önce UEFı geçişi için hazırlanacaktır.
    ![Bölüm Özellikleri](../../core/get-started/media/partition-properties.png)
   3. Görev dizisi altyapısının durumunu kaydetmek ve günlük dosyalarını depolamak için kullandığı bir NTFS bölümü oluşturun.
7. **Bilgisayarı yeniden Başlat** görev dizisi adımını ekleyin. **Yeniden başlatma işleminden sonra ne çalıştırılacağını belirtin**bölümünde, BILGISAYARı Windows PE 'de başlatmak için **Bu görev dizisine atanan önyükleme görüntüsünü** seçin.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Yerinde yükseltme sırasında BIOS 'tan UEFı 'ye dönüştürme
Windows 10 Creators Update, işlemi UEFı etkin donanımlar için sabit diski yeniden bölümlemek ve dönüştürme aracını Windows 10 yerinde yükseltme işlemine tümleştiren bir basit dönüştürme aracı sunuyor. Bu aracı işletim sistemi yükseltme görev diziniz ve bellenimi BIOS 'tan UEFı 'ye dönüştüren OEM aracı ile birleştirdiğinizde, Windows 10 Creators Update 'e yerinde yükseltme sırasında bilgisayarlarınızı BIOS 'tan UEFı 'e dönüştürebilirsiniz.

**Gereksinimler**:
- Windows 10 Creators Update
- UEFı 'yi destekleyen bilgisayarlar
- Bilgisayarın bellenimini BIOS 'tan UEFı 'ye dönüştüren OEM aracı

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Yerinde yükseltme sırasında BIOS 'tan UEFı 'ye dönüştürme
1. Windows 10 Creators Update 'e yerinde yükseltme gerçekleştiren bir işletim sistemi yükseltme görev dizisi oluşturun.
2. Görev sırasını düzenleyin. **Işlem sonrası grubunda**, aşağıdaki görev sırası adımlarını ekleyin:
   1. Genel olarak, **komut satırı Çalıştır** adımı ekleyin. Diskteki verileri değiştirmeden veya silmeden, bir diski MBR 'den GPT 'ye bağlayan MBR2GPT aracının komut satırını ekleyeceksiniz. Komut satırı ' nda şunları yazın: **MBR2GPT/Convert/disk: 0/AllowFullOS**. MBR2GPT çalıştırmayı da tercih edebilirsiniz. Tam işletim sistemi yerine Windows PE 'de olduğunda EXE aracı. Bunu, MBR2GPT çalıştırma adımından önce bilgisayarı WinPE 'ye yeniden başlatmak için bir adım ekleyerek yapabilirsiniz. EXE aracını ve/AllowFullOS seçeneğini komut satırından kaldırma. Araç ve kullanılabilir seçenekler hakkında daha fazla bilgi için bkz [. MBR2GPT. EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Yazılım yazılımını BIOS 'tan UEFı 'ye dönüştürecek OEM aracını başlatmak için bir adım ekleyin. Bu, tipik olarak bir komut satırı Çalıştır görev dizisi adımını bir komut satırı ile çalıştırarak OEM aracını başlatır.
   3. Genel olarak, **Bilgisayarı yeniden Başlat** adımını ekleyin. Yeniden başlatma sonrasında neyin çalıştırılacağını belirtmek için, **Şu anda yüklü varsayılan işletim sistemini**seçin.
3. Görev sırasını dağıtın.
