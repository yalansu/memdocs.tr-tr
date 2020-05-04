---
title: İstemci durumunu yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager istemci durumu ayarlarını seçin.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bb77e1e9f55919a03368d549946ee4dd1cda58a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713579"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Configuration Manager istemci durumunu yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemci durumunu izleyebilmeniz ve bulunan sorunları düzeltmeden önce, sitenizi istemcileri devre dışı olarak işaretlemek için kullanılan parametreleri belirtecek şekilde yapılandırmanız ve istemci etkinliği belirtilen eşiğin altına düştüğünde sizi uyaracak seçenekleri yapılandırmanız gerekir. Ayrıca bilgisayarların, istemci durumunun bulduğu sorunları otomatik olarak yeniden çözdüğünü de devre dışı bırakabilirsiniz.  

##  <a name="to-configure-client-status"></a><a name="BKMK_1"></a>Istemci durumunu yapılandırmak için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  **İzleme** çalışma alanında **istemci durumu**' na tıklayın, ardından **giriş** sekmesinde, **istemci durumu** grubunda **istemci durumu ayarları**' na tıklayın.  

3.  **Istemci durumu ayarları özellikleri** iletişim kutusunda, istemci etkinliğini belirlemek için aşağıdaki değerleri belirtin:  

    > [!NOTE]  
    >  Ayarlardan hiçbiri karşılanmazsa, istemci etkin değil olarak işaretlenir.  

    -   **Şu günlerde istemci ilkesi istekleri:** Bir istemcinin ilkeyi istemesinden itibaren geçen gün sayısını belirtin. Varsayılan değer **7** gündür.  

    -   **Şu günlerde sinyal bulma:** İstemci bilgisayarın site veritabanına bir sinyal bulma kaydı göndermesinden itibaren geçen gün sayısını belirtin. Varsayılan değer **7** gündür.  

    -   **Şu günlerde donanım envanteri:** İstemci bilgisayarın site veritabanına donanım Envanter kaydı göndermesinden itibaren geçen gün sayısını belirtin. Varsayılan değer **7** gündür.  

    -   **Şu günlerde yazılım envanteri:** İstemci bilgisayarın site veritabanına yazılım envanter kaydı göndermesinden itibaren geçen gün sayısını belirtin. Varsayılan değer **7** gündür.  

    -   **Şu günlerde durum iletileri:** İstemci bilgisayarın site veritabanına durum iletileri göndermesinden itibaren geçen gün sayısını belirtin. Varsayılan değer **7** gündür.  

4.  İstemci durumu **ayarları özellikleri** iletişim kutusunda, istemci durum geçmişi verilerinin ne kadar süreyle tutulacağını belirlemek için aşağıdaki değeri belirtin:  

    -   **İstemci durum geçmişini Şu sayıda gün boyunca sakla:** İstemci durum geçmişinin site veritabanında ne kadar süreyle kalmasını istediğinizi belirtin. Varsayılan değer **31** gündür.  

5.  Özellikleri kaydetmek ve **Istemci durumu ayarları özellikleri** iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.  

##  <a name="to-configure-the-schedule-for-client-status"></a><a name="BKMK_Schedule"></a>Istemci durumunun zamanlamasını yapılandırmak için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  **İzleme** çalışma alanında **istemci durumu**' nu tıklatın, ardından **giriş** sekmesinde, **istemci durumu** grubunda **istemci durumu güncelleştirmesini zamanla**' yı tıklatın.  

3.  **Istemci durumu güncelleştirmesini zamanla** iletişim kutusunda, istemci durumunun güncelleştirilmesini istediğiniz aralığı yapılandırın ve ardından Tamam ' a tıklayın.  

    > [!NOTE]  
    >  İstemci durumu güncelleştirmeleri için zamanlamayı değiştirdiğinizde güncelleştirme, bir sonraki zamanlanmış istemci durum güncelleştirmesine (daha önce yapılandırılmış zamanlama için) kadar etkili olmayacaktır.  

