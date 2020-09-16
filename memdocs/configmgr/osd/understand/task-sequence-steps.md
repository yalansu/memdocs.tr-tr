---
title: Görev dizisi adımları
titleSuffix: Configuration Manager
description: Configuration Manager görev dizisine ekleyebileceğiniz adımlar hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49792ea588f01cc57a1dbce9cc137b94a0e4d291
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574805"
---
# <a name="task-sequence-steps"></a>Görev dizisi adımları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki görev dizisi adımları Configuration Manager bir görev dizisine eklenebilir. Daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](task-sequence-editor.md).  

## <a name="common-settings"></a>Ortak ayarlar

Aşağıdaki ayarlar tüm görev dizisi adımları için ortaktır:

### <a name="properties-for-all-steps"></a>Tüm adımların özellikleri

- **Ad**: görev sırası Düzenleyicisi, bu adımı anlatmak için bir kısa ad belirtmenizi gerektirir. Yeni bir adım eklediğinizde, görev sırası Düzenleyicisi adı varsayılan olarak türe ayarlar. **Ad** uzunluğu 50 karakteri aşamaz.  

- **Açıklama**: isteğe bağlı olarak, bu adımla ilgili daha ayrıntılı bilgi belirtin. **Açıklama** uzunluğu 256 karakteri aşamaz.  

Bu makalenin geri kalanında her bir görev dizisi adımının **Özellikler** sekmesinde diğer ayarlar açıklanmaktadır.

### <a name="options-for-all-steps"></a>Tüm adımlar için seçenekler

- **Bu adımı devre dışı bırakın**: görev dizisi, bir bilgisayarda çalıştırıldığında bu adımı atlar. Bu adımın simgesi, görev sırası düzenleyicisinde gri renkte bulunur.  

- **Hatada devam et**: Adım çalıştırılırken bir hata oluşursa, görev sırası devam eder. Daha fazla bilgi için bkz. [görevleri otomatikleştirme Için planlama değerlendirmeleri](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups).  

- **Koşul Ekle**: görev dizisi, adımı yürüttüğünde karar vermek için bu koşullu deyimleri değerlendirir. Bir görev dizisi değişkenini koşul olarak kullanmanın bir örneği için bkz. [görev dizisi değişkenlerini kullanma](using-task-sequence-variables.md#bkmk_access-condition). Koşullar hakkında daha fazla bilgi için bkz. [görev dizisi Düzenleyicisi-koşullar](task-sequence-editor.md#bkmk_conditions).

Belirli görev dizisi adımları için aşağıdaki bölümler, **Seçenekler** sekmesindeki diğer olası ayarları anlatmaktadır.



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> Veri Görüntüsünü Uygula

Veri görüntüsünü belirtilen hedef bölüme kopyalamak için bu adımı kullanın.  

Bu adım yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **görüntüler**' i seçin ve **veri görüntüsünü Uygula**' yı seçin.

### <a name="variables-for-apply-data-image"></a>Veri Görüntüsünü Uygula değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>Veri Görüntüsünü Uygula cmdlet 'leri

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-Cmtsstepapplydataımage](/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage)
- [New-Cmtsstepapplydataımage](/powershell/module/configurationmanager/New-CMTSStepApplyDataImage)
- [Remove-Cmtsstepapplydataımage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage)
- [Set-Cmtsstepapplydataımage](/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage)

### <a name="properties-for-apply-data-image"></a>Veri Görüntüsünü Uygula özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="image-package"></a>Görüntü Paketi

Bu görev sırası tarafından kullanılan **görüntü paketini** belirtmek için **Araştır** ' ı seçin. **Bir Paket Seçin** iletişim kutusunda yüklemek istediğiniz paketi seçin. İletişim kutusunun en altında, varolan her görüntü paketi için ilişkili özellik bilgileri görüntülenir. Seçili **Görüntü Paketi**'nden yüklemek istediğiniz **Görüntü**'yü seçmek için açılır listeyi kullanın.  

> [!NOTE]  
> Bu görev dizisi eylemi, görüntüyü bir veri dosyası olarak değerlendirir. Bu eylem, görüntüyü bir işletim sistemi olarak önyüklemek için herhangi bir kurulum yapmaz.  

#### <a name="destination"></a>Hedef

Aşağıdaki seçeneklerden birini yapılandırın:

- **Sonraki kullanılabilir bölüm**: Bu görev dizisinde bir **işletim sistemini Uygula** veya **veri görüntüsünü Uygula** adımının bir sonraki sıralı bölümünü kullanın.  

- **Belirli disk ve bölüm**: **disk** numarasını (0 ' dan başlayarak) ve **bölüm** numarasını (1 ' den başlayarak) seçin.  

- **Belirli mantıksal sürücü harfi**: Windows PE 'nin bölüme atadığı **sürücü harfini** belirtin. Bu sürücü harfi, yeni dağıtılan işletim sistemi tarafından atanan sürücü harfinden farklı olabilir.  

- **Bir değişkende depolanan mantıksal sürücü harfi**: Windows PE tarafından bölüme atanan sürücü harfini içeren görev dizisi değişkenini belirtin. Bu değişken genellikle **Diski Biçimlendir ve bölümle disk** sırası adımı Için **bölüm özellikleri** iletişim kutusunun Gelişmiş bölümünde ayarlanır.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Görüntüyü uygulamadan önce bölümdeki tüm içeriği silin  

Görev dizisinin, görüntüyü yüklemeden önce hedef bölümdeki tüm dosyaları sildiğini belirtir. Bu eylem, bölümün içeriğini silmeyerek önceden hedeflenen bir bölüme ek içerik uygulamak için kullanılabilir.  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Sürücü paketini Uygula  

Sürücü paketindeki tüm sürücüleri indirmek ve Windows işletim sistemine yüklemek için bu adımı kullanın.

**Sürücü Paketini Uygula** görev dizisi adımı bir sürücü paketindeki tüm cihaz sürücülerini Windows tarafından kullanılabilir hale getirir. Bu adımı, **Işletim sistemini Uygula** ve **Windows 'u ve ConfigMgr 'yi Kur** adımları arasında ekleyerek paketteki sürücüleri Windows 'a kullanılabilir hale getirin. **Sürücü Paketini Uygula** görev dizisi adımı ayrıca tek başına medya dağıtımı senaryolarında da yararlıdır.  

Benzer cihaz sürücülerini bir sürücü paketine yerleştirin ve bunları uygun dağıtım noktalarına dağıtın. Örneğin, bir üreticiden tüm sürücüleri bir sürücü paketine yerleştirin. Ardından, paketi ilişkili bilgisayarların erişebileceği dağıtım noktalarına dağıtın.

**Sürücü paketini Uygula** adımı, tek başına medya için faydalıdır. Bu adım, belirli bir sürücü kümesini yüklemek için de kullanışlıdır. Bu tür sürücüler, Windows Tak ve Çalıştır 'ın ağ yazıcıları gibi algılamadığı cihazları içerir.  

Bu görev dizisi adımı yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **sürücüler**' i seçin ve **sürücü paketini Uygula**' yı seçin.

> [!TIP]
> Configuration Manager sürücülerle ilgili bir genel bakış için bkz. [sürücüleri yüklemek için görev dizilerini kullanma](../get-started/manage-drivers.md#BKMK_TSDrivers).
>
> Kullanıcı görev dizisini yüklemeden önce geçerli bir sürücü paketini indirmek için içeriği önceden önbelleğe alma özelliğini kullanın. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../deploy-use/configure-precache-content.md).

### <a name="variables-for-apply-driver-package"></a>Sürücü paketini Uygula değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [Osdınstalldriversadditionaloptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>Sürücü paketini Uygula cmdlet 'leri

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage)
- [New-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage)
- [Remove-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage)
- [Set-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage)

### <a name="properties-for-apply-driver-package"></a>Sürücü paketi Uygula özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="driver-package"></a>Sürücü paketi

Gerekli cihaz sürücülerini içeren sürücü paketini belirtin. **Bir paket seçin** iletişim kutusunu başlatmak için **Araştır** ' ı seçin. Uygulanacak var olan bir sürücü paketini seçin. İletişim kutusunun alt kısmında ilişkili paket özellikleri görüntülenir.  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>Recurse seçeneği ile DıSM çalıştırmayı kullanarak sürücü paketini yükler

`/recurse`Windows sürücü paketini uygularken, PARAMETREYI DISM komut satırına eklemek için bu seçeneği belirleyin.

Bu seçeneği etkinleştirdiğinizde, ek DıSM komut satırı parametreleri de belirtebilirsiniz. Daha fazla seçenek dahil etmek için [Osdınstalldriversaddıtionaloptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) görev dizisi değişkenini kullanın. Daha fazla bilgi için bkz. [Windows 10 DISM komut satırı seçenekleri](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Paketin içinde Windows Vista'dan önceki işletim sistemlerinde kurulumdan önce yüklenmesi gereken yığın depolama sürücüsünü seçin

Klasik bir işletim sistemi yüklemek için gereken herhangi bir yığın depolama sürücüsünü belirtin.  

##### <a name="driver"></a>Sürücü

Klasik bir işletim sistemi kurulumundan önce yüklenecek yığın depolama sürücüsü dosyasını seçin. Açılan liste belirtilen paketten doldurulur.  

##### <a name="model"></a>Modelleme

Windows Vista 'Dan önceki işletim sistemi dağıtımları için gereken önyükleme için kritik cihazı belirtin.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>İzin verilen Windows sürümünde imzasız sürücülerin katılımsız yüklemesini yapın

Bu seçenek Windows 'un, dijital imza olmadan sürücü yüklemesini sağlar.  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> Ağ ayarlarını uygula  

Hedef bilgisayar için ağ veya çalışma grubu yapılandırma bilgilerini belirtmek üzere bu adımı kullanın. Görev sırası bu değerleri uygun yanıt dosyasında depolar. Windows Kurulumu, **Windows 'u ve ConfigMgr 'Yi Kur** eylemini sırasında bu yanıt dosyasını kullanır.  

Bu görev dizisi adımı yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Ayarlar**' ı seçin ve **ağ ayarlarını uygula**' yı seçin.

> [!NOTE]
> Bu adımın birden çok örneğini bir görev dizisine eklerseniz, koşullar uygulanmaz. Görev dizisindeki bu adımın son örneğindeki ayarlar cihaza uygulanır. Bu davranışı geçici olarak çözmek için, her adımı gruptaki koşullara sahip ayrı bir gruba dahil edin.

### <a name="variables-for-apply-network-settings"></a>Ağ ayarlarını uygula değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>Ağ ayarlarını uygula için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting)
- [New-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting)
- [Remove-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting)
- [Set-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting)

### <a name="properties-for-apply-network-settings"></a>Ağ ayarlarını uygula özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="join-a-workgroup"></a>Çalışma grubuna katıl

Hedef bilgisayarın belirtilen çalışma grubuna katılmasını sağlamak için bu seçeneği belirleyin. **Çalışma grubu** satırına çalışma grubunun adını girin. **Ağ ayarlarını yakala** görev dizisi adımının yakaladığı değer bu değeri geçersiz kılabilir.

#### <a name="join-a-domain"></a>Bir etki alanına katılma

Hedef bilgisayarın belirtilen etki alanına katılmasını sağlamak için bu seçeneği belirleyin. (Gibi) etki alanını belirtin veya gösterin `fabricam.com` . Bir kuruluş birimi için Basit Dizin Erişim Protokolü (LDAP) yolunu belirtin veya buraya gidin. Örneğin: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

> [!NOTE]
> Bir Azure Active Directory (Azure AD) ile Birleşik istemci bir işletim sistemi dağıtımı görev dizisi çalıştırdığında, yeni işletim sistemindeki istemci Azure AD 'ye otomatik olarak katılmayacaktır. Azure AD 'ye katılmış olmasa bile, istemci hala yönetilecektir.

#### <a name="account"></a>Hesap

Bilgisayarı etki alanına katmak için gerekli izinlere sahip bir hesap belirtmek üzere **Ayarla** ' yı seçin. **Windows Kullanıcı hesabı** iletişim kutusunda, Kullanıcı adını şu biçimde girin: `Domain\User` . Daha fazla bilgi için bkz. [etki alanına katılma hesabı](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

#### <a name="adapter-settings"></a>Bağdaştırıcı ayarları

Bilgisayardaki her ağ bağdaştırıcısı için ağ yapılandırmalarını belirtin. **Ağ ayarları** iletişim kutusunu açmak için **Yeni** ' yi seçin ve ardından ağ ayarlarını belirtin.

- **Ağ ayarlarını yakala** adımını da kullanıyorsanız, görev dizisi daha önce yakalanan ayarları ağ bağdaştırıcısına uygular.
- Görev sırası daha önce ağ ayarlarını yakalamadıysa, bu adımda belirttiğiniz ayarları uygular.
- Görev sırası, bu ayarları Windows cihaz numaralandırma sırasında ağ bağdaştırıcılarına uygular.  
- Görev sırası, bu adımda bilgisayar için belirttiğiniz ayarları hemen uygulamaz.



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Işletim sistemi görüntüsünü Uygula  

Hedef bilgisayara bir işletim sistemi yüklemek için bu adımı kullanın.

**Işletim sistemini Uygula** eylemi çalıştıktan sonra, **OSDTargetSystemDrive** değişkenini, işletim sistemi dosyalarını içeren bölümün sürücü harfine ayarlar.  

Bu görev dizisi adımı yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **görüntüler**' i seçin ve **işletim sistemi görüntüsünü Uygula**' yı seçin.

> [!TIP]
> Windows 10, sürüm 1709 ' den başlayarak, medya birden çok sürümünü içerir. Bir görev dizisini bir işletim sistemi yükseltme paketi veya işletim sistemi görüntüsü kullanacak şekilde yapılandırdığınızda, [desteklenen bir sürüm](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)seçtiğinizden emin olun.  
>
> Kullanıcı görev dizisini yüklemeden önce geçerli bir işletim sistemi yükseltme paketini indirmek için içeriği önceden önbelleğe alma özelliğini kullanın. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../deploy-use/configure-precache-content.md).
>
> **Windows 'u ve ConfigMgr 'Yi Kur** adımı Windows yüklemesini başlatır.

### <a name="variables-for-apply-os-image"></a>İşletim sistemi görüntüsü Uygula değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>İşletim sistemi görüntüsü Uygula cmdlet 'leri

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem)
- [New-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem)
- [Remove-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem)
- [Set-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem)

### <a name="behaviors-for-apply-os-image"></a>İşletim sistemi görüntüsü uygulama davranışları

Bu adım, bir işletim sistemi görüntüsü veya bir işletim sistemi yükseltme paketi kullanıp kullanmadığına bağlı olarak farklı eylemler gerçekleştirir.  

#### <a name="os-image-actions"></a>İşletim sistemi görüntüsü eylemleri

**Işletim sistemi görüntüsünü Uygula** adımı bir işletim sistemi görüntüsü kullanırken aşağıdaki eylemleri gerçekleştirir:  

1. ** \_ SMSTSUserStatePath** değişkeni tarafından belirtilen klasördeki dosyalar hariç, Hedeflenen birimdeki tüm içeriği silin.  

2. Belirtilen. wim dosyasının içeriğini belirtilen hedef bölüme ayıklayın.  

3. Yanıt dosyasını hazırlama:  

    1. Dağıtılan işletim sistemi için yeni bir varsayılan Windows Kurulumu yanıt dosyası (Sysprep. inf veya unattend.xml) oluşturun.  

    2. Kullanıcı tarafından sağlanan yanıt dosyasındaki tüm değerleri birleştirin.  

4. Windows önyükleme yükleyicilerini etkin bölüme kopyalayın.  

5. Yeni yüklenen işletim sistemine başvurmak için boot.ini veya önyükleme yapılandırma veritabanı 'nı (BCD) ayarlayın.  

#### <a name="os-upgrade-package-actions"></a>İşletim sistemi yükseltme paketi eylemleri

**Işletim sistemi görüntüsünü Uygula** adımı bir işletim sistemi yükseltme paketi kullanırken aşağıdaki eylemleri gerçekleştirir:  

1. ** \_ SMSTSUserStatePath** değişkeni tarafından belirtilen klasördeki dosyalar hariç, Hedeflenen birimdeki tüm içeriği silin.  

2. Yanıt dosyasını hazırlama:  

    1. Configuration Manager tarafından oluşturulan standart değerlerle yeni bir yanıt dosyası oluşturun.  

    2. Kullanıcı tarafından sağlanan yanıt dosyasındaki tüm değerleri birleştirin.  

### <a name="properties-for-apply-os-image"></a>İşletim sistemi görüntüsü Uygula özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="apply-operating-system-from-a-captured-image"></a>İşletim sistemini yakalanan görüntüden uygula

Yakalamakta olduğunuz bir işletim sistemi görüntüsünü kurar. **Bir paket seçin** iletişim kutusunu açmak için **Araştır** ' ı seçin. Ardından, yüklemek istediğiniz mevcut görüntü paketini seçin. Belirtilen **görüntü paketi**ile birden fazla görüntü ilişkiliyse, bu dağıtım için kullanılacak olan ilişkili görüntüyü aşağı açılan listeden seçin. Varolan her bir görüntüyle ilgili temel bilgileri seçerek görüntüleyebilirsiniz.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>İşletim sistemi görüntüsünü özgün bir yükleme kaynağından uygula

Bir işletim sistemi yükseltme paketi kullanarak bir işletim sistemi yükleme, aynı zamanda bir de özgün yükleme kaynağıdır. **Bir Işletim sistemi yükseltme paketi Seç** iletişim kutusunu açmak için **Araştır** ' ı seçin. Ardından, kullanmak istediğiniz var olan işletim sistemi yükseltme paketini seçin. Varolan her görüntü kaynağıyla ilgili temel bilgileri seçerek görüntüleyebilirsiniz. İletişim kutusunun alt kısmındaki sonuçlar bölmesi ilişkili görüntü kaynağı özelliklerini görüntüler. Belirtilen paketle ilişkili birden çok sürüm varsa, kullanmak istediğiniz **sürümü** seçmek için açılan listeyi kullanın.  

> [!NOTE]  
> **Işletim sistemi yükseltme paketleri** öncelikle Windows 'un yeni yüklemeleri için değil yerinde yükseltmelerde kullanılmak üzere tasarlanmıştır. Yeni Windows yüklemelerini dağıttığınızda, **yakalanan bir görüntüden işletim sistemini Uygula** seçeneğini kullanın ve yükleme kaynak dosyalarından **. wim** ' i yükleme.
>
> **Işletim sistemi yükseltme paketleri** aracılığıyla yeni Windows yüklemelerini dağıtmak hala desteklenmektedir, ancak bu yöntemle uyumlu olan sürücülere bağımlıdır. Windows 'u bir işletim sistemi yükseltme paketinden yüklerken, Windows PE 'de hala Windows PE sırasında eklenen sürücüler yüklenir. Bazı sürücüler Windows PE 'de çalışırken yüklenmekte uyumlu değildir.
>
> Sürücüler Windows PE 'de yüklenirken yüklü değilse, özgün yükleme kaynak dosyalarından **Install. wim** dosyasını Içeren bir **işletim sistemi görüntüsü** oluşturun. Bunun yerine, **yakalanan bir görüntüden işletim sistemini Uygula** seçeneğini kullanarak dağıtın.

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Özel bir yükleme için katılımsız veya sysprep yanıt dosyası kullanın

İşletim sistemi sürümüne ve yükleme yöntemine bağlı olarak bir Windows kurulumu yanıt dosyası (**unattend.xml**, **unattend.txt**veya **Sysprep. inf**) sağlamak için bu seçeneği kullanın. Belirttiğiniz dosya Windows yanıt dosyaları tarafından desteklenen standart yapılandırma seçeneklerinden herhangi birini içerebilir. Örneğin, varsayılan Internet Explorer giriş sayfasını belirtmek için kullanabilirsiniz. Yanıt dosyasını içeren paketi ve paketteki dosyanın ilişkili yolunu belirtin.  

> [!NOTE]  
> Sağladığınız Windows kurulumu yanıt dosyası, formun gömülü görev dizisi değişkenleri içerebilir `%varname%` , burada *varname* değişkenin adıdır. **Windows 'u ve ConfigMgr 'Yi Kur** adımı, değişkenin gerçek değeri için değişken dize kullanır. Bu katıştırılmış görev dizisi değişkenlerini unattend.xml yanıt dosyasındaki yalnızca sayısal alanlarda kullanamazsınız.  

Bir Windows kurulumu yanıt dosyası belirtmezseniz, görev sırası otomatik olarak bir yanıt dosyası oluşturur.  

#### <a name="destination"></a>Hedef

Aşağıdaki seçeneklerden birini yapılandırın:  

