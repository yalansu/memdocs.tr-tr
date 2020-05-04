---
title: Desktop Analytics’i ayarlama
titleSuffix: Configuration Manager
description: Masaüstü analizlerini ayarlamaya ve eklemeye yönelik nasıl yapılır Kılavuzu.
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91a65f240a20e30af1610670c79182dee744e77b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714909"
---
# <a name="how-to-set-up-desktop-analytics"></a>Masaüstü analizlerini ayarlama

Bu yordamı kullanarak, masaüstü analizine oturum açın ve aboneliğinizde yapılandırın. Bu yordam, kuruluşunuz için masaüstü analizlerini ayarlamaya yönelik tek seferlik bir işlemdir.  

> [!Important]  
> Configuration Manager ile masaüstü analizlerinin genel önkoşulları hakkında bilgi için bkz. [Önkoşullar](overview.md#prerequisites).  

## <a name="initial-onboarding"></a>İlk ekleme

1. Microsoft 365 cihaz yönetimi ' nde, **genel yönetici** rolüne sahip bir kullanıcı olarak [Masaüstü Analizi portalını](https://aka.ms/desktopanalytics) açın. **Başlat**'ı seçin. Alternatif olarak, Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **Masaüstü Analizi bakım** düğümünü seçin ve **dağıtımları planla**' yı seçin.

2. **Hizmet sözleşmesini kabul et** sayfasında, hizmet sözleşmesini gözden geçirin ve **kabul et**' i seçin.  

3. **Aboneliğinizi onaylayın** sayfasında, gerekli nitelikli lisansların listesini gözden geçirin. **Desteklenen veya daha yüksek aboneliklerden birine sahip olduğunuz**Için ayarı **Evet** olarak değiştirin ve ardından **İleri**' yi seçin.  

4. **Kullanıcılara erişim izni** sayfasında:

    - **Masaüstü analizlerinin sizin adınıza Dizin rollerini yönetmesine Izin verin**: Masaüstü analizi, **çalışma alanı sahiplerini** **Masaüstü Analizi Yöneticisi** rolüne otomatik olarak atar. Bu gruplar zaten **genel yönetici**ise, değişiklik yoktur.

        Bu seçeneği seçmezseniz, masaüstü Analizi kullanıcıları yine de güvenlik grubunun üyesi olarak ekler. **Genel yöneticinin** kullanıcılar Için **Masaüstü Analizi yönetici** rolünü el ile ataması gerekir.

        Azure Active Directory ' de yönetici rolü izinleri atama hakkında daha fazla bilgi ve **Masaüstü Analizi yöneticilerine**atanan izinler hakkında daha fazla bilgi için, bkz. [Azure Active Directory içindeki yönetici rolü izinleri](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Masaüstü analizi, çalışma alanları ve dağıtım planları oluşturmak ve yönetmek için Azure Active Directory **çalışma alanı sahipleri** güvenlik grubunu önceden yapılandırır.

        Gruba bir kullanıcı eklemek için ad veya e-posta **adresi girin** bölümüne adını veya e-posta adresini yazın. İşiniz bittiğinde **İleri**' yi seçin.

5. **Çalışma alanınızı ayarlamak**için sayfasında:  

    > [!NOTE]  
    > Bu adımı gerçekleştirmek için, Kullanıcı **çalışma alanı sahibi** Izinlerine ve Azure aboneliğine ve kaynak grubuna ek erişime ihtiyaç duyuyor. Daha fazla bilgi için bkz. [Önkoşullar](overview.md#prerequisites).  

    - Masaüstü analizi için mevcut bir çalışma alanı kullanmak için, seçin ve sonraki adımla devam edin.  

        > [!TIP]  
        > Her Azure AD kiracısı için yalnızca bir masaüstü Analizi çalışma alanınız olabilir. Cihazlar yalnızca bir çalışma alanına Tanılama verileri gönderebilir.  

    - Masaüstü analizi için bir çalışma alanı oluşturmak üzere **çalışma alanı Ekle**' yi seçin.  

        1. Genel olarak benzersiz bir **çalışma alanı adı**girin.

        2. **Bu çalışma alanı Için Azure abonelik adını seçmek**üzere açılan listeyi seçin ve bu çalışma alanı için Azure aboneliğini seçin.  

        3. **Yeni oluştur** Kaynak grubu veya **mevcut olanı kullanın**.

        4. Listeden **bölgeyi** seçin ve ardından **Ekle**' yi seçin.  

6. Yeni veya mevcut bir çalışma alanı seçin ve ardından **Masaüstü Analizi çalışma alanı olarak ayarla**' yı seçin.  Ardından, **erişimi onayla ve erişim izni** Iletişim kutusunda **devam** ' ı seçin.  

7. Yeni tarayıcı sekmesinde, oturum açmak için kullanılacak bir hesap seçin. **Kuruluşunuz adına izin** vermek için seçeneği belirleyin ve **kabul et**' i seçin.  

    > [!Note]  
    > Bu izin, MALogAnalyticsReader uygulamasını çalışma alanı için Log Analytics okuyucu rolü atamak içindir. Bu uygulama rolü masaüstü analizi için gereklidir. Daha fazla bilgi için bkz. [MALogAnalyticsReader uygulama rolü](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. **Çalışma alanınızı ayarlamak**için sayfaya geri dönün, **İleri**' yi seçin.  

9. **Son adımlar** sayfasında, **Masaüstü Analizi 'ne git**' i seçin.

Azure portal, masaüstü Analizi **giriş** sayfasını gösterir.

## <a name="next-steps"></a>Sonraki adımlar

Configuration Manager, masaüstü analiziyle bağlantı kurmak için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]  
> [Configuration Manager’a bağlanma](connect-configmgr.md)  
