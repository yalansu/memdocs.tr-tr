---
title: Endpoint Protection sorunlarını giderme
titleSuffix: Configuration Manager
description: Windows Defender ve Endpoint Protection ile ilgili sorunları nasıl giderebileceğinizi öğrenin.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724492"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Windows Defender veya Endpoint Protection istemcisiyle ilgili sorunları giderme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Windows Defender veya Endpoint Protection ile ilgili sorunlar yaşıyorsanız, aşağıdaki sorunları gidermek için bu makaleyi kullanın:  

- [Windows Defender veya Endpoint Protection güncelleştirme](#update-windows-defender-or-endpoint-protection)  
- [Windows Defender veya Endpoint Protection hizmeti başlatılıyor](#starting-windows-defender-or-endpoint-protection-service)  
- [Internet bağlantısı sorunları](#internet-connection-issues)  
- [Algılanan tehdit düzeltilemiyor](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a> Windows Defender veya Endpoint Protection’ı güncelleştirme

### <a name="symptoms"></a>Belirtiler

Virüs ve casus yazılım Tanımlarınızın güncel tutulduğundan emin olmak için Windows Defender veya Endpoint Protection Microsoft Update otomatik olarak çalışır.  

Bu bölümde, aşağıdaki durumlar da dahil olmak üzere otomatik güncelleştirmelerle ilgili genel sorunlar ele alınmaktadır:  

- Güncelleştirmelerin başarısız olduğunu belirten hata iletileri görüyorsunuz.  

- Güncelleştirmeleri denetlediğinizde, virüs ve casus yazılım tanımı güncelleştirmelerinin denetlenemediğini, indirilebileceğini veya yüklenmediğini belirten bir hata iletisi alırsınız.  

- Cihazınız internet 'e bağlı olsa da, güncelleştirmeler başarısız olur.  

- Güncelleştirmeler zamanlandığı gibi otomatik olarak yüklenmiyor.  

### <a name="causes"></a>Nedenler

Güncelleştirme sorunlarının en yaygın nedenleri, internet bağlantısıyla ilgili sorunlardır. Diğer Web sitelerine gözatabildiğiniz için cihazınızın İnternet 'e bağlı olduğunu biliyorsanız, sorun Windows 'daki Internet ayarlarınızdaki çakışmalar nedeniyle oluşabilir.  

### <a name="options-to-resolve"></a>Çözümleme seçenekleri

#### <a name="step-1-reset-your-internet-settings"></a>1. Adım: Internet ayarlarınızı sıfırlama  

1. Web tarayıcısı da dahil olmak üzere tüm açık programlardan çıkın.  

    > [!NOTE]  
    > Bu İnternet ayarlarını sıfırladığınızda tarayıcı geçici dosyalarınızı, tanımlama bilgilerini, gözatma geçmişini ve çevrimiçi parolaları silebilir. Sık kullanılanları silmez.  

2. **Başlat** menüsüne gidin ve açın `inetcpl.cpl`.  

3. **Gelişmiş** sekmesine geçin.  

4. **Internet Explorer ayarlarını sıfırlama**bölümünde **Sıfırla**' yı seçin ve ardından onaylamak için yeniden **Sıfırla** ' yı seçin.  

5. Ayarlar sıfırlandığında **Tamam ' ı** seçin.

6. Windows Defender 'ı yeniden güncelleştirmeyi deneyin.

Sorun devam ederse, bir sonraki adımla devam edin.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>2. Adım: bilgisayarınızda tarih ve saatin doğru ayarlandığından emin olun  

Hata iletisi 0x80072F8F kodunu içeriyorsa, sorun büyük olasılıkla bilgisayarınızdaki yanlış tarih veya saat ayarından kaynaklanıyor olabilir. **Başlat** menüsüne gidin, **Ayarlar**' ı seçin, **zaman & dili**' ni seçin ve **Tarih & saati**' ni seçin.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>3. Adım: bilgisayarınızdaki yazılım dağıtım klasörünü yeniden adlandırma  

1. **Windows Update** hizmetini durdurun.  

    1. **Başlat**' a gidin ve **Services. msc**' yi açın.  

    2. **Windows Update** hizmeti seçin. **Eylem** menüsüne gidin ve **Durdur**' u seçin.

2. **SoftwareDistribution** dizinini yeniden adlandırın.  

    1. Yönetici olarak bir komut istemi açın.  

    2. Aşağıdaki komutları girin:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. **Windows Update** hizmetini yeniden başlatın.

    1. **Hizmetler** penceresine geri dönün.  

    2. **Windows Update** hizmeti seçin. **Eylem** menüsüne gidin ve **Başlat**' ı seçin.

    3. Hizmetler penceresini kapatın.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>4. Adım: bilgisayarınızda Microsoft Antivirus güncelleştirme motorunu sıfırlayın  

1. Yönetici olarak bir komut istemi açın.

2. Aşağıdaki komutları girin:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Bilgisayarı yeniden başlatın.  

4. Windows Defender 'ı yeniden güncelleştirmeyi deneyin.

Sorun devam ederse, bir sonraki adımla devam edin.  

#### <a name="step-5-manually-install-the-definition-updates"></a>5. Adım: tanım güncelleştirmelerini el Ile yüklerken  

[En son güncelleştirmeleri el ile indirin](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### <a name="step-6-contact-microsoft-support"></a>6. Adım: Microsoft destek 'e başvurun  

Bu adımlar sorunu gidermezse, Microsoft destek 'e başvurun. Daha fazla bilgi için bkz. [Destek seçenekleri ve topluluk kaynakları](../../core/understand/find-help.md#BKMK_SupportOptions).  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a> Windows Defender veya Endpoint Protection hizmetini başlatma

### <a name="symptom"></a>Belirti

**Programın hizmeti durdurulduğu Için Windows Defender veya Endpoint Protection bilgisayarınızı izlememeye yönelik olduğunu bildiren bir ileti alırsınız. Şimdi yeniden başlatmanız gerekir.**

### <a name="solution"></a>Çözüm

#### <a name="step-1-restart-your-computer"></a>1. Adım: bilgisayarınızı yeniden başlatın

Tüm uygulamaları kapatın ve bilgisayarınızı yeniden başlatın.  

#### <a name="step-2-check-the-windows-service"></a>2. Adım: Windows hizmetini denetleme

1. **Başlat**' a gidin ve **Services. msc**' yi açın.  

2. **Windows Defender virüsten koruma hizmetini**seçin.  

3. **Başlangıç türünün** **Otomatik**olarak ayarlandığından emin olun.

4. **Eylem** menüsüne gidin ve **Başlat**' ı seçin.

    1. Bu eylem kullanılamıyorsa **Durdur**' u seçin. Hizmetin durdurulmasını bekleyin ve ardından hizmeti yeniden başlatmak için **başlatma** eylemini seçin.  

Bu işlem sırasında görünebilen tüm hataları unutmayın. [Microsoft desteği başvurun](../../core/understand/find-help.md#BKMK_SupportOptions) ve hata bilgilerini sağlayın.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>3. Adım: üçüncü taraf güvenlik programlarını kaldırma  

> [!NOTE]  
> Bazı güvenlik uygulamaları tümüyle kaldırılmaz. Önceki güvenlik uygulamanız için tam olarak kaldırmak üzere bir Temizleme yardımcı programı indirmeniz ve çalıştırmanız gerekebilir.  

1. **Başlat** ' a gidin ve **appwiz. cpl**' i açın.  

2. Yüklü programlar listesinde, tüm üçüncü taraf güvenlik programlarını kaldırın.

3. Bilgisayarınızı yeniden başlatın.  

> [!CAUTION]  
> Güvenlik programlarını kaldırdığınızda bilgisayarınız korumasız olabilir. Mevcut güvenlik programlarını kaldırdıktan sonra Windows Defender 'ı yüklerken sorunlarla karşılaşırsanız [Microsoft desteği](https://support.microsoft.com/supportforbusiness/productselection)başvurun. **Güvenlik** ürün ailesini ve ardından **Windows Defender** ürününü seçin.

## <a name="internet-connection-issues"></a> İnternet bağlantısı sorunları

Bilgisayarınızda Windows Update en son güncelleştirmeleri almak için internet 'e bağlanın.  

1. **Başlat** ' a gidin ve **ncpa. cpl**' i açın.  

2. Bağlantı **durumunu**görüntülemek için bağlantı adını açın.  

3. Bilgisayarınız bağlıysa, **IPv4 bağlantısı** ve/veya **IPv6 bağlantı** durumu **Internet**olur.  

4. Bilgisayarınız bağlı gözükmezse bağlantı adını seçin ve **Bu bağlantıyı Tanıla**' yı seçin.

Tüm açık programları kapatın ve bilgisayarınızı yeniden başlatın.  

## <a name="detected-threat-cant-be-remediated"></a> Algılanan tehdit düzeltilemiyor

Windows Defender veya Endpoint Protection olası bir tehdit algıladığında, tehdidi ortadan kaldırarak veya kaldırarak tehdidi azaltmaya çalışır. Bu tehditler sıkıştırılmış bir arşiv (`.zip`) içinde veya bir ağ paylaşımında gizlenebilir.

### <a name="remove-or-scan-the-file"></a>Dosyayı kaldırın veya tarayın  

- Algılanan tehdit sıkıştırılmış bir arşiv dosyasında ise, dosyaya gidin. Dosyayı silin veya el ile tarayın. Dosyaya sağ tıklayın ve **Windows Defender Ile Tara**' yı seçin. Windows Defender dosyada ek tehditler algılarsa sizi bilgilendirir. Ardından, uygun bir eylem seçebilirsiniz.  

- Algılanan tehdit bir ağ paylaşımındaysa, paylaşma 'yı açın ve el ile tarayın. Dosyaya sağ tıklayın ve **Windows Defender Ile Tara**' yı seçin. Windows Defender ağ paylaşımında ek tehditler algılarsa sizi bilgilendirir. Ardından, uygun bir eylem seçebilirsiniz.  

- Dosyanın kaynağından emin değilseniz bilgisayarınızda bir tam tarama çalıştırın. Tam taramanın tamamlanması biraz zaman alabilir.  

## <a name="see-also"></a>Ayrıca bkz.

[Endpoint Protection istemci sık sorulan sorular](endpoint-protection-client-faq.md)

[Endpoint Protection istemci yardımı](endpoint-protection-client-help.md)
