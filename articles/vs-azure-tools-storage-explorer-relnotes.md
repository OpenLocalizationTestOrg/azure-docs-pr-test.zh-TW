---
title: "aaaMicrosoft Azure 儲存體總管 （預覽） 版本資訊 |Microsoft 文件"
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
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="7deb4-103">Microsoft Azure 儲存體總管 (預覽) 版本資訊</span><span class="sxs-lookup"><span data-stu-id="7deb4-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="7deb4-104">本文章包含 hello 版本的 Azure 儲存體總管 0.8.16 的資訊 （預覽） 發行的版本，以及針對先前版本的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="7deb4-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="7deb4-105">[Microsoft Azure 儲存體總管 （預覽）](./vs-azure-tools-storage-manage-with-storage-explorer.md)是獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="7deb4-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="7deb4-106">0.8.16 版 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="7deb4-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="7deb4-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="7deb4-108">下載 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="7deb4-109">適用於 Windows 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="7deb4-110">適用於 Mac 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="7deb4-111">適用於 Linux 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="7deb4-112">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-112">New</span></span>
* <span data-ttu-id="7deb4-113">當您開啟 blob 時，儲存體總管會提示您 tooupload hello 下載檔案在偵測到變更</span><span class="sxs-lookup"><span data-stu-id="7deb4-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="7deb4-114">增強的 Azure Stack 登入體驗</span><span class="sxs-lookup"><span data-stu-id="7deb4-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="7deb4-115">改良的 hello 效能上傳/下載許多小檔案在 hello 相同時間</span><span class="sxs-lookup"><span data-stu-id="7deb4-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="7deb4-116">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-116">Fixes</span></span>
* <span data-ttu-id="7deb4-117">對於某些 blob 類型中，選擇太 「 取代 」 期間上傳衝突會有時產生 hello 上傳正在重新啟動。</span><span class="sxs-lookup"><span data-stu-id="7deb4-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="7deb4-118">在 0.8.15 版中，上傳有時會延滯在 99%。</span><span class="sxs-lookup"><span data-stu-id="7deb4-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="7deb4-119">上傳時檔案 tooa 檔案共用，如果您選擇 tooupload tooa 目錄不存在，您上傳會失敗。</span><span class="sxs-lookup"><span data-stu-id="7deb4-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="7deb4-120">儲存體總管未正確產生共用存取簽章和資料表查詢的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="7deb4-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="7deb4-121">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-121">Known Issues</span></span>
* <span data-ttu-id="7deb4-122">目前無法使用名稱和金鑰連接字串。</span><span class="sxs-lookup"><span data-stu-id="7deb4-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="7deb4-123">它將會修正 hello 下一個版本。</span><span class="sxs-lookup"><span data-stu-id="7deb4-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="7deb4-124">在此之前，您可以使用名稱和金鑰附加。</span><span class="sxs-lookup"><span data-stu-id="7deb4-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="7deb4-125">如果您嘗試 tooopen 具有無效的 Windows 檔案名稱的檔案，hello 下載將會導致找不到錯誤的檔案。</span><span class="sxs-lookup"><span data-stu-id="7deb4-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="7deb4-126">之後的工作上，按一下 [取消]，花費時間，該工作 toocancel。</span><span class="sxs-lookup"><span data-stu-id="7deb4-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="7deb4-127">這是 hello Azure 儲存體節點文件庫的限制。</span><span class="sxs-lookup"><span data-stu-id="7deb4-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="7deb4-128">完成 blob 上傳之後, 會重新整理起始 hello 上載 hello 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7deb4-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="7deb4-129">這是從先前的行為變更，而且也會導致您 toobe 回復您是在 hello 容器 toohello 根目錄。</span><span class="sxs-lookup"><span data-stu-id="7deb4-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="7deb4-130">如果您選擇 hello 錯誤的 PIN/智慧卡憑證，則您必須在順序 toohave toorestart 存放裝置總管忘了該決策。</span><span class="sxs-lookup"><span data-stu-id="7deb4-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="7deb4-131">您需要 tooreenter 認證 toofilter 訂用帳戶可能會顯示 hello 帳戶設定 面板。</span><span class="sxs-lookup"><span data-stu-id="7deb4-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="7deb4-132">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7deb4-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7deb4-133">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7deb4-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7deb4-134">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7deb4-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="7deb4-135">Ubuntu 14.04 上的使用者，您將需要的 tooensure GCC 已啟動 toodate-這可以透過執行 hello 來完成下列命令，然後再重新啟動您的電腦：</span><span class="sxs-lookup"><span data-stu-id="7deb4-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="7deb4-136">Ubuntu 17.04 上的使用者，您將需要 tooinstall GConf-這可藉執行下列命令，然後再重新啟動您的電腦的 hello:</span><span class="sxs-lookup"><span data-stu-id="7deb4-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="7deb4-137">0.8.14 版 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="7deb4-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="7deb4-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="7deb4-139">下載 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="7deb4-140">下載適用於 Windows 的 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="7deb4-141">下載適用於 Mac 的 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="7deb4-142">下載適用於 Linux 的 Azure 儲存體總管 0.8.14 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7deb4-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="7deb4-143">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-143">New</span></span>

* <span data-ttu-id="7deb4-144">更新的電子束版本 too1.7.2 中順序 tootake 利用數個重要的安全性更新</span><span class="sxs-lookup"><span data-stu-id="7deb4-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="7deb4-145">您現在可以快速存取 hello 線上疑難排解指南從 hello [說明] 功能表</span><span class="sxs-lookup"><span data-stu-id="7deb4-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="7deb4-146">儲存體總管疑難排解[指南][2]</span><span class="sxs-lookup"><span data-stu-id="7deb4-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="7deb4-147">[指示][ 3]連接 tooan 堆疊 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="7deb4-148">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-148">Known Issues</span></span>

