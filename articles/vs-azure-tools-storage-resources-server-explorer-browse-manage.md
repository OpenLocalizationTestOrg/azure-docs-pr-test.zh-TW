---
title: "使用伺服器總管瀏覽和管理儲存體資源 | Microsoft Docs"
description: "使用伺服器總管瀏覽和管理儲存體資源"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: 43ab501c69c0c1e3271dbfcf08e5342a3507ab82
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a><span data-ttu-id="05723-103">使用伺服器總管瀏覽和管理儲存體資源</span><span class="sxs-lookup"><span data-stu-id="05723-103">Browsing and Managing Storage Resources with Server Explorer</span></span>
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a><span data-ttu-id="05723-104">概觀</span><span class="sxs-lookup"><span data-stu-id="05723-104">Overview</span></span>
<span data-ttu-id="05723-105">如果您已經安裝 Azure Tools for Microsoft Visual Studio，您可以從 Azure 的儲存體帳戶檢視 blob、佇列和資料表資料。</span><span class="sxs-lookup"><span data-stu-id="05723-105">If you've installed the Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span></span> <span data-ttu-id="05723-106">在 [伺服器總管] 中的 Azure 儲存體節點會顯示位於您的本機儲存體模擬器帳戶和其他 Azure 儲存體帳戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="05723-106">The Azure Storage node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span></span>

