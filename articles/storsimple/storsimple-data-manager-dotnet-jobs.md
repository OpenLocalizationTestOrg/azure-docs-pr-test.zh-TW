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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="acbb3-103">使用 hello.Net SDK tooinitiate 資料轉換 （私人預覽中）</span><span class="sxs-lookup"><span data-stu-id="acbb3-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="acbb3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="acbb3-104">Overview</span></span>

<span data-ttu-id="acbb3-105">本文說明如何使用 hello StorSimple Data Manager 服務 tootransform StorSimple 裝置資料中的 hello 資料轉換功能。</span><span class="sxs-lookup"><span data-stu-id="acbb3-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="acbb3-106">hello 已轉換的資料然後供 hello 雲端中的其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="acbb3-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="acbb3-107">hello 發行項也必須建立範例.NET 主控台應用程式 tooinitiate 資料轉換工作，然後將它追蹤完成逐步解說 toohelp。</span><span class="sxs-lookup"><span data-stu-id="acbb3-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acbb3-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="acbb3-108">Prerequisites</span></span>

<span data-ttu-id="acbb3-109">開始之前，請確定您有︰</span><span class="sxs-lookup"><span data-stu-id="acbb3-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="acbb3-110">已安裝 Visual Studio 2012、2013、2015 或 2017 的系統。</span><span class="sxs-lookup"><span data-stu-id="acbb3-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="acbb3-111">已安裝 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="acbb3-111">Azure Powershell installed.</span></span> <span data-ttu-id="acbb3-112">[下載 Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="acbb3-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="acbb3-113">組態設定 tooinitialize hello 資料轉換工作 （tooobtain 這些設定會包含在此處的指示）。</span><span class="sxs-lookup"><span data-stu-id="acbb3-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="acbb3-114">已在資源群組內的混合式資料資源中正確設定的作業定義。</span><span class="sxs-lookup"><span data-stu-id="acbb3-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="acbb3-115">所有必要的 hello dll。</span><span class="sxs-lookup"><span data-stu-id="acbb3-115">All hello required dlls.</span></span> <span data-ttu-id="acbb3-116">從 hello 下載這些 dll [GitHub 儲存機制](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls)。</span><span class="sxs-lookup"><span data-stu-id="acbb3-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="acbb3-117">`Get-ConfigurationParams.ps1`[指令碼](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1)hello github 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="acbb3-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="acbb3-118">逐步說明</span><span class="sxs-lookup"><span data-stu-id="acbb3-118">Step-by-step</span></span>

<span data-ttu-id="acbb3-119">執行下列步驟 toouse.NET toolaunch 資料轉換工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="acbb3-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="acbb3-120">tooretrieve hello 組態參數，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="acbb3-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="acbb3-121">下載 hello`Get-ConfigurationParams.ps1`中的 hello github 儲存機制指令碼的`C:\DataTransformation`位置。</span><span class="sxs-lookup"><span data-stu-id="acbb3-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="acbb3-122">執行 hello `Get-ConfigurationParams.ps1` hello github 儲存機制中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="acbb3-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="acbb3-123">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="acbb3-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="acbb3-124">您可以傳遞所有的值為 hello ActiveDirectoryKey 和應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="acbb3-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="acbb3-125">此指令碼輸出 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="acbb3-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="acbb3-126">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="acbb3-126">Client ID</span></span>
    * <span data-ttu-id="acbb3-127">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="acbb3-127">Tenant ID</span></span>
    * <span data-ttu-id="acbb3-128">Active Directory 金鑰 （相同 hello 上面輸入的其中一個）</span><span class="sxs-lookup"><span data-stu-id="acbb3-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="acbb3-129">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="acbb3-129">Subscription ID</span></span>

3. <span data-ttu-id="acbb3-130">使用 Visual Studio 2012、2013 或 2015 建立 C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="acbb3-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="acbb3-131">啟動 **Visual Studio 2012/2013/2015**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="acbb3-132">按一下**檔案**，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="acbb3-133">展開 [範本]，然後選取 [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="acbb3-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="acbb3-134">選取**主控台應用程式**從 hello hello 右上的專案類型清單。</span><span class="sxs-lookup"><span data-stu-id="acbb3-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="acbb3-135">輸入**DataTransformationApp** hello**名稱**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="acbb3-136">選取**C:\DataTransformation** hello**位置**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="acbb3-137">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="acbb3-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="acbb3-138">現在，加入所有 Dll 位於 hello [dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls)資料夾**參考**hello 專案中，您所建立。</span><span class="sxs-lookup"><span data-stu-id="acbb3-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="acbb3-139">toodownload hello dll 檔案，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="acbb3-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="acbb3-140">在 Visual Studio 中，移過**檢視 > 方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="acbb3-141">按一下 hello 箭號 toohello 左邊的資料轉換應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="acbb3-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="acbb3-142">按一下**參考**然後以滑鼠右鍵按一下太**加入參考**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="acbb3-143">瀏覽 toohello hello 封裝資料夾位置，選取所有 hello Dll 並按一下**新增**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="acbb3-144">新增下列 hello**使用**陳述式 toohello 原始程式檔 (Program.cs) hello 專案中的。</span><span class="sxs-lookup"><span data-stu-id="acbb3-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="acbb3-145">下列程式碼的 hello 初始化 hello 資料轉換工作的執行個體。</span><span class="sxs-lookup"><span data-stu-id="acbb3-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="acbb3-146">此增益集 hello **Main 方法**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="acbb3-147">Hello 如稍早取得的設定參數的值取代。</span><span class="sxs-lookup"><span data-stu-id="acbb3-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="acbb3-148">中的 hello 值插入**資源群組名稱**和**混合式資料的資源名稱**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="acbb3-149">hello**資源群組名稱**為 hello 裝載 hello 混合式資料資源的 hello 已設定的工作定義的其中一個。</span><span class="sxs-lookup"><span data-stu-id="acbb3-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

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

7. <span data-ttu-id="acbb3-150">指定使用哪一個 hello 工作定義需要 toobe 參數執行的 hello</span><span class="sxs-lookup"><span data-stu-id="acbb3-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="acbb3-151">(或)</span><span class="sxs-lookup"><span data-stu-id="acbb3-151">(OR)</span></span>

    <span data-ttu-id="acbb3-152">如果您想在執行階段期間的 toochange hello 工作定義參數，然後加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="acbb3-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

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

8. <span data-ttu-id="acbb3-153">Hello 初始化之後，加入下列程式碼 tootrigger hello 工作定義的資料轉換作業的 hello。</span><span class="sxs-lookup"><span data-stu-id="acbb3-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="acbb3-154">插入適當的 hello**工作定義名稱**。</span><span class="sxs-lookup"><span data-stu-id="acbb3-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="acbb3-155">這項作業將上傳 hello 根目錄 hello StorSimple 磁碟區 toohello 指定容器下存在的比對的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="acbb3-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="acbb3-156">Hello 佇列中上傳檔案時，就會捨棄訊息 (hello 在 hello 容器相同儲存體帳戶) 與 hello 相同的名稱，為 hello 工作定義。</span><span class="sxs-lookup"><span data-stu-id="acbb3-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="acbb3-157">這則訊息可以當做觸發程序 tooinitiate hello 檔案的任何進一步處理。</span><span class="sxs-lookup"><span data-stu-id="acbb3-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="acbb3-158">一旦已觸發 hello 作業，加入下列程式碼 tootrack hello 作業完成的 hello。</span><span class="sxs-lookup"><span data-stu-id="acbb3-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="acbb3-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acbb3-159">Next steps</span></span>

<span data-ttu-id="acbb3-160">[您的資料使用 StorSimple 資料管理員 UI tootransform](storsimple-data-manager-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="acbb3-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
