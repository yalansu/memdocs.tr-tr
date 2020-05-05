---
title: Şirket içi MDM için sertifikalar
titleSuffix: Configuration Manager
description: Configuration Manager ' de şirket içi mobil cihaz yönetimi (MDM) ile güvenilir iletişimler için sertifikaları ayarlayın.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc63a21970bb522407c86d027690b83894b3cb99
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721832"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Şirket içi MDM ile güvenilen iletişimler için sertifikaları ayarlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Şirket içi mobil cihaz yönetimi (MDM) Configuration Manager, site sistem rollerini yönetilen cihazlarla güvenilir iletişimler için yapılandırmanızı gerektirir. İki tür sertifika gerekir:

- Gerekli site sistem rollerini barındıran sunucularda IIS 'de bir **Web sunucusu sertifikası** . Bir sunucu birden çok site sistem rolü barındırıyorsa, bu sunucu için yalnızca bir sertifika gerekir. Her rol ayrı bir sunucu üzerinde ise, her sunucunun ayrı bir sertifikası olması gerekir.

- Web sunucusu sertifikalarını veren sertifika yetkilisinin (CA) **Güvenilen kök sertifikası** . Bu kök sertifikayı, site sistem rollerine bağlanması gereken tüm cihazlara yükler.

Etki alanına katılmış cihazlarda, Active Directory Sertifika Hizmetleri kullanıyorsanız, bu sertifikaları tüm cihazlara otomatik olarak yükleyebilir. Etki alanına katılmış olmayan cihazlarda, güvenilen kök sertifikayı başka yollarla de yüklersiniz.

Toplu kayıtlı cihazlarda, sertifikayı kayıt paketine dahil edebilirsiniz. Kullanıcının kaydettirdiği cihazlarda, sertifikayı e-posta, Web’den indirme veya başka bir yöntemle eklemeniz gerekir.

Sunucu sertifikaları vermek için Verisign veya GoDaddy gibi tanınmış bir ortak CA kullanırsanız, güvenilen kök sertifikayı her bir cihaza el ile yüklemek zorunda kalmaktan kaçınabilirsiniz. Çoğu cihaz bu genel yetkililere yerel olarak güvenir. Bu yöntem, sertifikayı başka yollarla yüklemek yerine, Kullanıcı tarafından kaydedilen cihazlar için kullanışlı bir alternatiftir.

