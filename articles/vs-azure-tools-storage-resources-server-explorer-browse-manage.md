---
title: "aaaBrowsing 和管理存放裝置資源，使用伺服器總管 |Microsoft 文件"
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
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a><span data-ttu-id="d469a-103">使用伺服器總管瀏覽和管理儲存體資源</span><span class="sxs-lookup"><span data-stu-id="d469a-103">Browsing and Managing Storage Resources with Server Explorer</span></span>
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a><span data-ttu-id="d469a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d469a-104">Overview</span></span>
<span data-ttu-id="d469a-105">如果您已安裝 hello Azure Tools for Microsoft Visual Studio，您可以檢視 blob、 佇列和資料表資料儲存體帳戶從 azure。</span><span class="sxs-lookup"><span data-stu-id="d469a-105">If you've installed hello Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span></span> <span data-ttu-id="d469a-106">在伺服器總管 中的 hello Azure 儲存體節點顯示您的本機儲存體模擬器帳戶和其他 Azure 儲存體帳戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="d469a-106">hello Azure Storage node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span></span>

<span data-ttu-id="d469a-107">tooview 在 Visual Studio 伺服器總管 hello 功能表列上，選擇**檢視**，**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="d469a-107">tooview Server Explorer in Visual Studio, on hello menu bar, choose **View**, **Server Explorer**.</span></span> <span data-ttu-id="d469a-108">hello 存放裝置 節點會顯示所有的 hello 存在每個 Azure 訂用帳戶/憑證您已經連接到下的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d469a-108">hello storage node shows all of hello storage accounts that exist under each Azure subscription/certificate you're connected to.</span></span> <span data-ttu-id="d469a-109">如果儲存體帳戶未出現，您可以將它加入 hello 指示[本主題稍後](#add-storage-accounts-by-using-server-explorer)。</span><span class="sxs-lookup"><span data-stu-id="d469a-109">If your storage account doesn't appear, you can add it by following hello instructions [later in this topic](#add-storage-accounts-by-using-server-explorer).</span></span>

<span data-ttu-id="d469a-110">您也可以從 Azure SDK 2.7 開始，使用新 Cloud Explorer tooview hello 和管理您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d469a-110">Starting in Azure SDK 2.7, you can also use hello new Cloud Explorer tooview and manage your Azure resources.</span></span> <span data-ttu-id="d469a-111">如需詳細資訊，請參閱 [使用雲端總管管理 Azure 資源](vs-azure-tools-resources-managing-with-cloud-explorer.md) 。</span><span class="sxs-lookup"><span data-stu-id="d469a-111">See [Managing Azure Resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) for more information.</span></span>

## <a name="view-and-manage-storage-resources-in-visual-studio"></a><span data-ttu-id="d469a-112">檢視和管理 Visual Studio 中的儲存體資源</span><span class="sxs-lookup"><span data-stu-id="d469a-112">View and manage storage resources in Visual Studio</span></span>
<span data-ttu-id="d469a-113">[伺服器總管] 會自動在您的儲存體模擬器帳戶中顯示 blob、佇列和資料表的清單。</span><span class="sxs-lookup"><span data-stu-id="d469a-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span></span> <span data-ttu-id="d469a-114">伺服器總管中列出 hello 儲存體模擬器帳戶下 hello 儲存節點做 hello**開發**節點。</span><span class="sxs-lookup"><span data-stu-id="d469a-114">hello storage emulator account is listed in Server Explorer under hello Storage node as hello **Development** node.</span></span>

<span data-ttu-id="d469a-115">toosee hello 儲存體模擬器帳戶的資源中，展開 hello**開發**節點。</span><span class="sxs-lookup"><span data-stu-id="d469a-115">toosee hello storage emulator account’s resources, expand hello **Development** node.</span></span> <span data-ttu-id="d469a-116">當您展開 hello 如果尚未開啟 hello 儲存體模擬器**開發** 節點，就會自動開始。</span><span class="sxs-lookup"><span data-stu-id="d469a-116">If hello storage emulator hasn’t been started when you expand hello **Development** node, it will automatically start.</span></span> <span data-ttu-id="d469a-117">這可能需要數秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d469a-117">This can take several seconds.</span></span> <span data-ttu-id="d469a-118">Hello 儲存體模擬器啟動時，您可以繼續 toowork Visual Studio 的其他區域中。</span><span class="sxs-lookup"><span data-stu-id="d469a-118">You can continue toowork in other areas of Visual Studio while hello storage emulator starts.</span></span>

<span data-ttu-id="d469a-119">tooview 資源儲存體帳戶中，展開 [伺服器總管] 中的 hello 儲存體帳戶的節點。</span><span class="sxs-lookup"><span data-stu-id="d469a-119">tooview resources in a storage account, expand hello storage account’s node in Server Explorer.</span></span> <span data-ttu-id="d469a-120">此時會出現下列子節點的 hello:</span><span class="sxs-lookup"><span data-stu-id="d469a-120">hello following sub-nodes appear:</span></span>

* <span data-ttu-id="d469a-121">Blob</span><span class="sxs-lookup"><span data-stu-id="d469a-121">Blobs</span></span>
* <span data-ttu-id="d469a-122">佇列</span><span class="sxs-lookup"><span data-stu-id="d469a-122">Queues</span></span>
* <span data-ttu-id="d469a-123">資料表</span><span class="sxs-lookup"><span data-stu-id="d469a-123">Tables</span></span>

