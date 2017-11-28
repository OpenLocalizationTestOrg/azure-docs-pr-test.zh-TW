---
title: "aaaAdd B2B 共同作業的使用者 tooAzure Active Directory 沒有邀請函 |Microsoft 文件"
description: "您可以讓不含兌換邀請中 Azure Active Directory B2B 共同作業新增其他 Azure AD 的來賓使用者 tooyour guest 使用者。"
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="38e50-103">在沒有邀請的情況下新增 B2B 共同作業來賓使用者</span><span class="sxs-lookup"><span data-stu-id="38e50-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="38e50-104">您可以允許使用者，例如 hello 夥伴 tooyour 組織，而不需要兌換邀請 toobe 夥伴代表 tooadd 使用者。</span><span class="sxs-lookup"><span data-stu-id="38e50-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="38e50-105">您必須執行的是您所使用的 hello 夥伴組織的 hello 目錄中的列舉權限授與該使用者</span><span class="sxs-lookup"><span data-stu-id="38e50-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="38e50-106">授與這些權限的時機︰</span><span class="sxs-lookup"><span data-stu-id="38e50-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="38e50-107">Hello 主機組織 (例如，WoodGrove) 中的使用者邀請 hello 夥伴組織中的一位使用者 (例如， Sam@litware.com) 為來賓。</span><span class="sxs-lookup"><span data-stu-id="38e50-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="38e50-108">hello hello 主機組織中的系統管理員設定原則，允許 Sam tooidentify 和從 hello 夥伴組織 (Litware) 新增其他使用者。</span><span class="sxs-lookup"><span data-stu-id="38e50-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="38e50-109">現在 Sam 可以加入其他使用者從 Litware toohello WoodGrove 目錄、 群組或應用程式而不需要兌換邀請 toobe。</span><span class="sxs-lookup"><span data-stu-id="38e50-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="38e50-110">如果 Sam Litware 在 hello 適當列舉權限，它會自動發生。</span><span class="sxs-lookup"><span data-stu-id="38e50-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="38e50-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38e50-111">Next steps</span></span>

<span data-ttu-id="38e50-112">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="38e50-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="38e50-113">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="38e50-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="38e50-114">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="38e50-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="38e50-115">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="38e50-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="38e50-116">hello hello B2B 共同作業邀請電子郵件項目</span><span class="sxs-lookup"><span data-stu-id="38e50-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="38e50-117">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="38e50-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="38e50-118">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="38e50-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="38e50-119">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="38e50-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="38e50-120">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="38e50-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="38e50-121">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="38e50-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="38e50-122">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="38e50-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="38e50-123">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="38e50-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)