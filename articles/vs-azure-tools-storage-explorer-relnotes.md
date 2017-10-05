---
title: "Microsoft Azure 儲存體總管 (預覽) 版本資訊 | Microsoft Docs"
description: "Microsoft Azure 儲存體總管 (預覽) 的版本資訊"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 63a24f6b153390533bba0888fd1051508c65bf6e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="7390b-103">Microsoft Azure 儲存體總管 (預覽) 版本資訊</span><span class="sxs-lookup"><span data-stu-id="7390b-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="7390b-104">本文包含 Microsoft Azure 儲存體總管 0.8.16 (預覽) 及先前版本的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="7390b-104">This article contains the release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="7390b-105">[Microsoft Azure 儲存體總管 (預覽)](./vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個獨立 App，可讓您在 Windows、macOS 和 Linux 上輕鬆使用 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="7390b-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="7390b-106">0.8.16 版 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="7390b-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="7390b-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="7390b-108">下載 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="7390b-109">適用於 Windows 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="7390b-110">適用於 Mac 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="7390b-111">適用於 Linux 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="7390b-112">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-112">New</span></span>
* <span data-ttu-id="7390b-113">您開啟 blob 時，如果偵測到變更，儲存體總管將提示您上傳已下載的檔案</span><span class="sxs-lookup"><span data-stu-id="7390b-113">When you open a blob, Storage Explorer will prompt you to upload the downloaded file if a change is detected</span></span>
* <span data-ttu-id="7390b-114">增強的 Azure Stack 登入體驗</span><span class="sxs-lookup"><span data-stu-id="7390b-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="7390b-115">改善同時上傳/下載許多小檔案的效能</span><span class="sxs-lookup"><span data-stu-id="7390b-115">Improved the performance of uploading/downloading many small files at the same time</span></span>


### <a name="fixes"></a><span data-ttu-id="7390b-116">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-116">Fixes</span></span>
* <span data-ttu-id="7390b-117">對於某些 blob 類型，在上傳衝突時選擇取代有時會導致重新啟動上傳。</span><span class="sxs-lookup"><span data-stu-id="7390b-117">For some blob types, choosing to "replace" during an upload conflict would sometimes result in the upload being restarted.</span></span> 
* <span data-ttu-id="7390b-118">在 0.8.15 版中，上傳有時會延滯在 99%。</span><span class="sxs-lookup"><span data-stu-id="7390b-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="7390b-119">將檔案上傳到檔案共用時，如果您選擇上傳到尚未存在的目錄，上傳會失敗。</span><span class="sxs-lookup"><span data-stu-id="7390b-119">When uploading files to a file share, if you chose to upload to a directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="7390b-120">儲存體總管未正確產生共用存取簽章和資料表查詢的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="7390b-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="7390b-121">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-121">Known Issues</span></span>
* <span data-ttu-id="7390b-122">目前無法使用名稱和金鑰連接字串。</span><span class="sxs-lookup"><span data-stu-id="7390b-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="7390b-123">這將在下一版中予以修正。</span><span class="sxs-lookup"><span data-stu-id="7390b-123">It will be fixed in the next release.</span></span> <span data-ttu-id="7390b-124">在此之前，您可以使用名稱和金鑰附加。</span><span class="sxs-lookup"><span data-stu-id="7390b-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="7390b-125">如果您嘗試開啟無效 Windows 檔案名稱的檔案，下載會導致找不到檔案的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7390b-125">If you try to open a file with an invalid Windows file name, the download will result in a file not found error.</span></span>
* <span data-ttu-id="7390b-126">按一下工作上的 [取消] 之後，該工作可能需要經過一段時間才會取消。</span><span class="sxs-lookup"><span data-stu-id="7390b-126">After clicking "Cancel" on a task, it may take a while for that task to cancel.</span></span> <span data-ttu-id="7390b-127">此為 Microsoft Azure 儲存體節點程式庫的限制。</span><span class="sxs-lookup"><span data-stu-id="7390b-127">This is a limitation of the Azure Storage Node library.</span></span>
* <span data-ttu-id="7390b-128">完成 Blob 上傳之後，系統會重新整理起始該上傳的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7390b-128">After completing a blob upload, the tab which initiated the upload is refreshed.</span></span> <span data-ttu-id="7390b-129">這和先前的行為不同，且會導致您返回所在容器的根。</span><span class="sxs-lookup"><span data-stu-id="7390b-129">This is a change from previous behavior, and will also cause you to be taken back to the root of the container you are in.</span></span>
* <span data-ttu-id="7390b-130">如果您選擇錯誤的 PIN/智慧卡憑證，則必須重新啟動，才能使儲存體總管忘記該決定。</span><span class="sxs-lookup"><span data-stu-id="7390b-130">If you choose the wrong PIN/Smartcard certificate, then you will need to restart in order to have Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="7390b-131">帳戶設定面板可能會提示您需要重新輸入認證以篩選訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7390b-131">The account settings panel may show that you need to reenter credentials to filter subscriptions.</span></span>
* <span data-ttu-id="7390b-132">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7390b-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7390b-133">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7390b-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7390b-134">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7390b-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="7390b-135">使用 Ubuntu 14.04 的使用者必須確定 GCC 編譯器集合是最新版本，這可以透過執行下列命令並重新啟動電腦來完成：</span><span class="sxs-lookup"><span data-stu-id="7390b-135">For users on Ubuntu 14.04, you will need to ensure GCC is up to date - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="7390b-136">使用 Ubuntu 17.04 的使用者必須安裝 GConf，這可以透過執行下列命令並重新啟動電腦來完成：</span><span class="sxs-lookup"><span data-stu-id="7390b-136">For users on Ubuntu 17.04, you will need to install GConf - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="7390b-137">0.8.14 版 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="7390b-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="7390b-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="7390b-139">下載 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="7390b-140">下載適用於 Windows 的 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="7390b-141">下載適用於 Mac 的 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="7390b-142">下載適用於 Linux 的 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7390b-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="7390b-143">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-143">New</span></span>

* <span data-ttu-id="7390b-144">將 Electron 版本更新至 1.7.2 以利用數個重要安全性更新</span><span class="sxs-lookup"><span data-stu-id="7390b-144">Updated Electron version to 1.7.2 in order to take advantage of several critical security updates</span></span>
* <span data-ttu-id="7390b-145">現已可從 [說明] 功能表快速存取線上疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="7390b-145">You can now quickly access the online troubleshooting guide from the help menu</span></span>
* <span data-ttu-id="7390b-146">儲存體總管疑難排解[指南][2]</span><span class="sxs-lookup"><span data-stu-id="7390b-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="7390b-147">連線至 Azure Stack 訂用帳戶的[指示][3]</span><span class="sxs-lookup"><span data-stu-id="7390b-147">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="7390b-148">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-148">Known Issues</span></span>

