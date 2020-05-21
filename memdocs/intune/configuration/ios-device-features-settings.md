---
title: iOS/ıpados cihaz özelliği ayarları Microsoft Intune-Azure | Microsoft Docs
description: İOS ve ıpados cihazlarını AirPrint, giriş ekranı düzeni, uygulama bildirimleri, paylaşılan cihazlar, çoklu oturum açma ve Microsoft Intune Web içeriği filtresi ayarları için yapılandırma için tüm ayarları görüntüleyin. Bu ayarları, kuruluşunuzda bu Apple özelliklerini kullanmak üzere iOS/ıpados cihazlarını yapılandırmak için bir cihaz yapılandırma profilinde kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 235a79f644bf15b82eb9e8750f04519238760aca
ms.sourcegitcommit: 5d32dd481e2a944465755ce74e14c835cce2cd1c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/18/2020
ms.locfileid: "83551936"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>Intune 'da ortak iOS/ıpados özelliklerini kullanmak için iOS ve ıpados cihaz ayarları

Intune, iOS/ıpados kullanıcılarının cihazlarında farklı Apple özellikleri kullanmasına izin veren bazı yerleşik ayarlar içerir. Örneğin, AirPrint yazıcılarını denetleyebilir, yerleştirme ve giriş ekranı sayfalarına uygulamalar ve klasörler ekleyebilir, uygulama bildirimlerini gösterebilir, kilit ekranında varlık etiketi ayrıntılarını gösterebilir, çoklu oturum açma kimlik doğrulaması kullanabilir ve sertifika kimlik doğrulaması kullanabilirsiniz.

Bu özellikleri, mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak iOS/ıpados cihazlarını denetlemek için kullanın.

Bu makale, bu ayarları listeler ve her ayarın ne yaptığını açıklar. Bu özellikler hakkında daha fazla bilgi için [iOS/ıpados veya macOS cihaz özelliği ayarları ekle](device-features-configure.md)' ye gidin.

## <a name="before-you-begin"></a>Başlamadan önce

[İOS/ıpados cihaz özellikleri profili oluşturun](device-features-configure.md).

