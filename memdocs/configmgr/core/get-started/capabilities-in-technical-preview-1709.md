---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1709 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b3cb491ff3bfb10935566c33e321542435d2e0af
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692919"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Configuration Manager için Technical Preview 1709 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1709 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanma, sürümler arasında güncelleştirme yapma ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlama hakkında bilgi almak üzere [Configuration Manager Için Teknik önizlemeyi](../../core/get-started/technical-preview.md) gözden geçirin.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bu teknik önizlemede bilinen sorunlar:**
- **Pasif modda bir site sunucunuz varsa, Preview sürüm 1709 ' e güncelleştirme başarısız olur**. Önizleme sürümünü 1706, 1707 veya 1708 çalıştırdığınızda ve [pasif modda bir birincil site sunucusuna](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)sahip olduğunuzda, önizleme sitenizi sürüm 1709 ' e başarıyla güncelleştirebilmeniz için Pasif mod site sunucusunu kaldırmanız gerekir. Siteniz sürüm 1709 ' i çalıştırdıktan sonra Pasif mod site sunucusunu yeniden yükleyebilirsiniz.

  Pasif mod site sunucusunu kaldırmak için:
  1. Konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **sunucuları ve site sistem rolleri**' ne gidin ve Pasif mod site sunucusunu seçin.
  2. **Site sistemi rolleri** bölmesinde, **site sunucusu** rolüne sağ tıklayın ve ardından **rolü kaldır**' ı seçin.
  3. Pasif mod site sunucusuna sağ tıklayın ve ardından **Sil**' i seçin.
  4. Site sunucusu kaldırıldıktan sonra, etkin birincil site sunucusunda hizmeti **CONFIGURATION_MANAGER_UPDATE**yeniden başlatın.


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Configuration Manager konsolunda geliştirilmiş VPN profili deneyimi
<!-- 1313282 -->
Bu sürümle birlikte, VPN profili Sihirbazı ve Özellikler sayfalarını seçili platforma uygun ayarları görüntüleyecek şekilde güncelleştirdik. Özellikle:

- Her platformun kendi iş akışı vardır, yani yeni VPN profillerinin yalnızca platform tarafından desteklenen ayarı vardır.
- **Desteklenen platformlar** sayfaları artık **genel** sayfasından sonra görüntülenir.  Artık özellik değerlerini ayarlamadan önce platformu seçersiniz.
- Platform **Android**, **Android for Work**veya **Windows Phone 8,1**olarak ayarlandığında, **Desteklenen platformlar** sayfası gerekli değildir ve gösterilmez.
- Configuration Manager istemci tabanlı iş akışı, karma mobil cihaz (MDM) istemci tabanlı Windows 10 iş akışlarıyla birleştirilmiştir. aynı ayarları destekler.
- Her platform iş akışı yalnızca ilgili iş akışına uygun olan ayarları içerir.  Örneğin, Android iş akışı Android için uygun ayarları içerir; iOS veya Windows 10 Mobile için uygun olan ayarlar artık Android iş akışında görünmez.
- Windows 8.1 cihazlarda, Configuration Manager tarafından yönetilen ayarlar açıkça işaretlenir.
- Otomatik VPN sayfası artık kullanılmıyor ve kaldırıldı.

Bu değişiklikler yeni VPN profilleri için geçerlidir.  

Uyumluluk riskini en aza indirmek için mevcut VPN profilleri değiştirilmez.  Mevcut bir profili düzenlediğinizde, ayarlar profil oluşturulduğu sırada olduğu gibi görüntülenir.  

### <a name="try-it-out"></a>Deneyin!

Olağan süreci kullanarak yeni bir VPN profili oluşturun. VPN profili Sihirbazı 'nın seçeneklerindeki ilk sayfanın değiştiğini unutmayın.

