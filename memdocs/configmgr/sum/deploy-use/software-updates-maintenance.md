---
title: Yazılım güncelleştirmeleri bakımı
titleSuffix: Configuration Manager
description: Configuration Manager güncelleştirmeleri sürdürmek için WSUS temizleme görevini zamanlayabilir veya el ile çalıştırabilirsiniz.
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 1b11d0e54305b148a2f73a3a3af9f0497fe8e557
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608040"
---
# <a name="software-updates-maintenance"></a>Yazılım güncelleştirmeleri bakımı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

WSUS temizleme görevlerini Configuration Manager konsolundan, yazılım güncelleştirme noktası bileşen özelliklerinden zamanlayabilir ve çalıştırabilirsiniz. WSUS temizleme görevini çalıştırmayı ilk seçtiğinizde, bir sonraki yazılım güncelleştirmeleri eşitlemesi sonrasında çalışır.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>WSUS temizleme işini zamanlamak ve çalıştırmak için

Aşağıdaki adımları çalıştırarak WSUS temizleme işini zamanlayın:

1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **siteler**' e gidin.
2. Configuration Manager hiyerarşinizin en üstünde bulunan siteyi seçin.

3. **Ayarlar** grubunda **Site Bileşenlerini Yapılandır** ’a tıklayın ve ardından Yazılım Güncelleştirme Noktası Bileşen Özellikleri’ni açmak için **Yazılım Güncelleştirme Noktası** ’na tıklayın.  

4. **Yenisiyle değiştirme davranışını**gözden geçirin. Gerekirse davranışı değiştirin.

   ![yenisiyle değiştirme davranışı ekran görüntüsü](media/supersedence-behavior.png)

5. **Yenisiyle değiştirme kuralları** sekmesine tıklayın, **WSUS temizleme sihirbazını çalıştır**' ı seçin. Sürüm 1806 ' de, bu seçenek, **eşitlemeden sonra WSUS temizliği çalıştırılacak**şekilde yeniden adlandırılır.

6. **Tamam** ' a tıklayın (1806 sürümünü çalıştırıyorsanız **Kapat** ' a tıklayın).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Sürüm 1802 ve önceki sürümlerde WSUS temizleme davranışı

Sürüm 1806 ' Configuration Manager önce, WSUS temizleme seçeneği aşağıdaki öğeyi çalıştırır:

- WSUS temizleme sihirbazından yalnızca en üst düzey sitenin WSUS sunucusunda bulunan **zaman aşımına uğradı** seçeneği.

  ![WSUS zaman aşımına uğradı güncelleştirme temizleme ekran görüntüsü](media/wsus-cleanup-expired.PNG)

- Configuration Manager veritabanındaki yazılım güncelleştirme yapılandırma öğeleri için Temizleme işlemi yedi günde bir gerçekleşir ve gereksiz güncelleştirmeleri konsolundan kaldırır.
  - Bu Temizleme, şu anda dağıtıldıklarında, Configuration Manager konsolundan zaman aşımına uğradı güncelleştirmeleri kaldırmaz.

Ek bakım, en üst düzey WSUS veritabanında ve ortamdaki diğer tüm WSUS veritabanlarında hala gereklidir. Daha fazla bilgi ve yönergeler için bkz. [MICROSOFT WSUS ve CONFIGURATION Manager SUP Bakımı](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) blog gönderisi Kılavuzu.

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>WSUS temizleme davranışı sürüm 1806 ' den başlayarak

Sürüm 1806 ' den başlayarak, WSUS temizleme seçeneği her eşitlemede sonra oluşur ve aşağıdaki Temizleme öğelerini yapar:
<!--1357898 -->

- CA 'larda ve birincil sitelerde WSUS sunucuları için **zaman aşımına uğradı** seçeneği.
  - İkincil siteler için WSUS sunucuları, süre dolma güncelleştirmeleri için WSUS temizlemeyi çalıştırmaz.
- Configuration Manager, veritabanından yenisiyle değiştirilen güncelleştirmelerin bir listesini oluşturur. Liste, yazılım güncelleştirme noktası bileşen özelliklerindeki yerine geçme davranışına dayalıdır.
  - Yerine geçme davranış ölçütlerine uyan yapılandırma öğelerinin güncelleştirilmesi Configuration Manager konsolunda zaman aşımına uğradı.
  - Güncelleştirmeler, CA 'LAR ve birincil siteler için WSUS 'de reddedilir, ancak ikincil siteler için kullanılmaz.
