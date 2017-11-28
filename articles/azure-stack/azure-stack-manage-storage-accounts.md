---
title: "aaaManage 堆疊 Azure 儲存體帳戶 |Microsoft 文件"
description: "了解 toofind，管理、 復原和回收堆疊 Azure 儲存體帳戶的方式"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="f487b-103">在 Azure Stack 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f487b-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="f487b-104">了解如何 toomanage 儲存體帳戶的 Azure 堆疊 toofind 復原，以及根據商務需求的儲存容量的回收。</span><span class="sxs-lookup"><span data-stu-id="f487b-104">Learn how toomanage storage accounts in Azure Stack toofind, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="f487b-105"><a name="find"></a>尋找儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f487b-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="f487b-106">hello hello 區域中的儲存體帳戶清單可以檢視由 Azure 堆疊中：</span><span class="sxs-lookup"><span data-stu-id="f487b-106">hello list of storage accounts in hello region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="f487b-107">在網際網路瀏覽器中，瀏覽至 https://adminportal.local.azurestack.external。</span><span class="sxs-lookup"><span data-stu-id="f487b-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="f487b-108">登入 toohello 堆疊 Azure 系統管理入口網站為雲端操作員 （使用您在部署期間所提供的認證）</span><span class="sxs-lookup"><span data-stu-id="f487b-108">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="f487b-109">Hello 預設儀表板 – 上尋找 hello**區域管理**清單，然後按一下您想要 tooexplore hello 區域。</span><span class="sxs-lookup"><span data-stu-id="f487b-109">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore.</span></span> <span data-ttu-id="f487b-110">例如 **(local**)。</span><span class="sxs-lookup"><span data-stu-id="f487b-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="f487b-111">選取**儲存體**從 hello**資源提供者**清單。</span><span class="sxs-lookup"><span data-stu-id="f487b-111">Select **Storage** from hello **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="f487b-112">現在，在 hello 儲存體資源提供者系統管理員 刀鋒視窗 – 向下捲動 hello**儲存體帳戶**索引標籤，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="f487b-112">Now, on hello storage Resource Provider administrator blade – scroll down to hello **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="f487b-113">hello 結果頁面是在該區域中的儲存體帳戶 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="f487b-113">hello resulting page is hello list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="f487b-114">根據預設，hello 前 10 個帳戶會顯示。</span><span class="sxs-lookup"><span data-stu-id="f487b-114">By default, hello first 10 accounts are displayed.</span></span> <span data-ttu-id="f487b-115">您可以按一下 hello 更多選擇 toofetch**載入更多**hello hello 清單底端的連結。</span><span class="sxs-lookup"><span data-stu-id="f487b-115">You can choose toofetch more by clicking hello  **Load more** link at hello bottom of hello list.</span></span>

<span data-ttu-id="f487b-116">或</span><span class="sxs-lookup"><span data-stu-id="f487b-116">OR</span></span>

<span data-ttu-id="f487b-117">如果您想要在特定的儲存體帳戶 – 您可以**篩選和 fetch hello 相關帳戶**只。</span><span class="sxs-lookup"><span data-stu-id="f487b-117">If you are interested in a particular storage account – you can **filter and fetch hello relevant accounts** only.</span></span>


<span data-ttu-id="f487b-118">**toofilter 帳戶：**</span><span class="sxs-lookup"><span data-stu-id="f487b-118">**toofilter for accounts:**</span></span>

