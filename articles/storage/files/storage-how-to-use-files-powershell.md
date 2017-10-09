---
title: "aaaHow toouse PowerShell toomanage Azure 檔案儲存體 |Microsoft 文件"
description: "了解 toouse PowerShell toomanage Azure 檔案儲存體。"
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="0929a-103">如何 toouse PowerShell toomanage Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="0929a-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="0929a-104">您可以使用 Azure PowerShell toocreate 和管理檔案共用。</span><span class="sxs-lookup"><span data-stu-id="0929a-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="0929a-105">安裝適用於 Azure 儲存體 hello PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="0929a-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="0929a-106">tooprepare toouse PowerShell 中，下載並安裝 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0929a-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0929a-107">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) hello 安裝點和安裝指示。</span><span class="sxs-lookup"><span data-stu-id="0929a-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="0929a-108">建議您下載並安裝或升級 toohello 最新的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="0929a-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="0929a-109">透過按一下 [啟動]，然後輸入 **Windows PowerShell** 來開啟 Azure PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="0929a-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="0929a-110">hello PowerShell 視窗會為您載入 hello Azure Powershell 模組。</span><span class="sxs-lookup"><span data-stu-id="0929a-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="0929a-111">建立儲存體帳戶和金鑰的內容</span><span class="sxs-lookup"><span data-stu-id="0929a-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="0929a-112">建立 hello 儲存體帳戶的內容。</span><span class="sxs-lookup"><span data-stu-id="0929a-112">Create hello storage account context.</span></span> <span data-ttu-id="0929a-113">hello 內容封裝 hello 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="0929a-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="0929a-114">如需有關您的帳戶金鑰複製 hello 指示[Azure 入口網站](https://portal.azure.com)，請參閱[檢視與複製的儲存體存取金鑰](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="0929a-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="0929a-115">取代`storage-account-name`和`storage-account-key`與您的儲存體帳戶名稱 hello 下列範例中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0929a-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="0929a-116">建立新的檔案共用</span><span class="sxs-lookup"><span data-stu-id="0929a-116">Create a new file share</span></span>
<span data-ttu-id="0929a-117">建立 hello 新的共用，名為`logs`。</span><span class="sxs-lookup"><span data-stu-id="0929a-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="0929a-118">現在，您的檔案儲存體中便有一個檔案共用。</span><span class="sxs-lookup"><span data-stu-id="0929a-118">You now have a file share in File storage.</span></span> <span data-ttu-id="0929a-119">接下來，我們將新增目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="0929a-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0929a-120">檔案共用的 hello 名稱必須全部小寫。</span><span class="sxs-lookup"><span data-stu-id="0929a-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="0929a-121">如需有關為檔案共用與檔案命名的完整詳細資料，請參閱 [命名和參考共用、目錄、檔案及中繼資料](https://msdn.microsoft.com/library/azure/dn167011.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0929a-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="0929a-122">在 hello 檔案共用建立目錄</span><span class="sxs-lookup"><span data-stu-id="0929a-122">Create a directory in hello file share</span></span>
<span data-ttu-id="0929a-123">Hello 共用中建立目錄。</span><span class="sxs-lookup"><span data-stu-id="0929a-123">Create a directory in hello share.</span></span> <span data-ttu-id="0929a-124">在下列範例的 hello，名為 hello 目錄`CustomLogs`。</span><span class="sxs-lookup"><span data-stu-id="0929a-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="0929a-125">上傳本機檔案 toohello 目錄</span><span class="sxs-lookup"><span data-stu-id="0929a-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="0929a-126">現在您可以上傳本機檔案 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="0929a-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="0929a-127">hello 例會將檔案上傳從`C:\temp\Log1.txt`。</span><span class="sxs-lookup"><span data-stu-id="0929a-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="0929a-128">編輯 hello 檔案路徑，使它所指 tooa 有效的檔案在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="0929a-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="0929a-129">Hello 目錄中的清單 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="0929a-129">List hello files in hello directory</span></span>
<span data-ttu-id="0929a-130">toosee hello hello 目錄中的檔案，您可以列出所有 hello 目錄檔案。</span><span class="sxs-lookup"><span data-stu-id="0929a-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="0929a-131">此命令傳回 hello 檔案和子目錄 （如果有的話） hello CustomLogs 目錄中。</span><span class="sxs-lookup"><span data-stu-id="0929a-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="0929a-132">Get-AzureStorageFile 會傳回已傳入任何目錄物件的檔案和目錄清單。</span><span class="sxs-lookup"><span data-stu-id="0929a-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="0929a-133">「 Get AzureStorageFile-共用 $s"hello 根目錄中會傳回一份檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="0929a-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="0929a-134">tooget 子目錄中檔案的清單，您必須 toopass hello 子目錄 tooGet AzureStorageFile。</span><span class="sxs-lookup"><span data-stu-id="0929a-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="0929a-135">這是這個動作--hello 第一部分 hello toohello 管道命令傳回 hello 子目錄 CustomLogs 的目錄執行個體。</span><span class="sxs-lookup"><span data-stu-id="0929a-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="0929a-136">然後，已傳遞到 Get-AzureStorageFile，在 CustomLogs 傳回 hello 檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="0929a-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="0929a-137">複製檔案</span><span class="sxs-lookup"><span data-stu-id="0929a-137">Copy files</span></span>
<span data-ttu-id="0929a-138">從 Azure PowerShell 0.9.7 版開始，您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="0929a-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="0929a-139">下面我們將示範這些複製 tooperform 如何使用 PowerShell 指令程式的作業。</span><span class="sxs-lookup"><span data-stu-id="0929a-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="0929a-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0929a-140">Next steps</span></span>
<span data-ttu-id="0929a-141">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0929a-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="0929a-142">常見問題集</span><span class="sxs-lookup"><span data-stu-id="0929a-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="0929a-143">在 Windows 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0929a-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="0929a-144">在 Linux 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0929a-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    