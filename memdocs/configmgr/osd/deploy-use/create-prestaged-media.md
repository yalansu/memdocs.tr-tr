---
title: Önceden hazırlanan ortam oluşturma
titleSuffix: Configuration Manager
description: Çeşitli senaryolarda Windows dağıtımını basitleştirmek için Configuration Manager önceden hazırlanan medyayı kullanın.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d5219b518d46ccca174c7aa3fef62fe3334def35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711115"
---
# <a name="create-prestaged-media"></a>Önceden hazırlanan ortam oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager 'de önceden hazırlanan medya, bir Windows Image (WıM) dosyasıdır. Üretici tarafından veya hazırlama merkezinizde üretim Configuration Manager ortamına bağlı olmayan çıplak bir bilgisayara yüklenebilir. Önceden hazırlanan medya, hedef bilgisayarı başlatmak için kullanılan önyükleme görüntüsünü ve hedef bilgisayara uygulanan işletim sistemi görüntüsünü içerir. Önceden hazırlanan medyaya dahil edilecek uygulamaları, paketleri ve sürücü paketlerini de belirtebilirsiniz. İşletim sistemini dağıtan görev dizisi medyaya dahil değildir. Önceden hazırlanmış medya, yeni bir bilgisayar son kullanıcıya gönderilmeden önce o bilgisayarın sabit sürücüsüne uygulanır.

Aşağıdaki işletim sistemi dağıtım senaryoları için önceden hazırlanmış medya kullanın:  

- [Fabrikada veya yerel depoda OEM için görüntü oluşturma](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)  

- [Windows to Go dağıtımı](deploy-windows-to-go.md)  


## <a name="usage"></a>Kullanım

Önceden hazırlanan medyayı uyguladıktan sonra bilgisayar ilk kez başlatıldığında, bilgisayar Windows PE 'de başlatılır. İşletim sistemi dağıtım işlemini tamamlayan görev dizisini bulmak için bir yönetim noktasına bağlanır. Önceden hazırlanan medya kullanan bir görev dizisini dağıttığınızda istemci, ilk olarak geçerli içerik için yerel görev sırası önbelleğini denetler. İçerik bulunamazsa veya yeniden değiştirilmişse, istemci içeriği bir dağıtım noktasından veya eşinden indirir.  


## <a name="prerequisites"></a>Önkoşullar

Görev sırası medyası oluşturma Sihirbazı 'Nı kullanarak önceden hazırlanmış medya oluşturmadan önce tüm koşulların karşılandığından emin olun.

### <a name="boot-image"></a>Önyükleme görüntüsü

İşletim sistemini dağıtmak için görev dizisinde kullandığınız önyükleme görüntüsü hakkında aşağıdaki noktaları göz önünde bulundurun:

- Önyükleme görüntüsünün mimarisi hedef bilgisayarın mimarisine uygun olmalıdır. Örneğin, bir x64 hedef bilgisayar, x86 veya x64 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. Ancak, bir x86 hedef bilgisayar yalnızca x86 önyükleme görüntüsünü başlatabilir ve çalıştırabilir.
- Önyükleme görüntüsünün, hedef bilgisayarı sağlamak için gereken ağ ve depolama sürücülerini içerdiğinden emin olun.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>İşletim sistemini dağıtmak için görev dizisi oluşturma