<span data-ttu-id="05723-107">若要在 Visual Studio 中檢視 [伺服器總管]，請在功能表列上選擇 [檢視] 和 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="05723-107">To view Server Explorer in Visual Studio, on the menu bar, choose **View**, **Server Explorer**.</span></span> <span data-ttu-id="05723-108">儲存體節點會顯示存在於您連接之每個 Azure 訂用帳戶/憑證下的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="05723-108">The storage node shows all of the storage accounts that exist under each Azure subscription/certificate you're connected to.</span></span> <span data-ttu-id="05723-109">如果您的儲存體帳戶未出現，您可以遵循 [本主題稍後](#add-storage-accounts-by-using-server-explorer)的指示加以新增。</span><span class="sxs-lookup"><span data-stu-id="05723-109">If your storage account doesn't appear, you can add it by following the instructions [later in this topic](#add-storage-accounts-by-using-server-explorer).</span></span>

<span data-ttu-id="05723-110">從 Azure SDK 2.7 開始，您也可以使用新的雲端總管來檢視和管理您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="05723-110">Starting in Azure SDK 2.7, you can also use the new Cloud Explorer to view and manage your Azure resources.</span></span> <span data-ttu-id="05723-111">如需詳細資訊，請參閱 [使用雲端總管管理 Azure 資源](vs-azure-tools-resources-managing-with-cloud-explorer.md) 。</span><span class="sxs-lookup"><span data-stu-id="05723-111">See [Managing Azure Resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) for more information.</span></span>

## <a name="view-and-manage-storage-resources-in-visual-studio"></a><span data-ttu-id="05723-112">檢視和管理 Visual Studio 中的儲存體資源</span><span class="sxs-lookup"><span data-stu-id="05723-112">View and manage storage resources in Visual Studio</span></span>
<span data-ttu-id="05723-113">[伺服器總管] 會自動在您的儲存體模擬器帳戶中顯示 blob、佇列和資料表的清單。</span><span class="sxs-lookup"><span data-stu-id="05723-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span></span> <span data-ttu-id="05723-114">儲存體模擬器帳戶會在儲存體節點下的 [伺服器總管] 中列出，做為 **開發** 節點。</span><span class="sxs-lookup"><span data-stu-id="05723-114">The storage emulator account is listed in Server Explorer under the Storage node as the **Development** node.</span></span>

<span data-ttu-id="05723-115">若要查看儲存體模擬器帳戶的資源，請展開 **開發** 節點。</span><span class="sxs-lookup"><span data-stu-id="05723-115">To see the storage emulator account’s resources, expand the **Development** node.</span></span> <span data-ttu-id="05723-116">當您展開 **開發** 節點時，如果尚未啟動儲存體模擬器，它會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="05723-116">If the storage emulator hasn’t been started when you expand the **Development** node, it will automatically start.</span></span> <span data-ttu-id="05723-117">這可能需要數秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="05723-117">This can take several seconds.</span></span> <span data-ttu-id="05723-118">當儲存體模擬器啟動時，您可以繼續在 Visual Studio 的其他區域中運作。</span><span class="sxs-lookup"><span data-stu-id="05723-118">You can continue to work in other areas of Visual Studio while the storage emulator starts.</span></span>

<span data-ttu-id="05723-119">若要檢視儲存體帳戶中的資源，請在 [伺服器總管] 中展開儲存體帳戶的節點。</span><span class="sxs-lookup"><span data-stu-id="05723-119">To view resources in a storage account, expand the storage account’s node in Server Explorer.</span></span> <span data-ttu-id="05723-120">下列子節點會隨即出現：</span><span class="sxs-lookup"><span data-stu-id="05723-120">The following sub-nodes appear:</span></span>

* <span data-ttu-id="05723-121">Blob</span><span class="sxs-lookup"><span data-stu-id="05723-121">Blobs</span></span>
* <span data-ttu-id="05723-122">佇列</span><span class="sxs-lookup"><span data-stu-id="05723-122">Queues</span></span>
* <span data-ttu-id="05723-123">資料表</span><span class="sxs-lookup"><span data-stu-id="05723-123">Tables</span></span>

## <a name="work-with-blob-resources"></a><span data-ttu-id="05723-124">使用 Blob 資源</span><span class="sxs-lookup"><span data-stu-id="05723-124">Work with Blob Resources</span></span>
<span data-ttu-id="05723-125">Blob 節點會顯示所選之儲存體帳戶的容器清單。</span><span class="sxs-lookup"><span data-stu-id="05723-125">The Blobs node displays a list of containers for the selected storage account.</span></span> <span data-ttu-id="05723-126">Blob 容器包含 blob 檔案，您可以將這些 blob 組織成資料夾和子資料夾。</span><span class="sxs-lookup"><span data-stu-id="05723-126">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span></span> <span data-ttu-id="05723-127">如需詳細資訊，請參閱 [如何從 .NET 使用 Blob 儲存體](storage/blobs/storage-dotnet-how-to-use-blobs.md) (英文)。</span><span class="sxs-lookup"><span data-stu-id="05723-127">See [How to use Blob Storage from .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information.</span></span>

### <a name="to-create-a-blob-container"></a><span data-ttu-id="05723-128">建立 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="05723-128">To create a blob container</span></span>
1. <span data-ttu-id="05723-129">開啟 **Blobs**節點的捷徑功能表，然後選擇 [建立 Blob 容器]。</span><span class="sxs-lookup"><span data-stu-id="05723-129">Open the shortcut menu for the **Blobs** node, and then choose **Create Blob Container**.</span></span>
2. <span data-ttu-id="05723-130">在 [建立 Blob 容器] 對話方塊中，輸入新容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="05723-130">In the **Create Blob Container** dialog box, enter the name of the new container.</span></span>  
3. <span data-ttu-id="05723-131">按下鍵盤上的 **ENTER** 鍵，也可以按一下或點選名稱欄位以外的地方，以儲存 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="05723-131">Press **ENTER** on your keyboard or you can click or tap outside of the name field to save the blob container.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05723-132">Blob 容器名稱必須以數字 (0-9) 或小寫字母 (a-z) 開頭。</span><span class="sxs-lookup"><span data-stu-id="05723-132">The blob container name must begin with a number (0-9) or lowercase letter (a-z).</span></span>
   > 
   > 

### <a name="to-delete-a-blob-container"></a><span data-ttu-id="05723-133">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="05723-133">To delete a blob container</span></span>
* <span data-ttu-id="05723-134">開啟您想要移除之 Blob 容器的捷徑功能表，然後選擇 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="05723-134">Open the shortcut menu for the blob container you want to remove and then choose **Delete**.</span></span>

### <a name="to-display-a-list-of-the-items-contained-in-a-blob-container"></a><span data-ttu-id="05723-135">顯示包含在 blob 容器中的項目清單</span><span class="sxs-lookup"><span data-stu-id="05723-135">To display a list of the items contained in a blob container</span></span>
* <span data-ttu-id="05723-136">開啟清單中 Blob 容器名稱的捷徑功能表，然後選擇 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="05723-136">Open the shortcut menu for a blob container name in the list and then choose **Open**.</span></span>
  
    <span data-ttu-id="05723-137">當您檢視 blob 容器的內容時，它就會出現在稱為 blob 容器檢視的索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="05723-137">When you view the contents of a blob container, it appears in a tab known as the blob container view.</span></span>
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    <span data-ttu-id="05723-139">您可以使用 blob 容器檢視右上角的按鈕在 blob 上執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="05723-139">You can perform the following operations on blobs by using the buttons in the top-right corner of the blob container view:</span></span>
  
  * <span data-ttu-id="05723-140">輸入篩選值並加以套用</span><span class="sxs-lookup"><span data-stu-id="05723-140">Enter a filter value and apply it</span></span>
  * <span data-ttu-id="05723-141">重新整理容器中的 blob 清單</span><span class="sxs-lookup"><span data-stu-id="05723-141">Refresh the list of blobs in the container</span></span>
  * <span data-ttu-id="05723-142">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="05723-142">Upload a file</span></span>
  * <span data-ttu-id="05723-143">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="05723-143">Delete a blob</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="05723-144">從 blob 容器中刪除檔案並不會刪除基礎的檔案。只會將它從 blob 容器移除。</span><span class="sxs-lookup"><span data-stu-id="05723-144">Deleting a file from a blob container doesn’t delete the underlying file; it only removes it from the blob container.</span></span>
    > 
    > 
  * <span data-ttu-id="05723-145">開啟 blob</span><span class="sxs-lookup"><span data-stu-id="05723-145">Open a blob</span></span>
  * <span data-ttu-id="05723-146">將 blob 儲存到本機電腦</span><span class="sxs-lookup"><span data-stu-id="05723-146">Save a blob to the local computer</span></span>

### <a name="to-create-a-folder-or-subfolder-in-a-blob-container"></a><span data-ttu-id="05723-147">在 blob 容器中建立資料夾或子資料夾</span><span class="sxs-lookup"><span data-stu-id="05723-147">To create a folder or subfolder in a blob container</span></span>
1. <span data-ttu-id="05723-148">在 [Cloud Explorer] 中選擇 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="05723-148">Choose the blob container in Cloud Explorer.</span></span> <span data-ttu-id="05723-149">在 [容器] 視窗中，選擇 [上傳 Blob]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-149">In the container window, choose the **Upload Blob** button.</span></span>
   
    ![將檔案上傳至 blob 資料夾](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. <span data-ttu-id="05723-151">在 [上傳新的檔案] 對話方塊中，選擇 [瀏覽] 按鈕來指定您想要上傳的檔案，然後在 [資料夾 (選擇性)] 方塊中輸入資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="05723-151">In the **Upload New File** dialog box, choose the **Browse** button to specify the file you want to upload, and then enter a folder name in the **Folder (optional)** box.</span></span>
   
    <span data-ttu-id="05723-152">您可以遵循相同的程序將子資料夾加入至容器資料夾。</span><span class="sxs-lookup"><span data-stu-id="05723-152">You can add subfolders in container folders by following the same procedure.</span></span> <span data-ttu-id="05723-153">如果您未指定資料夾名稱，檔案將會上傳至 Blob 容器的最上層。</span><span class="sxs-lookup"><span data-stu-id="05723-153">If you don’t specify a folder name, the file will be uploaded to the top level of the blob container.</span></span> <span data-ttu-id="05723-154">檔案會出現在容器中的特定資料夾。</span><span class="sxs-lookup"><span data-stu-id="05723-154">The file appears in the specified folder in the container.</span></span>
   
    ![加入至 blob 容器的資料夾](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. <span data-ttu-id="05723-156">按兩下資料夾或按下 ENTER 以查看資料夾的內容。</span><span class="sxs-lookup"><span data-stu-id="05723-156">Double-click the folder or press ENTER to see the contents of the folder.</span></span> <span data-ttu-id="05723-157">當您位於容器的資料夾中，您可以藉由選擇 [開啟上層目錄]  \(向上箭頭) 按鈕來瀏覽回容器的根。</span><span class="sxs-lookup"><span data-stu-id="05723-157">When you’re in the container’s folder, you can navigate back to the root of the container by choosing the **Open Parent Directory** (up arrow) button.</span></span>

### <a name="to-delete-a-container-folder"></a><span data-ttu-id="05723-158">刪除容器資料夾</span><span class="sxs-lookup"><span data-stu-id="05723-158">To delete a container folder</span></span>
* <span data-ttu-id="05723-159">刪除資料夾中的所有檔案</span><span class="sxs-lookup"><span data-stu-id="05723-159">Delete all of the files in the folder</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="05723-160">因為 blob 容器中的資料夾是虛擬資料夾，所以您無法建立空的資料夾，也無法刪除資料夾並刪除其檔案內容。</span><span class="sxs-lookup"><span data-stu-id="05723-160">Because folders in blob containers are virtual folders, you can’t create an empty folder, nor can you delete a folder to delete its file contents.</span></span> <span data-ttu-id="05723-161">您必須刪除資料夾的完整內容才能刪除該資料夾。</span><span class="sxs-lookup"><span data-stu-id="05723-161">You have to delete the entire contents of a folder to delete the folder.</span></span>
  > 
  > 

### <a name="to-filter-blobs-in-a-container"></a><span data-ttu-id="05723-162">在容器中篩選 Blob</span><span class="sxs-lookup"><span data-stu-id="05723-162">To filter blobs in a container</span></span>
<span data-ttu-id="05723-163">您可以藉由指定一般的前置詞來篩選顯示的 blob。</span><span class="sxs-lookup"><span data-stu-id="05723-163">You can filter the blobs that are displayed by specifying a common prefix.</span></span>

<span data-ttu-id="05723-164">例如，如果您在篩選文字方塊中輸入前置詞 `hello`，然後選擇 [執行 (!)] 按鈕，則只會出現以 'hello' 開頭的 blob。</span><span class="sxs-lookup"><span data-stu-id="05723-164">For example, if you enter the prefix `hello` in the filter text box and then choose the **Execute** (**!**)button, only blobs that begin with 'hello' appear.</span></span>

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> <span data-ttu-id="05723-166">篩選欄位會區分大小寫，並且不支援使用萬用字元篩選。</span><span class="sxs-lookup"><span data-stu-id="05723-166">The filter field is case-sensitive and doesn’t support filtering with wildcard characters.</span></span> <span data-ttu-id="05723-167">Blob 只可以利用前置詞篩選。</span><span class="sxs-lookup"><span data-stu-id="05723-167">Blobs can only be filtered by prefix.</span></span> <span data-ttu-id="05723-168">如果您要使用分隔符號在虛擬階層中組織 blob，前置詞可能會包含分隔符號。</span><span class="sxs-lookup"><span data-stu-id="05723-168">The prefix may include a delimiter if you are using a delimiter to organize blobs in a virtual hierarchy.</span></span> <span data-ttu-id="05723-169">例如，篩選前置詞 HelloFabric/ 會傳回所有以該字串開頭的 blob。</span><span class="sxs-lookup"><span data-stu-id="05723-169">For example, filtering on the prefix HelloFabric/ returns all blobs beginning with that string.</span></span>
> 
> 

### <a name="to-download-blob-data"></a><span data-ttu-id="05723-170">下載 blob 資料</span><span class="sxs-lookup"><span data-stu-id="05723-170">To download blob data</span></span>
* <span data-ttu-id="05723-171">在 [Cloud Explorer] 中，開啟一或多個 Blob 的捷徑功能表，並選擇 [開啟]，或選擇 Blob 名稱，然後選擇 [開啟] 按鈕，或按兩下 Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="05723-171">In **Cloud Explorer**, open the shortcut menu for one or more blobs and then choose **Open**, or choose the blob name and then choose the **Open** button, or double-click the blob name.</span></span>
  
    <span data-ttu-id="05723-172">Blob 下載進度會顯示在 [Azure 活動記錄檔]  視窗中。</span><span class="sxs-lookup"><span data-stu-id="05723-172">The progress of a blob download appears in the **Azure Activity Log** window.</span></span>
  
    <span data-ttu-id="05723-173">Blob 會在該檔案類型的預設編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="05723-173">The blob opens in the default editor for that file type.</span></span> <span data-ttu-id="05723-174">如果作業系統辨識出此檔案類型，檔案就會在本機安裝的應用程式中開啟。否則系統會提示您選擇適用於 blob 檔案類型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="05723-174">If the operating system recognizes the file type, the file opens in a locally installed application; otherwise, you're prompted to choose an application that’s appropriate for the file type of the blob.</span></span> <span data-ttu-id="05723-175">下載 blob 時所建立的本機檔案會標示為唯讀。</span><span class="sxs-lookup"><span data-stu-id="05723-175">The local file that’s created when you download a blob is marked as read-only.</span></span>
  
    <span data-ttu-id="05723-176">Blob 資料會在本機快取，並在 Blob 服務中針對上次修改 blob 的時間進行檢查。</span><span class="sxs-lookup"><span data-stu-id="05723-176">Blob data is cached locally and checked against the blob's last modified time in the Blob service.</span></span> <span data-ttu-id="05723-177">如果自上次下載 Blob 後已將其更新，它會再次下載。否則將從本機磁碟載入 Blob。</span><span class="sxs-lookup"><span data-stu-id="05723-177">If the blob has been updated since it was last downloaded, it will be downloaded again; otherwise, the blob will be loaded from the local disk.</span></span> <span data-ttu-id="05723-178">根據預設，Blob 會下載至暫存目錄。</span><span class="sxs-lookup"><span data-stu-id="05723-178">By default, a blob is downloaded to a temporary directory.</span></span> <span data-ttu-id="05723-179">若要下載 blob 到特定的目錄中，請開啟所選 blob 名稱的捷徑功能表並選擇 [另存新檔]。</span><span class="sxs-lookup"><span data-stu-id="05723-179">To download blobs to a specific directory, open the shortcut menu for the selected blob names and choose **Save As**.</span></span> <span data-ttu-id="05723-180">當您以這種方式儲存 blob 時，blob 檔案尚未開啟，本機檔案會利用讀寫屬性建立。</span><span class="sxs-lookup"><span data-stu-id="05723-180">When you save a blob in this manner, the blob file is not opened, and the local file is created with read-write attributes.</span></span>

### <a name="to-upload-blobs"></a><span data-ttu-id="05723-181">上傳 blob</span><span class="sxs-lookup"><span data-stu-id="05723-181">To upload blobs</span></span>
* <span data-ttu-id="05723-182">當容器開啟以在 blob 容器檢視中加以檢視時，選擇 [上傳 Blob]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-182">Choose the **Upload Blob** button when the container is open for viewing in the blob container view.</span></span>
  
    <span data-ttu-id="05723-183">您可以選擇一或多個檔案上傳，而且您可以上傳任何類型的檔案。</span><span class="sxs-lookup"><span data-stu-id="05723-183">You can choose one or more files to upload and you can upload files of any type.</span></span> <span data-ttu-id="05723-184">**Azure 活動記錄檔** 會顯示上傳的進度。</span><span class="sxs-lookup"><span data-stu-id="05723-184">The **Azure Activity Log** shows the progress of the upload.</span></span> <span data-ttu-id="05723-185">如需如何使用 blob 資料的詳細資訊，請參閱 [如何在 .NET 中使用 Azure Blob 儲存體服務](http://go.microsoft.com/fwlink/p/?LinkId=267911)。</span><span class="sxs-lookup"><span data-stu-id="05723-185">For more information about how to work with blob data, see [How to use the Azure Blob Storage Service in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span></span>

### <a name="to-view-logs-transferred-to-blobs"></a><span data-ttu-id="05723-186">檢視傳送輸到 blob 的記錄檔</span><span class="sxs-lookup"><span data-stu-id="05723-186">To view logs transferred to blobs</span></span>
* <span data-ttu-id="05723-187">如果您使用 Azure 診斷記錄來自 Azure 應用程式的資料，且您已將記錄檔傳輸至您的儲存體帳戶，您會看到 Azure 位這些記錄檔所建立的容器。</span><span class="sxs-lookup"><span data-stu-id="05723-187">If you are using Azure Diagnostics to log data from your Azure application and you have transferred logs to your storage account, you’ll see containers that were created by Azure for these logs.</span></span> <span data-ttu-id="05723-188">在 [伺服器總管] 中檢視這些記錄檔是利用應用程式識別問題的簡單方法，尤其是在應用程式部署至 Azure 時。</span><span class="sxs-lookup"><span data-stu-id="05723-188">Viewing these logs in Server Explorer is an easy way to identify problems with your application, especially if it’s been deployed to Azure.</span></span> <span data-ttu-id="05723-189">如需 Azure 診斷的詳細資訊，請參閱 [使用 Azure 診斷收集記錄資料](https://msdn.microsoft.com/library/azure/gg433048.aspx)。</span><span class="sxs-lookup"><span data-stu-id="05723-189">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span></span>

### <a name="to-get-the-url-for-a-blob"></a><span data-ttu-id="05723-190">取得 blob 的 URL</span><span class="sxs-lookup"><span data-stu-id="05723-190">To get the URL for a blob</span></span>
* <span data-ttu-id="05723-191">開啟 blob 的捷徑功能表並選擇 [複製 URL] 。</span><span class="sxs-lookup"><span data-stu-id="05723-191">Open the blob’s shortcut menu and then choose **Copy URL**.</span></span>

### <a name="to-edit-a-blob"></a><span data-ttu-id="05723-192">編輯 blob</span><span class="sxs-lookup"><span data-stu-id="05723-192">To edit a blob</span></span>
* <span data-ttu-id="05723-193">選取 blob，然後選擇 [開啟 Blob]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-193">Select the blob and then choose the **Open Blob** button.</span></span>
  
    <span data-ttu-id="05723-194">檔案會下載到暫存位置並在本機電腦上開啟。</span><span class="sxs-lookup"><span data-stu-id="05723-194">The file is downloaded to a temporary location and opened on the local computer.</span></span> <span data-ttu-id="05723-195">您必須在變更之後再次上傳 blob。</span><span class="sxs-lookup"><span data-stu-id="05723-195">You must upload the blob again after you make changes.</span></span>

## <a name="work-with-queue-resources"></a><span data-ttu-id="05723-196">使用佇列資源</span><span class="sxs-lookup"><span data-stu-id="05723-196">Work with Queue Resources</span></span>
<span data-ttu-id="05723-197">儲存體服務佇列裝載在 Azure 儲存體帳戶中，您可以使用它們來讓您的雲端服務角色利用訊息傳遞機制彼此通訊並與其他服務通訊。</span><span class="sxs-lookup"><span data-stu-id="05723-197">Storage services queues are hosted in an Azure storage account and you can use them to allow your cloud service roles to communicate with each other and with other services by a message passing mechanism.</span></span> <span data-ttu-id="05723-198">您可以透過雲端服務和外部用戶端的 web 服務以程式設計方式存取佇列。</span><span class="sxs-lookup"><span data-stu-id="05723-198">You can access the queue programmatically through a cloud service and over a web service for external clients.</span></span> <span data-ttu-id="05723-199">您也可以在 Visual Studio 中使用 [伺服器總管] 直接存取佇列。</span><span class="sxs-lookup"><span data-stu-id="05723-199">You can also access the queue directly by using Server Explorer in Visual Studio.</span></span>

<span data-ttu-id="05723-200">當您開發使用佇列的雲端服務時，您可能會想要使用 Visual Studio 來建立佇列，並且在您開發和測試您的程式碼時以互動方式使用它們。</span><span class="sxs-lookup"><span data-stu-id="05723-200">When you develop a cloud service that uses queues, you might want to use Visual Studio to create queues and work with them interactively while you develop and test your code.</span></span>

<span data-ttu-id="05723-201">在 [伺服器總管] 中，您可以檢視儲存體帳戶中的佇列、建立和刪除佇列、開啟佇列以檢視其訊息，以及將訊息加入至佇列。</span><span class="sxs-lookup"><span data-stu-id="05723-201">In Server Explorer, you can view the queues in a storage account, create and delete queues, open a queue to view its messages, and add messages to a queue.</span></span> <span data-ttu-id="05723-202">當您開啟佇列進行檢視時，您可以檢視個別訊息，而且您可以使用左上角的按鈕在佇列上執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="05723-202">When you open a queue for viewing, you can view the individual messages, and you can perform the following actions on the queue by using the buttons in the top-left corner:</span></span>

* <span data-ttu-id="05723-203">重新整理佇列的檢視</span><span class="sxs-lookup"><span data-stu-id="05723-203">Refresh the view of the queue</span></span>
* <span data-ttu-id="05723-204">將訊息新增至佇列</span><span class="sxs-lookup"><span data-stu-id="05723-204">Add a message to the queue</span></span>
* <span data-ttu-id="05723-205">清除最上層佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05723-205">Dequeue the topmost message</span></span>
* <span data-ttu-id="05723-206">清除整個佇列</span><span class="sxs-lookup"><span data-stu-id="05723-206">Clear the entire queue</span></span>

<span data-ttu-id="05723-207">下圖顯示包含兩個訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="05723-207">The following image shows a queue that contains two messages.</span></span>

![檢視佇列](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

<span data-ttu-id="05723-209">如需儲存體服務佇列的詳細資訊，請參閱 [作法：使用佇列儲存體服務](http://go.microsoft.com/fwlink/?LinkID=264702)。</span><span class="sxs-lookup"><span data-stu-id="05723-209">For more information about storage services queues, see [How to: Use the Queue Storage Service](http://go.microsoft.com/fwlink/?LinkID=264702).</span></span> <span data-ttu-id="05723-210">如需儲存體服務佇列之 Web 服務的詳細資訊，請參閱 [佇列服務概念](http://go.microsoft.com/fwlink/?LinkId=264788)。</span><span class="sxs-lookup"><span data-stu-id="05723-210">For information about the web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span></span> <span data-ttu-id="05723-211">如需有關如何使用 Visual Studio 將訊息傳送至儲存體服務佇列的資訊，請參閱 [傳送訊息至儲存體服務佇列](https://msdn.microsoft.com/library/azure/jj649344.aspx)。</span><span class="sxs-lookup"><span data-stu-id="05723-211">For information about how to send messages to a storage services queue by using Visual Studio, see [Sending Messages to a Storage Services Queue](https://msdn.microsoft.com/library/azure/jj649344.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="05723-212">儲存體服務佇列與服務匯流排佇列不同。</span><span class="sxs-lookup"><span data-stu-id="05723-212">Storage services queues are distinct from service bus queues.</span></span> <span data-ttu-id="05723-213">如需服務匯流排佇列的詳細資訊，請參閱服務匯流排佇列、主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="05723-213">For more information about service bus queues, see Service Bus Queues, Topics, and Subscriptions.</span></span>
> 
> 

## <a name="work-with-table-resources"></a><span data-ttu-id="05723-214">使用資料表資源</span><span class="sxs-lookup"><span data-stu-id="05723-214">Work with Table Resources</span></span>
<span data-ttu-id="05723-215">Azure 資料表儲存體服務可儲存大量的結構化資料。</span><span class="sxs-lookup"><span data-stu-id="05723-215">The Azure Table storage service stores large amounts of structured data.</span></span> <span data-ttu-id="05723-216">此服務是一個 NoSQL 資料存放區，接受來自 Azure 雲端內外經過驗證的呼叫。</span><span class="sxs-lookup"><span data-stu-id="05723-216">The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="05723-217">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="05723-217">Azure tables are ideal for storing structured, non-relational data.</span></span>

### <a name="to-create-a-table"></a><span data-ttu-id="05723-218">建立資料表</span><span class="sxs-lookup"><span data-stu-id="05723-218">To create a table</span></span>
1. <span data-ttu-id="05723-219">在 [Cloud Explorer] 中，選取儲存體帳戶的**資料表**節點，然後選擇 [建立資料表]。</span><span class="sxs-lookup"><span data-stu-id="05723-219">In Cloud Explorer, select the **Tables** node of the storage account, and then choose **Create Table**.</span></span>
2. <span data-ttu-id="05723-220">在 [建立資料表]  對話方塊中，輸入資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="05723-220">In the **Create Table** dialog box, enter a name for the table.</span></span>

### <a name="to-view-table-data"></a><span data-ttu-id="05723-221">檢視資料表資料</span><span class="sxs-lookup"><span data-stu-id="05723-221">To view table data</span></span>
1. <span data-ttu-id="05723-222">在 [Cloud Explorer] 中，開啟 **Azure** 節點，然後開啟**儲存體**節點。</span><span class="sxs-lookup"><span data-stu-id="05723-222">In Cloud Explorer, open the **Azure** node, and then open the **Storage** node.</span></span>
2. <span data-ttu-id="05723-223">開啟您有興趣的儲存體帳戶節點，然後開啟 **資料表** 節點以查看儲存體帳戶的資料表清單。</span><span class="sxs-lookup"><span data-stu-id="05723-223">Open the storage account node that you are interested in, and then open the **Tables** node to see a list of tables for the storage account.</span></span>
3. <span data-ttu-id="05723-224">開啟資料表的捷徑功能表，然後選擇 [檢視資料表] 。</span><span class="sxs-lookup"><span data-stu-id="05723-224">Open the shortcut menu for a table and then choose **View Table**.</span></span>
   
    ![方案總管中的 Azure 資料表](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

<span data-ttu-id="05723-226">資料表會根據實體 (顯示於資料列) 和屬性 (顯示於資料行) 加以組織。</span><span class="sxs-lookup"><span data-stu-id="05723-226">The table is organized by entities (shown in rows) and properties (shown in columns).</span></span> <span data-ttu-id="05723-227">例如，下圖顯示 **資料表設計工具**中所列的實體：</span><span class="sxs-lookup"><span data-stu-id="05723-227">For example, the following illustration shows entities listed in the **Table Designer**:</span></span>

### <a name="to-edit-table-data"></a><span data-ttu-id="05723-228">編輯資料表資料</span><span class="sxs-lookup"><span data-stu-id="05723-228">To edit table data</span></span>
1. <span data-ttu-id="05723-229">在**資料表設計工具**中，開啟實體 (單一資料列) 或屬性 (單一儲存格) 的捷徑功能表，然後選擇 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="05723-229">In the **Table Designer**, open the shortcut menu for an entity (a single row) or a property (a single cell) and then choose **Edit**.</span></span>
   
    ![新增或編輯資料表實體](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    <span data-ttu-id="05723-231">單一資料表中的實體不一定要有同一組屬性 (資料行)。</span><span class="sxs-lookup"><span data-stu-id="05723-231">Entities in a single table aren’t required to have the same set of properties (columns).</span></span> <span data-ttu-id="05723-232">請記住下列檢視和編輯資料表資料的限制。</span><span class="sxs-lookup"><span data-stu-id="05723-232">Keep in mind the following restrictions on viewing and editing table data.</span></span>
   
   * <span data-ttu-id="05723-233">您無法檢視或編輯二進位資料 (位元組類型)，但您可以將其儲存在資料表中。</span><span class="sxs-lookup"><span data-stu-id="05723-233">You can’t view or edit binary data (type byte[]), but you can store it in a table.</span></span>
   * <span data-ttu-id="05723-234">您無法編輯 **PartitionKey** 或 **RowKey** 值，因為 Azure 中的資料表儲存體不支援這項操作。</span><span class="sxs-lookup"><span data-stu-id="05723-234">You can’t edit the **PartitionKey** or **RowKey** values, because table storage in Azure doesn't support that operation.</span></span>
   * <span data-ttu-id="05723-235">您無法建立名為 Timestamp 的屬性，Azure 儲存體服務會使用該名稱的屬性。</span><span class="sxs-lookup"><span data-stu-id="05723-235">You can’t create a property called Timestamp, Azure Storage services use a property with that name.</span></span>
   * <span data-ttu-id="05723-236">如果您輸入日期時間值，您必須遵循適合您的電腦之區域和語言設定的格式 (例如，MM/DD/YYYY HH:MM:SS [AM|PM] 適用於美國英文)。</span><span class="sxs-lookup"><span data-stu-id="05723-236">If you enter a DateTime value, you must follow a format that's appropriate to the region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for U.S. English).</span></span>

### <a name="to-add-entities"></a><span data-ttu-id="05723-237">加入實體</span><span class="sxs-lookup"><span data-stu-id="05723-237">To add entities</span></span>
1. <span data-ttu-id="05723-238">在 [資料表設計工具] 中，選擇 [新增實體] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-238">In the **Table Designer**, choose the **Add Entity** button.</span></span>
   
    ![新增實體](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. <span data-ttu-id="05723-240">在 [新增實體] 對話方塊中，輸入 **PartitionKey** 和 **RowKey** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="05723-240">In the **Add Entity** dialog box, enter the values of the **PartitionKey** and **RowKey** properties.</span></span>
   
    ![新增實體對話方塊](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    <span data-ttu-id="05723-242">請小心輸入這些值，因為在您關閉對話方塊之後，您就無法變更這些值了，除非您刪除此實體並且再次將其加入。</span><span class="sxs-lookup"><span data-stu-id="05723-242">Enter the values carefully because you can't change them after you close the dialog box unless you delete the entity and add it again.</span></span>

### <a name="to-filter-entities"></a><span data-ttu-id="05723-243">篩選實體</span><span class="sxs-lookup"><span data-stu-id="05723-243">To filter entities</span></span>
<span data-ttu-id="05723-244">如果您使用查詢產生器，您就可以自訂會出現在資料表中的實體集。</span><span class="sxs-lookup"><span data-stu-id="05723-244">You can customize the set of entities that appear in a table if you use the query builder.</span></span>

1. <span data-ttu-id="05723-245">若要開啟查詢產生器，請開啟資料表進行檢視。</span><span class="sxs-lookup"><span data-stu-id="05723-245">To open the query builder, open a table for viewing.</span></span>
2. <span data-ttu-id="05723-246">選擇資料表檢視工具列上的 [查詢產生器] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-246">Choose the Query Builder button on the table view’s toolbar.</span></span>
   
    <span data-ttu-id="05723-247">[查詢產生器]  對話方塊會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="05723-247">The **Query Builder** dialog box appears.</span></span> <span data-ttu-id="05723-248">下圖顯示建置於查詢產生器中的查詢。</span><span class="sxs-lookup"><span data-stu-id="05723-248">The following illustration shows a query that's being built in the query builder.</span></span>
   
    ![查詢產生器](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. <span data-ttu-id="05723-250">當您完成查詢建置時，請關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="05723-250">When you’re done building the query, close the dialog box.</span></span> <span data-ttu-id="05723-251">產生的查詢文字格式會出現在文字方塊中做為 WCF Data Services 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="05723-251">The resulting text form of the query appears in a text box as a WCF Data Services filter.</span></span>
4. <span data-ttu-id="05723-252">若要執行查詢，請選擇綠色的三角形圖示。</span><span class="sxs-lookup"><span data-stu-id="05723-252">To run the query, choose the green triangle icon.</span></span>
   
    <span data-ttu-id="05723-253">如果您直接在篩選欄位中輸入 WCF Data Services 篩選字串，您也可以篩選出現在 **資料表設計工具** 中的實體資料。</span><span class="sxs-lookup"><span data-stu-id="05723-253">You can also filter entity data that appears in the **Table Designer** if you enter a WCF Data Services filter string directly in the filter field.</span></span> <span data-ttu-id="05723-254">這種類型的字串與 SQL WHERE 子句相似，但是會傳送至伺服器做為 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="05723-254">This kind of string is similar to a SQL WHERE clause but is sent to the server as an HTTP request.</span></span> <span data-ttu-id="05723-255">如需如何建構篩選字串的資訊，請參閱 [建構資料表設計工具的篩選字串](https://msdn.microsoft.com/library/azure/ff683669.aspx)。</span><span class="sxs-lookup"><span data-stu-id="05723-255">For information about how to construct filter strings, see [Constructing Filter Strings for the Table Designer](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>
   
    <span data-ttu-id="05723-256">下圖顯示有效篩選字串的範例：</span><span class="sxs-lookup"><span data-stu-id="05723-256">The following illustration shows an example of a valid filter string:</span></span>
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a><span data-ttu-id="05723-258">重新整理儲存體資料</span><span class="sxs-lookup"><span data-stu-id="05723-258">Refresh storage data</span></span>
<span data-ttu-id="05723-259">當 [伺服器總管] 連接到儲存體帳戶或從其取得資料時，它可能會佔用一分鐘的時間才能完成作業。</span><span class="sxs-lookup"><span data-stu-id="05723-259">When Server Explorer connects to or gets data from a storage account, it might take up to a minute for the operation to complete.</span></span> <span data-ttu-id="05723-260">如果無法連接，此作業可能會逾時。擷取資料時，您可以繼續在 Visual Studio 的其他部分中運作。</span><span class="sxs-lookup"><span data-stu-id="05723-260">If it can’t connect, the operation might time out. While data is retrieved, you can continue to work in other parts of Visual Studio.</span></span> <span data-ttu-id="05723-261">如果因為作業時間太長而要將其取消，請選擇 [伺服器總管] 工具列上的 [停止重新整理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-261">To cancel the operation if it’s taking too long, choose the **Stop Refresh** button on the Server Explorer toolbar.</span></span>

#### <a name="to-refresh-blob-container-data"></a><span data-ttu-id="05723-262">重新整理 blob 容器資料</span><span class="sxs-lookup"><span data-stu-id="05723-262">To refresh blob container data</span></span>
* <span data-ttu-id="05723-263">選取**儲存體**下的 **Blobs** 節點，並選擇 [伺服器總管] 工具列上的 [重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-263">Select the **Blobs** node beneath **Storage** and choose the **Refresh** button on the Server Explorer toolbar.</span></span>
* <span data-ttu-id="05723-264">若要重新整理顯示的 blob 清單，請選擇 [執行]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-264">To refresh the list of blobs that is displayed, choose the **Execute** button.</span></span>

#### <a name="to-refresh-table-data"></a><span data-ttu-id="05723-265">重新整理資料表資料</span><span class="sxs-lookup"><span data-stu-id="05723-265">To refresh table data</span></span>
* <span data-ttu-id="05723-266">選取**儲存體**下的**資料表**節點，並選擇 [重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-266">Select the **Tables** node beneath **Storage** and choose the **Refresh** button.</span></span>
* <span data-ttu-id="05723-267">若要重新整理**資料表設計工具**中所顯示的實體清單，請選擇**資料表設計工具**上的 [執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-267">To refresh the list of entities that is displayed in the **Table Designer**, choose the **Execute** button on the **Table Designer**.</span></span>

#### <a name="to-refresh-queue-data"></a><span data-ttu-id="05723-268">重新整理佇列資料</span><span class="sxs-lookup"><span data-stu-id="05723-268">To refresh queue data</span></span>
* <span data-ttu-id="05723-269">選取**佇列**節點，然後選擇 [重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-269">Select the **Queues** node, and then choose the **Refresh** button.</span></span>

#### <a name="to-refresh-all-items-in-a-storage-account"></a><span data-ttu-id="05723-270">重新整理儲存體帳戶中的所有項目</span><span class="sxs-lookup"><span data-stu-id="05723-270">To refresh all items in a storage account</span></span>
* <span data-ttu-id="05723-271">選擇帳戶名稱，然後選擇 [伺服器總管] 工具列上的 [重新整理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="05723-271">Choose the account name, and then choose the **Refresh** button on the toolbar for Server Explorer.</span></span>

### <a name="add-storage-accounts-by-using-server-explorer"></a><span data-ttu-id="05723-272">使用 [伺服器總管] 新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="05723-272">Add storage accounts by using Server Explorer</span></span>
<span data-ttu-id="05723-273">有兩種方式可以使用 [伺服器總管] 新增儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="05723-273">There are two ways to add storage accounts by using Server Explorer.</span></span> <span data-ttu-id="05723-274">您可以在您的 Azure 訂用帳戶中建立新的儲存體帳戶，或者您可以附加現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="05723-274">You can create a new storage account in your Azure subscription, or you can attach an existing storage account.</span></span>

#### <a name="to-create-a-new-storage-account-by-using-server-explorer"></a><span data-ttu-id="05723-275">使用伺服器總管建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="05723-275">To create a new storage account by using Server Explorer</span></span>
1. <span data-ttu-id="05723-276">在 [伺服器總管] 中，開啟儲存體節點的捷徑功能表，然後選擇 [建立儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="05723-276">In Server Explorer, open the shortcut menu for the Storage node, and then choose Create Storage Account.</span></span>
   
    ![建立新的 Azure 儲存體帳戶](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. <span data-ttu-id="05723-278">在 [建立儲存體帳戶]  對話方塊中選取或輸入新儲存體帳戶的下列資訊。</span><span class="sxs-lookup"><span data-stu-id="05723-278">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="05723-279">您要加入儲存體帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="05723-279">The Azure subscription to which you want to add the storage account.</span></span>
   * <span data-ttu-id="05723-280">您想要用於新儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="05723-280">The name you want to use for the new storage account.</span></span>
   * <span data-ttu-id="05723-281">區域或同質群組 (例如美國西部或東亞)。</span><span class="sxs-lookup"><span data-stu-id="05723-281">The region or affinity group (such as West US or East Asia).</span></span>
   * <span data-ttu-id="05723-282">您要用於儲存體帳戶的複寫類型，例如異地備援。</span><span class="sxs-lookup"><span data-stu-id="05723-282">The type of replication you want to use for the storage account, such as Geo-Redundant.</span></span>
3. <span data-ttu-id="05723-283">選擇 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="05723-283">Choose **Create**.</span></span>
   
    <span data-ttu-id="05723-284">新的儲存體帳戶會出現在 [方案總管] 中的 [儲存體]  清單。</span><span class="sxs-lookup"><span data-stu-id="05723-284">The new storage account appears in the **Storage** list in Solution Explorer.</span></span>

#### <a name="to-attach-an-existing-storage-account-by-using-server-explorer"></a><span data-ttu-id="05723-285">使用伺服器總管附加現有的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="05723-285">To attach an existing storage account by using Server Explorer</span></span>
1. <span data-ttu-id="05723-286">在 [伺服器總管] 中，開啟 Azure 儲存體節點的捷徑功能表，然後選擇 [附加外部儲存體] 。</span><span class="sxs-lookup"><span data-stu-id="05723-286">In Server Explorer, open the shortcut menu for the Azure storage node, and then choose **Attach External Storage**.</span></span>
   
    ![新增現有的儲存體帳戶](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. <span data-ttu-id="05723-288">在 [建立儲存體帳戶]  對話方塊中選取或輸入新儲存體帳戶的下列資訊。</span><span class="sxs-lookup"><span data-stu-id="05723-288">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="05723-289">您想要附加的現有儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="05723-289">The name of the existing storage account you want to attach.</span></span> <span data-ttu-id="05723-290">您可以輸入名稱或從清單中選取。</span><span class="sxs-lookup"><span data-stu-id="05723-290">You can enter a name or select it from the list.</span></span>
   * <span data-ttu-id="05723-291">選取之儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="05723-291">The key for the selected storage account.</span></span> <span data-ttu-id="05723-292">當您選取儲存體帳戶時，通常會提供這個值給您。</span><span class="sxs-lookup"><span data-stu-id="05723-292">This value is typically provided for you when you select a storage account.</span></span> <span data-ttu-id="05723-293">如果您想要 Visual Studio 記住儲存體帳戶金鑰，請選取 [記住帳戶金鑰] 方塊。</span><span class="sxs-lookup"><span data-stu-id="05723-293">If you want Visual Studio to remember the storage account key, select the Remember account key box.</span></span>
   * <span data-ttu-id="05723-294">要用於連接至儲存體帳戶的通訊協定，例如 HTTP、HTTPS 或自訂端點。</span><span class="sxs-lookup"><span data-stu-id="05723-294">The protocol to use to connect to the storage account, such as HTTP, HTTPS, or a custom endpoint.</span></span> <span data-ttu-id="05723-295">如需有關自訂端點的詳細資訊，請參閱 [如何設定連接字串](https://msdn.microsoft.com/library/azure/ee758697.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="05723-295">See [How to Configure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx) for more information about custom endpoints.</span></span>

### <a name="to-view-the-secondary-endpoints"></a><span data-ttu-id="05723-296">檢視次要端點</span><span class="sxs-lookup"><span data-stu-id="05723-296">To view the secondary endpoints</span></span>
* <span data-ttu-id="05723-297">如果您建立的儲存體帳戶使用 **讀取權限異地備援** 複寫選項，您可以檢視其次要端點。</span><span class="sxs-lookup"><span data-stu-id="05723-297">If you created a storage account using the **Read-Access Geo Redundant** replication option, you can view its secondary endpoints.</span></span> <span data-ttu-id="05723-298">開啟帳戶名稱的捷徑功能表，然後選擇 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="05723-298">Open the shortcut menu for the account name, and then choose **Properties**.</span></span>
  
    ![儲存體次要端點](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="to-remove-a-storage-account-from-server-explorer"></a><span data-ttu-id="05723-300">從伺服器總管移除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="05723-300">To remove a storage account from Server Explorer</span></span>
* <span data-ttu-id="05723-301">在 [伺服器總管] 中，開啟帳戶名稱的捷徑功能表，然後選擇 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="05723-301">In Server Explorer, open the shortcut menu for the account name, and then choose **Delete**.</span></span> <span data-ttu-id="05723-302">如果您刪除儲存體帳戶，也會移除該帳戶的所有已儲存金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="05723-302">If you delete a storage account, any saved key information for that account is also removed.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="05723-303">如果您從 [伺服器總管] 刪除儲存體帳戶，它並不會影響您的儲存體帳戶或其包含的任何資料，它只會從 [伺服器總管] 移除參考。</span><span class="sxs-lookup"><span data-stu-id="05723-303">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains; it simply removes the reference from Server Explorer.</span></span> <span data-ttu-id="05723-304">若要永久刪除儲存體帳戶，請使用 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="05723-304">To permanently delete a storage account, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
  > 
  > 

## <a name="next-steps"></a><span data-ttu-id="05723-305">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05723-305">Next steps</span></span>
<span data-ttu-id="05723-306">若要了解如何使用 Azure 儲存體服務的詳細資訊，請參閱 [存取 Azure 儲存體服務](https://msdn.microsoft.com/library/azure/ee405490.aspx)。</span><span class="sxs-lookup"><span data-stu-id="05723-306">To learn more about how use Azure storage services, see [Accessing the Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span></span>