1. **Varlıklar ve uyum**  >  **genel bakış**  >  **Uyumluluk ayarları**  >  **Şirket kaynağı erişimi**  >  **VPN profilleri** ' ne gidin ve ardından **VPN profili oluştur**' u seçin.
2. **Genel** sayfasında bir ad girin ve **oluşturmak istediğiniz VPN profili türünü belirtin**altında aşağıdaki seçeneklerden birini belirleyin:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS ve macOS  
    - Android  
    - Android for Work  

3. **Windows 8.1**' yi seçerseniz, **Yeni profil oluşturma** veya **Dosyadan içeri aktarma**seçeneğiniz de vardır.
4. Profili oluşturmayı tamamlayacak Sihirbazı doldurun.

Farklı platformları seçerken, yalnızca seçili platformla ilgili ayarların görüntülendiğine dikkat edin.

## <a name="co-management-for-windows-10-devices"></a>Windows 10 cihazları için ortak yönetim    
<!-- 1350871 -->
Birçok müşteri, Windows 10 cihazlarını Basitleştirilmiş, daha düşük maliyetli, bulut tabanlı bir çözüm kullanarak mobil cihazları yönetecek şekilde yönetmek ister. Ancak, geleneksel yönetimden modern yönetime geçiş yapmak zor olabilir. Windows 10, sürüm 1607 (yıldönümü güncelleştirmesi olarak da bilinir) ile başlayarak, bir Windows 10 cihazını şirket içi Active Directory (AD) ve bulut tabanlı Azure AD 'ye de aynı anda (karma Azure AD) katabilirsiniz. Ortak yönetim, bu iyileştirmelerden yararlanır ve hem Configuration Manager hem de Intune kullanarak Windows 10 cihazlarını eşzamanlı olarak yönetmenizi sağlar. Geleneksel ve modern yönetime köprü sağlayan ve bir aşamalı yaklaşım kullanarak geçişi yapmak için size yol veren bir çözümdür. 

### <a name="prerequisites"></a>Ön koşullar
Ortak yönetimi etkinleştirebilmeniz için aşağıdaki önkoşulların yerine gelmelidir. Genel Önkoşullar ve istemci olmayan mevcut Configuration Manager istemcileri ve cihazları için farklı Önkoşullar vardır.

### <a name="known-issues"></a>Bilinen sorunlar
Ortak yönetim ilkesi oluşturduktan sonra, ilkeyi düzenleyemezsiniz. İlkeyi değiştirmek için, silin ve ardından ihtiyacınız olan ayarlarla yeniden oluşturun. 

#### <a name="general-prerequisites"></a>Genel önkoşullar
Ortak yönetimi etkinleştirmek için aşağıdaki genel Önkoşullar verilmiştir:  

- Configuration Manager sürüm 1709 için teknik önizleme
- Azure AD 
- Tüm kullanıcılar için EMS veya Intune lisansı
- Intune 'da Intune aboneliği &#40;MDM **yetkilisi Intune 'a ayarlanır&#41;**

   > [!Note]  
   > Karma MDM ortamınız varsa (Configuration Manager ile tümleşik Intune), ortak yönetimi etkinleştiremezsiniz.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Mevcut Configuration Manager istemcileri için ek önkoşullar
