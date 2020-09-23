---
title: Microsoft Intune-Azure için bir VPN çözümü olan Microsoft Tunnel Gateway için dosya ve komut başvurusu | Microsoft Docs
description: Linux üzerinde çalışan bir VPN sunucusu olan Microsoft tünel ağ geçidini yüklemek veya yönetmek için kullandığınız araçlara yönelik dosya ve komut satırı başvurularını bulun.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 950e1d20ab975bd3c6b3dfa37a83a69a4ae88a62
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017745"
---
# <a name="reference-for-microsoft-tunnel-gateway"></a>Microsoft Tunnel Gateway için başvuru

Microsoft Tunnel Gateway 'e yönelik bu başvurudaki bilgiler, ortamınızda tünel yüklemesinin yüklenmesini ve bakımını desteklemek için sağlanır.

## <a name="mst-cli-command-line-tool-for-microsoft-tunnel-gateway"></a>MST-Microsoft tünel ağ geçidi için CLI komut satırı aracı

**MST-CLI** , Microsoft tüneli ağ geçidi ile kullanmak için bir komut satırı aracıdır. Bu araç, tünele yüklemeyi tamamladıktan sonra Linux sunucusunda kullanılabilir ve **/usr/sbin/MST-cli**adresinde bulunur. Bu aracı kullanabileceğiniz bazı görevler şunları içerir:

- Tünel sunucusu hakkında bilgi alın.
- Tünel sunucusunun yapılandırmasını ayarlayın veya güncelleştirin.
- Tünel sunucusunu yeniden başlatın.
- Tünel sunucusunu kaldırın.
Aracının ortak komut satırı kullanımları aşağıda verilmiştir.

**Komut satırı arabirimi**:  

- `mst-cli –help` -Kullanım: **MST-CLI [komut]**

  Komut  
  - `agent` -Aracı bileşeni üzerinde çalışır.
  - `server` -Sunucu bileşeni üzerinde çalışır.
  - `uninstall` -Microsoft tüneli 'ni kaldırın.
  - `eula` -EULA 'Yı gösterin.
  - `import_cert` -TLS sertifikasını içeri aktarın.

- `mst-cli agent –help` -Kullanım: **MST-CLI Aracısı [komut]**

  Komut  
  - `logs` -Aracı günlüklerini göster (daha fazla bilgi için-h).
  - `status` -Aracı durumunu gösterin.
  - `start` -Aracı hizmetini başlatın.
  - `stop` -Aracı hizmetini durdurun.
  - `restart` -Aracı hizmetini yeniden başlatın.

- `mst-cli agent logs   help` -Kullanım: **MST-CLI Aracı günlükleri [bayraklar]**

  Larına
  - `-f, --follow` -Günlük çıkışını izleyin. Varsayılan değer false.
  - `--since string` -ZAMAN DAMGASıNDAN itibaren günlükleri gösterin.
  - `--tail uint` -Günlüklerin sonunda belirtilen satır sayısını çıkar.  Varsayılan olarak, tüm satırları yazdıran sıfır (0) olur.
  - `-t, --timestamps` -Günlükteki zaman damgalarını çıkış.

- `mst-cli agent status` -Aşağıdaki örnekler, görebileceğiniz sonuçlara örnektir:  
  - Durum: çalışıyor  
  - Sistem durumu: sağlıklı

- `mst-cli agent start` -Durdurulmuşsa, Aracıyı başlatır.

- `mst-cli agent stop` -Aracıyı sonlandırır.  Durdurulduktan sonra el ile başlatılmış olması gerekir.

- `mst-cli agent restart` -Aracıyı yeniden başlatır.

- `mst-cli server --help` -Kullanım: **MST-CLI sunucusu [komut]**

  Komut
  - `logs` -Sunucu günlüklerini görüntüleyin. Daha fazla bilgi için **-h** kullanın.
  - `status` -Sunucu durumunu gösterin.
  - `start` -Sunucu hizmetini başlatın.
  - `stop` -Sunucu hizmetini durdurun.
  - `restart` -Sunucu hizmetini yeniden başlatın.
  - `show` -Çeşitli sunucu istatistiklerini gösterin. Daha fazla bilgi için **-h** kullanın.

