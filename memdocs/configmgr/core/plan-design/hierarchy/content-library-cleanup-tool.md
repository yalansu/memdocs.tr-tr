---
title: İçerik kitaplığı temizleme aracı
titleSuffix: Configuration Manager
description: Artık Configuration Manager dağıtımıyla ilişkili olmayan yalnız bırakılmış içeriği kaldırmak için içerik kitaplığı Temizleme aracını kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720222"
---
# <a name="content-library-cleanup-tool"></a>İçerik kitaplığı temizleme aracı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Artık bir dağıtım noktasındaki herhangi bir paket veya uygulamayla ilişkili olmayan içeriği kaldırmak için içerik kitaplığı temizleme komut satırı aracını kullanın. Bu içerik türü *yalnız bırakılmış içerik*olarak adlandırılır. Bu araç, geçmiş Configuration Manager ürünleri için yayınlanan benzer araçların eski sürümlerini değiştirir.  

Araç yalnızca aracı çalıştırdığınızda belirttiğiniz dağıtım noktasındaki içeriği etkiler. Araç, site sunucusundaki içerik kitaplığından içerik kaldıramıyor.

Site sunucusunda ' de **Contentlibrarycleanup. exe** ' `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` yi bulun.



## <a name="requirements"></a>Gereksinimler  

- Aracı tek seferde yalnızca tek bir dağıtım noktasına karşı çalıştırın.  

- Bunu doğrudan veya başka bir bilgisayardan uzaktan çalıştırmak için dağıtım noktasını barındıran bilgisayarda çalıştırın.  

- Aracı çalıştıran kullanıcı hesabının, Configuration Manager ' deki **tam yönetici** güvenlik rolüyle aynı izinlere sahip olması gerekir.  



## <a name="modes-of-operation"></a>İşlem modları

