---
title: Azure Microsoft Intune SCEP sertifika profillerini kullanma | Microsoft Docs
description: Microsoft Intune ile Basit Sertifika Kayıt Protokolü (SCEP) sertifika profilleri oluşturun ve atayın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0119ace5e1ec511ec0e8235a1dcea4b7199c058
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559547"
---
# <a name="create-and-assign-scep-certificate-profiles-in-intune"></a>Intune 'da SCEP sertifika profilleri oluşturma ve atama

Altyapınızı Basit Sertifika Kayıt Protokolü (SCEP) sertifikalarını destekleyecek şekilde [yapılandırdıktan](certificates-scep-configure.md) sonra, Intune 'da kullanıcılara ve cihazlara SCEP sertifika profilleri oluşturup atayabilirsiniz.

> [!IMPORTANT]
> Cihazların bir SCEP sertifika profili kullanması için, güvenilen kök sertifika yetkilinizin (CA) güvenmesi gerekir. Kök CA 'nın güveni, [güvenilir bir sertifika profilinin](../protect/certificates-configure.md#create-trusted-certificate-profiles) , SCEP sertifika profilini alan aynı gruba dağıtılmasıyla en iyi şekilde belirlenir. Güvenilen sertifika profilleri, güvenilen kök CA sertifikasını temin edin.

## <a name="create-a-scep-certificate-profile"></a>Bir SCEP sertifika profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. Seçin ve **cihazlar**  >  **yapılandırma profilleri**  >  **Profil oluştur**' a gidin.

3. Aşağıdaki özellikleri girin:
   - **Platform**: cihazlarınızın platformunu seçin.
   - **Profil**: **SCEP sertifikası** seçin

     **Android kurumsal** platformu Için, *profil türü* Iki kategoriye, *tam olarak yönetilen, adanmış ve şirkete ait Iş profiline* ve *yalnızca iş profiline*bölünmüştür. Yönettiğiniz cihazlar için doğru SCEP sertifika profilini seçtiğinizden emin olun.  

     *Tam olarak yönetilen, adanmış ve şirkete ait Iş profili* profılı için SCEP sertifika profilleri aşağıdaki sınırlamalara sahiptir:

      1. Izleme altında, sertifika raporlama cihaz sahibi SCEP sertifika profilleri için kullanılamaz.

      2. Cihaz sahipleri için SCEP sertifika profilleri tarafından sağlanan sertifikaları iptal etmek için Intune 'U kullanamazsınız. İptali bir dış işlem veya doğrudan sertifika yetkilisi ile yönetebilirsiniz.

      3. Android kurumsal adanmış cihazlarda, SCEP sertifika profilleri Wi-Fi ağ yapılandırması, VPN ve kimlik doğrulaması için desteklenir. Android kurumsal adanmış cihazlarda SCEP sertifika profilleri, uygulama kimlik doğrulaması için desteklenmez.

4. **Oluştur**’u seçin.