- Windows 10, sürüm 1709 (Fall Creators Update) ve üzeri
- Karma Azure AD 'ye katılmış (AD ve Azure AD 'ye katılmış)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Yeni Windows 10 cihazları için ek önkoşullar
- Windows 10, sürüm 1709 (Fall Creators Update) ve üzeri
- Configuration Manager [bulut yönetimi ağ geçidi](../clients/manage/manage-clients-internet.md#cloud-management-gateway)

### <a name="workloads-you-can-switch-to-intune"></a>Intune 'a geçiş yapmak için iş yükleri
Ortak yönetimi etkinleştirdikten sonra, Configuration Manager tüm iş yüklerini yönetmeye devam eder. Hazır olmaya karar verirken, Intune 'un kullanılabilir iş yüklerini yönetmeye başlamasını sağlayabilirsiniz. Bu sürümde, Intune 'un aşağıdaki iş yüklerini yönetmesini sağlayabilirsiniz.   

#### <a name="compliance-policies"></a>Uyumluluk ilkeleri
Uyumluluk ilkeleri, bir cihazın koşullu erişim ilkeleriyle uyumlu kabul edilmesi için uyması gereken kuralları ve ayarları tanımlar. Uyumluluk ilkelerini ayrıca, koşullu erişimden bağımsız olarak cihazlardaki uyumluluk sorunlarını izlemek ve gidermek için de kullanabilirsiniz.

#### <a name="windows-update-for-business-policies"></a>Iş ilkeleri için Windows Update
Iş ilkeleri için Windows Update, Windows 10 özellik güncelleştirmeleri için erteleme ilkelerini veya doğrudan Iş Windows Update tarafından yönetilen Windows 10 cihazları için kalite güncelleştirmelerini yapılandırmanızı sağlar. Ayrıntılar için bkz. [iş erteleme ilkelerini Windows Update yapılandırma](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Ortak yönetilen cihazlar için Azure 'da Intune 'da bulunan uzak eylemler
Ortak yönetim için bir Windows 10 cihazı etkinleştirildiğinde, Azure 'da Intune 'dan kullanabileceğiniz aşağıdaki uzak eylemlere sahipsiniz:  
- [Fabrika Sıfırlaması](/intune/devices-wipe#wipe)
- [Seçmeli silme](/intune/apps-selective-wipe)
- [Cihazları Sil](/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Cihazı yeniden başlatma](/intune/device-restart)
- [Yeni başlangıç](/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Intune 'U ortak yönetim için hazırlama
İş yüklerini Intune 'a Configuration Manager geçiş yapmadan önce, cihazlarınızın korumaya devam etmesini sağlamak için Intune 'da ihtiyacınız olan profilleri ve ilkeleri oluşturun.
Intune 'da, Configuration Manager sahip olduğunuz nesneleri temel alan nesneler oluşturabilirsiniz. Ya da, geçerli stratejiniz eski veya geleneksel Yönetimi temel alıyorsa, modern yönetim için hangi ilkelerin ve profillerin ihtiyacınız olduğunu yeniden düşünmek üzere bir adım geri almak isteyebilirsiniz. İlkeleri ve profilleri oluşturmak için aşağıdaki kaynakları kullanın.    
<!-- - [Device compliance policies](/intune/compliance-policy-create-windows)  -->
- [Iş ilkeleri için Windows Update](/intune/windows-update-for-business-configure)  
- [Cihaz yapılandırma profilleri](/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Ortak yönetim için mimari genel bakış
Aşağıdaki diyagramda ortak yönetime yönelik mimari genel bakış ve mevcut yapılandırma ve Intune altyapısına nasıl uyum sağlanmıştır.

![Ortak yönetim mimari diyagramı](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Ortak yönetimi etkinleştirme senaryoları  
Hem Microsoft Intune hem de mevcut Windows 10 Configuration Manager istemcilerinde kayıtlı Windows 10 cihazları için ortak yönetimi etkinleştirebilirsiniz. Her iki senaryo da Configuration Manager ve Intune tarafından aynı anda yönetilen Windows 10 cihazlarının yanı sıra AD ve Azure AD 'ye katılmış olarak sonuçlanır.  

#### <a name="devices-enrolled-in-intune"></a>Intune'a kayıtlı cihazlar  
Windows 10 cihazları Intune 'A kaydolduğunda, istemcileri ortak yönetime hazırlamak için cihazlara Configuration Manager istemcisini (belirli bir komut satırı bağımsız değişkenini kullanarak) yükleyebilirsiniz. Daha sonra, belirli iş yüklerini belirli Windows 10 cihazları için Intune 'a taşımaya başlamak üzere Configuration Manager konsolundan ortak yönetimi etkinleştirirsiniz.  

Intune 'a henüz kaydolmayan Windows 10 cihazlarında, cihazları kaydetmek için Azure 'da otomatik kaydı kullanabilirsiniz. Yeni Windows 10 cihazları için Windows AutoPilot ' yi kullanarak, cihazları Intune 'da kaydeden otomatik kaydı içeren kutudan çıkan deneyimi (OOBE) yapılandırabilirsiniz.  

#### <a name="configuration-manager-clients"></a>Configuration Manager istemcileri
Configuration Manager istemcileri olan Windows 10 cihazlarınız varsa, bu cihazları kaydedebilir ve Configuration Manager konsolundan ortak yönetimi etkinleştirebilirsiniz. Configuration Manager, Azure AD kiracı bilgilerine göre otomatik olarak Intune 'a kayıt tetikler.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Windows 10 cihazları ortak yönetim için hazırlama
AD ve Azure AD 'ye katılmış ve Intune 'a ve Configuration Manager bir istemciye kayıtlı olan Windows 10 cihazlarında ortak yönetimi etkinleştirebilirsiniz. Yeni Windows 10 cihazları ve Intune 'da zaten kayıtlı olan cihazlar için, ortak yönetilebilmesi için önce Configuration Manager istemcisini yükleyebilirsiniz. Zaten Configuration Manager istemcileri olan Windows 10 cihazlarında, cihazları Intune 'a kaydedebilir ve Configuration Manager konsolunda ortak yönetimi etkinleştirebilirsiniz.

#### <a name="command-line-to-install-configuration-manager-client"></a>Configuration Manager istemcisi 'ni yüklemek için komut satırı
Intune 'da, zaten Configuration Manager istemcileri olmayan Windows 10 cihazları için bir uygulama oluşturun. Uygulamayı sonraki bölümlerde oluşturduğunuzda, aşağıdaki komut satırını kullanın:

ccmsetup.msi CCMSETUPCMD = "/MP: &#60;*bulut yönetim ağ geçidi karşılıklı kimlik doğrulama uç noktası*&#62;/ccmhostname =&#60;*bulut yönetimi ağ geçidi karşılıklı kimlik doğrulama uç noktası*&#62; Smssitekodu =&#60;*sitekodu*&#62; smsmp = https: mp &#47;/&#60;*FQDN 'si*&#62; AADTENANTıD =&#60;*AAD kiracı kimliği*&#62; AADTENANTNAME =&#60;*kiracı adı*&#62; Aadclientappıd =&#60;*AAD tümleştirme Için sunucu appıd*&#62; aadresourceuri = https: &#47;/&#60;*kaynak kimliği*&#62;"

Örneğin, aşağıdaki değerlere sahipseniz:

- **Bulut yönetimi ağ geçidi karşılıklı kimlik doğrulama uç noktası URL 'si**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >**Bulut yönetimi ağ geçidi karşılıklı kimlik doğrulama uç noktası değerinin URL 'si** için **VProxy_Roles** SQL görünümünde **mutualauthpath** değerini kullanın.

- **Yönetim noktası FQDN 'si (MP)**: sccmmp.Corp.contoso.com    
- **Sitekodu**: ps1    
- **Azure AD KIRACı kimliği**: 72f988bf-86F1-41AF-91AB-2D7CD011XXXX    
- **Azure AD kiracı adı**: contoso    
- **Azure AD İstemci UYGULAMASı kimliği**: bef323b3-042F-41a6-907A-f9faf0d1XXXX     
- **AAD kaynak kimliği URI 'si**: configmgrserver    

  > [!Note]    
  > **AAD kaynak KIMLIĞI URI** değeri için **vSMS_AAD_Application_Ex** SQL görünümünde bulunan **ıdentifieruri** değerini kullanın.

Aşağıdaki komut satırını kullanabilirsiniz:

ccmsetup.msi CCMSETUPCMD = "/MP: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME = contoso. cloudapp. net/CCM_Proxy_MutualAuth/72057594037928100 Smssitekodu = PS1 SMSMP = https:/&#47;sccmmp.corp.contoso.com AADTENANTıD = 72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME = contoso AADCLIENTAPPıD = bef323b3-042F-41a6-907A-f9faf0d1XXXX AADRESOURCEURI = https:/&#47;ConfigMgrServer"

> [!Tip]
>Aşağıdaki adımları kullanarak sitenizin komut satırı parametrelerini bulabilirsiniz:     
> 1. Configuration Manager konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.  
> 2. Giriş sekmesinde, Yönet grubunda ortak yönetim Ekleme Sihirbazı 'nı açmak için **ortak yönetimi Yapılandır** ' ı seçin.    
> 3. Abonelik sayfasında, **oturum aç** ' a tıklayın ve Intune kiracınızda oturum açın ve ardından **İleri**' ye tıklayın.    
> 4. Etkinleştirme sayfasında, komut satırını panoya kopyalamak için **Intune 'a kayıtlı cihazlar** bölümünde **Kopyala** ' ya tıklayın ve ardından uygulamayı oluşturmak için yordamda kullanmak üzere komut satırını kaydedin.  
> 5. Sihirbazdan çıkmak için **iptal** ' e tıklayın.

#### <a name="new-windows-10-devices"></a>Yeni Windows 10 cihazları
Yeni Windows 10 cihazları için Autopilot hizmetini kullanarak cihazı AD ve Azure AD 'ye katılmayı ve cihazı Intune 'a kaydetmeyi de kapsayan, kullanıma hazır deneyimi yapılandırabilirsiniz. Daha sonra, Intune 'da Configuration Manager istemcisini dağıtmak için bir uygulama oluşturun.  
1. Yeni Windows 10 cihazları için AutoPilot etkinleştirin. Ayrıntılar için bkz. [Windows Autopilot 'e genel bakış](/windows/deployment/windows-10-auto-pilot).  
2. Cihazlarınızın otomatik olarak Intune 'a kaydolması için Azure AD 'de otomatik kaydı yapılandırın. Ayrıntılar için bkz. [Windows cihazlarını Microsoft Intune kaydetme](/intune/windows-enroll).
3. Intune 'da Configuration Manager istemci paketiyle bir uygulama oluşturun ve uygulamayı ortak yönetmek istediğiniz Windows 10 cihazlarına dağıtın. [Azure AD 'yi kullanarak istemcileri Internet 'ten yüklemeye](/sccm/core/clients/deploy/deploy-clients-cmg-azure)yönelik adımlara gittiğinizde [Configuration Manager Client 'ı yüklemek için komut satırını](#command-line-to-install-configuration-manager-client) kullanın.   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Intune 'A veya bir Configuration Manager istemcisine kaydolmayan Windows 10 cihazları
Intune 'a kayıtlı olmayan veya Configuration Manager istemcisine sahip Windows 10 cihazlarında, cihazı Intune 'a kaydetmek için otomatik kayıt kullanabilirsiniz. Daha sonra, Intune 'da Configuration Manager istemcisini dağıtmak için bir uygulama oluşturun.
1. Cihazlarınızın otomatik olarak Intune 'a kaydolması için Azure AD 'de otomatik kaydı yapılandırın. Ayrıntılar için bkz. [Windows cihazlarını Microsoft Intune kaydetme](/intune/windows-enroll).  
2. Intune 'da Configuration Manager istemci paketiyle bir uygulama oluşturun ve uygulamayı ortak yönetmek istediğiniz Windows 10 cihazlarına dağıtın. [Azure AD 'yi kullanarak istemcileri Internet 'ten yüklemeye](/sccm/core/clients/deploy/deploy-clients-cmg-azure)yönelik adımlara gittiğinizde [Configuration Manager Client 'ı yüklemek için komut satırını](#command-line-to-install-configuration-manager-client) kullanın.

#### <a name="windows-10-devices-enrolled-in-intune"></a>Intune 'A kayıtlı Windows 10 cihazları
Intune 'a zaten kayıtlı olan Windows 10 cihazlarında, Configuration Manager istemcisini dağıtmak için Intune 'da bir uygulama oluşturun. [Azure AD 'yi kullanarak istemcileri Internet 'ten yüklemeye](/sccm/core/clients/deploy/deploy-clients-cmg-azure)yönelik adımlara gittiğinizde [Configuration Manager Client 'ı yüklemek için komut satırını](#command-line-to-install-configuration-manager-client) kullanın.  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Configuration Manager iş yüklerinin Intune'a geçişi
Önceki bölümde, ortak yönetim için Windows 10 cihazları hazırladınız. Bu cihazlar artık AD ve Azure AD 'ye katıldı ve Intune 'a kaydolmuş ve Configuration Manager istemcisine sahip. Büyük olasılıkla AD 'ye katılmış olan ve Configuration Manager istemcisine katılmış ancak Azure AD 'ye katılmamış ya da Intune 'a kayıtlı olmayan Windows 10 cihazlara sahip olabilirsiniz. Aşağıdaki yordam ortak yönetimi etkinleştirme, geri kalan Windows 10 cihazlarınızı (Intune kaydı olmayan Configuration Manager istemcileri) ortak yönetim için hazırlama ve belirli Configuration Manager iş yüklerini Intune 'a geçişe başlayabilmeniz için gereken adımları sağlar.

1. Configuration Manager konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.    
2. Giriş sekmesinde, Yönet grubunda ortak yönetim Ekleme Sihirbazı 'nı açmak için **ortak yönetimi Yapılandır** ' ı seçin.    
3. Abonelik sayfasında, **oturum aç** ' a tıklayın ve Intune kiracınızda oturum açın ve ardından **İleri**' ye tıklayın.   
4. Hazırlama sayfasında, aşağıdaki ayarları yapılandırın ve ardından **İleri**' ye tıklayın:
    - **Pilot grup**: pilot grubu, seçtiğiniz bir veya daha fazla koleksiyonu içerir. Bu grubu, ortak yönetim 'in aşamalı olarak piyasaya çıkmalarınızın bir parçası olarak kullanın. Küçük bir test koleksiyonuyla başlayabilir ve daha fazla Kullanıcı ve cihaza ortak yönetimi kullanıma sunarak pilot grubuna daha fazla koleksiyon ekleyebilirsiniz. Pilot grubundaki koleksiyonları ortak yönetim özelliklerinden dilediğiniz zaman değiştirebilirsiniz.
    - **Üretim**: Bu ayarı seçtiğinizde, tüm desteklenen Windows 10 cihazları ortak yönetim için etkinleştirilir. **Dışlama grubunu** bir veya daha fazla koleksiyon ile yapılandırın. Bu gruptaki koleksiyonların herhangi birinin üyesi olan cihazlar ortak yönetim kullanılarak hariç tutulur. 
5. Etkinleştirme sayfasında, Intune 'da otomatik kaydı etkinleştirmek üzere **pilot** veya **Tümü** (hazırlama sayfasında yapılandırdığınız ayarlara bağlı olarak) seçeneğini belirleyin ve ardından **İleri**' ye tıklayın. **Pilot**' ı seçtiğinizde yalnızca pilot grubunun üyesi olan Configuration Manager Istemcileri Intune 'a otomatik olarak kaydedilir. Bu, başlangıçta ortak yönetimi test etmek ve aşamalı bir yaklaşım kullanarak ortak yönetimi sunmak için bir istemciler alt kümesinde ortak yönetimi etkinleştirmenizi sağlar. 
6. Iş yükleri sayfasında, Intune tarafından yönetilmek üzere Configuration Manager iş yüklerini geçip geçmeyeceğinizi seçin ve ardından **İleri**' ye tıklayın. Çalışma yükünü pilot grubuna veya tüm Windows 10 istemcilerine (hazırlama sayfasında yapılandırdığınız ayarlara bağlı olarak) geçiş yapılıp yapılmayacağını seçmek için kaydırıcıları kullanın. 
7. Ortak yönetimi etkinleştirmek için Sihirbazı doldurun.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Ayrıca bkz.
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).