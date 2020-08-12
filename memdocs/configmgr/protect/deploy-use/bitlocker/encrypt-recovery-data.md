---
title: Kurtarma verilerini şifreleme
titleSuffix: Configuration Manager
description: Ağ üzerinden ve Configuration Manager veritabanında BitLocker kurtarma anahtarlarını, kurtarma paketlerini ve TPM parola karmalarını şifreleyin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e887d594e80c0f92340081d9b922bfc334d1b3a5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129197"
---
# <a name="encrypt-recovery-data"></a>Kurtarma verilerini şifreleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

Bir BitLocker yönetim ilkesi oluşturduğunuzda, Configuration Manager kurtarma hizmetini bir yönetim noktasına dağıtır. BitLocker yönetim ilkesinin **Istemci yönetimi** sayfasında, **BitLocker yönetim hizmetleri 'ni yapılandırdığınızda**, istemci, anahtar kurtarma bilgilerini site veritabanına yedekler. Bu bilgilere BitLocker kurtarma anahtarları, kurtarma paketleri ve TPM parola karmaları dahildir. Kullanıcılar korunan cihazından kilitlendiğinde, bu bilgileri cihaza erişimi kurtarmaya yardımcı olması için kullanabilirsiniz.

Bu bilgilerin hassas doğası göz önüne alındığında, aşağıdaki durumlarda bunu korumanız gerekir:

- Configuration Manager, ağ üzerinden geçiş sırasında verileri şifrelemek için istemciyle kurtarma hizmeti arasında bir HTTPS bağlantısı gerektirir. İki seçenek vardır:

  - HTTPS-yönetim noktası rolünün tamamını değil, kurtarma hizmetini barındıran yönetim noktasında IIS Web sitesini etkinleştirin. Bu seçenek yalnızca Configuration Manager sürüm 2002 için geçerlidir.<!-- 5925660 -->

  - HTTPS için yönetim noktasını yapılandırın. Yönetim noktasının özelliklerinde **istemci bağlantıları** ayarı **https**olmalıdır. Bu seçenek 1910 veya 2002 Configuration Manager sürümleri için geçerlidir.

    > [!NOTE]
    > Şu anda gelişmiş HTTP 'yi desteklememektedir.

- Ayrıca, bu verileri site veritabanında depolandığında şifrelemeyi de göz önünde bulundurun. Bir SQL sertifikası yüklerseniz, verilerinizi SQL 'de şifreler Configuration Manager.

    BitLocker yönetim şifreleme sertifikası oluşturmak istemiyorsanız, kurtarma verilerinin düz metin depolamaya katılım yapın. Bir BitLocker yönetim ilkesi oluşturduğunuzda, **kurtarma bilgilerinin düz metin olarak depolanmasına Izin verme**seçeneğini etkinleştirin.

    > [!NOTE]
    > Başka bir güvenlik katmanı, tüm site veritabanını şifrelemelidir. Veritabanında şifrelemeyi etkinleştirirseniz, Configuration Manager işlevsel bir sorun yoktur.
    >
    > Özellikle büyük ölçekli ortamlarda, dikkatli bir şekilde şifreleyin. Şifrelediğiniz tablolara ve SQL sürümüne bağlı olarak, %25 oranında bir performans düşüşü fark edebilirsiniz. Şifrelenmiş verileri başarıyla kurtarabilmeniz için yedekleme ve kurtarma planlarınızı güncelleştirin.

## <a name="certificate-requirements"></a>Sertifika gereksinimleri

### <a name="https-server-authentication-certificate"></a>HTTPS sunucusu kimlik doğrulama sertifikası

<!--5925660-->

Configuration Manager geçerli dal sürümü 1910 ' de, BitLocker kurtarma hizmeti 'ni bütünleştirmek için, bir yönetim noktasını HTTPS olarak etkinleştirmeniz gerekir. HTTPS bağlantısı, ağ üzerindeki kurtarma anahtarlarını Configuration Manager istemcisinden yönetim noktasına şifrelemek için gereklidir. Yönetim noktasını yapılandırma ve HTTPS için tüm istemciler birçok müşteri için zor olabilir.

Sürüm 2002 ' den başlayarak, HTTPS gereksinimi, tüm yönetim noktası rolünü değil kurtarma hizmetini barındıran IIS Web sitesi içindir. Bu değişiklik, sertifika gereksinimlerini andırmakta ve aktarım içindeki kurtarma anahtarlarını şifreler.

Artık yönetim noktasının **istemci bağlantıları** özelliği **http** veya **https**olabilir. Yönetim noktası **http**için yapılandırılmışsa, BitLocker kurtarma hizmetini desteklemek için:

1. Sunucu kimlik doğrulama sertifikası alın. Sertifikayı, BitLocker kurtarma hizmetini barındıran yönetim noktasındaki IIS Web sitesine bağlayın.