- Configuration Manager veritabanındaki yazılım güncelleştirme yapılandırma öğeleri için Temizleme işlemi yedi günde bir gerçekleşir ve gereksiz güncelleştirmeleri konsolundan kaldırır.
  - Bu Temizleme, şu anda dağıtıldıklarında, Configuration Manager konsolundan zaman aşımına uğradı güncelleştirmeleri kaldırmaz.

> [!NOTE]
> "Yenisiyle değiştirilen güncelleştirme tamamlanmadan önce beklenecek ay sayısı", yerine geçen güncelleştirmenin oluşturulma tarihini temel alır. Örneğin, bu ayar için 2 ay kullanırsanız, yenisiyle değiştirilen Güncelleştirmeler 2 ay eski olduğunda WSUS 'de reddedilir ve Configuration Manager zaman aşımına uğradı.

Tüm WSUS bakımının ikincil site WSUS veritabanlarında el ile çalıştırılması gerekir. Aşağıdaki **WSUS sunucusu Temizleme Sihirbazı** seçenekleri CAS ve birincil sitelerde çalıştırılmazlar:

- Kullanılmayan güncelleştirmeler ve güncelleştirme düzeltmeleri
- Sunucuyla iletişim kurmayan bilgisayarlar
- Gereksiz güncelleştirme dosyaları

  Daha fazla bilgi ve yönergeler için bkz. [MICROSOFT WSUS ve CONFIGURATION Manager SUP Bakımı](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) blog gönderisi Kılavuzu.

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>WSUS temizleme davranışı sürüm 1810 ' den başlayarak

Sürüm 1810 ' den başlayarak, yazılım güncelleştirme noktası bileşen özelliklerindeki Özellik dışı güncelleştirmelerden ayrı olarak özellik güncelleştirmeleri için yerine geçme kuralları belirtebilirsiniz. WSUS temizleme seçeneği her eşitlemeden sonra oluşur ve aşağıdaki Temizleme öğelerini yapar:
<!--2839349,3098809, 2977644-->

- CA 'LAR, birincil ve ikincil sitelerde WSUS sunucuları için, **tarihi geçen güncelleştirmeler** seçeneği.
- Configuration Manager, veritabanından yenisiyle değiştirilen güncelleştirmelerin bir listesini oluşturur. Liste, yazılım güncelleştirme noktası bileşen özelliklerindeki yerine geçme davranışına dayalıdır.
  - Yerine geçme davranış ölçütlerine uyan yapılandırma öğelerinin güncelleştirilmesi Configuration Manager konsolunda zaman aşımına uğradı.
  - Güncelleştirmeler, CA 'LAR, birincil ve ikincil siteler için WSUS 'de reddedilir.
- Configuration Manager veritabanındaki yazılım güncelleştirme yapılandırma öğeleri için Temizleme işlemi yedi günde bir gerçekleşir ve gereksiz güncelleştirmeleri konsolundan kaldırır.
  - Bu Temizleme, şu anda dağıtıldıklarında, Configuration Manager konsolundan zaman aşımına uğradı güncelleştirmeleri kaldırmaz.

> [!NOTE]
> "Yenisiyle değiştirilen güncelleştirme tamamlanmadan önce beklenecek ay sayısı", yerine geçen güncelleştirmenin oluşturulma tarihini temel alır. Örneğin, bu ayar için 2 ay kullanırsanız, yenisiyle değiştirilen Güncelleştirmeler 2 ay eski olduğunda WSUS 'de reddedilir ve Configuration Manager zaman aşımına uğradı.

CA, birincil ve ikincil sitelerde aşağıdaki **WSUS sunucusu Temizleme Sihirbazı** seçenekleri çalıştırılmaz:

- Kullanılmayan güncelleştirmeler ve güncelleştirme düzeltmeleri
- Sunucuyla iletişim kurmayan bilgisayarlar
- Gereksiz güncelleştirme dosyaları

  Daha fazla bilgi ve yönergeler için bkz. [MICROSOFT WSUS ve CONFIGURATION Manager SUP Bakımı](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) blog gönderisi Kılavuzu.

## <a name="wsus-cleanup-starting-in-version-1906"></a>WSUS temizliği sürüm 1906 ' den başlayarak
<!--41101009-->

 Sağlıklı yazılım güncelleştirme noktalarını sürdürmek için Configuration Manager çalıştırabilirek WSUS bakım görevleriniz vardır. WSUS 'de süresi geçmiş güncelleştirmeleri reddetmenin yanı sıra, Configuration Manager WSUS veritabanlarına kümelenmemiş dizinler ekleyebilir ve eski güncelleştirmeleri WSUS veritabanlarından kaldırabilir. WSUS Bakımı her eşitlemeden sonra oluşur.

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>Değiştirme kurallarına göre WSUS 'ta zaman aşımına uğradı güncelleştirmeleri reddetme

