---
title: "身分識別同步處理和重複屬性恢復功能 | Microsoft Docs"
description: "在目錄同步處理期間如何使用 Azure AD Connect 來處理具有 UPN 或 ProxyAddress 衝突之物件的新行為。"
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
ms.openlocfilehash: 7a8700e70f64851a0c5e5e8c6b31ec7a6884a96c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a><span data-ttu-id="767bc-103">身分識別同步處理和重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="767bc-103">Identity synchronization and duplicate attribute resiliency</span></span>
<span data-ttu-id="767bc-104">「重複屬性恢復功能」是 Azure Active Directory 中的一項功能，可在執行 Microsoft 的其中一個同步處理工具時，用來消除 **UserPrincipalName** 和 **ProxyAddress** 衝突所造成的不便。</span><span class="sxs-lookup"><span data-stu-id="767bc-104">Duplicate Attribute Resiliency is a feature in Azure Active Directory that will eliminate friction caused by **UserPrincipalName** and **ProxyAddress** conflicts when running one of Microsoft’s synchronization tools.</span></span>

<span data-ttu-id="767bc-105">在指定之 Azure Active Directory 租用戶的所有「使用者」、「群組」或「連絡人」物件中，這兩個屬性通常必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="767bc-105">These two attributes are generally required to be unique across all **User**, **Group**, or **Contact** objects in a given Azure Active Directory tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="767bc-106">只有使用者可以擁有 UPN。</span><span class="sxs-lookup"><span data-stu-id="767bc-106">Only Users can have UPNs.</span></span>
> 
> 

<span data-ttu-id="767bc-107">這項功能賦予了同步管線雲端部分的新行為，因此對於任何 Microsoft 同步處理產品 (包括 Azure AD Connect、DirSync 和 MIM + 連接器) 而言，此功能不限於特定用戶端並與用戶端相關。</span><span class="sxs-lookup"><span data-stu-id="767bc-107">The new behavior that this feature enables is in the cloud portion of the sync pipeline, therefore it is client agnostic and relevant for any Microsoft synchronization product including Azure AD Connect, DirSync and MIM + Connector.</span></span> <span data-ttu-id="767bc-108">在本文件中，通用詞彙「同步用戶端」將用來代表上述任何一項產品。</span><span class="sxs-lookup"><span data-stu-id="767bc-108">The generic term “sync client” is used in this document to represent any one of these products.</span></span>

## <a name="current-behavior"></a><span data-ttu-id="767bc-109">目前的行為</span><span class="sxs-lookup"><span data-stu-id="767bc-109">Current behavior</span></span>
<span data-ttu-id="767bc-110">如果嘗試佈建的新物件具有違反此唯一性條件約束的 UPN 或 ProxyAddress 值，則 Azure Active Directory 不會建立該物件。</span><span class="sxs-lookup"><span data-stu-id="767bc-110">If there is an attempt to provision a new object with a UPN or ProxyAddress value that violates this uniqueness constraint, Azure Active Directory blocks that object from being created.</span></span> <span data-ttu-id="767bc-111">同樣地，如果以非唯一的 UPN 或 ProxyAddress 更新物件，則更新會失敗。</span><span class="sxs-lookup"><span data-stu-id="767bc-111">Similarly, if an object is updated with a non-unique UPN or ProxyAddress, the update fails.</span></span> <span data-ttu-id="767bc-112">同步用戶端會在每個匯出週期重試佈建嘗試或更新，在衝突解決前會繼續失敗。</span><span class="sxs-lookup"><span data-stu-id="767bc-112">The provisioning attempt or update is retried by the sync client upon each export cycle, and continues to fail until the conflict is resolved.</span></span> <span data-ttu-id="767bc-113">每次嘗試時都會產生錯誤報告電子郵件，並由同步用戶端記錄一個錯誤。</span><span class="sxs-lookup"><span data-stu-id="767bc-113">An error report email is generated upon each attempt and an error is logged by the sync client.</span></span>

