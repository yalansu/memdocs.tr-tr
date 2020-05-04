---
title: Uygulama bilgilerini ve atamalarını izleme
titleSuffix: Microsoft Intune
description: Kullanıcılara veya cihazlara uygulama atadıktan sonra, uygulamanın durumunu izlemenize yardımcı olması için bu bilgileri kullanın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 64e5133d-1e23-4ee6-b556-f5d32c0e95da
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c505b73b37daefac7027ff6b18f209583db99f0a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80324479"
---
# <a name="monitor-app-information-and-assignments-with-microsoft-intune"></a>Microsoft Intune ile uygulama bilgilerini ve atamalarını izleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune, yönettiğiniz uygulamanın özelliklerini izlemeniz ve uygulama atama durumunu yönetmeniz için birkaç yol sağlar.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar** > **tüm uygulamalar**' ı seçin.
3. Uygulama listesinde, izlenecek uygulamayı seçin. Cihaz durumuna ve kullanıcı durumuna genel bakışı içeren uygulama bölmesini göreceksiniz.

> [!NOTE]
> **Kullanılabilir** olarak dağıtılan Android Mağazası uygulamaları yükleme durumlarını bildirmez.
>
> Android kurumsal iş profili cihazlarına dağıtılan yönetilen Google Play uygulamaları için, Intune kullanarak bir cihazda yüklü olan uygulamanın durum ve sürüm numarasını görüntüleyebilirsiniz. 

## <a name="app-overview-pane"></a>Uygulamaya genel bakış bölmesi

Uygulama bölmesinde, ortamınızdaki bir uygulamanın durumu hakkındaki ayrıntıları gözden geçirebilirsiniz.

### <a name="essentials"></a>Temel Bileşenler
**Temel Parçalar** bölümünde, uygulama hakkında aşağıdaki bilgiler yer alır:

 | **Uygulama ayrıntıları**            | **Açıklama**                                                      |
|------------------------|------------------------------------------------------------------|
| **'In**          | Uygulamanın yayımcısı.                                            |
| **İşletim sistemi**   | Uygulamanın işletim sistemi (Windows, iOS/ıpados, Android, vb.). |
| **Oluşturulan**             | Düzeltmenin oluşturulduğu tarih ve saat. <b>**Note**: Bu tarih değeri, bir BT Yöneticisi uygulama meta verilerini değiştirdiğinde (uygulama kategorisi veya uygulama açıklaması gibi) güncelleştirilir.                        |
| **Atanan**           | Uygulamanın atanıp atanmadığı (**Evet** veya **Hayır**).                  |

### <a name="device-and-user-status-graphs"></a>Cihaz ve kullanıcı durum grafikleri
Grafikler aşağıdaki durumlar için uygulamaların sayısını gösterir:

| **Cihaz durumu**       | **Açıklama**                                       |
|-----------------------|-------------------------------------------------------|
| **Yüklendi**         | Yüklenen uygulamaların sayısı.                         |
| **Yüklü değil**     | Yüklenmemiş uygulamaların sayısı.                     |
| **Başaramadı**            | Başarısız olan yüklemelerin sayısı.                   |
| **Yükleme Bekletiliyor**   | Yüklenme sürecinde olan uygulamaların sayısı. |
| **Uygulanamaz**           | Durumun uygulanamadığı uygulamaların sayısı.            |

> [!NOTE]
> Android LOB uygulamalarının (. APK) **kayıt olmadan veya kaydı yapılmadan kullanılabilir** olarak dağıtılmış, kayıtlı cihazlar için uygulama yükleme durumunu rapor edin. Uygulama yükleme durumu, Intune'a kayıtlı olmayan cihazlar için kullanılamaz.

### <a name="device-install-status"></a>Cihaz yükleme durumu

Menünün **İzleme** bölümünde **Cihaz yükleme durumu**’nu seçtiğinizde cihaz durum listesi gösterilir. Ayrıntı tablosunda aşağıdaki sütunlar vardır:

| **Cihaz sütunu**      | **Açıklama**                                                                                                                                                                                                                                            |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Cihaz adı**      | Cihazı adlandırmaya izin veren platformlarda cihazın adı. Buna izin vermeyen platformlarda ise Intune, diğer özelliklerden bir ad oluşturur. Bu öznitelik başka hiçbir cihazda kullanılamaz.                                                                       |
| **Kullanıcı adı**        | Kullanıcının adı.                                                                                                                                                                                                                                      |
| **Platform**         | Cihazın işletim sistemi (Windows, iOS/ıpados, Android, vb.).                                                                                                                                                                                           |
| **Sürüm**          | Uygulamanın sürüm numarası. İş kolu (LOB) uygulamaları ve İş İçin Microsoft Store uygulamaları için, uygulamanın tam sürüm numarası gösterilir. Tam sürüm numarası uygulamanın belirli bir yayınını tanımlar. Numara _Sürüm_(_Derleme_) olarak görünür. Örneğin, 2.2(2.2.17560800). Standart Store uygulamaları için sürüm bilgisi gösterilmez. |
| **Durum**           | Uygulamanın durumu.                                                                                                                                                                                                                                     |
| **Durum ayrıntıları**   | Durumun ayrıntıları.                                                                                                                                                                                                                                     |
| **Son iade etme**    | Cihazın Intune ile son eşitlenme tarihi.                                                                                                                                                                                                                  |


### <a name="user-install-status"></a>Kullanıcı yükleme durumu

Menünün **İzleme** bölümünde **Kullanıcı yükleme durumu**’nu seçtiğinizde kullanıcı durum listesi gösterilir. Ayrıntı tablosunda aşağıdaki sütunlar vardır:

| **Kullanıcı sütunu**     | **Açıklama**                           |
|---------------------|-------------------------------------------|
| **Adı**            | Kullanıcının Azure Active Directory'deki adı.         |
| **Kullanıcı adı**       | Kullanıcının benzersiz adı.              |
| **Yüklemeler**   | Kullanıcı tarafından yüklenen uygulamaların sayısı. |
| **Kesil**        | Kullanıcı için başarısız olan uygulama yüklemelerinin sayısı.     |
| **Yüklü değil**   | Kullanıcı tarafından yüklenmeyen uygulamaların sayısı. |


## <a name="next-steps"></a>Sonraki adımlar

- Intune verilerinizle çalışma hakkında daha fazla bilgi edinmek için bkz. [Intune Veri Ambarı'nı kullanma](../developer/reports-nav-create-intune-reports.md).
- Uygulama yapılandırma ilkeleri hakkında bilgi edinmek için bkz. [Intune için uygulama yapılandırma ilkeleri](app-configuration-policies-overview.md).
