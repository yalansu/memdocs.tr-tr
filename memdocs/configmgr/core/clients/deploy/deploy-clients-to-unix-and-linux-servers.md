---
title: UNIX/Linux istemcilerini dağıtma
titleSuffix: Configuration Manager
description: Configuration Manager ' de bir istemciyi UNIX veya Linux sunucusuna dağıtmayı öğrenin.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4375867e70cb7f2989b78572c7fc8e005f95be73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713453"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Configuration Manager ' de UNIX ve Linux sunuculara istemci dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.


Configuration Manager ile bir Linux veya UNIX sunucusunu yönetebilmeniz için önce Linux ve UNIX için Configuration Manager istemcisini her bir Linux veya UNIX sunucusuna yüklemelisiniz. İstemcinin yüklemesini her bilgisayarda el ile gerçekleştirebilir ya da istemciyi uzaktan yükleyen bir kabuk betiği kullanabilirsiniz. Configuration Manager, Linux veya UNIX sunucuları için istemci anında yükleme kullanımını desteklemez. İsteğe bağlı olarak, istemcinin Linux veya UNIX sunucuya yüklenmesini otomatikleştirmek istiyorsanız bir System Center Orchestrator için Runbook yapılandırabilirsiniz.  

 Kullandığınız yükleme yönteminden bağımsız olarak, yükleme işlemi, yönetimi için **install** adlı bir betik gerektirir. Linux ve UNIX için istemciyi indirdiğinizde bu betik dahil edilir.  

 Linux ve UNIX için Configuration Manager istemcisinin Install betiği komut satırı özelliklerini destekler. Bazı komut satırı özellikleri gereklidir, diğerleri isteğe bağlıdır. Örneğin, istemciyi yüklerken sitede bulunan ve Linux veya UNIX sunucusu tarafından sunucunun site ile ilk iletişimi için kullanılan bir yönetim noktası belirtmeniz gerekir. Komut satırı özelliklerinin tam listesi için bkz. [Istemciyi Linux ve UNIX sunucularına yüklemek Için komut satırı özellikleri](#BKMK_CmdLineInstallLnUClient).  

 İstemcisini yükledikten sonra, istemci aracısını Windows tabanlı istemcilerle aynı şekilde yapılandırmak için Configuration Manager konsolundaki Istemci ayarlarını belirtirsiniz. Daha fazla bilgi için bkz.  [Linux ve UNIX Sunucuları istemci ayarları](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a>İstemci yükleme paketleri ve Universal Agent hakkında  
 Belirli bir platformda Linux ve UNIX için istemciyi yüklemek istiyorsanız istemciyi yüklediğiniz bilgisayar için uygun istemci yükleme paketini kullanmalısınız. [Microsoft İndirme Merkezi](https://go.microsoft.com/fwlink/?LinkID=525184)’nden gerçekleştirilen her istemci indirmesine uygun istemci yükleme paketleri dahil edilir. İstemci indirmesi, istemci yükleme paketlerine ek olarak istemcinin her bilgisayara yüklenmesini yöneten **install** betiğini içerir.  

 Bir istemciyi yüklediğinizde, kullandığınız istemci yükleme paketinden bağımsız olarak aynı işlem ve komut satırı özelliklerini kullanabilirsiniz.  

 Linux ve UNIX için Configuration Manager istemcisinin her bir sürümü tarafından desteklenen işletim sistemleri, platformlar ve istemci yükleme paketleri hakkında daha fazla bilgi için bkz. [Linux ve UNIX sunucuları](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers).  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a>İstemcisini Linux ve UNIX sunucularına yükler  
 Linux ve UNIX için istemciyi yüklemek için her bir Linux veya UNIX bilgisayarda bir betik çalıştırırsınız. Komut dosyası **install** olarak adlandırılır ve yükleme davranışını değiştiren ve istemci yükleme paketine başvuran komut satırı özelliklerini destekler. Yükleme betiğinin ve istemci yükleme paketinin istemcide bulunması gerekir. İstemci yükleme paketi, belirli bir Linux veya UNIX işletim sistemi ve platformu için Configuration Manager istemci dosyalarını içerir.
Her istemci yükleme paketi, istemci yüklemesini gerçekleştirmek için gerekli tüm dosyaları içerir ve Windows tabanlı bilgisayarlardan farklı olarak bir yönetim noktasından veya başka bir kaynak konumdan ek dosya indirmez.  

 Linux ve UNIX için Configuration Manager istemcisini yükledikten sonra bilgisayarı yeniden başlatmanız gerekmez. Yazılım yüklemesi tamamlandıktan hemen sonra istemci çalışır duruma gelir. Bilgisayarı yeniden başlattığınızda, Configuration Manager istemcisi otomatik olarak yeniden başlatılır.  

 Yüklenen istemci kök kimlik bilgileriyle çalışır. Donanım envanteri toplamak ve yazılım dağıtımları yapmak için kök kimlik bilgileri gereklidir.  

 Aşağıdaki komut biçimini kullanın:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install`, Linux ve UNIX için istemcisini yükleyen betik dosyasının adıdır. Bu dosya istemci yazılımıyla birlikte sağlanır.  

-   `-mp <computer>`istemci tarafından kullanılan ilk yönetim noktasını belirtir. Örnek: `smsmp.contoso.com`  

-   `-sitecode <site code>`istemcinin atandığı site kodunu belirtir. Örnek: `S01`  

-   `<property #1> <property #2>`yükleme betiği ile kullanılacak komut satırı özelliklerini belirtir.  

    > [!NOTE]  
    >  Daha fazla bilgi için bkz. [Istemciyi Linux ve UNIX sunucularına yüklemek Için komut satırı özellikleri](#BKMK_CmdLineInstallLnUClient).  

-   **istemci yükleme paketi** , bu bilgisayar işletim sistemi, sürümü ve CPU mimarisine yönelik istemci yükleme .tar paketinin adıdır. İstemci yükleme .tar dosyasının en son belirtilmesi gerekir. Örnek: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a>Configuration Manager istemcisini Linux ve UNIX sunuculara yüklemek için  

1.  Bir Windows bilgisayara yönetmek istediğiniz [Linux veya UNIX sunucusu için uygun istemci dosyasını](https://go.microsoft.com/fwlink/?LinkID=525184) indirin.  

2.  Yükleme betiğini ve istemci yükleme .tar dosyasını ayıklamak için Windows bilgisayarda kendiliğinden çalışan .exe dosyasını çalıştırın.  

3.  **install** betiğini ve .tar dosyasını yönetmek istediğiniz sunucu üzerinde bir klasöre kopyalayın.  

4.  UNIX veya Linux sunucusunda, betiğin bir program olarak çalışmasını sağlamak için aşağıdaki komutu çalıştırın:`chmod +x install`  

    > [!IMPORTANT]  
    >  İstemciyi yüklemek için kök kimlik bilgileri kullanmanız gerekir.  

5.  Sonra, Configuration Manager istemcisini yüklemek için aşağıdaki komutu çalıştırın:`./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Bu komutu girerken, gereksinim duyduğunuz ek komut satırı özelliklerini kullanın. Komut satırı özelliklerinin listesi için bkz [. Istemciyi Linux ve UNIX sunucularına yüklemek Için komut satırı özellikleri](#BKMK_CmdLineInstallLnUClient)  

6.  Betik çalıştıktan sonra **/var/opt/microsoft/scxcm.log** dosyasını gözden geçirerek yüklemeyi doğrulayın. Ayrıca, Configuration Manager konsolundaki **varlıklar ve uyum** çalışma alanının **cihazlar** düğümünde istemcinin ayrıntılarını görüntüleyerek istemcinin yüklendiğini ve siteyle iletişim kurduğunu doğrulayabilirsiniz.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a>İstemciyi Linux ve UNIX sunucularına yüklemek için komut satırı özellikleri  
 Aşağıdaki özellikler, Install betiğinin davranışını değiştirmek için kullanılabilir:  

> [!NOTE]  
>  Desteklenen özellikler listesini `-h` göstermek için özelliğini kullanın.  

-   `-mp <server FQDN>`  

     Gereklidir. İstemcinin ilk iletişim noktası olarak kullandığı yönetim noktası sunucusu olan FQDN değerine göre belirtir.  

    > [!IMPORTANT]  
    >  Bu özellik, istemcinin yükleme sonrasında atandığı yönetim noktasını belirtmez.  

    > [!NOTE]  
    >  Yalnızca HTTPS istemci bağlantılarını `-mp` kabul edecek şekilde yapılandırılmış bir yönetim noktası belirtmek için özelliğini kullandığınızda `-UsePKICert` özelliğini de kullanmanız gerekir.  

-   `-sitecode <sitecode>`  

     Gereklidir. Configuration Manager istemcisinin atanacağı Configuration Manager birincil sitesini belirtir. Örnek: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     İsteğe bağlı. FQDN değerine göre istemcinin durum iletilerini göndermek için kullandığı geri dönüş durum noktası sunucusunu belirtir. Daha fazla bilgi için, bkz. [geri dönüş durum noktası gerekip gerekmediğini belirleme](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

-   `-dir <directory>`  

     İsteğe bağlı. Configuration Manager istemci dosyalarını yüklemek için başka bir konum belirtir. Varsayılan olarak istemci şu konuma yüklenir:`/opt/microsoft`  

-   `-nostart`  

     İsteğe bağlı. İstemci yüklemesi tamamlandıktan sonra **Ccmexec. bin**Configuration Manager istemci hizmetinin otomatik olarak başlamasını engeller.  

     İstemci yüklendikten sonra istemci hizmetini el ile başlatmanız gerekir.  

     Varsayılan olarak, istemci hizmeti istemcinin yüklenmesi tamamlandıktan sonra ve bilgisayar her yeniden başlatıldığında başlatılır.  

-   `-clean`  

     İsteğe bağlı. Yeni yükleme başlamadan önce Linux ve UNIX için daha önce yüklenen bir istemciden tüm istemci dosyaları ve verilerinin kaldırılmasını belirtir. Bu eylem, istemcinin veritabanını ve sertifika deposunu kaldırır.  

-   `-keepdb`  

     İsteğe bağlı. Yerel istemci veritabanının saklanacağını belirtir ve bir istemciyi yeniden yüklediğinizde yeniden kullanılır. Varsayılan olarak, bir istemciyi yeniden yüklediğinizde bu veritabanı silinir.  

-   `-UsePKICert <parameter>`  

     İsteğe bağlı. Bir X.509 PKI sertifikasının tam yolunu ve dosya adını Public Key Certificate Standard (PKCS#12) biçiminde belirtir. Bu sertifika, istemci kimlik doğrulaması için kullanılır. Yükleme sırasında bir sertifika belirtilmediyse ve bir sertifika eklemeniz ya da bir sertifikayı değiştirmeniz gerekiyorsa **certutil** yardımcı programını kullanın. Daha fazla bilgi için bkz. [Linux ve UNIX için istemcideki sertifikaları yönetme](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Kullandığınızda `-UsePKICert`, `-certpw` komut satırı parametresini kullanarak PKCS # 12 dosyasıyla ilişkili parolayı da sağlamanız gerekir.  

     Bu özelliği bir PKI sertifikası belirtmek için kullanmıyorsanız, istemci otomatik olarak imzalanan bir sertifika kullanır ve site sistemlerine yapılan tüm iletişimler HTTP üzerinden gerçekleştirilir.  

     İstemci yükleme komut satırında geçersiz bir sertifika belirtirseniz hata döndürülmez. Sertifika doğrulama, istemci yüklendikten sonra oluşur. İstemci başladığında, sertifikalar yönetim noktasıyla onaylanır. Bir sertifika doğrulanamazsa, **scxcm. log**dosyasında şu ileti görünür: **Yönetim noktası için sertifika doğrulanamadı**. Varsayılan günlük dosyası konumu:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > Bir istemciyi yüklerken bu özelliği belirtmeniz ve yalnızca HTTPS istemci bağlantılarını kabul etmek `-mp` üzere yapılandırılan bir yönetim noktası belirtmek için özelliğini kullanmanız gerekir.  

     Örnek: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     İsteğe bağlı. `-UsePKICert` Özelliğini kullanarak belirttiğiniz PKCS # 12 dosyası ile ilişkili parolayı belirtir.  

     Örnek: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     İsteğe bağlı. Bir istemcinin, bir PKI sertifikası kullanarak HTTPS üzerinden iletişim kurduğunda sertifika iptal listesini (CRL) denetmaması gerektiğini belirtir. Bu seçenek belirtilmediğinde, istemci, PKI sertifikalarını kullanarak bir HTTPS bağlantısı kurmadan önce CRL 'YI denetler. İstemci CRL denetlemesi hakkında daha fazla bilgi için bkz. PKI Sertifikası İptalini Planlama.  

     Örnek: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     İsteğe bağlı. Configuration Manager güvenilen kök anahtarının tam yolunu ve dosya adını belirtir. Configuration Manager güvenilen kök anahtarı, Linux ve UNIX istemcilerinin doğru hiyerarşiye ait bir site sistemine bağlandığını doğrulamak için kullandığı bir mekanizma sağlar.  

     Komut satırında güvenilen kök anahtarı belirtmezseniz, istemci iletişim kurduğu ilk yönetim noktasına güvenir ve güvenilen kök anahtarı otomatik olarak bu yönetim noktasından alır.  

     Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Örnek: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     İsteğe bağlı. İstemcinin HTTP üzerinden yönetim noktalarıyla iletişim kurarken kullandığı yönetim noktalarında yapılandırılan bağlantı noktasını belirtir. Bağlantı noktası belirtilmemişse, varsayılan 80 değeri kullanılır.  

     Örnek: `-httpport 80`  

-   `-httpsport <port>`  

     İsteğe bağlı. İstemcinin HTTPS üzerinden yönetim noktalarıyla iletişim kurarken kullandığı yönetim noktalarında yapılandırılan bağlantı noktasını belirtir. Bağlantı noktası belirtilmemişse, varsayılan 443 değeri kullanılır.  

     Örnek: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     İsteğe bağlı. İstemci yüklemesinin SHA-256 doğrulamasını atladığını belirtir. İstemciyi, SHA-256 ' y i destekleyen bir OpenSSL sürümüyle birlikte olmayan işletim sistemlerine yüklerken bu seçeneği kullanın. Daha fazla bilgi için bkz. [SHA-256 desteklemeyen Linux ve UNIX işletim sistemleri hakkında](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     İsteğe bağlı. Site sunucusunda, dışarıya aktarılmış otomatik olarak imzalanan sertifikanın tam yolunu ve **. cer** dosya adını belirtir. PKI sertifikaları kullanılamıyorsa, Configuration Manager site sunucusu otomatik olarak otomatik olarak imzalanan sertifikalar oluşturur.  

     Bu sertifikalar, yönetim noktasından indirilen istemci ilkelerinin hedeflenen siteden gönderildiğini doğrulamak için kullanılır. Yükleme sırasında otomatik imzalı bir sertifika belirtilmez veya bir sertifikayı değiştirmeniz gerekirse **certutil** yardımcı programını kullanın. Daha fazla bilgi için bkz. [Linux ve UNIX için istemcideki sertifikaları yönetme](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Bu sertifika **SMS** sertifika deposundan alınabilir ve **Site Sunucusu** Konu adına ve **Site Sunucusu İmzalama Sertifikası**kolay adına sahip olur.  

     Yükleme sırasında bu seçenek belirtilmemişse, Linux ve UNIX istemcileri iletişim kurdukları ilk yönetim noktasına güvenir. İmza sertifikasını otomatik olarak bu yönetim noktasından alır.  

     Örnek: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     İsteğe bağlı. Bir yönetim noktaları sertifika yetkilisi (CA) hiyerarşisinin parçası olmayan içeri aktarılacak ek PKI sertifikalarını belirtir. Komut satırında birden çok sertifika belirtirseniz, bunların virgülle ayrılması gerekir.  

     Sitelerinizin yönetim noktaları tarafından güvenilen bir kök CA sertifikasına zincirsiz olmayan PKI istemci sertifikaları kullanıyorsanız bu seçeneği kullanın. İstemci sertifikası sitenin sertifika verenler listesinde güvenilen bir kök sertifikaya zincir oluşturmaz yönetim noktaları istemciyi reddeder.  

     Bu seçeneği kullanmazsanız, Linux ve UNIX istemcisi güven hiyerarşisini yalnızca `-UsePKICert` seçeneğinde bulunan sertifikayı kullanarak doğrular.  

     Örnek: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a>İstemciyi Linux ve UNIX sunucularından kaldırma  
 Linux ve UNIX için Configuration Manager istemcisini kaldırmak **için kaldırma yardımcı programını kullanın.** Varsayılan olarak, bu dosya istemci bilgisayardaki **/opt/microsoft/configmgr/bin/** klasöründe bulunur. Bu kaldırma komutu hiçbir komut satırı parametresini desteklemez ve istemci yazılımıyla ilişkili tüm dosyaları sunucudan kaldırır.  

 İstemciyi kaldırmak için şu komut satırını kullanın: **/opt/microsoft/configmgr/bin/uninstall**  

 Linux ve UNIX için Configuration Manager istemcisini kaldırdıktan sonra bilgisayarı yeniden başlatmanız gerekmez.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a>Linux ve UNIX için Istemci için Istek bağlantı noktalarını yapılandırma  
 Windows tabanlı istemcilere benzer şekilde, Linux ve UNIX için Configuration Manager istemcisi, Configuration Manager site sistemleriyle iletişim kurmak için HTTP ve HTTPS kullanır. Configuration Manager istemcisinin iletişim kurmak için kullandığı bağlantı noktaları istek bağlantı noktaları olarak adlandırılır.  

 Linux ve UNIX için Configuration Manager istemcisini yüklediğinizde, **-httpport** ve **-HttpsPort** yükleme özelliklerini belirterek istemcilerin varsayılan istek bağlantı noktalarını değiştirebilirsiniz. Yükleme özelliğini ve özel bir değeri belirtmezseniz, istemci varsayılan değerleri kullanır. Varsayılan değerler HTTP trafiği için **80** , HTTPS trafiği için **443** ’tür.  

 İstemcisini yükledikten sonra, istek bağlantı noktası yapılandırmasını değiştiremezsiniz. Bağlantı noktası yapılandırmasını değiştirmek için bunun yerine istemciyi yeniden yüklemeniz ve yeni bağlantı noktası yapılandırmasını belirtmeniz gerekir. İstek bağlantı noktası numaralarını değiştirmek için istemciyi yeniden yüklediğinizde, yeni istemci yüklemesine benzer olan **Install** komutunu çalıştırın, ancak **-St pdb**ek komut satırı özelliğini kullanın. Bu anahtar, yüklemeye istemci veritabanını ve istemcilerin GUID ve sertifika deposunu içeren dosyaları tutmasını sağlar.  

 İstemci iletişim bağlantı noktası numaraları hakkında daha fazla bilgi için bkz. [istemci iletişim bağlantı noktalarını yapılandırma](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a>Linux ve UNIX için Istemciyi yönetim noktalarını bulacak şekilde yapılandırma  
 Linux ve UNIX için Configuration Manager istemcisini yüklediğinizde, ilk iletişim noktası olarak kullanmak üzere bir yönetim noktası belirtmeniz gerekir.  

 Linux ve UNIX için Configuration Manager istemcisi, istemcinin yüklendiği zaman bu yönetim noktasıyla iletişim kurar. İstemci yönetim noktasıyla iletişim kuramazsa istemci yazılımı iletişim başarılı olana kadar yeniden denemeye devam eder.  

 İstemcilerin yönetim noktalarını nasıl bulduğu hakkında daha fazla bilgi için bkz. [Yönetim Noktalarını Bulma](assign-clients-to-a-site.md#locating-management-points).