Önceden hazırlanmış medyanın bir parçası olarak işletim sistemini dağıtmak için görev dizisini belirtin. Daha fazla bilgi için bkz. bir [işletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Görev dizisiyle ilişkili tüm içeriği dağıtma

Görev dizisinin gerektirdiği tüm içeriği en az bir dağıtım noktasına dağıtın. Bu içerik önyükleme görüntüsünü, işletim sistemi görüntüsünü ve diğer ilişkili dosyaları içerir. Sihirbaz, ön hazırlığı yapılmış medyayı oluşturduğunda dağıtım noktasından içeriği toplar.

Kullanıcı hesabınızın, bu dağıtım noktasındaki içerik kitaplığı için en azından **okuma** erişimi hakları olması gerekir. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Hedef bilgisayardaki sabit sürücü

Önceden hazırlanan medya uygulanmadan önce hedef bilgisayarın sabit sürücüsü biçimlendirilmelidir. Medya uygulandığında sabit sürücü biçimlendirilmemişse, işletim sistemini dağıtan görev sırası hedef bilgisayarı başlatmayı denediğinde başarısız olur.

> [!NOTE]  
> Görev sırası medyası oluşturma Sihirbazı medyada şu görev dizisi değişkeni koşulunu ayarlar: **_SMSTSMediaType = OEMMedia**. Görev dizinizdeki bu koşulu kullanabilirsiniz.  


## <a name="process"></a>İşleme

 > [!NOTE]  
 > PKI ortamları için, kök CA birincil sitede belirtildiğinden, önceden hazırlanan medyanın birincil sitede oluşturulduğundan emin olun. CAS sitesi, önceden hazırlanan medyayı düzgün şekilde oluşturmak için kök CA bilgilerine sahip değildir.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası medyası oluştur**' u seçin. Bu eylem, görev sırası medyası oluşturma Sihirbazı 'Nı başlatır.  

3. **Medya türü seçin** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Önhazırlığı yapılan medya**'yı seçin.  

    - İsteğe bağlı olarak, yalnızca IŞLETIM sisteminin kullanıcı girişi gerektirmeden dağıtılmasını istiyorsanız **Katılımsız işletim sistemi dağıtımına Izin ver**' i seçin.  

        > [!IMPORTANT]  
        > Bu seçeneği belirlediğinizde, kullanıcıya ağ yapılandırma bilgileri veya isteğe bağlı görev dizileri sorulmaz. Medyayı parola koruması için yapılandırırsanız, kullanıcıdan bir parola istenir.  

4. **Medya yönetimi** sayfasında, aşağıdaki seçeneklerden birini belirtin:  

    - **Dinamik medya**: bir yönetim noktasının, medyayı site sınırlarındaki istemci konumuna bağlı olarak başka bir yönetim noktasına yönlendirmesine izin verin.  

    - **Site tabanlı medya**: medya yalnızca belirtilen yönetim noktasıyla iletişim kurar.  

5. **Medya özellikleri** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Oluşturan**: Medyayı oluşturan kişiyi belirtin.  

    - **Sürüm**: Medyanın sürüm numarasını belirtin.  

    - **Açıklama**: Medyanın hangi amaçla kullanıldığına ilişkin benzersiz bir açıklama belirtin.  

    - **Medya dosyası**: Çıkış dosyalarının adını ve yolunu belirtin. Sihirbaz çıkış dosyalarını bu konuma yazar. Örneğin, `\\servername\folder\outputfile.wim`  

    - **Hazırlama klasörü**<!--1359388-->: Medya oluşturma işlemi çok sayıda geçici sürücü alanı gerektirebilir. Varsayılan olarak, bu konum şu yola benzer: `%UserProfile%\AppData\Local\Temp`. Sürüm 1902 ' den başlayarak, bu geçici dosyaları nerede depolayabileceğiniz konusunda daha fazla esneklik sağlamak için bu değeri başka bir sürücü ve yol olarak değiştirin.  

6. **Güvenlik** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Bilinmeyen bilgisayar desteğini etkinleştir**: medyanın, Configuration Manager tarafından yönetilmeyen bir bilgisayara işletim sistemi dağıtmasına izin verin. Configuration Manager veritabanında bu bilgisayarların kaydı yoktur. Daha fazla bilgi için bkz. [bilinmeyen bilgisayar dağıtımları Için hazırlanma](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Medyayı parolayla koru**: medyanın yetkisiz erişimlerden korunmasına yardımcı olmak için güçlü bir parola girin. Parola belirtirseniz kullanıcının önhazırlığı yapılan medyayı kullanabilmesi için o parolayı girmesi gerekir.  

        > [!IMPORTANT]  
        > En iyi güvenlik uygulaması olarak, önhazırlığı yapılan medyayı korumaya yardımcı olmak için her zaman parola atayın.  
 
    - HTTP iletişimleri için, **otomatik olarak imzalanan medya sertifikası oluştur**' u seçin. Ardından, sertifika için başlangıç ve sona erme tarihi belirtin.  
    
        > [!NOTE] 
        > Bu seçeneği belirlerseniz, HTTPS yönetim noktaları bu sihirbazın **önyükleme görüntüsü** sayfasında seçilebilir olarak kullanılamaz.

    - HTTPS iletişimleri için, **PKI sertifikasını Içeri aktar**' ı seçin. Ardından İçeri aktarılacak sertifikayı ve parolasını belirtin.  

        Önyükleme görüntülerinin kullandığı bu istemci sertifikası hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Kullanıcı cihaz benzeşimi**: Configuration Manager Kullanıcı merkezli yönetimi desteklemek için, medyanın kullanıcıları hedef bilgisayarla nasıl ilişkilendirmesini istediğinizi belirtin. İşletim sistemi dağıtımının Kullanıcı cihaz benzeşimini nasıl desteklediği hakkında daha fazla bilgi için bkz. [kullanıcıları bir hedef bilgisayarla ilişkilendirme](../get-started/associate-users-with-a-destination-computer.md).  

        - **Kullanıcı cihaz benzeşimine otomatik onay Ile Izin ver**: medya kullanıcıları hedef bilgisayarla otomatik olarak ilişkilendirir. Bu işlev, işletim sistemini dağıtan görev sırasının eylemlerine bağlıdır. Bu senaryoda görev sırası, işletim sistemini hedef bilgisayara dağıtırken belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur.  

        - **Kullanıcı cihaz benzeşimi bekleyen yönetici onayına Izin ver**: medya, onay verildikten sonra kullanıcıları hedef bilgisayarla ilişkilendirir. Bu işlev, işletim sistemini dağıtan görev dizisinin kapsamını temel alır. Bu senaryoda görev dizisi, belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur, ancak işletim sistemi dağıtılmadan önce yönetici kullanıcıdan onay bekler.  

        - **Kullanıcı cihaz benzeşimine izin verme**: medya, kullanıcıları hedef bilgisayarla ilişkilendirmez. Bu senaryoda, görev sırası, işletim sistemini dağıtırken kullanıcıları hedef bilgisayarla ilişkilendirmez.  

7. **Görev dizisi** sayfasında, hedef bilgisayarda çalışan görev sırasını seçin. Görev sırası tarafından başvurulan içerik listesini doğrulayın.  

    - **İlişkili uygulama bağımlılıklarını Algıla ve bu medyaya Ekle**: Ayrıca, uygulama bağımlılıkları için medyaya içerik ekleyin.  

        > [!TIP]  
        > Beklenen uygulama bağımlılıklarını görmüyorsanız Listeyi yenilemek için bu seçeneği kaldırın ve yeniden seçin.  

8. **Önyükleme görüntüsü** sayfasında, aşağıdaki seçenekleri belirtin:  

    > [!IMPORTANT]  
    > Dağıttığınız önyükleme görüntüsünün mimarisi hedef bilgisayarın mimarisine uygun olmalıdır. Örneğin, bir x64 hedef bilgisayar, x86 veya x64 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. Ancak, bir x86 hedef bilgisayar yalnızca x86 önyükleme görüntüsünü başlatabilir ve çalıştırabilir.  

    - **Önyükleme görüntüsü**: hedef bilgisayarı başlatmak için önyükleme görüntüsünü seçin.  

    - **Dağıtım noktası**: önyükleme görüntüsüne sahip olan dağıtım noktasını seçin. Sihirbaz önyükleme görüntüsünü dağıtım noktasından alır ve medyaya yazar.  

        > [!NOTE]  
        > Kullanıcı hesabınız, dağıtım noktasındaki içerik kitaplığı için en azından **okuma** izinlerine sahip olmalıdır.  

    - **Yönetim noktası**: yalnızca *Site tabanlı medya*için birincil siteden bir yönetim noktası seçin.  

    - **İlişkili yönetim noktaları**: yalnızca *dinamik medya*için, kullanılacak birincil site yönetim noktalarını ve ilk iletişim için öncelik sırasını seçin.  

        > [!NOTE]  
        > HTTPS etkin yönetim noktaları, yalnızca bu sihirbazın **güvenlik** SAYFASıNDA bir PKI sertifikası belirtildiğinde görüntülenir.  

9. **Görüntüler** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Görüntü paketi**: kullanılacak işletim sistemi görüntüsünü belirtin. Daha fazla bilgi için bkz. [OS görüntülerini yönetme](../get-started/manage-operating-system-images.md).  

    - **Görüntü dizini**: paket birden çok işletim sistemi görüntüsü içeriyorsa, dağıtılacak görüntünün dizinini belirtin.  

    - **Dağıtım noktası**: işletim sistemi görüntü paketinin bulunduğu dağıtım noktasını belirtin. Sihirbaz, işletim sistemi görüntüsünü dağıtım noktasından alır ve medyaya yazar.  

10. **Uygulama Seç** sayfasında, önceden hazırlanan medya dosyasına eklemek için ek uygulamalar ' ı seçin.  

11. **Paket Seç** sayfasında, önceden hazırlanan medya dosyasına eklenecek ek paketler ' i seçin.  

12. **Sürücü paketini Seç** sayfasında, önceden hazırlanan medya dosyasına eklemek için ek sürücü paketleri ' ni seçin.  

13. **Dağıtım noktaları** sayfasında, içeriğin alınacağı bir veya daha fazla dağıtım noktası seçin.  

    Configuration Manager yalnızca içeriği olan dağıtım noktalarını görüntüler. Devam etmeden önce görev dizisiyle ilişkili tüm içeriği en az bir dağıtım noktasına dağıtın. İçeriği dağıttıktan sonra dağıtım noktası listesini yenileyin. Bu sayfada zaten seçtiğiniz dağıtım noktalarını kaldırın, önceki sayfaya gidin ve **dağıtım noktaları** sayfasına dönün. Alternatif olarak, Sihirbazı yeniden başlatın. Daha fazla bilgi için bkz. [bir görev dizisi tarafından başvurulan Içeriği dağıtma](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) ve [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

14. **Özelleştirme** sayfasında, aşağıdaki seçenekleri belirtin:  

    - Görev dizisinin kullandığı tüm değişkenleri ekleyin.  

    - **Başlatma öncesi komutunu etkinleştir**: görev dizisi çalışmadan önce çalıştırmak istediğiniz başlatma öncesi komutlarını belirtin. Başlatma öncesi komutlar, görev dizisi çalıştırılmadan önce Windows PE 'de kullanıcıyla etkileşime girebilen bir betik veya yürütülebilir dosyadır. Daha fazla bilgi için bkz. [görev dizisi medyası Için başlatma öncesi komutları](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Medya oluşturma sırasında, görev sırası değişkenlerinin değeri de dahil olmak üzere paket KIMLIĞINI ve başlatma öncesi komut satırını, Configuration Manager konsolunu çalıştıran bilgisayardaki **CreateTsMedia. log** dosyasına yazar. Görev dizisi değişkenlerinin değerini doğrulamak için bu günlük dosyasını inceleyebilirsiniz.  

        Başlatma öncesi komutu herhangi bir içerik gerektiriyorsa, **başlatma öncesi komutu için dosya ekleme**seçeneğini belirleyin.  

15. Sihirbazı tamamlayın.  


## <a name="next-steps"></a>Sonraki adımlar

[Fabrikada veya yerel depoda OEM için görüntü oluşturma](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