2. İstemcileri sunucu kimlik doğrulama sertifikasına güvenecek şekilde yapılandırın. Bu güveni gerçekleştirmenin iki yöntemi vardır:

    - Ortak ve genel olarak güvenilen bir sertifika sağlayıcısından bir sertifika kullanın. Örneğin, DigiCert, Thawte veya VeriSign ile sınırlı değildir. Windows istemcileri, bu sağlayıcılardan güvenilen kök sertifika yetkililerini (CA 'Lar) içerir. Bu sağlayıcılardan biri tarafından verilen bir sunucu kimlik doğrulama sertifikası kullanarak, istemcileriniz otomatik olarak ona güvenmelidir.

    - Kuruluşunuzun ortak anahtar altyapısında (PKI) bir CA tarafından verilen bir sertifika kullanın. Çoğu PKI uygulaması, güvenilen kök CA 'Ları Windows istemcilerine ekler. Örneğin, Active Directory Sertifika Hizmetleri 'ni Grup İlkesi ile kullanma. İstemcilerinizin otomatik olarak güvendiği bir CA 'dan sunucu kimlik doğrulama sertifikası verirseniz, CA güvenilen kök sertifikayı istemcilere ekleyin.

> [!TIP]
> Yalnızca kurtarma hizmeti ile iletişim kurması gereken istemciler, bir BitLocker yönetim ilkesiyle hedeflemesini planladığınız ve bir **Istemci yönetim** kuralı içeren istemcilerdir.

Bu bağlantıyla ilgili sorunları gidermek için istemcide **Bitlockermanagementhandler. log** dosyasını kullanın. Kurtarma hizmetine bağlantı için, günlük istemcinin kullandığı URL 'YI gösterir. İle başlayan bir girişi bulun `Checking for Recovery Service at` .

> [!NOTE]
> Sitenizde birden fazla yönetim noktası varsa, BitLocker tarafından yönetilen bir istemcinin iletişim kurabileceği sitedeki tüm yönetim noktalarında HTTPS 'yi etkinleştirin. HTTPS yönetim noktası kullanılamıyorsa, istemci bir HTTP yönetim noktasına yük devreder ve ardından kurtarma anahtarını emander.
>
> Bu öneri her iki seçenek için de geçerlidir: HTTPS için yönetim noktasını etkinleştirin veya yönetim noktasındaki kurtarma hizmetini barındıran IIS Web sitesini etkinleştirin.

### <a name="sql-encryption-certificate"></a>SQL şifreleme sertifikası

Site veritabanındaki BitLocker kurtarma verilerini şifrelemek için bu SQL sertifikası Configuration Manager kullanın. Aşağıdaki gereksinimleri karşıladığı sürece, BitLocker yönetim şifreleme sertifikası oluşturmak ve dağıtmak için kendi işleminizi kullanabilirsiniz:

- BitLocker yönetim şifreleme sertifikası adı olmalıdır `BitLockerManagement_CERT` .

- Bu sertifikayı bir veritabanı ana anahtarıyla şifreleyin.

- Aşağıdaki SQL kullanıcıları sertifika üzerinde **Denetim** izinlerine sahip olmalıdır:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Hiyerarşinizdeki her site veritabanında aynı sertifikayı dağıtın.

- Ortamınızdaki SQL Server en son sürümüne sahip sertifikayı oluşturun. Örnek:
  - SQL Server 2016 veya üzeri ile oluşturulan sertifikalar SQL Server 2014 veya daha önceki bir sürüm ile uyumludur.
  - SQL Server 2014 veya öncesiyle oluşturulan sertifikalar SQL Server 2016 veya üzeri sürümlerle uyumlu değildir.

## <a name="example-scripts"></a>Örnek betikler

Bu SQL betikleri, Configuration Manager site veritabanında BitLocker yönetim şifreleme sertifikası oluşturma ve dağıtma örnekleridir.

### <a name="create-certificate"></a>Sertifika Oluştur

Bu örnek betik aşağıdaki eylemleri yapar:

- Bir sertifika oluşturur
- İzinleri ayarlar
- Bir veritabanı ana anahtarı oluşturur

Bu betiği bir üretim ortamında kullanmadan önce, aşağıdaki değerleri değiştirin:

- Site veritabanı adı ( `CM_ABC` )
- Ana anahtar () oluşturmak için parola `MyMasterKeyPassword`
- Sertifika sona erme tarihi ( `20391022` )

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Sertifikayı Yedekle

Bu örnek betik bir sertifikayı yedekler. Sertifikayı bir dosyaya kaydettiğinizde, daha sonra hiyerarşideki diğer site veritabanlarına [geri yükleyebilirsiniz](#restore-certificate) .

Bu betiği bir üretim ortamında kullanmadan önce, aşağıdaki değerleri değiştirin:

- Site veritabanı adı ( `CM_ABC` )
- Dosya yolu ve adı ( `C:\BitLockerManagement_CERT_KEY` )
- Anahtar parolasını dışa aktarma ( `MyExportKeyPassword` )

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Verdiğiniz sertifika dosyasını ve ilişkili parolayı güvenli bir konuma depolayın.

### <a name="restore-certificate"></a>Sertifikayı geri yükle

Bu örnek betik bir sertifikayı bir dosyadan geri yükler. Başka bir site veritabanında oluşturduğunuz bir sertifikayı dağıtmak için bu işlemi kullanın.

Bu betiği bir üretim ortamında kullanmadan önce, aşağıdaki değerleri değiştirin:

- Site veritabanı adı ( `CM_ABC` )
- Ana anahtar parolası ( `MyMasterKeyPassword` )
- Dosya yolu ve adı ( `C:\BitLockerManagement_CERT_KEY` )
- Anahtar parolasını dışa aktarma ( `MyExportKeyPassword` )

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Sertifikayı doğrula

SQL 'in gerekli izinlerle sertifikayı başarıyla oluşturduğunu doğrulamak için bu SQL betiğini kullanın.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Sertifika geçerliyse, betik bir değeri döndürür `1` .

## <a name="see-also"></a>Ayrıca bkz.

Bu SQL komutları hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [SQL Server ve veritabanı şifreleme anahtarları](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Sertifika Oluştur](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [Yedekleme sertifikası](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [Ana anahtar oluştur](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [Yedekleme ana anahtarı](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [Sertifika izinleri verme](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
