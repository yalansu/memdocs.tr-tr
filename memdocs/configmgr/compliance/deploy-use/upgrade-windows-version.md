---
title: Windows cihazlarını farklı bir sürüme yükseltme
titleSuffix: Configuration Manager
description: Windows 10 cihazlarını farklı bir Windows sürümüne otomatik olarak yükseltmek için Configuration Manager kullanın.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 57f8c503d8a8ac54604a2435641bb29d0b4a1847
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240686"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Windows cihazlarını Configuration Manager ile yeni bir sürüme yükseltme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

**Sürüm yükseltme Ilkesi** Windows 10 cihazlarını farklı bir sürüme otomatik olarak yükseltmenizi sağlar.

Aşağıdaki yükseltme yolları desteklenmektedir:

- Windows 10 Pro'dan Windows 10 Enterprise'a
- Windows 10 Home'dan Windows 10 Education'a
- Windows 10 Mobile'dan Windows 10 Mobile Enterprise'a

Cihazların Configuration Manager istemci yazılımını çalıştırması gerekir. [Şirket ıçı MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) tarafından yönetilen cihazlar desteklenmez.

## <a name="before-you-start"></a>Başlamadan önce

Cihazları en son sürüme yükseltmeye başlamadan önce, aşağıdaki önkoşulları gözden geçirin:  

- Windows 10 masaüstü sürümleri için: ilkeyle hedeflediğiniz tüm cihazlarda Windows 'un yeni sürümü için geçerli bir ürün anahtarı. Bu ürün anahtarı birden çok etkinleştirme anahtarı (MAK) veya bir genel toplu lisanslama anahtarı (GVLK) olabilir. Bir GVLK, anahtar yönetimi hizmeti (KMS) istemci kurulum anahtarı olarak da adlandırılır. Daha fazla bilgi için bkz. [toplu etkinleştirme planı](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). KMS istemci kurulum anahtarlarının bir listesi için, bkz. Windows Server etkinleştirme kılavuzunun [ek a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) . <!--496871-->  

- Windows 10 Mobile için: Microsoft Toplu Lisanslama Hizmet Merkezi 'nden (VLSC) bir XML Lisans dosyası. Bu dosya, ilkeyle hedeflediğiniz tüm cihazlarda Windows 'un yeni sürümü için lisanslama bilgilerini içerir.

- Bu ilke türünü yönetmek için Configuration Manager **tam yönetici** güvenlik rolünde olmanız gerekir.

## <a name="configure-the-policy"></a>İlkeyi yapılandırma  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve **Windows 10 sürüm yükseltme** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **sürüm yükseltme İlkesi Oluştur**' u seçin.  

3. **Ilke oluştur**' u seçin.  

4. **Sürüm Yükseltme İlkesi Oluşturma Sihirbazı** ’nın **Genel**sayfasında, aşağıdaki bilgileri belirtin:  

    - **Ad** -sürüm yükseltme ilkesi için bir ad girin  

    - **Açıklama** (isteğe bağlı)-isterseniz, ilke için Configuration Manager konsolunda tanımanıza yardımcı olacak bir açıklama girin  

    - **Cihaza Yükseltilecek SKU** -aşağı açılan listeden, Windows 10 Masaüstü veya Windows 10 Mobile 'ın hedef sürümünü seçin  

    - **Lisans bilgileri** -aşağıdaki seçeneklerden birini belirleyin:  

        - **Ürün anahtarı** -hedef Windows 10 masaüstü sürümü için geçerli bir ürün anahtarı girin  

            > [!NOTE]  
            > Ürün anahtarı içeren bir ilke oluşturduktan sonra, ürün anahtarını daha sonra düzenleyemezsiniz. Configuration Manager, güvenlik nedenleriyle anahtarı gizler. Ürün anahtarını değiştirmek için tüm anahtarı yeniden girin.  

        - **Lisans dosyası** -XML biçiminde geçerli bir lisans dosyası seçmek için **Araştır** ' ı seçin. Configuration Manager, Windows 10 Mobile cihazlarını yükseltmek için bu lisans dosyasını kullanır.  

5. Sihirbazı tamamlayın.  

## <a name="deploy-the-policy"></a>İlkeyi dağıtma  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve **Windows 10 sürüm yükseltme** düğümünü seçin.  

2. Dağıtmak istediğiniz Windows 10 sürüm yükseltme ilkesini seçin. Şeridin **giriş** sekmesinde, **dağıtım** grubunda, **Dağıt**' ı seçin.  

3. İlkeyi dağıtmak istediğiniz cihaz koleksiyonunu seçin.

4. İstemcinin ilkeyi değerlendiren zamanlamayı seçin.

5. Sihirbazı tamamlayın.

## <a name="next-steps"></a>Sonraki adımlar

Bu dağıtımı **izleme** çalışma alanının **dağıtımlar** düğümünden izleyin. Başarısız bir dağıtımı belirten hatalar görürseniz, örneğin:

- **Bu cihaz için uygulanamaz**
- **Veri türü dönüştürmesi başarısız oldu**

Bu hatalar dağıtımın başarısız olduğu anlamına gelmez. Hedeflenen cihazda yükseltmenin başarıyla çalıştığını doğrulayın.

İstemci hedeflenen ilkeyi değerlendirirken, yükseltmeyi iki saat içinde uygular. [Bazı Windows sürümlerinde](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades) bu süre için yeniden başlatma gerekebilir. İlkeyi dağıttığınız kullanıcıları bilgilendirdiğinizden emin olun veya ilkeyi kullanıcıların çalışma saatlerinin dışında çalışacak şekilde zamanlayın.

İstemci üzerindeki **Dcmwmiprovider. log** dosyasında aşağıdaki hata görünürse, etkinleştirme senaryonuz için uygun anahtarı kullandığınızdan emin olun. Daha fazla bilgi için, [başlamadan önce](#before-you-start) bölümüne bakın. Etkinleştirme için bir anahtar yönetimi hizmeti (KMS) kullanıyorsanız, bir [KMS istemci kurulum anahtarı](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)kullandığınızdan emin olun.  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>Ayrıca bkz.

- [Toplu etkinleştirme planı](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Windows 10 sürüm yükseltme](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Microsoft Intune kullanarak cihazlarda Windows 10 sürümlerini yükseltme veya S modunu değiştirme](https://docs.microsoft.com/intune/edition-upgrade-configure-windows-10)
