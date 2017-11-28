---
title: "Azure AD 屬性對應 aaaCustomizing |Microsoft 文件"
description: "了解 Azure Active Directory 中的 SaaS 應用程式的哪些屬性對應如何修改它們 tooaddress 業務需要。"
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
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="63154-103">在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應</span><span class="sxs-lookup"><span data-stu-id="63154-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="63154-104">Microsoft Azure AD 提供使用者佈建 toothird 合作對象 saas De terceros como Salesforce，Google Apps y otros 的支援。</span><span class="sxs-lookup"><span data-stu-id="63154-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="63154-105">如果您已將使用者佈建的協力廠商 SaaS 應用程式已啟用，hello Azure 管理入口網站控制它的屬性值，在表單的設定，稱為 「 屬性對應 」。</span><span class="sxs-lookup"><span data-stu-id="63154-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="63154-106">在 Azure AD 使用者物件和每個 SaaS app 的使用者物件之間，有一組預先設定的屬性對應。</span><span class="sxs-lookup"><span data-stu-id="63154-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="63154-107">有些 app 則管理其他類型的物件，例如群組或連絡人。</span><span class="sxs-lookup"><span data-stu-id="63154-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="63154-108">您可以自訂 hello 根據 tooyour 商務需求的預設屬性對應。</span><span class="sxs-lookup"><span data-stu-id="63154-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="63154-109">這表示您可以變更或刪除現有的屬性對應，或建立新的屬性對應。</span><span class="sxs-lookup"><span data-stu-id="63154-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="63154-110">在 hello Azure AD 入口網站中，您可以存取這項功能，依序按一下**對應**底下設定**佈建**在 hello**管理**區段**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="63154-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="63154-112">按一下**對應**組態中，開啟相關的 hello**屬性對應**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63154-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="63154-113">有 asignaciones de atributos que son necesarias para SaaS 應用程式 toofunction 正確。</span><span class="sxs-lookup"><span data-stu-id="63154-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="63154-114">必要的屬性，如 hello**刪除**則無法使用功能。</span><span class="sxs-lookup"><span data-stu-id="63154-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="63154-116">在 hello 上述範例中，您可以看到該 hello **Username**在 Salesforce 中的受管理物件的屬性填入 hello **userPrincipalName**的 hello 值連結的 Azure Active Directory 物件。</span><span class="sxs-lookup"><span data-stu-id="63154-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="63154-117">您可以按一下對應來自訂現有的 [屬性對應]。</span><span class="sxs-lookup"><span data-stu-id="63154-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="63154-118">這會開啟 hello**編輯屬性**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63154-118">This opens hello **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="63154-120">了解屬性對應類型</span><span class="sxs-lookup"><span data-stu-id="63154-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="63154-121">有了屬性對應，您就可以控制屬性在協力廠商 SaaS 應用程式中填入的方式。</span><span class="sxs-lookup"><span data-stu-id="63154-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="63154-122">支援四種不同的對應類型：</span><span class="sxs-lookup"><span data-stu-id="63154-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="63154-123">**直接**– hello 目標屬性在 Azure AD 時填入 hello hello 連結物件的屬性值。</span><span class="sxs-lookup"><span data-stu-id="63154-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="63154-124">**常數**– hello 目標屬性會填入您所指定的特定字串。</span><span class="sxs-lookup"><span data-stu-id="63154-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="63154-125">**運算式**-根據 hello 的類似指令碼運算式的結果填入 hello 目標屬性。</span><span class="sxs-lookup"><span data-stu-id="63154-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="63154-126">如需詳細資訊，請參閱[在 Azure Active Directory 中撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="63154-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="63154-127">**無**-hello 目標屬性會保留不變。</span><span class="sxs-lookup"><span data-stu-id="63154-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="63154-128">不過，如果 hello 目標 destino está vacío，它會填入 hello 您指定的預設值。</span><span class="sxs-lookup"><span data-stu-id="63154-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="63154-129">在加法 toothese 四個基本屬性對應類型中，自訂屬性對應還支援選擇性 hello 概念**預設**值指派。</span><span class="sxs-lookup"><span data-stu-id="63154-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="63154-130">hello 預設 la asignación del valor 目標屬性會填入值，如果沒有 ningún valor en Azure AD ni hello 目標物件上。</span><span class="sxs-lookup"><span data-stu-id="63154-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="63154-131">此空白 tooleave hello 最常見的組態。</span><span class="sxs-lookup"><span data-stu-id="63154-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="63154-132">了解屬性對應屬性</span><span class="sxs-lookup"><span data-stu-id="63154-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="63154-133">在 hello 前一個區段中，您已經導入了的 toohello 屬性對應類型屬性。</span><span class="sxs-lookup"><span data-stu-id="63154-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="63154-134">在加法 toothis 屬性中，屬性對應並也支援下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="63154-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="63154-135">**來源屬性**-hello 使用者屬性從 hello 來源系統 (例如： Azure Active Directory)。</span><span class="sxs-lookup"><span data-stu-id="63154-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="63154-136">**目標屬性**– hello 目標系統中的 hello 使用者屬性 (例如： ServiceNow)。</span><span class="sxs-lookup"><span data-stu-id="63154-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="63154-137">**符合使用此屬性的物件**– 是否應使用此對應 toouniquely 識別 hello 來源和目標系統之間的使用者。</span><span class="sxs-lookup"><span data-stu-id="63154-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="63154-138">這通常設定在 hello userPrincipalName，或在 Azure AD 中，通常是 mail 屬性對應 tooa 目標應用程式中的使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="63154-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="63154-139">**比對優先順序** – 您可以設定多個比對屬性。</span><span class="sxs-lookup"><span data-stu-id="63154-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="63154-140">有多個，會評估 hello 這個欄位所定義的順序。</span><span class="sxs-lookup"><span data-stu-id="63154-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="63154-141">只要找到相符項目，便不會評估進一步比對屬性。</span><span class="sxs-lookup"><span data-stu-id="63154-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="63154-142">**套用此對應**</span><span class="sxs-lookup"><span data-stu-id="63154-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="63154-143">**一律** – 將此對應套用於使用者建立和更新動作</span><span class="sxs-lookup"><span data-stu-id="63154-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="63154-144">**僅限建立期間** - 僅將此對應套用於使用者建立動作</span><span class="sxs-lookup"><span data-stu-id="63154-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="63154-145">您應該知道的事情</span><span class="sxs-lookup"><span data-stu-id="63154-145">What you should know</span></span>

<span data-ttu-id="63154-146">Microsoft Azure AD 提供有效率的同步處理程序實作。</span><span class="sxs-lookup"><span data-stu-id="63154-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="63154-147">在初始化環境中，同步處理期間只會處理需要更新的物件。</span><span class="sxs-lookup"><span data-stu-id="63154-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="63154-148">更新屬性對應上的同步處理循環的 hello 效能有影響。</span><span class="sxs-lookup"><span data-stu-id="63154-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="63154-149">更新 toohello 屬性對應組態需要重新評估所有受管理的物件 toobe。</span><span class="sxs-lookup"><span data-stu-id="63154-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="63154-150">它是建議最佳作法 tookeep hello 數目最少的連續變更 tooyour 屬性對應。</span><span class="sxs-lookup"><span data-stu-id="63154-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63154-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63154-151">Next steps</span></span>

* [<span data-ttu-id="63154-152">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="63154-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="63154-153">自動化使用者佈建/取消佈建 tooSaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="63154-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="63154-154">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="63154-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="63154-155">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="63154-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="63154-156">使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組</span><span class="sxs-lookup"><span data-stu-id="63154-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="63154-157">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="63154-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="63154-158">如何教學課程清單 tooIntegrate SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="63154-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

