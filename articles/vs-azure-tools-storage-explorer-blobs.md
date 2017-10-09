---
title: "aaaManage Azure Blob 儲存體資源，使用儲存體總管 （預覽） |Microsoft 文件"
description: "使用儲存體 Explorer 來管理 Azure Blob 容器和 Blob (預覽)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="5c587-103">使用儲存體 Explorer 來管理 Azure Blob 儲存體資源 (預覽)</span><span class="sxs-lookup"><span data-stu-id="5c587-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="5c587-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5c587-104">Overview</span></span>
<span data-ttu-id="5c587-105">[Azure Blob 儲存體](storage/blobs/storage-dotnet-how-to-use-blobs.md)是用來儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="5c587-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="5c587-106">您可以使用 Blob 儲存體 tooexpose 資料公開 toohello 世界中或 toostore 應用程式資料未公開。</span><span class="sxs-lookup"><span data-stu-id="5c587-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="5c587-107">在本文中，您將學習如何將存放裝置總管 （預覽） toowork toouse blob 容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="5c587-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c587-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c587-108">Prerequisites</span></span>
<span data-ttu-id="5c587-109">toocomplete hello 本文中的步驟，您將需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="5c587-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="5c587-110">下載並安裝儲存體 Explorer (預覽)</span><span class="sxs-lookup"><span data-stu-id="5c587-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="5c587-111">連接 tooa Azure 儲存體帳戶或服務</span><span class="sxs-lookup"><span data-stu-id="5c587-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="5c587-112">建立 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="5c587-112">Create a blob container</span></span>
<span data-ttu-id="5c587-113">所有 blob 必須都位於 blob 容器，這是 blob 的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="5c587-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="5c587-114">帳戶可以包含無限數量的容器，每個容器可以儲存無限數量的 blob。</span><span class="sxs-lookup"><span data-stu-id="5c587-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="5c587-115">hello 下列步驟說明如何 toocreate 存放裝置總管 （預覽） 中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5c587-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="5c587-116">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-117">Hello 左窗格中，展開要在其中 toocreate hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="5c587-118">以滑鼠右鍵按一下**Blob 容器**，和-hello 操作功能表： 從選取**建立 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![建立 Blob 容器內容功能表][0]
4. <span data-ttu-id="5c587-120">文字會出現一個方塊下方 hello **Blob 容器**資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c587-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="5c587-121">輸入您的 blob 容器的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="5c587-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="5c587-122">請參閱 hello[容器命名規則](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container)一節，以清單規則以及限制命名 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5c587-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![建立 Blob 容器文字方塊][1]
5. <span data-ttu-id="5c587-124">按**Enter**完成 toocreate hello blob 容器，或**Esc** toocancel。</span><span class="sxs-lookup"><span data-stu-id="5c587-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="5c587-125">一旦已成功建立 hello blob 容器，它就會顯示在 hello **Blob 容器**hello 資料夾選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Blob 容器已建立][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="5c587-127">檢視 blob 容器的內容</span><span class="sxs-lookup"><span data-stu-id="5c587-127">View a blob container's contents</span></span>
<span data-ttu-id="5c587-128">Blob 容器包含 blob 和資料夾 (也包含 blob)。</span><span class="sxs-lookup"><span data-stu-id="5c587-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="5c587-129">hello 下列步驟說明如何在儲存體總管 （預覽） 中的 blob 容器 tooview hello 內容：</span><span class="sxs-lookup"><span data-stu-id="5c587-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="5c587-130">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-131">Hello 左窗格中，展開包含您想 tooview hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="5c587-132">展開 hello 儲存體帳戶的**Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="5c587-133">以滑鼠右鍵按一下 hello blob 容器 tooview，並為 hello 操作功能表： 從選取**開啟 Blob 容器編輯器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="5c587-134">您也可以按兩下您想 tooview hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5c587-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![開啟 blob 容器編輯器內容功能表][19]
5. <span data-ttu-id="5c587-136">hello 主窗格會顯示 hello blob 容器的內容。</span><span class="sxs-lookup"><span data-stu-id="5c587-136">hello main pane will display hello blob container's contents.</span></span>

   ![Blob 容器編輯器][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="5c587-138">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="5c587-138">Delete a blob container</span></span>
<span data-ttu-id="5c587-139">Blob 容器可以輕鬆地建立並視需要刪除。</span><span class="sxs-lookup"><span data-stu-id="5c587-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="5c587-140">(toosee toodelete 個別的 blob，請參閱 toohello 區段[管理 blob 容器中的 blob](#managing-blobs-in-a-blob-container)。)</span><span class="sxs-lookup"><span data-stu-id="5c587-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="5c587-141">hello 下列步驟說明如何 toodelete blob 容器中儲存體總管 （預覽）：</span><span class="sxs-lookup"><span data-stu-id="5c587-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="5c587-142">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-143">Hello 左窗格中，展開包含您想 tooview hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="5c587-144">展開 hello 儲存體帳戶的**Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="5c587-145">以滑鼠右鍵按一下 hello blob 容器 toodelete，並為 hello 操作功能表： 從選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="5c587-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="5c587-146">您也可以按**刪除**toodelete hello 目前選取的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5c587-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![刪除 Blob 容器內容功能表][4]
5. <span data-ttu-id="5c587-148">選取**是**toohello 確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c587-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![刪除 Blob 容器確認][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="5c587-150">複製 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="5c587-150">Copy a blob container</span></span>
<span data-ttu-id="5c587-151">儲存體總管 （預覽） 可讓您 toocopy blob 容器 toohello 剪貼簿，然後到另一個儲存體帳戶 blob 容器的貼。</span><span class="sxs-lookup"><span data-stu-id="5c587-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="5c587-152">(toosee toocopy 個別的 blob，請參閱 toohello 區段[管理 blob 容器中的 blob](#managing-blobs-in-a-blob-container)。)</span><span class="sxs-lookup"><span data-stu-id="5c587-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="5c587-153">hello 下列步驟說明如何從一個儲存體 blob 容器 toocopy 帳戶 tooanother。</span><span class="sxs-lookup"><span data-stu-id="5c587-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="5c587-154">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-155">Hello 左窗格中，展開包含您想 toocopy hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="5c587-156">展開 hello 儲存體帳戶的**Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="5c587-157">以滑鼠右鍵按一下 hello blob 容器 toocopy，並為 hello 操作功能表： 從選取**複製 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![複製 Blob 容器內容功能表][6]
5. <span data-ttu-id="5c587-159">以滑鼠右鍵按一下 hello 所需"target"儲存體帳戶所在 toopaste hello blob 容器，再-hello 操作功能表： 從選取**貼上的 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![貼上 Blob 容器內容功能表][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="5c587-161">取得 blob 容器的 SAS hello</span><span class="sxs-lookup"><span data-stu-id="5c587-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="5c587-162">A[共用的存取簽章 (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md)提供儲存體帳戶中的委派的存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="5c587-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="5c587-163">這表示您可以授與用戶端限制在指定期間內的時間與一組指定的權限，在儲存體帳戶的權限 tooobjects，而不需要共用您的帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5c587-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="5c587-164">hello 下列步驟說明如何 toocreate blob 容器的 SAS:</span><span class="sxs-lookup"><span data-stu-id="5c587-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="5c587-165">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-166">Hello 左窗格中，展開包含您想 tooget SAS hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="5c587-167">展開 hello 儲存體帳戶的**Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="5c587-168">Hello 所需的 blob 容器，以滑鼠右鍵按一下和-hello 操作功能表： 從選取**取得共用存取簽章**。</span><span class="sxs-lookup"><span data-stu-id="5c587-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![取得 SAS 內容功能表][8]
5. <span data-ttu-id="5c587-170">在 [hello**共用存取簽章**] 對話方塊中，指定 hello 原則、 開始和到期日期、 時間區域，然後存取您想要用於 hello 資源層級。</span><span class="sxs-lookup"><span data-stu-id="5c587-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![取得 SAS 選項][9]
6. <span data-ttu-id="5c587-172">當您完成指定的 hello SAS 選項，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="5c587-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="5c587-173">第二個**共用存取簽章**清單 hello blob 容器以及 hello URL，您可以使用 tooaccess QueryStrings hello 儲存體資源，就會顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c587-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="5c587-174">選取**複製**想 toocopy toohello 剪貼簿的 下一步 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="5c587-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![複製 SAS URL][10]
8. <span data-ttu-id="5c587-176">完成時，選取 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="5c587-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="5c587-177">管理 blob 容器的存取原則</span><span class="sxs-lookup"><span data-stu-id="5c587-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="5c587-178">hello 下列步驟說明如何 toomanage （新增與移除） 存取的 blob 容器的原則：</span><span class="sxs-lookup"><span data-stu-id="5c587-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="5c587-179">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-180">Hello 左窗格中，展開包含您想 toomanage 其存取原則的 hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="5c587-181">展開 hello 儲存體帳戶的**Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="5c587-182">選取 hello 所需的 blob 容器，以及-hello 操作功能表： 從選取**管理存取原則**。</span><span class="sxs-lookup"><span data-stu-id="5c587-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![管理存取原則內容功能表][11]
5. <span data-ttu-id="5c587-184">hello**存取原則** 對話方塊會列出任何已建立 hello 選的 blob 容器的存取原則。</span><span class="sxs-lookup"><span data-stu-id="5c587-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![存取原則選項][12]        
6. <span data-ttu-id="5c587-186">遵循下列步驟，視 hello 存取原則的管理工作而定：</span><span class="sxs-lookup"><span data-stu-id="5c587-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="5c587-187">**新增新的存取原則** -選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5c587-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="5c587-188">一旦產生，hello**存取原則**對話方塊會顯示 hello 新加入的存取原則 （使用預設設定）。</span><span class="sxs-lookup"><span data-stu-id="5c587-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="5c587-189">**編輯存取原則** -進行任何所需的編輯，然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5c587-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="5c587-190">**移除存取原則**-選取**移除**想 tooremove 的下一個 toohello 存取原則。</span><span class="sxs-lookup"><span data-stu-id="5c587-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="5c587-191">Blob 容器設定 hello 公用存取層級</span><span class="sxs-lookup"><span data-stu-id="5c587-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="5c587-192">根據預設，每個 blob 容器設定太 「 沒有公用存取 」。</span><span class="sxs-lookup"><span data-stu-id="5c587-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="5c587-193">hello 下列步驟說明如何 toospecify 公用存取層級的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5c587-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="5c587-194">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-195">Hello 左窗格中，展開包含您想 toomanage 其存取原則的 hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="5c587-196">展開 hello 儲存體帳戶的**Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="5c587-197">選取 hello 所需的 blob 容器，以及-hello 操作功能表： 從選取**設定公用存取層級**。</span><span class="sxs-lookup"><span data-stu-id="5c587-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![設定公用存取層級內容功能表][13]
5. <span data-ttu-id="5c587-199">在 [hello**設定容器的公用存取層級**] 對話方塊中，指定所需的 hello 存取層級。</span><span class="sxs-lookup"><span data-stu-id="5c587-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![設定公用存取層級選項][14]
6. <span data-ttu-id="5c587-201">選取 [套用] 。</span><span class="sxs-lookup"><span data-stu-id="5c587-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="5c587-202">管理 blob 容器中的 blob</span><span class="sxs-lookup"><span data-stu-id="5c587-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="5c587-203">建立 blob 容器之後，您可以上傳 blob toothat blob 容器下載 blob tooyour 本機電腦、 開啟本機電腦，以及執行更多的 blob。</span><span class="sxs-lookup"><span data-stu-id="5c587-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="5c587-204">hello 下列步驟說明 toomanage 如何 hello blob （和資料夾） 內的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5c587-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="5c587-205">開啟儲存體 Explorer (預覽)。</span><span class="sxs-lookup"><span data-stu-id="5c587-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="5c587-206">Hello 左窗格中，展開包含您想 toomanage hello blob 容器的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c587-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="5c587-207">展開 hello 儲存體帳戶的**Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="5c587-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="5c587-208">按兩下您想 tooview hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5c587-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="5c587-209">hello 主窗格會顯示 hello blob 容器的內容。</span><span class="sxs-lookup"><span data-stu-id="5c587-209">hello main pane will display hello blob container's contents.</span></span>

   ![檢視 Blob 容器][3]
6. <span data-ttu-id="5c587-211">hello 主窗格會顯示 hello blob 容器的內容。</span><span class="sxs-lookup"><span data-stu-id="5c587-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="5c587-212">請遵循這些步驟視 hello 工作想 tooperform:</span><span class="sxs-lookup"><span data-stu-id="5c587-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="5c587-213">**上傳檔案 tooa blob 容器**</span><span class="sxs-lookup"><span data-stu-id="5c587-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="5c587-214">Hello 主窗格的工具列上，選取**上傳**，然後**上載檔案**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="5c587-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![上傳檔案功能表][15]
     2. <span data-ttu-id="5c587-216">在 hello**將檔案上傳**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**檔案**文字方塊想 tooupload tooselect hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="5c587-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![上傳檔案選項][16]
     3. <span data-ttu-id="5c587-218">指定 hello 類型**Blob 類型**。</span><span class="sxs-lookup"><span data-stu-id="5c587-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="5c587-219">hello 文章[開始使用適用於.NET 的 Azure Blob 儲存體使用](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts)說明 hello 差異 hello 各種 blob 類型。</span><span class="sxs-lookup"><span data-stu-id="5c587-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="5c587-220">選擇性地指定 hello 選取的檔案將會上傳到其中的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c587-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="5c587-221">如果 hello 目標資料夾不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="5c587-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="5c587-222">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="5c587-222">Select **Upload**.</span></span>
   * <span data-ttu-id="5c587-223">**上傳資料夾 tooa blob 容器**</span><span class="sxs-lookup"><span data-stu-id="5c587-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="5c587-224">Hello 主窗格的工具列上，選取**上傳**，然後**上傳資料夾**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="5c587-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![上傳資料夾功能表][17]
     2. <span data-ttu-id="5c587-226">在 hello**上傳資料夾**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**資料夾**文字方塊 tooselect hello 資料夾想 tooupload 其內容。</span><span class="sxs-lookup"><span data-stu-id="5c587-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![上傳資料夾選項][18]
     3. <span data-ttu-id="5c587-228">指定 hello 類型**Blob 類型**。</span><span class="sxs-lookup"><span data-stu-id="5c587-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="5c587-229">hello 文章[開始使用適用於.NET 的 Azure Blob 儲存體使用](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts)說明 hello 差異 hello 各種 blob 類型。</span><span class="sxs-lookup"><span data-stu-id="5c587-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="5c587-230">選擇性地指定所選的資料夾的內容將會上傳到哪個 hello 的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c587-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="5c587-231">如果 hello 目標資料夾不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="5c587-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="5c587-232">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="5c587-232">Select **Upload**.</span></span>
   * <span data-ttu-id="5c587-233">**下載 blob tooyour 本機電腦**</span><span class="sxs-lookup"><span data-stu-id="5c587-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="5c587-234">選取您想 toodownload hello blob。</span><span class="sxs-lookup"><span data-stu-id="5c587-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="5c587-235">在 hello 主窗格的工具列上，選取 **下載**。</span><span class="sxs-lookup"><span data-stu-id="5c587-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="5c587-236">在 [hello **toosave hello 下載 blob 的位置指定**] 對話方塊中，指定您要下載，hello blob 的 hello 位置和 hello 想 toogive 名稱它。</span><span class="sxs-lookup"><span data-stu-id="5c587-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="5c587-237">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="5c587-237">Select **Save**.</span></span>
   * <span data-ttu-id="5c587-238">**在您的本機電腦上開啟 blob**</span><span class="sxs-lookup"><span data-stu-id="5c587-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="5c587-239">選取您想 tooopen hello blob。</span><span class="sxs-lookup"><span data-stu-id="5c587-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="5c587-240">在 hello 主窗格的工具列上，選取 **開啟**。</span><span class="sxs-lookup"><span data-stu-id="5c587-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="5c587-241">hello blob 會下載，並使用 hello 與 hello blob 的基礎檔案類型相關聯的應用程式開啟。</span><span class="sxs-lookup"><span data-stu-id="5c587-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="5c587-242">**複製 blob toohello 剪貼簿**</span><span class="sxs-lookup"><span data-stu-id="5c587-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="5c587-243">選取您想 toocopy hello blob。</span><span class="sxs-lookup"><span data-stu-id="5c587-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="5c587-244">在 hello 主窗格的工具列上，選取 **複製**。</span><span class="sxs-lookup"><span data-stu-id="5c587-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="5c587-245">在 hello 左窗格中，瀏覽 tooanother blob 容器，然後按兩下該 tooview hello 主窗格中。</span><span class="sxs-lookup"><span data-stu-id="5c587-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="5c587-246">在 hello 主窗格的工具列上，選取 **貼上**toocreate hello blob 的複本。</span><span class="sxs-lookup"><span data-stu-id="5c587-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="5c587-247">**刪除 Blob**</span><span class="sxs-lookup"><span data-stu-id="5c587-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="5c587-248">選取您想 toodelete hello blob。</span><span class="sxs-lookup"><span data-stu-id="5c587-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="5c587-249">在 hello 主窗格的工具列上，選取 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="5c587-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="5c587-250">選取**是**toohello 確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c587-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c587-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c587-251">Next steps</span></span>
* <span data-ttu-id="5c587-252">檢視 hello[最新的存放裝置總管 （預覽） 版本資訊和視訊](http://www.storageexplorer.com)。</span><span class="sxs-lookup"><span data-stu-id="5c587-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="5c587-253">了解如何太[建立應用程式使用 Azure blob、 資料表、 佇列和檔案](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="5c587-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
