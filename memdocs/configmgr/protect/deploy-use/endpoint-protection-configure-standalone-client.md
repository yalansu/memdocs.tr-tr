---
title: Tek başına istemcide Endpoint Protection yapılandırma
titleSuffix: Configuration Manager
description: Tek başına istemcide Endpoint Protection yapılandırmayı öğrenin.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a7640fade49c70c013cf1d7c0939957a07f223fd
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546905"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>Tek başına istemcide Endpoint Protection yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kuruluşunuz, Microsoft uç noktası Configuration Manager yönetebileceğiniz veya koruyabileceğiniz bir dizi bağımsız istemciye sahip olabilir. Herhangi bir uç nokta koruması yoksa, bu tek başına istemciler olası kötü amaçlı yazılım saldırılarına karşı savunmasızdır. Bu bağımsız istemcileri korumak için, bu konuda açıklandığı gibi bunları Endpoint Protection el ile yapılandırabilirsiniz.

Tek başına istemcideki Endpoint Protection el ile yapılandırmak için:

- [Tek başına istemci için bir kötü amaçlı yazılımdan koruma ilkesi oluşturma](#create-an-antimalware-policy-for-the-standalone-client)
- [Endpoint Protection istemci yükleme paketini tek başına istemcisine aktar](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Tek başına istemcisine Endpoint Protection yükleme](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>Önkoşullar

Tek başına istemcisinde Endpoint Protection yapılandırmaya yönelik önkoşullar aşağıda verilmiştir:

- **scepinstall.exe**Endpoint Protection istemci yükleme paketine erişiminizin olması gerekir. Bu paketi **C:\Program Files\Microsoft Configuration Manager\Client** klasöründe bulabilirsiniz. 
- [Endpoint Protection istemcileri Için ocak 2017, kötü amaçlı yazılımdan koruma platformu güncelleştirmesinin](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie) yüklü olduğundan emin olun. 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>Tek başına istemci için bir kötü amaçlı yazılımdan koruma ilkesi oluşturma

Bu adımda, Configuration Manager konsolunda özel bir kötü amaçlı yazılımdan koruma ilkesi oluşturup bağımsız istemciye aktarırsınız.

Kötü amaçlı yazılımdan koruma ilkesi oluştururken, tek başına istemcide ilke tanımlarını güncel tutmak için tanım güncelleştirme kaynağını yapılandırmanız gerekir. Tek başına istemciniz Internet 'e bağlıysa, tanım güncelleştirme kaynağını [Microsoft Update](endpoint-definitions-microsoft-updates.md) ve [Microsoft kötü amaçlı yazılımdan koruma merkezi](endpoint-definitions-protection-center.md)olarak yapılandırabilirsiniz. Alternatif olarak, tanım dağıtım kaynağı olarak [ağ paylaşma](endpoint-definitions-network.md) ' yı seçin ve en son tanım güncelleştirme paketiyle düzenli olarak güncelleştirin. 

Tek başına istemci için bir kötü amaçlı yazılımdan koruma ilkesi oluşturmak için:

1. **Configuration Manager** konsolunda, **varlıklar ve uyum**' a tıklayın.
2. **Varlıklar ve Uyum** çalışma alanında **Endpoint Protection**’ı genişletin ve **Kötü Amaçlı Yazılımdan Koruma İlkeleri**’ne tıklayın.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **Kötü Amaçlı Yazılımdan Koruma İlkesi Oluştur**’a tıklayın.
4. **Kötü Amaçlı Yazılımdan Koruma İlkesi Oluştur** iletişim kutusunun **Genel** bölümünde, ilke için bir ad ve bir açıklama belirtin.
5. **Kötü Amaçlı Yazılımdan Koruma İlkesi Oluştur** iletişim kutusunda, bu kötü amaçlı yazılımdan koruma ilkesi için gerekli olan ayarları yapılandırıp **Tamam**’a tıklayın. Yapılandırabileceğiniz ayarların listesi için bkz. [kötü amaçlı yazılımdan koruma Ilkesi ayarlarının listesi](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings).
    > [!NOTE]
    > **Tanım güncelleştirmeleri** ayarı için, tek başına istemciniz internet 'e bağlıysa **Microsoft Update dağıtılan güncelleştirmeler** ve **Microsoft kötü amaçlı yazılımdan koruma merkezi 'nden dağıtılan** güncelleştirmeler ' i seçin.  
    > Alternatif olarak, ilke tanımlarını ağ paylaşımı üzerinden dağıtmak için **UNC dosya paylaşımlarından güncelleştirmeler** ' i seçin. Ardından, bir ağ paylaşımındaki tanım güncelleştirmeleri dosyalarının konumuna bir veya daha fazla UNC yolu ekleyin.

6. Yeni oluşturulan ilkeyi bir XML olarak dışarı aktar:
    1. **Kötü amaçlı yazılımdan koruma ilkeleri** listesinde, ilkenize sağ tıklayın.
    1. **Export** (Dışarı aktar) öğesini seçin.
    1. İlkeyi bir XML olarak kaydedin (örneğin, **standalone.xml**).
7. Yeni kötü amaçlı yazılımdan koruma ilkesi XML 'sini, Endpoint Protection yapılandırmak istediğiniz tek başına istemciye aktarın.

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Endpoint Protection istemci yükleme paketini tek başına istemcisine aktar

Bu adımda, Endpoint Protection istemci yükleme paketini (**scepinstall.exe**) Configuration Manager sunucusundan kopyalar ve bağımsız istemciye aktarırsınız.

1. Configuration Manager sunucusunda oturum açın.
2. Configuration Manager yükleme klasörünün **istemci** klasörüne gidin (**C:\Program Files\Microsoft Configuration Manager\Client**).
3. **scepinstall.exe**kopyalayın.
4. **scepinstall.exe** , Endpoint Protection istemci yazılımını yüklemek istediğiniz hedef tek başına istemciye aktarın.

## <a name="install-endpoint-protection-on-the-standalone-client"></a>Tek başına istemcisine Endpoint Protection yükleme
Bu adımda, tek başına istemcideki komut isteminden yükleyici paketini (**scepinstall.exe**) ve kötü amaçlı yazılımdan koruma ilkesini (daha önce Configuration Manager sunucudan aktarılan) çalıştırırsınız.

Tek başına istemcisine Endpoint Protection yüklemek için:

1. Tek başına istemcisinde, yönetici olarak bir komut istemi açın.
2. Dizini, **scepinstall.exe** yükleyici dosyasını kaydettiğiniz klasöre değiştirin.
3. Kötü amaçlı yazılımdan koruma ilkesiyle **scepinstall.exe** çalıştırmak için aşağıdaki komutu girin:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    `full path`Kötü amaçlı yazılımdan koruma ILKESI XML dosyasını ve `policy file` kötü amaçlı yazılımdan koruma ilkesi dosya adını kaydettiğiniz yol ile değiştirin.
 
    Yükleyici ayıklanır ve Yükleme Sihirbazı başlatılır.

4. İstemci yüklemesini gerçekleştirmek için ekrandaki yönergeleri izleyin.

    Yükleme sihirbazının son ekranında, en son güncelleştirmeleri aldıktan sonra bilgisayarı olası tehditlere karşı tarama seçeneği varsayılan olarak seçilidir. Taramayı atlamak için onay kutusunu temizleyebilirsiniz.

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>Tek başına Endpoint Protection istemcisinde kötü amaçlı yazılımdan koruma ilkesi ayarlarını değiştirme

Tek başına Endpoint Protection istemcinizdeki kötü amaçlı yazılımdan koruma ilkesini değiştirmek veya güncelleştirmek için: 

1. [Tek başına istemci için bir kötü amaçlı yazılımdan koruma Ilkesi oluşturun](#create-an-antimalware-policy-for-the-standalone-client).
2. Tek başına istemcisinde aşağıdaki komutu çalıştırın:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

`full path`Yeni kötü amaçlı yazılımdan koruma ILKESI XML dosyasını ve `policy file` kötü amaçlı yazılımdan koruma ilkesi dosya adını kaydettiğiniz yol ile değiştirin.