## <a name="work-with-blob-resources"></a><span data-ttu-id="d469a-124">使用 Blob 資源</span><span class="sxs-lookup"><span data-stu-id="d469a-124">Work with Blob Resources</span></span>
<span data-ttu-id="d469a-125">hello Blob 節點顯示 hello 選取儲存體帳戶的容器清單。</span><span class="sxs-lookup"><span data-stu-id="d469a-125">hello Blobs node displays a list of containers for hello selected storage account.</span></span> <span data-ttu-id="d469a-126">Blob 容器包含 blob 檔案，您可以將這些 blob 組織成資料夾和子資料夾。</span><span class="sxs-lookup"><span data-stu-id="d469a-126">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span></span> <span data-ttu-id="d469a-127">請參閱[如何從.NET 的 Blob 儲存體 toouse](storage/blobs/storage-dotnet-how-to-use-blobs.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d469a-127">See [How toouse Blob Storage from .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information.</span></span>

### <a name="toocreate-a-blob-container"></a><span data-ttu-id="d469a-128">toocreate blob 容器</span><span class="sxs-lookup"><span data-stu-id="d469a-128">toocreate a blob container</span></span>
1. <span data-ttu-id="d469a-129">開啟 hello hello 的捷徑功能表**Blob** ] 節點，然後選擇 [**建立 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="d469a-129">Open hello shortcut menu for hello **Blobs** node, and then choose **Create Blob Container**.</span></span>
2. <span data-ttu-id="d469a-130">在 hello**建立 Blob 容器**對話方塊方塊中，輸入 hello hello 新容器名稱。</span><span class="sxs-lookup"><span data-stu-id="d469a-130">In hello **Create Blob Container** dialog box, enter hello name of hello new container.</span></span>  
3. <span data-ttu-id="d469a-131">按**ENTER**上鍵盤，或者您可以按一下或點選 hello 名稱欄位 toosave hello blob 容器之外。</span><span class="sxs-lookup"><span data-stu-id="d469a-131">Press **ENTER** on your keyboard or you can click or tap outside of hello name field toosave hello blob container.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d469a-132">hello blob 容器名稱必須以數字 (0-9) 或小寫字母 (a-z) 開頭。</span><span class="sxs-lookup"><span data-stu-id="d469a-132">hello blob container name must begin with a number (0-9) or lowercase letter (a-z).</span></span>
   > 
   > 

### <a name="toodelete-a-blob-container"></a><span data-ttu-id="d469a-133">toodelete blob 容器</span><span class="sxs-lookup"><span data-stu-id="d469a-133">toodelete a blob container</span></span>
* <span data-ttu-id="d469a-134">開啟 hello hello blob 容器，您想 tooremove，然後選擇捷徑功能表**刪除**。</span><span class="sxs-lookup"><span data-stu-id="d469a-134">Open hello shortcut menu for hello blob container you want tooremove and then choose **Delete**.</span></span>

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a><span data-ttu-id="d469a-135">toodisplay hello 項目清單所包含的 blob 容器中</span><span class="sxs-lookup"><span data-stu-id="d469a-135">toodisplay a list of hello items contained in a blob container</span></span>
* <span data-ttu-id="d469a-136">開啟 hello 清單中的 hello blob 容器名稱的捷徑功能表，然後選擇**開啟**。</span><span class="sxs-lookup"><span data-stu-id="d469a-136">Open hello shortcut menu for a blob container name in hello list and then choose **Open**.</span></span>
  
    <span data-ttu-id="d469a-137">當您檢視 blob 容器的 hello 內容時，它會出現稱為 hello blob 容器檢視的索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="d469a-137">When you view hello contents of a blob container, it appears in a tab known as hello blob container view.</span></span>
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    <span data-ttu-id="d469a-139">您可以執行下列 blob 上的作業使用 hello 按鈕 hello hello blob 容器檢視右上角中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d469a-139">You can perform hello following operations on blobs by using hello buttons in hello top-right corner of hello blob container view:</span></span>
  
  * <span data-ttu-id="d469a-140">輸入篩選值並加以套用</span><span class="sxs-lookup"><span data-stu-id="d469a-140">Enter a filter value and apply it</span></span>
  * <span data-ttu-id="d469a-141">重新整理 hello hello 容器中的 blob 清單</span><span class="sxs-lookup"><span data-stu-id="d469a-141">Refresh hello list of blobs in hello container</span></span>
  * <span data-ttu-id="d469a-142">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="d469a-142">Upload a file</span></span>
  * <span data-ttu-id="d469a-143">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="d469a-143">Delete a blob</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d469a-144">從 blob 容器中刪除檔案並不會刪除 hello 基礎檔案。它只會移除它從 hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="d469a-144">Deleting a file from a blob container doesn’t delete hello underlying file; it only removes it from hello blob container.</span></span>
    > 
    > 
  * <span data-ttu-id="d469a-145">開啟 blob</span><span class="sxs-lookup"><span data-stu-id="d469a-145">Open a blob</span></span>
  * <span data-ttu-id="d469a-146">儲存 blob toohello 本機電腦</span><span class="sxs-lookup"><span data-stu-id="d469a-146">Save a blob toohello local computer</span></span>

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a><span data-ttu-id="d469a-147">toocreate 資料夾或子資料夾中的 blob 容器</span><span class="sxs-lookup"><span data-stu-id="d469a-147">toocreate a folder or subfolder in a blob container</span></span>
1. <span data-ttu-id="d469a-148">選擇在 Cloud Explorer 中的 hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="d469a-148">Choose hello blob container in Cloud Explorer.</span></span> <span data-ttu-id="d469a-149">在 hello 容器視窗中，選擇 hello**上傳 Blob**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-149">In hello container window, choose hello **Upload Blob** button.</span></span>
   
    ![將檔案上傳至 blob 資料夾](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. <span data-ttu-id="d469a-151">在 hello**上傳新的檔案**對話方塊方塊中，選擇 hello**瀏覽**按鈕 toospecify hello 檔案您想 tooupload，，然後輸入 hello 中的 資料夾名稱**資料夾 （選擇性）**方塊.</span><span class="sxs-lookup"><span data-stu-id="d469a-151">In hello **Upload New File** dialog box, choose hello **Browse** button toospecify hello file you want tooupload, and then enter a folder name in hello **Folder (optional)** box.</span></span>
   
    <span data-ttu-id="d469a-152">您可以將遵循的容器資料夾中的子資料夾 hello 相同程序。</span><span class="sxs-lookup"><span data-stu-id="d469a-152">You can add subfolders in container folders by following hello same procedure.</span></span> <span data-ttu-id="d469a-153">如果您未指定資料夾名稱，將會 hello 檔案上傳 toohello hello blob 容器的頂部層級。</span><span class="sxs-lookup"><span data-stu-id="d469a-153">If you don’t specify a folder name, hello file will be uploaded toohello top level of hello blob container.</span></span> <span data-ttu-id="d469a-154">hello 檔案會出現在 hello hello 容器中指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d469a-154">hello file appears in hello specified folder in hello container.</span></span>
   
    ![資料夾加入 tooa blob 容器](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. <span data-ttu-id="d469a-156">按兩下 [hello] 資料夾，或按下 ENTER toosee hello 內容 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d469a-156">Double-click hello folder or press ENTER toosee hello contents of hello folder.</span></span> <span data-ttu-id="d469a-157">當您準備 hello 容器資料夾中時，您可以瀏覽的 hello 容器後 toohello 根選擇 hello**開啟上層目錄**（向上箭頭） 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-157">When you’re in hello container’s folder, you can navigate back toohello root of hello container by choosing hello **Open Parent Directory** (up arrow) button.</span></span>

### <a name="toodelete-a-container-folder"></a><span data-ttu-id="d469a-158">toodelete 容器資料夾</span><span class="sxs-lookup"><span data-stu-id="d469a-158">toodelete a container folder</span></span>
* <span data-ttu-id="d469a-159">刪除所有 hello 資料夾中的 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="d469a-159">Delete all of hello files in hello folder</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d469a-160">Blob 容器中的資料夾是虛擬資料夾，因為您無法建立空的資料夾，也可以刪除資料夾 toodelete 其檔案內容。</span><span class="sxs-lookup"><span data-stu-id="d469a-160">Because folders in blob containers are virtual folders, you can’t create an empty folder, nor can you delete a folder toodelete its file contents.</span></span> <span data-ttu-id="d469a-161">您有 toodelete hello 整個資料夾 toodelete hello 資料夾內容。</span><span class="sxs-lookup"><span data-stu-id="d469a-161">You have toodelete hello entire contents of a folder toodelete hello folder.</span></span>
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a><span data-ttu-id="d469a-162">toofilter blob 容器中</span><span class="sxs-lookup"><span data-stu-id="d469a-162">toofilter blobs in a container</span></span>
<span data-ttu-id="d469a-163">您可以篩選會顯示藉由指定通用的前置詞的 hello blob。</span><span class="sxs-lookup"><span data-stu-id="d469a-163">You can filter hello blobs that are displayed by specifying a common prefix.</span></span>

<span data-ttu-id="d469a-164">例如，如果您輸入 hello 前置詞`hello`在 hello 篩選] 文字方塊，然後選擇 [hello **Execute** (**！**)按鈕，以 'hello' 開頭的 blob 會出現。</span><span class="sxs-lookup"><span data-stu-id="d469a-164">For example, if you enter hello prefix `hello` in hello filter text box and then choose hello **Execute** (**!**)button, only blobs that begin with 'hello' appear.</span></span>

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> <span data-ttu-id="d469a-166">hello 篩選欄位會區分大小寫，且不支援使用萬用字元進行篩選。</span><span class="sxs-lookup"><span data-stu-id="d469a-166">hello filter field is case-sensitive and doesn’t support filtering with wildcard characters.</span></span> <span data-ttu-id="d469a-167">Blob 只可以利用前置詞篩選。</span><span class="sxs-lookup"><span data-stu-id="d469a-167">Blobs can only be filtered by prefix.</span></span> <span data-ttu-id="d469a-168">如果您使用分隔符號 tooorganize blob 以虛擬階層 hello 前置詞可能包含分隔符號。</span><span class="sxs-lookup"><span data-stu-id="d469a-168">hello prefix may include a delimiter if you are using a delimiter tooorganize blobs in a virtual hierarchy.</span></span> <span data-ttu-id="d469a-169">例如，篩選 hello 前置詞 HelloFabric/會傳回所有以該字串開頭的 blob。</span><span class="sxs-lookup"><span data-stu-id="d469a-169">For example, filtering on hello prefix HelloFabric/ returns all blobs beginning with that string.</span></span>
> 
> 

### <a name="toodownload-blob-data"></a><span data-ttu-id="d469a-170">toodownload blob 資料</span><span class="sxs-lookup"><span data-stu-id="d469a-170">toodownload blob data</span></span>
* <span data-ttu-id="d469a-171">在**Cloud Explorer**，開啟一個或多個 blob 的 hello 捷徑功能表，然後選擇**開啟**，或選擇 hello blob 名稱，然後選擇 hello**開啟**按鈕，或按兩下hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="d469a-171">In **Cloud Explorer**, open hello shortcut menu for one or more blobs and then choose **Open**, or choose hello blob name and then choose hello **Open** button, or double-click hello blob name.</span></span>
  
    <span data-ttu-id="d469a-172">hello blob 下載進度會顯示在 hello **Azure 活動記錄檔**視窗。</span><span class="sxs-lookup"><span data-stu-id="d469a-172">hello progress of a blob download appears in hello **Azure Activity Log** window.</span></span>
  
    <span data-ttu-id="d469a-173">hello blob 會在 hello 該檔案類型的預設編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="d469a-173">hello blob opens in hello default editor for that file type.</span></span> <span data-ttu-id="d469a-174">Hello 作業系統辨識出 hello 檔案類型，若 hello 檔案會開啟在本機安裝的應用程式。否則，系統會提示您 toochoose 適合 hello blob hello 檔案類型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d469a-174">If hello operating system recognizes hello file type, hello file opens in a locally installed application; otherwise, you're prompted toochoose an application that’s appropriate for hello file type of hello blob.</span></span> <span data-ttu-id="d469a-175">hello 下載 blob 時所建立的本機檔案會標示為唯讀。</span><span class="sxs-lookup"><span data-stu-id="d469a-175">hello local file that’s created when you download a blob is marked as read-only.</span></span>
  
    <span data-ttu-id="d469a-176">Blob 資料是在本機快取和 blob 的上次修改的時間 hello Blob 服務在經過 hello。</span><span class="sxs-lookup"><span data-stu-id="d469a-176">Blob data is cached locally and checked against hello blob's last modified time in hello Blob service.</span></span> <span data-ttu-id="d469a-177">如果 hello blob 已更新上次下載之後，它將會再次下載。否則，會從 hello 本機磁碟載入 hello blob。</span><span class="sxs-lookup"><span data-stu-id="d469a-177">If hello blob has been updated since it was last downloaded, it will be downloaded again; otherwise, hello blob will be loaded from hello local disk.</span></span> <span data-ttu-id="d469a-178">根據預設，blob 是下載的 tooa 暫存目錄。</span><span class="sxs-lookup"><span data-stu-id="d469a-178">By default, a blob is downloaded tooa temporary directory.</span></span> <span data-ttu-id="d469a-179">blob 名稱 toodownload blob tooa 特定目錄中，開啟 hello hello 選取捷徑功能表，然後選擇 **存**。</span><span class="sxs-lookup"><span data-stu-id="d469a-179">toodownload blobs tooa specific directory, open hello shortcut menu for hello selected blob names and choose **Save As**.</span></span> <span data-ttu-id="d469a-180">當您以這種方式儲存 blob 時，hello blob 檔案尚未開啟，並建立 hello 本機檔案具有讀寫屬性。</span><span class="sxs-lookup"><span data-stu-id="d469a-180">When you save a blob in this manner, hello blob file is not opened, and hello local file is created with read-write attributes.</span></span>

### <a name="tooupload-blobs"></a><span data-ttu-id="d469a-181">tooupload blob</span><span class="sxs-lookup"><span data-stu-id="d469a-181">tooupload blobs</span></span>
* <span data-ttu-id="d469a-182">選擇 hello**上傳 Blob**按鈕 hello 容器開啟以供在 hello blob 容器檢視中檢視時。</span><span class="sxs-lookup"><span data-stu-id="d469a-182">Choose hello **Upload Blob** button when hello container is open for viewing in hello blob container view.</span></span>
  
    <span data-ttu-id="d469a-183">您可以選擇其中一個或多個檔案 tooupload，而且您可以上傳任何類型的檔案。</span><span class="sxs-lookup"><span data-stu-id="d469a-183">You can choose one or more files tooupload and you can upload files of any type.</span></span> <span data-ttu-id="d469a-184">hello **Azure 活動記錄檔**顯示 hello 的 hello 上傳進度。</span><span class="sxs-lookup"><span data-stu-id="d469a-184">hello **Azure Activity Log** shows hello progress of hello upload.</span></span> <span data-ttu-id="d469a-185">如需有關如何 toowork blob 資料，請參閱[toouse hello.net 的 Azure Blob 儲存體服務的方式](http://go.microsoft.com/fwlink/p/?LinkId=267911)。</span><span class="sxs-lookup"><span data-stu-id="d469a-185">For more information about how toowork with blob data, see [How toouse hello Azure Blob Storage Service in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span></span>

### <a name="tooview-logs-transferred-tooblobs"></a><span data-ttu-id="d469a-186">傳輸 tooblobs tooview 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d469a-186">tooview logs transferred tooblobs</span></span>
* <span data-ttu-id="d469a-187">如果您從 Azure 應用程式使用 Azure 診斷 toolog 資料，並且已傳輸記錄檔 tooyour 儲存體帳戶，您會看到由 Azure 為這些記錄建立的容器。</span><span class="sxs-lookup"><span data-stu-id="d469a-187">If you are using Azure Diagnostics toolog data from your Azure application and you have transferred logs tooyour storage account, you’ll see containers that were created by Azure for these logs.</span></span> <span data-ttu-id="d469a-188">在伺服器總管中檢視這些記錄檔是您的應用程式輕鬆 tooidentify 問題，特別是當它已部署的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d469a-188">Viewing these logs in Server Explorer is an easy way tooidentify problems with your application, especially if it’s been deployed tooAzure.</span></span> <span data-ttu-id="d469a-189">如需 Azure 診斷的詳細資訊，請參閱 [使用 Azure 診斷收集記錄資料](https://msdn.microsoft.com/library/azure/gg433048.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d469a-189">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span></span>

### <a name="tooget-hello-url-for-a-blob"></a><span data-ttu-id="d469a-190">blob 的 tooget hello URL</span><span class="sxs-lookup"><span data-stu-id="d469a-190">tooget hello URL for a blob</span></span>
* <span data-ttu-id="d469a-191">開啟 hello blob 的捷徑功能表，然後選擇**複製 URL**。</span><span class="sxs-lookup"><span data-stu-id="d469a-191">Open hello blob’s shortcut menu and then choose **Copy URL**.</span></span>

### <a name="tooedit-a-blob"></a><span data-ttu-id="d469a-192">tooedit blob</span><span class="sxs-lookup"><span data-stu-id="d469a-192">tooedit a blob</span></span>
* <span data-ttu-id="d469a-193">選取 hello blob，然後選擇 [hello**開啟 Blob** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-193">Select hello blob and then choose hello **Open Blob** button.</span></span>
  
    <span data-ttu-id="d469a-194">hello 檔案下載的 tooa 暫存位置，並開啟 hello 本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="d469a-194">hello file is downloaded tooa temporary location and opened on hello local computer.</span></span> <span data-ttu-id="d469a-195">您必須再次上傳 hello blob 進行變更之後。</span><span class="sxs-lookup"><span data-stu-id="d469a-195">You must upload hello blob again after you make changes.</span></span>

## <a name="work-with-queue-resources"></a><span data-ttu-id="d469a-196">使用佇列資源</span><span class="sxs-lookup"><span data-stu-id="d469a-196">Work with Queue Resources</span></span>
<span data-ttu-id="d469a-197">儲存體服務佇列裝載於 Azure 儲存體帳戶，您可以使用這些 tooallow 您雲端服務的角色有 toocommunicate 與彼此、 與其他服務的訊息傳遞機制。</span><span class="sxs-lookup"><span data-stu-id="d469a-197">Storage services queues are hosted in an Azure storage account and you can use them tooallow your cloud service roles toocommunicate with each other and with other services by a message passing mechanism.</span></span> <span data-ttu-id="d469a-198">您可以透過雲端服務，並透過外部用戶端的 web 服務以程式設計方式存取 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="d469a-198">You can access hello queue programmatically through a cloud service and over a web service for external clients.</span></span> <span data-ttu-id="d469a-199">您也可以使用 Visual Studio 中的伺服器總管 來直接存取 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="d469a-199">You can also access hello queue directly by using Server Explorer in Visual Studio.</span></span>

<span data-ttu-id="d469a-200">當您開發使用佇列的雲端服務時，您可能會想 toouse Visual Studio toocreate 佇列，並使用它們以互動方式在您開發並測試您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d469a-200">When you develop a cloud service that uses queues, you might want toouse Visual Studio toocreate queues and work with them interactively while you develop and test your code.</span></span>

<span data-ttu-id="d469a-201">在伺服器總管 中，您可以檢視儲存體帳戶中的 hello 佇列、 建立和刪除佇列、 開啟佇列 tooview 其訊息，並加入訊息 tooa 佇列。</span><span class="sxs-lookup"><span data-stu-id="d469a-201">In Server Explorer, you can view hello queues in a storage account, create and delete queues, open a queue tooview its messages, and add messages tooa queue.</span></span> <span data-ttu-id="d469a-202">當您開啟佇列進行檢視時，您可以檢視個別的 hello 訊息，以及您可以執行下列動作 hello 佇列上，使用 hello 按鈕 hello 左上角中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d469a-202">When you open a queue for viewing, you can view hello individual messages, and you can perform hello following actions on hello queue by using hello buttons in hello top-left corner:</span></span>

* <span data-ttu-id="d469a-203">重新整理 hello 佇列的 hello 檢視</span><span class="sxs-lookup"><span data-stu-id="d469a-203">Refresh hello view of hello queue</span></span>
* <span data-ttu-id="d469a-204">新增訊息 toohello 佇列</span><span class="sxs-lookup"><span data-stu-id="d469a-204">Add a message toohello queue</span></span>
* <span data-ttu-id="d469a-205">清除佇列 hello 最上層訊息</span><span class="sxs-lookup"><span data-stu-id="d469a-205">Dequeue hello topmost message</span></span>
* <span data-ttu-id="d469a-206">清除 hello 整個佇列</span><span class="sxs-lookup"><span data-stu-id="d469a-206">Clear hello entire queue</span></span>

<span data-ttu-id="d469a-207">hello 下列影像顯示包含兩個訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="d469a-207">hello following image shows a queue that contains two messages.</span></span>

![檢視佇列](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

<span data-ttu-id="d469a-209">如需有關儲存體服務佇列，請參閱[How to： 使用 hello 佇列儲存體服務](http://go.microsoft.com/fwlink/?LinkID=264702)。</span><span class="sxs-lookup"><span data-stu-id="d469a-209">For more information about storage services queues, see [How to: Use hello Queue Storage Service](http://go.microsoft.com/fwlink/?LinkID=264702).</span></span> <span data-ttu-id="d469a-210">如需 hello web 服務的儲存體服務佇列，請參閱[佇列服務概念](http://go.microsoft.com/fwlink/?LinkId=264788)。</span><span class="sxs-lookup"><span data-stu-id="d469a-210">For information about hello web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span></span> <span data-ttu-id="d469a-211">如需 toosend 訊息 tooa 儲存體服務佇列使用 Visual Studio 的如何資訊，請參閱[傳送訊息 tooa 儲存體服務佇列](https://msdn.microsoft.com/library/azure/jj649344.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d469a-211">For information about how toosend messages tooa storage services queue by using Visual Studio, see [Sending Messages tooa Storage Services Queue](https://msdn.microsoft.com/library/azure/jj649344.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d469a-212">儲存體服務佇列與服務匯流排佇列不同。</span><span class="sxs-lookup"><span data-stu-id="d469a-212">Storage services queues are distinct from service bus queues.</span></span> <span data-ttu-id="d469a-213">如需服務匯流排佇列的詳細資訊，請參閱服務匯流排佇列、主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d469a-213">For more information about service bus queues, see Service Bus Queues, Topics, and Subscriptions.</span></span>
> 
> 

## <a name="work-with-table-resources"></a><span data-ttu-id="d469a-214">使用資料表資源</span><span class="sxs-lookup"><span data-stu-id="d469a-214">Work with Table Resources</span></span>
<span data-ttu-id="d469a-215">hello Azure 資料表儲存體服務儲存大量結構化資料。</span><span class="sxs-lookup"><span data-stu-id="d469a-215">hello Azure Table storage service stores large amounts of structured data.</span></span> <span data-ttu-id="d469a-216">hello 服務是可接受的 NoSQL 資料存放區驗證呼叫從內部和外部 hello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="d469a-216">hello service is a NoSQL datastore which accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="d469a-217">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="d469a-217">Azure tables are ideal for storing structured, non-relational data.</span></span>

### <a name="toocreate-a-table"></a><span data-ttu-id="d469a-218">toocreate 資料表</span><span class="sxs-lookup"><span data-stu-id="d469a-218">toocreate a table</span></span>
1. <span data-ttu-id="d469a-219">在 Cloud Explorer 中選取 hello**資料表**節點 hello 儲存體帳戶，，然後選擇  **Create Table**。</span><span class="sxs-lookup"><span data-stu-id="d469a-219">In Cloud Explorer, select hello **Tables** node of hello storage account, and then choose **Create Table**.</span></span>
2. <span data-ttu-id="d469a-220">在 hello **Create Table**對話方塊方塊中，輸入 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="d469a-220">In hello **Create Table** dialog box, enter a name for hello table.</span></span>

### <a name="tooview-table-data"></a><span data-ttu-id="d469a-221">tooview 資料表資料</span><span class="sxs-lookup"><span data-stu-id="d469a-221">tooview table data</span></span>
1. <span data-ttu-id="d469a-222">在 Cloud Explorer 中開啟 hello **Azure**節點，然後再開啟 hello**儲存體**節點。</span><span class="sxs-lookup"><span data-stu-id="d469a-222">In Cloud Explorer, open hello **Azure** node, and then open hello **Storage** node.</span></span>
2. <span data-ttu-id="d469a-223">開啟 hello 的儲存體帳戶節點您感興趣，，，然後開啟 hello**資料表**節點 toosee hello 儲存體帳戶的表格清單。</span><span class="sxs-lookup"><span data-stu-id="d469a-223">Open hello storage account node that you are interested in, and then open hello **Tables** node toosee a list of tables for hello storage account.</span></span>
3. <span data-ttu-id="d469a-224">開啟 hello 資料表的捷徑功能表，然後選擇**檢視資料表**。</span><span class="sxs-lookup"><span data-stu-id="d469a-224">Open hello shortcut menu for a table and then choose **View Table**.</span></span>
   
    ![方案總管中的 Azure 資料表](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

<span data-ttu-id="d469a-226">hello 表格被依照 （顯示為資料列） 的實體和屬性 （資料行中顯示）。</span><span class="sxs-lookup"><span data-stu-id="d469a-226">hello table is organized by entities (shown in rows) and properties (shown in columns).</span></span> <span data-ttu-id="d469a-227">例如，下列圖例 hello 顯示 hello 中列出實體**資料表設計工具**:</span><span class="sxs-lookup"><span data-stu-id="d469a-227">For example, hello following illustration shows entities listed in hello **Table Designer**:</span></span>

### <a name="tooedit-table-data"></a><span data-ttu-id="d469a-228">tooedit 資料表資料</span><span class="sxs-lookup"><span data-stu-id="d469a-228">tooedit table data</span></span>
1. <span data-ttu-id="d469a-229">在 hello**資料表設計工具**，開啟 hello 實體 （單一資料列） 或屬性 （單一儲存格） 的捷徑功能表，然後選擇**編輯**。</span><span class="sxs-lookup"><span data-stu-id="d469a-229">In hello **Table Designer**, open hello shortcut menu for an entity (a single row) or a property (a single cell) and then choose **Edit**.</span></span>
   
    ![新增或編輯資料表實體](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    <span data-ttu-id="d469a-231">單一資料表中的實體不是必要的 toohave hello 相同設定的屬性 （資料行）。</span><span class="sxs-lookup"><span data-stu-id="d469a-231">Entities in a single table aren’t required toohave hello same set of properties (columns).</span></span> <span data-ttu-id="d469a-232">請注意 hello 遵循上檢視及編輯資料表資料的限制。</span><span class="sxs-lookup"><span data-stu-id="d469a-232">Keep in mind hello following restrictions on viewing and editing table data.</span></span>
   
   * <span data-ttu-id="d469a-233">您無法檢視或編輯二進位資料 (位元組類型)，但您可以將其儲存在資料表中。</span><span class="sxs-lookup"><span data-stu-id="d469a-233">You can’t view or edit binary data (type byte[]), but you can store it in a table.</span></span>
   * <span data-ttu-id="d469a-234">您無法編輯 hello **PartitionKey**或**RowKey**值，因為在 Azure 中的資料表儲存體不支援這項操作。</span><span class="sxs-lookup"><span data-stu-id="d469a-234">You can’t edit hello **PartitionKey** or **RowKey** values, because table storage in Azure doesn't support that operation.</span></span>
   * <span data-ttu-id="d469a-235">您無法建立名為 Timestamp 的屬性，Azure 儲存體服務會使用該名稱的屬性。</span><span class="sxs-lookup"><span data-stu-id="d469a-235">You can’t create a property called Timestamp, Azure Storage services use a property with that name.</span></span>
   * <span data-ttu-id="d469a-236">如果您輸入的日期時間值，您必須依照您的電腦的適當 toohello 地區和語言設定的格式 (例如，MM/DD/YYYY hh: mm: [AM |PM] 美國地區英文)。</span><span class="sxs-lookup"><span data-stu-id="d469a-236">If you enter a DateTime value, you must follow a format that's appropriate toohello region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for U.S. English).</span></span>

### <a name="tooadd-entities"></a><span data-ttu-id="d469a-237">tooadd 實體</span><span class="sxs-lookup"><span data-stu-id="d469a-237">tooadd entities</span></span>
1. <span data-ttu-id="d469a-238">在 [hello**資料表設計工具**，選擇 hello**加入實體**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-238">In hello **Table Designer**, choose hello **Add Entity** button.</span></span>
   
    ![新增實體](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. <span data-ttu-id="d469a-240">在 hello**加入實體**對話方塊方塊中，輸入 hello hello 值**PartitionKey**和**RowKey**屬性。</span><span class="sxs-lookup"><span data-stu-id="d469a-240">In hello **Add Entity** dialog box, enter hello values of hello **PartitionKey** and **RowKey** properties.</span></span>
   
    ![新增實體對話方塊](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    <span data-ttu-id="d469a-242">請仔細輸入 hello 值，因為您無法在關閉 hello 對話方塊中，除非您刪除 hello 實體，並將它重新加入之後變更它們。</span><span class="sxs-lookup"><span data-stu-id="d469a-242">Enter hello values carefully because you can't change them after you close hello dialog box unless you delete hello entity and add it again.</span></span>

### <a name="toofilter-entities"></a><span data-ttu-id="d469a-243">toofilter 實體</span><span class="sxs-lookup"><span data-stu-id="d469a-243">toofilter entities</span></span>
<span data-ttu-id="d469a-244">您可以自訂 hello 出現在資料表中，如果您使用 hello 查詢產生器的實體集。</span><span class="sxs-lookup"><span data-stu-id="d469a-244">You can customize hello set of entities that appear in a table if you use hello query builder.</span></span>

1. <span data-ttu-id="d469a-245">tooopen hello 查詢產生器中，開啟任一表格進行檢視。</span><span class="sxs-lookup"><span data-stu-id="d469a-245">tooopen hello query builder, open a table for viewing.</span></span>
2. <span data-ttu-id="d469a-246">選擇 hello hello 資料表檢視的工具列上的查詢產生器 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-246">Choose hello Query Builder button on hello table view’s toolbar.</span></span>
   
    <span data-ttu-id="d469a-247">hello**查詢產生器** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="d469a-247">hello **Query Builder** dialog box appears.</span></span> <span data-ttu-id="d469a-248">hello 如下圖所顯示的查詢正在建立 hello 查詢產生器中。</span><span class="sxs-lookup"><span data-stu-id="d469a-248">hello following illustration shows a query that's being built in hello query builder.</span></span>
   
    ![查詢產生器](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. <span data-ttu-id="d469a-250">當您完成建立 hello 查詢，關閉 [hello] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d469a-250">When you’re done building hello query, close hello dialog box.</span></span> <span data-ttu-id="d469a-251">hello 產生的文字格式的 hello 查詢會顯示在文字方塊中，為 WCF Data Services 篩選器。</span><span class="sxs-lookup"><span data-stu-id="d469a-251">hello resulting text form of hello query appears in a text box as a WCF Data Services filter.</span></span>
4. <span data-ttu-id="d469a-252">toorun hello 查詢中，選擇 hello 綠色的三角形圖示。</span><span class="sxs-lookup"><span data-stu-id="d469a-252">toorun hello query, choose hello green triangle icon.</span></span>
   
    <span data-ttu-id="d469a-253">您也可以篩選出現在 hello 中的實體資料**資料表設計工具**如果您直接在 hello 篩選欄位中輸入 WCF Data Services 篩選條件字串。</span><span class="sxs-lookup"><span data-stu-id="d469a-253">You can also filter entity data that appears in hello **Table Designer** if you enter a WCF Data Services filter string directly in hello filter field.</span></span> <span data-ttu-id="d469a-254">這類字串類似 tooa SQL WHERE 子句，但會以 HTTP 要求傳送 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d469a-254">This kind of string is similar tooa SQL WHERE clause but is sent toohello server as an HTTP request.</span></span> <span data-ttu-id="d469a-255">如需如何 tooconstruct 篩選字串資訊，請參閱[hello 資料表設計工具建構篩選字串](https://msdn.microsoft.com/library/azure/ff683669.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d469a-255">For information about how tooconstruct filter strings, see [Constructing Filter Strings for hello Table Designer](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>
   
    <span data-ttu-id="d469a-256">hello 下圖顯示有效的篩選字串的範例：</span><span class="sxs-lookup"><span data-stu-id="d469a-256">hello following illustration shows an example of a valid filter string:</span></span>
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a><span data-ttu-id="d469a-258">重新整理儲存體資料</span><span class="sxs-lookup"><span data-stu-id="d469a-258">Refresh storage data</span></span>
<span data-ttu-id="d469a-259">當伺服器總管 連接 tooor 取得資料時從儲存體帳戶時，就可能會在 hello 作業 toocomplete tooa 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d469a-259">When Server Explorer connects tooor gets data from a storage account, it might take up tooa minute for hello operation toocomplete.</span></span> <span data-ttu-id="d469a-260">如果它無法連接，hello 作業可能會逾時。擷取資料時，您可以繼續在 Visual Studio 的其他部分 toowork。</span><span class="sxs-lookup"><span data-stu-id="d469a-260">If it can’t connect, hello operation might time out. While data is retrieved, you can continue toowork in other parts of Visual Studio.</span></span> <span data-ttu-id="d469a-261">如果費時太久，toocancel hello 作業選擇 hello**停止重新整理**hello 伺服器總管 工具列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-261">toocancel hello operation if it’s taking too long, choose hello **Stop Refresh** button on hello Server Explorer toolbar.</span></span>

#### <a name="toorefresh-blob-container-data"></a><span data-ttu-id="d469a-262">toorefresh blob 容器資料</span><span class="sxs-lookup"><span data-stu-id="d469a-262">toorefresh blob container data</span></span>
* <span data-ttu-id="d469a-263">選取 hello **Blob**下方的節點**儲存體**選擇 hello**重新整理**hello 伺服器總管 工具列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-263">Select hello **Blobs** node beneath **Storage** and choose hello **Refresh** button on hello Server Explorer toolbar.</span></span>
* <span data-ttu-id="d469a-264">toorefresh hello 的 blob 清單，會顯示選擇 hello **Execute**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-264">toorefresh hello list of blobs that is displayed, choose hello **Execute** button.</span></span>

#### <a name="toorefresh-table-data"></a><span data-ttu-id="d469a-265">toorefresh 資料表資料</span><span class="sxs-lookup"><span data-stu-id="d469a-265">toorefresh table data</span></span>
* <span data-ttu-id="d469a-266">選取 hello**資料表**下方的節點**儲存體**選擇 hello**重新整理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-266">Select hello **Tables** node beneath **Storage** and choose hello **Refresh** button.</span></span>
* <span data-ttu-id="d469a-267">實體的 toorefresh hello 清單，會顯示在 hello**資料表設計工具**，選擇 hello **Execute**按鈕 hello**資料表設計工具**。</span><span class="sxs-lookup"><span data-stu-id="d469a-267">toorefresh hello list of entities that is displayed in hello **Table Designer**, choose hello **Execute** button on hello **Table Designer**.</span></span>

#### <a name="toorefresh-queue-data"></a><span data-ttu-id="d469a-268">toorefresh 佇列資料</span><span class="sxs-lookup"><span data-stu-id="d469a-268">toorefresh queue data</span></span>
* <span data-ttu-id="d469a-269">選取 hello**佇列** 節點，然後選擇 hello**重新整理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-269">Select hello **Queues** node, and then choose hello **Refresh** button.</span></span>

#### <a name="toorefresh-all-items-in-a-storage-account"></a><span data-ttu-id="d469a-270">toorefresh 儲存體帳戶中的所有項目</span><span class="sxs-lookup"><span data-stu-id="d469a-270">toorefresh all items in a storage account</span></span>
* <span data-ttu-id="d469a-271">選擇 hello 帳戶名稱，然後選擇 [hello**重新整理**hello 工具列上的伺服器總管] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d469a-271">Choose hello account name, and then choose hello **Refresh** button on hello toolbar for Server Explorer.</span></span>

### <a name="add-storage-accounts-by-using-server-explorer"></a><span data-ttu-id="d469a-272">使用 [伺服器總管] 新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d469a-272">Add storage accounts by using Server Explorer</span></span>
<span data-ttu-id="d469a-273">有兩種方式 tooadd 儲存體帳戶使用 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="d469a-273">There are two ways tooadd storage accounts by using Server Explorer.</span></span> <span data-ttu-id="d469a-274">您可以在您的 Azure 訂用帳戶中建立新的儲存體帳戶，或者您可以附加現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d469a-274">You can create a new storage account in your Azure subscription, or you can attach an existing storage account.</span></span>

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a><span data-ttu-id="d469a-275">toocreate 新的儲存體帳戶，使用伺服器總管</span><span class="sxs-lookup"><span data-stu-id="d469a-275">toocreate a new storage account by using Server Explorer</span></span>
1. <span data-ttu-id="d469a-276">在伺服器總管 中，開啟 hello hello 存放裝置 節點的捷徑功能表，然後選擇建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d469a-276">In Server Explorer, open hello shortcut menu for hello Storage node, and then choose Create Storage Account.</span></span>
   
    ![建立新的 Azure 儲存體帳戶](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. <span data-ttu-id="d469a-278">選取或輸入下列資訊在 hello hello 新儲存體帳戶的 hello**建立儲存體帳戶** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d469a-278">Select or enter hello following information for hello new storage account in hello **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="d469a-279">hello Azure 訂用帳戶 toowhich 想 tooadd hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d469a-279">hello Azure subscription toowhich you want tooadd hello storage account.</span></span>
   * <span data-ttu-id="d469a-280">您要新增儲存體帳戶 hello toouse hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d469a-280">hello name you want toouse for hello new storage account.</span></span>
   * <span data-ttu-id="d469a-281">hello 地區或同質群組 （例如美國西部或東亞）。</span><span class="sxs-lookup"><span data-stu-id="d469a-281">hello region or affinity group (such as West US or East Asia).</span></span>
   * <span data-ttu-id="d469a-282">hello 類型的複寫想 toouse hello 儲存體帳戶，例如 異地備援。</span><span class="sxs-lookup"><span data-stu-id="d469a-282">hello type of replication you want toouse for hello storage account, such as Geo-Redundant.</span></span>
3. <span data-ttu-id="d469a-283">選擇 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d469a-283">Choose **Create**.</span></span>
   
    <span data-ttu-id="d469a-284">hello 新儲存體帳戶會出現在 hello**儲存體**方案總管 中的清單。</span><span class="sxs-lookup"><span data-stu-id="d469a-284">hello new storage account appears in hello **Storage** list in Solution Explorer.</span></span>

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a><span data-ttu-id="d469a-285">tooattach 現有的儲存體帳戶使用伺服器總管</span><span class="sxs-lookup"><span data-stu-id="d469a-285">tooattach an existing storage account by using Server Explorer</span></span>
1. <span data-ttu-id="d469a-286">在 [伺服器總管] 中，開啟 hello hello Azure 儲存體] 節點的捷徑功能表，然後選擇 [**附加外部儲存體**。</span><span class="sxs-lookup"><span data-stu-id="d469a-286">In Server Explorer, open hello shortcut menu for hello Azure storage node, and then choose **Attach External Storage**.</span></span>
   
    ![新增現有的儲存體帳戶](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. <span data-ttu-id="d469a-288">選取或輸入下列資訊在 hello hello 新儲存體帳戶的 hello**建立儲存體帳戶** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d469a-288">Select or enter hello following information for hello new storage account in hello **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="d469a-289">hello hello 想 tooattach 現有儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d469a-289">hello name of hello existing storage account you want tooattach.</span></span> <span data-ttu-id="d469a-290">您可以輸入的名稱，或從 hello 清單中選取。</span><span class="sxs-lookup"><span data-stu-id="d469a-290">You can enter a name or select it from hello list.</span></span>
   * <span data-ttu-id="d469a-291">hello hello 索引鍵選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d469a-291">hello key for hello selected storage account.</span></span> <span data-ttu-id="d469a-292">當您選取儲存體帳戶時，通常會提供這個值給您。</span><span class="sxs-lookup"><span data-stu-id="d469a-292">This value is typically provided for you when you select a storage account.</span></span> <span data-ttu-id="d469a-293">如果您希望 Visual Studio tooremember hello 儲存體帳戶金鑰，請選取 hello 記住帳戶金鑰 方塊。</span><span class="sxs-lookup"><span data-stu-id="d469a-293">If you want Visual Studio tooremember hello storage account key, select hello Remember account key box.</span></span>
   * <span data-ttu-id="d469a-294">hello 通訊協定 toouse tooconnect toohello 儲存體帳戶，例如 HTTP、 HTTPS 或自訂端點。</span><span class="sxs-lookup"><span data-stu-id="d469a-294">hello protocol toouse tooconnect toohello storage account, such as HTTP, HTTPS, or a custom endpoint.</span></span> <span data-ttu-id="d469a-295">請參閱[如何 tooConfigure 連接字串](https://msdn.microsoft.com/library/azure/ee758697.aspx)如需有關自訂端點。</span><span class="sxs-lookup"><span data-stu-id="d469a-295">See [How tooConfigure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx) for more information about custom endpoints.</span></span>

### <a name="tooview-hello-secondary-endpoints"></a><span data-ttu-id="d469a-296">tooview hello 次要端點</span><span class="sxs-lookup"><span data-stu-id="d469a-296">tooview hello secondary endpoints</span></span>
* <span data-ttu-id="d469a-297">如果您建立儲存體帳戶使用 hello**讀取存取異地備援**複寫選項，您可以檢視其次要端點。</span><span class="sxs-lookup"><span data-stu-id="d469a-297">If you created a storage account using hello **Read-Access Geo Redundant** replication option, you can view its secondary endpoints.</span></span> <span data-ttu-id="d469a-298">開啟 hello hello 帳戶名稱的捷徑功能表，然後選擇**屬性**。</span><span class="sxs-lookup"><span data-stu-id="d469a-298">Open hello shortcut menu for hello account name, and then choose **Properties**.</span></span>
  
    ![儲存體次要端點](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a><span data-ttu-id="d469a-300">tooremove 儲存體帳戶，從 伺服器總管</span><span class="sxs-lookup"><span data-stu-id="d469a-300">tooremove a storage account from Server Explorer</span></span>
* <span data-ttu-id="d469a-301">在 伺服器總管 中，開啟 hello hello 帳戶名稱的捷徑功能表，然後選擇 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="d469a-301">In Server Explorer, open hello shortcut menu for hello account name, and then choose **Delete**.</span></span> <span data-ttu-id="d469a-302">如果您刪除儲存體帳戶，也會移除該帳戶的所有已儲存金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="d469a-302">If you delete a storage account, any saved key information for that account is also removed.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d469a-303">如果您從 [伺服器總管] 刪除儲存體帳戶，它不會影響您的儲存體帳戶或任何內含的資料只會從伺服器總管移除 hello 參考。</span><span class="sxs-lookup"><span data-stu-id="d469a-303">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains; it simply removes hello reference from Server Explorer.</span></span> <span data-ttu-id="d469a-304">toopermanently 刪除儲存體帳戶，請使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="d469a-304">toopermanently delete a storage account, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
  > 
  > 

## <a name="next-steps"></a><span data-ttu-id="d469a-305">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d469a-305">Next steps</span></span>
<span data-ttu-id="d469a-306">toolearn 進一步了解如何使用 Azure 儲存體服務，請參閱[存取 hello Azure 儲存體服務](https://msdn.microsoft.com/library/azure/ee405490.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d469a-306">toolearn more about how use Azure storage services, see [Accessing hello Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span></span>

