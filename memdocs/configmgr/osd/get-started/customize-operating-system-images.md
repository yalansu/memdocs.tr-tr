---
title: 'İşletim sistemi görüntülerini özelleştirme '
titleSuffix: Configuration Manager
description: Bir işletim sistemi görüntüsünü özelleştirmek için yakalama ve oluşturma görev dizilerini, el ile yapılandırmayı veya her ikisinin birleşimini kullanın.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 652a0c5e36ce7c4bacf40531a82fdf4e16197d95
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906910"
---
# <a name="customize-operating-system-images-with-configuration-manager"></a>Configuration Manager ile işletim sistemi görüntülerini özelleştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager işletim sistemi görüntüleri, WıM dosyalarıdır ve bir bilgisayarda bir işletim sistemini başarılı bir şekilde yüklemek ve yapılandırmak için gerekli referans dosya ve klasörlerinin sıkıştırılmış bir koleksiyonunu temsil eder. Özel bir işletim sistemi görüntüsü gerekli tüm işletim sistemi dosyaları, destek dosyaları, yazılım güncelleştirmeleri, araçlar ve diğer yazılım uygulamalarıyla yapılandırdığınız bir referans bilgisayardan oluşturulur ve yakalanır. Referans bilgisayarını elle nereye kadar yapılandıracağınız size kalmıştır. Oluşturma ve yakalama görev dizisini kullanarak referans bilgisayarın yapılandırmasını tamamen otomatikleştirebilir, referans bilgisayarın belirli özelliklerini elle yapılandırdıktan sonra görev dizilerini kullanarak kalan kısmı otomatikleştirebilir veya görev dizilerini kullanmadan referans bilgisayarı elle yapılandırabilirsiniz. Bir işletim sistemini özelleştirmek için aşağıdaki bölümleri kullanın.

##  <a name="prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a>Referans bilgisayarı için hazırlanma  
 Referans bilgisayardan bir işletim sistemi yakalama özelliği kullanmadan önce dikkat etmeniz gereken birkaç nokta vardır.  

###  <a name="decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a>Otomatikleştirilmiş veya el ile yapılandırma arasında karar verme  
 Aşağıdakiler, referans bilgisayarın otomatik veya el ile yapılandırılmasının avantajlarını ve dezavantajlarını özetlemektedir.  

#### <a name="automated-configuration"></a>Otomatik yapılandırma  
 **Üstünlü**  

- Bu yapılandırma, bir yönetici veya kullanıcının bulunma zorunluluğunu ortadan kaldırarak tamamen katılımsız yapılabilir.  

- Diğer referans bilgisayarların yapılandırmasını tekrar etmek için bu görev dizisini yüksek bir güven düzeyinde tekrar kullanabilirsiniz.  

- Görev dizisini en başından tekrar oluşturmak zorunda kalmadan referans bilgisayarlardaki farklara uyum sağlayacak şekilde görev dizisini değiştirebilirsiniz.  

  **Dezavantajlar**  

- Görev dizisi oluşturmadaki ilk eylemin oluşturulup test edilmesi uzun sürebilir.  

- Referans bilgisayarın gereksinimleri önemli düzeyde değişiyorsa görev dizisinin tekrar oluşturulup yeniden test edilmesi çok uzun sürebilir.  

#### <a name="manual-configuration"></a>El ile yapılandırma  
 **Üstünlü**  

- Görev dizisi oluşturmak veya bu diziyi test edip sorunlarını gidermeyi beklemek zorunda değilsiniz.  

