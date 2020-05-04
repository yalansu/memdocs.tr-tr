---
title: Dönüştürme eklentisini kullanma
titleSuffix: Configuration Manager
description: Çözümleme ve dönüştürme süreçlerini özelleştirmek için Paket Dönüştürme Yöneticisi eklentisini kullanın.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709883"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Paket Dönüştürme Yöneticisi eklentisini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1357861-->

Paket Dönüştürme Yöneticisi eklentisi, çözümleme ve dönüştürme süreçlerini özelleştirmenize yardımcı olur. Paket Dönüştürme Yöneticisi eklentisini kullanmak için özel işlemler gerçekleştiren bir yürütülebilir dosya veya betik dosyası yazın. Sonra yürütülebilir veya betiği çağırmak için Microsoft. ConfigurationManagement. exe. config yapılandırma dosyasını düzenleyin. Betiği yazmak için kullanılan en yaygın diller VBScript veya PowerShell 'tir.

Paket Dönüştürme Yöneticisi eklentisi her paket için bir kez çalışır. Aynı anda birden çok paketi çözümleyip dönüştürürseniz, Paket Dönüştürme Yöneticisi eklentisi her seferinde çalışır.

> [!NOTE]  
> Configuration Manager yapılandırma dosyasındaki Paket Dönüştürme Yöneticisi öğeleri hakkında daha fazla bilgi için bkz. [Paket Dönüştürme Yöneticisi eklenti YAPıLANDıRMASı XML Için teknik başvuru](plugin-config-xml.md).



## <a name="default-process"></a>Varsayılan işlem

Varsayılan olarak, Paket Dönüştürme Yöneticisi aşağıdaki eylemleri yapar:

1.  Bir Configuration Manager paketini okuyun.  

2.  Paketten bir uygulama oluşturun ve varsayılan öznitelikleri ekleyin.  

3.  Uygulamayı çözümleyin ve bir paket hazırlık durumu belirlenir.  

4.  Paket Dönüştürme Yöneticisi işlemine bağlı olarak aşağıdaki eylemlerden birini yapın:  

    - **Çözümle**: Configuration Manager konsolunda paket hazırlığı durumunu görüntüleyin.  

    - **Dönüştür**: uygulamayı Configuration Manager veritabanına yazın.  


## <a name="plug-in-based-process"></a>Eklenti tabanlı işlem 

Eklentiyi kullandığınızda, Paket Dönüştürme Yöneticisi aşağıdaki eylemleri yapar:

1.  Bir Configuration Manager paketini okuyun.  

2.  Paketten bir uygulama oluşturun ve varsayılan öznitelikleri ekleyin.  

3.  Uygulamayı XML 'e dönüştürün. Sonra dosyayı diske kaydedin.  

4.  Uygulama XML 'sini değiştirmek için eklenti betiğini çalıştırın. Daha fazla bilgi için bkz. [Paket Dönüştürme Yöneticisi eklenti YAPıLANDıRMASı XML Için teknik başvuru](plugin-config-xml.md).  

5.  Uygulama XML 'sini bir Configuration Manager uygulamasına dönüştürün.  

6.  Uygulamayı çözümleyin ve bir paket hazırlık durumu saptayın.  

7.  Paket Dönüştürme Yöneticisi işlemine bağlı olarak aşağıdaki eylemlerden birini yapın:  

    - **Çözümle**: Configuration Manager konsolunda paket hazırlığı durumunu görüntüleyin.  

    - **Dönüştür**: uygulamayı Configuration Manager veritabanına yazın.  



## <a name="see-also"></a>Ayrıca bkz.

[Paket Dönüştürme Yöneticisi eklenti yapılandırması XML 'SI için teknik başvuru](plugin-config-xml.md)
