---
title: Linux ve UNIX istemcilerini yükseltme
titleSuffix: Configuration Manager
description: Configuration Manager bir Linux veya UNIX sunucusunda bir istemciyi yükseltin.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715399"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Configuration Manager ' de Linux ve UNIX sunucuları için istemcileri yükseltme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Bir bilgisayardaki Linux ve UNIX istemcisinin sürümünü, öncelikle geçerli istemciyi kaldırmadan daha yeni bir sürüme yükseltebilirsiniz. Bunu yapmak için, **-St pdb** komut satırı özelliğini kullanırken yeni istemci yükleme paketini bilgisayara yüklemeniz gerekir. Linux ve UNIX istemcisi yüklendiğinde, yeni istemci dosyalarını var olan istemci verilerinin üzerine yazar. Ancak-St **pdb** komut satırı özelliği, istemcinin benzersiz tanımlayıcısını (GUID), bilgilerin yerel veritabanını ve sertifika deposunu saklamak için, yüklemeye yönelik işlemi yönlendirir. Bu bilgiler daha sonra yeni istemci yüklemesi tarafından kullanılır.  

 Örneğin, istemciyi Linux ve UNIX için özgün Configuration Manager istemcisi sürümünden çalıştıran bir RHEL5 x64 bilgisayara sahipsiniz. Bu istemciyi toplu güncelleştirme 1 ' den istemci sürümüne yükseltmek için, komut dosyasını, toplu güncelleştirme 1 ' den ilgili istemci paketini, **-Sin pdb** komut satırı anahtarı ile **birlikte yükleyecek şekilde** el ile çalıştırırsınız. Aşağıdaki örnek komut satırına bakın:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Linux ve UNIX Sunucularında İstemciyi Yükseltmek Yazılım Dağıtımını Kullanma  
 Linux ve UNIX istemcisini yeni bir istemci sürümüne yükseltmek için bir yazılım dağıtımı kullanabilirsiniz. Ancak, yeni istemci yüklemesi önce geçerli istemciyi kaldırması gerektiğinden Configuration Manager istemcisi Yeni istemciyi yüklemek için yükleme komut dosyasını doğrudan çalıştıramıyor. Bu eylem, yeni istemci yüklemesi başlamadan önce yükleme komut dosyasını çalıştıran Configuration Manager istemci işlemini sona erdir. Yeni istemciyi yüklemek üzere bir yazılım dağıtımını başarıyla kullanmak için, yüklemeyi gelecek bir zamanda başlayacak ve işletim sisteminin yerleşik zamanlama özellikleri tarafından çalıştırılacak şekilde zamanlamanız gerekir.  

 Yeni istemci yükleme paketinin dosyalarını istemci bilgisayara kopyalamak için bir yazılım dağıtımı kullanın. Ardından istemci yükleme işlemini zamanlamak için bir betiği dağıtıp çalıştırın. Betik, başlangıcını geciktirmek için işletim sisteminin yerleşik **at** komutunu kullanır. Betik çalıştığında, işlemi bilgisayardaki Configuration Manager istemcisi değil, istemci işletim sistemi tarafından yönetilir. Bu davranış, komut dosyası tarafından çağrılan komut satırının öncelikle Configuration Manager istemcisini kaldırmasına ve ardından Yeni istemciyi yüklemesine olanak tanır. Bu eylemler, Linux veya UNIX bilgisayarda istemci yükseltme işlemini tamamlar. Yükseltme tamamlandıktan sonra, yükseltilen istemci Configuration Manager tarafından yönetilmeye devam eder.  

 Linux ve UNIX istemcisini yükseltmek üzere bir yazılım dağıtımını yapılandırmanıza yardımcı olması için aşağıdaki yordamı kullanın. Aşağıdaki adımları ve örnekler, istemcinin başlangıç sürümünü çalıştıran bir RHEL5 x64 bilgisayarını toplu güncelleştirme 1 istemci sürümüne yükseltir.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Linux ve UNIX sunucularında istemciyi yükseltmek için yazılım dağıtımını kullanma  

1. Yeni istemci yükleme paketini yükseltmek için Configuration Manager istemcisini çalıştıran bilgisayara kopyalayın.  

    Örneğin, istemci yükleme paketini ve toplu güncelleştirme 1 için yükleme komut dosyasını istemci bilgisayarda aşağıdaki konuma yerleştirin: **/tmp/Patch**  

2. Configuration Manager istemcisinin yükseltmesini yönetmek için bir komut dosyası oluşturun. Ardından, komut dosyasının bir kopyasını istemci bilgisayarda, 1. adımdaki istemci yükleme dosyaları olarak aynı klasöre yerleştirin.  

    Betik için belirli bir ad gerekli değildir. İstemci yükleme dosyalarını istemci bilgisayardaki yerel bir klasörden kullanmak ve **-St pdb** komut satırı özelliğini kullanarak istemci yükleme paketini yüklemek için yeterli komut satırı içermesi gerekir. Yüklemekte olduğunuz yeni istemci tarafından kullanılmak üzere geçerli istemcinin benzersiz tanımlayıcısını sürdürmek için-LIST **pdb** komut satırı özelliğini kullanın.  

    Örneğin, aşağıdaki satırları içeren **Upgrade.sh** adlı bir komut dosyası oluşturun:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Ardından, istemci bilgisayardaki **/tmp/Patch** klasörüne kopyalayın.

3. Her bir istemcinin bilgisayardaki yerleşik **at** komutunu kullanarak, komut dosyası çalışmadan önce **upgrade.sh** komut dosyasını kısa bir gecikmeyle çalıştırması için yazılım dağıtımını kullanın.  

    Örneğin, komut dosyasını çalıştırmak için şu komut satırını kullanın: **at-f/tmp/Upgrade,sh-8 Now + 5 dakika**  

   İstemci **upgrade.sh** komut dosyasını çalıştırmayı başarıyla zamanladıktan sonra istemci, yazılım dağıtımının başarıyla tamamlandığını belirten bir durum iletisi gönderir. Ancak, gerçek istemci yüklemesi gecikmeden sonra bilgisayar tarafından yönetilir. İstemci yükseltmesi tamamlandıktan sonra istemci bilgisayardaki **/var/opt/microsoft/scxcm.log** dosyasını gözden geçirerek yüklemeyi doğrulayın. Configuration Manager konsolundaki **varlıklar ve uyum** çalışma alanının **cihazlar** düğümünde istemcinin ayrıntılarını görüntüleyerek istemcinin yüklendiğini ve siteyle iletişim kurduğunu onaylayın.  