- **Sonraki kullanılabilir bölüm**: Bu görev dizisinde, bir **işletim sistemini Uygula** veya **veri görüntüsünü Uygula** adımı tarafından henüz hedeflenmedi bir sonraki sıralı bölümü kullanın.  

- **Belirli disk ve bölüm**: **disk** numarasını (0 ' dan başlayarak) ve **bölüm** numarasını (1 ' den başlayarak) seçin.  

- **Belirli mantıksal sürücü harfi**: Windows PE tarafından bölüme atanan **sürücü harfini** belirtin. Bu sürücü harfi, yeni dağıtılan işletim sistemi tarafından atanan sürücü harfinden farklı olabilir.  

- **Bir değişkende depolanan mantıksal sürücü harfi**: Windows PE tarafından bölüme atanan sürücü harfini içeren görev dizisi değişkenini belirtin. Bu değişken genellikle **Diski Biçimlendir ve bölümle disk** sırası adımı Için **bölüm özellikleri** iletişim kutusunun Gelişmiş bölümünde ayarlanır.  

### <a name="options-for-apply-os-image"></a>İşletim sistemi görüntüsü uygulama seçenekleri

Varsayılan seçeneklerin yanı sıra, bu görev dizisi adımının **Seçenekler** sekmesinde aşağıdaki ek ayarları yapılandırın:  

#### <a name="access-content-directly-from-the-distribution-point"></a>İçeriğe doğrudan dağıtım noktasından erişin

Görev sırasını, işletim sistemi görüntüsüne doğrudan dağıtım noktasından erişecek şekilde yapılandırın. Örneğin, sınırlı depolama kapasitesine sahip katıştırılmış cihazlara işletim sistemi dağıtırken bu seçeneği kullanın. Bu seçeneği belirlediğinizde, işletim sistemi görüntüsü özelliklerinin **veri erişimi** sekmesinde paket paylaşma ayarlarını da yapılandırın.  

> [!NOTE]  
> Bu ayar, **Yazılım Dağıtma Sihirbazı**'Ndaki **dağıtım noktaları** sayfasında yapılandırdığınız dağıtım seçeneğini geçersiz kılar. Bu geçersiz kılma yalnızca bu adımın belirttiği işletim sistemi görüntüsü için, tüm görev sırası içerikleri için değildir.  

> [!IMPORTANT]  
> En yüksek güvenlik için, bu seçeneği seçmemelidir kesinlikle önerilir. Bu seçenek, genellikle sınırlı depolama kapasitesine sahip cihazlarda kullanılmak üzere tasarlanmıştır. Bu seçenek, görev dizisinin hızını artırmaya yardımcı olmak için tasarlanmamıştır. Bu seçenek belirlendiğinde, işletim sistemi paketi için paket karması doğrulanmaz. Bu nedenle, yönetici haklarına sahip kullanıcıların paket içeriğiyle değişiklik yapmak veya onu değiştirmesine izin vermek mümkün olduğundan, paket bütünlüğü uygun olamaz.



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Windows ayarlarını uygula

Hedef bilgisayar için Windows ayarlarını yapılandırmak üzere bu adımı kullanın. Görev sırası bu değerleri uygun yanıt dosyasında depolar. Windows Kurulumu, **Windows 'u ve ConfigMgr 'Yi Kur** adımı sırasında bu yanıt dosyasını kullanır.  

Bu görev dizisi adımı yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Ayarlar**' ı seçin ve **Windows ayarlarını uygula**' yı seçin.

### <a name="variables-for-apply-windows-settings"></a>Windows ayarlarını uygula değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [Osdwindowssettingsınputlocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Windows ayarlarını uygula için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-Cmtsstepapplywindowsayarı](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [New-Cmtsstepapplywindowsayarı](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [Remove-Cmtsstepapplywindowsayarı](/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting)
- [Set-Cmtsstepapplywindowsayarı](/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting)

### <a name="properties-for-apply-windows-settings"></a>Windows ayarlarını uygula özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="user-name"></a>Kullanıcı adı

Hedef bilgisayarla ilişkilendirilecek kayıtlı Kullanıcı adını belirtin. **Windows ayarlarını yakala** görev dizisi adımının yakaladığı değer bu değeri geçersiz kılabilir.  

#### <a name="organization-name"></a>Kuruluş adı

Hedef bilgisayarla ilişkilendirilecek kayıtlı kuruluş adını belirtin. **Windows ayarlarını yakala** görev dizisi adımının yakaladığı değer bu değeri geçersiz kılabilir.  

#### <a name="product-key"></a>Ürün anahtarı  

Hedef bilgisayardaki Windows yüklemesi için kullanılacak ürün anahtarını belirtin.  

#### <a name="server-licensing"></a>Sunucu lisanslama

Sunucu lisanslama modunu belirtin.

- Lisans modu olarak **sunucu başına** veya **Kullanıcı başına** ' yı seçin.  
- **Sunucu başına**' yı seçerseniz, lisans sözleşmeniz uyarınca izin verilen en fazla bağlantı sayısını da belirtin.  
- Hedef bilgisayar bir sunucu değilse veya lisanslama modunu belirtmek istemiyorsanız, **belirtme**' yi seçin.  

#### <a name="maximum-connections"></a>En fazla bağlantı sayısı

> [!NOTE]
> Bu ayar yalnızca artık desteklenmeyen eski Windows sürümleri için geçerlidir.<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Yerel yönetici parolasını rastgele oluşturun ve tüm desteklenen platformlarda hesabı devre dışı bırakın (önerilir)  

Yerel yönetici parolasını rastgele oluşturulmuş bir dizeye ayarlamak için bu seçeneği belirleyin. Bu seçenek ayrıca, bu özelliği destekleyen platformlarda yerel yönetici hesabını devre dışı bırakır.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Hesabı etkinleştirin ve yerel yönetici parolasını belirtin  

Yerel yönetici hesabını belirtilen parolayı kullanarak etkinleştirmek için bu seçeneği belirleyin. Parolayı **Parola** satırına girin ve **Parolayı onayla** satırında onaylayın.  

#### <a name="time-zone"></a>Saat dilimi

Hedef bilgisayarda yapılandırılacak saat dilimini belirtin. **Windows ayarlarını yakala** görev dizisi adımının yakaladığı değer bu değeri geçersiz kılabilir.  

#### <a name="language-settings"></a>Dil ayarları

<!--5411057, 5138936-->

Sürüm 1910 ' den başlayarak, işletim sistemi dağıtımı sırasında dil yapılandırmasını denetleyin. Bu dil ayarlarını zaten uyguluyorsanız, bu değişiklik işletim sistemi dağıtımı görev dizinizi basitleştirmenize yardımcı olabilir. Her dil veya ayrı komut dosyası başına birden çok adım kullanmak yerine, bu adımın dil başına bir örnek kullanın ve bu dilin bir koşulu vardır.

Aşağıdaki ayarları yapılandırın:

- Giriş yerel ayarı (varsayılan klavye düzeni)
- Sistem yerel ayarı
- Kullanıcı arabirimi dili
- Kullanıcı arabirimi dili geri dönüş
- Kullanıcı yerel ayarı

