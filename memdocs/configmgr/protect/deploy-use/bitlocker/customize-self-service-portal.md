---
title: Self servis portalı özelleştirme
titleSuffix: Configuration Manager
description: BitLocker yönetim self servis portalına özel kuruluşa özgü bilgiler ekleme
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f4fdb0d6a41c2b40c9e35840dfc27261a42e68b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713075"
---
# <a name="customize-the-self-service-portal"></a>Self servis portalı özelleştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

[BitLocker Self Servis Portalı 'nı yükledikten](setup-websites.md)sonra kuruluşunuz için özelleştirebilirsiniz. Özel bir uyarı, kuruluşunuzun adı ve kuruluşa özgü diğer bilgileri ekleyin.

## <a name="branding"></a>Markalama

Self Servis Portalı 'nı kuruluşunuzun adı, yardım masası URL 'SI ve uyarı metniyle birlikte markalama.

1. Self Servis Portalı 'nı barındıran Web sunucusunda, yönetici olarak oturum açın.

1. **Internet Information Services (IIS) Yöneticisi 'ni** başlatın ( **inetmgr. exe**' yi çalıştırın).

1. **Siteler**' i genişletin, **varsayılan Web sitesi**' ni genişletin ve **selfservice** düğümünü seçin. Ayrıntılar bölmesinde, **ASP.net** grubunda, **uygulama ayarları**' nı açın.

    [![IIS Yöneticisi 'nde SelfService uygulama ayarlarının örnek ekran görüntüsü](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Değiştirmek istediğiniz öğeyi seçin ve **Eylemler** bölmesinde **Düzenle**' yi seçin. **Değeri** , kullanmak istediğiniz yeni adla değiştirin.

    > [!CAUTION]
    > **Ad** değerlerini değiştirmeyin. Örneğin, değiştirme `CompanyName`, değiştirme `Contoso IT`. **Ad** değerlerini değiştirirseniz, Self Servis Portalı çalışmayı durdurur.

Değişiklikler hemen geçerli olur.

### <a name="supported-branding-values"></a>Desteklenen marka değerleri

Ayarlayabilmeniz gereken değerler için aşağıdaki tabloya bakın:

|Adı|Açıklama|Varsayılan&nbsp;değer|
|--- |--- |--- |
|CompanyName|Self Servis portalının her sayfanın üst kısmında üst bilgi olarak görüntüleyeceği kuruluş adı.|`Contoso IT`|
|Displaybildirimin|Kullanıcının kabul etmesi gereken bir ilk bildirim görüntüleyin.|`true`|
|HelpdeskText|"Diğer tüm ilgili sorunlar Için" altında sağ bölmedeki dize|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|HelpdeskText dizesinin bağlantısı.|olmamalıdır|
|NoticeTextPath|Kullanıcının kabul etmesi gereken ilk bildirimin metni. Varsayılan olarak, Web sunucusundaki tam dosya yolu `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`. Dosyayı bir düz metin düzenleyicisinde düzenleyin ve kaydedin. Bu yol değeri, SelfService uygulamasına göredir.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Varsayılan self servis portalının ekran görüntüsü için bkz. [BitLocker Self Servis Portalı](self-service-portal.md).

> [!TIP]
> Gerekirse, farklı dillerde görüntülenmek üzere Bu dizelerin bazılarını yerelleştirebilirsiniz. Daha fazla bilgi için bkz. [Yerelleştirme](#bkmk_localize).

## <a name="session-time-out"></a>Oturum zaman aşımı

Belirli bir süre işlem yapılmadan sonra kullanıcının oturumunun süresinin dolmasını sağlamak için self servis portalının oturum zaman aşımı ayarını değiştirebilirsiniz.

1. Self Servis Portalı 'nı barındıran Web sunucusunda, yönetici olarak oturum açın.

1. **Internet Information Services (IIS) Yöneticisi 'ni** başlatın ( **inetmgr. exe**' yi çalıştırın).

1. **Siteler**' i genişletin, **varsayılan Web sitesi**' ni genişletin ve **selfservice** düğümünü seçin. Ayrıntılar bölmesinde, **ASP.net** grubunda, **oturum durumu**' nu açın.

1. **Tanımlama bilgisi ayarları** grubunda, **zaman aşımı (dakika)** değerini değiştirin. Bu, kullanıcının oturumunun süresinin dolmasına geçen dakika sayısıdır. Varsayılan değer: `5`. Ayarı devre dışı bırakmak için, zaman aşımı olmaması için değerini olarak `0`ayarlayın.

1. **Eylemler** bölmesinde **Uygula**' yı seçin.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a>Yardım Masası metnini ve URL 'YI yerelleştirin

Self Servis portalı `HelpdeskText` bildiriminin ve `HelpdeskUrl` bağlantısının yerelleştirilmiş sürümlerini yapılandırabilirsiniz. Bu dize, kullanıcılara portalı kullanırken nasıl ek yardım alma hakkında bilgilendirir. Yerelleştirilmiş metni yapılandırırsanız Portal, Web tarayıcıları için yerelleştirilmiş sürümü bu dilde görüntüler. Yerelleştirilmiş bir sürüm bulamazsa, `HelpdeskText` ve `HelpdeskUrl` ayarlarında varsayılan değeri görüntüler.

1. Self Servis Portalı 'nı barındıran Web sunucusunda, yönetici olarak oturum açın.

1. **Internet Information Services (IIS) Yöneticisi 'ni** başlatın ( **inetmgr. exe**' yi çalıştırın).

1. **Siteler**' i genişletin, **varsayılan Web sitesi**' ni genişletin ve **selfservice** düğümünü seçin. Ayrıntılar bölmesinde, **ASP.net** grubunda, **uygulama ayarları**' nı açın.

1. **Eylemler** bölmesinde **Ekle**' yi seçin.

1. **Uygulama ayarı Ekle** penceresinde, aşağıdaki değerleri yapılandırın:

    - **Ad**: yazın `HelpdeskText_<language>`, burada `<language>` metin için dil kodudur.

      Örneğin, Ispanyolca (Ispanya) içinde `HelpdeskText` yerelleştirilmiş bir bildirim oluşturmak için, ad olur `HelpdeskText_es-es`.

    - **Değer**: aşağıdaki "diğer tüm sorunlar için" Self Servis Portalı 'nın sağ bölmesinde görüntülenecek yerelleştirilmiş dize "

1. Yeni ayarı kaydetmek için **Tamam ' ı** seçin.

1. İlişkili `HelpdeskUrl_<language>` `HelpdeskText_<language>` ayarla eşleşen yeni bir uygulama ayarı eklemek için bu işlemi tekrarlayın.

Kuruluşunuzda desteklediğiniz tüm diller için bir çift ayar eklemek için bu işlemi tekrarlayın.

## <a name="localize-the-notice-file"></a>Bildirim dosyasını yerelleştirin

Kullanıcının Self Servis Portalı 'nda kabul etmesi gereken ilk bildirimin yerelleştirilmiş sürümlerini yapılandırabilirsiniz. Varsayılan olarak, Web sunucusundaki tam dosya yolu `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`.

Yerelleştirilmiş bildirim metnini göstermek için yerelleştirilmiş bir bildirim. txt dosyası oluşturun. Ardından belirli bir dil klasörü altına kaydedin. Örneğin: `Self Service Website\es-es\Notice.txt` Ispanyolca (İspanya) için.

Self Servis portalı, aşağıdaki kurallara göre bildirim metnini görüntüler:

- Varsayılan bildirim dosyası eksikse, Portal varsayılan dosyanın eksik olduğunu belirten bir ileti görüntüler.

- Uygun dil klasöründe yerelleştirilmiş bir bildirim dosyası oluşturursanız, yerelleştirilmiş bildirim metnini görüntüler.

- Web sunucusu, bildirim dosyasının yerelleştirilmiş bir sürümünü bulamazsa, varsayılan bildirimi görüntüler.

- Kullanıcı kendi tarayıcısını yerelleştirilmiş bildirimi olmayan bir dile ayarlarsa, Portal varsayılan bildirimi görüntüler.

### <a name="create-a-localized-notice-file"></a>Yerelleştirilmiş bildirim dosyası oluşturma

1. Self Servis Portalı 'nı barındıran Web sunucusunda, yönetici olarak oturum açın.

1. Uygulama yolunda `<language>` desteklenen her dil için bir klasör oluşturun. `Self Service Website` Örneğin, `es-es` Ispanyolca (İspanya) için. Varsayılan olarak, tam yol `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`.

    Kullanabileceğiniz geçerli dil kodlarının listesi için bkz. [ulusal dil desteği (NLS) API başvurusu](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers).

    > [!TIP]
    > Dil klasörünün adı ayrıca dilden bağımsız bir ad olabilir. Örneğin, İspanyolca (Ispanya **) ve İspanyolca** (Arjantin) için es **-es** yerine İspanyolca için **es** . Kullanıcı tarayıcısını **es-es**olarak ayarladıysanız ve bu dil klasörü yoksa, Web sunucusu, üst yerel ayar klasörünü özyinelemeli olarak denetler.**es** (Üst ayarlar .NET içinde tanımlanmıştır.) Örneğin,`Self Service Website\es\Notice.txt`. Bu özyinelemeli geri dönüş, .NET kaynak yükleme kurallarını taklit eder.

1. Yerelleştirilmiş metinle varsayılan bildirim dosyanızın bir kopyasını oluşturun. Dil kodu klasörüne kaydedin. Örneğin, Ispanyolca (Ispanya) için, varsayılan olarak tam yol olur `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`.

Bu işlemi, kuruluşunuzda desteklediğiniz tüm diller için yerelleştirilmiş bir bildirim dosyasına yineleyin.

## <a name="next-steps"></a>Sonraki adımlar

Self Servis Portalı 'nı yükleyip özelleştirdiğinize göre, şimdi deneyin! Daha fazla bilgi için bkz. [BitLocker Self Servis Portalı](self-service-portal.md).
