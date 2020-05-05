---
title: İşletim sistemi dağıtımı için güvenlik ve gizlilik
titleSuffix: Configuration Manager
description: Configuration Manager işletim sistemi dağıtımı için güvenlik ve Gizlilik en iyi yöntemleri hakkında bilgi edinin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724429"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Configuration Manager işletim sistemi dağıtımı için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Configuration Manager işletim sistemi dağıtımı özelliği için güvenlik ve gizlilik bilgilerini içerir.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a>İşletim sistemi dağıtımı için en iyi güvenlik uygulamaları  

Configuration Manager ile işletim sistemlerini dağıtırken aşağıdaki en iyi güvenlik uygulamalarını kullanın:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Önyüklenebilir medyayı korumak için erişim denetimleri uygulayın

Önyüklenebilir medya oluştururken, medyanın korunmasına yardımcı olmak için her zaman bir parola atayın. Bir parolayla bile, yalnızca hassas bilgiler içeren dosyaları şifreler ve tüm dosyaların üzerine yazılabilir.  

Bir saldırganın istemci kimlik doğrulaması sertifikasını almak amacıyla şifreleme saldırılarını kullanmasını önlemek için medyaya fiziksel erişimi denetleyin.  

Bir istemcinin, üzerinde oynanmış bir içerik veya istemci ilkesi yüklemesini önlemeye yardımcı olmak için içeriğe karma uygulanır ve içerik orijinal ilkeyle kullanılmalıdır. İçerik karması başarısız olursa veya içeriğin ilkeyle eşleşip eşleşmediğini denetlemezse, istemci önyüklenebilir medyayı kullanmaz. Yalnızca içerik karma hale getirilir. İlke karma değildir, ancak bir parola belirttiğinizde şifrelenir ve güvenli hale getirilir. Bu davranış, bir saldırganın ilkeyi başarıyla değiştirmesini zorlaştırır.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>İşletim sistemi görüntüleri için medya oluştururken güvenli bir konum kullanın

Yetkisiz kullanıcıların konuma erişimi varsa, bu dosyalar oluşturduğunuz dosyalarla oynayabilir. Medya oluşturma işlemi başarısız olması için tüm kullanılabilir disk alanını da kullanabilirler.  


### <a name="protect-certificate-files"></a>Sertifika dosyalarını koruma 

Sertifika dosyalarını (. pfx) güçlü bir parolayla koruyun. Bunları ağda depolarsanız, ağ kanalını içeri aktarırken güvenli hale getirin Configuration Manager

Önyüklenebilir medya için kullandığınız istemci kimlik doğrulaması sertifikasını içeri aktarmak için parola istediğinizde bu yapılandırma, sertifikayı saldırgandan korumaya yardımcı olur.  

Saldırganların sertifika dosyasını izinsiz şekilde değiştirmesini engellemek için ağ konumu ile site sunucusu arasında SMB imzası veya IPsec kullanın.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Güvenliği aşılmış sertifikaları engelleme veya iptal etme 

İstemci sertifikası tehlikeye atılırsa, Configuration Manager sertifikayı engelleyin. Bu bir PKI sertifikasıysa, iptal edin.  

Bir işletim sistemini önyüklenebilir medya ve PXE önyüklemesi kullanarak dağıtmak için özel anahtara sahip bir istemci kimlik doğrulama sertifikasına sahip olmanız gerekir. Bu sertifika tehlikedeyse, **Yönetim** çalışma alanında **Güvenlik** düğümündeki **Sertifikalar** düğümünde bu sertifikayı engelleyin.  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Site sunucusu ve SMS sağlayıcısı arasındaki iletişim kanalının güvenliğini sağlama

SMS Sağlayıcısı site sunucusundan uzakta olduğunda, önyükleme görüntülerini korumak için iletişim kanalının güvenliğini sağlayın.

Önyükleme görüntülerini değiştirirken ve SMS Sağlayıcısı site sunucusu olmayan bir sunucuda çalıştığında, önyükleme görüntüleri saldırıya açık olur. SMB imzalama veya IPsec kullanarak bu bilgisayarlar arasındaki ağ kanalını koruyun.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Yalnızca güvenli ağ kesimlerinde PXE istemcisi iletişimi için dağıtım noktalarını etkinleştirin

