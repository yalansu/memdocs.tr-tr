---
title: Microsoft yönetilen giriş ekranı uygulamasını yapılandırma
titleSuffix: Microsoft Intune
description: Microsoft yönetilen giriş ekranı uygulamasını yapılandırma hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 865c7f03-f525-4dfa-b3a8-d088a9106502
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0279a85d0eb3bac7d222c27ce15203f58fd4ede6
ms.sourcegitcommit: ded11a8b999450f4939dcfc3d1c1adbc35c42168
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89281175"
---
# <a name="configure-the-microsoft-managed-home-screen-app-for-android-enterprise"></a>Android Enterprise için Microsoft tarafından yönetilen giriş ekranı uygulamasını yapılandırma

Yönetilen giriş ekranı, Intune ile kaydedilen ve çok uygulama bilgi noktası modunda çalışan şirkete ait Android kurumsal adanmış cihazlar için kullanılan uygulamadır. Bu cihazlar için, yönetilen giriş ekranı, diğer onaylanan uygulamaların en üstünde çalışacağı başlatıcı olarak davranır. Yönetilen giriş ekranı, BT yöneticilerine cihazlarını özelleştirme ve son kullanıcının erişebileceği özellikleri kısıtlama yeteneği sağlar. 

## <a name="when-to-configure-the-microsoft-managed-home-screen-app"></a>Microsoft tarafından yönetilen giriş ekranı uygulamasının ne zaman yapılandırılacağı

Genellikle, ayarlar cihaz yapılandırması aracılığıyla sizin için kullanılabilir ise, ayarları burada yapılandırın. Bunun yapılması zamandan tasarruf eder, hataları en aza indirir ve size daha iyi bir Intune destek deneyimi sağlar. Ancak, yönetilen giriş ekranı ayarlarından bazıları şu anda yalnızca Intune konsolundaki **uygulama yapılandırma ilkeleri** bölmesi aracılığıyla kullanılabilir. Yapılandırma tasarımcısını veya bir JSON betiği kullanarak farklı ayarların nasıl yapılandırılacağını öğrenmek için bu belgeyi kullanın. 