## <a name="behavior-with-duplicate-attribute-resiliency"></a><span data-ttu-id="767bc-114">重複屬性恢復功能的行為</span><span class="sxs-lookup"><span data-stu-id="767bc-114">Behavior with Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="767bc-115">Azure Active Directory 並不是完全無法佈建或更新具有重複屬性的物件，而是會「隔離」違反唯一性條件約束的重複屬性。</span><span class="sxs-lookup"><span data-stu-id="767bc-115">Instead of completely failing to provision or update an object with a duplicate attribute, Azure Active Directory “quarantines” the duplicate attribute which would violate the uniqueness constraint.</span></span> <span data-ttu-id="767bc-116">如果佈建時需要此屬性 (例如 UserPrincipalName)，則服務會指派預留位置值。</span><span class="sxs-lookup"><span data-stu-id="767bc-116">If this attribute is required for provisioning, like UserPrincipalName, the service assigns a placeholder value.</span></span> <span data-ttu-id="767bc-117">這些暫存值的格式為</span><span class="sxs-lookup"><span data-stu-id="767bc-117">The format of these temporary values is</span></span>  
<span data-ttu-id="767bc-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”。</span><span class="sxs-lookup"><span data-stu-id="767bc-118">“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.</span></span>  
<span data-ttu-id="767bc-119">如果不需要此屬性 (例如 **ProxyAddress**)，Azure Active Directory 就會隔離衝突屬性，然後繼續建立或更新物件。</span><span class="sxs-lookup"><span data-stu-id="767bc-119">If the attribute is not required, like a  **ProxyAddress**, Azure Active Directory simply quarantines the conflict attribute and proceeds with the object creation or update.</span></span>

<span data-ttu-id="767bc-120">隔離屬性時，衝突相關資訊會以舊版行為中使用的相同錯誤報告電子郵件傳送。</span><span class="sxs-lookup"><span data-stu-id="767bc-120">Upon quarantining the attribute, information about the conflict is sent in the same error report email used in the old behavior.</span></span> <span data-ttu-id="767bc-121">不過，此資訊只會出現在錯誤報告中一次，發生隔離時，將不會繼續記錄在未來的電子郵件中。</span><span class="sxs-lookup"><span data-stu-id="767bc-121">However, this info only appears in the error report one time, when the quarantine happens, it does not continue to be logged in future emails.</span></span> <span data-ttu-id="767bc-122">此外，此物件已成功匯出，所以同步用戶端不會記錄錯誤，而且不會在後續的同步週期中重試建立 / 更新作業。</span><span class="sxs-lookup"><span data-stu-id="767bc-122">Also, since the export for this object has succeeded, the sync client does not log an error and does not retry the create / update operation upon subsequent sync cycles.</span></span>

<span data-ttu-id="767bc-123">為了支援此行為，[使用者]、[群組] 和 [連絡人] 物件類別已加入新屬性︰</span><span class="sxs-lookup"><span data-stu-id="767bc-123">To support this behavior a new attribute has been added to the User, Group, and Contact object classes:</span></span>  
<span data-ttu-id="767bc-124">**DirSyncProvisioningErrors**</span><span class="sxs-lookup"><span data-stu-id="767bc-124">**DirSyncProvisioningErrors**</span></span>

<span data-ttu-id="767bc-125">這是多重值的屬性，用來儲存正常新增時會違反唯一性條件約束的衝突屬性。</span><span class="sxs-lookup"><span data-stu-id="767bc-125">This is a multi-valued attribute that is used to store the conflicting attributes that would violate the uniqueness constraint should they be added normally.</span></span> <span data-ttu-id="767bc-126">Azure Active Directory 中已啟用背景計時器工作，該工作會每小時執行以尋找已解決的重複屬性衝突，然後從隔離區中自動移除上述屬性。</span><span class="sxs-lookup"><span data-stu-id="767bc-126">A background timer task has been enabled in Azure Active Directory that  runs every hour to look for duplicate attribute conflicts that have been resolved, and automatically removes the attributes in question from quarantine.</span></span>

