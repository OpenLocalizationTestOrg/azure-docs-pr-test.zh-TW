---
title: "掛接 Azure 檔案共用並在 Windows 中存取共用 |Microsoft 文件"
description: "掛接 Azure 檔案共用並在 Windows 中存取共用。"
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
ms.openlocfilehash: e911e787cd1e29b2bbeaa648869c50245f2dd9ba
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="5d8a7-103">掛接 Azure 檔案共用並在 Windows 中存取共用</span><span class="sxs-lookup"><span data-stu-id="5d8a7-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="5d8a7-104">[Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)是 Microsoft 容易使用的雲端檔案系統。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="5d8a7-105">Azure 檔案共用可在 Windows 和 Windows Server 中掛接。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="5d8a7-106">本文將說明在 Windows 中掛接 Azure 檔案共用的三種不同方式：使用檔案總管 UI、透過 PowerShell，以及透過命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="5d8a7-107">若要在 Azure 區域之外掛接 Azure 檔案共用，例如內部部署或是在不同的 Azure 區域，作業系統必須支援 SMB 3.0。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="5d8a7-108">Azure 檔案共用可以掛接在 Windows 電腦上 (視 OS 版本而定，不是內部部署環境就是 Azure VM)。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="5d8a7-109">下表說明</span><span class="sxs-lookup"><span data-stu-id="5d8a7-109">Below table illustrates the</span></span> 

