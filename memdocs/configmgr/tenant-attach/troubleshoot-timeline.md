---
title: Cihaz zaman çizelgesinde sorun giderme
titleSuffix: Configuration Manager
description: Configuration Manager kiracı iliştirme için cihaz zaman çizelgesinde sorun giderme
ms.date: 09/8/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 54a58548-45f3-4f75-93d6-d2fd96227e6a
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 979ec6f081a318886eda9eeac91c16adc635701d
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564364"
---
# <a name="troubleshoot-the-timeline-for-devices-uploaded-to-the-admin-center-preview"></a><a name="bkmk_timeline"></a> Yönetim merkezine yüklenen cihazlar için zaman çizelgesinde sorun giderme (Önizleme)
<!--CM7141381, IN7552762 pubpreview Sept8, 2020 -->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Endpoint Manager Yönetim Merkezi 'nde cihaz zaman çizelgesinde sorun gidermek için aşağıdakileri kullanın:

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.


## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_common"></a> Microsoft Endpoint Manager Yönetim Merkezi 'ndeki yaygın hatalar

Microsoft Endpoint Manager yönetim merkezinden zaman çizelgesini görüntülerken veya eşitlerken, bu hatalardan birinde çalıştırabilirsiniz.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_401"></a> Gerekli Yapılandırma Azure Active Directory eksik

**Hata iletisi:** Gerekli Yapılandırma Azure Active Directory eksik. Configuration Manager sitesini Azure kiracınıza iliştirdiğinizden ve uygun Kullanıcı rolünü Azure AD 'ye atadığınızdan emin olun.

**Olası nedenler:**

- [Azure AD Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) ve [Active Directory Kullanıcı bulmanın](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) yapılandırıldığından ve kullanıcının her ikisiyle de bulunduğundan emin olun.
- Kullanıcı hesabının Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü eksik olabilir. Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir. Bu izne yapılan değişikliklerin etkili olması bir saate kadar sürebilir.

### <a name="unable-to-get-timeline-information"></a><a name="bkmk_403"></a> Zaman çizelgesi bilgisi alınamıyor

**Hata iletisi:** Zaman çizelgesi bilgileri alınamıyor. Azure AD ve AD Kullanıcı bulmanın yapılandırıldığından ve kullanıcının her ikisiyle de bulunduğundan emin olun. Kullanıcının Configuration Manager uygun izinlere sahip olduğunu doğrulayın.

**Olası nedenler:**

Hesabın aşağıdaki izinlere sahip olduğunu doğrulayın:
- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Configuration Manager içinde **koleksiyon** altında **kaynağı oku** izni.
- Configuration Manager içinde **koleksiyon** altında **kaynağı bilgilendir** izni.
   - Bu izin, en son olayları eşitleyebilmek için gereklidir.

### <a name="unable-to-get-timeline-information"></a><a name="bkmk_404"></a> Zaman çizelgesi bilgisi alınamıyor

**Hata iletisi:** Cihaz bilgileri henüz Configuration Manager 'den Microsoft Endpoint Manager yönetim merkezine eşitlenmedi. Siteyi Azure kiracınıza iliştirdikten 15 dakikaya kadar bekleyin.

**Olası çözüm:** Yaklaşık 15 dakika bekleyin ve sorun otomatik olarak çözümlenmelidir.

### <a name="unexpected-error-occurred"></a><a name="bkmk_500"></a> Beklenmeyen bir hata oluştu

**Hata iletisi:** Beklenmeyen bir hata oluştu

**Olası nedenler:**

- [Güncelleştirme paketi](https://support.microsoft.com/help/4560496/) ve konsolunun ilgili sürümü yüklü olan en az Configuration Manager sürüm 2002 olduğunu doğrulayın.
- Çok sayıda olay varsa (10.000 'den fazla, yaklaşık olarak) ve birden çok arama hızlı bir şekilde isteniyorsa, beklenmeyen bir hata almak mümkündür. Arama sonuçlarının [zaman aşımını](#bkmk_timeout)de görebilirsiniz.

### <a name="getting-results-timed-out"></a><a name="bkmk_timeout"></a> Sonuçların alınması zaman aşımına uğradı

**Hata iletisi:** Sonuçların alınması zaman aşımına uğradı. Configuration Manager hizmet bağlantı noktasının çalışır durumda olduğundan ve buluta bir bağlantı bulunduğundan emin olun.

**Olası neden:** Çok sayıda olay varsa (10.000 'den fazla) ve hızlı bir şekilde birden çok arama isteniyorsa, zaman aşımı görmeniz mümkündür. [Beklenmeyen bir hata](#bkmk_500)da görebilirsiniz.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="boundary-group-id-is-used-rather-than-the-name"></a>Sınır grubu KIMLIĞI, ad yerine kullanılıyor

**Senaryo:** Configuration Manager sürüm 2002 çalıştırıyorsanız ve bir cihaz sınır gruplarını değiştirirse, olay iletisi adı yerine sınır grubu KIMLIĞINI gösterir.

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Sonraki adımlar

[Kiracı eklemeyle ilgili sorunları giderme](troubleshoot.md)