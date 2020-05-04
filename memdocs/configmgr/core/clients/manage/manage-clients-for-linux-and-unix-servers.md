---
title: Linux ve UNIX istemcilerini yönetme
titleSuffix: Configuration Manager
description: İstemcileri Configuration Manager Linux ve UNIX sunucularında yönetin.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710646"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Configuration Manager 'da Linux ve UNIX sunucuları için istemcileri yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Linux ve UNIX sunucularını Configuration Manager ile yönetirken, sunucuları yönetmeye yardımcı olmak için koleksiyonları, bakım pencerelerini ve istemci ayarlarını yapılandırabilirsiniz. Ayrıca, Linux ve UNIX için Configuration Manager istemcisi bir kullanıcı arabirimine sahip olmasa da, istemciyi istemci ilkesi için el ile yoklamaya zorlayabilirsiniz.

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Linux ve UNIX sunucu gruplarını, diğer istemci türlerini yönetmek için koleksiyonları kullandığınız şekilde yönetmek için koleksiyonları kullanın. Koleksiyonlar doğrudan üyelik koleksiyonları veya sorgu tabanlı koleksiyonlar olabilir. Sorgu tabanlı koleksiyonlar, istemci işletim sistemlerini, donanım yapılandırmasını veya site veritabanında depolanan istemciyle ilgili diğer ayrıntıları belirler. Örneğin, aşağıdaki ayarları yönetmek için Linux ve UNIX sunucularını içeren koleksiyonları kullanabilirsiniz:  

- İstemci ayarları  

- Yazılım dağıtımları  

- Bakım pencerelerini zorlama  

  Bir Linux veya UNIX istemcisini işletim sistemine veya dağıtımına göre belirleyebilmeniz için önce istemciden [donanım envanterini](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) toplamanız gerekir.  

  Donanım envanteri için varsayılan istemci ayarları bir istemci bilgisayarın işletim sistemi hakkında bilgiler içerir. Bir Linux veya UNIX sunucusunun işletim sistemini tanımlamak için **İşletim Sistemi** sınıfının **Caption** özelliğini kullanabilirsiniz.  

  Linux ve UNIX için Configuration Manager istemcisini çalıştıran bilgisayarlarla ilgili ayrıntıları Configuration Manager konsolundaki **varlıklar ve uyum** çalışma alanının **cihazlar** düğümünde görüntüleyebilirsiniz. Configuration Manager konsolunun **varlık ve uyum** çalışma alanında, her bilgisayarın işletim sisteminin adını **işletim sistemi** sütununda görüntüleyebilirsiniz.  

  Varsayılan olarak, Linux ve UNIX sunucuları **Tüm Sistemler** koleksiyonunun üyeleridir. Yalnızca Linux ve UNIX sunucularını veya bunların bir alt kümesini içeren özel koleksiyonlar oluşturmanızı öneririz. Özel Koleksiyonlar, bir dağıtımın başarısını doğru bir şekilde ölçmenize olanak tanımak için yazılım dağıtma veya bilgisayar gibi gruplara istemci ayarları atama gibi işlemleri yönetmenizi sağlar.   

  Linux ve UNIX sunucuları için özel bir koleksiyon oluşturduğunuzda, İşletim Sistemi özniteliği için Resim Yazısı özniteliğini içeren üyelik kuralı sorgularını dahil edin. Koleksiyon oluşturma hakkında daha fazla bilgi için bkz. [koleksiyonları oluşturma](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a>Linux ve UNIX sunucuları için bakım pencereleri  
 Linux ve UNIX sunucuları için Configuration Manager istemcisi [bakım pencerelerinin](../../../core/clients/manage/collections/use-maintenance-windows.md)kullanımını destekler. Bu destek, Windows tabanlı istemcilerden değişmemiştir.  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a>Linux ve UNIX sunucuları için istemci ayarları  
 Linux ve UNIX sunucuları için uygulanan [istemci ayarlarını](../../../core/clients/deploy/configure-client-settings.md) , diğer istemcilerin ayarlarını yapılandırdığınız şekilde yapılandırabilirsiniz.  

 Varsayılan olarak, **Varsayılan İstemci Aracısı Ayarları** Linux ve UNIX sunucuları için geçerlidir. Ayrıca, özel istemci ayarları oluşturabilir ve bunları belirli istemci koleksiyonlarına dağıtabilirsiniz.  

 Yalnızca Linux ve UNIX istemciler için geçerli olan başka istemci ayarları yoktur. Ancak, Linux ve UNIX istemcileri için uygulanan varsayılan istemci ayarları vardır. Linux ve UNIX için istemcisi yalnızca desteklediği işlevlere yönelik ayarları uygular.  

 Örneğin, Linux ve UNIX için istemcisi uzaktan denetimi desteklemediğinden, uzaktan denetim ayarlarını sağlayan ve yapılandıran özel bir istemci cihaz ayarı, Linux ve UNIX sunucuları tarafından yok sayılır.  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a>Linux ve UNIX sunucuları için bilgisayar ilkesi  
 Linux ve UNIX sunucuları için istemcisi, istenen konfigürasyonlar hakkında bilgi edinmek ve dağıtımları denetlemek için kendi sitesini bilgisayar ilkesi için düzenli olarak yoklar.  

 Ayrıca, bir Linux veya UNIX sunucusu üzerindeki istemciyi bilgisayar ilkesini hemen yoklamaya zorlayabilirsiniz. Bunu yapmak için sunucuda **kök** kimlik bilgilerini kullanarak şu komutu çalıştırın: **/opt/microsoft/configmgr/bin/ccmexec-rs ilkesi**  

 Bilgisayar ilkesi yoklama ayrıntıları, paylaşılan **scxcm.log**istemci günlük dosyasına girilir.  

> [!NOTE]  
>  Linux ve UNIX için Configuration Manager istemcisi, kullanıcı ilkesini hiç istemez veya işlemez.  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a>Linux ve UNIX için istemcideki sertifikaları yönetme  
 Linux ve UNIX için istemciyi yükledikten sonra **certutil** aracını kullanarak istemciyi yeni bir PKI sertifikasıyla güncelleştirebilir ve yeni bir Sertifika İptal listesini (CRL) içe aktarabilirsiniz. Linux ve UNIX için istemcisini yüklediğinizde bu araç ' de yer `/opt/microsoft/configmgr/bin/certutil`alır. 

 Sertifikaları yönetmek için her bir istemcide certutil aracını aşağıdaki seçeneklerden biriyle çalıştırın:  

|Seçenek|Daha fazla bilgi|  
|------------|----------------------|  
|`importPFX`|Şu anda bir istemci tarafından kullanılan sertifikanın yerine bir sertifika belirtmek için bu seçeneği kullanın.<br /><br /> Kullandığınızda `-importPFX`, PKCS # 12 dosyasıyla ilişkili parolayı sağlamak `-password` için komut satırı parametresini de kullanmanız gerekir.<br /><br /> Ek `-rootcerts` kök sertifika gereksinimlerini belirtmek için kullanın.<br /><br /> Örnek: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Yönetim sunucusu üzerinde bulunan site sunucusu imzalama sertifikasını güncelleştirmek için bu seçeneği kullanın.<br /><br /> Örnek: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|İstemci üzerindeki CRL’yi bir veya daha fazla CRL dosya yoluyla güncelleştirmek için bu seçeneği kullanın.<br /><br /> Örnek: `certutil -importcrl <comma separated CRL file paths>`|  
