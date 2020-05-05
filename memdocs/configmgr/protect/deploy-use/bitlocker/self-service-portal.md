---
title: BitLocker Self Servis portalı
titleSuffix: Configuration Manager
description: Kullanıcı self servis portalı 'nı BitLocker kurtarma için Configuration Manager ' de kullanma
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda719aed4d70cd9783d158e17d546b698497997
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717408"
---
# <a name="bitlocker-self-service-portal"></a>BitLocker Self Servis portalı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

[BitLocker Self Servis Portalı 'nı yükledikten](setup-websites.md)sonra, BitLocker bir kullanıcının cihazını kilitlerse, kendilerine bağımsız olarak kendi bilgisayarlarına erişim alabilir. Self Servis portalı, yardım masası personelinden yardım gerektirmez.

[![Varsayılan BitLocker self servis portalının ekran görüntüsü](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Self Servis portalından bir kurtarma anahtarı almak için, bir kullanıcının bilgisayarda en az bir kez başarıyla oturum açmış olması gerekir. Bu oturum açma, uzak bir oturumda değil, cihazın yerel olması gerekir. Aksi takdirde, anahtar kurtarma için yardım masasına başvurmaları gerekir. Yardım Masası Yöneticisi, kurtarma anahtarını istemek için [Yönetim ve izleme Web sitesini](helpdesk-portal.md) kullanabilir.

BitLocker, aşağıdaki durumlarda cihazı kilitleyebilir:

- Kullanıcı BitLocker parolasını veya PIN 'ini unutuyor

- Cihazın işletim sistemi dosyalarında, BIOS 'unda veya Güvenilir Platform Modülü (TPM) bir değişikliği var

Self Servis portalından BitLocker kurtarma anahtarı istemek için:

1. BitLocker bir cihazı kilitlediğinde, başlangıç sırasında BitLocker kurtarma ekranını görüntüler. 32 basamaklı BitLocker kurtarma anahtarı KIMLIĞINI yazın.

1. Başka bir bilgisayarda, Web tarayıcısında Self Servis Portalı ' na gidin, örneğin `https://webserver.contoso.com/SelfService`.

1. Bildirimi okuyun ve kabul edin.

1. **Kurtarma anahtarı kimliği** alanında, BitLocker kurtarma anahtarı kimliğinin ilk sekiz basamağını girin. Birden çok anahtar eşleşiyorsa, tüm 32 basamakları girin.

1. Bu isteğin **nedeni** için aşağıdaki seçeneklerden birini belirleyin:

    - BIOS/TPM değişti
    - Değiştirilen işletim sistemi
    - Kayıp PIN/parola

1. **Anahtar al**' ı seçin. Self Servis portalı, 48 basamaklı **BitLocker kurtarma anahtarını**görüntüler.

1. Bu 48 basamaklı kodu bilgisayarınızdaki BitLocker kurtarma ekranına girin.

> [!NOTE]
> BitLocker Self Servis Portalı bir süre işlem yapılmadan sonra zaman aşımına uğrayabilir. Örneğin, beş dakika sonra 60 saniyelik bir sayaca sahip bir zaman aşımı uyarısı görebilirsiniz.
>
> ![BitLocker Self Servis Portalı zaman aşımı uyarısı](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Geri sayıma yanıt veremezseniz, oturumun kullanım süresini sona erecektir.
>
> ![BitLocker Self Servis Portalı oturumu süre dolma sayfası](media/bitlocker-self-service-portal-session-expired.png)
