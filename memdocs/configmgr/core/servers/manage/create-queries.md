---
title: Sorgu oluştur
titleSuffix: Configuration Manager
description: Configuration Manager sorguları oluşturma ve içeri aktarma hakkında daha fazla bulun. Örnek sorgular ve ipuçları içerir.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d15252c3b3c93c7e90e517c502c4c3dd2dfcf20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700053"
---
# <a name="create-queries-in-configuration-manager"></a>Configuration Manager sorgu oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager sorguları oluşturma ve içeri aktarma işlemi açıklanır.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a> Sorgu oluşturma  
 Configuration Manager bir sorgu oluşturmak için bu yordamı kullanın.  

1.  Configuration Manager konsolunda **izleme**' yi seçin.  

2.  **İzleme** çalışma alanında **sorgular**' ı seçin. **Giriş** sekmesinde, **Oluştur** grubunda, **sorgu oluştur**' u seçin.  

3.  **Sorgu oluşturma Sihirbazı**' nın **genel** sekmesinde, benzersiz bir ad ve isteğe bağlı olarak sorgu için bir açıklama belirtin.  

4.  Yeni sorgu için temel olarak kullanmak üzere varolan bir sorguyu içeri aktarmak istiyorsanız, **sorgu ekstresi al**' ı seçin. **Sorgu araştır** iletişim kutusunda, içeri aktarmak istediğiniz sorguyu seçin ve ardından **Tamam**' ı seçin.  

5.  **Nesne türü** listesinde sorgunun döndürmesini istediğiniz nesne türünü seçin. Bu tabloda, arayabileceğiniz nesne türlerinin bazı örnekleri açıklanmaktadır:  

    |Nesne türü|Açıklama|  
    |-----------------|-----------------|  
    |**Sistem Kaynağı**|Bir cihazın NetBIOS adı, istemci sürümü, istemci IP adresi ve Active Directory Domain Services bilgileri gibi tipik sistem özniteliklerini aramak için kullanın.|  
    |**User Kaynağı**|Kullanıcı adları, Kullanıcı grubu adları ve güvenlik grubu adları gibi tipik Kullanıcı bilgilerini aramak için kullanın.|  
    |**Dağıtım**|Dağıtım adı, zamanlama ve dağıtıldığı koleksiyon gibi tipik bir dağıtım özniteliklerini aramak için kullanın.|  

6.  Sorgu **Edit Query Statement** &lt; adı \> **ifade özellikleri** Iletişim kutusunu açmak için sorgu ifadesini düzenle ' yi seçin.  

7.  **General** &lt; Sorgu adı \> **ifade özellikleri** iletişim kutusunun Genel sekmesinde, sorgunun döndürdüğü öznitelikleri ve bunların nasıl görüntüleneceğini belirtin. Yeni bir öznitelik eklemek için **Yeni** simgesini seçin. Sorguyu doğrudan WMI Sorgu Dili (WQL) içinde girmek veya düzenlemek için **sorgu dilini göster** ' i de seçebilirsiniz. WMI sorgularının örnekleri için, bu makaledeki [örnek wql sorguları](#BKMK_Example) bölümüne bakın.  

    > [!TIP]  
    > Kendi WQL sorgularınızı oluşturmanıza yardımcı olması için aşağıdaki başvuru belgelerini kullanabilirsiniz:  
    >   
    > -   [WQL (WMI için SQL)](/windows/win32/wmisdk/wql-sql-for-wmi)  
    > -   [WHERE yan tümcesi](/windows/win32/wmisdk/where-clause)  
    > -   [WQL İşleçleri](/windows/win32/wmisdk/wql-operators)  

8.  **Criteria** &lt; Sorgu adı \> **ifade özellikleri** iletişim kutusunun ölçütler sekmesinde, sorgunun sonuçlarını iyileştirmek için kullanılan ölçütleri belirtin. Örneğin, yalnızca **xyz**site koduna sahip olan kaynakları döndürebilirsiniz. Bir sorgu için birden çok ölçüt yapılandırabilirsiniz.  

    > [!IMPORTANT]  
    > Hiçbir ölçüt içermeyen bir sorgu oluşturursanız, sorgu **Tüm Sistemler** koleksiyonundaki tüm cihazları döndürür.  

9. **Joins** &lt; Sorgu adı \> **ifade özellikleri** iletişim kutusunun birleşimler sekmesinde, iki farklı öznitelikten verileri Sorgu sonuçlarınızda birleştirebilirsiniz. Sorgu sonucunuz için farklı öznitelikler seçtiğinizde Configuration Manager otomatik olarak sorgu birleştirmeleri oluştursa da, **birleştirmeler** sekmesi daha gelişmiş seçenekler sağlar. Configuration Manager Bu öznitelik sınıflarını destekler:  

    |Katılım türü|Açıklama|  
    |---------------|-----------------|  
    |İç|Yalnızca eşleşen sonuçları görüntüler. Her zaman otomatik olarak oluşturulan birleşimler tarafından kullanılır.|  
    |Sol|Base özniteliği için tüm sonuçları ve join özniteliği için yalnızca eşleşen sonuçları görüntüler.|  
    |Sağ|JOIN özniteliği için tüm sonuçları ve Base özniteliği için yalnızca eşleşen sonuçları görüntüler.|  
    |Tam|Hem temel öznitelik hem de JOIN özniteliği için tüm sonuçları görüntüler.|  

     JOIN işlemlerini kullanma hakkında daha fazla bilgi için SQL Server belgelerine bakın.  

