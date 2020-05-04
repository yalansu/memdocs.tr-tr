---
title: Uzaktan denetim güvenlik gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager 'de uzaktan denetim için güvenlik ve gizlilik bilgilerini alın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 83631b331030f9648c3e88a2e101a013cfa0e98f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715105"
---
# <a name="security-and-privacy-for-remote-control-in-configuration-manager"></a>Configuration Manager 'de uzaktan denetim için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager içindeki uzaktan denetim için güvenlik ve gizlilik bilgilerini içerir.  

##  <a name="security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Uzak denetimde güvenlik için en iyi yöntemler  
 İstemci bilgisayarları uzaktan denetim aracılığıyla yönetirken aşağıdaki en iyi güvenlik yöntemlerini kullanın.  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Uzak bir bilgisayara bağlanırken, Kerberos kimlik doğrulaması yerine NTLM kullanılırsa devam etmeyin.|Configuration Manager, uzaktan denetim oturumunun kimlik doğrulamasının Kerberos yerine NTLM kullanarak yapıldığını algıladığında, uzak bilgisayarın kimliğinin doğrulanamadığını bildiren bir istem görürsünüz. Uzaktan denetim oturumuna devam etmeyin. NTLM kimlik doğrulaması, Kerberos’tan daha zayıf bir kimlik doğrulama protokolüdür ve yeniden yürütme ve kimliğe bürünmeye karşı savunmasızdır.|  
|Uzaktan denetim görüntüleyicisinde Pano paylaşımını etkinleştirmeyin.|Pano, yürütülebilir dosya ve metin gibi nesneleri destekler ve uzaktan denetim oturumu sırasında ana bilgisayardaki kullanıcı tarafından, kaynak bilgisayarda bir programı çalıştırmak için kullanılabilir.|  
|Bir bilgisayarı uzaktan yönetirken, ayrıcalıklı hesaplar için parola girmeyin.|Klavye girişini gözlemleyen yazılımlar parolayı ele geçirebilir. Ayrıca, istemci bilgisayarda çalıştırılan program, uzaktan denetim kullanıcısının varsaydığı program değilse parola, program tarafından ele geçiriliyor olabilir. Gerekli olduğunda, hesapları ve parolaları son kullanıcının girmesi gerekir.|  
|Uzaktan denetim oturumu sırasında klavyeyi ve fareyi kilitleyin.|Configuration Manager, uzaktan denetim bağlantısının sonlandırıldığını algılarsa, bir kullanıcının açık uzaktan denetim oturumu denetimini ele geçirmesine olanak sağlamak için, Configuration Manager otomatik olarak klavyeyi ve fareyi kilitler. Ancak, bu algılama hemen gerçekleşmeyebilir veya uzaktan denetim hizmeti sonlandırıldıysa gerçekleşmez.<br /><br /> **ConfigMgr Uzaktan Denetim** penceresindeki **Uzak Klavyeyi ve Fareyi Kilitle** eylemini seçin.|  
|Kullanıcıların Yazılım Merkezi'nde uzaktan denetim ayarlarını yapılandırmasına izin vermeyin.|**Kullanıcılar, Yazılım Merkezi'nde ilkeleri veya bildirim ayarlarını değiştirebilir** istemci ayarı kullanıcıların gözetlenmesine yol açabileceğinden, bu ayarı etkinleştirmeyin. Bir kullanıcı tarafından değişirse, aynı makinede farklı bir kullanıcının uzaktan görüntülenmesine izin verebilir. <br /><br />**Bu ayar, oturum açmış kullanıcı için değil, bilgisayar içindir**.|  
|**Etki Alanı** Windows Güvenlik Duvarı profilini etkinleştirin.|**İstemci Güvenlik duvarı özel durum profillerinde uzaktan denetimi etkinleştir** istemci ayarını etkinleştirin ve sonra intranet bilgisayarlar için **Etki Alanı** Windows Güvenlik Duvarı’nı seçin.|  
|Uzaktan denetim oturumu sırasında oturumunuzu kapatıp farklı bir kullanıcı olarak oturum açarsanız, uzaktan denetim oturumunun bağlantısını kesmeden önce bu oturumu kapattığınızdan emin olun.|Bu senaryoda açtığınız oturumu kapatmazsanız uzaktan denetim oturumu açık kalır.|  
|Kullanıcılara yerel yönetici hakları vermeyin.|Yerel yönetici hakları verdiğinizde kullanıcılar, uzaktan denetim oturumunun yönetimini ele geçirebilir veya kimlik bilgilerinizi riske atabilir.|  
|Uzaktan Yardım ayarlarını yapılandırmak için grup ilkesi ya da Configuration Manager kullanın, ancak ikisini birden kullanmayın.|Configuration Manager ve grup ilkesi kullanarak uzaktan yardım ayarlarında yapılandırma değişiklikleri yapabilirsiniz. Grup İlkesi, istemci üzerinde yenilendiğinde varsayılan olarak, yalnızca sunucu üzerinde değiştirilmiş olan ilkeleri değiştirerek işlemi optimize eder. Configuration Manager, yerel güvenlik ilkesindeki ayarları değiştirir ve bu, grup ilkesi güncelleştirme zorlanmadıkça üzerine yazılmayabilir.<br /><br /> İlkenin her iki yerde de ayarlanması tutarsız sonuçlara neden olabilir. Uzaktan Yardım ayarlarınızı yapılandırmak için aşağıdaki yöntemlerden birini seçin.|  
|**Kullanıcıya Uzaktan Denetim izni sor**istemci ayarını etkinleştirin.|Kullanıcıdan uzaktan denetim oturumunu onaylamasını isteyen bu istemci ayarını aşmanın yolları vardır, ancak kullanıcıların gizli görevler üzerinde çalışırken gözetlenme olasılığını azaltmak için bu ayarı etkinleştirin.<br /><br /> Ek olarak, uzaktan denetim oturumu sırasında görüntülenen hesap adını doğrulamaları ve hesabın yetkisiz olduğundan şüphelenmeleri durumunda oturumun bağlantısını kesmeleri konusunda kullanıcıları bilgilendirin.|  
|İzin Verilen Görüntüleyiciler listesini sınırlayın.|Bir kullanıcının uzaktan denetimi kullanabilmesi için yerel yönetici hakları gerekli değildir.|  

