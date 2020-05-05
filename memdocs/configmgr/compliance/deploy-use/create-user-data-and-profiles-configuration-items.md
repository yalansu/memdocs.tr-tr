---
title: Kullanıcı verileri ve profilleri yapılandırma öğeleri oluşturma
titleSuffix: Configuration Manager
description: Klasör yeniden yönlendirme, çevrimdışı dosyalar ve dolaşım profillerini yönetmek için Configuration Manager içindeki veri ve profil yapılandırma öğelerini kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2a99384772895ff2675ade671076163b74cecee2
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075311"
---
# <a name="create-user-data-and-profiles-configuration-items-in-configuration-manager"></a>Configuration Manager 'da Kullanıcı verileri ve profilleri yapılandırma öğeleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager içindeki kullanıcı verileri ve profilleri yapılandırma öğeleri, hiyerarşinizdeki kullanıcılar için Windows 8 ve üzeri sürümleri çalıştıran bilgisayarlarda klasör yeniden yönlendirmeyi, çevrimdışı dosyaları ve dolaşım profillerini yönetebilen ayarları içerir. Örneğin, şunları yapabilirsiniz:  

- Bir kullanıcının Belgeler klasörünü bir ağ paylaşımında yeniden yönlendirin.  

- Ağ bağlantısı kullanılamadığında, ağda depolanan belirtilen dosyaların bir kullanıcının bilgisayarında kullanılabilir olduğundan emin olun.  

- Kullanıcı oturum açtığında ve kapattığında bir ağ paylaşımıyla bir kullanıcının gezici profilindeki hangi dosyaların eşitlendiğini yapılandırın.  

  Configuration Manager diğer yapılandırma öğelerinin aksine, daha sonra dağıttığınız bir yapılandırma temeline Kullanıcı verileri ve profil yapılandırma öğeleri eklemeyin. Bunun yerine, yapılandırma öğesini doğrudan **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesini Dağıtma** iletişim kutusunu kullanarak dağıtırsınız.  

> [!IMPORTANT]  
>  Kullanıcı verileri ve profilleri yapılandırma öğelerini yalnızca kullanıcı koleksiyonlarına dağıtabilirsiniz.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Uyumluluk ayarları için kullanıcı verileri ve profillerini etkinleştirme  
 Kullanıcı verileri ve profilleri uyumluluk ayarları için hiyerarşinizdeki tüm bilgisayarlara uygulanacak varsayılan istemci ayarını yapılandırmak üzere aşağıdaki yordamı kullanın. Bu ayarın yalnızca bazı bilgisayarlara uygulanmasını istiyorsanız özel bir cihaz istemci ayarı oluşturun ve kullanıcı verileri ve profilleri uyumluluk ayarlarını kullanmak istediğiniz bilgisayarları içeren bir koleksiyona atayın. Özel cihaz ayarları oluşturma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).  

1.  Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan ayarlar**' a tıklayın.  

4.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

5.  **Varsayılan Ayarlar** iletişim kutusunda **Uyumluluk Ayarları**’na tıklayın.  

6.  **Kullanıcı Verilerini ve Profillerini Etkinleştir** açılır listesinden **Evet**’i seçin.  

7.  **Varsayılan Ayarlar** iletişim kutusunu kapatmak için **Tamam** 'a tıklayın.  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Kullanıcı verileri ve profilleri yapılandırma öğesi oluşturma  

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **uyumluluğu ayarları** > **Kullanıcı verileri ve profiller**' e tıklayın.  

2. **Giriş** sekmesindeki **Oluştur** grubundaki **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesi Oluştur**'a tıklayın.  

3. **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesi Oluşturma Sihirbazı** ’nın **Genel**sayfasında aşağıdaki bilgileri belirtin:  

   -   **Ad:** Yapılandırma öğesi için benzersiz bir ad girin. En fazla 256 karakter kullanabilirsiniz.  

   -   **Açıklama:** Yapılandırma öğesine genel bakış sağlayan bir açıklama ve Configuration Manager konsolunda tanımlanmasına yardımcı olan diğer ilgili bilgileri sağlar. En fazla 256 karakter kullanabilirsiniz.  

   -   **Klasör yeniden yönlendirme:** Bu yapılandırma öğesi için klasör yeniden yönlendirmesine yönelik ayarları yapılandırmak istiyorsanız bu kutuyu işaretleyin.  

   -   **Çevrimdışı dosyalar:** Bu yapılandırma öğesi için çevrimdışı dosya ayarlarını yapılandırmak istiyorsanız bu kutuyu işaretleyin.  

   -   **Gezici kullanıcı profilleri:** Bu yapılandırma öğesi için gezici kullanıcı profilleri ayarlarını yapılandırmak istiyorsanız bu kutuyu işaretleyin.  

