---
title: Koleksiyonlar giriş
titleSuffix: Configuration Manager
description: Configuration Manager içindeki koleksiyonları kullanmaya giriş alın.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0665c6378ac81d6f6f254501760647048ce66b0b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714356"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Configuration Manager içindeki koleksiyonlara giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Koleksiyonlar, kaynakları yönetilebilir birimlerde düzenlemenize yardımcı olur. İstemci yönetimi ihtiyaçlarınızı karşılamak için Koleksiyonlar oluşturabilir ve aynı anda birden çok kaynak üzerinde işlem yapabilirsiniz. 

Çoğu yönetim görevi bir veya daha fazla koleksiyon kullanır veya gerektirir. Tüm sistemlerin yerleşik koleksiyonunu kullanabilseniz de, yönetim görevleri için kullanmak en iyi yöntem değildir. Bir görev için cihazları veya kullanıcıları daha özel olarak tanımlamak üzere özel Koleksiyonlar oluşturun.  

 Yerleşik ve özel koleksiyonlar, Configuration Manager konsolundaki **varlıklar ve uyum** çalışma alanındaki **Kullanıcı koleksiyonları** ve **Cihaz Koleksiyonları** düğümlerinde görünür.  

 En son görüntülediğiniz koleksiyonlar **Kullanıcılar** düğümünde ve **varlıklar ve uyum** çalışma alanındaki **cihazlar** düğümünde görünür.  

Koleksiyon kullanımına ilişkin bazı örnekler aşağıda verilmiştir:  

|İşlem|Örnek|  
|---------|-------|  
|Kaynakları gruplandırma|Kaynakları, kuruluşunuzun hiyerarşisine göre gruplandıran koleksiyonlar oluşturabilirsiniz.<br /><br /> Örneğin, "Londra genel merkezleri" Active Directory kuruluş birimi 'nde (OU) tüm bilgisayarların bir koleksiyonunu oluşturabilirsiniz. Bu tür bir koleksiyonun nasıl oluşturulacağı hakkında daha fazla bilgi için bkz. [koleksiyonları oluşturma](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Bu koleksiyonu, Endpoint Protection ayarlarını yapılandırma, cihaz güç yönetimi ayarlarını yapılandırma veya Configuration Manager istemcisini yükleme gibi işlemler için kullanabilirsiniz.|  
|Uygulama dağıtımı|Microsoft Office 2013 yüklü olmayan tüm bilgisayarların bir koleksiyonunu oluşturabilir ve ardından bu koleksiyondaki tüm bilgisayarlara dağıtabilirsiniz.<br /><br /> Bu görevi gerçekleştirmek için uygulama gereksinimlerini de kullanabilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager ile uygulama oluşturma](../../../../apps/deploy-use/create-applications.md).|  
|[İstemci ayarlarını yönetme](../../../../core/clients/deploy/about-client-settings.md)|Configuration Manager’daki varsayılan istemci ayarları tüm cihazlar ve tüm kullanıcılar için geçerli olsa da, bir cihaz koleksiyonu veya kullanıcı koleksiyonu için geçerli olan özel istemci ayarları oluşturabilirsiniz.<br /><br /> Örneğin, bir kaç cihazda Uzaktan denetimin kullanılabilir olmasını istiyorsanız, varsayılan istemci ayarlarını uzaktan denetime izin verecek şekilde yapılandırın ve ardından uzaktan denetime izin verilmeyen özel istemci ayarlarını yapılandırın ve bunları olağanüstü istemciler koleksiyonuna dağıtın. |  
|[Güç yönetimi](../power/introduction-to-power-management.md)|Her koleksiyon için belirli güç ayarlarını yapılandırabilirsiniz.|  
|[Rol tabanlı yönetim](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Configuration Manager konsolundaki çeşitli işlevlere hangi kullanıcı gruplarının erişebileceğini denetlemek için koleksiyonları kullanın.|  
|[Bakım Pencereleri](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Bakım pencereleri ile bir cihaz koleksiyonu üyelerinde çeşitli Configuration Manager işlemleri gerçekleştirilebilse de bir zaman aralığı tanımlayabilirsiniz. |  


## <a name="collection-types-in-configuration-manager"></a>Configuration Manager'da koleksiyon türleri  
 Configuration Manager ortak işlemler için yerleşik koleksiyonlara sahiptir ve ayrıca özel koleksiyonlar da oluşturabilirsiniz.   

### <a name="built-in-collections"></a>Yerleşik koleksiyonlar  
 Varsayılan olarak, Configuration Manager değiştirilemeyen aşağıdaki koleksiyonları içerir.  

|**Koleksiyon adı**|Açıklama|  
|-------------------------|-----------------|  
|**Tüm Kullanıcı Grupları**|Active Directory Güvenlik Grubu Saptama kullanılarak bulunan kullanıcı gruplarını içerir.|  
|**Tüm Kullanıcılar**|Active Directory Kullanıcı Saptama kullanılarak bulunan kullanıcıları içerir.|  
|**Tüm Kullanıcılar ve Kullanıcı Grupları**|Tüm Kullanıcılar ve Tüm Kullanıcı Grupları koleksiyonlarını içerir. Bu koleksiyon, en büyük Kullanıcı ve Kullanıcı grubu kaynakları kapsamını içerir.|  
|**Tüm Masaüstü ve Sunucu İstemcileri**|Configuration Manager istemcisinin yüklü olduğu sunucu ve masaüstü cihazlarını içerir. Üyelik, Sinyal Saptama tarafından korunur.|  
|**Tüm Mobil Cihazlar**|Configuration Manager tarafından yönetilen mobil cihazları içerir. Üyelik bir siteye başarıyla atanan veya Exchange Server bağlayıcısı tarafından bulunan mobil cihazlarla sınırlıdır.|  
|**Tüm Sistemler**|Tüm masaüstü ve sunucu Istemcileri, tüm mobil cihazlar, tüm bilinmeyen bilgisayarlar koleksiyonlarını ve Microsoft Intune tarafından kaydedilen tüm mobil cihazları içerir. Bu koleksiyon, en büyük cihaz kaynakları kapsamını içerir.|  
|**Tüm Bilinmeyen Bilgisayarlar**|Birden çok bilgisayar platformu için genel bilgisayar kayıtlarını içerir. Görev dizisi ve PXE önyüklemesi, önyüklenebilir medya veya önhazırlığı yapılmış medya kullanarak bir işletim sistemini dağıtmak için bu koleksiyonu kullanabilirsiniz.|  

### <a name="custom-collections"></a>Özel koleksiyonlar  
 Configuration Manager içinde özel bir koleksiyon oluşturduğunuzda bu koleksiyonun üyeliği, [koleksiyonlar oluşturma](../../../../core/clients/manage/collections/create-collections.md)bölümünde açıklandığı gibi bir veya daha fazla koleksiyon kuralına göre belirlenir. 