### <a name="enabling-duplicate-attribute-resiliency"></a><span data-ttu-id="767bc-127">啟用重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="767bc-127">Enabling Duplicate Attribute Resiliency</span></span>
<span data-ttu-id="767bc-128">「重複屬性恢復功能」將會是所有 Azure Active Directory 租用戶的新預設行為。</span><span class="sxs-lookup"><span data-stu-id="767bc-128">Duplicate Attribute Resiliency will be the new default behavior across all Azure Active Directory tenants.</span></span> <span data-ttu-id="767bc-129">針對所有在 2016 年 8 月 22 日或之後第一次啟用同步處理的租用戶，預設都會開啟這項功能。</span><span class="sxs-lookup"><span data-stu-id="767bc-129">It will be on by default for all tenants that enabled synchronization for the first time on August 22nd, 2016 or later.</span></span> <span data-ttu-id="767bc-130">在此日期之前啟用同步功能的租用戶則會分批啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="767bc-130">Tenants that enabled sync prior to this date will have the feature enabled in batches.</span></span> <span data-ttu-id="767bc-131">這項功能推出將從 2016 年 9 月開始，每個租用戶的技術通知連絡人將會收到電子郵件通知，其中會指出啟用功能的特定日期。</span><span class="sxs-lookup"><span data-stu-id="767bc-131">This rollout will begin in September 2016, and an email notification will be sent to each tenant's technical notification contact with the specific date when the feature will be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="767bc-132">一旦開啟「重複屬性恢復功能」，即無法予以停用。</span><span class="sxs-lookup"><span data-stu-id="767bc-132">Once Duplicate Attribute Resiliency has been turned on it cannot be disabled.</span></span>

<span data-ttu-id="767bc-133">若要檢查是否已為您的租用戶啟用此功能，只要下載最新版的 Azure Active Directory PowerShell 模組並執行下列程式碼即可︰</span><span class="sxs-lookup"><span data-stu-id="767bc-133">To check if the feature is enabled for your tenant, you can do so by downloading the latest version of the Azure Active Directory PowerShell module and running:</span></span>

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> <span data-ttu-id="767bc-134">在為租用戶開啟該功能之前，您無法再使用 Set-MsolDirSyncFeature Cmdlet 來主動啟用重複屬性復原功能。</span><span class="sxs-lookup"><span data-stu-id="767bc-134">You can no longer use Set-MsolDirSyncFeature cmdlet to proactively enable the Duplicate Attribute Resiliency feature before it is turned on for your tenant.</span></span> <span data-ttu-id="767bc-135">若要測試該功能，您需要建立新的 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="767bc-135">To be able to test the feature, you will need to create a new Azure Active Directory tenant.</span></span>

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a><span data-ttu-id="767bc-136">識別具有 DirSyncProvisioningErrors 的物件</span><span class="sxs-lookup"><span data-stu-id="767bc-136">Identifying Objects with DirSyncProvisioningErrors</span></span>
<span data-ttu-id="767bc-137">目前有兩個方法可識別因為重複屬性衝突而發生錯誤的物件：Azure Active Directory PowerShell 和 Office 365 系統管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="767bc-137">There are currently two methods to identify objects that have these errors due to duplicate property conflicts, Azure Active Directory PowerShell and the Office 365 Admin Portal.</span></span> <span data-ttu-id="767bc-138">未來計劃擴充其他以入口網站為基礎的報告。</span><span class="sxs-lookup"><span data-stu-id="767bc-138">There are plans to extend to additional portal based reporting in the future.</span></span>

