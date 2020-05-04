---
title: Wi-Fi profilleri oluşturma
titleSuffix: Configuration Manager
description: Kuruluşunuzdaki kullanıcılara kablosuz ağ ayarları dağıtmak için Configuration Manager ' de Wi-Fi profillerini nasıl kullanacağınızı öğrenin.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710772"
---
# <a name="create-wi-fi-profiles"></a>Wi-Fi profilleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kuruluşunuzdaki kullanıcılara kablosuz ağ ayarları dağıtmak için Configuration Manager 'daki Wi-Fi profillerini kullanın. Bu ayarları dağıtarak kullanıcılarınızın Wi-Fi ' a bağlanmasını kolaylaştırmaktadır.  

Örneğin, tüm Windows dizüstü bilgisayarların bağlanmasını sağlamak istediğiniz bir Wi-Fi ağınız vardır. Kablosuz ağa bağlanmak için gerekli ayarları içeren bir Wi-Fi profili oluşturun. Ardından, profili hiyerarşinizdeki Windows dizüstü bilgisayarları olan tüm kullanıcılara dağıtın. Bu cihazların kullanıcıları ağınızı kablosuz ağlar listesinde görür ve bu ağa kolayca bağlanabilir.  

Wi-Fi profillerini aşağıdaki işletim sistemi sürümleri için yapılandırabilirsiniz:

- Windows 8.1 32-bit veya 64 bit

- Windows RT 8.1

- Windows 10 veya Windows 10 Mobile

