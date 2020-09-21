---
title: Bir yazılım güncelleştirme noktasını bir PKI sertifikası öğreticisiyle TLS/SSL kullanacak şekilde yapılandırma
titleSuffix: Configuration Manager
description: Öğretici-Windows Server Update Services (WSUS) sunucularını ve yazılım güncelleştirme noktalarını bir PKI sertifikasıyla TLS/SSL kullanacak şekilde yapılandırın.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
ms.openlocfilehash: 4f21af0a5431b5d06f6d96504fa99b52aa43e324
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814473"
---
# <a name="tutorial-configure-a-software-update-point-to-use-tlsssl-with-a-pki-certificate"></a>Öğretici: bir yazılım güncelleştirme noktasını bir PKI sertifikasıyla TLS/SSL kullanacak şekilde yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Windows Server Update Services (WSUS) sunucularını ve bunlara karşılık gelen yazılım güncelleştirme noktalarını (SUP) TLS/SSL kullanacak şekilde yapılandırmak, olası bir saldırganın bir istemcinin güvenliğini uzaktan tehlikeye atmasına ve ayrıcalıkları yükseltmesine olanak tanıyabilir. En iyi güvenlik protokollerinin yapıldığından emin olmak için, yazılım güncelleştirme altyapınızı güvenli hale getirmeye yardımcı olması için TLS/SSL protokolünü kullanmanızı kesinlikle öneririz. Bu makalede, WSUS sunucularınızın her birini ve yazılım güncelleştirme noktasını HTTPS kullanmak üzere yapılandırmak için gereken adımlarda adım adım gösterilmektedir. WSUS güvenliğini sağlama hakkında daha fazla bilgi için WSUS belgelerindeki [Güvenli Yuva Katmanı Protokolü Ile GÜVENLI WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) makalesine bakın.

Bu öğreticide şunları yapacaksınız:
> [!div class="checklist"]
> * Gerekirse bir PKI sertifikası alın
> * Sertifikayı WSUS Yönetimi Web sitesine bağlama
> * WSUS Web hizmetlerini SSL gerektirecek şekilde yapılandırma
> * WSUS uygulamasını SSL kullanacak şekilde yapılandırma
> * WSUS konsolu bağlantısının SSL kullanıp kullanbildiğini doğrulama
> * Yazılım güncelleştirme noktasını WSUS sunucusuna SSL iletişimi gerektirecek şekilde yapılandırma
> * Configuration Manager işlevleri doğrulama

## <a name="considerations-and-limitations"></a>Önemli noktalar ve sınırlamalar

WSUS, istemci bilgisayarların ve akış aşağı WSUS sunucularının kimliğini, yukarı akış WSUS sunucusuna doğrulamak için TLS/SSL kullanır. WSUS Ayrıca güncelleştirme meta verilerini şifrelemek için TLS/SSL kullanır. WSUS, bir güncelleştirmenin içerik dosyaları için TLS/SSL kullanmaz. İçerik dosyaları imzalanır ve dosyanın karması, güncelleştirmenin meta verilerinde yer alır. Dosyalar indirilmeden ve istemci tarafından yüklenmeden önce, hem dijital imza hem de karma denetlenir. Her iki denetim de başarısız olursa güncelleştirme yüklenmez.

Bir WSUS dağıtımının güvenliğini sağlamak için TLS/SSL kullandığınızda aşağıdaki sınırlamaları göz önünde bulundurun:

- TLS/SSL kullanmak sunucu iş yükünü artırır. Ağ üzerinden gönderilen tüm meta verileri şifrelemeden küçük bir performans kaybı beklemelisiniz.
- WSUS 'yi uzak bir SQL Server veritabanıyla kullanıyorsanız, WSUS sunucusu ve veritabanı sunucusu arasındaki bağlantı TLS/SSL ile güvenli değildir. Veritabanı bağlantısı güvenli hale getirilmelidir, aşağıdaki önerileri göz önünde bulundurun:
   - WSUS veritabanını WSUS sunucusuna taşıyın.
   - Uzak veritabanı sunucusunu ve WSUS sunucusunu özel bir ağa taşıyın.
   - Ağ trafiğini güvenli hale getirmeye yardımcı olması için İnternet Protokolü güvenliği’ni (IPSec) dağıtın.

