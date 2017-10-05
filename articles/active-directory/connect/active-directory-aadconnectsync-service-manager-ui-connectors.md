---
title: "Azure AD Synchronization Service Manager UI 中的連接器 | Microsoft Docs'"
description: "了解 Azure AD Connect 的 Synchronization Service Manager 中的 [連接器] 索引標籤。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="5c236-103">使用連接器搭配 Auzre AD Connect Sync Service Manager</span><span class="sxs-lookup"><span data-stu-id="5c236-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="5c236-105">[連接器] 索引標籤可用來管理同步處理引擎連接的所有系統。</span><span class="sxs-lookup"><span data-stu-id="5c236-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="5c236-106">連接器動作</span><span class="sxs-lookup"><span data-stu-id="5c236-106">Connector actions</span></span>
| <span data-ttu-id="5c236-107">動作</span><span class="sxs-lookup"><span data-stu-id="5c236-107">Action</span></span> | <span data-ttu-id="5c236-108">註解</span><span class="sxs-lookup"><span data-stu-id="5c236-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="5c236-109">建立</span><span class="sxs-lookup"><span data-stu-id="5c236-109">Create</span></span> |<span data-ttu-id="5c236-110">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="5c236-110">Do not use.</span></span> <span data-ttu-id="5c236-111">若要連接到其他的 AD 樹系，請使用安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="5c236-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="5c236-112">屬性</span><span class="sxs-lookup"><span data-stu-id="5c236-112">Properties</span></span> |<span data-ttu-id="5c236-113">用於網域和 OU 篩選。</span><span class="sxs-lookup"><span data-stu-id="5c236-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="5c236-114">刪除</span><span class="sxs-lookup"><span data-stu-id="5c236-114">Delete</span></span>](#delete) |<span data-ttu-id="5c236-115">用來刪除連接器空間中的資料或刪除與樹系的連接。</span><span class="sxs-lookup"><span data-stu-id="5c236-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="5c236-116">更新執行設定檔</span><span class="sxs-lookup"><span data-stu-id="5c236-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="5c236-117">除了網域篩選以外，不會在此處進行任何設定。</span><span class="sxs-lookup"><span data-stu-id="5c236-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="5c236-118">您可以使用此動作來查看已設定的執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="5c236-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="5c236-119">執行</span><span class="sxs-lookup"><span data-stu-id="5c236-119">Run</span></span> |<span data-ttu-id="5c236-120">用來啟動設定檔的一次性執行。</span><span class="sxs-lookup"><span data-stu-id="5c236-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="5c236-121">停止</span><span class="sxs-lookup"><span data-stu-id="5c236-121">Stop</span></span> |<span data-ttu-id="5c236-122">停止目前執行設定檔的連接器。</span><span class="sxs-lookup"><span data-stu-id="5c236-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="5c236-123">匯出連接器</span><span class="sxs-lookup"><span data-stu-id="5c236-123">Export Connector</span></span> |<span data-ttu-id="5c236-124">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="5c236-124">Do not use.</span></span> |
| <span data-ttu-id="5c236-125">匯入連接器</span><span class="sxs-lookup"><span data-stu-id="5c236-125">Import Connector</span></span> |<span data-ttu-id="5c236-126">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="5c236-126">Do not use.</span></span> |
| <span data-ttu-id="5c236-127">更新連接器</span><span class="sxs-lookup"><span data-stu-id="5c236-127">Update Connector</span></span> |<span data-ttu-id="5c236-128">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="5c236-128">Do not use.</span></span> |
| <span data-ttu-id="5c236-129">重新整理結構描述</span><span class="sxs-lookup"><span data-stu-id="5c236-129">Refresh Schema</span></span> |<span data-ttu-id="5c236-130">重新整理快取的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5c236-130">Refreshes the cached schema.</span></span> <span data-ttu-id="5c236-131">最好是改為在安裝精靈中使用此選項，因為其也會更新同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="5c236-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="5c236-132">搜尋連接器空間</span><span class="sxs-lookup"><span data-stu-id="5c236-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="5c236-133">用來尋找物件，以及 [在整個系統中追隨物件及其資料](#follow-an-object-and-its-data-through-the-system)。</span><span class="sxs-lookup"><span data-stu-id="5c236-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="5c236-134">刪除</span><span class="sxs-lookup"><span data-stu-id="5c236-134">Delete</span></span>
<span data-ttu-id="5c236-135">刪除動作適用於兩個不同的用途。</span><span class="sxs-lookup"><span data-stu-id="5c236-135">The delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="5c236-137">[僅刪除連接器空間]  選項會移除所有資料，但保留組態。</span><span class="sxs-lookup"><span data-stu-id="5c236-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="5c236-138">[刪除連接器和連接器空間]  選項會移除資料及組態。</span><span class="sxs-lookup"><span data-stu-id="5c236-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="5c236-139">當您不想再連接到樹系時，可使用此選項。</span><span class="sxs-lookup"><span data-stu-id="5c236-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="5c236-140">這兩個選項會同步處理所有物件，並更新 metaverse 物件。</span><span class="sxs-lookup"><span data-stu-id="5c236-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="5c236-141">此動作是長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="5c236-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="5c236-142">更新執行設定檔</span><span class="sxs-lookup"><span data-stu-id="5c236-142">Configure Run Profiles</span></span>
<span data-ttu-id="5c236-143">此選項可讓您查看連接器所設定的執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="5c236-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="5c236-145">搜尋連接器空間</span><span class="sxs-lookup"><span data-stu-id="5c236-145">Search Connector Space</span></span>
<span data-ttu-id="5c236-146">尋找物件和疑難排解資料問題時，搜尋連接器空間動作非常有用。</span><span class="sxs-lookup"><span data-stu-id="5c236-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="5c236-148">先選取一個 [範圍] 。</span><span class="sxs-lookup"><span data-stu-id="5c236-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="5c236-149">您可以依據資料 (RDN、DN、錨點、子樹狀目錄) 或物件狀態 (所有其他選項) 進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="5c236-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="5c236-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="5c236-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="5c236-151">例如，如果您進行樹狀子目錄的搜尋，將會取得某一個 OU 中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="5c236-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="5c236-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="5c236-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="5c236-153">您可以從此格線選取物件、選取「屬性」，然後[跟隨物件](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)，從來源連接器空間、通過 Metaverse，再到目標連接器空間。</span><span class="sxs-lookup"><span data-stu-id="5c236-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="5c236-154">變更 AD DS 帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="5c236-154">Changing the AD DS account password</span></span>
<span data-ttu-id="5c236-155">如果您變更帳戶密碼，同步處理服務就再也無法匯入/匯出內部部署 AD 的變更。</span><span class="sxs-lookup"><span data-stu-id="5c236-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="5c236-156">這時您會看到下列情形：</span><span class="sxs-lookup"><span data-stu-id="5c236-156">You may see the following:</span></span>

