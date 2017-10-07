---
title: "Microsoft Azure StorSimple Data Manager 作業 aaaUse.NET SDK |Microsoft 文件"
description: "了解如何 toouse.NET SDK toolaunch StorSimple Data Manager 作業 （私人預覽中）"
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
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>使用 hello.Net SDK tooinitiate 資料轉換 （私人預覽中）

## <a name="overview"></a>概觀

本文說明如何使用 hello StorSimple Data Manager 服務 tootransform StorSimple 裝置資料中的 hello 資料轉換功能。 hello 已轉換的資料然後供 hello 雲端中的其他 Azure 服務。 hello 發行項也必須建立範例.NET 主控台應用程式 tooinitiate 資料轉換工作，然後將它追蹤完成逐步解說 toohelp。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您有︰
*   已安裝 Visual Studio 2012、2013、2015 或 2017 的系統。
*   已安裝 Azure Powershell。 [下載 Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。
*   組態設定 tooinitialize hello 資料轉換工作 （tooobtain 這些設定會包含在此處的指示）。
*   已在資源群組內的混合式資料資源中正確設定的作業定義。
*   所有必要的 hello dll。 從 hello 下載這些 dll [GitHub 儲存機制](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls)。
*   `Get-ConfigurationParams.ps1`[指令碼](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1)hello github 儲存機制中。

## <a name="step-by-step"></a>逐步說明

執行下列步驟 toouse.NET toolaunch 資料轉換工作的 hello。

1. tooretrieve hello 組態參數，下列步驟 hello:
    1. 下載 hello`Get-ConfigurationParams.ps1`中的 hello github 儲存機制指令碼的`C:\DataTransformation`位置。
    1. 執行 hello `Get-ConfigurationParams.ps1` hello github 儲存機制中的指令碼。 輸入下列命令的 hello:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        您可以傳遞所有的值為 hello ActiveDirectoryKey 和應用程式名稱。


2. 此指令碼輸出 hello 下列值：
    * 用戶端識別碼
    * 租用戶識別碼
    * Active Directory 金鑰 （相同 hello 上面輸入的其中一個）
    * 訂用帳戶識別碼

3. 使用 Visual Studio 2012、2013 或 2015 建立 C# .NET 主控台應用程式。

    1. 啟動 **Visual Studio 2012/2013/2015**。
    1. 按一下**檔案**，點太**新增**，然後按一下**專案**。
    2. 展開 [範本]，然後選取 [Visual C#]。
    3. 選取**主控台應用程式**從 hello hello 右上的專案類型清單。
    4. 輸入**DataTransformationApp** hello**名稱**。
    5. 選取**C:\DataTransformation** hello**位置**。
    6. 按一下**確定**toocreate hello 專案。

4.  現在，加入所有 Dll 位於 hello [dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls)資料夾**參考**hello 專案中，您所建立。 toodownload hello dll 檔案，請勿 hello 遵循：

    1. 在 Visual Studio 中，移過**檢視 > 方案總管 中**。
    1. 按一下 hello 箭號 toohello 左邊的資料轉換應用程式專案。 按一下**參考**然後以滑鼠右鍵按一下太**加入參考**。
    2. 瀏覽 toohello hello 封裝資料夾位置，選取所有 hello Dll 並按一下**新增**，然後按一下**確定**。

5. 新增下列 hello**使用**陳述式 toohello 原始程式檔 (Program.cs) hello 專案中的。

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. 下列程式碼的 hello 初始化 hello 資料轉換工作的執行個體。 此增益集 hello **Main 方法**。 Hello 如稍早取得的設定參數的值取代。 中的 hello 值插入**資源群組名稱**和**混合式資料的資源名稱**。 hello**資源群組名稱**為 hello 裝載 hello 混合式資料資源的 hello 已設定的工作定義的其中一個。

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. 指定使用哪一個 hello 工作定義需要 toobe 參數執行的 hello

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    (或)

    如果您想在執行階段期間的 toochange hello 工作定義參數，然後加入下列程式碼的 hello:

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. Hello 初始化之後，加入下列程式碼 tootrigger hello 工作定義的資料轉換作業的 hello。 插入適當的 hello**工作定義名稱**。

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. 這項作業將上傳 hello 根目錄 hello StorSimple 磁碟區 toohello 指定容器下存在的比對的 hello 檔案。 Hello 佇列中上傳檔案時，就會捨棄訊息 (hello 在 hello 容器相同儲存體帳戶) 與 hello 相同的名稱，為 hello 工作定義。 這則訊息可以當做觸發程序 tooinitiate hello 檔案的任何進一步處理。

10. 一旦已觸發 hello 作業，加入下列程式碼 tootrack hello 作業完成的 hello。

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a>後續步驟

[您的資料使用 StorSimple 資料管理員 UI tootransform](storsimple-data-manager-ui.md)。
