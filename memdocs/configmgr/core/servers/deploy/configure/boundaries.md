---
title: Sınırları tanımla
titleSuffix: Configuration Manager
description: İntranetinizde, yönetmek istediğiniz cihazları içerebilen ağ konumlarını nasıl tanımlayacağınızı anlayın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 41c0d08c5f445cd6d643542cfaa646bc2d89de76
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128435"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Ağ konumlarını Configuration Manager için sınır olarak tanımlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sınırları, ağınızda yönetmek istediğiniz cihazları içeren konumlardır. Örneğin, bir Active Directory site veya ağ IP adresi gibi farklı türlerde sınırlar oluşturabilirsiniz. Configuration Manager istemcisi benzer bir ağ konumunu belirlediğinde, bu cihaz sınırın bir parçasıdır.

Configuration Manager aşağıdaki sınır türlerini destekler:

- IP alt ağı
- Active Directory sitesi
- IPv6 öneki
- IP adresi aralığı
- VPN (sürüm 2006 ' den başlayarak)

Tek tek sınırları el ile oluşturabilir veya [Active Directory orman keşfi](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)kullanabilirsiniz. Bu bulma yöntemi IP alt ağları ve Active Directory siteleri için sınırları otomatik olarak bulur ve oluşturur. Active Directory orman keşfi bir Active Directory sitesi için bir üst ağ belirlediğinde Configuration Manager, üst ağı bir IP adresi aralığı sınırına dönüştürür.

Bir cihaz, beklediğiniz sınırın içinde değilse, ağ konumunu sınır olarak tanımlamadınız olabilir. Bir cihazın ağ konumu şüpheli olduğunda, doğrulamak için cihazda aşağıdaki Windows komutlarını kullanın:

- IP adresi:`ipconfig`
- Active Directory site:`nltest /dsgetsite`
- SANAL`ipconfig /all`

## <a name="boundary-types"></a>Sınır türleri

### <a name="ip-subnet"></a>IP alt ağı

IP alt ağ sınır türü bir **alt ağ kimliği**gerektiriyor. Örneğin, `169.254.0.0`. **Ağ** (varsayılan ağ geçidi) ve **alt ağ maskesi** değerlerini sağlarsanız, Configuration Manager **alt ağ kimliğini**otomatik olarak hesaplar. Sınırı kaydettiğinizde Configuration Manager yalnızca alt ağ KIMLIĞI değerini kaydeder.

> [!NOTE]
> Configuration Manager, sınır olarak doğrudan bir üst ağ girişini desteklemez. Bunun yerine, IP adres aralığı sınır türünü kullanın.

### <a name="active-directory-site"></a>Active Directory sitesi

**Active Directory site** sınır türü için, site adını belirtirsiniz. Ad yazabilir veya site sunucusunun yerel ormanına gidebilirsiniz.

Sınır için bir Active Directory sitesi belirttiğinizde, sınır bu Active Directory sitesinin üyesi olan her bir IP alt ağını içerir. Active Directory sitesinin yapılandırması Active Directory'de değişirse, bu sınırda yer alan ağ konumları da değişir.  

Active Directory site sınırları, bulut etki alanına katılmış cihazlar olarak da adlandırılan saf Azure Active Directory (Azure AD) cihazları için çalışmaz. Şirket içinde dolaşırsa ve yalnızca Active Directory site türü sınırları oluşturuyorsanız, bu cihazlar bir sınır içinde olmayacaktır.

> [!TIP]
> Bir cihazın geçerli Active Directory sitesini görmek için aşağıdaki Windows komutunu kullanın: `nltest /dsgetsite` .
>
> Bir istemcinin bulut etki alanına katılmış olup olmadığını anlamak için aşağıdaki Windows komutunu kullanın: `dsregcmd /status` . Daha fazla bilgi için bkz. [dsregcmd komutu-cihaz durumu](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd).

### <a name="ipv6-prefix"></a>IPv6 öneki

**IPv6 öneki** sınır türü Için bir **ön ek**belirtirsiniz. Örneğin, `2001:1111:2222:3333`.

### <a name="ip-address-range"></a>IP adresi aralığı

**IP adresi aralığı** sınır türü için, Aralık IÇIN **Başlangıç IP ADRESINI** ve **bitiş IP adresini** belirtin. Aralık, bir IP alt ağının veya birden çok IP alt ağının bir parçasını içerebilir. Bir süper ağı desteklemek için bir IP adresi aralığı sınır türü kullanın.

Tek bir IP adresi için sınır tanımlamak üzere bu türü de kullanabilirsiniz. Başlangıç ve bitiş IP adreslerini aynı değer olarak ayarlayın. Bu yapılandırma, benzersiz cihazlar veya test ortamları için yararlı olabilir.

### <a name="vpn"></a>VPN

<!--7020519-->

Sürüm 2006 ' den başlayarak, uzak istemcilerin yönetilmesini kolaylaştırmak için VPN 'Ler için bir sınır türü oluşturun. Bir istemci bir konum isteği gönderdiğinde, ağ yapılandırması hakkında ek bilgiler içerir. Bu bilgilere bağlı olarak, sunucu istemcinin VPN üzerinde olup olmadığını belirler. İstemcinin sınırında ilişkilendirilmesi Configuration Manager için cihazı VPN 'ye bağlayın.

VPN sınırını birkaç yolla yapılandırabilirsiniz:

- **VPN 'Yi otomatik algıla**: Configuration Manager Noktadan Noktaya Tünel Protokolü (PPTP) kullanan HERHANGI bir VPN çözümünü algılar. VPN 'nizi algılamazsa, diğer seçeneklerden birini kullanın. Konsol listesindeki sınır değeri olacaktır `Auto:On` .

- **Bağlantı adı**: cihazdaki VPN bağlantısının adını belirtin. Bu, VPN bağlantısı için Windows 'daki ağ bağdaştırıcısının adıdır. Configuration Manager dizenin ilk 250 karakteriyle eşleşir, ancak joker karakterleri veya kısmi dizeleri desteklemez. Konsol listesindeki sınır değeri `Name:<name>` , burada `<name>` belirttiğiniz bağlantı adıdır.

  Örneğin, `ipconfig` komutu cihazda çalıştırın ve bölümlerden biri ile başlar: `PPP adapter ContosoVPN:` . Dizeyi `ContosoVPN` **bağlantı adı**olarak kullanın. Listede olarak görüntülenir `Name:CONTOSOVPN` .

- **Bağlantı açıklaması**: VPN bağlantısının açıklamasını belirtin. Configuration Manager dizenin ilk 243 karakteriyle eşleşir, ancak joker karakterleri veya kısmi dizeleri desteklemez. Konsol listesindeki sınır değeri `Description:<description>` , burada `<description>` belirttiğiniz bağlantı açıklamasıdır.

  Örneğin, `ipconfig /all` komutu cihazda çalıştırın ve bağlantılardan biri aşağıdaki satırı içerir: `Description . . . . . . . . . . . : ContosoMainVPN` . `ContosoMainVPN` **Bağlantı açıklaması**olarak dizeyi kullanın. Listede olarak görüntülenir `Description:CONTOSOMAINVPN` .

> [!IMPORTANT]
> Bu özellikten tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik görüntülenir. Tüm senaryo, istemci sürümü de en son olana kadar işlevsel değildir.
>
> Bir işletim sistemi dağıtımı sırasında bu VPN sınırını kullanmak için, önyükleme görüntüsünü en son istemci ikili dosyalarını içerecek şekilde güncelleştirdiğinizden emin olun.

## <a name="create-a-boundary"></a>Sınır oluşturma

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **sınırlar** düğümünü seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **sınır oluştur**' u seçin.

1. **Sınır oluştur** penceresinin **genel** sekmesinde aşağıdaki bilgileri belirtin:

    - **Açıklama**: sınırı, kolay bir ad veya başvuruya göre belirler.

        > [!NOTE]
        > Configuration Manager, kenarlığını türüne ve kapsamına göre otomatik olarak adlandırır. Adı değiştiremezsiniz.

    - **Tür**: oluşturulacak sınır türünü seçin. Ardından, türün gerektirdiği ek bilgileri belirtin. Daha fazla bilgi için bkz. [sınır türleri](#boundary-types).

1. **Sınır grupları** sekmesine geçin. Sitede zaten sınır grupları varsa, bu yeni sınırı bir veya daha fazla gruba hemen ekleyebilirsiniz.

1. Yeni sınırı kaydetmek için **Tamam ' ı** seçin.

## <a name="configure-a-boundary"></a>Sınır yapılandırma

> [!TIP]
> Bir sınır oluşturduğunuzda Configuration Manager, sınırın türüne ve kapsamına göre otomatik olarak adlandırır. Bu adı değiştiremezsiniz. Configuration Manager konsolundaki sınırı belirlemesine yardımcı olmak için bir açıklama belirtin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **sınırlar** düğümünü seçin.

1. Değiştirmek istediğiniz sınırı seçin. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.

1. Sınırın **Özellikler** penceresinde, **genel** sekmesinde aşağıdaki ayarları yapılandırabilirsiniz:

    - **Açıklamayı** Düzenle
    - Sınırın **türünü** değiştirin
    - Ağ konumlarını düzenleyerek sınırın kapsamını değiştirin. Örneğin, bir Active Directory sitesi sınırı için yeni bir Active Directory sitesi adı belirtebilirsiniz.

1. Bu sınırla ilişkilendirilmiş site sistemlerini görüntülemek için **site sistemleri** sekmesine geçin. Bu yapılandırmayı sınırın özelliklerinden değiştiremezsiniz.

    > [!TIP]
    > Bir sunucunun bir sınır için site sistemi olarak listelenmesi için, bu sınırı içeren en az bir sınır grubu için site sistem sunucusu olarak ilişkilendirin. Bu yapılandırmayı bir sınır grubunun **Başvurular** sekmesinde yapın. Daha fazla bilgi için bkz. [site atamasını yapılandırma ve site sistemi sunucularını seçme](boundary-group-procedures.md#bkmk_references).

1. Bu sınırın sınır grubu üyeliğini değiştirmek için **sınır grupları** sekmesini seçin:

    - Bu sınırı bir veya daha fazla sınır grubuna eklemek için **Ekle**' yi seçin. Bir veya daha fazla sınır grubu seçin ve ardından **Tamam**' ı seçin.

    - Bu sınırı bir sınır grubundan kaldırmak için, sınır grubunu seçin ve ardından **Kaldır**' ı seçin.

1. Sınır özelliklerini kapatmak ve yapılandırmayı kaydetmek için **Tamam** ' ı seçin.

## <a name="next-steps"></a>Sonraki adımlar

Her sınır hiyerarşinizdeki her site tarafından kullanılabilir. Sınır oluşturduktan sonra sınırı bir veya daha fazla [sınır grubuna](boundary-groups.md)ekleyin.
