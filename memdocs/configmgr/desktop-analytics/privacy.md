---
title: Masaüstü Analizi veri gizliliği
titleSuffix: Configuration Manager
description: Masaüstü Analizi Müşteri verileri gizliliğine kaydedildi
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 34005a63b372198bbc2e3079f8ab560ef6b2b791
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795655"
---
# <a name="desktop-analytics-data-privacy"></a>Masaüstü Analizi veri gizliliği

Masaüstü analizi, müşteri verileri gizliliğine tam olarak kaydedilir, bu, bu adalar üzerinde ortalama:

- **Saydamlık:** Windows Tanılama olaylarını tam belgeliyoruz. Bunları şirketinizin güvenlik ve uyumluluk ekipleriyle birlikte gözden geçirin. Windows tanılama veri Görüntüleyicisi, belirli bir cihazdan gönderilen tanılama verilerini görmenizi sağlar. Daha fazla bilgi için bkz. [Tanılama veri görüntüleyicisine genel bakış](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Denetim:** Microsoft ile paylaşılacak tanılama verilerinin düzeyini denetlersiniz. Windows 10, sürüm 1709, gelişmiş tanılama verilerini masaüstü analizi için gereken en düşük düzeyde sınırlamak üzere yeni bir ilke ekler.  

- **Güvenlik:** Microsoft, verilerinizi güçlü güvenlik ve şifrelemeyle korur.  

- **Güven:** Masaüstü analizi, Microsoft [Gizlilik bildirimi](https://privacy.microsoft.com/privacystatement) ve [çevrimiçi hizmet koşulları](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)'nı destekler.  

Daha fazla bilgi için, [Microsoft 'un GDPR altında işlemcinin olduğu Windows Hizmetleri](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr)bölümüne bakın.<!-- 5353168 -->

## <a name="data-flow"></a>Veri akışı

Aşağıdaki çizimde, tanılama verilerinin tanılama veri hizmeti, geçici depolama ve Log Analytics çalışma alanınıza göre ayrı cihazlardan nasıl akabileceği gösterilmektedir:

![Cihazlardan tanılama verilerinin akışını gösteren diyagram](media/da-data-flow.png)

1. Azure portal oturum açıp masaüstü analizine ekleyebilirsiniz. Configuration Manager ile bağlantı kurmak için Azure AD uygulaması oluşturursunuz. Masaüstü analizlerini ayarlarken, seçtiğiniz konumda bir Azure Log Analytics çalışma alanı oluşturursunuz.  

2. Configuration Manager bağlanıp cihazları Kaydet  

    1. Configuration Manager ' de masaüstü Analizi bulut hizmetini Azure AD uygulama ayrıntıları ile yapılandırırsınız.  

    2. 15 dakika içinde Configuration Manager, kiracı KIMLIĞINIZI kullanarak aşağıdaki verileri masaüstü analizi ile eşitler. Bu işlem her saat yinelenir.

      - [Dağıtım planları oluşturmak](create-deployment-plans.md)için gereken cihaz koleksiyonları hakkında bilgiler. Bu bilgiler koleksiyon KIMLIĞI, hiyerarşi KIMLIĞI, koleksiyon adı ve cihaz sayısını içerir. 
      - [Cihazları kaydetmek](enroll-devices.md)için gereken bilgiler. Bu bilgiler koleksiyon KIMLIĞI, SMS benzersiz tanımlayıcı, işletim sistemi derleme sürümü, cihaz adı ve seri numarası içerir.
      - [İzleyici bağlantısı sistem durumu](monitor-connection-health.md) panosundan bilgi. Bu bilgiler, sistem durumu başına cihaz sayısını ve cihaz özelliklerini içerir.
      - Dağıtım planları hakkında, koleksiyon KIMLIĞINI, dağıtım KIMLIĞINI, pilot veya üretim dağıtım türünü ve yükseltme kararı başına cihaz sayısını içeren bilgiler.

    3. Configuration Manager, hedef koleksiyondaki cihazların ticari KIMLIĞINI, tanılama veri düzeyini ve diğer ayarlarını belirler. Bu yapılandırma, masaüstü Analizi çalışma alanınızda görünecek cihazları belirler.  

    4. Uyumluluk güncelleştirmelerini tüm hedef cihazlara dağıtırsınız.  

3. Cihazlar, tanılama verilerini Windows için Microsoft Tanılama Veri Yönetimi hizmetine gönderir. Tüm Tanılama verileri HTTPS üzerinden şifrelenir ve cihazdan bu hizmete aktarım sırasında sertifika sabitleme kullanır. Microsoft Veri Yönetimi hizmeti Birleşik Devletler barındırılır.

      - Uygulama hataları, çekirdek hataları, yanıt vermeyen uygulamalar ve uygulamaya özgü diğer sorunlar, uygulamaya özgü sorun raporlarını Microsoft 'a göndermek için Windows Hata Bildirimi API kullanır. Bu veri akışı hakkında özel ayrıntılar için [wer kullanma](https://docs.microsoft.com/windows/win32/wer/using-wer) bölümüne bakın.
      
4. Her gün Microsoft, BT odaklı öngörülerin bir anlık görüntüsünü üretir. Bu anlık görüntü, Windows 'daki tanılama verilerini kayıtlı cihazların girişinde birleştirir. Bu işlem yalnızca masaüstü Analizi tarafından kullanılan geçici depolamada gerçekleşir. Geçici depolama, Birleşik Devletler Microsoft veri merkezlerinde barındırılır. Tüm veriler SSL (HTTPS) ile şifrelenmiş bir kanal üzerinden gönderilir. Anlık görüntüler ticari KIMLIĞE göre ayrılmış.  

5. Anlık görüntüler daha sonra Azure Log Analytics çalışma alanınıza kopyalanır. Bu veri aktarımı, Log Analytics bir özelliği olan Web kancası alma protokolü aracılığıyla HTTPS üzerinden yapılır. Masaüstü analizlerinin Log Analytics depolama alanınızı okuma veya yazma izni yoktur. Masaüstü analizi, paylaşılan erişim imzası (SAS) URI 'SI ile Web kancası API 'sini çağırır. Ardından Log Analytics, HTTPS üzerinden depolama tablolarından verileri alır.

6. Masaüstü analizi, girişinizi Log Analytics depolama alanına depolar. Bu yapılandırmalara dağıtım planları ve yükseltme ve önem için varlık kararları dahildir.  

## <a name="other-resources"></a>Diğer kaynaklar

Gizlilik açısından ilgili sık sorulan sorular için bkz. [gızlılık SSS](faq.md#privacy).

İlgili gizlilik yönleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Windows 10 ve BT karar mekanizmaları için GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7, Windows 8 ve Windows 8.1 Appraiser tanılama veri olayları ve alanları](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, sürüm 1809 temel düzey Windows Tanılama olayları ve alanları](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Masaüstü Analizi tarafından kullanılan Windows 10, sürüm 1709 Geliştirilmiş tanılama veri olayları ve alanları](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Windows Kurulumu hata bildirimi](https://docs.microsoft.com/windows/deployment/upgrade/windows-error-reporting)

- [Tanılama veri görüntüleyicisine genel bakış](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Lisans hüküm ve belgeler](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Log Analytics veri güvenliği](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Microsoft Azure veri merkezlerinde güvenlik ve Gizlilik](https://azure.microsoft.com/global-infrastructure/)  

- [Güvenilir bulutta güven](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Güven Merkezi](https://www.microsoft.com/trustcenter)  

- [Gizlilik kalkanı](https://www.privacyshield.gov/)  

Masaüstü analizinden ayrı olarak, Configuration Manager tanılama ve kullanım verilerini Microsoft 'a gönderir. Microsoft bu verileri, Configuration Manager gelecek sürümlerin yükleme deneyimini, kalitesini ve güvenliğini geliştirmek için kullanır. Daha fazla bilgi için bkz. [Configuration Manager Için tanılama ve kullanım verileri](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).
