---
title: Microsoft Intune-Azure 'da GPO 'Ları içeri aktarmak için Grup İlkesi analizlerini kullanma | Microsoft Docs
description: Microsoft Intune ve uç nokta yöneticisinde Grup İlkesi nesnelerinizi içeri aktarın ve çözümleyin. Bulutta aynı yapılandırma hizmeti sağlayıcısı (CSP) ayarına sahip olan ilkelere ve Windows 10 kullanıcılarınıza ve cihazlarınıza ata bakın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09d54a942bdd745cebd0a2c16dd77f74f0e718e7
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90816627"
---
# <a name="analyze-your-on-premises-group-policy-objects-gpo-using-group-policy-analytics-in-microsoft-endpoint-manager---preview"></a>Microsoft uç noktası yöneticisinde grup ilkesi Analytics kullanarak şirket içi Grup İlkesi nesnelerinizi (GPO) çözümleyin-Önizleme

Grup İlkesi nesneleri (GPO 'Lar), kişisel bilgisayarlarda ve diğer şirket içi cihazlarda ayarları yapılandırmak için şirket içinde kullanılır. Cihaz Yönetimi ' nde, GPO 'Lar, Windows işletim sistemi, Internet Explorer, Office uygulamaları ve daha birçok güvenlik ve özellikleri denetlemeye yardımcı olur.

Birçok kuruluş, büyüyen uzak iş gücünü desteklemek için bulut çözümlerine bakıyor. **Grup İlkesi Analytics** , Microsoft Endpoint Manager 'da şirket içi GPO 'larınızı analiz eden bir araç ve özelliktir. GPO 'larınızın bulutta nasıl çevrileceğini belirlemenize yardımcı olur. Çıktı, MDM sağlayıcıları 'nda Microsoft Intune dahil olmak üzere hangi ayarların desteklendiğini gösterir. Ayrıca, kullanım dışı bırakılmış ayarları veya MDM sağlayıcıları için kullanılamayan ayarları da gösterir.

Kuruluşunuz GPO 'Lar kullanıyorsa ve bazı iş yüklerini Microsoft Endpoint Manager ve Intune 'a taşımak istiyorsanız, grup ilkesi Analytics yardımcı olur.

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri

Bu makalede, GPO 'larınızı dışarı aktarma, GPO 'Ları Endpoint Manager 'a aktarma ve çözümleme ve sonuçları gözden geçirme işlemlerinin nasıl yapılacağı gösterilir.

## <a name="export-gpos-as-an-xml-file"></a>GPO 'Ları bir XML dosyası olarak dışarı aktar

1. Şirket içi bilgisayarınızda, `Group Policy Management` uygulamayı (GPMC. msc) açın.
2. Tüm GPO 'Ları görmek için etki alanınızı genişletin.
3. Bir GPO 'ya sağ tıklayın > **raporu kaydet**:

    :::image type="content" source="./media/group-policy-analytics/sample-group-policy-object-save-report.png" alt-text="Grup ilkesi yönetimi 'ni açın ve bir GPO 'YU bir XML dosyası raporu olarak kaydedin.":::

4. Dosyayı kolayca erişilebilen bir klasöre kaydedin ve bir XML dosyası olarak kaydedin. Bu dosyayı Endpoint Manager 'a eklersiniz.

Dosyanın 4 MB 'tan az olduğundan emin olun. 4 MB 'tan büyükse, raporunuzu kaydettiğinizde daha az GPO ekleyin.

## <a name="use-group-policy-analytics"></a>grup ilkesi Analytics kullanma

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **Grup İlkesi analiz (Önizleme)** öğesini seçin.
2. **Içeri aktar**' ı seçin ve ardından kaydedilmiş XML dosyanızı seçin. XML dosyasını seçtiğinizde, Intune, XML dosyasındaki GPO 'YU otomatik olarak analiz eder.

    Ayrı GPO XML dosyalarınızın boyutlarını denetleyin. Tek bir GPO 1 MB 'den büyük olamaz. Tek bir GPO 1 MB 'den büyükse içeri aktarma başarısız olur.

3. Analiz çalıştıktan sonra, içeri aktardığınız GPO aşağıdaki bilgilerle listelenir:

    - **Grup ilkesi adı**: ad, GPO 'daki bilgiler kullanılarak otomatik olarak oluşturulur.
    - **Hedef Active Directory**: hedef, GPO 'daki kuruluş BIRIMI (OU) hedef bilgileri kullanılarak otomatik olarak oluşturulur.
    - **MDM desteği**: Intune 'da aynı ayara sahıp olan GPO 'daki Grup İlkesi ayarlarının yüzdesini gösterir.
    - **Ad**: **Evet 'e** hedeflenmiş, GPO 'nun şirket ıçı grup ilkesindeki bir OU 'ya bağlı olması anlamına gelir. **Hayır** , GPO şirket ıçı bir OU 'ya bağlı olmadığı anlamına gelir.
    - **Son içeri**aktarma: son içeri aktarmanın tarihini gösterir.

    Analiz için daha fazla GPO **aktarabilir** , sayfayı **yenileyebilir** ve çıktıyı **filtreleyebilirsiniz** . Ayrıca, bu görünümü bir dosyaya **dışarı aktarabilirsiniz** `.csv` :

    :::image type="content" source="./media/group-policy-analytics/import-refresh-filter-options.png" alt-text="Bir Grup İlkesi nesnesi 'ni (GPO) Microsoft Intune ve Endpoint Manager Yönetim Merkezi 'ndeki bir CSV dosyasına aktarın, yenileyin, filtreleyin veya dışarı aktarın.":::

4. Listelenen bir GPO için **MDM desteği** yüzdesini seçin. GPO hakkında daha ayrıntılı bilgi gösterilir:

    - **Ayar adı**: ad, GPO ayarındaki bilgiler kullanılarak otomatik olarak oluşturulur.
    - **Grup İlkesi ayarı kategorisi**: Internet Explorer ve Microsoft Edge gibi ADMX ayarları için ayar kategorisini gösterir. Tüm ayarların ayar kategorisi yoktur.
    - **ADMX desteği**: **Evet** , bu ayar için bir ADMX şablonu olduğu anlamına gelir. **Hayır** , belirli bir ayar IÇIN bir ADMX şablonu olmadığı anlamına gelir.

      ADMX şablonları hakkında daha fazla bilgi için [Microsoft Intune Yönetim Şablonları](administrative-templates-windows.md)bakın.

    - **MDM desteği**: **Evet** , Endpoint Manager 'da eşleşen bir ayar olduğu anlamına gelir. Bu ayarı, bir cihaz yapılandırma profilinde yapılandırabilirsiniz. Cihaz yapılandırma profillerindeki ayarlar Windows CSP 'Lerine eşlenir.

      **Hayır** , MDM sağlayıcıları için Intune dahil olmak üzere uygun bir ayar olmadığı anlamına gelir.

      Cihaz yapılandırma profilleri hakkında daha fazla bilgi için bkz. [Cihaz profillerini kullanarak cihazlarınızda özellikleri ve ayarları uygulama](device-profiles.md).      

    - **Değer**: GPO 'dan içeri aktarılan değeri gösterir. ,,, Vb. gibi farklı değerleri gösterir `true` `900` `Enabled` `false` .
    - **Kapsam**: içeri aktarılan GPO 'nun kullanıcıları veya hedefleri cihazlarını hedeflediğini gösterir.
    - **En düşük işletim sistemi sürümü**: GPO ayarının geçerli olduğu en düşük Windows işletim sistemi sürümü derleme numaralarını gösterir. `18362`(1903), `17130` (1803) ve diğer Windows 10 sürümlerini gösterebilir.

      Örneğin, bir ilke ayarı gösteriyorsa `18362` , ayar derlemeyi `18362` ve daha yeni yapıları destekler.

    - **CSP adı**: bir yapılandırma hizmeti sağlayıcısı (CSP) Windows 10 ' da cihaz yapılandırma ayarlarını gösterir. Bu sütun, ayarı içeren CSP 'yi gösterir. Örneğin, Ilke, BitLocker, PassportforWork vb. görebilirsiniz.

      CSP 'Ler hakkında daha fazla bilgi için bkz. [CSP başvurusu](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).

    - **CSP eşleme**: şirket içi Ilke için OMA-URI yolunu gösterir. OMA-URI ' y i [özel bir cihaz yapılandırma profilinde](custom-settings-configure.md)kullanabilirsiniz. Örneğin, bkz `./Device/Vendor/MSFT/BitLocker/RequireDeviceEnryption` ..

## <a name="supported-csps"></a>Desteklenen CSP 'Ler

Grup ilkesi Analytics aşağıdaki CSP 'Leri ayrıştırabilirler:

- [İlke CSP 'si](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider)
- [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp)
- [BitLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)
- [Güvenlik Duvarı CSP 'si](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp)
- [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

## <a name="group-policy-migration-readiness-report"></a>grup ilkesi geçiş hazırlığı raporu

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **raporlar**  >  **Grup İlkesi Analizi (Önizleme)** öğesini seçin:

    :::image type="content" source="./media/group-policy-analytics/policy-analytics-reports.png" alt-text="Microsoft Intune ve Endpoint Manager Yönetim Merkezi 'nde grup ilkesi Analytics kullanarak içeri aktarılan GPO 'ların rapor ve çıkışını gözden geçirin.":::

2. **Özet** SEKMESINDE, GPO ve ilkelerinin bir özeti gösterilir. GPO 'daki ilkelerin durumunu öğrenmek için bu bilgileri kullanın:

    - **Geçişe hazırlanma**: ilkenin Intune 'da eşleşen bir ayarı vardır ve Intune 'a geçirilmeye hazırlanın.
    - **Desteklenmiyor**: ilkenin eşleşen bir ayarı yok. Genellikle, bu durumu gösteren ilke ayarları, Intune dahil MDM sağlayıcılarına gösterilmez.
    - **Kullanım dışı**: ilke, eski Windows sürümleri için uygulanabilir ve artık Windows 10 ve daha yeni sürümlerde kullanılmıyor olabilir.

3. **Grup İlkesi geçiş hazırlığı**> **raporlar** sekmesini seçin. Bu raporda şunları yapabilirsiniz:

    - Bir cihaz yapılandırma profilinde bulunan, özel bir profilde olabilecekleri, desteklenmiyorsa veya kullanım dışı bırakılmış olan GPO 'larınızdaki ayarların sayısını görün.
    - **Geçiş hazırlığı**, **profil türü**ve **CSP ad** filtrelerini kullanarak rapor çıkışını filtreleyin.
    - Geçerli verileri almak için **rapor oluştur** veya **yeniden oluştur** ' u seçin.
    - GPO 'larınızdaki ayarların listesine bakın.
    - Belirli ayarları bulmak için arama çubuğunu kullanın.
    - Raporun en son ne zaman oluşturulduğu zaman damgasını alır. 
    
    > [!NOTE]
    > İçeri aktarılan GPO 'larınızı ekledikten veya kaldırdıktan sonra, geçiş hazırlığı raporlama verilerinin güncelleştirilmesi yaklaşık 20 dakika sürebilir.

## <a name="privacy-and-security"></a>Gizlilik ve güvenlik

Kuruluşunuzda hangi GPO 'Ların kullanıldığı gibi müşteri verilerinin herhangi bir kullanımı toplanır. Herhangi bir üçüncü taraf satılamaz. Bu veriler, Microsoft içinde iş kararları vermek için kullanılabilir. Müşteri verileriniz güvenli bir şekilde depolanır.

Herhangi bir zamanda içeri aktarılan GPO 'Ları silebilirsiniz:

1. **Cihazlar**  >  **Grup İlkesi analiz (Önizleme)** sayfasına gidin.
2. > **Sil**bağlam menüsünü seçin:

    :::image type="content" source="./media/group-policy-analytics/delete-imported-gpo.png" alt-text="Microsoft Intune ve Endpoint Manager Yönetim Merkezi ' nde grup ilkesi Çözümleyicisi ' nde içeri aktardığınız Grup İlkesi nesnesini (GPO) silin veya kaldırın.":::

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Endpoint Manager 'da Grup İlkesi ayarlarını yapılandırmak için Windows 10 Yönetim Şablonları kullanma](administrative-templates-windows.md)

- [Microsoft Endpoint Manager 'da Endpoint Protection ayarları ekleme](../protect/endpoint-protection-configure.md)

## <a name="see-also"></a>Ayrıca bkz.

[Yapılandırma hizmeti sağlayıcıları (CSP)](https://docs.microsoft.com/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers)hakkında daha fazla bilgi edinin.
