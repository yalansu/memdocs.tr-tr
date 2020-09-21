---
title: Microsoft Intune-Azure 'da Windows 10 Team cihaz kısıtlamalarını Surface Hub | Microsoft Docs
titleSuffix: ''
description: Windows 10 Team çalıştıran Surface Hub cihaz ayarlarını eklemek veya yapılandırmak için Intune 'U kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11a0b2967f98600bf5468e30579f2c42069b298d
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813685"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Intune kullanarak Surface Hub cihazlarda özellikleri izin vermek veya kısıtlamak için Windows 10 Team ayarları

Bu makalede, Surface Hub cihazları dahil olmak üzere Windows 10 Team çalıştıran cihazlar için yapılandırabileceğiniz cihaz kısıtlama ayarlarını Microsoft Intune gösterilmektedir.

## <a name="before-you-begin"></a>Başlamadan önce

[Windows 10 ekipleri cihaz kısıtlamaları yapılandırma profili](device-restrictions-configure.md#create-the-profile)oluşturun.

## <a name="apps-and-experience"></a>Uygulamalar ve deneyim

Bu ayarlar [Surçok yönlü hub CSP](/windows/client-management/mdm/surfacehub-csp)kullanır.

- **Oda içinde birisi**: **blok** , algılayıcısı odada birini algıladığında ekranın otomatik olarak uyandırmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Hoş Geldiniz ekranında görüntülenen toplantı bilgileri**: hoş geldiniz ekranının toplantılar kutucuğunda gösterilen bilgileri seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Yalnızca düzenleyici ve saat**
  - **Düzenleyici, saat ve konu (özel toplantılar için konu gizlidir)**
- **Hoş geldiniz ekranı arka plan resmi URL 'si**: Windows 10 Team cihazlarının **hoş geldiniz** ekranında özel bir arka plan olarak istediğiniz BIR. png görüntüsünün URL 'sini girin. Görüntünün PNG biçiminde olması ve URL ile başlaması gerekir `https://` .
- **Otomatik başlatma Connect**: **Block** , bir projeksiyon başlatıldığında Connect uygulamasının otomatik olarak açılmasını önler. Engellenirse, kullanıcılar Connect uygulamasını hub ayarlarından el ile başlatabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Oturum açma önerileri**: **blok** , oturum açma iletişim kutusunun zamanlanan toplantılardan davetlerle oto doldurmasını devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Toplantılarım ve dosyalar**: **Engelle** , Başlat menüsündeki **toplantılarımı ve dosyalar** özelliğini devre dışı bırakır. Bu özellik Microsoft 365 oturum açan kullanıcının toplantılarını ve dosyalarını gösterir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="azure-operational-insights"></a>Azure operasyonel içgörüler

- **Azure operasyonel**içgörüler **: Azure** operasyonel Içgörüler ile Windows 10 Team cihazlarından günlük verilerini toplar, depolar ve analiz edin. Azure operasyonel içgörüler, Microsoft Operations Manager Suite 'in bir parçasıdır. Azure operasyonel içgörüler 'e bağlanmak için **çalışma alanı kimliği** ve **çalışma alanı anahtarını** girin.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu verileri toplamayabilir.

## <a name="maintenance"></a>Bakım

Bu ayarlar [Surçok yönlü hub CSP](/windows/client-management/mdm/surfacehub-csp)kullanır.

- **Güncelleştirmeler Için bakım penceresi**: **Etkinleştir** , güncelleştirmeler yüklenedurumlarda bir bakım penceresi oluşturur. Bakım penceresi **başlangıç saatini**ve **saat cinsinden süreyi**1-5 saatten girin.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="session"></a>Oturum

Bu ayarlar [Surçok yönlü hub CSP](/windows/client-management/mdm/surfacehub-csp)kullanır.

- **Birim**: 0-100 adresinden yeni bir oturum için varsayılan birim değerini girin. Boş bırakılırsa, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi birimi 45 olarak ayarlayabilir.
- **Ekran zaman aşımı**: hub ekranı kapanana kadar geçecek dakika sayısını girin.
- **Oturum zaman aşımı**: oturum zaman aşımına uğrayana kadar geçecek dakika sayısını girin.
- **Uyku zaman aşımı**: hub uyku moduna girene kadar geçecek dakika sayısını girin.
- **Oturum sürdürme**: **engelleme** , kullanıcıların oturum zaman aşımına uğrarsa oturumu sürdürmesine engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="wireless-projection"></a>Kablosuz yansıtma

Bu ayarlar [Surçok yönlü hub CSP](/windows/client-management/mdm/surfacehub-csp)kullanır.

- **Kablosuz Projeksiyon Için PIN**: **gerekli** , kullanıcıların cihazda kablosuz PROJEKSIYON özelliklerini kullanmadan önce PIN girmesini zorlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Miracast Kablosuz Projeksiyon**: **blok** , Miracast özellikli cihazların projeye kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Miracast Kablosuz Projeksiyon kanalı**: bağlantıyı kurmak için Miracast kanalını seçin.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz. [cihaz kısıtlama ayarlarını yapılandırma](device-restrictions-configure.md).

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).