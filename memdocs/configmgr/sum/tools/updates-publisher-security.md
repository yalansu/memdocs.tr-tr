---
title: Sertifikalar ve güvenlik
titleSuffix: Configuration Manager
description: System Center Updates Publisher için sertifikaları ve güvenliği yönetme
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc8e31245212136cd67f6f8cac062723c2cabefb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696013"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Updates Publisher için sertifikaları ve güvenliği yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki yordamlar, güncelleştirme sunucusunda sertifika deposunu yapılandırmanıza, istemci bilgisayarda bir otomatik imzalama sertifikasını yapılandırmanıza ve grup ilkesi, bilgisayarlardaki Windows Update aracısının yayımlanan güncelleştirmeleri taramasına izin verecek şekilde yapılandırmanıza yardımcı olabilir.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Güncelleştirme sunucusunda sertifika deposunu yapılandırma
 Updates Publisher, yayımladığı kataloglarda güncelleştirmeleri imzalamak için dijital bir sertifika kullanır. Bir kataloğun güncelleştirme sunucusunda yayımlanabilmesi için, bu sertifikanın güncelleştirme sunucusundaki sertifika deposunda ve bu bilgisayar güncelleştirme sunucusundan uzakta olduğunda Updates Publisher bilgisayarının sertifika deposunda olması gerekir.

Aşağıdaki yordam, sertifikayı güncelleştirme sunucusundaki sertifika deposuna eklemenin birkaç olası yönteminden biridir.

### <a name="to-configure-the-certificate-store"></a>Sertifika deposunu yapılandırmak için
1.  Güncelleştirme yayımcısı bilgisayarına ve güncelleştirme sunucusuna erişebilen bir bilgisayarda, **Başlat**' a tıklayın, **Çalıştır**' a tıklayın, metin kutusuna **MMC** yazın ve ardından **Tamam** ' a tıklayarak Microsoft Yönetim Konsolu 'nu (MMC) açın.

2.  **Dosya**, **ek bileşen Ekle/Kaldır**' a tıklayın, **Ekle**' ye tıklayın, **Sertifikalar**' a tıklayın, **Ekle**' ye tıklayın, **bilgisayar hesabı**' nı seçin ve ardından **İleri**

3.  **Başka bir bilgisayar**seçin, güncelleştirme sunucusunun adını yazın veya güncelleştirme sunucusu bilgisayarını **bulmak için, Tamam ' a** tıklayın, **son**' a tıklayın, **Kapat**' a tıklayın ve ardından **Tamam**' a tıklayın.

4.  **Sertifikalar (*sunucu adını Güncelleştir*)** öğesini genişletin, **WSUS**' u genişletin ve **Sertifikalar**' a tıklayın.

5.  Sonuçlar bölmesinde, istenen sertifikaya sağ tıklayın, **Tüm görevler**' e ve ardından **dışarı aktar**' a tıklayın.

6.  Sertifika dışarı aktarma sihirbazında, sihirbazda belirtilen ad ve konuma sahip bir dışarı aktarma dosyası oluşturmak için varsayılan ayarları kullanın. Sonraki adıma geçmeden önce bu dosya güncelleştirme sunucusu için kullanılabilir olmalıdır.

7.  **Güvenilen Yayımcılar**' a sağ tıklayın, **Tüm görevler**' e ve ardından **içeri aktar**' a tıklayın. Adım 6 ' dan dışarı aktarılan dosyayı kullanarak sertifika Içeri aktarma Sihirbazı 'nı doldurun.

8.  Otomatik olarak imzalanan bir sertifika kullanılıyorsa (örneğin, **WSUS yayımcıları kendinden imzalı**), **Güvenilen kök sertifika yetkilileri**' ne sağ tıklayın, **Tüm görevler**' e ve ardından **içeri aktar**' a tıklayın. Adım 6 ' dan dışarı aktarılan dosyayı kullanarak sertifika Içeri aktarma Sihirbazı 'nı doldurun.

9.  Sertifikalar ' a sağ tıklayın **(*sunucu adını Güncelleştir*)**, **başka bir bilgisayara bağlan**' a tıklayın, Updates Publisher bilgisayarı için bilgisayar adını girin ve **Tamam**' a tıklayın.

10. Updates Publisher, güncelleştirme sunucusundan uzak ise, sertifikayı Updates Publisher bilgisayarındaki sertifika deposuna aktarmak için 7 ' den 9 ' a kadar olan adımları yineleyin.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>İstemci bilgisayarlarda bir otomatik imzalama sertifikası yapılandırma
İstemci bilgisayarlarda, Windows Update Aracısı (WUA), güncelleştirmeleri katalogdan tarar. Bu işlem, aracı yerel bilgisayardaki güvenilen yayımcılar deposunda bulunan dijital sertifikayı bulamıyorsa güncelleştirmeleri yükleyemez. Güncelleştirme kataloğunu yayımlamak için otomatik olarak imzalanan bir sertifika kullanılmışsa (örneğin, **WSUS yayımcıları, otomatik imzalı**), aracının sertifikanın geçerliliğini doğrulayabilmesi için sertifikanın yerel bilgisayardaki güvenilen kök sertifika yetkilileri sertifika deposunda da olması gerekir.

İstemci bilgisayarlarda grup ilkesi ve **sertifika Içeri aktarma Sihirbazı 'nı** veya Certutil aracını ve yazılım dağıtımını kullanarak sertifika yapılandırmak için çeşitli yöntemlerden birini kullanabilirsiniz.