WSUS içindeki güncelleştirmelerin reddediliyor, bu güncelleştirmeleri istemcilere gönderilen kataloglardan kaldırarak performansı geliştirir. Yenisiyle değiştirilen Configuration Manager işaretlerinin reddediliyor, katalogları en aza indirir ve performansı geliştirir.

1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **siteler**' e gidin.
2. Configuration Manager hiyerarşinizin en üstünde bulunan siteyi seçin.
3. **Ayarlar** grubunda Site Bileşenlerini Yapılandır ’a tıklayın ve ardından Yazılım Güncelleştirme Noktası Bileşen Özellikleri’ni açmak için **Yazılım Güncelleştirme Noktası** ’na tıklayın.
4. **WSUS bakım** sekmesinde, **yenisiyle DEĞIŞTIRME kurallarına göre WSUS 'ta zaman aşımına uğradı güncelleştirmeleri Reddet**' i seçin.

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>WSUS temizleme performansını geliştirmek için, kümelenmiş olmayan dizinleri WSUS veritabanına ekleme

Kümelenmemiş dizinlerin eklenmesi Configuration Manager, WSUS temizleme performansını geliştirir.

1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **siteler**' e gidin.
2. Configuration Manager hiyerarşinizin en üstünde bulunan siteyi seçin.
3. **Ayarlar** grubunda Site Bileşenlerini Yapılandır ’a tıklayın ve ardından Yazılım Güncelleştirme Noktası Bileşen Özellikleri’ni açmak için **Yazılım Güncelleştirme Noktası** ’na tıklayın.
4. **WSUS bakım** sekmesinde, **KÜMELENMIŞ olmayan dizinleri WSUS veritabanına ekle**' yi seçin.
5. Configuration Manager tarafından kullanılan her bir SUSDB üzerinde, dizinler aşağıdaki tablolara eklenir:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>Dizinler oluşturmak için SQL izinleri

