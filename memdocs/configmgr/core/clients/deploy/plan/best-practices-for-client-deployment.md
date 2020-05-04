---
title: İstemci dağıtımı en iyi uygulamaları
titleSuffix: Configuration Manager
description: Configuration Manager 'de istemci dağıtımı için en iyi yöntemleri alın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713341"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Configuration Manager 'de istemci dağıtımı için en iyi uygulamalar

*Uygulama hedefi: Configuration Manager (geçerli dal)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Active Directory bilgisayarları için yazılım güncelleştirme tabanlı istemci yüklemesi kullanma  
 Bu istemci dağıtım yöntemi mevcut Windows teknolojilerini kullanır, Active Directory altyapınızla tümleştirilir, Configuration Manager en az yapılandırmayı gerektirir, güvenlik duvarları için en kolay yapılandırma ve en güvenli seçenektir. Grup ilkesi yapılandırmasına yönelik güvenlik gruplarını ve WMI filtresini kullanarak, hangi bilgisayarların Configuration Manager istemcisini yükleyeceğini denetlemek için çok fazla esneklik de vardır.  

 Daha fazla bilgi için bkz. [Yazılım Güncelleştirmesi Tabanlı Yükleme Kullanarak Configuration Manager İstemcileri Yükleme](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>CCMSetup'ı komut satırı seçenekleri olmadan çalıştırabilmek için Active Directory şemasını genişletme ve siteyi yayımlama  
 Configuration Manager için Active Directory şemasını uzatdığınızda ve site Active Directory Domain Services yayımlandığında, çoğu istemci yükleme özelliği Active Directory Domain Services olarak yayımlanır. Bir bilgisayar bu istemci yükleme özelliklerini bulabiliyorsa, Configuration Manager istemci dağıtımı sırasında onları kullanabilir. Bu bilgiler otomatik olarak oluşturulduğundan, yükleme özelliklerinin elle girilmesiyle ilişkili insan hatası riski ortadan kalkar.  

 Daha fazla bilgi için bkz. [Active Directory Domain Services yayımlanan istemci yükleme özellikleri hakkında](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>CPU kullanımını yönetmek için aşamalı bir dağıtım kullanın  
 İstemcilerin aşamalı olarak dağıtımını kullanarak site sunucusundaki CPU işleme gereksinimlerinin etkisini en aza indirin. Diğer hizmetlerin gün içinde daha fazla bant genişliğine sahip olması için istemcileri iş saatleri dışında dağıtın ve bilgisayar yavaşanıyorsa veya bir yeniden başlatma gerektiriyorsa kullanıcılar kesintiye uğramaz.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Ana istemci dağıtımınız tamamlandıktan sonra otomatik yükseltmeyi etkinleştirme  
 [Otomatik istemci yükseltmeleri](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) , ana istemci yükleme yönteminizin kaçırılmış olabilecek az sayıda istemci bilgisayarını, belki de çevrimdışı olduğu için yükseltmek istediğinizde yararlıdır. 

> [!NOTE]  
>  Configuration Manager performans iyileştirmeleri, Otomatik yükseltmeleri birincil istemci yükseltme yöntemi olarak kullanmanıza olanak tanıyabilir. Bununla birlikte, performans, hiyerarşi altyapınıza, örneğin istemcilerin sayısına bağlı olur.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>İstemciyi client.msi özellikleriyle yüklüyorsanız SMSMP ve FSP kullanma  
 SMSMP özelliği, istemcinin iletişim kuracağı ilk yönetim noktasını belirtir ve Active Directory Etki Alanı Hizmetleri, DNS ve WINS gibi hizmet bulma çözümlerine bağımlığı ortadan kaldırır.  

 İstemci yükleme ve atamasını izleyebilmek ve olası iletişim sorunlarını belirleyebilmek için FSP özelliğini kullanın ve geri dönüş durum noktası yükleyin.  

 Bu seçenekler hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>İstemcileri yüklemeden önce istemci dil paketlerini yükler  
İstemciyi dağıtmadan önce istemci dil paketlerini yüklemenizi öneririz. İstemcileri yükledikten sonra bir sitede [istemci dil paketlerini](../../../../core/servers/deploy/install/language-packs.md) (ek dilleri etkinleştirmek için) yüklerseniz, istemcileri bu dilleri kullanabilmeniz için yeniden yüklemeniz gerekir. Mobil aygıt istemcileri için mobil cihazı silip yeniden kaydetmeniz gerekir.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Gerekli PKI sertifikalarını önceden hazırlayın  
 İnternet'teki cihazları, kayıtlı mobil cihazları ve Mac bilgisayarları yönetmek için site sistemlerinde (yönetim noktaları ve dağıtım noktaları) ve istemci cihazlarda PKI sertifikalarınız olmalıdır. Üretim ağlarında, yeni sertifikalar kullanmak, site sistem sunucularını yeniden başlatmak için değişiklik yönetimi onayına ihtiyacınız olabilir veya kullanıcılar yeni grup üyeliği için oturumlarını kapatıp açmak zorunda kalabilirler. Ayrıca, güvenlik izinlerinin çoğaltılması ve tüm yeni sertifika şablonları için yeterli bir süre beklemeniz gerekebilir.  

 Gerekli PKI sertifikaları hakkında daha fazla bilgi için bkz. [Configuration Manager Için PKI sertifikası gereksinimleri](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>İstemcileri yüklemeden önce, gerekli tüm istemci ayarlarını ve bakım pencerelerini yapılandırma  
 İstemci ayarlarını ve bakım pencerelerini istemciler yüklenmeden önce veya sonra [yapılandırabilmenize](../../../../core/clients/deploy/configure-client-settings.md) rağmen, istemci yüklendikten hemen sonra kullanılabilmeleri için, istemcileri yüklemeden önce gerekli ayarları yapılandırmak daha iyidir. 

 Kritik cihazlarda iş sürekliliği sağlamak için sunucular ve Windows Embedded cihazları için bakım pencerelerini yapılandırın. Bakım pencereleri gerekli yazılım güncelleştirmelerinin ve kötü amaçlı yazılımdan koruma yazılımlarının bilgisayarı iş saatlerinde yeniden başlatmadığından emin olur.  

> [!IMPORTANT]  
>  Birleşik Yazma Filtresi (UWF) ile korumayı planladığınız Windows 10 bilgisayarlarında, istemciyi yüklemeden önce cihazı UWF için yapılandırmanız gerekir. Bu, Configuration Manager, düşük haklara sahip kullanıcıların bakım modundayken cihazda oturum açmasını engelleyen özel bir kimlik bilgisi sağlayıcısıyla istemciyi yüklemesini sağlar.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Mac bilgisayarlar ve mobil cihazlar için Kullanıcı kayıt deneyiminizi planlayın   
 Kullanıcılar kendi Mac bilgisayarlarını ve mobil cihazlarını Configuration Manager 'ye kaydedecektir, Kullanıcı deneyimini planlayın. Örneğin, bir Web sayfasını kullanarak yükleme ve kayıt işlemine komut dosyası yazarak, kullanıcıların gereken en düşük bilgi miktarını girmesini ve e-posta ile bir bağlantıyla birlikte talimatlarını göndermenizi sağlayabilirsiniz.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Windows Embedded cihazları için dosya tabanlı yazma filtreleri kullanma 
 Gelişmiş Yazma Filtrelerini (EWF) kullanan katıştırılmış cihazlarda, durum iletisinde yeniden eşitlemeler görülmesi mümkündür. Gelişmiş Yazma Filtreleri kullanan yalnızca birkaç katıştırılmış cihazınız varsa bunu fark etmeyebilirsiniz. Ancak, bilgilerini yeniden eşitleyen, örneğin fark envanteri yerine tam envanteri gönderen katıştırılmış birçok cihazınız varsa bu durum ağ paketlerinde dikkate değer bir artış ve site sunucusunda daha yüksek CPU işlemleri üretebilir.  

 Hangi tür yazma filtresini etkinleştirecağınızı seçebilmeniz için dosya tabanlı yazma filtreleri ' ni seçin ve Configuration Manager istemcisinde ağ ve CPU verimliliği için cihaz yeniden başlatmaları arasında istemci durumu ve envanter verilerini kalıcı hale getirmek için özel durumlar yapılandırın. Yazma filtreleri hakkında daha fazla bilgi için bkz. [Windows Embedded cihazlarına istemci dağıtımını planlama](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Birincil bir sitenin destekleyebileceği en yüksek Windows Embedded istemci sayısı hakkında daha fazla bilgi için bkz. [İstemciler ve cihazlar için desteklenen işletim sistemleri](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
