---
title: "aaaOffice 365 外部共用和 Azure Active Directory B2B 共同作業 |Microsoft 文件"
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
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="73c87-103">Office 365 外部共用與 Azure Active Directory B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="73c87-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="73c87-104">在 Office 365 （OneDrive，SharePoint Online、 統一群組等） 和 Azure Active Directory (Azure AD) B2B 共同作業技術上來說是共用的外部 hello 相同的動作。</span><span class="sxs-lookup"><span data-stu-id="73c87-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="73c87-105">所有外部共用 （除了 OneDrive/SharePoint Online)，包括客體中的 Office 365 群組，已使用共用的 hello Azure AD B2B 共同作業邀請應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="73c87-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="73c87-106">OneDrive/SharePoint Online 有個別的邀請管理員。</span><span class="sxs-lookup"><span data-stu-id="73c87-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="73c87-107">OneDrive/SharePoint Online 中的外部共用支援會在 Azure AD 開發其支援之前開始。</span><span class="sxs-lookup"><span data-stu-id="73c87-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="73c87-108">經過一段時間，OneDrive/SharePoint Online 的外部共用具有累加的數種功能，並使用 hello 產品的使用者數以百萬計的內建共用模式。</span><span class="sxs-lookup"><span data-stu-id="73c87-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="73c87-109">不過，OneDrive/SharePoint Online 外部共用的運作方式與 Azure AD B2B 共同作業的運作方式有些微差異：</span><span class="sxs-lookup"><span data-stu-id="73c87-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="73c87-110">之後使用者擁有兌換邀請其 OneDrive/SharePoint Online 將使用者 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="73c87-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="73c87-111">因此前兌換，, 您沒有看到 Azure AD 入口網站中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="73c87-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="73c87-112">如果另一個站台同時邀請 hello 中的使用者，就會產生新的邀請。</span><span class="sxs-lookup"><span data-stu-id="73c87-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="73c87-113">不過，當您使用 Azure AD B2B 共同作業時，使用者會立即新增於邀請上，因而顯示在每個地方。</span><span class="sxs-lookup"><span data-stu-id="73c87-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="73c87-114">在 OneDrive/SharePoint Online 中的 hello 兌換體驗看起來 hello Azure AD B2B 共同作業經驗與不同的。</span><span class="sxs-lookup"><span data-stu-id="73c87-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="73c87-115">使用者贖回邀請之後，hello 體驗看起來一樣。</span><span class="sxs-lookup"><span data-stu-id="73c87-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="73c87-116">您可以從 OneDrive/SharePoint Online 共用對話方塊挑選 Azure AD B2B 共同作業邀請的使用者。</span><span class="sxs-lookup"><span data-stu-id="73c87-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="73c87-117">在 OneDrive/SharePoint 邀請的使用者兌換其邀請之後，也會出現在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="73c87-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="73c87-118">外部 toomanage 中 OneDrive/SharePoint Online 與 Azure AD B2B 共同作業的共用設定 hello OneDrive/SharePoint Online 外部共用設定太**只允許與外部使用者已經共用 hello 目錄中**。</span><span class="sxs-lookup"><span data-stu-id="73c87-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="73c87-119">使用者可以前往 tooexternally 共用站台，並且加入從外部共同作業者 hello 系統管理員挑選。</span><span class="sxs-lookup"><span data-stu-id="73c87-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="73c87-120">hello 系統管理員可以新增 hello 透過 hello B2B 共同作業邀請應用程式開發介面的外部共同作業者。</span><span class="sxs-lookup"><span data-stu-id="73c87-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![hello OneDrive/SharePoint Online 外部共用設定](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="73c87-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73c87-122">Next steps</span></span>

<span data-ttu-id="73c87-123">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="73c87-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="73c87-124">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="73c87-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="73c87-125">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="73c87-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="73c87-126">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="73c87-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="73c87-127">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="73c87-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="73c87-128">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="73c87-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="73c87-129">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="73c87-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="73c87-130">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="73c87-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="73c87-131">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="73c87-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="73c87-132">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="73c87-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="73c87-133">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="73c87-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
