---
title: Intune için Apple MDM Anında İletme sertifikası alma
titleSuffix: ''
description: Intune ile iOS/ıpados cihazlarını yönetmek için bir Apple MDM anında Iletme sertifikası alın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/08/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd1bea64bbde5c7da7579471f93f659b71dffa87
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327202"
---
# <a name="get-an-apple-mdm-push-certificate"></a>Apple MDM anında iletme sertifikası alma

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune 'un iOS/ıpados ve macOS cihazlarını yönetmesi için bir Apple MDM anında Iletme sertifikası gereklidir. Siz sertifikayı Intune’a ekledikten sonra, kullanıcılarınız şunları kullanarak cihazlarını kaydedebilir:

- Şirket Portalı uygulaması.

- Apple Aygıt Kayıt Programı, Apple School Manager veya Apple Configurator gibi Apple toplu kayıt yöntemleri.

Kayıt seçenekleri hakkında daha fazla bilgi için bkz. [iOS/ıpados cihazlarının nasıl kaydedileceğini seçme](ios-enroll.md).

Bir anında iletme sertifikasının süresi dolduğunda bunu yenilemeniz gerekir. Sertifikayı yenilerken, anında iletme sertifikasını oluştururken kullandığınız aynı Apple kimliğini kullandığınızdan emin olun.


## <a name="steps-to-get-your-certificate"></a>Sertifikanızı almak için adımlar
[Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın, **cihazlar** > **cihazları** > Kaydet**Apple kayıt** > **Apple MDM anında iletme sertifikası**' ı seçin ve ardından aşağıdaki adımları izleyin.

### <a name="step-1-grant-microsoft-permission-to-send-user-and-device-information-to-apple"></a>1. Adım. Microsoft’un Apple’a kullanıcı ve cihaz bilgilerini göndermesine izin verin
Kabul ediyorum ' u seçin **.** Microsoft’a verileri Apple’a gönderme izni verin.

![MDM Anında İletme Sertifikası ekranında MDM Anında İletme’nin ayarlanmamış hali.](./media/apple-mdm-push-certificate-get/create-mdm-push-certificate.png)

### <a name="step-2-download-the-intune-certificate-signing-request-required-to-create-an-apple-mdm-push-certificate"></a>2. Adım Apple MDM anında iletme sertifikası oluşturmak için gereken Intune sertifika imzalama isteğini indirin
İstek dosyasını indirip yerel olarak kaydetmek için **CSR 'Nizi indirin** seçeneğini belirleyin. Bu dosya, Apple Push Certificates Portalından bir güven ilişkisi sertifikası istemek için kullanılır.

### <a name="step-3-create-an-apple-mdm-push-certificate"></a>3. Adım Apple MDM anında iletme sertifikası oluşturun
Apple anında iletme sertifikası portalı 'na gitmek için **MDM anında Iletme sertifikanızı oluşturun** öğesini seçin. Şirketinizin Apple KIMLIĞIYLE oturum açın ve ardından **Sertifika Oluştur ' a**tıklayın. **Dosya Seç** ' i seçin ve sertifika imzalama isteği dosyasına gidin ve ardından **karşıya yükle**' yi seçin. Onay sayfasında, sertifika (. pek) dosyasını indirmek için **İndir** ' i seçin ve dosyayı yerel olarak kaydedin.

> [!NOTE]
> Sertifika, sertifikayı oluşturmak için kullanılan Apple Kimliği ile ilişkilidir. En iyi yöntem olarak, yönetim görevleri için bir şirket Apple Kimliği kullanın ve posta kutusunun dağıtım listesi gibi birden fazla kişi tarafından izlendiğinden emin olun. Hiçbir zaman kişisel Apple Kimliği kullanmayın.

### <a name="step-4-enter-the-apple-id-used-to-create-your-apple-mdm-push-certificate"></a>4. Adım. Apple MDM anında iletme sertifikanızı oluşturmak için kullandığınız Apple kimliğini girin
Bu sertifikayı yenilemeniz gerektiği zamanı anımsatması için bu kimliği kaydedin.

### <a name="step-5-browse-to-your-apple-mdm-push-certificate-to-upload"></a>5. Adım. Karşıya yüklemek üzere Apple MDM anında iletme sertifikanıza gidin
Sertifika (. pek) dosyasına gidin, **Aç**' ı seçin ve ardından **karşıya yükle**' yi seçin. Anında iletme sertifikasıyla Intune, Apple cihazları kaydedebilir ve yönetebilir.

## <a name="renew-apple-mdm-push-certificate"></a>Apple MDM anında iletme sertifikasını yenileme
Apple MDM anında iletme sertifikası bir yıl boyunca geçerlidir ve iOS/ıpados ve macOS cihaz yönetiminin korunması için yıllık olarak yenilenmelidir. Sertifikanızın süresi dolarsa, kayıtlı Apple cihazlarıyla iletişim kurulamaz.

Sertifika, sertifikayı oluşturmak için kullanılan Apple Kimliği ile ilişkilidir. MDM anında iletme sertifikasını oluşturmak için kullandığınız aynı Apple Kimliği ile yenileyin.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın, **cihazlar** > **kayıt cihazları** > **Apple kayıt** > **Apple MDM anında iletme sertifikası**' yi seçin.
2. İstek dosyasını indirip yerel olarak kaydetmek için **CSR 'Nizi indirin** seçeneğini belirleyin. Bu dosya, Apple Push Certificates Portalından bir güven ilişkisi sertifikası istemek için kullanılır.
3. Apple anında iletme sertifikası portalı 'na gitmek için **MDM anında Iletme sertifikanızı oluşturun** öğesini seçin. Yenilemek istediğiniz sertifikayı bulun ve **Yenile**' yi seçin.
4. **Anında Iletme sertifikasını yenileme** ekranında, ileride sertifikayı tanımanıza yardımcı olacak notlar sağlayın, indirdiğiniz yeni istek dosyasına gitmek Için **Dosya Seç** ' i seçin ve **karşıya yükle**' yi seçin.
   > [!TIP]
   > Bir Sertifika, UID’i tarafından tanımlanabilir. UID 'nin GUID kısmını bulmak için sertifika ayrıntılarında **konu kimliği** ' ni inceleyin. Ya da kayıtlı bir iOS/ıpados cihazında **Ayarlar** > **genel** > **cihaz** **yönetimi** > **Yönetim profili** > **diğer ayrıntılar** > **Yönetim profili**' ne gidin. İkinci satır öğesi olan **Konu**, Apple anında iletme sertifikaları portalındaki sertifikayla eşleşitebilmeniz IÇIN benzersiz GUID 'yi içerir.
 
6. **Onay** ekranında, **karşıdan yükle** ' yi seçin ve. ped dosyasını yerel olarak kaydedin.
7. [Intune](https://go.microsoft.com/fwlink/?linkid=2090973)'DA **Apple MDM anında iletme sertifikası** araştır simgesini seçin, Apple 'dan indirilen. PEZ dosyasını seçin ve **karşıya yükle**' yi seçin.

Apple MDM anında iletme sertifikanız **etkin** görünüyor ve süresi dolmadan 365 gün kaldı.
