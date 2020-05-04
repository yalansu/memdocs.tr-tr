---
title: Cihazları otomatik olarak koleksiyonlara ayırma
titleSuffix: Configuration Manager
description: Cihazları otomatik olarak koleksiyonlara kategorilere ayırın.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714314"
---
# <a name="automatically-categorize-devices-into-collections"></a>Cihazları otomatik olarak koleksiyonlara ayırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Intune ile Configuration Manager kullanırken cihazları otomatik olarak cihaz koleksiyonlarına yerleştirmek için kullanılabilecek cihaz kategorileri oluşturabilirsiniz. Daha sonra kullanıcıların Intune 'A cihaz kaydettiğinde bir cihaz kategorisi seçmesi gerekir. Configuration Manager konsolundan bir cihaz kategorisini değiştirebilirsiniz.

> [!IMPORTANT]
>  Bu yetenek, Microsoft Intune ve sonraki sürümlerin **haziran 2016** sürümüyle birlikte çalışarak. Bu yordamları denemeden önce bu sürüme güncelleştirildiğinden emin olun.

## <a name="create-device-categories"></a>Cihaz kategorileri oluşturma

1.  **Varlıklar ve uyum** > **genel bakış** > **Cihaz Koleksiyonları**' na gidin.
2.  **Giriş** sekmesinde, **Cihaz Koleksiyonları** grubunda, **cihaz kategorilerini Yönet**' i seçin.
3.  Kategorileri oluşturun, düzenleyin veya kaldırın.

## <a name="associate-a-collection-with-a-device-category"></a>Bir koleksiyonu bir cihaz kategorisiyle ilişkilendir

Bir koleksiyonu bir cihaz kategorisiyle ilişkilendirdiğinizde, bu kategorideki tüm cihazlar koleksiyona eklenir. Bir cihaz kategorisi kuralını, **Tüm sistemler**gibi yerleşik bir koleksiyona ekleyemezsiniz.

1.  Bir cihaz koleksiyonunun **Özellikler** iletişim kutusunun **Üyelik kuralları** sekmesinde **kural** > **cihaz kategorisi kuralı**Ekle ' yi seçin.
2.  **Cihaz kategorilerini Seç** iletişim kutusunda, koleksiyondaki tüm cihazlara uygulanacak bir veya daha fazla cihaz kategorisi seçin.

## <a name="change-the-category-of-a-device"></a>Bir cihazın kategorisini değiştirme

1.  **Varlıklar ve uyum** > **genel bakış** > **cihazlarında**, **cihazlar** listesinden bir cihaz seçin.
2.  **Giriş** sekmesinde, **cihaz** grubunda, **Kategoriyi Değiştir**' i seçin.
3.  Bir kategori seçin, sonra **Tamam**' ı seçin.

## <a name="view-which-category-a-device-belongs-to"></a>Bir cihazın ait olduğu kategoriyi görüntüleme

**Varlıklar ve uyumluluk** > **genel bakış** > **cihazlarında**, **cihazlar** listesinde, kategori **cihaz kategorisi** sütununda görüntülenir.

**Cihaz kategorisi** sütunu görüntülenmiyorsa, **cihazlar** listesindeki sütunlardan birinin başlığına ( **ad**gibi) sağ tıklayın ve ardından **cihaz kategorisi**' ni seçin.

Bir cihaza bir cihaz atarsanız ve daha sonra kategoriyi silerseniz, **Microsoft Intune kullanıcı başına kaydedilen cihazların rapor listesi** , kategori adı yerine **cihaz KATEGORISI** sütununda bir GUID görüntüler.
