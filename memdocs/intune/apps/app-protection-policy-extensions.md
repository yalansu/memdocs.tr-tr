---
title: Uzantılar için uygulama koruma ilkeleri
titleSuffix: Microsoft Intune
description: Bu konuda, uzantılar için uygulama koruma ilkesi (APP) açıklanmaktadır.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ecb0e1864fd47cf7aad65fa88de765cb47fce583
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996733"
---
# <a name="protecting-application-extensions"></a>Uygulama uzantılarını koruma

Bu makalede, Microsoft Intune uzantılar için uygulama koruma ilkeleri açıklanmaktadır.

## <a name="add-ins-for-outlook-app"></a>Outlook uygulaması için eklentiler

Outlook eklentileri, popüler uygulamaları e-posta istemcisiyle tümleştirmenize imkan tanır. Outlook için eklentiler Web, Windows, Mac ve Android ve iOS/ıpados için Outlook 'ta kullanılabilir. Intune uygulama SDK 'Sı ve Intune uygulama koruma ilkeleri Outlook eklentilerini yönetme desteğini içermez, ancak kullanımlarını sınırlamak için başka yollar vardır. Eklentiler Microsoft Exchange yoluyla yönetildiğinden, eklentiler kullanıcı için Exchange tarafından kapatılmadığı sürece, kullanıcılar Outlook ile yönetilmeyen eklenti uygulamaları arasında verileri ve iletileri paylaşabilirler.

Son kullanıcılarınızın Outlook eklentilerine erişmesini ve bunları yüklemesini durdurmak isterseniz (bu işlem tüm Outlook istemcilerini etkiler), Exchange yönetim merkezinde rollerde aşağıdaki değişikliklerin yapıldığından emin olun:

- Kullanıcıların Office Mağazası eklentilerini yüklemesini engellemek için, onlardan Marketim rolünü kaldırın.
- Kullanıcıların dışarıdan eklenti yüklemesini engellemek için, onlardan Özel Uygulamalarım rolünü kaldırın.
- Kullanıcıların tüm eklentileri yüklemesini engellemek için, onlardan hem Özel Uygulamalarım rolünü hem de Marketim rolünü kaldırın.

Bu yönergeler Microsoft 365, Exchange 2016, Web 'de Outlook üzerinde Exchange 2013, Windows, Mac ve mobil için geçerlidir.

- [Outlook için eklentiler](/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/add-ins-for-outlook) hakkında daha fazla bilgi edinin.
- [Outlook uygulaması için eklentileri yükleyebilecek ve yönetebilecek kullanıcıları ve yöneticileri belirleme](/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins) hakkında daha fazla bilgi edinin.

## <a name="linkedin-account-connections-for-microsoft-apps"></a>Microsoft uygulamaları için LinkedIn hesap bağlantıları

LinkedIn hesap bağlantıları, kullanıcıların belirli Microsoft uygulamalarında LinkedIn profil bilgilerini görmesini sağlar. Varsayılan olarak, kullanıcılarınız ek LinkedIn bilgilerini görmek için LinkedIn ve Microsoft iş veya okul hesaplarını bağlamayı seçebilir. 

> [!NOTE]
> LinkedIn tümleştirmesi şu anda Birleşik Devletler Kamu müşterileri ve Avustralya, Kanada, Çin, Fransa, Almanya, Hindistan, Güney Kore, Birleşik Krallık, Japonya ve Güney Afrika’da barındırılan Exchange Online posta kutularına sahip olan kuruluşlar için kullanılamamaktadır.

Intune SDK’sı ve Intune uygulama koruma ilkeleri, LinkedIn hesap bağlantılarını yönetme desteği içermez. Ancak bunları yönetmenin başka yolları vardır. Tüm kuruluşunuz için LinkedIn hesabı bağlantılarını devre dışı bırakabilir veya kuruluşunuzda seçili kullanıcı grupları için LinkedIn bağlantılarını etkinleştirebilirsiniz. Bu ayarlar, tüm platformlarda (Web, mobil ve Masaüstü) Microsoft 365 uygulamalar arasında LinkedIn bağlantılarını etkiler. Seçenekleriniz şunlardır:

- Azure portalında kiracınız için LinkedIn hesap bağlantılarını etkinleştirin veya devre dışı bırakın. 
- Grup İlkesini kullanarak kuruluşunuzun Office 2016 uygulamalarında LinkedIn hesabı bağlantılarını etkinleştirin veya devre dışı bırakın.

Kiracınız için LinkedIn tümleştirmesi etkinse kuruluşunuzdaki kullanıcılar LinkedIn ve Microsoft iş veya okul hesaplarını bağladıklarında iki seçenekleri bulunur: 

- İki hesap arasında verileri paylaşmak için izin verebilirler. Bu, LinkedIn hesaplarının Microsoft iş veya okul hesaplarıyla veri paylaşmasına ve Microsoft iş veya okul hesaplarının LinkedIn hesaplarıyla veri paylaşmasına izin verdikleri anlamına gelir. LinkedIn ile paylaşılan veriler çevrimiçi hizmetlerden ayrılır. 
- Yalnızca LinkedIn hesaplarından Microsoft iş ve okul hesaplarına veri paylaşmak için izin verebilirler

Bir kullanıcı, Office eklentilerinde olduğu gibi hesaplar arasında veri paylaşımına izin verirse LinkedIn tümleştirmesi mevcut Microsoft Graph API’lerini kullanır. LinkedIn tümleştirmesi, Office eklentileri için kullanılabilir API’lerin yalnızca bir alt kümesini kullanır ve çeşitli dışlamaları destekler.


|Microsoft Graph izinleri  |Açıklama  |
|---------|---------|
|[Kişiler](/graph/permissions-reference#people-permissions) için okuma izinleri     |Uygulamanın oturum açan kullanıcıyla ilgili kişilerin puanlanmış bir listesini okumasına izin verir. Liste; yerel kişileri, sosyal ağ veya kuruluşunuzun dizinindeki kişileri ve son iletişim kurulan kişileri (e-posta ve Skype gibi) içerebilir.         |
|[Takvimler](/graph/permissions-reference#calendars-permissions) için okuma izinleri     |Uygulamanın kullanıcı takvimlerindeki etkinlikleri okumasına izin verir. Oturum açan kullanıcının takvimindeki toplantıları, zamanlarını, yerlerini ve katılımcıları içerir.         |
|[Kullanıcı Profili](/graph/permissions-reference#user-permissions) için okuma izinleri     |Kullanıcıların uygulamada oturum açmasını sağlar ve uygulamanın oturum açan kullanıcıların profilini okumasına izin verir. Ayrıca uygulamanın oturum açan kullanıcılar için temel şirket bilgilerini okumasına izin verir.         |
|Abonelikler     |Bu kapsam mevcut değil ve henüz kullanılmıyor. Bu, kullanıcının kuruluşu tarafından Microsoft 365 gibi Microsoft uygulamalarına ve hizmetlerine sunulan abonelikleri içerir.         |
|Insights     |Bu kapsam mevcut değil ve henüz kullanılmıyor. Oturum açan kullanıcı hesabıyla ilişkili Microsoft hizmetleri kullanımını temel alan ilgi alanlarını içerir.         |

### <a name="learn-more"></a>Daha fazla bilgi edinin

- [Microsoft uygulamalarınızdaki LinkedIn bilgileri ve özellikleri](https://go.microsoft.com/fwlink/?linkid=850740) hakkında bilgi edinin.
- [Microsoft 365 yol haritası sayfasında](https://products.office.com/en-US/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc)LinkedIn hesap bağlantıları sürümü hakkında bilgi edinin. 
- [LinkedIn hesap bağlantılarını yapılandırma](/azure/active-directory/linkedin-integration) hakkında bilgi edinin.
- Kullanıcıların LinkedIn ve Microsoft iş veya okul hesapları arasında paylaşılan veriler hakkında daha fazla bilgi için, [iş veya okulunuzdaki Microsoft uygulamalarında LinkedIn](https://www.linkedin.com/help/linkedin/answer/84077)'e bakın.

