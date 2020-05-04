---
title: 'Yapılandırma temelleri için ortak görevler '
titleSuffix: Configuration Manager
description: Configuration Manager yapılandırma temellerini oluşturma ve dağıtma hakkında bilgi edinin.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52e83639029db9eeb4ef64657e70e3dc11aab8f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712207"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>Configuration Manager ile yapılandırma temellerini oluşturmak ve dağıtmak için ortak görevler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager yapılandırma temellerini oluşturma ve dağıtma konusunda bilgi edinmenize yardımcı olacak yaygın senaryolar içerir.  

 Uyumluluk ayarlarını zaten biliyorsanız, [yapılandırma temelleri oluşturma](../../compliance/deploy-use/create-configuration-baselines.md) ve [yapılandırma temellerini dağıtma](../../compliance/deploy-use/deploy-configuration-baselines.md) konularında kullandığınız tüm özelliklerle ilgili ayrıntılı belgeler bulabilirsiniz.  

 Başlamadan önce uyumluluk ayarları hakkında bazı temel bilgileri öğrenmek için uyumluluk ayarlarını [kullanmaya](../../compliance/get-started/get-started-with-compliance-settings.md) başlayın ' ı okuyun ve ayrıca gerekli önkoşulları uygulamak üzere [Uyumluluk ayarları için planı okuyun ve yapılandırın](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) .  

## <a name="create-a-configuration-baseline"></a>Yapılandırma temeli oluşturma  
 Bu örnekte, yalnızca Configuration Manager istemcisini çalıştıran Windows 10 bilgisayarları için bir yapılandırma öğesi oluşturdunuz.  

 Bu yapılandırma öğesi, Windows 10 bilgisayarlarında en az 6 karakterden oluşan bir parolayı zorunlu kılar. Yapılandırma öğesi **Windows 10 Parola Zorlama**olarak adlandırılır.  

Bu yapılandırma öğesini dağıtıma hazırlamak için bir yapılandırma temeline nasıl ekleneceğini öğrenmek için aşağıdaki yordamı kullanın.  

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Uyumluluk ayarları** > **yapılandırma temelleri**' ne tıklayın.  

2. **Giriş** sekmesindeki **Oluştur** grubunda, **Yapılandırma Temeli Oluştur**'a tıklayın.  

3. **Yapılandırma temeli oluştur** iletişim kutusunda aşağıdaki ayarları yapılandırın:  

   -   **Ad** - **Windows 10 Parolaları** (veya tercih ettiğiniz başka bir ad) yazın  

4. **Yapılandırma öğeleri** **Ekle** > ' ye tıklayın.  

5. **Yapılandırma Öğesi Ekle** iletişim kutusunda, oluşturduğunuz **Windows 10 Parola Zorlama** yapılandırma öğesini seçin ve **Ekle**’ye tıklayın.  

6. **Yapılandırma öğeleri ekle** iletişim kutusunu kapatmak ve **yapılandırma temeli oluştur** iletişim kutusuna dönmek için Tamam ' ı tıklatın.

7. **Yapılandırma Temeli Oluştur** iletişim kutusunu kapatmak için **Tamam** ’a tıklayın.  

   Artık Yapılandırma temelini Configuration Manager konsolunun **yapılandırma temelleri** düğümünde görebilirsiniz.  

## <a name="deploy-the-configuration-baseline"></a>Yapılandırma temelini dağıt  
 Bu örnekte, önceki yordamda oluşturduğunuz yapılandırma temelini bir bilgisayar koleksiyonuna dağıtırsınız.  

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Uyumluluk ayarları** > **yapılandırma temelleri**' ne tıklayın.  

2. Yapılandırma temelleri listesinden **Windows 10 Parolaları**’nı seçin.  

3. **Giriş** sekmesinde, **Dağıtım** grubunda, **Dağıt**'a tıklayın.  

4. **Yapılandırma temellerini dağıt** iletişim kutusunda, aşağıdaki ayarları yapılandırın:  

   -   **Seçili yapılandırma temelleri** - **Windows 10 Parolaları** yapılandırma temelinin bu listeye otomatik olarak eklendiğinden emin olun.  

   -   **Desteklendiğinde uyumsuz kuralları düzelt** -hedeflenen cihazlarda doğru ayarların mevcut olmadığından emin olmak için bu kutuyu işaretleyin, ardından Configuration Manager tarafından düzeltilirler.  

   -   **Koleksiyon** -yapılandırma temelinin değerlendirildiği ve uyumluluk için düzeltileceği bilgisayar koleksiyonunu seçmek için **Araştır** ' a tıklayın. Bu örnekte yapılandırma temeli, yerleşik olarak bulunan **Tüm Masaüstü ve Sunucu İstemcileri** koleksiyonuna dağıtılmıştır.  

       > [!TIP]  
       >  Seçtiğiniz koleksiyon Windows 10 çalıştırmayan bilgisayar veya cihazlar içeriyorsa endişelenmeyin. Oluşturduğunuz yapılandırma öğesinde desteklenen platformları yapılandırdığınız sürece yalnızca Windows 10 bilgisayarları uyumluluk için değerlendirilir.  

   -   Gerekirse, yapılandırma temelinin değerlendirilme zamanlamasını yapılandırın. Aksi takdirde, varsayılan **7 Gün**ayarını değiştirmeyin.  

5. **Yapılandırma Temellerini Dağıt** iletişim kutusunu kapatmak ve dağıtım oluşturmak için **Tamam** ’a tıklayın.  

   Bu dağıtım için uyumluluk istatistiklerine hızlı bir şekilde göz atmak istiyorsanız **İzleme** çalışma alanında **Dağıtımlar**’a tıklayın. Ekranın alt kısmında bir **Uyumluluk istatistikleri** grafiği görürsünüz.  

## <a name="next-steps"></a>Sonraki adımlar 

Yapılandırma temellerini izleme hakkında daha ayrıntılı bilgi için bkz. [izleyici uyumluluk ayarları](../../compliance/deploy-use/monitor-compliance-settings.md).  
