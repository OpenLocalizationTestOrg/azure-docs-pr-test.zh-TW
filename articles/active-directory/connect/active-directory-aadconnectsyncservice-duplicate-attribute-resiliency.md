---
title: "aaaIdentity 同步處理和重複項目屬性的恢復功能 |Microsoft 文件"
description: "新的 UPN 或 ProxyAddress 衝突 toohandle 物件在使用 Azure AD Connect 目錄同步作業期間如何行為。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a><span data-ttu-id="15e64-103">身分識別同步處理和重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="15e64-103">Identity synchronization and duplicate attribute resiliency</span></span>
<span data-ttu-id="15e64-104">「重複屬性恢復功能」是 Azure Active Directory 中的一項功能，可在執行 Microsoft 的其中一個同步處理工具時，用來消除 **UserPrincipalName** 和 **ProxyAddress** 衝突所造成的不便。</span><span class="sxs-lookup"><span data-stu-id="15e64-104">Duplicate Attribute Resiliency is a feature in Azure Active Directory that will eliminate friction caused by **UserPrincipalName** and **ProxyAddress** conflicts when running one of Microsoft’s synchronization tools.</span></span>

<span data-ttu-id="15e64-105">所有之間這兩個屬性都是唯一通常需要的 toobe**使用者**，**群組**，或**連絡人**給定的 Azure Active Directory 租用戶中的物件。</span><span class="sxs-lookup"><span data-stu-id="15e64-105">These two attributes are generally required toobe unique across all **User**, **Group**, or **Contact** objects in a given Azure Active Directory tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="15e64-106">只有使用者可以擁有 UPN。</span><span class="sxs-lookup"><span data-stu-id="15e64-106">Only Users can have UPNs.</span></span>
> 
> 

<span data-ttu-id="15e64-107">hello 新行為，這項功能可讓 hello 雲端部份 hello 同步管線中，因此它是無從驗證，包括 Azure AD Connect、 DirSync 和 MIM + 連接器任何 Microsoft 同步處理產品相關的用戶端。</span><span class="sxs-lookup"><span data-stu-id="15e64-107">hello new behavior that this feature enables is in hello cloud portion of hello sync pipeline, therefore it is client agnostic and relevant for any Microsoft synchronization product including Azure AD Connect, DirSync and MIM + Connector.</span></span> <span data-ttu-id="15e64-108">hello 泛型的詞彙 「 同步處理用戶端 」 用於此文件 toorepresent 這些產品的任何一個。</span><span class="sxs-lookup"><span data-stu-id="15e64-108">hello generic term “sync client” is used in this document toorepresent any one of these products.</span></span>

## <a name="current-behavior"></a><span data-ttu-id="15e64-109">目前的行為</span><span class="sxs-lookup"><span data-stu-id="15e64-109">Current behavior</span></span>
<span data-ttu-id="15e64-110">如果沒有嘗試 tooprovision UPN 或 ProxyAddress 值違反了這個唯一性條件約束新的物件，Azure Active Directory 會封鎖來自建立該物件。</span><span class="sxs-lookup"><span data-stu-id="15e64-110">If there is an attempt tooprovision a new object with a UPN or ProxyAddress value that violates this uniqueness constraint, Azure Active Directory blocks that object from being created.</span></span> <span data-ttu-id="15e64-111">同樣地，如果更新物件時具有非唯一的 UPN 或 ProxyAddress，hello 更新將會失敗。</span><span class="sxs-lookup"><span data-stu-id="15e64-111">Similarly, if an object is updated with a non-unique UPN or ProxyAddress, hello update fails.</span></span> <span data-ttu-id="15e64-112">佈建嘗試或更新的 hello hello 同步用戶端時每個匯出循環中，會重試，並繼續 toofail，hello 衝突解決之前。</span><span class="sxs-lookup"><span data-stu-id="15e64-112">hello provisioning attempt or update is retried by hello sync client upon each export cycle, and continues toofail until hello conflict is resolved.</span></span> <span data-ttu-id="15e64-113">在每次嘗試時產生錯誤報表電子郵件和 hello 同步用戶端會將錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="15e64-113">An error report email is generated upon each attempt and an error is logged by hello sync client.</span></span>

