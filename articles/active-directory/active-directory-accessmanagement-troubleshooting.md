---
title: "aaaTroubleshooting 群組動態成員資格 |Microsoft 文件"
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="99195-103">疑難排解群組的動態成員資格</span><span class="sxs-lookup"><span data-stu-id="99195-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="99195-104">**我在群組上設定的規則，但沒有成員資格取得更新 hello 群組中**</span><span class="sxs-lookup"><span data-stu-id="99195-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="99195-105">請確認該 hello**啟用委派群組管理**設定為太**是**在 hello**設定** 索引標籤。只有當您登入 Azure Active Directory Premium 授權的使用者 toowhom 是指派，您會看到這項設定。</span><span class="sxs-lookup"><span data-stu-id="99195-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="99195-106">請確認 hello hello 規則上的使用者屬性的值： 是否有符合 hello 規則的使用者？</span><span class="sxs-lookup"><span data-stu-id="99195-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="99195-107">**我設定了規則，但現在會移除 hello 的 hello 規則的現有成員**</span><span class="sxs-lookup"><span data-stu-id="99195-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="99195-108">這是預期行為。</span><span class="sxs-lookup"><span data-stu-id="99195-108">This is expected behavior.</span></span> <span data-ttu-id="99195-109">啟用或變更規則時，會移除 hello 群組的現有成員。</span><span class="sxs-lookup"><span data-stu-id="99195-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="99195-110">傳回從 hello 規則的評估 hello 使用者會新增為成員 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="99195-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="99195-111">**當我新增或變更規則時，沒有立即看到成員資格變更，為什麼？**</span><span class="sxs-lookup"><span data-stu-id="99195-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="99195-112">專用的成員資格評估會定期在非同步的背景處理序中完成。</span><span class="sxs-lookup"><span data-stu-id="99195-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="99195-113">Hello 程序會接受時間長度取決於 hello 中您目錄和 hello 大小 hello 群組建立 hello 規則結果的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="99195-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="99195-114">通常，目錄與小量的使用者會看到 hello 群組成員資格變更小於幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="99195-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="99195-115">目錄具有大量的使用者可能需要 30 分鐘或更長的 toopopulate。</span><span class="sxs-lookup"><span data-stu-id="99195-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="99195-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99195-116">Next steps</span></span>
<span data-ttu-id="99195-117">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="99195-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="99195-118">使用 Azure Active Directory 群組來管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="99195-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="99195-119">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="99195-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="99195-120">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="99195-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="99195-121">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99195-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