WSUS sunucuları ve yazılım güncelleştirme noktalarını TLS/SSL kullanacak şekilde yapılandırırken, büyük Configuration Manager Hiyerarşilerle ilgili değişiklikleri aşamalandırmak isteyebilirsiniz. Bu değişiklikleri aşamayı tercih ederseniz hiyerarşinin en altından başlayın ve merkezi yönetim sitesiyle sona ermek üzere yukarı doğru ilerleyin.

## <a name="prerequisites"></a>Önkoşullar

Bu öğretici, Internet Information Services (IIS) ile kullanmak üzere bir sertifika almak için en sık kullanılan yöntemi ele almaktadır. Kuruluşunuzun kullandığı yöntem, sertifikanın Configuration Manager yazılım güncelleştirme noktası için [PKI sertifikası gereksinimlerini](../../core/plan-design/network/pki-certificate-requirements.md) karşıladığından emin olun. Her sertifikada olduğu gibi, sertifika yetkilisi WSUS sunucusuyla iletişim kuran cihazlar tarafından güvenilir olmalıdır.

- Yazılım güncelleştirme noktası rolünün yüklü olduğu bir WSUS sunucusu
- TLS/SSL 'yi etkinleştirmeden önce, geri dönüştürmeyi devre dışı bırakma ve WSUS için bellek sınırlarını yapılandırma konusunda [en iyi yöntemleri](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits) izlediğinizi doğrulayın.
- Aşağıdaki iki seçenekten biri:
   - WSUS sunucusunun **Kişisel** sertifika deposunda, uygun bir PKI sertifikası zaten var.
   - Kuruluş Kök Sertifika yetkilinizden (CA) WSUS sunucusu için uygun bir PKI sertifikası isteme ve alma özelliği.
      - Varsayılan olarak, Web sunucusu sertifika şablonu dahil olmak üzere çoğu sertifika şablonu yalnızca etki alanı yöneticilerine gönderilir. Oturum açan kullanıcı bir etki alanı yöneticisi değilse, Kullanıcı hesabına sertifika şablonunda **kaydolma** izni verilmesi gerekir.

## <a name="obtain-the-certificate-from-the-ca-if-needed"></a><a name="bkmk_pki"></a> Gerekirse sertifikayı CA 'dan alın