## <a name="behavior-with-duplicate-attribute-resiliency"></a><span data-ttu-id="15e64-114">重複屬性恢復功能的行為</span><span class="sxs-lookup"><span data-stu-id="15e64-114">Behavior with Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="15e64-115">而不完全失敗 tooprovision 或更新且重複的屬性，Azure Active Directory 「 隔離 」 hello 重複的屬性會違反 hello 唯一性條件約束的物件。</span><span class="sxs-lookup"><span data-stu-id="15e64-115">Instead of completely failing tooprovision or update an object with a duplicate attribute, Azure Active Directory “quarantines” hello duplicate attribute which would violate hello uniqueness constraint.</span></span> <span data-ttu-id="15e64-116">如果這是必要的佈建，例如 UserPrincipalName 屬性 hello 服務指派的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="15e64-116">If this attribute is required for provisioning, like UserPrincipalName, hello service assigns a placeholder value.</span></span> <span data-ttu-id="15e64-117">這些暫存值 hello 格式</span><span class="sxs-lookup"><span data-stu-id="15e64-117">hello format of these temporary values is</span></span>  
<span data-ttu-id="15e64-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”。</span><span class="sxs-lookup"><span data-stu-id="15e64-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.</span></span>  
<span data-ttu-id="15e64-119">如果 hello 屬性不是必要的如**ProxyAddress**，Azure Active Directory 只要隔離 hello 衝突的屬性，並繼續處理 hello 物件建立或更新。</span><span class="sxs-lookup"><span data-stu-id="15e64-119">If hello attribute is not required, like a  **ProxyAddress**, Azure Active Directory simply quarantines hello conflict attribute and proceeds with hello object creation or update.</span></span>

<span data-ttu-id="15e64-120">在隔離 hello 屬性，hello 衝突的相關資訊會在 hello 使用相同的錯誤報表電子郵件傳送 hello 舊的行為。</span><span class="sxs-lookup"><span data-stu-id="15e64-120">Upon quarantining hello attribute, information about hello conflict is sent in hello same error report email used in hello old behavior.</span></span> <span data-ttu-id="15e64-121">不過，此資訊只會出現在 hello 錯誤報告一次，hello 隔離發生失敗時，它不會繼續 toobe 未來記錄電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15e64-121">However, this info only appears in hello error report one time, when hello quarantine happens, it does not continue toobe logged in future emails.</span></span> <span data-ttu-id="15e64-122">此外，因為此物件的 hello 匯出成功，hello 同步用戶端不會記錄錯誤並不重試 hello 建立 / 更新作業，在後續同步處理循環時。</span><span class="sxs-lookup"><span data-stu-id="15e64-122">Also, since hello export for this object has succeeded, hello sync client does not log an error and does not retry hello create / update operation upon subsequent sync cycles.</span></span>

<span data-ttu-id="15e64-123">此行為的新屬性已被的 toosupport 加入 toohello 使用者、 群組和連絡人物件類別：</span><span class="sxs-lookup"><span data-stu-id="15e64-123">toosupport this behavior a new attribute has been added toohello User, Group, and Contact object classes:</span></span>  
<span data-ttu-id="15e64-124">**DirSyncProvisioningErrors**</span><span class="sxs-lookup"><span data-stu-id="15e64-124">**DirSyncProvisioningErrors**</span></span>

<span data-ttu-id="15e64-125">這是使用的 toostore hello 衝突的屬性會違反 hello 唯一性條件約束應該將它們加入通常在多重值的屬性。</span><span class="sxs-lookup"><span data-stu-id="15e64-125">This is a multi-valued attribute that is used toostore hello conflicting attributes that would violate hello uniqueness constraint should they be added normally.</span></span> <span data-ttu-id="15e64-126">執行有重複的屬性衝突已經解決，且會自動從隔離區移除有問題的 hello 屬性每個小時 toolook 的 Azure Active Directory 中已啟用背景計時器工作。</span><span class="sxs-lookup"><span data-stu-id="15e64-126">A background timer task has been enabled in Azure Active Directory that  runs every hour toolook for duplicate attribute conflicts that have been resolved, and automatically removes hello attributes in question from quarantine.</span></span>

