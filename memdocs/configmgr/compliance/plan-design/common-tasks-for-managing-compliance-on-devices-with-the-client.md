---
title: Ortak Uyumluluk yönetimi görevleri
titleSuffix: Configuration Manager
description: Bazı yaygın senaryolar üzerinden çalışarak uyumluluk ayarları Configuration Manager hakkında bilgi edinin.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 5920229331bca8d2a47b0bf1ab663530ef63c51e
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240669"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Configuration Manager istemcisiyle cihazlarda uyumluluğu yönetmeye yönelik ortak görevler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, içinde karşılaşabileceğiniz bazı yaygın senaryolarda size rehberlik ederek Configuration Manager uyumluluk ayarlarını kullanmaya yönelik bir giriş sunulmaktadır.  

 Uyumluluk ayarlarını zaten biliyorsanız, [Configuration Manager istemcisiyle yönetilen cihazlar Için yapılandırma öğelerinde](../../compliance/deploy-use/create-configuration-items.md)kullandığınız tüm özelliklerle ilgili ayrıntılı bilgileri bulabilirsiniz.  

 Başlamadan önce uyumluluk ayarları hakkında bazı temel bilgileri öğrenmek için [Uyumluluk ayarlarına](../../compliance/get-started/get-started-with-compliance-settings.md) başlayın makalesini okuyun. Gerekli Önkoşullar hakkında bilgi edinmek için [planı okuyun ve uyumluluk ayarlarını yapılandırın](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) .  

## <a name="general-information-for-each-scenario"></a>Her senaryo için genel bilgiler  
 Her senaryoda belirli bir görevi gerçekleştiren bir yapılandırma öğesi oluşturacaksınız. Yapılandırma öğesi oluşturma Sihirbazı 'Nı açmak ve kullanmaya başlamak için şu adımları uygulayın:  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk**  >  **Uyumluluk ayarları**  >  **yapılandırma öğeleri**' ni seçin.  

1.  **Giriş** sekmesinde, **Oluştur** grubunda, **yapılandırma öğesi oluştur**' u seçin.  

