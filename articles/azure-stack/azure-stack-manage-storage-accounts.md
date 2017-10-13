---
title: "管理 Azure Stack 儲存體帳戶 | Microsoft Docs"
description: "了解如何尋找、管理、復原及回收 Azure Stack 儲存體帳戶"
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
ms.openlocfilehash: 6e14bd6312135b45984a82099e68a934ec2a4a70
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="e7947-103">在 Azure Stack 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e7947-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="e7947-104">了解如何在 Azure Stack 中管理儲存體帳戶，以便根據業務需求來尋找、復原及回收儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="e7947-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="e7947-105"><a name="find"></a>尋找儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e7947-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="e7947-106">區域中的儲存體帳戶清單可在 Azure Stack 中，透過下列方式檢視：</span><span class="sxs-lookup"><span data-stu-id="e7947-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="e7947-107">在網際網路瀏覽器中，瀏覽至 https://adminportal.local.azurestack.external。</span><span class="sxs-lookup"><span data-stu-id="e7947-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="e7947-108">以雲端操作員身分 (使用您在部署期間所提供的認證)，登入 Azure Stack 系統管理入口網站</span><span class="sxs-lookup"><span data-stu-id="e7947-108">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="e7947-109">在預設儀表板上，尋找 [區域管理] 清單，然後按一下您想要探索的區域。</span><span class="sxs-lookup"><span data-stu-id="e7947-109">On the default dashboard – find the **Region management** list and click the region you want to explore.</span></span> <span data-ttu-id="e7947-110">例如 **(local**)。</span><span class="sxs-lookup"><span data-stu-id="e7947-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="e7947-111">從 [資源提供者] 清單中選取 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="e7947-111">Select **Storage** from the **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="e7947-112">現在，在儲存體資源提供者系統管理員刀鋒視窗中，向下捲動至 [儲存體帳戶] 索引標籤，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="e7947-112">Now, on the storage Resource Provider administrator blade – scroll down to the **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="e7947-113">所產生的頁面就是在該區域中的儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="e7947-113">The resulting page is the list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="e7947-114">預設會顯示前 10 個帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7947-114">By default, the first 10 accounts are displayed.</span></span> <span data-ttu-id="e7947-115">您可以按一下清單底部的 [載入更多] 連結，選擇擷取更多項目。</span><span class="sxs-lookup"><span data-stu-id="e7947-115">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span></span>

<span data-ttu-id="e7947-116">或</span><span class="sxs-lookup"><span data-stu-id="e7947-116">OR</span></span>

<span data-ttu-id="e7947-117">如果您只想看到特定儲存體帳戶，可以只**篩選並擷取相關的帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e7947-117">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span></span>


<span data-ttu-id="e7947-118">**篩選帳戶：**</span><span class="sxs-lookup"><span data-stu-id="e7947-118">**To filter for accounts:**</span></span>

1. <span data-ttu-id="e7947-119">按一下刀鋒視窗頂端的 [篩選]。</span><span class="sxs-lookup"><span data-stu-id="e7947-119">Click **Filter** at the top of the blade.</span></span>
2. <span data-ttu-id="e7947-120">在 [篩選] 刀鋒視窗上，您可以指定 [帳戶名稱]、[訂用帳戶識別碼] 或 [狀態]，以微調要顯示的儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="e7947-120">On the Filter blade, it allows you to specify **account name**, **subscription ID** or **status** to fine-tune the list of storage accounts to be displayed.</span></span> <span data-ttu-id="e7947-121">請適當地指定。</span><span class="sxs-lookup"><span data-stu-id="e7947-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="e7947-122">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="e7947-122">Click **Update**.</span></span> <span data-ttu-id="e7947-123">清單應該會隨著重新整理。</span><span class="sxs-lookup"><span data-stu-id="e7947-123">The list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="e7947-124">若要重設篩選：按一下 [篩選]、清除選取項目，然後更新。</span><span class="sxs-lookup"><span data-stu-id="e7947-124">To reset the filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="e7947-125">[搜尋] 文字方塊 (在儲存體帳戶清單刀鋒視窗的頂端) 可讓您反白顯示帳戶清單中選取的文字。</span><span class="sxs-lookup"><span data-stu-id="e7947-125">The search text box (on the top of the storage accounts list blade) lets you highlight the selected text in the list of accounts.</span></span> <span data-ttu-id="e7947-126">如果無法輕易地取得完整名稱或識別碼，這真的很方便。</span><span class="sxs-lookup"><span data-stu-id="e7947-126">This is really handy in the case when the full name or id is not easily available.</span></span>

