---
title: BIOS 'u UEFı 'ye Dönüştür
titleSuffix: Configuration Manager
description: Bir işletim sistemi dağıtımı görev dizisini, UEFı 'ye geçiş için bir FAT32 bölümü hazırlamak üzere nasıl özelleştireceğinizi öğrenin.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 761270fe9419330e2d60d0483554ee6c932c1b26
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124894"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>BIOS’tan UEFI’ye dönüştürmeyi yönetmek için görev sırası adımları

Windows 10, UEFı özellikli cihazlar gerektiren birçok yeni güvenlik özelliği sunar. UEFı 'yi destekleyen, ancak eski BIOS kullanan yeni Windows cihazları olabilir. Daha önce, bir cihazı UEFı 'ye dönüştürmek, her bir cihaza gitmeniz, sabit diski yeniden bölümlemeniz ve bellenimi yeniden yapılandırmanız gerekir.

Configuration Manager ile aşağıdaki eylemleri otomatikleştirebilirsiniz:

- BIOS 'TAN UEFı dönüştürmesi için sabit bir sürücü hazırlayın
- Yerinde yükseltme işleminin bir parçası olarak BIOS 'tan UEFı 'ye dönüştürme
- Donanım envanterinin bir parçası olarak UEFı bilgilerini toplayın

## <a name="hardware-inventory-collects-uefi-information"></a>Donanım envanteri, UEFı bilgilerini toplar

Donanım envanteri sınıfı (**SMS_Firmware**) ve özelliği (**UEFI**), bir bilgisayarın UEFI modunda başlatılıp başlatılmayacağını belirlemenize yardımcı olmak için kullanılabilir. Bir bilgisayar UEFı modunda başlatıldığında, **UEFI** özelliği **true**olarak ayarlanır. Donanım envanteri bu sınıfı varsayılan olarak sunar. Donanım envanteri hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Sabit sürücüyü hazırlamak için özel bir görev dizisi oluşturma

Bir işletim sistemi dağıtımı görev dizisini **Tsuefidrive** değişkeniyle özelleştirebilirsiniz. **Bilgisayarı yeniden Başlat** adımı, UEFI 'ye geçiş için sabit SÜRÜCÜDEKI bir FAT32 bölümünü hazırlar. Aşağıdaki yordam, bu eylemi yapmak için nasıl görev dizisi adımları oluşturabileceğiniz hakkında bir örnek sağlar.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>UEFı 'ye dönüştürme için FAT32 bölümünü hazırlama

Bir işletim sistemini yüklemek için var olan bir görev dizisinde, BIOS 'TAN UEFı dönüştürmesi yapmak için gereken adımları içeren yeni bir grup ekleyin.

1. Dosyaları ve ayarları yakalama adımından sonra ve işletim sistemini yüklemek için gereken adımları izleyerek yeni bir görev dizisi grubu oluşturun. Örneğin, **BIOS-UEFI**adlı **yakalama dosyaları ve ayarlar** grubundan sonra bir grup oluşturun.

1. Yeni grubun **Seçenekler** sekmesinde koşul olarak yeni bir görev dizisi değişkeni ekleyin. **True değerine eşit _SMSTSBootUEFI**ayarlayın. Bu koşulla birlikte, görev sırası yalnızca BIOS cihazlarında bu adımları çalıştırır.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="BIOS 'TAN UEFı grubuna yönelik koşul":::

1. Yeni Grup altında **Bilgisayarı yeniden Başlat** görev sırası adımını ekleyin. **Yeniden başlatmadan sonra ne çalıştırılacağını belirtin**bölümünde, **Bu görev dizisine atanan önyükleme görüntüsünü**seçin. Bu eylem, bilgisayarı Windows PE 'de yeniden başlatır.

1. **Seçenekler** sekmesinde, koşul olarak bir görev sırası değişkeni ekleyin. **_SMSTSInWinPE eşittir false**olarak ayarlayın. Bu koşulla birlikte, bilgisayar zaten Windows PE 'de ise görev dizisi bu adımı çalıştırmaz.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Bilgisayarı yeniden başlatma adımında koşul":::

1. Yazılım yazılımını BIOS 'tan UEFı 'ye dönüştürmek için OEM aracını başlatmak üzere bir adım ekleyin. Bu adım genellikle, OEM aracını çalıştırmak için komutuyla **komut satırını çalıştırır**.