Bir istemci bir PXE önyükleme isteği gönderdiğinde, isteğin geçerli bir PXE 'yi destekleyen dağıtım noktası tarafından hizmet edildiğinden emin olmanız mümkün değildir. Bu senaryoda aşağıdaki güvenlik riskleri bulunur:  

- PXE isteklerine yanıt veren standart dışı bir dağıtım noktası, istemcilere, üzerinde oynanmış bir görüntü sağlayabilir.  

- Saldırgan, PXE tarafından kullanılan TFTP protokolüne karşı ortadaki adam saldırısı başlatabilir. Bu saldırı, işletim sistemi dosyalarıyla kötü amaçlı kod gönderebilir. Saldırgan Ayrıca, TFTP isteklerini doğrudan dağıtım noktasına yapmak için standart dışı bir istemci oluşturabilir.  

- Saldırgan, dağıtım noktasına yönelik bir hizmet reddi saldırısı başlatmak için kötü amaçlı bir istemci kullanabilir.  

İstemcilerin PXE 'yi destekleyen dağıtım noktalarına erişen ağ kesimlerini korumak için derinlemesine savunma kullanın.  

> [!WARNING]  
>  Bu güvenlik riskleri nedeniyle, bir çevre ağı gibi güvenilmeyen bir ağda olduğunda PXE iletişimi için bir dağıtım noktası etkinleştirmeyin.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>PXE'yi destekleyen dağıtım noktalarını yalnızca belirtilen ağ arabirimlerindeki PXE isteklerine yanıt verecek şekilde yapılandırın  

Dağıtım noktasının tüm ağ arabirimlerindeki PXE isteklerine yanıt vermesine izin verirseniz bu yapılandırma, PXE hizmetini güvenilmeyen ağlara maruz bırakabilir  


### <a name="require-a-password-to-pxe-boot"></a>PXE önyüklemesi için parola isteyin

PXE önyüklemesi için parola gerektiğinde, bu yapılandırma PXE önyükleme işlemine ek bir güvenlik düzeyi ekler. Bu yapılandırma Configuration Manager hiyerarşisine katılan standart dışı istemcilere karşı korumaya yardımcı olur.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>PXE önyüklemesi veya çok noktaya yayın için kullanılan işletim sistemi görüntülerinde içeriği kısıtlama

PXE önyüklemesi veya çok noktaya yayın için kullandığınız bir görüntüde hassas veriler içeren iş kolu uygulamalarını veya yazılımlarını eklemeyin.  

PXE önyüklemesi ve çok noktaya yayın ile ilgili devralınmış güvenlik riskleri nedeniyle, standart dışı bir bilgisayar işletim sistemi görüntüsünü indirdiğinde riskleri azaltın.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Görev dizisi değişkenlerine göre yüklenen içeriği kısıtla

Görev dizileri değişkenlerini kullanarak yüklediğiniz uygulamalar paketlerinde hassas veriler içeren iş kolu uygulamalarını veya yazılımlarını eklemeyin.  

Yazılım, görev dizileri değişkenlerini kullanarak dağıttığınızda, bu yazılımı alma yetkisi olmayan bilgisayarlara ve kullanıcılara yüklenebilir.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Kullanıcı durumunu geçirirken ağ kanalının güvenliğini sağlama

Kullanıcı durumunu geçirirken, SMB imzalama veya IPSec kullanarak istemci ile durum geçiş noktası arasındaki ağ kanalının güvenliğini sağlayın.  

HTTP üzerinden ilk bağlantının ardından, kullanıcı durumu geçirme verileri SMB kullanılarak aktarılır. Ağ kanalını güvenli hale ayarlamazsanız, bir saldırgan bu verileri okuyabilir ve değiştirebilir.  


### <a name="use-the-latest-version-of-usmt"></a>USMT 'nin en son sürümünü kullanma

Configuration Manager tarafından desteklenen Kullanıcı Durumu Taşıma Aracı (USMT) en son sürümünü kullanın.  

USMT'nin en son sürümünde, kullanıcı durumu verilerinin geçirilmesiyle ilgili güvenlik geliştirmeleri ve daha fazla denetim sağlanmaktadır.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Durumları kullanımdan kaldırdığınızda durum geçiş noktalarında klasörleri el ile silin  

Durum geçiş noktası özelliklerindeki Configuration Manager konsolundaki bir durum geçiş noktası klasörünü kaldırdığınızda, site fiziksel klasörü silmez. Kullanıcı durumu taşıma verilerini bilgilerin açığa çıkmasına karşı korumak için, ağ payını el ile kaldırın ve klasörü silin.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Silme ilkesini, Kullanıcı durumunu hemen silecek şekilde yapılandırmayın  

