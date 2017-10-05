---
title: "使用 .NET SDK 執行 Microsoft Azure StorSimple Data Manager 作業 | Microsoft Docs"
description: "了解如何使用 .NET SDK 啟動 StorSimple Data Manager 作業 (私人預覽)"
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
ms.openlocfilehash: 44d243a034b20b99faf284c8615e470bc6f9d020
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-net-sdk-to-initiate-data-transformation-private-preview"></a><span data-ttu-id="96774-103">使用 .Net SDK 起始資料轉換 (私人預覽)</span><span class="sxs-lookup"><span data-stu-id="96774-103">Use the .Net SDK to initiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="96774-104">概觀</span><span class="sxs-lookup"><span data-stu-id="96774-104">Overview</span></span>

<span data-ttu-id="96774-105">本文說明如何使用 StorSimple Data Manager 服務中的資料轉換功能來轉換 StorSimple 裝置資料。</span><span class="sxs-lookup"><span data-stu-id="96774-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span></span> <span data-ttu-id="96774-106">轉換後的資料由雲端中的其他 Azure 服務取用。</span><span class="sxs-lookup"><span data-stu-id="96774-106">The transformed data is then consumed by other Azure services in the cloud.</span></span> <span data-ttu-id="96774-107">本文也提供逐步解說，協助建立範例 .NET 主控台應用程式來起始資料轉換作業，然後追蹤到完成為止。</span><span class="sxs-lookup"><span data-stu-id="96774-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96774-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="96774-108">Prerequisites</span></span>