- Tüm yazılım paketlerini (Windows 'un kendisi dahil) bir Configuration Manager paketine koymadan doğrudan CD 'lerden yükleyebilirsiniz.  

  **Dezavantajlar**  

- Referans bilgisayar yapılandırmasının doğruluğu o bilgisayarı yapılandıran yöneticiye veya kullanıcıya bağlıdır.  

- Yine de referans bilgisayarın düzgün yapılandırıldığını doğrulamanız ve test etmeniz gerekir.  

- Bu yapılandırma yöntemini tekrar kullanamazsınız.  

- Bir kişinin aktif olarak işlemin tamamının başında bulunmasını gerektirir.  

###  <a name="considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a>Başvuru bilgisayarı için önemli noktalar  
 Aşağıda, referans bilgisayar yapılandırılırken göz önüne alınacak temel öğeler sıralanmıştır.  

-   **Dağıtılacak işletim sistemi**  

     Hedef bilgisayarlarınıza dağıtmayı düşündüğünüz işletim sistemi referans bilgisayara yüklenmiş olmalıdır. Dağıtabileceğiniz işletim sistemleri hakkında daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için altyapı gereksinimleri](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Doğru hizmet paketi**  

     Hedef bilgisayarlarınıza dağıtmayı düşündüğünüz işletim sistemi referans bilgisayara yüklenmiş olmalıdır.  

-   **Doğru yazılım güncelleştirmeleri**  

     Referans bilgisayarından yakaladığınız işletim sistemi görüntüsüne eklenmesini istediğiniz tüm yazılım uygulamalarını yükleyin. Yazılım uygulamalarını, yakalanan işletim sistemi görüntüsünü hedef bilgisayarlarınıza dağıtırken de yükleyebilirsiniz.  

-   **Çalışma grubu üyeliği**  

     Referans bilgisayar, çalışma grubu üyesi olarak yapılandırılmalıdır.  

-   **'İ**  

     Sistem Hazırlama (Sysprep) aracı, Windows işletim sistemlerini yeni donanımlara yüklemek için diğer dağıtım araçlarıyla birlikte kullanılabilen bir teknolojidir. Sysprep, bilgisayar yeniden başlatıldığında yeni bir bilgisayar güvenlik tanımlayıcısı (SID) oluşturacak şekilde bilgisayarı yapılandırarak bir bilgisayarı disk görüntülemeye veya müşteriye teslime hazırlar. Sysprep ayrıca, hedef bilgisayara kopyalanmaması gereken kullanıcıya ve bilgisayara özel ayar ve verileri temizler.  

     Aşağıdaki komutu çalıştırarak referans bilgisayarı Sysprep ile elle hazırlayabilirsiniz:  

     `Sysprep /quiet /generalize /reboot`  

     /generalize seçeneği Sysprep aracından sisteme özgü verileri Windows yüklemesinden kaldırmasını ister. Sisteme özgü bilgiler olay günlükleri, benzersiz güvenlik kimlikleri (SID) ve diğer benzersiz bilgilerdir. Benzersiz sistem bilgileri kaldırıldıktan sonra bilgisayar yeniden başlatılır.  

     [Windows'u Yakalamaya Hazırla](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) görev sırası adımını veya yakalama medyasını kullanarak Sysprep'i otomatikleştirebilirsiniz.  

    > [!IMPORTANT]  
    >  [Windows'u Yakalamaya Hazırla](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) görev sırası adımı, Sysprep çalıştırılmadan önce referans bilgisayardaki yerel yönetici parolasını boş değere sıfırlamaya çalışır. **Parolalar karmaşıklık gereksinimlerine uymalıdır** Yerel Güvenlik ilkesi etkinse, bu görev dizisi adımı yönetici parolasını sıfırlayamaz. Bu senaryoda, görev dizisini çalıştırmadan önce bu ilkeyi devre dışı bırakın.  

     Sysprep hakkında daha fazla bilgi için bkz. [Sysprep (sistem hazırlığı) genel bakış](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview).  

-   **Yükleme senaryolarını kolaylaştırmak için gerekli doğru araçlar ve betikler**  

     Yükleme senaryolarını kolaylaştırmak için gerekli doğru araçlar ve betikler  

-   **Doğru masaüstü özelleştirmesi, örneğin duvar kağıdı, marka ve varsayılan kullanıcı profili**  

     Referans bilgisayardan işletim sistemi görüntüsünü yakaladığınızda referans bilgisayarı eklemek istediğiniz masaüstü özelleştirme özellikleriyle yapılandırabilirsiniz. Masaüstü özellikleri duvar kağıdını, kurumsal markayı ve standart varsayılan kullanıcı profilini içerir.  

##  <a name="manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a>Referans bilgisayarı el ile oluşturma  
 Bir referans bilgisayarı elle oluşturmak için aşağıdaki yordamı kullanın.  

> [!NOTE]  
>  Referans bilgisayarı elle oluşturursanız yakalama medyası kullanarak işletim sistemi görüntüsünü yakalayabilirsiniz. Daha fazla bilgi için bkz. [yakalama medyası oluşturma](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>Referans bilgisayarı elle oluşturmak için  

1. Referans olarak kullanılacak bilgisayarı belirleyin.  

2. Referans bilgisayarı, dağıtmak istediğiniz işletim sistemi görüntüsünü oluşturmak için gereken uygun işletim sistemi ve diğer yazılımlarla yapılandırın.  

   > [!WARNING]  
   >  En azından, uygun işletim sistemini ve hizmet paketini, destek sürücülerini ve varsa gerekli yazılım güncelleştirmelerini yükleyin.  

3. Referans bilgisayarı bir çalışma grubunun üyesi olarak yapılandırın.  

4. Referans bilgisayarda yerel Yönetici parolasını sıfırlayarak parola değerinin boş olmasını sağlayın.  

5. Şu komutu kullanarak Sysprep’i çalıştırın: **sysprep /quiet /generalize /reboot**. /generalize seçeneği Sysprep aracından sisteme özgü verileri Windows yüklemesinden kaldırmasını ister. Sisteme özgü bilgiler olay günlükleri, benzersiz güvenlik kimlikleri (SID) ve diğer benzersiz bilgilerdir. Benzersiz sistem bilgileri kaldırıldıktan sonra bilgisayar yeniden başlatılır.  

   Referans bilgisayarı hazırlandıktan sonra, referans bilgisayardan işletim sistemi görüntüsünü yakalamak için bir görev dizisi kullanın.  Ayrıntılı adımlar için bkz. [Var olan bir referans bilgisayardan işletim sistemi görüntüsü yakalama](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a>Başvuru bilgisayarı oluşturmak için görev dizisi kullanma  
 İşletim sistemi, sürücüler, uygulamalar ve daha fazlasını dağıtmak için bir görev dizisi kullanarak bir referans bilgisayar oluşturmak için süreci otomatik hale getirebilirsiniz.  Referans bilgisayarını oluşturmak ve referans bilgisayardan işletim sistemi görüntüsünü yakalamak için aşağıdaki adımları kullanın.  

-   Referans bilgisayarını oluşturmak ve referans bilgisayardan işletim sistemi görüntüsünü yakalamak için bir görev dizisi kullanın.  Ayrıntılı adımlar için bkz. [Başvuru bilgisayarı oluşturmak ve yakalamak için görev dizisi kullanma](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).  
