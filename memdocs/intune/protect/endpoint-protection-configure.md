---
title: Microsoft Intune - Azure’da Endpoint Protection ayarlarını yapılandırma | Microsoft Docs
description: Microsoft Intune’da bir macOS veya Windows 10 cihaz profili oluşturduğunuzda Endpoint Protection ayarları oluşturun.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 226416c896a3d21ad8e2d11868433353c6965c6c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910885"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Intune’da Endpoint Protection ayarları ekleme

Intune ile, cihazlarda aşağıdakiler de dahil olmak üzere ortak uç nokta koruma güvenlik özelliklerini yönetmek için cihaz yapılandırma profillerini kullanabilirsiniz:

- Güvenlik duvarı
- BitLocker
- Uygulamalara izin verme ve bunları engelleme
- Microsoft Defender ve şifreleme

Örneğin yalnızca macOS kullanıcılarının Mac App Store’dan uygulama indirmesine izin veren bir Endpoint Protection profili oluşturabilirsiniz. Veya Windows 10 cihazlarda uygulama çalıştırırken Windows SmartScreen’i etkinleştirebilirsiniz.

Bir profil oluşturmadan önce, Intune 'un desteklenen her platform için yöneteceği Endpoint Protection ayarlarını ayrıntılandırın aşağıdaki makalelerini gözden geçirin:

- [macOS ayarları](endpoint-protection-macos.md)
- [Windows 10 ayarları](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Endpoint Protection ayarlarını içeren bir cihaz profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. Aşağıdaki özellikleri girin:

    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:

        - **macOS**
        - **Windows 10 ve üzeri**

    - **Profil**: **Endpoint Protection**' ı seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

   - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı profil türünü ve platformunu içerebilir.

   - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

   - [macOS ayarları](endpoint-protection-macos.md)
   - [Windows 10 ayarları](endpoint-protection-windows-10.md)

8. **İleri**’yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Windows 10 cihazları için özel güvenlik duvarı kuralları ekleme

Microsoft Defender güvenlik duvarını Windows 10 için Endpoint Protection kurallarını içeren bir profilin parçası olarak yapılandırdığınızda güvenlik duvarları için özel kurallar yapılandırabilirsiniz. Özel kurallar, Windows 10 için desteklenen önceden tanımlanmış güvenlik duvarı kuralları kümesini genişletmenizi sağlar.

Özel güvenlik duvarı kuralları içeren profiller için plan yaparken, profillerinizin güvenlik duvarı kurallarını nasıl seçecağınızı etkileyebilecek aşağıdaki bilgileri göz önünde bulundurun:

- Her profil en fazla 150 güvenlik duvarı kuralını destekler. 150 'den fazla kural kullandığınızda, her biri 150 kuralla sınırlı ek profiller oluşturun.

- Her profil için, tek bir kural uygulanamazsa, bu profildeki tüm kurallar başarısız olur ve kurala hiçbiri cihaza uygulanmaz.

- Bir kural uygulanamazsa, profildeki tüm kurallar başarısız olarak bildirilir. Intune hangi bağımsız kuralın başarısız olduğunu tanımlayamıyor.  

Intune 'un yönetebileceği güvenlik duvarı kuralları, Windows [güvenlik duvarı yapılandırma hizmeti sağlayıcısı](/windows/client-management/mdm/firewall-csp) 'nda (CSP) ayrıntılı olarak açıklanmıştır. Intune 'un desteklediği Windows 10 cihazlarının özel güvenlik duvarı ayarlarının listesini gözden geçirmek için bkz. [özel güvenlik duvarı kuralları](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Uç nokta koruma profiline özel güvenlik duvarı kuralları eklemek için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. *Platform*için **Windows 10 ve üzeri**' i seçin ve ardından *profil* **Endpoint Protection**' ı seçin.

    **Oluştur**’u seçin.

4. **Daha sonra**> profiliniz Için bir **ad** girin.
5. **Yapılandırma ayarları**' nda, **Microsoft Defender güvenlik duvarı**' nı seçin. *Güvenlik duvarı kuralları*Için, **Ekle** ' yi seçerek **kural oluştur** sayfasını açın.

6. Güvenlik duvarı kuralı için ayarları belirtin ve sonra kaydetmek için **Tamam** ' ı seçin. Belgelerde bulunan özel güvenlik duvarı kuralı seçeneklerini gözden geçirmek için bkz. [özel güvenlik duvarı kuralları](endpoint-protection-windows-10.md#firewall-rules).

    1. Kural, kurallar listesindeki *Microsoft Defender güvenlik duvarı* sayfasında görüntülenir.
    2. Bir kuralı değiştirmek için listeden kuralı seçin, kuralı **Düzenle** sayfasını açın.
    3. Bir profilden bir kuralı silmek için, kural için üç nokta **(...)** simgesini seçin ve **Sil**' i seçin.
    4. Kuralların görüntülenme sırasını değiştirmek için, kural listesinin en üstündeki *yukarı ok, aşağı ok* simgesini seçin.

7. **Gözden geçirip oluştur**' a kadar **İleri ' yi** seçin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu, ancak henüz bir şey yapmamış olabilir. Ardından [profili atayın](../configuration/device-profile-assign.md) ve [durumunu izleyin](../configuration/device-profile-monitor.md).