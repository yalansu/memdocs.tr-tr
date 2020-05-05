---
title: Belgeleri kullanma
titleSuffix: Configuration Manager
description: Configuration Manager teknik belge kitaplığını kullanma hakkında ipuçları edinin.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d694f9985e6d1e5118f2620e5cbd556de249788a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771325"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Configuration Manager belgelerini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede Configuration Manager belge kitaplığı kullanımı için kaynaklar ve ipuçları sunulmaktadır.

- Arama
- Belge hataları, geliştirmeler, sorular ve yeni fikirler gönderme
- Değişiklikler hakkında bildirim alma
- Docs 'a katkıda bulunma

Ürünle ilgili genel yardım için bkz. [Yardım bulma](find-help.md).

## <a name="search"></a><a name="bkmk_searchtips"></a>Aramanız

İhtiyacınız olan bilgileri bulmanıza yardımcı olması için aşağıdaki arama ipuçlarını kullanın:

- Configuration Manager için içerik bulmak üzere tercih ettiğiniz arama altyapısını kullanırken, arama anahtar `ConfigMgr` kelimelerinizle birlikte dahil edin.

  - Configuration Manager geçerli dalı `docs.microsoft.com/configmgr` için sonuçları arayın. `docs.microsoft.com/previous-versions` Sonuçları eski ürün sürümleri içindir.

  - Arama sonuçlarını geçerli içerik kitaplığına daha fazla odaklanmak için, arama altyapısının kapsamına `site:docs.microsoft.com` ekleyin.

- Kullanıcı arabirimindeki ve çevrimiçi belgelerdeki terminoloji ile eşleşen arama terimlerini kullanın. Topluluk içeriğinde görebileceğiniz resmi olmayan terimlerin veya kısaltmaların önüne kaçının. Örneğin şunu arayın:

  - "MP" yerine "yönetim noktası"
  - "DT" yerine "dağıtım türü"
  - "SUM" yerine "yazılım güncelleştirmeleri"

- Geçerli makale içinde arama yapmak için tarayıcınızın **bul** özelliğini kullanın. Modern Web tarayıcıları sayesinde, **CTRL**+**F** tuşlarına basın ve arama terimlerinizi girin.

- Üzerindeki `docs.microsoft.com` her makale, içerik aramasına yardımcı olmak için aşağıdaki alanları içerir:

  - Sağ üst köşedeki **arama** yapın. Tüm makalelere aramak için bu alana terimler girin. Configuration Manager kitaplığındaki makaleler, `ConfigMgr` yalnızca bu belge kitaplığını aramak için kapsamı otomatik olarak içerir.

  - Sol içindekiler tablosunun üzerine **başlığa göre filtreleyin** . Geçerli içerik tablosunu aramak için bu alana terimler girin. Bu alan yalnızca geçerli düğümün makale başlıklarında görüntülenen terimlerle eşleşir. Örneğin, **çekirdek altyapı** (`docs.microsoft.com/configmgr/core`) veya **uygulama yönetimi** (`docs.microsoft.com/configmgr/apps`).