### <a name="enabling-duplicate-attribute-resiliency"></a><span data-ttu-id="15e64-127">啟用重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="15e64-127">Enabling Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="15e64-128">重複的屬性恢復功能會在所有的 Azure Active Directory 租用戶之間 hello 新的預設行為。</span><span class="sxs-lookup"><span data-stu-id="15e64-128">Duplicate Attribute Resiliency will be hello new default behavior across all Azure Active Directory tenants.</span></span> <span data-ttu-id="15e64-129">它會預設啟用的同步處理 hello 於 2016 年 8 月 22 日，或更新版本的第一次的所有租用戶上。</span><span class="sxs-lookup"><span data-stu-id="15e64-129">It will be on by default for all tenants that enabled synchronization for hello first time on August 22nd, 2016 or later.</span></span> <span data-ttu-id="15e64-130">啟用同步處理先前 toothis 日期的租用戶會有已啟用批次中的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="15e64-130">Tenants that enabled sync prior toothis date will have hello feature enabled in batches.</span></span> <span data-ttu-id="15e64-131">本次首度發行的 2016 年 9 月開始，會傳送電子郵件通知 tooeach 租用戶的技術通知接觸 hello hello 功能會啟用時的特定日期。</span><span class="sxs-lookup"><span data-stu-id="15e64-131">This rollout will begin in September 2016, and an email notification will be sent tooeach tenant's technical notification contact with hello specific date when hello feature will be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="15e64-132">一旦開啟「重複屬性恢復功能」，即無法予以停用。</span><span class="sxs-lookup"><span data-stu-id="15e64-132">Once Duplicate Attribute Resiliency has been turned on it cannot be disabled.</span></span>

<span data-ttu-id="15e64-133">如果您的租用戶啟用 hello 功能 toocheck，您可以下載 hello hello Azure Active Directory PowerShell 模組最新版本，執行：</span><span class="sxs-lookup"><span data-stu-id="15e64-133">toocheck if hello feature is enabled for your tenant, you can do so by downloading hello latest version of hello Azure Active Directory PowerShell module and running:</span></span>

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> <span data-ttu-id="15e64-134">它已為您的租用戶之前，無法再使用 Set-msoldirsyncfeature cmdlet tooproactively 啟用 hello 重複屬性恢復功能。</span><span class="sxs-lookup"><span data-stu-id="15e64-134">You can no longer use Set-MsolDirSyncFeature cmdlet tooproactively enable hello Duplicate Attribute Resiliency feature before it is turned on for your tenant.</span></span> <span data-ttu-id="15e64-135">toobe 無法 tootest hello 功能，您將需要 toocreate 新的 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="15e64-135">toobe able tootest hello feature, you will need toocreate a new Azure Active Directory tenant.</span></span>

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a><span data-ttu-id="15e64-136">識別具有 DirSyncProvisioningErrors 的物件</span><span class="sxs-lookup"><span data-stu-id="15e64-136">Identifying Objects with DirSyncProvisioningErrors</span></span>
<span data-ttu-id="15e64-137">這些錯誤，因為 tooduplicate 屬性衝突，Azure Active Directory PowerShell 和 Office 365 系統管理入口網站 hello tooidentify 物件有目前兩種方法。</span><span class="sxs-lookup"><span data-stu-id="15e64-137">There are currently two methods tooidentify objects that have these errors due tooduplicate property conflicts, Azure Active Directory PowerShell and hello Office 365 Admin Portal.</span></span> <span data-ttu-id="15e64-138">有計劃 tooextend tooadditional 入口網站基礎 hello 未來中的報告。</span><span class="sxs-lookup"><span data-stu-id="15e64-138">There are plans tooextend tooadditional portal based reporting in hello future.</span></span>