### <a name="azure-active-directory-powershell"></a><span data-ttu-id="767bc-139">Azure Active Directory PowerShell</span><span class="sxs-lookup"><span data-stu-id="767bc-139">Azure Active Directory PowerShell</span></span>
<span data-ttu-id="767bc-140">對於本主題中的 PowerShell Cmdlet，下列項目為真︰</span><span class="sxs-lookup"><span data-stu-id="767bc-140">For the PowerShell cmdlets in this topic, the following is true:</span></span>

* <span data-ttu-id="767bc-141">下列所有 Cmdlet 都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="767bc-141">All of the following cmdlets are case sensitive.</span></span>
* <span data-ttu-id="767bc-142">一律包含 **–ErrorCategory PropertyConflict** 。</span><span class="sxs-lookup"><span data-stu-id="767bc-142">The **–ErrorCategory PropertyConflict** must always be included.</span></span> <span data-ttu-id="767bc-143">目前沒有其他類型的 **ErrorCategory**，但可能會在未來加以擴充。</span><span class="sxs-lookup"><span data-stu-id="767bc-143">There are currently no other types of **ErrorCategory**, but this may be extended in the future.</span></span>

<span data-ttu-id="767bc-144">首先，執行 **Connect-MsolService** 並輸入租用戶系統管理員的認證。</span><span class="sxs-lookup"><span data-stu-id="767bc-144">First, get started by running **Connect-MsolService** and entering credentials for a tenant administrator.</span></span>

<span data-ttu-id="767bc-145">接著，使用下列 Cmdlet 和運算子，以不同的方式檢視錯誤︰</span><span class="sxs-lookup"><span data-stu-id="767bc-145">Then, use the following cmdlets and operators to view errors in different ways:</span></span>