* <span data-ttu-id="7390b-149">在 Linux 上，刪除資料夾確認對話方塊上的按鈕不會註冊滑鼠點選。</span><span class="sxs-lookup"><span data-stu-id="7390b-149">Buttons on the delete folder confirmation dialog don't register with the mouse clicks on Linux.</span></span> <span data-ttu-id="7390b-150">因應措施為使用 Enter 鍵</span><span class="sxs-lookup"><span data-stu-id="7390b-150">Workaround is to use the Enter key</span></span>
* <span data-ttu-id="7390b-151">如果您選擇錯誤的 PIN/智慧卡憑證，則必須重新啟動，才能使儲存體總管忘記該決定</span><span class="sxs-lookup"><span data-stu-id="7390b-151">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="7390b-152">同時上傳超過 3 個 Blob 或檔案群組可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-152">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="7390b-153">帳戶設定面板可能會提示您需要重新輸入認證以篩選訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-153">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="7390b-154">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7390b-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7390b-155">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7390b-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7390b-156">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7390b-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="7390b-157">Ubuntu 14.04 安裝需要更新或升級 gcc 版本，升級步驟如下：</span><span class="sxs-lookup"><span data-stu-id="7390b-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="7390b-158">舊版</span><span class="sxs-lookup"><span data-stu-id="7390b-158">Previous releases</span></span>