Silinmek üzere işaretlenen verileri hemen kaldırmak üzere durum geçiş noktasındaki silme ilkesini yapılandırırsanız ve bir saldırgan geçerli bilgisayardan önce Kullanıcı durumu verilerini almayı yönetirse, site Kullanıcı durumu verilerini hemen siler. **Sonra sil** aralığını, kullanıcı durumu verilerinin başarıyla geri yüklendiğini doğrulamaya yetecek kadar uzun olacak şekilde ayarlayın.  


### <a name="manually-delete-computer-associations"></a>Bilgisayar ilişkilendirmelerini el ile silme 

Kullanıcı durumu taşıma verilerini geri yükleme işlemi tamamlandığında ve doğrulandığında bilgisayar ilişkilendirmelerini el ile silin.

Configuration Manager, bilgisayar ilişkilendirmelerini otomatik olarak kaldırmaz. Artık gerekli olmayan bilgisayar ilişkilendirmelerini el ile silerek kullanıcı durumu verilerinin kimliğini korumaya yardımcı olma.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Durum geçiş noktasındaki kullanıcı durumu geçirme verilerini el ile yedekleyin  

Configuration Manager yedekleme, site yedeklemesinde Kullanıcı durumu geçiş verilerini içermez.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Önceden hazırlanan medyayı korumak için erişim denetimleri uygulayın  

Bir saldırganın istemci kimlik doğrulaması sertifikasını ve önemli verileri almak amacıyla şifreleme saldırılarını kullanmasını önlemek için medyaya fiziksel erişimi denetleyin.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Başvuru bilgisayarı görüntüleme işlemini korumak için erişim denetimleri uygulayın  

İşletim sistemi görüntülerini yakalamak için kullandığınız başvuru bilgisayarının güvenli bir ortamda olduğundan emin olun. Beklenmeyen veya kötü amaçlı yazılımların yüklenememesi ve yakalanan görüntüye istenmeden dahil edilmesini sağlamak için uygun erişim denetimlerini kullanın. Görüntüyü yakaladığınızda, hedef ağ konumunun güvenli olduğundan emin olun. Bu işlem, görüntüyü yakaladıktan sonra görüntünün üzerinde oynanamaz olmasına yardımcı olur.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Başvuru bilgisayarına daima en yeni güvenlik güncelleştirmelerini yükleyin  

Başvuru bilgisayarında güncel güvenlik güncelleştirmeleri mevcut olduğunda, bu durum, yeni bilgisayarlar ilk defa başlatıldığında bu bilgisayarlarda yaşanacak güvenlik açığı süresini azaltır.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Bilinmeyen bir bilgisayara işletim sistemi dağıtımında erişim denetimleri uygulama

Bilinmeyen bir bilgisayara işletim sistemi dağıtmanız gerekiyorsa, yetkisiz bilgisayarların ağa bağlanmasını engellemek için erişim denetimleri uygulayın.  

Bilinmeyen bilgisayarların sağlanması, yeni bilgisayarları isteğe bağlı olarak dağıtmak için kullanışlı bir yöntem sağlar. Ancak, bir saldırganın ağınızda güvenli bir şekilde güvenilir bir istemci haline gelmesine de izin verebilir. Ağa fiziksel erişimi kısıtlayın ve yetkisiz bilgisayarları algılamak için istemcileri izleyin. 

PXE tarafından başlatılan bir işletim sistemi dağıtımına yanıt veren bilgisayarlar, işlem sırasında tüm verileri yok edebilir. Bu davranış, yanlışlıkla yeniden biçimlendirilmiş sistemlerin kullanılabilirliği kaybına neden olabilir.  


### <a name="enable-encryption-for-multicast-packages"></a>Çok noktaya yayın paketleri için şifrelemeyi etkinleştirin  

Her işletim sistemi dağıtım paketi için, Configuration Manager paketi çok noktaya yayın kullanarak aktarırken şifrelemeyi etkinleştirebilirsiniz. Bu yapılandırma, standart dışı bilgisayarların çok noktaya yayın oturumuna katılmasını önlemeye yardımcı olur. Ayrıca, saldırganların iletim üzerinde oynama yapmasını önlemeye de yardımcı olur.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Yetkisiz çok noktaya yayını destekleyen dağıtım noktalarını izleyin  