- `mst-cli server logs –help` -Kullanım: **MST-CLI sunucu günlükleri [bayraklar]**

  Larına
  - `-f, --follow` -Günlük çıkışını izleyin. Varsayılan değer false.
  - `--since string` -ZAMAN DAMGASıNDAN itibaren günlükleri göster
  - `--tail uint` -Günlüklerin sonunda belirtilen satır sayısını çıkar.  Varsayılan olarak, tüm satırları yazdıran sıfır (0) olur.
  - `-t, --timestamps` -Günlükteki zaman damgalarını çıkış.

- `mst-cli server status` -Aşağıdaki örnekler, görebileceğiniz sonuçlara örnektir:

  - Durum: çalışıyor
  - Sistem durumu: sağlıklı

- `mst-cli server start` -Durdurulmuşsa sunucu başlatılır.

- `mst-cli server stop` -Sunucuyu sonlandırır.  Durdurulduktan sonra el ile başlatılmış olması gerekir.

- `mst-cli server restart` -Sunucuyu yeniden başlatır.

- `mst-cli server show`
  - `show status` -Sunucunun durumunu ve istatistiklerini yazdırır.
  - `show users` -Bağlı kullanıcıları yazdırır.
  - `show ip bans` -Yasaklanmış IP adreslerini yazdırır.
  - `show ip ban points` -Noktalara sahip olan tüm bilinen IP adreslerini yazdırır.
  - `show iroutes` -Sunucu kullanıcıları tarafından belirtilen yolları yazdırır.
  - `show sessions all` -Tüm oturum kimliklerini yazdırır.
  - `show sessions valid` -Tüm yeniden bağlanma oturumlarını yazdır.
  - `show session [SID]` -Belirtilen oturumdaki bilgileri yazdırır.
  - `show user [NAME]` -Belirtilen kullanıcı hakkındaki bilgileri yazdırır.
  - `show id [ID]` -Belirtilen KIMLIK hakkındaki bilgileri yazdırır.
  - `show events` -Kullanıcıları bağlama hakkında bilgi sağlar.
  - `show cookies all` -Tüm oturumları göster için diğer ad.
  - `show cookies valid` -Geçerli oturum göster için diğer ad.

## <a name="environment-variables"></a>Ortam değişkenleri

Linux sunucusuna Microsoft Tunnel Gateway yazılımını yüklerken yapılandırmak isteyebileceğiniz ortam değişkenleri aşağıda verilmiştir. Bu değişkenler **/etc/mstunnel/env.sh**ortam dosyasında bulunur:

- **http_proxy**= [address]-proxy sunucunuzun http adresi.
- **https_proxy**= [address]-proxy sunucunuzun https adresi. 

## <a name="data-paths"></a>Veri yolları  

| Yol/dosya                       | Açıklama             | İzinler |
|---------------------------------|-------------------------|------------|
| /.../mstunnel                     | Tüm yapılandırma için kök dizin.   | Sahip kökü, Grup mstunnel |
| /.../mstunnel/admin-settings.js | Sunucu yüklemesi için ayarları içerir.   *Bu dosya Intune tarafından yönetiliyor ve el ile düzenlenmemelidir*. | |
| /.../mstunnel/certs               | TLS sertifikasının depolandığı dizin.  | Sahip kökü, Grup mstunnel |
| /.../mstunnel/private             |Intune aracı sertifikasının ve TLS özel anahtarının depolandığı dizin. | Sahip kökü, Grup mstunnel |

## <a name="files-add-during-server-installation"></a>Sunucu yüklemesi sırasında dosya ekleme

**/etc/mstunnel**:

- **admin-settings.js**:
  - Intune 'dan serileştirilmiş *sunucu yapılandırmasını* içerir.
  - Sunucu kaydolduktan sonra oluşturulur.

- **agent-info.js**:
  - Kayıt tamamlandığında oluşturulur.
  - ,, Intunetenantid, Aadtenantıd ve Aracı sertifikası RenewalDate.
  - Aracı sertifikası yenilemesinde güncelleştirildi.

- **Private/Agent. p12**:
  - Intune 'da aracı kimlik doğrulaması için kullanılan PFX sertifikası.
  - Otomatik olarak yenilendi.

