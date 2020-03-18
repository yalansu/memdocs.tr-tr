---
title: Microsoft Intune’da Windows cihazları için Wi-Fi ayarlarını içeri aktarma - Azure | Microsoft Docs
description: Netsh wlan kullanarak Wi-Fi ayarlarını bir Windows cihazından dışarı aktarın. Ardından, Windows 8.1, Windows 10 ve Windows Holographic for Business çalıştıran cihazlara Wi-Fi profili oluşturmak için bu dosyayı Intune’da içeri aktarın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8cd8deb04dc939ed3dc742c9066c6dbfd4f51f3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332934"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>Intune’da Windows cihazları için Wi-Fi ayarlarını içeri aktarma

Windows çalıştıran cihazlar için daha önce bir dosyaya aktarılmış Wi-Fi yapılandırma profilini içeri aktarabilirsiniz. **Windows 10 ve sonrası cihazlar için doğrudan Intune’da [Wi-Fi profili de oluşturabilirsiniz](wi-fi-settings-windows.md)** .

Uygulama alanı:  
- Windows 8.1 ve üzeri
- Windows 10 ve üzeri
- Windows 10 masaüstü veya mobil
- Windows 10 Holographic for Business

## <a name="export-wi-fi-settings-from-a-windows-device"></a>Windows cihazından Wi-Fi ayarlarını dışarı aktarma

Windows’ta `netsh wlan` kullanarak mevcut bir Wi-Fi profilini Intune tarafından okunabilen bir XML dosyasına aktarın. Profili başarıyla kullanmak için anahtarın düz metin olarak dışarı aktarılması gerekir.

Gerekli WiFi profilinin zaten yüklü olduğu bir Windows bilgisayarda aşağıdaki adımları kullanın:

1. **C:\wifi**gibi, aktarılmış Wi-Fi profilleri için yerel bir klasör oluşturun.
2. Yönetici olarak bir Komut İstemi açın.
3. `netsh wlan show profiles` komutunu çalıştırın. Dışarı aktarmak istediğiniz profilin adını aklınızda edin. Bu örnekte profil adı **WiFiName** şeklindedir.
4. `netsh wlan export profile name="ProfileName" folder=c:\Wifi` komutunu çalıştırın. Bu komut, hedef klasörünüzde **Wi-Fi-WiFiName.xml** adlı bir Wi-Fi profil dosyası oluşturur.

## <a name="import-the-wi-fi-settings-into-intune"></a>Wi-Fi ayarlarını Intune'da içeri aktarma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki ayarları girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Adın Wi-Fi profili xml’indeki ad özniteliği ile aynı olması **gereklidir**. Yoksa işlem başarısız olur.
    - **Açıklama**: Ayara genel bir bakış sağlayan ve diğer önemli ayrıntıları veren bir açıklama girin.
    - **Platform**: **Windows 8.1 ve üstünü**seçin.
    - **Profil türü**: **Wi-Fi içeri aktarma**' yı seçin.

    > [!IMPORTANT]
    > - Önceden paylaşılan anahtar içeren bir Wi-Fi profilini dışarı aktarıyorsanız komuta **eklemeniz**gereklidir`key=clear`. Örneğin şunu girin: `netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`
    > - Windows 10 ile önceden paylaşılan bir anahtar kullanılması, Intune 'da bir düzeltme hatasına neden olur. Bu durumda, Wi-Fi profili cihaza düzgün bir şekilde atanır ve profil beklendiği gibi çalışır.
    > - Önceden paylaşılan anahtar içeren bir Wi-Fi profilini dışarı aktarıyorsanız dosyanın korumalı olduğundan emin olun. Anahtar düz metin biçimindedir, yani anahtarı korumak sizin sorumluluğunuzdadır.

4. Aşağıdaki ayarları girin:

    - **Bağlantı adı**: Wi-Fi bağlantısı için bir ad girin. Bu ad, kullanılabilir Wi-Fi ağlarına gözatarken kullanıcılara gösterilir.
    - **PROFIL XML**'i: tarayıcı düğmesini seçin ve içeri aktarmak istediğiniz Wi-Fi profili AYARLARıNı içeren XML dosyasını seçin.
    - **Dosya içeriği**: Seçtiğiniz yapılandırma profili için XML kodunu görüntüler.

5. Değişikliklerinizi kaydetmek için **Tamam**’ı seçin.
6. İşiniz bittiğinde, Intune profilini oluşturmak için **tamam** > **Oluştur** ' u seçin. Bu tamamlandığında, profiliniz **cihazlar-yapılandırma profilleri** listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu ancak hiçbir şey yapmıyor. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

Diğer kullanılabilir platformlar da dahil olmak üzere [Wi-Fi ayarlarına genel bakış](wi-fi-settings-configure.md)bölümüne bakın.