1.  Yapılandırma öğesi oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki ekran görüntüsünde gösterildiği gibi, yapılandırma öğesi için bir ad ve açıklama belirtin. Ardından, bu makaledeki her senaryo için uygun yapılandırma öğesi türünü seçin.  

     ![Yapılandırma öğesi oluşturma Sihirbazı ' nın genel sayfası](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Senaryo: Windows 10 cihazlarda Bluetooth 'U devre dışı bırakma

 Bu senaryoda, güvenlik departmanınız cihazlarda Bluetooth özelliğinin Şirket dışında hassas şirket bilgilerini iletmek için kullanılabileceğini belirlemiştir. Yakın zamanda tüm bilgisayarlarınızı Windows 10 ' a yükselttiniz. Bu cihazlarda Bluetooth 'un devre dışı bırakılacağını belirleyin.  

1. Yapılandırma öğesi oluşturma Sihirbazı ' nın **genel** sayfasında **Windows 10** yapılandırma öğesi türünü seçin ve ardından **İleri**' yi seçin.  

2. Sihirbazın **Desteklenen Platformlar** sayfasında tüm Windows 10 platformlarını seçin.  

3. **Cihaz ayarları** sayfasında **cihaz**' ı seçin ve ardından **İleri**' yi seçin.  

4. **Cihaz** sayfasında **Bluetooth** değeri olarak **Yasaklanmış**öğesini seçin.  

5. **Uyumlu olmayan ayarları düzelt** öğesini seçerek değişikliğin tüm Windows 10 cihazlarına uygulandığından emin olun.  

6. Yapılandırma öğesini oluşturmak için sihirbazı tamamlayın.  

 Artık, oluşturduğunuz yapılandırmayı cihazlara dağıtmanıza yardımcı olması için [Configuration Manager makaleyle yapılandırma temelleri oluşturup dağıtmak Için ortak görevlerdeki](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) bilgileri kullanabilirsiniz.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Senaryo: Windows masaüstü bilgisayarlarında yanlış bir kayıt defteri değerini düzeltme

> [!NOTE] 
> Configuration Manager istemcisini çalıştıran Mac bilgisayarlarda uyumluluğu değerlendirmek için iki seçeneğiniz vardır:  
> - Mac OS X tercihler (plist) dosyasını değerlendirin.
> - Özel bir komut dosyası kullanın ve komut dosyası tarafından döndürülen sonuçları değerlendirin.  
>
>Daha fazla bilgi için bkz. [Configuration Manager istemcisiyle yönetilen Mac OS X cihazları için yapılandırma öğeleri oluşturma](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 Bu senaryoda, önemli bir iş kolu uygulamasının yönettiğiniz bazı Windows 8.1 bilgisayarlarda düzgün çalışmadığını fark edersiniz. Bunun nedeni, **HKEY_LOCAL_MACHINE \SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** adlı bir kayıt defteri anahtarının bazı bilgisayarlarda **0** değerine ayarlandığını belirlersiniz. İş kolu uygulamasının başarıyla çalışması için bu değerin **1**olarak ayarlanması gerekir.  

 Bu yordamda, bulunan yanlış kayıt defteri anahtarı değerlerini izleyen ve otomatik olarak düzelten bir yapılandırma öğesi oluşturacaksınız.  

1. Yapılandırma öğesi oluşturma Sihirbazı ' nın **genel** sayfasında **Windows masaüstleri ve sunucular (özel)** yapılandırma öğesi türünü seçin ve ardından **İleri**' yi seçin.  

2. Sihirbazın **Desteklenen platformlar** sayfasında **Windows 8.1** ' yi seçin (yapılandırma öğesinin yalnızca etkilenen bilgisayarlara uygulandığından emin olmak için).  

3. **Ayarlar** sayfasında **Yeni** ' yi seçerek yeni bir ayar oluşturun.  

4. **Ayar oluştur** Iletişim kutusunun **genel** sekmesinde şu ayarları yapılandırın:  

   -   **Ad**  >  **Örnek ayar**  

   -   **Ayar türü**  >  **Kayıt defteri değeri**  

   -   **Veri türü**  >  **Tamsayı** (değer yalnızca bir sayı içerdiği için)  

   -   **Hive**  >  **HKEY_LOCAL_MACHINE**  

   -   **Anahtar**  >  **Software\woodgrove\lob App\Configuration\Configuration1**  

   -   **Değer**  >  **1** (gerekli değer)  

5. **Ayar oluştur** Iletişim kutusunun **Uyumluluk kuralları** sekmesinde **Yeni**' yi seçin. **Kural oluştur** iletişim kutusunda şu ayarları yapılandırın:  

   -   **Ad**  >  **Örnek kural**  

   -   **Seçili ayar > seçili** ayarın **örnek ayar**olduğunu doğrulayın.

   -   **Kural türü**  >  **Değer**  

   -   Ayar, ayar adının doğru olduğundan emin olmak için **aşağıdaki kurala uymalıdır** > ve ayar değerinin **1**' e eşit olması gerektiğini belirtmek için seçeneğini yapılandırın.  

   -   **Desteklendiğinde uyumsuz kuralları düzelt** >, Configuration Manager kayıt defteri anahtarı değerini doğru değere sıfırlamasını sağlamak için bu onay kutusunu işaretleyin.  

6. Yapılandırma öğesini oluşturmak için sihirbazı tamamlayın.  

 Artık, oluşturduğunuz yapılandırmayı cihazlara dağıtmanıza yardımcı olması için [yapılandırma temelleri oluşturmak ve dağıtmak üzere ortak görevlerdeki](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) bilgileri kullanabilirsiniz.  

## <a name="next-steps"></a>Sonraki adımlar

[Yapılandırma taban çizgilerini oluşturma ve dağıtma](common-tasks-for-creating-and-deploying-configuration-baselines.md)
