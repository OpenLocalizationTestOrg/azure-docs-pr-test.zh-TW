---
title: "aaaUsing Azure 檔案儲存體的儲存體總管 （預覽） |Microsoft 文件"
description: "深入了解如何了解如何 toouse 存放裝置總管 （預覽） toowork 與檔案共用和檔案。"
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="9739f-103">搭配使用儲存體 Explorer (預覽) 與 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="9739f-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="9739f-104">Azure 儲存體是一項服務，提供檔案共用中 hello 雲端使用的檔案 hello 標準伺服器訊息區塊 (SMB) 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9739f-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="9739f-105">SMB 2.1 和 SMB 3.0 皆受到支援。</span><span class="sxs-lookup"><span data-stu-id="9739f-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="9739f-106">使用 Azure 檔案儲存體，您可以移轉依賴檔案共用 tooAzure 快速且不昂貴的撰寫的舊版應用程式。</span><span class="sxs-lookup"><span data-stu-id="9739f-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="9739f-107">您可以使用檔案儲存體 tooexpose 資料公開 toohello 世界中或 toostore 應用程式資料未公開。</span><span class="sxs-lookup"><span data-stu-id="9739f-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="9739f-108">在本文中，您將學習如何 toouse 存放裝置總管 （預覽） toowork 與檔案共用和檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9739f-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="9739f-109">Prerequisites</span></span>

<span data-ttu-id="9739f-110">toocomplete hello 本文中的步驟，您將需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="9739f-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="9739f-111">下載並安裝儲存體 Explorer (預覽)</span><span class="sxs-lookup"><span data-stu-id="9739f-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="9739f-112">連接 tooa Azure 儲存體帳戶或服務</span><span class="sxs-lookup"><span data-stu-id="9739f-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="9739f-113">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="9739f-113">Create a File Share</span></span>

