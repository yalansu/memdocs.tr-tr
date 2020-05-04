---
title: Active Directory etki alanları için destek
titleSuffix: Configuration Manager
description: Active Directory bir etki alanında Configuration Manager site sistemine yönelik gereksinimler hakkında bilgi edinin.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709617"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Configuration Manager Active Directory etki alanları için destek

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Tüm Configuration Manager site sistemleri desteklenen bir Active Directory etki alanının üyesi olmalıdır. Configuration Manager istemci bilgisayarları etki alanı üyeleri veya çalışma grubu üyeleri olabilir.  

## <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar

- Etki alanı üyeliği Ayrıca bir çevre ağında Internet tabanlı istemci yönetimini destekleyen site sistemleri için de geçerlidir. (Bu ağlar DMZ, sivil bölge ve denetimli alt ağ olarak da bilinir).  

- Bir site sistem rolü barındıran bir bilgisayar için aşağıdaki yapılandırmaların değiştirilmesi desteklenmez:  

  - Etki alanından bir site sistemini kaldırıp aynı etki alanına yeniden katılırsınız da dahil olmak üzere etki alanı üyeliği.

  - Etki alanı adı  

  - Bilgisayar adı  

  Bu değişiklikleri yapmadan önce, site sistem rolünü kaldırın. Bir site sunucusunda bu değişiklikleri yapmak için önce siteyi kaldırın. Ayrıca, site sunucusunda bu değişikliği yönetmeye yardımcı olması için [pasif modda bir site sunucusu](../../servers/deploy/configure/site-server-high-availability.md) oluşturmayı düşünebilirsiniz.

- Configuration Manager, Windows Server 2008 R2 veya üzeri etki alanı ve orman işlev düzeyini destekler.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Ayrık ad alanı

Configuration Manager site sistemlerini ve istemcileri *ayrık ad alanına*sahip bir etki alanına yükleyebilirsiniz.  

Ayrık bir ad alanında, bir bilgisayarın birincil DNS son eki bu bilgisayarın Active Directory DNS etki alanı adıyla eşleşmez. Etki alanı denetleyicisinin NetBIOS etki alanı adı Active Directory DNS etki alanı adıyla eşleşmezse, başka bir ayrık ad alanı senaryosu oluşur.  

### <a name="disjoint-scenarios"></a>Ayrık senaryolar

Aşağıdaki bölümlerde ayrık ad alanı için desteklenen senaryolar tanımlanır.  

#### <a name="scenario-1"></a>Senaryo 1

Etki alanı denetleyicisinin birincil DNS soneki, Active Directory DNS etki alanı adından farklıdır. Etki alanının üyesi olan bilgisayarlar ayrık olabilir veya olmayabilir.

Etki alanı denetleyicisi bu senaryoda ayrıktır. Etki alanının site sunucusu ve bilgisayar gibi üyesi olan bilgisayarların, eşleşen bir birincil DNS soneki olabilir:

- Etki alanı denetleyicisinin birincil DNS son eki
- Active Directory DNS etki alanı adı

#### <a name="scenario-2"></a>Senaryo 2

Etki alanı denetleyicisi kopuk olmasa da Active Directory etki alanındaki üye bir bilgisayar kopuk.

Bu senaryoda, bir site sisteminin birincil DNS son eki Active Directory DNS etki alanı adından farklıdır. Etki alanı denetleyicisinin birincil DNS soneki, Active Directory DNS etki alanı adıyla aynıdır. Configuration Manager istemcileri olan üye bilgisayarlarda, eşleşen birincil DNS son eki olabilir:

- Ayrık site sistemi sunucusunun birincil DNS son eki
- Active Directory DNS etki alanı adı

### <a name="configure-disjoint-namespace"></a>Ayrık ad alanını Yapılandır

Bir bilgisayarın ayrık etki alanı denetleyicilerine erişmesine izin vermek için, etki alanı nesne kapsayıcısında **msDS-AllowedDNSSuffixes** Active Directory özniteliğini değiştirin. Özniteliğe her iki DNS soneki de ekleyin.  

*DNS soneki arama listesinin* KURULUŞTAKI tüm DNS ad alanlarını içerdiğinden emin olmak için ayrık etki alanındaki her bir bilgisayar için arama listesini yapılandırın. Ad alanları listesine aşağıdaki sonekleri ekleyin:

- Etki alanı denetleyicisinin birincil DNS son eki
- DNS etki alanı adı
- Configuration Manager ile iletişim kurabildiği diğer sunucular için ek ad alanları

**Etki alanı adı sistemi (DNS) soneki arama** listesini yapılandırmak için Grup İlkesi kullanabilirsiniz.  

> [!IMPORTANT]  
> Configuration Manager bir bilgisayara başvurduğunuzda, birincil DNS sonekini kullanarak bilgisayarı girin. Bu sonek, Active Directory etki alanında **dNSHostName** özniteliği olarak kaydedilmiş tam etki alanı adı ve sistemle ilişkili hizmet asıl adı ile eşleşmelidir.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Tek etiketli etki alanları

Configuration Manager, aşağıdaki ölçütler karşılandığında tek etiketli bir etki alanında site sistemlerini ve istemcileri destekler:  

- Active Directory Domain Services 'deki tek etiketli etki alanını, geçerli bir üst düzey etki alanına sahip ayrık bir DNS ad alanıyla yapılandırın.  

  **Örneğin:** Tek etiketli Contoso etki alanı, contoso.com DNS‘inde ayrık ad alanı içerecek şekilde yapılandırılmıştır. Contoso etki alanındaki bir bilgisayar için Configuration Manager DNS son ekini belirttiğinizde, "contoso" değil "Contoso.com" belirtirsiniz.  

- Sistem bağlamındaki site sunucuları arasındaki dağıtılmış bileşen nesne modeli (DCOM) bağlantıları, Kerberos kimlik doğrulaması kullanılarak başarılı olmalıdır.  
