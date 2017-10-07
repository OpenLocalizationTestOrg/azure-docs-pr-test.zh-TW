---
title: "在 Azure AD 同步處理服務管理員 UI hello aaaConnectors |Microsoft 文件 '"
description: "了解 Azure AD Connect 同步處理服務管理員 hello 的 hello 連接器 索引標籤。"
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
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="471fd-103">使用連接器與 hello Azure AD Connect 同步處理服務管理員</span><span class="sxs-lookup"><span data-stu-id="471fd-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="471fd-105">hello 連接器 索引標籤是所有系統 hello 同步作業引擎已都連線到使用的 toomanage。</span><span class="sxs-lookup"><span data-stu-id="471fd-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="471fd-106">連接器動作</span><span class="sxs-lookup"><span data-stu-id="471fd-106">Connector actions</span></span>
| <span data-ttu-id="471fd-107">動作</span><span class="sxs-lookup"><span data-stu-id="471fd-107">Action</span></span> | <span data-ttu-id="471fd-108">註解</span><span class="sxs-lookup"><span data-stu-id="471fd-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="471fd-109">建立</span><span class="sxs-lookup"><span data-stu-id="471fd-109">Create</span></span> |<span data-ttu-id="471fd-110">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="471fd-110">Do not use.</span></span> <span data-ttu-id="471fd-111">連線 tooadditional AD 樹系，請使用 hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="471fd-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="471fd-112">屬性</span><span class="sxs-lookup"><span data-stu-id="471fd-112">Properties</span></span> |<span data-ttu-id="471fd-113">用於網域和 OU 篩選。</span><span class="sxs-lookup"><span data-stu-id="471fd-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="471fd-114">刪除</span><span class="sxs-lookup"><span data-stu-id="471fd-114">Delete</span></span>](#delete) |<span data-ttu-id="471fd-115">使用的 tooeither 刪除 hello hello 連接器空間或 toodelete 連接 tooa 樹系中的資料。</span><span class="sxs-lookup"><span data-stu-id="471fd-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="471fd-116">更新執行設定檔</span><span class="sxs-lookup"><span data-stu-id="471fd-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="471fd-117">除了網域篩選，執行任何動作 tooconfigure 這裡。</span><span class="sxs-lookup"><span data-stu-id="471fd-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="471fd-118">您可以使用此動作 toosee 已經設定執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="471fd-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="471fd-119">執行</span><span class="sxs-lookup"><span data-stu-id="471fd-119">Run</span></span> |<span data-ttu-id="471fd-120">使用的 toostart 單次執行的設定檔。</span><span class="sxs-lookup"><span data-stu-id="471fd-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="471fd-121">停止</span><span class="sxs-lookup"><span data-stu-id="471fd-121">Stop</span></span> |<span data-ttu-id="471fd-122">停止目前執行設定檔的連接器。</span><span class="sxs-lookup"><span data-stu-id="471fd-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="471fd-123">匯出連接器</span><span class="sxs-lookup"><span data-stu-id="471fd-123">Export Connector</span></span> |<span data-ttu-id="471fd-124">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="471fd-124">Do not use.</span></span> |
| <span data-ttu-id="471fd-125">匯入連接器</span><span class="sxs-lookup"><span data-stu-id="471fd-125">Import Connector</span></span> |<span data-ttu-id="471fd-126">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="471fd-126">Do not use.</span></span> |
| <span data-ttu-id="471fd-127">更新連接器</span><span class="sxs-lookup"><span data-stu-id="471fd-127">Update Connector</span></span> |<span data-ttu-id="471fd-128">請勿使用。</span><span class="sxs-lookup"><span data-stu-id="471fd-128">Do not use.</span></span> |
| <span data-ttu-id="471fd-129">重新整理結構描述</span><span class="sxs-lookup"><span data-stu-id="471fd-129">Refresh Schema</span></span> |<span data-ttu-id="471fd-130">重新整理 hello 快取結構描述。</span><span class="sxs-lookup"><span data-stu-id="471fd-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="471fd-131">這是慣用的 toouse hello 選項 hello 安裝精靈 中之後，也更新同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="471fd-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="471fd-132">搜尋連接器空間</span><span class="sxs-lookup"><span data-stu-id="471fd-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="471fd-133">使用 toofind 物件和太[遵循物件和其資料透過 hello 系統](#follow-an-object-and-its-data-through-the-system)。</span><span class="sxs-lookup"><span data-stu-id="471fd-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="471fd-134">刪除</span><span class="sxs-lookup"><span data-stu-id="471fd-134">Delete</span></span>
<span data-ttu-id="471fd-135">hello delete 動作用於兩個不同的項目。</span><span class="sxs-lookup"><span data-stu-id="471fd-135">hello delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="471fd-137">hello 選項**刪除連接器空間只**移除所有的資料，但保留 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="471fd-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="471fd-138">hello 選項**刪除連接器與連接器空間**hello 資料與 hello 組態中移除。</span><span class="sxs-lookup"><span data-stu-id="471fd-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="471fd-139">當您不想 tooconnect tooa 樹系不再使用此選項。</span><span class="sxs-lookup"><span data-stu-id="471fd-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="471fd-140">這兩個選項會同步處理所有物件，與更新 hello metaverse 物件。</span><span class="sxs-lookup"><span data-stu-id="471fd-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="471fd-141">此動作是長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="471fd-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="471fd-142">更新執行設定檔</span><span class="sxs-lookup"><span data-stu-id="471fd-142">Configure Run Profiles</span></span>
<span data-ttu-id="471fd-143">此選項可讓您執行設定檔設定連接器 toosee hello。</span><span class="sxs-lookup"><span data-stu-id="471fd-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="471fd-145">搜尋連接器空間</span><span class="sxs-lookup"><span data-stu-id="471fd-145">Search Connector Space</span></span>
<span data-ttu-id="471fd-146">hello 搜尋連接器空間動作是很有用的 toofind 物件和疑難排解資料問題。</span><span class="sxs-lookup"><span data-stu-id="471fd-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="471fd-148">先選取一個 [範圍] 。</span><span class="sxs-lookup"><span data-stu-id="471fd-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="471fd-149">您可以搜尋依據的資料 （RDN，DN，錨點，子樹狀目錄），或 hello 物件 （所有其他選項） 的狀態。</span><span class="sxs-lookup"><span data-stu-id="471fd-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="471fd-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="471fd-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="471fd-151">例如，如果您進行樹狀子目錄的搜尋，將會取得某一個 OU 中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="471fd-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="471fd-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="471fd-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="471fd-153">此方格中，您可以選取物件、 選取**屬性**，和[其後](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)從透過 hello metaverse，hello 來源連接器空間和 toohello 目標連接器空間。</span><span class="sxs-lookup"><span data-stu-id="471fd-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="471fd-154">變更 hello AD DS 帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="471fd-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="471fd-155">如果您變更 hello 帳戶密碼，hello 同步處理服務將不再能夠 tooimport/匯出變更 tooon 內部部署 AD。</span><span class="sxs-lookup"><span data-stu-id="471fd-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="471fd-156">您可能會看到下列 hello:</span><span class="sxs-lookup"><span data-stu-id="471fd-156">You may see hello following:</span></span>