<span data-ttu-id="96774-109">開始之前，請確定您有︰</span><span class="sxs-lookup"><span data-stu-id="96774-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="96774-110">已安裝 Visual Studio 2012、2013、2015 或 2017 的系統。</span><span class="sxs-lookup"><span data-stu-id="96774-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="96774-111">已安裝 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="96774-111">Azure Powershell installed.</span></span> <span data-ttu-id="96774-112">[下載 Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="96774-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="96774-113">用於初始化資料轉換作業的組態設定 (這裡包含取得這些設定的指示)。</span><span class="sxs-lookup"><span data-stu-id="96774-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="96774-114">已在資源群組內的混合式資料資源中正確設定的作業定義。</span><span class="sxs-lookup"><span data-stu-id="96774-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="96774-115">所有必要的 dll。</span><span class="sxs-lookup"><span data-stu-id="96774-115">All the required dlls.</span></span> <span data-ttu-id="96774-116">從 [GitHub 儲存機制](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls)下載這些 dll。</span><span class="sxs-lookup"><span data-stu-id="96774-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="96774-117">Github 儲存機制中的 `Get-ConfigurationParams.ps1` [指令碼](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1)。</span><span class="sxs-lookup"><span data-stu-id="96774-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="96774-118">逐步說明</span><span class="sxs-lookup"><span data-stu-id="96774-118">Step-by-step</span></span>

<span data-ttu-id="96774-119">執行下列步驟，以使用 .NET 啟動資料轉換作業。</span><span class="sxs-lookup"><span data-stu-id="96774-119">Perform the following steps to use .NET to launch a data transformation job.</span></span>

1. <span data-ttu-id="96774-120">若要擷取設定參數，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="96774-120">To retrieve the configuration parameters, do the following steps:</span></span>
    1. <span data-ttu-id="96774-121">將 github 儲存機制中的 `Get-ConfigurationParams.ps1` 指令碼下載到 `C:\DataTransformation` 位置。</span><span class="sxs-lookup"><span data-stu-id="96774-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="96774-122">執行 github 儲存機制中的 `Get-ConfigurationParams.ps1` 指令碼。</span><span class="sxs-lookup"><span data-stu-id="96774-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span></span> <span data-ttu-id="96774-123">輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="96774-123">Type the following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="96774-124">您可以傳入任何值給 ActiveDirectoryKey 和 AppName。</span><span class="sxs-lookup"><span data-stu-id="96774-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="96774-125">此指令碼會輸出下列值：</span><span class="sxs-lookup"><span data-stu-id="96774-125">This script outputs the following values:</span></span>
    * <span data-ttu-id="96774-126">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="96774-126">Client ID</span></span>
    * <span data-ttu-id="96774-127">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="96774-127">Tenant ID</span></span>
    * <span data-ttu-id="96774-128">Active Directory 金鑰 (與上面輸入的金鑰相同)</span><span class="sxs-lookup"><span data-stu-id="96774-128">Active Directory key (same as the one entered above)</span></span>
    * <span data-ttu-id="96774-129">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="96774-129">Subscription ID</span></span>

3. <span data-ttu-id="96774-130">使用 Visual Studio 2012、2013 或 2015 建立 C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="96774-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="96774-131">啟動 **Visual Studio 2012/2013/2015**。</span><span class="sxs-lookup"><span data-stu-id="96774-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="96774-132">按一下 [檔案]，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="96774-132">Click **File**, point to **New**, and click **Project**.</span></span>
    2. <span data-ttu-id="96774-133">展開 [範本]，然後選取 [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="96774-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="96774-134">從右邊的專案類型清單中選取 [主控台應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="96774-134">Select **Console Application** from the list of project types on the right.</span></span>
    4. <span data-ttu-id="96774-135">輸入 **DataTransformationApp** 做為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="96774-135">Enter **DataTransformationApp** for the **Name**.</span></span>
    5. <span data-ttu-id="96774-136">選取 **C:\DataTransformation** 做為 [位置]。</span><span class="sxs-lookup"><span data-stu-id="96774-136">Select **C:\DataTransformation** for the **Location**.</span></span>
    6. <span data-ttu-id="96774-137">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="96774-137">Click **OK** to create the project.</span></span>

4.  <span data-ttu-id="96774-138">現在，在您建立的專案中，將 [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) 資料夾中出現的所有 DLL 新增為 [參考]。</span><span class="sxs-lookup"><span data-stu-id="96774-138">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span></span> <span data-ttu-id="96774-139">若要下載 dll 檔，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="96774-139">To download the dll files, do the following:</span></span>

    1. <span data-ttu-id="96774-140">在 Visual Studio 中，移至 [檢視] > [方案總管]。</span><span class="sxs-lookup"><span data-stu-id="96774-140">In Visual Studio, go to **View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="96774-141">按一下資料轉換應用程式專案左邊的箭號。</span><span class="sxs-lookup"><span data-stu-id="96774-141">Click the arrow to the left of Data Transformation App project.</span></span> <span data-ttu-id="96774-142">按一下 [參考]，然後按一下滑鼠右鍵以 [新增參考]。</span><span class="sxs-lookup"><span data-stu-id="96774-142">Click **References** and then right-click to **Add Reference**.</span></span>
    2. <span data-ttu-id="96774-143">瀏覽至套件資料夾的位置，選取所有 DLL，按一下 [新增]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="96774-143">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="96774-144">將下列 **using** 陳述式加入專案的原始程式檔 (Program.cs) 中。</span><span class="sxs-lookup"><span data-stu-id="96774-144">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="96774-145">下列程式碼會初始化資料轉換作業執行個體。</span><span class="sxs-lookup"><span data-stu-id="96774-145">The following code initializes the data transformation job instance.</span></span> <span data-ttu-id="96774-146">請將這段程式碼新增至 **Main 方法** 中。</span><span class="sxs-lookup"><span data-stu-id="96774-146">Add this in the **Main method**.</span></span> <span data-ttu-id="96774-147">取代先前取得的設定參數值。</span><span class="sxs-lookup"><span data-stu-id="96774-147">Replace the values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="96774-148">插入**資源群組名稱**和**混合式資料資源名稱**的值。</span><span class="sxs-lookup"><span data-stu-id="96774-148">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="96774-149">**資源群組名稱**裝載用於設定作業定義的混合式資料資源。</span><span class="sxs-lookup"><span data-stu-id="96774-149">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span></span>

    ```
    // Setup the configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize the Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="96774-150">指定執行作業定義所需的參數</span><span class="sxs-lookup"><span data-stu-id="96774-150">Specify the parameters with which the job definition needs to be run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="96774-151">(或)</span><span class="sxs-lookup"><span data-stu-id="96774-151">(OR)</span></span>

    <span data-ttu-id="96774-152">如果您想要在執行階段變更作業定義參數，請新增下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="96774-152">If you want to change the job definition parameters during run time, then add the following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of the volume on the StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require the latest existing backup to be picked else use TakeNow to trigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of the StorSimple device.
        DeviceName = "device-name",
        // Name of the container in Azure storage where the files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) to be applied on files under the root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of the volume on StorSimple device on which the relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="96774-153">初始化之後，在作業定義上新增下列程式碼來觸發資料轉換作業。</span><span class="sxs-lookup"><span data-stu-id="96774-153">After the initialization, add the following code to trigger a data transformation job on the job definition.</span></span> <span data-ttu-id="96774-154">插入適當的**作業定義名稱**。</span><span class="sxs-lookup"><span data-stu-id="96774-154">Plug in the appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve the jobId and the retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="96774-155">這項作業會將 StorSimple 磁碟區的根目錄底下相符的檔案上傳至指定的容器。</span><span class="sxs-lookup"><span data-stu-id="96774-155">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span></span> <span data-ttu-id="96774-156">上傳檔案時，佇列 (位於與容器相同的儲存體帳戶) 中會放入一則與作業定義同名的訊息。</span><span class="sxs-lookup"><span data-stu-id="96774-156">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span></span> <span data-ttu-id="96774-157">此訊息可做為觸發程序，以起始檔案的任何進一步處理。</span><span class="sxs-lookup"><span data-stu-id="96774-157">This message can be used as a trigger to initiate any further processing of the file.</span></span>

10. <span data-ttu-id="96774-158">觸發作業後，請新增下列程式碼來追蹤作業是否完成。</span><span class="sxs-lookup"><span data-stu-id="96774-158">Once the job has been triggered, add the following code to track the job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll the job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for the status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of the job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // To hold the console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="96774-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96774-159">Next steps</span></span>

<span data-ttu-id="96774-160">[使用 StorSimple Data Manager UI 來轉換資料](storsimple-data-manager-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="96774-160">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