<span data-ttu-id="e7947-127">您可以在這裡使用任意文字，以協助找出您想看到的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7947-127">You can use free text here to help find the account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="e7947-128">查看帳戶詳細資料</span><span class="sxs-lookup"><span data-stu-id="e7947-128">Look at account details</span></span>
<span data-ttu-id="e7947-129">一旦找到您想檢視的帳戶之後，可以按一下特定的帳戶，以檢視特定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7947-129">Once you have located the accounts you are interested in viewing, you can click the particular account to view certain details.</span></span> <span data-ttu-id="e7947-130">新刀鋒視窗隨即開啟，其中包含帳戶詳細資料，例如：帳戶類型、建立時間、位置等等。</span><span class="sxs-lookup"><span data-stu-id="e7947-130">A new blade opens with the account details such as: the type of the account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="e7947-131">復原已刪除的帳戶</span><span class="sxs-lookup"><span data-stu-id="e7947-131">Recover a deleted account</span></span>
<span data-ttu-id="e7947-132">有時候，您必須復原已刪除的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7947-132">You may be in a situation where you need to recover a deleted account.</span></span>

<span data-ttu-id="e7947-133">在 Azure Stack 中，有一個非常簡單的方式可以執行此作業：</span><span class="sxs-lookup"><span data-stu-id="e7947-133">In Azure Stack there is a very simple way to do that:</span></span>

