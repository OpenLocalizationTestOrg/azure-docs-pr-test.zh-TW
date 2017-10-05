---
title: "自訂 Azure AD 屬性對應 | Microsoft Docs"
description: "了解 Azure Active Directory 中 SaaS 應用程式有哪些屬性對應，以及如何修改屬性對應來應付業務需求。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6ca2fdc9c68ea0030d938eeaebd57aafa0e2790f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="50c8e-103">在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應</span><span class="sxs-lookup"><span data-stu-id="50c8e-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="50c8e-104">Microsoft Azure AD 支援使用者佈建到例如 Salesforce、Google Apps 等等的協力廠商 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="50c8e-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="50c8e-105">如果您啟用了協力廠商 SaaS 應用程式的使用者佈建，Azure 管理入口網站會以一種稱為「屬性對應」的組態方式控制其屬性值。</span><span class="sxs-lookup"><span data-stu-id="50c8e-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="50c8e-106">在 Azure AD 使用者物件和每個 SaaS app 的使用者物件之間，有一組預先設定的屬性對應。</span><span class="sxs-lookup"><span data-stu-id="50c8e-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="50c8e-107">有些 app 則管理其他類型的物件，例如群組或連絡人。</span><span class="sxs-lookup"><span data-stu-id="50c8e-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="50c8e-108">您可以根據您的業務需求自訂預設的屬性對應。</span><span class="sxs-lookup"><span data-stu-id="50c8e-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="50c8e-109">這表示您可以變更或刪除現有的屬性對應，或建立新的屬性對應。</span><span class="sxs-lookup"><span data-stu-id="50c8e-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="50c8e-110">在 Azure AD 入口網站中，您可以存取這項功能，方法是在 [企業應用程式] 的 [管理] 區段中，按一下 [佈建] 底下的 [對應] 設定。</span><span class="sxs-lookup"><span data-stu-id="50c8e-110">In the Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in the **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="50c8e-112">按一下 [對應]設定，可開啟相關的 [屬性對應] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="50c8e-112">Clicking a **Mappings** configuration, opens the related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="50c8e-113">SaaS 應用程式需要有幾個屬性對應才能正確運作。</span><span class="sxs-lookup"><span data-stu-id="50c8e-113">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="50c8e-114">若為必要的屬性，[刪除] 功能就無法使用。</span><span class="sxs-lookup"><span data-stu-id="50c8e-114">For required attributes, the **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="50c8e-116">在上述範例中，您可以看到 Salesforce 中受管理的物件的 **Username** 屬性填入了連結 Azure Active Directory 物件的 **userPrincipalName** 值。</span><span class="sxs-lookup"><span data-stu-id="50c8e-116">In the example above, you can see that the **Username** attribute of a managed object in Salesforce is populated with the **userPrincipalName** value of the linked Azure Active Directory Object.</span></span>

