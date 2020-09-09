---
title: Rol tabanlı yönetimi yapılandırma
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
description: Güvenlik rollerini, güvenlik kapsamlarını ve atanmış koleksiyonları birleştirerek her yönetici kullanıcının yönetim kapsamını tanımlayın
ms.openlocfilehash: a475660d2a171829e1592c1c411a3251e74eb79f
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607614"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Configuration Manager için rol tabanlı yönetimi yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, rol tabanlı yönetim güvenlik rollerini, güvenlik kapsamlarını ve atanmış koleksiyonları birleştirerek her yönetici kullanıcının yönetim kapsamını tanımlar. Yönetim kapsamı, bir yönetici kullanıcının Configuration Manager konsolunda görüntüleyebileceği nesneleri ve yönetici kullanıcının gerçekleştirme iznine sahip olduğu nesnelerle ilgili görevleri içerir. Rol tabanlı yönetim yapılandırmaları hiyerarşideki her sitede uygulanır.  

 Rol tabanlı yönetim kavramlarını henüz bilmiyorsanız, bkz. [rol tabanlı yönetimin temelleri](../../../understand/fundamentals-of-role-based-administration.md).  

 Aşağıdaki yordamlardaki bilgiler, rol tabanlı yönetim ve ilgili güvenlik ayarlarını oluşturmanıza ve yapılandırmanıza yardımcı olabilir:  

