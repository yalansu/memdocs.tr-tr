---
title: Sertifika profili önkoşulları
titleSuffix: Configuration Manager
description: Configuration Manager ' deki sertifika profilleri ve bunların dış bağımlılıkları ve ürün bağımlılıkları hakkında bilgi edinin.
ms.date: 12/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d072d6399675633dc80c826ce40edf7af56de25
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700455"
---
# <a name="prerequisites-for-certificate-profiles-in-configuration-manager"></a>Configuration Manager 'de sertifika profilleri için Önkoşullar

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Configuration Manager Sertifika profillerinin dış bağımlılıkları ve ürün içinde bağımlılıkları vardır.  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager için Dış Bağımlılıklar  

|Bağımlılık|Daha fazla bilgi|  
|----------------|----------------------|  
|Active Directory Sertifika Hizmetleri (AD CS) çalıştıran bir kurumsal yayımlama sertifika yetkilisi (CA).<br /><br /> Sertifikaları iptal etmek için hiyerarşinin en üstündeki site sunucusunun bilgisayar hesabı, Configuration Manager’da bir sertifika profili tarafından kullanılan her sertifika şablonu için *Sertifika Yayımlama ve Yönetme* haklarını gerektirir. Alternatif olarak, bu sertifika yetkilisi tarafından kullanılan tüm sertifika şablonlarında izin vermek üzere Sertifika Yöneticisi izinleri verin<br /><br /> Sertifika istekleri için yönetici onayı desteklenir. Ancak, sertifikaları vermek için kullanılan sertifika şablonlarının, sertifika konusu için **Istekte sağlama** için yapılandırılması gerekir, böylece Configuration Manager bu değeri otomatik olarak sağlayabilir.|Active Directory Sertifika Hizmetleri hakkında daha fazla bilgi için bkz. [Active Directory Sertifika hizmetlerine genel bakış](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740(v=ws.11)).|  
|Doğrulamak için PowerShell betiğini kullanın ve gerekirse, ağ cihazı kayıt hizmeti (NDES) rol hizmeti ve Configuration Manager sertifika kayıt noktası için önkoşulları yükler. <br /><br />|readme_crp.txt yönerge dosyası ConfigMgrInstallDir\cd.latest\SMSSETUP\POLICYMODULE\X64. içinde bulunur<br /><br />Test-NDES-CRP-Prereqs.ps1 PowerShell betiği, yönergeleriyle aynı dizinde. <br /><br /> PowerShell betiğinin NDES sunucusunda yerel olarak çalıştırılması gerekir.|
|Windows Server 2012 R2 üzerinde çalışan Active Directory Sertifika Hizmetleri için ağ cihazı kayıt hizmeti (NDES) rol hizmeti.<br /><br /> Bunlara ek olarak:<br /><br /> İstemciyle Ağ Aygıtı Kayıt Hizmeti arasındaki iletişimler için TCP 443 (HTTPS için) veya TCP 80 (HTTP için) dışındaki bağlantı noktası numaraları desteklenmez.<br /><br /> Ağ Aygıtı Kayıt Hizmeti'ni çalıştıran sunucu, yayımlayan CA'dan farklı bir sunucuda olmalıdır.|Configuration Manager, Basit Sertifika Kayıt Protokolü (SCEP) istekleri oluşturmak ve doğrulamak için Windows Server 2012 R2 'deki ağ aygıtı kayıt hizmeti ile iletişim kurar.<br /><br /> Microsoft Intune tarafından yönetilen mobil cihazlar gibi Internet 'ten bağlanan kullanıcı ve cihazlara sertifika yayımlayacaksanız, bu cihazların ağ cihazı kayıt hizmeti 'ni Internet 'ten çalıştıran sunucuya erişebilmesi gerekir. örneğin, sunucuyu bir çevre ağına (buna askersiz bölge ve denetimli alt ağ da denir) yükleyin.<br /><br /> Ağ Aygıtı Kayıt Hizmeti çalıştıran sunucu ile veren CA arasında güvenlik duvarı varsa, güvenlik duvarını iki sunucu arasında iletişim trafiğine (DCOM) izin verecek şekilde yapılandırmanız gerekir. Bu güvenlik duvarı gereksinimi Ayrıca, Configuration Manager site sunucusunu ve veren CA 'yı çalıştıran sunucu için de geçerlidir; böylece Configuration Manager sertifikaları iptal edebilir.<br /><br /> Ağ aygıtı Kayıt Hizmeti SSL gerektirecek şekilde yapılandırıldıysa, bağlanan cihazların sunucu sertifikasını doğrulamak için sertifika iptal listesine (CRL) erişebilmesini sağlamak en iyi güvenlik yöntemidir.<br /><br /> Ağ aygıtı kayıt hizmeti hakkında daha fazla bilgi için bkz. [ağ cihazı kayıt hizmeti Ile Ilke modülü kullanma](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016(v=ws.11)).|  
|Bir PKI istemci sertifikası ve dışarı aktarılan bir kök CA sertifikası.|Bu sertifika, Configuration Manager için ağ cihazı kayıt hizmeti 'ni çalıştıran sunucunun kimliğini doğrular.<br /><br /> Daha fazla bilgi için bkz. [Configuration Manager Için PKI sertifikası gereksinimleri](../../core/plan-design/network/pki-certificate-requirements.md).|  
|Desteklenen cihaz işletim sistemleri.|Windows 8.1, Windows RT 8,1 ve Windows 10 çalıştıran cihazlara sertifika profilleri dağıtabilirsiniz.|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager Bağımlılıkları  

