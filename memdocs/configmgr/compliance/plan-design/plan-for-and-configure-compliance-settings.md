---
title: Uyumluluk ayarlarını planlama ve yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager uyumluluk ayarlarıyla çalışmaya yönelik önkoşullar ve yapılandırma görevleri hakkında bilgi edinin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73ccec4ca318b522c0714bc8e5cc89f6c8899edd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712158"
---
# <a name="plan-for-and-configure-compliance-settings-in-configuration-manager"></a>Configuration Manager uyumluluk ayarlarını planlayın ve yapılandırın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager uyumluluk ayarları ile çalışmaya başlamadan önce bilmeniz gereken birkaç önkoşul ve gerçekleştirmeniz gereken bazı yapılandırma görevleri vardır.  

## <a name="prerequisites-for-compliance-settings"></a>Uyumluluk ayarları için önkoşullar  

|Önkoşul|Daha fazla bilgi|  
|------------------|----------------------|  
|Windows Configuration Manager istemcileri etkinleştirilmeli ve uyumluluk değerlendirmesi için yapılandırılmalıdır.|Aşağıya bakın|  
|Raporları çalıştırmak istiyorsanız siteniz için raporlamayı yapılandırmanız gerekir.|[Raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md)|  
|Gerekli güvenlik izinleri.|**Uyumluluk Ayarları Yöneticisi** güvenlik rolü, uyumluluk ayarlarını, Kullanıcı verilerini ve profil yapılandırma öğelerini ve uzak bağlantı profillerini yönetmek için gerekli izinleri içerir.<br /><br /> [Rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Uyumluluk ayarlarını etkinleştirme ve yapılandırma (yalnızca Windows bilgisayarlar için)  

Bu yordam, uyumluluk ayarları için varsayılan istemci ayarlarını yapılandırır ve hiyerarşinizdeki tüm bilgisayarlara uygular. Bu ayarların yalnızca bazı bilgisayarlara uygulanmasını istiyorsanız özel bir cihaz istemcisi ayarı oluşturun ve bu ayarı, uyumluluk ayarlarını kullanmak istediğiniz bilgisayarları içeren bir koleksiyonla ilişkilendirin. Özel cihaz ayarları oluşturma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Diğer cihaz türleri, uyumluluk ayarlarını değerlendirmek için belirli bir yapılandırma gerektirmez.  

1.  Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan ayarlar**' a tıklayın.  
2.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  
3.  **Varsayılan Ayarlar** iletişim kutusunda **Uyumluluk Ayarları**’na tıklayın.  
4.  Uyumluluk ayarları için aşağıdaki istemci ayarlarını yapılandırın:
    - **İstemcilerde uyumluluk değerlendirmesini etkinleştir** -istemci cihazlarda uyumluluğu değerlendirmek istiyorsanız **true** olarak ayarlayın.
    - **Uyumluluk değerlendirmesi zamanla** -istemci cihazlarda varsayılan uyumluluk değerlendirme zamanlamasını değiştirmek istiyorsanız **zamanla** ' ya tıklayın.
    - **Kullanıcı verilerini ve profillerini etkinleştir** -Windows bilgisayarlarına Kullanıcı verileri ve profilleri yapılandırma öğeleri oluşturup dağıtmak istiyorsanız bu seçeneği etkinleştirin. Ayrıntılar için bkz. [Kullanıcı verileri ve profilleri yapılandırma öğeleri oluşturma](../deploy-use/create-remote-connection-profiles.md).
5. **Varsayılan Ayarlar** iletişim kutusunu kapatmak için **Tamam** 'a tıklayın.  

İstemci bilgisayarlar, istemci ilkesini sonraki sefer indirdiklerinde bu ayarlarla yapılandırılır.  
