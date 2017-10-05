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
ms.openlocfilehash: f36f16a7bb00ace9fd5164eb38ba77f015f22f5c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a><span data-ttu-id="86846-103">在受管理的網域上設定 Kerberos 限制委派 (KCD)</span><span class="sxs-lookup"><span data-stu-id="86846-103">Configure kerberos constrained delegation (KCD) on a managed domain</span></span>
<span data-ttu-id="86846-104">許多應用程式都需要以使用者的登入身分存取資源。</span><span class="sxs-lookup"><span data-stu-id="86846-104">Many applications need to access resources in the context of the user.</span></span> <span data-ttu-id="86846-105">Active Directory 支援稱為 Kerberos 委派的機制，可用於此使用案例。</span><span class="sxs-lookup"><span data-stu-id="86846-105">Active Directory supports a mechanism called Kerberos delegation, which enables this use-case.</span></span> <span data-ttu-id="86846-106">再者，您可以限制委派，讓使用者的登入身分只能用來存取特定資源。</span><span class="sxs-lookup"><span data-stu-id="86846-106">Further, you can restrict delegation so that only specific resources can be accessed in the context of the user.</span></span> <span data-ttu-id="86846-107">Azure AD Domain Services 受管理的網域與傳統Active Directory 網域不同，因為前者的權限更為嚴格且更為安全。</span><span class="sxs-lookup"><span data-stu-id="86846-107">Azure AD Domain Services managed domains are different from traditional Active Directory domains since they are more securely locked down.</span></span>

<span data-ttu-id="86846-108">此文章說明如何在 Azure AD Domain Services 受管理的網域上設定 Krberos 限制委派。</span><span class="sxs-lookup"><span data-stu-id="86846-108">This article shows you how to configure kerberos constrained delegation on an Azure AD Domain Services managed domain.</span></span>

## <a name="kerberos-constrained-delegation-kcd"></a><span data-ttu-id="86846-109">Kerberos 限制委派 (KCD)</span><span class="sxs-lookup"><span data-stu-id="86846-109">Kerberos constrained delegation (KCD)</span></span>
<span data-ttu-id="86846-110">Kerberos 委派可讓帳戶模擬另一個安全性主體 (例如使用者) 以存取資源。</span><span class="sxs-lookup"><span data-stu-id="86846-110">Kerberos delegation enables an account to impersonate another security principal (such as a user) to access resources.</span></span> <span data-ttu-id="86846-111">考慮一個可以使用者登入身分存取後端 Wb API 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86846-111">Consider a web application that accesses a back-end web API in the context of a user.</span></span> <span data-ttu-id="86846-112">在此案例中，Web 應用程式 (以服務帳戶身分或電腦/機器帳戶身分執行) 在存取資源 (後端 Web API) 時會模擬使用者。</span><span class="sxs-lookup"><span data-stu-id="86846-112">In this example, the web application (running in the context of a service account or a computer/machine account) impersonates the user when accessing the resource (back-end web API).</span></span> <span data-ttu-id="86846-113">Kerberos 委派不安全，因為它不會限制使用者登入身分中的模擬帳戶可存取的資源。</span><span class="sxs-lookup"><span data-stu-id="86846-113">Kerberos delegation is insecure since it does not restrict the resources the impersonating account can access in the context of the user.</span></span>

<span data-ttu-id="86846-114">Kerberos 限制委派 (KCD) 會限制指定的伺服器可代表使用者存取的服務/資源。</span><span class="sxs-lookup"><span data-stu-id="86846-114">Kerberos constrained delegation (KCD) restricts the services/resources to which the specified server can act on the behalf of a user.</span></span> <span data-ttu-id="86846-115">傳統 KCD 需要網域系統管理員權限才能設定服務的網域帳戶，而且會將該帳戶限制在單一網域。</span><span class="sxs-lookup"><span data-stu-id="86846-115">Traditional KCD requires domain administrator privileges to configure a domain account for a service and it restricts the account to a single domain.</span></span>

<span data-ttu-id="86846-116">傳統 KCD 也有一些問題。</span><span class="sxs-lookup"><span data-stu-id="86846-116">Traditional KCD also has a few issues associated with it.</span></span> <span data-ttu-id="86846-117">在較早的作業系統中，當網域系統管理員設定服務時，服務系統管理員沒有實用的方式可知道哪個前端服務被委派給他們擁有的資源服務。</span><span class="sxs-lookup"><span data-stu-id="86846-117">In earlier operating systems where the domain administrator configured the service, the service administrator had no useful way to know which front-end services delegated to the resource services they owned.</span></span> <span data-ttu-id="86846-118">此外，任何可委派給資源服務的前端服務都會暴露一個潛在的受攻擊點。</span><span class="sxs-lookup"><span data-stu-id="86846-118">And any front-end service that could delegate to a resource service represented a potential attack point.</span></span> <span data-ttu-id="86846-119">若裝載前端服務的伺服器被入侵，而且它是設定為委派給資源服務，則資源服務可能也會被入侵。</span><span class="sxs-lookup"><span data-stu-id="86846-119">If a server that hosted a front-end service was compromised, and it was configured to delegate to resource services, the resource services could also be compromised.</span></span>