### <a name="azure-active-directory-powershell"></a><span data-ttu-id="15e64-139">Azure Active Directory PowerShell</span><span class="sxs-lookup"><span data-stu-id="15e64-139">Azure Active Directory PowerShell</span></span>
<span data-ttu-id="15e64-140">Hello 本主題中的 PowerShell cmdlet，hello 下列條件為真：</span><span class="sxs-lookup"><span data-stu-id="15e64-140">For hello PowerShell cmdlets in this topic, hello following is true:</span></span>

* <span data-ttu-id="15e64-141">下列指令程式的 hello 都區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="15e64-141">All of hello following cmdlets are case sensitive.</span></span>
* <span data-ttu-id="15e64-142">hello **– ErrorCategory PropertyConflict**必須永遠包含在內。</span><span class="sxs-lookup"><span data-stu-id="15e64-142">hello **–ErrorCategory PropertyConflict** must always be included.</span></span> <span data-ttu-id="15e64-143">目前沒有任何其他類型**ErrorCategory**，但可能會在 hello 未來擴充。</span><span class="sxs-lookup"><span data-stu-id="15e64-143">There are currently no other types of **ErrorCategory**, but this may be extended in hello future.</span></span>

<span data-ttu-id="15e64-144">首先，執行 **Connect-MsolService** 並輸入租用戶系統管理員的認證。</span><span class="sxs-lookup"><span data-stu-id="15e64-144">First, get started by running **Connect-MsolService** and entering credentials for a tenant administrator.</span></span>

<span data-ttu-id="15e64-145">然後，使用下列 cmdlet 和運算子 tooview 錯誤以不同方式的 hello:</span><span class="sxs-lookup"><span data-stu-id="15e64-145">Then, use hello following cmdlets and operators tooview errors in different ways:</span></span>