1. <span data-ttu-id="f487b-119">按一下**篩選**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="f487b-119">Click **Filter** at hello top of hello blade.</span></span>
2. <span data-ttu-id="f487b-120">Hello 篩選刀鋒視窗中，它可讓您 toospecify**帳戶名稱**，**訂用帳戶 ID**或**狀態**toofine 微調 hello 清單的儲存體帳戶 toobe 顯示。</span><span class="sxs-lookup"><span data-stu-id="f487b-120">On hello Filter blade, it allows you toospecify **account name**, **subscription ID** or **status** toofine-tune hello list of storage accounts toobe displayed.</span></span> <span data-ttu-id="f487b-121">請適當地指定。</span><span class="sxs-lookup"><span data-stu-id="f487b-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="f487b-122">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="f487b-122">Click **Update**.</span></span> <span data-ttu-id="f487b-123">hello 清單應該據此重新整理。</span><span class="sxs-lookup"><span data-stu-id="f487b-123">hello list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="f487b-124">tooreset hello 篩選： 按一下**篩選**、 清除選取項目和更新。</span><span class="sxs-lookup"><span data-stu-id="f487b-124">tooreset hello filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="f487b-125">hello 搜尋 文字方塊中 （在 hello hello 儲存體帳戶清單刀鋒視窗頂端） 可讓您反白顯示 hello 帳戶清單中選取的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="f487b-125">hello search text box (on hello top of hello storage accounts list blade) lets you highlight hello selected text in hello list of accounts.</span></span> <span data-ttu-id="f487b-126">Hello 完整名稱或識別碼無法輕鬆地使用時，這是在 hello 案例中非常有用。</span><span class="sxs-lookup"><span data-stu-id="f487b-126">This is really handy in hello case when hello full name or id is not easily available.</span></span>

<span data-ttu-id="f487b-127">您可以使用任意文字 toohelp 在這裡找到您感興趣的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f487b-127">You can use free text here toohelp find hello account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="f487b-128">查看帳戶詳細資料</span><span class="sxs-lookup"><span data-stu-id="f487b-128">Look at account details</span></span>
<span data-ttu-id="f487b-129">一旦您找到您感興趣檢視的 hello 帳戶，您可以按一下 hello 特定帳戶 tooview 特定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f487b-129">Once you have located hello accounts you are interested in viewing, you can click hello particular account tooview certain details.</span></span> <span data-ttu-id="f487b-130">新刀鋒視窗會開啟與 hello 帳戶詳細資料這類： hello hello 帳戶、 建立時間、 位置等等的類型。</span><span class="sxs-lookup"><span data-stu-id="f487b-130">A new blade opens with hello account details such as: hello type of hello account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="f487b-131">復原已刪除的帳戶</span><span class="sxs-lookup"><span data-stu-id="f487b-131">Recover a deleted account</span></span>
<span data-ttu-id="f487b-132">您可能需要 toorecover 的情況下已刪除的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f487b-132">You may be in a situation where you need toorecover a deleted account.</span></span>

<span data-ttu-id="f487b-133">Azure 堆疊中沒有非常簡單的方式 toodo 的：</span><span class="sxs-lookup"><span data-stu-id="f487b-133">In Azure Stack there is a very simple way toodo that:</span></span>