Saldırganlar ağınıza erişebiliyorsa, standart dışı çok noktaya yayın sunucularını işletim sistemi dağıtımına sızması için yapılandırabilirler.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Görev dizilerini bir ağ konumuna aktardığınızda konumun ve ağ kanalının güvenliğini sağlayın

Ağ klasörüne erişebilecek kişileri kısıtlayın.  

Saldırganların dışarı aktarılan görev dizisinde oynama yapmasını önlemek için ağ konumu ile site sunucusu arasında SMB imzalama veya IPsec kullanın.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Görev sırası farklı çalıştır hesabını kullanıyorsanız, ek güvenlik önlemleri alın

[Görev sırası farklı çalıştır hesabını](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)kullanıyorsanız aşağıdaki önlem amaçlı adımları uygulayın:  

- Mümkün olan en düşük izinlere sahip bir hesap kullanın.  

- Bu hesap için ağ erişim hesabı kullanmayın.  

- Hesabı asla etki alanı yöneticisi yapmayın.  

- Bu hesap için asla dolaşım profilleri yapılandırmayın. Görev sırası çalıştırıldığında, hesap için dolaşım profilini indirir, bu, profilin yerel bilgisayardaki erişime açık kalmasına neden olur.  

- Hesabın kapsamını sınırlandırın. Örneğin, her bir görev dizisi için farklı görev dizisi farklı çalıştır hesapları oluşturun. Bir hesap tehlikeye girerse, yalnızca bu hesabın erişimi olan istemci bilgisayarlarının güvenliği aşılmış olur. Komut satırı bilgisayarda yönetici erişimi gerektiriyorsa, yalnızca görev dizisi farklı çalıştır hesabı için bir yerel yönetici hesabı oluşturmayı düşünün. Bu yerel hesabı görev dizisini çalıştıran tüm bilgisayarlarda oluşturun ve artık gerekli olmadığı anda hesabı silin.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>İşletim sistemi Deployment Manager güvenlik rolü verilen yönetici kullanıcılarını kısıtlayın ve izleyin

**Işletim sistemi dağıtım Yöneticisi** güvenlik rolü verilen yönetici kullanıcılar, otomatik olarak imzalanan sertifikalar oluşturabilir. Bu sertifikalar daha sonra, bir istemcinin kimliğine bürünmek ve Configuration Manager istemci ilkesi almak için kullanılabilir.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Ağ erişim hesabı gereksinimini azaltmak için gelişmiş HTTP kullanın

