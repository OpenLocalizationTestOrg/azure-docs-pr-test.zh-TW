---
title: "變更預設的 Blob 路徑 | Microsoft Docs"
description: "了解如何設定 Azure 函式來重新命名 Blob 檔案路徑 (私人預覽)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="b63a7-103">變更預設的 Blob 路徑 (私人預覽)</span><span class="sxs-lookup"><span data-stu-id="b63a7-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="b63a7-104">此文章說明如何設定 Azure 函式來重新命名預設的 Blob 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="b63a7-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b63a7-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="b63a7-105">Prerequisites</span></span>

<span data-ttu-id="b63a7-106">請確定您有已在資源群組內的混合式資料資源中正確設定的作業定義。</span><span class="sxs-lookup"><span data-stu-id="b63a7-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="b63a7-107">建立 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="b63a7-107">Create an Azure function</span></span>

<span data-ttu-id="b63a7-108">若要建立 Azure 函式，請執行以下步驟：</span><span class="sxs-lookup"><span data-stu-id="b63a7-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="b63a7-109">移至 [Azure 入口網站](http://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b63a7-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="b63a7-110">在左窗格頂端按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b63a7-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="b63a7-111">在 [搜尋] 方塊中輸入**函式應用程式**，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b63a7-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![在 [搜尋] 方塊中輸入「函式應用程式」](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="b63a7-113">在**結果**清單中按一下 [函式應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b63a7-113">In the **Results** list, click **Function App**.</span></span>

    ![在結果清單中選取函式應用程式資源](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="b63a7-115">[函式應用程式] 視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b63a7-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="b63a7-116">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b63a7-116">Click **Create**.</span></span>

    ![函式應用程式視窗的 [建立] 按鈕](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="b63a7-118">在 [函式應用程式] 組態刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="b63a7-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="b63a7-119">a.</span><span class="sxs-lookup"><span data-stu-id="b63a7-119">a.</span></span> <span data-ttu-id="b63a7-120">在 [應用程式名稱] 方塊中輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="b63a7-121">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b63a7-121">b.</span></span> <span data-ttu-id="b63a7-122">在 [訂用帳戶] 方塊中輸入訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="b63a7-123">c.</span><span class="sxs-lookup"><span data-stu-id="b63a7-123">c.</span></span> <span data-ttu-id="b63a7-124">在**資源群組**下，按一下 [建立新項目]，然後輸入資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="b63a7-125">d.</span><span class="sxs-lookup"><span data-stu-id="b63a7-125">d.</span></span> <span data-ttu-id="b63a7-126">在 [主控方案] 方塊中輸入**取用方案**。</span><span class="sxs-lookup"><span data-stu-id="b63a7-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="b63a7-127">e.</span><span class="sxs-lookup"><span data-stu-id="b63a7-127">e.</span></span> <span data-ttu-id="b63a7-128">在 [位置]方塊中輸入位置。</span><span class="sxs-lookup"><span data-stu-id="b63a7-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="b63a7-129">f.</span><span class="sxs-lookup"><span data-stu-id="b63a7-129">f.</span></span> <span data-ttu-id="b63a7-130">在**儲存體帳戶**下選取現有的儲存體帳戶，或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b63a7-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="b63a7-131">儲存體帳戶會在內部針對函式使用。</span><span class="sxs-lookup"><span data-stu-id="b63a7-131">A storage account is used internally for the function.</span></span>

    ![輸入新的函式應用程式組態資料](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="b63a7-133">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b63a7-133">Click **Create**.</span></span>  
    <span data-ttu-id="b63a7-134">函式應用程式隨即建立。</span><span class="sxs-lookup"><span data-stu-id="b63a7-134">The function app is created.</span></span>

8. <span data-ttu-id="b63a7-135">在左窗格中，按一下 [更多服務]，然後執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="b63a7-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="b63a7-136">a.</span><span class="sxs-lookup"><span data-stu-id="b63a7-136">a.</span></span> <span data-ttu-id="b63a7-137">在 [篩選] 方塊中輸入**應用程式服務**。</span><span class="sxs-lookup"><span data-stu-id="b63a7-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="b63a7-138">b.</span><span class="sxs-lookup"><span data-stu-id="b63a7-138">b.</span></span> <span data-ttu-id="b63a7-139">按一下 [應用程式服務]。</span><span class="sxs-lookup"><span data-stu-id="b63a7-139">Click **App Services**.</span></span> 

    ![在左側窗格中，選取 [更多服務]](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="b63a7-141">在應用程式服務的清單中，按一下函式應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="b63a7-142">函式應用程式頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b63a7-142">The function app page opens.</span></span>

10. <span data-ttu-id="b63a7-143">在左窗格中，按一下 [新函式]，然後執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="b63a7-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="b63a7-144">a.</span><span class="sxs-lookup"><span data-stu-id="b63a7-144">a.</span></span> <span data-ttu-id="b63a7-145">在**語言**清單中，選取 **C#**。</span><span class="sxs-lookup"><span data-stu-id="b63a7-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="b63a7-146">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b63a7-146">b.</span></span> <span data-ttu-id="b63a7-147">在範本圖格的陣列中，選取 **QueueTrigger CSharp**。</span><span class="sxs-lookup"><span data-stu-id="b63a7-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="b63a7-148">c.</span><span class="sxs-lookup"><span data-stu-id="b63a7-148">c.</span></span> <span data-ttu-id="b63a7-149">在 [為您的函式命名] 方塊中，輸入您函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="b63a7-150">d.</span><span class="sxs-lookup"><span data-stu-id="b63a7-150">d.</span></span> <span data-ttu-id="b63a7-151">在 [佇列名稱]方塊中，輸入您的資料轉換作業定義名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="b63a7-152">e.</span><span class="sxs-lookup"><span data-stu-id="b63a7-152">e.</span></span> <span data-ttu-id="b63a7-153">在**儲存體帳戶連線**下，按一下 [新增]，然後選取對應至資料轉換作業的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b63a7-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="b63a7-154">記下連線名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-154">Make a note of the connection name.</span></span> <span data-ttu-id="b63a7-155">稍後在 Azure 函式中需要此名稱。</span><span class="sxs-lookup"><span data-stu-id="b63a7-155">The name is required later in the Azure function.</span></span>

       ![建立新的 C# 函式](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="b63a7-157">f.</span><span class="sxs-lookup"><span data-stu-id="b63a7-157">f.</span></span> <span data-ttu-id="b63a7-158">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b63a7-158">Click **Create**.</span></span>  
    <span data-ttu-id="b63a7-159">[函式] 視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b63a7-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="b63a7-160">在 [函式]視窗中，執行 _.csx_ 檔案，並接著執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="b63a7-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="b63a7-161">a.</span><span class="sxs-lookup"><span data-stu-id="b63a7-161">a.</span></span> <span data-ttu-id="b63a7-162">貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b63a7-162">Paste the following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create the blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="b63a7-163">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b63a7-163">b.</span></span> <span data-ttu-id="b63a7-164">使用您的儲存體帳戶連線，取代行 11 中的 **STORAGE_CONNECTIONNAME** (請參閱 8c)。</span><span class="sxs-lookup"><span data-stu-id="b63a7-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="b63a7-165">c.</span><span class="sxs-lookup"><span data-stu-id="b63a7-165">c.</span></span> <span data-ttu-id="b63a7-166">按一下左上角的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b63a7-166">At the top left, click **Save**.</span></span>

    ![儲存函式](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="b63a7-168">若要完成此函式，請透過執行以下動作再新增一個檔案︰</span><span class="sxs-lookup"><span data-stu-id="b63a7-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="b63a7-169">a.</span><span class="sxs-lookup"><span data-stu-id="b63a7-169">a.</span></span> <span data-ttu-id="b63a7-170">按一下 [檢視檔案]。</span><span class="sxs-lookup"><span data-stu-id="b63a7-170">Click **View files**.</span></span>

       ![[檢視檔案] 連結](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="b63a7-172">b.</span><span class="sxs-lookup"><span data-stu-id="b63a7-172">b.</span></span> <span data-ttu-id="b63a7-173">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b63a7-173">Click **Add**.</span></span>
    
    <span data-ttu-id="b63a7-174">c.</span><span class="sxs-lookup"><span data-stu-id="b63a7-174">c.</span></span> <span data-ttu-id="b63a7-175">輸入 **project.json** 並按 Enter。</span><span class="sxs-lookup"><span data-stu-id="b63a7-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="b63a7-176">d.</span><span class="sxs-lookup"><span data-stu-id="b63a7-176">d.</span></span> <span data-ttu-id="b63a7-177">在 **project.json** 檔案中貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b63a7-177">In the **project.json** file, paste the following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="b63a7-178">e.</span><span class="sxs-lookup"><span data-stu-id="b63a7-178">e.</span></span> <span data-ttu-id="b63a7-179">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b63a7-179">Click **Save**.</span></span>

<span data-ttu-id="b63a7-180">您已建立 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="b63a7-180">You have created an Azure function.</span></span> <span data-ttu-id="b63a7-181">每一次資料轉換作業產生新的 Blob，都會觸發此函式。</span><span class="sxs-lookup"><span data-stu-id="b63a7-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b63a7-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b63a7-182">Next steps</span></span>

[<span data-ttu-id="b63a7-183">使用 StorSimple Data Manager UI 來轉換資料</span><span class="sxs-lookup"><span data-stu-id="b63a7-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