Aşağıdakiler, istemci bilgisayarlarda imza sertifikasının nasıl yapılandırılacağı hakkında bir örnek olarak sunulmaktadır.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>İstemci bilgisayarlarda bir otomatik imza sertifikası yapılandırmak için
1. Güncelleştirme sunucusuna erişimi olan bir bilgisayarda, **Başlat**' a tıklayın, **Çalıştır**' a tıklayın, metin kutusuna **MMC** yazın ve ardından **Tamam** ' a tıklayarak Microsoft Yönetim Konsolu 'nu (MMC) açın.

2. **Dosya**, **ek bileşen Ekle/Kaldır**' a tıklayın, **Ekle**' ye tıklayın, **Sertifikalar**' a tıklayın, **Ekle**' ye tıklayın, **bilgisayar hesabı**' nı seçin ve ardından **İleri**

3. **Başka bir bilgisayar**seçin, güncelleştirme sunucusunun adını yazın veya güncelleştirme sunucusu bilgisayarını **bulmak için, Tamam ' a** tıklayın, **son**' a tıklayın, **Kapat**' a tıklayın ve ardından **Tamam**' a tıklayın.

4. **Sertifikalar (*sunucu adını Güncelleştir*)** öğesini genişletin, **WSUS**' u genişletin ve **Sertifikalar**' a tıklayın.

5. Sonuçlar bölmesinde sertifikaya sağ tıklayın, **Tüm görevler**' e ve ardından **dışarı aktar**' a tıklayın. Sihirbazda belirtilen ad ve konumla bir dışarı aktarma sertifikası dosyası oluşturmak için varsayılan ayarları kullanarak **sertifika dışarı aktarma Sihirbazı** 'nı doldurun.

6. Güncelleştirme kataloğunu, katalogdaki güncelleştirmeleri taramak üzere WUA kullanacak olan her bir istemci bilgisayara eklemek için aşağıdaki yöntemlerden birini kullanın. Sertifikayı istemci bilgisayara aşağıdaki gibi ekleyin:

   -   Otomatik olarak imzalanan sertifikalar için: sertifikayı **Güvenilen kök sertifika yetkililerine** ve **Güvenilen Yayımcılar** sertifika depolarına ekleyin.

   -   Sertifika yetkilisi (CA) tarafından verilen sertifikalar için: sertifikayı **Güvenilen Yayımcılar** sertifika deposuna ekleyin.

   > [!NOTE]
   > WUA Ayrıca yerel bilgisayarda **Intranet Microsoft güncelleştirme hizmeti konumundan imzalı Içeriğe Izin ver** Grup İlkesi ayarının etkinleştirilip etkinleştirilmediğini denetler. Updates Publisher ile oluşturulup yayımlanan güncelleştirmeleri taramak üzere WUA için bu ilke ayarı etkinleştirilmelidir. Bu grup ilkesi ayarını etkinleştirme hakkında daha fazla bilgi için bkz. [Istemci bilgisayarlarda Grup ilkesi yapılandırma](/previous-versions/bb530967(v=technet.10)).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Bilgisayarlarda WUA 'nın yayımlanan güncelleştirmeleri taramasına izin vermek için grup ilkesi yapılandırma
Bilgisayarlardaki Windows Update Aracısı (WUA), Updates Publisher ile oluşturulup yayımlanan güncelleştirmeleri taramadan önce, bir intranet Microsoft güncelleştirme hizmeti konumundan imzalı içeriğe izin vermek için bir ilke ayarı etkinleştirilmelidir. İlke ayarı etkinleştirildiğinde, güncelleştirmeler yerel bilgisayardaki **Güvenilen Yayımcılar** sertifika deposunda IMZALANMıŞSA, WUA bir intranet konumu üzerinden alınan güncelleştirmeleri kabul eder. Ortamındaki bilgisayarlarda grup ilkesi yapılandırmak için çeşitli yöntemler vardır.

Etki alanında olmayan bilgisayarlar için, bir intranet Microsoft Update hizmet konumundan imzalı içeriğe izin veren bir kayıt defteri anahtarı ayarı yapılandırılabilir.

Aşağıdaki yordamlarda, etki alanındaki bilgisayarlar için grup ilkesi yapılandırmak için kullanılabilen temel adımlar ve etki alanında olmayan bilgisayarlardaki bir kayıt defteri anahtarı değeri sağlanmaktadır.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>grup ilkesi yapılandırmak için, WUA 'ın yayımlanan güncelleştirmeleri taramasına izin ver
1.  Grup ilkesi yapılandırmak için uygun güvenlik haklarına sahip bir kullanıcıyla Microsoft Yönetim Konsolu (MMC) ek bileşenini Grup İlkesi Nesne Düzenleyicisi açın.

2.  **Araştır** ' a tıklayın ve yapılandırılmış Grup İlkesi istenen istemci bilgisayarlara yaykaydedileceği siteye bağlı etki ALANıNı, OU veya GPO 'ları seçin. **Tamam**' a, **son**' a, **Kapat**' a ve ardından **Tamam**' a tıklayın.

3.  Konsol ağacındaki seçili ilke ayarını genişletin, **bilgisayar yapılandırması**' nı genişletin, **Yönetim Şablonları**' ı genişletin, **Windows bileşenleri**' ni genişletin ve ardından **Windows Update**' e tıklayın.

4.  Sonuçlar bölmesinde, **Intranet Microsoft güncelleştirme hizmeti konumundan imzalı Içeriğe Izin ver**' e sağ tıklayın, **Özellikler**' e tıklayın, **etkin**' e ve ardından **Tamam**' a tıklayın.