---
title: Tanılama ve kullanım verileri hakkında SSS
titleSuffix: Configuration Manager
description: Configuration Manager için tanılama ve kullanım verileri hakkında sık sorulan sorular
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709547"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Tanılama ve kullanım verileri hakkında sık sorulan sorular

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Configuration Manager tanılama ve kullanım verileri hakkında sık sorulan soruların yanıtlarını sağlar.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a>Tanılama ve kullanım verilerini kapatabilir miyim?

Sitenin veri gönderdiği zaman yönetimine yardımcı olmak için, hizmet bağlantı noktasını çevrimdışı modda kullanın. Ardından, verileri el ile göndermek için hizmet bağlantı aracını kullanın. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Hizmet bağlantı noktası hakkında](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Hizmet bağlantısı aracını kullanma](../../servers/manage/use-the-service-connection-tool.md)

Windows 10 ' un yeni sürümlerini ve Microsoft Intune gibi bulut hizmetlerini desteklemek için, geçerli Configuration Manager dalını düzenli olarak güncelleştirmeniz gerekir. Microsoft, en azından temel düzeyde tanılama ve kullanım verisi gerektirir. Bu veriler, ürünü güncel tutmak, güncelleştirme deneyimini geliştirmek ve ürünün kalitesini ve güvenliğini geliştirmek için kullanılır.

Hizmet bağlantı noktası çevrimdışı moddayken hizmete veri gönderilmez. Çevrimiçi moda geçtiğinizde veya hizmet bağlantı aracını kullandığınızda, güncelleştirmeleri denetlemek için hizmetine veri gönderilir.

Configuration Manager topladığı veri düzeyini de seçebilirsiniz. Daha fazla bilgi için bkz. [Tanılama kullanım verileri düzeyleri](levels-overview.md).

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> Veri saklama süresi nedir?

Microsoft Configuration Manager tanılama ve kullanım verilerini bir yıl boyunca depolar.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a>Tanılama ve kullanım verileri, kurulum çalıştırıldığında gönderilir mi?

Hayır. Tanılama ve kullanım verileri yalnızca site yüklendikten ve çalışır duruma geldikten sonra gönderilir.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> Veriler ne sıklıkla gönderiliyor?

SQL saklı yordamları, siteyi yüklediğiniz tarihten itibaren her yedi günde bir çalışır.

- Çevrimiçi modda, hizmet bağlantı noktası sorgular çalıştırıldıktan sonra verileri karşıya yükler.

- Çevrimdışı modda, verileri karşıya yüklemek için hizmet bağlantısı aracını kullanırsınız. (Bu veriler başlangıçta, siteyi yükledikten sonra yedi güne kadar çevrimdışı kullanım için kullanılabilir değildir.)  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> Veriler bir ağ haritası oluşturmak için kullanılabilir mi?

Hayır. Bu veriler, IP adresleri veya ayrıntılı coğrafi bilgiler gibi herhangi bir ağ ayrıntısı içermez. Daha fazla bilgi için bkz. [Tanılama kullanım verileri düzeyleri](levels-overview.md#bkmk_versions)ve kullanmakta olduğunuz sürüm için daha fazla ayrıntı bulma.

Veriler, her sitenin saat dilimi bilgisini içerir. Bu bilgiler, bir hiyerarşideki sitelerin geniş coğrafi konumu ve küresel dağılımı hakkında öngörüler sağlayabilir.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a>Verileri özel SQL tablolarında görebilmeniz gerekir mi?

Hayır. Configuration Manager, SQL saklı yordamları aracılığıyla tanılama ve kullanım verilerini toplar. Bu saklı yordamlar veritabanındaki varsayılan ürün tablolarına karşı çalışır. Bu SQL tablolarının tümüne **TEL_** ön eki eklenir. SQL şeması algılama sorgusunun bir parçası olarak, bilinen varsayılan değerlerle karşılaştırmak için tüm tablo adlarının karma değerleri oluşturulur. Bu davranış, veritabanında özel tabloların mevcut olduğunu belirler. Özel tabloların varlığı, Microsoft 'un veritabanı şemasını varsayılan olarak genişletmiş olduğunu bildirir. Bu tablolar içinde depolanan verilerin hiçbirini içermez.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a>Diğer veritabanlarını görebilir misiniz?

Hayır. Veri toplamaya yönelik saklı yordamlar Configuration Manager site veritabanıyla sınırlıdır. Microsoft diğer veritabanlarının adlarını veya diğer veritabanlarındaki verileri göremez.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a>Diğer tümleşik bulut hizmetlerine gönderilen veriler midir?

Evet, bu hizmetleri Configuration Manager ile tümleştirdiğinizde. Tüm bulut hizmetleri etkileşiminin bir parçası olarak Configuration Manager, bu hizmete bazı veriler gönderir. Bu veriler, bu bulut hizmetine özeldir ve Configuration Manager tanılama ve kullanım verilerinden ayrıdır. Başka bir bulut hizmetiyle etkileşime göre kullanılan belirli veriler hakkında daha fazla bilgi için, bu hizmet için belgelere bakın.

Örneğin, aşağıdaki bulut Hizmetleri Microsoft Endpoint Manager 'ın bir parçasıdır:

- [Masaüstü Analizi veri gizliliği](../../../desktop-analytics/privacy.md)
- [Intune’da gizlilik ve kişisel veriler](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Windows Autopilot gereksinimleri](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a>Kişisel verileri toplamak Configuration Manager mı?

Hayır. Yapılandırma kişisel verileri veya müşteri verilerini toplamaz veya iletmez. Bu, doğrudan dağıttığınız, yönettiğiniz ve işletebilmeniz gereken şirket içi bir üründür. Microsoft tarafından toplanan tanılama ve kullanım verileri, gelecekteki sürümlerin yükleme deneyimini, kalitesini ve güvenliğini geliştirir.

Configuration Manager verileri hakkında daha fazla bilgi için bkz. [Tanılama kullanım verileri düzeyleri](levels-overview.md).
