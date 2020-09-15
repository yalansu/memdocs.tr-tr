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
ms.openlocfilehash: db28653207d7bf4341d614aeecb769dcc145caaa
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083939"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Microsoft Intune 'de Win32 uygulama yönetimi

Microsoft Intune Win32 uygulama yönetimi özelliklerine izin verir. Buluta bağlı müşterilerin Win32 uygulama yönetimi için Microsoft uç nokta Configuration Manager kullanması mümkün olsa da, yalnızca Intune müşterileri Win32 iş kolu (LOB) uygulamaları için daha fazla yönetim özelliğine sahip olur. Bu konu, Intune Win32 uygulama yönetimi özelliklerine ve ilgili bilgilere genel bir bakış sağlar.

> [!NOTE]
> Bu uygulama yönetimi özelliği, Windows uygulamaları için hem 32-bit hem de 64-bit işletim sistemi mimarisini destekler.

> [!IMPORTANT]
> Win32 uygulamaları dağıttığınızda, özellikle de çok sayfalı bir Win32 uygulaması yükleyicinizin olduğu durumlarda [Intune yönetim uzantısı](../apps/intune-management-extension.md) yaklaşımını özel olarak kullanmayı düşünün. AutoPilot kaydı sırasında Win32 uygulamaları ve iş kolu uygulamaları yüklemesini karıştırırsanız, uygulama yüklemesi başarısız olabilir. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza atandığında otomatik olarak yüklenir.

## <a name="prerequisites"></a>Önkoşullar

Win32 uygulama yönetimini kullanmak için aşağıdaki ölçütleri karşıladığınızdan emin olun:

- Windows 10 sürüm 1607 veya üstünü (Enterprise, Pro ve eğitim sürümleri) kullanın.
- Cihazların Azure Active Directory (Azure AD) ve otomatik olarak kaydedilmiş olması gerekir. Intune yönetim uzantısı, Azure AD 'ye katılmış, karma etki alanına katılmış ve Grup İlkesi kayıtlı olan cihazları destekler. 
  > [!NOTE]
  > Kullanıcı, Grup İlkesi kaydı senaryosunda, Azure AD 'de Windows 10 cihazını birleştirmek için yerel kullanıcı hesabını kullanır. Kullanıcı, Azure AD Kullanıcı hesabını kullanarak cihazda oturum açması ve Intune 'a kaydolmalıdır. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza hedeflenirse, bu cihaza Intune yönetim uzantısını yükler.
- Windows uygulama boyutu uygulama başına 8 GB 'A göre belirlenir.

## <a name="prepare-the-win32-app-content-for-upload"></a>Karşıya yükleme için Win32 uygulaması içeriğini hazırlama

Microsoft Intune bir Win32 uygulaması ekleyebilmeniz için, uygulamayı Microsoft Win32 Içerik hazırlığı aracını kullanarak hazırlamanız gerekir. Windows Klasik (Win32) uygulamalarını önceden işlemek için Microsoft Win32 Içerik hazırlığı aracını kullanın. Araç, uygulama yükleme dosyalarını *. ıntunewin* biçimine dönüştürür. Daha fazla bilgi ve adım için bkz. [karşıya yükleme Için Win32 uygulama Içeriğini hazırlama](apps-win32-prepare.md). 

## <a name="add-assign-and-monitor-a-win32-app"></a>Win32 uygulaması ekleme, atama ve izleme

Microsoft Win32 Içerik Hazırlama Aracı 'nı kullanarak [Intune 'a yüklenecek bir Win32 uygulaması hazırladıktan](apps-win32-prepare.md) sonra, uygulamayı Intune 'a ekleyebilirsiniz. Daha fazla bilgi ve adım için bkz. [Microsoft Intune bir Win32 uygulaması ekleme, atama ve izleme](apps-win32-add.md).

## <a name="delivery-optimization"></a>Teslim iyileştirme

Windows 10 1709 ve üzeri istemciler, Windows 10 istemcisinde teslim iyileştirme bileşeni kullanarak Intune Win32 uygulama içeriğini indirir. Teslim iyileştirme, varsayılan olarak açık olan eşler arası işlevsellik sağlar. 

