---
title: "Office 365 外部共用語 Azure Active Directory B2B 共同作業 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業的宣告對應參考資料"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="4c1a6-103">Office 365 外部共用與 Azure Active Directory B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="4c1a6-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="4c1a6-104">Office 365 (OneDrive、SharePoint Online、整合群組等) 中的外部共用與 Azure Active Directory (Azure AD) B2B 共同作業在技術上而言是相同的。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="4c1a6-105">所有外部共用 (OneDrive/SharePoint Online 除外)，包括 Office 365 群組中的來賓都已使用 Azure AD B2B 共同作業邀請 API 來進行共用。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="4c1a6-106">OneDrive/SharePoint Online 有個別的邀請管理員。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="4c1a6-107">OneDrive/SharePoint Online 中的外部共用支援會在 Azure AD 開發其支援之前開始。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="4c1a6-108">隨著時間的經過，OneDrive/SharePoint Online 外部共用已發展出數個功能，而且已有數百萬個使用者使用該產品的內建共用模式。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="4c1a6-109">不過，OneDrive/SharePoint Online 外部共用的運作方式與 Azure AD B2B 共同作業的運作方式有些微差異：</span><span class="sxs-lookup"><span data-stu-id="4c1a6-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="4c1a6-110">OneDrive/SharePoint Online 會在使用者兌換其邀請之後，將使用者新增至目錄。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="4c1a6-111">因此在兌換前，您不會在 Azure AD 入口網站中看到使用者。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="4c1a6-112">如果其他網站同時邀請使用者，則會產生新的邀請。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="4c1a6-113">不過，當您使用 Azure AD B2B 共同作業時，使用者會立即新增於邀請上，因而顯示在每個地方。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="4c1a6-114">OneDrive/SharePoint Online 中的兌換體驗與 Azure AD B2B 共同作業中的體驗有所差異。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="4c1a6-115">在使用者兌換邀請之後，體驗看起來很類似。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="4c1a6-116">您可以從 OneDrive/SharePoint Online 共用對話方塊挑選 Azure AD B2B 共同作業邀請的使用者。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="4c1a6-117">在 OneDrive/SharePoint 邀請的使用者兌換其邀請之後，也會出現在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="4c1a6-118">若要使用 Azure AD B2B 共同作業來管理 OneDrive/SharePoint Online 中的外部共用，請將 OneDrive/SharePoint Online 外部共用設定設為 [只允許與已位於目錄中的外部使用者共用]。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="4c1a6-119">使用者可以移至外部共用網站，並從系統管理員新增的外部共同作業者之間選擇。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="4c1a6-120">系統管理員可以透過 B2B 共同作業邀請 API 來新增外部共同作業者。</span><span class="sxs-lookup"><span data-stu-id="4c1a6-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![OneDrive/SharePoint Online 外部共用設定](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="4c1a6-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c1a6-122">Next steps</span></span>

<span data-ttu-id="4c1a6-123">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="4c1a6-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4c1a6-124">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="4c1a6-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4c1a6-125">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="4c1a6-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4c1a6-126">將 B2B 共同作業使用者新增至角色</span><span class="sxs-lookup"><span data-stu-id="4c1a6-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="4c1a6-127">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="4c1a6-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4c1a6-128">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="4c1a6-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4c1a6-129">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="4c1a6-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4c1a6-130">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="4c1a6-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="4c1a6-131">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="4c1a6-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4c1a6-132">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="4c1a6-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="4c1a6-133">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="4c1a6-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
