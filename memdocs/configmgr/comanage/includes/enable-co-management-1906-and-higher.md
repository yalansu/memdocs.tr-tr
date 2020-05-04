---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
ms.openlocfilehash: 37376d137409b06816d4c5dff5a0909f57531443
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710898"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **ortak yönetim** düğümünü seçin. **Ortak yönetim Yapılandırma Sihirbazı**'nı açmak için şeritte **ortak yönetimi yapılandırma** ' ya tıklayın.

2. Sihirbazın **abonelik** sayfasında, aşağıdaki ayarları yapılandırın:

    - Kullanılacak **Azure ortamı** . Örneğin, Azure genel bulutu veya Azure ABD kamu bulutu.<!--4075452-->  

    - **Oturum aç '** ı seçin. Azure AD Genel Yöneticisi olarak oturum açın ve ardından **İleri**' yi seçin.  

        > [!TIP]
        > Bu sihirbazın amaçları doğrultusunda bu bir kez oturum açmanız gerekir. Kimlik bilgileri başka bir yerde depolanmaz veya yeniden kullanılmaz.

3. **Etkinleştirme** sayfasında, aşağıdaki ayarları seçin:

   - **Intune 'Da otomatik kayıt** -mevcut Configuration Manager Istemcileri için Intune 'da otomatik istemci kaydına izin vermez. Bu seçenek, başlangıçta ortak yönetimi test etmek ve aşamalı bir yaklaşım kullanarak ortak yönetimi sunmak için bir istemciler alt kümesinde ortak yönetimi etkinleştirmenizi sağlar. Bir cihazın Kullanıcı tarafından kaydı geri alıyorsa, ilkenin bir sonraki değerlendirmesi sırasında yeniden kaydedilir. <!--3330596-->

      - **Pilot** -yalnızca **Intune otomatik kayıt** koleksiyonunun üyesi olan Configuration Manager istemciler otomatik olarak Intune 'a kaydedilir.
      - **All** -tüm Windows 10, sürüm 1709 veya üzeri istemciler için otomatik kaydı etkinleştirin.

   - **Intune otomatik kayıt** -bu koleksiyon, ortak yönetime eklemek istediğiniz tüm istemcileri içermelidir. Bu aslında diğer tüm hazırlama koleksiyonlarının bir üst kümesidir.

   ![Intune otomatik kayıt toplamayı belirtin ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > Sürüm 1806 ' den başlayarak, otomatik kayıt tüm istemciler için hemen olmaz. Bu davranış, büyük ortamlar için kayıt ölçeklendirilmesine yardımcı olur. İstemci sayısına göre Configuration Manager rastgele kayıt. Örneğin, ortamınız 100.000 istemci içeriyorsa, bu ayarı etkinleştirdiğinizde, kayıt birkaç gün boyunca gerçekleşir.<!--1358003-->  
      >
      > 1906 sürümünden itibaren:
      >
      > - Yeni bir ortak yönetilen cihaz artık, Azure Active Directory (Azure AD) *cihaz* belirtecine göre Microsoft Intune hizmetine otomatik olarak kaydeder. Kullanıcının otomatik kayıt işleminin başlaması için cihazda oturum açmasını beklemesi gerekmez. Bu değişiklik, *kullanıcının oturum açmasını bekleyen*cihaz sayısını azaltmaya yardımcı olur.<!-- 4454491 --> Bu davranışı desteklemek için, cihazın Windows 10, sürüm 1803 veya sonraki bir sürümü çalıştırması gerekir. Daha fazla bilgi için bkz. [ortak yönetim kayıt durumu](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Zaten ortak yönetime kaydedilmiş cihazlara sahipseniz, yeni cihazlar artık [önkoşulları](../overview.md#prerequisites)karşıladıktan hemen sonra kaydolur.<!--4321130-->

4. Intune 'a zaten kayıtlı olan internet tabanlı cihazlar için, **etkinleştirme** sayfasında komut satırını kopyalayın ve kaydedin. Bu komut satırını, Configuration Manager istemcisini Internet tabanlı cihazlar için Intune 'da bir uygulama olarak yüklemek üzere kullanacaksınız. Bu komut satırını şimdi kaydetmezseniz, bu komut satırını almak için istediğiniz zaman ortak yönetim yapılandırmasını gözden geçirebilirsiniz.

5. **Iş yükleri** sayfasında, her iş yükü Için, Intune ile yönetim için hangi cihaz grubunun üzerine taşınacağını seçin. Daha fazla bilgi için bkz. [Iş yükleri](../workloads.md). Yalnızca ortak yönetimi etkinleştirmek istiyorsanız, iş yüklerine Şimdi geçiş yapmanız gerekmez. İş yüklerini daha sonra geçirebilirsiniz. Daha fazla bilgi için bkz. [iş yüklerini değiştirme](../how-to-switch-workloads.md).  

    - **Pilot Intune** -ilgili iş yükünü yalnızca **hazırlama** sayfasında belirttiğiniz pilot koleksiyonlardaki cihazlar için geçirir. Her iş yükünün farklı bir pilot koleksiyonu olabilir.
    - **Intune** -ilişkili iş yükünü tüm ortak yönetilen Windows 10 cihazları için geçirir.  

    > [!Important]
    > Herhangi bir iş yükünü değiştirmeden önce, Intune 'da ilgili iş yükünü doğru şekilde yapılandırıp dağıttığınızdan emin olun. İş yüklerinin her zaman cihazlarınızın yönetim araçlarından biri tarafından yönetildiğinden emin olun.  

6. **Hazırlama** sayfasında, **pilot Intune**olarak ayarlanan her iş yükü için pilot koleksiyonu belirtin.

   ![Intune otomatik kayıt toplamayı belirtin ](../media/3555750-co-management-onboarding-staging.png)

7. Ortak yönetimi etkinleştirmek için Sihirbazı doldurun.
