---
title: "如何使用 PowerShell 來管理 Azure 檔案儲存體 | Microsoft Docs"
description: "了解如何使用 PowerShell 來管理 Azure 檔案儲存體。"
services: storage
documentationcenter: 
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
ms.openlocfilehash: ce62d4423ce711a6902aed7b8174ff4e827f6083
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="da228-103">如何使用 PowerShell 來管理 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="da228-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="da228-104">您可以使用 Azure PowerShell 建立及管理檔案共用。</span><span class="sxs-lookup"><span data-stu-id="da228-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="da228-105">安裝適用於 Azure 儲存體的 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="da228-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="da228-106">若要準備使用 PowerShell，請下載並安裝 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="da228-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="da228-107">如需安裝點和安裝指示的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) 。</span><span class="sxs-lookup"><span data-stu-id="da228-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="da228-108">建議您下載和安裝或升級至最新的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="da228-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="da228-109">透過按一下 [啟動]，然後輸入 **Windows PowerShell** 來開啟 Azure PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="da228-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="da228-110">PowerShell 視窗便會為您載入 Azure Powershell 模組。</span><span class="sxs-lookup"><span data-stu-id="da228-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="da228-111">建立儲存體帳戶和金鑰的內容</span><span class="sxs-lookup"><span data-stu-id="da228-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="da228-112">建立儲存體帳戶內容。</span><span class="sxs-lookup"><span data-stu-id="da228-112">Create the storage account context.</span></span> <span data-ttu-id="da228-113">內容包含儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="da228-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="da228-114">如需從 [Azure 入口網站](https://portal.azure.com)複製帳戶金鑰的指示，請參閱[檢視和複製儲存體存取金鑰](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="da228-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="da228-115">使用下列範例中的儲存體帳戶名稱和金鑰來取代 `storage-account-name` 和 `storage-account-key`。</span><span class="sxs-lookup"><span data-stu-id="da228-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="da228-116">建立新的檔案共用</span><span class="sxs-lookup"><span data-stu-id="da228-116">Create a new file share</span></span>
<span data-ttu-id="da228-117">建立名為 `logs` 的新共用。</span><span class="sxs-lookup"><span data-stu-id="da228-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="da228-118">現在，您的檔案儲存體中便有一個檔案共用。</span><span class="sxs-lookup"><span data-stu-id="da228-118">You now have a file share in File storage.</span></span> <span data-ttu-id="da228-119">接下來，我們將新增目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="da228-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da228-120">您的檔案共用名稱必須是全部小寫。</span><span class="sxs-lookup"><span data-stu-id="da228-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="da228-121">如需有關為檔案共用與檔案命名的完整詳細資料，請參閱 [命名和參考共用、目錄、檔案及中繼資料](https://msdn.microsoft.com/library/azure/dn167011.aspx)。</span><span class="sxs-lookup"><span data-stu-id="da228-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="da228-122">在檔案共用中建立目錄</span><span class="sxs-lookup"><span data-stu-id="da228-122">Create a directory in the file share</span></span>
<span data-ttu-id="da228-123">在共用中建立目錄。</span><span class="sxs-lookup"><span data-stu-id="da228-123">Create a directory in the share.</span></span> <span data-ttu-id="da228-124">在下列範例中，目錄的名稱為 `CustomLogs`。</span><span class="sxs-lookup"><span data-stu-id="da228-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="da228-125">上傳本機檔案至目錄</span><span class="sxs-lookup"><span data-stu-id="da228-125">Upload a local file to the directory</span></span>
<span data-ttu-id="da228-126">現在，請上傳本機檔案至目錄。</span><span class="sxs-lookup"><span data-stu-id="da228-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="da228-127">下列範例會從 `C:\temp\Log1.txt` 上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="da228-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="da228-128">編輯檔案路徑，以指向本機機器上的有效檔案。</span><span class="sxs-lookup"><span data-stu-id="da228-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="da228-129">列出目錄中的檔案</span><span class="sxs-lookup"><span data-stu-id="da228-129">List the files in the directory</span></span>
<span data-ttu-id="da228-130">若要查看目錄中的檔案，您可以列出目錄的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="da228-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="da228-131">此命令會傳回 CustomLogs 目錄中的檔案和子目錄 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="da228-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="da228-132">Get-AzureStorageFile 會傳回已傳入任何目錄物件的檔案和目錄清單。</span><span class="sxs-lookup"><span data-stu-id="da228-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="da228-133">"Get-AzureStorageFile -Share $s" 會傳回根目錄中的檔案和目錄清單。</span><span class="sxs-lookup"><span data-stu-id="da228-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="da228-134">若要取得子目錄中的檔案清單，您必須將子目錄傳遞至 Get-AzureStorageFile。</span><span class="sxs-lookup"><span data-stu-id="da228-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="da228-135">這就是其作用 -- 命令的第一個部分 (由管道決定) 會傳回 CustomLogs 子目錄的目錄執行個體。</span><span class="sxs-lookup"><span data-stu-id="da228-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="da228-136">然後該執行個體會傳入 Get-AzureStorageFile，進而傳回 CustomLogs 中的檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="da228-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="da228-137">複製檔案</span><span class="sxs-lookup"><span data-stu-id="da228-137">Copy files</span></span>
<span data-ttu-id="da228-138">從 Azure PowerShell 0.9.7 版開始，您可以將檔案複製到另一個檔案、將檔案複製到 Blob 或將 Blob 複製到檔案。</span><span class="sxs-lookup"><span data-stu-id="da228-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="da228-139">下列示範如何使用 PowerShell Cmdlet 執行這些複製作業。</span><span class="sxs-lookup"><span data-stu-id="da228-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="da228-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da228-140">Next steps</span></span>
<span data-ttu-id="da228-141">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="da228-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="da228-142">常見問題集</span><span class="sxs-lookup"><span data-stu-id="da228-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="da228-143">在 Windows 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="da228-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="da228-144">在 Linux 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="da228-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    