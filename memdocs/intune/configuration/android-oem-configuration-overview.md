---
title: Microsoft Intune-Azure 'da Android kurumsal cihazlarda OEMConfig kullanma | Microsoft Docs
description: OEMConfig ile Android Enterprise çalıştıran cihazları yönetmek ve kullanmak için Microsoft Intune kullanın. Genel bakış da dahil olmak üzere tüm adımlara göz atın, önkoşullara bakın, Intune 'da yapılandırma profilini oluşturun ve desteklenen OEMConfig uygulamalarının listesini görüntüleyin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 014608a5042f15ab9ef250b42ad816e8130e2960
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791700"
---
# <a name="use-and-manage-android-enterprise-devices-with-oemconfig-in-microsoft-intune"></a>Microsoft Intune 'de OEMConfig ile Android kurumsal cihazlarını kullanma ve yönetme

Microsoft Intune 'de, Android Kurumsal cihazları için OEM 'e özgü ayarları eklemek, oluşturmak ve özelleştirmek üzere OEMConfig ' i kullanabilirsiniz. OEMConfig, genellikle Intune 'da yerleşik olmayan ayarları yapılandırmak için kullanılır. Farklı orijinal ekipman üreticileri (OEM) farklı ayarlar içerir. Kullanılabilir ayarlar, OEM 'lerin OEMConfig uygulamasında neleri içerdiğine bağlıdır.

Bu özellik şu platformlarda geçerlidir:  

- Android Kurumsal

Android Cihaz Yöneticisi cihazları için [Mobil uzantılar (MX)](android-zebra-mx-overview.md)kullanın.

Bu makalede, OEMConfig açıklanmakta, önkoşulları listelemektedir, bir yapılandırma profili oluşturma ve Intune 'da desteklenen OEMConfig uygulamalarının nasıl listelendiği gösterilmektedir.

## <a name="overview"></a>Genel Bakış

OEMConfig ilkeleri, [uygulama yapılandırma ilkesine](../apps/app-configuration-policies-overview.md)benzer şekilde özel bir cihaz yapılandırma ilkesi türüdür. OEMConfig, Android tarafından, OEM 'Ler tarafından yazılan uygulamalara cihaz ayarları göndermek için Android 'de uygulama yapılandırması kullanan bir standart standarttır (özgün ekipman üreticileri). Bu standart, OEM 'Lerin ve EMMs 'nin (Enterprise Mobility Management), OEM 'e özgü özellikleri standartlaştırılmış bir şekilde oluşturmasına ve desteklemeye izin verir. [OEMConfig hakkında daha fazla bilgi edinin](https://blog.google/products/android-enterprise/oemconfig-supports-enterprise-device-features/).

Geçmişte, Intune gibi, OEM tarafından sunulduktan sonra OEM 'e özgü özellikler için el ile destek desteği. Bu yaklaşım, yinelenen çabalara ve yavaş benimsemeye yol açar.

OEMConfig ile OEM, OEM 'e özgü yönetim özelliklerini tanımlayan bir şema oluşturur. OEM, şemayı bir uygulamaya katıştırır ve sonra bu uygulamayı Google Play koyar. EMM uygulamadan şemayı okur ve bu şemayı EMM yönetici konsolunda kullanıma sunar. Konsol, Intune yöneticilerinin şemadaki ayarları yapılandırmasına izin verir.

OEMConfig uygulaması bir cihaza yüklediğinde, cihazı yönetmek için EMM Yöneticisi 'nde yapılandırılan ayarları kullanır. Cihaz ayarları, EMM tarafından oluşturulan bir MDM Aracısı yerine OEMConfig uygulaması tarafından yürütülür.

OEM, yönetim özelliklerini ekler ve iyileştirir. Ayrıca, OEM Google Play de uygulamayı güncelleştirir. Yönetici olarak, bu yeni özellikleri ve güncelleştirmeleri (düzeltmeler dahil), EMMs 'lerin bu güncelleştirmeleri içermesini beklemeden alırsınız.

> [!TIP]
> Yalnızca bu özelliği destekleyen ve karşılık gelen bir OEMConfig uygulaması olan cihazlarla OEMConfig kullanabilirsiniz. Belirli Ayrıntılar için OEM 'nize danışın.

