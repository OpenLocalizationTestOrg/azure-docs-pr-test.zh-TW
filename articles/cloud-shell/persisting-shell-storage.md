---
title: "在 Azure Cloud Shell (預覽) 中保存檔案 | Microsoft Docs"
description: "逐步解說 Azure Cloud Shell 如何保存檔案。"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="dc149-103">在 Azure Cloud Shell 中保存檔案</span><span class="sxs-lookup"><span data-stu-id="dc149-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="dc149-104">Cloud Shell 會利用 Azure 檔案儲存體在工作階段間保存檔案。</span><span class="sxs-lookup"><span data-stu-id="dc149-104">Cloud Shell takes advantage of Azure File storage to persist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="dc149-105">設定 `clouddrive` 檔案共用</span><span class="sxs-lookup"><span data-stu-id="dc149-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="dc149-106">在初始啟動時，Cloud Shell 會提示您關聯新的或現有的檔案共用，以在工作階段間保存檔案。</span><span class="sxs-lookup"><span data-stu-id="dc149-106">On initial start, Cloud Shell prompts you to associate a new or existing file share to persist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="dc149-107">建立新的儲存體</span><span class="sxs-lookup"><span data-stu-id="dc149-107">Create new storage</span></span>

<span data-ttu-id="dc149-108">當您使用基本設定並只選取訂用帳戶時，Cloud Shell 會代表您在距離您最近的支援區域中建立三個資源：</span><span class="sxs-lookup"><span data-stu-id="dc149-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in the supported region that's nearest to you:</span></span>
* <span data-ttu-id="dc149-109">資源群組：`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="dc149-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="dc149-110">儲存體帳戶：`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="dc149-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="dc149-111">檔案共用：`cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="dc149-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![訂用帳戶設定](media/basic-storage.png)

<span data-ttu-id="dc149-113">檔案共用會在您的 `$Home` 目錄中掛接為 `clouddrive`。</span><span class="sxs-lookup"><span data-stu-id="dc149-113">The file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="dc149-114">檔案共用也會用來儲存為您建立的 5 GB 映像，以便自動更新並保存您的 `$Home` 目錄。</span><span class="sxs-lookup"><span data-stu-id="dc149-114">The file share is also used to store a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="dc149-115">這是一次性的動作，後續的工作階段會自動掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-115">This is a one-time action, and the file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="dc149-116">使用現有的資源</span><span class="sxs-lookup"><span data-stu-id="dc149-116">Use existing resources</span></span>

