---
title: Microsoft Intune-Azure 'da Windows 10 için teslim Iyileştirme ayarları | Microsoft Docs
description: Intune ile yönettiğiniz Windows 10 cihazlarının teslim Iyileştirmesi kullanma şeklini yapılandırın. Intune 'da, güncelleştirmeleri Internet 'ten yüklemek için bir cihaz yapılandırma profili oluşturun. Ayrıca bkz. var olan güncelleştirme halkalarını teslim Iyileştirme profiliyle değiştirme.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 3ffef32f4f33e79b25145dd4c0257b8a5bcfd32a
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913775"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Microsoft Intune teslim Iyileştirme ayarları

Intune ile, bu cihazlar uygulamaları ve güncelleştirmeleri indirdiğinizde bant genişliği tüketimini azaltmak için Windows 10 cihazlarınız için teslim Iyileştirme ayarlarını kullanın. Cihaz yapılandırma profillerinizin bir parçası olarak teslim Iyileştirmesini yapılandırın.  

Bu makalede, teslim Iyileştirme ayarlarının cihaz yapılandırma profilinin bir parçası olarak nasıl yapılandırılacağı açıklanır. Bir profil oluşturduktan sonra, bu profili Windows 10 cihazlarınıza atar veya dağıtabilirsiniz.

Intune 'un desteklediği teslim Iyileştirme ayarlarının listesini görüntülemek için, bkz. [Intune Için teslim iyileştirme ayarları](delivery-optimization-settings.md).  

Windows 10 ' da teslim Iyileştirmesi hakkında bilgi edinmek için Windows belgelerindeki [teslim iyileştirme güncelleştirmeleri](/windows/deployment/update/waas-delivery-optimization) bölümüne bakın.  

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. Aşağıdaki özellikleri girin:

   - **Platform**: **Windows 10 ve üstünü**seçin.
   - **Profil**: **teslim iyileştirme**'yi seçin.

4. **Oluştur**’u seçin.

5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

   - **Ad**: Yeni profil için açıklayıcı bir ad girin.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları** sayfasında, güncelleştirmelerin ve uygulamaların nasıl indirilmesini istediğinizi tanımlayın. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Intune Için teslim iyileştirme ayarları](delivery-optimization-settings.md).

   Ayarları yapılandırmayı bitirdiğinizde **İleri**' yi seçin.

8. Scope **(Etiketler)** sayfasında kapsam **etiketleri Seç ' i seçerek profile** kapsam etiketleri atayın *Select tags* .
  
   Devam etmek için **İleri** seçeneğini belirleyin.

9. **Atamalar** sayfasında, bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

   **İleri**’yi seçin.

10. **Uygulanabilirlik kuralları** sayfasında, bu profilin atanmış gruplar içinde nasıl uygulanacağını tanımlamak için **kural**, **özellik**ve **değer** seçeneklerini kullanın.

11. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Profil oluşturulur ve listede gösterilir.

Her cihazın bir sonraki denetimi sırasında ilke uygulanır.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Windows 10 güncelleştirme halkalarından teslim Iyileştirmeyi kaldır

Teslim Iyileştirme daha önce yazılım güncelleştirme halkalarının bir parçası olarak yapılandırılmıştır. Dağıtım Iyileştirme ayarları, Şubat 2019 ' den itibaren cihazlara yazılım güncelleştirme teslimini etkileyen ek ayarlar içeren bir teslim Iyileştirme cihaz yapılandırma profilinin bir parçası olarak yapılandırılır. Henüz yapmadıysanız, dağıtım Iyileştirme ayarını güncelleştirme halkalarından *Yapılandırılmadı*olarak ayarlayarak kaldırın ve daha fazla kullanılabilir seçenek aralığını yönetmek Için bir teslim iyileştirme profili kullanın.

1. Teslim Iyileştirme cihaz yapılandırma profili oluşturma:

    1. Microsoft Endpoint Manager Yönetim Merkezi 'nde, **cihazlar**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
    2. Aşağıdaki özellikleri girin:

        - **Platform**: **Windows 10 ve üstünü**seçin.
        - **Profil**: **teslim iyileştirme**'yi seçin.

    3. **Oluştur**’u seçin.
    4. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

        - **Ad**: Yeni profil için açıklayıcı bir ad girin.
        - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

    5. **İleri**’yi seçin.
    6. **Yapılandırma ayarları**  >  **indirme modu**' nda, cihazlarınıza uyguladığınız ayarları değiştirmek istemediğiniz *takdirde* , var olan yazılım güncelleştirme halkası tarafından kullanılan modu seçin. Seçenekleriniz şunlardır:

        - **Yapılandırılmadı**
        - **Yalnızca HTTP, eşleme yok**
        - **Aynı NAT 'nin arkasında eşleme ile HTTP karıştırılmış**
        - **Özel bir Grup genelinde eşleme ile HTTP karıştırılmış**
        - **Internet eşlemesi ile HTTP karıştırılmış**
        - **Eşleme olmadan basit indirme modu**
        - **Atlama modu**

    7. Yönetmek istediğiniz [diğer ayarları](delivery-optimization-settings.md) yapılandırın ve profili oluşturmaya devam edin.

        **Atamalar**' da, bu yeni profili var olan yazılım güncelleştirme halkası ile aynı cihazlara ve kullanıcılara atayın. Daha fazla bilgi için bkz. [profili atama](device-profile-assign.md).

2. Mevcut yazılım halkasını yapılandırmayı geri al:

    1. Microsoft Endpoint Manager Yönetim Merkezi 'nde Windows 10 güncelleştirme halkaları > **yazılım güncelleştirmeleri** ' ne gidin.
    2. Listeden güncelleştirme halkasını seçin.
    3. Ayarlar ' da **teslim iyileştirme indirme modunu** **Yapılandırılmadı**olarak ayarlayın.
    4. **Tamam**  >  Değişikliklerinizi **kaydedin** .

## <a name="next-steps"></a>Sonraki adımlar

[Profili atadıktan](device-profile-assign.md)sonra durumunu [izleyin](device-profile-monitor.md) .

Intune için [teslim iyileştirme ayarlarını](delivery-optimization-settings.md) görüntüleyin.