### <a name="security-issues-for-remote-control"></a>Uzaktan denetimde güvenlik sorunları  
 İstemci bilgisayarlarını Uzaktan Denetim aracılığıyla yönetmek, aşağıdaki gibi güvenlik sorunlarına neden olur:  

-   Uzaktan denetim denetleme iletilerini güvenilir olarak değerlendirmeyin.  

     Uzaktan denetim oturumu başlatır ve sonra alternatif kimlik bilgilerini kullanarak oturum açarsanız, denetim iletileri alternatif kimlik bilgilerini kullanan hesap tarafından değil özgün hesap tarafından gönderilir.  

     Configuration Manager konsolunu yüklemeden önce uzak denetim için ikili dosyaları kopyalarsanız ve sonra komut isteminde uzaktan denetimi çalıştırmak için denetim iletileri gönderilmez.  

##  <a name="privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Uzaktan denetimde gizlilik bilgileri  
 Uzaktan denetim, Configuration Manager istemci bilgisayarlarda etkin oturumları görüntülemenize ve bu bilgisayarlarda depolanan tüm bilgileri görüntülemenize olanak sağlar. Uzaktan denetim varsayılan olarak etkin değildir.  

 Uzaktan denetim, oturum başlamadan önce açık bir uyarı sağlayıp kullanıcıdan izin alacak şekilde yapılandırılabilmekle birlikte kullanıcının izni veya bilgisi olmadan da kullanıcıları izleyebilir. Uzaktan denetimde veya Tam Denetim’de değişiklik yapılmasını engellemek için Yalnızca Görüntüle erişim düzeyini yapılandırabilirsiniz. Kullanıcıların bilgisayarlarına bağlanan kişiyi tanımasına yardımcı olmak için, uzaktan denetim oturumunda bağlantı yöneticisinin hesabı görüntülenir.  

 Varsayılan olarak, Configuration Manager yerel Yöneticiler grubuna uzaktan denetim izinleri verir.  

 Uzaktan denetimi yapılandırmadan önce gizlilik gereksinimlerinizi göz önünde bulundurun.  
