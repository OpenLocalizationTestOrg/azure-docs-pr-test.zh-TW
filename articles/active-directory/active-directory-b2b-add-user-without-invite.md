---
title: "無邀請將 B2B 共同作業使用者新增至 Azure Active Directory | Microsoft Docs"
description: "您可以讓來賓使用者將其他來賓使用者加入您的 Azure AD，而不需在 Azure Active Directory B2B 共同作業中兌換邀請。"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="2ce55-103">在沒有邀請的情況下新增 B2B 共同作業來賓使用者</span><span class="sxs-lookup"><span data-stu-id="2ce55-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="2ce55-104">您可以允許使用者 (例如合作夥伴代表) 將來自合作夥伴的使用者加入您的組織，而不需要兌換邀請。</span><span class="sxs-lookup"><span data-stu-id="2ce55-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="2ce55-105">您必須做的是將合作夥伴組織在目錄中的列舉權限授與該使用者。</span><span class="sxs-lookup"><span data-stu-id="2ce55-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="2ce55-106">授與這些權限的時機︰</span><span class="sxs-lookup"><span data-stu-id="2ce55-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="2ce55-107">主組織 (例如，WoodGrove) 中的使用者邀請合作夥伴組織 (例如，Sam@litware.com) 的使用者做為「來賓」。</span><span class="sxs-lookup"><span data-stu-id="2ce55-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="2ce55-108">主組織中的系統管理員設定原則以允許 Sam 識別及新增來自合作夥伴組織 (Litware) 的使用者。</span><span class="sxs-lookup"><span data-stu-id="2ce55-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="2ce55-109">現在 Sam 可以將來自 Litware 的其他使用者新增到 WoodGrove 目錄、群組或應用程式，而不需要兌換邀請。</span><span class="sxs-lookup"><span data-stu-id="2ce55-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="2ce55-110">若 Sam 具有 Litware 中的適當列舉權限，這會自動發生。</span><span class="sxs-lookup"><span data-stu-id="2ce55-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="2ce55-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ce55-111">Next steps</span></span>

<span data-ttu-id="2ce55-112">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="2ce55-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="2ce55-113">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="2ce55-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2ce55-114">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="2ce55-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="2ce55-115">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="2ce55-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="2ce55-116">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="2ce55-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="2ce55-117">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="2ce55-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="2ce55-118">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="2ce55-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="2ce55-119">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2ce55-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="2ce55-120">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="2ce55-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="2ce55-121">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="2ce55-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="2ce55-122">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="2ce55-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="2ce55-123">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="2ce55-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)