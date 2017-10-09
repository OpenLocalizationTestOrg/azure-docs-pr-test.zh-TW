---
title: "aaaPrivileged 身分識別管理訂閱]-[Azure |Microsoft 文件"
description: "說明 hello 訂用帳戶和授權管理和租用戶中使用 Azure AD Privileged Identity Management 的需求"
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
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a><span data-ttu-id="71766-103">Azure Active Directory Privileged Identity Management 訂用帳戶需求</span><span class="sxs-lookup"><span data-stu-id="71766-103">Azure Active Directory Privileged Identity Management subscription requirements</span></span>

<span data-ttu-id="71766-104">Azure AD Privileged Identity Management 可做為 Azure AD Premium P2 hello 版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="71766-104">Azure AD Privileged Identity Management is available as part of hello Premium P2 edition of Azure AD.</span></span> <span data-ttu-id="71766-105">如需有關 hello P2 和 tooPremium P1 的比較的其他功能，請參閱[Azure Active Directory 版本](../active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="71766-105">For more information on hello other features of P2 and how it compares tooPremium P1, see [Azure Active Directory editions](../active-directory-editions.md).</span></span>

>[!NOTE]
<span data-ttu-id="71766-106">Azure Active Directory (Azure AD) Privileged Identity Management 在預覽中時，沒有任何租用戶 tootry hello 服務的授權檢查。</span><span class="sxs-lookup"><span data-stu-id="71766-106">When Azure Active Directory (Azure AD) Privileged Identity Management was in preview, there were no license checks for a tenant tootry hello service.</span></span>  <span data-ttu-id="71766-107">現在，Azure AD Privileged Identity Management 到達的正式運作時，必須存在 hello 在 2016 年 12 月之後使用 Privileged Identity Management 的租用戶 toocontinue 才能試用或付費訂閱。</span><span class="sxs-lookup"><span data-stu-id="71766-107">Now that Azure AD Privileged Identity Management has reached general availability, a trial or paid subscription must be present for hello tenant toocontinue using Privileged Identity Management after December 2016.</span></span>
  

## <a name="confirm-your-trial-or-paid-subscription"></a><span data-ttu-id="71766-108">確認試用或付費訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="71766-108">Confirm your trial or paid subscription</span></span>

<span data-ttu-id="71766-109">如果您不確定您的組織是否有試用或購買訂用帳戶，您可以檢查是否有您的租用戶中的訂閱使用包含在 Azure Active Directory 模組的 Windows PowerShell V1 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="71766-109">If you're not sure whether your organization has a trial or purchased subscription, then you can check whether there is a subscription in your tenant by using hello commands included in Azure Active Directory Module for Windows PowerShell V1.</span></span> 
1. <span data-ttu-id="71766-110">開啟 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="71766-110">Open a PowerShell window.</span></span>
2. <span data-ttu-id="71766-111">輸入`Connect-MsolService`tooauthenticate 成為您的租用戶中的使用者。</span><span class="sxs-lookup"><span data-stu-id="71766-111">Enter `Connect-MsolService` tooauthenticate as a user in your tenant.</span></span>
3. <span data-ttu-id="71766-112">輸入 `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`。</span><span class="sxs-lookup"><span data-stu-id="71766-112">Enter `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.</span></span>

<span data-ttu-id="71766-113">此命令會擷取您的租用戶中的 hello 訂閱清單。</span><span class="sxs-lookup"><span data-stu-id="71766-113">This command retrieves a list of hello subscriptions in your tenant.</span></span> <span data-ttu-id="71766-114">如果沒有傳回任何線條，您將需要 Azure AD Premium P2 tooobtain 試用版，購買的 Azure AD Premium P2 訂閱或 EMS E5 訂用帳戶 toouse Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="71766-114">If there are no lines returned, you will need tooobtain an Azure AD Premium P2 trial, purchase an Azure AD Premium P2 subscription or EMS E5 subscription toouse Azure AD Privileged Identity Management.</span></span>  <span data-ttu-id="71766-115">讀取 tooget 試用版和開始使用 Azure AD Privileged Identity Management[開始使用 Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="71766-115">tooget a trial and start using Azure AD Privileged Identity Management, read [Get started with Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).</span></span>

<span data-ttu-id="71766-116">如果此命令會傳回中的資料行的 SkuPartNumber"AAD_PREMIUM_P2"或"EMSPREMIUM 」 和 IsTrial 為"True"，這表示 Azure AD Premium P2 試用版已存在於 hello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="71766-116">If this command returns a line in which SkuPartNumber is "AAD_PREMIUM_P2" or "EMSPREMIUM" and IsTrial is "True", this indicates an Azure AD Premium P2 trial is present in hello tenant.</span></span>  <span data-ttu-id="71766-117">如果未啟用 hello 訂閱狀態，而且您不需要 Azure AD Premium P2 或 EMS E5 訂閱購買，然後您必須購買的 Azure AD Premium P2 訂閱或使用 Azure AD Privileged Identity Management EMS E5 訂用帳戶 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="71766-117">If hello subscription status is not enabled, and you do not have an Azure AD Premium P2 or EMS E5 subscription purchase, then you must purchase an Azure AD Premium P2 subscription or EMS E5 subscription toocontinue using Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="71766-118">Azure AD Premium P2 是可透過[Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx)，hello[開啟的大量授權方案](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)，和 hello[雲端方案提供者程式](https://partner.microsoft.com/en-US/cloud-solution-provider)。</span><span class="sxs-lookup"><span data-stu-id="71766-118">Azure AD Premium P2 is available through a [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [Open Volume License Program](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), and hello [Cloud Solution Providers program](https://partner.microsoft.com/en-US/cloud-solution-provider).</span></span> <span data-ttu-id="71766-119">Azure 和 Office 365 訂閱者也可以線上購買 Azure AD Premium P2。</span><span class="sxs-lookup"><span data-stu-id="71766-119">Azure and Office 365 subscribers can also buy Azure AD Premium P2 online.</span></span>  <span data-ttu-id="71766-120">Azure AD Premium 價格和 tooorder 線上方式可以在找到更多資訊[Azure Active Directory 定價](https://azure.microsoft.com/en-us/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="71766-120">More information on Azure AD Premium pricing and how tooorder online can be found at [Azure Active Directory Pricing](https://azure.microsoft.com/en-us/pricing/details/active-directory/).</span></span>

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a><span data-ttu-id="71766-121">Azure AD Privileged Identity Management 不適用於租用戶</span><span class="sxs-lookup"><span data-stu-id="71766-121">Azure AD Privileged Identity Management is not available in tenant</span></span>

<span data-ttu-id="71766-122">在下列情況下，Azure AD Privileged Identity Management 無法再適用於租用戶︰</span><span class="sxs-lookup"><span data-stu-id="71766-122">Azure AD Privileged Identity Management will no longer be available in your tenant if:</span></span>
- <span data-ttu-id="71766-123">您的組織使用預覽狀態的 Azure AD Privileged Identity Management，且未購買 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="71766-123">Your organization was using Azure AD Privileged Identity Management when it was in preview and does not purchase Azure AD Premium P2 subscription or EMS E5 subscription.</span></span>
- <span data-ttu-id="71766-124">您的組織擁有的 Azure AD Premium P2 或 EMS E5 試用版已過期。</span><span class="sxs-lookup"><span data-stu-id="71766-124">Your organization had an Azure AD Premium P2 or EMS E5 trial that expired.</span></span>
- <span data-ttu-id="71766-125">您的組織購買的訂用帳戶已過期。</span><span class="sxs-lookup"><span data-stu-id="71766-125">Your organization had a purchased subscription that expired.</span></span>

<span data-ttu-id="71766-126">當 Azure AD Premium P2 訂用帳戶或 EMS E5 訂用帳戶過期，或使用預覽狀態 Azure AD Privileged Identity Management 的組織未取得 Azure AD Premium P2 或 EMS E5 訂用帳戶時：</span><span class="sxs-lookup"><span data-stu-id="71766-126">When an Azure AD Premium P2 subscription or EMS E5 subscription expires, or an organization that was using Azure AD Privileged Identity Management in preview does not obtain Azure AD Premium P2 or EMS E5 subscription:</span></span>

- <span data-ttu-id="71766-127">永久性的角色指派 tooAzure AD 角色不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="71766-127">Permanent role assignments tooAzure AD roles will be unaffected.</span></span>
- <span data-ttu-id="71766-128">hello hello Azure 入口網站中的 Azure AD Privileged Identity Management 延伸模組，以及 hello Graph API cmdlet 和 PowerShell 的 Azure AD Privileged Identity Management 的介面將不再可供使用者 tooactivate 特殊權限角色管理特殊權限存取，或執行存取檢查的權限的角色。</span><span class="sxs-lookup"><span data-stu-id="71766-128">hello Azure AD Privileged Identity Management extension in hello Azure portal, as well as hello Graph API cmdlets and PowerShell interfaces of Azure AD Privileged Identity Management, will no longer be available for users tooactivate privileged roles, manage privileged access, or perform access reviews of privileged roles.</span></span>
- <span data-ttu-id="71766-129">符合資格的角色指派的 Azure AD 角色將會移除，因為使用者將不再能夠 tooactivate 特殊權限角色。</span><span class="sxs-lookup"><span data-stu-id="71766-129">Eligible role assignments of Azure AD roles will be removed, as users will no longer be able tooactivate privileged roles.</span></span>
- <span data-ttu-id="71766-130">Azure AD 角色的任何進行中存取檢閱將會結束，而且 Azure AD Privileged Identity Management 組態設定將會遭到移除。</span><span class="sxs-lookup"><span data-stu-id="71766-130">Any ongoing access reviews of Azure AD roles will end, and Azure AD Privileged Identity Management configuration settings will be removed.</span></span>
- <span data-ttu-id="71766-131">Azure AD Privileged Identity Management 將不再傳送有關角色指派變更的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="71766-131">Azure AD Privileged Identity Management will no longer send emails on role assignment changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71766-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71766-132">Next steps</span></span>

- [<span data-ttu-id="71766-133">開始使用 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="71766-133">Get started with Azure AD Privileged Identity Management</span></span>](../active-directory-privileged-identity-management-getting-started.md)
- [<span data-ttu-id="71766-134">Azure AD Privileged Identity Management 中的角色</span><span class="sxs-lookup"><span data-stu-id="71766-134">Roles in Azure AD Privileged Identity Management</span></span>](../active-directory-privileged-identity-management-roles.md)