> [!NOTE]
> Bu ayarlar, bazı ayarların tüm kayıt seçeneklerine uygulanmasıyla farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [iOS/ıpados kaydı](../enrollment/ios-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

> [!NOTE]
> Tüm yazıcıları aynı profile eklediğinizden emin olun. Apple, birden çok AirPrint profilinin aynı cihazı hedeflemesini önler.

- **IP adresi**: yazıcının IPv4 veya IPv6 adresini girin. Yazıcıları tanımlamak için ana bilgisayar adları kullanırsanız, terminaldeki yazıcıya ping ekleyerek IP adresini alabilirsiniz. IP adresini ve yolu al (Bu makalede) daha fazla ayrıntı sağlar.
- **Yol**: yol, genellikle `ipp/print` ağınızdaki yazıcılar içindir. IP adresini ve yolu al (Bu makalede) daha fazla ayrıntı sağlar.
- **Bağlantı noktası**: AirPrint hedefinin dinleme bağlantı noktasını girin. Bu özelliği boş bırakırsanız AirPrint varsayılan bağlantı noktasını kullanır. İOS 11.0 + ve ıpados 13.0 + ' da kullanılabilir.
- **TLS**: **Enable** , Aktarım Katmanı Güvenliği (TLS) ile AirPrint bağlantılarının güvenliğini sağlar. İOS 11.0 + ve ıpados 13.0 + ' da kullanılabilir.

AirPrint sunucuları eklemek için şunları yapabilirsiniz:

- **Ekle** , AirPrint sunucusunu listeye ekler. Birçok AirPrint sunucusu eklenebilir.
- Bu bilgilerle, virgülle ayrılmış bir dosyayı (. csv) **Içeri aktarın** . Ya da, eklediğiniz AirPrint sunucularının bir listesini oluşturmak için **dışa aktarın** .

### <a name="get-server-ip-address-resource-path-and-port"></a>Sunucu IP adresi, kaynak yolu ve bağlantı noktası al

AirPrinter sunucuları eklemek için, yazıcının IP adresi, kaynak yolu ve bağlantı noktası gerekir. Aşağıdaki adımlarda bu bilgilerin nasıl alınacağı gösterilmektedir.

1. AirPrint yazıcıları ile aynı yerel ağa (alt ağ) bağlı bir Mac üzerinde, açık **Terminal** ( **/Applications/Utilities**).
2. Terminalde yazın `ippfind` ve ENTER ' u seçin.

    Yazıcı bilgilerini aklınızda edin. Örneğin, şuna benzer bir şey döndürebilir `ipp://myprinter.local.:631/ipp/port1` . İlk bölüm, yazıcının adıdır. Son Bölüm ( `ipp/port1` ) kaynak yoludur.

3. Terminalde yazın `ping myprinter.local` ve ENTER ' u seçin.

   IP adresini aklınızda edin. Örneğin, şuna benzer bir şey döndürebilir `PING myprinter.local (10.50.25.21)` .

4. IP adresi ve kaynak yolu değerlerini kullanın. Bu örnekte, IP adresi `10.50.25.21` ve kaynak yolu olur `/ipp/port1` .

## <a name="home-screen-layout"></a>Giriş ekranı düzeni

Bu özellik şu platformlarda geçerlidir:

- iOS 9,3 veya üzeri
- ıpados 13,0 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

### <a name="dock"></a>Dock

Ekrandaki Dock 'a en fazla altı öğe veya klasör eklemek için **yerleştirme** ayarlarını kullanın. Birçok cihaz daha az öğeyi destekler. Örneğin, iPhone cihazları en fazla dört öğeyi destekler. Bu durumda, cihazlarda yalnızca eklediğiniz ilk dört öğe gösterilir.

Cihaz yuvası için en fazla **altı** öğe (birleştirilmiş uygulamalar ve klasörler) ekleyebilirsiniz.

- **Ekle**: cihazlarda yuvaya uygulama veya klasör ekler.
- **Tür**: bir **uygulama** veya **klasör**ekleyin:

  - **Uygulama**: ekrandaki yerleştirmeyi uygulama eklemek için bu seçeneği belirleyin. Şunları girin:

    - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
    - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

  - **Klasör**: ekrandaki yerleştirmeyi bir klasör eklemek için bu seçeneği belirleyin.

    Bir klasördeki bir sayfaya eklediğiniz uygulamalar, soldan sağa ve listeyle aynı sırada düzenlenir. Bir sayfaya sığmayacak kadar fazla uygulama eklerseniz, uygulamalar başka bir sayfaya taşınır.

    - **Klasör adı**: klasörün adını girin. Bu ad, cihazlarda kullanıcılara gösterilir.
    - **Sayfaların listesi**: sayfa **ekleyin** ve aşağıdaki özellikleri girin:

      - **Sayfa adı**: sayfa için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
      - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
      - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

      Cihaz yuvası için en fazla **20** sayfa ekleyebilirsiniz.

> [!NOTE]
> Sayfa eklemek için giriş ekranı düzen ayarlarını kullandığınızda veya yerleştir 'e sayfalar ve uygulamalar eklemek için, giriş ekranındaki ve sayfalardaki simgeler kilitlenir. Bunlar taşınamaz veya silinemez. Bu davranış, iOS/ıpados ve Apple 'ın MDM ilkeleriyle tasarım sağlayabilir.

#### <a name="example"></a>Örnek

Aşağıdaki örnekte, Dock ekranı Safari, mail ve hisse senetleri uygulamalarını gösterir. Posta uygulaması özelliklerini göstermek için seçilmiştir:

> [!div class="mx-imgBorder"]
> ![Intune 'da örnek iOS/ıpados giriş ekranı düzen yerleştirme ayarları](./media/ios-device-features-settings/dock-screen-mail-app.png)

İlkeyi bir iPhone 'a atadığınızda, yuva aşağıdaki resme benzer şekilde görünür:

> [!div class="mx-imgBorder"]
> ![İPhone 'daki örnek iOS/ıpados yerleştirme düzeni](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Sayfalar

Giriş ekranında görünmesini istediğiniz sayfaları ve her sayfada görünmesini istediğiniz uygulamaları ekleyin. Bir sayfaya eklediğiniz uygulamalar, listeyle aynı sırada, soldan sağa düzenlenir. Bir sayfaya sığmayacak kadar fazla uygulama eklerseniz, uygulamalar başka bir sayfaya taşınır.

> [!TIP]
> Herhangi bir giriş ekranında ve sayfa listelerindeki öğeleri yeniden sıralamak için, onları sürükleyip bırakabilirsiniz.

Bir cihaza en fazla **40** sayfa ekleyebilirsiniz.

- **Sayfaların listesi**: sayfa **ekleyin** ve aşağıdaki özellikleri girin:

  - **Sayfa adı**: sayfa için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için *kullanılır ve iOS* /ıpados cihazında gösterilmez.

  Bir cihaza en fazla **60** öğe (birleştirilmiş uygulamalar ve klasör) ekleyebilirsiniz.

  - **Ekle**: cihazlarda bir sayfaya uygulamalar veya klasörler ekler.

    - **Tür**: bir **uygulama** veya **klasör**ekleyin:

      - **Uygulama**: ekrandaki bir sayfaya uygulama eklemek için bu seçeneği belirleyin. Şunları da girin:

        - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
        - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

      - **Klasör**: ekrandaki yerleştirmeyi bir klasör eklemek için bu seçeneği belirleyin.

        Bir klasördeki bir sayfaya eklediğiniz uygulamalar, soldan sağa ve listeyle aynı sırada düzenlenir. Bir sayfaya sığmayacak kadar fazla uygulama eklerseniz, uygulamalar başka bir sayfaya taşınır.

        - **Klasör adı**: klasör için bir ad girin. Bu ad, cihazlarda kullanıcılara gösterilir.
        - **Ekle**: klasöre sayfa ekler. Aşağıdaki özellikleri de girin:

          - **Sayfa adı**: sayfa için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
          - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
          - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

#### <a name="example"></a>Örnek

Aşağıdaki örnekte, **contoso** adlı yeni bir sayfa eklenmiştir. Sayfa, arkadaşları ve ayarları bul uygulamalarını gösterir:

> [!div class="mx-imgBorder"]
> ![iOS/ıpados giriş ekranı düzeni yeni sayfa ayarları ve Intune 'da örnek](./media/ios-device-features-settings/page-find-friends-settings-apps.png)

Ayarlar uygulaması özelliklerini göstermek için seçilmiştir:

> [!div class="mx-imgBorder"]
> ![iOS/ıpados giriş ekranı Düzen ayarları Intune 'da uygulama özellikleri örneği](./media/ios-device-features-settings/page-settings-app-properties.png)

İlkeyi bir iPhone 'a atadığınızda, sayfa aşağıdaki resme benzer şekilde görünür:

> [!div class="mx-imgBorder"]
> ![Intune 'da değiştirilmiş giriş ekranına sahip iOS/ıpados cihazı](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>Uygulama bildirimleri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Ekle**: uygulamalar için bildirim ekleme:

  > [!div class="mx-imgBorder"]
  > ![Intune 'da iOS/ıpados profilinde uygulama bildirimi ekleme](./media/ios-device-features-settings/ios-ipados-app-notifications.png)

  - **Uygulama PAKETI kimliği**: eklemek Istediğiniz uygulamanın **uygulama paket kimliğini** girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .
  - **Uygulama adı**: eklemek istediğiniz uygulamanın adını girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. Cihazlarda *gösterilmez.*
  - **Yayımcı**: eklemekte olduğunuz uygulamanın yayımcısını girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. Cihazlarda *gösterilmez.*
  - **Bildirimler**: uygulamanın cihazlara bildirim göndermesini **etkinleştirin** veya **devre dışı bırakın** .
    - **Bildirim merkezinde göster**: **Etkinleştir** , uygulamanın cihaz bildirim merkezinde bildirimleri göstermesini sağlar. **Devre dışı bırak ayarı** , uygulamanın bildirim merkezinde bildirimleri göstermesini önler.
    - **Kilit ekranında göster**: **Etkinleştir** ayarı, cihaz kilidi ekranında uygulama bildirimlerini gösterir. **Devre dışı bırak ayarı** , uygulamanın kilit ekranında bildirimleri göstermesini önler.
    - **Uyarı türü**: cihazların kilidi açıldığında, bildirimin nasıl gösterileceğini seçin. Seçenekleriniz şunlardır:
      - **Hiçbiri**: hiçbir bildirim gösterilmez.
      - **Başlık**: bir başlık, bildirimle kısaca gösterilir.
      - **Kalıcı**: bildirim gösterilir ve kullanıcıların cihazı kullanmaya devam etmeden önce el ile kapatması gerekir.
    - **Uygulama simgesinde rozet**: uygulama simgesine rozet eklemek için **Etkinleştir** ' i seçin. Rozet, uygulamanın bir bildirim gönderdiği anlamına gelir.
    - **Sesler**: bir bildirim teslim edildiğinde ses çalmak için **Etkinleştir** ' i seçin.

## <a name="lock-screen-message"></a>Kilit ekranı iletisi

Bu özellik şu platformlarda geçerlidir:

- iOS 9.3 ve üzeri
- ıpados 13,0 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Varlık etiketi bilgileri**: cihazın varlık etiketiyle ilgili bilgileri girin. Örneğin `Owned by Contoso Corp` veya `Serial Number: {{serialnumber}}` girin.

  Girdiğiniz metin, oturum açma penceresinde ve cihazlarda kilit ekranında gösterilir.

- **Kilit ekranı dipnotu**: cihazlar kaybolur veya çalınırsa, cihazın döndürülmesini sağlamaya yardımcı olabilecek bir durum girin. İstediğiniz herhangi bir metin girebilirsiniz. Örneğin `If found, call Contoso at ...` gibi bir URI girebilirsiniz.

  Cihaz belirteçleri, bu alanlara cihaza özgü bilgiler eklemek için de kullanılabilir. Örneğin, seri numarasını göstermek için girin `Serial Number: {{serialnumber}}` . Kilit ekranında metin şuna benzer şekilde görünür `Serial Number 123456789ABC` . Değişken girerken, küme ayraçları kullandığınızdan emin olun `{{ }}` . [Uygulama yapılandırma belirteçleri](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) , kullanılabilecek değişkenlerin bir listesini içerir. Ayrıca, `deviceName` herhangi bir cihaza özgü değeri de kullanabilirsiniz.

  > [!NOTE]
  > Değişkenler kullanıcı arabiriminde doğrulanmaz ve büyük/küçük harfe duyarlıdır. Sonuç olarak, yanlış girişle kaydedilmiş profiller görebilirsiniz. Örneğin, `{{DeviceID}}` `{{deviceid}}` ya da ' {{DeviceID}} ' yerine girerseniz, CIHAZıN benzersiz kimliği yerine değişmez dize gösterilir. Doğru bilgileri girdiğinizden emin olun. Tüm küçük harfler veya tüm büyük harfler desteklenir, ancak bir karışımı değildir. 

## <a name="single-sign-on"></a>Çoklu oturum açma

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Bölge**: URL 'nin etki alanı parçasını girin. Örneğin, `contoso.com` girin.
- **Kerberos asıl adı**: Intune, Azure AD 'de her bir kullanıcı için bu özniteliğe bakar. Ardından Intune, cihazlara yüklenen XML oluşturmadan önce ilgili alanı (UPN gibi) doldurur. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, profil cihazlara dağıtıldığında kullanıcılardan bir Kerberos asıl adı ister. MDMs 'nin SSO profillerini yüklemesi için bir asıl ad gereklidir.
  - **Kullanıcı asıl adı**: Kullanıcı asıl adı (UPN) aşağıdaki şekilde ayrıştırılır:

    > [!div class="mx-imgBorder"]
    > ![Intune 'da iOS/ıpados Kullanıcı adı SSO özniteliği](./media/ios-device-features-settings/User-name-attribute.png)

    Ayrıca, **Bölge** metin kutusuna girdiğiniz metinle bölge değerinin üzerine yazabilirsiniz.

    Örneğin contoso, Avrupa, Asya ve Kuzey Amerika dahil olmak üzere birkaç bölgeye sahiptir. Contoso, Asya kullanıcılarının SSO kullanmasını istiyor ve uygulama, UPN 'nin biçiminde olmasını istiyor `username@asia.contoso.com` . **Kullanıcı asıl adı**' nı seçtiğinizde, her bir kullanıcının BÖLGESI Azure AD 'den alınır `contoso.com` . Böylece, Asya 'daki kullanıcılar için **Kullanıcı asıl adı**' nı seçin ve girin `asia.contoso.com` . `username@asia.contoso.com`Bunun yerine kullanıcının UPN 'si olur `username@contoso.com` .

  - **Intune CIHAZ kimliği**: Intune, ıNTUNE cihaz kimliğini otomatik olarak seçer.

    Varsayılan olarak, uygulamaların yalnızca cihaz kimliğini kullanması gerekir. Ancak uygulamanız bölge ve cihaz kimliği kullanıyorsa **Bölge** metin kutusuna bölgeyi yazabilirsiniz.

    > [!NOTE]
    > Varsayılan olarak, cihaz kimliğini kullanıyorsanız bölgeyi boş bırakın.

  - **Azure AD cihaz KIMLIĞI**
  - **SAM hesap adı**: Intune, şirket Içi güvenlik hesapları YÖNETICISI (Sam) hesap adını doldurur.


- **Uygulamalar**: Kullanıcıların cihazlarına çoklu oturum açma kullanan uygulamalar **ekleyin** .

  `AppIdentifierMatches`Dizi, uygulama paketi kimlikleriyle eşleşen dizeler içermelidir. Bu dizeler gibi tam eşleşmeler olabilir `com.contoso.myapp` veya joker karakterini kullanarak paket kimliğinde bir ön ek eşleşmesi girebilirsiniz \* . Joker karakter, bir nokta karakterinden (.) sonra görünmelidir ve dizenin sonunda, gibi yalnızca bir kez görünebilir `com.contoso.*` . Joker karakter eklendiğinde, paket kimlikleri bu ön ekle başlayan tüm uygulamaların hesaba erişimine izin verilir.

  **Uygulama Adı**’nı kullanarak paket kimliğini ayırt etmenize yardımcı olacak bir kolay ad ekleyin.

- **URL ön ekleri**: kuruluşunuzda Kullanıcı çoklu oturum açma kimlik doğrulaması gerektiren tüm URL 'leri **ekleyin** .

  Örneğin, bir Kullanıcı bu sitelerden birine bağlanırsa, iOS/ıpados cihazı çoklu oturum açma kimlik bilgilerini kullanır. Kullanıcıların ek kimlik bilgileri girmesi gerekmez. Multi-Factor Authentication etkinleştirilirse, kullanıcıların ikinci kimlik doğrulamasını girmesi gerekir.

  > [!NOTE]
  > Bu URL'ler düzgün biçimlendirilmiş FQDN'ler olmalıdır. Apple bunların biçiminde olmasını gerektirir `http://<yourURL.domain>` .

  URL eşleştirme desenleri `http://` veya `https://` ile başlamalıdır. Basit bir dize eşleşmesi çalıştırılır, bu nedenle `http://www.contoso.com/` URL öneki eşleşmez `http://www.contoso.com:80/` . İOS 10.0 + ve ıpados 13.0 + ile \* eşleşen tüm değerleri girmek için tek bir joker karakter kullanılabilir. Örneğin, `http://*.contoso.com/` ve ile eşleşir `http://store.contoso.com/` `http://www.contoso.com` .

  `http://.com`Ve `https://.com` desenleri SıRASıYLA tüm http ve https URL 'leri ile eşleşir.

- **Yenileme sertifikası**: kimlik doğrulaması için Sertifikalar (parolalar değil) kullanılıyorsa, mevcut SCEP veya PFX sertifikasını kimlik doğrulama sertifikası olarak seçin. Genellikle, bu sertifika VPN, Wi-Fi veya e-posta gibi diğer profiller için kullanıcılara dağıtılan aynı sertifikadır.

## <a name="web-content-filter"></a>Web içeriği filtresi

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Filtre türü**: belirli Web sitelerine izin vermeyi seçin. Seçenekleriniz şunlardır:

  - **URL 'Leri yapılandırma**: doğrudan küfür ve açık cinsel dil dahil olmak üzere yetişkin koşullarını gösteren yerleşik Web filtresini kullanın. Bu özellik her bir Web sayfasını yüklendiği şekilde değerlendirir ve uygun olmayan içeriği tanımlar ve engeller. Filtre tarafından denetlenmesini istemediğiniz URL 'Ler de ekleyebilirsiniz. Ya da Apple 'ın filtre ayarlarından bağımsız olarak belirli URL 'Leri engelleyin.

    - İzin **verilen URL 'ler**: izin vermek Istediğiniz URL 'leri **ekleyin** . Bu URL 'Ler Apple 'ın Web filtresini atlar.

        > [!NOTE]
        > Girdiğiniz URL 'ler, Apple Web filtresi tarafından evauluated istemediğiniz URL 'lerdir. Bu URL 'Ler, izin verilen Web sitelerinin bir listesi değildir. İzin verilen Web sitelerinin bir listesini oluşturmak için **filtre türünü** **yalnızca belirli Web siteleri**olarak ayarlayın.

    - **Engellenen URL 'ler** **: Apple** Web Filter ayarlarından bağımsız olarak, durdurmak istediğiniz URL 'leri açmayı açın.

  - **Yalnızca belirli Web siteleri** (yalnızca Safari Web tarayıcısı için): Bu URL 'ler Safari tarayıcısının yer işaretlerine eklenir. Kullanıcılara **yalnızca** bu siteleri ziyaret etme izni verilir; başka hiçbir site açılamaz. Bu seçeneği yalnızca kullanıcıların erişebileceği URL'lerin tam listesini biliyorsanız kullanın.

    - **URL**: izin vermek istediğiniz Web sitesinin URL 'sini girin. Örneğin, `https://www.contoso.com` girin.
    - **Yer Işareti yolu**: Apple bu ayarı değiştirdi. Tüm yer işaretleri **onaylanan siteler** klasörüne gider. Yer işaretleri girdiğiniz yer işareti yoluna gitmez.
    - **Başlık**: yer işareti için açıklayıcı bir başlık girin.

    Herhangi bir URL girmezseniz, kullanıcılar, ve dışında herhangi bir Web sitesine erişemez `microsoft.com` `microsoft.net` `apple.com` . Bu URL 'Lere Intune tarafından otomatik olarak izin verilir.

## <a name="single-sign-on-app-extension"></a>Çoklu oturum açma uygulama uzantısı

Bu özellik şu platformlarda geçerlidir:

- iOS 13,0 ve üzeri
- ıpados 13,0 ve üzeri

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **SSO uygulama uzantısı türü**: SSO uygulama uzantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uygulama uzantılarını kullanmaz. Bir uygulama uzantısını devre dışı bırakmak için, SSO uygulama uzantısı türü ' ni **Yapılandırılmadı**' ya geçirebilirsiniz.
  - **Microsoft Azure AD**: bir yeniden YÖNLENDIRME türü SSO uygulama uzantısı olan MICROSOFT Enterprise SSO eklentisini kullanır. Bu eklenti, [Apple 'ın Kurumsal Çoklu oturum açma](https://developer.apple.com/documentation/authenticationservices) özelliğini destekleyen tüm uygulamalarda Active Directory hesapları için SSO sağlar. Azure AD kullanarak kimlik doğrulaması yapan Microsoft uygulamalarında, kuruluş uygulamalarında ve web sitelerinde SSO 'yu etkinleştirmek için bu SSO uygulama uzantısı türünü kullanın.

    SSO eklentisi, güvenlik ve Kullanıcı deneyimi iyileştirmeleri sunan gelişmiş bir kimlik doğrulama Aracısı işlevi görür. Daha önce Microsoft Authenticator uygulamayla aracılı kimlik doğrulamasını kullanan tüm uygulamalar, [Apple cihazları Için Microsoft ENTERPRISE SSO EKLENTISIYLE](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin)SSO almaya devam eder.

    > [!IMPORTANT]
    > Microsoft Azure AD SSO uygulama uzantısı türüyle SSO sağlamak için önce cihazlara iOS/ıpados Microsoft Authenticator uygulamasını yüklemeniz gerekir. Authenticator uygulaması Microsoft Enterprise SSO eklentisini cihazlara sunar ve MDM SSO uygulama uzantısı ayarları eklentiyi etkinleştirir. Bir Authenticator ve SSO uygulama uzantısı profili cihazlara yüklendikten sonra, kullanıcıların oturum açması için kimlik bilgilerini girmesi ve cihazlarında oturum kurması gerekir. Bu oturum daha sonra kullanıcıların kimlik doğrulamasını yapmasına gerek kalmadan farklı uygulamalar arasında kullanılır. Doğrulayıcı hakkında daha fazla bilgi için bkz. [Microsoft Authenticator uygulaması nedir?](https://docs.microsoft.com/azure/active-directory/user-help/user-help-auth-app-overview).

  - **Yeniden yönlendir**: SSO 'yu modern kimlik doğrulama akışlarıyla kullanmak için genel, özelleştirilebilir bir yeniden yönlendirme uygulama uzantısı kullanın. Kuruluşunuzun uygulama uzantısının uzantı KIMLIĞINI öğrendiğinizden emin olun.
  - **Kimlik bilgisi**: sınama ve yanıt kimlik doğrulama akışlarıyla SSO 'yu kullanmak için genel, özelleştirilebilir bir kimlik bilgisi uygulama uzantısı kullanın. Kuruluşunuzun uygulama uzantısının uzantı KIMLIĞINI öğrendiğinizden emin olun.
  - **Kerberos**: iOS 13.0 + ve ıpados 13.0 + ' da bulunan Apple 'ın yerleşik Kerberos uzantısını kullanın. Bu seçenek, **kimlik bilgisi** uygulama uzantısının Kerberos 'a özgü bir sürümüdür.

  > [!TIP]
  > **Yeniden yönlendirme** ve **kimlik bilgisi** türleriyle, uzantıdan geçirilecek kendi yapılandırma değerlerinizi eklersiniz. **Kimlik bilgisi**kullanıyorsanız, Apple tarafından **Kerberos** türünde sunulan yerleşik yapılandırma ayarlarını kullanmayı göz önünde bulundurun.

- **Paylaşılan cihaz modu** (yalnızca Microsoft Azure AD): Azure AD 'nin paylaşılan cihaz modu özelliği Için yapılandırılmış IOS/ıpados cihazlarına MICROSOFT Enterprise SSO eklentisini dağıtıyorsanız **Etkinleştir** ' i seçin. Paylaşılan moddaki cihazlar birçok kullanıcının paylaşılan cihaz modunu destekleyen uygulamaların genel olarak oturum açmasını ve çıkmasına izin verir. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, iOS/ıpados cihazları birden çok kullanıcı arasında paylaşılmak üzere tasarlanmamıştır.

  Paylaşılan cihaz modu ve bu aygıtın nasıl etkinleştirileceği hakkında daha fazla bilgi için bkz. iOS cihazları için [paylaşılan cihaz moduna](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices) ve [paylaşılan cihaz moduna](https://docs.microsoft.com/azure/active-directory/develop/msal-ios-shared-devices)genel bakış.  

- **UZANTı kimliği** (yeniden yönlendirme ve kimlik bilgisi): SSO uygulama uzantınızı tanımlayan paket tanımlayıcısını (gibi) girin `com.apple.extensiblesso` .

- **Takım Kimliği** (yeniden yönlendirme ve kimlik bilgisi): SSO uygulama uzantınızın ekip tanımlayıcısını girin. Takım tanımlayıcısı, Apple tarafından oluşturulan ve gibi 10 karakterlik alfasayısal bir dizedir (sayılar ve harfler) `ABCDE12345` . Takım KIMLIĞI gerekli değildir.

  [Takım kimliğinizi bulun](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

- **Bölge** (kimlik bilgileri ve Kerberos): kimlik doğrulama Realm adını girin. Bölge adı, gibi büyük harfli olmalıdır `CONTOSO.COM` . Genellikle, bölge adınız DNS etki alanı adınızla aynıdır, ancak tümü büyük harfle aynıdır.

- **Etki alanları** (kimlik bilgileri ve Kerberos): SSO aracılığıyla kimlik doğrulayabilecek sitelerin etki alanı veya ana bilgisayar adlarını girin. Örneğin, Web siteniz ise, `mysite.contoso.com` `mysite` ana bilgisayar adı ve `contoso.com` etki alanı adıdır. Kullanıcılar bu sitelerden birine bağlandıklarında, uygulama uzantısı kimlik doğrulama sınamasını işler. Bu kimlik doğrulaması, kullanıcıların oturum açmak için yüz KIMLIĞI, Touch ID veya Apple pincode/geçiş kodu kullanmasına izin verir.

  - Çoklu oturum açma uygulama uzantılarınızın Intune profillerindeki tüm etki alanları benzersiz olmalıdır. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, bir etki alanını hiçbir oturum açma uygulama uzantısı profilinde tekrarlayamıyorum.
  - Bu etki alanları büyük/küçük harfe duyarlı değildir.

- **URL 'ler** (yalnızca yeniden yönlendir): kimlik SAĞLAYıCıLARıNıZıN URL öneklerini girin adına yeniden yönlendirme uygulama uzantısı SSO kullanır. Kullanıcılar bu URL 'lere yeniden yönlendirildiğinde, SSO uygulama uzantısı SSO 'yu müdahale eder ve sorar.

  - Intune çoklu oturum açma uygulama uzantısı profillerindeki tüm URL 'Lerin benzersiz olması gerekir. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, hiçbir SSO uygulama uzantısı profilinde bir etki alanını tekrarlayabilirsiniz.
  - URL 'Ler veya ile başlamalıdır `http://` `https://` .

- **Ek yapılandırma** (Microsoft Azure AD, yeniden yönlendirme ve kimlik bilgisi): SSO uygulama uzantısına geçirilecek uzantıya özgü ek veriler girin:
  - **Anahtar**: eklemek istediğiniz öğenin adını girin, örneğin `user name` .
  - **Tür**: veri türünü girin. Seçenekleriniz şunlardır:

    - Dize
    - Boole: **yapılandırma değerinde**, veya girin `True` `False` .
    - Tamsayı: **yapılandırma değeri**alanına bir sayı girin.

  - **Değer**: verileri girin.

  - **Ekle**: yapılandırma anahtarlarınızı eklemek için seçin.

- **Anahtarlık kullanımı** (yalnızca Kerberos): **blok** , parolaların anahtarlıkta kaydedilmesini ve depolanmasını engeller. Engellenirse, kullanıcılardan parolasını kaydetmesi istenmez ve Kerberos anahtarının süresi dolarsa parolayı yeniden girmesi gerekir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parolaların anahtarlıkta kaydedilmesine ve depolanmasına izin verebilir. Anahtarın süresi dolarsa kullanıcılardan parolasını yeniden girmesi istenmez.
- **Yüz kimliği, Touch ID veya geçiş kodu** (yalnızca Kerberos): Kerberos biletini yenilemek için kimlik bilgisi gerektiğinde KULLANıCıLARıN yüz kimliğini, Touch ID 'sini veya cihaz geçiş kodunu girmesini **zorunlu** kılar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, Kerberos biletini yenilemek için kullanıcıların biyometri veya cihaz geçiş kodu kullanmasını gerektirmeyebilir. **Anahtarlık kullanımı** engellenirse, bu ayar uygulanmaz.
- **Varsayılan bölge** (yalnızca Kerberos): **Etkinleştir** varsayılan bölge olarak girdiğiniz **bölge** değerini ayarlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi varsayılan bir bölge ayarlayamayabilir.

  > [!TIP]
  > - Kuruluşunuzda birden çok Kerberos SSO uygulama uzantısını yapılandırıyorsanız, bu ayarı **etkinleştirin** .
  > - Birden çok bölge kullanıyorsanız bu ayarı **etkinleştirin** . Girdiğiniz **bölge** değerini varsayılan bölge olarak ayarlar.
  > - Yalnızca bir bölge varsa, **Yapılandırılmadı** (varsayılan) olarak bırakın.

- **Asıl ad** (yalnızca Kerberos): Kerberos sorumlusunun Kullanıcı adını girin. Bölge adını eklemeniz gerekmez. Örneğin, içinde `user@contoso.com` `user` asıl addır ve `contoso.com` bölge adıdır.

  > [!TIP]
  > - Ayrıca, küme ayraçları girerek asıl ad içindeki değişkenleri de kullanabilirsiniz `{{ }}` . Örneğin, Kullanıcı adını göstermek için girin `Username: {{username}}` . 
  > - Ancak, değişkenler kullanıcı arabiriminde doğrulanmamış ve büyük/küçük harfe duyarlı olduğundan değişken değiştirme konusunda dikkatli olun. Doğru bilgileri girdiğinizden emin olun.

- **Active Directory site kodu** (yalnızca Kerberos): Kerberos uzantısının kullanması gereken Active Directory sitenin adını girin. Kerberos uzantısı Active Directory site kodunu otomatik olarak bulagerekebilmeniz için bu değeri değiştirmeniz gerekebilir.
- **Önbellek adı** (yalnızca Kerberos): Kerberos önbelleğinin genel güvenlik HIZMETLERI (GSS) adını girin. Büyük olasılıkla bu değeri ayarlamanız gerekmez.
- **Uygulama paketi kimlikleri** (yalnızca Kerberos): cihazlarınızda çoklu oturum açma kullanması gereken uygulama paketi tanımlayıcılarını **ekleyin** . Bu uygulamalara, Kerberos Anahtar verme bileti, kimlik doğrulama bileti ve kullanıcılara erişim yetkisi oldukları hizmetler için kimlik doğrulaması erişimi verilir.
- **Etki alanı bölge eşlemesi** (yalnızca Kerberos): bölge ile eşleşmesi gereken etkı alanı DNS soneklerini **ekleyin** . Ana bilgisayarların DNS adları bölge adıyla eşleşmezse bu ayarı kullanın. Büyük olasılıkla bu özel etki alanı/bölge eşlemesini oluşturmanız gerekmez.
- **PKINIT sertifikası** (yalnızca Kerberos): Kerberos kimlik doğrulaması Için kullanılabilecek Ilk kimlik doğrulaması (PKI) sertifikası Için ortak anahtar şifrelemesini **seçin** . Intune 'A eklediğiniz [PKCS](../protect/certficates-pfx-configure.md) veya [SCEP](../protect/certificates-scep-configure.md) sertifikaları arasından seçim yapabilirsiniz. Sertifikalar hakkında daha fazla bilgi için bkz. [Microsoft Intune kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md).

## <a name="wallpaper"></a>Duvar Kağıdı

Var olan bir görüntüye sahip cihazlara sahip olmayan bir profil atandığında beklenmeyen davranışlarla karşılaşabilirsiniz. Örneğin, görüntü olmadan bir profil oluşturursunuz. Bu profil, zaten bir görüntüsü olan cihazlara atanır. Bu senaryoda, görüntü cihaz varsayılana değişebilir veya orijinal görüntü cihazda kalabilir. Bu davranış, Apple 'ın MDM platformu tarafından denetlenir ve sınırlandırılmıştır.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Duvar kağıdı görüntü konumu**: cihazlarda görüntüyü göstermek için bir konum seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Cihazlara özel bir görüntü eklenmez. Varsayılan olarak, işletim sistemi kendi görüntüsünü ayarlayabilir.
  - **Kilit ekranı**: görüntüyü kilit ekranına ekler.
  - **Ana ekran**: görüntüyü giriş ekranına ekler.
  - **Kilit ekranı ve giriş ekranı**: kilit ekranında ve ana ekranda aynı görüntüyü kullanır.
- **Duvar kağıdı resmi**: kullanmak istediğiniz var olan bir. png,. jpg veya. JPEG görüntüsünü karşıya yükleyin. Dosya boyutunun 750 KB 'tan az olduğundan emin olun. Ayrıca, eklediğiniz bir görüntüyü de **kaldırabilirsiniz** .

> [!TIP]
> Kilit ekranında ve ana ekranda farklı görüntüleri göstermek için, kilit ekranı görüntüsüyle bir profil oluşturun. Giriş ekranı görüntüsüyle başka bir profil oluşturun. Her iki profili de iOS/ıpados Kullanıcı veya cihaz gruplarına atayın.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[MacOS](macos-device-features-settings.md) cihazları için cihaz özelliği profilleri de oluşturabilirsiniz.