<span data-ttu-id="dc149-117">您可以使用進階選項來建立與現有資源的關聯。</span><span class="sxs-lookup"><span data-stu-id="dc149-117">By using the advanced option, you can associate existing resources.</span></span> <span data-ttu-id="dc149-118">當儲存體設定提示出現時，請選取 [顯示進階設定] 以檢視其他選項。</span><span class="sxs-lookup"><span data-stu-id="dc149-118">When the storage setup prompt appears, select **Show advanced settings** to view additional options.</span></span> <span data-ttu-id="dc149-119">現有的檔案共用會收到用來保存 `$Home` 目錄的 5 GB 使用者映像。</span><span class="sxs-lookup"><span data-stu-id="dc149-119">Existing file shares receive a 5-GB user image to persist your `$Home` directory.</span></span> <span data-ttu-id="dc149-120">下拉式功能表會針對您的 Cloud Shell 區域以及本地備援和異地備援儲存體帳戶進行篩選。</span><span class="sxs-lookup"><span data-stu-id="dc149-120">The drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![資源群組設定](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="dc149-122">使用 Azure 資源原則限制資源建立</span><span class="sxs-lookup"><span data-stu-id="dc149-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="dc149-123">您在 Cloud Shell 中建立的儲存體帳戶都會標記 `ms-resource-usage:azure-cloud-shell`。</span><span class="sxs-lookup"><span data-stu-id="dc149-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="dc149-124">如果您想要禁止使用者在 Cloud Shell 中建立儲存體帳戶，請建立這個特定標籤所觸發之[標籤的 Azure 資源原則](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags)。</span><span class="sxs-lookup"><span data-stu-id="dc149-124">If you want to disallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="dc149-125">Cloud Shell 的運作方式</span><span class="sxs-lookup"><span data-stu-id="dc149-125">How Cloud Shell works</span></span>
<span data-ttu-id="dc149-126">Cloud Shell 透過下列兩種方法來保存檔案：</span><span class="sxs-lookup"><span data-stu-id="dc149-126">Cloud Shell persists files through both of the following methods:</span></span>
* <span data-ttu-id="dc149-127">建立 `$Home` 目錄的磁碟映像，以保存該目錄內的所有內容。</span><span class="sxs-lookup"><span data-stu-id="dc149-127">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="dc149-128">此磁碟映像會在您指定的檔案共用中儲存為 `acc_<User>.img` (位於 `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`)，並自動同步變更。</span><span class="sxs-lookup"><span data-stu-id="dc149-128">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="dc149-129">在您的 `$Home` 目錄中，將指定的檔案共用掛接為 `clouddrive`，以便直接與檔案共用互動。</span><span class="sxs-lookup"><span data-stu-id="dc149-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="dc149-130">`/Home/<User>/clouddrive` 對應至 `fileshare.storage.windows.net/fileshare`。</span><span class="sxs-lookup"><span data-stu-id="dc149-130">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="dc149-131">`$Home` 目錄中的所有檔案 (例如 SSH 金鑰) 會都保存於已掛接檔案共用中儲存的使用者磁碟映像中。</span><span class="sxs-lookup"><span data-stu-id="dc149-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="dc149-132">當您在 `$Home` 目錄和已掛接的檔案共用中保存資訊時，請套用最佳做法。</span><span class="sxs-lookup"><span data-stu-id="dc149-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-the-clouddrive-command"></a><span data-ttu-id="dc149-133">使用 `clouddrive` 命令</span><span class="sxs-lookup"><span data-stu-id="dc149-133">Use the `clouddrive` command</span></span>
<span data-ttu-id="dc149-134">Cloud Shell 可讓您執行名為 `clouddrive` 的命令，以手動更新掛接至 Cloud Shell 的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that's mounted to Cloud Shell.</span></span>
<span data-ttu-id="dc149-135">![執行 "clouddrive" 命令](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="dc149-135">![Running the "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="dc149-136">掛接新的 `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="dc149-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="dc149-137">手動掛接的先決條件</span><span class="sxs-lookup"><span data-stu-id="dc149-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="dc149-138">您可以使用 `clouddrive mount` 命令來更新與 Cloud Shell 關聯的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-138">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="dc149-139">如果您要掛接現有的檔案共用，儲存體帳戶必須為：</span><span class="sxs-lookup"><span data-stu-id="dc149-139">If you mount an existing file share, the storage accounts must be:</span></span>
* <span data-ttu-id="dc149-140">可支援檔案共用的本地備援儲存體或異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="dc149-140">Locally-redundant storage or geo-redundant storage to support file shares.</span></span>
* <span data-ttu-id="dc149-141">位於您的指派區域。</span><span class="sxs-lookup"><span data-stu-id="dc149-141">Located in your assigned region.</span></span> <span data-ttu-id="dc149-142">當您要上架時，您的指派區域會列在名為 `cloud-shell-storage-<region>` 的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="dc149-142">When you are onboarding, the region you are assigned to is listed in the resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="dc149-143">支援的儲存體區域</span><span class="sxs-lookup"><span data-stu-id="dc149-143">Supported storage regions</span></span>
<span data-ttu-id="dc149-144">Azure 檔案必須位於與所掛接之目標 Cloud Shell 電腦相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="dc149-144">The Azure files must reside in the same region as the Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="dc149-145">Cloud Shell 叢集目前存在於下列區域：</span><span class="sxs-lookup"><span data-stu-id="dc149-145">Cloud Shell clusters currently exist in the following regions:</span></span>
|<span data-ttu-id="dc149-146">領域</span><span class="sxs-lookup"><span data-stu-id="dc149-146">Area</span></span>|<span data-ttu-id="dc149-147">區域</span><span class="sxs-lookup"><span data-stu-id="dc149-147">Region</span></span>|
|---|---|
|<span data-ttu-id="dc149-148">美洲</span><span class="sxs-lookup"><span data-stu-id="dc149-148">Americas</span></span>|<span data-ttu-id="dc149-149">美國東部、美國中南部、美國西部</span><span class="sxs-lookup"><span data-stu-id="dc149-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="dc149-150">歐洲</span><span class="sxs-lookup"><span data-stu-id="dc149-150">Europe</span></span>|<span data-ttu-id="dc149-151">北歐、西歐</span><span class="sxs-lookup"><span data-stu-id="dc149-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="dc149-152">亞太地區</span><span class="sxs-lookup"><span data-stu-id="dc149-152">Asia Pacific</span></span>|<span data-ttu-id="dc149-153">印度中部、東南亞</span><span class="sxs-lookup"><span data-stu-id="dc149-153">India Central, Southeast Asia</span></span>|

### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="dc149-154">`clouddrive mount` 命令</span><span class="sxs-lookup"><span data-stu-id="dc149-154">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="dc149-155">如果您要掛接新的檔案共用，系統會為您的 `$Home` 目錄建立一個新的使用者映像，因為先前的 `$Home` 映像會保留在先前的檔案共用中。</span><span class="sxs-lookup"><span data-stu-id="dc149-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in the previous file share.</span></span>

<span data-ttu-id="dc149-156">執行 `clouddrive mount` 命令搭配下列參數：</span><span class="sxs-lookup"><span data-stu-id="dc149-156">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="dc149-157">若要檢視更多詳細資料，請執行 `clouddrive mount -h`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc149-157">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![執行 `clouddrive mount` 命令](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="dc149-159">卸載 `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="dc149-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="dc149-160">您可以隨時將掛接至 Cloud Shell 的檔案共用卸載。</span><span class="sxs-lookup"><span data-stu-id="dc149-160">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="dc149-161">一旦卸載您的檔案共用，系統會提示您在下一個工作階段之前掛接新的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-161">Once your file share is unmounted, you will be prompted to mount a new file share prior to your next session.</span></span>

<span data-ttu-id="dc149-162">若要從 Cloud Shell 中移除檔案共用：</span><span class="sxs-lookup"><span data-stu-id="dc149-162">To remove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="dc149-163">執行 `clouddrive unmount`。</span><span class="sxs-lookup"><span data-stu-id="dc149-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="dc149-164">了解並確認提示。</span><span class="sxs-lookup"><span data-stu-id="dc149-164">Acknowledge and confirm the prompts.</span></span>

<span data-ttu-id="dc149-165">除非手動刪除，否則您的檔案共用將會繼續存在。</span><span class="sxs-lookup"><span data-stu-id="dc149-165">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="dc149-166">Cloud Shell 在後續的工作階段中將不再搜尋此檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="dc149-167">若要檢視更多詳細資料，請執行 `clouddrive unmount -h`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc149-167">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![執行 `clouddrive unmount` 命令](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="dc149-169">執行這個命令不會刪除任何資源。</span><span class="sxs-lookup"><span data-stu-id="dc149-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="dc149-170">手動刪除對應至 Cloud Shell 的資源群組、儲存體帳戶或檔案共用，將會永久刪除您的 `$Home` 目錄映像及檔案共用中的任何其他檔案。</span><span class="sxs-lookup"><span data-stu-id="dc149-170">Manually deleting a resource group, storage account, or file share that is mapped to Cloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="dc149-171">此動作無法復原。</span><span class="sxs-lookup"><span data-stu-id="dc149-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="dc149-172">列出 `clouddrive` 檔案共用</span><span class="sxs-lookup"><span data-stu-id="dc149-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="dc149-173">若要探索已掛接為 `clouddrive` 的檔案共用，請執行下列 `df` 命令。</span><span class="sxs-lookup"><span data-stu-id="dc149-173">To discover which file share is mounted as `clouddrive`, run the following `df` command.</span></span> 

<span data-ttu-id="dc149-174">clouddrive 檔案路徑會在 URL 中顯示您的儲存體帳戶名稱和檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-174">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="dc149-175">例如， `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="dc149-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-to-cloud-shell"></a><span data-ttu-id="dc149-176">將本機檔案傳輸至 Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="dc149-176">Transfer local files to Cloud Shell</span></span>
<span data-ttu-id="dc149-177">`clouddrive` 目錄會與 Azure 入口網站儲存體刀鋒視窗同步。</span><span class="sxs-lookup"><span data-stu-id="dc149-177">The `clouddrive` directory syncs with the Azure portal storage blade.</span></span> <span data-ttu-id="dc149-178">使用此刀鋒視窗對檔案共用雙向傳輸本機檔案。</span><span class="sxs-lookup"><span data-stu-id="dc149-178">Use this blade to transfer local files to or from your file share.</span></span> <span data-ttu-id="dc149-179">從 Cloud Shell 中更新的檔案，會在您重新整理刀鋒視窗時反映在檔案儲存體 GUI 中。</span><span class="sxs-lookup"><span data-stu-id="dc149-179">Updating files from within Cloud Shell is reflected in the file storage GUI when you refresh the blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="dc149-180">下載檔案</span><span class="sxs-lookup"><span data-stu-id="dc149-180">Download files</span></span>

![本機檔案清單](media/download.png)
1. <span data-ttu-id="dc149-182">在 Azure 入口網站中，移至掛接的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-182">In the Azure portal, go to the mounted file share.</span></span>
2. <span data-ttu-id="dc149-183">選取目標檔案。</span><span class="sxs-lookup"><span data-stu-id="dc149-183">Select the target file.</span></span>
3. <span data-ttu-id="dc149-184">選取 [下載] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc149-184">Select the **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="dc149-185">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="dc149-185">Upload files</span></span>

![要上傳的本機檔案](media/upload.png)
1. <span data-ttu-id="dc149-187">移至掛接的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc149-187">Go to your mounted file share.</span></span>
2. <span data-ttu-id="dc149-188">選取 [上傳] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc149-188">Select the **Upload** button.</span></span>
3. <span data-ttu-id="dc149-189">選取您要上傳的一或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="dc149-189">Select the file or files that you want to upload.</span></span>
4. <span data-ttu-id="dc149-190">確認上傳。</span><span class="sxs-lookup"><span data-stu-id="dc149-190">Confirm the upload.</span></span>

<span data-ttu-id="dc149-191">您現在應會看到 Cloud Shell 的 `clouddrive` 目錄中可存取的檔案。</span><span class="sxs-lookup"><span data-stu-id="dc149-191">You should now see the files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc149-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc149-192">Next steps</span></span>
[<span data-ttu-id="dc149-193">Cloud Shell 快速入門</span><span class="sxs-lookup"><span data-stu-id="dc149-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="dc149-194">
[了解 Azure 檔案儲存體](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="dc149-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="dc149-195">
[了解儲存體標籤](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="dc149-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
