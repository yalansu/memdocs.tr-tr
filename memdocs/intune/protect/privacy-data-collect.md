---
title: Intune’da veri toplama
titleSuffix: Microsoft Intune
description: Intune’da kişisel verilerin nasıl toplandığını öğrenin.
keywords: Gizlilik, kişisel veriler
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcd7ff1ae51314bc57be2bed39c7fe8ca7114d82
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076116"
---
# <a name="data-collection-in-intune"></a>Intune’da veri toplama

Kullanıcılar şirket veya kişisel cihazlarını Intune kullanarak kaydettiğinde, Intune iş işlemlerini desteklemek, müşteri ile iş yürütmek ve hizmeti desteklemek için bazı kişisel verileri toplar, işler ve paylaşır. Intune, kişisel verileri aşağıdaki kaynaklardan toplar:

- Microsoft Endpoint Manager Yönetim Merkezi 'nde Intune kullanan yöneticiler.
- Son Kullanıcı cihazları (cihazlar Intune yönetimine kaydolduktan ve kullanım sırasında).
- Üçüncü taraf hizmetlerindeki müşteri hesapları (yönetici talimatları başına).
- Tanılama, performans ve kullanım bilgileri.

Intune, bu kaynaklardan aşağıdaki iki kategoride yer alan bilgileri toplar: [gerekli](#required-data), [isteğe bağlı](#optional-data). Kategorilerin her birinde, veriler müşteri verileri, kişisel veriler, tanılama verileri ve hizmet tarafından oluşturulan veriler tarafından daha fazla bölünür. 

> [!NOTE]
> Her nedenden dolayı hizmetimizin tarafından toplanan herhangi bir veriyi üçüncü taraflardan satmayacağız.

## <a name="required-data"></a>Gerekli veriler

Gerekli kategoride bulunan veriler, hizmetimizi müşteri tarafından beklendiği gibi çalışır hale getirmek için gereken verilerden oluşur. Intune tarafından toplanan verilerin büyük bir kısmının gerekli verileri vardır. Bu tür veriler bir kullanıcı, cihaz veya uygulamaya bağlıdır ve yönetimin yapısı gereği gereklidir. Toplanan veriler hem kişisel verileri hem de kişisel olmayan verileri içerir. Kişisel veriler, son kullanıcıyı doğrudan belirleyebilen veya sistem tarafından oluşturulan benzersiz bir tanımlayıcıya sahip, verileri ve hesap verilerini destekleyecek şekilde kullanılan benzersiz bir tanımlayıcıya sahip sahte veriler içeren tanımlanabilir verileri içerir. Kişisel olmayan veriler, hizmet tarafından oluşturulan sistem meta verilerini ve kuruluş/kiracı bilgilerini içerir. Intune, yönetim rollerine ve işlevlerine erişimi, [rol tabanlı Access Control](../fundamentals/role-based-access-control.md)gibi özelliklerle yönetmek için erişim denetimi verilerini de toplar.

Intune tarafından toplanan gerekli veriler şunlar olabilir, ancak bunlarla sınırlı değildir: 

- Kullanıcı bilgileri
  - Sahip adı/Kullanıcı görüntüsü (AzureUserID tarafından tanımlanan kullanıcının Azure tarafından kaydedilen adı)
  - Kullanıcı Asıl Adı veya e-posta adresi
  - Telefon numarası
  - Üçüncü taraf kullanıcı tanımlamaları (AppleID gibi)
- Donanım envanteri bilgileri
  - Cihaz adı
  - Üretici
  - İşletim sistemi
  - Seri numarası
  - IMEI numarası
  - IP adresi
  - Wi-Fi MacAddress
  - ICCID
- Aşağıdaki etkinliklere ilişkin veriler dahil olmak üzere denetim günlüğü bilgileri
  - Yönetim
  - Oluştur
  - Güncelleştirme (düzenleme)
  - Sil
  - Ata
  - Uzak görevler
- Destek bilgileri
  - İletişim bilgileri (ad, telefon numarası, e-posta adresi)
  - Microsoft’un destek, ürün ve/veya müşteri deneyimi ekibi üyeleriyle e-posta yoluyla yapılan tartışmalar
- Erişim denetimi bilgileri 
  - Statik kimlik doğrulayıcılar (müşterinin parolası)
  - Sertifikalar için gizlilik anahtarları 
- Yönetici ve hesap bilgileri
  - Yönetici kullanıcının adı ve soyadı
  - Yönetici kullanıcı adı
  - UPN (e-posta)
  - Telefon numarası
  - Hesap sahibinin e-posta adresi
  - Tüm müşteri BT yöneticilerinin Active Directory kimliği
  - Müşteriyi faturalandırma için ödeme verileri
  - Abonelik anahtarı
- Uygulama envanteri, örneğin
  - uygulama adı
  - sürüm
  - uygulama kimliği
  - size
  - yükleme konumu
  - Uygulama envanteri verileri, yalnızca Yönetici tarafından şirkete ait cihaz olarak işaretlendiğinde veya uyumlu uygulama özelliği açık olduğunda toplanır.  
- Müşteri üçüncü taraf kiracı kimlikleri (Apple KIMLIĞI gibi)
- Cihaz verileri
  - Intune cihaz kimliği
  - Azure Active Directory cihaz kimliği
  - Intune cihaz yönetimi kimliği
  - Kiracı Kimliği
  - Hesap Kimliği
  - EAS cihaz kimliği
  - Platforma özgü kimlikler
  - İOS için AppleID/ıpados cihazları
  - Mac cihazlar için Mac Adresi
  - Windows cihazlar için Windows kimliği
- Yönetilen uygulama bilgileri
  - Yönetilen uygulama kimliği
  - Yönetilen uygulama cihaz etiketi
  - Intune cihaz yönetimi kimliği
  - Azure Active Directory cihaz kimliği
  - Şifreleme anahtarları
- Tüm Intune kiracılarındaki yönetici kullanım verileri (örneğin Yönetici konsoluyla etkileşimdeyken seçilen yönetici denetimleri)
- Kiracı hesap bilgileri (bu verilere Intune dikey penceresinden ulaşılabilir)
  - Kayıtlı cihaz veya kullanıcı sayısı
  - Tanımlı cihaz platformu sayısı  
  - Yüklü cihaz sayısı
  - installedDeviceCount: Uygulamanın yüklü olduğu cihaz sayısı.
  - notApplicableDeviceCount: Uygulamanın kullanılamadığı cihaz sayısı.
  - notInstalledDeviceCount: Uygulamanın kullanılabildiği ancak yüklü olmadığı cihaz sayısı.
  - Pendingınstalldevicecount: uygulamanın geçerli olduğu ve yüklemenin beklediği cihaz sayısı.

## <a name="optional-data"></a>İsteğe bağlı veriler

İsteğe bağlı kategoride yer alan veriler ürün veya hizmet deneyimi için gerekli değildir. Müşteriler isteğe bağlı verilerin toplanmasını denetleyebilir. Intune, müşterilerin isteğe bağlı veri toplamayı kabul etmesini veya geri çevirmesine olanak sağlar. İsteğe bağlı verilerin örnekleri, Intune 'un tanılama ve telemetri için topladığı verilerden oluşur. Yeni ve daha zengin deneyimler için fırsatlar oluşturduğundan, kullanıcıların bu isteğe bağlı verileri paylaşması için önemli nedenler olduğunu düşündüğünüzden emin olun, ancak kullanıcılara bu seçimleri yapma fırsatı sağlamak için önemi anladık. 

İsteğe bağlı tanılama verilerine örnek olarak uygulama kullanım verileri, hata ve performans verileri dahil olabilir. Kurumsal uygulamalar ve hizmetler için tüm Microsoft 365 uygulamalarının kullanımı sırasında Microsoft tarafından toplanan tüm Tanılama verileri, ISO/ıEC 19944:2017 (Section 8.3.3) standardında tanımlanan şekilde belirlenir.

## <a name="certain-end-user-data-or-content-is-never-collected"></a>Belirli Son Kullanıcı verileri veya Içeriği hiçbir şekilde toplanmaz

Intune, bir kullanıcının bir fotoğraf uygulaması veya kamerasından dahil olmak üzere son kullanıcıların çağrı veya Web tarama geçmişini, kişisel e-posta, metin iletilerini, kişileri, kişisel hesaplara, takvim olaylarını veya fotoğraflarını görmesine veya buna izin vermez. Bkz. [cihaz kaydetme ile çalışmaya](../enrollment/device-enrollment.md)başlama.

Veri türleri ve tanımı hakkında daha fazla bilgi için bkz. [Microsoft 'un verileri çevrimiçi hizmetler nasıl kategorilere](https://www.microsoft.com/trust-center/privacy/customer-data-definitions) ayırır. 

## <a name="next-steps"></a>Sonraki adımlar

Intune’un verileri nasıl [depolayıp işlediği](privacy-data-store-process.md) ve [paylaştığı](privacy-data-secure-share.md) hakkında daha fazla bilgi edinin. 
