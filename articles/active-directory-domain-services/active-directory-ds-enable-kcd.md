---
title: "Azure Active Directory Domain Services：啟用 Kerberos 限制委派 | Microsoft Docs"
description: "在 Azure Active Directory Domain Services 受管理的網域上啟用 Kerberos 限制委派"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a><span data-ttu-id="39c00-103">在受管理的網域上設定 Kerberos 限制委派 (KCD)</span><span class="sxs-lookup"><span data-stu-id="39c00-103">Configure kerberos constrained delegation (KCD) on a managed domain</span></span>
<span data-ttu-id="39c00-104">許多應用程式需要 tooaccess hello hello 使用者內容中的資源。</span><span class="sxs-lookup"><span data-stu-id="39c00-104">Many applications need tooaccess resources in hello context of hello user.</span></span> <span data-ttu-id="39c00-105">Active Directory 支援稱為 Kerberos 委派的機制，可用於此使用案例。</span><span class="sxs-lookup"><span data-stu-id="39c00-105">Active Directory supports a mechanism called Kerberos delegation, which enables this use-case.</span></span> <span data-ttu-id="39c00-106">此外，您可以限制委派，以便只有特定的資源可存取 hello hello 使用者內容中。</span><span class="sxs-lookup"><span data-stu-id="39c00-106">Further, you can restrict delegation so that only specific resources can be accessed in hello context of hello user.</span></span> <span data-ttu-id="39c00-107">Azure AD Domain Services 受管理的網域與傳統Active Directory 網域不同，因為前者的權限更為嚴格且更為安全。</span><span class="sxs-lookup"><span data-stu-id="39c00-107">Azure AD Domain Services managed domains are different from traditional Active Directory domains since they are more securely locked down.</span></span>

<span data-ttu-id="39c00-108">本文章將示範如何 tooconfigure kerberos 限制委派，在 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="39c00-108">This article shows you how tooconfigure kerberos constrained delegation on an Azure AD Domain Services managed domain.</span></span>

## <a name="kerberos-constrained-delegation-kcd"></a><span data-ttu-id="39c00-109">Kerberos 限制委派 (KCD)</span><span class="sxs-lookup"><span data-stu-id="39c00-109">Kerberos constrained delegation (KCD)</span></span>
<span data-ttu-id="39c00-110">Kerberos 委派可讓帳戶 tooimpersonate 另一個安全性主體 （例如使用者） tooaccess 資源。</span><span class="sxs-lookup"><span data-stu-id="39c00-110">Kerberos delegation enables an account tooimpersonate another security principal (such as a user) tooaccess resources.</span></span> <span data-ttu-id="39c00-111">請考慮存取 hello 使用者內容中的後端 web 應用程式開發介面的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39c00-111">Consider a web application that accesses a back-end web API in hello context of a user.</span></span> <span data-ttu-id="39c00-112">在此範例中，hello （hello 的服務帳戶或電腦/機器帳戶的內容中執行） 的 web 應用程式會模擬 hello 使用者存取 hello 資源 (後端 web 應用程式開發介面) 時。</span><span class="sxs-lookup"><span data-stu-id="39c00-112">In this example, hello web application (running in hello context of a service account or a computer/machine account) impersonates hello user when accessing hello resource (back-end web API).</span></span> <span data-ttu-id="39c00-113">Kerberos 委派是不安全的因為它並未限制資源 hello 模擬帳戶可以存取 hello hello 使用者內容中的 hello。</span><span class="sxs-lookup"><span data-stu-id="39c00-113">Kerberos delegation is insecure since it does not restrict hello resources hello impersonating account can access in hello context of hello user.</span></span>

<span data-ttu-id="39c00-114">Kerberos 限制委派 (KCD) 會限制的 hello hello 代表使用者執行的服務/資源 toowhich hello 指定的伺服器可採取動作。</span><span class="sxs-lookup"><span data-stu-id="39c00-114">Kerberos constrained delegation (KCD) restricts hello services/resources toowhich hello specified server can act on hello behalf of a user.</span></span> <span data-ttu-id="39c00-115">傳統的 KCD 的服務需要網域系統管理員權限 tooconfigure 網域帳戶，它會限制 hello 帳戶 tooa 單一網域。</span><span class="sxs-lookup"><span data-stu-id="39c00-115">Traditional KCD requires domain administrator privileges tooconfigure a domain account for a service and it restricts hello account tooa single domain.</span></span>

<span data-ttu-id="39c00-116">傳統 KCD 也有一些問題。</span><span class="sxs-lookup"><span data-stu-id="39c00-116">Traditional KCD also has a few issues associated with it.</span></span> <span data-ttu-id="39c00-117">在舊版作業系統 hello 網域系統管理員設定 hello 服務的位置，hello 服務系統管理員有哪些前端服務委派 toohello 他們所擁有的資源服務不實用的方式 tooknow。</span><span class="sxs-lookup"><span data-stu-id="39c00-117">In earlier operating systems where hello domain administrator configured hello service, hello service administrator had no useful way tooknow which front-end services delegated toohello resource services they owned.</span></span> <span data-ttu-id="39c00-118">和任何前端服務都可以委派 tooa 資源服務代表一個潛在的攻擊點。</span><span class="sxs-lookup"><span data-stu-id="39c00-118">And any front-end service that could delegate tooa resource service represented a potential attack point.</span></span> <span data-ttu-id="39c00-119">如果裝載前端服務的伺服器已遭到洩露，而且它是設定的 toodelegate tooresource 服務，可能也會有 hello 資源服務。</span><span class="sxs-lookup"><span data-stu-id="39c00-119">If a server that hosted a front-end service was compromised, and it was configured toodelegate tooresource services, hello resource services could also be compromised.</span></span>