> [!NOTE]
> **Uygulama** ve **cihaz yapılandırması**aracılığıyla, izin verilen uygulamaları ve sabitlenmiş web bağlantılarını ayarlamak için şu anda mümkün değildir ve önerilir. Yönetilen giriş ekranını etkileyen **cihaz yapılandırmasında** kullanılabilen ayarların tam listesi için bkz. [adanmış cihaz ayarları](../configuration/device-restrictions-android-for-work.md#device-experience).  

İlk olarak, [Microsoft Endpoint Manager yönetim merkezine](https://go.microsoft.com/fwlink/?linkid=2109431) gidin ve **uygulamalar**  >  **uygulama yapılandırma ilkeleri**' ni seçin. **Android** çalıştıran **yönetilen cihazlar** için bir yapılandırma ilkesi ekleyin ve Ilişkili uygulama olarak **yönetilen giriş ekranı** ' nı seçin. Kullanılabilir farklı yönetilen giriş ekranı ayarlarını yapılandırmak için **yapılandırma ayarları** ' na tıklayın. 

## <a name="choosing-a-configuration-settings-format"></a>Yapılandırma ayarları biçimi seçme

Yönetilen giriş ekranının yapılandırma ayarlarını tanımlamak için kullanabileceğiniz iki yöntem vardır:

- **Yapılandırma Tasarımcısı** , özellikleri açık veya kapalı ve değerleri ayarlamanıza olanak tanıyan kullanımı kolay bir kullanıcı arabirimi ile ayarları yapılandırmanıza olanak tanır. Bu yöntemde, değer türünde devre dışı bırakılmış birkaç yapılandırma anahtarı vardır `BundleArray` . Bu yapılandırma anahtarları yalnızca JSON verileri girilerek yapılandırılabilir. 
- **JSON verileri** , bir JSON betiği kullanarak tüm olası yapılandırma anahtarlarını tanımlamanızı sağlar. 

Yapılandırma Tasarımcısı ile Özellikler eklerseniz, **yapılandırma ayarları biçim** AÇıLAN listesinden **JSON verisi gir** ' i seçerek bu özellikleri otomatik olarak JSON 'a dönüştürebilirsiniz.

![Yapılandırma ayarı biçim seçeneklerinin ekran görüntüsü](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_01.png)

## <a name="using-configuration-designer"></a>Yapılandırma tasarımcısını kullanma

Yapılandırma Tasarımcısı, önceden doldurulmuş ayarları ve bunlarla ilişkili değerleri seçmenizi sağlar. 

![Eklenen yapılandırma ayarlarının ekran görüntüsü](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_02.png)

Aşağıdaki tablo, yönetilen giriş ekranı kullanılabilir yapılandırma anahtarlarını, değer türlerini, varsayılan değerleri ve açıklamaları listeler. Açıklama, seçilen değerlere göre beklenen cihaz davranışını sağlar. Yapılandırma tasarımcısında devre dışı bırakılan yapılandırma anahtarları tabloda listelenmez.

| Yapılandırma anahtarı | Değer Türü | Varsayılan değer | Açıklama |
|---------------------------------------------------------------------------------------------------------------------------|-------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Izgara boyutunu ayarla | string | Otomatik | Yönetilen giriş ekranında, uygulamaların kılavuz boyutunu ayarlamanızı sağlar. Kılavuz boyutunu tanımlamak için uygulama satır ve sütun sayısını aşağıdaki biçimde ayarlayabilirsiniz `columns;rows` . Kılavuz boyutunu tanımlarsanız, giriş ekranındaki bir satırda gösterilecek en fazla uygulama sayısı, ayarladığınız satır sayısı ve giriş ekranındaki bir sütunda gösterilecek en fazla uygulama sayısı, ayarladığınız sütun sayısı olacak şekilde değişir. |
| Bildirimleri etkinleştir rozet | bool | FALSE | Uygulamadaki yeni bildirimlerin sayısını gösteren uygulama simgeleri için bildirim rozetini sunar. Bu ayarı etkinleştirirseniz, son kullanıcılar okunmamış bildirimlere sahip uygulamalarda bildirim rozetlerini görür. Bu yapılandırma anahtarını devre dışı tutarsanız, Son Kullanıcı okunmamış bildirimlere sahip olabilecek uygulamalar için herhangi bir bildirim görmeyecektir. |
| Giriş ekranını kilitle | bool | TRUE | Son kullanıcının, ana ekranda uygulama simgeleri etrafında hareket etme yeteneğini kaldırır. Bu yapılandırma anahtarını etkinleştirirseniz, giriş ekranındaki uygulama simgeleri kilitlenir ve Son Kullanıcı, ana ekranın farklı kılavuz konumlarına sürükleyip bırakamaz. ' A açıldıysa `false` , son kullanıcılar, yönetilen giriş ekranındaki uygulama ve Web bağlantısı simgeleri etrafında hareket edebilir.  |
| Cihaz duvar kağıdını ayarla | string | Varsayılan | Duvar kağıdı olarak ayarlamak istediğiniz görüntünün URL 'sini girerek tercih ettiğiniz bir duvar kağıdını ayarlamanıza olanak sağlar. |
| Uygulama simge boyutunu ayarla | integer | 2 | Ana ekranda görüntülenecek uygulamalar için simge boyutunu ayarlamanıza olanak sağlar. Bu yapılandırmada, farklı boyutlar (en küçük), 1 (küçük), 2 (normal), 3 (büyük) ve 4 (en büyük) için aşağıdaki değerleri seçebilirsiniz. |
| Uygulama klasörü simgesini ayarla | integer | 0 | Ana ekranda uygulama klasörlerinin görünümünü tanımlamanızı sağlar. Şu değerlerden görünümü seçebilirsiniz: koyu kare (0);   Koyu Daire (1); Açık kare (2); Açık daire (3). |
| Ekran yönünü ayarla | integer | 1 | Giriş ekranının yönünü dikey moda, yatay moda ayarlamanıza veya otomatik olarak döndürmeye izin verir. Yönü 1 (dikey mod için), 2 (Yatay mod için), 3 (Oto döndürme için) değerini girerek ayarlayabilirsiniz. |
| İzin verilen uygulamaları ayarla | Paketleme Learray | FALSE | , Cihazda yüklü uygulamalar arasından giriş ekranında görünür olan uygulama kümesini tanımlamanızı sağlar. Uygulamaları, görünür hale getirmek istediğiniz uygulamaların uygulama paketi adını girerek tanımlayabilirsiniz, örneğin com. Microsoft. emmx, ayarları giriş ekranında erişilebilir hale getirir. Bu bölümde izin verilen uygulamaların, ana ekranda görünür olması için cihazda zaten yüklü olması gerekir. |
| Sabitlenmiş Web bağlantıları ayarla | Paketleme Learray | FALSE | Web sitelerini giriş ekranında hızlı başlatma simgeleri olarak sabitetmenize olanak tanır. Bu yapılandırmayla, URL 'YI tanımlayabilir ve son kullanıcının tarayıcıda tek bir dokunmayla başlatması için giriş ekranına ekleyebilirsiniz. Note: cihazlarınıza, izin verilen uygulamalar gibi kabul edilen [yönetilen Google Play web bağlantıları](./apps-add-android-for-work.md#managed-google-play-web-links) oluşturmanızı, atamanızı ve onaylamanızı öneririz. |
| Ekran koruyucuyu etkinleştir | bool | FALSE | Ekran koruyucu modunu etkinleştirmek için. True olarak ayarlanırsa, **screen_saver_image**, **screen_saver_show_time**,   **inactive_time_to_show_screen_saver**ve   **media_detect_screen_saver**yapılandırabilirsiniz. |
| Ekran koruyucu görüntüsü | string |   | Ekran koruyucu görüntüsünün URL 'sini ayarlayın. Hiçbir URL ayarlanmamışsa, ekran koruyucusu etkinleştirildiğinde cihazlar varsayılan ekran koruyucu görüntüsünü gösterir. Varsayılan görüntüde, yönetilen giriş ekranı uygulaması simgesi gösterilir.  |
| Ekran koruyucunun zamanı gösterme | integer | 0 | Cihazın ekran koruyucu modu sırasında ekran koruyucuyu görüntüleyeceği süre miktarını saniye cinsinden ayarlama seçeneği sunar. 0 olarak ayarlanırsa, ekran koruyucusu cihaz etkin hale gelene kadar ekran koruyucu modunda süresiz olarak görünür.  |
| Ekran koruyucuyu etkinleştirmek için etkin olmayan süre | integer | 30 | Ekran koruyucusunu tetiklemeden önce cihazın etkin olmayan saniye sayısı. 0 olarak ayarlanırsa cihaz, ekran koruyucu moduna hiçbir şekilde gitmeyecektir. |
| Ekran koruyucuyu göstermeden önce Medya Algılama | bool | TRUE | Cihazda ses/video oynatılırken cihaz ekranının ekran koruyucuyu gösterip göstermeyeceğini seçin. True olarak ayarlanırsa cihaz, **inactive_time_to_show_scree_saver**değerden bağımsız olarak ses/video oynamaz. False olarak ayarlanırsa, cihaz ekranı,   **inactive_time_to_show_screen_saver**ayarlanan değere göre ekran koruyucuyu gösterir.   |
| Sanal giriş düğmesini etkinleştir | bool | FALSE | `True`Son kullanıcının, kullanıcının içinde bulundukları geçerli görevden yönetilen giriş ekranına döndürdüğü bir yönetilen giriş ekranı giriş düğmesine erişmesine izin vermek için bu ayarı etkinleştirin.  |
| Sanal giriş düğmesi türü | string | swipe_up | Giriş düğmesine bir çekme hareketi ile erişmek için **swipe_up** kullanın. Son Kullanıcı tarafından ekran etrafında taşınabilecek yapışkan ve kalıcı bir giriş düğmesine erişmek için **float** kullanın. |
| Pil ve sinyal gücü gösterge çubuğu | bool | Doğru  | Bu ayar `True` , pil ve sinyal gücü gösterge çubuğunu gösterir. |
| Kilit görev modu parolasıyla çık | string |   | Sorun giderme için kilit görevi modunun geçici olarak devre dışı bırakması için kullanılacak 4-6 basamaklı bir kod girin. |
| Yönetilen ayarı göster | bool | TRUE | "Yönetilen ayar", yalnızca hızlı erişim için herhangi bir ayar, **Wi-Fi ayarını göster**, **Bluetooth ayarını**göster, **birim ayarını**göster ve **el feneri ayarını göster**dahil olmak üzere herhangi bir ayarı yapılandırdıysanız görüntülenen, yönetilen bir giriş ekranı uygulamasıdır. Bu ayarlara, ekranda aşağı doğru da erişilebilir. `False`"Yönetilen ayar" uygulamasını gizlemek ve yalnızca aşağı doğru kaydırarak son kullanıcılara erişim ayarları sağlamak için bu anahtarı olarak ayarlayın.    |
| Kolay erişim hata ayıklama menüsünü etkinleştir | bool | FALSE | Yönetilen `True` Giriş ekranında, yönetilen ayarlar uygulamasından veya açılan menüden hata ayıklama menüsüne erişmek için bu ayarı etkinleştirin. Hata ayıklama menüsü Şu anda bilgi noktası modundan çıkma yeteneğinin yaşar ve geri düğmesine 15 kez tıklanarak erişilir. `False`Giriş noktasını hata ayıklama menüsüne tutmak için, yalnızca geri düğmesi aracılığıyla erişilebilen bu ayarı olarak ayarlayın.   |
| Wi-Fi ayarını göster | bool | FALSE | `True`Son kullanıcının Wi-Fi açmasına veya devre dışı olmasına veya farklı Wi-Fi ağlarına bağlanmasına izin vermek için bu ayarı etkinleştirmek.  |
| Wi-Fi izin verilenler listesini etkinleştir | bool | FALSE | Bu ayarı `True` , hangi Wi-Fi ağlarının yönetilen giriş ekranında gösterildiğini kısıtlamak Için **Wi-Fi izin verilenler-liste** anahtarını açın ve doldurun. `False`Cihazın bulduğu tüm olası Wi-Fi ağlarını göstermek için olarak ayarlayın. Bu ayarın yalnızca **Wi-Fi ayarını göster ayarı** olarak ayarlanmışsa `True` ve **Wi-Fi izin verilenler-listesi** doldurulduysa ilgili olduğunu unutmayın.   |
| Wi-Fi izin verilenler-liste| Paketleme Learray | FALSE | Cihazın yönetilen giriş ekranında görünmesini istediğiniz Wi-Fi ağlarının tüm SSID 'Lerini listeetmenize olanak tanır. Bu liste yalnızca **Wi-Fi ayarını göster** ve **Wi-Fi izin ver ' i etkinleştir-liste** olarak ayarlandıysa geçerlidir `True` . Bunlardan biri olarak ayarlandıysa `False` , bu yapılandırmayı değiştirmeniz gerekmez.    |
| Bluetooth ayarını göster | bool | FALSE | `True`Son kullanıcının Bluetooth 'u açmasına veya kapatmasına ve Bluetooth özellikli farklı cihazlara bağlanmasına izin vermek için bu ayar açılıyor.   |
| Birim ayarını göster | bool | FALSE | Bu ayar `True` , son kullanıcının medya birimini ayarlamak için bir birim kaydırıcıya erişmesine izin vermek üzere açılıyor.   |
| El feneri ayarını göster | bool | FALSE | `True`Son kullanıcının cihazın Flashlight 'e açık veya kapalı olmasına izin vermek için bu ayar açılıyor. Cihaz bir Flashlight desteklemiyorsa, bu ayar olarak yapılandırılmış olsa bile görünmez `True` .   |
| Cihaz bilgisi ayarını göster | bool | FALSE | Bu ayar `True` , son kullanıcının yönetilen ayar uygulamasından veya aşağı çekerek Cihaz hakkında hızlı bilgilere erişmesine izin verir. Erişilebilir bilgiler cihazın marka, model ve seri numarasını içerir.   |
| Klasördeki uygulamalar ada göre sıralanır | bool | TRUE | `False`Bir klasördeki öğelerin belirtildikleri sırada görünmesine izin vermek için bu ayarı açmak. Aksi takdirde, bu, klasörde alfabetik olarak görünürler.   |
| Uygulama sırası etkin | bool | FALSE | Bu ayarın etkinleştirilmesi, `True` yönetilen giriş ekranındaki uygulamaların, Web bağlantılarının ve klasörlerin sırasını ayarlamanıza olanak sağlar. Etkinleştirildikten sonra sıralamayı **app_order**ayarlayın.   |
| Uygulama sırası | Paketleme Learray | FALSE | Yönetilen giriş ekranındaki uygulamaların, Web bağlantılarının ve klasörlerin sırasını belirtmenize olanak tanır. Bu ayarı kullanmak için, **kilit giriş ekranının** etkinleştirilmesi gerekir, **Izgara boyutunu ayarlama** tanımlanmalıdır ve **uygulama sırası etkin** olmalıdır `True` .   |

## <a name="enter-json-data"></a>JSON verilerini girin

Yönetilen giriş ekranının tüm kullanılabilir ayarlarını ve **yapılandırma tasarımcısında**devre dışı bırakılmış ayarları YAPıLANDıRMAK için JSON verilerini girin.

![Eklenen JSON verilerinin ekran görüntüsü](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_03.png)

**Yapılandırma Tasarımcısı** tablosunda (yukarıda) listelenen yapılandırılabilir ayarların listesine ek olarak, aşağıdaki tablo yalnızca JSON verileri aracılığıyla yapılandırabileceğiniz yapılandırma anahtarlarını sağlar.

|    Yapılandırma anahtarı    |    Değer türü    |    Varsayılan değer    |    Açıklama    |
|-------------------------------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    İzin verilen uygulamaları ayarla    |    Paketleme Learray    | <img alt="JSON - Example 1" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson01.png" width="300"> |    , Cihazda yüklü uygulamalar arasından giriş ekranında görünür olan uygulama kümesini tanımlamanızı sağlar. Uygulamaları, görünür hale getirmek istediğiniz uygulamaların uygulama paketi adını (örneğin, com. Android) girerek tanımlayabilir. ayarlar, ayarları giriş ekranında erişilebilir hale getirir. Bu bölümde izin verilen uygulamaların, ana ekranda görünür olması için cihazda zaten yüklü olması gerekir.    |
|    Sabitlenmiş Web bağlantıları ayarla    |    Paketleme Learray    | <img alt="JSON - Example 2" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson02.png" width="300"> |    Web sitelerini giriş ekranında hızlı başlatma simgeleri olarak sabitetmenize olanak tanır. Bu yapılandırmayla, URL 'YI tanımlayabilir ve son kullanıcının tarayıcıda tek bir dokunmayla başlatması için giriş ekranına ekleyebilirsiniz. Note: cihazlarınıza, izin verilen uygulamalar gibi kabul edilen [yönetilen Google Play web bağlantıları](./apps-add-android-for-work.md#managed-google-play-web-links) oluşturmanızı, atamanızı ve onaylamanızı öneririz.    |
|    Uygulamaları gruplandırmak için yönetilen klasör oluştur    |    Paketleme Learray    | <img alt="JSON - Example 3" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson03.png" width="300"> |    Klasörler oluşturup bu klasörler içinde grup uygulamaları oluşturmanıza olanak tanır. Son kullanıcılar klasörleri taşıyamayacak, klasörleri yeniden adlandıramayacak veya uygulamaları klasörler içinde taşıyaamayacak.   Klasörler oluşturulan sırada görünür ve klasörler içindeki uygulamalar alfabetik olarak görünür.         Note: klasörlere gruplandırmak istediğiniz tüm uygulamaların cihaza gerekli olarak atanması ve yönetilen giriş ekranına eklenmiş olması gerekir.     |

Aşağıda, tüm kullanılabilir yapılandırma anahtarlarının dahil olduğu bir JSON betiği verilmiştir:

```json
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "com.microsoft.launcher.enterprise",
    "managedProperty": [
        {
            "key": "lock_home_screen",
            "valueBool": true
        },
        {
            "key": "wallpaper",
            "valueString": "default"
        },
        {
            "key": "icon_size",
            "valueInteger": 2
        },
        {
            "key": "app_folder_icon",
            "valueInteger": 0
        },
        {
            "key": "screen_orientation",
            "valueInteger": 1
        },
        {
            "key": "applications",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "app package name here"
                        }
                    ]
                }
            ]
        },
        {
            "key": "weblinks",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "link",
                            "valueString": "link here"
                        },
                        {
                            "key": "label",
                            "valueString": "weblink label here"
                        }
                    ]
                }
            ]
        },
        {
            "key": "show_virtual_home",
            "valueBool": false
        },
        {
            "key": "virtual_home_type",
            "valueString": "swipe_up"
        },
        {
            "key": "show_virtual_status_bar",
            "valueBool": true
        },
        {
            "key": "exit_lock_task_mode_code",
            "valueString": ""
        },
        {
            "key": "show_wifi_setting",
            "valueBool": false
        },
        {
            "key": "show_bluetooth_setting",
            "valueBool": false
        },
        {
            "key": "show_flashlight_setting",
            "valueBool": false
        },
        {
            "key": "show_volume_setting",
            "valueBool": false
        },
        {
            "key": "show_device_info_setting",
            "valueBool": false
        },
        {
            "key": "show_managed_setting",
            "valueBool": false
        },
        {
            "key": "enable_easy_access_debugmenu",
            "valueBool": false
        },
        {
            "key": "enable_wifi_allowlist",
            "valueBool": false
        },
        {
            "key": "wifi_allowlist",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "SSID",
                            "valueString": "name of Wi-Fi network 1 here"
                        }
                    ]
                },   
                {
                    "managedProperty": [
                        {
                            "key": "SSID",
                            "valueString": "name of Wi-Fi network 2 here"
                        }
                    ]
                }  
            ]
        },
        {
            "key": "grid_size",
            "valueString": "4;5"
        },
        {
            "key": "app_order_enabled",
            "valueBool": true
        },
        {
            "key": "apps_in_folder_ordered_by_name",
            "valueBool": true
        },
        {
            "key": "app_orders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.Microsoft.emmx"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 1
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Work"
                        },
                        {
                            "key": "type",
                            "valueString": "managed_folder"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 2
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.microsoft.launcher.enterprise"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "class",
                            "valueString": "com.microsoft.launcher.launcher"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 3
                        }
                    ]
                }
            ]
        },
        {
            "key": "managed_folders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Folder name here"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.emmx"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.bing"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "link",
                                            "valueString": "https://microsoft.com/"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Example folder name 2"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.office.word"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="googles-android-device-policy-app"></a>Google 'ın Android cihaz Ilkesi uygulaması
Yönetilen giriş ekranı uygulaması artık Google 'ın Android cihaz Ilkesi uygulamasına erişim sağlar. Yönetilen giriş ekranı uygulaması, Intune 'A kayıtlı cihazlar için çok uygulama bilgi noktası modunu kullanan Android kurumsal (AE) adanmış cihazlar olarak kullanılan özel bir başlatıdır. Android cihaz Ilkesi uygulamasına erişebilir veya destek ve hata ayıklama amacıyla kullanıcılara Android cihaz Ilkesi uygulamasına rehberlik edebilirsiniz. Bu başlatma özelliği, cihazın ne zaman kaydolur ve yönetilen giriş ekranına kilitlediği sırada kullanılabilir. Bu işlevselliği kullanmak için ek yükleme gerekmez.

## <a name="managed-home-screen-debug-screen"></a>Yönetilen giriş ekranı hata ayıklama ekranı
Hata ayıklama ekranı görüntülenene kadar **geri** düğmesine tıklayarak yönetilen giriş ekranının hata ayıklama ekranına erişebilirsiniz ( **geri** düğmesine 15 kez veya daha fazla tıklayın). Bu hata ayıklama ekranından, Android cihaz Ilkesi uygulamasını başlatabilir, günlükleri görüntüleyebilir ve yükleyebilir ya da cihazı güncelleştirmek için geçici olarak bilgi noktası modunu duraklatabilirsiniz. Bilgi noktası modunu duraklatma hakkında daha fazla bilgi için, Android kurumsal [adanmış cihaz ayarlarındaki](../configuration/device-restrictions-android-for-work.md#device-experience) **bilgi noktası modu** öğesine bakın. Yönetilen giriş ekranının hata ayıklama ekranına erişmenin daha kolay bir yolunu isterseniz, uygulama yapılandırma ilkelerini kullanmak için **kolay erişim hata ayıklama menüsünü etkinleştir** seçeneğini belirleyebilirsiniz `True` . 

## <a name="next-steps"></a>Sonraki adımlar

- Android kurumsal adanmış cihazlar hakkında daha fazla bilgi için bkz. [Android kurumsal adanmış cihazların Intune kaydını ayarlama](../enrollment/android-kiosk-enroll.md).