| <span data-ttu-id="5d8a7-110">Windows 版本</span><span class="sxs-lookup"><span data-stu-id="5d8a7-110">Windows Version</span></span>        | <span data-ttu-id="5d8a7-111">SMB 版本</span><span class="sxs-lookup"><span data-stu-id="5d8a7-111">SMB Version</span></span> |<span data-ttu-id="5d8a7-112">可在 Azure VM 上掛接</span><span class="sxs-lookup"><span data-stu-id="5d8a7-112">Mountable On Azure VM</span></span>|<span data-ttu-id="5d8a7-113">可在內部部署環境掛接</span><span class="sxs-lookup"><span data-stu-id="5d8a7-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="5d8a7-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="5d8a7-114">Windows 7</span></span>              | <span data-ttu-id="5d8a7-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="5d8a7-115">SMB 2.1</span></span>     | <span data-ttu-id="5d8a7-116">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-116">Yes</span></span>                 | <span data-ttu-id="5d8a7-117">否</span><span class="sxs-lookup"><span data-stu-id="5d8a7-117">No</span></span>                  |
| <span data-ttu-id="5d8a7-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="5d8a7-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="5d8a7-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="5d8a7-119">SMB 2.1</span></span>     | <span data-ttu-id="5d8a7-120">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-120">Yes</span></span>                 | <span data-ttu-id="5d8a7-121">否</span><span class="sxs-lookup"><span data-stu-id="5d8a7-121">No</span></span>                  |
| <span data-ttu-id="5d8a7-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="5d8a7-122">Windows 8</span></span>              | <span data-ttu-id="5d8a7-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5d8a7-123">SMB 3.0</span></span>     | <span data-ttu-id="5d8a7-124">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-124">Yes</span></span>                 | <span data-ttu-id="5d8a7-125">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-125">Yes</span></span>                 |
| <span data-ttu-id="5d8a7-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5d8a7-126">Windows Server 2012</span></span>    | <span data-ttu-id="5d8a7-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5d8a7-127">SMB 3.0</span></span>     | <span data-ttu-id="5d8a7-128">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-128">Yes</span></span>                 | <span data-ttu-id="5d8a7-129">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-129">Yes</span></span>                 |
| <span data-ttu-id="5d8a7-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5d8a7-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="5d8a7-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5d8a7-131">SMB 3.0</span></span>     | <span data-ttu-id="5d8a7-132">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-132">Yes</span></span>                 | <span data-ttu-id="5d8a7-133">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-133">Yes</span></span>                 |
| <span data-ttu-id="5d8a7-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="5d8a7-134">Windows 10</span></span>             | <span data-ttu-id="5d8a7-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5d8a7-135">SMB 3.0</span></span>     | <span data-ttu-id="5d8a7-136">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-136">Yes</span></span>                 | <span data-ttu-id="5d8a7-137">是</span><span class="sxs-lookup"><span data-stu-id="5d8a7-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="5d8a7-138">我們一律建議針對您的 Windows 版本採取最新的 KB。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="5d8a7-139"></a>使用 Windows 掛接 Azure 檔案共用的必要條件</span><span class="sxs-lookup"><span data-stu-id="5d8a7-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="5d8a7-140">**儲存體帳戶名稱**：若要掛接 Azure 檔案共用，您需要儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="5d8a7-141">**儲存體帳戶金鑰**：若要掛接 Azure 檔案共用，您需要主要 (或次要) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="5d8a7-142">掛接目前不支援 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="5d8a7-143">**請確定已開啟連接埠 445**：Azure 檔案儲存體使用 SMB 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="5d8a7-144">SMB 透過 TCP 通訊埠 445 進行通訊 - 請檢查您的防火牆不會將 TCP 通訊埠 445 從用戶端電腦封鎖。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="5d8a7-145">使用檔案總管掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="5d8a7-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="5d8a7-146">請注意，下列指示會顯示在 Windows 10 上，與較舊版本可能稍有不同。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="5d8a7-147">**開啟檔案總管**：作法是從 [開始] 功能表中開啟，或按 Win + E 捷徑。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="5d8a7-148">**瀏覽至視窗左側的「本機」項目。這會變更功能區中所提供的功能表。在 [電腦] 功能表中，選取 [連線網路磁碟機]**。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    ![「連線網路磁碟機」下拉式功能表的螢幕擷取畫面](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="5d8a7-150">**從 Azure 入口網站中的 [連線] 窗格複製 UNC 路徑**：您可以在[這裡](storage-file-how-to-use-files-portal.md#connect-to-file-share)找到如何尋找這項資訊的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Azure 檔案儲存體連線窗格的 UNC 路徑](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="5d8a7-152">**選取磁碟機代號並輸入 UNC 路徑。**</span><span class="sxs-lookup"><span data-stu-id="5d8a7-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    ![「連線網路磁碟機」對話方塊的螢幕擷取畫面](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="5d8a7-154">**使用前面加上 `Azure\` 的儲存體帳戶名稱作為使用者名稱，並使用儲存體帳戶金鑰作為密碼。**</span><span class="sxs-lookup"><span data-stu-id="5d8a7-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![網路認證對話方塊的螢幕擷取畫面](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="5d8a7-156">**視需要使用 Azure 檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-156">**Use Azure File share as desired**.</span></span>
    
    ![現在已掛接 Azure 檔案共用](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="5d8a7-158">**當您準備好要卸載 (或中斷連線) Azure 檔案共用時，您可以以滑鼠右鍵按一下 [檔案總管] 中「網路位置」下的共用項目，然後選取 [中斷連線]**。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="5d8a7-159">使用 PowerShell 掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="5d8a7-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="5d8a7-160">**使用下列命令來掛接 Azure 檔案共用**：請記得要使用正確的資訊來取代 `<storage-account-name>`、`<share-name>`、`<storage-account-key>` 以及 `<desired-drive-letter>`。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="5d8a7-161">**視需要使用 Azure 檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="5d8a7-162">**當您完成時，使用下列命令卸載 Azure 檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="5d8a7-163">當仍掛接時，您可以在 `New-PSDrive`上使用 `-Persist` 參數對其餘的 OS 顯示 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="5d8a7-164">使用命令提示字元掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="5d8a7-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="5d8a7-165">**使用下列命令來掛接 Azure 檔案共用**：請記得要使用正確的資訊來取代 `<storage-account-name>`、`<share-name>`、`<storage-account-key>` 以及 `<desired-drive-letter>`。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="5d8a7-166">**視需要使用 Azure 檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="5d8a7-167">**當您完成時，使用下列命令卸載 Azure 檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="5d8a7-168">您可以藉由保存 Windows 的認證，設定在重新開機時自動重新連線 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="5d8a7-169">下列命令將會保存認證：</span><span class="sxs-lookup"><span data-stu-id="5d8a7-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="5d8a7-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d8a7-170">Next steps</span></span>
<span data-ttu-id="5d8a7-171">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5d8a7-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="5d8a7-172">常見問題集</span><span class="sxs-lookup"><span data-stu-id="5d8a7-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="5d8a7-173">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5d8a7-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="5d8a7-174">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="5d8a7-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="5d8a7-175">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="5d8a7-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="5d8a7-176">如何搭配使用 Azure 檔案儲存體與 Linux</span><span class="sxs-lookup"><span data-stu-id="5d8a7-176">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="5d8a7-177">Azure 檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="5d8a7-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="5d8a7-178">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="5d8a7-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="5d8a7-179">如何搭配使用 AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="5d8a7-179">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="5d8a7-180">使用 Azure CLI 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="5d8a7-180">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="5d8a7-181">針對 Azure 檔案儲存體的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="5d8a7-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="5d8a7-182">部落格文章</span><span class="sxs-lookup"><span data-stu-id="5d8a7-182">Blog posts</span></span>
* [<span data-ttu-id="5d8a7-183">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="5d8a7-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="5d8a7-184">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="5d8a7-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="5d8a7-185">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="5d8a7-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="5d8a7-186">將資料移轉至 Azure 檔案</span><span class="sxs-lookup"><span data-stu-id="5d8a7-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="5d8a7-187">參考</span><span class="sxs-lookup"><span data-stu-id="5d8a7-187">Reference</span></span>
* [<span data-ttu-id="5d8a7-188">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="5d8a7-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="5d8a7-189">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="5d8a7-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
