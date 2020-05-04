---
title: Hata iletileri
titleSuffix: Configuration Manager
description: Paket dönüştürme yöneticisinden hata iletileri hakkında bilgi edinin.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709890"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Paket Dönüştürme Yöneticisi hata iletileri için teknik başvuru

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1357861-->

Bu makalede, Paket Dönüştürme Yöneticisi 'nin görüntülediği hata iletileri açıklanmaktadır. Ayrıca hatanın olası nedenlerini ve hatayı düzeltmek için yöntemleri içerir. Paket Dönüştürme Yöneticisi **PCMtrace. log**dosyasında hata iletilerini günlüğe kaydeder. Ayrıntı düzeyinin nasıl kontrol edilmesi de dahil olmak üzere daha fazla bilgi için bkz. [günlük dosyaları](troubleshoot-pcm.md#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Uygulama oluşturma, şu özel durumla başarısız oldu

Uygulama nesnesinin Configuration Manager sunucusuna gönderilmesi sırasında belirtilen özel durum oluştu.

Configuration Manager izinlerinizi denetleyin, bağlantınızı doğrulayın ve yeniden deneyin. Bu eylemler sorunu gidermezse, **PCMtrace. log** dosyasını (ayrıntı düzeyi 4) ve **Smsprov. log**dosyasını inceleyin.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Dönüştürme hatası – bir paket dönüştürme durumu IÇIN geçerlıdır

Paket dönüştürülürken genel bir özel durum oluştu. **PCMtrace. log** dosyasına bakın (ayrıntı düzeyi 4).

Ağ paylaşımının (paket veri kaynağı) Kullanıcı izinlerini denetleyin, bağlantınızı doğrulayın ve yeniden deneyin. Bu eylemler sorunu gidermezse, **PCMtrace. log** dosyasını inceleyin (ayrıntı düzeyi 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>İş akışı çıktılarında dönüştürülmüş bir paket ve sonuç uygulaması bulunamadı
Uygulama (dönüştürülen paket/program) silindi.

Bağımlı paket/programın var olduğundan emin olmak için bağımlı paketi/programı değiştirin.


#### <a name="objects-were-not-created-successfully"></a>Nesneler başarıyla oluşturulamadı
Birkaç olası neden vardır.

Configuration Manager izinlerinizi denetleyin, bağlantınızı doğrulayın ve yeniden deneyin. Bu eylemler sorunu gidermezse, **PCMtrace. log** dosyasını (ayrıntı düzeyi 4) ve **Smsprov. log** dosyasını inceleyin.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Lütfen Sihirbazı kapatın ve seçili paketle ilgili tüm sorunları çözün. Daha fazla bilgi için bkz. PCMTrace. log
Birkaç olası neden vardır.

Configuration Manager izinlerinizi denetleyin, bağlantınızı doğrulayın ve yeniden deneyin. Bu eylemler sorunu gidermezse, **PCMtrace. log** dosyasını (ayrıntı düzeyi 4) ve **Smsprov. log** dosyasını inceleyin.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Bazı dağıtım türlerinde algılama yöntemleri eksik. Tüm dağıtım türlerinde algılama metotları olmalıdır
Programda algılama yöntemleri yok.

**Onarma ve dönüştürme** işlemi sırasında bir veya daha fazla algılama yöntemi ekleyin.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Paket dönüştürme için hazırlanırken bir hata oluştu
Birkaç olası neden vardır.

Configuration Manager izinlerinizi denetleyin, bağlantınızı doğrulayın ve yeniden deneyin. Bu eylemler sorunu gidermezse, **PCMtrace. log** dosyasını (ayrıntı düzeyi 4) ve **Smsprov. log** dosyasını inceleyin.