* <span data-ttu-id="7deb4-149">Hello 刪除資料夾確認對話方塊上的按鈕沒有註冊 hello Linux 上按兩下滑鼠。</span><span class="sxs-lookup"><span data-stu-id="7deb4-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="7deb4-150">因應措施是 toouse hello Enter 鍵</span><span class="sxs-lookup"><span data-stu-id="7deb4-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="7deb4-151">如果您選擇 hello 錯誤的 PIN/智慧卡憑證，則您必須在順序 toohave 存放裝置總管 toorestart 忘記 hello 決策</span><span class="sxs-lookup"><span data-stu-id="7deb4-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="7deb4-152">3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="7deb4-153">hello 帳戶設定 面板中可能會顯示您需要 tooreenter 順序 toofilter 訂用帳戶中的認證</span><span class="sxs-lookup"><span data-stu-id="7deb4-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="7deb4-154">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7deb4-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7deb4-155">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7deb4-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7deb4-156">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7deb4-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="7deb4-157">Ubuntu 14.04 gcc 版本更新，或升級 – 步驟 tooupgrade 安裝需求如下：</span><span class="sxs-lookup"><span data-stu-id="7deb4-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="7deb4-158">舊版</span><span class="sxs-lookup"><span data-stu-id="7deb4-158">Previous releases</span></span>

