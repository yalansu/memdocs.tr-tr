---
title: Şirket içi MDM için kayıt ayarlama
titleSuffix: Configuration Manager
description: Kullanıcılara şirket içi mobil cihaz yönetimi (MDM) için cihazlarını kaydetme izni verin Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721846"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager ' de şirket içi MDM için cihaz kaydını ayarlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Şirket içi mobil cihaz yönetimi (MDM) ayarlamaya yönelik son adım, kullanıcıların cihazlarını kaydetmelerini olanaklı hale etkinleştirmektir. Kullanıcılara şirket içi MDM 'de cihaz kaydetme izni vermek için Configuration Manager istemci ayarlarını kullanın.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a>Kayıt profili oluşturma

Kullanıcıların mobil cihazları kaydetmesine izin vermek için gereken ayarları göndermek üzere varsayılan istemci ayarlarına yeni bir kayıt profili ekleyin. Bu profil daha sonra Configuration Manager sitesindeki tüm kullanıcılar için geçerlidir.

> [!NOTE]
> Bu işlem, tüm cihazlar ve kullanıcılara otomatik olarak uygulanacak **varsayılan Istemci ayarlarını**kullanır. Alternatif olarak, özel istemci ayarları oluşturabilir ve ardından istediğiniz koleksiyonlara dağıtabilirsiniz. Bu alternatif yöntem, biri *cihaz* ayarları ve biri *Kullanıcı* ayarları için olmak üzere en az iki özel istemci ayarı gerektirir. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **istemci ayarları** düğümünü seçin. **Varsayılan Istemci ayarlarını** açın ve **kayıt** grubunu seçin.

1. Cihaz ayarları altında **modern cihazlar Için yoklama aralığını belirtin (dakika)**. Varsayılan olarak, bu Aralık 60 dakikadır.

1. Kullanıcı ayarları altında **kullanıcıların modern cihazları kaydetmesine Izin ver**seçeneğini etkinleştirin.

1. **Modern cihaz kayıt profili**Için **profili ayarla**' yı seçin. Kayıt profili penceresinde **Oluştur**' u seçin.

1. Kayıt profili Oluştur penceresinde, aşağıdaki bilgileri belirtin:

    - Kayıt profili için benzersiz ve açıklayıcı bir **ad** .

    - Profil hakkında ek bilgi sağlamak için isteğe bağlı bir **Açıklama** .

    - Cihaz yönetim noktasını içeren **Yönetim sitesi kodunu** seçin. Kaydetmek ve kapatmak için **Tamam ' ı** seçin.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Ek istemci ayarlarını yapılandırma

Cihazları kaydolduktan sonra yapılandırmak için ek istemci ayarları vardır. Daha fazla genel bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).

Configuration Manager, şirket içi MDM için aşağıdaki istemci ayarlarını destekler:

- **İstemci ilkesi**: Bu ayarlar cihaza istemci ilkesi indirme sıklığını belirtir. Ayrıca, Kullanıcı ilkesi ayarlarını da etkinleştirebilirsiniz. Daha fazla bilgi için bkz. [istemci ayarları-Istemci Ilkesi hakkında](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Yazılım dağıtımı**: yazılım dağıtımlarını değerlendirmek için aralığı ayarlayın. Daha fazla bilgi için bkz. [istemci ayarları-yazılım dağıtımı hakkında](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > Şirket içi MDM için, yazılım dağıtım ayarları yalnızca varsayılan istemci ayarları olarak kullanılabilir.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Kullanıcıları bul

Kullanıcıların, şirket içi MDM için kayıt profiliyle istemci ayarlarını alması için, site Kullanıcı hesabını Active Directory bulur. Kayıt profiline gereksinim duyan herkesin kayıt profilini aldığından emin olmak için Active Directory kullanıcılarına yönelik saptama gerçekleştirin. Daha fazla bilgi için bkz. [Kullanıcı keşfi Active Directory](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Güvenilen kök sertifikayı yükler

Etki alanına katılmış cihazlar, site sistem rollerini barındıran sunucularla güvenilir iletişim için güven kök sertifikasını alır. Active Directory Sertifika Hizmetleri, güvenilen kök sertifikayı otomatik olarak dağıtır. Etki alanına katılmış olmayan bilgisayarlar ve mobil cihazlar, kayda izin vermek için diğer yollarla bu sertifikaya sahip olmalıdır.

> [!NOTE]
> Web sunucusu sertifikaları bir ortak sertifika yetkilisi tarafından verildiyse, çoğu cihaz bu CA 'Lara zaten güvenilir. Tasarımınız bu genel CA 'Lardan birini kullanıyorsa, bu adımı uygulamanız gerekmez.

[Güvenilen kök sertifikayı dışa](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)aktardıktan sonra, kaydolmasını gerektiren cihazlara yüklemeniz gerekir. Örneğin, etki alanına katılmamış cihazlar ve Active Directory otomatik olarak alamıyor. Kullandığınız işlem aşağıdaki faktörlere bağlı olacaktır:

- Belirli cihaz türleri ve teknik yetenekler
- İşletim sistemi sürümü
- İşiniz, güvenlik ve Kullanıcı deneyimi gereksinimleriniz

Aşağıdaki liste, cihazlarda güvenilen kök sertifikayı teslim etmek ve yüklemek için bazı örnek yöntemleri içerir:

- Dosya paylaşımı

- E-posta eki

- Bellek kartı

- İnternet paylaşımlı cihaz

- Bulut depolama (OneDrive gibi)

- Yakın alan iletişimi (NFC) bağlantısı

- Barkod tarayıcısı

- İlk çalıştırma deneyimi (OOBE) sağlama paketi

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Güvenilen kök sertifikayı Windows 'a el ile yükler

1. Kaydedilen cihazda, dosya Gezgini ' ne güvenilir kök sertifika dosyası (. cer) konumuna gidin ve **açın** .

1. Sertifika penceresinde **sertifikayı yükler**' i seçin.

1. Sertifika Içeri aktarma sihirbazında **yerel makine**' yi seçin ve ardından yönetici olarak devam etmek için **İleri** ' yi seçin.

1. Sertifika Deposu sayfasında, **tüm sertifikaları aşağıdaki depolama alanına yerleştir**' i seçin ve ardından, ardından da **Araştır**' ı seçin.

1. Sertifika deposu Seç penceresinde, **Güvenilen kök sertifika yetkilileri**' ni seçin ve **Tamam**' ı seçin.

1. Tamamlanmış ve sihirbaz.

## <a name="next-step"></a>Sonraki adım

> [!div class="nextstepaction"]
> [Cihazları kaydetme](../deploy-use/enroll-devices-on-premises-mdm.md)