Teslim Iyileştirme aracısını, atamaya göre arka planda veya ön plan modunda Win32 uygulama içeriğini indirmek için yapılandırabilirsiniz. Teslim iyileştirme, Grup İlkesi ve Intune cihaz yapılandırması aracılığıyla yapılandırılabilir. Daha fazla bilgi için bkz. [Windows 10 Için teslim iyileştirmesi](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> Ayrıca, Intune Win32 uygulama içeriğini önbelleğe almak için Configuration Manager dağıtım noktalarınıza Microsoft bağlı önbellek sunucusu yükleyebilirsiniz. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## <a name="install-required-and-available-apps-on-devices"></a>Gerekli ve kullanılabilir uygulamaları cihazlara yükleme

Kullanıcı, gerekli ve kullanılabilir uygulama yüklemeleri için Windows bildirimleri görür. Aşağıdaki görüntüde, cihaz yeniden başlatılana kadar uygulama yüklemesinin tamamlanmadığına ilişkin örnek bir bildirim gösterilmektedir. 

![Uygulama yüklemesi için Windows bildirimlerinin ekran görüntüsü.](./media/apps-win32-app-management/apps-win32-app-08.png)    

Aşağıdaki görüntü, kullanıcıya uygulama değişikliklerinin cihaza yapıldığını bildirir.

![Kullanıcıya uygulama değişikliklerinin yapıldığını bildiren ekran görüntüsü.](./media/apps-win32-app-management/apps-win32-app-09.png)    

Ayrıca, Şirket Portalı uygulama kullanıcılara daha fazla uygulama yükleme durumu iletisi gösterir. Win32 bağımlılık özellikleri için aşağıdaki koşullar geçerlidir:
- Uygulama yüklenemedi. Yönetici tarafından tanımlanan bağımlılıklar karşılanmadı.
- Uygulama başarıyla yüklendi, ancak yeniden başlatma gerekiyor.
- Uygulama yüklenme sürecinde ancak devam etmek için yeniden başlatma gerekiyor.

## <a name="set-win32-app-availability-and-notifications"></a>Win32 uygulama kullanılabilirliğini ve bildirimlerini ayarlama
Bir Win32 uygulaması için başlangıç saatini ve son tarih saatini yapılandırabilirsiniz. Başlangıç zamanında, Intune yönetim uzantısı uygulama içeriğini indirmeyi başlatacak ve gerekli amaç için önbelleğe alacak. Uygulama son tarihte yüklenecektir. 

Kullanılabilir uygulamalar için, uygulama şirket portalında görünür olduğunda başlangıç saati görüntülenir ve Kullanıcı uygulamayı şirket portalından istediğinde içerik indirilir. Yeniden başlatma yetkisiz kullanım süresini de etkinleştirebilirsiniz. 

> [!IMPORTANT]
> **Atama** bölümündeki **yeniden başlatma yetkisiz kullanım süresi** ayarı, yalnızca **Program** bölümünün **cihaz yeniden başlatma davranışı** aşağıdaki seçeneklerden birine ayarlandığında kullanılabilir:
> - **Dönüş kodlarına dayalı davranışı belirleme**
> - **Intune zorunlu bir cihaz yeniden başlatmaya zorlayacaktır**

Aşağıdaki adımları kullanarak, gerekli bir uygulama için bir tarih ve saate göre uygulama kullanılabilirliğini ayarlayın:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **tüm uygulamalar**' ı seçin.
3. **Windows uygulaması (Win32)** listesinde bir uygulama seçin. 
4. Uygulama bölmesinde, **Properties**  >  **atamalar** bölümünün yanındaki Özellikler**Düzenle** ' yi seçin. Ardından **gerekli** atama türünün altında **grubu Ekle** ' yi seçin. 
   
   Uygulama kullanılabilirliği atama türüne göre ayarlanılabileceğini unutmayın. **Atama türü** **gerekli**, **Kayıtlı cihazlar için kullanılabilir**veya **kaldırma**olabilir.
5. Uygulamaya atanacak kullanıcı grubunu belirtmek için **Grup Seç** bölmesinde bir grup seçin. 

    > [!NOTE]
    > **Atama türü** seçenekleri şunları içerir:<br>
    > - **Gerekli**: **Bu uygulamayı tüm kullanıcılar için gerekli yap** ve/veya **Bu uygulamayı tüm cihazlarda gerekli**yap seçeneğini belirleyebilirsiniz.<br>
    > - **Kayıtlı cihazlar Için kullanılabilir**: **Bu uygulamayı, kayıtlı cihazları olan tüm kullanıcılar için kullanılabilir yap**' ı seçebilirsiniz.<br>
    > - **Kaldır**: **Bu uygulamayı tüm kullanıcılar için Kaldır** ve/veya **Bu uygulamayı tüm cihazlar için Kaldır**seçeneğini belirleyebilirsiniz.

6. **Son Kullanıcı bildirim** seçeneklerini değiştirmek için **Tüm bildirimleri göster**' i seçin.
7. **Atama düzenleme** bölmesinde, **Kullanıcı bildirimleri** ' ni **tüm bildirim bildirimlerini gösterecek**şekilde ayarlayın. **Son Kullanıcı bildirimlerini** **tüm bildirim bildirimlerini göstermek**, **bilgisayar yeniden başlatmaları için bildirimleri göstermek**veya **Tüm bildirimleri gizlemek**için ayarlayabileceğinizi unutmayın.
8. **Uygulama kullanılabilirliğini** **belirli bir tarih ve saate** ayarlayın ve Tarih ve saati seçin. Bu tarih ve saat, uygulamanın kullanıcının cihazına ne zaman indirildiğini belirtir. 
9. **Uygulama yükleme son tarihini** **belirli bir tarih ve saate** ayarlayın ve Tarih ve saati seçin. Bu tarih ve saat, uygulamanın kullanıcının cihazına ne zaman yüklendiğini belirtir. Aynı kullanıcı veya cihaz için birden çok atama yapıldığında, uygulama yüklemesinin son tarihi, mümkün olan en erken zamana göre çekilir.

10. **Yeniden başlatma**süresi ' nin yanında **etkin** ' i seçin. Yeniden başlatma yetkisiz kullanım süresi, cihazda uygulama yüklemesi tamamlandıktan hemen sonra başlar. Ayar devre dışı bırakıldığında, cihaz uyarı vermeden yeniden başlatılabilir. 

    Aşağıdaki seçenekleri özelleştirebilirsiniz:
    
    - **Cihaz yeniden başlatma yetkisiz kullanım süresi (dakika)**: varsayılan değer 1.440 dakikadır (24 saat). Bu değer en fazla 2 hafta olabilir.
    - **Yeniden başlatma işleminin (dakika) ardından yeniden başlatma geri sayımı iletişim kutusunun ne zaman gösterileceğini seçin (dakika)**: varsayılan değer 15 dakikadır.
    - **Kullanıcının yeniden başlatma bildirimini yeniden görüntülemesine Izin ver**: **Evet** veya **Hayır**seçeneğini belirleyebilirsiniz.
        - **Erteleme süresini (dakika) seçin**: varsayılan değer 240 dakikadır (4 saat). Erteleme değeri, yeniden başlatma yetkisiz kullanım süresinden daha fazla olamaz.

11. **Gözden geçir + kaydet**' i seçin.

## <a name="notifications-for-win32-apps"></a>Win32 uygulamaları için bildirimler 
Gerekirse, uygulama ataması başına kullanıcı bildirimlerinin gösterilmesini gizleyebilirsiniz. Intune 'da, **uygulamalar**  >  **tüm uygulamalar**' ı seçin  >  *uygulama*  >  **atamaları**  >  **gruplar dahil**değildir. 

> [!NOTE]
> Intune yönetim uzantısı aracılığıyla yüklenen Win32 uygulamaları, kayıtlı olmayan cihazlarda kaldırılmaz. Yöneticiler, kendi cihazını (BYOD) cihazlarını getirmek için Win32 uygulamaları sunmayan atama dışlamasını kullanabilir.

## <a name="next-steps"></a>Sonraki adımlar

- Intune'a uygulamaları ekleme hakkında daha fazla bilgi için bkz. [Microsoft Intune'a uygulama ekleme](apps-add.md).
