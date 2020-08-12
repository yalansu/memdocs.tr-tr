---
title: CMPivot sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager 'de CMPivot sorunlarını giderme hakkında bilgi edinin.
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6bddf46df63eac70a536faaee04a2ac7243e534a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128282"
---
# <a name="troubleshoot-cmpivot"></a>CMPivot sorunlarını giderme

CMPivot, ortamınızdaki cihazların gerçek zamanlı durumuna erişim sağlayan bir araçtır. CMPivot, hedef koleksiyondaki Şu anda bağlı olan tüm cihazlarda bir sorgu çalıştırır ve sonuçları döndürür.

Bazen CMPivot sorun gidermeniz gerekebilir. Örneğin, bir istemciden CMPivot 'e bir durum iletisi bozuksa, site sunucusu iletiyi işleyemez. Bu makale, CMPivot bilgi akışını anlamanıza yardımcı olur.

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a>Sürüm 1902 ve sonraki sürümlerde CMPivot sorunlarını giderme

Configuration Manager sürümleri 1902 ve üzeri sürümlerde, bir hiyerarşide merkezi yönetim sitesinden (CAS) CMPivot çalıştırabilirsiniz. Birincil site, istemci iletişimini hala işler.

CA 'lardan CMPivot çalıştırdığınızda, birincil siteyle iletişim kurmak için yüksek hızlı ileti abonelik kanalını kullanır. CMPivot, siteler arasında standart SQL çoğaltma kullanmaz. SQL Server Örneğiniz veya SQL sağlayıcınız uzak ise veya SQL Server her zaman açık kullanıyorsanız, CMPivot için bir "çift atlama senaryosu" olur. "Çift atlama senaryosu" için kısıtlanmış temsilciyi tanımlama hakkında daha fazla bilgi için bkz. [sürüm 1902 ' den başlayarak CMPivot](cmpivot-changes.md#bkmk_cmpivot1902).

>[!IMPORTANT]
> CMPivot sorunlarını giderirken, daha fazla bilgi edinmek için yönetim noktalarınız (MPs) ve site sunucusunun SMS_MESSAGE_PROCESSING_ENGINE ayrıntılı günlük kaydını etkinleştirin. Ayrıca, istemcinin çıkışı 80 KB 'tan büyükse, MP ve site sunucusunun SMS_STATE_SYSTEM bileşeninde ayrıntılı günlük kaydını etkinleştirin. Ayrıntılı günlük kaydını etkinleştirme hakkında daha fazla bilgi için bkz. [site sunucusu günlük seçenekleri](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="get-information-from-the-site-server"></a>Site sunucusundan bilgi al

Varsayılan olarak, site sunucusu günlük dosyaları konumunda bulunur `C:\Program Files\Microsoft Configuration Manager\logs` . Varsayılan olmayan bir yükleme dizini veya başka bir sunucuya SMS sağlayıcısı gibi boşaltılan öğeler belirttiyseniz bu konum farklı olabilir. CA 'lardan CMPivot çalıştırırsanız, Günlükler birincil site sunucusudur.

`smsprov.log`Şu satırları arayın:

- Configuration Manager sürüm 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager sürüm 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14`, CMPivot için komut dosyası GUID 'Sidir. Bu GUID 'yi, [CMPivot denetim durumu iletilerinde](cmpivot-changes.md#cmpivot-audit-status-messages)de görebilirsiniz.

Sonra, CMPivot penceresinde KIMLIĞI bulun. Bu KIMLIK `ClientOperationID` .

![Clienentoperationıd vurgulanmış CMPivot penceresi](media/cmpivot-client-operationid-1902.png)

`TaskID`ClientAction tablosundan öğesini bulun. , `TaskID` `UniqueID` Clientaction tablosundaki öğesine karşılık gelir.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

İçinde `BgbServer.log` , `TaskID` SQL 'den toplanan ve ' a göz atın `PushID` . , `TaskID` Etiketlidir `TaskGUID` . Örnek:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>İstemci günlükleri

Site sunucusundan bilgi aldıktan sonra istemci günlüklerine bakın. Varsayılan olarak, istemci günlükleri ' de bulunur `C:\Windows\CCM\Logs` .

' De `CcmNotificationAgent.log` , aşağıdaki satırlar gibi görünen günlük girdilerini arayın:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

İçin olup olmadığını denetleyin `Scripts.log` `TaskID` . Aşağıdaki örnekte şunları görürsünüz `Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}` :  

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> İçinde "(hızlı)" öğesini görmüyorsanız, `Scripts.log` veriler büyük olasılıkla 80 KB 'tan fazla olur. Bu durumda, bilgiler site sunucusuna durum iletisi olarak gönderilir. İstemci `StateMessage.log` ve site sunucusu ' nı kullanın `Statesys.log` .

### <a name="review-messages-on-the-site-server"></a>Site sunucusundaki iletileri gözden geçirme

Yönetim noktasında [ayrıntılı günlük](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client) etkinleştirildiğinde, gelen istemci iletilerinin nasıl işlendiğini görebilirsiniz. İçinde, `MP_RelayMsgMgr.log` için öğesini arayın `TaskID` .

`MP_RelayMsgMgr.log`Örnekte, ISTEMCININ kimliğini ve ' u görebilirsiniz `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}` . İleti işleme altyapısına gönderilmeden önce istemcinin yanıtına bir ileti KIMLIĞI atanır:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

[Ayrıntılı günlük](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) etkinleştirildiğinde `SMS_MESSAGE_PROCESSING_ENGINE.log` , istemci sonuçları işlenir. İçinden bulduğunuz ileti KIMLIĞINI kullanın `MP_RelayMsgMgr.log` . İşlem günlüğü girdileri aşağıdaki örneğe benzer:

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> İşlem sırasında bir özel durum alırsanız, aşağıdaki SQL sorgusunu çalıştırarak ve özel durum sütununa bakarak onu gözden geçirebilirsiniz. İleti işlendikten sonra artık tabloda yer olmayacaktır `MPE_RequestMessages_Instant` .
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

İçinde, `BgbServer.log` `PushID` bildirilen veya başarısız olan istemci sayısını görmek için öğesine bakın.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Kullanarak SQL 'den CMPivot için izleme görünümü ' ne bakın `TaskID` .

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[![1902 sürümünde sorun giderme IÇIN SQL sorguları CMPivot](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a>1810 ve önceki sürümlerde CMPivot sorunlarını giderme

Configuration Manager sürüm 1810 ve önceki sürümlerde, site sunucunuz istemci iletişimini yönetir.

### <a name="get-information-from-the-site-server"></a>Site sunucusundan bilgi al

Varsayılan olarak, site sunucusu günlük dosyaları konumunda bulunur `C:\Program Files\Microsoft Configuration Manager\logs` . Varsayılan olmayan bir yükleme dizini veya başka bir sunucuya SMS sağlayıcısı gibi boşaltılan öğeler belirttiyseniz bu konum farklı olabilir.

`smsprov.log`Bu satır için bakın:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

CMPivot penceresinde KIMLIĞI bulun. Bu KIMLIK `ClientOperationID` .

![Clienentoperationıd vurgulanmış CMPivot penceresi](media/cmpivot-clientoperationid.png)

`TaskID`ClientAction tablosundan öğesini bulun. , `TaskID` `UniqueID` Clientaction tablosundaki öğesine karşılık gelir.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

İçinde `BgbServer.log` , `TaskID` SQL 'den toplanan öğesine bakın. Etiketlendi `TaskGUID` . Örnek:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>İstemci günlükleri

Site sunucusundan bilgi aldıktan sonra istemci günlüklerine bakın. Varsayılan olarak, istemci günlükleri ' de bulunur `C:\Windows\CCM\Logs` .

' De `CcmNotificationAgent.log` , aşağıdaki girdiye benzer Günlükler arayın:  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

İçin bölümüne bakın `Scripts.log` `TaskID` . Aşağıdaki örnekte şunları görüyoruz `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}` :

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Bölümüne bakın `StateMessage.log` . Aşağıdaki örnekte, `TaskID` öğesinin yanındaki iletinin altına yaklaştı görürsünüz `<Param>` :

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Site sunucusundaki iletileri gözden geçirme

`statesys.log`İletinin alınıp işlenip işlenmediğini görmek için açın. Aşağıdaki örnekte, `TaskID` öğesinin yanında iletinin alt kısmına yakın bir ileti görürsünüz `<Param>` . Bu günlük girişlerini görmek için SMS_STATE_SYSTEM bileşende [ayrıntılı günlük kaydını](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) etkinleştirin.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

İleti işlenmediyse, durum iletisi gelen kutusunu kontrol edin. Varsayılan gelen kutusu konumu `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\` . Şu konumlardaki dosyaları arayın:

- Gelen
- Hatalı
- İşlem

Kullanarak SQL 'den CMPivot için izleme görünümü ' ne bakın `TaskID` .

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>Sürüm 1810 veya üstünü kullanan istemcilerde, çıkış 80 KB 'den büyük değilse durum mesajlaşma kullanılmaz. Bu durumlarda CMPivot sorunlarını giderirken, MPs 'niz ve site sunucusunun SMS_MESSAGE_PROCESSING_ENGINE ayrıntılı günlük kaydını etkinleştirdiğinizde daha fazla bilgi edinebilirsiniz. Ayrıntılı günlük kaydını etkinleştirme hakkında daha fazla bilgi için bkz. [site sunucusu günlük seçenekleri](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).
>
> Sorun gidermek için aşağıdaki günlüklere başvurun:
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>Sonraki adımlar

- [CMPivot kullanma](cmpivot.md)
- [PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md)