> [!IMPORTANT]  
> Şirket içi MDM için cihazlar ve site sistem sunucuları arasındaki güvenilir iletişimler için sertifikaları kurmanın birçok yolu vardır. Bu makaledeki bilgiler, bunu yapmanın bir yolu örneğidir. Bu yöntem, sertifika yetkilisi ve sertifika yetkilisi Web kaydı rolüyle Active Directory Sertifika Hizmetleri gerektirir. Daha fazla bilgi için bkz. [Active Directory Sertifika Hizmetleri](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a>CRL yayımlama

Active Directory Sertifika yetkilisi (CA), varsayılan olarak LDAP tabanlı sertifika iptal listeleri (CRL 'Ler) kullanır. Etki alanına katılmış cihazlar için CRL 'ye bağlantılara izin verir. Etki alanına katılmış olmayan cihazların CA 'dan verilen sertifikalara güvenmesine izin vermek için, HTTP tabanlı bir CRL ekleyin.

1. Siteniz için sertifika yetkilisini çalıştıran sunucuda, **Başlat** menüsüne gidin, **Yönetim Araçları**' nı seçin ve **sertifika yetkilisi**' ni seçin.

1. Sertifika Yetkilisi konsolunda, **CertificateAuthority**' ye sağ tıklayın ve ardından **Özellikler**' i seçin.

1. CertificateAuthority özellikleri ' nde, **Uzantılar** sekmesine geçin. **uzantı Seç** ' in **CRL dağıtım noktası (CDP)** olarak ayarlandığından emin olun.

1. `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl` öğesini seçin. Ardından aşağıdaki seçenekleri belirleyin:

    - **CRL 'Lere dahil et. Istemciler Delta CRL konumlarını bulmak için bunu kullanır.**

    - **Verilen sertifikaların CDP uzantısına dahil et.**

    - **Verilen CRL’lerin IDP uzantısına dahil et**

1. **Çıkış modülü** sekmesine geçin. **Özellikler**' i seçin, sonra **sertifikaların dosya sistemine yayımlanmasına izin ver**' i seçin. Active Directory Sertifika Hizmetleri 'ni yeniden başlatma hakkında bir bildirim görürsünüz.

1. **Iptal edilen sertifikalar**' a sağ tıklayın, **Tüm görevler**' i ve ardından **Yayımla**' yı seçin.

1. CRL Yayımla penceresinde **yalnızca Delta CRL**' yi seçin ve ardından pencereyi kapatmak için **Tamam** ' ı seçin.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a>Sertifika şablonu oluşturma

CA, site sistem rollerini barındıran sunucular için sertifikalar vermek üzere Web sunucusu sertifika şablonunu kullanır. Bu sunucular, site sistem rolleri ve kayıtlı cihazlar arasındaki güvenilen iletişimler için SSL uç noktaları olacaktır.

1. **CONFIGMGR MDM sunucuları**adlı bir etki alanı güvenlik grubu oluşturun. Site sistem sunucularının bilgisayar hesaplarını gruba ekleyin.

1. Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın ve **Yönet**' i seçin. Bu eylem, Sertifika Şablonları konsolunu yükler.

1. Sonuçlar bölmesinde, **şablon görünen adı** sütununda **Web sunucusu** ' nu görüntüleyen girişe sağ tıklayın ve **Yinelenen şablon**' u seçin.

1. **Yinelenen şablon** penceresinde **Windows 2003 Server, Enterprise edition** veya **Windows 2008 Server, Enterprise Edition**' ı seçin ve ardından **Tamam**' ı seçin.

    > [!TIP]
    > Configuration Manager, v3 veya şifreleme: yeni nesil (CNG) sertifikaları olarak da bilinen Windows 2008 Server sertifika şablonlarını destekler. Daha fazla bilgi için bkz. [CNG sertifikalarına genel bakış](../../core/plan-design/network/cng-certificates-overview.md).

    CA 'nız Windows Server 2012 veya üzeri sürümlerde çalışıyorsa, bu pencere sertifika şablonu sürümü seçeneğini göstermez. Şablonu çoğaltdıktan sonra şablon özelliklerinin **Uyumluluk** sekmesinde sürümü seçin.

1. **Yeni Şablon Özellikleri** penceresinde, **genel** sekmesinde, bir şablon adı girin. CA, Configuration Manager site sistemlerinde kullanılacak web sertifikalarını oluşturmak için bu adı kullanır. Örneğin **CONFIGMGR MDM Web sunucusu**yazın.

1. **Konu adı** sekmesine geçin ve **Active Directory bilgilerden oluştur**' u seçin. Konu adı biçimi için **DNS adını**belirtin. **Kullanıcı asıl adı (UPN)** seçiliyse, alternatif konu adı seçeneğini devre dışı bırakın.

1. **Güvenlik** sekmesine geçin.

    1. **Etki alanı yöneticileri** ve **Enterprise Admins** güvenlik gruplarından **kaydetme** iznini kaldırın.

    1. **Ekle**' yi seçin ve güvenlik grubunuzun adını girin. Örneğin, **CONFIGMGR MDM sunucuları**. Pencereyi kapatmak için **Tamam ' ı** seçin.

    1. Bu grup için **kaydetme** iznini seçin. **Oku** iznini kaldırmayın.

1. Değişikliklerinizi kaydetmek için **Tamam** ' ı seçin ve Sertifika Şablonları konsolunu kapatın.

1. Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın, **Yeni**' yi seçin ve ardından **verilecek sertifika şablonu**' nu seçin.

1. **Sertifika şablonlarını etkinleştir** penceresinde, yeni şablonu seçin. Örneğin **CONFIGMGR MDM Web sunucusu**. Ardından **Tamam** ' ı seçerek pencereyi kaydedin ve kapatın.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a>Sertifikayı iste

Bu işlem, IIS için Web sunucusu sertifikasının nasıl isteneceğini açıklar. Şirket içi MDM için rollerden birini barındıran her site sistem sunucusu için bu işlemi yapın.

1. Rollerden birini barındıran site sistemi sunucusunda, yönetici olarak bir komut istemi açın. Boş `mmc` bir Microsoft Yönetim Konsolu açmak için girin.

1. Konsol penceresinde, **Dosya** menüsüne gidin ve **ek bileşen Ekle/Kaldır**' ı seçin.

    1. Kullanılabilir ek bileşenler listesinden **Sertifikalar** ' ı seçin ve **Ekle**' yi seçin.

    1. Sertifikalar ek bileşeni penceresinde **bilgisayar hesabı**' nı seçin. **İleri**' yi seçin ve ardından yerel bilgisayarı yönetmek için **son** ' u seçin.

    1. Ek bileşen Ekle veya Kaldır penceresinden çıkmak için **Tamam ' ı** seçin.

1. **Sertifikalar (yerel bilgisayar)**' ı genişletin ve **Kişisel** Mağaza ' yı seçin. **Eylem** menüsüne gidin, **Tüm görevler**' i seçin ve **Yeni sertifika iste**' yi seçin. Bu eylem, daha önce oluşturduğunuz şablonu kullanarak yeni bir sertifika oluşturmak için Active Directory Sertifika hizmetleriyle iletişim kurar.

    1. Sertifika kayıt sihirbazında, başlamadan önce sayfasında, **İleri**' yi seçin.

    1. Sertifika kayıt Ilkesi Seç sayfasında, **Active Directory kayıt ilkesi**' ni seçin ve ardından **İleri**' yi seçin.

    1. Web sunucusu sertifika şablonunuzu (**CONFIGMGR MDM Web sunucusu**) seçin ve ardından **Kaydet**' i seçin.

    1. Sertifikayı istediğinde, **son**' u seçin.

Her sunucu için benzersiz bir Web sunucusu sertifikası gerekir. Gerekli site sistemi rollerinden birini barındıran her sunucu için bu işlemi tekrarlayın. Sunucu tüm site sistem rollerini barındırıyorsa, yalnızca bir Web sunucusu sertifikası istemeniz yeterlidir.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a>Sertifikayı bağlama

Sonraki adım, yeni sertifikayı Web sunucusuna bağlayamıyor. *Kayıt noktası* ve *kayıt proxy noktası* site sistem rollerini barındıran her sunucu için bu işlemi izleyin. Bir sunucu tüm site sistem rollerini barındırıyorsa, bu işlemi yalnızca bir kez yapmanız gerekir.

> [!NOTE]
> Dağıtım noktası ve cihaz yönetim noktası site sistemi rolleri için bu işlemi yapmanız gerekmez. Kayıt sırasında gerekli sertifikayı otomatik olarak alır.

1. Kayıt noktasını veya kaydolma proxy noktasını barındıran sunucuda **Başlat** menüsüne gidin, **Yönetim Araçları**' nı seçin ve **IIS Yöneticisi**' ni seçin.

1. Bağlantı listesinde, **varsayılan Web sitesi**' ni seçin ve ardından **bağlamaları Düzenle**' yi seçin.

    1. Site bağlamaları penceresinde **https**' yi seçin ve ardından **Düzenle**' yi seçin.

    1. Site bağlamayı Düzenle penceresinde, **SSL sertifikası**için yeni kaydedilen sertifikayı seçin. Kaydetmek için **Tamam** ' ı seçin ve ardından **Kapat**' ı seçin.

1. IIS Yöneticisi konsolunda, bağlantılar listesinde, Web sunucusunu seçin. Sağ taraftaki eylem panelinde **Yeniden Başlat**' ı seçin. Bu eylem Web sunucusu hizmetini yeniden başlatır.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a>Güvenilen kök sertifikayı dışarı aktarma

Active Directory Sertifika Hizmetleri, etki alanına katılmış tüm cihazlarda gerekli sertifikayı CA 'dan otomatik olarak yüklenir. Etki alanına katılmış olmayan cihazların site sistem rolleriyle iletişim kurması için gereken sertifikayı almak için, Web sunucusuna bağlanan sertifikadan dışarı aktarın.

1. IIS Yöneticisi 'nde **varsayılan Web sitesi**' ni seçin. Sağ taraftaki eylem panelinde **bağlamalar**' ı seçin.

1. Site bağlamaları penceresinde **https**' yi seçin ve ardından **Düzenle**' yi seçin.

1. Web sunucusu sertifikası ' nı seçin ve **görüntüle**' yi seçin.

1. Web sunucusu sertifikasının özelliklerinde, **sertifika yolu** sekmesine geçin. sertifika yolunun kökünü seçin ve **sertifikayı görüntüle**' yi seçin.

1. Kök sertifikanın özelliklerinde, **Ayrıntılar** sekmesine geçin ve ardından **Dosyaya Kopyala**' yı seçin.

1. Sertifika Dışarı Aktarma Sihirbazı ' nda, hoş geldiniz sayfasında **İleri**' yi seçin.

1. **Der kodlamalı Ikili X. 509.440 (. CER)** biçimlendirme yapın ve **İleri**' yi seçin.

1. Bu güvenilen kök sertifikayı tanımlamak için bir yol ve dosya adı girin. Dosya adı için, **araştır...**' a tıklayın, sertifika dosyasının kaydedileceği konumu seçin, dosyayı adlandırın ve **İleri**' yi seçin.

1. Ayarları gözden geçirin ve sertifikayı dosyaya aktarmak için **son** ' u seçin.

Sertifika yetkilinizin tasarımına bağlı olarak, ek alt CA kök sertifikalarını dışarı aktarmanız gerekebilir. Web sunucusu sertifikasının sertifika yolundaki diğer sertifikaları dışarı aktarmak için bu işlemi tekrarlayın.

## <a name="next-step"></a>Sonraki adım

> [!div class="nextstepaction"]
> [Cihaz kaydını ayarlama](set-up-device-enrollment-on-premises-mdm.md)