WSUS veritabanı uzak bir SQL Server 'da olduğunda, dizin oluşturmak için SQL 'de izinler eklemeniz gerekebilir. WSUS veritabanına bağlanmak ve dizinleri oluşturmak için kullanılan hesap farklılık gösterebilir. [Yazılım güncelleştirme noktası özelliklerinde bir WSUS sunucusu bağlantı hesabı](../get-started/install-a-software-update-point.md#wsus-server-connection-account)belirtirseniz, bağlantı hesabının SQL izinlerine sahip olduğundan emin olun. WSUS sunucusu bağlantı hesabı belirtmezseniz, site sunucusunun bilgisayar hesabı SQL izinlerine ihtiyaç duyuyor.

- Dizin oluşturmak `ALTER` için tablo veya görünümde izin gerekir. Hesap, `sysadmin` sabit sunucu rolü veya `db_ddladmin` ve `db_owner` sabit veritabanı rollerinin bir üyesi olmalıdır. Oluşturma ve dizin ve izinler hakkında daha fazla bilgi için bkz. [create INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql#permissions).
- `CONNECT SQL`Hesaba sunucu izni verilmelidir. Daha fazla bilgi için bkz. [sunucu Izinleri verme (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql).

> [!NOTE]  
>  WSUS veritabanı, varsayılan olmayan bir bağlantı noktası kullanan uzak bir SQL Server 'da bulunuyorsa, dizinler eklenmeyebilir. Bu senaryo için [SQL Server Yapılandırma Yöneticisi kullanarak bir sunucu diğer adı](/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client) oluşturabilirsiniz. Diğer ad eklendikten ve Configuration Manager WSUS veritabanıyla bağlantı yapabilirler, dizinler eklenir.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Eski güncelleştirmeleri WSUS veritabanından kaldır

Eski güncelleştirmeler, WSUS veritabanında kullanılmayan güncelleştirmeler ve güncelleştirme düzeltmeleridir. Genellikle, bir güncelleştirme artık [Microsoft Update kataloğunda](https://www.catalog.update.microsoft.com/) olmadığı ve bir önkoşul veya bağımlılık olarak diğer güncelleştirmeler tarafından gerekli olmadığı kabul edilmez.

1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **siteler**' e gidin.
2. Configuration Manager hiyerarşinizin en üstünde bulunan siteyi seçin.
3. **Ayarlar** grubunda Site Bileşenlerini Yapılandır ’a tıklayın ve ardından Yazılım Güncelleştirme Noktası Bileşen Özellikleri’ni açmak için **Yazılım Güncelleştirme Noktası** ’na tıklayın.
4. **WSUS Bakımı** sekmesinde, **eski güncelleştirmeleri WSUS veritabanından kaldır**' ı seçin.
   - Eski güncelleştirme kaldırma işleminin durdurulmadan önce en fazla 30 dakika çalışmasına izin verilir. Sonraki eşitleme gerçekleştikten sonra yeniden başlatılır.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>Eski güncelleştirmeleri kaldırmak için SQL izinleri

WSUS veritabanı uzak bir SQL Server 'da olduğunda, site sunucusunun bilgisayar hesabı aşağıdaki SQL izinlerine ihtiyaç duyuyor:

- `db_datareader`Ve `db_datawriter` sabit veritabanı rolleri. Daha fazla bilgi için bkz. [veritabanı düzeyinde roller](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles).
- `CONNECT SQL`Sunucu izni, site sunucusunun bilgisayar hesabına verilmelidir. Daha fazla bilgi için bkz. [sunucu Izinleri verme (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql).

#### <a name="wsus-cleanup-wizard"></a>WSUS Temizleme Sihirbazı

Sürüm 1906 ' den başlayarak, aşağıdaki **WSUS sunucusu Temizleme Sihirbazı** seçenekleri CAS, birincil ve ikincil sitelerde çalıştırılmaz:

- Sunucuyla iletişim kurmayan bilgisayarlar
- Gereksiz güncelleştirme dosyaları

  Daha fazla bilgi ve yönergeler için bkz. [MICROSOFT WSUS ve CONFIGURATION Manager SUP Bakımı](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) blog gönderisi Kılavuzu.


### <a name="known-issues-for-version-1906"></a>Sürüm 1906 için bilinen sorunlar

Şu senaryoyu göz önünde bulundurun:
<!--5418148-->
- Configuration Manager sürüm 1906 kullanıyorsunuz
- Windows Iç veritabanı kullanan uzak yazılım güncelleştirme noktalarınız var
- **Yazılım güncelleştirme noktası bileşen özellikleri**' nde, **WSUS bakım** sekmesi altında aşağıdaki seçili seçeneklerden birini kullanabilirsiniz:
   - WSUS veritabanına kümelenmemiş dizinler ekleme
   - Eski güncelleştirmeleri WSUS veritabanından kaldır

Bu senaryoda Configuration Manager, uzak yazılım güncelleştirme noktaları için bir Windows Iç veritabanı kullanan yukarıdaki WSUS bakım görevlerini gerçekleştiremiyor. Bu sorun, Windows Iç veritabanı uzak bağlantılara izin vermediğinden oluşur. Site sunucusunda aşağıdaki hataları görürsünüz `WSyncMgr.log` :

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

Bu sorunu geçici olarak çözmek için, Windows Iç veritabanı 'nı kullanarak uzak yazılım güncelleştirme noktaları için WSUS bakımını otomatik hale getirebilirsiniz. Daha fazla bilgi ve ayrıntılı adımlar için bkz. [MICROSOFT WSUS ve CONFIGURATION Manager SUP bakımı için kapsamlı kılavuz](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

## <a name="updates-cleanup-log-entries"></a>Güncelleştirmeler Temizleme günlüğü girdileri

Aşağıdaki girişler için wsyncmgr. log ' i inceleyerek bu temizlemeyi doğrulayabilirsiniz:

- Bu günlük girişini gördüğünüzde WSUS 'ta yenisiyle değiştirilen güncelleştirmelerin reddi tamamlanır: `Cleanup processed <number> total updates and declined <number>`
- WSUS temizliği bu girişi gördüğünüzde başlatılıyor: `Calling WSUS Cleanup.`
- Bu girdiyi gördüğünüzde, zaman aşımına uğradı güncelleştirmeler için WSUS temizliği tamamlanır: `Successfully completed WSUS Cleanup.`
- Bu girdiyi gördüğünüzde Configuration Manager süre dolduğunda güncelleştirme yapılandırma öğeleri temizliği başlatılıyor: `Deleting old expired updates...`
- Bu girdiyi gördüğünüzde Configuration Manager süre dolduğunda güncelleştirme yapılandırma öğelerini Temizleme işlemi tamamlanır: `Deleted <number> expired updates total`