1. [<span data-ttu-id="15e64-146">檢視全部</span><span class="sxs-lookup"><span data-stu-id="15e64-146">See All</span></span>](#see-all)
2. [<span data-ttu-id="15e64-147">依屬性類型</span><span class="sxs-lookup"><span data-stu-id="15e64-147">By Property Type</span></span>](#by-property-type)
3. [<span data-ttu-id="15e64-148">依衝突的值</span><span class="sxs-lookup"><span data-stu-id="15e64-148">By Conflicting Value</span></span>](#by-conflicting-value)
4. [<span data-ttu-id="15e64-149">使用字串搜尋</span><span class="sxs-lookup"><span data-stu-id="15e64-149">Using a String Search</span></span>](#using-a-string-search)
5. [<span data-ttu-id="15e64-150">排序</span><span class="sxs-lookup"><span data-stu-id="15e64-150">Sorted</span></span>](#sorted)
6. [<span data-ttu-id="15e64-151">以有限的數量或全部</span><span class="sxs-lookup"><span data-stu-id="15e64-151">In a Limited Quantity or All</span></span>](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a><span data-ttu-id="15e64-152">檢視全部</span><span class="sxs-lookup"><span data-stu-id="15e64-152">See all</span></span>
<span data-ttu-id="15e64-153">一旦連接之後，toosee 一般佈建錯誤 hello 租用戶中的屬性清單執行：</span><span class="sxs-lookup"><span data-stu-id="15e64-153">Once connected, toosee a general list of attribute provisioning errors in hello tenant run:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

<span data-ttu-id="15e64-154">這會產生類似 hello 下列結果：</span><span class="sxs-lookup"><span data-stu-id="15e64-154">This produces a result like hello following:</span></span>  
 <span data-ttu-id="15e64-155">![Get MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")</span><span class="sxs-lookup"><span data-stu-id="15e64-155">![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get-MsolDirSyncProvisioningError")</span></span>  

#### <a name="by-property-type"></a><span data-ttu-id="15e64-156">依屬性類型</span><span class="sxs-lookup"><span data-stu-id="15e64-156">By property type</span></span>
<span data-ttu-id="15e64-157">依屬性類型的 toosee 錯誤新增 hello **-PropertyName**旗標以 hello **UserPrincipalName**或**ProxyAddresses**引數：</span><span class="sxs-lookup"><span data-stu-id="15e64-157">toosee errors by property type, add hello **-PropertyName** flag with hello **UserPrincipalName** or **ProxyAddresses** argument:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

<span data-ttu-id="15e64-158">或</span><span class="sxs-lookup"><span data-stu-id="15e64-158">Or</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a><span data-ttu-id="15e64-159">依衝突的值</span><span class="sxs-lookup"><span data-stu-id="15e64-159">By conflicting value</span></span>
<span data-ttu-id="15e64-160">toosee 錯誤相關 tooa 特定屬性新增 hello **-PropertyValue**旗標 (**-PropertyName**加入這個旗標時必須一併使用):</span><span class="sxs-lookup"><span data-stu-id="15e64-160">toosee errors relating tooa specific property add hello **-PropertyValue** flag (**-PropertyName** must be used as well when adding this flag):</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a><span data-ttu-id="15e64-161">使用字串搜尋</span><span class="sxs-lookup"><span data-stu-id="15e64-161">Using a string search</span></span>
<span data-ttu-id="15e64-162">toodo 廣泛的字串搜尋使用 hello **-SearchString**旗標。</span><span class="sxs-lookup"><span data-stu-id="15e64-162">toodo a broad string search use hello **-SearchString** flag.</span></span> <span data-ttu-id="15e64-163">這適用於獨立從所有旗標，但 hello 的例外是上述 hello **-ErrorCategory PropertyConflict**，永遠是必要項：</span><span class="sxs-lookup"><span data-stu-id="15e64-163">This can be used independently from all of hello above flags, with hello exception of **-ErrorCategory PropertyConflict**, which is always required:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a><span data-ttu-id="15e64-164">以有限的數量或全部</span><span class="sxs-lookup"><span data-stu-id="15e64-164">In a limited quantity or all</span></span>
1. <span data-ttu-id="15e64-165">**MaxResults <Int>** 可以是使用 toolimit hello 查詢 tooa 特定數目的值。</span><span class="sxs-lookup"><span data-stu-id="15e64-165">**MaxResults <Int>** can be used toolimit hello query tooa specific number of values.</span></span>
2. <span data-ttu-id="15e64-166">**所有**可以是使用的 tooensure 大量錯誤存在的 hello 案例中擷取所有結果。</span><span class="sxs-lookup"><span data-stu-id="15e64-166">**All** can be used tooensure all results are retrieved in hello case that a large number of errors exists.</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a><span data-ttu-id="15e64-167">Office 365 系統管理入口網站</span><span class="sxs-lookup"><span data-stu-id="15e64-167">Office 365 admin portal</span></span>
<span data-ttu-id="15e64-168">您可以在 hello Office 365 系統管理中心檢視目錄同步作業錯誤。</span><span class="sxs-lookup"><span data-stu-id="15e64-168">You can view directory synchronization errors in hello Office 365 admin center.</span></span> <span data-ttu-id="15e64-169">hello hello Office 365 入口網站只會顯示在報表**使用者**發生這些錯誤的物件。</span><span class="sxs-lookup"><span data-stu-id="15e64-169">hello report in hello Office 365 portal only displays **User** objects that have these errors.</span></span> <span data-ttu-id="15e64-170">並不會顯示「群組」和「連絡人」之間的衝突相關資訊。</span><span class="sxs-lookup"><span data-stu-id="15e64-170">It does not show info about conflicts between **Groups** and **Contacts**.</span></span>

<span data-ttu-id="15e64-171">![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="15e64-171">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Active Users")</span></span>

<span data-ttu-id="15e64-172">如需如何 tooview 目錄同步作業錯誤的 hello Office 365 admin center 指示，請參閱[識別 Office 365 中的目錄同步作業錯誤](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)。</span><span class="sxs-lookup"><span data-stu-id="15e64-172">For instructions on how tooview directory synchronization errors in hello Office 365 admin center, see [Identify directory synchronization errors in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).</span></span>

### <a name="identity-synchronization-error-report"></a><span data-ttu-id="15e64-173">身分識別同步處理錯誤報告</span><span class="sxs-lookup"><span data-stu-id="15e64-173">Identity synchronization error report</span></span>
<span data-ttu-id="15e64-174">當具有重複的屬性發生衝突的物件會處理與通知包含在這個新行為 hello 標準識別身分同步處理錯誤報告的電子郵件，會傳送 hello 租用戶的 toohello 通知技術連絡人。</span><span class="sxs-lookup"><span data-stu-id="15e64-174">When an object with a duplicate attribute conflict is handled with this new behavior a notification is included in hello standard Identity Synchronization Error Report email that is sent toohello Technical Notification contact for hello tenant.</span></span> <span data-ttu-id="15e64-175">不過，此行為有一項重大變更。</span><span class="sxs-lookup"><span data-stu-id="15e64-175">However, there is an important change in this behavior.</span></span> <span data-ttu-id="15e64-176">在過去 hello，重複的屬性發生衝突的相關資訊會包含在每個後續的錯誤報告之前 hello 衝突已解決。</span><span class="sxs-lookup"><span data-stu-id="15e64-176">In hello past, information about a duplicate attribute conflict would be included in every subsequent error report until hello conflict was resolved.</span></span> <span data-ttu-id="15e64-177">使用這個新的行為，指定衝突的 hello 錯誤通知未只能出現一次-次 hello hello 衝突的屬性會被隔離。</span><span class="sxs-lookup"><span data-stu-id="15e64-177">With this new behavior, hello error notification for a given conflict does only appear once- at hello time hello conflicting attribute is quarantined.</span></span>

<span data-ttu-id="15e64-178">哪些 hello 電子郵件通知看起來像 ProxyAddress 衝突的範例如下：</span><span class="sxs-lookup"><span data-stu-id="15e64-178">Here is an example of what hello email notification looks like for a ProxyAddress conflict:</span></span>  
    <span data-ttu-id="15e64-179">![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="15e64-179">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

## <a name="resolving-conflicts"></a><span data-ttu-id="15e64-180">解決衝突</span><span class="sxs-lookup"><span data-stu-id="15e64-180">Resolving conflicts</span></span>
<span data-ttu-id="15e64-181">疑難排解這些錯誤的策略與解決策略不應該從 hello hello 過去中的重複屬性錯誤處理的方式不同。</span><span class="sxs-lookup"><span data-stu-id="15e64-181">Troubleshooting strategy and resolution tactics for these errors should not differ from hello way duplicate attribute errors were handled in hello past.</span></span> <span data-ttu-id="15e64-182">hello 唯一的差異是，透過在 hello 服務端 tooautomatically hello 租用戶的 hello 計時器工作掃掠加入 hello 屬性問題 toohello 適當物件中一旦 hello 衝突的解決。</span><span class="sxs-lookup"><span data-stu-id="15e64-182">hello only difference is that hello timer task sweeps through hello tenant on hello service-side tooautomatically add hello attribute in question toohello proper object once hello conflict is resolved.</span></span>

<span data-ttu-id="15e64-183">hello 下列文件概述各種疑難排解和解決方式：[重複或無效的屬性會讓 Office 365 中的目錄同步作業](https://support.microsoft.com/kb/2647098)。</span><span class="sxs-lookup"><span data-stu-id="15e64-183">hello following article outlines various troubleshooting and resolution strategies: [Duplicate or invalid attributes prevent directory synchronization in Office 365](https://support.microsoft.com/kb/2647098).</span></span>

## <a name="known-issues"></a><span data-ttu-id="15e64-184">已知問題</span><span class="sxs-lookup"><span data-stu-id="15e64-184">Known issues</span></span>
<span data-ttu-id="15e64-185">沒有任何已知問題會導致資料遺失或服務降級。</span><span class="sxs-lookup"><span data-stu-id="15e64-185">None of these known issues causes data loss or service degradation.</span></span> <span data-ttu-id="15e64-186">其中幾個美觀，其他人會導致標準 「*前的恢復功能*"重複的屬性而不是隔離 hello 衝突的屬性，而另一個會擲回的錯誤 toobe 會造成特定錯誤 toorequire 額外的手動 v-table 修正。</span><span class="sxs-lookup"><span data-stu-id="15e64-186">Several of them are aesthetic, others cause standard “*pre-resiliency*” duplicate attribute errors toobe thrown instead of quarantining hello conflict attribute, and another causes certain errors toorequire extra manual fix-up.</span></span>

<span data-ttu-id="15e64-187">**核心行為︰**</span><span class="sxs-lookup"><span data-stu-id="15e64-187">**Core behavior:**</span></span>

1. <span data-ttu-id="15e64-188">具有特定的屬性設定的物件相對於的 toohello 重複屬性被隔離繼續 tooreceive 匯出錯誤。</span><span class="sxs-lookup"><span data-stu-id="15e64-188">Objects with specific attribute configurations continue tooreceive export errors as opposed toohello duplicate attribute(s) being quarantined.</span></span>  
   <span data-ttu-id="15e64-189">例如：</span><span class="sxs-lookup"><span data-stu-id="15e64-189">For example:</span></span>
   
    <span data-ttu-id="15e64-190">a.</span><span class="sxs-lookup"><span data-stu-id="15e64-190">a.</span></span> <span data-ttu-id="15e64-191">新使用者會在 AD 中以 UPN 為 **Joe@contoso.com**、ProxyAddress 為 **smtp:Joe@contoso.com** 的方式建立</span><span class="sxs-lookup"><span data-stu-id="15e64-191">New user is created in AD with a UPN of **Joe@contoso.com** and ProxyAddress **smtp:Joe@contoso.com**</span></span>
   
    <span data-ttu-id="15e64-192">b.</span><span class="sxs-lookup"><span data-stu-id="15e64-192">b.</span></span> <span data-ttu-id="15e64-193">hello 這個物件屬性發生衝突與現有的群組，其中是 ProxyAddress  **SMTP:Joe@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="15e64-193">hello properties of this object conflict with an existing Group, where ProxyAddress is **SMTP:Joe@contoso.com**.</span></span>
   
    <span data-ttu-id="15e64-194">c.</span><span class="sxs-lookup"><span data-stu-id="15e64-194">c.</span></span> <span data-ttu-id="15e64-195">在匯出時**ProxyAddress 衝突**而不需要隔離 hello 衝突的屬性會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="15e64-195">Upon export, a **ProxyAddress conflict** error is thrown instead of having hello conflict attributes quarantined.</span></span> <span data-ttu-id="15e64-196">hello 作業是在每個後續同步處理循環中，重試，因為它可能已啟用 hello 恢復功能之前。</span><span class="sxs-lookup"><span data-stu-id="15e64-196">hello operation is retried upon each subsequent sync cycle, as it would have been before hello resiliency feature was enabled.</span></span>
2. <span data-ttu-id="15e64-197">如果在建立兩個群組會在內部以 hello 相同 SMTP 位址，一個失敗 tooprovision hello 第一次嘗試重複的標準**ProxyAddress**錯誤。</span><span class="sxs-lookup"><span data-stu-id="15e64-197">If two Groups are created on-premises with hello same SMTP address, one fails tooprovision on hello first attempt with a standard duplicate **ProxyAddress** error.</span></span> <span data-ttu-id="15e64-198">不過，hello 重複的值是適當隔離時 hello 下一個同步處理循環。</span><span class="sxs-lookup"><span data-stu-id="15e64-198">However, hello duplicate value is properly quarantined upon hello next sync cycle.</span></span>

<span data-ttu-id="15e64-199">**Office 入口網站報告**：</span><span class="sxs-lookup"><span data-stu-id="15e64-199">**Office Portal Report**:</span></span>

1. <span data-ttu-id="15e64-200">UPN 衝突集合中的兩個物件的 hello 詳細的錯誤訊息是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="15e64-200">hello detailed error message for two objects in a UPN conflict set is hello same.</span></span> <span data-ttu-id="15e64-201">這表示它們都已變更 / 隔離 UPN，當事實上只有其中一個變更了資料。</span><span class="sxs-lookup"><span data-stu-id="15e64-201">This indicates that they have both had their UPN changed / quarantined, when in fact only a one of them had any data changed.</span></span>
2. <span data-ttu-id="15e64-202">hello UPN 衝突的詳細的錯誤訊息會顯示 hello 錯誤 displayName 的使用者已變更/隔離其 UPN。</span><span class="sxs-lookup"><span data-stu-id="15e64-202">hello detailed error message for a UPN conflict shows hello wrong displayName for a user who has had their UPN changed/quarantined.</span></span> <span data-ttu-id="15e64-203">例如：</span><span class="sxs-lookup"><span data-stu-id="15e64-203">For example:</span></span>
   
    <span data-ttu-id="15e64-204">a.</span><span class="sxs-lookup"><span data-stu-id="15e64-204">a.</span></span> <span data-ttu-id="15e64-205">**User A** 會先與 **UPN = User@contoso.com** 同步。</span><span class="sxs-lookup"><span data-stu-id="15e64-205">**User A** syncs up first with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="15e64-206">b.</span><span class="sxs-lookup"><span data-stu-id="15e64-206">b.</span></span> <span data-ttu-id="15e64-207">**使用者 B**嘗試的 toobe 同步處理與接**UPN = User@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="15e64-207">**User B** is attempted toobe synced up next with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="15e64-208">c.</span><span class="sxs-lookup"><span data-stu-id="15e64-208">c.</span></span> <span data-ttu-id="15e64-209">**使用者 B 的**UPN 變更太**User1234@contoso.onmicrosoft.com** 和 **User@contoso.com** 太加入**DirSyncProvisioningErrors**。</span><span class="sxs-lookup"><span data-stu-id="15e64-209">**User B’s** UPN is changed too**User1234@contoso.onmicrosoft.com** and **User@contoso.com** is added too**DirSyncProvisioningErrors**.</span></span>
   
    <span data-ttu-id="15e64-210">d.</span><span class="sxs-lookup"><span data-stu-id="15e64-210">d.</span></span> <span data-ttu-id="15e64-211">hello 錯誤訊息，取得**使用者 B**應該指出**使用者 A**已經有 **User@contoso.com**  UPN，但它示**使用者 B**自己顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="15e64-211">hello error message for **User B** should indicate that **User A** already has **User@contoso.com** as a UPN, but it shows **User B’s** own displayName.</span></span>

<span data-ttu-id="15e64-212">**身分識別同步處理錯誤報告**：</span><span class="sxs-lookup"><span data-stu-id="15e64-212">**Identity synchronization error report**:</span></span>

<span data-ttu-id="15e64-213">hello 連結*步驟 tooresolve 此問題*不正確：</span><span class="sxs-lookup"><span data-stu-id="15e64-213">hello link for *steps on how tooresolve this issue* is incorrect:</span></span>  
    <span data-ttu-id="15e64-214">![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="15e64-214">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

<span data-ttu-id="15e64-215">它應該太點[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency)。</span><span class="sxs-lookup"><span data-stu-id="15e64-215">It should point too[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).</span></span>

## <a name="see-also"></a><span data-ttu-id="15e64-216">另請參閱</span><span class="sxs-lookup"><span data-stu-id="15e64-216">See also</span></span>
* [<span data-ttu-id="15e64-217">Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="15e64-217">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="15e64-218">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15e64-218">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="15e64-219">在 Office 365 中識別目錄同步處理錯誤</span><span class="sxs-lookup"><span data-stu-id="15e64-219">Identify directory synchronization errors in Office 365</span></span>](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

