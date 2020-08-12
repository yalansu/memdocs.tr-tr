---
title: Yönetim merkezinde kiracı iliştirme-uygulamalar (Önizleme)
titleSuffix: Configuration Manager
description: Yönetim merkezinden karşıya yüklenen Configuration Manager cihazları için uygulama yükleme.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ca71d40b29a9dcd9c239ccd06a8a28321f50f62c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127687"
---
# <a name="tenant-attach-install-an-application-from-the-admin-center-preview"></a><a name="bkmk_apps"></a>Kiracı iliştirme: yönetim merkezinden bir uygulama yükler (Önizleme)
<!--cm 6024389, in 7220536 pubpreview Aug 10, 2020-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir. Microsoft uç nokta Yönetimi yönetim merkezinden, bir kiracı ekli cihazı için gerçek zamanlı olarak bir uygulama yüklemesi başlatabilirsiniz.

   :::image type="content" source="media/6024389-tenant-attach-application-list.png" alt-text="Microsoft Endpoint Manager Yönetim Merkezi 'ndeki uygulamalar" lightbox="media/6024389-tenant-attach-application-list.png":::

## <a name="prerequisites"></a>Ön koşullar

- [Kiracı iliştirme önkoşulları: ConfigMgr istemci ayrıntıları](client-details.md#prerequisites).
- [Microsoft uç noktası Configuration Manager sürüm 2002](https://support.microsoft.com/help/4560496/) ve ilgili konsolun yüklü sürümü Için güncelleştirme paketi
- İsteğe bağlı özelliği **cihaz başına Kullanıcı için uygulama Isteklerini Onayla**' yı etkinleştirin. Daha fazla bilgi için, bkz. [Enable optional features from updates](../core/servers/manage/install-in-console-updates.md#bkmk_options).
- Yönetici ile bir cihaz koleksiyonuna dağıtılan en az bir uygulamanın, dağıtımda ayarlanan **cihaz seçeneğinde bu uygulama için bir isteği onaylaması gerekir** . Daha fazla bilgi için bkz. [uygulamaları onaylama](../apps/deploy-use/app-approval.md#bkmk_opt).
   - Onay seçenek kümesi olmayan kullanıcı hedefli uygulamalar veya uygulamalar, Configuration Manager sürüm 2002 ' i kullanırken uygulama listesinde görünmez.

Ayrıca, [Kullanıcı hedefli uygulamaları](#bkmk_user)yüklemek için aşağıdakiler gerekir:<!--7518897-->

- Configuration Manager sürüm 2006 ve ilgili konsolun yüklü sürümü.


## <a name="permissions"></a>İzinler

Kullanıcı hesabının aşağıdaki izinleri olması gerekir:

- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Configuration Manager içindeki **uygulama** için **okuma** izni.
- Configuration Manager uygulamasındaki **uygulama** için **onay** izni.
- Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü. 
  - Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir.
   > [!TIP]
   > [Azure AD 'Deki uygulama Yöneticisi rolü](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) , uygulamanın **Yönetici Kullanıcı** rolüne bir kullanıcı eklemek için yeterli izinlere sahiptir.

## <a name="deploy-an-application-to-a-device"></a><a name="bkmk_deploy"></a>Cihaza uygulama dağıtma

1. Bir tarayıcıda öğesine gidin [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. **Cihazlar** ve **tüm cihazlar**' ı seçin.
1. [Kiracı iliştirme](device-sync-actions.md)aracılığıyla Configuration Manager eşitlenen bir cihaz seçin.
1. **Uygulamalar**' ı seçin.
1. Uygulamayı seçin ve ardından **yüklensin**' e tıklayın.

   :::image type="content" source="media/6024389-tenant-attach-application-install.png" alt-text="Microsoft Endpoint Manager yönetim merkezinden uygulama yüklemesi" lightbox="media/6024389-tenant-attach-application-install.png":::

Görünümdeki tüm verileri bir. csv dosyasına dışarı aktarabilirsiniz. Sayfanın üst kısmında, dosyayı oluşturmak için **dışarı aktar** seçeneğini belirleyin. Görünüm 500 satırı aşarsa, yalnızca ilk 500 verilir.

## <a name="application-status"></a>Uygulama durumu

Durum temelinde uygulama listesini filtreleyebilirsiniz. Uygulama durumu aşağıdakilerden biri olabilir:

- **Kullanılabilir**: uygulama cihaza hiç yüklenmemiş.
- **Yüklü**: uygulama cihaza yüklenir.
- **Yükleme**: uygulama yükleme sürecinde.
- **Yükleme istendi**: yükleme istendi, ancak istemci isteği henüz kabul edilmedi.
   - Cihaz çevrimdışıysa, yeniden çevrimiçi olduktan ve ilkeyi aldıktan sonra Install isteği onaylanır.  
- **Başarısız**: uygulama yüklemesi başarısız oldu.
- **Gereksinimler Karşılanmadı**: uygulama gereksinimleri karşılanmadı.
- **Yüklü değil**: uygulama şu anda yüklü değil. Genellikle bu durum, farklı bir dağıtım veya Kullanıcı uygulamayı kaldırmışsa görülür.
- **Yeniden başlatma bekliyor**: uygulama yüklendi, ancak tamamlanmak için yeniden başlatma gerekiyor (sürüm 2006 ' den başlayarak).

## <a name="deploy-an-application-to-a-user"></a><a name="bkmk_user"></a>Kullanıcıya uygulama dağıtma
<!--7518897-->
Configuration Manager sürüm 2006 ' den başlayarak, Kullanıcı tarafından kullanılabilir uygulamalar ConfigMgr cihazının **uygulamalar** düğümünde görünür. Cihaz için kullanılabilen uygulamaların listesi, cihazın Şu anda oturum açmış olan kullanıcısına dağıtılan uygulamalar da içerir.

Bir kullanıcıya uygulama dağıtmak aşağıdaki sınırlamalara sahiptir:
- Çoklu Kullanıcı oturum senaryoları desteklenmez.
- Azure AD 'ye katılmış cihazlar şu anda desteklenmiyor.
   - Hem etki alanına katılmış hem de Azure AD 'ye katılmış cihazlar desteklenir.

## <a name="next-steps"></a>Sonraki adımlar

[Uygulama sorunlarını giderme](troubleshoot-applications.md)