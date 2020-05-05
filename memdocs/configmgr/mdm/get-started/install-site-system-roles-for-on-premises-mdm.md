---
title: Şirket içi MDM için rolleri yükler
titleSuffix: Configuration Manager
description: Configuration Manager ' de şirket içi mobil cihaz yönetimi (MDM) için gerekli site sistemi rollerini yükler.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721860"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager ' de şirket içi MDM için site sistemi rolleri 'ni yükler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Şirket içi mobil cihaz yönetimi (MDM) Configuration Manager Configuration Manager sitenizde aşağıdaki site sistem rollerini gerektirir:

- Kayıt noktası

- Kayıt proxy noktası

- Dağıtım noktası

- Mobil cihazlar için izin veren bir yönetim noktası olan cihaz yönetim noktası

## <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar

- Şirket içi MDM, HTTPS iletişimleri için site sistem rollerini etkinleştirmenizi gerektirir. Daha fazla bilgi için bkz. Şirket [ıçı MDM 'de güvenilir iletişimler için sertifikaları ayarlama](set-up-certificates-on-premises-mdm.md).

- Geçerli Configuration Manager dalı yalnızca cihazlardan şirket içi MDM için dağıtım noktalarına ve cihaz yönetim noktalarına *intranet* bağlantılarını destekler. Ancak, macOS bilgisayarlarını de yönetiyorsanız, bu istemciler aynı rollere *İnternet* bağlantısı gerektirir. Dağıtım noktasını ve cihaz yönetim noktasını yapılandırırken, **intranet ve internet bağlantılarına Izin verme**seçeneğini kullanın.

- İntranet bağlantıları için yapılandırdığınız dağıtım noktaları, site sınırlarını sizin için yapılandırmanızı gerektirir. Configuration Manager yalnızca şirket içi MDM için IPv4 aralığı sınırlarını destekler. Daha fazla bilgi için bkz. [site sınırlarını ve sınır gruplarını tanımlama](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- Cihaz yönetim noktanlarınızla [veritabanı çoğaltmaları](../../core/servers/deploy/configure/database-replicas-for-management-points.md) kullanıyorsanız, yeni kaydedilen cihazların bağlantısı başlangıçta başarısız olur. Bu bağlantı hatası, veritabanı çoğaltması başarılı bir bağlantı için gerekli olan yeni kaydedilmiş cihazla ilgili bilgiler içermediğinden oluşur. Çoğaltmalar her beş dakikada bir eşitlenir. Cihazlar, genellikle iki bağlantı girişimi olan kayıttan sonra ilk beş dakika boyunca bağlanamaz. Ardından, cihazlar başarıyla bağlanır.

## <a name="add-roles"></a>Rolleri ekleme

Şirket içi MDM 'yi Configuration Manager istemcisiyle yönetilen birçok cihaz içeren bir siteye ekliyorsanız, bu rollerden bazıları zaten sitede yüklü olabilir. Örneğin, dağıtım noktası ortak bir roldür ve macOS cihazlarını yönetmek için cihaz yönetim noktası gereklidir.

Sitenize rol ekleme hakkında daha fazla bilgi için bkz. [site sistemi rolleri ekleme](../../core/servers/deploy/configure/install-site-system-roles.md).

## <a name="configure-roles"></a>Rolleri yapılandırma

Mobil cihazları yönetmek için yeni veya mevcut rolleri yapılandırın. Şirket içi MDM için dağıtım noktasını ve cihaz yönetim noktasını doğru şekilde çalışacak şekilde yapılandırmak için aşağıdaki adımları izleyin:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **sunucular ve site sistemi rolleri** düğümünü seçin.

1. Yapılandırmak istediğiniz dağıtım noktası veya cihaz yönetim noktası ile site sistem sunucusunu seçin. Listeden sunucuyu seçin, sonra site sistem rolleri Ayrıntılar bölmesinde **site sistemi** rolünü seçin. Şeritte, **site rolü** sekmesinde **Özellikler**' i seçin.

    > [!TIP]
    > Büyük bir sitede, görünümün kapsamını yalnızca belirli rollere sahip sunucuları gösterecek şekilde tanımlayabilirsiniz. **Sunucular ve site sistemi rolleri** düğümünü seçtiğinizde, şeritte giriş etiketinde **role sahip sunucular**' ı seçin. Daha sonra sitede Şu anda kullanılabilir olan roller listesinden istediğiniz rolü seçin.

    **Site sistem özelliklerinin** **genel** sekmesinde, **adın** tam etki alanı adı (FQDN) olduğundan emin olun. Özellikleri kapatın.

1. Konsol listesinde, şirket içi dağıtım noktası rolüne sahip bir sunucu seçin. Site sistem rolleri Ayrıntılar bölmesinde **dağıtım noktası** rolünü seçin. Şeritte, **site rolü** sekmesinde **Özellikler**' i seçin. **Dağıtım noktası özelliklerinin** **iletişim** sekmesinde:

    1. **Https**' yi seçin ve **yalnızca Intranet bağlantılarına izin ver**' i seçin.

        > [!IMPORTANT]
        > MacOS bilgisayarlarını Configuration Manager istemcisiyle de yönetiyorsanız, bunun yerine **intranet ve internet bağlantılarına Izin ver** ' i kullanın.

    1. **Mobil cihazların bu dağıtım noktasına bağlanmasına Izin ver**seçeneğini etkinleştirin ve sonra özellikleri kapatın.

1. **Yönetim noktası** site sistemi rolünün özelliklerini açın.

    1. **Genel** sekmesinde **https**' yi seçin ve **yalnızca Intranet bağlantılarına izin ver**' i seçin.

        > [!IMPORTANT]
        > MacOS bilgisayarlarını Configuration Manager istemcisiyle de yönetiyorsanız, bunun yerine **intranet ve internet bağlantılarına Izin ver** ' i kullanın.

    1. **Mobil cihazların ve Mac bilgisayarın bu yönetim noktasını kullanmasına Izin ver**seçeneğini etkinleştirin ve sonra özellikleri kapatın.

        > [!NOTE]
        > Bu seçenek, yönetim noktasını etkin bir şekilde bir *cihaz* yönetim noktasına dönüştürür.  

## <a name="next-step"></a>Sonraki adım

Mobil cihazları yönetmeye yönelik rolleri ekledikten ve yapılandırdıktan sonra, sunucuları güvenilir uç noktalar olarak yapılandırın. Bu güven, rollerin yönetilen cihazlarla iletişim kurmasını ve bunları kaydetmelerini sağlar.

> [!div class="nextstepaction"]
> [Güvenilen iletişim için sertifikalar ayarlama](set-up-certificates-on-premises-mdm.md)
