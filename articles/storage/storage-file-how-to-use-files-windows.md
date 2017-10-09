---
title: "aaaMount Azure 檔案共用及存取 hello 共用 windows |Microsoft 文件"
description: "裝載 Azure 檔案共用及存取在 Windows 中的 hello 共用。"
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="0769c-103">裝載 Azure 檔案共用及存取在 Windows 中的 hello 共用</span><span class="sxs-lookup"><span data-stu-id="0769c-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="0769c-104">[Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)是 Microsoft 的簡單 toouse 雲端的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="0769c-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="0769c-105">Azure 檔案共用可在 Windows 和 Windows Server 中掛接。</span><span class="sxs-lookup"><span data-stu-id="0769c-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="0769c-106">本文將說明三種不同的方式 toomount Azure 檔案共用在 Windows 上： 以 hello 檔案總管 UI，透過 PowerShell，並透過 hello 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="0769c-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="0769c-107">Azure 檔案共用之外 hello Azure 區域中，例如內部或在不同的 Azure 區域中裝載的順序 toomount，hello 作業系統必須支援 SMB 3.0。</span><span class="sxs-lookup"><span data-stu-id="0769c-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="0769c-108">Azure 檔案共用可以掛接在 Windows 電腦上 (視 OS 版本而定，不是內部部署環境就是 Azure VM)。</span><span class="sxs-lookup"><span data-stu-id="0769c-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="0769c-109">下表說明 hello</span><span class="sxs-lookup"><span data-stu-id="0769c-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="0769c-110">Windows 版本</span><span class="sxs-lookup"><span data-stu-id="0769c-110">Windows Version</span></span>        | <span data-ttu-id="0769c-111">SMB 版本</span><span class="sxs-lookup"><span data-stu-id="0769c-111">SMB Version</span></span> |<span data-ttu-id="0769c-112">可在 Azure VM 上掛接</span><span class="sxs-lookup"><span data-stu-id="0769c-112">Mountable On Azure VM</span></span>|<span data-ttu-id="0769c-113">可在內部部署環境掛接</span><span class="sxs-lookup"><span data-stu-id="0769c-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="0769c-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="0769c-114">Windows 7</span></span>              | <span data-ttu-id="0769c-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="0769c-115">SMB 2.1</span></span>     | <span data-ttu-id="0769c-116">是</span><span class="sxs-lookup"><span data-stu-id="0769c-116">Yes</span></span>                 | <span data-ttu-id="0769c-117">否</span><span class="sxs-lookup"><span data-stu-id="0769c-117">No</span></span>                  |
| <span data-ttu-id="0769c-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0769c-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="0769c-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="0769c-119">SMB 2.1</span></span>     | <span data-ttu-id="0769c-120">是</span><span class="sxs-lookup"><span data-stu-id="0769c-120">Yes</span></span>                 | <span data-ttu-id="0769c-121">否</span><span class="sxs-lookup"><span data-stu-id="0769c-121">No</span></span>                  |
| <span data-ttu-id="0769c-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="0769c-122">Windows 8</span></span>              | <span data-ttu-id="0769c-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0769c-123">SMB 3.0</span></span>     | <span data-ttu-id="0769c-124">是</span><span class="sxs-lookup"><span data-stu-id="0769c-124">Yes</span></span>                 | <span data-ttu-id="0769c-125">是</span><span class="sxs-lookup"><span data-stu-id="0769c-125">Yes</span></span>                 |
| <span data-ttu-id="0769c-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0769c-126">Windows Server 2012</span></span>    | <span data-ttu-id="0769c-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0769c-127">SMB 3.0</span></span>     | <span data-ttu-id="0769c-128">是</span><span class="sxs-lookup"><span data-stu-id="0769c-128">Yes</span></span>                 | <span data-ttu-id="0769c-129">是</span><span class="sxs-lookup"><span data-stu-id="0769c-129">Yes</span></span>                 |
| <span data-ttu-id="0769c-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0769c-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="0769c-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0769c-131">SMB 3.0</span></span>     | <span data-ttu-id="0769c-132">是</span><span class="sxs-lookup"><span data-stu-id="0769c-132">Yes</span></span>                 | <span data-ttu-id="0769c-133">是</span><span class="sxs-lookup"><span data-stu-id="0769c-133">Yes</span></span>                 |
| <span data-ttu-id="0769c-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="0769c-134">Windows 10</span></span>             | <span data-ttu-id="0769c-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0769c-135">SMB 3.0</span></span>     | <span data-ttu-id="0769c-136">是</span><span class="sxs-lookup"><span data-stu-id="0769c-136">Yes</span></span>                 | <span data-ttu-id="0769c-137">是</span><span class="sxs-lookup"><span data-stu-id="0769c-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="0769c-138">我們仍建議製作 hello 最新版本 Windows 的 KB。</span><span class="sxs-lookup"><span data-stu-id="0769c-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="0769c-139"></a>使用 Windows 掛接 Azure 檔案共用的必要條件</span><span class="sxs-lookup"><span data-stu-id="0769c-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="0769c-140">**儲存體帳戶名稱**: toomount Azure 檔案共用，您將需要 hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0769c-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="0769c-141">**儲存體帳戶金鑰**: toomount Azure 檔案共用，您將需要 hello 主要 （或次要） 的儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="0769c-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="0769c-142">掛接目前不支援 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0769c-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="0769c-143">**請確定已開啟連接埠 445**：Azure 檔案儲存體使用 SMB 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0769c-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="0769c-144">SMB 通訊透過 TCP 通訊埠 445-檢查 toosee，如果您的防火牆不會封鎖從用戶端電腦的 TCP 通訊埠 445。</span><span class="sxs-lookup"><span data-stu-id="0769c-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="0769c-145">掛接檔案總管 中的 hello Azure 檔案的共用</span><span class="sxs-lookup"><span data-stu-id="0769c-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="0769c-146">請注意，hello 指示會顯示在 Windows 10 上，而且上較舊版本中可能稍有不同。</span><span class="sxs-lookup"><span data-stu-id="0769c-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="0769c-147">**開啟檔案總管**： 作法是從 [開始] 功能表中的 hello 開頭或按 Win + E 捷徑。</span><span class="sxs-lookup"><span data-stu-id="0769c-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="0769c-148">**瀏覽 toohello"此 PC"hello 左手邊內的項目 hello 視窗。這會變更提供 hello 功能區中的 hello 功能表。在 hello 電腦] 功能表上選取 [對應網路磁碟機"**。</span><span class="sxs-lookup"><span data-stu-id="0769c-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Hello 「 對應網路磁碟機 」 的螢幕擷取畫面下拉式功能表](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="0769c-150">**從 hello hello Azure 入口網站中的 [連線] 窗格複製 hello UNC 路徑**： 的詳細的說明如何 toofind 這項資訊可以找到[這裡](storage-file-how-to-use-files-portal.md#connect-to-file-share)。</span><span class="sxs-lookup"><span data-stu-id="0769c-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![從 hello Azure 檔案儲存體連線 窗格中的 hello UNC 路徑](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="0769c-152">**選取 hello 磁碟機代號，然後輸入 hello UNC 路徑。**</span><span class="sxs-lookup"><span data-stu-id="0769c-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Hello 」 對應網路磁碟機 對話方塊的螢幕擷取畫面](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="0769c-154">**使用 hello 儲存體帳戶名稱前面加上`Azure\`hello 使用者名稱以及與 hello 密碼的儲存體帳戶金鑰。**</span><span class="sxs-lookup"><span data-stu-id="0769c-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Hello 網路認證 對話方塊的螢幕擷取畫面](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="0769c-156">**視需要使用 Azure 檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="0769c-156">**Use Azure File share as desired**.</span></span>
    
    ![現在已掛接 Azure 檔案共用](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="0769c-158">**當您準備好 toodismount （或中斷連線） hello Azure 檔案共用時，您可以 hello 下 hello 」 網路位置"檔案總管 中的 hello 共用的項目上按一下滑鼠右鍵，然後選取 「 中斷連線 」**。</span><span class="sxs-lookup"><span data-stu-id="0769c-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="0769c-159">掛接 hello Azure 檔案共用使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="0769c-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="0769c-160">**使用 hello 下列命令 toomount hello Azure 檔案共用**： 記住 tooreplace `<storage-account-name>`， `<share-name>`， `<storage-account-key>`， `<desired-drive-letter>` hello 適當資訊。</span><span class="sxs-lookup"><span data-stu-id="0769c-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="0769c-161">**使用 hello Azure 檔案共用做為所需**。</span><span class="sxs-lookup"><span data-stu-id="0769c-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="0769c-162">**當您完成時，卸載 hello Azure 檔案共用使用下列命令的 hello**。</span><span class="sxs-lookup"><span data-stu-id="0769c-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="0769c-163">您可以使用 hello`-Persist`參數`New-PSDrive`toomake hello 的 hello OS 裝載時的 Azure 檔案共用可見 toohello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="0769c-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="0769c-164">掛接 hello Azure 檔案共用，透過命令提示字元</span><span class="sxs-lookup"><span data-stu-id="0769c-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="0769c-165">**使用 hello 下列命令 toomount hello Azure 檔案共用**： 記住 tooreplace `<storage-account-name>`， `<share-name>`， `<storage-account-key>`， `<desired-drive-letter>` hello 適當資訊。</span><span class="sxs-lookup"><span data-stu-id="0769c-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="0769c-166">**使用 hello Azure 檔案共用做為所需**。</span><span class="sxs-lookup"><span data-stu-id="0769c-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="0769c-167">**當您完成時，卸載 hello Azure 檔案共用使用下列命令的 hello**。</span><span class="sxs-lookup"><span data-stu-id="0769c-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="0769c-168">您可以保存在 Windows 中的 hello 認證在重新開機設定 hello Azure 檔案共用 tooautomatically 重新連線。</span><span class="sxs-lookup"><span data-stu-id="0769c-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="0769c-169">hello，下列命令將會保存 hello 認證：</span><span class="sxs-lookup"><span data-stu-id="0769c-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="0769c-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0769c-170">Next steps</span></span>
<span data-ttu-id="0769c-171">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0769c-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="0769c-172">常見問題集</span><span class="sxs-lookup"><span data-stu-id="0769c-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="0769c-173">疑難排解</span><span class="sxs-lookup"><span data-stu-id="0769c-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="0769c-174">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="0769c-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="0769c-175">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="0769c-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="0769c-176">如何 toouse Linux 的 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="0769c-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="0769c-177">Azure 檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="0769c-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="0769c-178">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0769c-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="0769c-179">如何 toouse AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0769c-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="0769c-180">使用 Azure CLI hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0769c-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="0769c-181">針對 Azure 檔案儲存體的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0769c-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="0769c-182">部落格文章</span><span class="sxs-lookup"><span data-stu-id="0769c-182">Blog posts</span></span>
* [<span data-ttu-id="0769c-183">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="0769c-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="0769c-184">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="0769c-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="0769c-185">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="0769c-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="0769c-186">移轉資料 tooAzure 檔案</span><span class="sxs-lookup"><span data-stu-id="0769c-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="0769c-187">參考</span><span class="sxs-lookup"><span data-stu-id="0769c-187">Reference</span></span>
* [<span data-ttu-id="0769c-188">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="0769c-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="0769c-189">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="0769c-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