- [Özel güvenlik rolleri oluşturma](#BKMK_CreateSecRole)  
- [Güvenlik rollerini yapılandırma](#BKMK_ConfigSecRole)  
- [Nesnenin güvenlik kapsamlarını yapılandırma](#BKMK_ConfigSecScope)  
- [Güvenliği yönetmek için koleksiyonları yapılandırma](#BKMK_ConfigColl)  
- [Yeni yönetici kullanıcı oluştur](#BKMK_Create_AdminUser)  
- [Yönetici kullanıcının yönetim kapsamını değiştirme](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Özel güvenlik rolleri oluşturma

 Configuration Manager, birkaç yerleşik güvenlik rolü sağlar. Ek güvenlik rollerine ihtiyacınız varsa mevcut güvenlik rolünün kopyasını oluşturduktan sonra kopyayı değiştirerek bir özel güvenlik rolü oluşturabilirsiniz. Yönetici kullanıcılara, gerekli olan ve atanmış olan güvenlik rolüne dahil olmayan ek güvenlik izinlerini vermek için özel bir güvenlik rolü oluşturabilirsiniz. Özel güvenlik rolünü kullanarak onlara yalnızca ihtiyaç duydukları izinleri verebilir ve ihtiyaç duyduklarından fazla izinler veren bir güvenlik rolünün atanmasına engel olabilirsiniz.  

 Mevcut güvenlik rolünü şablon olarak kullanarak yeni bir güvenlik rolü oluşturmak için aşağıdaki yordamı kullanın.  

### <a name="to-create-custom-security-roles"></a>Özel güvenlik rolleri oluşturmak için

1. Configuration Manager konsolunda, **Yönetim**' e gidin.  

2. **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **güvenlik rolleri**' ni seçin.  

   ‏Yeni güvenlik rolünü oluşturmak için aşağıdaki işlemlerden birini kullanın:  

    - Yeni özel güvenlik rolünü oluşturmak için aşağıdaki eylemleri gerçekleştirin:  

      1. Yeni güvenlik rolünün kaynağı olarak kullanmak için mevcut bir güvenlik rolünü seçin.
      2. **Giriş** sekmesinde, **güvenlik rolü** grubunda, **Kopyala**' yı seçin. Bu eylem, kaynak güvenlik rolünün bir kopyasını oluşturur.  
      3. Güvenlik Rolünü Kopyala sihirbazında, yeni özel güvenlik rolü için bir **Ad** belirtin.  
      4. **Güvenlik işlemi atamaları**'nda, kullanılabilir işlemleri görüntülemek için her bir **Güvenlik İşlemleri** düğümünü genişletin.  
      5. Bir güvenlik işleminin ayarını değiştirmek için **değer** sütununda aşağı oku seçin ve **Evet** veya **Hayır**' ı seçin.

            > [!CAUTION]  
            > Özel güvenlik rolünü yapılandırırken, yeni güvenlik rolüyle ilişkilendirilmiş yönetici kullanıcılar için gerekli olmayan izinleri vermemenizi doğrulayın. Örneğin, **güvenlik rolleri** güvenlik işleminin **Değiştir** değeri, yönetici kullanıcılara, bu güvenlik rolüyle ilişkili olmasalar bile, erişilebilir güvenlik rollerini düzenleme izni verir.  

      6. İzinleri yapılandırdıktan sonra, yeni güvenlik rolünü kaydetmek için **Tamam** ' ı seçin.  

    - Başka bir Configuration Manager hiyerarşisinden dışarı aktarılmış bir güvenlik rolünü içeri aktarmak için aşağıdaki işlemleri gerçekleştirin:  

        1. **Giriş** sekmesinde, **Oluştur** grubunda, **güvenlik rolünü içeri aktar**' ı seçin.  
        2. İçeri aktarmak istediğiniz güvenlik rolü yapılandırmasını içeren. xml dosyasını belirtin. Yordamı tamamlayıp güvenlik rolünü kaydetmek için **Aç** ' ı seçin.  

            > [!NOTE]  
            > Güvenlik rolünü içeri aktardıktan sonra, güvenlik rolü özelliklerini düzenleyerek o güvenlik rolüyle ilişkilendirilmiş nesne izinlerini değiştirebilirsiniz.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Güvenlik rollerini yapılandırma

 Bir güvenlik rolü için tanımlanmış güvenlik izinleri gruplarına güvenlik işlemi atamaları denir. Güvenlik işlemi atamaları, her nesne türünde kullanılabilen nesne türleri ve eylemlerin bileşimini temsil eder. Herhangi bir özel güvenlik rolü için hangi güvenlik işlemlerinin kullanılabilir olduğunu değiştirebilirsiniz, ancak Configuration Manager sağladığı yerleşik güvenlik rollerini değiştiremezsiniz.  

 Bir güvenlik rolünün güvenlik işlemlerini değiştirmek için aşağıdaki yordamı kullanın.  

### <a name="to-modify-security-roles"></a>Güvenlik rollerini değiştirmek için

1. Configuration Manager konsolunda, **Yönetim**' i seçin.  
2. **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **güvenlik rolleri**' ni seçin.  
3. Değiştirmek istediğiniz özel güvenlik rolünü seçin.  
4. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  
5. **İzinler** sekmesini seçin.  
6. **Güvenlik işlemi atamaları**'nda, kullanılabilir işlemleri görüntülemek için her bir **Güvenlik İşlemleri** düğümünü genişletin.  
7. Bir güvenlik işleminin ayarını değiştirmek için **değer** sütununda aşağı oku seçin ve ardından **Evet** veya **Hayır**' ı seçin.  

    > [!CAUTION]  
    > Özel güvenlik rolünü yapılandırırken, yeni güvenlik rolüyle ilişkilendirilmiş yönetici kullanıcılar için gerekli olmayan izinleri vermemenizi doğrulayın. Örneğin, **güvenlik rolleri** güvenlik işleminin **Değiştir** değeri, yönetici kullanıcılara, bu güvenlik rolüyle ilişkili olmasalar bile, erişilebilir güvenlik rollerini düzenleme izni verir.  

8. Güvenlik işlemi atamalarını yapılandırmayı tamamladığınızda, yeni güvenlik rolünü kaydetmek için **Tamam** ' ı seçin.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Bir nesne için güvenlik kapsamlarını yapılandırma
 Nesnesinden bir nesne için güvenlik kapsamının ilişkilendirmesini, güvenlik kapsamından değil nesneden yönetirsiniz. Güvenlik kapsamları, doğrudan yapılandırmalar olarak yalnızca ada ve açıklamaya yapılan değişiklikleri destekler. Güvenlik kapsamı özelliklerini görüntülerken bir güvenlik kapsamının adını ve açıklamasını değiştirmek için güvenliği sağlanabilir **Güvenlik Kapsamları** nesnesi için **Değiştir** izninizin olması gerekir.  

 Configuration Manager yeni bir nesne oluşturduğunuzda, bu, nesneyi oluşturmak için kullanılan hesabın güvenlik rolleriyle ilişkili olan her güvenlik kapsamıyla ilişkilendirilir. Bu davranış, bu güvenlik rolleri **oluşturma** Izni veya **güvenlik kapsamını ayarla** iznini sağladığınızda oluşur. Oluşturduktan sonra nesnenin güvenlik kapsamlarını değiştirebilirsiniz.  

 Örnek olarak, size yeni sınır grubu oluşturma izni veren bir güvenlik rolü atamış olursunuz. Yeni bir sınır grubu oluşturduğunuzda, öğesine belirli güvenlik kapsamları atayabileceğiniz bir seçeneğe sahip olursunuz. Bunun yerine, ilişkili olduğunuz güvenlik rollerinin kullanabildiği güvenlik kapsamları otomatik olarak yeni sınır grubuna atanır. Yeni sınır grubunu kaydettikten sonra, yeni sınır grubuyla ilişkilendirilmiş güvenlik kapsamlarını düzenleyebilirsiniz.  

 Bir nesneye atanmış güvenlik kapsamlarını yapılandırmak için aşağıdaki yordamı kullanın.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a> Bir nesnenin güvenlik kapsamlarını yapılandırmak için  

1. Configuration Manager konsolunda, bir güvenlik kapsamına atanmasını destekleyen bir nesne seçin.  
2. **Giriş** sekmesinde, **sınıflandır** grubunda, **güvenlik kapsamlarını ayarla**' yı seçin.
3. **Güvenlik Kapsamlarını Ayarla** iletişim kutusunda, bu nesnenin ilişkilendirildiği güvenlik kapsamlarını seçin veya temizleyin. Güvenlik kapsamlarını destekleyen her nesneye en az bir güvenlik kapsamı atanmalıdır.  
4. Atanan güvenlik kapsamlarını kaydetmek için **Tamam ' ı** seçin.  

    > [!NOTE]  
    > Yeni nesne oluşturduğunuzda, onu birden çok güvenlik kapsamına atayabilirsiniz. Nesneyle ilişkili güvenlik kapsamlarının sayısını değiştirmek için nesne oluşturulduktan sonra bu atamayı değiştirmeniz gerekir.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a> Bir klasöre yönelik güvenlik kapsamlarını yapılandırmak için (sürüm 1906 ' den başlayarak)
<!--3600867-->

1. Configuration Manager konsolunda bir klasör seçin.  
1. Şeritteki **klasör** sekmesinde, **güvenlik kapsamlarını ayarla**' yı seçin.
   - Ayrıca, klasöre sağ tıklayıp **klasör**  >  **Ayarla güvenlik kapsamları**' nı seçebilirsiniz.
1. **Güvenlik kapsamlarını ayarla** iletişim kutusunda, klasör için güvenlik kapsamlarını seçin veya temizleyin. Her bir klasör en az bir güvenlik kapsamına atanmalıdır. Tüm klasörlere, siz değiştirene kadar **varsayılan** güvenlik kapsamı atanır.
1. Atanan güvenlik kapsamlarını kaydetmek için **Tamam ' ı** seçin.  

    > [!IMPORTANT]  
    > - Configuration Manager sürüm 1906 ' i yüklediğinizde, mevcut güvenlik rolleri otomatik olarak **klasör sınıfı** izinlerini alır. Yeni güvenlik rolleri için **klasör sınıfı** izinleri eklemeniz ve mevcut rollerin ortamınız için uygun izinlere sahip olduğundan emin olmanız gerekir.
    > 
    > - Bu Kullanıcı, nesneyi oluşturan kişiyle bir güvenlik kapsamı paylaşıyorsa, bir öğe kullanıcının güvenlik kapsamı dışında bir klasörde aranabilir. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Güvenliği yönetmek için koleksiyonları Yapılandırma

 Koleksiyonları rol tabanlı yönetim için yapılandırma amaçlı bir yordam yoktur. Koleksiyonların rol tabanlı yönetim yapılandırması yoktur. Bunun yerine, yönetici kullanıcıyı yapılandırdığınızda koleksiyonları bir yönetici kullanıcıya atarsınız. Kullanıcı tarafından atanan güvenlik rollerinde etkinleştirilen koleksiyon güvenliği işlemleri, bir yönetici kullanıcının koleksiyonlar ve koleksiyon kaynakları (koleksiyon üyeleri) için sahip olduğu izinleri belirleyebilir.  

 Yönetici kullanıcıların bir koleksiyonla ilgili izinleri varsa o koleksiyonla sınırlanmış olan koleksiyonlarda da izinleri olur. Örnek olarak, kuruluşunuz tüm masaüstleri adlı bir koleksiyon kullanır. Ayrıca tüm masaüstleri koleksiyonuyla sınırlı olan tüm Kuzey Amerika masaüstleri adlı bir koleksiyon da vardır. Bir yönetici kullanıcının Tüm Masaüstleri için izinleri varsa, Tüm Kuzey Amerika Masaüstleri koleksiyonu için de aynı izinleri olur.

 Ayrıca, bir yönetici kullanıcı doğrudan kendisine atanmış bir koleksiyonda **Sil** veya **Değiştir** iznini kullanamaz. Ancak, bu izinleri Bu koleksiyonla sınırlı olan koleksiyonlar üzerinde kullanabilirler. Önceki örnekte, Yönetici Kullanıcı tüm Kuzey Amerika masaüstleri koleksiyonunu silebilir veya değiştirebilir, ancak tüm masaüstleri koleksiyonunu silemez veya değiştiremezler.  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Yeni yönetici kullanıcı oluştur

 Configuration Manager yönetmek üzere kişilere veya bir güvenlik grubu üyelerine erişim sağlamak için, Configuration Manager bir yönetici kullanıcı oluşturun ve kullanıcının veya Kullanıcı grubunun Windows hesabını belirtin. Configuration Manager içindeki her yönetici kullanıcıya en az bir güvenlik rolü ve bir güvenlik kapsamı atanması gerekir. Ayrıca yönetici kullanıcının yönetim kapsamını sınırlamak üzere koleksiyonlar da atayabilirsiniz.  

 Yeni yönetici kullanıcılar oluşturmak için aşağıdaki yordamları kullanın.  

### <a name="to-create-a-new-administrative-user"></a>Yeni yönetici kullanıcı oluşturmak için  

1. Configuration Manager konsolunda, **Yönetim**' i seçin.  
2. **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **Yönetim kullanıcıları**' nı seçin.  
3. **Giriş** sekmesinde, **Oluştur** grubunda, **Kullanıcı veya Grup Ekle**' yi seçin.  
4. **Araştır**' ı seçin ve ardından bu yeni yönetici kullanıcı için kullanılacak kullanıcı hesabını veya grubunu seçin.  

    > [!NOTE]  
    > Konsol tabanlı yönetim için, yalnızca etki alanı kullanıcıları veya güvenlik grupları yönetici kullanıcı olarak belirtilebilir.

5. **İlişkili güvenlik rolleri**Için, **Ekle** ' yi seçerek kullanılabilir güvenlik rollerinin bir listesini açın, bir veya daha fazla güvenlik rolü için kutuyu işaretleyin ve ardından **Tamam**' ı seçin.  

6. Yeni Kullanıcı için güvenli kılınabilir nesne davranışını tanımlamak üzere aşağıdaki iki seçenekten birini seçin:  

    - **Atanan güvenlik rolleriyle ilişkili nesnelerin tüm örnekleri**: Bu seçenek yönetici kullanıcıyı **Tüm** güvenlik kapsamıyla, tüm **sistemler** ve tüm **Kullanıcılar ve Kullanıcı grupları** koleksiyonları ile ilişkilendirir. Kullanıcıya atanan güvenlik rolleri nesnelere erişimi tanımlar. Bu yönetici kullanıcının oluşturduğu yeni nesneler **Varsayılan** güvenlik kapsamına atanır.  

    - **Yalnızca belirtilen güvenlik kapsamlarına ve koleksiyonlara atanmış nesne örnekleri**: varsayılan olarak, bu seçenek yönetici kullanıcıyı **varsayılan** güvenlik kapsamıyla, **Tüm sistemler** ve **tüm kullanıcılar ve Kullanıcı grupları** koleksiyonları ile ilişkilendirir. Bununla birlikte, gerçek güvenlik kapsamları ve koleksiyonlar, yeni yönetici kullanıcıyı oluşturmak için kullandığınız hesapla ilişkilendirilenlerle sınırlıdır. Bu seçenek güvenlik kapsamları ve koleksiyonları ekleyip kaldırarak, yönetici kullanıcının yönetim kapsamını özelleştirmeyi destekler.  

    > [!IMPORTANT]  
    > Yukarıdaki seçenekler, her atanan güvenlik kapsamını ve koleksiyonunu, yönetici kullanıcıya atanan her güvenlik rolüyle ilişkilendirir. Bireysel güvenlik rollerini belirli güvenlik kapsamları ve koleksiyonlarıyla ilişkilendirmek için, **belirli güvenlik kapsamları ve koleksiyonlarla atanan güvenlik rollerini ilişkilendirebilirsiniz**, üçüncü bir seçeneği kullanabilirsiniz. Bu üçüncü seçenek, yönetici kullanıcıyı değiştirirken, yeni yönetici kullanıcıyı oluşturduktan sonra kullanılabilir.  

7. 6. adımda yaptığınız seçime bağlı olarak, aşağıdaki eylemi gerçekleştirin:  

    - **Atanan güvenlik rolleriyle ilişkili nesnelerin tüm örneklerini**seçtiyseniz, bu yordamı gerçekleştirmek için **Tamam** ' ı seçin.  

    - **Yalnızca belirtilen güvenlik kapsamlarına ve koleksiyonlara atanmış nesne örneklerini**seçtiyseniz, ek koleksiyonlar ve güvenlik kapsamları seçmek için **Ekle** ' yi seçebilirsiniz. İsterseniz listeden bir veya daha fazla nesne seçin **ve Kaldır '** ı seçerek kaldırın. Bu yordamı gerçekleştirmek için **Tamam ' ı** seçin.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Yönetici kullanıcının yönetim kapsamını değiştirme

 Bir yönetici kullanıcının yönetim kapsamını, kullanıcıyla ilişkili güvenlik rolleri, güvenlik kapsamları ve koleksiyonlar ekleyip kaldırarak değiştirebilirsiniz. Her yönetici kullanıcı en az bir güvenlik rolü ve bir güvenlik kapsamı ile ilişkilendirilmelidir. Kullanıcının yönetim kapsamına bir veya daha fazla koleksiyon atamanız gerekebilir. Çoğu güvenlik rolü koleksiyonlarla etkileşim kurar ve atanmış bir koleksiyon olmadan düzgün çalışmaz.  

 Bir yönetici kullanıcıyı değiştirdiğinizde, güvenli kılınabilir nesnelerin atanan güvenlik rolleriyle nasıl ilişkilendirileceğiyle ilgili davranışı değiştirebilirsiniz. Seçebileceğiniz üç davranış aşağıdaki gibidir:  

- **Atanan güvenlik rolleriyle ilişkili nesnelerin tüm örnekleri**: Bu seçenek yönetici kullanıcıyı **Tüm** kapsamlarla, tüm **sistemler** ve **tüm kullanıcılar ve Kullanıcı grupları** koleksiyonları ile ilişkilendirir. Kullanıcıya atanan güvenlik rolleri nesnelere erişimi tanımlar.  

- **Yalnızca belirtilen güvenlik kapsamlarına ve koleksiyonlara atanmış nesne örnekleri**: Bu seçenek yönetici kullanıcıyı, yönetici kullanıcıyı yapılandırmak için kullandığınız hesapla ilişkili güvenlik kapsamları ve koleksiyonlarla ilişkilendirir. Bu seçenek güvenlik rolleri ve koleksiyonları ekleyip kaldırarak, yönetici kullanıcının yönetim kapsamını özelleştirmeyi destekler.  

- **Atanmış güvenlik rollerini belirli güvenlik kapsamları ve koleksiyonlarla ilişkilendirin**: Bu seçenek, bireysel güvenlik rolleri ile belirli güvenlik kapsamları ve kullanıcının koleksiyonları arasında belirli ilişkilendirmeler oluşturmanızı sağlar.  

    > [!NOTE]  
    > Bu seçenek yalnızca, bir yönetici kullanıcının özelliklerini değiştirdiğinizde kullanılabilir.  

Güvenli kılınabilir nesne davranışı için mevcut yapılandırma, ek güvenlik rolleri atamak için kullandığınız süreci değiştirir. Bir yönetici kullanıcıyı yönetmenize yardımcı olması için, güvenli kılınabilir nesnelerle ilgili olarak farklı seçeneklere dayalı olan aşağıdaki yordamları kullanın.  

Bir yönetici kullanıcının güvenli kılınabilir nesnelerinin yapılandırmasını görüntülemek ve yönetmek için aşağıdaki yordamı kullanın.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Bir yönetici kullanıcıyla ilgili güvenli kılınabilir nesne davranışını görüntülemek ve yönetmek için  

1. Configuration Manager konsolunda, **Yönetim**' i seçin.  
2. **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **Yönetim kullanıcıları**' nı seçin.  
3. Düzenlemek istediğiniz yönetici kullanıcıyı seçin.  
4. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  
5. Bu yönetici kullanıcıyla ilgili güvenli kılınabilir nesnelerin geçerli yapılandırmasını görüntülemek için **güvenlik kapsamları** sekmesini seçin.  
6. Güvenli kılınabilir nesne davranışını değiştirmek için, güvenli kılınabilir nesne davranışı için yeni bir seçeneği belirleyin. Bu yapılandırmayı değiştirdikten sonra, bu yönetici kullanıcı için güvenlik kapsamlarını ve koleksiyonları ve güvenlik rollerini yapılandırmaya yönelik daha fazla rehberlik için uygun yordama bakın.  
7. Yordamı gerçekleştirmek için **Tamam ' ı** seçin.  

Güvenli kılınabilir nesne davranışı **atanmış güvenlik rolleriyle ilişkili nesnelerin tüm örneklerine**ayarlanmış bir yönetici kullanıcıyı değiştirmek için aşağıdaki yordamı kullanın.  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Seçenek için: atanan güvenlik rolleriyle ilişkili nesnelerin tüm örnekleri  

1. Configuration Manager konsolunda, **Yönetim**' i seçin.  
2. **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **Yönetim kullanıcıları**' nı seçin.  
3. Düzenlemek istediğiniz yönetici kullanıcıyı seçin.  
4. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  
5. Yönetici kullanıcının **atanan güvenlik rolleriyle ilişkili nesnelerin tüm örnekleri**için yapılandırıldığını doğrulamak Için **güvenlik kapsamları** sekmesini seçin.  
6. Atanan güvenlik rollerini değiştirmek için **güvenlik rolleri** sekmesini seçin.  

    - Bu yönetici kullanıcıya ek güvenlik rolleri atamak için, **Ekle**' yi seçin, atamak istediğiniz her ek güvenlik rolünün onay kutusunu işaretleyin ve ardından **Tamam**' ı seçin.  
    - Güvenlik rollerini kaldırmak için listeden bir veya daha fazla güvenlik rolü seçin ve ardından **Kaldır**' ı seçin.

7. Güvenli kılınabilir nesne davranışını değiştirmek için **güvenlik kapsamları** sekmesini seçin ve güvenli kılınabilir nesne davranışı için yeni bir seçenek belirleyin. Bu yapılandırmayı değiştirdikten sonra, bu yönetici kullanıcı için güvenlik kapsamlarını ve koleksiyonları ve güvenlik rollerini yapılandırmaya yönelik daha fazla rehberlik için uygun yordama bakın.  

    > [!NOTE]  
    > Güvenli kılınabilir nesne davranışı, **atanan güvenlik rolleriyle ilişkili nesnelerin tüm örneklerine**ayarlandığında, belirli güvenlik kapsamlarını ve koleksiyonlarını ekleyemez veya kaldıramazsınız.  

8. Bu yordamı gerçekleştirmek için **Tamam ' ı** seçin.  

Güvenli kılınabilir nesne davranışı **yalnızca belirtilen güvenlik kapsamlarına ve koleksiyonlara atanmış nesne örneklerine**ayarlanmış bir yönetici kullanıcıyı değiştirmek için aşağıdaki yordamı kullanın.  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Seçenek: yalnızca belirtilen güvenlik kapsamlarına ve koleksiyonlara atanmış nesne örnekleri  

1. Configuration Manager konsolunda, **Yönetim**' i seçin.  
2. **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **Yönetim kullanıcıları**' nı seçin.  
3. Düzenlemek istediğiniz yönetici kullanıcıyı seçin.  
4. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  
5. Kullanıcının **yalnızca belirtilen güvenlik kapsamlarına ve koleksiyonlara atanmış nesne örnekleri**için yapılandırıldığını doğrulamak Için **güvenlik kapsamları** sekmesini seçin.  
6. Atanan güvenlik rollerini değiştirmek için **güvenlik rolleri** sekmesini seçin.  

    - Bu kullanıcıya ek güvenlik rolleri atamak için, **Ekle**' yi seçin, atamak istediğiniz her ek güvenlik rolünün onay kutusunu işaretleyin ve ardından **Tamam**' ı seçin.  
    - Güvenlik rollerini kaldırmak için listeden bir veya daha fazla güvenlik rolü seçin ve ardından **Kaldır**' ı seçin.  
7. Güvenlik rolleriyle ilişkili güvenlik kapsamlarını ve koleksiyonları değiştirmek için **güvenlik kapsamları** sekmesini seçin.  

    - Yeni güvenlik kapsamlarını veya koleksiyonları bu yönetici kullanıcıya atanan tüm güvenlik rolleriyle ilişkilendirmek için, **Ekle** ' yi seçin ve dört seçenekten birini belirleyin. **Güvenlik kapsamı** veya **koleksiyon**seçeneğini belirlerseniz, bu seçimi tamamlamaya yönelik bir veya daha fazla nesnenin kutusunu işaretleyin ve ardından **Tamam**' ı seçin.  
    - Bir güvenlik kapsamını veya koleksiyonu kaldırmak için, nesneyi seçin ve ardından **Kaldır**' ı seçin.

8. Bu yordamı gerçekleştirmek için **Tamam ' ı** seçin.  

**Atanmış güvenlik rollerini belirli güvenlik kapsamları ve koleksiyonlarla ilişkilendirmek**üzere, güvenli kılınabilir nesne davranışı ayarlanmış bir yönetici kullanıcıyı değiştirmek için aşağıdaki yordamı kullanın.  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Seçenek için: atanmış güvenlik rollerini belirli güvenlik kapsamları ve koleksiyonlarla Ilişkilendirin  

1. Configuration Manager konsolunda, **Yönetim**' i seçin.  
2. **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **Yönetim kullanıcıları**' nı seçin.  
3. Düzenlemek istediğiniz yönetici kullanıcıyı seçin.  
4. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  
5. Yönetici kullanıcının **belirli güvenlik kapsamları ve koleksiyonlarla atanmış güvenlik rollerini ilişkilendirmek**için yapılandırıldığını doğrulamak Için **güvenlik kapsamları** sekmesini seçin.  
6. Atanan güvenlik rollerini değiştirmek için **güvenlik rolleri** sekmesini seçin.  

    - Bu yönetici kullanıcıya ek güvenlik rolleri atamak için **Ekle**' yi seçin. **Güvenlik rolü Ekle** iletişim kutusunda, bir veya daha fazla kullanılabilir güvenlik rolü seçin, **Ekle**' yi seçin ve seçili güvenlik rolleriyle ilişkilendirilecek bir nesne türü seçin. **Güvenlik kapsamı** veya **koleksiyon**seçeneğini belirlerseniz, bu seçimi tamamlamaya yönelik bir veya daha fazla nesnenin kutusunu işaretleyin ve ardından **Tamam**' ı seçin.  

        > [!NOTE]  
        > Seçili güvenlik rollerinin yönetici kullanıcıya atanabilmesi için önce en az bir güvenlik kapsamı yapılandırmanız gerekir. Birden fazla güvenlik rolü seçtiğinizde, yapılandırdığınız her güvenlik kapsamı ve koleksiyon seçili güvenlik rollerinin her biriyle ilişkilendirilir.  

    - Güvenlik rollerini kaldırmak için listeden bir veya daha fazla güvenlik rolü seçin ve ardından **Kaldır**' ı seçin.  

7. Belirli bir güvenlik rolüyle ilişkilendirilen güvenlik kapsamlarını ve koleksiyonları değiştirmek için **güvenlik kapsamları** sekmesini seçin, güvenlik rolünü seçin ve ardından **Düzenle**' yi seçin.  

    - Yeni nesneleri bu güvenlik rolüyle ilişkilendirmek için, **Ekle**' yi seçin ve seçili güvenlik rolleriyle ilişkilendirilecek bir nesne türü seçin. **Güvenlik kapsamı** veya **koleksiyon**seçeneğini belirlerseniz, bu seçimi tamamlamaya yönelik bir veya daha fazla nesnenin kutusunu işaretleyin ve ardından **Tamam**' ı seçin.  

        > [!NOTE]  
        > En az bir güvenlik kapsamı yapılandırmanız gerekir.  

    - Bu güvenlik rolüyle ilişkilendirilmiş bir güvenlik kapsamını veya koleksiyonu kaldırmak için, nesneyi seçin ve ardından **Kaldır**' ı seçin.  

    - İlişkili nesneleri değiştirmeyi bitirdiğinizde **Tamam**' ı seçin.  

8. Bu yordamı gerçekleştirmek için **Tamam ' ı** seçin.  

    > [!CAUTION]  
    > Bir güvenlik rolü yönetici kullanıcılara koleksiyon dağıtım izni veriyorsa, güvenlik kapsamı farklı bir güvenlik rolüyle ilişkilendirilmiş olsa bile, bu yönetici kullanıcılar nesne **okuma** izinlerine sahip oldukları herhangi bir güvenlik kapsamından nesne dağıtabilirler.  

## <a name="next-steps"></a>Sonraki adımlar

[Configuration Manager kullanılan hesaplar](../../../plan-design/hierarchy/accounts.md)