- <span data-ttu-id="5c236-157">AD 連接器的匯入/匯出步驟失敗，並出現「no-start-credentials」錯誤。</span><span class="sxs-lookup"><span data-stu-id="5c236-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="5c236-158">Windows 事件檢視器底下的應用程式事件記錄會包含事件識別碼為 6000 的錯誤與「管理代理程式 "contoso.com" 無法執行，因為認證無效」的訊息。</span><span class="sxs-lookup"><span data-stu-id="5c236-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="5c236-159">若要解決此問題，請使用下列程序來更新 AD DS 使用者帳戶︰</span><span class="sxs-lookup"><span data-stu-id="5c236-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="5c236-160">啟動同步處理服務管理員 ([開始] → [同步處理服務])。</span><span class="sxs-lookup"><span data-stu-id="5c236-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="5c236-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="5c236-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="5c236-162">移至 [連接器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5c236-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="5c236-163">選取設定為使用 AD DS 帳戶的 AD 連接器。</span><span class="sxs-lookup"><span data-stu-id="5c236-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="5c236-164">選取 [動作] 下方的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="5c236-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="5c236-165">在快顯對話方塊中，選取 [連線至 Active Directory 樹系]：</span><span class="sxs-lookup"><span data-stu-id="5c236-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="5c236-166">樹系名稱會指出對應的內部部署 AD。</span><span class="sxs-lookup"><span data-stu-id="5c236-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="5c236-167">使用者名稱會指出用於同步處理服務的 AD DS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c236-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="5c236-168">在 [密碼] 文字方塊中輸入新的 AD DS 帳戶密碼 ![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="5c236-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="5c236-169">按一下 [確定] 以儲存新密碼，然後重新啟動同步處理服務，以從記憶體快取中移除舊密碼。</span><span class="sxs-lookup"><span data-stu-id="5c236-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="5c236-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c236-170">Next steps</span></span>
<span data-ttu-id="5c236-171">深入了解 [Azure AD Connect 同步](active-directory-aadconnectsync-whatis.md) 組態。</span><span class="sxs-lookup"><span data-stu-id="5c236-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="5c236-172">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="5c236-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
