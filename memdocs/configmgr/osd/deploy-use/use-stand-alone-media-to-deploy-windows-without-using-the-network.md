---
title: Windows dağıtmak için tek başına medya kullanma
titleSuffix: Configuration Manager
description: Bilgisayar yenileme, yüklemeyi veya yükseltme seçeneği olarak bant genişliğinin sınırlı olduğu Windows 'u dağıtmak için Configuration Manager 'de tek başına medya kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724226"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Windows’u ağ kullanmadan dağıtmak için tek başına ortam kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager tek başına medya, bir işletim sistemini bir bilgisayara dağıtmak için gereken her şeyi içerir. Buna önyükleme görüntüsü, işletim sistemi görüntüsü ve uygulamalar, sürücüler vb. dahil olmak üzere işletim sistemini yüklemeye ilişkin görev dizisi dahildir. Tek başına medya dağıtımları, aşağıdaki durumlarda işletim sistemlerini dağıtmanızı sağlar:  

-   Bir işletim sistemi görüntüsünün veya başka büyük paketlerin ağ üzerinden kopyalanması uygun olmayan ortamlarda.  

-   Ağ bağlantısı olmayan veya düşük bant genişliğine sahip ağ bağlantısı olan ortamlarda.  

Aşağıdaki işletim sistemi dağıtım senaryolarında tek başına medya kullanabilirsiniz:  

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)  

- [Windows’u en yeni sürüme yükseltme](upgrade-windows-to-the-latest-version.md)  

  İşletim sistemi dağıtım senaryolarından birindeki adımları tamamlayın ve ardından aşağıdaki bölümleri kullanarak tek başına medyayı hazırlayın ve oluşturun.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Tek başına medya kullanılırken görev dizisi eylemleri desteklenmez.  
 Desteklenen işletim sistemi dağıtım senaryolarından birindeki adımları tamamladıysanız, işletim sisteminin dağıtılması ya da güncelleştirilmesi için görev dizisi oluşturulmuştur ve ilgili tüm içerikler bir dağıtım noktasına dağıtılmıştır. Tek başına medya kullandığınızda aşağıdaki eylemler görev dizisinde desteklenmez:  

-   Görev dizisindeki Sürücüleri Otomatik Uygulama adımı. Cihaz kataloğundaki cihaz sürücülerinin otomatik uygulanması desteklenmez, ancak belirli bir sürücü kümesinin Windows Kurulumu’nda kullanılabilir olması için Cihaz Paketi Uygulama adımı seçebilirsiniz.  

-   Yazılım güncelleştirmelerinin yüklenmesi.  

-   Bir işletim sistemini dağıtmadan önce yazılımı yükleme.  

-   Kullanıcı cihaz benzeşimini desteklemek için kullanıcılar ile hedef bilgisayarın ilişkilendirilmesi.  

-   Dinamik paketler, Paket Yükle göreviyle yüklenir.  

-   Dinamik uygulama, Uygulama Yükle göreviyle yüklenir.  

> [!NOTE]  
>  Bir işletim sistemini dağıtmaya yönelik görev diziniz [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) adımını içeriyorsa ve tek başına medyayı merkezi yönetim sitesinde oluşturursanız bir hata oluşabilir. Yönetim merkezi sitesi, görev dizisinin yürütülmesi sırasında yazılım dağıtım aracısını etkinleştirmek için gerekli olan istemci yapılandırma ilkelerine sahip değildir. CreateTsMedia.log dosyasında aşağıdaki hata görünebilir:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  **Paketi Yükle** adımı içeren tek başına medya için, tek başına medyayı yazılım dağıtım aracısı etkinleştirilmiş bir birincil sitede oluşturmanız veya görev dizisindeki [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_RunCommandLine) adımından sonra ve birinci [Paketi Yükle](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) adımından önce **Run Command Line** adımı eklemeniz gerekir. **Komut Satırını Çalıştır** adımı, ilk Paketi Yükle adımı çalışmadan önce yazılım dağıtım aracısını etkinleştirmek için bir WMIC komutu çalıştırır. **Komut Satırını Çalıştır** görev dizisi adımınızda aşağıdakileri kullanabilirsiniz:  
>   
>  **Komut Satırı**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma  
 İşletim sistemi dağıtım işlemini başlatmak üzere tek başına medya kullandığınızda, işletim sistemini medya tarafından kullanılabilir hale getirmek için dağıtımı yapılandırmanız gerekir. Bu yapılandırmayı Yazılım Dağıtma Sihirbazı’nın **Dağıtım Ayarları** sayfasında veya dağıtımın özelliklerindeki **Dağıtım Ayarları** sekmesinde yapabilirsiniz.  **Aşağıdakiler için kullanılabilir yap** ayarı için aşağıdakilerden birini yapılandırın:  

-   **Configuration Manager istemcileri, medya ve PXE**  

-   **Yalnızca medya ve PXE**  

-   **Yalnızca medya ve PXE (gizli)**  

## <a name="create-the-stand-alone-media"></a>Tek başına medya oluşturma  
 Tek başına medyanın bir USB flash sürücü veya CD/DVD seti olduğunu belirtebilirsiniz. Medyayı başlatacak bilgisayar önyüklenebilir sürücü olarak belirlediğiniz seçeneği desteklemelidir. Daha fazla bilgi için bkz. [tek başına medya oluşturma](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Tek başına medyadan işletim sistemini yükleme  
 Tek başına medyayı bilgisayarda önyüklenebilir bir sürücüye yerleştirin ve ardından çalıştırarak işletim sistemini yükleyin.  