WSUS sunucusunun **Kişisel** sertifika deposunda zaten uygun bir sertifikanız varsa, bu bölümü atlayın ve [sertifikayı bağla](#bkmk_bind) bölümüne başlayın. Yeni bir sertifika yüklemek üzere iç sertifika YETKILISINE sertifika isteği göndermek için bu bölümdeki yönergeleri izleyin.
 
1. WSUS sunucusundan bir yönetim komut istemi açın ve komutunu çalıştırın `certlm.msc` . Yerel bilgisayar için sertifikaları yönetmek üzere Kullanıcı hesabınızın yerel bir yönetici olması gerekir.

   Yerel cihaz için Sertifika Yöneticisi aracı görünür.

1. **Kişisel**' i genişlettikten sonra **Sertifikalar**' a sağ tıklayın.
1. **Tüm görevler** ' i seçin ve **Yeni sertifika isteyin**.
1. Sertifika kaydını başlatmak için **İleri ' yi** seçin.
1. Kaydedilecek sertifika türünü seçin. Sertifika amacı, **sunucu kimlik doğrulamasıdır** ve kullanılacak Microsoft sertifika **şablonu,** **Gelişmiş anahtar kullanımı**olarak belirtilen **sunucu kimlik doğrulamasına** sahip özel bir şablondur. Sertifikayı kaydetmek için ek bilgiler istenebilir. Genellikle, en az aşağıdaki bilgileri belirtin:

   - **Ortak ad:** **Konu** sekmesinde bulunan değeri WSUS sunucusunun FQDN 'si olarak ayarlayın.
   - **Kolay ad:** **Genel** sekmesinde, sertifikayı daha sonra tanımanıza yardımcı olması için değeri açıklayıcı bir ad olarak ayarlayın.
   
   :::image type="content" source="media/certificate-properties.png" alt-text="Kayıt hakkında daha fazla bilgi belirtmek için sertifika özellikleri penceresi":::

1. Kaydı tamamlamaya sonra **Kaydet** ' i ve ardından **son** ' u seçin.
1. Sertifikanın parmak izi gibi ayrıntılarını görmek istiyorsanız sertifikayı açın.

> [!TIP]
> WSUS sunucunuz internet 'e yönelik ise, sertifikadaki Konu veya konu alternatif adı (SAN) dış FQDN 'niz gerekir.

## <a name="bind-the-certificate-to-the-wsus-administration-site"></a><a name="bkmk_bind"></a> Sertifikayı WSUS yönetim sitesine bağlayın

WSUS sunucusunun kişisel sertifika deposundaki sertifikaya sahip olduktan sonra, uygulamayı IIS 'deki WSUS yönetim sitesine bağlayın.

1. WSUS sunucusunda, Internet Information Services (IIS) Yöneticisi'ni açın.
1. **Sitelere**  >  **WSUS Yönetimi**' ne gidin.
1. Eylem menüsünden ya da siteye sağ tıklayarak **bağlamalar** ' ı seçin.
1. **Site bağlamaları** penceresinde, **https**için satırı seçin ve ardından **Düzenle...** seçeneğini belirleyin.

   - HTTP site bağlamasını kaldırmayın. WSUS, güncelleştirme içerik dosyaları için HTTP kullanır.
   
1. **SSL sertifikası** SEÇENEĞINDE, WSUS yönetim sitesine bağlanacak sertifikayı seçin. Sertifikanın kolay adı, açılan menüde gösterilir. Kolay bir ad belirtilmemişse, sertifikanın `IssuedTo` alanı gösterilir. Hangi sertifikanın kullanılacağını bilmiyorsanız, **görüntüle** ' yi seçin ve parmak izinin elde ettiğiniz ile eşleştiğini doğrulayın.

   :::image type="content" source="media/edit-site-binding.png" alt-text="Site bağlama penceresini SSL sertifikası seçimiyle Düzenle":::

1. İşiniz bittiğinde **Tamam** ' ı ve ardından site bağlamalarından çıkmak için **Kapat** ' ı seçin. Sonraki adımlarda Internet Information Services (IIS) Yöneticisi 'Ni açık tutun.



## <a name="configure-the-wsus-web-services-to-require-ssl"></a><a name="bkmk_webserv"></a> WSUS Web hizmetlerini SSL gerektirecek şekilde yapılandırma

1. WSUS sunucusundaki IIS Yöneticisi ' nde, **siteler**  >  **WSUS Yönetimi**' ne gidin.
1. WSUS yönetim sitesini genişleterek WSUS için Web hizmetlerinin ve sanal dizinlerin listesini görürsünüz.
1. Aşağıdaki WSUS Web hizmetlerinin her biri için:
   - Apıremoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   Aşağıdaki değişiklikleri yapın:
   
   1. **SSL ayarları**' nı seçin.
   1. **SSL gerektir** seçeneğini etkinleştirin.
   1. **İstemci sertifikaları** seçeneğinin **Yoksay**olarak ayarlandığını doğrulayın.
   1. **Uygula**’yı seçin.

İçerik gibi bazı işlevlerin HTTP kullanması gerektiğinden, üst düzey WSUS yönetim sitesinde SSL ayarlarını yapmayın.

## <a name="configure-the-wsus-application-to-use-ssl"></a><a name="bkmk_wsusutil"></a> WSUS uygulamasını SSL kullanacak şekilde yapılandırma

Web Hizmetleri SSL isteyecek şekilde ayarlandığında, WSUS uygulamasına değişikliği desteklemek için bazı ek yapılandırmalar yapabilmesi için bildirilmesi gerekir.

1. WSUS sunucusunda bir yönetici komut istemi açın. Bu komutu çalıştıran kullanıcı hesabı, WSUS yöneticileri grubunun veya yerel Yöneticiler grubunun üyesi olmalıdır.
1. Klasörü WSUS için Araçlar klasörüne değiştirin:

   `cd "c:\Program Files\Update Services\Tools"`
   
1. Aşağıdaki komutla WSUS 'i SSL kullanacak şekilde yapılandırın:

    `WsusUtil.exe configuressl server.contoso.com`
   
   Burada *Server.contoso.com* , WSUS sunucusunun FQDN 'sidir.
   
1. WsusUtil, WSUS sunucusunun URL 'sini sonunda belirtilen bağlantı noktası numarasıyla birlikte döndürür. Bağlantı noktası 8531 (varsayılan) ya da 443 olacaktır. Döndürülen URL 'nin beklendiğini doğrulayın. Bir hata yanlış olursa, komutu yeniden çalıştırabilirsiniz.

   :::image type="content" source="media/wsusutil.png" alt-text="WSUS için HTTPS URL 'sini döndüren WSUSutil configuressl komutu":::

> [!TIP] 
> WSUS sunucunuz internet 'e sunul, çalışırken dış FQDN 'yi belirtin `WsusUtil.exe configuressl` .

## <a name="verify-the-wsus-console-can-connect-using-ssl"></a><a name="bkmk_wsus_console"></a> WSUS konsolunun SSL kullanarak bağlanabildiğini doğrulayın

WSUS konsolu bağlantı için Apıremoting30 Web hizmetini kullanır. Configuration Manager yazılım güncelleştirme noktası (SUP), WSUS 'yi aşağıdaki gibi belirli eylemleri gerçekleştirmek üzere yönlendirmek için de aynı Web hizmetini kullanır:

- Yazılım güncelleştirme eşitlemesi başlatılıyor
- SUP sitesinin Configuration Manager hiyerarşinizde bulunduğu yere bağlı olan WSUS için uygun yukarı akış sunucusunu ayarlama
- Hiyerarşinin en üst düzey WSUS sunucusundan eşitleme için ürün ve sınıflandırmalar ekleme veya kaldırma.
- Süre dolma güncelleştirmeleri kaldırılıyor

WSUS sunucusunun Apıremoting30 Web hizmetine bir SSL bağlantısı kullanacağınızı doğrulamak için WSUS konsolunu açın. Diğer Web hizmetlerinden bazılarını daha sonra test edeceğiz.

1. WSUS konsolunu açın ve **Action**  >  **sunucuya Bağlan**' ı seçin.
1. **Sunucu adı** SEÇENEĞI için WSUS sunucusunun FQDN 'sini girin.
1. WSUSutil adresinden URL 'de döndürülen **bağlantı noktası numarasını** seçin.

1. **Bu sunucuya bağlanmak için güvenli yuva katmanı kullan (SSL)** seçeneği, 8531 (varsayılan) veya 443 seçildiğinde otomatik olarak etkinleştirilir.

       :::image type="content" source="media/connect-wsus-console.png" alt-text="Connect to the WSUS console over the HTTPS port":::
       
1. Configuration Manager site sunucunuz, yazılım güncelleştirme noktasından uzak ise, site sunucusundan WSUS konsolunu başlatın ve WSUS konsolunun SSL üzerinden bağlanabildiğini doğrulayın.
   - Uzak WSUS konsolu bağlanamıyorsa, büyük olasılıkla sertifika, ad çözümlemesi veya engellenen bağlantı noktası ile ilgili bir sorun olduğunu gösterir.

## <a name="configure-the-software-update-point-to-require-ssl-communication-to-the-wsus-server"></a><a name="bkmk_cm_sup"></a> Yazılım güncelleştirme noktasını WSUS sunucusuna SSL iletişimi gerektirecek şekilde yapılandırma

WSUS, TLS/SSL kullanmak üzere ayarlandığında, karşılık gelen Configuration Manager yazılım güncelleştirme noktasını SSL 'yi gerektirecek şekilde güncelleştirmeniz gerekir. Bu değişikliği yaptığınızda Configuration Manager şunları yapar:

- Yazılım güncelleştirme noktası için WSUS sunucusunu yapılandırabildiğini doğrulama
- İstemcileri, bu WSUS sunucusunda tarama yapıldığında SSL bağlantı noktasını kullanacak şekilde yönlendirin.

Yazılım güncelleştirme noktasını WSUS sunucusuna SSL iletişimi gerektirecek şekilde yapılandırmak için aşağıdaki adımları uygulayın: 

1. Configuration Manager konsolunu açın ve düzenlemeniz gereken yazılım güncelleştirme noktası için merkezi yönetim sitenize veya birincil site sunucusuna bağlanın.
1. **Yönetime**  >  **genel bakış**  >  **site yapılandırma**  >  **sunucuları ve site sistem rolleri '** ne gidin.
1. WSUS 'nin yüklü olduğu site sistem sunucusunu seçin, sonra yazılım güncelleştirme noktası site sistemi rolünü seçin.
1. Şeritte **Özellikler**' i seçin.
1. **WSUS sunucusu Ile SSL Iletişimini gerektir** seçeneğini etkinleştirin.

   :::image type="content" source="media/sup-properties.png" alt-text="WSUS sunucusu için SSL iletişimi ıste seçeneğini gösteren SUP özellikleri":::
   
1. Site için [**WCM. log**](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) dosyasında, değişikliği uyguladığınızda aşağıdaki girişleri görürsünüz:

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

Bu senaryoya yönelik gereksiz bilgileri kaldırmak için günlük dosyası örnekleri düzenlendi.  

## <a name="verify-functionality-with-configuration-manager"></a><a name="bkmk_cm_verify"></a> Configuration Manager işlevleri doğrulama

### <a name="verify-the-site-server-can-sync-updates"></a>Site sunucusunun güncelleştirmeleri eşitleyebildiğini doğrulama

1. Configuration Manager konsolunu en üst düzey siteye bağlayın.
1. **Yazılım kitaplığı**'na  >  **genel bakış**  >  **yazılım**güncelleştirme  >  **tüm yazılım güncelleştirmeleri**' ne gidin.
1. Şeritte, **yazılım güncelleştirmelerini eşitler**' ı seçin.
1. Yazılım güncelleştirmeleri için site genelinde bir eşitleme başlatmak isteyip istemediğinizi soran bildirime **Evet** ' i seçin.

   - WSUS yapılandırması değiştiğinden, bir Delta eşitlemesi yerine tam yazılım güncelleştirmeleri eşitlemesi gerçekleşmeyecektir.
   
1. Site için **wsyncmgr. log** ' i açın. Bir alt siteyi izliyorsanız, önce üst sitenin eşitlemeyi bitirmesini beklemeniz gerekir. Aşağıdakine benzer girişlerin günlüğünü inceleyerek sunucunun başarıyla eşitlendikten emin olun:

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="verify-a-client-can-scan-for-updates"></a>Bir istemcinin güncelleştirme taraması bildiğini doğrulama

Yazılım güncelleştirme noktasını SSL isteyecek şekilde değiştirdiğinizde Configuration Manager istemciler, yazılım güncelleştirme noktası için bir konum isteği yaptığında güncelleştirilmiş WSUS URL 'sini alırlar. Bir istemciyi test ederek şunları yapabilirsiniz:
-  İstemcinin WSUS sunucusunun sertifikasına güvendiğini belirleme. 
- SimpleAuthWebService ve WSUS için ClientWebService çalışır.
-  WSUS içerik sanal dizini, tarama sırasında istemci EULA 'Yı almaya başladıysanız çalışır.

1. Son zamanlarda TLS/SSL kullanmak için değiştirilen yazılım güncelleştirme noktasına göre tarayan bir istemciyi belirler. Bir istemciyi tanımlamaya yönelik yardıma ihtiyacınız varsa, aşağıdaki PowerShell betiği ile [çalıştırma betikleri](../..//apps/deploy-use/create-deploy-scripts.md) kullanın:

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```

1. Test istemciniz üzerinde bir yazılım güncelleştirme tarama döngüsünü çalıştırın. Aşağıdaki PowerShell betiği ile taramaya zorlayabilirsiniz:

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```

1. Yazılım güncelleştirme noktasına karşı taranacak iletinin alındığını doğrulamak için istemcinin **Scanagent. log dosyasına** bakın.

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
      <ForceScan>TRUE</ForceScan>
      <UpdateSourceIDs>
            <ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
      </UpdateSourceIDs>
    </UpdateSourceMessage>'
   ```

1. İstemcinin doğru WSUS URL 'sini görbildiğini doğrulamak için **LocationServices. log** ' i gözden geçirin.
**LocationServices.log**

   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. İstemcinin başarıyla tarayacağını doğrulamak için **WUAHandler. log** ' i gözden geçirin.

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="next-steps"></a>Sonraki adımlar

[Yazılım güncelleştirmelerini dağıtma](../deploy-use/deploy-software-updates.md)
