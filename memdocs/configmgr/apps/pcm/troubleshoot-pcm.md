---
title: Paket Dönüştürme Yöneticisi sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager 'de Paket Dönüştürme Yöneticisi ile ilgili sorunları nasıl giderebileceğinizi öğrenin.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877631"
---
# <a name="troubleshoot-package-conversion-manager"></a>Paket Dönüştürme Yöneticisi sorunlarını giderme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1357861-->

Paket Dönüştürme Yöneticisi 'Ni kullanırken sorunları gidermenize yardımcı olması için bu makaledeki bilgileri kullanın.



## <a name="sms-provider"></a>site veritabanı

Paket Dönüştürme Yöneticisi SMS sağlayıcısını kullanır. Daha fazla bilgi için bkz. [plan for SMS Provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).

SMS sağlayıcısı düzgün çalışmıyorsa, Paket Dönüştürme Yöneticisi de dahil Configuration Manager konsolu çalışmaz.



## <a name="package-readiness"></a>Paket hazırlığı

Bir paketi uygulamaya dönüştürmeden önce Paket Dönüştürme Yöneticisi **Çözümle** işlevini kullanarak paketi çözümleyin. Analizden sonra, Configuration Manager konsolunun **paketler** düğümüne **hazırlık** sütununu ekleyin. Paket listesi, çözümlenmiş paketin aşağıdaki hazırlık durumlarından birini görüntüler:

- **Otomatik**: paket, **Convert** işlevi kullanılarak doğrudan dönüştürülebilir.      

  > [!NOTE]  
  > Otomatik dönüştürme, WQL sorgularını uygulama gereksinimlerine dönüştürmez. Bu sorguları dönüştürmek için **onarma ve dönüştürme** işlemini kullanın.  

- **El ile**: Package, **düzeltmesini ve Convert** işlevini kullanarak dönüştürebilmeniz için bazı eklemelere veya değişikliklere ihtiyaç duyuyor.  

- **Uygulanamaz**: paket dönüştürme için uygun değil. Paketle ilgili sorunları giderin veya paketi bir paket olarak dağıtmaya devam edin.  

- **Hata**: pakette hata var. Bu hataları analiz etmeden ve dönüştürebilmeniz için el ile düzeltin.  

Configuration Manager konsolundaki **paketler** düğümünün Ayrıntılar bölmesi tüm hazırlık sorunlarını gösterir. Bir paket seçin ve ardından Ayrıntılar bölmesinde **Özet** sekmesini seçin.



## <a name="log-files"></a>Günlük dosyaları

### <a name="enable-logging"></a>Günlü kaydını etkinleştir

Paket Dönüştürme Yöneticisi için günlük kaydını etkinleştirdiğinizde, tüm eylemlerini, özel durumlarını ve hatalarını günlüğe kaydeder.

Configuration Manager Bu bileşen için günlüğe kaydetmeyi etkinleştirmek üzere **Microsoft. ConfigurationManagement. exe. config dosyasını**değiştirin. Varsayılan olarak, bu yapılandırma dosyası şu yolda bulunur:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> Sürüm 1910 ' den başlayarak, bu yol klasörü kullanacak şekilde değiştirilmiştir `Microsoft Endpoint Manager` . Dosyanın başka bir klasörde mevcut olabilecek eski bir sürümünü kullandığınızdan emin olun.

Aşağıdaki **anahtarları** ve **Trace** XML öğelerini, son **kaynaklar** öğesinden sonra **System. Diagnostics** öğesine ekleyin:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Bu örnek **PCMtrace. log**dosyasını kullanır. Bu günlük Configuration Manager konsolunu çalıştıran bilgisayarda aşağıdaki yolda bulunur:  
`%UserProfile%\AppData\Local\Temp`

Ayrıntı düzeyini yapılandırmak için **PcmLogging** izleme anahtarı ayarını değiştirin. Bu değeri, en az Detailed ( `1` ) ile en ayrıntılı () arasında dört ayrıntı düzeyine ayarlayın `4` .


### <a name="smsprovlog"></a>SMSProv.log

Bazı durumlarda, paket dönüştürme işleminin giderilmesi ile ilgili bilgiler **Smsprov. log** dosyasında bulunur. Bu dosya Configuration Manager SMS sağlayıcısından bilgi yakalar.

Varsayılan olarak, bu günlük dosyası Configuration Manager site sunucusunda aşağıdaki yolda bulunur:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Aşağıdaki hata iletilerinden birini görürseniz, **Smsprov. log** dosyasında ilgili sorun giderme bilgileri bulunabilir:

- `The SMS Provider reported an error`

- `Generic Failure`

Bu hata iletileri genellikle site sunucusunda bir hata oluştuğunu ve hata bilgilerinin Configuration Manager konsoluna gönderilmediğini gösterir.

Daha fazla bilgi için bkz. [Paket Dönüştürme Yöneticisi hata iletileri Için teknik başvuru](error-messages.md).



## <a name="changing-package-attributes-after-analysis"></a>Analiz sonrasında paket özniteliklerini değiştirme

Bir paketi çözümledikten ve **Otomatik** veya **el ile**hazırlık durumuna sahip olduktan sonra, ilgili özniteliklerden herhangi birini değiştirirseniz dönüştürme işlemi başarısız olabilir.

Örneğin, bir paketi analiz edersiniz ve hazırlık durumu **otomatiktir**. Daha sonra pakete başka bir program eklersiniz. Paket dönüştürme başarısız olabilir.

Analiz sonrasında bir pakette değişiklik yapmanız gerekiyorsa, dönüştürmeden önce çözümlemeyi yeniden çalıştırın. 



## <a name="see-also"></a>Ayrıca bkz.

[Paket Dönüştürme Yöneticisi hata iletileri için teknik başvuru](error-messages.md)
