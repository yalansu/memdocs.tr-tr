---
title: Yapılandırma taban çizgileri oluşturma
titleSuffix: Configuration Manager
description: Bir koleksiyona dağıtabileceğiniz Configuration Manager yapılandırma temelleri oluşturun.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2028974c166e060f445b255db6c5af707725a3f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712928"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Configuration Manager yapılandırma temelleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Configuration Manager içindeki yapılandırma temelleri, önceden tanımlanmış yapılandırma öğelerini ve isteğe bağlı olarak diğer yapılandırma temellerini içerir. Yapılandırma temeli oluşturduktan sonra, bir koleksiyona dağıtarak söz konusu koleksiyondaki cihazların yapılandırma temelini indirmesini ve uyumluluklarını değerlendirmesini sağlayabilirsiniz.  

## <a name="configuration-baselines"></a>Yapılandırma temelleri

 Configuration Manager yapılandırma temelleri, yapılandırma öğelerinin belirli düzeltmelerini içerebilir veya her zaman bir yapılandırma öğesinin en son sürümünü kullanacak şekilde yapılandırılabilir. Yapılandırma öğesi düzeltmeleri hakkında daha fazla bilgi için bkz. [yapılandırma verileri Için yönetim görevleri](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Yapılandırma temelleri oluşturmak için kullanabileceğiniz iki yöntem vardır:  

- Yapılandırma verilerini bir dosyadan içeri aktarın. **Yapılandırma Verilerini İçeri Aktarma Sihirbazı**’nı başlatmak için **Varlıklar ve Uyumluluk** çalışma alanının **Yapılandırma Öğeleri** veya **Yapılandırma Temelleri** düğümünde **Yapılandırma Verilerini İçeri Aktar**’a tıklayın. Daha fazla bilgi için bkz. [yapılandırma verilerini Içeri aktarma](import-configuration-data.md).

- Yeni bir yapılandırma temeli oluşturmak için **Yapılandırma Temeli Oluştur** iletişim kutusunu kullanın.  

## <a name="create-a-configuration-baseline"></a>Yapılandırma temeli oluşturma

**Yapılandırma temeli oluştur** iletişim kutusunu kullanarak yapılandırma temeli oluşturmak için aşağıdaki yordamı kullanın:  

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Uyumluluk ayarları** > **yapılandırma temelleri**' ne tıklayın.  

2. **Giriş** sekmesindeki **Oluştur** grubunda, **Yapılandırma Temeli Oluştur**'a tıklayın.  

3. **Yapılandırma Temeli Oluştur** iletişim kutusunda yapılandırma temeli için benzersiz bir ad ve açıklama girin. Ad için en fazla 255 ve açıklama için en fazla 512 karakter kullanabilirsiniz.  

4. **Yapılandırma verileri** bu yapılandırma temeline dahil edilen tüm yapılandırma öğelerini veya yapılandırma temellerini görüntüler. Listeye yeni bir yapılandırma öğesi veya yapılandırma temeli eklemek için **Ekle** ’ye tıklayın. Aşağıdaki öğeler arasından seçim yapabilirsiniz:  

   - **Varlıklar ve Uyumluluk**  

   - **Yazılım güncelleştirmeleri**  

   - **Yapılandırma Öğeleri**  
     > [!IMPORTANT]
     > Her yapılandırma temelini 1000 'den daha fazla yazılım güncelleştirmesi olmadan sınırlamanız gerekir.
5. **Yapılandırma verileri** listesinde seçtiğiniz bir yapılandırma öğesinin davranışını belirtmek Için **amacı Değiştir** listesini kullanın. Aşağıdaki öğelerden seçim yapabilirsiniz:  

   -   **Gerekli**: yapılandırma öğesi bir istemci cihazında algılanmadıysa yapılandırma temeli uyumsuz olarak değerlendirilir. Algılanırsa, uyumluluk için değerlendirilir  

   -   **Isteğe bağlı**: yapılandırma öğesi yalnızca başvurduğu uygulamanın istemci bilgisayarlarda bulunması durumunda uyumluluk için değerlendirilir. Uygulama bulunamazsa yapılandırma temeli uyumsuz olarak işaretlenmez (yalnızca uygulama yapılandırma öğeleri için geçerlidir).  

   -   **Yasaklanmış**: yapılandırma öğesi istemci bilgisayarlarda algılanırsa (yalnızca uygulama yapılandırma öğeleri için geçerlidir) yapılandırma temeli uyumsuz olarak değerlendirilir.  

   > [!NOTE]
   >  **Amacı Değiştir** listesi yalnızca **Yapılandırma Öğesi Oluşturma Sihirbazı** ’nın **Genel** sayfasındaki **Bu yapılandırma öğesi uygulama ayarlarını içerir**seçeneğine tıkladıysanız kullanılabilir.  

6. İstemci cihazlarda uyumluluğu değerlendirmek üzere yapılandırma öğesinin belirli bir sürümünü veya son sürümünü seçmek için **Revizyonu Değiştir** listesini kullanın veya her zaman son sürümü kullanmak için **Her Zaman Son Sürümü Kullan** ’ı seçin. Yapılandırma öğesi düzeltmeleri hakkında daha fazla bilgi için bkz. [yapılandırma verileri Için yönetim görevleri](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7. Yapılandırma temelinden bir yapılandırma öğesini kaldırmak için bir yapılandırma öğesi seçip **Kaldır**' a tıklayın.  

8. Sürüm 1806 ' den başlayarak, **Bu taban çizgisini ortak yönetilen istemciler Için her zaman uygulamak**istiyorsanız seçin. İşaretlendiğinde, bu taban çizgisi Intune tarafından yönetilen istemciler için de geçerlidir.  Bu özel durum, kuruluşunuz için gereken ancak henüz Intune 'da kullanılamayan ayarları yapılandırmak için kullanılabilir.

9. İsteğe bağlı olarak, arama ve filtreleme için temele kategori atamak üzere **Kategoriler** ' e tıklayın. 

10. **Yapılandırma Temeli Oluştur** iletişim kutusunu kapatmak yapılandırma temeli oluşturmak için **Tamam** ’a tıklayın.  

>[!NOTE]
> Mevcut bir taban çizgisini değiştirme (örneğin, **Bu temeli ortak yönetilen istemciler Için her zaman Uygula**), temel içerik sürümünü artırır. İstemcilerin temel raporlamayı güncelleştirmek için yeni sürümü değerlendirmesi gerekecektir.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a>Uyumluluk ilkesi değerlendirmesinin bir parçası olarak özel yapılandırma temellerini dahil et
<!--3608345-->
*(Sürüm 1910 ' de tanıtılmıştır)*

Sürüm 1910 ' den başlayarak, özel yapılandırma temellerinin değerlendirmesi bir uyumluluk ilkesi değerlendirme kuralı olarak eklenebilir. Bir yapılandırma temeli oluşturduğunuzda veya düzenlediğinizde, **Bu taban çizgisini uyumluluk ilkesi değerlendirmesinin bir parçası olarak değerlendirmek**için bir seçeneğe sahip olursunuz. Bir uyumluluk ilkesi kuralı eklerken veya düzenlenirken, **Uyumluluk ilkesi değerlendirmesi ' nde yapılandırılmış taban çizgileri ekle**adlı bir koşulunuz vardır. Ortak yönetilen cihazlar için ve Intune 'u, genel uyumluluk durumunun bir parçası olarak Configuration Manager uyumluluk değerlendirmesi sonuçları alacak şekilde yapılandırdığınızda, bu bilgiler Azure AD 'ye gönderilir. Daha sonra bunu, Office 365 kaynaklarınıza koşullu erişim için kullanabilirsiniz. Daha fazla bilgi için bkz. [ortak yönetim Ile koşullu erişim](../../comanage/quickstart-conditional-access.md).

Uyumluluk ilkesi değerlendirmesinin bir parçası olarak özel yapılandırma temelleri eklemek için aşağıdakileri yapın:

- [**Uyumluluk ilkesi değerlendirmesinde yapılandırılmış taban çizgileri dahil**](#bkmk_CA)etmek için bir kuralla bir kullanıcı koleksiyonuna uyumluluk ilkesi oluşturun ve dağıtın.
- Bir cihaz koleksiyonuna dağıtılan bir yapılandırma temelindeki [**Uyumluluk ilkesi değerlendirmesinin bir parçası olarak bu temeli değerlendir**](#bkmk_eval-baseline) ' i seçin.

> [!IMPORTANT]
> Ortak yönetilen cihazları hedeflerken, [ortak yönetim önkoşullarını](../../comanage/overview.md#prerequisites)karşıladığınızdan emin olun.

### <a name="example-evaluation-scenario"></a>Örnek değerlendirme senaryosu

Kullanıcı, **Uyumluluk ilkesi değerlendirmesi içinde yapılandırılmış taban çizgilerini**içeren bir uyumluluk ilkesiyle hedeflenen bir koleksiyonun parçası olduğunda, kullanıcıya dağıtılan veya Kullanıcı cihazının uyumluluk **değerlendirmesi için bu temeli, uyumluluk Ilkesi değerlendirmesi kapsamında değerlendir** seçeneğinin seçili olduğu taban çizgileri. Örneğin:

- `User1`parçasıdır `User Collection 1`.
- `User1`, `Device1`ve `Device Collection 1` `Device Collection 2`içinde olan kullanır.
- `Compliance Policy 1`**Uyumluluk ilkesi değerlendirmesi kural koşulunda yapılandırılmış taban çizgilerini içerir** ve öğesine `User Collection 1`dağıtılır.
- `Configuration Baseline 1`, seçilen ve dağıtıldığı **Uyumluluk ilkesi değerlendirmesi kapsamında bu temeli değerlendirmiştir** `Device Collection 1`.
- `Configuration Baseline 2`, seçilen ve dağıtıldığı **Uyumluluk ilkesi değerlendirmesi kapsamında bu temeli değerlendirmiştir** `Device Collection 2`.

Bu senaryoda `Compliance Policy 1` , `User1` `Device1`kullanımı değerlendirirken, her ikisi de `Configuration Baseline 1` `Configuration Baseline 2` olarak değerlendirilir.

- `User1`Bazen kullanır `Device2`.
- `Device2`, `Device Collection 2` ve `Device Collection 3`üyesidir.
- `Device Collection 3`kendisine `Configuration Baseline 3` dağıtıldı, ancak **Uyumluluk ilkesi değerlendirmesi kapsamında bu temeli değerlendir** seçili değildir.

`User1` Kullandığında `Device2`, yalnızca `Configuration Baseline 2` `Compliance Policy 1` değerlendirirken değerlendirilir.

> [!NOTE]
><!--5582516-->
> Uyumluluk ilkesi daha önce istemcide hiçbir daha önce değerlendirilmeyen yeni bir temeli değerlendiriyorsa, uyumsuz olmayan rapor verebilir. Bu durum, uyumluluk değerlendirildiği zaman taban çizgisi değerlendirmesi hala çalışıyorsa oluşur. Bu soruna geçici bir çözüm olarak, **Yazılım Merkezi**'Nde **uyumluluğu denetle** ' ye tıklayın.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a>Temel uyumluluk ilkesi değerlendirmesi için bir kuralla uyumluluk ilkesi oluşturma ve dağıtma

1. **Varlıklar ve uyum** çalışma alanında, **Uyumluluk ayarları**' nı genişletin ve **uyumluluk ilkeleri** düğümünü seçin.
1. **Uyumluluk Ilkesi oluşturma Sihirbazı 'nı**açmak Için şeritte **Uyumluluk İlkesi Oluştur** ' a tıklayın. 
1. **Genel** sayfasında, **Configuration Manager istemcisiyle yönetilen cihazlar için Uyumluluk kuralları**' nı seçin.
   - Uyumluluk ilkesi değerlendirmesinin bir parçası olarak özel yapılandırma temellerini dahil etmek için cihazların Configuration Manager istemcisiyle yönetilmesi gerekir.
1. **Desteklenen platformlar** sayfalarında Platformlarınızı seçin.
1. **Kurallar** sayfasında, **Yeni**' yi seçin ve ardından **Uyumluluk ilkesi değerlendirmesi durumunda yapılandırılmış taban çizgileri dahil et** ' i seçin.

   ![Uyumluluk ilkesi değerlendirmesi koşulunda yapılandırılan temelleri dahil et](./media/3608345-create-compliance-policy-rule.png)

1. **Özet** sayfasına ulaşmak için **Tamam**' a ve ardından **İleri** ' ye tıklayın.
1. Seçimlerinizi doğrulayın ve **İleri** ' ye tıkladıktan sonra **Kapat**' a tıklayın.
1. **Uyumluluk ilkeleri** düğümünde, oluşturduğunuz ilkeye sağ tıklayın ve **Dağıt**' ı seçin.
1. İlke için koleksiyonunuzu, uyarı oluşturma ayarlarınızı ve uyumluluk değerlendirme zamanlamanızı seçin.
1. Uyumluluk ilkesini dağıtmak için **Tamam** ' ı tıklatın.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Bir yapılandırma temeli seçin ve "uyumluluk ilkesi değerlendirmesi kapsamında bu temeli değerlendir" seçeneğini işaretleyin

1. **Varlıklar ve uyum** çalışma alanında, **Uyumluluk ayarları**' nı genişletin ve **yapılandırma temelleri** düğümünü seçin.
1. Bir cihaz koleksiyonuna dağıtılan mevcut bir taban çizgisine sağ tıklayıp **Özellikler**' i seçin. Gerekirse, yeni bir taban çizgisi oluşturabilirsiniz.
   - Taban çizgisi, bir kullanıcı koleksiyonuna değil, bir cihaz koleksiyonuna dağıtılmalıdır.
1. **Bu taban çizgisini uyumluluk ilkesi değerlendirmesi kapsamında değerlendir** ayarını etkinleştirin.
   - Intune 'U **cihaz yapılandırma** yetkilisi olarak kullanan ortak yönetilen cihazlar için, **ortak yönetilen istemciler de seçili olsa bile bu temeli her zaman uygulayın** .
1. Yapılandırma temelinizdeki değişiklikleri kaydetmek için **Tamam** ' ı tıklatın.

   ![Yapılandırma temeli özellikleri iletişim kutusu](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Uyumluluk ilkesi değerlendirmesinin bir parçası olarak özel yapılandırma temelleri için günlük dosyaları

- Karmaşıancehandler. log
- SettingsAgent. log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Sonraki adımlar

[Yapılandırma verilerini içeri aktarma](import-configuration-data.md)
