---
title: "疑難排解群組的動態成員資格 | Microsoft Docs"
description: "Azure AD 中群組動態成員資格的疑難排解秘訣。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="4df9f-103">疑難排解群組的動態成員資格</span><span class="sxs-lookup"><span data-stu-id="4df9f-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="4df9f-104">**我針對某個群組設定了一個規則，但是群組中的成員資格沒有任何更新**</span><span class="sxs-lookup"><span data-stu-id="4df9f-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="4df9f-105">請確認 [設定] 索引標籤中的 [啟用委派的群組管理] 設定是設為 [是]。</span><span class="sxs-lookup"><span data-stu-id="4df9f-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="4df9f-106">只有當您以 Azure Active Directory Premium 授權指派對象的使用者身分登入時，才看得到這項設定。</span><span class="sxs-lookup"><span data-stu-id="4df9f-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="4df9f-107">請針對規則確認使用者屬性的值：是否有符合規則的使用者？</span><span class="sxs-lookup"><span data-stu-id="4df9f-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="4df9f-108">**我已設定一個規則，但是目前現有的規則成員已被移除**</span><span class="sxs-lookup"><span data-stu-id="4df9f-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="4df9f-109">這是預期行為。</span><span class="sxs-lookup"><span data-stu-id="4df9f-109">This is expected behavior.</span></span> <span data-ttu-id="4df9f-110">因為在啟用或變更規則時，現有群組的成員會遭到移除。</span><span class="sxs-lookup"><span data-stu-id="4df9f-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="4df9f-111">從評估規則所傳回的使用者會當作成員，新增至群組。</span><span class="sxs-lookup"><span data-stu-id="4df9f-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="4df9f-112">**當我新增或變更規則時，沒有立即看到成員資格變更，為什麼？**</span><span class="sxs-lookup"><span data-stu-id="4df9f-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="4df9f-113">專用的成員資格評估會定期在非同步的背景處理序中完成。</span><span class="sxs-lookup"><span data-stu-id="4df9f-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="4df9f-114">該程序所需的時間，取決於您目錄中的使用者數目以及因規則所建立的群組大小。</span><span class="sxs-lookup"><span data-stu-id="4df9f-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="4df9f-115">具有少量使用者的目錄通常會在很短的時間內看到群組成員資格變更。</span><span class="sxs-lookup"><span data-stu-id="4df9f-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="4df9f-116">具有大量使用者的目錄則可能需要 30 分鐘或更長的時間填入。</span><span class="sxs-lookup"><span data-stu-id="4df9f-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4df9f-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4df9f-117">Next steps</span></span>
<span data-ttu-id="4df9f-118">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="4df9f-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4df9f-119">使用 Azure Active Directory 群組管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="4df9f-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="4df9f-120">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="4df9f-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="4df9f-121">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="4df9f-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="4df9f-122">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4df9f-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