<span data-ttu-id="9739f-114">所有檔案必須都位於檔案共用，這是檔案的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="9739f-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="9739f-115">帳戶可以包含無限數量的檔案共用，每個共用可以儲存無限數量的檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="9739f-116">hello 下列步驟說明如何 toocreate 檔案共用儲存體總管 （預覽） 內。</span><span class="sxs-lookup"><span data-stu-id="9739f-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="9739f-117">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="9739f-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="9739f-118">Hello 左窗格中，展開要在其中 toocreate hello 檔案共用的 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="9739f-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="9739f-119">以滑鼠右鍵按一下**檔案共用**，和-hello 操作功能表： 從選取**建立檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![建立檔案共用](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="9739f-121">文字會出現一個方塊下方 hello**檔案共用**資料夾。</span><span class="sxs-lookup"><span data-stu-id="9739f-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="9739f-122">輸入 hello 檔案共用的名稱。</span><span class="sxs-lookup"><span data-stu-id="9739f-122">Enter hello name for your file share.</span></span> <span data-ttu-id="9739f-123">請參閱 hello[共用命名規則](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container)一節，以清單規則以及限制命名的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="9739f-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![命名 hello 共用](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="9739f-125">按**Enter**時完成的 toocreate hello 檔案共用或**Esc** toocancel。</span><span class="sxs-lookup"><span data-stu-id="9739f-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="9739f-126">一旦已成功建立 hello 檔案共用，它就會顯示在 hello**檔案共用**hello 資料夾選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![hello 新的共用](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="9739f-128">檢視檔案共用的內容</span><span class="sxs-lookup"><span data-stu-id="9739f-128">View a file share's contents</span></span>

<span data-ttu-id="9739f-129">檔案共用包含檔案和資料夾 (也包含檔案)。</span><span class="sxs-lookup"><span data-stu-id="9739f-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="9739f-130">hello 下列步驟說明如何 tooview hello 檔案內容的共用存放裝置總管 （預覽） 中: +</span><span class="sxs-lookup"><span data-stu-id="9739f-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="9739f-131">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="9739f-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="9739f-132">Hello 左窗格中，展開包含您想 tooview hello 檔案共用的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="9739f-133">展開 hello 儲存體帳戶的**檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="9739f-134">以滑鼠右鍵按一下 hello 檔案共用您想 tooview，和-hello 操作功能表： 從選取**開啟**。</span><span class="sxs-lookup"><span data-stu-id="9739f-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="9739f-135">您也可以按兩下您想 tooview hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="9739f-135">You can also double-click hello file share you wish tooview.</span></span>

    ![開啟共用](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="9739f-137">hello 主窗格會顯示 hello 檔案共用的內容。</span><span class="sxs-lookup"><span data-stu-id="9739f-137">hello main pane will display hello file share's contents.</span></span>
    
    ![hello 共用的內容](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="9739f-139">刪除檔案共用</span><span class="sxs-lookup"><span data-stu-id="9739f-139">Delete a file share</span></span>

<span data-ttu-id="9739f-140">檔案共用可以輕鬆地建立並視需要刪除。</span><span class="sxs-lookup"><span data-stu-id="9739f-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="9739f-141">(toosee toodelete 個別檔案，請參閱 toohello 區段中，如何[管理檔案共用中的檔案](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)。)</span><span class="sxs-lookup"><span data-stu-id="9739f-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="9739f-142">hello 下列步驟說明如何 toodelete 檔案共用儲存體總管 （預覽） 中所示：</span><span class="sxs-lookup"><span data-stu-id="9739f-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="9739f-143">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="9739f-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="9739f-144">Hello 左窗格中，展開包含您想 tooview hello 檔案共用的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="9739f-145">展開 hello 儲存體帳戶的**檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="9739f-146">以滑鼠右鍵按一下 hello 檔案共用您想 toodelete，和-hello 操作功能表： 從選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="9739f-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="9739f-147">您也可以按**刪除**toodelete hello 目前選取的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="9739f-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![刪除](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="9739f-149">選取**是**toohello 確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9739f-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![確認對話方塊](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="9739f-151">複製檔案共用</span><span class="sxs-lookup"><span data-stu-id="9739f-151">Copy a file share</span></span>

<span data-ttu-id="9739f-152">儲存體總管 （預覽） 可讓您 toocopy 檔案共用 toohello 剪貼簿，然後將該檔案共用貼到另一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="9739f-153">(toosee toocopy 個別檔案，請參閱 toohello 區段中，如何[管理檔案共用中的檔案](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)。)</span><span class="sxs-lookup"><span data-stu-id="9739f-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="9739f-154">hello 下列步驟說明從一個儲存體帳戶 tooanother toocopy 檔案共用的方式。</span><span class="sxs-lookup"><span data-stu-id="9739f-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="9739f-155">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="9739f-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="9739f-156">Hello 左窗格中，展開包含您想 toocopy hello 檔案共用的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="9739f-157">展開 hello 儲存體帳戶的**檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="9739f-158">以滑鼠右鍵按一下 hello 檔案共用您想 toocopy，和-hello 操作功能表： 從選取**複製的檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![複製檔案共用](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="9739f-160">以滑鼠右鍵按一下 hello 所需"target"儲存體帳戶所在 toopaste hello 檔案共用，再-hello 操作功能表： 從選取**貼上檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![貼上檔案共用](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="9739f-162">取得檔案共用中的 hello SAS</span><span class="sxs-lookup"><span data-stu-id="9739f-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="9739f-163">A[共用的存取簽章 (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1)提供儲存體帳戶中的委派的存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="9739f-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="9739f-164">這表示您可以授與用戶端在指定期間內的時間與一組指定的權限，在儲存體帳戶的權限 tooobjects 限制而不需要 tooshare 帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="9739f-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="9739f-165">hello 下列步驟說明如何 toocreate SAS，使檔案共用: +</span><span class="sxs-lookup"><span data-stu-id="9739f-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="9739f-166">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="9739f-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="9739f-167">Hello 左窗格中，展開包含您想 tooget SAS hello 檔案共用的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="9739f-168">展開 hello 儲存體帳戶的**檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="9739f-169">Hello 所需的檔案共用，以滑鼠右鍵按一下和-hello 操作功能表： 從選取**取得共用存取簽章**。</span><span class="sxs-lookup"><span data-stu-id="9739f-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![取得共用存取簽章](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="9739f-171">在 [hello**共用存取簽章**] 對話方塊中，指定 hello 原則、 開始和到期日期、 時間區域，然後存取您想要用於 hello 資源層級。</span><span class="sxs-lookup"><span data-stu-id="9739f-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![SAS 對話方塊](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="9739f-173">當您完成指定的 hello SAS 選項，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="9739f-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="9739f-174">第二個**共用存取簽章**清單 hello 以及 hello URL 的檔案共用，您可以使用 tooaccess QueryStrings hello 儲存體資源，就會顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9739f-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="9739f-175">選取**複製**想 toocopy toohello 剪貼簿的 下一步 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="9739f-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![第二個 SAS 對話方塊](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="9739f-177">完成時，選取 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="9739f-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="9739f-178">管理檔案共用的存取原則</span><span class="sxs-lookup"><span data-stu-id="9739f-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="9739f-179">hello 下列步驟說明如何 toomanage （新增與移除） 存取檔案共用的原則: +。</span><span class="sxs-lookup"><span data-stu-id="9739f-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="9739f-180">hello 存取原則用來建立 SAS Url，透過該人員可以定義的時間期間使用 tooaccess hello 儲存體檔案資源。</span><span class="sxs-lookup"><span data-stu-id="9739f-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="9739f-181">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="9739f-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="9739f-182">Hello 左窗格中，展開包含 hello 檔案共用您想 toomanage 的存取原則的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="9739f-183">展開 hello 儲存體帳戶的**檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="9739f-184">選取 hello 所需的檔案共用，以及-hello 操作功能表： 從選取**管理存取原則**。</span><span class="sxs-lookup"><span data-stu-id="9739f-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![管理存取原則內容功能表](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="9739f-186">hello**存取原則** 對話方塊會列出任何已建立 hello 選取的檔案共用的存取原則。</span><span class="sxs-lookup"><span data-stu-id="9739f-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![存取原則](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="9739f-188">遵循下列步驟，視 hello 存取原則的管理工作而定：</span><span class="sxs-lookup"><span data-stu-id="9739f-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="9739f-189">**新增新的存取原則** -選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9739f-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="9739f-190">一旦產生，hello**存取原則**對話方塊會顯示 hello 新加入的存取原則 （使用預設設定）。</span><span class="sxs-lookup"><span data-stu-id="9739f-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="9739f-191">**編輯存取原則** - 進行任何所需的編輯，然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9739f-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="9739f-192">**移除存取原則**-選取**移除**想 tooremove 的下一個 toohello 存取原則。</span><span class="sxs-lookup"><span data-stu-id="9739f-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="9739f-193">建立新的 SAS URL，使用 hello 您稍早建立的存取原則：</span><span class="sxs-lookup"><span data-stu-id="9739f-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![取得 SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS 名稱和屬性](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="9739f-196">檔案共用中的管理檔案</span><span class="sxs-lookup"><span data-stu-id="9739f-196">Managing files in a file share</span></span>

<span data-ttu-id="9739f-197">一旦您已建立的檔案共用，您可以上傳檔案 toothat 檔案共用、 下載檔案 tooyour 本機電腦、 開啟本機電腦，以及執行更多檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="9739f-198">hello 下列步驟說明如何 toomanage hello 檔案 （和資料夾） 內的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="9739f-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="9739f-199">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="9739f-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="9739f-200">Hello 左窗格中，展開包含您想 toomanage hello 檔案共用的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9739f-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="9739f-201">展開 hello 儲存體帳戶的**檔案共用**。</span><span class="sxs-lookup"><span data-stu-id="9739f-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="9739f-202">按兩下您想 tooview hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="9739f-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="9739f-203">hello 主窗格會顯示 hello 檔案共用的內容。</span><span class="sxs-lookup"><span data-stu-id="9739f-203">hello main pane will display hello file share's contents.</span></span>

    ![hello 共用的內容](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="9739f-205">hello 主窗格會顯示 hello 檔案共用的內容。</span><span class="sxs-lookup"><span data-stu-id="9739f-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="9739f-206">請遵循這些步驟視 hello 工作想 tooperform:</span><span class="sxs-lookup"><span data-stu-id="9739f-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="9739f-207">**上傳檔案 tooa 檔案共用**</span><span class="sxs-lookup"><span data-stu-id="9739f-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="9739f-208">a.</span><span class="sxs-lookup"><span data-stu-id="9739f-208">a.</span></span>  <span data-ttu-id="9739f-209">Hello 主窗格的工具列上，選取**上傳**，然後**上載檔案**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="9739f-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![上傳檔案](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="9739f-211">b.</span><span class="sxs-lookup"><span data-stu-id="9739f-211">b.</span></span> <span data-ttu-id="9739f-212">在 hello**將檔案上傳**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**檔案**文字方塊想 tooupload tooselect hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![新增檔案](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="9739f-214">c.</span><span class="sxs-lookup"><span data-stu-id="9739f-214">c.</span></span> <span data-ttu-id="9739f-215">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="9739f-215">Select **Upload**.</span></span>

    - <span data-ttu-id="9739f-216">**上傳資料夾 tooa 檔案共用**</span><span class="sxs-lookup"><span data-stu-id="9739f-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="9739f-217">a.</span><span class="sxs-lookup"><span data-stu-id="9739f-217">a.</span></span> <span data-ttu-id="9739f-218">Hello 主窗格的工具列上，選取**上傳**，然後**上傳資料夾**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="9739f-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![上傳資料夾功能表](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="9739f-220">b.</span><span class="sxs-lookup"><span data-stu-id="9739f-220">b.</span></span> <span data-ttu-id="9739f-221">在 hello**上傳資料夾**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**資料夾**文字方塊 tooselect hello 資料夾想 tooupload 其內容。</span><span class="sxs-lookup"><span data-stu-id="9739f-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="9739f-222">c.</span><span class="sxs-lookup"><span data-stu-id="9739f-222">c.</span></span> <span data-ttu-id="9739f-223">選擇性地指定所選的資料夾的內容將會上傳到哪個 hello 的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="9739f-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="9739f-224">如果 hello 目標資料夾不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="9739f-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="9739f-225">d.</span><span class="sxs-lookup"><span data-stu-id="9739f-225">d.</span></span> <span data-ttu-id="9739f-226">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="9739f-226">Select **Upload**.</span></span>

    - <span data-ttu-id="9739f-227">**下載檔案 tooyour 本機電腦**</span><span class="sxs-lookup"><span data-stu-id="9739f-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="9739f-228">a.</span><span class="sxs-lookup"><span data-stu-id="9739f-228">a.</span></span> <span data-ttu-id="9739f-229">選取您想 toodownload hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="9739f-230">b.</span><span class="sxs-lookup"><span data-stu-id="9739f-230">b.</span></span> <span data-ttu-id="9739f-231">在 hello 主窗格的工具列上，選取 **下載**。</span><span class="sxs-lookup"><span data-stu-id="9739f-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="9739f-232">c.</span><span class="sxs-lookup"><span data-stu-id="9739f-232">c.</span></span> <span data-ttu-id="9739f-233">在 [hello **toosave hello 下載檔案的位置指定**] 對話方塊中，指定您希望 hello 檔案下載，hello 位置，然後 hello 想 toogive 名稱它。</span><span class="sxs-lookup"><span data-stu-id="9739f-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="9739f-234">d.</span><span class="sxs-lookup"><span data-stu-id="9739f-234">d.</span></span> <span data-ttu-id="9739f-235">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="9739f-235">Select **Save**.</span></span>

    - <span data-ttu-id="9739f-236">**在您的本機電腦上開啟檔案**</span><span class="sxs-lookup"><span data-stu-id="9739f-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="9739f-237">a.</span><span class="sxs-lookup"><span data-stu-id="9739f-237">a.</span></span>  <span data-ttu-id="9739f-238">選取您想 tooopen hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="9739f-239">b.</span><span class="sxs-lookup"><span data-stu-id="9739f-239">b.</span></span>  <span data-ttu-id="9739f-240">在 hello 主窗格的工具列上，選取 **開啟**。</span><span class="sxs-lookup"><span data-stu-id="9739f-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="9739f-241">c.</span><span class="sxs-lookup"><span data-stu-id="9739f-241">c.</span></span>  <span data-ttu-id="9739f-242">hello 檔案會下載，並使用 hello 與 hello 檔案基礎的檔案類型相關聯的應用程式開啟。</span><span class="sxs-lookup"><span data-stu-id="9739f-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="9739f-243">**複製檔案 toohello 剪貼簿**</span><span class="sxs-lookup"><span data-stu-id="9739f-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="9739f-244">a.</span><span class="sxs-lookup"><span data-stu-id="9739f-244">a.</span></span> <span data-ttu-id="9739f-245">選取您想 toocopy hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="9739f-246">b.</span><span class="sxs-lookup"><span data-stu-id="9739f-246">b.</span></span> <span data-ttu-id="9739f-247">在 hello 主窗格的工具列上，選取 **複製**。</span><span class="sxs-lookup"><span data-stu-id="9739f-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="9739f-248">c.</span><span class="sxs-lookup"><span data-stu-id="9739f-248">c.</span></span> <span data-ttu-id="9739f-249">在 hello 左窗格中，瀏覽 tooanother 檔案共用，然後按兩下該 tooview hello 主窗格中。</span><span class="sxs-lookup"><span data-stu-id="9739f-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="9739f-250">d.</span><span class="sxs-lookup"><span data-stu-id="9739f-250">d.</span></span> <span data-ttu-id="9739f-251">在 hello 主窗格的工具列上，選取 **貼上**toocreate hello 檔案的副本。</span><span class="sxs-lookup"><span data-stu-id="9739f-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="9739f-252">**刪除檔案**</span><span class="sxs-lookup"><span data-stu-id="9739f-252">**Delete a file**</span></span>

        <span data-ttu-id="9739f-253">a.</span><span class="sxs-lookup"><span data-stu-id="9739f-253">a.</span></span> <span data-ttu-id="9739f-254">選取您想 toodelete hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9739f-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="9739f-255">b.</span><span class="sxs-lookup"><span data-stu-id="9739f-255">b.</span></span> <span data-ttu-id="9739f-256">在 hello 主窗格的工具列上，選取 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="9739f-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="9739f-257">c.</span><span class="sxs-lookup"><span data-stu-id="9739f-257">c.</span></span> <span data-ttu-id="9739f-258">選取**是**toohello 確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9739f-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9739f-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9739f-259">Next steps</span></span>

- <span data-ttu-id="9739f-260">檢視 hello[最新的存放裝置總管 （預覽） 版本資訊和視訊](http://www.storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="9739f-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="9739f-261">了解如何太[建立應用程式使用 Azure blob、 資料表、 佇列和檔案](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="9739f-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
