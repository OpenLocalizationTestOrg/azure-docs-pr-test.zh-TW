---
title: "搭配使用儲存體 Explorer (預覽) 與 Azure 檔案儲存體 | Microsoft Docs"
description: "了解如何透過儲存體 Explorer (預覽) 來使用檔案共用和檔案。"
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
ms.openlocfilehash: 964691758254531cb92a5b1cbe055ef61d25dba8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="04a5b-103">搭配使用儲存體 Explorer (預覽) 與 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="04a5b-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="04a5b-104">Azure 檔案儲存體是使用標準伺服器訊息區塊 (SMB) 通訊協定，在雲端中提供檔案共用功能的服務。</span><span class="sxs-lookup"><span data-stu-id="04a5b-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="04a5b-105">SMB 2.1 和 SMB 3.0 皆受到支援。</span><span class="sxs-lookup"><span data-stu-id="04a5b-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="04a5b-106">使用 Azure 檔案儲存體時，您可以快速地將依賴檔案共用功能的舊式應用程式移轉至 Azure，而不必浪費成本來重新撰寫程式。</span><span class="sxs-lookup"><span data-stu-id="04a5b-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span></span> <span data-ttu-id="04a5b-107">您可以使用檔案儲存體向全球公開資料，或私下儲存應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="04a5b-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="04a5b-108">在本文中，您將學習如何使用儲存體 Explorer (預覽) 來使用檔案共用和檔案。</span><span class="sxs-lookup"><span data-stu-id="04a5b-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04a5b-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="04a5b-109">Prerequisites</span></span>

<span data-ttu-id="04a5b-110">若要完成這篇文章中的步驟，您需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="04a5b-110">To complete the steps in this article, you'll need the following:</span></span>