1. <span data-ttu-id="e7947-134">瀏覽至儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="e7947-134">Browse to the storage accounts list.</span></span> <span data-ttu-id="e7947-135">如需詳細資訊，請參閱本主題中的[尋找儲存體帳戶](#find)。</span><span class="sxs-lookup"><span data-stu-id="e7947-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="e7947-136">在清單中找出該特定帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7947-136">Locate that particular account in the list.</span></span> <span data-ttu-id="e7947-137">您可能需要篩選。</span><span class="sxs-lookup"><span data-stu-id="e7947-137">You may need to filter.</span></span>
3. <span data-ttu-id="e7947-138">請檢查帳戶的 [狀態]。</span><span class="sxs-lookup"><span data-stu-id="e7947-138">Check the *state* of the account.</span></span> <span data-ttu-id="e7947-139">它應該指出 [已刪除]。</span><span class="sxs-lookup"><span data-stu-id="e7947-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="e7947-140">按一下可開啟 [帳戶詳細資料] 刀鋒視窗的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7947-140">Click the account which opens the account details blade.</span></span>
5. <span data-ttu-id="e7947-141">在這個刀鋒視窗的頂端，找出 [復原] 按鈕，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="e7947-141">On top of this blade, locate the **Recover** button and click it.</span></span>
6. <span data-ttu-id="e7947-142">按一下 [ **是** ] 以確認。</span><span class="sxs-lookup"><span data-stu-id="e7947-142">Click **Yes** to confirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="e7947-143">復原現在處於 [處理中...請等待] 的狀態，正在等待復原成功的訊息出現。</span><span class="sxs-lookup"><span data-stu-id="e7947-143">The recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="e7947-144">您也可以按一下入口網站頂端的「鈴鐺」圖示，以檢視進度指示。</span><span class="sxs-lookup"><span data-stu-id="e7947-144">You can also click the “bell” icon at the top of the portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="e7947-145">一旦成功同步處理已復原的帳戶之後，就可以再次使用該帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7947-145">Once the recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="e7947-146">注意事項</span><span class="sxs-lookup"><span data-stu-id="e7947-146">Some Gotchas</span></span>
* <span data-ttu-id="e7947-147">已刪除的帳戶顯示 [不再保留] 狀態。</span><span class="sxs-lookup"><span data-stu-id="e7947-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="e7947-148">這表示已刪除的帳戶已超出保留期限，可能無法復原。</span><span class="sxs-lookup"><span data-stu-id="e7947-148">This means that the deleted account has exceeded the retention period and may not be recoverable.</span></span>
* <span data-ttu-id="e7947-149">已刪除的帳戶未顯示在帳戶清單中。</span><span class="sxs-lookup"><span data-stu-id="e7947-149">Your deleted account does not show in the accounts list.</span></span>
  
  <span data-ttu-id="e7947-150">這可能表示已刪除的帳戶已經被記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="e7947-150">This could mean that the deleted account has already been garbage collected.</span></span> <span data-ttu-id="e7947-151">在此情況下，便無法復原該帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7947-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="e7947-152">請參閱本主題中的[回收容量](#reclaim)。</span><span class="sxs-lookup"><span data-stu-id="e7947-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-the-retention-period"></a><span data-ttu-id="e7947-153">設定保留期限</span><span class="sxs-lookup"><span data-stu-id="e7947-153">Set the retention period</span></span>
<span data-ttu-id="e7947-154">保留期限設定可讓雲端操作員指定時間間隔天數 (介於 0 到 9999 天)，在此期間，任何已刪除的帳戶都可能復原。</span><span class="sxs-lookup"><span data-stu-id="e7947-154">The retention period setting allows a cloud operator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="e7947-155">預設保留期限設定為 15 天。</span><span class="sxs-lookup"><span data-stu-id="e7947-155">The default retention period is set to 15 days.</span></span> <span data-ttu-id="e7947-156">將值設定為 "0" 表示立即不保留任何已刪除的帳戶，並標示供定期記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="e7947-156">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="e7947-157">**變更保留期限：**</span><span class="sxs-lookup"><span data-stu-id="e7947-157">**To change the retention period:**</span></span>

1. <span data-ttu-id="e7947-158">在網際網路瀏覽器中，瀏覽至 https://adminportal.local.azurestack.external。</span><span class="sxs-lookup"><span data-stu-id="e7947-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="e7947-159">以雲端操作員身分 (使用您在部署期間所提供的認證)，登入 Azure Stack 系統管理入口網站</span><span class="sxs-lookup"><span data-stu-id="e7947-159">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="e7947-160">在預設儀表板上，尋找 [區域管理] 清單，然後按一下您想要探索的區域，例如 **(local**)。</span><span class="sxs-lookup"><span data-stu-id="e7947-160">On the default dashboard – find the **Region management** list and click the region you want to explore – for example **(local**).</span></span>
4. <span data-ttu-id="e7947-161">從 [資源提供者] 清單中選取 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="e7947-161">Select **Storage** from the **Resource Providers** list.</span></span>
5. <span data-ttu-id="e7947-162">按一下頂端的 [設定]，開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e7947-162">Click **Settings** at the top to open the setting blade.</span></span>
6. <span data-ttu-id="e7947-163">按一下 [設定]，然後編輯保留期限值。</span><span class="sxs-lookup"><span data-stu-id="e7947-163">Click **Configuration** then edit the retention period value.</span></span>

   <span data-ttu-id="e7947-164">設定天數，然後加以儲存。</span><span class="sxs-lookup"><span data-stu-id="e7947-164">Set the number of days and then save it.</span></span>
   
   <span data-ttu-id="e7947-165">此值會立即生效，而且會設定您的整個區域。</span><span class="sxs-lookup"><span data-stu-id="e7947-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="e7947-166"><a name="reclaim"></a>回收容量</span><span class="sxs-lookup"><span data-stu-id="e7947-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="e7947-167">保留期限會有副作用，亦即已刪除的帳戶會繼續耗用容量，直到超出保留期限為止。</span><span class="sxs-lookup"><span data-stu-id="e7947-167">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span></span> <span data-ttu-id="e7947-168">身為雲端操作員，即使保留期限尚未到期，您可能還是需要一個回收已刪除帳戶空間的方式。</span><span class="sxs-lookup"><span data-stu-id="e7947-168">As a cloud operator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span></span>

<span data-ttu-id="e7947-169">您可以使用入口網站或 PowerShell 來回收容量。</span><span class="sxs-lookup"><span data-stu-id="e7947-169">You can reclaim capacity using either the portal or PowerShell.</span></span>

<span data-ttu-id="e7947-170">**使用入口網站回收容量：**</span><span class="sxs-lookup"><span data-stu-id="e7947-170">**To reclaim capacity using the portal:**</span></span>
1. <span data-ttu-id="e7947-171">瀏覽至儲存體帳戶刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e7947-171">Navigate to the storage accounts blade.</span></span> <span data-ttu-id="e7947-172">請參閱[尋找儲存體帳戶](#find)。</span><span class="sxs-lookup"><span data-stu-id="e7947-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="e7947-173">按一下刀鋒視窗頂端的 [回收空間]。</span><span class="sxs-lookup"><span data-stu-id="e7947-173">Click **Reclaim space** at the top of the blade.</span></span>
3. <span data-ttu-id="e7947-174">讀取訊息，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="e7947-174">Read the message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="e7947-175">等候成功通知。請查看入口網站上的鈴鐺圖示。</span><span class="sxs-lookup"><span data-stu-id="e7947-175">Wait for success notification See the bell icon on the portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="e7947-176">重新整理 [儲存體帳戶] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e7947-176">Refresh the Storage accounts page.</span></span> <span data-ttu-id="e7947-177">已刪除的帳戶已遭到清除，因此不會再顯示在清單中。</span><span class="sxs-lookup"><span data-stu-id="e7947-177">The deleted accounts are no longer shown in the list because they have been purged.</span></span>

<span data-ttu-id="e7947-178">您也可以使用 PowerShell 明確地覆寫保留期限，並立即回收容量。</span><span class="sxs-lookup"><span data-stu-id="e7947-178">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="e7947-179">**使用 PowerShell 回收容量：**</span><span class="sxs-lookup"><span data-stu-id="e7947-179">**To reclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="e7947-180">確認您已安裝並設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e7947-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="e7947-181">否則，請使用下列指示：</span><span class="sxs-lookup"><span data-stu-id="e7947-181">If not, use the following instructions:</span></span> 
   * <span data-ttu-id="e7947-182">若要安裝最新的 Azure PowerShell 版本，並將它與您的 Azure 訂用帳戶建立關聯，請參閱[如何安裝和設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="e7947-182">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="e7947-183">如需有關 Azure Resource Manager Cmdlet 的詳細資訊，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="e7947-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="e7947-184">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="e7947-184">Run the following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="e7947-185">如果您執行這個 Cmdlet，將會永久刪除帳戶及其內容。</span><span class="sxs-lookup"><span data-stu-id="e7947-185">If you run this cmdlet you permanently delete the account and its contents.</span></span> <span data-ttu-id="e7947-186">無法復原。</span><span class="sxs-lookup"><span data-stu-id="e7947-186">It is not recoverable.</span></span> <span data-ttu-id="e7947-187">使用時請務必小心。</span><span class="sxs-lookup"><span data-stu-id="e7947-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="e7947-188">如需詳細資訊，請參閱 [Azure Stack PowerShell 文件](https://msdn.microsoft.com/library/mt637964.aspx) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e7947-188">For more details, refer to [Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="e7947-189">移轉容器</span><span class="sxs-lookup"><span data-stu-id="e7947-189">Migrate a container</span></span>
<span data-ttu-id="e7947-190">由於租用戶的儲存體用量不平均，因此雲端操作員可能會發現其中一個或多個基礎租用戶共用所使用的空間比其他租用戶更多。</span><span class="sxs-lookup"><span data-stu-id="e7947-190">Due to uneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="e7947-191">如果發生這種情況，雲端操作員可以嘗試將部分 Blob 容器手動移轉至另一個共用，為使用量較大的共用釋放一些空間。</span><span class="sxs-lookup"><span data-stu-id="e7947-191">If this occurs, the cloud operator can attempt to free up some space on the stressed share by manually migrating some blob containers to another share.</span></span> 

<span data-ttu-id="e7947-192">您必須使用 PowerShell 來移轉容器。</span><span class="sxs-lookup"><span data-stu-id="e7947-192">You must use PowerShell to migrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="e7947-193">Blob 容器移轉不支援即時移轉，而且目前是離線作業。</span><span class="sxs-lookup"><span data-stu-id="e7947-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="e7947-194">在移轉期間以及完成移轉之前，該容器中的基礎 Blob 都無法使用，而且是處於「離線」狀態。</span><span class="sxs-lookup"><span data-stu-id="e7947-194">During migration and until it is complete the underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="e7947-195">**使用 PowerShell 來移轉容器：**</span><span class="sxs-lookup"><span data-stu-id="e7947-195">**To migrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="e7947-196">確認您已安裝並設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e7947-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="e7947-197">否則，請使用下列指示：</span><span class="sxs-lookup"><span data-stu-id="e7947-197">If not, use the following instructions:</span></span>
    * <span data-ttu-id="e7947-198">若要安裝最新的 Azure PowerShell 版本，並將它與您的 Azure 訂用帳戶建立關聯，請參閱[如何安裝和設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="e7947-198">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="e7947-199">如需有關 Azure Resource Manager Cmdlet 的詳細資訊，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="e7947-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="e7947-200">取得伺服器陣列名稱：</span><span class="sxs-lookup"><span data-stu-id="e7947-200">Get the farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="e7947-201">取得共用：</span><span class="sxs-lookup"><span data-stu-id="e7947-201">Get the shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="e7947-202">取得指定共用的容器。</span><span class="sxs-lookup"><span data-stu-id="e7947-202">Get the containers for a given share.</span></span> <span data-ttu-id="e7947-203">請注意，count 和 intent 都是選擇性參數：</span><span class="sxs-lookup"><span data-stu-id="e7947-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="e7947-204">接著，檢查 $containers：</span><span class="sxs-lookup"><span data-stu-id="e7947-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="e7947-205">取得用於容器移轉的最佳目的地共用：</span><span class="sxs-lookup"><span data-stu-id="e7947-205">Get the best destination shares for the container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="e7947-206">接著，檢查 $destinationshares：</span><span class="sxs-lookup"><span data-stu-id="e7947-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="e7947-207">開始進行容器移轉。請注意，這是非同步實作，因此可以循環處理共用中的所有容器，並使用傳回的工作識別碼來追蹤狀態。</span><span class="sxs-lookup"><span data-stu-id="e7947-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track the status using the returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="e7947-208">接著，檢查 $jobId：</span><span class="sxs-lookup"><span data-stu-id="e7947-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="e7947-209">依工作識別碼檢查移轉工作的狀態。當容器移轉完成時，MigrationStatus 會設定為 「已完成」。</span><span class="sxs-lookup"><span data-stu-id="e7947-209">Check status of the migration job by its job id. When the container migration finishes, MigrationStatus is set to “Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="e7947-210">您可以取消進行中的移轉工作。</span><span class="sxs-lookup"><span data-stu-id="e7947-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="e7947-211">這仍然是非同步作業，而且可以使用 $jobid 來追蹤：</span><span class="sxs-lookup"><span data-stu-id="e7947-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="e7947-212">您可以再次檢查移轉取消的狀態：</span><span class="sxs-lookup"><span data-stu-id="e7947-212">You can check the status of the migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  