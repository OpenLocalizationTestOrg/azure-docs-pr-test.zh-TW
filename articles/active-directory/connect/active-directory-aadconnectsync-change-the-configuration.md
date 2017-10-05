---
title: "Azure AD Connect 同步：在 Azure AD Connect 同步中進行組態變更 | Microsoft Docs"
description: "逐步解說如何對 Azure AD Connect 同步處理中的組態進行變更。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 63a7ae9d39e1a74294637172efd607ee41b2d69b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-make-a-change-to-the-default-configuration"></a><span data-ttu-id="ff38f-103">Azure AD Connect 同步處理：如何變更預設組態</span><span class="sxs-lookup"><span data-stu-id="ff38f-103">Azure AD Connect sync: How to make a change to the default configuration</span></span>
<span data-ttu-id="ff38f-104">本主題的目的在於逐步解說如何對 Azure AD Connect 同步處理中的預設組態進行變更。</span><span class="sxs-lookup"><span data-stu-id="ff38f-104">The purpose of this topic is to walk you through how to make changes to the default configuration in Azure AD Connect sync.</span></span> <span data-ttu-id="ff38f-105">其中提供一些常見案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="ff38f-105">It provides steps for some common scenarios.</span></span> <span data-ttu-id="ff38f-106">具備此知識，您應該能夠根據自己的商務規則對自己的組態進行一些簡單的變更。</span><span class="sxs-lookup"><span data-stu-id="ff38f-106">With this knowledge, you should be able to make some simple changes to your own configuration based on your own business rules.</span></span>

