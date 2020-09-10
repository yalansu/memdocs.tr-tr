---
title: Microsoft Intune 'de Win32 uygulama yönetimi
titleSuffix: ''
description: Microsoft Intune ile Win32 uygulamalarını yönetmeyi öğrenin. Bu konu, Intune Win32 uygulama teslimi ve yönetim özelliklerine genel bir bakış sağlar.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6579f5137abd20e564616bf1ef6188fc7b5a5009
ms.sourcegitcommit: 54a771f1a632aef5d6bf8c71ce1e2c7823513b52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "90003014"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Microsoft Intune 'de Win32 uygulama yönetimi

Microsoft Intune Win32 uygulama yönetimi özelliklerine izin verir. Bulut bağlantılı müşterilerin Win32 uygulama yönetiminde Configuration Manager'ı kullanmaları mümkün olsa da, yanızca Intune kullanan müşteriler Win32 iş kolu (LOB) uygulamalarında daha fazla yönetim özelliğinden yararlanabilir. Bu konu, Intune Win32 uygulama yönetimi özelliklerine ve ilgili bilgilere genel bir bakış sağlar.

> [!NOTE]
> Bu uygulama yönetimi özelliği, Windows uygulamaları için hem 32-bit hem de 64-bit işletim sistemi mimarisini destekler.

> [!IMPORTANT]
> Win32 uygulamalarını dağıttığınızda, özellikle de çok sayfalı bir Win32 uygulaması yükleyicinizin olduğu durumlarda, [Intune yönetim uzantısı](../apps/intune-management-extension.md) yaklaşımını özel olarak kullanmayı düşünün. AutoPilot kaydı sırasında Win32 uygulamaları ve iş kolu uygulamaları yüklemesini karıştırırsanız, uygulama yüklemesi başarısız olabilir. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza atandığında otomatik olarak yüklenir.

## <a name="prerequisites"></a>Önkoşullar

Win32 uygulama yönetimini kullanmak için aşağıdaki ölçütleri karşıladığınızdan emin olun:

- Windows 10 sürüm 1607 veya üzeri (Enterprise, Pro ve eğitim sürümleri)
- Windows 10 istemcisi: 
  - Cihazların Azure AD 'ye katılması ve otomatik kaydı yapılmalıdır. Intune yönetim uzantısı, Azure AD 'ye katılmış, karma etki alanına katılmış, Grup İlkesi kayıtlı cihazlar desteklenir. 
  > [!NOTE]
  > Grup İlkesi kayıtlı senaryosu için Son Kullanıcı, Windows 10 cihazını birleştirmek için yerel kullanıcı hesabını kullanır. Kullanıcının AAD Kullanıcı hesabını kullanarak cihazda oturum açması ve Intune 'a kaydedilmesi gerekir. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza hedeflenirse, bu cihaza Intune yönetim uzantısını yükler.
- Windows uygulama boyutu uygulama başına 8 GB 'A göre belirlenir.

## <a name="prepare-the-win32-app-content-for-upload"></a>Karşıya yükleme için Win32 uygulaması içeriğini hazırlama

Microsoft Intune bir Win32 uygulaması ekleyebilmeniz için önce Microsoft Win32 Içerik hazırlığı aracını kullanarak uygulamayı hazırlamanız gerekir. Microsoft Win32 Içerik Hazırlama Aracı Windows Klasik (Win32) uygulamalarını ön işlemden kullanıyorsunuz. Araç, uygulama yükleme dosyalarını *. ıntunewin* biçimine dönüştürür. Daha fazla bilgi ve adım için bkz. [karşıya yükleme Için Win32 uygulama Içeriğini hazırlama](apps-win32-prepare.md). 

## <a name="add-assign-and-monitor-a-win32-app"></a>Win32 uygulaması ekleme, atama ve izleme

Microsoft Win32 Içerik Hazırlama Aracı 'nı kullanarak [Intune 'a karşıya yüklenecek bir Win32 uygulamasını hazırladıktan](apps-win32-prepare.md) sonra, uygulamayı Intune 'a ekleyebilirsiniz. Daha fazla bilgi ve adım için bkz. [Microsoft Intune bir Win32 uygulaması ekleme, atama ve izleme](apps-win32-add.md).

## <a name="delivery-optimization"></a>Teslim Iyileştirme