> [!NOTE]
> <span data-ttu-id="39c00-120">在 Azure AD Domain Services 受管理的網域上，您沒有網域系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="39c00-120">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="39c00-121">因此，**無法在受管理的網域上設定傳統 KCD**。</span><span class="sxs-lookup"><span data-stu-id="39c00-121">Therefore, **traditional KCD cannot be configured on a managed domain**.</span></span> <span data-ttu-id="39c00-122">使用此文章中所述的資源型 KCD。</span><span class="sxs-lookup"><span data-stu-id="39c00-122">Use resource-based KCD as described in this article.</span></span> <span data-ttu-id="39c00-123">此機制也比較安全。</span><span class="sxs-lookup"><span data-stu-id="39c00-123">This mechanism is also more secure.</span></span>
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="39c00-124">資源型 Kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="39c00-124">Resource-based kerberos constrained delegation</span></span>
<span data-ttu-id="39c00-125">在 Windows Server 2012 R2 和 Windows Server 2012 中，已從 hello 網域系統管理員 toohello 服務系統管理員移轉的 hello 服務的 hello 能力 tooconfigure 限制委派。</span><span class="sxs-lookup"><span data-stu-id="39c00-125">In Windows Server 2012 R2 and Windows Server 2012, hello ability tooconfigure constrained delegation for hello service has been transferred from hello domain administrator toohello service administrator.</span></span> <span data-ttu-id="39c00-126">如此一來，hello 後端服務系統管理員可以允許或拒絕前端服務。</span><span class="sxs-lookup"><span data-stu-id="39c00-126">In this way, hello back-end service administrator can allow or deny front-end services.</span></span> <span data-ttu-id="39c00-127">此模型稱為「資源型 Kerberos 限制委派」。</span><span class="sxs-lookup"><span data-stu-id="39c00-127">This model is known as **resource-based kerberos constrained delegation**.</span></span>

<span data-ttu-id="39c00-128">資源型 KCD 是使用 PowerShell 所設定的。</span><span class="sxs-lookup"><span data-stu-id="39c00-128">Resource-based KCD is configured using PowerShell.</span></span> <span data-ttu-id="39c00-129">您可以使用 hello Set-adcomputer 或 Set-aduser cmdlet，根據 hello 模擬帳戶是電腦帳戶或使用者帳戶/服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="39c00-129">You use hello Set-ADComputer or Set-ADUser cmdlets, depending on whether hello impersonating account is a computer account or a user account/service account.</span></span>

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a><span data-ttu-id="39c00-130">為受管理的網域上的電腦帳戶設定資源型 KCD</span><span class="sxs-lookup"><span data-stu-id="39c00-130">Configure resource-based KCD for a computer account on a managed domain</span></span>
<span data-ttu-id="39c00-131">假設您擁有 hello 電腦上執行的 web 應用程式 ' contoso100-webapp.contoso100.com'。</span><span class="sxs-lookup"><span data-stu-id="39c00-131">Assume you have a web app running on hello computer 'contoso100-webapp.contoso100.com'.</span></span> <span data-ttu-id="39c00-132">它需要 tooaccess hello 資源 (web API 上執行 ' contoso100-api.contoso100.com') 的網域使用者的 hello 內容中。</span><span class="sxs-lookup"><span data-stu-id="39c00-132">It needs tooaccess hello resource (a web API running on 'contoso100-api.contoso100.com') in hello context of domain users.</span></span> <span data-ttu-id="39c00-133">以下是針對此案例設定資源型 KCD 的方式。</span><span class="sxs-lookup"><span data-stu-id="39c00-133">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a><span data-ttu-id="39c00-134">為受管理的網域上的使用者帳戶設定資源型 KCD</span><span class="sxs-lookup"><span data-stu-id="39c00-134">Configure resource-based KCD for a user account on a managed domain</span></span>
<span data-ttu-id="39c00-135">假設您有 web 應用程式執行為服務帳戶 'appsvc' 以及它 hello 網域使用者內容中需要 tooaccess hello 資源 (web API 執行為服務帳戶-'backendsvc')。</span><span class="sxs-lookup"><span data-stu-id="39c00-135">Assume you have a web app running as a service account 'appsvc' and it needs tooaccess hello resource (a web API running as a service account - 'backendsvc') in hello context of domain users.</span></span> <span data-ttu-id="39c00-136">以下是針對此案例設定資源型 KCD 的方式。</span><span class="sxs-lookup"><span data-stu-id="39c00-136">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a><span data-ttu-id="39c00-137">相關內容</span><span class="sxs-lookup"><span data-stu-id="39c00-137">Related Content</span></span>
* [<span data-ttu-id="39c00-138">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="39c00-138">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="39c00-139">Kerberos 限制委派概觀</span><span class="sxs-lookup"><span data-stu-id="39c00-139">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