5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:
   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı *şirketin tamamına ait SCEP profilidir*.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, aşağıdaki yapılandırmaları doldurun:

   - **Sertifika türü**:

     *(İçin geçerlidir: Android, Android Enterprise, iOS/ıpados, macOS, Windows 8.1 ve üzeri ve Windows 10 ve üzeri.)*

     Sertifika profilini nasıl kullanacağınızı gösteren bir tür seçin:

     - **Kullanıcı**: *Kullanıcı* sertifikaları hem Kullanıcı hem de cihaz özniteliklerini, sertifikanın konu ve San 'ı içerebilir.  
     - **Cihaz**:  *cihaz* sertifikaları, sertifikanın konu ve San 'ı yalnızca cihaz özniteliklerini içerebilir.

       **Cihazı** , kiosks gibi Kullanıcı-daha az cihazlar veya Windows cihazları gibi senaryolar için kullanın. Windows cihazlarında, sertifika yerel bilgisayar sertifika deposuna yerleştirilir.

     > [!NOTE]
     > MacOS 'ta, SCEP ile sağladığınız sertifikalar her zaman cihazın sistem anahtarlığınıza (sistem deposuna) yerleştirilir.
 
   - **Konu adı biçimi**:

     Intune 'un sertifika isteğinde konu adını otomatik olarak nasıl oluşturduğunu seçin. Konu adı biçimi için seçenekler, **Kullanıcı** veya **cihaz**' ı seçtiğiniz sertifika türüne bağlıdır.

     > [!NOTE]
     > Elde edilen sertifika Imzalama Isteğindeki (CSR) konu adı, kaçış karakteri olarak aşağıdaki karakterlerden birini içerdiğinde (bir ters eğik çizgiyle devam eder), sertifika almak için SCEP kullanmanın [bilinen bir sorunu](#avoid-certificate-signing-requests-with-escaped-special-characters) vardır \\ :
     > - \+
     > - ;
     > - ,
     > - =

     - **Kullanıcı sertifika türü**

       *Konu adı biçimi* için biçim seçenekleri şunları içerir:

       - **Yapılandırılmadı**
       - **Ortak ad**
       - **E-postayı içeren ortak ad**
       - **E-posta olarak ortak ad**
       - **IMEI (Uluslararası Mobil Donanım Kimliği)**
       - **Seri numarası**
       - **Özel**: Bu seçeneği işaretlediğinizde bir **Özel** metin kutusu da gösterilir. Bu alanı, değişkenler dahil özel bir konu adı biçimi girmek için kullanın. Özel biçim, şu iki değişkeni destekler: **Ortak Ad (CN)** ve **E-posta (E)**. **Ortak Ad (CN)** şu iki değerden biri olarak ayarlanabilir:

         - **CN = {{username}}**: kullanıcının Kullanıcı adı (örneğin, ocetikan).
         - **CN = {{userPrincipalName}}**: kullanıcının Kullanıcı asıl adı, örneğin janedoe@contoso.com .\*
         - **CN={{AAD_Device_ID}}**: Azure Active Directory’ye (AD) yeni bir cihaz kaydettiğinizde atanan bir kimlik. Bu kimlik genellikle Azure AD’de kimlik doğrulamak için kullanılır.
         - **CN = {{SERIALNUMBER}}**: genellikle üretici tarafından bir cihazı tanımlamak için kullanılan benzersiz seri numarası (sn).
         - **CN = {{ımekarmsayı}}**: bir cep telefonu tanımlamak Için kullanılan uluslararası mobil ekipman KIMLIĞI (IMEI) benzersiz numarası.
         - **CN = {{OnPrem_Distinguished_Name}}**: *CN = Gamze Etikan, OU = USERACCOUNTS, DC = Corp, DC = contoso, DC = com*gibi virgülle ayrılmış göreli ayırt edici adların sırası.

           *{{OnPrem_Distinguished_Name}}* değişkenini kullanmak Için, Azure AD 'nize [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) kullanarak *onpremisesdistinguishedname* Kullanıcı özniteliğini eşitlediğinizden emin olun.

         - **CN = {{onPremisesSamAccountName}}**: Yöneticiler, *adlı BIR*özniteliğe Azure AD connect kullanarak sAMAccountName ÖZNITELIĞINI Active Directory 'den Azure AD 'ye eşitleyebilir. Intune, bu değişkeni bir sertifika konusunun sertifika verme isteğinin bir parçası olarak kullanabilir. SamAccountName özniteliği, Windows 'un önceki bir sürümünden (Windows 2000 öncesi) istemcileri ve sunucuları desteklemek için kullanılan Kullanıcı oturum açma adıdır. Kullanıcı oturum açma adı biçimi: EtkiAlanıAdı \ *testuser*veya yalnızca *testuser*.

            *{{OnPremisesSamAccountName}}* değişkenini kullanmak Için, Azure AD 'nize [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) kullanarak *onPremisesSamAccountName* User özniteliğini eşitlediğinizden emin olun.

         Bu değişkenlerin ve statik dizelerin bir veya birkaç tanesinin bir bileşimini kullanarak aşağıdaki gibi özel bir konu adı biçimi oluşturabilirsiniz:  
         - **CN={{KullanıcıAdı}},E={{EpostaAdresi}},OU=Mobil,O=Finans Grubu,L=Redmond,ST=Washington,C=US**

         Bu örnekte, CN ve E değişkenlerini kullanan bir konu adı biçimi ve kuruluş birimi, kuruluş, konum, durum ve ülke değerleri için dizeler bulunur. [CertStrToName işlevi](https://msdn.microsoft.com/library/windows/desktop/aa377160.aspx), bu işlevi ve desteklenen dizelerini açıklar.
         
         \* Android tam olarak yönetilen, adanmış ve şirkete ait Iş profili profilleri için **CN = {{userPrincipalName}}** ayarı çalışmaz. Android tam olarak yönetilen, adanmış ve şirkete ait Iş profili profilleri kullanıcı olmayan cihazlarda kullanılabilir, bu nedenle kullanıcının Kullanıcı asıl adını alabilmesi mümkün olmayacaktır. Kullanıcılar için bu seçeneğe gerçekten ihtiyaç duyuyorsanız, şu şekilde bir geçici çözüm kullanabilirsiniz: **CN = {{username}} \@ contoso.com** , Kullanıcı adı ve el ile eklediğiniz etki alanı gibi janedoe@contoso.com

      - **Cihaz sertifika türü**

        Konu adı biçimi için biçim seçenekleri aşağıdaki değişkenleri içerir:

        - **{{AAD_Device_ID}}** veya **{{azureaddeviceıd}}** -her iki değişken de BIR cihazı Azure AD kimliğine göre belirlemek için kullanılabilir.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{Imekarmsayı}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEı}}**
        - **{{Aygıtadı}}**
        - **{{Fullyıqualifieddomainname}}** *(yalnızca Windows ve etki alanına katılmış cihazlar için geçerlidir)*
        - **{{MEıD}}**

        Bu değişkenleri ve metin kutusu içinde değişkeni için metni belirtebilirsiniz. Örneğin, *Device1* adlı bir cihazın ortak adı **CN = {{aygıtadı}} Device1**olarak eklenebilir.

        > [!IMPORTANT]
        > - Bir değişken belirttiğinizde, bir hatadan kaçınmak için, değişken adını örnekte görüldüğü gibi küme ayraçları {} içine alın.  
        > - **IMEI**, **SerialNumber**ve **fullyıqualifieddomainname**gibi bir cihaz sertifikasının *Konu* veya *San* 'ı üzerinde kullanılan cihaz özellikleri, cihaza erişimi olan bir kişi tarafından sızılmış özelliklerdir.
        > - Bir cihazın, bu cihaza yüklemek için bir sertifika profilinde belirtilen tüm değişkenleri desteklemesi gerekir.  Örneğin, bir SCEP profilinin konu adında **{{IMEI}}** kullanılıyorsa ve IMEI numarası olmayan bir cihaza atanırsa, profil yüklenemez.

   - **Konu diğer adı**: Intune 'un sertifika isteğinde konu alternatif adı 'Nı (San) otomatik olarak nasıl oluşturduğunu seçin. SAN seçenekleri seçtiğiniz sertifika türüne bağlıdır; **Kullanıcı** ya da **cihaz**.

      - **Kullanıcı sertifika türü**

        Kullanılabilir özniteliklerden seçin:

        - **E-posta adresi**
        - **Kullanıcı asıl adı (UPN)**

        Örneğin, Kullanıcı sertifika türleri konu alternatif adına Kullanıcı asıl adını (UPN) içerebilir. İstemci sertifikası bir Ağ İlkesi Sunucusunda kimlik doğrulamak için kullanılacaksa konu alternatif adını UPN'ye ayarlayın.

      - **Cihaz sertifika türü**

        **Öznitelik** açılan listesini kullanın ve bir öznitelik seçin, bir **değer**atayın ve bunu sertifika profiline **ekleyin** . Ek öznitelikler ' i seçerek birden çok değer ekleyebilirsiniz.

        Kullanılabilir öznitelikler şunlardır:

        - **E-posta adresi**
        - **Kullanıcı asıl adı (UPN)**
        - **DNS**

        *Cihaz* sertifika türüyle değer için aşağıdaki cihaz sertifika değişkenlerini kullanabilirsiniz:

        - **{{AAD_Device_ID}}** veya **{{azureaddeviceıd}}** -her iki değişken de BIR cihazı Azure AD kimliğine göre belirlemek için kullanılabilir.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{Imekarmsayı}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEı}}**
        - **{{Aygıtadı}}**
        - **{{Fullyıqualifieddomainname}}**
        - **{{MEıD}}**

        Bir özniteliğe ilişkin bir değer belirtmek için, değişken adını küme ayraçları ile, sonra da bu değişken için olan metinle birlikte ekleyin. Örneğin, DNS özniteliği için bir değer **{{Azureaddeviceıd}}. domain. com** ' u *. domain.com* ise metindir. *Kullanıcı1* adlı bir Kullanıcı Için e-posta adresi {{Fullyıqualifieddomainname}} olarak görünebilir User1@Contoso.com .

        > [!IMPORTANT]
        > - Bir cihaz sertifikası değişkeni kullanırken, değişken adını kaşlı ayraçlar {} içine alın.
        > - Değişkeni izleyen metinde süslü ayraçları **{}**, kanal sembolleri **|** ve noktalı virgül **;** kullanmayın.
        > - **IMEI**, **SerialNumber**ve **fullyıqualifieddomainname**gibi bir cihaz sertifikasının *Konu* veya *San* 'ı üzerinde kullanılan cihaz özellikleri, cihaza erişimi olan bir kişi tarafından sızılmış özelliklerdir.
        > - Bir cihazın, bu cihaza yüklemek için bir sertifika profilinde belirtilen tüm değişkenleri desteklemesi gerekir.  Örneğin, **{{IMEI}}** bir SCEP profilinin San 'ı içinde kullanılıyorsa ve IMEI numarası olmayan bir cihaza atanırsa, profil yüklenemez.

   - **Sertifika geçerlilik süresi**:

     Sertifika şablonundaki geçerlilik süresinden düşük bir değer girebilirsiniz ancak daha yüksek bir değer giremezsiniz. Sertifika şablonunu [Intune konsolu içinden ayarlanılabilecek özel bir değeri destekleyecek](certificates-scep-configure.md#modify-the-validity-period-of-the-certificate-template)şekilde yapılandırdıysanız, sertifikanın süresi dolmadan önce kalan süreyi belirtmek için bu ayarı kullanın.

     Örneğin, sertifika şablonunda sertifika geçerlilik süresi iki yılsa beş yıl değerini giremezsiniz ancak bir yıl değerini girebilirsiniz. Değerin, yayımlayan sertifika yetkilisinin sertifikası için kalan geçerlilik süresinden de düşük olması gerekir.

   - **Anahtar depolama sağlayıcısı (KSP)**:

     *(İçin geçerlidir: Windows 8.1 ve üzeri, ve Windows 10 ve üzeri)*

     Sertifika anahtarının depolanacağı yeri belirtin. Aşağıdaki değerlerden birini seçin:

     - **Varsa Güvenilir Platform Modülü (TPM) KSP'sine, aksi halde Yazılım KSP'sine kaydol**
     - **Güvenilir Platform Modülü (TPM) KSP'sine kaydol, aksi halde hata ver**
     - **Passport'a kaydet, aksi halde hata ver (Windows 10 ve üzeri)**
     - **Software KSP’ye kaydol**

   - **Anahtar kullanımı**:

     Sertifika için anahtar kullanım seçeneklerini belirleyin:

     - **Dijital imza**: Yalnızca anahtarın korunmasına bir dijital imza yardımcı olduğunda anahtar değişimine izin verir.
     - **Anahtar şifreleme**: Yalnızca anahtar şifreli olduğunda anahtar değişimine izin verir.

   - **Anahtar boyutu (bit)**:

     Anahtarda bulunan bitlerin sayısını seçin.

   - **Karma algoritması**:

     *(Android, Android Enterprise, Windows 8.1 ve üzeri ve Windows 10 ve üzeri için geçerlidir)*

     Bu sertifika ile kullanmak için kullanılabilir karma algoritma türlerinden birini seçin. Bağlanan cihazların destekleyeceği en güçlü güvenlik düzeyini seçin.

   - **Kök sertifika**:

     Daha önce yapılandırdığınız ve bu SCEP sertifika profili için geçerli kullanıcılara ve cihazlara atadığınız *Güvenilen sertifika profilini* seçin. Güvenilen sertifika profili, kullanıcılara ve cihazlara güvenilen kök CA sertifikası sağlamak için kullanılır. Güvenilen sertifika profili hakkında daha fazla bilgi için bkz. *Intune 'da kimlik doğrulaması için sertifikaları kullanma*' da [Güvenilen kök CA sertifikanızı dışarı aktarma](certificates-configure.md#export-the-trusted-root-ca-certificate) ve [Güvenilen sertifika profilleri oluşturma](certificates-configure.md#create-trusted-certificate-profiles) . Kök sertifika yetkiliniz ve veren bir sertifika yetkiliniz varsa, sertifikayı veren sertifika yetkilisini doğrulayan güvenilen kök sertifika profilini seçin.
     > [!NOTE]
     > İOS/ıpados cihazlarında, bir kök sertifika yetkiliniz ve veren bir sertifika yetkiliniz varsa, kök sertifika yetkilisini doğrulayan güvenilen kök sertifika profilini seçin. 

   - **Genişletilmiş anahtar kullanımı**:

     Sertifikanın amaçlanan amacı için değer ekleyin. Çoğu durumda, Kullanıcı veya cihazın bir sunucuda kimliğini doğrulayabilmesi için sertifika *istemci kimlik doğrulaması* gerektirir. Gerektiğinde ek anahtar kullanımları ekleyebilirsiniz.

   - **Yenileme eşiği (%)**:

     Cihazın sertifikayı yenilemeyi istemesi için kalan sertifika ömrünün yüzdesini girin. Örneğin, 20 girerseniz, sertifikanın %80 ' ı dolduğunda sertifikanın yenilenmesi denenir. Yenileme başarılı olana kadar yenileme denemeleri devam eder. Yenileme, yeni bir ortak/özel anahtar çifti ile sonuçlanan yeni bir sertifika oluşturur.

   - **SCEP sunucu URL 'leri**:

     SCEP aracılığıyla sertifika veren NDES sunucuları için bir veya daha fazla URL girin. Örneğin `https://ndes.contoso.com/certsrv/mscep/mscep.dll` gibi bir URI girebilirsiniz.

     Gerektiğinde yük dengeleme için ek SCEP URL 'Leri ekleyebilirsiniz. Cihazlar NDES sunucusuna üç ayrı çağrı yapar; sunucu yeteneklerini almak için, bir ortak anahtar alın ve ardından bir imzalama isteği gönderebilirsiniz. Birden çok URL kullandığınızda, Yük Dengeleme bir NDES sunucusuna sonraki çağrılar için farklı bir URL kullanılmasına neden olabilir. Aynı istek sırasında sonraki bir çağrı için farklı bir sunucuya bağlantı kurulursa, istek başarısız olur.

     NDES sunucu URL 'sini yönetme davranışı her bir cihaz platformuna özgüdür:

     - **Android**: CIHAZ, SCEP Ilkesinde alınan URL 'lerin listesini rasgeleleştirir ve sonra ERIŞILEBILIR bir NDES sunucusu bulunana kadar liste aracılığıyla çalışacaktır. Daha sonra cihaz, işlemin tamamında aynı URL 'yi ve sunucuyu kullanmaya devam eder. Cihaz NDES sunucularının hiçbirine erişemezse, işlem başarısız olur.
     - **iOS/ıpados**: Intune, URL 'leri rasgeleleştirir ve bir cihaza tek bir URL sağlar. Cihaz NDES sunucusuna erişemezse SCEP isteği başarısız olur.
     - **Windows**: NDES URL 'lerinin listesi rasgeledir ve ardından Windows cihazına geçirilir ve bu, kullanılabilir olana kadar bunları alınan sırayla dener. Cihaz NDES sunucularının hiçbirine erişemezse, işlem başarısız olur.

     Bir cihaz NDES sunucusuna yapılan üç çağrının herhangi biri sırasında aynı NDES sunucusuna başarıyla ulaşamazsa, SCEP isteği başarısız olur. Örneğin, bu, bir yük dengeleme çözümü NDES sunucusuna ikinci veya üçüncü çağrı için farklı bir URL sağlıyorsa veya NDES için sanallaştırılmış bir URL 'yi temel alan farklı bir gerçek NDES sunucusu sağlıyorsa meydana gelebilir. Başarısız bir istekten sonra cihaz, NDES URL 'Lerinin rastgele listesi (veya iOS/ıpados için tek URL) ile başlayarak sonraki ilke döngüsündeki işlemi yeniden dener.  

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

   **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

    **İleri**’yi seçin.

11. (*Yalnızca Windows 10 Için geçerlidir*) **Uygulanabilirlik kuralları**' nda, bu profilin atanmasını iyileştirmek için uygulanabilirlik kurallarını belirtin. Profili, bir cihazın işletim sistemi sürümüne veya sürümüne göre atamayı veya atamayı seçebilirsiniz.

   Daha fazla bilgi için *Microsoft Intune bir cihaz profili oluşturma*içindeki [uygulanabilirlik kuralları](../configuration/device-profile-create.md#applicability-rules) bölümüne bakın.

12. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. Oluştur ' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

### <a name="avoid-certificate-signing-requests-with-escaped-special-characters"></a>Kaçışlı özel karakterlerle sertifika imzalama isteklerinden kaçının

Bir kaçan karakter olarak aşağıdaki özel karakterlerden birini veya daha fazlasını içeren bir konu adı (CN) içeren SCEP ve PKCS sertifika istekleri için bilinen bir sorun vardır. Kaçış karakteri olarak özel karakterlerden birini içeren konu adları, yanlış konu adına sahip bir CSR 'de sonuçlanır. Yanlış konu adı, Intune SCEP sınama doğrulaması başarısız olur ve sertifika verilmemiş olur.

Özel karakterler şunlardır:
- \+
- ,
- ;
- =

Konu adınız özel karakterlerden birini içerdiğinde, bu sınırlamaya geçici bir çözüm bulmak için aşağıdaki seçeneklerden birini kullanın:

- Tırnak işaretleriyle özel karakteri içeren CN değerini kapsülle.  
- CN değerinden özel karakteri kaldırın.

**Örneğin**, *test kullanıcısı (TESTCOMPANY, LLC)* olarak görünen bir konu adı vardır.  *Testcompany* ve *LLC* arasında virgül bulunan BIR CN içeren bir CSR bir sorun gösterir.  Bu sorun, tüm CN 'nin çevresine tırnak işareti koyarak veya tam olarak *Testcompany* ile *LLC*arasında virgül kaldırılarak önlenebilir:

- **Tırnak Işaretleri ekleme**: *CN = "test kullanıcısı (TESTCOMPANY, LLC)", OU = useraccounts, DC = Corp, DC = contoso, DC = com*
- **Virgülü kaldırın**: *CN = test kullanıcısı (testcompany LLC), OU = useraccounts, DC = Corp, DC = contoso, DC = com*

 Ancak, bir ters eğik çizgi karakterini kullanarak virgül kaçış girişimleri, CRP günlüklerinde hata vererek başarısız olur:
 
- **Kaçan virgül**: *CN = test kullanıcısı (testcompany \\ , LLC), OU = useraccounts, DC = Corp, DC = contoso, DC = com*

Hata aşağıdaki hatayla benzerdir:

```
Subject Name in CSR CN="Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com" and challenge CN=Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com do not match  

  Exception: System.ArgumentException: Subject Name in CSR and challenge do not match

   at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

Exception:    at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

   at Microsoft.ConfigurationManager.CertRegPoint.Controllers.CertificateController.VerifyRequest(VerifyChallengeParams value
```

## <a name="assign-the-certificate-profile"></a>Sertifika profilini atama

SCEP sertifika profillerini, diğer amaçlar için [Cihaz profillerini dağıttığınız](../configuration/device-profile-assign.md) şekilde atayın.

Bir SCEP sertifika profili kullanmak için, bir cihazın güvenilen kök CA sertifikanız ile onu sağlayan güvenilen sertifika profilini de almış olması gerekir. Hem güvenilen kök sertifika profilini hem de SCEP sertifika profilini aynı gruplara dağıtmanızı öneririz.

Devam etmeden önce aşağıdakileri göz önünde bulundurun:

- Gruplara SCEP sertifika profilleri atadığınızda, güvenilen kök CA sertifika dosyası ( *Güvenilen sertifika profilinde*belirtildiği gibi) cihaza yüklenir. Cihaz, bu güvenilen kök CA sertifikasına yönelik bir sertifika isteği oluşturmak için SCEP sertifika profilini kullanır.

- SCEP sertifika profili yalnızca, sertifika profilini oluştururken belirttiğiniz platformu çalıştıran cihazlara yüklenir.

- Sertifika profillerini kullanıcı koleksiyonlarına veya cihaz koleksiyonlarına atayabilirsiniz.

- Cihaz kaydolduktan sonra cihaza hızlıca bir sertifika yayımlamak için sertifika profilini bir cihaz grubu yerine bir kullanıcı grubuna atayın. Bir cihaz grubuna atarsanız, ilkeleri almadan önce cihazın tam olarak kaydedilmesi gerekir.

- Intune ve Configuration Manager için ortak yönetim kullanıyorsanız, Configuration Manager ' de kaynak erişim Ilkeleri için [iş yükü kaydırıcısını](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) **Intune** veya **pilot Intune**'a ayarlayın. Bu ayar, Windows 10 istemcilerinin sertifika isteme işlemini başlatmasını sağlar.

> [!NOTE]
> - İOS/ıpados cihazlarında, bir SCEP sertifika profili veya PKCS sertifika profili, Wi-Fi veya VPN profili gibi ek bir profille ilişkilendirildiğinde, cihaz bu ek profillerin her biri için bir sertifika alır. Bu, iOS/ıpados cihazının SCEP veya PKCS sertifika isteği tarafından sunulan birden çok sertifikaya sahip olmasına neden olur. 
> 
>   SCEP tarafından sunulan sertifikalar benzersizdir. PKCS tarafından sunulan sertifikalar aynı sertifikadır, ancak her profil örneği yönetim profilinde ayrı bir satırla temsil edildiğinde farklı şekilde görünür.
> - İOS 13 ve macOS 10,15 ' de, Apple tarafından ele alınması gereken bazı [ek güvenlik gereksinimleri](https://support.apple.com/HT210176) vardır.  


## <a name="next-steps"></a>Sonraki adımlar

[Profil atama](../configuration/device-profile-assign.md)

[SCEP Sertifika profillerinin dağıtımı sorunlarını giderme](../protect/troubleshoot-scep-certificate-profiles.md)
