---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: b0c25174873e00cf23dacd2c77208775f1fb1ced
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644140"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->

Ortak yönetimi etkinleştirirken Azure genel bulutu, Azure ABD kamu bulutu 'nı veya Microsoft Azure Çin 21Vianet (sürüm 2006 ' de eklenmiştir) kullanabilirsiniz. Ortak yönetimi Configuration Manager sürüm 1906 ' den başlayarak etkinleştirmek için aşağıdaki yönergeleri izleyin:

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **ortak yönetim** düğümünü seçin. **Ortak yönetim Yapılandırma Sihirbazı**'nı açmak için Şeritteki **ortak yönetimi Yapılandır** ' ı seçin.

1. Sihirbazın **kiracı ekleme** sayfasında, kullanılacak **Azure ortamını** yapılandırın. Aşağıdaki ortamlardan birini seçin:

   - Azure genel bulutu
   - Azure ABD kamu bulutu.<!--4075452-->
   - Azure Çin bulutu (sürüm 2006 ' de eklendi)<!--7133238-->
      - Azure Çin bulutuna eklemeden önce Configuration Manager istemcisini cihazlarınızda en son sürüme güncelleştirin. <!--7630213--> 

   Azure Çin bulutu veya Azure ABD Kamu Bulutu ' nı seçtiğinizde, [kiracı iliştirme](../../tenant-attach/device-sync-actions.md) Için **Microsoft Uç Nokta Yöneticisi Yönetim Merkezi 'ne yükle** seçeneği devre dışıdır.

1. **Oturum aç '** ı seçin. Azure AD Genel Yöneticisi olarak oturum açın ve ardından **İleri**' yi seçin. Bu sihirbazın amaçları doğrultusunda bu bir kez oturum açmanız gerekir. Kimlik bilgileri başka bir yerde depolanmaz veya yeniden kullanılmaz.

1. **Etkinleştirme** sayfasında, aşağıdaki ayarları seçin:

   - **Intune 'Da otomatik kayıt** -mevcut Configuration Manager Istemcileri için Intune 'da otomatik istemci kaydına izin vermez. Bu seçenek, başlangıçta ortak yönetimi test etmek ve aşamalı bir yaklaşım kullanarak ortak yönetimi sunmak için bir istemciler alt kümesinde ortak yönetimi etkinleştirmenizi sağlar. Bir cihazın Kullanıcı tarafından kaydı geri alıyorsa, ilkenin bir sonraki değerlendirmesi sırasında yeniden kaydedilir. <!--3330596-->

      - **Pilot** -yalnızca **Intune otomatik kayıt** koleksiyonunun üyesi olan Configuration Manager istemciler otomatik olarak Intune 'a kaydedilir.
      - **All** -tüm Windows 10, sürüm 1709 veya üzeri istemciler için otomatik kaydı etkinleştirin.

   - **Intune otomatik kayıt** -bu koleksiyon, ortak yönetime eklemek istediğiniz tüm istemcileri içermelidir. Bu aslında diğer tüm hazırlama koleksiyonlarının bir üst kümesidir.

   ![Intune otomatik kayıt toplamayı belirtin ](../media/3555750-co-management-onboarding-enablement.png)
      
      Otomatik kayıt tüm istemciler için anında değil. Bu davranış, büyük ortamlar için kayıt ölçeklendirilmesine yardımcı olur. İstemci sayısına göre Configuration Manager rastgele kayıt. Örneğin, ortamınız 100.000 istemci içeriyorsa, bu ayarı etkinleştirdiğinizde, kayıt birkaç gün boyunca gerçekleşir.<!--1358003-->

      > [!Note]  
      > 1906 sürümünden itibaren:
      >
      > - Yeni bir ortak yönetilen cihaz artık, Azure Active Directory (Azure AD) *cihaz* belirtecine göre Microsoft Intune hizmetine otomatik olarak kaydeder. Kullanıcının otomatik kayıt işleminin başlaması için cihazda oturum açmasını beklemesi gerekmez. Bu değişiklik, *kullanıcının oturum açmasını bekleyen*cihaz sayısını azaltmaya yardımcı olur.<!-- 4454491 --> Bu davranışı desteklemek için, cihazın Windows 10, sürüm 1803 veya sonraki bir sürümü çalıştırması gerekir. Daha fazla bilgi için bkz. [ortak yönetim kayıt durumu](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Zaten ortak yönetime kaydedilmiş cihazlara sahipseniz, yeni cihazlar artık [önkoşulları](../overview.md#prerequisites)karşıladıktan hemen sonra kaydolur.<!--4321130-->

1. Intune 'a zaten kayıtlı olan internet tabanlı cihazlar için, **etkinleştirme** sayfasında komut satırını kopyalayın ve kaydedin. Bu komut satırını, Configuration Manager istemcisini Internet tabanlı cihazlar için Intune 'da bir uygulama olarak yüklemek üzere kullanacaksınız. Bu komut satırını şimdi kaydetmezseniz, bu komut satırını almak için istediğiniz zaman ortak yönetim yapılandırmasını gözden geçirebilirsiniz.

1. **Iş yükleri** sayfasında, her iş yükü Için, Intune ile yönetim için hangi cihaz grubunun üzerine taşınacağını seçin. Daha fazla bilgi için bkz. [Iş yükleri](../workloads.md). Yalnızca ortak yönetimi etkinleştirmek istiyorsanız, iş yüklerine Şimdi geçiş yapmanız gerekmez. İş yüklerini daha sonra geçirebilirsiniz. Daha fazla bilgi için bkz. [iş yüklerini değiştirme](../how-to-switch-workloads.md).  

    - **Pilot Intune** -ilgili iş yükünü yalnızca **hazırlama** sayfasında belirttiğiniz pilot koleksiyonlardaki cihazlar için geçirir. Her iş yükünün farklı bir pilot koleksiyonu olabilir.
    - **Intune** -ilişkili iş yükünü tüm ortak yönetilen Windows 10 cihazları için geçirir.  

    > [!Important]
    > Herhangi bir iş yükünü değiştirmeden önce, Intune 'da ilgili iş yükünü doğru şekilde yapılandırıp dağıttığınızdan emin olun. İş yüklerinin her zaman cihazlarınızın yönetim araçlarından biri tarafından yönetildiğinden emin olun.  

1. **Hazırlama** sayfasında, **pilot Intune**olarak ayarlanan her iş yükü için pilot koleksiyonu belirtin.

   ![Ortak yönetim Yapılandırma Sihirbazı, hazırlama sayfası, pilot koleksiyonları belirtme](../media/3555750-co-management-onboarding-staging.png)

1. Ortak yönetimi etkinleştirmek için Sihirbazı doldurun.
