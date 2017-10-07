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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>變更 blob 路徑從 hello 預設路徑 （私人預覽中）

本文說明如何設定 Azure tooset 函式 toorename 預設 blob 檔案路徑。 

## <a name="prerequisites"></a>必要條件

請確定您有已在資源群組內的混合式資料資源中正確設定的作業定義。

## <a name="create-an-azure-function"></a>建立 Azure 函式

toocreate Azure 的函式，請勿 hello 遵循：

1. 移 toohello [Azure 入口網站](http://portal.azure.com/)。

2. 在 hello hello 左窗格頂端，按一下**新增**。 

3. 在 hello**搜尋**方塊中，輸入**函式應用程式**，然後按 Enter 鍵。

    ![Hello 搜尋方塊中輸入 「 函式應用程式 」](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. 在 hello**結果**清單中，按一下**函式應用程式**。

    ![選取在 hello 結果清單中的 hello 函式應用程式資源](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    hello**函式應用程式**視窗隨即開啟。

5. 按一下 [建立] 。

    ![hello 函式應用程式視窗的 [建立] 按鈕](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. 在 hello**函式應用程式**組態刀鋒視窗中，執行下列 hello:

    a. 在 [hello**應用程式名稱**] 方塊中，輸入 hello 應用程式名稱。
    
    b. 在 [hello**訂用帳戶**] 方塊中，輸入 hello 名稱 hello 訂用帳戶。

    c. 在下**資源群組**，按一下**建立新**，並接著類型 hello hello 資源群組的名稱。

    d. 在 hello**虛擬主機方案**方塊中，輸入**耗用量規劃**。

    e. 在 hello**位置**方塊中，型別 hello 位置。

    f. 在**儲存體帳戶**下選取現有的儲存體帳戶，或建立新的儲存體帳戶。 儲存體帳戶是在內部用 hello 函式。

    ![輸入新的函式應用程式組態資料](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. 按一下 [建立] 。  
    建立 hello 函式應用程式。

8. Hello 左窗格中，按一下 **更多服務**，並執行再 hello 遵循：
    
    a. 在 hello**篩選**方塊中，輸入**應用程式服務**。
    
    b. 按一下 [應用程式服務]。 

    ![Hello 左窗格中的 「 多個服務 」 連結](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. 在 [hello] 清單中的應用程式服務，hello hello 函式應用程式名稱。  
    hello 函式應用程式頁面隨即開啟。

10. Hello 左窗格中，按一下 **新函式**，並執行再 hello 遵循： 

    a. 在 hello**語言**清單中，選取**C#**。
    
    b. 在 hello 陣列範本並排顯示中，選取**QueueTrigger CSharp**。

    c. 在 hello**命名您的函式**方塊中，輸入您的函式的名稱。

    d. 在 hello**佇列名稱**方塊中，輸入您的資料轉換工作定義名稱。

    e. 在下**儲存體帳戶連接**，按一下 **新**，然後選取對應 toohello 資料轉換工作的 hello 帳戶。  
        記下 hello 連接名稱。 稍後在 hello Azure 函式需要 hello 的名稱。

       ![建立新的 C# 函式](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. 按一下 [建立] 。  
    hello**函式**視窗隨即開啟。

11. 在 hello**函式**視窗中，執行_.csx_檔案，並執行再 hello 遵循：

    a. 貼上下列程式碼的 hello:

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

    b. 使用您的儲存體帳戶連線，取代行 11 中的 **STORAGE_CONNECTIONNAME** (請參閱 8c)。

    c. 在 hello 左上方，按一下**儲存**。

    ![儲存函式](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete hello 函式，藉由 hello 下列加入多個檔案：

    a. 按一下 [檢視檔案]。

       ![hello [檢視檔案] 連結](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. 按一下 [新增]。
    
    c. 輸入 **project.json** 並按 Enter。
    
    d. 在 hello **project.json**檔案中，貼上下列程式碼的 hello:

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

    e. 按一下 [儲存] 。

您已建立 Azure 函式。 此函式就會觸發 hello 資料轉換作業會產生新的 blob 每一次。

## <a name="next-steps"></a>後續步驟

[使用 StorSimple 資料管理員 UI tootransform 您的資料](storsimple-data-manager-ui.md)
