---
title: Technical Preview 1512 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1512 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3e618a8a0db81ad870c5aeedc89b01ba6089a0f8
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607921"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Configuration Manager için Technical Preview 1512 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1512 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](technical-preview.md).  

 Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a> Cihaz Durumu Kanıtlama  
 Microsoft, Technical Preview 1512 ' den itibaren, Windows 10 Cihaz Sistem Durumu Kanıtlama durumunu Configuration Manager konsolunda görüntüleyebilir.  Bu işlevsellik Microsoft Intune Configuration Manager ve Configuration Manager için kullanılabilir. Cihaz durumu kanıtlama, yöneticinin istemci bilgisayarlarda güvenilir BIOS, TPM ve önyükleme yazılımı yapılandırmaları olduğundan emin olmasına imkan tanır. Cihaz durumu kanıtlamayı desteklemek için istemci cihazların TPM 2 ' nin etkin win10 çalıştırıyor olması gerekir. Cihaz durumu kanıtlama aşağıdakilerin her biri için etkinleştirilmiş cihaz sayısını görüntüler:  

-   Erken başlatılan kötü amaçlı yazılımdan koruma  

-   BitLocker  

-   Güvenli Önyükleme  

-   Kod Bütünlüğü  

Konsol Ayrıca cihaz sayısıyla birlikte eksik olan durum kanıtlama ayarlarını görüntüler.  

Cihaz sistem durumu kanıtlama görünümünü önizlemek için, Configuration Manager konsolundaki **izleme** çalışma alanına gidin, **güvenlik** düğümü ' ne ve ardından **sistem durumu kanıtlama**' na tıklayın.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a> Hüküm ve koşullar için konsol içi izleme  
Technical Preview 1512 ' den itibaren, Configuration Manager Microsoft Intune ile tümleştirdiğinizde, hangi kullanıcıların BT departmanınız tarafından yapılandırılan hüküm ve koşulları kabul ettiğini ve hangi kullanıcıların bu koşullara sahip olduğunu görüntülemek için Configuration Manager konsolunu kullanabilirsiniz.  

**Özet bilgileri görüntülemek için:**  

-   Configuration Manager konsolunda **izlemeye**  >  **genel bakış**  >  **dağıtımlar** ' a gidin ve görüntülemek istediğiniz hüküm ve koşullar dağıtımını seçin.  

**Ayrıntılı bilgileri görüntülemek için:**  

1.  Configuration Manager konsolunda **varlıklar ve uyum**  >  **genel bakış**  >  **Uyumluluk ayarları**  >  **hüküm ve koşullar**' a gidin ve ardından görüntülemek istediğiniz hüküm ve koşulları seçin.  

2.  Konsolunun en altında **dağıtımlar** sekmesini seçin, dağıtımı seçin ve ardından **durumu görüntüle** ' ye tıklayın.  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a> Endpoint Protection ilke ayarlarındaki iyileştirmeler  
1512 Technical Preview sürümünde, Endpoint Protection kötü amaçlı yazılımdan koruma ilkesine aşağıdaki yeni ayarları ekledik:  

-   Gerçek zamanlı koruma: istenmeyebilecek **uygulamaları indirme sırasında ve yüklemeden önce engelle**  

    -   İstenmeyebilecek Uygulamalar (PUA) itibara ve araştırma tabanlı tanımlamaya dayalı bir tehdit sınıflandırmasıdır. En yaygın olarak, bunlar istenmeyen uygulama paketleyicileri veya onların paketlenmiş uygulamalarıdır.  

    -   Koruma ilkesi ayarı varsayılan olarak etkindir ("Yes" olarak ayarlanır). Etkinleştirildiğinde, bu ayar indirme ve yükleme sırasında PUA’yı engeller. Ancak, ortamınızın belirli ihtiyaçlarını karşılamak için belirli dosya veya klasörleri dışarıda bırakabilirsiniz.  

