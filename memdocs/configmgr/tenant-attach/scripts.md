---
title: Yönetim merkezinden kiracı iliştirme çalıştırma betikleri (Önizleme)
titleSuffix: Configuration Manager
description: Yönetim merkezinden Configuration Manager cihazları için betikleri çalıştırın.
ms.date: 09/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 6b6c0a9b-01c6-4e3f-9ae4-45c780b46f8b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: db3656f98949bfbff2bf31b19b50b0ccb9959845
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90803309"
---
# <a name="tenant-attach-run-scripts-preview-from-the-admin-center"></a><a name="bkmk_scripts"></a> Kiracı iliştirme: yönetim merkezinden betikleri çalıştırma (Önizleme)
<!--CM6234688, IN7220536-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

Şirket içi Configuration Manager Çalıştır özelliğinin gücünü Microsoft Endpoint Manager yönetim merkezine taşıyın. Yardım masası gibi ek personbuna, tek başına Configuration Manager yönetilen bir cihaza gerçek zamanlı olarak, PowerShell betikleri çalıştırmanızı sağlar. Bu, bu yeni ortama Configuration Manager yöneticisi tarafından önceden tanımlanmış ve onaylanmış olan PowerShell betiklerinin tüm geleneksel avantajlarını sağlar.

:::image type="content" source="./media/6234688-scripts.png" alt-text="Yönetim merkezindeki betik listesinin ekran görüntüsü" lightbox="./media/6234688-scripts.png":::


## <a name="prerequisites"></a>Önkoşullar

Yönetim merkezinden betikleri çalıştırmak için aşağıdaki öğeler gereklidir:

- [Kiracı iliştirme önkoşulları: ConfigMgr istemci ayrıntıları](client-details.md#prerequisites)
- [Configuration Manager geçerli dalı için sürüm 2006 yüklü olan KB4580678-Tenant iliştirme toplaması](https://support.microsoft.com/help/4580678) ile en az Configuration Manager sürüm 2006.
   - Hiyerarşideki tüm sitelerin en düşük Configuration Manager sürümü gereksinimini karşılaması gerekir.
- Configuration Manager istemcileri en son sürümü istemcisini çalıştırıyor olmalıdır.
- PowerShell betikleri çalıştırmak için, istemcinin PowerShell sürüm 3,0 veya üzerini çalıştırıyor olması gerekir.
   - Çalıştırdığınız bir betik, PowerShell 'in sonraki bir sürümünden işlevsellik içeriyorsa, betiği çalıştırdığınız istemcinin bu PowerShell 'in daha sonraki sürümünü çalıştırması gerekir.
- Configuration Manager ' de zaten oluşturulmuş ve onaylanmış en az bir betik.
   - Parametreleri olan betikler Şu anda desteklenmez ve Microsoft Endpoint Manager Yönetim merkezinde görünmez.
   - Yalnızca önceden oluşturulup onaylanan betikler Yönetim merkezinde görüntülenir. Betikleri onaylama hakkında daha fazla bilgi için bkz. [betiği onaylama veya reddetme](../apps/deploy-use/create-deploy-scripts.md#run-script-authors-and-approvers).

## <a name="permissions"></a>İzinler

Kullanıcı hesabının aşağıdaki izinleri olması gerekir:

- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Configuration Manager içinde cihaz **koleksiyonu** Için **kaynak oku** izni.
- Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü.
  - Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir.
- Betikleri kullanmak için uygun Configuration Manager güvenlik rolünün bir üyesi olmanız gerekir. Daha fazla bilgi için bkz. [çalıştırma betikleri Için güvenlik kapsamları](../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).
- Betikleri çalıştırmak için, hesabın **koleksiyonlar**Için **komut dosyası çalıştırma** izinlerine sahip olması gerekir.

## <a name="run-a-script"></a>Betik çalıştırma

1. Bir tarayıcıda öğesine gidin [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. **Cihazlar** ve **tüm cihazlar**' ı seçin.
1. [Kiracı iliştirme](device-sync-actions.md)aracılığıyla Configuration Manager eşitlenen bir cihaz seçin.
1. **Betikleri**seçin.
   
   En son çalıştırılan ve cihazı doğrudan hedefleyen betikler zaten listede olacak. Liste, Yönetim Merkezi, SDK veya Configuration Manager konsolundan çalıştırılan betikleri içerir. Şirket içi konsolundan, cihazı içeren koleksiyonlara karşı başlatılan betikler, komut dosyaları özel olarak tek bir cihaz için başlatılmadıkça gösterilmez.

   :::image type="content" source="./media/6234688-run-script.png" alt-text="Betiği yönetim merkezinden çalıştırma" lightbox="./media/6234688-run-script.png":::

1. **Betiği Çalıştır**' ı seçin.
   
   Configuration Manager ' de atanan kapsamları temel alan yönetici tarafından kullanılabilen betikler listelenecektir.
1. Betiği çalıştırmak için **Çalıştır** ' ı seçin.

1. Betiğinizin başlatıldığı size bildirilir. Cihaza bir tane göndermeden önce betiğin bitmesini beklemeniz gerekmez.
1. Listeyi en son betik durumuyla ve son çalışma zamanına göre güncelleştirmek için ana sayfada **Yenile** ' yi seçin.

1. Betik tamamlandığında, sonuçları **Çıkış** bölmesinde göstermek için betiği seçebilirsiniz. Betik çıktısının metnini kopyalayabilirsiniz. Betiğin yeniden çalıştırılmasını istiyorsanız **betiği yeniden çalıştır** ' ı seçin.

   :::image type="content" source="./media/6234688-script-output.png" alt-text="Yönetim merkezinde betik çıkışı" lightbox="./media/6234688-script-output.png":::

## <a name="next-steps"></a>Sonraki adımlar

[Yönetim merkezinden uygulama yüklemesi](applications.md)

[PowerShell betiği güvenliği hakkında daha fazla bilgi edinin](../apps/deploy-use/learn-script-security.md)