10. **OK** &lt; Sorgu adı \> **ifade özellikleri** Iletişim kutusunu kapatmak için Tamam ' ı seçin.  

11. **Sorgu oluşturma Sihirbazı**' nın **genel** sekmesinde, sorgunun sonuçlarının bir koleksiyonun üyeleriyle sınırlı olmadığından, belirtilen bir koleksiyonun üyeleriyle sınırlı olduğunu veya sorgunun her çalıştırılışında bir koleksiyon isteminin göründüğünü belirtin.  

12. Sorguyu oluşturmak için sihirbazı tamamlayın. Yeni sorgu **izleme** çalışma alanındaki **sorgular** düğümünde görünür.  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a> Sorgu içeri aktar  
 Configuration Manager bir sorguyu içeri aktarmak için bu yordamı kullanın. Sorguları dışa aktarma hakkında daha fazla bilgi için bkz. [sorguları yönetme](../../../core/servers/manage/manage-queries.md).  

1.  Configuration Manager konsolunda **izleme**' yi seçin.  

2.  **İzleme** çalışma alanında **sorgular**' ı seçin. **Giriş** sekmesinde, **Oluştur** grubunda, **nesneleri içeri aktar**' ı seçin.  

3.  **Nesneleri Içeri aktarma Sihirbazı**' nın **MOF dosya adı** sayfasında, içeri aktarmak istediğiniz SORGUYU içeren yönetilen nesne biçimi (MOF) dosyasını seçmek için **Araştır** ' ı seçin.  

4.  İçeri aktarılacak sorguyla ilgili bilgileri gözden geçirin ve Sihirbazı doldurun. Yeni sorgu **izleme** çalışma alanındaki **sorgular** düğümünde görünür.  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Örnek WQL sorguları

Bu bölüm, hiyerarşinizde kullanabileceğiniz veya başka amaçlarla değiştirebileceğiniz örnek WQL sorgularını içerir. Bu sorguları kullanmak için **sorgu ekstresi özellikleri** Iletişim kutusunda **sorgu dilini göster** ' i seçin. Sonra sorguyu kopyalayıp **sorgu ekstresi** alanına yapıştırın.  

> [!TIP]  
> Herhangi bir karakter dizesini belirtmek için `%` joker karakterini kullanın. Örneğin, `%Visio%` Microsoft Office Visio 2010 ' i döndürür.  

### <a name="computers-that-run-windows-10"></a>Windows 10 çalıştıran bilgisayarlar

Windows 7 çalıştıran tüm bilgisayarların NetBIOS adını ve işletim sistemi sürümünü döndürmek için aşağıdaki sorguyu kullanın.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Belirli bir yazılım paketinin yüklü olduğu bilgisayarlar  

Belirli bir yazılım paketinin yüklü olduğu tüm bilgisayarların NetBIOS adını ve yazılım paketi adını döndürmek için aşağıdaki sorguyu kullanın. Bu örnek, bir Microsoft Visio sürümü yüklü olan tüm bilgisayarları döndürür. `Microsoft%Visio%`Sorgulamak istediğiniz yazılım paketi ile değiştirin.  

> [!TIP]  
> Bu sorgu, Windows Denetim Masası'ndaki programlar listesinde görüntülenen adları kullanarak yazılım paketini arar.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Belirli bir Active Directory Domain Services kuruluş birimindeki bilgisayarlar

Belirtilen bir OU 'daki tüm bilgisayarların NetBIOS adını ve kuruluş birimi (OU) adını döndürmek için aşağıdaki sorguyu kullanın. Metni, `OU Name` sorgulamak ISTEDIĞINIZ OU adı ile değiştirin.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Belirli bir NetBIOS adına sahip bilgisayarlar

Belirli bir karakter dizesi ile başlayan tüm bilgisayarların NetBIOS adını döndürmek için aşağıdaki sorguyu kullanın. Bu örnekte sorgu, ile başlayan bir NetBIOS adı olan tüm bilgisayarları döndürür `ABC` .  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Belirli bir türdeki cihazlar

Cihaz türleri, kaynak sınıfı **SMS_R_System** ve öznitelik adı **sistem**adı altında Configuration Manager veritabanında depolanır. Yalnızca belirttiğiniz cihaz türünün Aracı sürümüyle eşleşen cihazları almak için bu sorguyu kullanın:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Cihaz KIMLIĞI için şu değerlerden birini kullanın &lt; \> :  

|Cihaz Türü|AgentEdition değeri|  
|-----------------|---------------------------|  
|Windows Masaüstü veya dizüstü bilgisayar|0|  
|Windows ARM tabanlı cihaz (Windows RT çalıştıran)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac bilgisayar|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Yonga üzerinde Intel sistemi|12|  
|Unix ve Linux sunucuları|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> Bu tabloda listelenmeyen değerler artık desteklenmeyen cihazlarla ilişkilidir.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Örneğin, yalnızca Mac bilgisayarları döndürmek istiyorsanız bu sorguyu kullanın:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Sonraki adımlar

[Sorguları yönetme](manage-queries.md)