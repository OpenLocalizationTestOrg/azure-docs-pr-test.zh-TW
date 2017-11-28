---
title: "Privileged Identity Management 訂用帳戶 - Azure| Microsoft Docs"
description: "說明在租用戶中管理及使用 Azure AD Privileged Identity Management 的訂用帳戶和授權需求"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 62d8f80fa1bec3a1b75e316f0b0ee7be8cbefbff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a><span data-ttu-id="35044-103">Azure Active Directory Privileged Identity Management 訂用帳戶需求</span><span class="sxs-lookup"><span data-stu-id="35044-103">Azure Active Directory Privileged Identity Management subscription requirements</span></span>

<span data-ttu-id="35044-104">Azure AD Privileged Identity Management 可在 Azure AD 的 Premium P2 Edition 中使用。</span><span class="sxs-lookup"><span data-stu-id="35044-104">Azure AD Privileged Identity Management is available as part of the Premium P2 edition of Azure AD.</span></span> <span data-ttu-id="35044-105">如需 P2 的其他功能資訊以及其與 Premium P1 的比較詳細資訊，請參閱 [Azure Active Directory 版本](../active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="35044-105">For more information on the other features of P2 and how it compares to Premium P1, see [Azure Active Directory editions](../active-directory-editions.md).</span></span>

>[!NOTE]
<span data-ttu-id="35044-106">Azure Active Directory (Azure AD) Privileged Identity Management 處於預覽狀態時，不會對嘗試服務的租用戶進行任何授權檢查。</span><span class="sxs-lookup"><span data-stu-id="35044-106">When Azure Active Directory (Azure AD) Privileged Identity Management was in preview, there were no license checks for a tenant to try the service.</span></span>  <span data-ttu-id="35044-107">現在，Azure AD Privileged Identity Management 已公開上市，必須存在試用或付費訂用帳戶，租用戶才能在 2016 年 12 月之後繼續使用 Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="35044-107">Now that Azure AD Privileged Identity Management has reached general availability, a trial or paid subscription must be present for the tenant to continue using Privileged Identity Management after December 2016.</span></span>
  

## <a name="confirm-your-trial-or-paid-subscription"></a><span data-ttu-id="35044-108">確認試用或付費訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="35044-108">Confirm your trial or paid subscription</span></span>

<span data-ttu-id="35044-109">如果您不確定您的組織是否有試用或購買的訂用帳戶時，您可以使用適用於 Windows PowerShell V1 的 Azure Active Directory 模組中包含的命令，檢查您的租用戶中是否有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="35044-109">If you're not sure whether your organization has a trial or purchased subscription, then you can check whether there is a subscription in your tenant by using the commands included in Azure Active Directory Module for Windows PowerShell V1.</span></span> 
1. <span data-ttu-id="35044-110">開啟 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="35044-110">Open a PowerShell window.</span></span>
2. <span data-ttu-id="35044-111">輸入 `Connect-MsolService` 以在您的租用戶中以使用者身分進行驗證。</span><span class="sxs-lookup"><span data-stu-id="35044-111">Enter `Connect-MsolService` to authenticate as a user in your tenant.</span></span>
3. <span data-ttu-id="35044-112">輸入 `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`。</span><span class="sxs-lookup"><span data-stu-id="35044-112">Enter `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.</span></span>

<span data-ttu-id="35044-113">此命令會擷取您租用戶中的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="35044-113">This command retrieves a list of the subscriptions in your tenant.</span></span> <span data-ttu-id="35044-114">如果未傳回任何資料行，您必須取得 Azure AD Premium P2 試用版、購買 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶，才能使用 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="35044-114">If there are no lines returned, you will need to obtain an Azure AD Premium P2 trial, purchase an Azure AD Premium P2 subscription or EMS E5 subscription to use Azure AD Privileged Identity Management.</span></span>  <span data-ttu-id="35044-115">若要取得試用版並開始使用 Azure AD Privileged Identity Management，請參閱[開始使用 Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="35044-115">To get a trial and start using Azure AD Privileged Identity Management, read [Get started with Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).</span></span>

<span data-ttu-id="35044-116">如果此命令傳回一個資料行，其中的 SkuPartNumber 為 "AAD_PREMIUM_P2" 或 "EMSPREMIUM" 且 IsTrial 為 "True"，這表示 Azure AD Premium P2 試用版已存在於租用戶。</span><span class="sxs-lookup"><span data-stu-id="35044-116">If this command returns a line in which SkuPartNumber is "AAD_PREMIUM_P2" or "EMSPREMIUM" and IsTrial is "True", this indicates an Azure AD Premium P2 trial is present in the tenant.</span></span>  <span data-ttu-id="35044-117">如果訂用帳戶狀態為未啟用，而且您未購買 Azure AD Premium P2 或 EMS E5 訂用帳戶，則您必須購買 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶，才能繼續使用 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="35044-117">If the subscription status is not enabled, and you do not have an Azure AD Premium P2 or EMS E5 subscription purchase, then you must purchase an Azure AD Premium P2 subscription or EMS E5 subscription to continue using Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="35044-118">您可以透過 [Microsoft Enterprise 合約](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx)、[Open Volume 授權方案](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)與[雲端解決方案提供者方案](https://partner.microsoft.com/en-US/cloud-solution-provider)取得 Azure AD Premium P2。</span><span class="sxs-lookup"><span data-stu-id="35044-118">Azure AD Premium P2 is available through a [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), the [Open Volume License Program](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), and the [Cloud Solution Providers program](https://partner.microsoft.com/en-US/cloud-solution-provider).</span></span> <span data-ttu-id="35044-119">Azure 和 Office 365 訂閱者也可以線上購買 Azure AD Premium P2。</span><span class="sxs-lookup"><span data-stu-id="35044-119">Azure and Office 365 subscribers can also buy Azure AD Premium P2 online.</span></span>  <span data-ttu-id="35044-120">如需關於 Azure AD Premium 價格或線上訂購方式的詳細資訊，請瀏覽 [Azure Active Directory 價格](https://azure.microsoft.com/en-us/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="35044-120">More information on Azure AD Premium pricing and how to order online can be found at [Azure Active Directory Pricing](https://azure.microsoft.com/en-us/pricing/details/active-directory/).</span></span>

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a><span data-ttu-id="35044-121">Azure AD Privileged Identity Management 不適用於租用戶</span><span class="sxs-lookup"><span data-stu-id="35044-121">Azure AD Privileged Identity Management is not available in tenant</span></span>

<span data-ttu-id="35044-122">在下列情況下，Azure AD Privileged Identity Management 無法再適用於租用戶︰</span><span class="sxs-lookup"><span data-stu-id="35044-122">Azure AD Privileged Identity Management will no longer be available in your tenant if:</span></span>
- <span data-ttu-id="35044-123">您的組織使用預覽狀態的 Azure AD Privileged Identity Management，且未購買 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="35044-123">Your organization was using Azure AD Privileged Identity Management when it was in preview and does not purchase Azure AD Premium P2 subscription or EMS E5 subscription.</span></span>
- <span data-ttu-id="35044-124">您的組織擁有的 Azure AD Premium P2 或 EMS E5 試用版已過期。</span><span class="sxs-lookup"><span data-stu-id="35044-124">Your organization had an Azure AD Premium P2 or EMS E5 trial that expired.</span></span>
- <span data-ttu-id="35044-125">您的組織購買的訂用帳戶已過期。</span><span class="sxs-lookup"><span data-stu-id="35044-125">Your organization had a purchased subscription that expired.</span></span>

<span data-ttu-id="35044-126">當 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶過期，或使用預覽狀態 Azure AD Privileged Identity Management 的組織未取得 Azure AD Premium P2 或 EMS E5 訂用帳戶時：</span><span class="sxs-lookup"><span data-stu-id="35044-126">When an Azure AD Premium P2 subscription or EMS E5 subscription expires, or an organization that was using Azure AD Privileged Identity Management in preview does not obtain Azure AD Premium P2 or EMS E5 subscription:</span></span>

- <span data-ttu-id="35044-127">Azure AD 角色的永久角色指派不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="35044-127">Permanent role assignments to Azure AD roles will be unaffected.</span></span>
- <span data-ttu-id="35044-128">使用者無法再利用 Azure 入口網站中的 Azure AD Privileged Identity Management 擴充以及 Azure AD Privileged Identity Management 的 Graph API Cmdlet 和 PowerShell 介面，來啟動特殊權限的角色、管理特殊權限的存取權，或執行特殊權限角色的存取檢閱。</span><span class="sxs-lookup"><span data-stu-id="35044-128">The Azure AD Privileged Identity Management extension in the Azure portal, as well as the Graph API cmdlets and PowerShell interfaces of Azure AD Privileged Identity Management, will no longer be available for users to activate privileged roles, manage privileged access, or perform access reviews of privileged roles.</span></span>
- <span data-ttu-id="35044-129">Azure AD 角色的合格角色指派將會遭到移除，因為使用者將無法再啟動特殊權限的角色。</span><span class="sxs-lookup"><span data-stu-id="35044-129">Eligible role assignments of Azure AD roles will be removed, as users will no longer be able to activate privileged roles.</span></span>
- <span data-ttu-id="35044-130">Azure AD 角色的任何進行中存取檢閱將會結束，而且 Azure AD Privileged Identity Management 組態設定將會遭到移除。</span><span class="sxs-lookup"><span data-stu-id="35044-130">Any ongoing access reviews of Azure AD roles will end, and Azure AD Privileged Identity Management configuration settings will be removed.</span></span>
- <span data-ttu-id="35044-131">Azure AD Privileged Identity Management 將不再傳送有關角色指派變更的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="35044-131">Azure AD Privileged Identity Management will no longer send emails on role assignment changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35044-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35044-132">Next steps</span></span>

- [<span data-ttu-id="35044-133">開始使用 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="35044-133">Get started with Azure AD Privileged Identity Management</span></span>](../active-directory-privileged-identity-management-getting-started.md)
- [<span data-ttu-id="35044-134">Azure AD Privileged Identity Management 中的角色</span><span class="sxs-lookup"><span data-stu-id="35044-134">Roles in Azure AD Privileged Identity Management</span></span>](../active-directory-privileged-identity-management-roles.md)
