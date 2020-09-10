---
title: Microsoft Intune yüklenecek bir Win32 uygulaması hazırlayın
titleSuffix: ''
description: Microsoft Intune yüklenecek bir Win32 uygulamasını nasıl hazırlayacağınızı öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aaf4f009b25b09500d1a17a8c8a97b5f91e330e2
ms.sourcegitcommit: 54a771f1a632aef5d6bf8c71ce1e2c7823513b52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "90003456"
---
# <a name="prepare-win32-app-content-for-upload"></a>Win32 uygulama içeriğini karşıya yükleme için hazırlama

Microsoft Intune bir Win32 uygulaması ekleyebilmeniz için önce [Microsoft Win32 Içerik hazırlığı aracını](https://go.microsoft.com/fwlink/?linkid=2065730)kullanarak uygulamayı hazırlamanız gerekir.

## <a name="prerequisites"></a>Önkoşullar

Win32 uygulama yönetimini kullanmak için aşağıdaki ölçütleri karşıladığınızdan emin olun:

- Windows 10 sürüm 1607 veya üzeri (Enterprise, Pro ve eğitim sürümleri)
- Windows 10 istemcisi: 
  - Cihazların Azure AD 'ye katılması ve otomatik kaydı yapılmalıdır. Intune yönetim uzantısı, Azure AD 'ye katılmış, karma etki alanına katılmış, Grup İlkesi kayıtlı cihazlar desteklenir. 
  > [!NOTE]
  > Grup İlkesi kayıtlı senaryosu için Son Kullanıcı, Windows 10 cihazını birleştirmek için yerel kullanıcı hesabını kullanır. Kullanıcının AAD Kullanıcı hesabını kullanarak cihazda oturum açması ve Intune 'a kaydedilmesi gerekir. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza hedeflenirse, bu cihaza Intune yönetim uzantısını yükler.
- Windows uygulama boyutu uygulama başına 8 GB 'A göre belirlenir.

## <a name="convert-the-win32-app-content"></a>Win32 uygulama içeriğini Dönüştür

Windows Klasik (Win32) uygulamalarını önceden işlemek için [Microsoft Win32 Içerik hazırlığı aracını](https://go.microsoft.com/fwlink/?linkid=2065730) kullanın. Araç, uygulama yükleme dosyalarını *. ıntunewin* biçimine dönüştürür. Araç ayrıca, uygulama yükleme durumunu belirlemede Intune için gereken bazı öznitelikleri algılar. Bu aracı uygulama yükleyicisi klasöründe kullandıktan sonra, Intune konsolunda bir Win32 uygulaması oluşturabilirsiniz.

> [!IMPORTANT]
> [Microsoft Win32 içerik hazırlama aracı](https://go.microsoft.com/fwlink/?linkid=2065730) , *. ıntunewin* dosyasını oluşturduğunda tüm dosyaları ve alt klasörleri sıkıştırır. Microsoft Win32 Içerik Hazırlama Aracı 'nı yükleyici dosya ve klasörlerinden ayrı tutmanız gerekir, böylece araç veya diğer gereksiz dosya ve klasörleri *. ıntunewin* dosyanıza dahil etmeyin.

GitHub 'dan [Microsoft Win32 Içerik hazırlığı aracını](https://go.microsoft.com/fwlink/?linkid=2065730) bir zip dosyası olarak indirebilirsiniz. Daraltılmış dosya **Microsoft-Win32-Content-Prep-Tool-Master**adlı bir klasör içerir. Klasör Prep aracını, lisansı, bir Benioku dosyasını ve sürüm notlarını içerir. 

### <a name="process-flow-to-create-intunewin-file"></a>. Intunewin dosyası oluşturmak için işlem akışı

   <img alt="Process flow to create a .intunewin file" src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="run-the-microsoft-win32-content-prep-tool"></a>Microsoft Win32 Içerik hazırlığı aracını çalıştırma

`IntuneWinAppUtil.exe`Komut penceresinden parametresiz çalıştırırsanız araç, gerekli parametreleri adım adım girmek için size rehberlik eder. Ya da aşağıdaki kullanılabilir komut satırı parametrelerine göre parametreleri komuta ekleyebilirsiniz.

### <a name="available-command-line-parameters"></a>Kullanılabilir komut satırı parametreleri 

|    **Komut satırı parametresi**    |    **Açıklama**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    Yardım    |
|    `-c <setup_folder>`     |    Tüm kurulum dosyalarının klasörü. Bu klasördeki tüm dosyalar *. ıntunewin* dosyasına sıkıştırılacaktır.    |
|    `-s <setup_file>`     |    Kurulum dosyası (*setup.exe* veya *setup.msi* gibi).    |
|    `-o <output_folder>`     |    Oluşturulan *.intunewin* dosyası için çıkış klasörü.    |
|    `-q`       |    Sessiz mod    |

### <a name="example-commands"></a>Örnek komutlar

|    **Örnek komut**    |    **Açıklama**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    Bu komut aracın kullanım bilgilerini gösterir.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    Bu komut, belirtilen kaynak klasörden ve kurulum dosyasından `.intunewin` dosyasını oluşturur. MSI kurulum dosyası için, bu araç Intune'a gereken bilgileri alır. `-q` belirtilirse, komut sessiz modda çalıştırılır ve çıkış dosyası zaten varsa, bu dosyanın üzerine yazılır. Ayrıca, çıkış klasörü yoksa otomatik olarak oluşturulur.    |

*. Intunewin* dosyası oluştururken, kurulum klasörünün bir alt klasörüne başvurmak için gereken tüm dosyaları yerleştirin. Ardından, ihtiyacınız olan belirli bir dosyaya başvurmak için göreli bir yol kullanın. Örneğin:

**Kurulum kaynak klasörü:** *c:\testapp\v1.0*<br>
**Lisans dosyası:** *c:\testapp\v1.0\licenses\license.txt*

Göreli yol *licenses\license.txt*kullanarak *license.txt* dosyasına bakın.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune için bir Win32 uygulaması ekleyin](apps-win32-add.md).
