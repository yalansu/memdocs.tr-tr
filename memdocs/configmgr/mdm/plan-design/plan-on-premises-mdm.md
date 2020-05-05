---
title: Şirket içi MDM 'yi planlayın
titleSuffix: Configuration Manager
description: Configuration Manager mobil cihazları yönetmek için şirket içi mobil cihaz yönetimini planlayın
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721853"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager ' de şirket içi MDM için plan yapın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' de şirket içi mobil cihaz yönetimi (MDM) uygulamayı planlarken gözden geçirmeniz gereken birkaç temel alan vardır:

- Desteklenen cihazlar ve işletim sistemi sürümleri
- Gerekli site sistemi rolleri
- Güvenli iletişim
- Cihaz kaydı

> [!IMPORTANT]
> Site veya mobil cihaz Microsoft Intune bağlanmazsa, kuruluşunuz bu özelliği kullanmak için Intune lisanslarını hala istiyor. Daha fazla bilgi için bkz. [Microsoft Intune lisanslama](https://docs.microsoft.com/intune/fundamentals/licenses).

Configuration Manager altyapısını şirket içi MDM 'yi işleyecek şekilde hazırlamadan önce aşağıdaki gereksinimleri göz önünde bulundurun.

## <a name="supported-devices"></a><a name="bkmk_devices"></a>Desteklenen cihazlar  

Configuration Manager geçerli dalı, Windows 10 çalıştıran cihazlar için şirket içi mobil cihaz yönetiminde kaydı destekler. Bu cihaz türleri öncelikle dizüstü bilgisayarları, IoT ve Surface Hub içerir. Daha fazla bilgi ve belirli sürümlerin listesi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemi sürümleri](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Site sistemi rolleri

Şirket içi MDM, aşağıdaki site sistemi rollerinden en az birini gerektirir:

- Kayıt isteklerini desteklemek için **kaydolma proxy noktası**.

- Cihaz kaydını desteklemek için **kaydolma noktası**.

- İlke teslimi için **cihaz yönetim noktası**. Bu rol, yönetim noktasının bir çeşitlemesi olur, ancak mobil cihaz yönetimine izin verir.

- İçerik teslimi için **dağıtım noktası**.

Kuruluşunuzun ihtiyaçlarına bağlı olarak, bu rolleri tek sunucuya yükleyebilir veya farklı sunuculara ayrı ayrı yükleyebilirsiniz.

> [!NOTE]
> Şirket içi MDM için kullanılan her bir rolü, güvenilir cihazlarla iletişim için bir HTTPS uç noktası olarak yapılandırmanız gerekir. Daha fazla bilgi için bkz. [Gerekli güvenilen iletişimler](#bkmk_trustedComs).

Daha fazla genel bilgi için bkz. [site sistemi sunucularını ve rollerini planlayın](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>Güvenilen iletişimler

Şirket içi MDM, HTTPS iletişimleri için site sistem rollerini etkinleştirmenizi gerektirir. Gereksinimlerinize bağlı olarak, sunucular ile cihazlar arasında güvenilen bağlantılar kurmak için kuruluşunuzun sertifika yetkilisini (CA) kullanabilirsiniz. Güvenilen yetkili olarak genel kullanıma açık bir CA da kullanabilirsiniz. Her iki durumda da aşağıdaki sertifikaları yapılandırmanız gerekir:

- Gerekli site sistem rollerini barındıran sunucularda IIS 'de bir **Web sunucusu sertifikası** . Bir sunucu birden çok site sistem rolü barındırıyorsa, bu sunucu için yalnızca bir sertifika gerekir. Her rol ayrı bir sunucu üzerinde ise, her sunucunun ayrı bir sertifikası olması gerekir.

- Web sunucusu sertifikalarını veren CA 'nın **Güvenilen kök sertifikası** . Bu kök sertifikayı, site sistem rollerine bağlanması gereken tüm cihazlara yükler.

Daha fazla bilgi için bkz. Şirket [ıçı MDM 'de güvenilir iletişimler için sertifikaları ayarlama](../get-started/set-up-certificates-on-premises-mdm.md).

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>Cihaz kaydı

Şirket içi MDM için cihaz kaydını etkinleştirmek için:

- Kullanıcılara istemci ayarları aracılığıyla kaydolma izni verme

- Gerekli rolleri barındıran site sistemi sunucularıyla güvenilir iletişim için cihazları yapılandırın

Kullanıcı tarafından başlatılan kayda alternatif olarak, toplu kayıt paketi ayarlayabilirsiniz. Bu paket, cihazın kullanıcı müdahalesi olmadan kaydolmasını sağlar. Paketi kullanım için sağlanmadan veya OOBE sürecinden geçtikten sonra cihaza sunun.

Daha fazla bilgi için bkz. Şirket [ıçı MDM için cihaz kaydını ayarlama](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## <a name="next-step"></a>Sonraki adım

> [!div class="nextstepaction"]
> [Site sistemi rolleri yükleme](../get-started/install-site-system-roles-for-on-premises-mdm.md)