Windows 10 1709 ve üzeri istemciler, Windows 10 istemcisindeki bir teslim iyileştirme bileşeni kullanarak Intune Win32 uygulama içeriğini indirecek. Teslim iyileştirme, varsayılan olarak açık olan eşler arası işlevsellik sağlar. Teslim Iyileştirme aracısını, atamaya göre arka planda veya ön plan modunda Win32 uygulama içeriğini indirmek için yapılandırabilirsiniz. Teslim iyileştirme, Grup İlkesi ve Intune cihaz yapılandırması aracılığıyla yapılandırılabilir. Daha fazla bilgi için bkz. [Windows 10 Için teslim iyileştirmesi](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> Ayrıca, Intune Win32 uygulama içeriğini önbelleğe almak için Configuration Manager dağıtım noktalarınıza Microsoft bağlı önbellek sunucusu yükleyebilirsiniz. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager-Intune Win32 uygulamaları Için destek](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## <a name="install-required-and-available-apps-on-devices"></a>Gerekli ve kullanılabilir uygulamaları cihazlara yükleme

Son Kullanıcı, gerekli ve kullanılabilir uygulama yüklemeleri için Windows bildirimleri görüntülenir. Aşağıdaki resimde, cihaz yeniden başlatılana kadar uygulama yüklemesinin tamamlanmayacağına ilişkin bildirim örneği gösterilir. 

![Uygulama yüklemesi için Windows bildirim bildirimlerinin ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-08.png)    

Aşağıdaki görüntüde, son kullanıcıya cihazda uygulama değişikliklerinin yapıldığını bildirir.

![Kullanıcıya uygulama değişikliklerinin yapıldığını bildiren ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-09.png)    

Ayrıca, Şirket Portalı uygulaması son kullanıcılara ek uygulama yükleme durumu iletileri gösterir. Win32 bağımlılık özellikleri için aşağıdaki koşullar geçerlidir:
- Uygulama yüklenemedi. Yönetici tarafından tanımlanan bağımlılıklar karşılanmadı.
- Uygulama başarıyla yüklendi, ancak yeniden başlatma gerekiyor.
- Uygulama yükleme sürecinde, ancak devam etmek için yeniden başlatma gerekiyor.

## <a name="set-win32-app-availability-and-notifications"></a>Win32 uygulama kullanılabilirliğini ve bildirimlerini ayarlama
Bir Win32 uygulaması için başlangıç saatini ve son tarih saatini yapılandırabilirsiniz. Başlangıç zamanında, Intune yönetim uzantısı uygulama içeriğini indirmeyi başlatacak ve gerekli amaç için önbelleğe alacak. Uygulama son tarihte yüklenecektir. Kullanılabilir uygulamalar için, uygulama Şirket Portalı görünür olduğunda başlangıç zamanı görüntülenir ve Son Kullanıcı uygulamayı Şirket Portalı istediğinde içerik indirilir. Ayrıca, yeniden başlatma yetkisiz kullanım süresini de etkinleştirebilirsiniz. 

> [!IMPORTANT]
> **Atama** bölümündeki **yeniden başlatma yetkisiz kullanım süresi** ayarı yalnızca **Program** bölümünün **cihaz yeniden başlatma davranışı** aşağıdaki seçeneklerden birine ayarlandığında kullanılabilir:
> - **Dönüş kodlarına dayalı davranışı belirleme**
> - **Intune zorunlu bir cihaz yeniden başlatmaya zorlayacaktır**

Aşağıdaki adımları kullanarak, gerekli bir uygulama için bir tarih ve saate göre uygulama kullanılabilirliğini ayarlayın:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **tüm uygulamalar**' ı seçin.
3. Listeden var olan bir **Windows uygulaması (Win32)** seçin. 
4. Uygulama bölmesinden, atamalar bölümünün yanındaki Düzenle ' **yi seçin ve**  >  **Edit** **gerekli** atama türünün altına **Grup ekleyin** >. **Assignments** 
   Uygulama kullanılabilirliği atama türüne göre ayarlanılabileceğini unutmayın. **Atama türü** **gerekli**, **Kayıtlı cihazlar için kullanılabilir**veya **kaldırma**olabilir.
5. Uygulamaya atanacak kullanıcı grubunu belirtmek için **Grup Seç** bölmesinde bir grup seçin. 

    > [!NOTE]
    > **Atama türü** seçenekleri şunları içerir:<br>
    > - **Gerekli**: **Bu uygulamayı tüm kullanıcılar için gerekli hale getirme** ve/veya **Bu uygulamayı tüm cihazlarda gerekli hale**getirme seçeneğini belirleyebilirsiniz.<br>
    > - **Kayıtlı cihazlar Için kullanılabilir**: **Bu uygulamayı kayıtlı cihazları olan tüm kullanıcılar için kullanılabilir**hale getirme seçeneğini belirleyebilirsiniz.<br>
    > - **Kaldır**: ***Bu uygulamayı tüm kullanıcılar için Kaldır** ve/veya **Bu uygulamayı tüm cihazlar için Kaldır**seçeneğini belirleyebilirsiniz.

6. **Son Kullanıcı bildirim** seçeneklerini değiştirmek için **tüm bildirim bildirimlerini göster**' i seçin.
7. **Atama düzenleme** bölmesinde, bu **Kullanıcı bildirimlerini** **tüm bildirim bildirimlerini gösterecek**şekilde ayarlayın. **Son Kullanıcı bildirimlerini** **tüm bildirim bildirimlerini göstermek**, **bilgisayar yeniden başlatmaları için bildirimleri göstermek**veya **Tüm bildirimleri gizlemek**için ayarlayabileceğinizi unutmayın.
8. **Uygulama kullanılabilirliğini** **belirli bir tarih ve saate** ayarlayın ve Tarih ve saati seçin. Bu tarih ve saat, uygulamanın son kullanıcılar cihazına ne zaman indirildiğini belirtir. 
9. **Uygulama yükleme son tarihini** **belirli bir tarih ve saate** ayarlayın ve Tarih ve saati seçin. Bu tarih ve saat, uygulamanın son kullanıcılar cihazında yüklü olduğunu belirtir. Aynı kullanıcı veya cihaz için birden çok atama yapıldığında, uygulama yüklemesinin son tarihi, mümkün olan en erken zamana göre çekilir.

10. **Yeniden başlatma yetkisiz kullanım süresinin**yanında **etkin** ' e tıklayın. Yeniden başlatma yetkisiz kullanım süresi, cihazda uygulama yüklemesi tamamlandıktan hemen sonra başlar. Devre dışı bırakıldığında, cihaz uyarı vermeden yeniden başlatılabilir. <br>Aşağıdaki seçenekleri özelleştirebilirsiniz:
    - **Cihaz yeniden başlatma yetkisiz kullanım süresi (dakika)**: varsayılan değer 1440 dakikadır (24 saat). Bu değer en fazla 2 hafta olabilir.
    - **Yeniden başlatma işleminin (dakika) ardından yeniden başlatma geri sayımı iletişim kutusunun ne zaman gösterileceğini seçin (dakika)**: varsayılan değer 15 dakikadır.
    - **Kullanıcının yeniden başlatma bildirimini yeniden görüntülemesine Izin ver**: **Evet** veya **Hayır**seçeneğini belirleyebilirsiniz.
        - **Erteleme süresini (dakika) seçin**: varsayılan değer 240 dakikadır (4 saat). Erteleme değeri, yeniden başlatma yetkisiz kullanım süresinden daha fazla olamaz.

11. **Gözden geçir + kaydet**' e tıklayın.

## <a name="toast-notifications-for-win32-apps"></a>Win32 uygulamaları için bildirim bildirimleri 
Gerekirse, uygulama ataması başına Son Kullanıcı bildirim bildirimlerinin gösterilmesini gizleyebilirsiniz. Intune 'da, **uygulamalar**  >  **tüm uygulamalar** ' ı seçin > uygulama > **atamaları**  >  **dahil et**' i seçin. 

> [!NOTE]
> Kaydı kaldırılan cihazlardaki Intune yönetim uzantısıyla yüklenmiş olan Win32 uygulamaları kaldırılmaz. Yöneticiler, KCG cihazlarına Win32 uygulamalarını sunmamak amacıyla bunları atamadan hariç tutma seçeneğini değerlendirebilir.

## <a name="next-steps"></a>Sonraki adımlar

- Intune'a uygulamaları ekleme hakkında daha fazla bilgi için bkz. [Microsoft Intune'a uygulama ekleme](apps-add.md).