Şirket içi mobil cihaz yönetimi (MDM) kullanarak mobil cihazlara kablosuz ağ ayarları dağıtmak için Configuration Manager de kullanabilirsiniz. Daha fazla genel bilgi için bkz. [Şirket ıçı MDM nedir](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Bir Wi-Fi profili oluşturduğunuzda, çok çeşitli güvenlik ayarları ekleyebilirsiniz. Bu ayarlar, Configuration Manager sertifika profilleri kullanılarak gönderilen sunucu doğrulaması ve istemci kimlik doğrulaması sertifikalarını içerir. Sertifika profilleri hakkında daha fazla bilgi için bkz. [sertifika profilleri](introduction-to-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a>Wi-Fi profili oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin, **Şirket kaynağına erişim**' i genişletin ve **Wi-Fi profilleri** düğümünü seçin.

1. **Giriş** sekmesinde, **Oluştur** grubunda, **Wi-Fi profili oluştur**' u seçin.

1. Wi-Fi profili oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki bilgileri belirtin:

    - **Ad**: konsolda profili tanımlamak için benzersiz bir ad girin.

    - **Açıklama**: isteğe bağlı olarak, Wi-Fi profiliyle ilgili daha fazla bilgi sağlamak için bir açıklama ekleyin.

    - **Bir dosyadan var olan bir Wi-Fi profili öğesini Içeri aktar**: başka bir Wi-Fi profilinden ayarları kullanmak için bu seçeneği belirleyin. Bu seçeneği belirlediğinizde, sihirbazın geri kalan sayfaları iki sayfaya basitleştirilerek: **Wi-Fi profilini Içeri aktarma** ve **desteklenen platformları**.

        > [!IMPORTANT]
        > İçeri aktardığınız Wi-Fi profilinin Wi-Fi profili için geçerli XML içerdiğinden emin olun. Dosyayı içeri aktardığınızda Configuration Manager profil doğrulanmaz.

    - **Raporlar Için uyumsuzluk önem derecesi**: Wi-Fi profilini uyumsuz olacak şekilde değerlendirdiğinde cihazın rapor aldığı aşağıdaki önem düzeylerinden birini seçin. Örneğin, profil yüklemesi başarısız olursa, uyumsuz olur.

        - **Hiçbiri**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için bir hata önem derecesi raporlamaz.

        - **Bilgi**

        - **Warning**

        - **Kritik**

        - **Kritik ve olayla**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar. Cihazlar ayrıca uyumsuz durumu uygulama olay günlüğünde bir Windows olayı olarak da günlüğe kaydeder.

1. Sihirbazın **Wi-Fi profili** sayfasında aşağıdaki bilgileri belirtin:

    - **Ağ adı**: cihazların ağ adı olarak görüntüleyeceği adı belirtin.

        > [!IMPORTANT]
        > Configuration Manager, ağ adında kesme işareti (`'`) veya virgül (`,`) karakterlerinin kullanılmasını desteklemez.

    - **SSID**: Kablosuz ağın büyük/küçük harfe duyarlı kimliğini belirtin.

    - **Bu ağ aralıkta olduğunda otomatik olarak bağlan**
    - **Bu ağa bağlıyken diğer kablosuz ağı ara**
    - **Ağ kendi adını (SSID) yayınlamadığında bağlan**

1. **Güvenlik Yapılandırması** sayfasında, aşağıdaki bilgileri belirtin:

    > [!IMPORTANT]
    > Şirket [ıçı MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)Için bir Wi-Fi profili oluşturuyorsanız, Configuration Manager geçerli dalı yalnızca aşağıdaki Wi-Fi güvenlik yapılandırmasını destekler:  
    >
    > - Güvenlik türleri: **WPA2 Enterprise** veya **WPA2 Kişisel**  
    > - Şifreleme türleri: **AES** veya **TKIP**  
    > - EAP türleri: **Akıllı Kart veya diğer sertifika** ya da **PEAP**  

    - **Güvenlik türü**: Kablosuz ağın kullandığı güvenlik protokolünü seçin veya ağ güvenli değilse **kimlik doğrulaması yok (açık)** seçeneğini belirleyin.

    - **Şifreleme**: güvenlik türü destekliyorsa, kablosuz ağ için şifreleme yöntemini ayarlayın.

    - **EAP türü**: Seçili şifreleme yöntemi için kimlik doğrulama protokolünü seçin.

        > [!NOTE]
        > Yalnızca Windows Phone cihazlar için: **artık** EAP türleri ve **EAP-FAST** desteklenmez.

        Seçili EAP türünün özelliklerini belirtmek için **Yapılandır** ' ı seçin. Bu seçenek bazı seçili EAP türleri için kullanılamaz.

        > [!IMPORTANT]
        > EAP türü yapılandırma penceresi Windows 'dan. Configuration Manager konsolunu, seçili EAP türünü destekleyen bir bilgisayarda çalıştırdığınızdan emin olun.

    - **Her oturum açmada kullanıcı kimlik bilgilerini hatırla**: kullanıcıların Windows 'ta her oturum açtıklarında kablosuz ağ kimlik bilgilerini girmesi gerekmiyorsa Kullanıcı kimlik bilgilerini depolamak için bu seçeneği belirleyin.

1. Sihirbazın **Gelişmiş ayarlar** sayfasında, Wi-Fi profili için ek ayarları belirtin. Sihirbazın **Güvenlik Yapılandırması** sayfasında belirlediğiniz seçeneklere bağlı olarak, Gelişmiş ayarlar kullanılamayabilir veya farklılık gösterebilir. Örneğin, kimlik doğrulama modu veya çoklu oturum açma seçenekleri.

1. **Proxy ayarları** sayfasında, kablosuz ağınız bir ara sunucu kullanıyorsa, **Bu Wi-Fi profili Için proxy ayarlarını yapılandırma**seçeneğini belirleyin. Ardından, proxy için yapılandırma bilgilerini sağlayın.

1. **Desteklenen platformlar** sayfasında, bu Wi-Fi profilinin geçerli olduğu işletim sistemi sürümlerini seçin.

1. Sihirbazı tamamlayın.

## <a name="next-step"></a>Sonraki adım

> [!div class="nextstepaction"]
> [Wi-Fi profillerini dağıtma](deploy-wifi-vpn-email-cert-profiles.md)