-   Tarama ayarları: **tam tarama çalıştırılırken eşlenen ağ sürücülerine tarama** yapın  

    -   Bu ayar, zamanlanmış bir tam tarama sırasında eşlenmiş ağ sürücülerinin her zaman taranması riski olmadan, yöneticinin ağ dosyalarının isteğe bağlı taranmasını sağlamak için daha fazla ayrıntı düzeyi sağlar.  

    -   Bu ayarın yapılandırılması için kullanılabilir olması için **ağ dosyalarını Tara** ayarının önce etkinleştirilmesi gerekir ("Evet").  

    -   Varsayılan olarak, bu ayar "Hayır" anlamına gelir ve tam bir tarama eşlenmiş ağ sürücülerine erişmez.  

-   Otomatik örnek dosya gönderimi ayarları:  

     Kötü amaçlı yazılımdan koruma altyapısı, daha fazla analiz için Microsoft 'a gönderilecek dosya örnekleri isteyebilir. Varsayılan olarak, bu tür örnekleri göndermeden önce her zaman sorar. Yöneticiler artık bu davranışı yapılandırmak için aşağıdaki ayarları yönetebilir:  

    -   Gelişmiş: **Microsoft 'un algılanan belirli öğelerin kötü amaçlı olup olmadığını belirlemesine yardımcı olmak için otomatik örnek dosya gönderimini etkinleştirin**: Otomatik örnek dosya gönderimini etkinleştirmek için bu ayarı "Evet" olarak değiştirin. Varsayılan olarak, bu ayar, otomatik örnek dosya gönderimi devre dışı bırakıldığı ve örnekleri göndermeden önce kullanıcılara sorulacak anlamına gelen "Hayır" dır.   (Bu ayar ilk olarak System Center 2012 R2 Configuration Manager SP1 'de tanıtılmıştır)  

    -   Gelişmiş: **kullanıcıların otomatik örnek dosya gönderimi ayarlarını değiştirmesine Izin ver**: Bu ayar, bir cihazda yerel yönetici haklarına sahip bir kullanıcının istemci arabirimindeki otomatik örnek dosya gönderimi ayarını değiştirip değiştiremeyeceğini belirler. Varsayılan olarak, bu ayar, ayarların yalnızca Configuration Manager konsolundan değiştirilebileceği ve bir cihazdaki yerel yöneticilerin bu yapılandırmayı değiştiremeyeceği anlamına gelen "Hayır" dır.  

         Örneğin, aşağıdaki, yönetici tarafından etkin olarak ayarlanan Windows 10 ' da Windows Defender ayarını gösterir ve kullanıcının bunu değiştirmesine izin verilmez:  

         ![Windows Defender-otomatik örnek gönderimi](../../core/get-started/media/TechRef_WinDefender.png)  

    Ayrıca, Endpoint Protection kötü amaçlı yazılımdan koruma ilkesinin "dışlama ayarları" bölümünde bulunan **dosyaları ve klasörleri dışarıda bırak** ayarı, cihaz dışlamalarına izin verecek şekilde geliştirilmiştir. Örneğin, bundan böyle şunları bir dışlama olarak belirtebilirsiniz: **\device\mvfs** (Çok Sürümlü Dosya Sistemi için). İlke, cihaz yolunu doğrulamaz; Endpoint Protection ilkesi, istemci üzerinde cihaz dizesini yorumlayabilmesi gereken kötü amaçlı yazılımdan koruma altyapısına sağlanır.  

**Endpoint Protection ilkeleri kullanma önkoşulları:**  

Endpoint Protection ilkeleri kullanabilmeniz için Endpoint Protection istemci ayarlarını kullanarak Endpoint Protection istemcisini yüklemeli ve yönetmeniz gerekir. Bu işlem, Windows 7, Windows 8, Windows 8.1 veya Windows 10 için yönetilen Windows Defender için System Center Endpoint Protection istemcisi kullanılarak yapılır. Bkz. [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  