Sürüm 1806 ' den başlayarak, [GELIŞMIŞ http](../../core/plan-design/hierarchy/enhanced-http.md)'yi etkinleştirdiğinizde, çeşitli işletim sistemi dağıtım senaryoları bir dağıtım noktasından içerik indirmek için bir ağ erişim hesabı gerektirmez. Daha fazla bilgi için bkz. [görev dizileri ve ağ erişim hesabı](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>İşletim sistemi dağıtımı için güvenlik sorunları  

İşletim sistemi dağıtımı, ağınızdaki bilgisayarlar için en güvenli işletim sistemlerini ve konfigürasyonları dağıtmanın uygun bir yolu olabilir, ancak aşağıdaki güvenlik riskleri de vardır:  


### <a name="information-disclosure-and-denial-of-service"></a>Bilgilerin açığa çıkması ve hizmet reddi  

Bir saldırgan Configuration Manager altyapınızın denetimini elde edebilir, herhangi bir görev dizisini çalıştırabilir. Bu işlem, tüm istemci bilgisayarların sabit sürücülerinin biçimlendirilmesini içerebilir. Görev dizileri, önemli bilgileri (örneğin, etki alanına katılma izinleri olan hesaplar ve toplu lisanslama anahtarları) içerecek şekilde yapılandırılabilir.  


### <a name="impersonation-and-elevation-of-privileges"></a>Kimliğe bürünme ve ayrıcalıkların yükseltilmesi  

Görev dizileri, bir bilgisayarın etki alanına katılmasını sağlayabilir ve bu da standart dışı bir bilgisayara kimlik doğrulamalı ağ erişimi sağlayabilir. 

Önyüklenebilir görev sırası medyası ve PXE önyükleme dağıtımı için kullanılan istemci kimlik doğrulama sertifikasını koruyun. Bir istemci kimlik doğrulaması sertifikasını yakaladığınızda, bu işlem, bir saldırganın sertifikadaki özel anahtarı elde etme olanağı sunar. Bu sertifika, ağdaki geçerli bir istemcinin kimliğine bürünmesini sağlar. Bu senaryoda dolandırıcı bilgisayar, duyarlı verileri içerebilen ilkeyi indirebilir.  

İstemciler durum yükseltme noktasında depolanan verilere erişmek için ağ erişim hesabı 'nı kullanıyorsa bu istemciler, aynı kimliği etkin bir şekilde paylaşır. Ağ erişim hesabı kullanan başka bir istemciden durum geçiş verilerine erişebilirler. Veriler şifrelenir, böylece bu verileri yalnızca orijinal istemci okuyabilir; ancak verilerle oynanabilir veya veriler silinebilir.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>Durum geçiş noktasına istemci kimlik doğrulaması, yönetim noktası tarafından verilen bir Configuration Manager belirteci kullanılarak elde edilir.  

Configuration Manager, durum geçiş noktasında depolanan verilerin miktarını sınırlamaz veya yönetmez. Bir saldırgan kullanılabilir disk alanını doldurup hizmet reddine neden olabilir.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Koleksiyon değişkenleri kullanıyorsanız yerel yöneticiler olası duyarlı bilgileri okuyabilir  

Koleksiyon değişkenleri işletim sistemlerini dağıtmak için esnek bir yöntem sunmakla birlikte, bu özellik bilgilerin açığa çıkmasına neden olabilir.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a>İşletim sistemi dağıtımı için gizlilik bilgileri  

Bir işletim sistemini bilgisayar olmadan bilgisayarlara dağıtmaya ek olarak, Configuration Manager kullanıcıların dosyalarını ve ayarlarını bir bilgisayardan başka bir bilgisayara geçirmek için kullanılabilir. Kişisel veri dosyaları, yapılandırma ayarları ve tarayıcı tanımlama bilgileri dahil olmak üzere yönetici, hangi bilgilerin aktarılacağını yapılandırır.  

Configuration Manager, bilgileri bir durum geçiş noktasına depolar ve iletim ve depolama sırasında şifreler. Yalnızca durum bilgileriyle ilişkili yeni bilgisayar depolanan bilgileri alabilir. Yeni bilgisayar, bilgileri almak için anahtarı kaybederse, bilgisayar ilişkilendirme örnek nesnelerinde **Kurtarma bilgilerini görüntüle** hakkı olan bir Configuration Manager yöneticisi bilgilere erişebilir ve yeni bir bilgisayarla ilişkilendirebilir. Yeni bilgisayar durum bilgilerini geri yükledikten sonra, varsayılan olarak bir gün sonra verileri siler. Silme için işaretlenen verilerin durum yükseltme noktası tarafından ne zaman kaldırılacağını yapılandırabilirsiniz. Configuration Manager durum geçiş bilgilerini site veritabanında depolamaz ve Microsoft 'a göndermez.  

İşletim sistemi görüntülerini dağıtmak için Önyükleme medyası kullanıyorsanız, önyükleme medyasını parolayla korumak için her zaman varsayılan seçeneği kullanın. Parola görev sırasında depolanan tüm değişkenleri şifreler, ancak bir değişkende depolanmayan bilgiler ifşaya açık olabilir.  

İşletim sistemi dağıtımı, uygulamaların ve yazılım güncelleştirmelerinin yüklenmesini içeren dağıtım işlemi sırasında birçok farklı görevi gerçekleştirmek için görev dizilerini kullanabilir. Görev sıralarını yapılandırdığınızda aynı zamanda yazılım yüklemeye ait gizlilik bilgilerine de dikkat etmeniz gerekir.  

Configuration Manager, varsayılan olarak işletim sistemi dağıtımını uygulamaz. Kullanıcı durum bilgilerini toplamadan veya görev dizileri veya önyükleme görüntüleri oluşturmadan önce çeşitli yapılandırma adımları gerektirir.  

İşletim sistemi dağıtımını yapılandırmadan önce gizlilik gereksinimlerinizi göz önünde bulundurun.  



## <a name="see-also"></a>Ayrıca bkz.

[Tanılama ve kullanım verileri](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Configuration Manager için güvenlik ve gizlilik](../../core/plan-design/security/security-and-privacy.md)
