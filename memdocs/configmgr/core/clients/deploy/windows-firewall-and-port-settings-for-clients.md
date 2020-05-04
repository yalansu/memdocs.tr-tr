---
title: Windows istemci güvenlik duvarı ve bağlantı noktası ayarları
titleSuffix: Configuration Manager
description: Configuration Manager içindeki istemciler için Windows Güvenlik Duvarı ve bağlantı noktası ayarları ' nı seçin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713971"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Configuration Manager içindeki istemciler için Windows Güvenlik Duvarı ve bağlantı noktası ayarları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Windows Güvenlik Duvarı 'Nı çalıştıran Configuration Manager istemci bilgisayarlar genellikle siteleri ile iletişime izin verecek şekilde özel durumlar yapılandırmanızı gerektirir. Yapılandırmanız gereken özel durumlar, Configuration Manager istemcisi ile kullandığınız yönetim özelliklerine bağlıdır.  

 Bu yönetim özelliklerini belirlemek ve Windows Güvenlik Duvarı'nı bu özel durumlarla ilgili yapılandırma hakkında ek bilgi için aşağıdaki bölümleri kullanın.  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Windows Güvenlik Duvarı'nın İzin Verdiği Bağlantı Noktalarını ve Programları Değiştirme  
 Configuration Manager istemcisi için Windows Güvenlik Duvarı 'ndaki bağlantı noktalarını ve programları değiştirmek için aşağıdaki yordamı kullanın.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Windows Güvenlik Duvarı'nın izin verdiği bağlantı noktalarını ve programları değiştirmek için  

1.  Windows Güvenlik Duvarı'nı çalıştıran bilgisayarda, Denetim Masası'nı açın.  

2.  **Windows Güvenlik Duvarı**'na sağ tıkladıktan sonra **Aç**'a tıklayın.  

3.  Tüm gerekli özel durumları ve ihtiyaç duyduğunuz tüm özel programları ve bağlantı noktalarını yapılandırın.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Configuration Manager İçin Gereken Programlar ve Bağlantı Noktaları  
 Aşağıdaki Configuration Manager özellikleri Windows Güvenlik Duvarı 'nda özel durumlar gerektirir:  

### <a name="queries"></a>Sorgular  
 Configuration Manager konsolunu Windows güvenlik duvarı çalıştıran bir bilgisayarda çalıştırırsanız, sorgular ilk çalıştırıldıklarında başarısız olur ve işletim sistemi statview. exe ' nin engellemesini kaldırmak isteyip istemediğinizi soran bir iletişim kutusu görüntüler. Statview.exe’yi engellerseniz gelecekteki sorgular hatasız çalışır. Statview.exe'yi bir sorgu çalıştırmadan önce Windows Güvenlik Duvarı'nın **Özel Durumlar** sekmesine el ile de ekleyebilirsiniz.  

### <a name="client-push-installation"></a>İstemci Gönderme Yüklemesi  
 Configuration Manager istemcisini yüklemek üzere Client Push kullanmak için, Windows Güvenlik Duvarı 'na aşağıdaki özel durumları ekleyin:  

-   Giden ve gelen: **Dosya ve Yazıcı Paylaşımı**  

