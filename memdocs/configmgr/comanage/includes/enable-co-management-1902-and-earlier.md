---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 4c669bbbd9f996ae820f695925ba63cd6a92da2a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127332"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
Configuration Manager sürüm 1902 ve önceki sürümleri için ortak yönetimi etkinleştirmek üzere aşağıdaki yönergeleri izleyin:

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **ortak yönetim** düğümünü seçin. **Ortak yönetim Yapılandırma Sihirbazı**'nı açmak için şeritte **ortak yönetimi yapılandırma** ' ya tıklayın.

2. Sihirbazın **abonelik** sayfasında **oturum aç**' ı seçin. Intune kiracınızda oturum açın ve ardından **İleri**' yi seçin.  

3. **Etkinleştirme** sayfasında, **Tüm** **pilot** veya hepsi **Intune ayarında otomatik kayıt** seçeneğini belirleyin. Bir cihazın Kullanıcı tarafından kaydı geri alıyorsa, ilkenin bir sonraki değerlendirmesi sırasında yeniden kaydedilir. <!--3330596--> 

    Bu eylem, mevcut Configuration Manager istemcileri için Intune 'da otomatik istemci kaydına izin vermez. **Pilot**' ı seçtiğinizde yalnızca pilot koleksiyonun üyesi olan Configuration Manager istemciler otomatik olarak Intune 'a kaydedilir. Bu seçenek, başlangıçta ortak yönetimi test etmek ve aşamalı bir yaklaşım kullanarak ortak yönetimi sunmak için bir istemciler alt kümesinde ortak yönetimi etkinleştirmenizi sağlar. 

    Otomatik kayıt tüm istemciler için anında değil. Bu davranış, büyük ortamlar için kayıt ölçeklendirilmesine yardımcı olur. İstemci sayısına göre Configuration Manager rastgele kayıt. Örneğin, ortamınız 100.000 istemci içeriyorsa, bu ayarı etkinleştirdiğinizde, kayıt birkaç gün boyunca gerçekleşir.<!--1358003-->  

4. Intune 'a zaten kayıtlı olan internet tabanlı cihazlar için, **etkinleştirme** sayfasında komut satırını kopyalayın ve kaydedin. Configuration Manager istemcisini Intune 'da uygulama olarak yüklemek için bu komut satırını kullanabilirsiniz. Bu komut satırını şimdi kaydetmezseniz, bu komut satırını almak için istediğiniz zaman ortak yönetim yapılandırmasını gözden geçirebilirsiniz.

5. **Iş yükleri** sayfasında, her iş yükü Için, Intune ile yönetim için hangi cihaz grubunun üzerine taşınacağını seçin. Daha fazla bilgi için bkz. [Iş yükleri](../workloads.md).  

    Yalnızca ortak yönetimi etkinleştirmek istiyorsanız, iş yüklerine Şimdi geçiş yapmanız gerekmez. İş yüklerini daha sonra geçirebilirsiniz. Daha fazla bilgi için bkz. [iş yüklerini değiştirme](../how-to-switch-workloads.md).  

    **Pilot Intune** ayarı, ilişkili iş yükünü yalnızca pilot koleksiyondaki cihazlar için değiştirir. **Intune** ayarı, tüm ortak yönetilen Windows 10 cihazları için ilişkili iş yükünü değiştirir.  

    > [!Important]
    > Herhangi bir iş yükünü değiştirmeden önce, Intune 'da ilgili iş yükünü doğru şekilde yapılandırıp dağıttığınızdan emin olun. İş yüklerinin her zaman cihazlarınızın yönetim araçlarından biri tarafından yönetildiğinden emin olun.  

6. **Hazırlama** sayfasında, aşağıdaki ayarları yapılandırın:  

    - **Pilot**: pilot grubu seçtiğiniz bir veya daha fazla koleksiyonu içerir. Bu grubu, ortak yönetim 'in aşamalı olarak piyasaya çıkmalarınızın bir parçası olarak kullanın. Küçük bir test koleksiyonuyla başlayın ve daha fazla Kullanıcı ve cihaza ortak yönetimi kullanıma sunarak pilot grubuna daha fazla koleksiyon ekleyin. Pilot grubundaki koleksiyonları dilediğiniz zaman değiştirebilirsiniz.  

    - **Üretim**: **dışlama grubunu** bir veya daha fazla koleksiyon ile yapılandırın. Bu gruptaki koleksiyonların herhangi birinin üyesi olan cihazlar ortak yönetim kullanılarak hariç tutulur.  

7. Ortak yönetimi etkinleştirmek için Sihirbazı doldurun.  