<span data-ttu-id="50c8e-117">您可以按一下對應來自訂現有的 [屬性對應]。</span><span class="sxs-lookup"><span data-stu-id="50c8e-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="50c8e-118">這會開啟 [編輯屬性] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="50c8e-118">This opens the **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="50c8e-120">了解屬性對應類型</span><span class="sxs-lookup"><span data-stu-id="50c8e-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="50c8e-121">有了屬性對應，您就可以控制屬性在協力廠商 SaaS 應用程式中填入的方式。</span><span class="sxs-lookup"><span data-stu-id="50c8e-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="50c8e-122">支援四種不同的對應類型：</span><span class="sxs-lookup"><span data-stu-id="50c8e-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="50c8e-123">**直接** - 目標屬性會填入 Azure AD 中連結物件的屬性值。</span><span class="sxs-lookup"><span data-stu-id="50c8e-123">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="50c8e-124">**常數** - 目標屬性會填入您所指定的特定字串。</span><span class="sxs-lookup"><span data-stu-id="50c8e-124">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="50c8e-125">**運算式** - 目標屬性會根據類似指令碼的運算式結果填入。</span><span class="sxs-lookup"><span data-stu-id="50c8e-125">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="50c8e-126">如需詳細資訊，請參閱[在 Azure Active Directory 中撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="50c8e-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="50c8e-127">**無** - 目標屬性保留未修改。</span><span class="sxs-lookup"><span data-stu-id="50c8e-127">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="50c8e-128">不過，如果目標屬性是空的，就會填入您所指定的預設值。</span><span class="sxs-lookup"><span data-stu-id="50c8e-128">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="50c8e-129">除了這四個基本屬性對應類型，自訂屬性對應還支援選擇性的**預設**值指派的概念。</span><span class="sxs-lookup"><span data-stu-id="50c8e-129">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of an optional **default** value assignment.</span></span> <span data-ttu-id="50c8e-130">預設值指派可確保當 Azure AD 中和目標物件都沒有值時，目標屬性會填入某個值。</span><span class="sxs-lookup"><span data-stu-id="50c8e-130">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span> <span data-ttu-id="50c8e-131">最常見的設定是將其保留空白。</span><span class="sxs-lookup"><span data-stu-id="50c8e-131">The most common configuration is to leave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="50c8e-132">了解屬性對應屬性</span><span class="sxs-lookup"><span data-stu-id="50c8e-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="50c8e-133">在前一個區段中，您已經引進了屬性對應類型屬性。</span><span class="sxs-lookup"><span data-stu-id="50c8e-133">In the previous section, you have already been introduced to the attribute mapping type property.</span></span>
<span data-ttu-id="50c8e-134">除了這個屬性之外，屬性對應也會支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="50c8e-134">In addition to this property, attribute mappings do also support the following attributes:</span></span>

- <span data-ttu-id="50c8e-135">**來源屬性** - 來源系統的使用者屬性 (例如：Azure Active Directory)。</span><span class="sxs-lookup"><span data-stu-id="50c8e-135">**Source attribute** - The user attribute from the source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="50c8e-136">**目標屬性** – 目標系統中的使用者屬性 (例如：ServiceNow)。</span><span class="sxs-lookup"><span data-stu-id="50c8e-136">**Target attribute** – The user attribute in the target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="50c8e-137">**使用此屬性比對物件** – 是否應該將此對應用於唯一識別來源與目標系統之間的使用者。</span><span class="sxs-lookup"><span data-stu-id="50c8e-137">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between the source and target systems.</span></span> <span data-ttu-id="50c8e-138">這通常會在 Azure AD 中的 userPrincipalName 或 mail 屬性上加以設定，通常會對應至目標應用程式中的使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="50c8e-138">This is typically set on the userPrincipalName or mail attribute in Azure AD, which is typically mapped to a username field in a target application.</span></span>
- <span data-ttu-id="50c8e-139">**比對優先順序** – 您可以設定多個比對屬性。</span><span class="sxs-lookup"><span data-stu-id="50c8e-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="50c8e-140">具有多個屬性時，系統會以此欄位定義的順序進行評估。</span><span class="sxs-lookup"><span data-stu-id="50c8e-140">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="50c8e-141">只要找到相符項目，便不會評估進一步比對屬性。</span><span class="sxs-lookup"><span data-stu-id="50c8e-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="50c8e-142">**套用此對應**</span><span class="sxs-lookup"><span data-stu-id="50c8e-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="50c8e-143">**一律** – 將此對應套用於使用者建立和更新動作</span><span class="sxs-lookup"><span data-stu-id="50c8e-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="50c8e-144">**僅限建立期間** - 僅將此對應套用於使用者建立動作</span><span class="sxs-lookup"><span data-stu-id="50c8e-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="50c8e-145">您應該知道的事情</span><span class="sxs-lookup"><span data-stu-id="50c8e-145">What you should know</span></span>

<span data-ttu-id="50c8e-146">Microsoft Azure AD 提供有效率的同步處理程序實作。</span><span class="sxs-lookup"><span data-stu-id="50c8e-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="50c8e-147">在初始化環境中，同步處理期間只會處理需要更新的物件。</span><span class="sxs-lookup"><span data-stu-id="50c8e-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="50c8e-148">更新屬性對應會影響同步處理期間的效能。</span><span class="sxs-lookup"><span data-stu-id="50c8e-148">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="50c8e-149">更新屬性對應組態需要重新評估所有受管理的物件。</span><span class="sxs-lookup"><span data-stu-id="50c8e-149">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="50c8e-150">建議您最好不要經常變更屬性對應。</span><span class="sxs-lookup"><span data-stu-id="50c8e-150">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50c8e-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50c8e-151">Next steps</span></span>

* [<span data-ttu-id="50c8e-152">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="50c8e-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="50c8e-153">自動化 SaaS 應用程式使用者佈建/解除佈建</span><span class="sxs-lookup"><span data-stu-id="50c8e-153">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="50c8e-154">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="50c8e-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="50c8e-155">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="50c8e-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="50c8e-156">使用 SCIM 以啟用從 Azure Active Directory 到應用程式的使用者和群組自動佈建</span><span class="sxs-lookup"><span data-stu-id="50c8e-156">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="50c8e-157">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="50c8e-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="50c8e-158">如何整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="50c8e-158">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