- Bir şeyi bulmada sorun mu yaşıyorsunuz? [Dosya geri bildirimi!](#bkmk_docfeedback) Sorunu dosyalayarak, kullanmakta olduğunuz arama altyapısını, denediğiniz anahtar sözcükleri ve hedef makaleyi sağlayın. Bu geribildirim, Microsoft 'un içeriği daha iyi arama için iyileştirilmesine yardımcı olur.

> [!TIP]
> Configuration Manager sürüm 1902 ' den başlayarak, Configuration Manager konsolunun yeni **topluluk** çalışma alanında bir **belge** düğümü vardır. Bu düğüm Configuration Manager belge ve destek makaleleri hakkında güncel bilgiler içerir. Daha fazla bilgi için, bkz. [Configuration Manager konsolunu kullanma](../servers/manage/admin-console.md#bkmk_doc-dashboard).

## <a name="feedback"></a><a name="bkmk_docfeedback"></a>Lerimi

Alttaki geri bildirim bölümüne gitmek için herhangi bir makalenin sağ üst kısmındaki **geri bildirim** bağlantısını seçin. Bu bölüm, GitHub sorunlarıyla tümleştirilir. GitHub sorunlarıyla tümleştirme hakkında daha fazla bilgi için bkz. [docs platform blog gönderisi](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Configuration Manager ürünün kendisi üzerinde geri bildirim paylaşmak için **ürün geri bildirimi**' ni seçin. Daha fazla bilgi için bkz. [ürün geri bildirimi](find-help.md#product-feedback).

[GitHub hesabı](https://github.com/join) , belge geri bildirimi sağlamak için bir önkoşuldur. Oturum açtıktan sonra, MicrosoftDocs organizasyonu için tek seferlik bir yetkilendirme vardır. **İçerik geri bildirimi**' ni seçtiğinizde bir başlık ve açıklama girin ve ardından **geri bildirim gönderin**. Bu eylem, [Sccmdocs deposundaki](https://github.com/MicrosoftDocs/SCCMdocs/issues)hedef makale için yeni bir sorun dosyaları.

Bu tümleştirme Ayrıca hedef makale için mevcut açık veya kapalı sorunları da görüntüler. Varsa, yeni bir sorun göndermeden önce bunları gözden geçirin. İlgili bir sorun bulursanız, bir yeniden eylem eklemek için yüz simgesini seçin veya bir yorum eklemek için genişletebilirsiniz.

#### <a name="types-of-feedback"></a>Geri bildirim türleri

Aşağıdaki geri bildirim türlerini göndermek için GitHub sorunlarını kullanın:

- Belge hatası: içerik güncel değil, belirsiz, kafa karıştırıcı veya bozuk.
- Belge geliştirme: makaleyi geliştirmeye yönelik bir öneride bulunun.
- Belge sorusu: mevcut belgeleri bulmaya yardım etmeniz gerekir.
- Belge fikri: yeni bir makale önerisi. Belge geri bildirimi için UserVoice yerine bu yöntemi kullanın.
- Kudos: faydalı veya bilgilendirici bir makale hakkında olumlu geri bildirim!
- Yerelleştirme: içerik çevirisi hakkında geri bildirim.
- Arama altyapısı iyileştirmesi (SEO): içerik arama sorunları hakkında geri bildirim. Yorumlara arama altyapısını, anahtar sözcükleri ve hedef makaleyi dahil edin.

Belge ile ilgili olmayan konularda bir sorun oluşturursanız Microsoft bu sorunları kapatır. Örneğin:

- [Ürün geri bildirimi](find-help.md#product-feedback)
- [Ürün soruları](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Destek istekleri](https://aka.ms/cmcbsupport)

Temel docs.microsoft.com platformunda geri bildirim paylaşmak için bkz. [docs geri bildirimi](https://aka.ms/sitefeedback). Platform, üst bilgi, içindekiler tablosu ve sağ menü gibi tüm sarmalayıcı bileşenlerini içerir. Ayrıca makalelerin, yazı tipi, uyarı kutuları ve sayfa bağlayıcıları gibi tarayıcıda nasıl işlenmesi.

## <a name="notifications"></a><a name="bkmk_notifications"></a>Bildirimi

Belge kitaplığındaki içerik değiştiğinde bildirim almak için aşağıdaki adımları kullanın:

1. Bir makale veya makale kümesi bulmak için [docs aramasını](https://docs.microsoft.com/search/index?scope=ConfigMgr) kullanın. Örneğin:

    - ["Sorun giderme Için günlük dosyaları-Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr) başlığına göre tek bir makaleyi arayın

    - [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr) hakkında herhangi bir makale arayın

2. Sağ üst köşede **RSS** bağlantısını seçin.

3. Herhangi bir arama sonuçlarından değişiklik yapıldığında bildirim almak için bu akışı herhangi bir RSS uygulamasında kullanın.

> [!TIP]
> Ayrıca, GitHub 'daki [Sccmdocs deposunu](https://github.com/MicrosoftDocs/SCCMdocs) **izleyebilirsiniz** . Bu yöntem birçok bildirim oluşturur. Ayrıca Microsoft tarafından kullanılan özel bir depodan değişiklik içermez.

## <a name="contribute"></a><a name="bkmk_contribute"></a>Bulun

Configuration Manager belge kitaplığı, docs.microsoft.com üzerindeki içerikler, GitHub üzerinde açık kaynaklıdır. Bu kitaplık, topluluk katkılarını kabul eder ve teşvik eder. Kullanmaya başlama hakkında daha fazla bilgi için bkz. katkıda bulunan [Kılavuzu](https://docs.microsoft.com/contribute). Tek önkoşul, [GitHub hesabı](https://github.com/join)oluşturmaktır.

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>SCCMdocs 'a katkıda bulunmak için temel adımlar

1. Hedef makaleden **Düzenle**' yi seçin. Bu eylem, kaynak dosyayı GitHub 'da açar.

2. Kaynak dosyayı düzenlemek için kalem simgesini seçin.

3. Markaşağı kaynağında değişiklik yapın. Daha fazla bilgi için bkz. [belgeleri yazmak Için Marku kullanma](https://docs.microsoft.com/contribute/markdown-reference).

4. Dosya değişikliğini öner bölümünde, *nelerin* değiştirildiğini açıklayan genel teslim açıklamasını girin. Ardından **Dosya değişikliğini öner**' i seçin.

5. Aşağı kaydırın ve yaptığınız değişiklikleri doğrulayın. Formu açmak için **çekme Isteği oluştur** ' u seçin. Bu değişikliği *neden* yaptık açıkla. Makalenin yazarına ve gözden geçirdikleri isteği etiketleyerek. **Çekme Isteği oluştur**' u seçin.

### <a name="what-to-contribute"></a>Katkıda bulunma

Katkıda bulunmak istiyorsanız ancak nereden başlayabileceğinizi bilmiyorsanız aşağıdaki önerilere bakın:

- Topluluk hedefli Etiketler için sorun listesinde arama yapın:

  - [iyi ilk sorun](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [yardım-istenen](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Microsoft yazarları bu etiketleri, topluluk katkısı için iyi adaylar olan sorunlara atar.

- Doğruluk için bir makaleyi gözden geçirin. Ardından biçimi `mm/dd/yyyy` kullanarak **MS. Date** meta verilerini güncelleştirin. Bu katkı, içeriğin yeni kalmasına yardımcı olur.

- Deneyiminize göre açıklamalar, örnekler veya rehberlik ekleyin. Bu katkı, bilgi paylaşmak için topluluğun gücünü kullanır.

- Ingilizce olmayan bir dilde çevirileri doğru yapın. Bu katkı, yerelleştirilmiş içeriğin kullanılabilirliğini geliştirir.

> [!NOTE]
> Büyük katkılar, bir Microsoft çalışanı değilseniz bir katkı lisans sözleşmesinin (CLA) imzalanmasını gerektirir. Bir katkı eşiği karşıladığında GitHub otomatik olarak bu sözleşmeyi imzalamanız gerekir.

### <a name="tips"></a>İpuçları

Configuration Manager belgelerine katkıda bulunmak için aşağıdaki genel yönergeleri izleyin:

- Büyük çekme istekleri konusunda sürmeyin. Bunun yerine [bir sorun verin](#bkmk_docfeedback) ve bir tartışma başlatın. Daha sonra, büyük bir süre yatırmadan önce bir yönü kabul eteceğiz.

- [Microsoft Stil Kılavuzu ' nu](https://aka.ms/MicrosoftStyle)okuyun. [Microsoft stili ve sesi Için en iyi 10 ipucunu](https://docs.microsoft.com/style-guide/top-10-tips-style-voice)öğrenin.

- [Çekme isteği şablonunu](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) , çalışmanızın başlangıç noktası olarak kullanın.

- [GitHub Flow iş akışını](https://guides.github.com/introduction/flow/)izleyin.

- Web günlüğü ve Tweet (veya herhangi bir) katkılarınız hakkında sıkça!

(Bu liste, [.net katkıda bulunan kılavuzdan](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts)ödünç alındı.)

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Microsoft Uç Nokta Yöneticisi belgelerinin birleştirilmesi

Intune ve Configuration Manager birleştirilmiş senaryoları daha iyi desteklemek için, belge kitaplıkları [Microsoft Endpoint Manager sitesinde](https://docs.microsoft.com/mem)birleştirilir. Intune belgeleri artık [docs.Microsoft.com/mem/inTune](https://docs.microsoft.com/mem/intune)' dir ve Configuration Manager belgeleri artık [docs.Microsoft.com/mem/ConfigMgr](https://docs.microsoft.com/mem/configmgr). Hala eski bir URL kullanıyorsanız, bu içeriği okumak için herhangi bir değişiklik yapmanıza gerek kalmaz, otomatik olarak yeniden yönlenmez.

Geribildirim sağlar veya makalelere katkıda bulunun, bazı değişiklikler yapmanız gerekir:

- Mevcut GitHub sorunları özgün depoda, [ıntunedocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) veya [sccmdocs](https://github.com/MicrosoftDocs/SCCMDocs/issues)içinde kalır.

  - Bu sorunlar, bağlantılı makalenin geri bildirim bölümünde açık veya kapalı sorunlar olarak gösterilmez.

  - Bu sorunları çözmeye yönelik çalışmaya devam edeceğiz.

  - Bazı örneklerde, adreslerimizi düşündüğdiğimiz bir sorunu kapatmaya yönelik zor kararı veriyoruz.

  - Mevcut depoda bir sorununuz varsa ve onunla ilgili bir sorun varsa, [Memdocs deposundaki](https://github.com/MicrosoftDocs/MEMDocs)geçirilmiş makalede dosya geri bildirimi.

- Şimdi geri bildirim dosyası veya bir makaleyi düzenlediğinizde, sorun veya çekme isteği MEMDocs deposuna gider.