- <span data-ttu-id="471fd-157">hello hello AD 連接器匯入/匯出步驟失敗，發生 「 否-start-認證 」 錯誤。</span><span class="sxs-lookup"><span data-stu-id="471fd-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="471fd-158">在 Windows 事件檢視器，hello 應用程式事件記錄檔包含具有事件識別碼 6000 和訊息的錯誤"hello 管理代理程式"contoso.com"無法 toorun 因為 hello 認證無效。"</span><span class="sxs-lookup"><span data-stu-id="471fd-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="471fd-159">tooresolve hello 發出使用 hello 下列更新 hello AD DS 使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="471fd-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="471fd-160">啟動 hello Synchronization Service Manager （開始 → 同步處理服務）。</span><span class="sxs-lookup"><span data-stu-id="471fd-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="471fd-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="471fd-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="471fd-162">移 toohello**連接器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="471fd-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="471fd-163">選取 hello 設定的 toouse hello AD DS 帳戶 AD 連接器。</span><span class="sxs-lookup"><span data-stu-id="471fd-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="471fd-164">選取 [動作] 下方的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="471fd-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="471fd-165">在 hello 快顯對話方塊中，選取連接 tooActive Directory 樹系：</span><span class="sxs-lookup"><span data-stu-id="471fd-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="471fd-166">hello 樹系名稱表示 hello 對應由內部部署 AD。</span><span class="sxs-lookup"><span data-stu-id="471fd-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="471fd-167">hello 使用者名稱表示 hello AD DS 帳戶用於進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="471fd-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="471fd-168">在 hello 密碼 文字方塊中輸入 hello hello AD DS 帳戶新密碼![Azure AD 連線同步加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="471fd-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="471fd-169">按一下 [確定] toosave hello 新密碼，然後重新啟動 hello 同步處理服務 tooremove hello 舊密碼從記憶體快取。</span><span class="sxs-lookup"><span data-stu-id="471fd-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="471fd-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="471fd-170">Next steps</span></span>
<span data-ttu-id="471fd-171">深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。</span><span class="sxs-lookup"><span data-stu-id="471fd-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="471fd-172">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="471fd-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
