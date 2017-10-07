---
title: "從 hello 預設 aaaChange blob 路徑 |Microsoft 文件"
description: "了解如何註冊 Azure tooset 函式 toorename 的 blob 檔案的路徑 （私人預覽中）"
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
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="862be-103">變更 blob 路徑從 hello 預設路徑 （私人預覽中）</span><span class="sxs-lookup"><span data-stu-id="862be-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="862be-104">本文說明如何設定 Azure tooset 函式 toorename 預設 blob 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="862be-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="862be-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="862be-105">Prerequisites</span></span>

<span data-ttu-id="862be-106">請確定您有已在資源群組內的混合式資料資源中正確設定的作業定義。</span><span class="sxs-lookup"><span data-stu-id="862be-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="862be-107">建立 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="862be-107">Create an Azure function</span></span>

<span data-ttu-id="862be-108">toocreate Azure 的函式，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="862be-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="862be-109">移 toohello [Azure 入口網站](http://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="862be-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="862be-110">在 hello hello 左窗格頂端，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="862be-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="862be-111">在 hello**搜尋**方塊中，輸入**函式應用程式**，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="862be-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Hello 搜尋方塊中輸入 「 函式應用程式 」](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="862be-113">在 hello**結果**清單中，按一下**函式應用程式**。</span><span class="sxs-lookup"><span data-stu-id="862be-113">In hello **Results** list, click **Function App**.</span></span>

    ![選取在 hello 結果清單中的 hello 函式應用程式資源](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="862be-115">hello**函式應用程式**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="862be-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="862be-116">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="862be-116">Click **Create**.</span></span>

    ![hello 函式應用程式視窗的 [建立] 按鈕](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="862be-118">在 hello**函式應用程式**組態刀鋒視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="862be-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="862be-119">a.</span><span class="sxs-lookup"><span data-stu-id="862be-119">a.</span></span> <span data-ttu-id="862be-120">在 [hello**應用程式名稱**] 方塊中，輸入 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="862be-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="862be-121">b.</span><span class="sxs-lookup"><span data-stu-id="862be-121">b.</span></span> <span data-ttu-id="862be-122">在 [hello**訂用帳戶**] 方塊中，輸入 hello 名稱 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="862be-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="862be-123">c.</span><span class="sxs-lookup"><span data-stu-id="862be-123">c.</span></span> <span data-ttu-id="862be-124">在下**資源群組**，按一下**建立新**，並接著類型 hello hello 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="862be-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="862be-125">d.</span><span class="sxs-lookup"><span data-stu-id="862be-125">d.</span></span> <span data-ttu-id="862be-126">在 hello**虛擬主機方案**方塊中，輸入**耗用量規劃**。</span><span class="sxs-lookup"><span data-stu-id="862be-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="862be-127">e.</span><span class="sxs-lookup"><span data-stu-id="862be-127">e.</span></span> <span data-ttu-id="862be-128">在 hello**位置**方塊中，型別 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="862be-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="862be-129">f.</span><span class="sxs-lookup"><span data-stu-id="862be-129">f.</span></span> <span data-ttu-id="862be-130">在**儲存體帳戶**下選取現有的儲存體帳戶，或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="862be-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="862be-131">儲存體帳戶是在內部用 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="862be-131">A storage account is used internally for hello function.</span></span>

    ![輸入新的函式應用程式組態資料](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="862be-133">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="862be-133">Click **Create**.</span></span>  
    <span data-ttu-id="862be-134">建立 hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="862be-134">hello function app is created.</span></span>

8. <span data-ttu-id="862be-135">Hello 左窗格中，按一下 **更多服務**，並執行再 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="862be-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="862be-136">a.</span><span class="sxs-lookup"><span data-stu-id="862be-136">a.</span></span> <span data-ttu-id="862be-137">在 hello**篩選**方塊中，輸入**應用程式服務**。</span><span class="sxs-lookup"><span data-stu-id="862be-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="862be-138">b.</span><span class="sxs-lookup"><span data-stu-id="862be-138">b.</span></span> <span data-ttu-id="862be-139">按一下 [應用程式服務]。</span><span class="sxs-lookup"><span data-stu-id="862be-139">Click **App Services**.</span></span> 

    ![Hello 左窗格中的 「 多個服務 」 連結](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="862be-141">在 [hello] 清單中的應用程式服務，hello hello 函式應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="862be-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="862be-142">hello 函式應用程式頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="862be-142">hello function app page opens.</span></span>

10. <span data-ttu-id="862be-143">Hello 左窗格中，按一下 **新函式**，並執行再 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="862be-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="862be-144">a.</span><span class="sxs-lookup"><span data-stu-id="862be-144">a.</span></span> <span data-ttu-id="862be-145">在 hello**語言**清單中，選取**C#**。</span><span class="sxs-lookup"><span data-stu-id="862be-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="862be-146">b.</span><span class="sxs-lookup"><span data-stu-id="862be-146">b.</span></span> <span data-ttu-id="862be-147">在 hello 陣列範本並排顯示中，選取**QueueTrigger CSharp**。</span><span class="sxs-lookup"><span data-stu-id="862be-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="862be-148">c.</span><span class="sxs-lookup"><span data-stu-id="862be-148">c.</span></span> <span data-ttu-id="862be-149">在 hello**命名您的函式**方塊中，輸入您的函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="862be-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="862be-150">d.</span><span class="sxs-lookup"><span data-stu-id="862be-150">d.</span></span> <span data-ttu-id="862be-151">在 hello**佇列名稱**方塊中，輸入您的資料轉換工作定義名稱。</span><span class="sxs-lookup"><span data-stu-id="862be-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="862be-152">e.</span><span class="sxs-lookup"><span data-stu-id="862be-152">e.</span></span> <span data-ttu-id="862be-153">在下**儲存體帳戶連接**，按一下 **新**，然後選取對應 toohello 資料轉換工作的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="862be-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="862be-154">記下 hello 連接名稱。</span><span class="sxs-lookup"><span data-stu-id="862be-154">Make a note of hello connection name.</span></span> <span data-ttu-id="862be-155">稍後在 hello Azure 函式需要 hello 的名稱。</span><span class="sxs-lookup"><span data-stu-id="862be-155">hello name is required later in hello Azure function.</span></span>

       ![建立新的 C# 函式](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="862be-157">f.</span><span class="sxs-lookup"><span data-stu-id="862be-157">f.</span></span> <span data-ttu-id="862be-158">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="862be-158">Click **Create**.</span></span>  
    <span data-ttu-id="862be-159">hello**函式**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="862be-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="862be-160">在 hello**函式**視窗中，執行_.csx_檔案，並執行再 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="862be-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="862be-161">a.</span><span class="sxs-lookup"><span data-stu-id="862be-161">a.</span></span> <span data-ttu-id="862be-162">貼上下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="862be-162">Paste hello following code:</span></span>

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

        // Create hello blob client.
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
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
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

    <span data-ttu-id="862be-163">b.</span><span class="sxs-lookup"><span data-stu-id="862be-163">b.</span></span> <span data-ttu-id="862be-164">使用您的儲存體帳戶連線，取代行 11 中的 **STORAGE_CONNECTIONNAME** (請參閱 8c)。</span><span class="sxs-lookup"><span data-stu-id="862be-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="862be-165">c.</span><span class="sxs-lookup"><span data-stu-id="862be-165">c.</span></span> <span data-ttu-id="862be-166">在 hello 左上方，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="862be-166">At hello top left, click **Save**.</span></span>

    ![儲存函式](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="862be-168">toocomplete hello 函式，藉由 hello 下列加入多個檔案：</span><span class="sxs-lookup"><span data-stu-id="862be-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="862be-169">a.</span><span class="sxs-lookup"><span data-stu-id="862be-169">a.</span></span> <span data-ttu-id="862be-170">按一下 [檢視檔案]。</span><span class="sxs-lookup"><span data-stu-id="862be-170">Click **View files**.</span></span>

       ![hello [檢視檔案] 連結](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="862be-172">b.</span><span class="sxs-lookup"><span data-stu-id="862be-172">b.</span></span> <span data-ttu-id="862be-173">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="862be-173">Click **Add**.</span></span>
    
    <span data-ttu-id="862be-174">c.</span><span class="sxs-lookup"><span data-stu-id="862be-174">c.</span></span> <span data-ttu-id="862be-175">輸入 **project.json** 並按 Enter。</span><span class="sxs-lookup"><span data-stu-id="862be-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="862be-176">d.</span><span class="sxs-lookup"><span data-stu-id="862be-176">d.</span></span> <span data-ttu-id="862be-177">在 hello **project.json**檔案中，貼上下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="862be-177">In hello **project.json** file, paste hello following code:</span></span>

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

    <span data-ttu-id="862be-178">e.</span><span class="sxs-lookup"><span data-stu-id="862be-178">e.</span></span> <span data-ttu-id="862be-179">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="862be-179">Click **Save**.</span></span>

<span data-ttu-id="862be-180">您已建立 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="862be-180">You have created an Azure function.</span></span> <span data-ttu-id="862be-181">此函式就會觸發 hello 資料轉換作業會產生新的 blob 每一次。</span><span class="sxs-lookup"><span data-stu-id="862be-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="862be-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="862be-182">Next steps</span></span>

[<span data-ttu-id="862be-183">使用 StorSimple 資料管理員 UI tootransform 您的資料</span><span class="sxs-lookup"><span data-stu-id="862be-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
