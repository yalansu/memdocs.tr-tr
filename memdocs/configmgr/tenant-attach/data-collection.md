---
title: Kiracı veri toplamayı bağlama
titleSuffix: Configuration Manager
description: Kiracı iliştirme özellikleri için Configuration Manager topladığı Tanılama verileri hakkında bilgi edinin.
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 4b305a71-9ad8-4332-9692-d51554158981
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00a01e4ceadc716a42381999b2e4603bcbe55524
ms.sourcegitcommit: eaa077aa028a76a4873e4aa7437888f901a7e77f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90767806"
---
# <a name="tenant-attach-data-collection"></a>Kiracı veri toplamayı bağlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!-- 6505626 -->
Configuration Manager sitenizi Microsoft Intune kiracısıyla iliştirçalıştığınızda, site Microsoft 'a ek veriler gönderir. Bu makalede gönderilen veriler özetlenmektedir.

Kiracı iliştirme, Microsoft Endpoint Manager yönetici merkezini konsolunuza getirir. Mimari, Configuration Manager sitesinin cihaz ve kullanıcı hakkındaki verileri Intune kiracınızla eşitlemesine olanak tanır. Daha sonra, etkin eşitleme olmadan bulut konsolundaki şirket içi ortamınızdan verileri sorgulayabilir ve gerçek zamanlı olarak sunabilirsiniz. Şirket içi sitenizden büyük geçici veriler getirebilir. Kiracı iliştirme, bulut konsolunda etkili güncel bilgiler sağlamak için bu yöntemlerin bir karışımını kullanır.

> [!IMPORTANT]
> Microsoft veri işleme ilkeleri [Microsoft Intune Gizlilik bildiriminde](/legal/intune/microsoft-intune-privacy-statement)açıklanmaktadır. Yalnızca sizin imzaladığınız hizmetleri sağlamak için müşteri verilerinizi kullanıyoruz.
>
> Her nedenden dolayı hizmetimizin tarafından herhangi bir üçüncü taraf için toplanan verileri salamadık.
>
> Veriler, kiracı iliştirme bağlı deneyimi için gereken tüm hizmet verileri olur. Gerekli hizmet verileri aşağıdaki bilgileri içerir:
>
> - Oluşturduğunuz içerik olan **Müşteri içeriği**. Örneğin, LOB uygulamanızın adı.
> - **İşlevsel veriler**, görevi gerçekleştirmek için bağlı bir deneyim için gereken bilgileri içerir. Örneğin, uygulamayla ilgili yapılandırma bilgileri.
> - Hizmet **Tanılama verileri**, hizmeti güvenli tutmak için gereken veriler, güncel ve beklendiği gibi gerçekleştiriliyor. Bu veriler bağlı deneyimle tamamen ilişkili olduğundan, gerekli veya isteğe bağlı tanılama veri düzeylerinden ayrıdır.

Microsoft Uç Nokta Yöneticisi üç kategoride yer alan bilgileri toplar:

- **Tanımlanan veri**: Microsoft Endpoint Manager tarafından toplanan verilerin çoğu veri tanımlı değildir. Bu tür veriler bir kullanıcı, cihaz veya uygulamaya bağlıdır ve yönetimin yapısı gereği gereklidir. Tanımlanan veriler, bir kullanıcının cihazını ve uygulamalarını yönetmek için kullanılır.

- **Sahte veriler**: Bu veriler benzersiz bir tanımlayıcı ile ilişkilendirilir. Genellikle sistem tarafından oluşturulan bir sayı, tek bir kişiyi tanımlayamıyorum. Microsoft Uç Nokta Yöneticisi bu verileri Enterprise hizmetini sunmak için kullanır.

- **Toplanan veriler**: Bu veriler, cihaz sayısı veya Microsoft Endpoint Manager Yönetim merkezinde kullandığınız denetimleri gibi kullanım istatistikleridir.

Aşağıdaki bölümler, kiracının buluta eşitlendiği veri türlerinin örneklerini sağlar. Bunlar işlevsel varlığa göre gruplandırılır, bu sayede kullanmakta olduğunuz belirli özellikleri gözden geçirebilirsiniz.

## <a name="applications"></a>Uygulamalar
<!-- 6502080 -->

Her Windows Installer (MSI) dağıtım türü için:

- **ProductName**: uygulamanın adı
- **Yayımcı**: yazılımı yayımlayan varlık
- **Sürüm**: uygulamanın sürümü
- **Productlanguage**: uygulamanın dil kodu
- **ProgramID**: dağıtım türü için bir tanımlayıcı

## <a name="device-sync"></a>Cihaz eşitleme
<!-- 6505639 -->

Her cihaz için:

- **SMSID**: Configuration Manager hiyerarşinizin benzersiz tanımlayıcısı
- **Aadtenantıd**: Azure Active Directory (Azure AD) kiracınızın benzersiz tanımlayıcısı
- **Aaddeviceıd**: Azure AD 'de cihazın benzersiz tanımlayıcısı
- **Ad**: cihazın ana bilgisayar adı
- **Deviceos**: cihazın işletim sisteminin adı. Örneğin, `Microsoft Windows NT Server 6.3`
- **Deviceosbuild**: cihazın işletim sisteminin derleme sürümü. Örneğin, `10.0.19041`
- **Aadprimaryuserıd**: CIHAZıN Azure AD 'deki birincil kullanıcısının benzersiz tanımlayıcısı
- **Model**: cihaz modeli
- **Üretici**: cihaz üreticisi
- **SerialNumber**: cihaz seri numarası
- **DomainNames**: cihaz için tüm etki alanı adları
- **SKU**

## <a name="windows-defender-advanced-threat-protection-atp"></a>Windows Defender Gelişmiş Tehdit Koruması (ATP)
<!-- 6505652 -->

ATP İlkesi dağıtımı için seçtiğiniz herhangi bir koleksiyon için:

- **CollectionId**: koleksiyonun benzersiz tanımlayıcısı. Örneğin, `ABC00014`
- **CollectionName**: koleksiyonun adı. Örneğin, `All Windows servers`
- **CollectionType**: bir cihaz veya Kullanıcı koleksiyonu olduğunu tanımlar.
- **Sayaçhedeflenen**: Bu ilkeyle hedeflediğiniz cihazların sayısı
- **Sayaçuyumlu**: Bu ilkeyle uyumlu olan cihazların sayısı
- **Sayaçuyumsuz**: Bu ilkeyle uyumlu olmayan cihazların sayısı
- **Countfailed**: Bu ilkeyi işleyeme başarısız olan cihazların sayısı
- **CountActivated**
- **Countenzorlamalı**

## <a name="see-also"></a>Ayrıca bkz.

Configuration Manager toplanan veriler hakkında daha fazla genel bilgi için bkz. [Configuration Manager Için tanılama ve kullanım verileri](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

İlgili gizlilik yönleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Microsoft Intune Gizlilik bildirimi](/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 ve gizlilik uyumluluğu](/windows/privacy/windows-10-and-privacy-compliance)
- [Lisans hüküm ve belgeler](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Microsoft Azure veri merkezlerinde güvenlik ve Gizlilik](https://azure.microsoft.com/global-infrastructure/)  
- [Güvenilir bulutta güven](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Güven Merkezi](https://www.microsoft.com/trustcenter)  