## <a name="synchronization-rules-editor"></a><span data-ttu-id="ff38f-107">同步處理規則編輯器</span><span class="sxs-lookup"><span data-stu-id="ff38f-107">Synchronization Rules Editor</span></span>
<span data-ttu-id="ff38f-108">同步處理規則編輯器用於查看和變更預設組態。</span><span class="sxs-lookup"><span data-stu-id="ff38f-108">The Synchronization Rules Editor is used to see and change the default configuration.</span></span> <span data-ttu-id="ff38f-109">您可以在 [開始] 功能表的 [Azure AD Connect]  群組之下找到它。</span><span class="sxs-lookup"><span data-stu-id="ff38f-109">You can find it in the Start Menu under the **Azure AD Connect** group.</span></span>  
<span data-ttu-id="ff38f-110">![內含同步處理規則編輯器的開始功能表](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-110">![Start Menu with Sync Rule Editor](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)</span></span>

<span data-ttu-id="ff38f-111">當您開啟它時，您會看到預設的現成可用規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-111">When you open it, you see the default out-of-box rules.</span></span>

![同步處理規則編輯器](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-the-editor"></a><span data-ttu-id="ff38f-113">在編輯器中瀏覽</span><span class="sxs-lookup"><span data-stu-id="ff38f-113">Navigating in the editor</span></span>
<span data-ttu-id="ff38f-114">編輯器頂端的下拉式清單可讓您快速找到特定規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-114">The drop-downs at the top of the editor allow you to quickly find a particular rule.</span></span> <span data-ttu-id="ff38f-115">例如，如果您想要查看已納入屬性 proxyAddresses 的規則，您可將下拉式清單變更如下︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-115">For example, if you want to see the rules where the attribute proxyAddresses is included, you would change the drop-downs to the following:</span></span>  
<span data-ttu-id="ff38f-116">![SRE 篩選](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-116">![SRE filtering](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)</span></span>  
<span data-ttu-id="ff38f-117">若要重設篩選並載入全新的組態，請按鍵盤上的 **F5** 。</span><span class="sxs-lookup"><span data-stu-id="ff38f-117">To reset filtering and load a fresh configuration, press **F5** on the keyboard.</span></span>

<span data-ttu-id="ff38f-118">右上方有 [新增規則] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff38f-118">To the top right, you have a button **Add new rule**.</span></span> <span data-ttu-id="ff38f-119">此按鈕用於建立您自己的自訂規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-119">This button is used to create your own custom rule.</span></span>

<span data-ttu-id="ff38f-120">底部有可供您處理選取的同步處理規則的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff38f-120">At the bottom, you have buttons for acting on a selected sync rule.</span></span> <span data-ttu-id="ff38f-121">[編輯] 和 [刪除] 會如您預期般執行。</span><span class="sxs-lookup"><span data-stu-id="ff38f-121">**Edit** and **Delete** do what you expect them to.</span></span> <span data-ttu-id="ff38f-122"> 會產生 PowerShell 指令碼以便重新建立同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-122">**Export** produces a PowerShell script for recreating the sync rule.</span></span> <span data-ttu-id="ff38f-123">此程序可讓您將同步處理規則從一部伺服器移到另一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff38f-123">This procedure allows you to move a sync rule from one server to another.</span></span>

## <a name="create-your-first-custom-rule"></a><span data-ttu-id="ff38f-124">建立您的第一個自訂規則</span><span class="sxs-lookup"><span data-stu-id="ff38f-124">Create your first custom rule</span></span>
<span data-ttu-id="ff38f-125">最常見的變更是屬性流程的變更。</span><span class="sxs-lookup"><span data-stu-id="ff38f-125">The most common change is changes to the attribute flows.</span></span> <span data-ttu-id="ff38f-126">您來源目錄中的資料可能不會與 Azure AD 中的一樣。</span><span class="sxs-lookup"><span data-stu-id="ff38f-126">The data in your source directory might not be as in Azure AD.</span></span> <span data-ttu-id="ff38f-127">在本節的範例中，您要確保使用者的名稱一律為 **適當的大小寫**。</span><span class="sxs-lookup"><span data-stu-id="ff38f-127">In the example in this section, you want to make sure the given name of a user is always in **Proper case**.</span></span>

### <a name="disable-the-scheduler"></a><span data-ttu-id="ff38f-128">停用排程器</span><span class="sxs-lookup"><span data-stu-id="ff38f-128">Disable the scheduler</span></span>
<span data-ttu-id="ff38f-129">[排程器](active-directory-aadconnectsync-feature-scheduler.md) 預設會每隔 30 分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="ff38f-129">The [scheduler](active-directory-aadconnectsync-feature-scheduler.md) runs every 30 minutes by default.</span></span> <span data-ttu-id="ff38f-130">您要確保在您進行變更時，排程器未啟動，並疑難排解您的新規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-130">You want to make sure it is not starting while you are making changes and troubleshoot your new rules.</span></span> <span data-ttu-id="ff38f-131">若要暫時停用排程器，請啟動 PowerShell，然後執行 `Set-ADSyncScheduler -SyncCycleEnabled $false`</span><span class="sxs-lookup"><span data-stu-id="ff38f-131">To temporarily disable the scheduler, start PowerShell, and run `Set-ADSyncScheduler -SyncCycleEnabled $false`</span></span>

![停用排程器](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-the-rule"></a><span data-ttu-id="ff38f-133">建立規則</span><span class="sxs-lookup"><span data-stu-id="ff38f-133">Create the rule</span></span>
1. <span data-ttu-id="ff38f-134">按一下 [新增規則] 。</span><span class="sxs-lookup"><span data-stu-id="ff38f-134">Click **Add new rule**.</span></span>
2. <span data-ttu-id="ff38f-135">在 [說明] 頁面上輸入下列各項：</span><span class="sxs-lookup"><span data-stu-id="ff38f-135">On the **Description** page enter the following:</span></span>  
   <span data-ttu-id="ff38f-136">![輸入規則篩選](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-136">![Inbound rule filtering](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)</span></span>  
   * <span data-ttu-id="ff38f-137">名稱：賦予規則描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="ff38f-137">Name: Give the rule a descriptive name.</span></span>
   * <span data-ttu-id="ff38f-138">描述︰讓其他人可以了解規則用途的一些說明。</span><span class="sxs-lookup"><span data-stu-id="ff38f-138">Description: Some clarification so someone else can understand what the rule is for.</span></span>
   * <span data-ttu-id="ff38f-139">連接的系統︰可在其中找到物件的系統。</span><span class="sxs-lookup"><span data-stu-id="ff38f-139">Connected system: The system the object can be found in.</span></span> <span data-ttu-id="ff38f-140">在此案例中，請選取 [Active Directory 連接器]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-140">In this case, select the Active Directory Connector.</span></span>
   * <span data-ttu-id="ff38f-141">已連線的系統/Metaverse 物件類型︰分別選取 [使用者] 和 [人員]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-141">Connected System/Metaverse Object Type: Select **User** and **Person** respectively.</span></span>
   * <span data-ttu-id="ff38f-142">連結類型︰將此值變更為 [聯結] 。</span><span class="sxs-lookup"><span data-stu-id="ff38f-142">Link Type: Change this value to **Join**.</span></span>
   * <span data-ttu-id="ff38f-143">優先順序︰提供在系統中是唯一的值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-143">Precedence: Provide a value that is unique in the system.</span></span> <span data-ttu-id="ff38f-144">較低的數值表示優先順序較高。</span><span class="sxs-lookup"><span data-stu-id="ff38f-144">A lower numeric value indicates higher precedence.</span></span>
   * <span data-ttu-id="ff38f-145">標籤︰保留空白。</span><span class="sxs-lookup"><span data-stu-id="ff38f-145">Tag: Leave empty.</span></span> <span data-ttu-id="ff38f-146">只有 Microsoft 提供的現成可用規則應該在此方塊中填入值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-146">Only out-of-box rules from Microsoft should have this box populated with a value.</span></span>
3. <span data-ttu-id="ff38f-147">在 [範圍篩選器] 頁面上，輸入 **givenName ISNOTNULL**。</span><span class="sxs-lookup"><span data-stu-id="ff38f-147">On the **Scoping filter** page, enter **givenName ISNOTNULL**.</span></span>  
   <span data-ttu-id="ff38f-148">![輸入規則範圍篩選器](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-148">![Inbound rule scoping filter](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)</span></span>  
   <span data-ttu-id="ff38f-149">此區段用來定義應套用規則的物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-149">This section is used to define which objects the rule should apply to.</span></span> <span data-ttu-id="ff38f-150">如果保留空白，規則會套用到所有的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-150">If left empty, the rule would apply to all user objects.</span></span> <span data-ttu-id="ff38f-151">但會包括會議室、服務帳戶，以及其他非人員的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-151">But that would include conference rooms, service accounts, and other non-people user objects.</span></span>
4. <span data-ttu-id="ff38f-152">在 [聯結規則] 上，將它保留空白。</span><span class="sxs-lookup"><span data-stu-id="ff38f-152">On the **Join rules**, leave it empty.</span></span>
5. <span data-ttu-id="ff38f-153">在 [轉換] 頁面上，將 FlowType 變更為 [運算式]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-153">On the **Transformations** page, change the FlowType to **Expression**.</span></span> <span data-ttu-id="ff38f-154">選取目標屬性 **givenName**，並在 [來源] 中輸入 `PCase([givenName])`。</span><span class="sxs-lookup"><span data-stu-id="ff38f-154">Select the Target Attribute **givenName**, and in Source enter `PCase([givenName])`.</span></span>
   <span data-ttu-id="ff38f-155">![輸入規則轉換](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-155">![Inbound rule transformations](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)</span></span>  
   <span data-ttu-id="ff38f-156">同步處理引擎會區分函式名稱和屬性名稱的大小寫。</span><span class="sxs-lookup"><span data-stu-id="ff38f-156">The sync engine is case-sensitive both on the function name and the name of the attribute.</span></span> <span data-ttu-id="ff38f-157">如果您輸入錯誤，您會在新增規則時看到警告。</span><span class="sxs-lookup"><span data-stu-id="ff38f-157">If you type something wrong, you see a warning when you add the rule.</span></span> <span data-ttu-id="ff38f-158">編輯器可讓您儲存並繼續進行，因此您必須重新開啟規則並予以更正。</span><span class="sxs-lookup"><span data-stu-id="ff38f-158">The editor allows you to save and continue, so you would have to reopen the rule and correct the rule.</span></span>
6. <span data-ttu-id="ff38f-159">按一下 [新增] 以儲存規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-159">Click **Add** to save the rule.</span></span>

<span data-ttu-id="ff38f-160">新的自訂規則應與其他同步處理規則一起顯示在系統中。</span><span class="sxs-lookup"><span data-stu-id="ff38f-160">Your new custom rule should be visible with the other sync rules in the system.</span></span>

### <a name="verify-the-change"></a><span data-ttu-id="ff38f-161">驗證變更</span><span class="sxs-lookup"><span data-stu-id="ff38f-161">Verify the change</span></span>
<span data-ttu-id="ff38f-162">利用這項新變更，您可確保其如預期般運作，而且不會擲回任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="ff38f-162">With this new change, you want to make sure it is working as expected and is not throwing any errors.</span></span> <span data-ttu-id="ff38f-163">視您擁有的物件數目而言，有兩種不同的方式可執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="ff38f-163">Depending on the number of objects you have, there are two different ways to do this step.</span></span>

1. <span data-ttu-id="ff38f-164">在所有物件上執行完整同步處理</span><span class="sxs-lookup"><span data-stu-id="ff38f-164">Run a full sync on all objects</span></span>
2. <span data-ttu-id="ff38f-165">在單一物件上執行預覽和完整同步處理</span><span class="sxs-lookup"><span data-stu-id="ff38f-165">Run a preview and full sync on a single object</span></span>

<span data-ttu-id="ff38f-166">從 [開始] 功能表啟動 [同步處理服務]  。</span><span class="sxs-lookup"><span data-stu-id="ff38f-166">Start **Synchronization Service** from the start menu.</span></span> <span data-ttu-id="ff38f-167">本節中的步驟全都在此工具中執行。</span><span class="sxs-lookup"><span data-stu-id="ff38f-167">The steps in this section are all in this tool.</span></span>

1. <span data-ttu-id="ff38f-168">**所有物件的完整同步處理**</span><span class="sxs-lookup"><span data-stu-id="ff38f-168">**Full sync on all objects**</span></span>  
   <span data-ttu-id="ff38f-169">從 [動作] 中選取 [執行]  。</span><span class="sxs-lookup"><span data-stu-id="ff38f-169">Select **Connectors** at the top.</span></span> <span data-ttu-id="ff38f-170">識別您在前一節中進行變更的連接器，在此例中為 Active Directory 網域服務，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="ff38f-170">Identify the Connector you made a change to in the previous section, in this case the Active Directory Domain Services, and select it.</span></span> <span data-ttu-id="ff38f-171">從 [動作] 中選取 [執行]，然後選取 [完整同步處理] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-171">Select **Run** from Actions and select **Full Synchronization** and **OK**.</span></span>
   <span data-ttu-id="ff38f-172">![完整同步處理](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-172">![Full sync](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)</span></span>  
   <span data-ttu-id="ff38f-173">物件現已在 Metaverse 中更新。</span><span class="sxs-lookup"><span data-stu-id="ff38f-173">The objects are now updated in the metaverse.</span></span> <span data-ttu-id="ff38f-174">您現在想要查看 Metaverse 中的物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-174">You now want to look at the object in the metaverse.</span></span>
2. <span data-ttu-id="ff38f-175">**單一物件的預覽和完整同步處理**</span><span class="sxs-lookup"><span data-stu-id="ff38f-175">**Preview and full sync on a single object**</span></span>  
   <span data-ttu-id="ff38f-176">從 [動作] 中選取 [執行]  。</span><span class="sxs-lookup"><span data-stu-id="ff38f-176">Select **Connectors** at the top.</span></span> <span data-ttu-id="ff38f-177">識別您在前一節中進行變更的連接器，在此例中為 Active Directory 網域服務，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="ff38f-177">Identify the Connector you made a change to in the previous section, in this case the Active Directory Domain Services, and select it.</span></span> <span data-ttu-id="ff38f-178">選取 [搜尋連接器空間] 。</span><span class="sxs-lookup"><span data-stu-id="ff38f-178">Select **Search Connector Space**.</span></span> <span data-ttu-id="ff38f-179">使用範圍來尋找您要用來測試變更的物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-179">Use scope to find an object you want to use to test the change.</span></span> <span data-ttu-id="ff38f-180">選取物件，然後按一下 [預覽] 。</span><span class="sxs-lookup"><span data-stu-id="ff38f-180">Select the object and click **Preview**.</span></span> <span data-ttu-id="ff38f-181">在新的畫面中，選取 [認可預覽] 。</span><span class="sxs-lookup"><span data-stu-id="ff38f-181">In the new screen, select **Commit Preview**.</span></span>  
   <span data-ttu-id="ff38f-182">![Commit preview](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-182">![Commit preview](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)</span></span>  
   <span data-ttu-id="ff38f-183">變更現已認可至 Metaverse。</span><span class="sxs-lookup"><span data-stu-id="ff38f-183">The change is now committed to the metaverse.</span></span>

<span data-ttu-id="ff38f-184">**查看 Metaverse 中的物件**</span><span class="sxs-lookup"><span data-stu-id="ff38f-184">**Look at the object in the metaverse**</span></span>  
<span data-ttu-id="ff38f-185">您現在可挑選幾個範例物件，確定這是預期的值並已套用規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-185">You now want to pick a few sample objects to make sure the value is expected and that the rule applied.</span></span> <span data-ttu-id="ff38f-186">從頂端選取 [Metaverse 搜尋]  。</span><span class="sxs-lookup"><span data-stu-id="ff38f-186">Select **Metaverse Search** from the top.</span></span> <span data-ttu-id="ff38f-187">新增您需要的任何篩選，以尋找相關的物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-187">Add any filter you need to find the relevant objects.</span></span> <span data-ttu-id="ff38f-188">從搜尋結果中，開啟物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-188">From the search result, open an object.</span></span> <span data-ttu-id="ff38f-189">查看屬性值，同時在 [同步處理規則]  資料行中確認已如預期套用規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-189">Look at the attribute values and also verify in the **Sync Rules** column that the rule applied as expected.</span></span>  
<span data-ttu-id="ff38f-190">![Metaverse search](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-190">![Metaverse search](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)</span></span>  

### <a name="enable-the-scheduler"></a><span data-ttu-id="ff38f-191">停用排程器</span><span class="sxs-lookup"><span data-stu-id="ff38f-191">Enable the scheduler</span></span>
<span data-ttu-id="ff38f-192">如果一切如同預期，您可以再次啟用排程器。</span><span class="sxs-lookup"><span data-stu-id="ff38f-192">If everything is as expected, you can enable the scheduler again.</span></span> <span data-ttu-id="ff38f-193">從 PowerShell，執行 `Set-ADSyncScheduler -SyncCycleEnabled $true`。</span><span class="sxs-lookup"><span data-stu-id="ff38f-193">From PowerShell, run `Set-ADSyncScheduler -SyncCycleEnabled $true`.</span></span>

## <a name="other-common-attribute-flow-changes"></a><span data-ttu-id="ff38f-194">其他常見屬性流程變更</span><span class="sxs-lookup"><span data-stu-id="ff38f-194">Other common attribute flow changes</span></span>
<span data-ttu-id="ff38f-195">上一節說明如何變更屬性流程。</span><span class="sxs-lookup"><span data-stu-id="ff38f-195">The previous section described how to make changes to an attribute flow.</span></span> <span data-ttu-id="ff38f-196">本節提供了一些其他的範例。</span><span class="sxs-lookup"><span data-stu-id="ff38f-196">In this section, some additional examples are provided.</span></span> <span data-ttu-id="ff38f-197">如何建立同步處理規則的步驟已縮減，但您可以在上一節中找到完整的步驟。</span><span class="sxs-lookup"><span data-stu-id="ff38f-197">The steps for how to create the sync rule is abbreviated, but you can find the full steps in the previous section.</span></span>

### <a name="use-another-attribute-than-the-default"></a><span data-ttu-id="ff38f-198">使用預設以外的其他屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-198">Use another attribute than the default</span></span>
<span data-ttu-id="ff38f-199">Fabrikam 中有對名字、姓氏和顯示名稱使用當地字母的樹系。</span><span class="sxs-lookup"><span data-stu-id="ff38f-199">At Fabrikam, there is a forest where the local alphabet is used for given name, surname, and display name.</span></span> <span data-ttu-id="ff38f-200">在擴充屬性中可以找到以拉丁字母表示的這些屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-200">The Latin character representation of these attributes can be found in the extension attributes.</span></span> <span data-ttu-id="ff38f-201">在 Azure AD 和 Office 365 中建立全域通訊清單時，組織反而想要使用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-201">When building the global address list in Azure AD and Office 365, the organization wants these attributes to be used instead.</span></span>

<span data-ttu-id="ff38f-202">在使用預設組態時，當地樹系中的物件看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ff38f-202">With a default configuration, an object from the local forest looks like this:</span></span>  
![屬性流程 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

<span data-ttu-id="ff38f-204">若要建立具有其他屬性流程的規則，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="ff38f-204">To create a rule with other attribute flows, do the following:</span></span>

* <span data-ttu-id="ff38f-205">從 [開始] 功能表啟動 [同步處理規則編輯器]  。</span><span class="sxs-lookup"><span data-stu-id="ff38f-205">Start **Synchronization Rule Editor** from the start menu.</span></span>
* <span data-ttu-id="ff38f-206">在左側依然選取 [輸入] 的情況下，按一下 [新增規則] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff38f-206">With **Inbound** still selected to the left, click the button **Add new rule**.</span></span>
* <span data-ttu-id="ff38f-207">賦予規則名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="ff38f-207">Give the rule a name and description.</span></span> <span data-ttu-id="ff38f-208">選取內部部署 Active Directory 和相關的物件類型。</span><span class="sxs-lookup"><span data-stu-id="ff38f-208">Select the on-premises Active Directory and the relevant object types.</span></span> <span data-ttu-id="ff38f-209">在 [連結類型] 中，選取 [聯結]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-209">In **Link Type**, select **Join**.</span></span> <span data-ttu-id="ff38f-210">為優先順序挑選一個其他規則還沒使用的數字。</span><span class="sxs-lookup"><span data-stu-id="ff38f-210">For precedence, pick a number that is not used by another rule.</span></span> <span data-ttu-id="ff38f-211">現成可用的規則是從 100 開始，因此此範例可以使用 50 這個值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-211">The out-of-box rules start with 100, so the value 50 can be used in this example.</span></span>
  <span data-ttu-id="ff38f-212">![屬性流程 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-212">![Attribute flow 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)</span></span>
* <span data-ttu-id="ff38f-213">將範圍留空 (也就是，應該套用到樹系中的所有使用者物件)。</span><span class="sxs-lookup"><span data-stu-id="ff38f-213">Leave scope empty (that is, should apply to all user objects in the forest).</span></span>
* <span data-ttu-id="ff38f-214">將聯結規則留空 (也就是，讓現成可用的規則處理任何聯結)。</span><span class="sxs-lookup"><span data-stu-id="ff38f-214">Leave join rules empty (that is, let the out-of-box rule handle any joins).</span></span>
* <span data-ttu-id="ff38f-215">在 [轉換] 中，建立下列流程：</span><span class="sxs-lookup"><span data-stu-id="ff38f-215">In Transformations, create the following flows:</span></span>  
  ![屬性流程 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* <span data-ttu-id="ff38f-217">按一下 [新增] 以儲存規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-217">Click **Add** to save the rule.</span></span>
* <span data-ttu-id="ff38f-218">移至 [同步處理服務管理員] 。</span><span class="sxs-lookup"><span data-stu-id="ff38f-218">Go to **Synchronization Service Manager**.</span></span> <span data-ttu-id="ff38f-219">在 [連接器] 上，選取我們已在其中新增規則的連接器。</span><span class="sxs-lookup"><span data-stu-id="ff38f-219">On **Connectors**, select the Connector where we added the rule.</span></span> <span data-ttu-id="ff38f-220">依序選取 [執行] 和 [完整同步處理]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-220">Select **Run**, and **Full Synchronization**.</span></span> <span data-ttu-id="ff38f-221">完整同步處理會使用目前的規則重新計算所有物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-221">A Full Synchronization recalculates all objects using the current rules.</span></span>

<span data-ttu-id="ff38f-222">這是具有此自訂規則之相同物件的結果：</span><span class="sxs-lookup"><span data-stu-id="ff38f-222">This is the result for the same object with this custom rule:</span></span>  
![屬性流程 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a><span data-ttu-id="ff38f-224">屬性的長度</span><span class="sxs-lookup"><span data-stu-id="ff38f-224">Length of attributes</span></span>
<span data-ttu-id="ff38f-225">字串屬性預設會設定為可索引，且最大長度為 448 個字元。</span><span class="sxs-lookup"><span data-stu-id="ff38f-225">String attributes are by default set to be indexable and the maximum length is 448 characters.</span></span> <span data-ttu-id="ff38f-226">如果您使用的字串屬性可能包含更多字元，則確定在屬性流程中包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="ff38f-226">If you are working with string attributes that might contain more, then make sure to include the following in the attribute flow:</span></span>  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-the-userprincipalsuffix"></a><span data-ttu-id="ff38f-227">變更 userPrincipalSuffix</span><span class="sxs-lookup"><span data-stu-id="ff38f-227">Changing the userPrincipalSuffix</span></span>
<span data-ttu-id="ff38f-228">由於使用者未必會知道 Active Directory 中的 userPrincipalName 屬性，因此這個屬性可能不適合做為登入識別碼。</span><span class="sxs-lookup"><span data-stu-id="ff38f-228">The userPrincipalName attribute in Active Directory is not always known by the users and might not be suitable as the sign-in ID.</span></span> <span data-ttu-id="ff38f-229">Azure AD Connect 同步處理安裝精靈允許挑選不同的屬性，例如 mail。</span><span class="sxs-lookup"><span data-stu-id="ff38f-229">The Azure AD Connect sync installation wizard allows picking a different attribute, for example mail.</span></span> <span data-ttu-id="ff38f-230">但是在某些情況下必須計算屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-230">But in some cases the attribute must be calculated.</span></span> <span data-ttu-id="ff38f-231">例如，Contoso 公司有兩個 Azure AD 目錄，一個用於生產環境，一個用於測試。</span><span class="sxs-lookup"><span data-stu-id="ff38f-231">For example, the company Contoso has two Azure AD directories, one for production and one for testing.</span></span> <span data-ttu-id="ff38f-232">他們想讓其測試租用戶中的使用者在登入識別碼中使用其他後置詞。</span><span class="sxs-lookup"><span data-stu-id="ff38f-232">They want the users in their test tenant to use another suffix in the sign-in ID.</span></span>  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

<span data-ttu-id="ff38f-233">在此運算式中，取出第一個 @-sign 左邊的所有內容 (Word)，然後使用固定的字串串連。</span><span class="sxs-lookup"><span data-stu-id="ff38f-233">In this expression, take everything left of the first @-sign (Word) and concatenate with a fixed string.</span></span>

### <a name="convert-a-multi-value-to-a-single-value"></a><span data-ttu-id="ff38f-234">將多重值轉換成單一值</span><span class="sxs-lookup"><span data-stu-id="ff38f-234">Convert a multi-value to a single-value</span></span>
<span data-ttu-id="ff38f-235">Active Directory 中的某些屬性在結構描述中是多重值，但是在 [Active Directory 使用者和電腦] 中看起來是單一值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-235">Some attributes in Active Directory are multi-valued in the schema even though they look single valued in Active Directory Users and Computers.</span></span> <span data-ttu-id="ff38f-236">描述屬性是其中一個範例。</span><span class="sxs-lookup"><span data-stu-id="ff38f-236">An example is the description attribute.</span></span>  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

<span data-ttu-id="ff38f-237">在此運算式中，如果屬性有值，請取屬性中的第一個項目 (Item)、移除開頭和結尾的空格 (Trim)，然後保留字串中的前 448 個字元 (Left)。</span><span class="sxs-lookup"><span data-stu-id="ff38f-237">In this expression in case the attribute has a value, take the first item (Item) in the attribute, remove leading and trailing spaces (Trim), and then keep the first 448 characters (Left) in the string.</span></span>

### <a name="do-not-flow-an-attribute"></a><span data-ttu-id="ff38f-238">請勿傳送屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-238">Do not flow an attribute</span></span>
<span data-ttu-id="ff38f-239">如需本節案例的背景，請參閱 [控制屬性流程程序](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process)。</span><span class="sxs-lookup"><span data-stu-id="ff38f-239">For background on the scenario for this section, see [Control the attribute flow process](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).</span></span>

<span data-ttu-id="ff38f-240">有兩種方式可防止傳送屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-240">There are two ways to not flow an attribute.</span></span> <span data-ttu-id="ff38f-241">第一個可在安裝精靈中使用，而且可讓您 [移除選取的屬性](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering)。</span><span class="sxs-lookup"><span data-stu-id="ff38f-241">The first is available in the installation wizard and allows you to [remove selected attributes](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).</span></span> <span data-ttu-id="ff38f-242">如果您先前不曾同步處理該屬性，則適用這個選項。</span><span class="sxs-lookup"><span data-stu-id="ff38f-242">This option works if you have never synchronized the attribute before.</span></span> <span data-ttu-id="ff38f-243">不過，如果您已開始同步處理這個屬性，且稍後利用這個功能來移除它，則同步處理引擎會停止管理屬性，而現有的值會留在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ff38f-243">However, if you have started to synchronize this attribute and later remove it with this feature, then the sync engine stops managing the attribute and the existing values are left in Azure AD.</span></span>

<span data-ttu-id="ff38f-244">如果您想要移除屬性的值並確定未來不會傳送它，就需要改為建立自訂規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-244">If you want to remove the value of an attribute and make sure it does not flow in the future, you need create a custom rule instead.</span></span>

<span data-ttu-id="ff38f-245">在 Fabrikam，我們在同步處理到雲端的屬性中發現了一些不應該存在的屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-245">At Fabrikam, we have realized that some of the attributes we synchronize to the cloud should not be there.</span></span> <span data-ttu-id="ff38f-246">我們想要確定這些屬性會從 Azure AD 中移除。</span><span class="sxs-lookup"><span data-stu-id="ff38f-246">We want to make sure these attributes are removed from Azure AD.</span></span>  
![不正確的擴充屬性](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* <span data-ttu-id="ff38f-248">建立新的輸入同步處理規則並填入說明![說明](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-248">Create a new inbound Synchronization Rule and populate the description ![Descriptions](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)</span></span>
* <span data-ttu-id="ff38f-249">建立類型為 **Expression** 且來源為 **AuthoritativeNull** 的屬性流程。</span><span class="sxs-lookup"><span data-stu-id="ff38f-249">Create attribute flows of type **Expression** and with the source **AuthoritativeNull**.</span></span> <span data-ttu-id="ff38f-250">即使優先順序較低的同步處理規則會嘗試填入值，常值 **AuthoritativeNull** 還是會指出 MV 中的值應該是空的。</span><span class="sxs-lookup"><span data-stu-id="ff38f-250">The literal **AuthoritativeNull** indicates that the value should be empty in the MV even if a lower precedence sync rule tries to populate the value.</span></span>
  <span data-ttu-id="ff38f-251">![擴充屬性的轉換](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-251">![Transformation for Extension Attributes](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)</span></span>
* <span data-ttu-id="ff38f-252">儲存同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-252">Save the Sync Rule.</span></span> <span data-ttu-id="ff38f-253">啟動 [同步處理服務]、尋找連接器、選取 [執行] 和 [完整同步處理]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-253">Start **Synchronization Service**, find the Connector, select **Run**, and **Full Synchronization**.</span></span> <span data-ttu-id="ff38f-254">此步驟會重新計算所有屬性流程。</span><span class="sxs-lookup"><span data-stu-id="ff38f-254">This step recalculates all attribute flows.</span></span>
* <span data-ttu-id="ff38f-255">藉由搜尋連接器空間，來確認即將匯出所需的變更。</span><span class="sxs-lookup"><span data-stu-id="ff38f-255">Verify that the intended changes are about to be exported by searching the connector space.</span></span>
  <span data-ttu-id="ff38f-256">![分段刪除](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-256">![Staged delete](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)</span></span>

## <a name="create-rules-with-powershell"></a><span data-ttu-id="ff38f-257">使用 PowerShell 建立規則</span><span class="sxs-lookup"><span data-stu-id="ff38f-257">Create rules with PowerShell</span></span>
<span data-ttu-id="ff38f-258">當您只需要進行一些變更時，使用同步處理規則編輯器就足以完成工作。</span><span class="sxs-lookup"><span data-stu-id="ff38f-258">Using the sync rule editor works fine when you only have a few changes to make.</span></span> <span data-ttu-id="ff38f-259">如果您需要進行許多變更，則 PowerShell 可能是較好的選擇。</span><span class="sxs-lookup"><span data-stu-id="ff38f-259">If you need to make many changes, then PowerShell might be a better option.</span></span> <span data-ttu-id="ff38f-260">某些進階功能只有 PowerShell 才提供。</span><span class="sxs-lookup"><span data-stu-id="ff38f-260">Some advanced features are only available with PowerShell.</span></span>

### <a name="get-the-powershell-script-for-an-out-of-box-rule"></a><span data-ttu-id="ff38f-261">取得 PowerShell 指令碼，獲得可立即使用的內建規則</span><span class="sxs-lookup"><span data-stu-id="ff38f-261">Get the PowerShell script for an out-of-box rule</span></span>
<span data-ttu-id="ff38f-262">若要查看已建立內建規則的 PowerShell 指令碼，請在同步處理規則編輯器中選取規則，然後按一下 [匯出]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-262">To see the PowerShell script that created an out-of-box rule, select the rule in the sync rules editor and click **Export**.</span></span> <span data-ttu-id="ff38f-263">此動作會為您提供已建立規則的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ff38f-263">This action gives you the PowerShell script that created the rule.</span></span>

### <a name="advanced-precedence"></a><span data-ttu-id="ff38f-264">進階優先順序</span><span class="sxs-lookup"><span data-stu-id="ff38f-264">Advanced precedence</span></span>
<span data-ttu-id="ff38f-265">內建同步處理規則具有從 100 開始算起的優先順序值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-265">The out-of-box sync rules start with a precedence value of 100.</span></span> <span data-ttu-id="ff38f-266">如果您有許多樹系且需要進行許多自訂變更，那麼 99 同步處理規則可能不太夠。</span><span class="sxs-lookup"><span data-stu-id="ff38f-266">If you have many forests and you need to make many custom changes, then 99 sync rules might not be enough.</span></span>

<span data-ttu-id="ff38f-267">您可以指示同步處理引擎，指定要在內建規則前面插入其他規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-267">You can instruct the Sync Engine that you want additional rules inserted before the out-of-box rules.</span></span> <span data-ttu-id="ff38f-268">若要取得此行為，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-268">To get this behavior, follow these steps:</span></span>

1. <span data-ttu-id="ff38f-269">在同步處理規則編輯器中標記第一個內建同步處理規則 (此規則是 **In from AD-User Join**)，然後選取 [匯出]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-269">Mark the first out-of-box sync rule (this rule is the **In from AD-User Join**) in the sync rule editor and select **Export**.</span></span> <span data-ttu-id="ff38f-270">複製 SR 識別碼值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-270">Copy the SR Identifier value.</span></span>  
<span data-ttu-id="ff38f-271">![變更前的 PowerShell](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-271">![PowerShell before change](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)</span></span>  
2. <span data-ttu-id="ff38f-272">建立新的同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-272">Create the new sync rule.</span></span> <span data-ttu-id="ff38f-273">您可以使用同步處理規則編輯器來建立它。</span><span class="sxs-lookup"><span data-stu-id="ff38f-273">You can use the sync rule editor to create it.</span></span> <span data-ttu-id="ff38f-274">將規則匯出到 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ff38f-274">Export the rule to a PowerShell script.</span></span>
3. <span data-ttu-id="ff38f-275">在屬性 **PrecedenceBefore** 中，插入內建規則的識別碼值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-275">In the property **PrecedenceBefore**, insert the identifier value from the out-of-box rule.</span></span> <span data-ttu-id="ff38f-276">將 **Precedence** 設定為 **0**。</span><span class="sxs-lookup"><span data-stu-id="ff38f-276">Set the **Precedence** to **0**.</span></span> <span data-ttu-id="ff38f-277">確定 [識別碼] 屬性是唯一的，而且您沒有重複使用另一個規則的 GUID。</span><span class="sxs-lookup"><span data-stu-id="ff38f-277">Make sure the Identifier attribute is unique and you are not reusing a GUID from another rule.</span></span> <span data-ttu-id="ff38f-278">此外，請確定 **ImmutableTag** 屬性未設定；此屬性只應該針對內建規則設定。</span><span class="sxs-lookup"><span data-stu-id="ff38f-278">Also make sure that the **ImmutableTag** property is not set; this property should only be set for an out-of-box rule.</span></span> <span data-ttu-id="ff38f-279">儲存 PowerShell 指令碼並執行它。</span><span class="sxs-lookup"><span data-stu-id="ff38f-279">Save the PowerShell script and run it.</span></span> <span data-ttu-id="ff38f-280">得到的結果是系統會對您的自訂規則指派優先順序值 100，而且所有其他內建規則會自此開始遞增。</span><span class="sxs-lookup"><span data-stu-id="ff38f-280">The result is that your custom rule is assigned the precedence value of 100 and all other out-of-box rules are incremented.</span></span>  
<span data-ttu-id="ff38f-281">![變更後的 PowerShell](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)</span><span class="sxs-lookup"><span data-stu-id="ff38f-281">![PowerShell after change](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)</span></span>  

<span data-ttu-id="ff38f-282">您可以依據自己的需求，擁有許多個使用相同 **PrecedenceBefore** 值的自訂同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-282">You can have many custom sync rules using the same **PrecedenceBefore** value when needed.</span></span>


## <a name="enable-synchronization-of-preferreddatalocation"></a><span data-ttu-id="ff38f-283">啟用 PreferredDataLocation 的同步處理</span><span class="sxs-lookup"><span data-stu-id="ff38f-283">Enable synchronization of PreferredDataLocation</span></span>
<span data-ttu-id="ff38f-284">Azure AD Connect 可對 1.1.524.0 版和更新版本之**使用者**物件的 **PreferredDataLocation** 屬性進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="ff38f-284">Azure AD Connect supports synchronization of the **PreferredDataLocation** attribute for **User** objects in version 1.1.524.0 and after.</span></span> <span data-ttu-id="ff38f-285">更具體地說，我們已導入下列變更︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-285">More specifically, following changes have been introduced:</span></span>

* <span data-ttu-id="ff38f-286">Azure AD 連接器中**使用者**物件類型的結構描述已擴充而納入了 PreferredDataLocation 屬性，此屬性是字串類型，且具備單一值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-286">The schema of the object type **User** in the Azure AD Connector is extended to include PreferredDataLocation attribute, which is of type string and is single-valued.</span></span>

* <span data-ttu-id="ff38f-287">Metaverse 中**人員**物件類型的結構描述已擴充而納入了 PreferredDataLocation 屬性，此屬性是字串類型，且具備單一值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-287">The schema of the object type **Person** in the Metaverse is extended to include PreferredDataLocation attribute, which is of type string and is single-valued.</span></span>

<span data-ttu-id="ff38f-288">內部部署 Active Directory 中沒有對應的 PreferredDataLocation 屬性，因此根據預設，PreferredDataLocation 屬性並未啟用同步處理。</span><span class="sxs-lookup"><span data-stu-id="ff38f-288">By default, the PreferredDataLocation attribute is not enabled for synchronization because there is no corresponding PreferredDataLocation attribute in on-premises Active Directory.</span></span> <span data-ttu-id="ff38f-289">您必須手動啟用同步處理。</span><span class="sxs-lookup"><span data-stu-id="ff38f-289">You must manually enable synchronization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff38f-290">Azure AD 目前允許使用 Azure AD PowerShell，直接設定「已同步處理的使用者物件」和「雲端使用者物件」上的 PreferredDataLocation 屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-290">Currently, Azure AD allows the PreferredDataLocation attribute on both synchronized User objects and cloud User objects to be directly configured using Azure AD PowerShell.</span></span> <span data-ttu-id="ff38f-291">在啟用了 PreferredDataLocation 屬性的同步處理之後，您就必須停止使用 Azure AD PowerShell 來設定**已同步處理的使用者物件**上的屬性，因為 Azure AD Connect 會根據內部部署 Active Directory 中的來源屬性值將這些物件加以覆寫。</span><span class="sxs-lookup"><span data-stu-id="ff38f-291">Once you have enabled synchronization of the PreferredDataLocation attribute, you must stop using Azure AD PowerShell to configure the attribute on **synchronized User objects** as Azure AD Connect will override them based on the source attribute values in on-premises Active Directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff38f-292">到了 2017 年 9 月 1 日時，Azure AD 就不會再允許使用 Azure AD PowerShell，來直接設定**已同步處理的使用者物件**上的 PreferredDataLocation 屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-292">On September 1 2017, Azure AD will no longer allow the PreferredDataLocation attribute on **synchronized User objects** to be directly configured using Azure AD PowerShell.</span></span> <span data-ttu-id="ff38f-293">若要設定「已同步處理的使用者物件」上的 PreferredLocation 屬性，您就只能使用 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="ff38f-293">To configure PreferredLocation attribute on synchronized User objects, you must use Azure AD Connect only.</span></span>

<span data-ttu-id="ff38f-294">在啟用 PreferredDataLocation 屬性的同步處理之前，您必須︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-294">Before enabling synchronization of the PreferredDataLocation attribute, you must:</span></span>

 * <span data-ttu-id="ff38f-295">首先，決定要使用哪個內部部署 Active Directory 屬性來作為來源屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-295">First, decide which on-premises Active Directory attribute to be used as the source attribute.</span></span> <span data-ttu-id="ff38f-296">此屬性的類型必須是**字串**，且具備**單一值**。</span><span class="sxs-lookup"><span data-stu-id="ff38f-296">It should be of type **string** and is **single-valued**.</span></span>

 * <span data-ttu-id="ff38f-297">如果您先前已使用 Azure AD PowerShell，來設定 Azure AD 中現有「已同步處理的使用者物件」上的 PreferredDataLocation 屬性，則必須將這些屬性值**向下移植**到內部部署 Active Directory 中對應的使用者物件內。</span><span class="sxs-lookup"><span data-stu-id="ff38f-297">If you have previously configured the PreferredDataLocation attribute on existing synchronized User objects in Azure AD using Azure AD PowerShell, you must **backport** the attribute values to the corresponding User objects in on-premises Active Directory.</span></span>
 
    > [!IMPORTANT]
    > <span data-ttu-id="ff38f-298">如果您未將這些屬性值向下移植到內部部署 Active Directory 中對應的使用者物件，Azure AD Connect 將會在 PreferredDataLocation 屬性的同步處理啟用時，移除 Azure AD 中現有的屬性值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-298">If you do not backport the attribute values to the corresponding User objects in on-premises Active Directory, Azure AD Connect will remove the existing attribute values in Azure AD when synchronization for the PreferredDataLocation attribute is enabled.</span></span>

 * <span data-ttu-id="ff38f-299">目前我們會建議您在至少幾個內部部署 AD 使用者物件上設定來源屬性，以供稍後用來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ff38f-299">It is recommended you configure the source attribute on at least a couple of on-premises AD User objects now, which can be used for verification later.</span></span>
 
<span data-ttu-id="ff38f-300">為 PreferredDataLocation 屬性啟用同步處理的步驟可總結為以下幾項︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-300">The steps to enable synchronization of the PreferredDataLocation attribute can be summarized as:</span></span>

1. <span data-ttu-id="ff38f-301">停用同步排程器，並確認沒有任何同步處理在進行中</span><span class="sxs-lookup"><span data-stu-id="ff38f-301">Disable sync scheduler and verify there is no synchronization in progress</span></span>

2. <span data-ttu-id="ff38f-302">在內部部署 AD 連接器結構描述中新增來源屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-302">Add the source attribute to the on-premises AD Connector schema</span></span>

3. <span data-ttu-id="ff38f-303">在 Azure AD 連接器結構描述中新增 PreferredDataLocation</span><span class="sxs-lookup"><span data-stu-id="ff38f-303">Add PreferredDataLocation to the Azure AD Connector schema</span></span>

4. <span data-ttu-id="ff38f-304">建立輸入同步處理規則，以從內部部署 Active Directory 傳輸屬性值</span><span class="sxs-lookup"><span data-stu-id="ff38f-304">Create an inbound synchronization rule to flow the attribute value from on-premises Active Directory</span></span>

5. <span data-ttu-id="ff38f-305">建立輸出同步處理規則，以將屬性值傳輸到 Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff38f-305">Create an outbound synchronization rule to flow the attribute value to Azure AD</span></span>

6. <span data-ttu-id="ff38f-306">執行完整的同步處理週期</span><span class="sxs-lookup"><span data-stu-id="ff38f-306">Run Full Synchronization cycle</span></span>

7. <span data-ttu-id="ff38f-307">啟用同步排程器</span><span class="sxs-lookup"><span data-stu-id="ff38f-307">Enable sync scheduler</span></span>

> [!NOTE]
> <span data-ttu-id="ff38f-308">本節的剩餘內容會詳述這些步驟。</span><span class="sxs-lookup"><span data-stu-id="ff38f-308">The rest of this section covers these steps in details.</span></span> <span data-ttu-id="ff38f-309">用來說明這些步驟的環境是某個 Azure AD 部署，其具有單一樹系拓撲，但沒有自訂的同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-309">They are described in the context of an Azure AD deployment with single-forest topology and without custom synchronization rules.</span></span> <span data-ttu-id="ff38f-310">如果您設定了多樹系拓撲和自訂同步處理規則，或具有預備伺服器，則需要據此現況調整這些步驟。</span><span class="sxs-lookup"><span data-stu-id="ff38f-310">If you have multi-forest topology, custom synchronization rules configured or have a staging server, you need to adjust the steps accordingly.</span></span>

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a><span data-ttu-id="ff38f-311">步驟 1：停用同步排程器，並確認沒有任何同步處理在進行中</span><span class="sxs-lookup"><span data-stu-id="ff38f-311">Step 1: Disable sync scheduler and verify there is no synchronization in progress</span></span>
<span data-ttu-id="ff38f-312">請確定在您更新同步處理規則時系統不會進行同步處理，以免將不想要的變更匯出到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="ff38f-312">Ensure no synchronization takes place while you are in the middle of updating synchronization rules to avoid unintended changes being exported to Azure AD.</span></span> <span data-ttu-id="ff38f-313">若要停用內建的同步排程器︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-313">To disable the built-in sync scheduler:</span></span>

 1. <span data-ttu-id="ff38f-314">在 Azure AD Connect 伺服器上啟動 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="ff38f-314">Start PowerShell session on the Azure AD Connect server.</span></span>

 2. <span data-ttu-id="ff38f-315">執行 Cmdlet 以停用排定的同步處理︰`Set-ADSyncScheduler -SyncCycleEnabled $false`</span><span class="sxs-lookup"><span data-stu-id="ff38f-315">Disable scheduled synchronization by running cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $false`</span></span>
 
 3. <span data-ttu-id="ff38f-316">移至 [開始] → [同步處理服務] 來啟動 **Synchronization Service Manager**。</span><span class="sxs-lookup"><span data-stu-id="ff38f-316">Start the **Synchronization Service Manager** by going to START → Synchronization Service.</span></span>
 
 4. <span data-ttu-id="ff38f-317">移至 [作業] 索引標籤，確認沒有任何作業是「進行中」狀態。</span><span class="sxs-lookup"><span data-stu-id="ff38f-317">Go to the **Operations** tab and confirm there is no operation whose status is *“in progress.”*</span></span>

![同步處理服務管理員 - 確認沒有進行中的作業](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema"></a><span data-ttu-id="ff38f-319">步驟 2：在內部部署 AD 連接器結構描述中新增來源屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-319">Step 2: Add the source attribute to the on-premises AD Connector schema</span></span>
<span data-ttu-id="ff38f-320">並非所有 AD 屬性都會匯入至內部部署 AD 連接器空間。</span><span class="sxs-lookup"><span data-stu-id="ff38f-320">Not all AD attributes are imported into the on-premises AD Connector Space.</span></span> <span data-ttu-id="ff38f-321">若要在所匯入屬性的清單中新增來源屬性︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-321">To add the source attribute to the list of the imported attributes:</span></span>

 1. <span data-ttu-id="ff38f-322">移至 Synchronization Service Manager 中的 [連接器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ff38f-322">Go to the **Connectors** tab in the Synchronization Service Manager.</span></span>
 
 2. <span data-ttu-id="ff38f-323">以滑鼠右鍵按一下 [內部部署 AD 連接器]，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-323">Right-click on the **on-premises AD Connector** and select **Properties**.</span></span>
 
 3. <span data-ttu-id="ff38f-324">在彈出的對話方塊中，移至 [選取屬性] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ff38f-324">In the pop-up dialog, go to the **Select Attributes** tab.</span></span>
 
 4. <span data-ttu-id="ff38f-325">確定您已在屬性清單中勾選來源屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-325">Make sure the source attribute is checked in the attribute list.</span></span>
 
 5. <span data-ttu-id="ff38f-326">按一下 [確定] 來進行儲存。</span><span class="sxs-lookup"><span data-stu-id="ff38f-326">Click **OK** to save.</span></span>

![在內部部署 AD 連接器結構描述中新增來源屬性](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-to-the-azure-ad-connector-schema"></a><span data-ttu-id="ff38f-328">步驟 3：在 Azure AD 連接器結構描述中新增 PreferredDataLocation</span><span class="sxs-lookup"><span data-stu-id="ff38f-328">Step 3: Add PreferredDataLocation to the Azure AD Connector schema</span></span>
<span data-ttu-id="ff38f-329">根據預設，系統不會在 Azure AD Connect 空間中匯入 PreferredDataLocation 屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-329">By default, the PreferredDataLocation attribute is not imported into the Azure AD Connect Space.</span></span> <span data-ttu-id="ff38f-330">若要在所匯入屬性的清單中新增 PreferredDataLocation 屬性︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-330">To add the PreferredDataLocation attribute to the list of imported attributes:</span></span>

 1. <span data-ttu-id="ff38f-331">移至 Synchronization Service Manager 中的 [連接器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ff38f-331">Go to the **Connectors** tab in the Synchronization Service Manager.</span></span>

 2. <span data-ttu-id="ff38f-332">以滑鼠右鍵按一下 [Azure AD 連接器]，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-332">Right-click on the **Azure AD Connector** and select **Properties**.</span></span>

 3. <span data-ttu-id="ff38f-333">在彈出的對話方塊中，移至 [選取屬性] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ff38f-333">In the pop-up dialog, go to the **Select Attributes** tab.</span></span>

 4. <span data-ttu-id="ff38f-334">確定您已在屬性清單中勾選 PreferredDataLocation 屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-334">Make sure the PreferredDataLocation attribute is checked in the attribute list.</span></span>

 5. <span data-ttu-id="ff38f-335">按一下 [確定] 來進行儲存。</span><span class="sxs-lookup"><span data-stu-id="ff38f-335">Click **OK** to save.</span></span>

![在 Azure AD 連接器結構描述中新增來源屬性](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-to-flow-the-attribute-value-from-on-premises-active-directory"></a><span data-ttu-id="ff38f-337">步驟 4：建立輸入同步處理規則，以從內部部署 Active Directory 傳輸屬性值</span><span class="sxs-lookup"><span data-stu-id="ff38f-337">Step 4: Create an inbound synchronization rule to flow the attribute value from on-premises Active Directory</span></span>
<span data-ttu-id="ff38f-338">輸入同步處理規則允許屬性值從內部部署 Active Directory 的來源屬性傳輸到 Metaverse︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-338">The inbound synchronization rule permits the attribute value to flow from the source attribute from on-premises Active Directory to the Metaverse:</span></span>

1. <span data-ttu-id="ff38f-339">移至 [開始] → [同步處理規則編輯器] 來啟動**同步處理規則編輯器**。</span><span class="sxs-lookup"><span data-stu-id="ff38f-339">Start the **Synchronization Rules Editor** by going to START → Synchronization Rules Editor.</span></span>

2. <span data-ttu-id="ff38f-340">將搜尋篩選條件的 [方向] 設定為 [輸入]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-340">Set the search filter **Direction** to be **Inbound**.</span></span>

3. <span data-ttu-id="ff38f-341">按一下 [新增規則] 按鈕以建立新的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-341">Click **Add new rule** button to create a new inbound rule.</span></span>

4. <span data-ttu-id="ff38f-342">在 [描述] 索引標籤下，提供下列設定︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-342">Under the **Description** tab, provide the following configuration:</span></span>
 
    | <span data-ttu-id="ff38f-343">屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-343">Attribute</span></span> | <span data-ttu-id="ff38f-344">值</span><span class="sxs-lookup"><span data-stu-id="ff38f-344">Value</span></span> | <span data-ttu-id="ff38f-345">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ff38f-345">Details</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="ff38f-346">名稱</span><span class="sxs-lookup"><span data-stu-id="ff38f-346">Name</span></span> | <span data-ttu-id="ff38f-347">提供名稱</span><span class="sxs-lookup"><span data-stu-id="ff38f-347">*Provide a name*</span></span> | <span data-ttu-id="ff38f-348">例如，「In from AD – User PreferredDataLocation」</span><span class="sxs-lookup"><span data-stu-id="ff38f-348">For example, *“In from AD – User PreferredDataLocation”*</span></span> |
    | <span data-ttu-id="ff38f-349">說明</span><span class="sxs-lookup"><span data-stu-id="ff38f-349">Description</span></span> | <span data-ttu-id="ff38f-350">提供描述</span><span class="sxs-lookup"><span data-stu-id="ff38f-350">*Provide a description*</span></span> |  |
    | <span data-ttu-id="ff38f-351">連線系統</span><span class="sxs-lookup"><span data-stu-id="ff38f-351">Connected System</span></span> | <span data-ttu-id="ff38f-352">選取內部部署 AD 連接器</span><span class="sxs-lookup"><span data-stu-id="ff38f-352">*Pick the on-premises AD connector*</span></span> |  |
    | <span data-ttu-id="ff38f-353">連線系統物件類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-353">Connected System Object Type</span></span> | <span data-ttu-id="ff38f-354">**使用者**</span><span class="sxs-lookup"><span data-stu-id="ff38f-354">**User**</span></span> |  |
    | <span data-ttu-id="ff38f-355">Metaverse 物件類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-355">Metaverse Object Type</span></span> | <span data-ttu-id="ff38f-356">**人員**</span><span class="sxs-lookup"><span data-stu-id="ff38f-356">**Person**</span></span> |  |
    | <span data-ttu-id="ff38f-357">連結類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-357">Link Type</span></span> | <span data-ttu-id="ff38f-358">**Join**</span><span class="sxs-lookup"><span data-stu-id="ff38f-358">**Join**</span></span> |  |
    | <span data-ttu-id="ff38f-359">優先順序</span><span class="sxs-lookup"><span data-stu-id="ff38f-359">Precedence</span></span> | <span data-ttu-id="ff38f-360">選擇 1 - 99 之間的數字</span><span class="sxs-lookup"><span data-stu-id="ff38f-360">*Choose a number between 1 – 99*</span></span> | <span data-ttu-id="ff38f-361">1 - 99 已保留供自訂同步處理規則使用。</span><span class="sxs-lookup"><span data-stu-id="ff38f-361">1 – 99 is reserved for custom sync rules.</span></span> <span data-ttu-id="ff38f-362">請勿挑選已由其他同步處理規則使用的值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-362">Do not pick a value that is used by another synchronization rule.</span></span> |

5. <span data-ttu-id="ff38f-363">移至 [範圍篩選器] 索引標籤，並**使用下列子句來新增單一範圍篩選器群組**：</span><span class="sxs-lookup"><span data-stu-id="ff38f-363">Go to the **Scoping filter** tab and add a **single scoping filter group with the following clause**:</span></span>
 
    | <span data-ttu-id="ff38f-364">屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-364">Attribute</span></span> | <span data-ttu-id="ff38f-365">運算子</span><span class="sxs-lookup"><span data-stu-id="ff38f-365">Operator</span></span> | <span data-ttu-id="ff38f-366">值</span><span class="sxs-lookup"><span data-stu-id="ff38f-366">Value</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="ff38f-367">adminDescription</span><span class="sxs-lookup"><span data-stu-id="ff38f-367">adminDescription</span></span> | <span data-ttu-id="ff38f-368">NOTSTARTWITH</span><span class="sxs-lookup"><span data-stu-id="ff38f-368">NOTSTARTWITH</span></span> | <span data-ttu-id="ff38f-369">使用者\_</span><span class="sxs-lookup"><span data-stu-id="ff38f-369">User\_</span></span> | 
 
    <span data-ttu-id="ff38f-370">範圍篩選器會決定此輸入同步處理規則要套用至哪個內部部署 AD 物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-370">Scoping filter determines which on-premises AD objects this inbound synchronization rule is applied to.</span></span> <span data-ttu-id="ff38f-371">在此範例中，我們所使用的範圍篩選器和「In from AD – User Common」OOB 同步處理規則所使用的相同，這是為了避免系統將同步處理規則套用到透過 Azure AD 使用者回寫功能所建立的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-371">In this example, we use the same scoping filter used as *“In from AD – User Common”* OOB synchronization rule, which prevents the synchronization rule from being applied to User objects created through Azure AD User writeback feature.</span></span> <span data-ttu-id="ff38f-372">您可能需要根據 Azure AD Connect 部署來調整範圍篩選器。</span><span class="sxs-lookup"><span data-stu-id="ff38f-372">You may need to tweak the scoping filter according to your Azure AD Connect deployment.</span></span>

6. <span data-ttu-id="ff38f-373">移至 [轉換] 索引標籤，並實作下列轉換規則︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-373">Go to the **Transformation tab** and implement the following transformation rule:</span></span>
 
    | <span data-ttu-id="ff38f-374">流程類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-374">Flow Type</span></span> | <span data-ttu-id="ff38f-375">目標屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-375">Target Attribute</span></span> | <span data-ttu-id="ff38f-376">來源</span><span class="sxs-lookup"><span data-stu-id="ff38f-376">Source</span></span> | <span data-ttu-id="ff38f-377">套用一次</span><span class="sxs-lookup"><span data-stu-id="ff38f-377">Apply Once</span></span> | <span data-ttu-id="ff38f-378">合併類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-378">Merge Type</span></span> |
    | --- | --- | --- | --- | --- |
    | <span data-ttu-id="ff38f-379">直接</span><span class="sxs-lookup"><span data-stu-id="ff38f-379">Direct</span></span> | <span data-ttu-id="ff38f-380">PreferredDataLocation</span><span class="sxs-lookup"><span data-stu-id="ff38f-380">PreferredDataLocation</span></span> | <span data-ttu-id="ff38f-381">挑選來源屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-381">Pick the source attribute</span></span> | <span data-ttu-id="ff38f-382">未核取</span><span class="sxs-lookup"><span data-stu-id="ff38f-382">Unchecked</span></span> | <span data-ttu-id="ff38f-383">更新</span><span class="sxs-lookup"><span data-stu-id="ff38f-383">Update</span></span> |

7. <span data-ttu-id="ff38f-384">按一下 [新增] 來建立輸入規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-384">Click **Add** to create the inbound rule.</span></span>

![建立輸入同步處理規則](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-to-flow-the-attribute-value-to-azure-ad"></a><span data-ttu-id="ff38f-386">步驟 5：建立輸出同步處理規則，以將屬性值傳輸到 Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff38f-386">Step 5: Create an outbound synchronization rule to flow the attribute value to Azure AD</span></span>
<span data-ttu-id="ff38f-387">輸出同步處理規則允許屬性值從 Metaverse 傳輸到 Azure AD 中的 PreferredDataLocation 屬性︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-387">The outbound synchronization rule permits the attribute value to flow from the Metaverse to the PreferredDataLocation attribute in Azure AD:</span></span>

1. <span data-ttu-id="ff38f-388">移至**同步處理規則**編輯器。</span><span class="sxs-lookup"><span data-stu-id="ff38f-388">Go to the **Synchronization Rules** Editor.</span></span>

2. <span data-ttu-id="ff38f-389">將搜尋篩選條件的 [方向] 設定為 [輸出]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-389">Set the search filter **Direction** to be **Outbound**.</span></span>

3. <span data-ttu-id="ff38f-390">按一下 [新增規則] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff38f-390">Click **Add new rule** button.</span></span>

4. <span data-ttu-id="ff38f-391">在 [描述] 索引標籤下，提供下列設定︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-391">Under the **Description** tab, provide the following configuration:</span></span>

    | <span data-ttu-id="ff38f-392">屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-392">Attribute</span></span> | <span data-ttu-id="ff38f-393">值</span><span class="sxs-lookup"><span data-stu-id="ff38f-393">Value</span></span> | <span data-ttu-id="ff38f-394">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ff38f-394">Details</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="ff38f-395">名稱</span><span class="sxs-lookup"><span data-stu-id="ff38f-395">Name</span></span> | <span data-ttu-id="ff38f-396">提供名稱</span><span class="sxs-lookup"><span data-stu-id="ff38f-396">*Provide a name*</span></span> | <span data-ttu-id="ff38f-397">例如，「Out to AAD – User PreferredDataLocation」</span><span class="sxs-lookup"><span data-stu-id="ff38f-397">For example, “Out to AAD – User PreferredDataLocation”</span></span> |
    | <span data-ttu-id="ff38f-398">說明</span><span class="sxs-lookup"><span data-stu-id="ff38f-398">Description</span></span> | <span data-ttu-id="ff38f-399">提供描述</span><span class="sxs-lookup"><span data-stu-id="ff38f-399">*Provide a description*</span></span> |
    | <span data-ttu-id="ff38f-400">連線系統</span><span class="sxs-lookup"><span data-stu-id="ff38f-400">Connected System</span></span> | <span data-ttu-id="ff38f-401">選取 AAD 連接器</span><span class="sxs-lookup"><span data-stu-id="ff38f-401">*Select the AAD connector*</span></span> |
    | <span data-ttu-id="ff38f-402">連線系統物件類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-402">Connected System Object Type</span></span> | <span data-ttu-id="ff38f-403">User</span><span class="sxs-lookup"><span data-stu-id="ff38f-403">User</span></span> ||
    | <span data-ttu-id="ff38f-404">Metaverse 物件類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-404">Metaverse Object Type</span></span> | <span data-ttu-id="ff38f-405">**人員**</span><span class="sxs-lookup"><span data-stu-id="ff38f-405">**Person**</span></span> ||
    | <span data-ttu-id="ff38f-406">連結類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-406">Link Type</span></span> | <span data-ttu-id="ff38f-407">**Join**</span><span class="sxs-lookup"><span data-stu-id="ff38f-407">**Join**</span></span> ||
    | <span data-ttu-id="ff38f-408">優先順序</span><span class="sxs-lookup"><span data-stu-id="ff38f-408">Precedence</span></span> | <span data-ttu-id="ff38f-409">選擇 1 - 99 之間的數字</span><span class="sxs-lookup"><span data-stu-id="ff38f-409">*Choose a number between 1 – 99*</span></span> | <span data-ttu-id="ff38f-410">1 - 99 已保留供自訂同步處理規則使用。</span><span class="sxs-lookup"><span data-stu-id="ff38f-410">1 – 99 is reserved for custom sync rules.</span></span> <span data-ttu-id="ff38f-411">請勿挑選已由其他同步處理規則使用的值。</span><span class="sxs-lookup"><span data-stu-id="ff38f-411">YDo not pick a value that is used by another synchronization rule.</span></span> |

5. <span data-ttu-id="ff38f-412">移至 [範圍篩選器] 索引標籤，並**使用兩個子句來新增單一範圍篩選器群組**：</span><span class="sxs-lookup"><span data-stu-id="ff38f-412">Go to the **Scoping filter** tab and add a **single scoping filter group with two clauses**:</span></span>
 
    | <span data-ttu-id="ff38f-413">屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-413">Attribute</span></span> | <span data-ttu-id="ff38f-414">運算子</span><span class="sxs-lookup"><span data-stu-id="ff38f-414">Operator</span></span> | <span data-ttu-id="ff38f-415">值</span><span class="sxs-lookup"><span data-stu-id="ff38f-415">Value</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="ff38f-416">sourceObjectType</span><span class="sxs-lookup"><span data-stu-id="ff38f-416">sourceObjectType</span></span> | <span data-ttu-id="ff38f-417">EQUAL</span><span class="sxs-lookup"><span data-stu-id="ff38f-417">EQUAL</span></span> | <span data-ttu-id="ff38f-418">User</span><span class="sxs-lookup"><span data-stu-id="ff38f-418">User</span></span> |
    | <span data-ttu-id="ff38f-419">cloudMastered</span><span class="sxs-lookup"><span data-stu-id="ff38f-419">cloudMastered</span></span> | <span data-ttu-id="ff38f-420">NOTEQUAL</span><span class="sxs-lookup"><span data-stu-id="ff38f-420">NOTEQUAL</span></span> | <span data-ttu-id="ff38f-421">True</span><span class="sxs-lookup"><span data-stu-id="ff38f-421">True</span></span> |

    <span data-ttu-id="ff38f-422">範圍篩選器會決定此輸出同步處理規則要套用至哪個 Azure AD 物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-422">Scoping filter determines which Azure AD objects this outbound synchronization rule is applied to.</span></span> <span data-ttu-id="ff38f-423">在此範例中，我們會使用來自「Out to AD – User Identity」OOB 同步處理規則的同一個範圍篩選器。</span><span class="sxs-lookup"><span data-stu-id="ff38f-423">In this example, we use the same scoping filter from “Out to AD – User Identity” OOB synchronization rule.</span></span> <span data-ttu-id="ff38f-424">它可避免同步處理規則套用到並非從內部部署 Active Directory 同步過來的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-424">It prevents the synchronization rule from being applied to User objects which are not synchronized from on-premises Active Directory.</span></span> <span data-ttu-id="ff38f-425">您可能需要根據 Azure AD Connect 部署來調整範圍篩選器。</span><span class="sxs-lookup"><span data-stu-id="ff38f-425">You may need to tweak the scoping filter according to your Azure AD Connect deployment.</span></span>
    
6. <span data-ttu-id="ff38f-426">移至 [轉換] 索引標籤，並實作下列轉換規則︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-426">Go to the **Transformation** tab and implement the following transformation rule:</span></span>

    | <span data-ttu-id="ff38f-427">流程類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-427">Flow Type</span></span> | <span data-ttu-id="ff38f-428">目標屬性</span><span class="sxs-lookup"><span data-stu-id="ff38f-428">Target Attribute</span></span> | <span data-ttu-id="ff38f-429">來源</span><span class="sxs-lookup"><span data-stu-id="ff38f-429">Source</span></span> | <span data-ttu-id="ff38f-430">套用一次</span><span class="sxs-lookup"><span data-stu-id="ff38f-430">Apply Once</span></span> | <span data-ttu-id="ff38f-431">合併類型</span><span class="sxs-lookup"><span data-stu-id="ff38f-431">Merge Type</span></span> |
    | --- | --- | --- | --- | --- |
    | <span data-ttu-id="ff38f-432">直接</span><span class="sxs-lookup"><span data-stu-id="ff38f-432">Direct</span></span> | <span data-ttu-id="ff38f-433">PreferredDataLocation</span><span class="sxs-lookup"><span data-stu-id="ff38f-433">PreferredDataLocation</span></span> | <span data-ttu-id="ff38f-434">PreferredDataLocation</span><span class="sxs-lookup"><span data-stu-id="ff38f-434">PreferredDataLocation</span></span> | <span data-ttu-id="ff38f-435">未核取</span><span class="sxs-lookup"><span data-stu-id="ff38f-435">Unchecked</span></span> | <span data-ttu-id="ff38f-436">更新</span><span class="sxs-lookup"><span data-stu-id="ff38f-436">Update</span></span> |

7. <span data-ttu-id="ff38f-437">關閉 [新增] 來建立輸出規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-437">Close **Add** to create the outbound rule.</span></span>

![建立輸出同步處理規則](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a><span data-ttu-id="ff38f-439">步驟 6：執行完整的同步處理週期</span><span class="sxs-lookup"><span data-stu-id="ff38f-439">Step 6: Run Full Synchronization cycle</span></span>
<span data-ttu-id="ff38f-440">由於我們已在 AD 和 Azure AD 連接器結構描述中同時新增屬性，並導入了自訂同步處理規則，因此一般來說，我們必須經歷完整的同步處理週期。</span><span class="sxs-lookup"><span data-stu-id="ff38f-440">In general, full synchronization cycle is required since we have added new attributes to both the AD and Azure AD Connector schema, and introduced custom synchronization rules.</span></span> <span data-ttu-id="ff38f-441">建議您先驗證變更，再將它們匯出至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="ff38f-441">It is recommended that you verify the changes before exporting them to Azure AD.</span></span> <span data-ttu-id="ff38f-442">在手動執行構成完整同步處理週期的步驟時，您可以使用下列步驟來驗證變更。</span><span class="sxs-lookup"><span data-stu-id="ff38f-442">You can use the following steps to verify the changes while manually running the steps that make up a full synchronization cycle.</span></span> 

1. <span data-ttu-id="ff38f-443">在**內部部署 AD 連接器**上執行**完整匯入**步驟：</span><span class="sxs-lookup"><span data-stu-id="ff38f-443">Run **Full import** step on the **on-premises AD Connector**:</span></span>

   1. <span data-ttu-id="ff38f-444">移至 Synchronization Service Manager 中的 [作業] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ff38f-444">Go to the **Operations** tab in the Synchronization Service Manager.</span></span>

   2. <span data-ttu-id="ff38f-445">以滑鼠右鍵按一下 [內部部署 AD 連接器]，然後選取 [執行...]</span><span class="sxs-lookup"><span data-stu-id="ff38f-445">Right-click on the **on-premises AD Connector** and select **Run...**</span></span>

   3. <span data-ttu-id="ff38f-446">在彈出的對話方塊中選取 [完整匯入]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-446">In the pop-up dialog, select **Full Import** and click **OK**.</span></span>
    
   4. <span data-ttu-id="ff38f-447">等候作業完成。</span><span class="sxs-lookup"><span data-stu-id="ff38f-447">Wait for operation to complete.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff38f-448">如果所匯入屬性的清單中已包含來源屬性，您可以略過內部部署 AD 連接器上的完整匯入。</span><span class="sxs-lookup"><span data-stu-id="ff38f-448">You can skip Full Import on the on-premises AD Connector if the source attribute is already included in the list of imported attributes.</span></span> <span data-ttu-id="ff38f-449">換句話說，在[步驟 2：在內部部署 AD 連接器結構描述中新增來源屬性](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema)期間，您不必進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="ff38f-449">In other words, you did not have to make any change during [Step 2: Add the source attribute to the on-premises AD Connector schema](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).</span></span>

2. <span data-ttu-id="ff38f-450">在 **Azure AD 連接器**上執行**完整匯入**步驟：</span><span class="sxs-lookup"><span data-stu-id="ff38f-450">Run **Full import** step on the **Azure AD Connector**:</span></span>

   1. <span data-ttu-id="ff38f-451">以滑鼠右鍵按一下 [Azure AD 連接器]，然後選取 [執行...]</span><span class="sxs-lookup"><span data-stu-id="ff38f-451">Right-click on the **Azure AD Connector** and select **Run...**</span></span>

   2. <span data-ttu-id="ff38f-452">在彈出的對話方塊中選取 [完整匯入]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-452">In the pop-up dialog, select **Full Import** and click **OK**.</span></span>
   
   3. <span data-ttu-id="ff38f-453">等候作業完成。</span><span class="sxs-lookup"><span data-stu-id="ff38f-453">Wait for operation to complete.</span></span>

3. <span data-ttu-id="ff38f-454">驗證現有使用者物件上的同步處理規則變更︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-454">Verify the synchronization rule changes on an existing User object:</span></span>

<span data-ttu-id="ff38f-455">來自內部部署 Active Directory 的來源屬性和來自 Azure AD 的 PreferredDataLocation 已匯入個別的連接器空間。</span><span class="sxs-lookup"><span data-stu-id="ff38f-455">The source attribute from on-premises Active Directory and PreferredDataLocation from Azure AD have been imported into the respective Connecter Space.</span></span> <span data-ttu-id="ff38f-456">在繼續進行「完整同步處理」步驟之前，建議您先**預覽**內部部署 AD 連接器空間上的現有使用者物件。</span><span class="sxs-lookup"><span data-stu-id="ff38f-456">Before proceeding with Full Synchronization step, it is recommended that you do a **Preview** on an existing User object in the on-premises AD Connector Space.</span></span> <span data-ttu-id="ff38f-457">您所挑選的物件應該要填入來源屬性。</span><span class="sxs-lookup"><span data-stu-id="ff38f-457">The object you picked should have the source attribute populated.</span></span> <span data-ttu-id="ff38f-458">若能成功**預覽**到 Metaverse 中已填入 PreferredDataLocation，則表示您已正確設定同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="ff38f-458">A successful **Preview** with the PreferredDataLocation populated in the Metaverse is a good indicator that you have configured the synchronization rules correctly.</span></span> <span data-ttu-id="ff38f-459">如需如何進行**預覽**的相關資訊，請參閱[驗證變更](#verify-the-change)一節。</span><span class="sxs-lookup"><span data-stu-id="ff38f-459">For information about how to do a **Preview**, refer to section [Verify the change](#verify-the-change).</span></span>

4. <span data-ttu-id="ff38f-460">在**內部部署 AD 連接器**上執行**完整同步處理**步驟：</span><span class="sxs-lookup"><span data-stu-id="ff38f-460">Run **Full Synchronization** step on the **on-premises AD Connector**:</span></span>

   1. <span data-ttu-id="ff38f-461">以滑鼠右鍵按一下 [內部部署 AD 連接器]，然後選取 [執行...]</span><span class="sxs-lookup"><span data-stu-id="ff38f-461">Right-click on the **on-premises AD Connector** and select **Run...**</span></span>
  
   2. <span data-ttu-id="ff38f-462">在彈出的對話方塊中選取 [完整同步處理]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-462">In the pop-up dialog, select **Full Synchronization** and click **OK**.</span></span>
   
   3. <span data-ttu-id="ff38f-463">等候作業完成。</span><span class="sxs-lookup"><span data-stu-id="ff38f-463">Wait for operation to complete.</span></span>

5. <span data-ttu-id="ff38f-464">確認要對 Azure AD 執行的**擱置匯出**：</span><span class="sxs-lookup"><span data-stu-id="ff38f-464">Verify **Pending Exports** to Azure AD:</span></span>

   1. <span data-ttu-id="ff38f-465">以滑鼠右鍵按一下 [Azure AD 連接器]，然後選取 [搜尋連接器空間]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-465">Right-click on the **Azure AD Connector** and select **Search Connector Space**.</span></span>

   2. <span data-ttu-id="ff38f-466">在彈出的 [搜尋連接器空間] 對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="ff38f-466">In the Search Connector Space pop-up dialog:</span></span>

      1. <span data-ttu-id="ff38f-467">將 [範圍] 設定為 [擱置匯出]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-467">Set **Scope** to **Pending Export**.</span></span>
      
      2. <span data-ttu-id="ff38f-468">將 3 個核取方塊全部勾選，包括 [新增]、[修改] 和 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-468">Check all three checkboxes, including **Add, Modify, and Delete**.</span></span>
      
      3. <span data-ttu-id="ff38f-469">按一下 [搜尋] 按鈕以取得有變更要匯出的物件清單。</span><span class="sxs-lookup"><span data-stu-id="ff38f-469">Click the **Search** button to get the list of objects with changes to be exported.</span></span> <span data-ttu-id="ff38f-470">若要檢查給定物件的變更，請對物件按兩下。</span><span class="sxs-lookup"><span data-stu-id="ff38f-470">To examine the changes for a given object, double-click the object.</span></span>
      
      4. <span data-ttu-id="ff38f-471">確認變更符合預期。</span><span class="sxs-lookup"><span data-stu-id="ff38f-471">Verify the changes are expected.</span></span>

6. <span data-ttu-id="ff38f-472">在 **Azure AD 連接器**上執行**完整匯出**步驟</span><span class="sxs-lookup"><span data-stu-id="ff38f-472">Run **Export** step on the **Azure AD Connector**</span></span>
      
   1. <span data-ttu-id="ff38f-473">以滑鼠右鍵按一下 [Azure AD 連接器]，然後選取 [執行...]</span><span class="sxs-lookup"><span data-stu-id="ff38f-473">Right-click the **Azure AD Connector** and select **Run...**</span></span>
   
   2. <span data-ttu-id="ff38f-474">在彈出的 [執行連接器] 對話方塊中選取 [匯出]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ff38f-474">In the Run Connector pop-up dialog, select **Export** and click **OK**.</span></span>
   
   3. <span data-ttu-id="ff38f-475">等待「匯出至 Azure AD」完成。</span><span class="sxs-lookup"><span data-stu-id="ff38f-475">Wait for Export to Azure AD to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="ff38f-476">您可能會發現，Azure AD 連接器的步驟並未包含「完整同步處理」步驟和「匯出」步驟。</span><span class="sxs-lookup"><span data-stu-id="ff38f-476">You may notice that the steps do not include the Full Synchronization step and Export step on the Azure AD Connector.</span></span> <span data-ttu-id="ff38f-477">屬性值只會從內部部署 Active Directory 傳輸到 Azure AD，因此 Azure AD 不需要這些步驟。</span><span class="sxs-lookup"><span data-stu-id="ff38f-477">The steps are not required since the attribute values are flowing from on-premises Active Directory to Azure AD only.</span></span>

### <a name="step-7-re-enable-sync-scheduler"></a><span data-ttu-id="ff38f-478">步驟 7：重新啟用同步排程器</span><span class="sxs-lookup"><span data-stu-id="ff38f-478">Step 7: Re-enable sync scheduler</span></span>
<span data-ttu-id="ff38f-479">重新啟用內建的同步排程器︰</span><span class="sxs-lookup"><span data-stu-id="ff38f-479">Re-enable the built-in sync scheduler:</span></span>

1. <span data-ttu-id="ff38f-480">啟動 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="ff38f-480">Start PowerShell session.</span></span>

2. <span data-ttu-id="ff38f-481">執行 Cmdlet 以重新啟用排定的同步處理︰`Set-ADSyncScheduler -SyncCycleEnabled $true`</span><span class="sxs-lookup"><span data-stu-id="ff38f-481">Re-enable scheduled synchronization by running cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $true`</span></span>



## <a name="next-steps"></a><span data-ttu-id="ff38f-482">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff38f-482">Next steps</span></span>
* <span data-ttu-id="ff38f-483">如需組態模型的詳細資訊，請參閱 [了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="ff38f-483">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="ff38f-484">如需運算式語言的詳細資訊，請參閱 [了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="ff38f-484">Read more about the expression language in [Understanding Declarative Provisioning Expressions](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).</span></span>

<span data-ttu-id="ff38f-485">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="ff38f-485">**Overview topics**</span></span>

* [<span data-ttu-id="ff38f-486">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="ff38f-486">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="ff38f-487">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff38f-487">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