1. **Diski Biçimlendir ve bölümle** görev dizisi adımını ekleyin. Bu adımda, aşağıdaki seçenekleri yapılandırın:

    1. İşletim sistemi yüklenmeden önce UEFı 'ye dönüştürülecek FAT32 bölümünü oluşturun. **Disk türü**için **GPT**'yi seçin.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="Biçim ve Bölüm diski adımının yapılandırması":::

    1. FAT32 bölümünün özelliklerine gidin. **Değişken** alanına, girin `TSUEFIDrive` . Görev dizisi bu değişkeni algıladığında, bilgisayar yeniden başlatılmadan önce, bölümü UEFı geçişi için hazırlar.

        :::image type="content" source="media/partition-properties.png" alt-text="FAT32 bölüm özelliklerinin yapılandırması":::

    1. Görev dizisinin durumunu kaydetmek ve günlük dosyalarını depolamak için kullandığı bir NTFS bölümü oluşturun.

1. Başka bir **Bilgisayarı yeniden Başlat** görev dizisi adımı ekleyin. **Yeniden başlatma işleminden sonra ne çalıştırılacağını belirtin**bölümünde, BILGISAYARı Windows PE 'de başlatmak için **Bu görev dizisine atanan önyükleme görüntüsünü** seçin.

    > [!TIP]
    > Varsayılan olarak, EFı bölüm boyutu 500 MB 'tır. Bazı ortamlarda, önyükleme görüntüsü bu bölümde depolamaya çok büyük. Bu sorunu geçici olarak çözmek için, EFı bölümünün boyutunu artırın. Örneğin, bunu 1 GB olarak ayarlayın.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a>Yerinde yükseltme sırasında BIOS 'tan UEFı 'ye dönüştürme

Windows 10, **MBR2GPT**basit bir dönüştürme aracı içerir. Bu işlem, UEFı etkin donanımlar için sabit diski yeniden bölümlemek için işlemi otomatikleştirir. Dönüştürme aracını yerinde yükseltme işlemiyle Windows 10 ' a tümleştirebilirsiniz. Bu aracı, yükseltme görev diziniz ve bellenimi BIOS 'tan UEFı 'ye dönüştüren OEM aracıyla birleştirin.

### <a name="requirements"></a>Gereksinimler

- Desteklenen bir Windows 10 sürümü
- UEFı 'yi destekleyen bilgisayarlar
- Bilgisayarın bellenimini BIOS 'tan UEFı 'ye dönüştüren OEM aracı

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Yerinde yükseltme görev sırası sırasında BIOS 'tan UEFı 'ye dönüştürme işlemi

1. [İşletim sistemini yükseltmek için görev dizisi oluşturma](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Görev sırasını düzenleyin. **Işlem sonrası** grubunda, aşağıdaki değişiklikleri yapın:

    1. **Komut satırını Çalıştır** adımını ekleyin. MBR2GPT aracı için komut satırını belirtin. Tam işletim sisteminde çalıştırıldığında, verileri değiştirmek veya silmek zorunda kalmadan diski MBR 'den GPT 'ye eklemek için yapılandırın. **Komut satırı**' nda, aşağıdaki komutu girin:`MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > Ayrıca, tüm işletim sistemi yerine Windows PE 'de MBR2GPT.EXE aracını çalıştırmayı da seçebilirsiniz. MBR2GPT.EXE aracını çalıştırma adımından önce bilgisayarı Windows PE 'ye yeniden başlatmak için bir adım ekleyin. Ardından komut satırından **/Allowfullos** seçeneğini kaldırın.

    Araç ve kullanılabilir seçenekler hakkında daha fazla bilgi için bkz. [MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt).

    1. Yazılım yazılımını BIOS 'tan UEFı 'ye dönüştüren OEM aracını çalıştırmak için bir adım ekleyin. Bu adım genellikle, OEM aracını çalıştırmak için komut satırı ile birlikte komut satırını **çalıştırır**.

    1. **Bilgisayarı yeniden Başlat** adımını ekleyin ve **Şu anda yüklü varsayılan işletim sistemini**seçin.

1. Görev sırasını dağıtın.