1. [<span data-ttu-id="767bc-146">檢視全部</span><span class="sxs-lookup"><span data-stu-id="767bc-146">See All</span></span>](#see-all)
2. [<span data-ttu-id="767bc-147">依屬性類型</span><span class="sxs-lookup"><span data-stu-id="767bc-147">By Property Type</span></span>](#by-property-type)
3. [<span data-ttu-id="767bc-148">依衝突的值</span><span class="sxs-lookup"><span data-stu-id="767bc-148">By Conflicting Value</span></span>](#by-conflicting-value)
4. [<span data-ttu-id="767bc-149">使用字串搜尋</span><span class="sxs-lookup"><span data-stu-id="767bc-149">Using a String Search</span></span>](#using-a-string-search)
5. [<span data-ttu-id="767bc-150">排序</span><span class="sxs-lookup"><span data-stu-id="767bc-150">Sorted</span></span>](#sorted)
6. [<span data-ttu-id="767bc-151">以有限的數量或全部</span><span class="sxs-lookup"><span data-stu-id="767bc-151">In a Limited Quantity or All</span></span>](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a><span data-ttu-id="767bc-152">檢視全部</span><span class="sxs-lookup"><span data-stu-id="767bc-152">See all</span></span>
<span data-ttu-id="767bc-153">連線之後，若要查看租用戶執行中屬性佈建錯誤的一般清單︰</span><span class="sxs-lookup"><span data-stu-id="767bc-153">Once connected, to see a general list of attribute provisioning errors in the tenant run:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

<span data-ttu-id="767bc-154">這會產生如下所示的結果︰</span><span class="sxs-lookup"><span data-stu-id="767bc-154">This produces a result like the following:</span></span>  
 <span data-ttu-id="767bc-155">![Get MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")</span><span class="sxs-lookup"><span data-stu-id="767bc-155">![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get-MsolDirSyncProvisioningError")</span></span>  

#### <a name="by-property-type"></a><span data-ttu-id="767bc-156">依屬性類型</span><span class="sxs-lookup"><span data-stu-id="767bc-156">By property type</span></span>
<span data-ttu-id="767bc-157">若要依屬性類型查看錯誤，請搭配 **UserPrincipalName** 或 **ProxyAddresses** 引數新增 **-PropertyName** 旗標︰</span><span class="sxs-lookup"><span data-stu-id="767bc-157">To see errors by property type, add the **-PropertyName** flag with the **UserPrincipalName** or **ProxyAddresses** argument:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

<span data-ttu-id="767bc-158">或</span><span class="sxs-lookup"><span data-stu-id="767bc-158">Or</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a><span data-ttu-id="767bc-159">依衝突的值</span><span class="sxs-lookup"><span data-stu-id="767bc-159">By conflicting value</span></span>
<span data-ttu-id="767bc-160">若要查看與特定屬性相關的錯誤，請新增 **-PropertyValue** 旗標 (新增此旗標時，必須一併使用 **-PropertyName**)：</span><span class="sxs-lookup"><span data-stu-id="767bc-160">To see errors relating to a specific property add the **-PropertyValue** flag (**-PropertyName** must be used as well when adding this flag):</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a><span data-ttu-id="767bc-161">使用字串搜尋</span><span class="sxs-lookup"><span data-stu-id="767bc-161">Using a string search</span></span>
<span data-ttu-id="767bc-162">若要進行廣泛的字串搜尋，請使用 **-SearchString** 旗標。</span><span class="sxs-lookup"><span data-stu-id="767bc-162">To do a broad string search use the **-SearchString** flag.</span></span> <span data-ttu-id="767bc-163">此旗標可以與上述所有旗標獨立使用，但一律為必要項目的 **-ErrorCategory PropertyConflict**除外︰</span><span class="sxs-lookup"><span data-stu-id="767bc-163">This can be used independently from all of the above flags, with the exception of **-ErrorCategory PropertyConflict**, which is always required:</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a><span data-ttu-id="767bc-164">以有限的數量或全部</span><span class="sxs-lookup"><span data-stu-id="767bc-164">In a limited quantity or all</span></span>
1. <span data-ttu-id="767bc-165">**MaxResults <Int>** 可用來將查詢的值數量限制為特定數目。</span><span class="sxs-lookup"><span data-stu-id="767bc-165">**MaxResults <Int>** can be used to limit the query to a specific number of values.</span></span>
2. <span data-ttu-id="767bc-166">**All** 可用於確保在有大量錯誤的情況下擷取所有的結果。</span><span class="sxs-lookup"><span data-stu-id="767bc-166">**All** can be used to ensure all results are retrieved in the case that a large number of errors exists.</span></span>

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a><span data-ttu-id="767bc-167">Office 365 系統管理入口網站</span><span class="sxs-lookup"><span data-stu-id="767bc-167">Office 365 admin portal</span></span>
<span data-ttu-id="767bc-168">您可以在 Office 365 系統管理中心檢視目錄同步處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="767bc-168">You can view directory synchronization errors in the Office 365 admin center.</span></span> <span data-ttu-id="767bc-169">Office 365 入口網站中的報告只會顯示有這些錯誤的 **User** 物件。</span><span class="sxs-lookup"><span data-stu-id="767bc-169">The report in the Office 365 portal only displays **User** objects that have these errors.</span></span> <span data-ttu-id="767bc-170">並不會顯示「群組」和「連絡人」之間的衝突相關資訊。</span><span class="sxs-lookup"><span data-stu-id="767bc-170">It does not show info about conflicts between **Groups** and **Contacts**.</span></span>

<span data-ttu-id="767bc-171">![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="767bc-171">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Active Users")</span></span>

<span data-ttu-id="767bc-172">如需有關如何在 Office 365 系統管理中心檢視目錄同步處理錯誤的指示，請參閱[在 Office 365 中識別目錄同步處理錯誤](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)。</span><span class="sxs-lookup"><span data-stu-id="767bc-172">For instructions on how to view directory synchronization errors in the Office 365 admin center, see [Identify directory synchronization errors in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).</span></span>

### <a name="identity-synchronization-error-report"></a><span data-ttu-id="767bc-173">身分識別同步處理錯誤報告</span><span class="sxs-lookup"><span data-stu-id="767bc-173">Identity synchronization error report</span></span>
<span data-ttu-id="767bc-174">當利用這個新行為處理具有重複屬性衝突的物件時，通知會包含在標準身分識別同步處理錯誤報告電子郵件中，而該電子郵件回傳送給租用戶的技術通知連絡人。</span><span class="sxs-lookup"><span data-stu-id="767bc-174">When an object with a duplicate attribute conflict is handled with this new behavior a notification is included in the standard Identity Synchronization Error Report email that is sent to the Technical Notification contact for the tenant.</span></span> <span data-ttu-id="767bc-175">不過，此行為有一項重大變更。</span><span class="sxs-lookup"><span data-stu-id="767bc-175">However, there is an important change in this behavior.</span></span> <span data-ttu-id="767bc-176">在過去，重複屬性衝突的相關資訊會包含在每個後續的錯誤報告中，直到解決衝突為止。</span><span class="sxs-lookup"><span data-stu-id="767bc-176">In the past, information about a duplicate attribute conflict would be included in every subsequent error report until the conflict was resolved.</span></span> <span data-ttu-id="767bc-177">利用這個新行為，給定衝突的錯誤通知只會出現一次 - 在衝突的屬性遭到隔離時。</span><span class="sxs-lookup"><span data-stu-id="767bc-177">With this new behavior, the error notification for a given conflict does only appear once- at the time the conflicting attribute is quarantined.</span></span>

<span data-ttu-id="767bc-178">ProxyAddress 衝突的電子郵件通知範例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="767bc-178">Here is an example of what the email notification looks like for a ProxyAddress conflict:</span></span>  
    <span data-ttu-id="767bc-179">![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="767bc-179">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

## <a name="resolving-conflicts"></a><span data-ttu-id="767bc-180">解決衝突</span><span class="sxs-lookup"><span data-stu-id="767bc-180">Resolving conflicts</span></span>
<span data-ttu-id="767bc-181">這些錯誤的疑難排解策略和解決技巧不得與過去處理重複屬性錯誤的方式不同。</span><span class="sxs-lookup"><span data-stu-id="767bc-181">Troubleshooting strategy and resolution tactics for these errors should not differ from the way duplicate attribute errors were handled in the past.</span></span> <span data-ttu-id="767bc-182">唯一的差別在於計時器工作將會掃掠服務端上的租用戶，以在衝突解決後，自動將有問題的屬性新增至適當的物件。</span><span class="sxs-lookup"><span data-stu-id="767bc-182">The only difference is that the timer task sweeps through the tenant on the service-side to automatically add the attribute in question to the proper object once the conflict is resolved.</span></span>

<span data-ttu-id="767bc-183">下列文章概述各種疑難排解和解決策略︰ [重複或無效的屬性會防止在 Office 365 中進行目錄同步作業](https://support.microsoft.com/kb/2647098)。</span><span class="sxs-lookup"><span data-stu-id="767bc-183">The following article outlines various troubleshooting and resolution strategies: [Duplicate or invalid attributes prevent directory synchronization in Office 365](https://support.microsoft.com/kb/2647098).</span></span>

## <a name="known-issues"></a><span data-ttu-id="767bc-184">已知問題</span><span class="sxs-lookup"><span data-stu-id="767bc-184">Known issues</span></span>
<span data-ttu-id="767bc-185">沒有任何已知問題會導致資料遺失或服務降級。</span><span class="sxs-lookup"><span data-stu-id="767bc-185">None of these known issues causes data loss or service degradation.</span></span> <span data-ttu-id="767bc-186">其中有幾個是美觀的問題，其他問題會導致擲回標準「恢復前」重複屬性錯誤，而不是隔離衝突屬性，而別的問題會導致特定錯誤需要額外的手動修復。</span><span class="sxs-lookup"><span data-stu-id="767bc-186">Several of them are aesthetic, others cause standard “*pre-resiliency*” duplicate attribute errors to be thrown instead of quarantining the conflict attribute, and another causes certain errors to require extra manual fix-up.</span></span>

<span data-ttu-id="767bc-187">**核心行為︰**</span><span class="sxs-lookup"><span data-stu-id="767bc-187">**Core behavior:**</span></span>

1. <span data-ttu-id="767bc-188">具有特定屬性組態的物件會繼續收到匯出錯誤，而不是將重複屬性隔離。</span><span class="sxs-lookup"><span data-stu-id="767bc-188">Objects with specific attribute configurations continue to receive export errors as opposed to the duplicate attribute(s) being quarantined.</span></span>  
   <span data-ttu-id="767bc-189">例如：</span><span class="sxs-lookup"><span data-stu-id="767bc-189">For example:</span></span>
   
    <span data-ttu-id="767bc-190">a.</span><span class="sxs-lookup"><span data-stu-id="767bc-190">a.</span></span> <span data-ttu-id="767bc-191">新使用者會在 AD 中以 UPN 為 **Joe@contoso.com**、ProxyAddress 為 **smtp:Joe@contoso.com** 的方式建立</span><span class="sxs-lookup"><span data-stu-id="767bc-191">New user is created in AD with a UPN of **Joe@contoso.com** and ProxyAddress **smtp:Joe@contoso.com**</span></span>
   
    <span data-ttu-id="767bc-192">b.</span><span class="sxs-lookup"><span data-stu-id="767bc-192">b.</span></span> <span data-ttu-id="767bc-193">此物件的屬性會與 ProxyAddress 為 **SMTP:Joe@contoso.com** 的現有「群組」發生衝突。</span><span class="sxs-lookup"><span data-stu-id="767bc-193">The properties of this object conflict with an existing Group, where ProxyAddress is **SMTP:Joe@contoso.com**.</span></span>
   
    <span data-ttu-id="767bc-194">c.</span><span class="sxs-lookup"><span data-stu-id="767bc-194">c.</span></span> <span data-ttu-id="767bc-195">匯出時，會擲回「ProxyAddress 衝突」 錯誤，而不是將衝突屬性隔離。</span><span class="sxs-lookup"><span data-stu-id="767bc-195">Upon export, a **ProxyAddress conflict** error is thrown instead of having the conflict attributes quarantined.</span></span> <span data-ttu-id="767bc-196">此作業會在每個後續的同步處理週期中重試，就如同在啟用恢復功能之前一樣。</span><span class="sxs-lookup"><span data-stu-id="767bc-196">The operation is retried upon each subsequent sync cycle, as it would have been before the resiliency feature was enabled.</span></span>
2. <span data-ttu-id="767bc-197">如果在內部部署上建立兩個具有相同 SMTP 位址的群組，則會在第一次嘗試時佈建失敗並發生標準的重複 **ProxyAddress** 錯誤。</span><span class="sxs-lookup"><span data-stu-id="767bc-197">If two Groups are created on-premises with the same SMTP address, one fails to provision on the first attempt with a standard duplicate **ProxyAddress** error.</span></span> <span data-ttu-id="767bc-198">不過，重複值會在下一個同步處理週期時被適當隔離。</span><span class="sxs-lookup"><span data-stu-id="767bc-198">However, the duplicate value is properly quarantined upon the next sync cycle.</span></span>

<span data-ttu-id="767bc-199">**Office 入口網站報告**：</span><span class="sxs-lookup"><span data-stu-id="767bc-199">**Office Portal Report**:</span></span>

1. <span data-ttu-id="767bc-200">UPN 衝突集中兩個物件的詳細錯誤訊息是相同的。</span><span class="sxs-lookup"><span data-stu-id="767bc-200">The detailed error message for two objects in a UPN conflict set is the same.</span></span> <span data-ttu-id="767bc-201">這表示它們都已變更 / 隔離 UPN，當事實上只有其中一個變更了資料。</span><span class="sxs-lookup"><span data-stu-id="767bc-201">This indicates that they have both had their UPN changed / quarantined, when in fact only a one of them had any data changed.</span></span>
2. <span data-ttu-id="767bc-202">UPN 衝突的詳細錯誤訊息會對已變更/隔離其 UPN 的使用者，顯示錯誤的 displayName。</span><span class="sxs-lookup"><span data-stu-id="767bc-202">The detailed error message for a UPN conflict shows the wrong displayName for a user who has had their UPN changed/quarantined.</span></span> <span data-ttu-id="767bc-203">例如：</span><span class="sxs-lookup"><span data-stu-id="767bc-203">For example:</span></span>
   
    <span data-ttu-id="767bc-204">a.</span><span class="sxs-lookup"><span data-stu-id="767bc-204">a.</span></span> <span data-ttu-id="767bc-205">**User A** 會先與 **UPN = User@contoso.com** 同步。</span><span class="sxs-lookup"><span data-stu-id="767bc-205">**User A** syncs up first with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="767bc-206">b.</span><span class="sxs-lookup"><span data-stu-id="767bc-206">b.</span></span> <span data-ttu-id="767bc-207">接著，會嘗試將 **User B** 與 User@contoso.comUPN =  同步。</span><span class="sxs-lookup"><span data-stu-id="767bc-207">**User B** is attempted to be synced up next with **UPN = User@contoso.com**.</span></span>
   
    <span data-ttu-id="767bc-208">c.</span><span class="sxs-lookup"><span data-stu-id="767bc-208">c.</span></span> <span data-ttu-id="767bc-209">**User B** 的 UPN 會變更為 **User1234@contoso.onmicrosoft.com**，而 **User@contoso.com** 會新增至 **DirSyncProvisioningErrors**。</span><span class="sxs-lookup"><span data-stu-id="767bc-209">**User B’s** UPN is changed to **User1234@contoso.onmicrosoft.com** and **User@contoso.com** is added to **DirSyncProvisioningErrors**.</span></span>
   
    <span data-ttu-id="767bc-210">d.</span><span class="sxs-lookup"><span data-stu-id="767bc-210">d.</span></span> <span data-ttu-id="767bc-211">**User B** 的錯誤訊息應指出 **User A** 已經有 **User@contoso.com** 作為 UPN，但顯示的卻是 **User B** 自己的 displayName。</span><span class="sxs-lookup"><span data-stu-id="767bc-211">The error message for **User B** should indicate that **User A** already has **User@contoso.com** as a UPN, but it shows **User B’s** own displayName.</span></span>

<span data-ttu-id="767bc-212">**身分識別同步處理錯誤報告**：</span><span class="sxs-lookup"><span data-stu-id="767bc-212">**Identity synchronization error report**:</span></span>

<span data-ttu-id="767bc-213">「如何解決此問題的步驟」的連結不正確：</span><span class="sxs-lookup"><span data-stu-id="767bc-213">The link for *steps on how to resolve this issue* is incorrect:</span></span>  
    <span data-ttu-id="767bc-214">![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="767bc-214">![Active Users](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Active Users")</span></span>  

<span data-ttu-id="767bc-215">它應該指向 [https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency)。</span><span class="sxs-lookup"><span data-stu-id="767bc-215">It should point to [https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).</span></span>

## <a name="see-also"></a><span data-ttu-id="767bc-216">另請參閱</span><span class="sxs-lookup"><span data-stu-id="767bc-216">See also</span></span>
* [<span data-ttu-id="767bc-217">Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="767bc-217">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="767bc-218">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="767bc-218">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="767bc-219">在 Office 365 中識別目錄同步處理錯誤</span><span class="sxs-lookup"><span data-stu-id="767bc-219">Identify directory synchronization errors in Office 365</span></span>](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