Bu Windows kurulumu yanıt dosyası değerleri hakkında daha fazla bilgi için bkz. [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

> [!NOTE]
> Özel bir Windows kurulumu yanıt dosyası (unattend.xml) oluşturursanız, bu adım varolan değerlerin üzerine yazar. Bu ayarlar için dinamik bir işlemi otomatik hale getirmek üzere ilgili görev dizisi değişkenlerini kullanın. Örneğin, [Osdwindowssettingsınputlocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale). 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Sürücüleri otomatik olarak Uygula

Sürücüleri işletim sistemi dağıtımının bir parçası olarak eşleştirmek ve yüklemek için bu adımı kullanın.  

> [!IMPORTANT]  
> Tek başına medya, **sürücüleri otomatik olarak Uygula** adımını kullanamaz. Görev dizisinin Bu senaryodaki Configuration Manager sitesiyle bağlantısı yok.  

Bu görev dizisi adımı yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **sürücüler**' i seçin ve **sürücüleri otomatik olarak Uygula**' yı seçin.

> [!TIP]
> Configuration Manager sürücülere genel bir bakış için bkz. [sürücüleri yüklemek için görev dizilerini kullanma](../get-started/manage-drivers.md#BKMK_TSDrivers).

### <a name="behaviors-for-auto-apply-drivers"></a>Sürücüleri otomatik olarak Uygula davranışları

**Sürücüleri Otomatik Olarak Uygula** görev dizisi adımı aşağıdaki eylemleri gerçekleştirir:  

1. Donanımı tarayın ve sistemde bulunan tüm cihazlar için Tak ve Çalıştır kimliklerini bulun.  

2. Cihazların listesini ve bunların Tak ve Çalıştır kimliklerini yönetim noktasına gönderin. Yönetim noktası, her donanım cihazının sürücü kataloğundan uyumlu sürücülerin listesini döndürür. Liste, hangi sürücü paketine sahip olduklarına ve belirtilen sürücü kategorisiyle etiketlenmiş sürücülerle bağımsız olarak etkinleştirilmiş tüm sürücüleri içerir.  

3. Her donanım aygıtı için, görev sırası en iyi sürücüyü seçer. Bu sürücü, dağıtılan işletim sistemi için uygundur ve erişilebilir bir dağıtım noktasıdır.  

4. Görev sırası, seçilen sürücüleri bir dağıtım noktasından indirir ve hedef işletim sisteminde sürücüleri aşamalar.  

    1. Bir işletim sistemi görüntüsü kullanırken, görev sırası sürücüleri işletim sistemi sürücü deposuna koyar.  

    2. Bir işletim sistemi yükseltme paketini özgün yükleme kaynağı olarak kullanırken, görev sırası, sürücülerin konumuyla Windows Kurulumu yapılandırır.  

5. Görev dizisinde **Windows 'u ve ConfigMgr 'Yi Kur** adımı sırasında Windows kurulumu, bu adım tarafından hazırlanan sürücüleri bulur.  

### <a name="variables-for-auto-apply-drivers"></a>Sürücüleri otomatik olarak Uygula değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>Sürücüleri otomatik olarak Uygula cmdlet 'leri

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver)
- [New-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver)
- [Remove-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver)
- [Set-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver)

### <a name="properties-for-auto-apply-drivers"></a>Sürücüleri otomatik olarak Uygula özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Yalnızca en iyi eşleşen uyumlu sürücüleri yükleyin

Görev dizisi adımının algılanan her cihaz için yalnızca en iyi eşleşen sürücüyü yükleyeceğini belirtir.  

#### <a name="install-all-compatible-drivers"></a>Uyumlu tüm sürücüleri yükleyin

Görev sırası, algılanan her bir donanım aygıtı için uyumlu tüm sürücüleri kurar. Windows Kurulumu sonra en iyi sürücüyü seçer. Bu seçenek, daha fazla ağ bant genişliği ve disk alanı alır. Görev sırası daha fazla sürücü indirir, ancak Windows daha iyi bir sürücü seçebilir.  

#### <a name="consider-drivers-from-all-categories"></a>Tüm kategorilerden sürücüleri düşünün

Görev sırası, uygun cihaz sürücüleri için kullanılabilir tüm sürücü kategorilerini arar.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Eşleşmeyi yalnızca seçili kategorilerdeki sürücülerle sınırla

Görev sırası, uygun cihaz sürücüleri için belirtilen sürücü kategorilerini arar.  

Birden çok kategori seçerseniz, kategorilerin hiçbirinde bulunan tüm eşleşen sürücüleri döndürür. Bir `OR` işleme eşdeğerdir.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>İzin verilen Windows sürümlerinde imzasız sürücülerin katılımsız yüklemesini yapın

Bu seçenek Windows 'un, dijital imza olmadan sürücü yüklemesini sağlar.  

> [!IMPORTANT]  
> Bu seçenek, sürücü imzalama ilkesini yapılandırabileceğiniz işletim sistemlerine uygulanmaz.  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Ağ ayarlarını yakala

Görev sırasını çalıştıran bilgisayardan Microsoft ağ ayarlarını yakalamak için bu adımı kullanın. Görev sırası bu ayarları görev dizisi değişkenlerine kaydeder. Bu ayarlar, **ağ ayarlarını uygula** adımında yapılandırdığınız varsayılan ayarları geçersiz kılar.  

Bu görev dizisi adımı yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Ayarlar**' ı seçin ve **ağ ayarlarını yakala**' yı seçin.

### <a name="variables-for-capture-network-settings"></a>Yakalama ağ ayarları için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>Yakalama ağ ayarları için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings)
- [New-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings)
- [Remove-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings)
- [Set-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings)

### <a name="properties-for-capture-network-settings"></a>Yakalama ağ ayarları özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Etki alanı ve çalışma grubu üyeliğini taşıma

Hedef bilgisayarın etki alanı ve çalışma grubu üyelik bilgilerini yakalar.  

#### <a name="migrate-network-adapter-configuration"></a>Taşıma ağ bağdaştırıcısı yapılandırması

Hedef bilgisayarın ağ bağdaştırıcısı yapılandırmasını yakalar. Aşağıdaki bilgileri yakalar:

- Genel ağ ayarları  
- Bağdaştırıcı sayısı  
- Her bağdaştırıcı ile ilişkili aşağıdaki ağ ayarları: DNS, WINS, IP ve bağlantı noktası filtreleri



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Işletim sistemi görüntüsünü yakala

Bu adım, bir başvuru bilgisayarından bir veya daha fazla görüntü yakalar. Görev sırası, belirtilen ağ paylaşımında bir Windows görüntü (. wim) dosyası oluşturur. Ardından bu görüntüyü görüntü tabanlı IŞLETIM sistemi dağıtımları için Configuration Manager içine aktarmak üzere **Işletim sistemi görüntü paketi ekleme** Sihirbazı 'nı kullanın.  

Configuration Manager, başvuru bilgisayarından her birimi (sürücü). wim dosyası içinde ayrı bir görüntüye yakalar. Başvurulan bilgisayarda birden çok birim varsa, elde edilen. wim dosyası her birim için ayrı bir görüntü içerir. Bu adım yalnızca NTFS veya FAT32 olarak biçimlendirilen birimleri yakalar. Diğer biçimlere ve USB birimlerine sahip birimleri atlar.  

Başvuru bilgisayarında yüklü işletim sistemi, Configuration Manager desteklediği bir Windows sürümü olmalıdır. İşletim sistemini başvuru bilgisayarında hazırlamak için SysPrep aracını kullanın. Yüklü işletim sistemi birimi ve önyükleme biriminin aynı birim olması gerekir.  

Seçili ağ paylaşımında yazma izinlerine sahip bir hesap belirtin. İşletim sistemi görüntüsü Yakala hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

Bu görev dizisi adımı yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **görüntüler**' i seçin ve **işletim sistemi görüntüsünü yakala**' yı seçin.

### <a name="variables-for-capture-os-image"></a>İşletim sistemi görüntüsü yakalama değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>İşletim sistemi görüntüsü yakalama için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-Cmtsstepcapturessystemutility Mımage](/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage)
- [New-Cmtsstepcapturessystemutility Mımage](/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage)
- [Remove-Cmtsstepcapturessystemutility Mımage](/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage)
- [Set-Cmtsstepcapturessystemutility Mımage](/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage)

### <a name="properties-for-capture-os-image"></a>İşletim sistemi görüntüsü yakalama özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="target"></a>Hedef  

Yakalanan işletim sistemi görüntüsünü depolarken Configuration Manager kullandığı konumun dosya sistemi yolu.  

#### <a name="description"></a>Description  

Yansıma dosyasında depolanan yakalanan işletim sistemi görüntüsünün isteğe bağlı kullanıcı tanımlı bir açıklaması.  

#### <a name="version"></a>Sürüm  

Yakalanan işletim sistemi görüntüsüne atanacak, Kullanıcı tanımlı isteğe bağlı bir sürüm numarası. Bu değer, harflerin ve sayıların herhangi bir birleşimi olabilir. Görüntü dosyasında depolanır.  

#### <a name="created-by"></a>Oluşturan:  

İşletim sistemi görüntüsünü oluşturan kullanıcının isteğe bağlı adı. Görüntü dosyasında depolanır.  

#### <a name="capture-operating-system-image-account"></a>İşletim sistemi görüntüsü yakalama hesabı  

Belirtilen ağ paylaşımıyla ilgili izinlere sahip Windows hesabını girin. Windows hesabının adını belirtmek için **Ayarla** ' yı seçin.  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Kullanıcı durumunu yakala

Bu adım, görev dizisini çalıştıran bilgisayardan Kullanıcı durumu ve ayarlarını yakalamak için Kullanıcı Durumu Taşıma Aracı (USMT) kullanır. Bu görev dizisi adımı **Kullanıcı Durumunu Geri Yükle** görev dizisi adımıyla birlikte kullanılır. Bu adım, Configuration Manager oluşturup yöneten bir şifreleme anahtarı kullanarak USMT durum deposunu her zaman şifreler.  

İşletim sistemlerini dağıttığınızda kullanıcı durumunu yönetme hakkında daha fazla bilgi için bkz. [Manage user State](../get-started/manage-user-state.md).  

Kullanıcı durumu ayarlarını bir durum geçiş noktasından kaydetmek ve geri yüklemek istiyorsanız, bu adımı **durum depolama iste** ve **durum depolamayı serbest bırak** adımları ile birlikte kullanın.  

Bu adım, en sık kullanılan USMT seçeneklerinin sınırlı bir alt kümesinde denetim sağlar. **OSDMigrateAdditionalCaptureOptions** görev dizisi değişkenini kullanarak ek komut satırı seçeneklerini belirtin.  

Bu görev dizisi adımı yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Kullanıcı durumu**' nu seçin ve **Kullanıcı durumunu yakala**' yı seçin.

### <a name="variables-for-capture-user-state"></a>Yakalama Kullanıcı durumu değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>Yakalama Kullanıcı durumu için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState)
- [New-CMTSStepCaptureUserState](/powershell/module/configurationmanager/New-CMTSStepCaptureUserState)
- [Remove-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState)
- [Set-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState)

### <a name="properties-for-capture-user-state"></a>Kullanıcı durumunu yakala özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="user-state-migration-tool-package"></a>Kullanıcı durumu taşıma aracı paketi

Kullanıcı Durumu Taşıma Aracı (USMT) içeren paketi belirtin. Görev sırası, Kullanıcı durumunu ve ayarlarını yakalamak için USMT 'nin bu sürümünü kullanır. Bu paket bir program gerektirmez. USMT 'nin 32-bit veya 64 bit sürümünü içeren bir paket belirtin. USMT mimarisi, görev dizisinin yakaladığı işletim sisteminin mimarisine bağlıdır.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Standart seçeneklerle tüm kullanıcı profillerini yakalama

Tüm Kullanıcı profili bilgilerini geçirin. Bu seçenek varsayılandır.  

Bu seçeneği belirlerseniz ancak **Kullanıcı durumunu geri yükle** adımında **Yerel bilgisayar kullanıcı profillerini geri yükle** ' yi seçmezseniz görev sırası başarısız olur. Configuration Manager, yeni hesapları parola atamadan geçiremez.

**Yeni görev dizisi** Sihirbazı 'nın **var olan bir görüntü paketini Kur** seçeneğini kullandığınızda, sonuçta elde edilen görev sırası varsayılan olarak **tüm Kullanıcı profillerini standart seçeneklerle yakalar**. Bu varsayılan görev sırası, **Yerel bilgisayar kullanıcı profillerini**veya etki alanı olmayan kullanıcı hesaplarını geri yükleme seçeneğini seçmeyin.  

**Yerel bilgisayar kullanıcı profillerini geri yükle** ' yi seçin ve geçirilecek hesap için bir parola sağlayın. Elle oluşturulan bir görev dizisinde, bu ayar **Kullanıcı durumunu geri yükle** adımı altında bulunur. **Yeni Görev Dizisi** sihirbazı tarafından oluşturulan bir görev dizisinde, bu ayar **Kullanıcı Dosyaları ve Ayarlarını Geri Yükle** sihirbaz sayfasında bulunur.  

Yerel Kullanıcı hesabınız yoksa, bu ayar uygulanmaz.  

#### <a name="customize-how-user-profiles-are-captured"></a>Kullanıcı profillerinin nasıl yakalandığını özelleştirin

Geçiş için özel bir profil dosyası belirtmek üzere bu seçeneği belirleyin. USMT 'nin bu adımla kullanacağı yapılandırma dosyalarını seçmek için **dosyalar** ' ı seçin. Geçirilecek Kullanıcı durum dosyalarını tanımlayan kuralları içeren özel bir. xml dosyası belirtin.  

#### <a name="click-here-to-select-configuration-files"></a>Yapılandırma dosyalarını seçmek için buraya tıklayın

Kullanıcı profillerini yakalamak için kullanmak istediğiniz USMT paketindeki yapılandırma dosyalarını seçmek için bu seçeneği belirleyin. **Yapılandırma dosyaları** iletişim kutusunu başlatmak için **dosyalar** düğmesini seçin. Bir yapılandırma dosyası belirtmek **için dosya adı satırına dosyanın** adını girin ve **Ekle** düğmesini seçin.  

#### <a name="enable-verbose-logging"></a>Ayrıntılı günlük kaydını etkinleştir

Daha ayrıntılı günlük dosyası bilgileri oluşturmak için bu seçeneği etkinleştirin. Durum yakalarken, görev sırası varsayılan olarak görev dizisi günlük klasöründe **Scanstate. log** ' u oluşturur `%WinDir%\ccm\logs` .  

#### <a name="skip-files-using-encrypted-file-system"></a>Şifrelenmiş dosya sistemi kullanan dosyaları atla

Şifrelenmiş dosya sistemi (EFS) ile şifrelenmiş dosyaların yakalanmasını atlamak için bu seçeneği etkinleştirin. Bu dosyalar, Kullanıcı profili dosyalarını içerir. İşletim sistemi ve USMT sürümlerine bağlı olarak, şifrelenmiş dosyalar geri yüklendikten sonra okunabilir olmayabilir. Daha fazla bilgi için USMT belgelerine bakın.  

#### <a name="copy-by-using-file-system-access"></a>Dosya sistemi erişimini kullanarak kopyalayın

Aşağıdaki ayarlarından herhangi birini belirtmek için bu seçeneği etkinleştirin:  

- **Bazı dosyalar yakalanamazsa devam et**: bazı dosyaları yakalamasa bile geçiş işlemine devam etmek için bu ayarı etkinleştirin. Bu seçeneği devre dışı bırakırsanız ve bir dosya yakalanamazsa, bu adım başarısız olur. Bu seçenek varsayılan olarak etkindir.  

- **Dosyaları kopyalamak yerine bağlantıları kullanarak yerel olarak yakala**: Dosyaları yakalamak için NTFS sabit bağlantılarını kullanmak üzere bu ayarı etkinleştirin.  

    Sabit bağlantılar kullanarak verileri geçirme hakkında daha fazla bilgi için bkz. [sabit bağlantı geçiş deposu](/windows/deployment/usmt/usmt-hard-link-migration-store).  

- **Çevrimdışı modda yakala (yalnızca WINDOWS PE)**: Bu ayarı, Windows PE 'de tüm işletim sistemi yerine Kullanıcı durumunu yakalamak için etkinleştirin.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Birim Gölge Kopyası Hizmeti'ni (VSS) Kullanarak Yakalama

Bu seçenek, dosyaları başka bir uygulama tarafından düzenlenmek üzere kilitlenseler bile yakalamanızı sağlar.  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Windows ayarlarını yakala

Görev sırasını çalıştıran bilgisayardan Windows ayarlarını yakalamak için bu adımı kullanın. Görev sırası bu ayarları görev dizisi değişkenlerine kaydeder. Yakalanan bu ayarlar **Windows ayarlarını uygula** adımında yapılandırdığınız varsayılan ayarları geçersiz kılar.  

Bu görev dizisi adımı, Windows PE 'de veya tam işletim sisteminde çalışır.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Ayarlar**' ı seçin ve **Windows ayarlarını yakala**' yı seçin.

### <a name="variables-for-capture-windows-settings"></a>Yakalama Windows ayarları için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Yakalama Windows ayarları için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings)
- [New-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings)
- [Remove-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings)
- [Set-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings)

### <a name="properties-for-capture-windows-settings"></a>Yakalama Windows ayarları özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="migrate-computer-name"></a>Bilgisayar adını taşıma

Bilgisayarın NetBIOS bilgisayar adını yakalayın.  

#### <a name="migrate-registered-user-and-organization-names"></a>Kayıtlı kullanıcı ve kuruluş adlarını taşıma

Kayıtlı Kullanıcı ve kuruluş adlarını bilgisayardan yakalayın.  

#### <a name="migrate-time-zone"></a>Saat dilimini taşıma

Bilgisayardaki saat dilimi ayarını yakalayın.  


## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> Hazır olma durumunu denetle

Hedef bilgisayarın belirtilen dağıtım önkoşul koşullarını karşıladığını doğrulamak için bu adımı kullanın.  

Bu adımı görev sırası düzenleyicisine eklemek için, **Ekle**' yi seçin, **genel**' i seçin ve **hazırlığı denetle**' yi seçin.

Sürüm 2002 ' den başlayarak, bu adım sekiz yeni denetim içerir. Bu yeni denetimlerden hiçbiri, adımın yeni veya var olan örneklerinde varsayılan olarak seçili değildir.<!--6005561--> Her denetim hakkında daha fazla bilgi için aşağıdaki belirli bölümlere bakın.

- **Geçerli işletim sisteminin mimarisi**
- **En düşük işletim sistemi sürümü**
- **En yüksek işletim sistemi sürümü**
- **En düşük istemci sürümü**
- **Geçerli işletim sisteminin dili**
- **AC güç takıldı**
- **Ağ bağdaştırıcısı bağlı**
  - **Ağ bağdaştırıcısı kablosuz değil**

Sürüm 2006 ' den başlayarak bu adım, cihazın UEFı kullanıp kullanmadığını, **BILGISAYARıN UEFI modunda**olup olmadığını belirlemede bir denetim içerir.<!--6452769-->

> [!IMPORTANT]
> Bu yeni Configuration Manager özelliğinden yararlanmak için, siteyi güncelleştirdikten sonra da istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

**Smsts. log** tüm denetimlerin sonucunu içerir. Bir denetim başarısız olursa, görev dizisi altyapısı diğer denetimleri değerlendirmeye devam eder. Tüm denetimler tamamlanana kadar adım başarısız olmaz. En az bir denetim başarısız olursa, adım başarısız olur ve **4316**hata kodunu döndürür. Bu hata kodu, "Bu işlem için gereken kaynak yok" olarak çevrilir.

### <a name="variables-for-check-readiness"></a>Kullanıma hazır olma değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH) (2002 sürümünden başlayarak)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER) (2002 sürümünden başlayarak)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER) (2002 sürümünden başlayarak)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER) (2002 sürümünden başlayarak)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE) (2002 sürümünden başlayarak)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER) (2002 sürümünden başlayarak)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK) (2002 sürümünden başlayarak)
- [_TS_CRUEFI](task-sequence-variables.md#TSCRUEFI) (2006 sürümünden başlayarak)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED) (2002 sürümünden başlayarak)

### <a name="cmdlets-for-check-readiness"></a>Kullanıma hazır olma için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck)
- [New-CMTSStepPrestartCheck](/powershell/module/configurationmanager/New-CMTSStepPrestartCheck)
- [Remove-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck)
- [Set-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck)

### <a name="properties-for-check-readiness"></a>Kullanıma hazır olma özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="minimum-memory-mb"></a>Minimum bellek (MB)

Megabayt (MB) cinsinden bellek miktarının belirtilen miktarı karşıladığını veya aştığından emin olun. Adım bu ayarı varsayılan olarak sunar.  

#### <a name="minimum-processor-speed-mhz"></a>En düşük işlemci hızı (MHz)  

İşlemci hızının megahertz (MHz) cinsinden belirtilen miktarı karşıladığını veya aşmadığını doğrulayın. Adım bu ayarı varsayılan olarak sunar.  

#### <a name="minimum-free-disk-space-mb"></a>Minimum boş disk alanı (MB)

Megabayt (MB) cinsinden boş disk alanı miktarının belirtilen miktarı karşıladığını veya aştığından emin olun.  

#### <a name="current-os-to-be-refreshed-is"></a>Yenilenecek geçerli işletim sistemi

Hedef bilgisayarda yüklü olan işletim sisteminin belirtilen gereksinimi karşıladığını doğrulayın. Adımı varsayılan olarak bu ayarı **istemci** olarak ayarlar.  

#### <a name="architecture-of-current-os"></a>Geçerli işletim sisteminin mimarisi

Sürüm 2002 ' den başlayarak, geçerli işletim sisteminin **32 bit** mi yoksa **64-bit**mi olduğunu doğrulayın.

#### <a name="minimum-os-version"></a>En düşük işletim sistemi sürümü

Sürüm 2002 ' den başlayarak, geçerli işletim sisteminin belirtilen sürümden daha sonraki bir sürümü çalıştırdığından emin olun. Birincil sürüm, ikincil sürüm ve derleme numarası ile sürümü belirtin. Örneğin, `10.0.16299`.

#### <a name="maximum-os-version"></a>En yüksek işletim sistemi sürümü

Sürüm 2002 ' den başlayarak, geçerli işletim sisteminin belirtilen sürümden önceki bir sürümü çalıştırdığından emin olun. Birincil sürüm, ikincil sürüm ve derleme numarası ile sürümü belirtin. Örneğin, `10.0.18356`.

#### <a name="minimum-client-version"></a>En düşük istemci sürümü

Sürüm 2002 ' den başlayarak, Configuration Manager istemci sürümünün en azından belirtilen sürüme sahip olduğunu doğrulayın. İstemci sürümünü şu biçimde belirtin: `5.00.8913.1005` .

#### <a name="language-of-current-os"></a>Geçerli işletim sisteminin dili

Sürüm 2002 ' den başlayarak, geçerli işletim sistemi dilinin belirttiğiniz şekilde eşleştiğini doğrulayın. Dil adını seçin ve adım ilişkili dil kodunu karşılaştırır. Bu denetim, seçtiğiniz dili istemcisinde **Win32_OperatingSystem** WMI sınıfının **OSLanguage** özelliği ile karşılaştırır.

#### <a name="ac-power-plugged-in"></a>AC güç takıldı

Sürüm 2002 ' den başlayarak, cihazın takılı olduğundan ve pilde olmadığından emin olun.

#### <a name="network-adapter-connected"></a>Ağ bağdaştırıcısı bağlı

Sürüm 2002 ' den başlayarak, cihazın ağa bağlı bir ağ bağdaştırıcısı olduğunu doğrulayın. Ayrıca, **ağ bağdaştırıcısının kablosuz**olmadığını doğrulamak için bağımlı denetimi de seçebilirsiniz.

#### <a name="computer-is-in-uefi-mode"></a>Bilgisayar, UEFı modunda

Sürüm 2006 ' den başlayarak, cihazın UEFı veya BIOS için yapılandırılmış olup olmadığını saptayın.

### <a name="options-for-check-readiness"></a>Kullanıma hazır olma seçenekleri

> [!NOTE]  
> Bu adımın **Seçenekler** sekmesinde **hata durumunda devam et** ayarını etkinleştirirseniz, yalnızca hazırlık denetimi sonuçlarını günlüğe kaydeder. Bir denetim başarısız olursa, görev sırası durdurulur.  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Ağ klasörüne Bağlan

Paylaşılan bir ağ klasörüne bağlantı oluşturmak için bu adımı kullanın.  

Bu görev dizisi adımı, tam işletim sisteminde veya Windows PE 'de çalışır.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **ağ klasörüne Bağlan**' ı seçin.

### <a name="variables-for-connect-to-network-folder"></a>Ağ klasörüne Bağlan değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>Ağ klasörüne Bağlan için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder)
- [New-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder)
- [Remove-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder)
- [Set-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder)

### <a name="properties-for-connect-to-network-folder"></a>Ağ klasörüne Bağlan özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="path"></a>Yol  

Ağ klasörü yolunu belirtmek için **Araştır** ' ı seçin. `\\server\share` biçimini kullanın.

#### <a name="drive"></a>Sürücü  

Bu bağlantı için atanacak yerel sürücü harfini seçin.

#### <a name="account"></a>Hesap

Bu ağ klasörüne bağlanma izinlerine sahip kullanıcı hesabını belirtmek için **Ayarla** ' yı seçin. Görev dizisi ağ klasörü bağlantı hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> BitLocker 'ı devre dışı bırak

Geçerli işletim sistemi sürücüsünde veya belirli bir sürücüde BitLocker şifrelemesini devre dışı bırakmak için bu adımı kullanın. Bu eylem, anahtar koruyucularını sabit sürücüdeki şifresiz metinde görünür bırakır. Sürücü içeriğinin şifresini çözmez. Bu eylem neredeyse anında tamamlanır.  

> [!NOTE]  
> BitLocker sürücü şifrelemesi disk birimi içeriği için alt düzey şifreleme sağlar.  

Birden çok şifrelenmiş sürücünüz varsa, işletim sistemi sürücüsünde BitLocker 'ı devre dışı bırakmadan önce tüm veri sürücülerinde BitLocker 'ı devre dışı bırakın.  

Bu adım yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **diskler**' i seçin ve **BitLocker 'ı devre dışı bırak**' ı seçin.

### <a name="variables-for-disable-bitlocker"></a>BitLocker 'ı devre dışı bırakma değişkenleri

Sürüm 1906 ' den başlayarak, aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>BitLocker 'ı devre dışı bırakma cmdlet 'leri

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker)
- [New-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker)
- [Remove-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker)
- [Set-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker)

### <a name="properties-for-disable-bitlocker"></a>BitLocker 'ı devre dışı bırakma özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="current-operating-system-drive"></a>Geçerli işletim sistemi sürücüsü

Geçerli işletim sistemi sürücüsünde BitLocker 'ı devre dışı bırakır.  

#### <a name="specific-drive"></a>Belirli sürücü  

BitLocker'ı belirli bir sürücüde devre dışı bırakır. BitLocker'ın devre dışı bırakılacağı sürücüyü belirtmek için açılır listeyi kullanın.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>Windows belirtilen sayıda yeniden başlatıldıktan sonra korumayı sürdürür

<!-- 4512937 -->
Sürüm 1906 ' den başlayarak, BitLocker 'ı devre dışı bırakmak için yeniden başlatma sayısını belirtmek üzere bu seçeneği kullanın. Bu adımın birden fazla örneğini eklemek yerine 1 (varsayılan) ve 15 arasında bir değer ayarlayın.

Bu davranışı, [Osdbitlockerrebootcount](task-sequence-variables.md#OSDBitLockerRebootCount) ve [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)görev dizisi değişkenleriyle ayarlayabilir ve değiştirebilirsiniz.


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Paket Içeriğini indir

Aşağıdaki paket türlerinden birini indirmek için bu adımı kullanın:  

- İşletim sistemi görüntüleri  
- İşletim sistemi yükseltme paketleri  
- Sürücü paketleri  
- Paketler  
- Önyükleme görüntüleri <sup> [Note 1](#bkmk_note1)</sup>  

Bu adım, aşağıdaki senaryolarda bir işletim sistemini yükseltmek için görev dizisinde iyi bir şekilde çalışmaktadır:  

- Hem x86 hem de x64 platformlarıyla çalışabilen tek bir yükseltme görev dizisi kullanma. **Yükseltme Için hazırlama** grubuna Iki **paket içeriğini indirme** adımı ekleyin. **Seçenekler** sekmesinde, istemci mimarisini algılamaya yönelik koşulları belirtin ve yalnızca uygun işletim sistemi yükseltme paketini indirin. Her bir **paket Içeriğini indirme** adımını aynı değişkeni kullanacak şekilde yapılandırın. **Işletim sistemini yükseltme** adımındaki medya yolu için değişkeni kullanın.  

- Uygun bir sürücü paketini dinamik olarak indirmek için, her bir sürücü paketine uygun donanım türünü algılamaya yönelik koşulları içeren iki adet **Paket İçeriğini İndirme** adımı kullanın. Her bir **paket Içeriğini indirme** adımını aynı değişkeni kullanacak şekilde yapılandırın. **Işletim sistemini yükseltme** adımının sürücüler bölümündeki **hazırlanmış içerik** değeri için değişkenini kullanın.  

> [!NOTE]  
> Bu adımı içeren bir görev dizisini dağıttığınızda, **görev sırasını başlatmadan önce tüm içeriği yerel olarak indir** ' i veya yazılım dağıtma sihirbazının **dağıtım noktaları** sayfasında **dağıtım seçenekleri** için **doğrudan dağıtım noktasından içeriğe erişim** ' i seçmeyin.  

Bu adım, tam işletim sisteminde veya Windows PE 'de çalışır. Paketi Configuration Manager istemci önbelleğinde kaydetme seçeneği Windows PE 'de desteklenmez.

> [!NOTE]  
> **Paket Içeriğini indir** görevi tek başına medyayla kullanım için desteklenmez. Daha fazla bilgi için bkz. [tek başına medya Için desteklenmeyen eylemler](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media).  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**, **yazılım**Seç ' i seçin ve **paket içeriğini indir**' i seçin.

### <a name="cmdlets-for-download-package-content"></a>Paket Içeriğini Indirme için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent)
- [New-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent)
- [Remove-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent)
- [Set-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent)

### <a name="properties-for-download-package-content"></a>Paket Içeriğini Indirme özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="select-package"></a>Paket seçme  

İndirilecek paketi seçmek için simgeyi seçin. Bir paket seçtikten sonra başka bir paket seçmek için simgeyi yeniden seçin.  

#### <a name="place-into-the-following-location"></a>Şu konuma yerleştir

Paketi aşağıdaki konumlardan birine kaydetmeyi seçin:  

- **Görev dizisi çalışma dizini**: Bu konum, görev sırası önbelleği olarak da adlandırılır.  

- **İstemci önbelleği Configuration Manager**: içeriği istemci önbelleğinde depolamak için bu seçeneği kullanın. Varsayılan olarak, bu yol olur `%WinDir%\ccmcache` .  

- **Özel yol**: görev sırası altyapısı ilk olarak paketi görev dizisi çalışma dizinine indirir. Daha sonra içeriği belirttiğiniz bu yola taşıdıkça. Görev sırası altyapısı, yolu paket KIMLIĞIYLE ekler.  

#### <a name="save-path-as-a-variable"></a>Yolu değişken olarak kaydetme

Paketin yolunu özel bir görev dizisi değişkenine kaydedin. Daha sonra bu değişkeni başka bir görev dizisi adımında kullanın.

Configuration Manager, değişken adına sayısal bir sonek ekler. Örneğin, bir değişkeni `%MyContent%` özel değişken olarak belirtirsiniz. Bu, görev dizisinin, bu adım için başvurulan tüm içeriği depoladığı bir köküdür. Bu içerik birden çok paket içerebilir. Değişkenine başvurduğunuzda sayısal bir sonek ekleyin. İlk paket için bölümüne bakın `%MyContent01%` . Örneğin, **Işletim sistemini yükseltme**gibi sonraki adımlarda değişkenine başvurduğunuzda, `%MyContent02%` veya `%MyContent03%` ' i kullanın; burada, sayı, **paket içeriğini indirme** adımının paketleri listeleyen sıraya karşılık gelir.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Bir paketin indirmesi başarısız olursa listedeki diğer paketleri indirmeye devam et

Görev dizisi bir paketi indiremediğinde, listedeki bir sonraki paketi indirmeye başlar.  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> Note 1: paket Içeriğini Indir adımında önyükleme görüntülerinin kullanımı

*Sürüm 1910 ve üzeri için geçerlidir*<!-- SCCMDocs-pr #4202 -->

[Görev dizisi özelliklerini](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) **bir önyükleme görüntüsü kullanacak**şekilde yapılandırırsanız, bu adıma bir önyükleme görüntüsü eklemek gereksizdir. Görev dizisinin özelliklerinde belirtilmemişse, bu adıma yalnızca bir önyükleme görüntüsü ekleyin.

#### <a name="example-use-case"></a>Örnek kullanım örneği

- İçeriği önceden indirmek için tek bir görev dizisi:
  - İlişkili önyükleme görüntüsü yok.
  - Büyük olasılıkla Kullanıcı etkileşimi olmadan yalnızca tam işletim sisteminde çalışır.
  - Birden çok **paket Içeriğini indirme** adımını koşullara göre kullanır. Belirli dile ve mimariye bağlı olarak, işletim sistemi dağıtımı görev dizisine hazırlanmak için içeriği istemci önbelleğine indirir.
  - Bu görev dizisinin yalnızca bir örneği, tüm olası içerik seçenekleriyle birlikte bulunur.

- Birden çok işletim sistemi dağıtımı görev dizisi:
  - Normal bir işletim sistemi dağıtımı görev dizisi.
  - , Özelliklerinde başvurulan bir önyükleme görüntüsüne sahiptir.
  - Bu görev dizisinin birden çok örneği, mimari ve dil için gereken farklı önyükleme görüntülerine sahiptir

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> BitLocker 'ı etkinleştir

BitLocker sürücü şifrelemesi disk birimi içeriği için alt düzey şifreleme sağlar. Sabit sürücüdeki en az iki bölümde BitLocker şifrelemesini etkinleştirmek için bu adımı kullanın. İlk etkin bölüm Windows önyükleme kodunu içerir. Başka bir bölüm işletim sistemini içerir. Önyükleme bölümü şifrelenmemiş kalmalıdır.  

Windows PE 'de bir sürücüde BitLocker 'ı etkinleştirmek için, [BitLocker 'ın ön sağlamasını](#BKMK_PreProvisionBitLocker) yap adımını kullanın.

Bu adım yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **diskler**' i seçin ve **BitLocker 'ı etkinleştir**' i seçin.

Yalnızca TPM, USB veya **TPM ve PIN** **üzerinde** **yalnızca TPM**belirttiğinizde, **BitLocker 'ı etkinleştir** adımını çalıştırmadan önce Güvenilir Platform Modülü (TPM) aşağıdaki durumda olmalıdır:  

- Etkin  
- Etkinleştirildi  
- Sahipliğe İzin Veriliyor  

Sürüm 2006 ' den başlayarak, TPM olmayan veya TPM etkinleştirilmediğinde bu adımı atlayabilirsiniz. Yeni bir ayar, BitLocker 'ı tam olarak desteklemeyen cihazlarda görev sırası davranışını yönetmeyi kolaylaştırır.<!--6995601-->

Bu adım, kalan TPM başlatma işlemini tamamlar. Kalan eylemler fiziksel varlık veya yeniden başlatma gerektirmez. **BitLocker 'ı etkinleştir** adımı, gerekirse AŞAĞıDAKI kalan TPM başlatma eylemlerini saydam olarak tamamlar:

- Onay anahtarı çifti oluşturma  
- Sahip yetkilendirme değeri oluşturun ve bu değeri desteklemek için genişletilmesi gereken Active Directory'de tutun  
- Sahipliği alın  
- Depolama kök anahtarı oluşturun veya zaten varsa ancak uyumsuzsa sıfırlayın  

Görev dizisinin **BitLocker 'ı etkinleştir** adımının sürücü şifreleme işlemini tamamlamasını beklemesini Istiyorsanız, **bekle** seçeneğini belirleyin. **Bekle** seçeneğini seçmezseniz, sürücü şifreleme işlemi arka planda gerçekleşir. Görev sırası hemen sonraki adıma geçer.  

BitLocker, bir bilgisayar sisteminde, hem işletim sistemi hem de veri sürücüleri üzerinde birden çok sürücüyü şifrelemek için kullanılabilir. Bir veri sürücüsünü şifrelemek için, önce işletim sistemi sürücüsünü şifreleyin ve şifreleme işlemini tamamlayabilirsiniz. Bu gereksinim, işletim sistemi sürücüsünün veri sürücüleri için anahtar koruyucuları depoladığından kaynaklanır. İşletim sistemi ve veri sürücüleri aynı görev dizisinde şifrelerseniz, işletim sistemi sürücüsü için **BitLocker 'ı etkinleştir** adımını seçin. **Wait**  

Sabit sürücü zaten şifrelendiyse ancak BitLocker devre dışı bırakıldıysa, **BitLocker 'ı etkinleştir** adımı, anahtar koruyucularını yeniden etkinleştirir ve hızlı bir şekilde tamamlanır. Bu durumda sabit sürücünün yeniden şifrelenmesi gerekmez.  

### <a name="variables-for-enable-bitlocker"></a>BitLocker 'ı etkinleştir için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDBitLockerPIN](task-sequence-variables.md#OSDBitLockerPIN)
- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)

### <a name="cmdlets-for-enable-bitlocker"></a>BitLocker 'ı etkinleştirme için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker)
- [New-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker)
- [Remove-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker)
- [Set-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker)

### <a name="properties-for-enable-bitlocker"></a>BitLocker 'ı etkinleştir özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="choose-the-drive-to-encrypt"></a>Şifrelenecek sürücüyü seçin

Şifrelenecek sürücüyü belirtir. Geçerli işletim sistemi sürücüsünü şifrelemek için **geçerli işletim sistemi sürücüsü**' nü seçin. Sonra anahtar yönetimi için aşağıdaki seçeneklerden birini yapılandırın:  

- **Yalnızca TPM**: Yalnızca Güvenilir Platform Modülü’nü (TPM) kullanmak için bu seçeneği belirleyin.  

- **Yalnızca USB üzerindeki Başlangıç Anahtarı**: USB flash sürücüde depolanan bir başlangıç anahtarını kullanmak için bu seçeneği belirleyin. Bu seçeneği belirlediğinizde, BitLocker bir BitLocker başlangıç anahtarı içeren bir USB cihaz bilgisayara bağlanana kadar normal önyükleme işlemini kilitler.  

- **TPM ve USB üzerindeki Başlangıç Anahtarı**: TPM ve USB flash sürücüde depolanan bir başlangıç anahtarını kullanmak için bu seçeneği belirleyin. Bu seçeneği belirlediğinizde, BitLocker bir BitLocker başlangıç anahtarı içeren bir USB cihaz bilgisayara bağlanana kadar normal önyükleme işlemini kilitler.  

- **TPM ve PIN**: TPM ve kişisel kimlik numarası (PIN) kullanmak için bu seçeneği belirleyin. Bu seçeneği belirlediğinizde, BitLocker kullanıcı bir PIN sağlayana kadar normal önyükleme işlemini kilitler.  

Belirli, işletim sistemi olmayan bir veri sürücüsünü şifrelemek için belirli bir **sürücü**seçin. Ardından listeden sürücüyü seçin.  

#### <a name="disk-encryption-mode"></a>Disk şifreleme modu

<!--6995601-->
Sürüm 2006 ' den başlayarak, aşağıdaki şifreleme algoritmalarından birini seçin:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Varsayılan olarak veya belirtilmemişse, adım işletim sistemi sürümü için varsayılan şifreleme yöntemini kullanmaya devam eder. Adım, belirtilen algoritmayı desteklemeyen bir Windows sürümü üzerinde çalışıyorsa, işletim sistemi varsayılan durumuna geri döner. Bu durumda, görev dizisi altyapısı 11911 durum iletisini gönderir.

#### <a name="use-full-disk-encryption"></a>Tam disk şifrelemesi kullan

<!--SCCMDocs-pr issue 2671-->
Varsayılan olarak, bu adım yalnızca sürücüdeki kullanılan alanı şifreler. Bu varsayılan davranış, daha hızlı ve daha verimli olduğu için önerilir. Kuruluşunuz, kurulum sırasında tüm sürücüyü şifrelemeyi gerektiriyorsa, bu seçeneği etkinleştirin. Windows Kurulumu, özellikle büyük sürücülerde, daha uzun zaman alan, tüm sürücünün şifrelenmesi için bekler.

> [!TIP]
> Sürüm 1910 ' den başlayarak, *tam disk* şifrelemesi kullanan BitLocker yönetim ilkeleri oluşturabilir ve dağıtabilirsiniz. Görev dizisi işletim sistemini dağıtduktan sonra cihazlarda BitLocker 'ı yönetmek için bu seçeneği etkinleştirin. Daha fazla bilgi için bkz. [plan for BitLocker Management](../../protect/plan-design/bitlocker-management.md).

#### <a name="choose-where-to-create-the-recovery-key"></a>Kurtarma anahtarının nerede oluşturulacağını seçin

BitLocker 'ın kurtarma parolasını oluşturmasını ve Active Directory için **Active Directory**' de seçin. Bu seçenek BitLocker anahtar Emanet için Active Directory genişletmenizi gerektirir. BitLocker daha sonra ilişkili kurtarma bilgilerini Active Directory kaydedebilir. Parola oluşturmak için **Kurtarma anahtarı oluşturma** ' yı seçin. Parola oluşturmak önerilen seçenektir.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Görev dizisini yürütmeye devam etmeden önce BitLocker'ın tüm sürücülerde sürücü şifrelemesi işlemini tamamlamasını bekleyin

Görev dizisindeki bir sonraki adımı çalıştırmadan önce BitLocker Sürücü Şifrelemesi 'nin tamamlanmasına izin vermek için bu seçeneği belirleyin. Bu seçeneği belirlerseniz, BitLocker, Kullanıcı bilgisayarda oturum açabilmeniz için tüm disk birimini şifreler.  

Büyük bir sabit sürücü şifrelerken, şifreleme işleminin tamamlanması saatler sürebilir. Bu seçeneğin belirlenmediğinden, görev dizisinin hemen devam etmesine izin verir.  

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>TPM olmayan bilgisayarlar için veya TPM etkin olmadığında bu adımı atlayın

<!--6995601-->
Sürüm 2006 ' den başlayarak, desteklenen veya etkinleştirilmiş TPM içermeyen bir bilgisayardaki sürücü şifrelemesini atlamak için bu seçeneği belirleyin. Örneğin, bir sanal makineye bir işletim sistemi dağıtırken bu seçeneği kullanın. Varsayılan olarak, bu ayar **BitLocker 'ı etkinleştir** adımı için devre dışıdır. Bu ayarı etkinleştirirseniz ve cihazda işlevsel TPM yoksa, görev sırası altyapısı Smsts. log dosyasına bir hata kaydeder ve 11912 durum iletisini gönderir. Görev sırası bu adımı geçti.


## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Diski Biçimlendir ve bölümle

Hedef bilgisayarda belirtilen bir diski biçimlendirmek ve bölümlemek için bu adımı kullanın.  

> [!IMPORTANT]  
> Bu adım için belirttiğiniz her ayar, belirtilen tek bir disk için geçerlidir. Hedef bilgisayarda başka bir diski biçimlendirmek ve bölümlemek için, görev dizisine ek bir **Biçim ve Bölüm diski** adımı ekleyin.  

Bu adım yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **diskler**' i seçin ve **Diski Biçimlendir ve bölümlendir**' ı seçin.

### <a name="variables-for-format-and-partition-disk"></a>Biçim ve Bölüm diski değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>Biçim ve Bölüm diski için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](/powershell/module/configurationmanager/get-cmtssteppartitiondisk)
- [New-CMTSStepPartitionDisk](/powershell/module/configurationmanager/new-cmtssteppartitiondisk)
- [Remove-CMTSStepPartitionDisk](/powershell/module/configurationmanager/remove-cmtssteppartitiondisk)
- [Set-CMTSStepPartitionDisk](/powershell/module/configurationmanager/set-cmtssteppartitiondisk)

### <a name="properties-for-format-and-partition-disk"></a>Biçim ve Bölüm diski özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="disk-number"></a>Disk Numarası

Biçimlendirilecek diskin fiziksel disk numarası. Numara, Windows disk numaralandırma sırasını temel alır.  

#### <a name="variable-name-to-store-disk-number"></a>Disk numarasını depolamak için değişken adı

<!--6610288-->

Sürüm 2006 ' den başlayarak biçimlendirilecek hedef diski belirtmek için bir görev dizisi değişkeni kullanın. Bu değişken seçeneği, dinamik davranışlarla daha karmaşık görev dizilerini destekler. Örneğin, özel bir betik diski algılayabilir ve değişkeni donanım türüne göre ayarlayabilir. Daha sonra farklı donanım türlerini ve bölümlerini yapılandırmak için bu adımın birden fazla örneğini kullanabilirsiniz.

Bu özelliği seçerseniz, özel bir değişken adı girin. Bu özel değişkenin değerini fiziksel disk için bir tamsayı değerine ayarlamak üzere görev dizisine daha önceki bir adım ekleyin.

Aşağıdaki sahte adımlarda bir örnek gösterilmektedir:

- **PowerShell betiğini Çalıştır**: hedef diskleri toplamak için özel bir betik
  - `myOSDisk`Olarak ayarlar`1`
  - `myDataDisk`Olarak ayarlar`2`

- İşletim sistemi diski için **Diski Biçimlendir ve bölümle** : `myOSDisk` değişkeni belirtir
  - Disk 1 ' i sistem diski olarak yapılandırır

- Veri diski için **Diski Biçimlendir ve bölümle** : `myDataDisk` değişkeni belirtir
  - Ham depolama için disk 2 ' i yapılandırır

Bu örneğin bir çeşitlemesi, farklı donanım türleri için disk numaralarını ve bölümleme planlarını kullanır.

> [!NOTE]
> Mevcut görev dizisi değişkeni **Osddiskındex**' i kullanmaya devam edebilirsiniz. Ancak, **Biçim ve Bölüm diski** adımının her bir örneği aynı dizin değerini kullanır. Bu adımın birden fazla örneği için programlı olarak disk numarası ayarlamak istiyorsanız bu değişken özelliğini kullanın.

#### <a name="disk-type"></a>Disk Türü

Biçimlendirilecek diskin türü. Açılır listeden belirlenebilecek iki seçenek vardır:

- **Standart (MBR)**: Ana önyükleme kaydı  
- **GPT**: GUID bölümleme tablosu  

> [!NOTE]  
> Disk türünü **Standart (MBR)** ' den **GPT**' ye değiştirirseniz ve bölüm düzeni genişletilmiş bir bölüm içeriyorsa, görev sırası tüm genişletilmiş ve mantıksal bölümleri düzenden kaldırır. Görev sırası Düzenleyicisi, disk türünü değiştirmeden önce bu eylemi onaylamanızı ister.  

#### <a name="volume"></a>Birim

Aşağıdaki öznitelikler de dahil olmak üzere, görev dizisinin oluşturduğu bölüm veya birim hakkında belirli bilgiler:  

- Name  
- Kalan disk alanı  

Yeni bir bölüm oluşturmak için **bölüm özellikleri** iletişim kutusunu başlatmak üzere **Yeni** ' yi seçin. Bölüm türü ve boyutunu ve bir önyükleme bölümüyse belirtin. Mevcut bir bölümü değiştirmek için, değiştirilecek bölümü seçin ve ardından **Özellikler** düğmesini seçin. Sabit sürücü bölümlerinin nasıl yapılandırılacağı hakkında daha fazla bilgi için aşağıdaki makalelerden birine bakın:  

- [UEFı/GPT tabanlı sabit sürücü bölümleri](/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [BIOS/MBR tabanlı sabit sürücü bölümleri](/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Bir bölümü silmek için bölümü seçin ve ardından **Sil**' i seçin.  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> Uygulamayı yükler

Bu adım belirtilen uygulamaları veya dinamik bir görev dizisi değişkenleri listesi tarafından tanımlanan bir uygulama kümesini yüklüyor. Görev dizisi bu adımı çalıştırdığında, uygulama yüklemesi bir ilke yoklama aralığı için beklenmeden hemen başlar.  

Uygulamalar aşağıdaki ölçütleri karşılamalıdır:  

- Uygulamanın **Windows Installer** veya **betik** yükleyici dağıtım türünde olması gerekir. Windows uygulama paketi (. appx dosyası) dağıtım türleri desteklenmez.  

- Kullanıcı hesabı değil, yerel sistem hesabı altında çalışmalıdır.  

- Bu masaüstü ile etkileşimde bulunmamalıdır. Program sessiz bir şekilde veya katılımsız modda çalışmalıdır.  

- Kendi başına bir yeniden başlatma işlemi gerçekleştirmemelidir. Uygulamanın, standart yeniden başlatma kodu olan 3010 kullanılarak yeniden başlatma istemesi gerekir. Bu davranış, bu adımın yeniden başlatma işlemini doğru bir şekilde işleyeceğinden emin olur. Uygulama bir 3010 çıkış kodu döndürürse, görev sırası altyapısı bilgisayarı yeniden başlatır. Yeniden başladıktan sonra görev dizisi otomatik olarak devam eder.  

> [!Note]
> Uygulama [yürütülebilir dosyaları çalıştırmaya denetlediğinde](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check), görev sırası bunu yükleyemez. Bu adımı hata durumunda devam etmek için yapılandırmazsanız, tüm görev sırası başarısız olur.

Bu adım çalıştığında, uygulama, dağıtım türlerinde gereksinim kuralları ve algılama yönteminin uygulanabilirliğini denetler. Uygulama bu denetimin sonuçlarına bağlı olarak ilgili dağıtım türünü yükler. Dağıtım türü bağımlılıklar içeriyorsa, bağımlı dağıtım türü değerlendirilir ve bu adımın bir parçası olarak yüklenir. Uygulama bağımlılıkları tek başına medya için desteklenmez.  

> [!NOTE]  
> Başka bir uygulamanın yerine geçen bir uygulamayı yüklemek için, yenisiyle değiştirilen uygulamanın içerik dosyaları kullanılabilir olmalıdır. Aksi takdirde bu görev dizisi adımı başarısız olur. Örneğin, bir istemciye veya yakalanan görüntüye Microsoft Visio 2010 yükleniyor. **Uygulama yükleme** adımı microsoft Visio 2013 yüklediğinde, microsoft Visio 2010 (yenisiyle değiştirilen uygulama) için içerik dosyaları bir dağıtım noktasında kullanılabilir olmalıdır. Microsoft Visio, bir istemcide veya yakalanan görüntüde hiç yüklenmemişse, görev sırası Microsoft Visio 2010 içerik dosyalarını denetlemeden Microsoft Visio 2013 ' i de yüklüyor.  
>
> Yenisiyle değiştirilen bir uygulamayı devre dışı bırakırsanız ve yeni uygulamaya bir görev dizisinde başvuruluyorsa, görev sırası başlatılamaz.
Bu davranış tasarıma göre belirlenir: görev sırası tüm uygulama başvurularını gerektirir.<!-- SCCMDocs 1711 -->  

Bu görev dizisi adımı yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**, **yazılım**Seç ' i seçin ve **uygulamayı yüklemeyi**seçin.

### <a name="variables-for-install-application"></a>Uygulama yüklemeye yönelik değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> İstemci, konum hizmetlerinden yönetim noktası listesini alamaırsa **Smstsmplistrequesttimeoutenabled** ve **SMSTSMPListRequestTimeout** görev sırası değişkenlerini kullanın. Bu değişkenler, bir görev dizisinin bir uygulamayı yüklemeyi yeniden denemeden önce kaç milisaniye bekleyeceğini belirtir. Daha fazla bilgi için bkz. [görev dizisi değişkenleri](task-sequence-variables.md).

### <a name="cmdlets-for-install-application"></a>Uygulama yüklemesi için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-Cmtsstepınstallapplication](/powershell/module/configurationmanager/get-cmtsstepinstallapplication)
- [New-Cmtsstepınstallapplication](/powershell/module/configurationmanager/new-cmtsstepinstallapplication)
- [Remove-Cmtsstepınstallapplication](/powershell/module/configurationmanager/remove-cmtsstepinstallapplication)
- [Set-Cmtsstepınstallapplication](/powershell/module/configurationmanager/set-cmtsstepinstallapplication)

### <a name="properties-for-install-application"></a>Uygulama yüklemesi için Özellikler

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="install-the-following-applications"></a>Aşağıdaki uygulamaları yükle

Görev sırası, bu uygulamaları belirtilen sırada kurar.  

Configuration Manager devre dışı bırakılmış uygulamaları veya aşağıdaki ayarlara sahip herhangi bir uygulamayı filtreler:  

- Yalnızca bir kullanıcı oturum açtığında  
- Kullanıcı hakları ile çalıştır  

Bu uygulamalar **yüklenecek uygulamayı seçin** iletişim kutusunda görünmez.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Uygulamaları dinamik değişken listesine göre yükleyin

Görev sırası, bu temel değişken adını kullanarak uygulamalar yüklüyor. Temel değişken adı bir koleksiyon veya bilgisayar için tanımlanan bir görev dizisi değişkenleri kümesi içindir. Bu değişkenler, görev dizisinin bu koleksiyon veya bilgisayar için yüklediği uygulamaları belirtir. Her bir değişken adı, ortak bir taban adına ve 01 ile başlayan sayısal bir son eke sahiptir. Her bir değişken değeri, yalnızca uygulamanın adını içermelidir.  

Bir dinamik değişken listesi kullanarak uygulamaları yüklemek için görev dizisinin, uygulama **özelliklerinin** **genel** sekmesinde aşağıdaki ayarı etkinleştirin: **Bu uygulamanın el ile dağıtma yerine uygulama yükleme görev dizisi eylemiyle yüklenmesine izin ver**.  

> [!NOTE]  
> Tek başına medya dağıtımları için dinamik değişken listesini kullanarak uygulama yükleyemezsiniz.  

Örneğin, AA01 adlı bir görev dizisi değişkeni kullanarak tek bir uygulama yüklemek için aşağıdaki değişkeni belirtin:  

|Değişken Adı|Değişken Değeri|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

İki uygulama yüklemek için aşağıdaki değişkenleri belirtin:  

|Değişken Adı|Değişken Değeri|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Aşağıdaki koşullar, görev sırası tarafından yüklenen uygulamaları etkiler:  

- Bir değişkenin değeri uygulamanın adı dışında herhangi bir bilgi içeriyorsa. Görev sırası uygulamayı yüklemez ve görev sırası devam eder.  

- Görev sırası belirtilen temel adı ve "01" sonekine sahip bir değişken bulamazsa, görev sırası herhangi bir uygulama yüklemez.  

> [!Important]  
> Bu değerler büyük/küçük harfe duyarlıdır. Örneğin, "Install", "Install" sürümünden farklıdır. Değeri değiştirmeniz gerekiyorsa, görev dizisi Düzenleyicisi durum değişikliğini algılamaz. Aynı anda başka bir düzenleme yapın, örneğin adım açıklamasını değiştirin.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Bir uygulama başarısız olursa, listedeki diğer uygulamaların yüklenmesine devam edilsin

Bu ayar, tek bir uygulama yüklemesi başarısız olduğunda adımın devam edeceğini belirtir. Bu ayarı belirtirseniz, görev dizisi, yükleme hatalarından bağımsız olarak devam eder. Bu ayarı belirtmezseniz ve yükleme başarısız olursa, adım hemen sona erer.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Yükledikten sonra önbellekten uygulama içeriğini temizle

<!--4485675-->
Sürüm 1906 ' den başlayarak, adım çalıştıktan sonra istemci önbelleğinden uygulama içeriğini silin. Bu davranış, küçük sabit sürücüler içeren cihazlarda veya birçok büyük uygulamayı art arda yüklerken faydalıdır.


### <a name="options-for-install-application"></a>Uygulama yüklemeye yönelik seçenekler

> [!NOTE]  
> Bu adımın **Seçenekler** sekmesinde **hata durumunda devam et** ' i seçtiğinizde, bir uygulamanın yüklenmesi başarısız olduğunda görev dizisi devam eder. Bu seçeneği etkinleştirmezseniz, görev sırası başarısız olur ve kalan uygulamaları yüklemez.  

Varsayılan seçeneklerin yanı sıra, bu görev dizisi adımının **Seçenekler** sekmesinde aşağıdaki ek ayarları yapılandırın:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Bilgisayar beklenmedik şekilde yeniden başlatılırsa bu adımı yeniden deneyin

Uygulama yüklemelerinden biri beklenmedik bir şekilde bilgisayarı yeniden başlattığında, bu adımı yeniden deneyin. Adım, varsayılan olarak iki yeniden denemeden bu ayarı sunar. Bunlardan beş kez yeniden deneme arasında bir tane belirtebilirsiniz.  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> Paketi yükler

Görev dizisinin bir parçası olarak bir yazılım paketi yüklemek için bu adımı kullanın. Bu adım çalıştığında, yükleme bir ilke yoklama aralığı için beklenmeden hemen başlar.  

Paketin aşağıdaki ölçütlere uyması gerekir:  

- Kullanıcı hesabı değil, yerel sistem hesabı altında çalışmalıdır.  

- Bu masaüstü ile etkileşimde bulunmamalıdır. Program sessiz bir şekilde veya katılımsız modda çalışmalıdır.  

- Kendi başına bir yeniden başlatma işlemi gerçekleştirmemelidir. Yazılım standart yeniden başlatma kodu olan 3010 kullanılarak yeniden başlatma istemesi gerekir. Bu davranış, görev dizisinin yeniden başlatmayı doğru bir şekilde işlemesini sağlar. Yazılım bir 3010 çıkış kodu getirmezse, görev sırası altyapısı bilgisayarı yeniden başlatır. Yeniden başladıktan sonra görev dizisi otomatik olarak devam eder.  

Bağımlı bir program yüklemek için **önce başka bir program çalıştır** seçeneğini kullanan programlar bir işletim sistemi dağıtımında desteklenmez. **Önce başka bir programı çalıştır**paket seçeneğini etkinleştirirseniz ve bağımlı program hedef bilgisayarda zaten çalıştırıldıysa, bağımlı program çalıştırılır ve görev dizisi devam eder. Ancak, bağımlı program hedef bilgisayarda zaten çalıştırılmadıysa, görev dizisi adımı başarısız olur.  

> [!NOTE]  
> Yönetim Merkezi sitesi, görev sırası sırasında yazılım dağıtım aracısını etkinleştirmek için gerekli olan istemci yapılandırma ilkelerine sahip değildir. Yönetim merkezi sitesinde bir görev dizisi için tek başına medya oluşturduğunuzda ve görev dizisi bir **Paketi Yükle** adımı içerdiğinde CreateTsMedia.log dosyasında aşağıdaki hata belirebilir:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> **Paketi yüklemeyi** içeren tek başına medya için, tek başına medyayı yazılım dağıtım Aracısı etkinleştirilmiş bir birincil sitede oluşturun. Alternatif olarak, **Windows 'u ve ConfigMgr 'Yi Kur** adımından sonra ve **paketi yükleme** adımından önce bir **komut satırı Çalıştır** adımı ekleyin. **Komut satırını Çalıştır** adımı, Ilk **paketi Kur** adımından önce yazılım dağıtım ARACıSıNı etkinleştirmek için bir WMIC komutu çalıştırır. **Komut satırını Çalıştır** adımında aşağıdaki komutu kullanın:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Tek başına medya oluşturma hakkında daha fazla bilgi için bkz. [tek başına medya oluşturma](../deploy-use/create-stand-alone-media.md).  

Bu görev dizisi adımı yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**, **yazılım**Seç ' i seçin ve **paketi Kur**' u seçin.

### <a name="variables-for-install-package"></a>Paketi yüklemeye yönelik değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>Paketi yüklemeye yönelik cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-Cmtsstepınstallsoftware](/powershell/module/configurationmanager/get-cmtsstepinstallsoftware)
- [New-Cmtsstepınstallsoftware](/powershell/module/configurationmanager/new-cmtsstepinstallsoftware)
- [Remove-Cmtsstepınstallsoftware](/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware)
- [Set-Cmtsstepınstallsoftware](/powershell/module/configurationmanager/set-cmtsstepinstallsoftware)

> [!TIP]
> Kullanıcı görev dizisini yüklemeden önce geçerli bir işletim sistemi yükseltme paketini indirmek için içeriği önceden önbelleğe alma özelliğini kullanın. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../deploy-use/configure-precache-content.md).

### <a name="properties-for-install-package"></a>Paketi yüklemeye yönelik özellikler

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="install-a-single-software-package"></a>Tek yazılım paketi yükleme

Bu ayar bir Configuration Manager yazılım paketi belirtir. Bu adım, yükleme tamamlanana kadar bekler.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Yazılım paketlerini dinamik değişken listesine göre yükleyin

Görev sırası, bu temel değişken adını kullanarak paketleri yüklüyor. Temel değişken adı bir koleksiyon veya bilgisayar için tanımlanan bir görev dizisi değişkenleri kümesi içindir. Bu değişkenler, görev dizisinin bu koleksiyon veya bilgisayar için yüklediği paketleri belirtir. Her bir değişken adı, ortak bir taban adına ve 001 ile başlayan sayısal bir son eke sahiptir. Her bir değişken adı, virgülle ayrılmış olarak paket kimliğini ve yazılımın adını içermelidir.  

Bir dinamik değişken listesini kullanarak yazılım yükleme görevi için, paket **özelliklerinin** **Gelişmiş** sekmesinde aşağıdaki ayarı etkinleştirin: **Bu programın dağıtılmadan paket yükleme görev sırasından yüklenmesine izin ver**.  

> [!NOTE]  
> Tek başına medya dağıtımları için dinamik değişken listesini kullanarak yazılım paketleri yükleyemezsiniz.  

Örneğin, AA001 adında bir görev dizisi değişkeni kullanarak tek bir yazılım paketi yüklemek için aşağıdaki değişkeni belirtmeniz gerekir:  

|Değişken Adı|Değişken Değeri|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Üç yazılım paketi yüklemek için aşağıdaki değişkenleri belirtmeniz gerekir:  

|Değişken Adı|Değişken Değeri|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Sessiz Yükle|  
|AA003|CEN00031:Install|  

Aşağıdaki koşullar, görev sırası tarafından yüklenen paketleri etkiler:  

- Bir değişkenin değerini doğru biçimde oluşturmayın veya geçerli bir paket KIMLIĞI ve adı belirtmezseniz, yazılım yüklemesi başarısız olur.  

- Paket KIMLIĞI küçük harfli karakterler içeriyorsa, yazılım yüklemesi başarısız olur.  

- Görev sırası belirtilen temel adı ve "001" son ekine sahip bir değişken bulamazsa, görev dizisi hiçbir paket yüklemez. Görev sırası devam eder.  

> [!Important]  
> Bu değerler büyük/küçük harfe duyarlıdır. Örneğin, "Install", "Install" sürümünden farklıdır. Değeri değiştirmeniz gerekiyorsa, görev dizisi Düzenleyicisi durum değişikliğini algılamaz. Aynı anda başka bir düzenleme yapın, örneğin adım açıklamasını değiştirin.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Bir yazılım paketi yüklemesi başarısız olursa listedeki diğer paketlerin yüklenmesine devam edilsin

Bu ayar, bir yazılım paketinin yüklenmesi başarısız olursa adımın devam edeceğini belirtir. Bu ayarı belirtirseniz, görev dizisi, yükleme hatalarından bağımsız olarak devam eder. Bu ayarı belirtmezseniz ve yükleme başarısız olursa, adım hemen sona erer.  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Yazılım güncelleştirmelerini yükler

Yazılım güncelleştirmelerini hedef bilgisayara yüklemek için bu adımı kullanın. Bu görev dizisi adımı çalıştırılıncaya kadar hedef bilgisayar ilgili yazılım güncelleştirmeleri için değerlendirilmez. Bu sırada, hedef bilgisayar yazılım güncelleştirmeleri için diğer Configuration Manager istemcileri gibi değerlendirilir. Yazılım güncelleştirmelerini yüklemek için bu adım için, önce güncelleştirmeleri hedef bilgisayarın üyesi olduğu bir koleksiyona dağıtın.  

> [!IMPORTANT]  
> En iyi performans için Windows Update aracısının en son sürümünü yükler.  

Bu görev dizisi adımı yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**, **yazılım**Seç ' i seçin ve **yazılım güncelleştirmelerini yükler**' i seçin.

### <a name="variables-for-install-software-updates"></a>Yazılım güncelleştirmelerini yüklemeye yönelik değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> İstemci, konum hizmetlerinden yönetim noktası listesini alamaırsa **Smstsmplistrequesttimeoutenabled** ve **SMSTSMPListRequestTimeout** değişkenlerini kullanın. Bu değişkenler, bir görev dizisinin bir uygulama veya yazılım güncelleştirmesini yüklemeyi yeniden denemeden önce kaç milisaniye bekleyeceğini belirtir. Daha fazla bilgi için bkz. [görev dizisi değişkenleri](task-sequence-variables.md).  

### <a name="cmdlets-for-install-software-updates"></a>Yazılım güncelleştirmelerini yüklemeye yönelik cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-Cmtsstepınstallupdate](/powershell/module/configurationmanager/get-cmtsstepinstallupdate)
- [New-Cmtsstepınstallupdate](/powershell/module/configurationmanager/new-cmtsstepinstallupdate)
- [Remove-Cmtsstepınstallupdate](/powershell/module/configurationmanager/remove-cmtsstepinstallupdate)
- [Set-Cmtsstepınstallupdate](/powershell/module/configurationmanager/set-cmtsstepinstallupdate)

Bu adım için daha fazla öneri ve teknik akış grafiği diyagramı için bkz. [yazılım güncelleştirmelerini yüklemeyi](install-software-updates.md).

### <a name="properties-for-install-software-updates"></a>Yazılım güncelleştirmelerini yüklemeye yönelik özellikler

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Yüklenmesi gerekli - Yalnızca zorunlu yazılım güncelleştirmeleri

Yönetici tarafından tanımlanan yükleme son tarihlerine sahip tüm zorunlu yazılım güncelleştirmelerini yüklemek için bu seçeneği belirleyin.  

#### <a name="available-for-installation---all-software-updates"></a>Yüklenmeye hazır - Tüm yazılım güncelleştirmeleri var

Tüm kullanılabilir yazılım güncelleştirmelerini yüklemek için bu seçeneği belirleyin. Önce bu güncelleştirmeleri bilgisayarın üyesi olduğu bir koleksiyona dağıtın. Görev sırası, tüm kullanılabilir yazılım güncelleştirmelerini hedef bilgisayarlara yüklenir.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Önbelleğe alınan tarama sonuçlarındaki yazılım güncelleştirmelerini değerlendirme

Varsayılan olarak, bu adım Windows Update aracısında önbelleğe alınmış tarama sonuçlarını kullanır. Windows Update aracısına, yazılım güncelleştirme noktasından en son kataloğu indirmesini bildirmek için bu seçeneği devre dışı bırakın. Bir [işletim sistemi görüntüsü yakalamak ve derlemek](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)için bir görev dizisi kullanırken bu seçeneği etkinleştirin. Bu senaryoda çok sayıda yazılım güncelleştirmesi olabilir.

Bu güncelleştirmelerin çoğunda bağımlılıklar vardır. Örneğin, Update XYZ güncelleştirmesi, geçerli olduğu gibi görünür. Bu ayarı devre dışı bıraktığınızda ve görev dizisini birçok istemciye dağıttığınızda, hepsi aynı anda yazılım güncelleştirme noktasına bağlanır. Bu davranış, güncelleştirme kataloğunun işlenmesi ve indirilmesi sırasında performans sorunlarına neden olur.

Çoğu durumda, önbelleğe alınmış tarama sonuçlarını kullanmak için varsayılan ayarı kullanın.

**SMSTSSoftwareUpdateScanTimeout** değişkeni, bu adım sırasında yazılım güncelleştirmeleri tarama zaman aşımını denetler. Varsayılan değer 60 dakikadır. Daha fazla bilgi için bkz. [görev dizisi değişkenleri](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).

### <a name="options-for-install-software-updates"></a>Yazılım güncelleştirmelerini yüklemeye yönelik seçenekler

Varsayılan seçeneklerin yanı sıra, bu görev dizisi adımının **Seçenekler** sekmesinde aşağıdaki ek ayarları yapılandırın:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Bilgisayar beklenmedik şekilde yeniden başlatılırsa bu adımı yeniden deneyin

Güncelleştirmelerden biri bilgisayarı beklenmedik şekilde yeniden başlattığında, bu adımı yeniden deneyin. Adım, varsayılan olarak iki yeniden denemeden bu ayarı sunar. Bunlardan beş kez yeniden deneme arasında bir tane belirtebilirsiniz.  

> [!NOTE]  
> Bu senaryoda bilgisayar yeniden başlatıldıktan sonra görev dizisinin kaç saniye duraklayacağını belirtmek için **SMSTSWaitForSecondReboot** değişkenini yapılandırın. Daha fazla bilgi için bkz. [görev dizisi değişkenleri](task-sequence-variables.md#SMSTSWaitForSecondReboot).  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Etki alanına veya çalışma grubuna katıl

Hedef bilgisayarı bir çalışma grubuna veya etki alanına eklemek için bu adımı kullanın.  

> [!NOTE]
> Bir Azure Active Directory (Azure AD) ile Birleşik istemci bir işletim sistemi dağıtımı görev dizisi çalıştırdığında, yeni işletim sistemindeki istemci Azure AD 'ye otomatik olarak katılmayacaktır. Azure AD 'ye katılmış olmasa bile, istemci hala yönetilecektir.

Bu görev dizisi adımı yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **etki alanına veya çalışma grubuna katıl**' ı seçin.

### <a name="variables-for-join-domain-or-workgroup"></a>Katılma etki alanı veya çalışma grubu için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>Katılma etki alanı veya çalışma grubu için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup)
- [New-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup)
- [Remove-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup)
- [Set-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup)

### <a name="properties-for-join-domain-or-workgroup"></a>Katılma etki alanı veya çalışma grubu özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="join-a-workgroup"></a>Çalışma grubuna katıl

Hedef bilgisayarın belirtilen çalışma grubuna katılmasını sağlamak için bu seçeneği belirleyin. Bilgisayar şu anda bir etki alanının üyesiyse, bu seçeneğin belirlenmesi bilgisayarın yeniden başlatılmasına neden olur.  

#### <a name="join-a-domain"></a>Bir etki alanına katılma

Hedef bilgisayarın belirtilen etki alanına katılmasını sağlamak için bu seçeneği belirleyin.  

İsteğe bağlı olarak, belirtilen etki alanında bilgisayarın katılması için bir kuruluş birimi (OU) belirtin veya gözatın. Bilgisayar şu anda başka bir etki alanının veya çalışma grubunun üyesi ise, bu seçenek bilgisayarın yeniden başlatılmasına neden olur. Bilgisayar zaten başka bir OU 'nun üyesiyse Active Directory Domain Services, bu yöntem aracılığıyla OU 'yu değiştirmeye izin vermediğinden, bu ayarı yok sayar Windows Kurulumu.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Etki alanına katılmak için yeterli izne sahip olan hesabı belirtin

Etki alanına ekleme izinleri olan bir hesabın kullanıcı adını ve parolasını girmek için **Ayarla** ' yı seçin. Hesabı şu biçimde girin:  `Domain\account` . Görev sırası etki alanına katılma hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> ConfigMgr Istemcisini yakalamaya hazırla

Başvuru bilgisayarında Configuration Manager istemcisini kaldırmak veya yapılandırmak için bu adımı kullanın. Bu eylem, görüntüleme işleminin bir parçası olarak bilgisayarı yakalamaya hazırlar.

Bu adım yalnızca anahtar bilgilerini kaldırmak yerine Configuration Manager istemcisini tamamen kaldırır. Görev dizisi yakalanan işletim sistemi görüntüsünü dağıttığında, her seferinde yeni bir Configuration Manager istemci yüklenir.  

> [!TIP]
> Varsayılan olarak, görev dizisi altyapısı yalnızca derleme sırasında istemciyi kaldırır **ve bir başvuru işletim sistemi görüntüsünü yakala** görev sırasını yakalar. Görev sırası altyapısı, yakalama medyası veya özel bir görev dizisi gibi diğer yakalama yöntemleri sırasında istemciyi kaldırmaz. Bu davranışı bir işletim sistemi dağıtımı görev dizisi için overide yapabilirsiniz. {1 & gt; görev dizisi değişkenini **yakala adımı Için hazırlama** **adımını yapmadan önce** , **Smstsunınstallccmclient** . Bu değişken ve davranış yalnızca işletim sistemi dağıtımı görev dizileri için geçerlidir. Cihazın bir sonraki yeniden başlatıldıktan sonra istemciyi kaldırır.

Bu görev dizisi adımı yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**, **görüntüler**Seç ' i seçin ve **ConfigMgr istemcisini yakalama için hazırla**' yı seçin.


### <a name="variables-for-prepare-configmgr-client-for-capture"></a>ConfigMgr Istemcisini yakalamaya hazırlama değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- Smstsunınstallccmclient


### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>ConfigMgr Istemcisini yakalamaya hazırlamaya yönelik cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient)
- [New-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient)
- [Remove-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient)
- [Set-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Windows 'u yakalamaya hazırla

Referans bilgisayarda bir işletim sistemi görüntüsü yakalarken Sysprep seçeneklerini belirtmek için bu adımı kullanın. Bu adım Sysprep 'i çalıştırır ve ardından bilgisayarı görev sırası için belirtilen Windows PE önyükleme görüntüsü ile yeniden başlatır. Başvuru bilgisayarı bir etki alanına katılırsa bu eylem başarısız olur.  

Bu adım yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **görüntüler**' i seçin ve **Windows 'u yakalama için hazırla**' yı seçin.

### <a name="variables-for-prepare-windows-for-capture"></a>Windows 'u yakalamaya hazırlama değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Windows 'u yakalamaya hazırlamak için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows)
- [New-CMTSStepPrepareWindows](/powershell/module/configurationmanager/New-CMTSStepPrepareWindows)
- [Remove-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows)
- [Set-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows)

### <a name="properties-for-prepare-windows-for-capture"></a>Windows 'u yakalamaya hazırlamaya yönelik özellikler

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Otomatik olarak yığın depolama sürücü listesi oluşturun

Sysprep'in başvuru bilgisayarından yığın depolama sürücülerin listesini otomatik olarak oluşturması için bu seçeneği belirleyin. Bu seçenek başvuru bilgisayarındaki sysprep.inf dosyasındaki Yığın Depolama Sürücüleri Oluştur seçeneğini etkinleştirir. Bu ayar hakkında daha fazla bilgi için Sysprep belgelerine bakın.  

#### <a name="do-not-reset-activation-flag"></a>Etkinleştirme bayrağını sıfırlama

Sysprep'in ürün etkinleştirme bayrağını sıfırlamasını önlemek için bu seçeneği belirleyin.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Bu eylemi çalıştırdıktan sonra bilgisayarı kapatır

<!--SCCMDocs-pr issue 2695-->
Bu seçenek Sysprep 'in varsayılan yeniden başlatma davranışı yerine bilgisayarı kapatması talimatını verir.

[Var olan cihazlar Için Windows Autopilot](../../../autopilot/existing-devices.md) görev sırası bu seçenekle bu adımı kullanır.

- Görev dizisinin cihazı yenilemesini ve sonra Autopilot için OOBE 'yi hemen başlatmasını istiyorsanız, bu seçeneği kapalı bırakın.  

- Görüntüleme sonrasında cihazı kapatması için bu seçeneği etkinleştirin. Ardından, cihazı ilk kez açtığında Autopilot ile OOBE Başlatan bir kullanıcıya gönderebilirsiniz.  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> BitLocker 'ın ön sağlamasını yap

Windows PE 'de bir sürücüde BitLocker 'ı etkinleştirmek için bu adımı kullanın. Varsayılan olarak, yalnızca kullanılan sürücü alanı şifrelenir, bu nedenle şifreleme süreleri çok daha hızlıdır. Anahtar yönetim seçeneklerini işletim sistemi yüklendikten sonra [BitLocker 'ı etkinleştir](#BKMK_EnableBitLocker) adımını kullanarak uygularsınız.

> [!IMPORTANT]
> BitLocker 'ın ön sağlamasını yapmak için bilgisayarın desteklenen ve etkinleştirilmiş bir Güvenilir Platform Modülü (TPM) olması gerekir.

Bu adım yalnızca Windows PE'de çalışır. Tam işletim sisteminde çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **diskler**' i seçin ve **BitLocker 'ın ön sağlamasını**yap ' ı seçin.

### <a name="cmdlets-for-pre-provision-bitlocker"></a>BitLocker 'ın ön sağlamasını yapmak için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker)
- [New-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker)
- [Remove-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker)
- [Set-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker)

### <a name="properties-for-pre-provision-bitlocker"></a>BitLocker 'ın ön sağlamasını yapmak için Özellikler

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>BitLocker'ı belirtilen sürücüye uygula

BitLocker'ı etkinleştirmek istediğiniz sürücüyü belirtin. BitLocker yalnızca sürücüdeki kullanılan alanı şifreler.  

#### <a name="disk-encryption-mode"></a>Disk şifreleme modu

<!--6995601-->
Sürüm 2006 ' den başlayarak, aşağıdaki şifreleme algoritmalarından birini seçin:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Varsayılan olarak veya belirtilmemişse, adım işletim sistemi sürümü için varsayılan şifreleme yöntemini kullanmaya devam eder. Adım, belirtilen algoritmayı desteklemeyen bir Windows sürümü üzerinde çalışıyorsa, işletim sistemi varsayılan durumuna geri döner. Bu durumda, görev dizisi altyapısı 11911 durum iletisini gönderir.

#### <a name="use-full-disk-encryption"></a>Tam disk şifrelemesi kullan

<!--SCCMDocs-pr issue 2671-->
Varsayılan olarak, bu adım yalnızca sürücüdeki kullanılan alanı şifreler. Bu varsayılan davranış, daha hızlı ve daha verimli olduğu için önerilir. Kuruluşunuz, kurulum sırasında tüm sürücüyü şifrelemeyi gerektiriyorsa, bu seçeneği etkinleştirin. Windows Kurulumu, özellikle büyük sürücülerde, daha uzun zaman alan, tüm sürücünün şifrelenmesi için bekler.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>TPM olmayan bilgisayarlar için veya TPM etkin olmadığında bu adımı atlayın

Desteklenen veya etkinleştirilmiş TPM içermeyen bir bilgisayardaki sürücü şifrelemesini atlamak için bu seçeneği belirleyin. Örneğin, bir sanal makineye bir işletim sistemi dağıtırken bu seçeneği kullanın. Varsayılan olarak, bu ayar **BitLocker 'ın ön sağlamasını** yap adımı için etkinleştirilmiştir. Bu adım, bir TPM veya başlatılmamış TPM olmadan bir cihazda başarısız olur. Sürüm 2006 ' den başlayarak, cihazda işlevsel TPM yoksa, görev sırası altyapısı Smsts. log dosyasına bir uyarı kaydeder ve durum iletisi 11912 ' yi gönderir.



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Yayın durumu deposu

Durum geçiş noktasına yakalama veya geri yükleme eyleminin tamamlandığını bildirmek için bu adımı kullanın. Bu adımı, **durum deposu iste**, **Kullanıcı durumunu yakala**ve **Kullanıcı durumunu geri yükle** adımlarını birlikte kullanın. Bir durum geçiş noktası ve Kullanıcı Durumu Taşıma Aracı (USMT) kullanarak Kullanıcı durumu verilerini geçirmek için bu adımları kullanın.  

İşletim sistemlerini dağıttığınızda kullanıcı durumunu yönetme hakkında daha fazla bilgi için bkz. [Manage user State](../get-started/manage-user-state.md).  

Kullanıcı durumunu *yakalamak* için bir durum geçiş noktasına erişim Istemek üzere **durum depolama iste** adımını kullanırsanız, bu adım durum geçiş noktasına yakalama işleminin tamamlandığını bildirir. Ardından durum geçiş noktası, Kullanıcı durumu verilerini geri yükleme için kullanılabilir olarak işaretler. Durum geçiş noktası, yalnızca geri yükleme bilgisayarının salt okuma erişimi olması için Kullanıcı durumu verileri için erişim denetimi izinlerini ayarlar.  

Kullanıcı durumunu *geri yüklemek* için bir durum geçiş noktasına erişim Istemek üzere **durum depolama iste** adımını kullanırsanız, bu adım durum geçiş noktasına geri yükleme işleminin tamamlandığını bildirir. Durum geçiş noktası daha sonra yapılandırılan veri saklama ayarlarını etkinleştirir.  

> [!IMPORTANT]  
> **Durum depolama** ve **yayın durumu deposu** adımları arasındaki herhangi bir adım Için **hata durumunda devam et** seçeneğini belirleyin. Her **Istek durum deposu** adımının eşleşen bir **yayın durumu deposu** adımı olmalıdır.  

Bu adım yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Kullanıcı durumu**' nu seçin ve **durum deposunu serbest bırak**' ı seçin.

### <a name="variables-for-release-state-store"></a>Yayın durumu deposu için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>Yayın durumu deposu için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore)
- [New-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore)
- [Remove-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore)
- [Set-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore)

### <a name="properties-for-release-state-store"></a>Yayın durumu deposunun özellikleri

Bu adım, **Özellikler** sekmesinde herhangi bir ayar gerektirmez.



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> Durum depolama alanını iste

Durumu yakalama veya geri yükleme sırasında bir durum geçiş noktasına erişim istemek için bu adımı kullanın.  

İşletim sistemlerini dağıttığınızda kullanıcı durumunu yönetme hakkında daha fazla bilgi için bkz. [Manage user State](../get-started/manage-user-state.md).  

Bu adımı, **durum depolama alanını serbest bırak**, **Kullanıcı durumunu yakala**ve **Kullanıcı durumu adımlarını geri yükle** ile birlikte kullanın. Bir durum geçiş noktası ve Kullanıcı Durumu Taşıma Aracı (USMT) kullanarak bilgisayar durumunu geçirmek için bu adımları kullanın.  

> [!NOTE]  
> Yeni bir durum geçiş noktası oluştururken, Kullanıcı durumu depolaması bir saate kadar kullanılabilir değildir. Kullanılabilirliği hızlandırmak için durum geçiş noktasındaki özellik ayarlarını bir site denetim dosyası güncelleştirmesini tetiklemek için ayarlayın.  

Bu adım, çevrimdışı USMT için tam işletim sisteminde ve Windows PE 'de çalışır.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Kullanıcı durumu**' nu seçin ve **durum deposu iste**' yi seçin.

### <a name="variables-for-request-state-store"></a>Istek durumu deposu için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>Istek durumu deposu için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore)
- [New-CMTSStepRequestStateStore](/powershell/module/configurationmanager/New-CMTSStepRequestStateStore)
- [Remove-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore)
- [Set-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore)

### <a name="properties-for-request-state-store"></a>Istek durumu deposu özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="capture-state-from-the-computer"></a>Durumu bilgisayardan yakala

Durum geçiş noktası ayarlarında yapılandırıldığı şekilde en düşük gereksinimleri karşılayan bir durum geçiş noktası bulun. Örneğin, **en fazla istemci sayısı** ve **minimum boş disk alanı miktarı**. Bu seçenek, durum geçişi sırasında yeterli alanın kullanılabilir olmasını garanti etmez. Bu seçenek, bir bilgisayardan Kullanıcı durumunu ve ayarlarını yakalama amacıyla durum geçiş noktasına erişim ister.  

Configuration Manager sitesinde birden çok etkin durum geçiş noktası varsa, bu adım kullanılabilir disk alanına sahip bir durum geçiş noktası bulur. Görev dizisi, bir durum geçiş noktaları listesi için yönetim noktasını sorgular ve ardından en düşük gereksinimleri karşılayan bir tane bulana kadar her birini değerlendirir.  

#### <a name="restore-state-from-another-computer"></a>Başka bir bilgisayardan durumu geri yükle

Daha önce yakalanan Kullanıcı durumu ve ayarlarını bir hedef bilgisayara geri yüklemek için bir durum geçiş noktasına erişim isteyin.  

Birden fazla durum geçiş noktası varsa, bu adım hedef bilgisayarın durumuna sahip durum geçiş noktasını bulur.  

#### <a name="number-of-retries"></a>Yeniden deneme sayısı

Bu adımın başarısız olmadan önce uygun bir durum geçiş noktası bulmayı deneme sayısı.  

#### <a name="retry-delay-in-seconds"></a>Yeniden deneme bekleme süresi (saniye)

Görev dizisi adımının yeniden denemeler arasında bekleyeceği saniye cinsinden zaman.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Bilgisayar hesabı bir durum deposuna bağlanamazsa, ağ erişim hesabını kullanın.

Görev sırası, bilgisayar hesabı kullanılarak durum geçiş noktasına erişebağlanamazsa, bağlanmak için ağ erişim hesabı kimlik bilgilerini kullanır. Diğer bilgisayarlar depolanan duruma erişmek için ağ erişim hesabını kullanabileceğinden Bu seçenek daha az güvenlidir. Hedef bilgisayar etki alanına katılmamışsa, bu seçenek gerekli olabilir.  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> Bilgisayarı yeniden Başlat

Görev sırasını çalıştıran bilgisayarı yeniden başlatmak için bu adımı kullanın. Yeniden başlatmadan sonra, bilgisayar otomatik olarak görev dizisindeki bir sonraki adımla devam eder.  

Bu adım, tam işletim sisteminde veya Windows PE 'de çalıştırılabilir.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **Bilgisayarı yeniden Başlat**' ı seçin.

### <a name="variables-for-restart-computer"></a>Bilgisayarı yeniden Başlat için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>Bilgisayarı yeniden başlatma için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](/powershell/module/configurationmanager/get-cmtsstepreboot)
- [New-CMTSStepReboot](/powershell/module/configurationmanager/new-cmtsstepreboot)
- [Remove-CMTSStepReboot](/powershell/module/configurationmanager/remove-cmtsstepreboot)
- [Set-CMTSStepReboot](/powershell/module/configurationmanager/set-cmtsstepreboot)

### <a name="properties-for-restart-computer"></a>Bilgisayarı yeniden Başlat için Özellikler

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>Bu görev dizisine atanan önyükleme görüntüsü

Hedef bilgisayarın görev dizisine atanan önyükleme görüntüsünü kullanması için bu seçeneği belirleyin. Görev dizisi, Windows PE 'de sonraki adımları çalıştırmak için önyükleme görüntüsünü kullanır.  

#### <a name="the-currently-installed-default-operating-system"></a>Şu anda yüklü varsayılan işletim sistemi

Hedef bilgisayarın yüklü işletim sisteminde yeniden başlatılması için bu seçeneği belirleyin.  

#### <a name="notify-the-user-before-restarting"></a>Yeniden başlatmadan önce kullanıcıyı uyar

Hedef bilgisayar yeniden başlatılmadan önce kullanıcıya bir bildirim göstermek için bu seçeneği belirleyin. Adım bu seçeneği varsayılan olarak seçer.  

#### <a name="notification-message"></a>Bildirim iletisi

Hedef bilgisayar yeniden başlatılmadan önce kullanıcıya görüntülenecek bir bildirim iletisi girin.  

#### <a name="message-display-time-out"></a>İleti görüntüleme zaman aşımı

Hedef bilgisayar yeniden başlatılmadan önceki saniye cinsinden süreyi belirtin. Varsayılan değer 60 saniyedir.  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Kullanıcı durumunu geri yükle

Kullanıcı durumunu ve ayarlarını hedef bilgisayara geri yüklemek üzere Kullanıcı Durumu Taşıma Aracı (USMT) başlatmak için bu adımı kullanın. Bu adımı, **Kullanıcı durumunu yakala** adımla birlikte kullanırsınız.  

İşletim sistemlerini dağıttığınızda kullanıcı durumunu yönetme hakkında daha fazla bilgi için bkz. [Manage user State](../get-started/manage-user-state.md).  

Durum ayarlarını bir durum geçiş noktasıyla kaydetmek veya geri yüklemek için durum **depolama iste** ve **durum depolamayı serbest bırak** adımları ile bu adımı kullanın. Bu seçenek, Configuration Manager oluşturup yöneten bir şifreleme anahtarı kullanarak USMT durum deposunun her zaman şifresini çözer.  

**Kullanıcı durumunu geri yükle** adımı, en sık kullanılan USMT seçeneklerinin sınırlı bir alt kümesinde denetim sağlar. **OSDMigrateAdditionalRestoreOptions** değişkeniyle ek komut satırı seçenekleri belirtin.  

> [!IMPORTANT]  
> Bu adımı bir işletim sistemi dağıtımı senaryosuyla ilgisi olmayan bir amaç için kullanıyorsanız, [Bilgisayarı yeniden Başlat](#BKMK_RestartComputer) adımını **Kullanıcı durumunu geri yükle** adımından hemen sonra ekleyin.  

Bu adım yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **Kullanıcı durumu**' nu seçin ve **Kullanıcı durumunu geri yükle**' yi seçin.

### <a name="variables-for-restore-user-state"></a>Kullanıcı durumunu geri yükle değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>Kullanıcı durumunu geri yükle için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState)
- [New-CMTSStepRestoreUserState](/powershell/module/configurationmanager/New-CMTSStepRestoreUserState)
- [Remove-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState)
- [Set-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState)

### <a name="properties-for-restore-user-state"></a>Kullanıcı durumunu geri yükle özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="user-state-migration-tool-package"></a>Kullanıcı durumu taşıma aracı paketi

Bu adımın kullanılacağı USMT sürümünü içeren paketi belirtin. Bu paket bir program gerektirmez. Adım çalıştığında, görev sırası belirtilen paketteki USMT sürümünü kullanır. USMT 'nin 32-bit veya 64 bit sürümünü içeren bir paket belirtin. USMT mimarisi, görev dizisinin durumu geri yüklendiği işletim sisteminin mimarisine bağlıdır.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Standart seçeneklere sahip tüm yakalanan kullanıcı profillerini geri yükle

Standart seçeneklere sahip yakalanan kullanıcı profillerini geri yükler. USMT 'nin geri yüklediği seçenekleri özelleştirmek için **Kullanıcı profili yakalamayı özelleştir**' i seçin.  

#### <a name="customize-how-user-profiles-are-restored"></a>Kullanıcı profillerinin nasıl geri yükleneceğini özelleştirin

Hedef bilgisayara geri yüklemek istediğiniz dosyaları özelleştirmenizi sağlar. Kullanıcı profillerini geri yüklemek için kullanmak istediğiniz USMT paketindeki yapılandırma dosyalarını belirtmek için **dosyalar** ' ı seçin. Bir yapılandırma dosyası eklemek **için dosya adı kutusuna dosyanın** adını girin ve **Ekle**' yi seçin. Dosyalar bölmesi, USMT 'nin kullandığı yapılandırma dosyalarını listeler. Belirttiğiniz. xml dosyası, USMT 'nin hangi kullanıcı dosyası tarafından geri yükleneceği tanımlar.  

#### <a name="restore-local-computer-user-profiles"></a>Yerel bilgisayar kullanıcı profillerini geri yükle

Yerel bilgisayar kullanıcı profillerini geri yükler. Bu profiller etki alanı kullanıcıları için değildir. Geri yüklenen yerel kullanıcı hesaplarına yeni parolalar atayın. USMT özgün parolaları geçiremez. Yeni parolayı **Parola** kutusuna girin ve **Parolayı Onayla** kutusunda onaylayın.  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Bazı dosyalar geri yüklenemezse devam et

USMT bazı dosyaları geri yüklemeseler bile Kullanıcı durumu ve ayarlarını geri yüklemeye devam eder. Adım bu seçeneği varsayılan olarak sunar. Bu seçeneği devre dışı bırakırsanız ve USMT dosyaları geri yüklerken hatalarla karşılaşırsa, bu adım hemen başarısız olur. USMT tüm dosyaları geri almaz.

#### <a name="enable-verbose-logging"></a>Ayrıntılı günlük kaydını etkinleştir

Daha ayrıntılı günlük dosyası bilgileri oluşturmak için bu seçeneği etkinleştirin. Durum geri yüklenirken, görev sırası varsayılan olarak görev dizisi günlük klasöründe **LoadState. log** ' u oluşturur `%WinDir%\ccm\logs` .  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> Komut satırını Çalıştır

Belirtilen komut satırını çalıştırmak için bu adımı kullanın.  

Çalıştırılan komut aşağıdaki ölçütlere uymalıdır:  

- Bu masaüstü ile etkileşimde bulunmamalıdır. Komutun sessizce veya katılımsız modda çalışması gerekir.  

- Kendi başına bir yeniden başlatma işlemi gerçekleştirmemelidir. Komutun standart yeniden başlatma kodu olan 3010 kullanılarak yeniden başlatma istemesi gerekir. Bu davranış, görev dizisinin yeniden başlatmayı doğru bir şekilde işlemesini sağlar. Komut bir 3010 çıkış kodu getirmezse, görev sırası altyapısı bilgisayarı yeniden başlatır. Yeniden başladıktan sonra görev dizisi otomatik olarak devam eder.

Bu adım tam işletim sisteminde veya Windows PE 'de çalıştırılabilir.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **komut satırını Çalıştır**' ı seçin.

### <a name="variables-for-run-command-line"></a>Komut satırı çalıştırma değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [Osddonotlogcommand](task-sequence-variables.md#OSDDoNotLogCommand) (sürüm 1902 ' den başlayarak)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (sürüm 2002 ' den başlayarak)<!-- 5573175 -->
- [Başlangıç](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>Çalıştır komut satırı için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](/powershell/module/configurationmanager/get-cmtsstepruncommandline)
- [New-CMTSStepRunCommandLine](/powershell/module/configurationmanager/new-cmtsstepruncommandline)
- [Remove-CMTSStepRunCommandLine](/powershell/module/configurationmanager/remove-cmtsstepruncommandline)
- [Set-CMTSStepRunCommandLine](/powershell/module/configurationmanager/set-cmtsstepruncommandline)

### <a name="properties-for-run-command-line"></a>Komut satırı çalıştırma özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="command-line"></a>Komut satırı

Görev dizisinin çalıştırıldığı komut satırını belirtir. Bu alan gereklidir. Dosya adı uzantılarını ekleyin, örneğin. vbs ve. exe. Tüm gerekli ayar dosyalarını ve komut satırı seçeneklerini dahil edin.  

Dosya adı uzantısını belirtmezseniz, Configuration Manager. com,. exe ve. bat ' yi dener. Dosya adının bir yürütülebilir tür olmayan bir uzantısı varsa Configuration Manager, yerel bir ilişkilendirme uygulamaya çalışır. Örneğin, komut satırı readme.gif ise, Configuration Manager. gif dosyalarını açmak için hedef bilgisayarda belirtilen uygulamayı başlatır.  

Örnekler:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Başarılı bir şekilde çalıştırmak için komut satırı eylemleriyle **cmd.exe/c** komutuyla önüne geçin. Bu eylemlere örnek olarak çıktı yeniden yönlendirme, boru ve kopyalama komutları dahildir.  

#### <a name="output-to-task-sequence-variable"></a>Çıkış görev dizisi değişkeni

<!--user story 4977616/bug 4798352-->

Sürüm 1910 ' den başlayarak, komut çıkışını özel bir görev dizisi değişkenine kaydedin.

> [!Note]  
> Configuration Manager Bu çıktıyı son 1000 karakterle sınırlandırır.

#### <a name="disable-64-bit-file-system-redirection"></a>64-bit dosya sistemi yeniden yönlendirmesini devre dışı bırak

Varsayılan olarak, 64 bit işletim sistemleri komut satırlarını çalıştırmak için WOW64 dosya sistemi yeniden yönlendiricisini kullanır. Bu davranış, işletim sistemi yürütülebilir dosyalarının ve kitaplıklarının 32 bitlik sürümlerini doğru bir şekilde bulmalıdır. WOW64 dosya sistemi yeniden yönlendiricisinin kullanımını devre dışı bırakmak için bu seçeneği belirleyin. Windows, işletim sistemi yürütülebilir dosyalarının ve kitaplıklarının yerel 64 bit sürümlerini kullanarak komutu çalıştırır. Bu seçenek, 32 bitlik bir IŞLETIM sisteminde çalışırken etkisizdir.  

#### <a name="start-in"></a>Başlangıç konumu

Program için yürütülebilir klasörü belirtir, en fazla 127 karakter olabilir. Bu klasör, hedef bilgisayar üzerindeki tam yol veya paketi içeren dağıtım noktası klasörüyle ilgili yol olabilir. Bu alan isteğe bağlıdır.  

Örnekler:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> **Göz at** düğmesi yerel bilgisayara dosya ve klasörler Için göz atar. Seçtiğiniz her şey hedef bilgisayarda da bulunmalıdır. Aynı konumda ve aynı dosya ve klasör adlarıyla bulunmalıdır.  

#### <a name="package"></a>Paket

Komut satırında hedef bilgisayarda zaten mevcut olmayan dosya veya programları belirttiğinizde, gerekli dosyaları içeren Configuration Manager paketini belirtmek için bu seçeneği belirleyin. Paket bir program gerektirmez. Belirtilen dosyalar hedef bilgisayarda mevcutsa bu seçenek gerekli değildir.  

#### <a name="time-out"></a>Zaman aşımı

Configuration Manager, komut satırının ne kadar süreyle çalışmasına izin verdiğini temsil eden bir değer belirtir. Bu değer bir dakika ile 999 dakika arasında olabilir. Varsayılan değer 15 dakikadır. Bu seçenek varsayılan olarak devre dışıdır.  

> [!IMPORTANT]  
> Belirtilen komutun başarıyla tamamlanabilmesi için yeterli zaman izni olmayan bir değer girerseniz, bu adım başarısız olur. Tüm görev sırası, adım veya grup koşullarına bağlı olarak başarısız olabilir. Zaman aşımı süresi dolarsa, Configuration Manager komut satırı işlemini sonlandırır.  

#### <a name="run-this-step-as-the-following-account"></a>Bu adımı şu hesap olarak çalıştır

Komut satırının yerel sistem hesabı dışında bir Windows Kullanıcı hesabı olarak çalıştırıldığını belirtir.  

> [!NOTE]  
> İşletim sistemini yükledikten sonra basit betikleri veya komutları başka bir hesapla çalıştırmak için öncelikle hesabı bilgisayara ekleyin. Ayrıca, Windows Installer gibi daha karmaşık programları çalıştırmak için Windows Kullanıcı profillerini geri yüklemeniz gerekebilir.  

#### <a name="account"></a>Hesap

Bu adımın komut satırını çalıştırmak için kullandığı Windows Kullanıcı hesabını belirtir. Komut satırı belirtilen hesabın izinleriyle çalışır. Yerel Kullanıcı veya etki alanı hesabını belirtmek için **Ayarla** ' yı seçin. Görev sırası farklı çalıştır hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Bu adım bir kullanıcı hesabı belirtir ve Windows PE 'de çalışırsa, eylem başarısız olur. Windows PE 'yi bir etki alanına birleştiremezsiniz. **Smsts. log** dosyası bu hatayı kaydeder.  

### <a name="options-for-run-command-line"></a>Komut satırı çalıştırma seçenekleri

Varsayılan seçeneklerin yanı sıra, bu görev dizisi adımının **Seçenekler** sekmesinde aşağıdaki ek ayarları yapılandırın:  

#### <a name="success-codes"></a>Başarı kodları

Betikten, adımın başarılı olarak değerlendirilmesi gereken diğer çıkış kodlarını dahil edin.



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> PowerShell betiğini Çalıştır

Belirtilen Windows PowerShell betiğini çalıştırmak için bu adımı kullanın.  

Betiğin aşağıdaki ölçütlere uyması gerekir:  

- Bu masaüstü ile etkileşimde bulunmamalıdır. Betiğin sessizce veya katılımsız modda çalışması gerekir.  

- Kendi başına bir yeniden başlatma işlemi gerçekleştirmemelidir. Sscript, standart yeniden başlatma kodu olan 3010 kullanılarak yeniden başlatma istemesi gerekir. Bu davranış, görev dizisinin yeniden başlatmayı doğru bir şekilde işlemesini sağlar. Betik bir 3010 çıkış kodu döndürmezse, görev sırası altyapısı bilgisayarı yeniden başlatır. Yeniden başladıktan sonra görev dizisi otomatik olarak devam eder.

Bu adım tam işletim sisteminde veya Windows PE 'de çalıştırılabilir. Bu adımı Windows PE 'de çalıştırmak için önyükleme görüntüsünde PowerShell 'i etkinleştirin. WinPE-PowerShell bileşenini, önyükleme görüntüsünün özelliklerinde **Isteğe bağlı bileşenler** sekmesinden etkinleştirin. Önyükleme görüntüsünü değiştirme hakkında daha fazla bilgi için bkz. [önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  

> [!NOTE]  
> PowerShell, Windows Embedded işletim sistemlerinde varsayılan olarak etkin değildir.  

> [!WARNING]
> Kötü amaçlı yazılımdan koruma yazılımı, Configuration Manager PowerShell Betiği Çalıştır görev dizisi adımından yanlışlıkla olayları tetikleyebiliriz. Kötü amaçlı yazılımdan koruma yazılımının bu betiklerin girişim olmadan çalışmasına izin vermesi için%windir%\temp\smstspowershellscripts hariç tutulması önerilir.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **PowerShell betiğini Çalıştır**' ı seçin.

### <a name="variables-for-run-powershell-script"></a>PowerShell betiği çalıştırma değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [Osdlogpowershellparameters](task-sequence-variables.md#OSDLogPowerShellParameters) (sürüm 1902 ' den başlayarak)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (sürüm 2002 ' den başlayarak)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>PowerShell betiği çalıştırma için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/get-cmtssteprunpowershellscript)
- [New-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/new-cmtssteprunpowershellscript)
- [Remove-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript)
- [Set-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/set-cmtssteprunpowershellscript)

> [!Note]  
> İmzalı PowerShell betiklerini Unicode biçiminde kullanın. Varsayılan olan ANSI biçimi, bu adımla çalışmaz.

### <a name="properties-for-run-powershell-script"></a>PowerShell betiğini Çalıştır özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="package"></a>Paket

PowerShell betiğini içeren Configuration Manager paketini belirtin. Bir paket birden çok PowerShell betiği içerebilir.  

#### <a name="script-name"></a>Betik adı

Çalıştırılacak PowerShell betiğinin adını belirtir. Bu alan gereklidir.  

#### <a name="enter-a-powershell-script"></a>Bir PowerShell betiği girin

<!-- 3556028 -->
Sürüm 1902 ' den başlayarak, bu adımda Windows PowerShell kodunu doğrudan girin. Bu özellik, komut dosyası ile bir paket oluşturmadan ve dağıtmadan, bir görev sırası sırasında PowerShell komutlarını çalıştırmanızı sağlar.

Bir komut dosyası eklediğinizde veya düzenlediğinizde, PowerShell betiği penceresi aşağıdaki eylemleri sağlar:  

- Betiği doğrudan Düzenle  

- Dosyadan var olan bir betiği aç  

- Configuration Manager ' de var olan bir onaylanan [betiğe](../../apps/deploy-use/create-deploy-scripts.md) gidin

> [!Important]  
> Bu yeni Configuration Manager özelliğinden yararlanmak için, siteyi güncelleştirdikten sonra da istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

#### <a name="parameters"></a>Parametreler

PowerShell betiğine geçirilen parametreleri belirtir. Bu parametreler, komut satırındaki PowerShell betiği parametreleriyle aynıdır.  

Windows PowerShell komut satırı için değil, betik tarafından kullanılan parametreler belirtin.  
Aşağıdaki örnek, geçerli parametreleri içerir:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

Aşağıdaki örnek, geçersiz parametreleri içerir. İlk iki öğe Windows PowerShell komut satırı parametreleridir (**-nologo** ve **-ExecutionPolicy Kısıtlamasız**). Betik bu parametreleri tüketmez.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Bir parametre değeri özel bir karakter içeriyorsa, değer etrafında tek tırnak işaretleri ( `'` ) kullanın. Çift tırnak işaretleri () kullanmak, `"` görev dizisi adımının parametreyi yanlış işlemesini sağlayabilir.

Örnek: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

Sürüm 2002 ' den başlayarak bu özelliği bir değişken olarak ayarlayın.<!-- 5690481 --> Örneğin, `%MyScriptVariable%` öğesini belirtirseniz, görev dizisi betiği çalıştırdığında, bu özel değişkenin değerini PowerShell komut satırına ekler.

#### <a name="powershell-execution-policy"></a>PowerShell yürütme ilkesi

Bilgisayarda çalıştırmaya izin verilen PowerShell betiklerini (varsa) saptayın. Aşağıdaki yürütme ilkelerinden birini seçin:  

- **AllSigned**: yalnızca güvenilir bir yayımcı tarafından imzalanan betikleri Çalıştır  

- **Tanımsız**: herhangi bir yürütme ilkesi tanımlama  

- **Bypass**: tüm yapılandırma dosyalarını yükler ve tüm betikleri Çalıştır. İnternet 'ten imzasız bir betiği indirdiğinizde, Windows PowerShell betiği çalıştırmadan önce izin istemez.  

> [!IMPORTANT]  
> PowerShell 1,0 tanımsız ve atlama yürütme ilkelerini desteklemez.  

#### <a name="output-to-task-sequence-variable"></a>Çıkış görev dizisi değişkeni

<!-- 3556028 -->
Sürüm 1902 ' den başlayarak, komut dosyası çıkışını özel bir görev dizisi değişkenine kaydedin.

> [!Note]  
> Sürüm 1910 ' den başlayarak, bu çıktıyı son 1000 karakterle sınırlar Configuration Manager.

Bu adım özelliğinin nasıl kullanılacağına ilişkin bir örnek için bkz. [değişkenlerin nasıl ayarlanacağı](using-task-sequence-variables.md#bkmk_run-ps).

#### <a name="start-in"></a>Başlangıç konumu

<!-- 3556028 -->
Sürüm 1902 ' den başlayarak, komut dosyası için en fazla 127 karaktere kadar başlangıç klasörünü belirtin. Bu klasör, hedef bilgisayar üzerindeki tam yol veya paketi içeren dağıtım noktası klasörüyle ilgili yol olabilir. Bu alan isteğe bağlıdır.  

> [!NOTE]  
> **Göz at** düğmesi yerel bilgisayara dosya ve klasörler Için göz atar. Seçtiğiniz her şey hedef bilgisayarda da bulunmalıdır. Aynı konumda ve aynı dosya ve klasör adlarıyla bulunmalıdır.  

#### <a name="time-out"></a>Zaman aşımı

<!-- 3556028 -->
Sürüm 1902 ' den başlayarak, Configuration Manager PowerShell betiğinin çalışmasına ne kadar süreyle izin verdiğini temsil eden bir değer belirtin. Bu değer bir dakika ile 999 dakika arasında olabilir. Varsayılan değer 15 dakikadır. Bu seçenek varsayılan olarak devre dışıdır.  

> [!IMPORTANT]  
> Belirtilen betiğin başarıyla tamamlanabilmesi için yeterli zaman izni olmayan bir değer girerseniz, bu adım başarısız olur. Tüm görev sırası, adım veya grup koşullarına bağlı olarak başarısız olabilir. Zaman aşımı süresi dolarsa, Configuration Manager PowerShell işlemini sonlandırır.  

#### <a name="run-this-step-as-the-following-account"></a>Bu adımı şu hesap olarak çalıştır

<!-- 3556028 -->
Sürüm 1902 ' den başlayarak, PowerShell betiğinin yerel sistem hesabı dışında bir Windows Kullanıcı hesabı olarak çalıştırılacağını belirtin.  

> [!NOTE]  
> İşletim sistemini yükledikten sonra basit betikleri veya komutları başka bir hesapla çalıştırmak için öncelikle hesabı bilgisayara ekleyin. Ayrıca, daha karmaşık eylemler çalıştırmak için Windows Kullanıcı profillerini geri yüklemeniz gerekebilir.  

#### <a name="account"></a>Hesap

<!-- 3556028 -->
Sürüm 1902 ' den başlayarak, bu adımın PowerShell betiğini çalıştırmak için kullandığı Windows Kullanıcı hesabını belirtin. Belirtilen hesap, sistemde bir yerel yönetici olmalıdır ve betik bu hesabın izinleriyle çalışır. Yerel Kullanıcı veya etki alanı hesabını belirtmek için **Ayarla** ' yı seçin. Görev sırası farklı çalıştır hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Bu adım bir kullanıcı hesabı belirtir ve Windows PE 'de çalışırsa, eylem başarısız olur. Windows PE 'yi bir etki alanına birleştiremezsiniz. **Smsts. log** dosyası bu hatayı kaydeder.  

### <a name="options-for-run-powershell-script"></a>PowerShell betiği çalıştırma seçenekleri

Varsayılan seçeneklerin yanı sıra, bu görev dizisi adımının **Seçenekler** sekmesinde aşağıdaki ek ayarları yapılandırın:  

#### <a name="success-codes"></a>Başarı kodları

<!-- 3556028 -->
Sürüm 1902 ' den başlayarak, komut dosyasındaki, adımın başarılı olarak değerlendirilmesi gereken diğer çıkış kodlarını ekleyin.



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> Görev sırasını Çalıştır

> [!Note]  
> Sürüm 1910 ' de, Configuration Manager Bu özelliği varsayılan olarak sunar. Sürüm 1906 veya önceki sürümlerde, bu isteğe bağlı özelliği varsayılan olarak etkinleştirmez Configuration Manager. Kullanmadan önce bu özelliği etkinleştirin. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).

Bu adım başka bir görev dizisi çalıştırır. Görev dizileri arasında bir üst-alt ilişkisi oluşturur. Alt görev dizileri ile daha modüler, yeniden kullanılabilir görev dizileri oluşturabilirsiniz.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **görev sırasını Çalıştır**' ı seçin.

### <a name="specifications-and-limitations-for-run-task-sequence"></a>Çalışma görev dizisi belirtimleri ve sınırlamaları

Bir görev dizisine bir alt görev sırası eklediğinizde aşağıdaki noktaları göz önünde bulundurun:  

- Üst ve alt görev dizileri, istemcinin çalıştırdığı tek bir ilkede etkili bir şekilde birleştirilir.  

- Ortam geneldir. Üst görev sırası bir değişken ayarlarsa ve sonra alt görev sırası bu değişkeni değiştirirse, en son değeri korur. Alt görev dizisi yeni bir değişken oluşturursa, üst görev dizisinin geri kalanı için kullanılabilir.  

- Durum iletileri, tek bir görev dizisi işlemi için normal başına gönderilir.  

- Görev sırası, bir alt görev sırası başlatıldığında, bu girişi yeni günlük girişleri ile **Smsts. log** dosyasına yazar.  

<!--the following points are from SCCMdocs issue #1079-->

- Önyükleme görüntüsü başvurusuyla bir görev sırası seçemezsiniz. Önyükleme görüntüsü gerektiren tüm dağıtımlar için, bunu üst görev sırasında belirtin.  

- Bir alt görev sırası devre dışıysa, dağıtım başarısız olur. Bu sınırlamaya geçici bir çözüm için **hata durumunda devam et** seçeneğini kullanamazsınız.  

- Bir alt görev sırası *yüksek etki*olarak kabul edilen adımlar içeriyorsa, yazılım merkezi bunu algılamaz ve yüksek etki bildirimini göstermez. Üst görev dizisinin özelliklerini, Kullanıcı bildirimi sekmesinde, **bunun yüksek etkili bir görev dizisi**olduğunu belirtmek için değiştirin.  

- Bir alt görev dizisinin paket başvurusu eksik ise, üst görev dizisinin görüntülenmesi bu durumu algılamaz. Üst görev sırasını düzenlerseniz, üst öğede değişiklik yaptığınızda alt görev sıralarında eksik başvuruları algılar.  

### <a name="cmdlets-for-run-task-sequence"></a>Çalıştır görev dizisi için cmdlet 'ler

Sürüm 1906 ' den başlayarak, bu adımı aşağıdaki PowerShell cmdlet 'leriyle yönetin:<!-- 2839943, SCCMDocs#1118 -->

- [Get-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/get-cmtsstepruntasksequence)
- [New-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/new-cmtsstepruntasksequence)
- [Remove-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/remove-cmtsstepruntasksequence)
- [Set-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/set-cmtsstepruntasksequence)

Daha fazla bilgi için bkz. [1906 sürüm notları-yeni cmdlet 'ler](/powershell/sccm/1906-release-notes#new-cmdlets).

### <a name="properties-for-run-task-sequence"></a>Çalışma görev dizisinin özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="select-task-sequence-to-run"></a>Çalıştırılacak görev sırasını seçin

Alt görev sırasını seçmek için **Araştır** ' ı seçin. **Görev sırası Seç** iletişim kutusu üst görev dizisini görüntülemez.



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Dinamik değişkenleri ayarla

Aşağıdaki eylemleri gerçekleştirmek için bu adımı kullanın:  

1. Bilgisayardan ve ortamından bilgi toplayın. Ardından, belirtilen görev dizisi değişkenlerini bilgilerle ayarlayın.  

2. Tanımlı kuralları değerlendirin. Doğru sonucunu veren kurallara göre görev dizisi değişkenlerini ayarlayın.  

Bu adım, tam işletim sisteminde veya Windows PE 'de çalıştırılabilir.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **dinamik değişkenleri ayarla**' yı seçin.

### <a name="variables-for-set-dynamic-variables"></a>Dinamik değişkenleri ayarla değişkenleri

Görev dizisi, aşağıdaki salt okunur görev dizisi değişkenlerini otomatik olarak ayarlar.  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>Dinamik değişkenleri ayarla için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable)
- [New-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable)
- [Remove-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable)
- [Set-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable)

### <a name="properties-for-set-dynamic-variables"></a>Dinamik değişkenleri ayarla özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="dynamic-rules-and-variables"></a>Dinamik kurallar ve değişkenler

Görev dizisinde kullanım için dinamik bir değişken ayarlamak üzere bir kural ekleyin. Ardından kuralda belirtilen her değişken için bir değer ayarlayın. Ayrıca, kural eklemeden bir veya daha fazla değişken ekleyin. Bir kural eklediğinizde, aşağıdaki kategorilerden birini seçin:  

- **Bilgisayar**: donanım varlık etıketı, UUID, seri numarası veya MAC adresi değerlerini değerlendirin. Gerektiğinde birden çok değer ayarlayın. Herhangi bir değer doğruysa, kural doğru olarak değerlendirilir. Örneğin, cihaz seri numarası 5892087 ve MAC adresi 22-a4-5A-13-78-26 ise aşağıdaki kural doğru olarak değerlendirilir:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Konum**: varsayılan ağ geçidi değerlerini değerlendir  

- **Marka ve model**: bir bilgisayarın marka ve model değerlerini değerlendirin. Kuralın doğru olarak değerlendirilebilmesi için hem marka hem de model doğru olarak değerlendirilmelidir.

    `*`Joker karakter karakteri olarak bir yıldız işareti () ve soru işareti ( `?` ) belirtin. Yıldız işareti birden çok karakterle eşleşir ve soru işareti tek bir karakterle eşleşir. Örneğin, dize hem hem `DELL*900?` de ile `DELL-ABC-9001` eşleşir `DELL9009` .  

- **Görev dizisi değişkeni**: değerlendirilecek bir görev dizisi değişkeni, koşul ve değer ekleyin. Değişken için ayarlanan değer belirtilen koşulu karşılıyorsa kural doğru olarak değerlendirilir.  

    True olarak değerlendirilen bir kural için ayarlanacak bir veya daha fazla değişken belirtin veya değişkenleri bir kural kullanmadan ayarlayın. Varolan bir değişken seçin veya özel bir değişken oluşturun.  

  - **Mevcut görev dizisi değişkenleri**: mevcut görev dizisi değişkenleri listesinden bir veya daha fazla değişken seçin. Dizi değişkenleri seçilecek şekilde kullanılamıyor.  

  - **Özel görev dizisi değişkenleri**: özel bir görev dizisi değişkeni tanımlayın. Ayrıca, mevcut bir görev dizisi değişkenini belirtebilirsiniz. Bu ayar, değişken dizileri mevcut görev dizisi değişkenleri listesinde olmadığından, **Osdaddapter**gibi mevcut bir değişken dizisini belirtmek için kullanışlıdır.  

Bir kural için değişkenleri seçtikten sonra her değişken için bir değer belirtin. Kural doğru olarak değerlendirildiğinde değişken belirtilen değere ayarlanır. Her değişken için, değişkenin değerini gizlemek için **Bu değeri gösterme** seçeneğini belirleyebilirsiniz. Varsayılan olarak, bazı mevcut değişkenler **OSDCaptureAccountPassword** değişkeni gibi değerleri gizler.  

> [!IMPORTANT]  
> **Dinamik değişkenleri ayarla** adımını içeren bir görev dizisini içeri aktardığınızda Configuration Manager, **Bu değeri gösterme**olarak işaretlenen tüm değişken değerlerini kaldırır. Görev sırasını içeri aktardıktan sonra dinamik değişkenin değerini yeniden girin.

**Bu değeri gösterme**seçeneğini kullandığınızda, değişkenin değeri görev sırası düzenleyicisinde gösterilmez. Görev sırası günlük dosyası (**Smsts. log**) veya görev sırası hata ayıklayıcı değişken değerini göstermez. Değişken, çalışma sırasında görev sırası tarafından hala kullanılıyor olabilir. Artık bu değişkenlerin gizli olmasını istemiyorsanız, önce bunları silin. Sonra değişkenleri gizleme seçeneğini seçmeden yeniden tanımlayın.  

> [!WARNING]  
> **Komut satırı** adımının komut satırını Çalıştır ' a değişkenler eklerseniz, görev sırası günlük dosyası değişken değerleri dahil olmak üzere tam komut satırını görüntüler. Potansiyel olarak gizli verilerin günlük dosyasında görünmesini engellemek için **Osddonotlogcommand** görev sırası değişkenini olarak ayarlayın `TRUE` .


## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Görev sırası değişkenini ayarla

Görev dizisiyle kullanılan bir değişkenin değerini ayarlamak için bu adımı kullanın.  

Bu adım, tam işletim sisteminde veya Windows PE 'de çalıştırılabilir.

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **genel**' i seçin ve **görev dizisi değişkenini ayarla**' yı seçin.

### <a name="variables-for-set-task-sequence-variable"></a>Görev dizisi değişkenini ayarla değişkenleri

Görev dizisi değişkenleri, görev dizisi eylemleri tarafından okunur ve bu eylemlerin davranışını belirtir. Belirli görev dizisi değişkenleri ve bunların nasıl kullanılacağı hakkında daha fazla bilgi için aşağıdaki makalelere bakın:  

- [Görev dizisi değişkenlerini kullanma](using-task-sequence-variables.md)  
- [Görev dizisi değişkenleri](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>Ayarla görev dizisi değişkeni için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](/powershell/module/configurationmanager/get-cmtsstepsetvariable)
- [New-CMTSStepSetVariable](/powershell/module/configurationmanager/new-cmtsstepsetvariable)
- [Remove-CMTSStepSetVariable](/powershell/module/configurationmanager/remove-cmtsstepsetvariable)
- [Set-CMTSStepSetVariable](/powershell/module/configurationmanager/set-cmtsstepsetvariable)

### <a name="properties-for-set-task-sequence-variable"></a>Görev dizisi değişkenini ayarla özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="task-sequence-variable"></a>Görev dizisi değişkeni

Bir görev dizisinin yerleşik veya eylem değişkeninin adını belirtin veya kendi Kullanıcı tanımlı değişken adınızı belirtin.  

#### <a name="do-not-display-this-value"></a>Bu değeri gösterme

<!--1358330-->
Görev sırası değişkenlerinde depolanan hassas verileri maskelemek için bu seçeneği etkinleştirin. Örneğin, bir parola belirtirken.

> [!NOTE]
> Bu seçeneği etkinleştirin ve sonra görev dizisi değişkeninin değerini ayarlayın. Aksi halde, değişken değeri, görev dizisi çalışırken beklenmeyen davranışlara neden olabilecek şekilde, sizin istediğiniz şekilde ayarlanamaz.<!--SCCMdocs issue #800-->

**Bu değeri gösterme**seçeneğini kullandığınızda, değişkenin değeri görev sırası düzenleyicisinde gösterilmez. Görev sırası günlük dosyası (**Smsts. log**) veya görev sırası hata ayıklayıcı değişken değerini göstermez. Değişken, çalışma sırasında görev sırası tarafından hala kullanılıyor olabilir. Artık bu değişkenin gizli olmasını istemiyorsanız, önce silin. Sonra, öğeyi gizleme seçeneğini seçmeden değişkeni yeniden tanımlayın.

> [!WARNING]
> **Komut satırı** adımının komut satırını Çalıştır ' a değişkenler eklerseniz, görev sırası günlük dosyası değişken değerleri dahil olmak üzere tam komut satırını görüntüler. Potansiyel olarak gizli verilerin günlük dosyasında görünmesini engellemek için **Osddonotlogcommand** görev sırası değişkenini olarak ayarlayın `TRUE` .<!-- 6963278 -->

#### <a name="value"></a>Değer  

Görev sırası, değişkeni bu değere ayarlar. Bu görev dizisi değişkenini söz dizimi ile başka bir görev dizisi değişkeninin değerine ayarlayın `%varname%` .  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Windows 'u ve ConfigMgr 'yi Kur

Windows PE 'den yeni işletim sistemine geçişi gerçekleştirmek için bu adımı kullanın. Bu görev dizisi adımı herhangi bir işletim sistemi dağıtımının gerekli bir parçasıdır. Configuration Manager istemcisini yeni işletim sistemine yükleyip görev dizisinin yeni IŞLETIM sisteminde yürütmeye devam etmesine hazırlar.  

Bu adım, görev dizisinin Windows PE 'den tam işletim sistemine geçişini sağlamaktan sorumludur. Bu geçiş nedeniyle, bu adım hem Windows PE 'de hem de tam işletim sisteminde çalışır. Ancak, geçiş Windows PE 'de başladığından, bu, yalnızca görev dizisinin Windows PE bölümü sırasında eklenebilir.  

Bu adım, `%WINDIR%` `%ProgramFiles%` Windows PE yükleme diziniyle ve gibi Sysprep. inf veya unattend.xml Dizin değişkenlerinin yerini alır `X:\Windows` . Görev sırası, bu ortam değişkenleri kullanılarak belirtilen değişkenleri yoksayar.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**, **görüntü**Seç ' i seçin ve **Windows 'u ve ConfigMgr 'yi ayarla**' yı seçin.

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Windows ve ConfigMgr kurulumu davranışları

Bu adım aşağıdaki eylemleri gerçekleştirir:  

#### <a name="preliminaries-windows-pe"></a>Başlangıç kuralları: Windows PE  

1. unattend.xml dosyadaki görev sırası değişkenlerini değiştirin.  

2. Configuration Manager istemcisini içeren paketi indirin. Paketi dağıtılan görüntüye ekleyin.  

#### <a name="set-up-windows"></a>Windows'u Kurma  

- Görüntü tabanlı yükleme  

    1. Varsa, görüntüde Configuration Manager istemcisini devre dışı bırakın. Diğer bir deyişle Configuration Manager istemci hizmeti için autostart 'ı devre dışı bırakın.  

    2. Dağıtılan işletim sistemini referans bilgisayarla aynı sürücü harfiyle başlatmak için dağıtılan görüntüdeki kayıt defterini güncelleştirin.  

    3. Dağıtılan işletim sistemine yeniden başlatın.  

    4. Windows Mini Kurulum, önceden belirtilen Sysprep. inf ' i veya tüm son kullanıcı etkileşimini gizlenen unattend.xml yanıt dosyasını kullanarak çalışır. Bir etki alanına katmak için **ağ ayarlarını uygula** adımını kullanırsanız, bu bilgiler yanıt dosyasında bulunur. Windows Mini Kurulum, bilgisayarı etki alanına birleştirir.  

- Setup.exe tabanlı yükleme. Normal Windows kurulum işlemi gerçekleştiren Setup.exe dosyasını çalıştırır:  

    1. **Işletim sistemini Uygula** adımında belirtilen işletim sistemi yükseltme paketini sabit disk sürücüsüne kopyalayın.  

    2. Yeni dağıtılan işletim sistemine yeniden başlatın.  

    3. Windows Mini Kurulum, önceden belirtilen Sysprep. inf veya tüm Kullanıcı arabirimi ayarlarını gizlenen unattend.xml yanıt dosyasını kullanarak çalışır. Bir etki alanına katmak için  **ağ ayarlarını uygula** adımını kullanırsanız, bu bilgiler yanıt dosyasında bulunur. Windows Mini Kurulum, bilgisayarı etki alanına birleştirir.  

#### <a name="set-up-the-configuration-manager-client"></a>Configuration Manager istemcisini ayarlama  

1. Windows mini kurulumu tamamlandıktan sonra görev dizisi, setupcomplete.cmd dosyasını kullanarak devam eder. Daha fazla bilgi için bkz. [Kurulum tamamlandıktan sonra betiği çalıştırma (SetupComplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).  

2. **Windows ayarlarını uygula** adımında seçilen seçeneğe bağlı olarak yerel yönetici hesabını etkinleştirin veya devre dışı bırakın.  

3. Configuration Manager istemcisini, daha önce indirilen paketi ve bu adımda belirtilen yükleme özelliklerini kullanarak yükleme. İstemci "sağlama modunda" yüklenir. Bu mod, istemci, görev dizisi tamamlanana kadar yeni ilke isteklerini işlemesini engeller. Daha fazla bilgi için bkz. [sağlama modu](provisioning-mode.md).  

4. İstemcinin tam olarak çalışır durumda olmasını bekleyin.  

#### <a name="the-step-completes"></a>Adım tamamlanır

Görev dizisi bir sonraki adımı çalıştırmaya devam eder.  

> [!Note]  
> Windows Grup ilkesi, görev sırası tamamlanana kadar normalde işlemez. Bu davranış, farklı Windows sürümleri arasında tutarlıdır. Görev sırası sırasında diğer özel eylemler, Grup İlkesi değerlendirmesini tetikleyebilir. İşlemlerin sırası hakkında daha fazla bilgi için bkz. [Kurulum tamamlandıktan sonra betiği çalıştırma (SetupComplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd). <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Windows ve ConfigMgr kurulumu için değişkenler

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Windows ve ConfigMgr kurulumu için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr)
- [New-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr)
- [Set-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr)

### <a name="properties-for-setup-windows-and-configmgr"></a>Windows ve ConfigMgr kurulum özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="client-package"></a>İstemci paketi

**Araştır**' ı seçin ve ardından bu adımla birlikte kullanılacak Configuration Manager istemci yükleme paketini seçin.  

#### <a name="use-pre-production-client-package-when-available"></a>Mevcut olduğunda ön üretim istemci paketini kullan

Kullanılabilir bir ön üretim istemci paketi varsa ve bilgisayar, pilot koleksiyonunun bir üyesiyse, görev sırası üretim istemci paketi yerine bu paketi kullanır. Üretim öncesi istemci, üretim ortamında test için daha yeni bir sürümdür. **Araştır**' ı seçin ve ardından bu adımla birlikte kullanılacak ön üretim istemcisi yükleme paketini seçin.  

#### <a name="installation-properties"></a>Yükleme Özellikleri

Görev sırası adımı otomatik olarak site atamasını ve varsayılan yapılandırmayı belirler. İstemcisini yüklerken kullanılacak ek yükleme özelliklerini belirtmek için bu alanı kullanın. Birden çok yükleme özelliği belirtmek için boşlukla ayırın.  

İstemci yüklemesi sırasında kullanılacak komut satırı seçeneklerini belirtin. Örneğin, `/skipprereq: silverlight.exe` CCMSetup.exe Microsoft Silverlight önkoşulu yüklememeyi bildirmek için yazın. CCMSetup.exe için kullanılabilir komut satırı seçenekleri hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../core/clients/deploy/about-client-installation-properties.md).  

Azure AD 'ye katılmış olan veya belirteç tabanlı kimlik doğrulaması kullanan bir internet tabanlı istemcide bir işletim sistemi dağıtımı görev dizisi çalıştırdığınızda, **Windows 'u ve ConfigMgr 'Yi Kur** adımında [CCMHOSTNAME](../../core/clients/deploy/about-client-installation-properties.md#ccmhostname) özelliğini belirtmeniz gerekir. Örneğin, `CCMHOSTNAME=OTTERFALLS.CLOUDAPP.NET/CCM_Proxy_MutualAuth/12345678907927939`.

### <a name="options-for-setup-windows-and-configmgr"></a>Windows ve ConfigMgr kurulum seçenekleri

> [!NOTE]  
> **Seçenekler** sekmesinde **hata durumunda devam et '** i etkinleştirmeyin. Bu adım sırasında bir hata oluşursa, bu ayarı etkinleştirip etkinleştirmeyeceğinizi değil, görev sırası başarısız olur.  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Işletim sistemini yükselt

Eski bir Windows sürümünü Windows 10 ' un daha yeni bir sürümüne yükseltmek için bu adımı kullanın.  

Bu görev dizisi adımı yalnızca tam işletim sisteminde çalışır. Windows PE 'de çalışmaz.  

Bu adımı görev sırası düzenleyicisine eklemek için **Ekle**' yi seçin, **görüntüler**' i seçin ve **işletim sistemini Yükselt**' i seçin.

> [!TIP]
> Windows 10, sürüm 1709 ' den başlayarak, medya birden çok sürümünü içerir. Bir görev dizisini bir işletim sistemi yükseltme paketi veya işletim sistemi görüntüsü kullanacak şekilde yapılandırdığınızda, [desteklenen bir sürüm](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)seçtiğinizden emin olun.  
>
> Kullanıcı görev dizisini yüklemeden önce geçerli bir işletim sistemi yükseltme paketini indirmek için içeriği önceden önbelleğe alma özelliğini kullanın. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../deploy-use/configure-precache-content.md).

### <a name="variables-for-upgrade-os"></a>İşletim sistemi yükseltme değişkenleri

Aşağıdaki görev dizisi değişkenlerini bu adımla kullanın:  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>İşletim sistemi yükseltme için cmdlet 'ler

Aşağıdaki PowerShell cmdlet 'leriyle bu adımı yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem)
- [New-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem)
- [Remove-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem)
- [Set-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem)

### <a name="properties-for-upgrade-os"></a>İşletim sistemi yükseltme özellikleri

Bu adımın **Özellikler** sekmesinde, bu bölümde açıklanan ayarları yapılandırın.  

#### <a name="upgrade-package"></a>Paketi yükselt

Yükseltme için kullanılacak Windows 10 işletim sistemi yükseltme paketini belirtmek için bu seçeneği belirleyin.  

#### <a name="source-path"></a>Kaynak yol

Windows Kurulumu kullandığı Windows 10 medyası için yerel veya ağ yolunu belirtir. Bu ayar Windows Kurulumu komut satırı seçeneğine karşılık gelir `/InstallFrom` .

Veya gibi bir değişken de belirtebilirsiniz `%MyContentPath%` `%DPC01%` . Kaynak yolu için bir değişken kullandığınızda, değerini görev dizisinde daha önce ayarlayın. Örneğin, işletim sistemi yükseltme paketi konumu için bir değişken belirtmek üzere [paket Içeriğini indir](#BKMK_DownloadPackageContent) adımını kullanın. Daha sonra bu değişkeni, bu adımın kaynak yolu için kullanın.  

#### <a name="edition"></a>Sürüm

İşletim sistemi ortamında yükseltme için kullanılacak sürümü belirtin.  

#### <a name="product-key"></a>Ürün anahtarı

Yükseltme işlemine uygulanacak ürün anahtarını belirtin.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Yükseltme sırasında Windows Kurulumu’na aşağıdaki sürücü içeriklerini sağlayın

Yükseltme işlemi sırasında hedef bilgisayara sürücü ekleyin. Sürücülerin Windows 10 ile uyumlu olmaları gerekir. Bu ayar Windows Kurulumu komut satırı seçeneğine karşılık gelir `/InstallDriver` . Daha fazla bilgi için bkz. [Windows kurulumu komut satırı seçenekleri](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers).

Aşağıdaki seçeneklerden birini belirtin:  

- **Sürücü paketi**: **Araştır** ' ı seçin ve listeden var olan bir sürücü paketini seçin.

- **Hazırlanan içerik**: sürücü içeriğinin konumunu belirtmek için bu seçeneği belirleyin. Yerel bir klasör, ağ konumu veya görev dizisi değişkeni belirtebilirsiniz. Kaynak yolu için bir değişken kullandığınızda, değerini görev dizisinde daha önce ayarlayın. Örneğin, [paket Içeriğini indir](task-sequence-steps.md#BKMK_DownloadPackageContent) adımını kullanarak.  

> [!TIP]
> Birden çok donanım türü için dinamik içeriğe sahip olmak istiyorsanız:
>
> - Donanım türleri ve ayrı sürücü içeriği için koşulları ile bu adımın birden çok örneğini kullanın.
>
> - [Paket Içeriğini indir](task-sequence-steps.md#BKMK_DownloadPackageContent) adımının birden çok örneğini kullanın. İçeriği ortak bir konuma yerleştirin ve ardından **hazırlanan içerik** seçeneğini kullanın. Bu yöntemin avantajı, görev dizisinin tek bir **yükseltme işletim sistemi** adımını içerir.

#### <a name="time-out-minutes"></a>Zaman aşımı (dakika)

Configuration Manager Bu adımın başarısız olması için geçmesi gereken dakika sayısını belirtin. Windows Kurulumu işlemeyi durdurup sonlandırmazsa Bu seçenek faydalıdır.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Windows Kurulumu uyumluluk taramasını yükseltmeyi başlatmadan gerçekleştir

Yükseltme işlemini başlatmadan Windows Kurulumu uyumluluk taramasını gerçekleştirin. Bu ayar Windows Kurulumu komut satırı seçeneğine karşılık gelir `/Compat ScanOnly` . Tüm işletim sistemi yükseltme paketini bu seçenekle dağıtın.

<!--SCCMDocs-pr issue 2812-->
Bu seçeneği etkinleştirdiğinizde, bu adım Configuration Manager istemcisini sağlama moduna yerleştirmez. Windows Kurulumu arka planda sessizce çalışır ve istemci normal şekilde çalışmaya devam eder. Daha fazla bilgi için bkz. [sağlama modu](provisioning-mode.md).

Kurulum, tarama sonucunda bir çıkış kodu döndürür. Aşağıdaki tabloda daha yaygın çıkış kodları verilmiştir:  

|Çıkış kodu|Ayrıntılar|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Uyumluluk sorunu yok ("başarılı").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|İşlem yapılabilir uyumluluk sorunları.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Seçili geçiş seçeneği kullanılamıyor. Örneğin, Enterprise sürümünden Professional sürümüne yükseltme.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Windows 10 için uygun değil.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Yeterli boş disk alanı yok.|  

Bu parametre hakkında daha fazla bilgi için bkz. [Windows kurulumu komut satırı seçenekleri](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Atlanabilir tüm uyumluluk iletilerini yok say

Kurulumun, hiçbir türlü uyumluluk iletilerini yoksayarak yüklemeyi tamamladığını belirtir. Bu ayar Windows Kurulumu komut satırı seçeneğine karşılık gelir `/Compat IgnoreWarning` .  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Windows Kurulumu’nu Windows Update ile dinamik olarak güncelleştir

Kurulum 'u arama, indirme ve yükleme gibi dinamik güncelleştirme işlemleri gerçekleştirmek için etkinleştirin. Bu ayar Windows Kurulumu komut satırı seçeneğine karşılık gelir `/DynamicUpdate` . Bu ayar Configuration Manager yazılım güncelleştirmeleriyle uyumlu değildir. Tek başına Windows Server Update Services (WSUS) veya Iş için Windows Update güncelleştirmeleri yönetirken bu seçeneği etkinleştirin.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>İlkeyi geçersiz kıl ve varsayılan Microsoft Update kullan

Dinamik güncelleştirme işlemlerini çalıştırmak için yerel ilkeyi gerçek zamanlı olarak geçici olarak geçersiz kılın. Bilgisayar Windows Update güncelleştirmeleri alır.