- [<span data-ttu-id="04a5b-111">下載並安裝儲存體 Explorer (預覽)</span><span class="sxs-lookup"><span data-stu-id="04a5b-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="04a5b-112">連接到 Azure 儲存體帳戶或服務</span><span class="sxs-lookup"><span data-stu-id="04a5b-112">Connect to a Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="04a5b-113">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="04a5b-113">Create a File Share</span></span>

<span data-ttu-id="04a5b-114">所有檔案必須都位於檔案共用，這是檔案的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="04a5b-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="04a5b-115">帳戶可以包含無限數量的檔案共用，每個共用可以儲存無限數量的檔案。</span><span class="sxs-lookup"><span data-stu-id="04a5b-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="04a5b-116">下列步驟說明如何在儲存體 Explorer (預覽) 中建立檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="04a5b-117">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="04a5b-118">在左窗格中，展開您要在其中建立檔案共用的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="04a5b-118">In the left pane, expand the storage account within which you wish to create the File Share</span></span>

3. <span data-ttu-id="04a5b-119">以滑鼠右鍵按一下 [檔案共用]，然後從內容功能表中 - 選取 [建立檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span></span>

    ![建立檔案共用](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="04a5b-121">[檔案共用] 資料夾底下會出現文字方塊。</span><span class="sxs-lookup"><span data-stu-id="04a5b-121">A text box will appear below the **File Shares** folder.</span></span> <span data-ttu-id="04a5b-122">輸入檔案共用的名稱。</span><span class="sxs-lookup"><span data-stu-id="04a5b-122">Enter the name for your file share.</span></span> <span data-ttu-id="04a5b-123">請參閱 [共用命名規則](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) 區段，以取得命名檔案共用的規則和限制的清單。</span><span class="sxs-lookup"><span data-stu-id="04a5b-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![命名共用](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="04a5b-125">完成建立檔案共用時按下 **Enter**鍵，或按下 **Esc** 鍵取消。</span><span class="sxs-lookup"><span data-stu-id="04a5b-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span></span> <span data-ttu-id="04a5b-126">一旦成功建立檔案共用，它就會顯示在所選的儲存體帳戶的 [檔案共用] 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="04a5b-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span></span>

    ![新增共用](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="04a5b-128">檢視檔案共用的內容</span><span class="sxs-lookup"><span data-stu-id="04a5b-128">View a file share's contents</span></span>

<span data-ttu-id="04a5b-129">檔案共用包含檔案和資料夾 (也包含檔案)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="04a5b-130">下列步驟說明如何在儲存體 Explorer (預覽) 中檢視檔案共用的內容：+</span><span class="sxs-lookup"><span data-stu-id="04a5b-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="04a5b-131">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="04a5b-132">在左窗格中，展開儲存體帳戶，其中包含您要檢視的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-132">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="04a5b-133">展開儲存體帳戶的 [檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-133">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="04a5b-134">以滑鼠右鍵按一下您想要檢視的檔案共用，從內容功能表中，選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span></span> <span data-ttu-id="04a5b-135">您也可以按兩下想要檢視的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-135">You can also double-click the file share you wish to view.</span></span>

    ![開啟共用](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="04a5b-137">主窗格會顯示檔案共用的內容。</span><span class="sxs-lookup"><span data-stu-id="04a5b-137">The main pane will display the file share's contents.</span></span>
    
    ![檔案共用的內容](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="04a5b-139">刪除檔案共用</span><span class="sxs-lookup"><span data-stu-id="04a5b-139">Delete a file share</span></span>

<span data-ttu-id="04a5b-140">檔案共用可以輕鬆地建立並視需要刪除。</span><span class="sxs-lookup"><span data-stu-id="04a5b-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="04a5b-141">(若要查看如何刪除個別的檔案，請參閱[管理檔案共用中的檔案](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)。)</span><span class="sxs-lookup"><span data-stu-id="04a5b-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="04a5b-142">下列步驟說明如何在儲存體 Explorer (預覽) 中刪除檔案共用：</span><span class="sxs-lookup"><span data-stu-id="04a5b-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="04a5b-143">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="04a5b-144">在左窗格中，展開儲存體帳戶，其中包含您要檢視的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-144">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="04a5b-145">展開儲存體帳戶的 [檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-145">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="04a5b-146">以滑鼠右鍵按一下您想要刪除的檔案共用，從內容功能表中，選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span></span> <span data-ttu-id="04a5b-147">您也可以按 [刪除] 以刪除目前選取的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-147">You can also press **Delete** to delete the currently selected file share.</span></span>

    ![刪除](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="04a5b-149">選取確認對話方塊上的 [是]  。</span><span class="sxs-lookup"><span data-stu-id="04a5b-149">Select **Yes** to the confirmation dialog.</span></span>
    
    ![確認對話方塊](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="04a5b-151">複製檔案共用</span><span class="sxs-lookup"><span data-stu-id="04a5b-151">Copy a file share</span></span>

<span data-ttu-id="04a5b-152">儲存體 Explorer (預覽) 可讓您將檔案共用複製到剪貼簿，然後將該檔案共用貼到另一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="04a5b-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="04a5b-153">(若要查看如何複製個別的檔案，請參閱[管理檔案共用中的檔案](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)。)</span><span class="sxs-lookup"><span data-stu-id="04a5b-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="04a5b-154">下列步驟說明如何將檔案共用從某個儲存體帳戶複製到另一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="04a5b-154">The following steps illustrate how to copy a file share from one storage account to another.</span></span>

1. <span data-ttu-id="04a5b-155">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="04a5b-156">在左窗格中，展開儲存體帳戶，其中包含您要複製的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-156">In the left pane, expand the storage account containing the file share you wish to copy.</span></span>

3. <span data-ttu-id="04a5b-157">展開儲存體帳戶的 [檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-157">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="04a5b-158">以滑鼠右鍵按一下您想要複製的檔案共用，從內容功能表中，選取 [複製檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span></span>

    ![複製檔案共用](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="04a5b-160">以滑鼠右鍵按一下想要貼上至檔案共用的「目標」儲存體帳戶，從內容功能表中，選取 [貼上檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span></span>

    ![貼上檔案共用](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a><span data-ttu-id="04a5b-162">取得檔案共用的 SAS</span><span class="sxs-lookup"><span data-stu-id="04a5b-162">Get the SAS for a file share</span></span>

<span data-ttu-id="04a5b-163">[共用存取簽章 (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) 可提供您儲存體帳戶中資源的委派存取。</span><span class="sxs-lookup"><span data-stu-id="04a5b-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="04a5b-164">這表示您可以在無需分享您帳戶存取金鑰的情況下，將您儲存體帳戶中的物件有限權限授與用戶端，該用戶端便可在指定的時間期間內及使用指定的權限集來進行存取。</span><span class="sxs-lookup"><span data-stu-id="04a5b-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="04a5b-165">下列步驟說明如何建立檔案共用的 SAS：</span><span class="sxs-lookup"><span data-stu-id="04a5b-165">The following steps illustrate how to create a SAS for a file share:+</span></span>

1. <span data-ttu-id="04a5b-166">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="04a5b-167">在左窗格中，展開儲存體帳戶，其中包含您要取得 SAS 的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span></span>

3. <span data-ttu-id="04a5b-168">展開儲存體帳戶的 [檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-168">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="04a5b-169">以滑鼠右鍵按一下想要的檔案共用，從內容功能表中，選取 [取得共用存取簽章]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

    ![取得共用存取簽章](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="04a5b-171">在 [共用存取簽章]  對話方塊中，指定您要用於資源的原則、開始和到期日期、時區和存取層級。</span><span class="sxs-lookup"><span data-stu-id="04a5b-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

    ![SAS 對話方塊](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="04a5b-173">當您完成指定 SAS 選項時，選取 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-173">When you're finished specifying the SAS options, select **Create**.</span></span>

7. <span data-ttu-id="04a5b-174">第二個 [共用存取簽章] 對話方塊會顯示，列出您可以用來存取儲存體資源的檔案共用及 URL 和 QueryStrings。</span><span class="sxs-lookup"><span data-stu-id="04a5b-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span></span> <span data-ttu-id="04a5b-175">選取您想要複製到剪貼簿的 URL 旁邊的 [複製]  。</span><span class="sxs-lookup"><span data-stu-id="04a5b-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>
    
    ![第二個 SAS 對話方塊](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="04a5b-177">完成時，選取 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="04a5b-178">管理檔案共用的存取原則</span><span class="sxs-lookup"><span data-stu-id="04a5b-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="04a5b-179">下列步驟說明如何管理 (新增和移除) 檔案共用的存取原則︰+。</span><span class="sxs-lookup"><span data-stu-id="04a5b-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="04a5b-180">存取原則用來建立 SAS URL，使用者可藉此使用在定義的時間期間存取儲存體檔案資源。</span><span class="sxs-lookup"><span data-stu-id="04a5b-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="04a5b-181">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="04a5b-182">在左窗格中，展開儲存體帳戶，其中包含您要管理其存取原則的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span></span>

3. <span data-ttu-id="04a5b-183">展開儲存體帳戶的 [檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-183">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="04a5b-184">選取想要的檔案共用，從內容功能表中，選取 [管理存取原則]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span></span>

    ![管理存取原則內容功能表](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="04a5b-186">[存取原則] 對話方塊會列出已針對所選的檔案共用建立的任何存取原則。</span><span class="sxs-lookup"><span data-stu-id="04a5b-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span></span>
    
    ![存取原則](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="04a5b-188">根據存取原則管理工作遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="04a5b-188">Follow these steps depending on the access policy management task:</span></span>
    
    - <span data-ttu-id="04a5b-189">**新增新的存取原則** -選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="04a5b-190">一旦產生，[存取原則]  對話方塊將會顯示新加入的存取原則 (具有預設設定)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="04a5b-191">**編輯存取原則** - 進行任何所需的編輯，然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="04a5b-192">**移除存取原則** -選取您想要移除的存取原則旁邊的 [移除]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

7. <span data-ttu-id="04a5b-193">使用您稍早建立的存取原則建立新的 SAS URL︰</span><span class="sxs-lookup"><span data-stu-id="04a5b-193">Create a new SAS URL using the Access Policy you created earlier:</span></span>
    
    ![取得 SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS 名稱和屬性](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="04a5b-196">檔案共用中的管理檔案</span><span class="sxs-lookup"><span data-stu-id="04a5b-196">Managing files in a file share</span></span>

<span data-ttu-id="04a5b-197">建立檔案共用之後，您可以將檔案上傳至檔案共用、將檔案下載到本機電腦或在本機電腦上開啟檔案等等。</span><span class="sxs-lookup"><span data-stu-id="04a5b-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="04a5b-198">下列步驟說明如何管理檔案共用中的檔案 (及資料夾)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-198">The following steps illustrate how to manage the files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="04a5b-199">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="04a5b-200">在左窗格中，展開儲存體帳戶，其中包含您要管理的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-200">In the left pane, expand the storage account containing the file share you wish to manage.</span></span>

3.  <span data-ttu-id="04a5b-201">展開儲存體帳戶的 [檔案共用]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-201">Expand the storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="04a5b-202">按兩下想要檢視的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="04a5b-202">Double-click the file share you wish to view.</span></span>

5.  <span data-ttu-id="04a5b-203">主窗格會顯示檔案共用的內容。</span><span class="sxs-lookup"><span data-stu-id="04a5b-203">The main pane will display the file share's contents.</span></span>

    ![檔案共用的內容](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="04a5b-205">主窗格會顯示檔案共用的內容。</span><span class="sxs-lookup"><span data-stu-id="04a5b-205">The main pane will display the file share's contents.</span></span>

7.  <span data-ttu-id="04a5b-206">根據您想要執行的工作遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="04a5b-206">Follow these steps depending on the task you wish to perform:</span></span>

    - <span data-ttu-id="04a5b-207">**將檔案上傳至檔案共用**</span><span class="sxs-lookup"><span data-stu-id="04a5b-207">**Upload files to a file share**</span></span>

        <span data-ttu-id="04a5b-208">a.</span><span class="sxs-lookup"><span data-stu-id="04a5b-208">a.</span></span>  <span data-ttu-id="04a5b-209">在主窗格工具列上，選取 [上傳]，然後從下拉式功能表選取 [上傳檔案]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![上傳檔案](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="04a5b-211">b.</span><span class="sxs-lookup"><span data-stu-id="04a5b-211">b.</span></span> <span data-ttu-id="04a5b-212">在 [上傳檔案] 對話方塊中，選擇 [檔案] 文字方塊右側的省略符號 (**…**) 按鈕，以選取您想要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="04a5b-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![新增檔案](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="04a5b-214">c.</span><span class="sxs-lookup"><span data-stu-id="04a5b-214">c.</span></span> <span data-ttu-id="04a5b-215">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-215">Select **Upload**.</span></span>

    - <span data-ttu-id="04a5b-216">**將資料夾上傳至檔案共用**</span><span class="sxs-lookup"><span data-stu-id="04a5b-216">**Upload a folder to a file share**</span></span>
        
        <span data-ttu-id="04a5b-217">a.</span><span class="sxs-lookup"><span data-stu-id="04a5b-217">a.</span></span> <span data-ttu-id="04a5b-218">在主窗格工具列上，選取 [上傳]，然後從下拉式功能表選取 [上傳資料夾]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![上傳資料夾功能表](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="04a5b-220">b.</span><span class="sxs-lookup"><span data-stu-id="04a5b-220">b.</span></span> <span data-ttu-id="04a5b-221">在 [上傳資料夾] 對話方塊中，選擇 [資料夾] 文字方塊右側的省略符號 (**…**) 按鈕，以選取您想要上傳其內容的資料夾。</span><span class="sxs-lookup"><span data-stu-id="04a5b-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        <span data-ttu-id="04a5b-222">c.</span><span class="sxs-lookup"><span data-stu-id="04a5b-222">c.</span></span> <span data-ttu-id="04a5b-223">選擇性地指定選取的資料夾的內容將會上傳至其中的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="04a5b-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="04a5b-224">如果目標資料夾不存在，系統就會加以建立。</span><span class="sxs-lookup"><span data-stu-id="04a5b-224">If the target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="04a5b-225">d.</span><span class="sxs-lookup"><span data-stu-id="04a5b-225">d.</span></span> <span data-ttu-id="04a5b-226">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-226">Select **Upload**.</span></span>

    - <span data-ttu-id="04a5b-227">**將檔案下載到本機電腦**</span><span class="sxs-lookup"><span data-stu-id="04a5b-227">**Download a file to your local computer**</span></span>
        
        <span data-ttu-id="04a5b-228">a.</span><span class="sxs-lookup"><span data-stu-id="04a5b-228">a.</span></span> <span data-ttu-id="04a5b-229">選取您想要下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="04a5b-229">Select the file you wish to download.</span></span>
        
        <span data-ttu-id="04a5b-230">b.</span><span class="sxs-lookup"><span data-stu-id="04a5b-230">b.</span></span> <span data-ttu-id="04a5b-231">在主窗格工具列上選取 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-231">On the main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="04a5b-232">c.</span><span class="sxs-lookup"><span data-stu-id="04a5b-232">c.</span></span> <span data-ttu-id="04a5b-233">在 [指定儲存下載的檔案的位置] 對話方塊中，指定要下載檔案的位置，和您想要給予它的名稱。</span><span class="sxs-lookup"><span data-stu-id="04a5b-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span></span>

        <span data-ttu-id="04a5b-234">d.</span><span class="sxs-lookup"><span data-stu-id="04a5b-234">d.</span></span> <span data-ttu-id="04a5b-235">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="04a5b-235">Select **Save**.</span></span>

    - <span data-ttu-id="04a5b-236">**在您的本機電腦上開啟檔案**</span><span class="sxs-lookup"><span data-stu-id="04a5b-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="04a5b-237">a.</span><span class="sxs-lookup"><span data-stu-id="04a5b-237">a.</span></span>  <span data-ttu-id="04a5b-238">選取您想要開啟的檔案。</span><span class="sxs-lookup"><span data-stu-id="04a5b-238">Select the file you wish to open.</span></span>
        
        <span data-ttu-id="04a5b-239">b.</span><span class="sxs-lookup"><span data-stu-id="04a5b-239">b.</span></span>  <span data-ttu-id="04a5b-240">在主窗格工具列上選取 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-240">On the main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="04a5b-241">c.</span><span class="sxs-lookup"><span data-stu-id="04a5b-241">c.</span></span>  <span data-ttu-id="04a5b-242">檔案會被下載，並使用與檔案的基礎檔案類型相關聯的應用程式開啟。</span><span class="sxs-lookup"><span data-stu-id="04a5b-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span></span>

    - <span data-ttu-id="04a5b-243">**將檔案複製到剪貼簿**</span><span class="sxs-lookup"><span data-stu-id="04a5b-243">**Copy a file to the clipboard**</span></span>

        <span data-ttu-id="04a5b-244">a.</span><span class="sxs-lookup"><span data-stu-id="04a5b-244">a.</span></span> <span data-ttu-id="04a5b-245">選取您想要複製的檔案。</span><span class="sxs-lookup"><span data-stu-id="04a5b-245">Select the file you wish to copy.</span></span>

        <span data-ttu-id="04a5b-246">b.</span><span class="sxs-lookup"><span data-stu-id="04a5b-246">b.</span></span> <span data-ttu-id="04a5b-247">在主窗格工具列上選取 [複製] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-247">On the main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="04a5b-248">c.</span><span class="sxs-lookup"><span data-stu-id="04a5b-248">c.</span></span> <span data-ttu-id="04a5b-249">在左窗格中，瀏覽至另一個檔案共用，然後在主窗格中按兩下加以檢視。</span><span class="sxs-lookup"><span data-stu-id="04a5b-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span></span>

        <span data-ttu-id="04a5b-250">d.</span><span class="sxs-lookup"><span data-stu-id="04a5b-250">d.</span></span> <span data-ttu-id="04a5b-251">在主窗格工具列上選取 [貼上] 以建立檔案的複本。</span><span class="sxs-lookup"><span data-stu-id="04a5b-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span></span>

    - <span data-ttu-id="04a5b-252">**刪除檔案**</span><span class="sxs-lookup"><span data-stu-id="04a5b-252">**Delete a file**</span></span>

        <span data-ttu-id="04a5b-253">a.</span><span class="sxs-lookup"><span data-stu-id="04a5b-253">a.</span></span> <span data-ttu-id="04a5b-254">選取您想要刪除的檔案。</span><span class="sxs-lookup"><span data-stu-id="04a5b-254">Select the file you wish to delete.</span></span>

        <span data-ttu-id="04a5b-255">b.</span><span class="sxs-lookup"><span data-stu-id="04a5b-255">b.</span></span> <span data-ttu-id="04a5b-256">在主窗格工具列上選取 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="04a5b-256">On the main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="04a5b-257">c.</span><span class="sxs-lookup"><span data-stu-id="04a5b-257">c.</span></span> <span data-ttu-id="04a5b-258">選取確認對話方塊上的 [是]  。</span><span class="sxs-lookup"><span data-stu-id="04a5b-258">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04a5b-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04a5b-259">Next steps</span></span>

- <span data-ttu-id="04a5b-260">檢視 [最新的儲存體 Explorer (預覽) 版本資訊與影片](http://www.storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="04a5b-261">了解如何 [利用 Azure Blob、資料表、佇列和檔案建立應用程式](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="04a5b-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