4. **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesi Oluşturma Sihirbazı** ’nın **Klasör Yeniden Yönlendirme**sayfasında, bu yapılandırma öğesini alan kullanıcıların istemci bilgisayarlarının klasör yeniden yönlendirmeyi nasıl yönetmesini istediğinizi belirtin. Kullanıcının oturum açtığı herhangi bir cihaz için veya yalnızca kullanıcının birincil cihazları için ayarları yapılandırabilirsiniz. Klasör yeniden yönlendirme hakkında daha fazla bilgi için Windows Server belgelerinize bakın.  

   > [!NOTE]  
   >  Bu sayfa yalnızca sihirbazın **genel** sayfasındaki **klasör yeniden yönlendirme** 'yi işaretliyse görüntülenir.  

5. **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesi Oluşturma Sihirbazı** ’nın **Çevrimdışı Dosyalar**sayfasında bu yapılandırma öğesini alan kullanıcılar için çevrimdışı dosyaların kullanımını etkinleştirebilir veya devre dışı bırakabilir ve çevrimdışı dosyaların davranışına ilişkin ayarları yapılandırabilirsiniz. Ayrıca, kullanıcının oturum açtığı herhangi bir bilgisayarda her zaman kullanılabilir olacak çevrimdışı dosyaları belirtebilirsiniz. Çevrimdışı dosyalar hakkında daha fazla bilgi için Windows Server belgelerinize bakın.  

   > [!NOTE]  
   >  Bu sayfa yalnızca sihirbazın **genel** sayfasındaki **çevrimdışı dosyalar** kutusunu işaretliyse görüntülenir.  

6. **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesi Sihirbazı** ’nın **Gezici Profiller**sayfasında, gezici profillerin kullanıcının oturum açtığı bilgisayarlarda kullanılabilir olup olmadığını ve ayrıca bu profillerin nasıl davrandığına ilişkin diğer bilgileri yapılandırabilirsiniz. Gezici profiller hakkında daha fazla bilgi için Windows Server belgelerinize bakın.  

   > [!NOTE]  
   >  Bu sayfa yalnızca sihirbazın **genel** sayfasındaki **Gezici Kullanıcı profilleri** kutusunu işaretliyse görüntülenir.  

7. Sihirbazı tamamlayın.  

   Yeni kullanıcı verileri ve profilleri yapılandırma öğesi **Varlıklar ve Uyumluluk** çalışma alanının **Kullanıcı Verileri ve Profilleri** düğümünde gösterilir.  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Kullanıcı verileri ve profilleri yapılandırma öğesi dağıtma  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **uyumluluğu ayarları** > **Kullanıcı verileri ve profiller**' e tıklayın.  

3.  Dağıtmak istediğiniz kullanıcı verileri ve profilleri yapılandırma öğesini seçtikten sonra **Giriş** sekmesindeki **Dağıtım** grubunda **Dağıt**'a tıklayın.  

4.  **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesi Dağıtma** iletişim kutusunda aşağıdaki bilgileri belirtin.  

    -   **Koleksiyon** - Yapılandırma öğesini dağıtmak istediğiniz kullanıcı koleksiyonunu seçmek için **Gözat** 'a tıklayın.  

        > [!IMPORTANT]  
        >  Kullanıcı verileri ve profilleri yapılandırma öğelerini yalnızca kullanıcı koleksiyonlarına dağıtabilirsiniz.  

    -   **Desteklendiğinde uyumsuz kuralları düzelt** – İstemci bilgisayarlarda uyumsuz olarak değerlendirilen kuralları otomatik olarak düzeltmek için bu seçeneği etkinleştirin.  

    -   **Bakım süresi dışında düzeltmeye izin ver** – Yapılandırma öğesini dağıtmakta olduğunuz koleksiyon için bir bakım penceresi yapılandırıldıysa, uyumluluk ayarlarının bakım penceresi dışındaki değeri düzeltmesine izin vermek üzere bu seçeneği etkinleştirin. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Uyarı oluştur** - Yapılandırma öğesi uyumu, belirtilen tarih ve saate göre belirtilen yüzdeden küçük olduğunda bir uyarı oluşturulmasını yapılandırmak için bu seçeneği etkinleştirin. System Center Operations Manager'a bir uyarının ne zaman gönderilmesini istediğinizi de belirtebilirsiniz.  

    -   **Bu yapılandırma öğesine ait yapılandırma değerlendirme zamanlamasını belirtin** - Dağıtılan yapılandırma öğesinin istemci bilgisayarlarda değerlendirildiği zamanlamayı belirtin. Bu, basit veya özel zamanlama olabilir.  

5.  **Tamam** 'a tıklayarak **Kullanıcı Verileri ve Profilleri Yapılandırma Öğesini Dağıt** iletişim kutusunu kapatın ve dağıtımı oluşturun.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Kullanıcı verileri ve profilleri yapılandırma öğesini izleme  
 Bu tür bir yapılandırma öğesini diğer uyumluluk ayarlarını izlediğiniz şekilde izlersiniz.  

 Daha fazla bilgi için bkz. [Uyumluluk ayarlarını izleme](../../compliance/deploy-use/monitor-compliance-settings.md).  
