---
title: Kullanıcıları bir bilgisayarla ilişkilendirme
titleSuffix: Configuration Manager
description: İşletim sistemlerini dağıttığınızda kullanıcıları hedef bilgisayarlarla ilişkilendirmek için Configuration Manager yapılandırın.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724205"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Kullanıcıları Configuration Manager bir hedef bilgisayarla ilişkilendir

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İşletim sistemlerini dağıtmak için Configuration Manager kullandığınızda, kullanıcıları hedef bilgisayarla ilişkilendirebilirsiniz. Bu seçenek, tek bir kullanıcının veya birden çok kullanıcının hedef bilgisayarın birincil kullanıcısı olup olmadığı konusunda çalışmaktadır.  

Kullanıcı aygıt benzeşimi, uygulamaları dağıttığınızda kullanıcı merkezli yönetimi destekler. Bir kullanıcıyı bir işletim sistemini yüklemek için hedef bilgisayarla ilişkilendirdiğinizde, daha sonra bu kullanıcıya uygulamalar dağıtabilirsiniz ve uygulamalar hedef bilgisayara otomatik olarak yüklenir. İşletim sistemi dağıtımı sırasında Kullanıcı cihaz benzeşimi desteğini yapılandırabilmeniz sırasında, işletim sistemini dağıtmak için Kullanıcı aygıt benzeşimini kullanamazsınız.  

Kullanıcı cihaz benzeşimi hakkında daha fazla bilgi için bkz. [Kullanıcı cihaz benzeşimi ile kullanıcıları ve cihazları bağlama](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Kullanıcı cihaz benzeşimini işletim sistemi dağıtımlarınızla tümleştirebilmeniz için kullanabileceğiniz çeşitli yöntemler vardır. Kullanıcı aygıt benzeşimi ile PXE dağıtımlarını, önyüklenebilir medya dağıtımlarını ve önceden hazırlanan medya dağıtımlarını tümleştirebilirsiniz.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>**SMSTSAssignUsersMode** değişkenini içeren bir görev dizisi oluşturun

[Görev dizisi değişkenini ayarla](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımını kullanarak **SMSTSAssignUsersMode** değişkenini görev dizinizin başına ekleyin. Bu değişken, kullanıcı bilgisinin nasıl işlendiğini belirlemektedir.

Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Kullanıcı bilgilerini toplayan bir başlatma öncesi komutu oluşturun

Başlatma öncesi komutu bir giriş kutusuyla VBScript olabilir. Ayrıca, girdikleri Kullanıcı verilerini doğrulayan bir HTML uygulaması (HTA) de olabilir. 

Bu başlatma öncesi komutu, görev dizisi çalıştırıldığında kullanılan **Smstsudadusers** değişkenini ayarlamalıdır. Bu değişken, bir bilgisayar, koleksiyon veya bir görev dizisi değişkeni için ayarlanabilir.

Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Dağıtım noktaları ve medyanın, kullanıcı ile hedef bilgisayarı nasıl ilişkilendireceğini yapılandırın

Dağıtım noktası veya medya, kullanıcıların işletim sisteminin dağıtıldığı hedef bilgisayarla ilişkilendirilmesini destekler. Aşağıdaki yöntemlerden birini kullanın: 

- [PXE önyükleme isteklerini kabul etmek için bir dağıtım noktası yapılandırma](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [Önyüklenebilir ortam oluşturma](../deploy-use/create-bootable-media.md)  
- [Önceden hazırlanmış medya oluşturma](../deploy-use/create-prestaged-media.md)  


Kullanıcı cihaz benzeşimi desteğinin yapılandırılması, Kullanıcı kimliğini doğrulamak için yerleşik bir yönteme sahip değildir. Bu davranış, bir teknisyen bilgisayarı hazırlayarak ve bilgileri Kullanıcı adına girdiğinde önemlidir. Görev dizisinin Kullanıcı bilgilerini nasıl işleyeceğini ayarlamaya ek olarak, bu seçenekleri dağıtım noktası ve medyada yapılandırmak, PXE önyüklemesinden veya belirli bir medya türünden başlatılan dağıtımları kısıtlama yeteneği sağlar.