## <a name="before-you-begin"></a>Başlamadan önce

OEMConfig kullanırken aşağıdaki bilgileri unutmayın:

- Intune, OEMConfig uygulamasının şemasını, yapılandırmak için kullanıma sunar. Intune, uygulama tarafından belirtilen şemayı doğrulamaz veya değiştirmez. Bu nedenle, şema yanlışsa veya hatalı veriler içeriyorsa, bu veriler cihazlara gönderilir. Şemada kaynaklanan bir sorun bulursanız, kılavuza yönelik OEM ile görüşün.
- Intune, uygulama şemasının içeriğini etkilemez veya denetlemez. Örneğin, Intune dizeler, dil, izin verilen eylemler ve benzeri bir denetim yoktur. OEMConfig ile cihazlarını yönetme hakkında daha fazla bilgi için OEM 'ye başvurmanızı öneririz.
- Herhangi bir zamanda, OEM 'Ler desteklenen özellikleri ve şemaları güncelleştirebilir ve yeni bir uygulamayı Google Play karşıya yükleyebilir. Intune, Google Play 'ten her zaman OEMConfig uygulamasının en son sürümünü eşitler. Intune, şemanın veya uygulamanın eski sürümlerini korumaz. Sürüm çakışmaları ' nı çalıştırırsanız daha fazla bilgi için OEM 'ye başvurmanızı öneririz.
- Zeköşeli cihazlarda birden çok profil oluşturabilir ve bunları aynı cihaza atayabilirsiniz. Daha fazla bilgi için bkz. [Zeköşeli cihazlarda Oemconfig](oemconfig-zebra-android-devices.md).

  Zemilden olmayan cihazlarda OEMConfig modeli yalnızca cihaz başına tek bir ilkeyi destekler. Aynı cihaza birden çok profil atanmışsa, tutarsız bir davranış görebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

Cihazlarınızda OEMConfig kullanmak için aşağıdaki gereksinimlere sahip olduğunuzdan emin olun:

- Intune 'A kayıtlı bir Android kurumsal cihaz.
- OEM tarafından oluşturulan ve Google Play yüklenen bir OEMConfig uygulaması. Google Play yoksa daha fazla bilgi için OEM ile görüşün.
- Intune Yöneticisi, **mobil uygulamalar**için rol tabanlı erişim denetımı (RBAC) izinlerine, **cihaz yapılandırmalarına**ve **Android for Work**altında "okuma" iznine sahiptir. OEMConfig profilleri cihaz yapılandırmalarını yönetmek için yönetilen uygulama yapılandırmalarını kullandığından, bu izinler gereklidir.

## <a name="prepare-the-oemconfig-app"></a>OEMConfig uygulamasını hazırlama

Cihazın OEMConfig 'i desteklediğinden emin olun, Intune 'a doğru OEMConfig uygulamasının eklendiğinden ve uygulamanın cihaza yüklü olduğundan emin olun. Bu bilgi için OEM ile görüşün.

> [!TIP] 
> OEMConfig uygulamaları OEM 'e özgüdür. Örneğin, Zeköşeli teknolojiler cihazında yüklü bir Sony OEMConfig uygulaması hiçbir şey yapmaz.

1. Yönetilen Google Play Store OEMConfig uygulamasını alın. [Android kurumsal cihazlara yönetilen Google Play uygulamaları ekleme](../apps/apps-add-android-for-work.md) adımları listeler.
2. Bazı OEM 'Ler, önceden yüklenmiş OEMConfig uygulaması olan cihazları sevk edebilir. Uygulama önceden yüklü değilse, Intune 'u kullanarak [uygulamayı ekleyin ve cihazlara dağıtın](../apps/apps-deploy.md).

## <a name="create-an-oemconfig-profile"></a>OEMConfig profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **Android kurumsal**' i seçin.
    - **Profil**: **oemconfig**' i seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: Yeni profil için açıklayıcı bir ad girin.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Oemconfig uygulaması**: **bir oemconfig uygulaması seçin**öğesini seçin.

