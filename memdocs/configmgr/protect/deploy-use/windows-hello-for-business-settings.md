---
title: İş İçin Windows Hello ayarları
titleSuffix: Configuration Manager
description: Iş için Windows Hello 'Yu Configuration Manager ile tümleştirmeyi öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c60f30e306c6ff52849cfcdd4696d67a7d26f395
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722238"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Configuration Manager Iş için Windows Hello ayarları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1245704-->
Configuration Manager Iş için Windows Hello ile tümleşir. (Bu özellik daha önce İş için Microsoft Passport olarak bilinirdi.) Iş için Windows Hello, Windows 10 cihazlar için alternatif bir oturum açma yöntemidir. Parolayı, akıllı kartı ya da sanal akıllı kartı değiştirmek için Active Directory veya bir Azure Active Directory (Azure AD) hesabı kullanır. Iş için Hello, parola yerine oturum açmak için bir *Kullanıcı hareketi* kullanmanıza imkan tanır. Kullanıcı hareketi bir PIN, biyometrik kimlik doğrulaması veya parmak izi okuyucu gibi harici bir cihaz olabilir.

> [!Important]  
> Sürüm 1910 ' den başlayarak Configuration Manager ' deki Iş için Windows Hello ayarları ile sertifika tabanlı kimlik doğrulaması desteklenmez. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Anahtar tabanlı kimlik doğrulaması hala geçerli.
>
> Active Directory Federasyon Hizmetleri (AD FS) kayıt yetkilisi (ADFS RA) dağıtımı basittir, daha iyi bir kullanıcı deneyimi sağlar ve daha belirleyici bir sertifika kayıt deneyimi vardır. Iş için Windows Hello ile sertifika tabanlı kimlik doğrulaması için ADFS RA kullanın.
>
> Ortak yönetilen cihazlar için, [ **kaynak erişim ilkeleri** iş yükünü](../../comanage/workloads.md#resource-access-policies) Intune 'a taşımayı düşünün. Daha sonra bu sertifikaları yönetmek için Intune ilkelerini kullanın. Daha fazla bilgi için bkz. [iş yüklerini değiştirme](../../comanage/how-to-switch-workloads.md).

Daha fazla bilgi için bkz. [iş Için Windows Hello](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Configuration Manager aşağıdaki yollarla Iş için Windows Hello ile tümleşir:  

- Kullanıcıların oturum açmak için hangi hareketleri kullanabileceğini ve kullanabileceğini denetleyin.  

- Kimlik doğrulama sertifikalarını Iş için Windows Hello anahtar depolama sağlayıcısına (KSP) depolayın. Daha fazla bilgi için bkz. [sertifika profilleri](introduction-to-certificate-profiles.md).  

- Configuration Manager istemcisini çalıştıran etki alanına katılmış Windows 10 cihazlarında ayarlarını denetlemek için bir Iş için Windows Hello profili oluşturun ve dağıtın. Sürüm 1910 ' den başlayarak sertifika tabanlı kimlik doğrulaması kullanamazsınız. Anahtar tabanlı kimlik doğrulaması kullanırken, bir sertifika profili dağıtmanız gerekmez.

## <a name="configure-a-profile"></a>Profil yapılandırma  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Uyumluluk ayarları**' nı genişletin, **Şirket kaynağına erişim**' i genişletin ve **iş için Windows Hello profilleri** düğümünü seçin.

1. Şeritte, profil sihirbazını başlatmak için **iş Için Windows Hello profili oluştur** ' u seçin.

1. **Genel** sayfasında, bu profil için bir ad ve isteğe bağlı bir açıklama belirtin.

1. **Desteklenen platformlar** sayfasında, bu profilin uygulanacağı işletim sistemi sürümlerini seçin.

1. **Ayarlar** sayfasında, aşağıdaki ayarları yapılandırın:

    - **İş Için Windows Hello 'Yu Yapılandır**: Bu profilin Iş Için Hello 'yu etkinleştirip etkinleştirmeyeceğini, devre dışı bırakıp değiştirmediğini belirtin.

    - **Güvenilir Platform Modülü (TPM) kullanın**: TPM, ek bir veri güvenliği katmanı sağlar. Aşağıdaki değerlerden birini seçin:  

      - **Gerekli**: yalnızca erişilebilir TPM 'ye sahip cihazlar Iş Için Windows Hello 'yu sağlayabilir.  

      - **Tercih edilen**: cihazlar ilk olarak bir TPM kullanmayı dener. Kullanılabilir değilse, yazılım şifrelemesini kullanabilirler.

    - **Kimlik doğrulama yöntemi**: Bu seçeneği **Yapılandırılmadı** veya **anahtar tabanlı**olarak ayarlayın.

        > [!NOTE]
        > Sürüm 1910 ' den başlayarak Configuration Manager ' deki Iş için Windows Hello ayarları ile sertifika tabanlı kimlik doğrulaması desteklenmez.

    - **MINIMUM PIN uzunluğunu Yapılandır**: kullanıcının PIN 'i için en az bir uzunluk gerektirmek istiyorsanız, bu seçeneği etkinleştirin ve bir değer belirtin. Etkinleştirildiğinde, varsayılan değer `4`.

    - **MAKSIMUM PIN uzunluğunu Yapılandır**: kullanıcının PIN 'i için maksimum uzunluk gerektirmek istiyorsanız, bu seçeneği etkinleştirin ve bir değer belirtin. Etkinleştirildiğinde varsayılan değer `127`.

    - **PIN süre sonu iste (gün)**: kullanıcının cihaz PIN 'ini değiştirmesi gereken gün sayısını belirtir.

    - **Önceki PIN 'lerin yeniden kullanılmasını engelle**: kullanıcıların daha önce kullandıkları PIN 'leri kullanmasına izin verme.

    - **PIN 'de büyük harfli harfler iste**: kullanıcıların Iş Için WINDOWS Hello PIN kodunda büyük harfler içerip içermediğini belirtir. Aşağıdakilerden birini seçin:  

      - **Izin verilen**: kullanıcılar PIN kodlarında büyük harf karakterler kullanabilir, ancak bunu yapmak zorunda değildir.

      - **Gerekli**: kullanıcılar PIN kodlarına en az bir büyük harf karakter içermelidir.  

      - **İzin verilmiyor**: kullanıcılar PIN kodlarında büyük harf karakterler kullanamaz.  

    - **PIN 'de**küçük harf gerektir: kullanıcıların Iş Için WINDOWS Hello PIN kodunda küçük harfler mi içermesi gerektiğini belirtir. Aşağıdakilerden birini seçin:  

      - **Izin verilen**: kullanıcılar PIN kodlarında küçük harfli karakterler kullanabilir, ancak bunu yapmak zorunda kalmaz.

      - **Gerekli**: kullanıcılar PIN kodlarına en az bir küçük harf karakter içermelidir.  

      - **İzin verilmiyor**: kullanıcılar PIN kodlarında küçük harf karakterler kullanamaz.  

    - **Özel karakterleri Yapılandır**: PIN 'de özel karakterlerin kullanımını belirtir. Aşağıdakilerden birini seçin:  

        > [!NOTE]
        > Özel karakterler aşağıdaki kümeyi içerir:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Izin verilen**: kullanıcılar PIN kodlarında özel karakterler kullanabilir, ancak bunu yapmak zorunda değildir.  

      - **Gerekli**: kullanıcılar PIN kodlarına en az bir özel karakter içermelidir.  

      - **İzin verilmiyor**: kullanıcılar PIN kodlarında özel karakterler kullanamaz. Bu davranış, ayar **yapılandırılmamışsa**da olur.  

    - **PIN 'de basamakların kullanımını yapılandırma**: PIN 'teki sayıların kullanımını belirtir. Aşağıdakilerden birini seçin:

      - **Izin verilen**: kullanıcılar PIN kodlarında sayı kullanabilir, ancak bunu yapmak zorunda kalmaz.  

      - **Gerekli**: kullanıcıların PIN kodlarına en az bir sayı eklemesi gerekir.  

      - **İzin verilmiyor**: kullanıcılar PIN kodlarında sayı kullanamaz.

    - **Biyometrik hareketleri etkinleştir**: yüz tanıma veya parmak izi gibi biyometrik kimlik doğrulaması kullanın. Bu modlar, Iş için Windows Hello PIN 'inin bir alternatifidir. Kullanıcılar, biyometrik kimlik doğrulaması başarısız olursa PIN 'ı hala yapılandırır.  

      **Evet**olarak ayarlanırsa iş Için Windows Hello, biyometrik kimlik doğrulamasına izin verir. **Hayır**olarak ayarlanırsa, iş Için Windows Hello, tüm hesap türleri için biyometrik kimlik doğrulamasını engeller.  

    - **Gelişmiş kimlik sahtekarlığına karşı koruma kullan**: destekleyen cihazlarda gelişmiş kimlik sahtekarlığı korumasını yapılandırır. **Evet**olarak ayarlanırsa, Windows, yüz özellikleri için tüm kullanıcıların yanıltma koruması kullanmasını gerektirir.  

    - **Telefonla oturum açma kullan**: bir cep telefonuyla iki öğeli kimlik doğrulamayı yapılandırır.

1. Sihirbazı tamamlayın.

Aşağıdaki ekran görüntüsünde Iş için Windows Hello profil ayarları örneği verilmiştir:  

![Iş için Windows Hello Ilke Sihirbazı, kullanılabilir ayarların listesini gösterir](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>İzinleri yapılandırma

1. Bir etki alanı yöneticisi veya eşdeğer kimlik bilgileri olarak, aşağıdaki isteğe bağlı özelliği yüklemiş olan güvenli, yönetim iş istasyonunda oturum açın: RSAT: Active Directory Domain Services ve hafif Dizin Hizmetleri Araçları.

1. **Active Directory Kullanıcıları ve bilgisayarları** konsolunu açın.

1. Etki alanını seçin, **eylem** menüsüne gidin ve **Özellikler**' i seçin.

1. **Güvenlik** sekmesine geçin ve **Gelişmiş**' i seçin.

    > [!TIP]
    > **Güvenlik** sekmesini görmüyorsanız Özellikler penceresini kapatın. **Görünüm** menüsüne gidin ve **Gelişmiş Özellikler**' i seçin.

1. **Add (Ekle)** seçeneğini belirleyin.

1. **Sorumluyu Seç** ' i seçin `Key Admins`ve girin.

1. **Uygulanacağı** öğe listesinde, alt **Kullanıcı nesneleri**' ni seçin.

1. Sayfanın alt kısmındaki **Tümünü Temizle**' yi seçin.

1. **Özellikler** bölümünde **msDS-Keycredentiallink okuma**' yı seçin.

1. Değişikliklerinizi kaydetmek ve tüm pencereleri kapatmak için **Tamam** ' ı seçin.

## <a name="next-steps"></a>Sonraki adımlar

[Sertifika profilleri](introduction-to-certificate-profiles.md)
