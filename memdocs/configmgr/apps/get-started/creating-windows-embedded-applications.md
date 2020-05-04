---
title: Windows Embedded uygulamaları oluşturma
titleSuffix: Configuration Manager
description: Windows Embedded cihazları için uygulama oluştururken ve dağıtırken dikkate almanız gereken önemli noktalar bölümüne bakın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710499"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Configuration Manager ile Windows Embedded uygulamaları oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Uygulama oluşturmaya yönelik diğer Configuration Manager gereksinimleri ve yordamlarına ek olarak, Windows Embedded cihazları için uygulama oluştururken ve dağıtırken aşağıdaki noktaları da göz önüne almanız gerekir.  

## <a name="general-considerations"></a>Dikkat edilmesi gereken temel noktalar  

-   Yazma filtrelemesi için etkinleştirilmiş Windows Embedded cihazlarına uygulamalar dağıttığınızda, uygulama dağıtımı sırasında cihazda Yazma filtresinin devre dışı bırakılıp başlatılmayacağını belirtebilirsiniz. Ardından, uygulama dağıtımından sonra yazma filtresini yeniden başlatmayı tercih edebilirsiniz. Yazma filtresi devre dışı bırakılmamışsa, yazılım geçici bir katmana dağıtılır. Bu, başka bir dağıtım değişikliklerin kalıcı olmasını zorlamazsa, cihaz yeniden başlatıldığında yazılımın artık yüklenemeyeceği anlamına gelir.  

-   Windows Katıştırılmış aygıtına bir uygulamayı dağıttığınızda, aygıtın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun. Bu, yazma filtresinin ne zaman devre dışı ve etkin olduğunu ve aygıtın ne zaman yeniden başlatılacağını yönetmenizi sağlar.  

-   Yazma Filtresi davranışını denetleyen ayar, **değişiklikleri son tarihte veya bakım penceresinde Yürüt (yeniden başlatma gerektirir)** adlı bir onay kutusudur.  

## <a name="tips-for-deploying-applications"></a>Uygulamaları dağıtmak için ipuçları  

**Yazma filtreleri etkinleştirilmiş Windows Embedded cihazları için kullanılabilir uygulamalar yerine gerekli uygulamaları kullanın.** Kullanıcılar, yazma filtreleri kullanan Windows Embedded cihazındaki yazılım merkezi 'nden uygulama yükleyemediği için, her zaman bu cihazlar için **kullanılabilir** değil, uygulamaları **gerekli** bir dağıtım amacına dağıtın. Genellikle, Windows Embedded işletim sistemi çalıştıran bilgisayarlar genellikle birden çok kullanıcı için aynı şekilde çalıştırılması gereken tek bir uygulama çalıştırdığı için bu bir sorun değildir. Bundan dolayı bu aygıtlar BT departmanı tarafından yüksek oranda yönetilir ve kilitlenir. Gerekli uygulamalar bu senaryoya uymaktadır.

 Ancak, kullanıcılar yazma filtreleri kullanan katıştırılmış aygıtlarda birden fazla uygulama çalıştırmazlarsa aşağıdaki sınırlamalar konusunda bu kullanıcıları bilgilendirin:  

-   Kullanıcılar, Software Center'dan gerekli yazılımı yükleyemiyor.  

-   Kullanıcılar Yazılım Merkezi’nin Seçenekler sekmesinde bulunan iş saatlerini değiştiremiyor.  

-   Kullanıcılar gerekli bir uygulamanın yüklemesini erteleyemiyor.  

Ayrıca, yazılım yüklemeleri ve güncelleştirmelerinde Configuration Manager değişiklikler varsa düşük haklara sahip kullanıcılar bir bakım dönemi sırasında oturum açabilirler. Bu süre içinde kullanıcılar, aygıtın bakımı yapıldığından kullanılabilir olmadığını bildiren bir ileti görür.  

**Uygulamalar, kullanıcıların lisans koşullarını kabul etmesini gerektiriyorsa, yazma filtreleri etkinleştirilmiş Windows Embedded cihazlarına uygulamalar dağıtmayın.** Yazma filtreleri devre dışı bırakıldığında, Configuration Manager katıştırılmış cihazlara yazılım yükleyebildiğinden düşük haklara sahip kullanıcılar cihazda oturum açabilirler. Yükleme için kullanıcının lisans koşullarını kabul etmesi gerekirse bu mümkün olmayacaktır ve yükleme başarısız olacaktır. Uygulama kullanıcı etkileşimi gerektirdiğinde Windows Katıştırılmış aygıtlarına yazılım dağıtmadığınızdan emin olun. Bu işletim sistemlerini filtrelemek için Uygulanabilir Platformlar listesini kullanabilirsiniz.  