6. **İlişkili uygulamada**, daha önce eklemiş olduğunuz mevcut bir oemconfig uygulamasını seçin > **seçin**. İlkeyi atadığınız cihazlar için doğru OEMConfig uygulamasını seçtiğinizden emin olun.

    Listelenen herhangi bir uygulamayı görmüyorsanız, yönetilen Google Play ayarlayın ve yönetilen Google Play deposundan uygulamalar alın. [Android kurumsal cihazlara yönetilen Google Play uygulamaları ekleme](../apps/apps-add-android-for-work.md) adımları listeler.

    > [!IMPORTANT]
    > Bir OEMConfig uygulaması eklediyseniz ve onu Google Play olarak eşitledi ancak **ilişkili bir uygulama**olarak listelenmediyse, uygulamayı eklemek için Intune ile iletişim kurmanız gerekebilir. Bkz. [Yeni uygulama ekleme](#supported-oemconfig-apps) (Bu makalede).

7. **İleri**’yi seçin.
8. **Ayarları Yapılandır**bölümünde **yapılandırma tasarımcısını** veya **JSON düzenleyicisini**seçin:

    > [!TIP]
    > Özellikleri doğru şekilde yapılandırdığınızdan emin olmak için OEM belgelerini okuyun. Bu uygulama özellikleri, Intune 'A değil, OEM tarafından dahildir. Intune, özelliklerin en düşük doğrulamasını veya girdiğiniz şeyleri yapar. Örneğin, `abcd` bir bağlantı noktası numarası girerseniz, profil olarak kaydedilir ve yapılandırdığınız değerlerle cihazlarınıza dağıtılır. Doğru bilgileri girdiğinizden emin olun.

    - **Yapılandırma Tasarımcısı**: Bu seçeneği belirlediğinizde, uygulama şeması içinde kullanılabilen özellikler, yapılandırmanız için gösterilir.

      - Yapılandırma tasarımcısında bağlam menüleri daha fazla seçenek olduğunu gösterir. Örneğin, bağlam menüsü ayarları eklemenize, silmenize ve yeniden sıralamanıza izin verebilir. Bu seçenekler OEM tarafından dahildir. Bu seçeneklerin profil oluşturmak için nasıl kullanılması gerektiğini öğrenmek için OEM uygulaması belgelerini okuduğunuzdan emin olun.

      - Birçok ayar OEM tarafından sağlanan varsayılan değerlere sahiptir. Varsayılan bir değer olup olmadığını görmek için, ayarın yanındaki bilgi simgesinin üzerine gelin. Araç ipucu, bu ayar (varsa) için varsayılan değerleri ve OEM tarafından sağlanmış diğer ayrıntıları gösterir.

      - **Temizle** ' ye tıkladığınızda profilden bir ayar silinir. Bir ayar profilde değilse, profil uygulandığında cihazdaki değeri değişmez.

      - Yapılandırma tasarımcısında boş (yapılandırılmamış) bir paket oluşturursanız, JSON düzenleyicisine geçildiğinde silinir.

    - **JSON Düzenleyicisi**: Bu seçeneği belirlediğinizde, uygulamada gömülü tam yapılandırma şeması için bir şablon IÇEREN bir JSON Düzenleyicisi açılır. Düzenleyicide, şablonu farklı ayarlar için değerlerle özelleştirin. Değerlerinizi değiştirmek için **yapılandırma tasarımcısını** KULLANıRSANıZ, JSON Düzenleyicisi şablonun üzerine yapılandırma tasarımcısından değerler yazar.

      - Var olan bir profili güncelleştiriyorsanız JSON Düzenleyicisi, en son profille kaydedilen ayarları gösterir.

      - OEMConfig şemaları büyük ve karmaşık olabilir. Bu ayarları farklı bir düzenleyici kullanarak güncelleştirmeyi tercih ediyorsanız **JSON şablonu indir** düğmesini seçin. Yapılandırma değerlerinizi şablona eklemek için istediğiniz düzenleyiciyi kullanın. Ardından, içindeki güncelleştirilmiş JSON ' ı kopyalayın ve **JSON Düzenleyicisi** özelliğine yapıştırın.

      - Yapılandırmanızın bir yedeğini oluşturmak için JSON düzenleyicisini kullanabilirsiniz. Ayarlarınızı yapılandırdıktan sonra, bu özelliği kullanarak JSON ayarlarını değerlerinizle birlikte alın. JSON dosyasını kopyalayıp bir dosyaya yapıştırın ve kaydedin. Artık bir yedekleme dosyanız var.

    Yapılandırma tasarımcısında yapılan tüm değişiklikler JSON düzenleyicisinde de otomatik olarak yapılır. Benzer şekilde, JSON düzenleyicisinde yapılan tüm değişiklikler otomatik olarak yapılandırma tasarımcısında yapılır. Giriş bilgileriniz geçersiz değerler içeriyorsa, sorunları düzelene kadar yapılandırma Tasarımcısı ile JSON Düzenleyicisi arasında geçiş yapamazsınız.

9. **İleri**’yi seçin.
10. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

11. **Atamalar**' da, profilinizi alacak kullanıcıları veya grupları seçin. Her cihaza bir profil atayın. OEMConfig modeli cihaz başına yalnızca bir ilkeyi destekler.

    Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

12. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

Cihaz yapılandırma güncelleştirmelerini bir daha denetlediğinde, yapılandırdığınız OEM 'e özgü ayarlar OEMConfig uygulamasına uygulanır.

> [!NOTE]
> OEMConfig standart Şu anda durum bildirimi içermiyor. Bu nedenle, profiller varsayılan olarak **bekleyen** bir durumu gösterir.

## <a name="supported-oemconfig-apps"></a>Desteklenen OEMConfig uygulamaları

OEMConfig Apps, standart uygulamalarla karşılaştırıldığında, Google tarafından daha karmaşık şemaları desteklemek için verilen yönetilen yapılandırma ayrıcalıklarını genişletir. Intune Şu anda aşağıdaki OEMConfig uygulamalarını desteklemektedir:

-----------------

| OEM | Paket Kimliği | OEM belgeleri (varsa) |
| --- | --- | ---|
| Ascom | com. Ascom. Myco. oemconfig | |
| Cipherlab | com. cipherlab. oemconfig | |
| Dataloi | com. datalobir. Settings. oemconfig | [Datalobir OEMConfig Kılavuzu](https://datalogic.github.io/oemconfig/overview) |
| Honeywell | com. Honeywell. oemconfig |  |
| HMDGlobal-7,2 | com. hmdglobal. app. oemconfig. n7_2 | 
| HMDGlobal-4,2 | com. hmdglobal. app. oemconfig. n4_2 | 
| Kyocera | JP. Kyocera. enterprisedeviceconfig |  |
| Samsung | com. Samsung. Android. Knox. kpu | [Knox hizmeti eklentisi Yönetici Kılavuzu](https://docs.samsungknox.com/knox-service-plugin/admin-guide/index.htm) |
| Seuic | com. seuic. seuicoemconfig | |
| Spectralink-barkodlar | com. spectralınk. Barcode. Service |  |
| Spectralink-düğmeler | com. spectralınk. düğmeler |  |
| Spectralink-cihaz | com. Spectralink. slnkdevicesettings  |  |
| Spectralink-günlüğe kaydetme | com. Spectralink. slnklogger |  |
| Spectralink-VQO | com. Spectralink. slnkvqo |  |
| Unitech elektroniği | com. Unitech. oemconfig | |
| Zeköşeli teknolojiler | com. zeköşeli. oemconfig. Common | [Zeköşeli OEMConfig genel bakış](http://techdocs.zebra.com/oemconfig ) |

-----------------

Cihazınız için bir OEMConfig uygulaması varsa, ancak yukarıdaki tabloda değil veya Intune konsolunda, e-posta ile gösterilmemişse `IntuneOEMConfig@microsoft.com` .

> [!NOTE]
> Oemconfig Apps, OEMConfig profilleriyle yapılandırılanmadan önce Intune tarafından eklenmediyse olmalıdır. Bir uygulama desteklendikten sonra kiracınızda ayarlama hakkında Microsoft 'a başvurmanız gerekmez. Bu sayfadaki yönergeleri izlemeniz yeterlidir.
>
> Yanlış davranan bir OEMConfig uygulaması yaşarsanız, OEMConfig uygulamasının geliştiricilerine başvurun. Intune, bireysel OEMConfig uygulamalarıyla ilgili teknik sorunlardan sorumlu değildir.

## <a name="next-steps"></a>Sonraki adımlar

[Profil durumunu izleyin](device-profile-monitor.md).