> [!NOTE]
> <span data-ttu-id="86846-120">在 Azure AD Domain Services 受管理的網域上，您沒有網域系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="86846-120">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="86846-121">因此，**無法在受管理的網域上設定傳統 KCD**。</span><span class="sxs-lookup"><span data-stu-id="86846-121">Therefore, **traditional KCD cannot be configured on a managed domain**.</span></span> <span data-ttu-id="86846-122">使用此文章中所述的資源型 KCD。</span><span class="sxs-lookup"><span data-stu-id="86846-122">Use resource-based KCD as described in this article.</span></span> <span data-ttu-id="86846-123">此機制也比較安全。</span><span class="sxs-lookup"><span data-stu-id="86846-123">This mechanism is also more secure.</span></span>
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="86846-124">資源型 Kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="86846-124">Resource-based kerberos constrained delegation</span></span>
<span data-ttu-id="86846-125">在 Windows Server 2012 R2 與 Windows Server 2012 中，為服務設定限制委派的能力已從網域系統管理員轉移至服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="86846-125">In Windows Server 2012 R2 and Windows Server 2012, the ability to configure constrained delegation for the service has been transferred from the domain administrator to the service administrator.</span></span> <span data-ttu-id="86846-126">使用這種方式，後端服務系統管理員可以允許或拒絕前端服務。</span><span class="sxs-lookup"><span data-stu-id="86846-126">In this way, the back-end service administrator can allow or deny front-end services.</span></span> <span data-ttu-id="86846-127">此模型稱為「資源型 Kerberos 限制委派」。</span><span class="sxs-lookup"><span data-stu-id="86846-127">This model is known as **resource-based kerberos constrained delegation**.</span></span>

<span data-ttu-id="86846-128">資源型 KCD 是使用 PowerShell 所設定的。</span><span class="sxs-lookup"><span data-stu-id="86846-128">Resource-based KCD is configured using PowerShell.</span></span> <span data-ttu-id="86846-129">視模擬的帳戶是電腦帳戶或使用者帳戶/服務帳戶而定，您必須使用 Set-ADComputer 或 Set-ADUser Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="86846-129">You use the Set-ADComputer or Set-ADUser cmdlets, depending on whether the impersonating account is a computer account or a user account/service account.</span></span>

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a><span data-ttu-id="86846-130">為受管理的網域上的電腦帳戶設定資源型 KCD</span><span class="sxs-lookup"><span data-stu-id="86846-130">Configure resource-based KCD for a computer account on a managed domain</span></span>
<span data-ttu-id="86846-131">假設您有在電腦 'contoso100-webapp.contoso100.com' 上執行的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86846-131">Assume you have a web app running on the computer 'contoso100-webapp.contoso100.com'.</span></span> <span data-ttu-id="86846-132">它需要以網域使用者的登入身分存取資源 ('contoso100-api.contoso100.com' 上執行的 Web API)。</span><span class="sxs-lookup"><span data-stu-id="86846-132">It needs to access the resource (a web API running on 'contoso100-api.contoso100.com') in the context of domain users.</span></span> <span data-ttu-id="86846-133">以下是針對此案例設定資源型 KCD 的方式。</span><span class="sxs-lookup"><span data-stu-id="86846-133">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a><span data-ttu-id="86846-134">為受管理的網域上的使用者帳戶設定資源型 KCD</span><span class="sxs-lookup"><span data-stu-id="86846-134">Configure resource-based KCD for a user account on a managed domain</span></span>
<span data-ttu-id="86846-135">假設您有以服務帳戶 'appsvc' 執行的 Web 應用程式，且它需要以網域使用者登入身分存取資源 (以服務帳戶 - 'backendsvc' 執行的 Web API)。</span><span class="sxs-lookup"><span data-stu-id="86846-135">Assume you have a web app running as a service account 'appsvc' and it needs to access the resource (a web API running as a service account - 'backendsvc') in the context of domain users.</span></span> <span data-ttu-id="86846-136">以下是針對此案例設定資源型 KCD 的方式。</span><span class="sxs-lookup"><span data-stu-id="86846-136">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a><span data-ttu-id="86846-137">相關內容</span><span class="sxs-lookup"><span data-stu-id="86846-137">Related Content</span></span>
* [<span data-ttu-id="86846-138">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="86846-138">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="86846-139">Kerberos 限制委派概觀</span><span class="sxs-lookup"><span data-stu-id="86846-139">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
