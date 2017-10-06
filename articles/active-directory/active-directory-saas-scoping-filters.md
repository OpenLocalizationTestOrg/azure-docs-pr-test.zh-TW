---
title: "使用範圍設定篩選 aaaProvisioning 應用程式 |Microsoft 文件"
description: "了解如何 toouse 範圍設定篩選 tooprevent 支援自動的使用者佈建實際佈建如果物件不符合您的業務需求的應用程式中的物件。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="c4711-103">含範圍篩選器的屬性型應用程式佈建</span><span class="sxs-lookup"><span data-stu-id="c4711-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="c4711-104">本節 hello 目標是的 tooexplain 如何 toouse 範圍設定篩選 toodefine 屬性為基礎的規則，以決定哪些使用者佈建 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4711-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="c4711-105">子句和範圍群組</span><span class="sxs-lookup"><span data-stu-id="c4711-105">Clauses and Scope Groups</span></span>
![範圍篩選器][1] 

<span data-ttu-id="c4711-107">範圍篩選器由一或多個**範圍群組**所定義，其中每個範圍群組都包含一或多個**子句**。</span><span class="sxs-lookup"><span data-stu-id="c4711-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="c4711-108">toosee hello 子句為特定範圍群組，請展開它，依序按一下 hello 箭號 toohello 左邊的 hello 群組名稱。</span><span class="sxs-lookup"><span data-stu-id="c4711-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="c4711-109">A**子句**決定哪些使用者可以 toopass 透過 hello 範圍設定篩選，藉由評估每個使用者的屬性。</span><span class="sxs-lookup"><span data-stu-id="c4711-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="c4711-110">比方說，您可能必須一個子句要求使用者的 'state' 屬性等於紐約，因此只有紐約使用者所佈建到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4711-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![範圍群組名稱][2] 

<span data-ttu-id="c4711-112">每個**範圍群組**一開始就有一個強制**子句**hello 上方螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="c4711-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="c4711-113">這個子句只是指出該 hello 使用者之前，必須先指派 toohello 應用程式範圍篩選器評估。</span><span class="sxs-lookup"><span data-stu-id="c4711-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="c4711-114">您無法刪除或修改這個子句。</span><span class="sxs-lookup"><span data-stu-id="c4711-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="c4711-115">您可以按下 hello 適當按鈕，來加入新子句或新的範圍群組。</span><span class="sxs-lookup"><span data-stu-id="c4711-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="c4711-116">您可以編輯範圍群組的 [範圍群組名稱]  屬性，以便為每個範圍群組提供一個名稱。</span><span class="sxs-lookup"><span data-stu-id="c4711-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="c4711-117">範圍篩選器的評估方式</span><span class="sxs-lookup"><span data-stu-id="c4711-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="c4711-118">在佈建，我們測試範圍的篩選器 toodetermine 針對每個指派的使用者，如果該使用者需要存取 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4711-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="c4711-119">您可以將每個子句視為必須傳入 hello 使用者 tooavoid 被篩除的順序的測試。</span><span class="sxs-lookup"><span data-stu-id="c4711-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="c4711-120">如果您有多個定義的範圍群組，每位使用者必須通過至少其中一個 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4711-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="c4711-121">在每個範圍群組，不過，hello 使用者必須通過每個子句 toopass 該特定範圍群組。</span><span class="sxs-lookup"><span data-stu-id="c4711-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="c4711-122">換句話說，您可以將範圍群組視為集合在一起，或您可以將 hello 子句視為 AND 集合在一起。</span><span class="sxs-lookup"><span data-stu-id="c4711-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="c4711-123">例如，請考慮 hello 範圍設定篩選的下方：</span><span class="sxs-lookup"><span data-stu-id="c4711-123">For example, consider hello scoping filter below:</span></span>

![範圍群組名稱][3]  

<span data-ttu-id="c4711-125">根據 toothis 範圍設定篩選，使用者必須滿足 hello 下列準則，toobe 佈建：</span><span class="sxs-lookup"><span data-stu-id="c4711-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="c4711-126">它們必須被指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4711-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="c4711-127">它們必須在 hello 工程部門工作</span><span class="sxs-lookup"><span data-stu-id="c4711-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="c4711-128">他們必須在舊金山或加拿大工作。</span><span class="sxs-lookup"><span data-stu-id="c4711-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="c4711-129">相關文章</span><span class="sxs-lookup"><span data-stu-id="c4711-129">Related Articles</span></span>
* [<span data-ttu-id="c4711-130">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="c4711-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c4711-131">自動化使用者佈建和取消佈建 tooSaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="c4711-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="c4711-132">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="c4711-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="c4711-133">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="c4711-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="c4711-134">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="c4711-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="c4711-135">使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組</span><span class="sxs-lookup"><span data-stu-id="c4711-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="c4711-136">如何教學課程清單 tooIntegrate SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="c4711-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
