---
title: Azure'da laboratuvar oluşturma
titleSuffix: Configuration Manager
description: Azure şablonları kullanarak Configuration Manager Teknik Önizleme Laboratuvarı veya güncel dal değerlendirmesi Laboratuvarı oluşturmayı otomatikleştirin
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd2a8b3bfb7c4b8af277616c7eaed329bc143bb7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711605"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Azure 'da Configuration Manager Laboratuvarı oluşturma

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

<!--3556017-->

Bu kılavuzda, Microsoft Azure bir Configuration Manager laboratuvar ortamının nasıl oluşturulacağı açıklanmaktadır. Azure kaynaklarını kullanarak bir laboratuvarın oluşturulmasını basitleştirmek ve otomatikleştirmek için Azure şablonlarını kullanır. İki Azure şablonu sağlanır: 

- Configuration Manager Technical Preview Azure şablonu, Configuration Manager Technical Preview dalının en son sürümünü yüklüyor.
- Geçerli dalı Configuration Manager Azure şablonu, Configuration Manager geçerli dalın en son sürümünün değerlendirmesini kurar. 

Daha fazla bilgi için bkz. [Azure 'da Configuration Manager](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Önkoşullar

Bu işlem, aşağıdaki nesneleri oluşturabileceğiniz bir Azure aboneliği gerektirir: 
- Etki alanı contoller ve MP & DP rolleri için iki Standard_B2s sanal makine.
- Birincil site sunucusu ve SQL veritabanı sunucusu için bir Standard_B2ms sanal makine.
- Standard_LRS depolama hesabı

> [!Tip]  
> Olası maliyetleri belirlemede yardımcı olması için bkz. [Azure Fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) .  



## <a name="process"></a>İşleme

1. [Configuration Manager Technical Preview şablonuna](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) gidin veya [geçerli dal şablonunu Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Azure portal açan **Azure 'A dağıt**' ı seçin.  

3. Azure hızlı başlangıç şablonunu aşağıdaki bilgilerle doldurun:

    - Temel Bilgiler  

        - **Abonelik**: VM 'lerin oluşturulacağı aboneliğin adı  

        - **Kaynak grubu**: Bu VM 'ler için kullanılacak bir kaynak grubu seçin  

        - **Konum**: Bu laboratuvar ortamını barındırmak Için bir Azure veri merkezi seçin  

    - Ayarlar  

        - **Ön ek**: makinelerin ön ek adı. Daha fazla bilgi için bkz. [Azure VM bilgileri](#azure-vm-info).  

        - **Yönetici Kullanıcı adı**: yönetici haklarına sahip VM 'lerde bir kullanıcının adı. Bu kullanıcıyı VM 'lerde oturum açmak için kullanırsınız.  

        - **Yönetici parolası**: parolanın Azure karmaşıklık gereksinimlerini karşılaması gerekir. Daha fazla bilgi için bkz. [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Azure için aşağıdaki ayarlar gereklidir. Varsayılan değerleri kullanın. Bu değerleri değiştirmeyin.  
    > 
    > - yapıt konumu: Bu şablon için betiklerin konumu ** \_** <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - yapıt konumu SAS belirteci: yapıt konumuna erişmek için sastoken gereklidir ** \_**  
    > 
    > - **Konum**: tüm kaynakların konumu

4. Hüküm ve koşulları okuyun. Kabul ediyorsanız, **yukarıda belirtilen hüküm ve koşulları kabul**ediyorum ' u seçin. Ardından devam etmek için **satın al** ' ı seçin. 

Azure, ayarları doğrular ve ardından dağıtıma başlar. Azure portal dağıtım durumunu denetleyin. 

> [!NOTE]
> İşlem, 2-4 saat sürebilir. Azure portal başarılı dağıtımı gösterdiği zaman bile, yapılandırma betikleri çalışmaya devam eder. İşlem sırasında VM 'Leri yeniden başlatmayın.

Yapılandırma betiklerinin durumunu görmek için `<prefix>PS1` sunucuya bağlanın ve şu dosyayı görüntüleyin:. `%windir%\TEMP\ProvisionScript\PS1.json` Tüm adımları tamamlandı olarak gösteriyorsa, işlem yapılır.

VM 'lere bağlanmak için öncelikle her bir VM 'nin genel IP adreslerini Azure portal alın. SANAL makineye bağlandığınızda, etki alanı adı olur `contoso.com`. Dağıtım şablonunda belirttiğiniz kimlik bilgilerini kullanın. Daha fazla bilgi için bkz. [Windows çalıştıran bir Azure sanal makinesine bağlanma ve oturum](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon)açma.



## <a name="azure-vm-info"></a>Azure VM bilgileri

Üç sanal makine aşağıdaki özelliklere sahiptir:
- 150 GB disk alanı
- Hem ortak hem de özel IP adresi. Genel IP 'Ler, yalnızca TCP bağlantı noktası 3389 üzerinde Uzak Masaüstü bağlantılarına izin veren bir ağ güvenlik grubudur. 

Dağıtım şablonunda belirttiğiniz ön ek VM adı önekidir. Örneğin, ön ek olarak "contoso" değerini ayarlarsanız, etki alanı denetleyicisi makine adı olur `contosoDC`.


### `<prefix>DC01`

- Active Directory etki alanı denetleyicisi
- İki CPU ve 4 GB bellek içeren Standard_B2s
- Windows Server 2019 Datacenter Edition

#### <a name="windows-features-and-roles"></a>Windows özellikleri ve rolleri
- Active Directory Domain Services (ekler)
- .NET
- Uzaktan değişiklikleri sıkıştırma (RDC)


### `<prefix>PS01`

- İki CPU ve 8 GB bellek içeren Standard_B2ms
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows PE ile Windows 10 ADK 
- Birincil site Configuration Manager

#### <a name="windows-features-and-roles"></a>Windows özellikleri ve rolleri
- .NET
- Uzaktan değişiklikleri sıkıştırma (RDC) 
- Internet Information Service (IIS)


### `<prefix>DPMP01`

- İki CPU ve 4 GB bellek içeren Standard_B2s
- Windows Server 2019 Datacenter Edition
- Dağıtım noktası
- Yönetim noktası

#### <a name="windows-features-and-roles"></a>Windows özellikleri ve rolleri
- .NET
- Uzaktan değişiklikleri sıkıştırma (RDC) 
- Internet Information Service (IIS)
- Arka plan Akıllı Aktarım Hizmeti (BITS)

### `<prefix>CL01`

- Yalnızca Configuration Manager geçerli dal değerlendirme şablonu
- Windows 10
- Configuration Manager istemcisi