- **version-info.js**:
  - Çeşitli bileşenler için sürüm bilgilerini içerir.
  - ConfigVersion, DockerVersion, Ker Tımagehash, AgentCreateDate, ServerImageHash, ServerCreateDate.

- **ocserv. conf**:
  - Sunucu yapılandırması

- **Images_configured**

**Kapsayıcıları oluşturmak için kullanılan Docker görüntüleri**:

- te Tımagedigest
- serverImageDigest

### <a name="example-of-admin-settingsjson"></a>admin-settings.jsörneği

``` JSON
{
"PolicyName": "Auto Generated Policy for rh7vm",
   "DisplayName": "rh7vm Policy",
   "Description": "This policy was auto generated for rh7vm",  
   "Network": "169.100.0.0/16",
   "DNSServers": ["168.63.129.16"],
   "DefaultDomainSuffix": "nmqjwlanybmubp4imht0k2b4qd.xx.internal.cloudapp.net",
   "RoutesInclude": ["default"],
   "RoutesExclude": [],
   "ListenPort": 443
}
```

| Yönetici ayarı     | Açıklama                           |
|-------------------|---------------------------------------|
| PolicyName          |Ayarlar ilkesinin adı. Adı seçebilirsiniz.       |
| DisplayName         |  Kısa görünen ad. Adı seçebilirsiniz.              |
| Açıklama        | İlkenin açıklaması. Açıklamayı seçebilirsiniz. |
| Ağ             | İstemci sanal adreslerini atamak için kullanılacak maskeyle ağ. Çakışmadığınız müddetçe bunun değiştirilmesi gerekmez. Bu ayar 64.000 istemcisini destekleyecektir. |
| DNSServers          | İstemcinin kullanması gereken DNS sunucularının listesi.  Bu sunucular iç kaynakların adreslerini çözümleyebilir. |
| DefaultDomainSuffix | İstemci, kaynakları çözümlemeye çalışırken ana bilgisayar adına eklenen etki alanı son eki. |
| Kabatesınclude       | VPN aracılığıyla yönlendirilecek yolların listesi.  Varsayılan değer tüm yollardır. |
| RoutesExclude       | VPN 'i atlaması gereken yolların listesi.                 |
| ListenPort          | VPN sunucusunun trafik alacağı bağlantı noktası.          |

## <a name="docker-commands"></a>Docker komutları

Aşağıda, bir tünel sunucusundaki sorunları araştırmanız gerekiyorsa kullanabileceğiniz Docker için ortak komutlar verilmiştir.

Komut satırı arabirimi:

- `docker ps –a` – Tüm kapsayıcılara bakın.
  - *mstunnel-Server* – bu kapsayıcı **ocserv** Server bileşenlerini çalıştırır ve gelen bağlantı noktası 443 *(varsayılan)* veya özel bir bağlantı noktası yapılandırması kullanır.
  - *mstunnel-Agent* -bu kapsayıcı Intune bağlayıcısını çalıştırır ve 443 giden bağlantı noktasını kullanır.

- **Docker 'ı yeniden başlatmak için**:  
  - `systemctl restart docker`

- **Bir kapsayıcıda bir şey çalıştırmak için**:
  - `docker exec –it mstunnel-server bash`
  - `docker exec –it mstunnel-agent bash`

## <a name="linux-commands"></a>Linux komutları

Aşağıda, bir tünel sunucusuyla kullanabileceğiniz yaygın Linux komutları verilmiştir.

- `sudo su` – Kutunun üzerinde kök oluşturur.  Aşağıdaki komutları çalıştırmadan önce ve mstunnel-Setup ' ı çalıştırmadan önce bu komutu kullanın.

- `ls` – dizinin içeriğini listeleyin.

- `ls – l` – Zaman damgaları dahil olmak üzere dizinin içeriğini listeleyin.

- `cd` – başka bir dizine geçin. Örneğin, `cd /etc/test/stuff` *kök* dizinden ve, > *Test* alt klasörüne ve *etc* sonra da *dosyalar* klasörüne >.

- `cp <source> <destination>` -Sertifikaları doğru konuma kopyalamak için kullanışlıdır.

- `ln –s <source> <target>` -Bir softlink oluşturun.

- `curl <URL>` – Bir Web sitesine erişimi denetler. Örnek: `curl https://microsoft.com`

- `./<filename>` -Bir betiği çalıştırın.