Aracı şu iki modda çalıştırın: [What-if](#what-if-mode) ve [Delete](#delete-mode).

> [!Tip]  
> *Durum* modunu başlatın. Sonuçlardan memnun kaldığınızda, aracı *silme* modunda çalıştırın.  


### <a name="what-if-mode"></a>Durum modu   

`/delete` Parametresini belirtmezseniz, araç, bir durum modunda çalışır. Bu mod, dağıtım noktasından silinecek içeriği tanımlar.

- Bu modda çalıştırıldığında, araç hiçbir veri silmez.  

- Araç, silinecek içerikle ilgili günlük dosyası bilgilerine yazar. Olası her silme işlemini onaylamanız istenmez.  


### <a name="delete-mode"></a>Silme modu   

Aracı `/delete` parametresiyle çalıştırdığınızda, araç silme modunda çalışır.

- Bu modda çalıştırıldığında, belirtilen dağıtım noktasında bulduğu yalnız bırakılmış içerikler dağıtım noktasının içerik kitaplığından silinebilir.  

- Her bir dosyayı silmeden önce aracın onu silmesi gerektiğini doğrulayın. Daha fazla komut istemini atlamak ve yalnız bırakılmış tüm içeriği silmek için **Evet, hayır** için **Y** , **Tümüne Evet** ' i seçin.  


### <a name="log-file"></a>Günlük dosyası

Araç her iki modda da çalıştığında, otomatik olarak bir günlük oluşturur. Günlük dosyasını aşağıdaki bilgilerle adlandırır: 
- Aracının çalıştığı mod  
- Dağıtım noktasının adı  
- İşlemin tarih ve saati  

Araç tamamlandığında, otomatik olarak Windows 'ta günlük dosyasını açar. 

Araç, varsayılan olarak günlük dosyasını, aracı çalıştıran kullanıcı hesabının geçici klasörüne yazar. Bu konum, aracı çalıştırdığınız ve her zaman aracın hedefi olmayan bir bilgisayardır. Günlük dosyasını `/log` bir ağ paylaşma da dahil olmak üzere başka bir konuma yönlendirmek için parametresini kullanın.



## <a name="run-the-tool"></a>Aracı çalıştırma

Aracı çalıştırmak için: 

1. Yönetici olarak bir komut istemi açın. Dizini, **Contentlibrarycleanup. exe**dosyasını içeren klasöre değiştirin.  

2. Gerekli [komut satırı parametrelerini](#bkmk_params)ve kullanmak istediğiniz tüm isteğe bağlı parametreleri içeren bir komut satırı girin.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a>Komut satırı parametreleri  

Bu komut satırı parametrelerini istediğiniz sırada kullanın.   

### <a name="required-parameters"></a>Gerekli parametreler

|Parametre|Ayrıntılar|
|---------|-------|
| `/dp <distribution point FQDN>`  | Temizleyen dağıtım noktasının tam etki alanı adını (FQDN) belirtin. |
| `/ps <primary site FQDN>` | Yalnızca İkincil sitedeki bir dağıtım noktasından içerik temizlenirken *gereklidir* . Araç, SMS sağlayıcısına yönelik sorguları çalıştırmak için üst birincil siteye bağlanır. Bu sorgular, aracının dağıtım noktasında hangi içeriğin olması gerektiğini belirlemesine izin verir. Ardından, kaldırılacak yalnız bırakılmış içeriği tanımlayabilir. Gerekli ayrıntılar doğrudan ikincil siteden kullanılamadığından, bu üst birincil siteye yönelik bu bağlantı ikincil bir sitede dağıtım noktaları için yapılmalıdır.|
| `/sc <primary site code>`  | Yalnızca İkincil sitedeki bir dağıtım noktasından içerik temizlenirken *gereklidir* . Üst birincil sitenin site kodunu belirtin. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Örnek: hangi içeriğin silineceğini Tara ve günlüğe kaydet (ne olur)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Örnek: ikincil sitede bir DP için içerik tarama ve günlüğe kaydetme
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>İsteğe bağlı parametreler

|Parametre|Ayrıntılar|
|---------|-------|
|`/delete`| Dağıtım noktasındaki içeriği silmeye hazırsanız bu parametreyi kullanın. İçerik silinmeden önce sizi uyarır. </br></br> Bu parametreyi kullanmazsanız araç, silinecek içerik hakkındaki sonuçları günlüğe kaydeder. Bu parametre olmadan, aslında dağıtım noktasındaki içeriği silmez. |
| `/q` | Bu parametre, aracı tüm istemleri belirten sessiz modda çalıştırır. Bu istemler içerikleri ne zaman sildiğini içerir. Günlük dosyasını da otomatik olarak açmaz. |
| `/ps <primary site FQDN>` | Yalnızca birincil sitedeki bir dağıtım noktasından içerik temizlenirken isteğe bağlıdır. Dağıtım noktasının ait olduğu birincil sitenin FQDN 'sini belirtin. |
| `/sc <primary site code>` | Yalnızca birincil sitedeki bir dağıtım noktasından içerik temizlenirken isteğe bağlıdır. Dağıtım noktasının ait olduğu birincil sitenin site kodunu belirtin. |
| `/log <log file directory>` | Aracın günlük dosyasını yazdığı konumu belirtin. Bu konum bir yerel sürücü veya bir ağ paylaşımından olabilir.</br></br> Bu parametreyi kullanmazsanız araç, günlük dosyasını aracın çalıştığı bilgisayarda kullanıcının geçici dizinine koyar.|

#### <a name="example-delete-content"></a>Örnek: içeriği sil 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Örnek: istemsiz içerik silme
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Örnek: yerel sürücüde günlüğe kaydet
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Örnek: ağ paylaşımında günlüğe kaydet
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Bilinen sorun

Herhangi bir paket veya dağıtım başarısız olduğunda veya devam ederken, araç aşağıdaki hatayı döndürebilir:`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Bu sorun için geçici çözüm yoktur. İçerik devam ederken veya dağıtımı başarısız olduğunda, araç yalnız bırakılmış dosyaları güvenilir bir şekilde tanımlayamıyor. Araç, bu sorunu çözene kadar içeriği temizleyemeyecek.