1. <span data-ttu-id="f487b-134">瀏覽 toohello 儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="f487b-134">Browse toohello storage accounts list.</span></span> <span data-ttu-id="f487b-135">如需詳細資訊，請參閱本主題中的[尋找儲存體帳戶](#find)。</span><span class="sxs-lookup"><span data-stu-id="f487b-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="f487b-136">Hello 清單中，找出該特定的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f487b-136">Locate that particular account in hello list.</span></span> <span data-ttu-id="f487b-137">您可能需要 toofilter。</span><span class="sxs-lookup"><span data-stu-id="f487b-137">You may need toofilter.</span></span>
3. <span data-ttu-id="f487b-138">檢查 hello*狀態*的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f487b-138">Check hello *state* of hello account.</span></span> <span data-ttu-id="f487b-139">它應該指出 [已刪除]。</span><span class="sxs-lookup"><span data-stu-id="f487b-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="f487b-140">按一下以開啟刀鋒視窗中的帳戶詳細資料 hello hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f487b-140">Click hello account which opens hello account details blade.</span></span>
5. <span data-ttu-id="f487b-141">在這個刀鋒視窗中，找出 hello**復原**按鈕，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="f487b-141">On top of this blade, locate hello **Recover** button and click it.</span></span>
6. <span data-ttu-id="f487b-142">按一下**是**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="f487b-142">Click **Yes** tooconfirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="f487b-143">hello 正在復原現在*...處理稍候*是否有指出已順利完成。</span><span class="sxs-lookup"><span data-stu-id="f487b-143">hello recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="f487b-144">您也可以按一下上方的 hello 入口網站來檢視進度指示 hello hello"鈴鐺 」 圖示。</span><span class="sxs-lookup"><span data-stu-id="f487b-144">You can also click hello “bell” icon at hello top of hello portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="f487b-145">Hello 復原帳戶已順利同步處理，才能使用一次。</span><span class="sxs-lookup"><span data-stu-id="f487b-145">Once hello recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="f487b-146">注意事項</span><span class="sxs-lookup"><span data-stu-id="f487b-146">Some Gotchas</span></span>
* <span data-ttu-id="f487b-147">已刪除的帳戶顯示 [不再保留] 狀態。</span><span class="sxs-lookup"><span data-stu-id="f487b-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="f487b-148">這表示已超過 hello 保留期限 hello 刪除帳戶，而且可能無法復原。</span><span class="sxs-lookup"><span data-stu-id="f487b-148">This means that hello deleted account has exceeded hello retention period and may not be recoverable.</span></span>
* <span data-ttu-id="f487b-149">已刪除的帳戶不會顯示 hello 帳戶清單中。</span><span class="sxs-lookup"><span data-stu-id="f487b-149">Your deleted account does not show in hello accounts list.</span></span>
  
  <span data-ttu-id="f487b-150">這可能表示 hello 刪除帳戶已經過記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="f487b-150">This could mean that hello deleted account has already been garbage collected.</span></span> <span data-ttu-id="f487b-151">在此情況下，便無法復原該帳戶。</span><span class="sxs-lookup"><span data-stu-id="f487b-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="f487b-152">請參閱本主題中的[回收容量](#reclaim)。</span><span class="sxs-lookup"><span data-stu-id="f487b-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-hello-retention-period"></a><span data-ttu-id="f487b-153">設定 hello 保留期限</span><span class="sxs-lookup"><span data-stu-id="f487b-153">Set hello retention period</span></span>
<span data-ttu-id="f487b-154">hello 保留期限設定可讓雲端操作員 toospecify 天數 （介於 0 到 9999 天） 中的時間範圍期間的任何已刪除的帳戶可能已復原。</span><span class="sxs-lookup"><span data-stu-id="f487b-154">hello retention period setting allows a cloud operator toospecify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="f487b-155">hello 預設保留週期設 too15 天。</span><span class="sxs-lookup"><span data-stu-id="f487b-155">hello default retention period is set too15 days.</span></span> <span data-ttu-id="f487b-156">設定 hello 值太"0"，則表示立即超出保留已刪除的帳戶，並標示為定期記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="f487b-156">Setting hello value too“0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="f487b-157">**toochange hello 保留期限：**</span><span class="sxs-lookup"><span data-stu-id="f487b-157">**toochange hello retention period:**</span></span>

1. <span data-ttu-id="f487b-158">在網際網路瀏覽器中，瀏覽至 https://adminportal.local.azurestack.external。</span><span class="sxs-lookup"><span data-stu-id="f487b-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="f487b-159">登入 toohello 堆疊 Azure 系統管理入口網站為雲端操作員 （使用您在部署期間所提供的認證）</span><span class="sxs-lookup"><span data-stu-id="f487b-159">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="f487b-160">Hello 預設儀表板 – 上尋找 hello**區域管理**清單，然後按一下您想要 tooexplore – 例如 hello 區域**(本機**)。</span><span class="sxs-lookup"><span data-stu-id="f487b-160">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore – for example **(local**).</span></span>
4. <span data-ttu-id="f487b-161">選取**儲存體**從 hello**資源提供者**清單。</span><span class="sxs-lookup"><span data-stu-id="f487b-161">Select **Storage** from hello **Resource Providers** list.</span></span>
5. <span data-ttu-id="f487b-162">按一下**設定**在 hello 頂端 tooopen hello 設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f487b-162">Click **Settings** at hello top tooopen hello setting blade.</span></span>
6. <span data-ttu-id="f487b-163">按一下**組態**然後編輯 hello 保留週期值。</span><span class="sxs-lookup"><span data-stu-id="f487b-163">Click **Configuration** then edit hello retention period value.</span></span>

   <span data-ttu-id="f487b-164">設定 hello 的天數，然後將它儲存。</span><span class="sxs-lookup"><span data-stu-id="f487b-164">Set hello number of days and then save it.</span></span>
   
   <span data-ttu-id="f487b-165">此值會立即生效，而且會設定您的整個區域。</span><span class="sxs-lookup"><span data-stu-id="f487b-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="f487b-166"><a name="reclaim"></a>回收容量</span><span class="sxs-lookup"><span data-stu-id="f487b-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="f487b-167">其中一個 hello 副作用的保留期限是已刪除的帳戶將繼續 tooconsume 容量，直到它來自 hello 保留期限。</span><span class="sxs-lookup"><span data-stu-id="f487b-167">One of hello side effects of having a retention period is that a deleted account continues tooconsume capacity until it comes out of hello retention period.</span></span> <span data-ttu-id="f487b-168">為雲端您可能需要方法 tooreclaim hello 的運算子會刪除帳戶空間，即使 hello 保留期間尚未過期。</span><span class="sxs-lookup"><span data-stu-id="f487b-168">As a cloud operator you may need a way tooreclaim hello deleted account space even though hello retention period has not yet expired.</span></span>

<span data-ttu-id="f487b-169">您可以回收容量使用 hello 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f487b-169">You can reclaim capacity using either hello portal or PowerShell.</span></span>

<span data-ttu-id="f487b-170">**tooreclaim 容量使用 hello 入口網站：**</span><span class="sxs-lookup"><span data-stu-id="f487b-170">**tooreclaim capacity using hello portal:**</span></span>
1. <span data-ttu-id="f487b-171">瀏覽 toohello 儲存體帳戶 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f487b-171">Navigate toohello storage accounts blade.</span></span> <span data-ttu-id="f487b-172">請參閱[尋找儲存體帳戶](#find)。</span><span class="sxs-lookup"><span data-stu-id="f487b-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="f487b-173">按一下**回收空間**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="f487b-173">Click **Reclaim space** at hello top of hello blade.</span></span>
3. <span data-ttu-id="f487b-174">閱讀 hello 訊息，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="f487b-174">Read hello message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="f487b-175">等候 hello 入口網站中的成功通知，請參閱 hello 鈴鐺圖示。</span><span class="sxs-lookup"><span data-stu-id="f487b-175">Wait for success notification See hello bell icon on hello portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="f487b-176">重新整理 hello 儲存體帳戶 頁面。</span><span class="sxs-lookup"><span data-stu-id="f487b-176">Refresh hello Storage accounts page.</span></span> <span data-ttu-id="f487b-177">hello 刪除帳戶不再是 hello 清單中顯示，因為已遭清除。</span><span class="sxs-lookup"><span data-stu-id="f487b-177">hello deleted accounts are no longer shown in hello list because they have been purged.</span></span>

<span data-ttu-id="f487b-178">您可以也使用 PowerShell tooexplicitly 覆寫 hello 保留期限，並立即回收容量。</span><span class="sxs-lookup"><span data-stu-id="f487b-178">You can also use PowerShell tooexplicitly override hello retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="f487b-179">**使用 PowerShell tooreclaim 容量：**</span><span class="sxs-lookup"><span data-stu-id="f487b-179">**tooreclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="f487b-180">確認您已安裝並設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f487b-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="f487b-181">否則，請使用下列指示的 hello:</span><span class="sxs-lookup"><span data-stu-id="f487b-181">If not, use hello following instructions:</span></span> 
   * <span data-ttu-id="f487b-182">tooinstall hello 最新的 Azure PowerShell 版本並將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="f487b-182">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="f487b-183">如需有關 Azure Resource Manager Cmdlet 的詳細資訊，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="f487b-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="f487b-184">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="f487b-184">Run hello following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="f487b-185">如果您執行這個指令程式永久刪除 hello 帳戶和其內容。</span><span class="sxs-lookup"><span data-stu-id="f487b-185">If you run this cmdlet you permanently delete hello account and its contents.</span></span> <span data-ttu-id="f487b-186">無法復原。</span><span class="sxs-lookup"><span data-stu-id="f487b-186">It is not recoverable.</span></span> <span data-ttu-id="f487b-187">使用時請務必小心。</span><span class="sxs-lookup"><span data-stu-id="f487b-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="f487b-188">如需詳細資訊，請參閱太[Azure 堆疊 powershell 文件。](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="f487b-188">For more details, refer too[Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="f487b-189">移轉容器</span><span class="sxs-lookup"><span data-stu-id="f487b-189">Migrate a container</span></span>
<span data-ttu-id="f487b-190">Toouneven 儲存體租用戶所使用，因為雲端運算子可能會發現其中一個或多基礎租用戶共用使用比其他更多空間。</span><span class="sxs-lookup"><span data-stu-id="f487b-190">Due toouneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="f487b-191">如果發生這種情況，hello 雲端操作員可以手動移轉某些 blob 容器 tooanother 共用嘗試 toofree 出一些空間在 hello 注重重音的共用。</span><span class="sxs-lookup"><span data-stu-id="f487b-191">If this occurs, hello cloud operator can attempt toofree up some space on hello stressed share by manually migrating some blob containers tooanother share.</span></span> 

<span data-ttu-id="f487b-192">您必須使用 PowerShell toomigrate 容器。</span><span class="sxs-lookup"><span data-stu-id="f487b-192">You must use PowerShell toomigrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="f487b-193">Blob 容器移轉不支援即時移轉，而且目前是離線作業。</span><span class="sxs-lookup"><span data-stu-id="f487b-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="f487b-194">在移轉期間，該容器中的 hello 基礎 blob 完成之前無法使用，而且是 「 離線 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="f487b-194">During migration and until it is complete hello underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="f487b-195">**使用 PowerShell toomigrate 容器：**</span><span class="sxs-lookup"><span data-stu-id="f487b-195">**toomigrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="f487b-196">確認您已安裝並設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f487b-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="f487b-197">否則，請使用下列指示的 hello:</span><span class="sxs-lookup"><span data-stu-id="f487b-197">If not, use hello following instructions:</span></span>
    * <span data-ttu-id="f487b-198">tooinstall hello 最新的 Azure PowerShell 版本並將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="f487b-198">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="f487b-199">如需有關 Azure Resource Manager Cmdlet 的詳細資訊，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="f487b-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="f487b-200">收到 hello 伺服陣列名稱：</span><span class="sxs-lookup"><span data-stu-id="f487b-200">Get hello farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="f487b-201">取得 hello 共用：</span><span class="sxs-lookup"><span data-stu-id="f487b-201">Get hello shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="f487b-202">取得指定的共用 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="f487b-202">Get hello containers for a given share.</span></span> <span data-ttu-id="f487b-203">請注意，count 和 intent 都是選擇性參數：</span><span class="sxs-lookup"><span data-stu-id="f487b-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="f487b-204">接著，檢查 $containers：</span><span class="sxs-lookup"><span data-stu-id="f487b-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="f487b-205">取得 hello 容器移轉 hello 最佳目的共用：</span><span class="sxs-lookup"><span data-stu-id="f487b-205">Get hello best destination shares for hello container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="f487b-206">接著，檢查 $destinationshares：</span><span class="sxs-lookup"><span data-stu-id="f487b-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="f487b-207">開始進行移轉的容器，請注意這是非同步實作，因此一個可以迴圈中使用 hello 傳回的作業識別碼的共用及追蹤 hello 狀態的所有容器。</span><span class="sxs-lookup"><span data-stu-id="f487b-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track hello status using hello returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="f487b-208">接著，檢查 $jobId：</span><span class="sxs-lookup"><span data-stu-id="f487b-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="f487b-209">檢查它的作業識別碼 hello 移轉作業的狀態。Hello 容器移轉完成時，MigrationStatus 設定太 「 已完成 」。</span><span class="sxs-lookup"><span data-stu-id="f487b-209">Check status of hello migration job by its job id. When hello container migration finishes, MigrationStatus is set too“Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="f487b-210">您可以取消進行中的移轉工作。</span><span class="sxs-lookup"><span data-stu-id="f487b-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="f487b-211">這仍然是非同步作業，而且可以使用 $jobid 來追蹤：</span><span class="sxs-lookup"><span data-stu-id="f487b-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="f487b-212">您可以再次檢查 hello hello 移轉取消 5d; 狀態：</span><span class="sxs-lookup"><span data-stu-id="f487b-212">You can check hello status of hello migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  