-   Gelen: **Windows Yönetim Araçları (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Grup İlkesi Kullanarak İstemci Yükleme  
 Configuration Manager istemcisini yüklemek üzere grup ilkesi kullanmak için, Windows Güvenlik Duvarı 'na özel durum olarak **dosya ve yazıcı paylaşımı** ekleyin.  

### <a name="client-requests"></a>İstemci İstekleri  
 İstemci bilgisayarların Configuration Manager site sistemleriyle iletişim kurması için aşağıdakileri özel durum olarak Windows Güvenlik Duvarı 'na ekleyin:  

 Giden: TCP Bağlantı Noktası **80** (HTTP iletişimi için)  

 Giden: TCP Bağlantı Noktası **443** (HTTPS iletişimi için)  

> [!IMPORTANT]  
>  Bunlar, Configuration Manager ' de değiştirilebilen varsayılan bağlantı noktası numaralarıdır. Daha fazla bilgi için bkz. [istemci iletişim bağlantı noktalarını yapılandırma](../../../core/clients/deploy/configure-client-communication-ports.md). Bu bağlantı noktaları varsayılan değerlerinden değiştirilmişse, Windows Güvenlik Duvarı'nda da eşleşen özel durumlar yapılandırmanız gerekir.  

### <a name="client-notification"></a>İstemci Bildirimi  
 Yönetim noktası, bir yönetici kullanıcı Configuration Manager konsolunda, bilgisayar ilkesini indir veya kötü amaçlı yazılım taraması başlatma gibi bir istemci eylemi seçtiğinde, istemci bilgisayarlara bir eylem hakkında bilgilendirmesini sağlamak için, Windows Güvenlik Duvarı 'na özel durum olarak aşağıdakini ekleyin:  

 Giden: TCP Bağlantı Noktası **10123**  

 Bu iletişim başarılı olmazsa Configuration Manager, mevcut istemciden yönetim noktası iletişim bağlantı noktasını (HTTP veya HTTPS) kullanmaya otomatik olarak geri döner:  

 Giden: TCP Bağlantı Noktası **80** (HTTP iletişimi için)  

 Giden: TCP Bağlantı Noktası **443** (HTTPS iletişimi için)  

> [!IMPORTANT]  
>  Bunlar, Configuration Manager ' de değiştirilebilen varsayılan bağlantı noktası numaralarıdır. Daha fazla bilgi için bkz. [istemci iletişim bağlantı noktalarını yapılandırma](../../../core/clients/deploy/configure-client-communication-ports.md). Bu bağlantı noktaları varsayılan değerlerinden değiştirilmişse, Windows Güvenlik Duvarı'nda da eşleşen özel durumlar yapılandırmanız gerekir.  

### <a name="remote-control"></a>Uzaktan Denetim  
 Uzaktan denetim Configuration Manager kullanmak için şu bağlantı noktasına izin verin:  

-   Gelen: TCP bağlantı noktası **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Uzaktan Yardım ve Uzak Masaüstü  
 Configuration Manager konsolundan uzaktan yardım başlatmak için **helpsvc. exe** özel programını ve gelen özel bağlantı noktası TCP **135** ' i Istemci bilgisayardaki Windows Güvenlik Duvarı 'nda izin verilen program ve hizmetler listesine ekleyin. **Uzaktan Yardım** 'a ve **Uzak Masaüstü**'ne de izin vermeniz gerekir. İstemci bilgisayardan Uzaktan Yardım'ı başlattığınızda, Windows Güvenlik Duvarı otomatik olarak **Uzaktan Yardım** 'ı ve **Uzak Masaüstü**'nü yapılandırır ve izin verir.  

### <a name="wake-up-proxy"></a>Uyandırma Proxy'si  
 Uyandırma proxy'si istemci ayarını etkinleştirirseniz, ConfigMgr Uyandırma Proxy'si adlı yeni bir hizmet eşler arası protokolü kullanarak alt ağdaki diğer bilgisayarların uyanık olup olmadığını denetler ve gerekirse onları uyandırır. Bu iletişim şu bağlantı noktalarını kullanır:  

 Giden: UDP Bağlantı Noktası **25536**  

 Giden: UDP Bağlantı Noktası **9**  

 Bunlar, **uyandırma proxy 'si bağlantı noktası numarası (UDP)** ve **LAN'da Uyandırma bağlantı noktası numarası (UDP)**' nın **güç yönetimi** istemcileri ayarları kullanılarak Configuration Manager değiştirilebilen varsayılan bağlantı noktası numaralarıdır. **Güç Yönetimi**: **Uyandırma proxy'si için Windows Güvenlik Duvarı özel durumu** istemci ayarını belirtirseniz, bu bağlantı noktaları otomatik olarak istemciler için Windows Güvenlik Duvarı'nda yapılandırılır. Ancak istemciler farklı bir güvenlik duvarında çalışıyorsa bu bağlantı noktası numaralarının özel durumlarını el ile yapılandırmanız gerekir.  

 Bu bağlantı noktalarına ek olarak, uyandırma proxy'si aynı zamanda bir istemci bilgisayardan diğer istemci bilgisayara İnternet Denetim İletisi Protokolü (ICMP) yankı isteği mesajlarını kullanır. Bu iletişim, ağdaki diğer istemci bilgisayarın uyanık olup olmadığını doğrulamak için kullanılır. ICMP bazen TCP/IP ping komutları olarak adlandırılır.  

 Uyandırma proxy 'si hakkında daha fazla bilgi için bkz. [istemcileri nasıl uyandırmayı planlayın](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Windows Olay Görüntüleyicisi, Windows Performans İzleyicisi ve Windows Tanılama  
 Configuration Manager konsolundan Windows Olay Görüntüleyicisi, Windows performans Izleyicisi ve Windows Tanılama 'ya erişmek için **dosya ve yazıcı paylaşımını** Windows Güvenlik Duvarı 'nda özel durum olarak etkinleştirin.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Configuration Manager İstemci Dağıtımı Sırasında Kullanılan Bağlantı Noktaları  
 Aşağıdaki tablolarda istemci yükleme işlemi sırasında kullanılan bağlantı noktaları verilmiştir.  

> [!IMPORTANT]  
>  Site sistemi sunucuları ile istemci bilgisayar arasında güvenlik duvarı varsa, bu güvenlik duvarının seçtiğiniz istemci yükleme yöntemi için gereken bağlantı noktalarına yönelik trafiğe izin verip vermediğini onaylayın. Örneğin, güvenlik duvarları Sunucu İleti Bloğunu (SMB) ve Uzaktan Yordam Çağrılarını (RPC) engellediği için istemci gönderme yüklemesinin başarılı olmasına sıkça engel olur. Bu senaryoda, elle yükleme (CCMSetup.exe'yi çalıştırarak) veya Grup İlkesi kullanarak istemci yükleme gibi farklı bir istemci yükleme yöntemini kullanın. Bu alternatif istemci yükleme yöntemleri SMB veya RPC gerektirmez.  

 Windows Güvenlik Duvarı'nı istemci bilgisayarda yapılandırma hakkında bilgi için bkz. [Windows Güvenlik Duvarı'nın İzin Verdiği Bağlantı Noktalarını ve Programları Değiştirme](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Tüm yükleme yöntemlerinde kullanılan bağlantı noktaları  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|İstemciye bir geri dönüş durum noktası atandığında istemci bilgisayardan geri dönüş durum noktasına Köprü Metni Aktarım Protokolü (HTTP).|--|80 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>İstemci gönderme yüklemesinde kullanılan bağlantı noktaları  
 İstemci gönderme yüklemesi aşağıda listelenen bağlantı noktalarına ek olarak, istemci bilgisayarın ağda kullanılıp kullanılamadığından emin olmak için site sunucusundan istemci bilgisayara İnternet Denetim İletisi Protokolü (ICMP) yankı isteği mesajlarını da kullanır. ICMP bazen TCP/IP ping komutları olarak adlandırılır. ICMP'nin bir UDP veya TCP protokol numarası olmadığından aşağıdaki tabloda listelenmemiştir. Ancak, istemci gönderme yüklemesinin başarılı olması için güvenlik duvarı gibi müdahalede bulunan tüm ağ cihazları ICMP trafiğine izin vermelidir.  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Site sunucusu ile istemci bilgisayar arasında Sunucu İleti Bloğu (SMB).|--|445|  
|Site sunucusu ile istemci bilgisayar arasında RPC bitiş noktası eşleştiricisi.|135|135|  
|Site sunucusu ile istemci bilgisayar arasında RPC dinamik bağlantı noktaları.|--|DİNAMİK|  
|Bağlantı HTTP üzerinden olduğunda istemci bilgisayardan yönetim noktasına Köprü Metni Aktarım Protokolü (HTTP).|--|80 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  
|Bağlantı HTTPS üzerinden olduğunda istemci bilgisayardan yönetim noktasına Güvenli Köprü Metni Aktarım Protokolü (HTTPS).|--|443 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Yazılım güncelleştirme noktası tabanlı yüklemede kullanılan bağlantı noktaları  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|İstemci bilgisayardan yazılım güncelleştirme noktasına Köprü Metni Aktarım Protokolü (HTTP) .|--|80 veya 8530 (bkz. not 2, **Windows Server Update Services**)|  
|İstemci bilgisayardan yazılım güncelleştirme noktasına Güvenli Köprü Metni Aktarım Protokolü (HTTPS).|--|443 veya 8531 (bkz. not 2, **Windows Server Update Services**)|  
|CCMSetup komut satırı özelliği **/Source:&lt;\>Path**' i belirttiğinizde kaynak sunucu Ile istemci BILGISAYAR arasındaki sunucu ileti bloğu (SMB).|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Grup İlkesi tabanlı yüklemede kullanılan bağlantı noktaları  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Bağlantı HTTP üzerinden olduğunda istemci bilgisayardan yönetim noktasına Köprü Metni Aktarım Protokolü (HTTP).|--|80 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  
|Bağlantı HTTPS üzerinden olduğunda istemci bilgisayardan yönetim noktasına Güvenli Köprü Metni Aktarım Protokolü (HTTPS).|--|443 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  
|CCMSetup komut satırı özelliği **/Source:&lt;\>Path**' i belirttiğinizde kaynak sunucu Ile istemci BILGISAYAR arasındaki sunucu ileti bloğu (SMB).|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Elle yükleme ve oturum açma betiği tabanlı yüklemede kullanılan bağlantı noktaları  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|İstemci bilgisayar ile CCMSetup.exe'yi çalıştırdığınız ağ paylaşımı arasında Sunucu İleti Bloğu (SMB).<br /><br /> Configuration Manager yüklediğinizde, istemci yükleme kaynak dosyaları kopyalanır ve yönetim noktalarında * &lt;InstallationPath\>* \Client klasöründen otomatik olarak paylaşılır. Ancak, bu dosyaları kopyalayabilir ve ağdaki herhangi bir bilgisayarda yeni bir paylaşım oluşturabilirsiniz. Alternatif olarak, CCMSetup.exe'yi yerel olarak çalıştırma yoluyla, örneğin, çıkarılabilir medyayı kullanarak bu ağ trafiğini ortadan kaldırabilirsiniz.|--|445|  
|Bağlantı HTTP üzerinden olduğunda istemci bilgisayardan yönetim noktasına Köprü Metni Aktarım Protokolü (HTTP) ve CCMSetup komut satırı özelliği **/Source:&lt;\>Path**belirtmeyin.|--|80 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  
|Bağlantı HTTPS üzerinden olduğunda istemci bilgisayardan yönetim noktasına Güvenli Köprü Metni Aktarım Protokolü (HTTPS) ve CCMSetup komut satırı özelliği **/Source:&lt;\>Path**belirtmeyin.|--|443 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  
|CCMSetup komut satırı özelliği **/Source:&lt;\>Path**' i belirttiğinizde kaynak sunucu Ile istemci BILGISAYAR arasındaki sunucu ileti bloğu (SMB).|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Yazılım dağıtımı tabanlı yüklemede kullanılan bağlantı noktaları  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Dağıtım noktası ile istemci bilgisayar arasında Sunucu İleti Bloğu (SMB).|--|445|  
|Bağlantı HTTP üzerinden olduğunda istemciden dağıtım noktasına Köprü Metni Aktarım Protokolü (HTTP).|--|80 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  
|Bağlantı HTTPS üzerinden olduğunda istemciden dağıtım noktasına Güvenli Köprü Metni Aktarım Protokolü (HTTPS).|--|443 (bkz. not 1, **Alternatif Bağlantı Noktası Kullanılabilir**)|  

## <a name="notes"></a>Notlar  
 **1 alternatif bağlantı noktası var** Configuration Manager, bu değer için alternatif bir bağlantı noktası tanımlayabilirsiniz. Özel bağlantı noktası tanımlanmışsa, IPsec ilkelerine veya güvenlik duvarlarını yapılandırmaya yönelik IP filtresi bilgilerini tanımlarken bu özel bağlantı noktasını yerine koyun.  

 **2 Windows Server Update Services** Windows Server Update Services'ı (WSUS) varsayılan Web sitesine (bağlantı noktası 80) veya özel Web sitesine (bağlantı noktası 8530) yükleyebilirsiniz.  

 Yüklemeden sonra bu bağlantı noktasını değiştirebilirsiniz. Site hiyerarşisinin her yerinde aynı bağlantı noktasını kullanmanız gerekmez.  

 HTTP bağlantı noktası 80 ise HTTPS bağlantı noktası 443 olmalıdır.  

 HTTP bağlantı noktası başka bir şeydir, HTTPS bağlantı noktası 1 daha yüksek olmalıdır. Örneğin, 8530 ve 8531.
