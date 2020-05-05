---
title: Kullanıcılar cihazları nasıl kaydeder
titleSuffix: Configuration Manager
description: Kullanıcıların Configuration Manager ' de şirket içi mobil cihaz yönetimi (MDM) ile cihazları nasıl kaydedebileceğini anlayın.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722336"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Kullanıcıların Configuration Manager ' de şirket içi MDM ile cihaz kaydetme sıklığı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Şirket içi mobil cihaz yönetimi (MDM) ile kullanıcılar cihazlarını kaydedebilir. İki önkoşul vardır:

- İstemci ayarları ile kullanıcıya kaydolma iznini verirsiniz.

- Gerekli güvenilen kök sertifikayı cihaza yüklersiniz.

Kayıt ayarlama hakkında daha fazla bilgi için bkz. Şirket [ıçı MDM için cihaz kaydını ayarlama](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Windows 10 ' a Kaydet

1. Bir Windows 10 bilgisayarda **Ayarlar**’a gidin.

1. **Hesaplar**' ı seçin ve sonra **Iş veya okul erişimi**' ni seçin.

1. **Bağlan**' ı seçin, Kullanıcı asıl adını (UPN) girin ve **devam**' ı seçin. UPN, örneğin, jdoe@contoso.come-posta adresinizle aynı olabilir.

1. Kayıt proxy noktasının tam etki alanı adını (FQDN) girin ve **devam**' ı seçin.

1. Parolanızı girin ve **oturum aç**' ı seçin.

1. Windows 'un bu eylem için oturum açma bilgilerini anımsamasını gerekmez, bu nedenle **Atla**' yı seçin.

Kısa bir süre sonra, cihaz Configuration Manager ile kaydolur.

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Windows 10 Mobile 'ı kaydetme

1. Windows 10 mobil cihazda **Ayarlar**’a gidin.

1. **Hesaplar**' ı seçin ve ardından **iş erişimi**' ni seçin.

1. **Bağlan**’ı seçin.

1. UPN 'nizi ve kayıt proxy noktasının FQDN 'sini girin. Ardından **Bağlan**'ı seçin.

1. Bir sonraki ekranda, UPN ve parolanızı girip **oturum aç**' ı seçin.

Kısa bir süre sonra, cihaz Configuration Manager ile kaydolur. **Done** (Bitti) öğesini seçin.

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>Kaydı doğrula

Cihazların başarıyla kaydedildiğini doğrulamak için Configuration Manager konsolunu kullanın. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar**' ı seçin. Cihaz listesinde kayıtlı cihaza gözatıp arama yapın.