* [<span data-ttu-id="7deb4-159">0.8.13 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="7deb4-160">0.8.12 / 0.8.11 / 0.8.10 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="7deb4-161">0.8.9 / 0.8.8 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="7deb4-162">0.8.7 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="7deb4-163">0.8.6 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="7deb4-164">0.8.5 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="7deb4-165">0.8.4 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="7deb4-166">0.8.3 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="7deb4-167">0.8.2 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="7deb4-168">0.8.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="7deb4-169">0.7.20160509.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="7deb4-170">0.7.20160325.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="7deb4-171">0.7.20160129.1 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="7deb4-172">0.7.20160105.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="7deb4-173">0.7.20151116.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="7deb4-174">0.8.13 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-174">Version 0.8.13</span></span>
<span data-ttu-id="7deb4-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="7deb4-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="7deb4-176">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-176">New</span></span>

* <span data-ttu-id="7deb4-177">儲存體總管疑難排解[指南][2]</span><span class="sxs-lookup"><span data-stu-id="7deb4-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="7deb4-178">[指示][ 3]連接 tooan 堆疊 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-179">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-179">Fixes</span></span>

* <span data-ttu-id="7deb4-180">已修正︰檔案上傳先前很容易造成記憶體不足錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="7deb4-181">已修正：您現在可以使用 PIN/智慧卡登入</span><span class="sxs-lookup"><span data-stu-id="7deb4-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="7deb4-182">已修正：[在入口網站中開啟] 現已可以搭配 Azure 中國、Azure 德國、Azure 美國政府及 Azure Stack 運作</span><span class="sxs-lookup"><span data-stu-id="7deb4-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="7deb4-183">修正問題︰ 同時上傳資料夾 tooa blob 容器，「 不合法作業 」 會有時會發生錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="7deb4-184">已修正：先前在管理快照集時會停用 [全選]</span><span class="sxs-lookup"><span data-stu-id="7deb4-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="7deb4-185">已修正︰ hello hello 基底 blob 的中繼資料可能會覆寫檢視其快照集的 hello 屬性之後</span><span class="sxs-lookup"><span data-stu-id="7deb4-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-186">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-186">Known Issues</span></span>

* <span data-ttu-id="7deb4-187">如果您選擇 hello 錯誤的 PIN/智慧卡憑證，則您必須在順序 toohave 存放裝置總管 toorestart 忘記 hello 決策</span><span class="sxs-lookup"><span data-stu-id="7deb4-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="7deb4-188">放大或縮小，雖然 hello 縮放層級可能會短暫地重設 toohello 預設層級</span><span class="sxs-lookup"><span data-stu-id="7deb4-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="7deb4-189">3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="7deb4-190">hello 帳戶設定 面板中可能會顯示您需要 tooreenter 順序 toofilter 訂用帳戶中的認證</span><span class="sxs-lookup"><span data-stu-id="7deb4-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="7deb4-191">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7deb4-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7deb4-192">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7deb4-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7deb4-193">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7deb4-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="7deb4-194">Ubuntu 14.04 gcc 版本更新，或升級 – 步驟 tooupgrade 安裝需求如下：</span><span class="sxs-lookup"><span data-stu-id="7deb4-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="7deb4-195">0.8.12 / 0.8.11 / 0.8.10 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="7deb4-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="7deb4-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="7deb4-197">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-197">New</span></span>

* <span data-ttu-id="7deb4-198">儲存體總管即將自動關閉當您安裝更新時從 hello 更新通知</span><span class="sxs-lookup"><span data-stu-id="7deb4-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="7deb4-199">就地快速存取能針對您經常存取的資源提供加強的使用體驗</span><span class="sxs-lookup"><span data-stu-id="7deb4-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="7deb4-200">在 hello Blob 容器編輯器中，您現在可以看到租用的 blob 所屬的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7deb4-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="7deb4-201">您現在可以摺疊 hello 左側面板</span><span class="sxs-lookup"><span data-stu-id="7deb4-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="7deb4-202">探索現在就會在 hello 相同時間下載</span><span class="sxs-lookup"><span data-stu-id="7deb4-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="7deb4-203">在 hello Blob 容器、 檔案共用，以及資料表編輯器 toosee hello 大小的資源或選取中使用的統計資料</span><span class="sxs-lookup"><span data-stu-id="7deb4-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="7deb4-204">您可以現在登入 tooAzure Active Directory (AAD) 基礎堆疊 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7deb4-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="7deb4-205">您可以現在上載封存檔案超過 32 MB tooPremium 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="7deb4-206">改善協助工具支援</span><span class="sxs-lookup"><span data-stu-id="7deb4-206">Improved accessibility support</span></span>
* <span data-ttu-id="7deb4-207">您現在可以新增受信任的 base-64 編碼 X.509 SSL 憑證將 tooEdit-&gt; SSL 憑證-&gt;匯入憑證</span><span class="sxs-lookup"><span data-stu-id="7deb4-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-208">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-208">Fixes</span></span>

* <span data-ttu-id="7deb4-209">已修正︰ 在重新整理帳戶的認證之後, hello 樹狀檢視會有時不自動重新整理</span><span class="sxs-lookup"><span data-stu-id="7deb4-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="7deb4-210">已修正：先前針對模擬器佇列和資料表產生 SAS 會導致無效的 URL</span><span class="sxs-lookup"><span data-stu-id="7deb4-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="7deb4-211">已修正：進階儲存體帳戶現在可以在啟用 Proxy 時展開</span><span class="sxs-lookup"><span data-stu-id="7deb4-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="7deb4-212">已修正： hello 的套用按鈕 hello 帳戶如果您已選取 1 或 0 帳戶管理 頁面上將無法運作</span><span class="sxs-lookup"><span data-stu-id="7deb4-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="7deb4-213">已修正：上傳需要衝突解決的 Blob 可能會失敗 - 已在 0.8.11 中修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="7deb4-214">已修正：傳送意見反應的功能在 0.8.11 中無法運作 - 已在 0.8.12 中修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="7deb4-215">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-215">Known Issues</span></span>

* <span data-ttu-id="7deb4-216">升級之後 too0.8.10，您將需要 toorefresh 所有您的認證。</span><span class="sxs-lookup"><span data-stu-id="7deb4-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="7deb4-217">放大或縮小，雖然 hello 縮放層級可能會短暫地重設 toohello 預設層級。</span><span class="sxs-lookup"><span data-stu-id="7deb4-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="7deb4-218">3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="7deb4-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="7deb4-219">您需要 tooreenter 順序 toofilter 訂用帳戶中的認證可能會顯示 hello 帳戶設定 面板。</span><span class="sxs-lookup"><span data-stu-id="7deb4-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="7deb4-220">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7deb4-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7deb4-221">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。</span><span class="sxs-lookup"><span data-stu-id="7deb4-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="7deb4-222">雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。</span><span class="sxs-lookup"><span data-stu-id="7deb4-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="7deb4-223">Ubuntu 14.04 gcc 版本更新，或升級 – 步驟 tooupgrade 安裝需求如下：</span><span class="sxs-lookup"><span data-stu-id="7deb4-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="7deb4-224">0.8.9 / 0.8.8 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="7deb4-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="7deb4-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="7deb4-226">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-226">New</span></span>

* <span data-ttu-id="7deb4-227">儲存體總管 0.8.9 將會自動下載更新的 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="7deb4-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="7deb4-228">Hotfix： 使用入口網站產生 SAS URI tooattach 儲存體帳戶會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="7deb4-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="7deb4-229">現已能針對 Blob 快照集進行建立、管理及升階。</span><span class="sxs-lookup"><span data-stu-id="7deb4-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="7deb4-230">您現在可以登入 tooAzure 中國、 Azure 德國和 Azure 美國政府帳戶。</span><span class="sxs-lookup"><span data-stu-id="7deb4-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="7deb4-231">您現在可以變更 hello 縮放層級。</span><span class="sxs-lookup"><span data-stu-id="7deb4-231">You can now change hello zoom level.</span></span> <span data-ttu-id="7deb4-232">使用 In、 拉遠和重設縮放 hello 檢視功能表 tooZoom hello 選項。</span><span class="sxs-lookup"><span data-stu-id="7deb4-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="7deb4-233">Blob 和檔案的使用者中繼資料現已支援 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="7deb4-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="7deb4-234">協助工具改進。</span><span class="sxs-lookup"><span data-stu-id="7deb4-234">Accessibility improvements.</span></span>
* <span data-ttu-id="7deb4-235">從 hello 更新通知，就可以檢視 hello 下一版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="7deb4-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="7deb4-236">您也可以檢視 hello 目前的版本資訊從 hello [說明] 功能表。</span><span class="sxs-lookup"><span data-stu-id="7deb4-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-237">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-237">Fixes</span></span>

* <span data-ttu-id="7deb4-238">已修正︰ hello 版本號碼現在會正確顯示在 Windows [控制台] 中</span><span class="sxs-lookup"><span data-stu-id="7deb4-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="7deb4-239">已修正： 搜尋不再限制的 too50，000 節點</span><span class="sxs-lookup"><span data-stu-id="7deb4-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="7deb4-240">已修正︰ 上載 tooa 檔案共用開始永遠如果 hello 目的地目錄原本不存在</span><span class="sxs-lookup"><span data-stu-id="7deb4-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="7deb4-241">已修正：改善較長上傳及下載的穩定性</span><span class="sxs-lookup"><span data-stu-id="7deb4-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-242">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-242">Known Issues</span></span>

* <span data-ttu-id="7deb4-243">放大或縮小，雖然 hello 縮放層級可能會短暫地重設 toohello 預設層級。</span><span class="sxs-lookup"><span data-stu-id="7deb4-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="7deb4-244">快速存取僅適用於以訂用帳戶為基礎的項目。</span><span class="sxs-lookup"><span data-stu-id="7deb4-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="7deb4-245">此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源。</span><span class="sxs-lookup"><span data-stu-id="7deb4-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="7deb4-246">它可能需要快速存取幾秒 toonavigate toohello 目標資源，視您所擁有的資源數目而定。</span><span class="sxs-lookup"><span data-stu-id="7deb4-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="7deb4-247">3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="7deb4-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="7deb4-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="7deb4-249">0.8.7 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7deb4-250">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-250">New</span></span>

* <span data-ttu-id="7deb4-251">您可以選擇如何 tooresolve 衝突的更新，hello 開頭下載或複製在 hello 活動視窗的工作階段</span><span class="sxs-lookup"><span data-stu-id="7deb4-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="7deb4-252">將滑鼠停留在 hello 儲存體資源的索引標籤 toosee hello 完整路徑</span><span class="sxs-lookup"><span data-stu-id="7deb4-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="7deb4-253">當您按一下索引標籤上時，與同步處理其 hello 左側瀏覽窗格中的位置</span><span class="sxs-lookup"><span data-stu-id="7deb4-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-254">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-254">Fixes</span></span>

* <span data-ttu-id="7deb4-255">已修正：儲存體總管在 Mac 上現已是受信任的應用程式</span><span class="sxs-lookup"><span data-stu-id="7deb4-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="7deb4-256">已修正：再次支援 Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="7deb4-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="7deb4-257">已修正︰ 有時 hello 將帳戶加入載入訂用帳戶時，UI 會閃爍</span><span class="sxs-lookup"><span data-stu-id="7deb4-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="7deb4-258">已修正︰ 有時並非所有的儲存體資源中所列 hello 左側瀏覽窗格</span><span class="sxs-lookup"><span data-stu-id="7deb4-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="7deb4-259">已修正︰ hello 動作 窗格有時顯示空白的動作</span><span class="sxs-lookup"><span data-stu-id="7deb4-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="7deb4-260">已修正︰ hello 從 hello 上次關閉工作階段的視窗大小是現在保留</span><span class="sxs-lookup"><span data-stu-id="7deb4-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="7deb4-261">已修正： 您可以開啟多個索引標籤的 hello 相同的資源使用 hello 操作功能表</span><span class="sxs-lookup"><span data-stu-id="7deb4-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-262">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-262">Known Issues</span></span>

* <span data-ttu-id="7deb4-263">快速存取僅適用於以訂用帳戶為基礎的項目。</span><span class="sxs-lookup"><span data-stu-id="7deb4-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="7deb4-264">此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源</span><span class="sxs-lookup"><span data-stu-id="7deb4-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="7deb4-265">可能需要快速存取幾秒 toonavigate toohello 目標資源，視您所擁有的資源數目而定</span><span class="sxs-lookup"><span data-stu-id="7deb4-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="7deb4-266">3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="7deb4-267">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能或造成未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="7deb4-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="7deb4-268">Hello 第一次使用 hello 存放裝置總管上 macOS，您可能會看到多個提示要求使用者的權限 tooaccess keychain。</span><span class="sxs-lookup"><span data-stu-id="7deb4-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="7deb4-269">我們建議您選取永遠允許讓 hello 提示不會顯示一次</span><span class="sxs-lookup"><span data-stu-id="7deb4-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="7deb4-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="7deb4-271">0.8.6 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="7deb4-272">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-272">New</span></span>

* <span data-ttu-id="7deb4-273">您可以現在 pin 碼最常使用服務 toohello 快速存取您輕鬆瀏覽</span><span class="sxs-lookup"><span data-stu-id="7deb4-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="7deb4-274">現已可在多個索引標籤開啟多個編輯器。</span><span class="sxs-lookup"><span data-stu-id="7deb4-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="7deb4-275">單鍵 tooopen 暫存的索引標籤。按兩下 tooopen 永久索引標籤。您也可以按一下 hello 暫存索引標籤 toomake 它永久索引標籤</span><span class="sxs-lookup"><span data-stu-id="7deb4-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="7deb4-276">我們已大幅改善上傳及下載的效能和穩定性，尤其是在高效能機器上處理大型檔案的情況</span><span class="sxs-lookup"><span data-stu-id="7deb4-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="7deb4-277">現可在 Blob 容器內建立空白的「虛擬」資料夾</span><span class="sxs-lookup"><span data-stu-id="7deb4-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="7deb4-278">我們已重新推出範圍搜尋，並搭配全新增強的子字串搜尋，因此您現在將會有兩種搜尋的選項：</span><span class="sxs-lookup"><span data-stu-id="7deb4-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="7deb4-279">全域搜尋-只要 hello [搜尋] 文字方塊中輸入搜尋詞彙</span><span class="sxs-lookup"><span data-stu-id="7deb4-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="7deb4-280">限定範圍的搜尋-按一下 hello 放大鏡圖示下一步 tooa 節點，然後加入搜尋詞彙 toohello hello 路徑結尾，或以滑鼠右鍵按一下並選取"Here 搜尋從"</span><span class="sxs-lookup"><span data-stu-id="7deb4-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="7deb4-281">已新增多種佈景主題：淺色 (預設)、深色、黑色高對比和白色高對比。</span><span class="sxs-lookup"><span data-stu-id="7deb4-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="7deb4-282">移 tooEdit-&gt;佈景主題 toochange 主題設定喜好設定</span><span class="sxs-lookup"><span data-stu-id="7deb4-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="7deb4-283">您可以修改 Blob 和檔案的屬性</span><span class="sxs-lookup"><span data-stu-id="7deb4-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="7deb4-284">我們現已支援編碼 (base64) 及未編碼的佇列訊息</span><span class="sxs-lookup"><span data-stu-id="7deb4-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="7deb4-285">若使用 Linux，必須為 64 位元作業系統。</span><span class="sxs-lookup"><span data-stu-id="7deb4-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="7deb4-286">針對此版本，我們僅支援 64 位元的 Ubuntu 16.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="7deb4-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="7deb4-287">已更新我們的標誌！</span><span class="sxs-lookup"><span data-stu-id="7deb4-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-288">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-288">Fixes</span></span>

* <span data-ttu-id="7deb4-289">已修正︰畫面凍結的問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="7deb4-290">已修正：增強安全性</span><span class="sxs-lookup"><span data-stu-id="7deb4-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="7deb4-291">已修正：有時候可能會出現重複的附加帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="7deb4-292">已修正：具有未定義內容類型的 Blob 可能會產生例外狀況</span><span class="sxs-lookup"><span data-stu-id="7deb4-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="7deb4-293">已修正︰ 開啟 hello 查詢面板上的空白資料表是不可行</span><span class="sxs-lookup"><span data-stu-id="7deb4-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="7deb4-294">已修正：數個搜尋功能中的錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="7deb4-295">已修正︰ 增加 hello 按下 「 多負載 」 時，從 50 too100 載入的資源數目</span><span class="sxs-lookup"><span data-stu-id="7deb4-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="7deb4-296">已修正：首次執行時，如果已登入某個帳戶，現在預設會選取該帳戶的所有定用帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="7deb4-297">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-297">Known Issues</span></span>

* <span data-ttu-id="7deb4-298">Ubuntu 14.04 上無法執行這一版的 hello 存放裝置總管</span><span class="sxs-lookup"><span data-stu-id="7deb4-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="7deb4-299">tooopen 多個索引標籤上，按一下相同的資源，不會持續執行的 hello 相同的資源。</span><span class="sxs-lookup"><span data-stu-id="7deb4-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="7deb4-300">另一個資源上按一下並再返回，然後按一下 hello 原始資源 tooopen 上它一次在另一個索引標籤</span><span class="sxs-lookup"><span data-stu-id="7deb4-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="7deb4-301">快速存取僅適用於以訂用帳戶為基礎的項目。</span><span class="sxs-lookup"><span data-stu-id="7deb4-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="7deb4-302">此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源</span><span class="sxs-lookup"><span data-stu-id="7deb4-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="7deb4-303">可能需要快速存取幾秒 toonavigate toohello 目標資源，視您所擁有的資源數目而定</span><span class="sxs-lookup"><span data-stu-id="7deb4-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="7deb4-304">3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="7deb4-305">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能或造成未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="7deb4-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="7deb4-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="7deb4-307">0.8.5 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="7deb4-308">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-308">New</span></span>

* <span data-ttu-id="7deb4-309">現在使用入口網站產生 SAS 金鑰 tooattach tooStorage 可以帳戶和資源</span><span class="sxs-lookup"><span data-stu-id="7deb4-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-310">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-310">Fixes</span></span>

* <span data-ttu-id="7deb4-311">修正問題︰ 有時搜尋期間的競爭情形會造成非可展開的節點 toobecome</span><span class="sxs-lookup"><span data-stu-id="7deb4-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="7deb4-312">已修正︰ 「 使用 HTTP 」 不適用於 tooStorage 帳戶連線與帳戶名稱和金鑰</span><span class="sxs-lookup"><span data-stu-id="7deb4-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="7deb4-313">已修正：SAS 金鑰 (特別是由入口網站所產生的 SAS 金鑰) 會傳回「結尾斜線」錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="7deb4-314">已修正：資料表匯入問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="7deb4-315">資料分割索引鍵和列索引鍵有時候會反轉</span><span class="sxs-lookup"><span data-stu-id="7deb4-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="7deb4-316">「 Null 」 資料分割索引鍵無法 tooread</span><span class="sxs-lookup"><span data-stu-id="7deb4-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-317">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-317">Known Issues</span></span>

* <span data-ttu-id="7deb4-318">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能</span><span class="sxs-lookup"><span data-stu-id="7deb4-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="7deb4-319">Azure 堆疊目前不支援檔案，因此嘗試 tooexpand 檔案將會顯示錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="7deb4-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="7deb4-321">0.8.4 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7deb4-322">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-322">New</span></span>

* <span data-ttu-id="7deb4-323">產生的直接連結 toostorage 帳戶、 容器、 佇列、 資料表或檔案共用的共用，且容易存取 tooyour 資源-Windows 和 Mac OS 支援</span><span class="sxs-lookup"><span data-stu-id="7deb4-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="7deb4-324">搜尋 blob 容器、 資料表、 佇列、 檔案共用或從 hello [搜尋] 方塊的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="7deb4-325">您現在可以將群組 hello 資料表查詢產生器中的子句</span><span class="sxs-lookup"><span data-stu-id="7deb4-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="7deb4-326">從 SAS 附加帳戶及容器內對 Blob 容器、檔案共用、資料表、Blob、Blob 資料夾、檔案及目錄進行重新命名和複製/貼上</span><span class="sxs-lookup"><span data-stu-id="7deb4-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="7deb4-327">對 Blob 容器和檔案共用進行重新命名和複製時，現在會保留屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="7deb4-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-328">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-328">Fixes</span></span>

* <span data-ttu-id="7deb4-329">已修正：無法編輯包含布林值或二進位屬性的資料表實體</span><span class="sxs-lookup"><span data-stu-id="7deb4-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-330">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-330">Known Issues</span></span>

* <span data-ttu-id="7deb4-331">搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能</span><span class="sxs-lookup"><span data-stu-id="7deb4-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="7deb4-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="7deb4-333">0.8.3 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7deb4-334">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-334">New</span></span>

* <span data-ttu-id="7deb4-335">對容器、資料表、檔案共用進行重新命名</span><span class="sxs-lookup"><span data-stu-id="7deb4-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="7deb4-336">改善查詢建立器體驗</span><span class="sxs-lookup"><span data-stu-id="7deb4-336">Improved Query builder experience</span></span>
* <span data-ttu-id="7deb4-337">能力 toosave 和載入查詢</span><span class="sxs-lookup"><span data-stu-id="7deb4-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="7deb4-338">直接連結 toostorage 帳戶或容器、 佇列資料表，或檔案共用，並輕鬆地存取您的資源共用 （僅限 Windows-macOS 支援即將推出 ！）</span><span class="sxs-lookup"><span data-stu-id="7deb4-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="7deb4-339">能力 toomanage 設定 CORS 規則</span><span class="sxs-lookup"><span data-stu-id="7deb4-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-340">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-340">Fixes</span></span>

* <span data-ttu-id="7deb4-341">已修正：Microsoft 帳戶每 8 至 12 小時便需要重新驗證</span><span class="sxs-lookup"><span data-stu-id="7deb4-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-342">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-342">Known Issues</span></span>

* <span data-ttu-id="7deb4-343">有時 hello UI 可能看似凍結-最大化 hello 視窗可協助解決此問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="7deb4-344">macOS 安裝可能會需要較高的權限</span><span class="sxs-lookup"><span data-stu-id="7deb4-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="7deb4-345">可能會顯示帳戶設定 面板中，您需要 tooreenter 順序 toofilter 訂用帳戶中的認證</span><span class="sxs-lookup"><span data-stu-id="7deb4-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="7deb4-346">重新命名的檔案共用、 blob 容器和資料表不會保留中繼資料或 hello 容器，例如檔案共用配額、 公用存取層級或存取原則上的其他屬性</span><span class="sxs-lookup"><span data-stu-id="7deb4-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="7deb4-347">重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。</span><span class="sxs-lookup"><span data-stu-id="7deb4-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="7deb4-348">Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留</span><span class="sxs-lookup"><span data-stu-id="7deb4-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="7deb4-349">在 SAS 附加帳戶內並無法對資源進行複製或重新命名</span><span class="sxs-lookup"><span data-stu-id="7deb4-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="7deb4-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="7deb4-351">0.8.2 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7deb4-352">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-352">New</span></span>

* <span data-ttu-id="7deb4-353">儲存體帳戶是依訂用帳戶進行群組。透過金鑰或 SAS 附加的開發儲存體和資源會顯示在 (本機和附加的) 節點之下</span><span class="sxs-lookup"><span data-stu-id="7deb4-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="7deb4-354">在 [Azure 帳戶設定] 面板中登出帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="7deb4-355">設定 proxy 設定 tooenable 及管理登入</span><span class="sxs-lookup"><span data-stu-id="7deb4-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="7deb4-356">建立和中斷 Blob 租用</span><span class="sxs-lookup"><span data-stu-id="7deb4-356">Create and break blob leases</span></span>
* <span data-ttu-id="7deb4-357">按一下便能開啟 Blob 容器、佇列、資料表及檔案</span><span class="sxs-lookup"><span data-stu-id="7deb4-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-358">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-358">Fixes</span></span>

* <span data-ttu-id="7deb4-359">已修正：使用 .NET 或 Java 程式庫插入的佇列訊息沒有從 base64 正確解碼</span><span class="sxs-lookup"><span data-stu-id="7deb4-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="7deb4-360">已修正：$metrics 資料表不會針對 Blob 儲存體帳戶顯示</span><span class="sxs-lookup"><span data-stu-id="7deb4-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="7deb4-361">已修正：資料表節點無法用於本機 (開發) 儲存體</span><span class="sxs-lookup"><span data-stu-id="7deb4-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-362">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-362">Known Issues</span></span>

* <span data-ttu-id="7deb4-363">macOS 安裝可能會需要較高的權限</span><span class="sxs-lookup"><span data-stu-id="7deb4-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="7deb4-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="7deb4-365">0.8.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="7deb4-366">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-366">New</span></span>

* <span data-ttu-id="7deb4-367">檔案共用支援：檢視、上傳、下載、複製檔案和目錄、SAS URI (建立和連線)</span><span class="sxs-lookup"><span data-stu-id="7deb4-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="7deb4-368">改善使用者體驗 SAS Uri 或帳戶金鑰以連線 tooStorage</span><span class="sxs-lookup"><span data-stu-id="7deb4-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="7deb4-369">匯出資料表查詢結果</span><span class="sxs-lookup"><span data-stu-id="7deb4-369">Export table query results</span></span>
* <span data-ttu-id="7deb4-370">針對資料表資料行的重新排列和自訂</span><span class="sxs-lookup"><span data-stu-id="7deb4-370">Table column reordering and customization</span></span>
* <span data-ttu-id="7deb4-371">搭配啟用的計量檢視儲存體帳戶的 $logs Blob 容器和 $metrics 資料表</span><span class="sxs-lookup"><span data-stu-id="7deb4-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="7deb4-372">改善匯出和匯入行為，現已包含屬性值類型</span><span class="sxs-lookup"><span data-stu-id="7deb4-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-373">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-373">Fixes</span></span>

* <span data-ttu-id="7deb4-374">已修正：上傳或下載大型 Blob 可能會導致不完整的上傳/下載</span><span class="sxs-lookup"><span data-stu-id="7deb4-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="7deb4-375">已修正︰ 編輯、 加入或匯入實體具有數值的字串值 ("1") 會將它轉換 toodouble</span><span class="sxs-lookup"><span data-stu-id="7deb4-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="7deb4-376">Hello 本機開發環境中已修正︰ 無法 tooexpand hello 資料表節點</span><span class="sxs-lookup"><span data-stu-id="7deb4-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-377">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-377">Known Issues</span></span>

* <span data-ttu-id="7deb4-378">$metrics 資料表不會針對 Blob 儲存體帳戶顯示</span><span class="sxs-lookup"><span data-stu-id="7deb4-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="7deb4-379">以程式設計方式加入的佇列訊息可能無法正確顯示如果 hello 訊息使用 Base64 編碼方式編碼</span><span class="sxs-lookup"><span data-stu-id="7deb4-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="7deb4-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="7deb4-381">0.7.20160509.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="7deb4-382">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-382">New</span></span>

* <span data-ttu-id="7deb4-383">改善應用程式當機的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="7deb4-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-384">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-384">Fixes</span></span>

* <span data-ttu-id="7deb4-385">已修正在需要登入認證時，InfoBar 訊息有時候不會顯示的錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-386">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-386">Known Issues</span></span>

* <span data-ttu-id="7deb4-387">資料表： 加入、 編輯或匯入實體具有模稜兩可的數字的值，例如"1"或"1.0"，具有的屬性和 hello 使用者嘗試 toosend 為`Edm.String`，傳回透過 hello 用戶端 API 為 Edm.Double 是 hello 值</span><span class="sxs-lookup"><span data-stu-id="7deb4-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="7deb4-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="7deb4-389">0.7.20160325.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="7deb4-390">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-390">New</span></span>

* <span data-ttu-id="7deb4-391">資料表支援：針對實體的檢視、查詢、匯出、匯入及 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="7deb4-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="7deb4-392">佇列支援：針對訊息進行檢視、新增、清除佇列</span><span class="sxs-lookup"><span data-stu-id="7deb4-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="7deb4-393">針對儲存體帳戶產生 SAS URI</span><span class="sxs-lookup"><span data-stu-id="7deb4-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="7deb4-394">TooStorage 帳戶連線使用 SAS Uri</span><span class="sxs-lookup"><span data-stu-id="7deb4-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="7deb4-395">更新通知。 未來的更新 tooStorage 總管</span><span class="sxs-lookup"><span data-stu-id="7deb4-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="7deb4-396">更新外觀與風格</span><span class="sxs-lookup"><span data-stu-id="7deb4-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-397">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-397">Fixes</span></span>

* <span data-ttu-id="7deb4-398">改善效能和可靠性</span><span class="sxs-lookup"><span data-stu-id="7deb4-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="7deb4-399">已知問題 &amp; 緩解方式</span><span class="sxs-lookup"><span data-stu-id="7deb4-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="7deb4-400">下載大型 Blob 檔案並無法正確運作。在我們解決此問題的期間，建議您使用 AzCopy</span><span class="sxs-lookup"><span data-stu-id="7deb4-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="7deb4-401">無法再進行擷取或如果 hello 主資料夾找不到或無法寫入快取帳戶認證</span><span class="sxs-lookup"><span data-stu-id="7deb4-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="7deb4-402">如果我們要加入、 編輯，或匯入實體具有模稜兩可的數字的值，例如"1"或"1.0"，具有的屬性，且 hello 使用者嘗試 toosend 為`Edm.String`，傳回透過 hello 用戶端 API 為 Edm.Double 是 hello 值</span><span class="sxs-lookup"><span data-stu-id="7deb4-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="7deb4-403">當匯入 CSV 檔案，具有多行的記錄，hello 資料可能會取得切碎或變碼的</span><span class="sxs-lookup"><span data-stu-id="7deb4-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="7deb4-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="7deb4-405">0.7.20160129.1 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-406">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-406">Fixes</span></span>

* <span data-ttu-id="7deb4-407">改善上傳、下載及複製 Blob 的整體效能</span><span class="sxs-lookup"><span data-stu-id="7deb4-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="7deb4-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="7deb4-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="7deb4-409">0.7.20160105.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="7deb4-410">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-410">New</span></span>

* <span data-ttu-id="7deb4-411">Linux 支援 (同位功能 tooOSX)</span><span class="sxs-lookup"><span data-stu-id="7deb4-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="7deb4-412">新增具有共用存取簽章 (SAS) 金鑰的 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="7deb4-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="7deb4-413">新增 Azure 中國的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="7deb4-414">新增具有自訂端點的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7deb4-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="7deb4-415">開啟並檢視 hello 內容的文字和圖片 blob</span><span class="sxs-lookup"><span data-stu-id="7deb4-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="7deb4-416">檢視及編輯 Blob 屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="7deb4-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="7deb4-417">修正</span><span class="sxs-lookup"><span data-stu-id="7deb4-417">Fixes</span></span>

* <span data-ttu-id="7deb4-418">已修正： 上傳或下載大量的 blob （500 +） 有時可能會發生 hello 應用程式 toohave 白色螢幕</span><span class="sxs-lookup"><span data-stu-id="7deb4-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="7deb4-419">已修正︰ 當 blob 容器的公用存取層級設定，hello 新值會更新直到您重新設定 hello 焦點 hello 容器上。</span><span class="sxs-lookup"><span data-stu-id="7deb4-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="7deb4-420">此外，hello 對話方塊太一律使用預設 「 公用存取 」，而非 hello 實際目前的值。</span><span class="sxs-lookup"><span data-stu-id="7deb4-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="7deb4-421">更佳的整體鍵盤/協助工具及 UI 支援</span><span class="sxs-lookup"><span data-stu-id="7deb4-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="7deb4-422">階層連結記錄在因大量空白字元而變得過長時便會自動換行</span><span class="sxs-lookup"><span data-stu-id="7deb4-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="7deb4-423">SAS 對話方塊支援輸入驗證</span><span class="sxs-lookup"><span data-stu-id="7deb4-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="7deb4-424">本機儲存體繼續 toobe 可用，即使使用者的認證已過期</span><span class="sxs-lookup"><span data-stu-id="7deb4-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="7deb4-425">刪除開啟的 blob 容器時，關閉 hello 右側 hello blob 總管</span><span class="sxs-lookup"><span data-stu-id="7deb4-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-426">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-426">Known Issues</span></span>

* <span data-ttu-id="7deb4-427">Gcc 版本更新，或升級 – 步驟 tooupgrade Linux 安裝需求如下：</span><span class="sxs-lookup"><span data-stu-id="7deb4-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="7deb4-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="7deb4-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="7deb4-429">0.7.20151116.0 版</span><span class="sxs-lookup"><span data-stu-id="7deb4-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="7deb4-430">新增</span><span class="sxs-lookup"><span data-stu-id="7deb4-430">New</span></span>

* <span data-ttu-id="7deb4-431">macOS 及 Windows 版本</span><span class="sxs-lookup"><span data-stu-id="7deb4-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="7deb4-432">登入 tooview 儲存體帳戶 – 使用您組織帳戶，Microsoft 帳戶、 2FA、 等等。</span><span class="sxs-lookup"><span data-stu-id="7deb4-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="7deb4-433">本機開發儲存體 (使用儲存體模擬器，僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="7deb4-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="7deb4-434">Azure Resource Manager 和傳統資源支援</span><span class="sxs-lookup"><span data-stu-id="7deb4-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="7deb4-435">建立及刪除 Blob、佇列或資料表</span><span class="sxs-lookup"><span data-stu-id="7deb4-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="7deb4-436">搜尋特定的 Blob、佇列或資料表</span><span class="sxs-lookup"><span data-stu-id="7deb4-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="7deb4-437">瀏覽 hello 的 blob 容器的內容</span><span class="sxs-lookup"><span data-stu-id="7deb4-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="7deb4-438">檢視並瀏覽目錄</span><span class="sxs-lookup"><span data-stu-id="7deb4-438">View and navigate through directories</span></span>
* <span data-ttu-id="7deb4-439">上傳、下載及刪除 Blob 和資料夾</span><span class="sxs-lookup"><span data-stu-id="7deb4-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="7deb4-440">檢視及編輯 Blob 屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="7deb4-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="7deb4-441">產生 SAS 金鑰</span><span class="sxs-lookup"><span data-stu-id="7deb4-441">Generate SAS keys</span></span>
* <span data-ttu-id="7deb4-442">管理及建立儲存的存取原則 (SAP)</span><span class="sxs-lookup"><span data-stu-id="7deb4-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="7deb4-443">使用前置詞搜尋 Blob</span><span class="sxs-lookup"><span data-stu-id="7deb4-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="7deb4-444">拖曳 ' n 卸除檔案 tooupload 或下載</span><span class="sxs-lookup"><span data-stu-id="7deb4-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="7deb4-445">已知問題</span><span class="sxs-lookup"><span data-stu-id="7deb4-445">Known Issues</span></span>

* <span data-ttu-id="7deb4-446">Blob 容器的公用存取層級設定，當 hello 新值會更新直到您重新設定 hello 容器上的 hello 焦點</span><span class="sxs-lookup"><span data-stu-id="7deb4-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="7deb4-447">則當您開啟 hello 對話方塊 tooset hello 公用存取層級時，永遠會顯示 「 沒有公用存取 」 hello 預設值，而非 hello 實際目前的值為</span><span class="sxs-lookup"><span data-stu-id="7deb4-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="7deb4-448">無法對已下載的 Blob 進行重新命名</span><span class="sxs-lookup"><span data-stu-id="7deb4-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="7deb4-449">活動記錄檔項目將有時"堵塞 」 在進行中狀態，當發生錯誤，並不會顯示 hello 錯誤</span><span class="sxs-lookup"><span data-stu-id="7deb4-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="7deb4-450">有時候當機或開啟完全白色時嘗試 tooupload 或下載大量的 blob</span><span class="sxs-lookup"><span data-stu-id="7deb4-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="7deb4-451">取消複製作業有時候會無法運作</span><span class="sxs-lookup"><span data-stu-id="7deb4-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="7deb4-452">期間建立的容器 （blob/佇列/資料表），如果輸入無效的名稱，並繼續 toocreate 在不同的容器類型的另一個您無法設定焦點的 hello 新類型</span><span class="sxs-lookup"><span data-stu-id="7deb4-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="7deb4-453">無法建立新資料夾或對資料夾進行重新命名</span><span class="sxs-lookup"><span data-stu-id="7deb4-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md