|Bağımlılık|Daha fazla bilgi|  
|----------------|----------------------|  
|Sertifika kayıt noktası site sistemi rolü|Sertifika profillerini kullanabilmeniz için önce, sertifika kayıt noktası site sistemi rolünü yüklemeniz gerekir. Bu rol Configuration Manager veritabanı, Configuration Manager site sunucusu ve Configuration Manager Ilkesi modülü ile iletişim kurar.<br /><br /> Bu site sistemi rolü için sistem gereksinimleri ve rolün hiyerarşide yükleneceği yer hakkında daha fazla bilgi için, [desteklenen Configuration Manager için yapılandırma](../../core/plan-design/configs/supported-configurations.md) makalesinde bulunan **site sistem gereksinimleri** bölümüne bakın.<br /><br /> Sertifika kayıt noktası, ağ cihazı kayıt hizmeti 'ni çalıştıran sunucuya yüklenmemelidir.|  
|Active Directory Sertifika Hizmetleri için ağ cihazı kayıt hizmeti rol hizmetini çalıştıran sunucuda yüklü Configuration Manager Ilke modülü|Sertifika profillerini dağıtmak için Configuration Manager Ilkesi modülünü yüklemelisiniz. Bu ilke modülünü Configuration Manager yükleme medyasında bulabilirsiniz.|  
|Bulma verileri|Sertifika konusu ve konu alternatif adı değerleri Configuration Manager tarafından sağlanır ve bulma işleminden toplanan bilgilerden alınır:<br /><br /> Kullanıcı sertifikaları için: Active Directory Kullanıcı Saptama<br /><br /> Bilgisayar sertifikaları için: Active Directory Sistem Saptama ve Ağ Bulma|  
|Sertifika profillerini yönetmek için belirli güvenlik izinleri|Sertifika profilleri, Wi-Fi profilleri ve VPN profilleri gibi şirket kaynaklarına erişim ayarlarını yönetmek için aşağıdaki güvenlik izinlerine sahip olmanız gerekir:<br /><br /> Sertifika profillerinin uyarılarını ve raporlarını görüntüleyip yönetmek için: **Uyarılar**nesnesi için **Oluştur**, **Sil**, **Değiştir**, **Raporu Değiştir**, **Oku** ve **Raporu Çalıştır** .<br /><br /> Sertifika profilleri oluşturup yönetmek için: **sertifika profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .<br /><br /> Wi-Fi, sertifika ve VPN profili dağıtımlarını yönetmek için: **Koleksiyon**nesnesi izinleri için **Yapılandırma İlkeleri Dağıt**, **İstemci Durumu Uyarısını Değiştir**, **Oku** ve **Kaynağı Oku** .<br /><br /> Tüm yapılandırma ilkelerini yönetmek için: **yapılandırma ilkesi** nesnesi için **Oluştur**, **Sil**, **Değiştir**, **Oku**ve **güvenlik kapsamını ayarla** .<br /><br /> Sertifika profilleriyle ilgili sorguları çalıştırmak için: **Sorgu** nesnesi için **Oku** izni.<br /><br /> Configuration Manager konsolundaki sertifika profilleri bilgilerini görüntülemek için: **site** nesnesi için **Oku** izni.<br /><br /> Sertifika profillerinin durum iletilerini görüntülemek için: **Durum İletileri** nesnesi için **Oku** izni.<br /><br /> Güvenilen CA sertifika profili oluşturup değiştirmek için: **GÜVENILIR CA sertifika profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .<br /><br /> VPN profilleri oluşturup yönetmek için: **VPN profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .<br /><br /> Wi-Fi profilleri oluşturup yönetmek için: **Wi-Fi profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .<br /><br /> **Şirket kaynağı Erişim Yöneticisi** güvenlik rolü, Configuration Manager sertifika profillerini yönetmek için gereken bu izinleri içerir. Daha fazla bilgi için [güvenlik yapılandırma](../../core/plan-design/security/configure-security.md) makalesindeki **rol tabanlı yönetimi yapılandırma** bölümüne bakın.|