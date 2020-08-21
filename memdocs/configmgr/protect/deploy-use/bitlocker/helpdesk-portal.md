---
title: BitLocker yönetim ve izleme Web sitesi
titleSuffix: Configuration Manager
description: Configuration Manager 'de BitLocker yönetim ve izleme Web sitesini (yardım masası portalı) kullanma
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf9301e4fcb279b7d79a6f6c3d0a90ab3d15e277
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697322"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>BitLocker yönetim ve izleme Web sitesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

BitLocker yönetim ve izleme Web sitesi, BitLocker Sürücü Şifrelemesi için bir yönetim arabirimidir. Ayrıca, yardım masası portalı olarak da adlandırılır. Raporları gözden geçirmek, kullanıcıların sürücülerinde kurtarmak ve cihaz TPMs 'yi yönetmek için bu Web sitesini kullanın.

[![Varsayılan BitLocker yönetim ve izleme Web sitesinin ekran görüntüsü](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Kullanabilmeniz için, bu bileşeni bir Web sunucusuna yükleyebilirsiniz. Daha fazla bilgi için bkz. [BitLocker raporlarını ve portallarını ayarlama](setup-websites.md).

Yönetim ve izleme Web sitesine aşağıdaki URL aracılığıyla erişin: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> **Kurtarma denetim raporunu** yönetim ve izleme Web sitesinde görüntüleyebilirsiniz. Diğer BitLocker yönetim raporlarını Raporlama Hizmetleri noktasına eklersiniz. Daha fazla bilgi için bkz. [BitLocker raporlarını görüntüleme](view-reports.md).

## <a name="groups"></a>Gruplar

Yönetim ve izleme Web sitesinin belirli bölgelerine erişmek için, Kullanıcı hesabınızın aşağıdaki gruplardan birinde olması gerekir. İstediğiniz adı kullanarak bu grupları Active Directory oluşturun. Bu Web sitesini yüklediğinizde, bu grup adlarını belirtirsiniz. Daha fazla bilgi için bkz. [BitLocker raporlarını ve portallarını ayarlama](setup-websites.md).

|Grup|Açıklama|
|--- |--- |
|BitLocker yardım masası yöneticileri|Yönetim ve izleme Web sitesinin tüm bölümlerine erişim sağlar. Bir kullanıcının sürücüsünü kurtarmasına yardımcı olduğunuzda, etki alanını ve Kullanıcı adını değil, yalnızca kurtarma anahtarını girersiniz. Bir kullanıcı hem bu grubun hem de BitLocker yardım masası kullanıcıları grubunun üyesiyse, yönetici grubu izinleri Kullanıcı grubu izinlerini geçersiz kılar.|
|BitLocker yardım masası kullanıcıları|Yönetim ve izleme Web sitesinin **TPM** ve **sürücü kurtarma** alanlarının yönetimine erişim sağlar. Her iki alanı da kullandığınızda, kullanıcının etki alanı ve hesap adı dahil olmak üzere tüm alanları doldurmanız gerekir. Bir kullanıcı hem bu grubun hem de BitLocker yardım masası yöneticileri grubunun üyesiyse, yönetici grubu izinleri Kullanıcı grubu izinlerini geçersiz kılar.|
|BitLocker rapor kullanıcıları|Yönetim ve izleme Web sitesinin **raporlar** alanına erişim sağlar.|

## <a name="manage-tpm"></a>TPM 'YI yönetme

Bir Kullanıcı çok fazla kez hatalı PIN girerse TPM 'YI kilitleyebilir. TPM kilitleri üreticiden üreticiye kadar değişiklik yapmadan önce kullanıcının hatalı PIN girebilmesi için gereken sayı. Yönetim ve izleme Web sitesinin **TPM 'Yi Yönet** alanından merkezi anahtar kurtarma veri sistemine erişin.

TPM sahipliği hakkında daha fazla bilgi için bkz. [TPM 'yi emanetmek IÇIN MBAD 'Yi yapılandırma ve OwnerAuth parolalarını depolama](/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> Windows 10, sürüm 1607 ' den itibaren, Windows TPM 'yi sağlarken TPM sahip parolasını tutmaz.

1. Örneğin, Web tarayıcısında yönetim ve izleme Web sitesine gidin `https://webserver.contoso.com/HelpDesk` .

1. Sol bölmede **TPM 'Yi Yönet** alanını seçin.

    ![BitLocker yönetim ve izleme Web sitesi TPM sayfasını yönetme](media/bitlocker-admin-manage-tpm.png)

1. Bilgisayar için tam etki alanı adını ve bilgisayar adını girin.

1. Gerekirse TPM sahip parola dosyasını almak için kullanıcının etki alanını ve Kullanıcı adını girin.

1. **TPM sahip parola dosyası ISTEME nedeni**için aşağıdaki seçeneklerden birini belirleyin:

    - PIN kilitlemeyi Sıfırla
    - TPM 'yi aç
    - TPM 'YI kapatma
    - TPM parolasını değiştirme
    - TPM 'YI temizle
    - Diğer

    Formu **gönderdikten** sonra, Web sitesi aşağıdaki yanıtlardan birini döndürür:

    - Eşleşen bir TPM sahip parola dosyası bulamazsa, bir hata iletisi döndürür.

    - Gönderilen bilgisayar için TPM sahip parolası dosyası

    TPM sahip parola dosyasını aldıktan sonra, Web sitesi sahip parolasını görüntüler.

1. Parolayı bir dosyaya kaydetmek için **Kaydet**' i seçin.

1. **TPM 'Yi Yönet** alanında **TPM kilitlemeyi Sıfırla** seçeneğini belirleyin ve TPM sahibi parola dosyasını belirtin.

    TPM kilitleme sıfırlanır. BitLocker kullanıcının cihaza erişimini geri yükler.

    > [!IMPORTANT]
    > TPM karma değeri veya TPM sahip parola dosyasını paylaşmayın.

## <a name="drive-recovery"></a>Sürücü kurtarma

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a> Kurtarma modunda bir sürücüyü kurtarma

Sürücüler, aşağıdaki senaryolarda kurtarma moduna geçer:

- Kullanıcı PIN veya parolasını kaybeder veya unutur
- Güvenilir modül platformu (TPM) bilgisayarın BIOS veya başlangıç dosyalarındaki değişiklikleri algılar

Kurtarma parolası almak için yönetim ve izleme Web sitesinin **sürücü kurtarma** alanını kullanın.

> [!IMPORTANT]
> Kurtarma parolalarının kullanım süresini tek bir kullanım sonrasında dolacak. İşletim sistemi sürücülerinde ve sabit veri sürücülerinde, tek kullanım kuralı otomatik olarak uygulanır. Çıkarılabilir sürücülerde, sürücüyü kaldırıp yeniden eklediğinizde geçerli olur.

1. Örneğin, Web tarayıcısında yönetim ve izleme Web sitesine gidin `https://webserver.contoso.com/HelpDesk` .

1. Sol bölmede **sürücü kurtarma** alanını seçin.

    ![BitLocker yönetim ve izleme Web sitesi sürücü kurtarma sayfası](media/bitlocker-admin-drive-recovery.png)

1. Gerekirse, kurtarma bilgilerini görüntülemek için kullanıcının etki alanını ve Kullanıcı adını girin.

1. Olası eşleşen kurtarma anahtarlarının bir listesini görmek için, kurtarma anahtarı KIMLIĞININ ilk sekiz basamağını girin. Tam kurtarma anahtarını almak için tüm kurtarma anahtarı KIMLIĞINI girin.

1. **Sürücü kilidi açma nedeni**olarak aşağıdaki seçeneklerden birini belirleyin:

    - İşletim sistemi önyükleme sırası değişti
    - BIOS değişti
    - Değiştirilen işletim sistemi dosyaları
    - Kayıp başlangıç anahtarı
    - PIN kayıp
    - TPM sıfırlama
    - Kayıp parola
    - Kayıp akıllı kart
    - Diğer

    Formu **gönderdikten** sonra, Web sitesi aşağıdaki yanıtlardan birini döndürür:

    - Kullanıcının birden çok eşleşen kurtarma parolası varsa, birden çok olası eşleşme döndürür.

    - Gönderilen Kullanıcı için kurtarma parolası ve kurtarma paketi.

        > [!NOTE]
        > Hasarlı bir sürücüyü kurtarıyorsanız, kurtarma paketi seçeneği BitLocker 'ı sürücüyü kurtarmak için gereken kritik bilgileri sağlar.

    - Eşleşen bir kurtarma parolası bulamazsa, bir hata iletisi döndürür.

    Kurtarma parolasını ve kurtarma paketini aldıktan sonra, Web sitesi kurtarma parolasını görüntüler.

1. Parolayı kopyalamak için **anahtarı Kopyala**' yı seçin. Kurtarma parolasını bir dosyaya kaydetmek için **Kaydet**' i seçin.

Sürücünün kilidini açmak için kurtarma parolasını girin veya kurtarma paketini kullanın.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a> Taşınan sürücüyü kurtarma

TPM farklı olduğu için bir sürücüyü yeni bir bilgisayara taşıdığınızda, BitLocker önceki PIN 'ı kabul etmez. Taşınan sürücüyü kurtarmak için kurtarma parolasını almak üzere kurtarma anahtarı KIMLIĞINI alın.

Taşınan bir sürücüyü kurtarmak için yönetim ve izleme Web sitesinin **sürücü kurtarma** alanını kullanın.

1. Taşınan sürücüye sahip bilgisayarda, bilgisayarı Windows kurtarma ortamı (WinRE) modunda başlatın.

1. WinRE 'de, BitLocker taşınan işletim sistemi sürücüsünü sabit veri sürücüsü olarak değerlendirir. BitLocker, sürücünün kurtarma parolası KIMLIĞINI görüntüler ve kurtarma parolası ister.

    > [!NOTE]
    > Bazı durumlarda, başlangıç işlemi sırasında, seçenek varsa **PIN 'i unuttum** ' u seçin. Kurtarma anahtarı KIMLIĞINI göstermek için kurtarma moduna girin.

1. Yönetim ve izleme Web sitesinden Kurtarma parolasını almak için kurtarma anahtarı KIMLIĞINI kullanın. Daha fazla bilgi için bkz. [Kurtarma modunda bir sürücüyü kurtarma](#bkmk_recovery).

Taşınan sürücüyü özgün bilgisayarda bir TPM yongasını kullanacak şekilde yapılandırdıysanız, aşağıdaki adımları izleyin. Aksi takdirde, kurtarma işlemi tamamlanır.

1. Sürücünün kilidini açtıktan sonra, bilgisayarı WinRE modunda başlatın. WinRE 'de bir komut istemi açın ve `manage-bde` sürücünün şifresini çözmek için komutunu kullanın. Bu araç, **TPM + PIN** koruyucuyu orijinal TPM yongası olmadan kaldırmanın tek yoludur. Bu komut hakkında daha fazla bilgi için bkz. [manage-bde](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. Bu tamamlandığında bilgisayarı normal şekilde başlatın. Configuration Manager BitLocker ilkesini, sürücüyü yeni bilgisayarın TPM Plus PIN 'ı ile şifrelemek üzere zorlayacaktır.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a> Bozuk sürücüyü kurtarma

Yönetim ve izleme Web sitesinden bir kurtarma anahtarı paketi almak için kurtarma anahtarı KIMLIĞINI kullanın. Daha fazla bilgi için bkz. [Kurtarma modunda bir sürücüyü kurtarma](#bkmk_recovery).

1. **Kurtarma anahtarı paketini** bilgisayarınıza kaydedin, ardından sürücüyü bozuk sürücüye kopyalayın.

1. Yönetici olarak bir komut istemi açın ve aşağıdaki komutu yazın:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Aşağıdaki değerleri değiştirin:

    - `<corrupted drive>`: Bozuk sürücünün sürücü harfi, örneğin `D:`
    - `<fixed drive>`: Var olan bir sabit disk sürücüsünün sürücü harfi, bozulan sürücüden benzer veya daha büyük boyutlu. BitLocker, bozuk sürücüdeki verileri belirtilen sürücüye kurtarır ve bu sürücüdeki verileri taşıyor. Bu sürücüdeki tüm verilerin üzerine yazılır.
    - `<key package>`: Kurtarma anahtarı paketinin konumu
    - `<recovery password>`: İlişkili kurtarma parolası

    Örnek:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Bu komut hakkında daha fazla bilgi için bkz. [Repair-BDE](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Raporlar

Yönetim ve izleme Web sitesi, **Kurtarma denetim raporunu**içerir. Diğer raporlar Configuration Manager Raporlama Hizmetleri noktasından kullanılabilir. Daha fazla bilgi için bkz. [BitLocker raporlarını görüntüleme](view-reports.md).

1. Örneğin, Web tarayıcısında yönetim ve izleme Web sitesine gidin `https://webserver.contoso.com/HelpDesk` .

1. Sol bölmede **raporlar** alanını seçin.

1. Üst menü çubuğundan **Kurtarma denetim raporunu**seçin.

Bu rapor hakkında daha fazla bilgi için bkz. [Kurtarma denetim raporu](view-reports.md#bkmk-audit)

> [!TIP]
> Rapor sonuçlarını kaydetmek için, **raporlar** menü çubuğunda **dışarı aktar** ' ı seçin.