##  <a name="to-configure-alerts-for-client-status"></a><a name="BKMK_2"></a>Istemci durumu uyarılarını yapılandırmak için  

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2. **Varlıklar ve Uyum** çalışma alanında, **Aygıt Koleksiyonları**'nı tıklatın.  

3. **Cihaz Koleksiyonları** listesinde, uyarıları yapılandırmak istediğiniz koleksiyonu seçin ve sonra **Giriş** sekmesinde, **Özellikler** grubunda **Özellikler**'i tıklatın.  

   > [!NOTE]  
   >  Kullanıcı koleksiyonları için uyarılar yapılandıramasınız.  

4. **Properties** <em>\>Koleksiyon adı Özellikler iletişim kutusunun uyarılar sekmesinde Ekle ' ye &lt;</em>tıklayın. **Alerts** **Add**  

   > [!NOTE]  
   >  **Uyarılar** sekmesi yalnızca, ilişkilendirilmiş olduğunuz güvenlik rolünün uyarılarla ilgili izinleri varsa görünür.  

5. **Yeni Koleksiyon Uyarıları Ekle** iletişim kutusunda, istemci durumu eşikleri belirli bir değerin altında kaldığında oluşturulmasını istediğiniz uyarıları seçin ve **Tamam**'ı tıklatın.  

6. **Uyarılar** sekmesinin **Koşullar** listesinde, her istemci durumu uyarısını seçip aşağıdaki bilgileri belirtin.  

   -   **Uyarı adı** -varsayılan adı kabul edin veya uyarı için yeni bir ad girin.  

   -   **Uyarı önem derecesi** -aşağı açılan listeden Configuration Manager konsolunda görüntülenecek uyarı düzeyini seçin.  

   -   **Uyarı oluştur** -uyarı için eşik yüzdesini belirtin.  

7. **Properties** <em>\>Koleksiyon adı Özellikler iletişim kutusunu kapatmak için Tamam ' ı &lt;</em>tıklatın. **OK**  

##  <a name="to-exclude-computers-from-automatic-remediation"></a><a name="BKMK_3"></a>Bilgisayarları otomatik düzeltmeden dışlamak için  

1. Otomatik düzeltmeyi devre dışı bırakmak istediğiniz istemci bilgisayarda kayıt defteri düzenleyicisini açın.  

   > [!WARNING]  
   >  Kayıt Defteri Düzenleyicisi 'Ni yanlış kullanırsanız, işletim sisteminizi yeniden yüklemenizi gerektirebilecek önemli sorunlara neden olabilirsiniz. Microsoft, Kayıt Defteri Düzenleyicisi'ni yanlış kullanımınızdan kaynaklanan sorunları çözebileceğinizi garanti edemez. Kayıt Defteri Düzenleyicisi'ni kullanım riski size aittir.  

2. **HKEY_LOCAL_MACHINE \Software\Microsoft\CCM\CcmEval\NotifyOnly**konumuna gidin.  

3. Bu kayıt defteri anahtarı için aşağıdaki değerlerden birini girin:  

   -   **Doğru** -istemci bilgisayar, bulunan sorunları otomatik olarak düzeltmeyecektir. Ancak, bu istemciyle ilgili herhangi bir sorun hakkında **izleme** çalışma alanında yine de uyarı alırsınız.  

   -   **Yanlış** -istemci bilgisayar bulunan sorunları otomatik olarak düzeltir ve **izleme** çalışma alanında uyarı alırsınız. Bu varsayılan ayardır.  

4. Kayıt defteri düzenleyicisini kapatın.  

   Ayrıca, istemcileri otomatik düzeltmeden dışlamak için CCMSetup **Notifyonly** yükleme özelliğini kullanarak da yükleyebilirsiniz. Bu istemci yükleme özelliği hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties.md).  