* [<span data-ttu-id="7390b-159">0.8.13 版</span><span class="sxs-lookup"><span data-stu-id="7390b-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="7390b-160">0.8.12 / 0.8.11 / 0.8.10 版</span><span class="sxs-lookup"><span data-stu-id="7390b-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="7390b-161">0.8.9 / 0.8.8 版</span><span class="sxs-lookup"><span data-stu-id="7390b-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="7390b-162">0.8.7 版</span><span class="sxs-lookup"><span data-stu-id="7390b-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="7390b-163">0.8.6 版</span><span class="sxs-lookup"><span data-stu-id="7390b-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="7390b-164">0.8.5 版</span><span class="sxs-lookup"><span data-stu-id="7390b-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="7390b-165">0.8.4 版</span><span class="sxs-lookup"><span data-stu-id="7390b-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="7390b-166">0.8.3 版</span><span class="sxs-lookup"><span data-stu-id="7390b-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="7390b-167">0.8.2 版</span><span class="sxs-lookup"><span data-stu-id="7390b-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="7390b-168">0.8.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="7390b-169">0.7.20160509.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="7390b-170">0.7.20160325.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="7390b-171">0.7.20160129.1 版</span><span class="sxs-lookup"><span data-stu-id="7390b-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="7390b-172">0.7.20160105.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="7390b-173">0.7.20151116.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="7390b-174">0.8.13 版</span><span class="sxs-lookup"><span data-stu-id="7390b-174">Version 0.8.13</span></span>
<span data-ttu-id="7390b-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="7390b-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="7390b-176">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-176">New</span></span>

* <span data-ttu-id="7390b-177">儲存體總管疑難排解[指南][2]</span><span class="sxs-lookup"><span data-stu-id="7390b-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="7390b-178">連線至 Azure Stack 訂用帳戶的[指示][3]</span><span class="sxs-lookup"><span data-stu-id="7390b-178">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-179">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-179">Fixes</span></span>

* <span data-ttu-id="7390b-180">已修正︰檔案上傳先前很容易造成記憶體不足錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="7390b-181">已修正：您現在可以使用 PIN/智慧卡登入</span><span class="sxs-lookup"><span data-stu-id="7390b-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="7390b-182">已修正：[在入口網站中開啟] 現已可以搭配 Azure 中國、Azure 德國、Azure 美國政府及 Azure Stack 運作</span><span class="sxs-lookup"><span data-stu-id="7390b-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="7390b-183">已修正：先前將資料夾上傳至 Blob 容器時，有時候會發生「作業不合法」錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-183">Fixed: While uploading a folder to a blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="7390b-184">已修正：先前在管理快照集時會停用 [全選]</span><span class="sxs-lookup"><span data-stu-id="7390b-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="7390b-185">已修正：在檢視基底 Blob 的快照集屬性後，可能會覆寫該基底 Blob 的中繼資料</span><span class="sxs-lookup"><span data-stu-id="7390b-185">Fixed: The metadata of the base blob might get overwritten after viewing the properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-186">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-186">Known Issues</span></span>

* <span data-ttu-id="7390b-187">如果您選擇錯誤的 PIN/智慧卡憑證，則必須重新啟動，才能使儲存體總管忘記該決定</span><span class="sxs-lookup"><span data-stu-id="7390b-187">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="7390b-188">在放大或縮小期間，縮放層級可能會暫時重設為預設層級</span><span class="sxs-lookup"><span data-stu-id="7390b-188">While zoomed in or out, the zoom level may momentarily reset to the default level</span></span>
* <span data-ttu-id="7390b-189">同時上傳超過 3 個 Blob 或檔案群組可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-189">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="7390b-190">帳戶設定面板可能會提示您需要重新輸入認證以篩選訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-190">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="7390b-191">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7390b-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7390b-192">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7390b-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7390b-193">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7390b-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="7390b-194">Ubuntu 14.04 安裝需要更新或升級 gcc 版本，升級步驟如下：</span><span class="sxs-lookup"><span data-stu-id="7390b-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="7390b-195">0.8.12 / 0.8.11 / 0.8.10 版</span><span class="sxs-lookup"><span data-stu-id="7390b-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="7390b-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="7390b-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="7390b-197">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-197">New</span></span>

* <span data-ttu-id="7390b-198">儲存體總管現在會在您從更新通知安裝更新之後自動關閉</span><span class="sxs-lookup"><span data-stu-id="7390b-198">Storage Explorer will now automatically close when you install an update from the update notification</span></span>
* <span data-ttu-id="7390b-199">就地快速存取能針對您經常存取的資源提供加強的使用體驗</span><span class="sxs-lookup"><span data-stu-id="7390b-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="7390b-200">在 Blob 容器編輯器中，您現在可以查看租用 Blob 所屬的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7390b-200">In the Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="7390b-201">現已能摺疊左側面板</span><span class="sxs-lookup"><span data-stu-id="7390b-201">You can now collapse the left side panel</span></span>
* <span data-ttu-id="7390b-202">探索現在會和下載同時執行</span><span class="sxs-lookup"><span data-stu-id="7390b-202">Discovery now runs at the same time as download</span></span>
* <span data-ttu-id="7390b-203">使用 Blob 容器、檔案共用及資料表編輯器中的 [統計資料] 來查看您資源或選取項目的大小</span><span class="sxs-lookup"><span data-stu-id="7390b-203">Use Statistics in the Blob Container, File Share, and Table editors to see the size of your resource or selection</span></span>
* <span data-ttu-id="7390b-204">現已能登入以 Azure Active Directory (AAD) 為基礎的 Azure Stack 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7390b-204">You can now sign-in to Azure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="7390b-205">現已能將大小超過 32MB 的封存檔案上傳至進階儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-205">You can now upload archive files over 32MB to Premium storage accounts</span></span>
* <span data-ttu-id="7390b-206">改善協助工具支援</span><span class="sxs-lookup"><span data-stu-id="7390b-206">Improved accessibility support</span></span>
* <span data-ttu-id="7390b-207">現已能移至 [編輯] -&gt; [SSL 憑證] -&gt; [匯入憑證] 來新增受信任的 Base-64 編碼 X.509 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="7390b-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going to Edit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-208">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-208">Fixes</span></span>

* <span data-ttu-id="7390b-209">已修正：先前在重新整理帳戶的認證之後，樹狀檢視有時候不會自動重新整理</span><span class="sxs-lookup"><span data-stu-id="7390b-209">Fixed: after refreshing an account's credentials, the tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="7390b-210">已修正：先前針對模擬器佇列和資料表產生 SAS 會導致無效的 URL</span><span class="sxs-lookup"><span data-stu-id="7390b-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="7390b-211">已修正：進階儲存體帳戶現在可以在啟用 Proxy 時展開</span><span class="sxs-lookup"><span data-stu-id="7390b-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="7390b-212">已修正：先前在選取 1 或 0 個帳戶的情況下，帳戶管理頁面的 [套用] 按鈕會無法運作</span><span class="sxs-lookup"><span data-stu-id="7390b-212">Fixed: the apply button on the accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="7390b-213">已修正：上傳需要衝突解決的 Blob 可能會失敗 - 已在 0.8.11 中修正</span><span class="sxs-lookup"><span data-stu-id="7390b-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="7390b-214">已修正：傳送意見反應的功能在 0.8.11 中無法運作 - 已在 0.8.12 中修正</span><span class="sxs-lookup"><span data-stu-id="7390b-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="7390b-215">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-215">Known Issues</span></span>

* <span data-ttu-id="7390b-216">升級至 0.8.10 之後，您必須重新整理所有認證。</span><span class="sxs-lookup"><span data-stu-id="7390b-216">After upgrading to 0.8.10, you will need to refresh all of your credentials.</span></span>
* <span data-ttu-id="7390b-217">在放大或縮小期間，縮放層級可能會暫時重設為預設層級。</span><span class="sxs-lookup"><span data-stu-id="7390b-217">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="7390b-218">同時上傳超過 3 個 Blob 或檔案群組可能會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="7390b-218">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>
* <span data-ttu-id="7390b-219">帳戶設定面板可能會提示您需要重新輸入認證以篩選訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7390b-219">The account settings panel may show that you need to reenter credentials in order to filter subscriptions.</span></span>
* <span data-ttu-id="7390b-220">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7390b-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7390b-221">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7390b-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7390b-222">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7390b-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="7390b-223">Ubuntu 14.04 安裝需要更新或升級 gcc 版本，升級步驟如下：</span><span class="sxs-lookup"><span data-stu-id="7390b-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="7390b-224">0.8.9 / 0.8.8 版</span><span class="sxs-lookup"><span data-stu-id="7390b-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="7390b-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="7390b-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="7390b-226">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-226">New</span></span>

* <span data-ttu-id="7390b-227">儲存體總管 0.8.9 將會自動下載最新版本的更新。</span><span class="sxs-lookup"><span data-stu-id="7390b-227">Storage Explorer 0.8.9 will automatically download the latest version for updates.</span></span>
* <span data-ttu-id="7390b-228">Hotfix：先前使用由入口網站所產生的 SAS URI 來附加儲存體帳戶將會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="7390b-228">Hotfix: using a portal generated SAS URI to attach a storage account would result in an error.</span></span>
* <span data-ttu-id="7390b-229">現已能針對 Blob 快照集進行建立、管理及升階。</span><span class="sxs-lookup"><span data-stu-id="7390b-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="7390b-230">現已能登入 Azure 中國、Azure 德國及 Azure 美國政府帳戶。</span><span class="sxs-lookup"><span data-stu-id="7390b-230">You can now sign in to Azure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="7390b-231">現已能變更縮放層級。</span><span class="sxs-lookup"><span data-stu-id="7390b-231">You can now change the zoom level.</span></span> <span data-ttu-id="7390b-232">使用 [檢視] 功能表中的選項來放大、縮小及重設縮放。</span><span class="sxs-lookup"><span data-stu-id="7390b-232">Use the options in the View menu to Zoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="7390b-233">Blob 和檔案的使用者中繼資料現已支援 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="7390b-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="7390b-234">協助工具改進。</span><span class="sxs-lookup"><span data-stu-id="7390b-234">Accessibility improvements.</span></span>
* <span data-ttu-id="7390b-235">可從更新通知中檢視下個版本的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="7390b-235">The next version's release notes can be viewed from the update notification.</span></span> <span data-ttu-id="7390b-236">您也可以從 [說明] 功能表檢視目前版本的資訊。</span><span class="sxs-lookup"><span data-stu-id="7390b-236">You can also view the current release notes from the Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-237">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-237">Fixes</span></span>

* <span data-ttu-id="7390b-238">已修正：版本號碼現在已會正確顯示於 Windows 上的 [控制台] 中</span><span class="sxs-lookup"><span data-stu-id="7390b-238">Fixed: the version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="7390b-239">已修正：搜尋已不再具有 50,000 個節點的限制</span><span class="sxs-lookup"><span data-stu-id="7390b-239">Fixed: search is no longer limited to 50,000 nodes</span></span>
* <span data-ttu-id="7390b-240">已修正：在目的地目錄不存在的情況下，上傳至檔案共用會卡在無限的迴圈之中</span><span class="sxs-lookup"><span data-stu-id="7390b-240">Fixed: upload to a file share spun forever if the destination directory did not already exist</span></span>
* <span data-ttu-id="7390b-241">已修正：改善較長上傳及下載的穩定性</span><span class="sxs-lookup"><span data-stu-id="7390b-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-242">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-242">Known Issues</span></span>

* <span data-ttu-id="7390b-243">在放大或縮小期間，縮放層級可能會暫時重設為預設層級。</span><span class="sxs-lookup"><span data-stu-id="7390b-243">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="7390b-244">快速存取僅適用於以訂用帳戶為基礎的項目。</span><span class="sxs-lookup"><span data-stu-id="7390b-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="7390b-245">此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源。</span><span class="sxs-lookup"><span data-stu-id="7390b-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="7390b-246">視您擁有的資源數量而定，快速存取可能需要幾秒鐘才能瀏覽至目標資源。</span><span class="sxs-lookup"><span data-stu-id="7390b-246">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="7390b-247">同時上傳超過 3 個 Blob 或檔案群組可能會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="7390b-247">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>

<span data-ttu-id="7390b-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="7390b-249">0.8.7 版</span><span class="sxs-lookup"><span data-stu-id="7390b-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7390b-250">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-250">New</span></span>

* <span data-ttu-id="7390b-251">在剛開始更新、下載或複製工作階段時，您可以在 [活動] 視窗中選擇如何解決衝突</span><span class="sxs-lookup"><span data-stu-id="7390b-251">You can choose how to resolve conflicts at the beginning of an update, download or copy session in the Activities window</span></span>
* <span data-ttu-id="7390b-252">將游標暫留在索引標籤上可以看到儲存體資源的完整路徑</span><span class="sxs-lookup"><span data-stu-id="7390b-252">Hover over a tab to see the full path of the storage resource</span></span>
* <span data-ttu-id="7390b-253">按一下索引標籤之後，它會與左側導覽窗格中的位置同步</span><span class="sxs-lookup"><span data-stu-id="7390b-253">When you click on a tab, it synchronizes with its location in the left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-254">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-254">Fixes</span></span>

* <span data-ttu-id="7390b-255">已修正：儲存體總管在 Mac 上現已是受信任的應用程式</span><span class="sxs-lookup"><span data-stu-id="7390b-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="7390b-256">已修正：再次支援 Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="7390b-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="7390b-257">已修正：「新增帳戶」UI 在載入訂用帳戶時有時會閃爍</span><span class="sxs-lookup"><span data-stu-id="7390b-257">Fixed: Sometimes the add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="7390b-258">已修正：左側導覽窗格中有時不會列出所有儲存體資源</span><span class="sxs-lookup"><span data-stu-id="7390b-258">Fixed: Sometimes not all storage resources were listed in the left side navigation pane</span></span>
* <span data-ttu-id="7390b-259">已修正：[動作] 窗格有時會顯示空白動作</span><span class="sxs-lookup"><span data-stu-id="7390b-259">Fixed: The action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="7390b-260">已修正：現已會保留上次工作階段關閉時的視窗大小</span><span class="sxs-lookup"><span data-stu-id="7390b-260">Fixed: The window size from the last closed session is now retained</span></span>
* <span data-ttu-id="7390b-261">已修正：可以使用內容選單針對相同資源開啟多個索引標籤</span><span class="sxs-lookup"><span data-stu-id="7390b-261">Fixed: You can open multiple tabs for the same resource using the context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-262">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-262">Known Issues</span></span>

* <span data-ttu-id="7390b-263">快速存取僅適用於以訂用帳戶為基礎的項目。</span><span class="sxs-lookup"><span data-stu-id="7390b-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="7390b-264">此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源</span><span class="sxs-lookup"><span data-stu-id="7390b-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="7390b-265">視您擁有的資源數量而定，快速存取可能需要幾秒鐘才能瀏覽至目標資源</span><span class="sxs-lookup"><span data-stu-id="7390b-265">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="7390b-266">同時上傳超過 3 個 Blob 或檔案群組可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-266">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="7390b-267">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能或造成未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="7390b-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="7390b-268">在 macOS 上第一次使用儲存體總管時，系統可能會多次要求使用者的許可，以存取鑰匙圈。</span><span class="sxs-lookup"><span data-stu-id="7390b-268">For the first time using the Storage Explorer on macOS, you might see multiple prompts asking for user's permission to access keychain.</span></span> <span data-ttu-id="7390b-269">建議您選取 [一律允許] 來使系統不會再次顯示該提示</span><span class="sxs-lookup"><span data-stu-id="7390b-269">We suggest you select Always Allow so the prompt won't show up again</span></span>

<span data-ttu-id="7390b-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="7390b-271">0.8.6 版</span><span class="sxs-lookup"><span data-stu-id="7390b-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="7390b-272">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-272">New</span></span>

* <span data-ttu-id="7390b-273">現已可將常用的服務釘選到 Quick Access 以便瀏覽</span><span class="sxs-lookup"><span data-stu-id="7390b-273">You can now pin most frequently used services to the Quick Access for easy navigation</span></span>
* <span data-ttu-id="7390b-274">現已可在多個索引標籤開啟多個編輯器。</span><span class="sxs-lookup"><span data-stu-id="7390b-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="7390b-275">按一下以開啟暫時索引標籤；按兩下以開啟永久索引標籤。您也可以按一下暫時索引標籤來將它設為永久索引標籤</span><span class="sxs-lookup"><span data-stu-id="7390b-275">Single click to open a temporary tab; double click to open a permanent tab. You can also click on the temporary tab to make it a permanent tab</span></span>
* <span data-ttu-id="7390b-276">我們已大幅改善上傳及下載的效能和穩定性，尤其是在高效能機器上處理大型檔案的情況</span><span class="sxs-lookup"><span data-stu-id="7390b-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="7390b-277">現可在 Blob 容器內建立空白的「虛擬」資料夾</span><span class="sxs-lookup"><span data-stu-id="7390b-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="7390b-278">我們已重新推出範圍搜尋，並搭配全新增強的子字串搜尋，因此您現在將會有兩種搜尋的選項：</span><span class="sxs-lookup"><span data-stu-id="7390b-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="7390b-279">全域搜尋：請直接在搜尋文字方塊中輸入搜尋字詞</span><span class="sxs-lookup"><span data-stu-id="7390b-279">Global search - just enter a search term into the search textbox</span></span>
    * <span data-ttu-id="7390b-280">範圍搜尋：按一下位於節點旁邊的放大鏡圖示，然後將搜尋字詞新增至路徑末端，或是以滑鼠右鍵按一下並選取 [從這裡搜尋]</span><span class="sxs-lookup"><span data-stu-id="7390b-280">Scoped search - click the magnifying glass icon next to a node, then add a search term to the end of the path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="7390b-281">已新增多種佈景主題：淺色 (預設)、深色、黑色高對比和白色高對比。</span><span class="sxs-lookup"><span data-stu-id="7390b-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="7390b-282">移至 [編輯] -&gt; [佈景主題] 來變更佈景主題喜好設定</span><span class="sxs-lookup"><span data-stu-id="7390b-282">Go to Edit -&gt; Themes to change your theming preference</span></span>
* <span data-ttu-id="7390b-283">您可以修改 Blob 和檔案的屬性</span><span class="sxs-lookup"><span data-stu-id="7390b-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="7390b-284">我們現已支援編碼 (base64) 及未編碼的佇列訊息</span><span class="sxs-lookup"><span data-stu-id="7390b-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="7390b-285">若使用 Linux，必須為 64 位元作業系統。</span><span class="sxs-lookup"><span data-stu-id="7390b-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="7390b-286">針對此版本，我們僅支援 64 位元的 Ubuntu 16.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="7390b-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="7390b-287">已更新我們的標誌！</span><span class="sxs-lookup"><span data-stu-id="7390b-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-288">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-288">Fixes</span></span>

* <span data-ttu-id="7390b-289">已修正︰畫面凍結的問題</span><span class="sxs-lookup"><span data-stu-id="7390b-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="7390b-290">已修正：增強安全性</span><span class="sxs-lookup"><span data-stu-id="7390b-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="7390b-291">已修正：有時候可能會出現重複的附加帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="7390b-292">已修正：具有未定義內容類型的 Blob 可能會產生例外狀況</span><span class="sxs-lookup"><span data-stu-id="7390b-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="7390b-293">已修正：先前並無法在空白資料表上開啟 [查詢] 面板</span><span class="sxs-lookup"><span data-stu-id="7390b-293">Fixed: Opening the Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="7390b-294">已修正：數個搜尋功能中的錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="7390b-295">已修正：按一下 [載入更多] 時所載入資源的數目已從 50 提升至 100</span><span class="sxs-lookup"><span data-stu-id="7390b-295">Fixed: Increased the number of resources loaded from 50 to 100 when clicking "Load More"</span></span>
* <span data-ttu-id="7390b-296">已修正：首次執行時，如果已登入某個帳戶，現在預設會選取該帳戶的所有定用帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="7390b-297">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-297">Known Issues</span></span>

* <span data-ttu-id="7390b-298">此版本的儲存體總管並無法在 Ubuntu 14.04 上執行</span><span class="sxs-lookup"><span data-stu-id="7390b-298">This release of the Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="7390b-299">若要針對相同資源開啟多個索引標籤，請不要持續點選相同的資源。</span><span class="sxs-lookup"><span data-stu-id="7390b-299">To open multiple tabs for the same resource, do not continuously click on the same resource.</span></span> <span data-ttu-id="7390b-300">請先按一下其他資源，然後再返回按一下原始資源，以在另一個索引標籤上再次開啟它</span><span class="sxs-lookup"><span data-stu-id="7390b-300">Click on another resource and then go back and then click on the original resource to open it again in another tab</span></span> 
* <span data-ttu-id="7390b-301">快速存取僅適用於以訂用帳戶為基礎的項目。</span><span class="sxs-lookup"><span data-stu-id="7390b-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="7390b-302">此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源</span><span class="sxs-lookup"><span data-stu-id="7390b-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="7390b-303">視您擁有的資源數量而定，快速存取可能需要幾秒鐘才能瀏覽至目標資源</span><span class="sxs-lookup"><span data-stu-id="7390b-303">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="7390b-304">同時上傳超過 3 個 Blob 或檔案群組可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-304">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="7390b-305">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能或造成未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="7390b-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="7390b-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="7390b-307">0.8.5 版</span><span class="sxs-lookup"><span data-stu-id="7390b-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="7390b-308">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-308">New</span></span>

* <span data-ttu-id="7390b-309">現已能使用由入口網站所產生的 SAS 金鑰來附加儲存體帳戶和資源</span><span class="sxs-lookup"><span data-stu-id="7390b-309">Can now use Portal-generated SAS keys to attach to Storage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-310">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-310">Fixes</span></span>

* <span data-ttu-id="7390b-311">已修正：先前在搜尋期間的競爭條件有時候會使節點無法展開</span><span class="sxs-lookup"><span data-stu-id="7390b-311">Fixed: race condition during search sometimes caused nodes to become non-expandable</span></span>
* <span data-ttu-id="7390b-312">已修正：在以帳戶名稱和金鑰連線至儲存體帳戶時，[使用 HTTP] 會無法運作</span><span class="sxs-lookup"><span data-stu-id="7390b-312">Fixed: "Use HTTP" doesn't work when connecting to Storage Accounts with account name and key</span></span>
* <span data-ttu-id="7390b-313">已修正：SAS 金鑰 (特別是由入口網站所產生的 SAS 金鑰) 會傳回「結尾斜線」錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="7390b-314">已修正：資料表匯入問題</span><span class="sxs-lookup"><span data-stu-id="7390b-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="7390b-315">資料分割索引鍵和列索引鍵有時候會反轉</span><span class="sxs-lookup"><span data-stu-id="7390b-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="7390b-316">無法讀取 "null" 資料分割索引鍵</span><span class="sxs-lookup"><span data-stu-id="7390b-316">Unable to read "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-317">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-317">Known Issues</span></span>

* <span data-ttu-id="7390b-318">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能</span><span class="sxs-lookup"><span data-stu-id="7390b-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="7390b-319">Azure Stack 目前不支援 [檔案]，因此嘗試展開 [檔案] 將會顯示錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-319">Azure Stack doesn't currently support Files, so trying to expand Files will show an error</span></span>

<span data-ttu-id="7390b-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="7390b-321">0.8.4 版</span><span class="sxs-lookup"><span data-stu-id="7390b-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7390b-322">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-322">New</span></span>

* <span data-ttu-id="7390b-323">產生針對儲存體帳戶、容器、佇列、資料表或檔案共用的直接連結，以便共用及輕鬆存取資源 - Windows 與 Mac 作業系統支援</span><span class="sxs-lookup"><span data-stu-id="7390b-323">Generate direct links to storage accounts, containers, queues, tables, or file shares for sharing and easy access to your resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="7390b-324">從搜尋方塊搜尋 Blob 容器、資料表、佇列、檔案共用或儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-324">Search for your blob containers, tables, queues, file shares, or storage accounts from the search box</span></span>
* <span data-ttu-id="7390b-325">現已能在資料表查詢建立器中對子句進行群組</span><span class="sxs-lookup"><span data-stu-id="7390b-325">You can now group clauses in the table query builder</span></span>
* <span data-ttu-id="7390b-326">從 SAS 附加帳戶及容器內對 Blob 容器、檔案共用、資料表、Blob、Blob 資料夾、檔案及目錄進行重新命名和複製/貼上</span><span class="sxs-lookup"><span data-stu-id="7390b-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="7390b-327">對 Blob 容器和檔案共用進行重新命名和複製時，現在會保留屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="7390b-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-328">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-328">Fixes</span></span>

* <span data-ttu-id="7390b-329">已修正：無法編輯包含布林值或二進位屬性的資料表實體</span><span class="sxs-lookup"><span data-stu-id="7390b-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-330">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-330">Known Issues</span></span>

* <span data-ttu-id="7390b-331">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能</span><span class="sxs-lookup"><span data-stu-id="7390b-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="7390b-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="7390b-333">0.8.3 版</span><span class="sxs-lookup"><span data-stu-id="7390b-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7390b-334">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-334">New</span></span>

* <span data-ttu-id="7390b-335">對容器、資料表、檔案共用進行重新命名</span><span class="sxs-lookup"><span data-stu-id="7390b-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="7390b-336">改善查詢建立器體驗</span><span class="sxs-lookup"><span data-stu-id="7390b-336">Improved Query builder experience</span></span>
* <span data-ttu-id="7390b-337">能夠儲存及載入查詢</span><span class="sxs-lookup"><span data-stu-id="7390b-337">Ability to save and load queries</span></span>
* <span data-ttu-id="7390b-338">針對儲存體帳戶或容器、佇列、資料表或檔案共用的直接連結，可用來進行共用及輕鬆存取資源 (僅限 Windows，macOS 支援即將推出！)</span><span class="sxs-lookup"><span data-stu-id="7390b-338">Direct links to storage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="7390b-339">能夠管理及設定 CORS 規則</span><span class="sxs-lookup"><span data-stu-id="7390b-339">Ability to manage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-340">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-340">Fixes</span></span>

* <span data-ttu-id="7390b-341">已修正：Microsoft 帳戶每 8 至 12 小時便需要重新驗證</span><span class="sxs-lookup"><span data-stu-id="7390b-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-342">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-342">Known Issues</span></span>

* <span data-ttu-id="7390b-343">UI 有時候會呈現為凍結的情況，將視窗最大化能協助解決此問題</span><span class="sxs-lookup"><span data-stu-id="7390b-343">Sometimes the UI might appear frozen - maximizing the window helps resolve this issue</span></span>
* <span data-ttu-id="7390b-344">macOS 安裝可能會需要較高的權限</span><span class="sxs-lookup"><span data-stu-id="7390b-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="7390b-345">帳戶設定面板可能會提示您需要重新輸入認證以篩選訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-345">Account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="7390b-346">對檔案共用、Blob 容器及資料表進行重新命名，並不會保留中繼資料或容器上的其他屬性，例如檔案共用配額、公用存取層級或存取原則</span><span class="sxs-lookup"><span data-stu-id="7390b-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on the container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="7390b-347">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7390b-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7390b-348">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留</span><span class="sxs-lookup"><span data-stu-id="7390b-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="7390b-349">在 SAS 附加帳戶內並無法對資源進行複製或重新命名</span><span class="sxs-lookup"><span data-stu-id="7390b-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="7390b-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="7390b-351">0.8.2 版</span><span class="sxs-lookup"><span data-stu-id="7390b-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7390b-352">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-352">New</span></span>

* <span data-ttu-id="7390b-353">儲存體帳戶是依訂用帳戶進行群組。透過金鑰或 SAS 附加的開發儲存體和資源會顯示在 (本機和附加的) 節點之下</span><span class="sxs-lookup"><span data-stu-id="7390b-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="7390b-354">在 [Azure 帳戶設定] 面板中登出帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="7390b-355">設定 Proxy 設定以啟用並管理登入</span><span class="sxs-lookup"><span data-stu-id="7390b-355">Configure proxy settings to enable and manage sign-in</span></span>
* <span data-ttu-id="7390b-356">建立和中斷 Blob 租用</span><span class="sxs-lookup"><span data-stu-id="7390b-356">Create and break blob leases</span></span>
* <span data-ttu-id="7390b-357">按一下便能開啟 Blob 容器、佇列、資料表及檔案</span><span class="sxs-lookup"><span data-stu-id="7390b-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-358">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-358">Fixes</span></span>

* <span data-ttu-id="7390b-359">已修正：使用 .NET 或 Java 程式庫插入的佇列訊息沒有從 base64 正確解碼</span><span class="sxs-lookup"><span data-stu-id="7390b-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="7390b-360">已修正：$metrics 資料表不會針對 Blob 儲存體帳戶顯示</span><span class="sxs-lookup"><span data-stu-id="7390b-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="7390b-361">已修正：資料表節點無法用於本機 (開發) 儲存體</span><span class="sxs-lookup"><span data-stu-id="7390b-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-362">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-362">Known Issues</span></span>

* <span data-ttu-id="7390b-363">macOS 安裝可能會需要較高的權限</span><span class="sxs-lookup"><span data-stu-id="7390b-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="7390b-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="7390b-365">0.8.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7390b-366">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-366">New</span></span>

* <span data-ttu-id="7390b-367">檔案共用支援：檢視、上傳、下載、複製檔案和目錄、SAS URI (建立和連線)</span><span class="sxs-lookup"><span data-stu-id="7390b-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="7390b-368">改善透過 SAS URI 或帳戶金鑰連線至儲存體的使用者體驗</span><span class="sxs-lookup"><span data-stu-id="7390b-368">Improved user experience for connecting to Storage with SAS URIs or account keys</span></span>
* <span data-ttu-id="7390b-369">匯出資料表查詢結果</span><span class="sxs-lookup"><span data-stu-id="7390b-369">Export table query results</span></span>
* <span data-ttu-id="7390b-370">針對資料表資料行的重新排列和自訂</span><span class="sxs-lookup"><span data-stu-id="7390b-370">Table column reordering and customization</span></span>
* <span data-ttu-id="7390b-371">搭配啟用的計量檢視儲存體帳戶的 $logs Blob 容器和 $metrics 資料表</span><span class="sxs-lookup"><span data-stu-id="7390b-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="7390b-372">改善匯出和匯入行為，現已包含屬性值類型</span><span class="sxs-lookup"><span data-stu-id="7390b-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-373">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-373">Fixes</span></span>

* <span data-ttu-id="7390b-374">已修正：上傳或下載大型 Blob 可能會導致不完整的上傳/下載</span><span class="sxs-lookup"><span data-stu-id="7390b-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="7390b-375">已修正：編輯、新增或匯入具有數值字串值 ("1") 的實體會將它轉換為 double</span><span class="sxs-lookup"><span data-stu-id="7390b-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it to double</span></span>
* <span data-ttu-id="7390b-376">已修正：無法在本機開發環境中展開資料表節點</span><span class="sxs-lookup"><span data-stu-id="7390b-376">Fixed: Unable to expand the table node in the local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-377">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-377">Known Issues</span></span>

* <span data-ttu-id="7390b-378">$metrics 資料表不會針對 Blob 儲存體帳戶顯示</span><span class="sxs-lookup"><span data-stu-id="7390b-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="7390b-379">如果以程式設計方式新增的佇列訊息是使用 Base64 編碼方式進行編碼，則該訊息可能會無法正確顯示</span><span class="sxs-lookup"><span data-stu-id="7390b-379">Queue messages added programmatically may not be displayed correctly if the messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="7390b-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="7390b-381">0.7.20160509.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="7390b-382">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-382">New</span></span>

* <span data-ttu-id="7390b-383">改善應用程式當機的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="7390b-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-384">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-384">Fixes</span></span>

* <span data-ttu-id="7390b-385">已修正在需要登入認證時，InfoBar 訊息有時候不會顯示的錯誤</span><span class="sxs-lookup"><span data-stu-id="7390b-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-386">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-386">Known Issues</span></span>

* <span data-ttu-id="7390b-387">資料表：新增、編輯或匯入具有不明確數值 (例如 "1" 或 "1.0") 的實體，且使用者嘗試將它傳送為 `Edm.String` 時，該值將會透過用戶端 API 以 Edm.Double 的形式傳回</span><span class="sxs-lookup"><span data-stu-id="7390b-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>

<span data-ttu-id="7390b-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="7390b-389">0.7.20160325.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="7390b-390">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-390">New</span></span>

* <span data-ttu-id="7390b-391">資料表支援：針對實體的檢視、查詢、匯出、匯入及 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="7390b-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="7390b-392">佇列支援：針對訊息進行檢視、新增、清除佇列</span><span class="sxs-lookup"><span data-stu-id="7390b-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="7390b-393">針對儲存體帳戶產生 SAS URI</span><span class="sxs-lookup"><span data-stu-id="7390b-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="7390b-394">透過 SAS URI 連線至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-394">Connecting to Storage Accounts with SAS URIs</span></span>
* <span data-ttu-id="7390b-395">針對儲存體總管未來更新的更新通知</span><span class="sxs-lookup"><span data-stu-id="7390b-395">Update notifications for future updates to Storage Explorer</span></span>
* <span data-ttu-id="7390b-396">更新外觀與風格</span><span class="sxs-lookup"><span data-stu-id="7390b-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-397">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-397">Fixes</span></span>

* <span data-ttu-id="7390b-398">改善效能和可靠性</span><span class="sxs-lookup"><span data-stu-id="7390b-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="7390b-399">已知問題 &amp; 緩解方式</span><span class="sxs-lookup"><span data-stu-id="7390b-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="7390b-400">下載大型 Blob 檔案並無法正確運作。在我們解決此問題的期間，建議您使用 AzCopy</span><span class="sxs-lookup"><span data-stu-id="7390b-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="7390b-401">如果找不到主資料夾，或是無法寫入該資料夾，則不會擷取或快取帳戶認證</span><span class="sxs-lookup"><span data-stu-id="7390b-401">Account credentials will not be retrieved nor cached if the home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="7390b-402">在新增、編輯或匯入具有不明確數值 (例如 "1" 或 "1.0") 的實體，且使用者嘗試將它傳送為 `Edm.String` 時，該值將會透過用戶端 API 以 Edm.Double 的形式傳回</span><span class="sxs-lookup"><span data-stu-id="7390b-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>
* <span data-ttu-id="7390b-403">匯入具有多行記錄的 CSV 檔案時，資料可能會變得破碎或變成亂碼</span><span class="sxs-lookup"><span data-stu-id="7390b-403">When importing CSV files with multiline records, the data may get chopped or scrambled</span></span>

<span data-ttu-id="7390b-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="7390b-405">0.7.20160129.1 版</span><span class="sxs-lookup"><span data-stu-id="7390b-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-406">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-406">Fixes</span></span>

* <span data-ttu-id="7390b-407">改善上傳、下載及複製 Blob 的整體效能</span><span class="sxs-lookup"><span data-stu-id="7390b-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="7390b-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="7390b-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="7390b-409">0.7.20160105.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="7390b-410">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-410">New</span></span>

* <span data-ttu-id="7390b-411">Linux 支援 (和 OSX 相同的功能)</span><span class="sxs-lookup"><span data-stu-id="7390b-411">Linux support (parity features to OSX)</span></span>
* <span data-ttu-id="7390b-412">新增具有共用存取簽章 (SAS) 金鑰的 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="7390b-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="7390b-413">新增 Azure 中國的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="7390b-414">新增具有自訂端點的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7390b-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="7390b-415">開啟及檢視內容文字和圖片 Blob</span><span class="sxs-lookup"><span data-stu-id="7390b-415">Open and view the contents text and picture blobs</span></span>
* <span data-ttu-id="7390b-416">檢視及編輯 Blob 屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="7390b-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="7390b-417">修正</span><span class="sxs-lookup"><span data-stu-id="7390b-417">Fixes</span></span>

* <span data-ttu-id="7390b-418">已修正：上傳或下載大量的 Blob (超過 500 個) 時，有時候可能會導致應用程式出現白色畫面</span><span class="sxs-lookup"><span data-stu-id="7390b-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause the app to have a white screen</span></span> 
* <span data-ttu-id="7390b-419">已修正：設定 Blob 容器公用存取層級時，在您重新將焦點設定在容器上之前，新的值將不會更新。</span><span class="sxs-lookup"><span data-stu-id="7390b-419">Fixed: when setting blob container public access level, the new value is not updated until you re-set the focus on the container.</span></span> <span data-ttu-id="7390b-420">此外，對話方塊預設一律會顯示「無公用存取」，而非目前實際的值。</span><span class="sxs-lookup"><span data-stu-id="7390b-420">Also, the dialog always defaults to "No public access", and not the actual current value.</span></span>
* <span data-ttu-id="7390b-421">更佳的整體鍵盤/協助工具及 UI 支援</span><span class="sxs-lookup"><span data-stu-id="7390b-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="7390b-422">階層連結記錄在因大量空白字元而變得過長時便會自動換行</span><span class="sxs-lookup"><span data-stu-id="7390b-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="7390b-423">SAS 對話方塊支援輸入驗證</span><span class="sxs-lookup"><span data-stu-id="7390b-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="7390b-424">本機存放區在使用者認證過期後仍會持續可用</span><span class="sxs-lookup"><span data-stu-id="7390b-424">Local storage continues to be available even if user credentials have expired</span></span>
* <span data-ttu-id="7390b-425">刪除已開啟的 Blob 容器時，便會關閉位於右側的 Blob 總管</span><span class="sxs-lookup"><span data-stu-id="7390b-425">When an opened blob container is deleted, the blob explorer on the right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-426">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-426">Known Issues</span></span>

* <span data-ttu-id="7390b-427">Linux 安裝需要更新或升級 gcc 版本，升級步驟如下：</span><span class="sxs-lookup"><span data-stu-id="7390b-427">Linux install needs gcc version updated or upgraded – steps to upgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="7390b-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="7390b-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="7390b-429">0.7.20151116.0 版</span><span class="sxs-lookup"><span data-stu-id="7390b-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="7390b-430">新增</span><span class="sxs-lookup"><span data-stu-id="7390b-430">New</span></span>

* <span data-ttu-id="7390b-431">macOS 及 Windows 版本</span><span class="sxs-lookup"><span data-stu-id="7390b-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="7390b-432">登入以檢視儲存體帳戶，使用您的組織帳戶、Microsoft 帳戶、2FA 等等。</span><span class="sxs-lookup"><span data-stu-id="7390b-432">Sign in to view your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="7390b-433">本機開發儲存體 (使用儲存體模擬器，僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="7390b-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="7390b-434">Azure Resource Manager 和傳統資源支援</span><span class="sxs-lookup"><span data-stu-id="7390b-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="7390b-435">建立及刪除 Blob、佇列或資料表</span><span class="sxs-lookup"><span data-stu-id="7390b-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="7390b-436">搜尋特定的 Blob、佇列或資料表</span><span class="sxs-lookup"><span data-stu-id="7390b-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="7390b-437">瀏覽 Blob 容器的內容</span><span class="sxs-lookup"><span data-stu-id="7390b-437">Explore the contents of blob containers</span></span>
* <span data-ttu-id="7390b-438">檢視並瀏覽目錄</span><span class="sxs-lookup"><span data-stu-id="7390b-438">View and navigate through directories</span></span>
* <span data-ttu-id="7390b-439">上傳、下載及刪除 Blob 和資料夾</span><span class="sxs-lookup"><span data-stu-id="7390b-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="7390b-440">檢視及編輯 Blob 屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="7390b-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="7390b-441">產生 SAS 金鑰</span><span class="sxs-lookup"><span data-stu-id="7390b-441">Generate SAS keys</span></span>
* <span data-ttu-id="7390b-442">管理及建立儲存的存取原則 (SAP)</span><span class="sxs-lookup"><span data-stu-id="7390b-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="7390b-443">使用前置詞搜尋 Blob</span><span class="sxs-lookup"><span data-stu-id="7390b-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="7390b-444">拖放檔案以上傳或下載</span><span class="sxs-lookup"><span data-stu-id="7390b-444">Drag 'n drop files to upload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7390b-445">已知問題</span><span class="sxs-lookup"><span data-stu-id="7390b-445">Known Issues</span></span>

* <span data-ttu-id="7390b-446">設定 Blob 容器公用存取層級時，在您重新將焦點設定在容器上之前，新的值將不會更新</span><span class="sxs-lookup"><span data-stu-id="7390b-446">When setting blob container public access level, the new value is not updated until you re-set the focus on the container</span></span>
* <span data-ttu-id="7390b-447">當您開啟對話方塊以設定公用存取層級時，該對話方塊預設一律會顯示「無公用存取」，而非目前實際的值</span><span class="sxs-lookup"><span data-stu-id="7390b-447">When you open the dialog to set the public access level, it always shows "No public access" as the default, and not the actual current value</span></span>
* <span data-ttu-id="7390b-448">無法對已下載的 Blob 進行重新命名</span><span class="sxs-lookup"><span data-stu-id="7390b-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="7390b-449">發生錯誤時，活動記錄項目有時候會卡在進行中的狀態，且該錯誤不會顯示</span><span class="sxs-lookup"><span data-stu-id="7390b-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and the error is not displayed</span></span>
* <span data-ttu-id="7390b-450">嘗試上傳或下載大量的 Blob 時，有時候會當機或是出現白色畫面</span><span class="sxs-lookup"><span data-stu-id="7390b-450">Sometimes crashes or turns completely white when trying to upload or download a large number of blobs</span></span>
* <span data-ttu-id="7390b-451">取消複製作業有時候會無法運作</span><span class="sxs-lookup"><span data-stu-id="7390b-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="7390b-452">在建立容器 (Blob/佇列/資料表) 的期間，如果您輸入無效的名稱，並繼續以不同的容器類型建立另一個容器，將無法把焦點設定在新的類型上</span><span class="sxs-lookup"><span data-stu-id="7390b-452">During creating a container (blob/queue/table), if you input an invalid name and proceed to create another under a different container type you cannot set focus on the new type</span></span>
* <span data-ttu-id="7390b-453">無法建立新資料夾或對資料夾進行重新命名</span><span class="sxs-lookup"><span data-stu-id="7390b-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md