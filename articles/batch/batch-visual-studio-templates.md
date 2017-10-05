---
title: "使用 Visual Studio 專案範本開始建置 Batch 解決方案 - Azure | Microsoft Docs"
description: "了解 Visual Studio 專案範本如何協助您在 Azure Batch 中實作和執行計算密集型工作負載。"
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: da77ce827c65deb18d9d84ce5cf768d89788e205
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-project-templates-to-jump-start-batch-solutions"></a><span data-ttu-id="f9dae-103">使用 Visual Studio 專案範本快速啟動 Batch 解決方案</span><span class="sxs-lookup"><span data-stu-id="f9dae-103">Use Visual Studio project templates to jump-start Batch solutions</span></span>

<span data-ttu-id="f9dae-104">Batch 的**作業管理員**和**工作處理器 Visual Studio 範本**提供了程式碼，協助您以最少的心力在 Batch 上實作並執行計算密集型工作負載。</span><span class="sxs-lookup"><span data-stu-id="f9dae-104">The **Job Manager** and **Task Processor Visual Studio templates** for Batch provide code to help you to implement and run your compute-intensive workloads on Batch with the least amount of effort.</span></span> <span data-ttu-id="f9dae-105">本文件會說明這些範本，並提供其使用方式指引。</span><span class="sxs-lookup"><span data-stu-id="f9dae-105">This document describes these templates and provides guidance for how to use them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9dae-106">本文只討論適用於這兩個範本的資訊，並假設您熟悉與其相關的 Batch 服務和重要概念︰集區、計算節點、作業和工作、作業管理員工作、環境變數和其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dae-106">This article discusses only information applicable to these two templates, and assumes that you are familiar with the Batch service and key concepts related to it: pools, compute nodes, jobs and tasks, job manager tasks, environment variables, and other relevant information.</span></span> <span data-ttu-id="f9dae-107">您可以在 [Azure Batch 的基本概念](batch-technical-overview.md)、[適用於開發人員的 Batch 功能概觀](batch-api-basics.md)和[開始使用適用於 .NET 的 Azure Batch 程式庫](batch-dotnet-get-started.md)中找到更多資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dae-107">You can find more information in [Basics of Azure Batch](batch-technical-overview.md), [Batch feature overview for developers](batch-api-basics.md), and [Get started with the Azure Batch library for .NET](batch-dotnet-get-started.md).</span></span>
> 
> 

## <a name="high-level-overview"></a><span data-ttu-id="f9dae-108">高階概述</span><span class="sxs-lookup"><span data-stu-id="f9dae-108">High-level overview</span></span>
<span data-ttu-id="f9dae-109">作業管理員和工作處理器範本可用來建立兩個有用的元件︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-109">The Job Manager and Task Processor templates can be used to create two useful components:</span></span>

* <span data-ttu-id="f9dae-110">作業管理員工作，此工作會實作作業分割器，後者可將作業細分為多個可以平行且獨立執行的工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-110">A job manager task that implements a job splitter that can break a job down into multiple tasks that can run independently, in parallel.</span></span>
* <span data-ttu-id="f9dae-111">工作處理器，可用來圍繞應用程式命令列執行前置處理和後置處理。</span><span class="sxs-lookup"><span data-stu-id="f9dae-111">A task processor that can be used to perform pre-processing and post-processing around an application command line.</span></span>

<span data-ttu-id="f9dae-112">例如，在影片轉譯案例中，作業分割器會將單一影片作業轉變成數百個或數千個會分開處理個別畫面的不同工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-112">For example, in a movie rendering scenario, the job splitter would turn a single movie job into hundreds or thousands of separate tasks that would process individual frames separately.</span></span> <span data-ttu-id="f9dae-113">相對來說，工作處理器則會叫用為了轉譯每個畫面所需要的轉譯應用程式和所有相依處理序，並執行任何額外動作 (例如，將轉譯的畫面複製到儲存體位置)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-113">Correspondingly, the task processor would invoke the rendering application and all dependent processes that are needed to render each frame, as well as perform any additional actions (for example, copying the rendered frame to a storage location).</span></span>

> [!NOTE]
> <span data-ttu-id="f9dae-114">作業管理員和工作處理器範本彼此獨立，因此您可以根據計算作業需求和個人喜好，選擇同時使用兩者或只使用其中之一。</span><span class="sxs-lookup"><span data-stu-id="f9dae-114">The Job Manager and Task Processor templates are independent of each other, so you can choose to use both, or only one of them, depending on the requirements of your compute job and on your preferences.</span></span>
> 
> 

<span data-ttu-id="f9dae-115">如下圖所示，使用這些範本的計算作業會經歷三個階段︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-115">As shown in the diagram below, a compute job that uses these templates will go through three stages:</span></span>

1. <span data-ttu-id="f9dae-116">用戶端程式碼 (例如，應用程式、Web 服務等) 將作業提交至 Azure 上的 Batch 服務，將其作業管理員工作指定為作業管理員程式。</span><span class="sxs-lookup"><span data-stu-id="f9dae-116">The client code (e.g., application, web service, etc.) submits a job to the Batch service on Azure, specifying as its job manager task the job manager program.</span></span>
2. <span data-ttu-id="f9dae-117">Batch 服務在計算節點上執行作業管理員工作，作業分割器則根據作業分割器程式碼中的參數和規格，在任意數量的所需計算節點上啟動指定數量的工作處理器工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-117">The Batch service runs the job manager task on a compute node and the job splitter launches the specified number of task processor tasks, on as many compute nodes as required, based on the parameters and specifications in the job splitter code.</span></span>
3. <span data-ttu-id="f9dae-118">工作處理器工作以平行方式獨立執行，處理輸入資料並產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="f9dae-118">The task processor tasks run independently, in parallel, to process the input data and generate the output data.</span></span>

![顯示用戶端程式碼與 Batch 服務互動方式的圖表][diagram01]

## <a name="prerequisites"></a><span data-ttu-id="f9dae-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="f9dae-120">Prerequisites</span></span>
<span data-ttu-id="f9dae-121">若要使用 Batch 範本，您需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-121">To use the Batch templates, you will need the following:</span></span>

* <span data-ttu-id="f9dae-122">已安裝 Visual Studio 2015 的電腦。</span><span class="sxs-lookup"><span data-stu-id="f9dae-122">A computer with Visual Studio 2015 installed.</span></span> <span data-ttu-id="f9dae-123">目前只有針對 Visual Studio 2015 支援批次範本。</span><span class="sxs-lookup"><span data-stu-id="f9dae-123">Batch templates are currently only supported for Visual Studio 2015.</span></span>
* <span data-ttu-id="f9dae-124">Batch 範本，可從 [Visual Studio 資源庫][vs_gallery]取得作為 Visual Studio 擴充。</span><span class="sxs-lookup"><span data-stu-id="f9dae-124">The Batch templates, which are available from the [Visual Studio Gallery][vs_gallery] as Visual Studio extensions.</span></span> <span data-ttu-id="f9dae-125">有兩種方式可取得範本︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-125">There are two ways to get the templates:</span></span>
  
  * <span data-ttu-id="f9dae-126">在 Visual Studio 中，使用 [擴充功能和更新] 對話方塊安裝範本 (如需詳細資訊，請參閱[尋找及使用 Visual Studio 擴充][vs_find_use_ext])。</span><span class="sxs-lookup"><span data-stu-id="f9dae-126">Install the templates using the **Extensions and Updates** dialog box in Visual Studio (for more information, see [Finding and Using Visual Studio Extensions][vs_find_use_ext]).</span></span> <span data-ttu-id="f9dae-127">在 [擴充功能和更新]  對話方塊中，搜尋和下載下列兩個延伸模組︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-127">In the **Extensions and Updates** dialog box, search and download the following two extensions:</span></span>
    
    * <span data-ttu-id="f9dae-128">具有作業分割器的 Azure Batch 作業管理員</span><span class="sxs-lookup"><span data-stu-id="f9dae-128">Azure Batch Job Manager with Job Splitter</span></span>
    * <span data-ttu-id="f9dae-129">Azure Batch 工作處理器</span><span class="sxs-lookup"><span data-stu-id="f9dae-129">Azure Batch Task Processor</span></span>
  * <span data-ttu-id="f9dae-130">從 Visual Studio 的線上資源庫下載範本：[Microsoft Azure Batch 專案範本][vs_gallery_templates]</span><span class="sxs-lookup"><span data-stu-id="f9dae-130">Download the templates from the online gallery for Visual Studio: [Microsoft Azure Batch Project Templates][vs_gallery_templates]</span></span>
* <span data-ttu-id="f9dae-131">如果您打算使用 [應用程式封裝](batch-application-packages.md) 功能將作業管理員和工作處理器部署到 Batch 計算節點，您必須連結儲存體帳戶和 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9dae-131">If you plan to use the [Application Packages](batch-application-packages.md) feature to deploy the job manager and task processor to the Batch compute nodes, you need to link a storage account to your Batch account.</span></span>

## <a name="preparation"></a><span data-ttu-id="f9dae-132">準備工作</span><span class="sxs-lookup"><span data-stu-id="f9dae-132">Preparation</span></span>
<span data-ttu-id="f9dae-133">我們建議您建立可在其中包含作業管理員和工作處理器的方案，因為這樣便能更輕鬆地在作業管理員和工作處理器程式之間共用程式碼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-133">We recommend creating a solution that can contain your job manager as well as your task processor, because this can make it easier to share code between your job manager and task processor programs.</span></span> <span data-ttu-id="f9dae-134">若要建立此方案，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-134">To create this solution, follow these steps:</span></span>

1. <span data-ttu-id="f9dae-135">開啟 Visual Studio，然後選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="f9dae-135">Open Visual Studio and select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="f9dae-136">在 [範本] 底下展開 [其他專案類型]、按一下 [Visual Studio 方案]，然後選取 [空白方案]。</span><span class="sxs-lookup"><span data-stu-id="f9dae-136">Under **Templates**, expand **Other Project Types**, click **Visual Studio Solutions**, and then select **Blank Solution**.</span></span>
3. <span data-ttu-id="f9dae-137">輸入可描述應用程式和此方案用途的名稱 (例如，「LitwareBatchTaskPrograms」)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-137">Type a name that describes your application and the purpose of this solution (e.g., "LitwareBatchTaskPrograms").</span></span>
4. <span data-ttu-id="f9dae-138">若要建立新方案，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f9dae-138">To create the new solution, click **OK**.</span></span>

## <a name="job-manager-template"></a><span data-ttu-id="f9dae-139">作業管理員範本</span><span class="sxs-lookup"><span data-stu-id="f9dae-139">Job Manager template</span></span>
<span data-ttu-id="f9dae-140">作業管理員範本可協助您實作作業管理員工作以執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-140">The Job Manager template helps you to implement a job manager task that can perform the following actions:</span></span>

* <span data-ttu-id="f9dae-141">將作業分割成多個工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-141">Split a job into multiple tasks.</span></span>
* <span data-ttu-id="f9dae-142">提交這些工作以在 Batch 上執行。</span><span class="sxs-lookup"><span data-stu-id="f9dae-142">Submit those tasks to run on Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="f9dae-143">如需作業管理員工作的詳細資訊，請參閱 [適用於開發人員的 Batch 功能概觀](batch-api-basics.md#job-manager-task)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-143">For more information about job manager tasks, see [Batch feature overview for developers](batch-api-basics.md#job-manager-task).</span></span>
> 
> 

### <a name="create-a-job-manager-using-the-template"></a><span data-ttu-id="f9dae-144">使用範本建立作業管理員</span><span class="sxs-lookup"><span data-stu-id="f9dae-144">Create a Job Manager using the template</span></span>
<span data-ttu-id="f9dae-145">若要在稍早建立的方案中新增作業管理員，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-145">To add a job manager to the solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="f9dae-146">在 Visual Studio 中開啟現有方案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-146">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="f9dae-147">在 [方案總管] 中，以滑鼠右鍵按一下方案，然後按一下 [新增] > [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="f9dae-147">In Solution Explorer, right-click the solution, click **Add** > **New Project**.</span></span>
3. <span data-ttu-id="f9dae-148">在 [Visual C#] 底下按一下 [雲端]，然後按一下 [具有作業分割器的 Azure Batch 作業管理員]。</span><span class="sxs-lookup"><span data-stu-id="f9dae-148">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Job Manager with Job Splitter**.</span></span>
4. <span data-ttu-id="f9dae-149">輸入可描述應用程式並將此專案識別為作業管理員的名稱 (例如"LitwareJobManager")。</span><span class="sxs-lookup"><span data-stu-id="f9dae-149">Type a name that describes your application and identifies this project as the job manager (e.g. "LitwareJobManager").</span></span>
5. <span data-ttu-id="f9dae-150">若要建立專案，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f9dae-150">To create the project, click **OK**.</span></span>
6. <span data-ttu-id="f9dae-151">最後，建置專案來強制 Visual Studio 載入所有參考的 NuGet 套件，以及確認專案是否有效以便能開始對其進行修改。</span><span class="sxs-lookup"><span data-stu-id="f9dae-151">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span></span>

### <a name="job-manager-template-files-and-their-purpose"></a><span data-ttu-id="f9dae-152">作業管理員範本檔案及其用途</span><span class="sxs-lookup"><span data-stu-id="f9dae-152">Job Manager template files and their purpose</span></span>
<span data-ttu-id="f9dae-153">當您使用作業管理員範本建立專案時，它會產生三組程式碼檔案︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-153">When you create a project using the Job Manager template, it generates three groups of code files:</span></span>

* <span data-ttu-id="f9dae-154">主要程式檔 (Program.cs)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-154">The main program file (Program.cs).</span></span> <span data-ttu-id="f9dae-155">這包含程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="f9dae-155">This contains the program entry point and top-level exception handling.</span></span> <span data-ttu-id="f9dae-156">通常來說，您應該不需要修改此檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-156">You shouldn't normally need to modify this.</span></span>
* <span data-ttu-id="f9dae-157">架構目錄。</span><span class="sxs-lookup"><span data-stu-id="f9dae-157">The Framework directory.</span></span> <span data-ttu-id="f9dae-158">其所包含的檔案負責處理作業管理員程式所進行的「重複使用」工作，像是解壓縮參數、在 Batch 作業中新增工作等。通常來說，您應該不需要修改這些檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-158">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span></span>
* <span data-ttu-id="f9dae-159">作業分割器檔案 (JobSplitter.cs)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-159">The job splitter file (JobSplitter.cs).</span></span> <span data-ttu-id="f9dae-160">此處可供存放用於將作業分割成多個工作的應用程式特定邏輯。</span><span class="sxs-lookup"><span data-stu-id="f9dae-160">This is where you will put your application-specific logic for splitting a job into tasks.</span></span>

<span data-ttu-id="f9dae-161">當然，您可以根據作業分割邏輯的複雜度，視需要新增其他檔案來支援作業分割器程式碼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-161">Of course you can add additional files as required to support your job splitter code, depending on the complexity of the job splitting logic.</span></span>

<span data-ttu-id="f9dae-162">範本也會產生標準的 .NET 專案檔案，例如 .csproj 檔案、app.config、packages.config 等等。</span><span class="sxs-lookup"><span data-stu-id="f9dae-162">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="f9dae-163">本節其餘部分會說明不同檔案和其程式碼結構，並解釋每個類別的用途。</span><span class="sxs-lookup"><span data-stu-id="f9dae-163">The rest of this section describes the different files and their code structure, and explains what each class does.</span></span>

![顯示作業管理員範本方案的 Visual Studio 方案總管][solution_explorer01]

<span data-ttu-id="f9dae-165">**架構檔案**</span><span class="sxs-lookup"><span data-stu-id="f9dae-165">**Framework files**</span></span>

* <span data-ttu-id="f9dae-166">`Configuration.cs`︰封裝作業組態資料的載入，例如 Batch 帳戶詳細資料、連結的儲存體帳戶認證、作業和工作資訊，以及作業參數。</span><span class="sxs-lookup"><span data-stu-id="f9dae-166">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="f9dae-167">它也會透過 Configuration.EnvironmentVariable 類別提供 Batch 定義的環境變數 (請參閱 Batch 文件中適用於工作的「環境」設定) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="f9dae-167">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="f9dae-168">`IConfiguration.cs`︰摘要組態類別的實作，以便您可以使用假的或模擬的組態物件對作業分割器進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="f9dae-168">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="f9dae-169">`JobManager.cs`︰協調作業管理員程式的元件。</span><span class="sxs-lookup"><span data-stu-id="f9dae-169">`JobManager.cs`: Orchestrates the components of the job manager program.</span></span> <span data-ttu-id="f9dae-170">它負責初始化作業分割器、叫用作業分割器，以及將作業分割器傳回的工作分派給工作傳送者。</span><span class="sxs-lookup"><span data-stu-id="f9dae-170">It is responsible for the initializing the job splitter, invoking the job splitter, and dispatching the tasks returned by the job splitter to the task submitter.</span></span>
* <span data-ttu-id="f9dae-171">`JobManagerException.cs`︰代表需要由作業管理員終止的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f9dae-171">`JobManagerException.cs`: Represents an error that requires the job manager to terminate.</span></span> <span data-ttu-id="f9dae-172">JobManagerException 會用來包裝可在終止過程中提供特定診斷資訊的「預期」錯誤。</span><span class="sxs-lookup"><span data-stu-id="f9dae-172">JobManagerException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>
* <span data-ttu-id="f9dae-173">`TaskSubmitter.cs`︰此類別負責將作業分割器傳回的工作新增至 Batch 作業。</span><span class="sxs-lookup"><span data-stu-id="f9dae-173">`TaskSubmitter.cs`: This class is responsible to adding tasks returned by the job splitter to the Batch job.</span></span> <span data-ttu-id="f9dae-174">JobManager 類別會將一連串工作彙總成一批，以便有效率但及時地新增到作業中，然後在每一批的背景執行緒上呼叫 TaskSubmitter.SubmitTasks。</span><span class="sxs-lookup"><span data-stu-id="f9dae-174">The JobManager class aggregates the sequence of tasks into batches for efficient but timely addition to the job, then calls TaskSubmitter.SubmitTasks on a background thread for each batch.</span></span>

<span data-ttu-id="f9dae-175">**作業分割器**</span><span class="sxs-lookup"><span data-stu-id="f9dae-175">**Job Splitter**</span></span>

<span data-ttu-id="f9dae-176">`JobSplitter.cs`︰此類別包含用於將作業分割成多個工作的應用程式特定邏輯。</span><span class="sxs-lookup"><span data-stu-id="f9dae-176">`JobSplitter.cs`: This class contains application-specific logic for splitting the job into tasks.</span></span> <span data-ttu-id="f9dae-177">架構會叫用 JobSplitter.Split 方法以取得一連串的工作，並在方法傳回工作時將方法新增至作業中。</span><span class="sxs-lookup"><span data-stu-id="f9dae-177">The framework invokes the JobSplitter.Split method to obtain a sequence of tasks, which it adds to the job as the method returns them.</span></span> <span data-ttu-id="f9dae-178">這是您將在其中插入作業邏輯的類別。</span><span class="sxs-lookup"><span data-stu-id="f9dae-178">This is the class where you will inject the logic of your job.</span></span> <span data-ttu-id="f9dae-179">實作分割方法，傳回一連串代表要將作業分割成之工作的 CloudTask 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f9dae-179">Implement the Split method to return a sequence of CloudTask instances representing the tasks into which you want to partition the job.</span></span>

<span data-ttu-id="f9dae-180">**標準 .NET 命令列專案檔**</span><span class="sxs-lookup"><span data-stu-id="f9dae-180">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="f9dae-181">`App.config`︰標準的 .NET 應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="f9dae-181">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="f9dae-182">`Packages.config`︰標準的 NuGet 套件相依性檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-182">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="f9dae-183">`Program.cs`：包含程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="f9dae-183">`Program.cs`: Contains the program entry point and top-level exception handling.</span></span>

### <a name="implementing-the-job-splitter"></a><span data-ttu-id="f9dae-184">實作作業分割器</span><span class="sxs-lookup"><span data-stu-id="f9dae-184">Implementing the job splitter</span></span>
<span data-ttu-id="f9dae-185">當您開啟作業管理員範本專案時，專案依預設會開啟 JobSplitter.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-185">When you open the Job Manager template project, the project will have the JobSplitter.cs file open by default.</span></span> <span data-ttu-id="f9dae-186">您可以如下所示使用 Split() 方法為工作負載中的工作實作分割邏輯︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-186">You can implement the split logic for the tasks in your workload by using the Split() method show below:</span></span>

```csharp
/// <summary>
/// Gets the tasks into which to split the job. This is where you inject
/// your application-specific logic for decomposing the job into tasks.
///
/// The job manager framework invokes the Split method for you; you need
/// only to implement it, not to call it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and the "yield return" statement; this allows tasks to be added
/// and to start running while splitting is still in progress.
/// </summary>
/// <returns>The tasks to be added to the job. Tasks are added automatically
/// by the job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for the split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> <span data-ttu-id="f9dae-187">`Split()` 在方法中，註解區段是作業管理員範本程式碼中唯一可供您修改的區段，方法是新增用來將作業分割成不同工作的邏輯。</span><span class="sxs-lookup"><span data-stu-id="f9dae-187">The annotated section in the `Split()` method is the only section of the Job Manager template code that is intended for you to modify by adding the logic to split your jobs into different tasks.</span></span> <span data-ttu-id="f9dae-188">如果您想要修改範本的其他區段，請確定您熟悉 Batch 的運作方式，並先在幾個 [Batch 程式碼範例][github_samples]中試試看。</span><span class="sxs-lookup"><span data-stu-id="f9dae-188">If you want to modify a different section of the template, please ensure you are familiarized with how Batch works, and try out a few of the [Batch code samples][github_samples].</span></span>
> 
> 

<span data-ttu-id="f9dae-189">Split() 實作具有下列項目的存取權︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-189">Your Split() implementation has access to:</span></span>

* <span data-ttu-id="f9dae-190">作業參數，透過 `_parameters` 欄位。</span><span class="sxs-lookup"><span data-stu-id="f9dae-190">The job parameters, via the `_parameters` field.</span></span>
* <span data-ttu-id="f9dae-191">代表作業的 CloudJob 物件，透過 `_job` 欄位。</span><span class="sxs-lookup"><span data-stu-id="f9dae-191">The CloudJob object representing the job, via the `_job` field.</span></span>
* <span data-ttu-id="f9dae-192">代表作業管理員工作的 CloudJob 物件，透過 `_jobManagerTask` 欄位。</span><span class="sxs-lookup"><span data-stu-id="f9dae-192">The CloudTask object representing the job manager task, via the `_jobManagerTask` field.</span></span>

<span data-ttu-id="f9dae-193">`Split()` 實作不需要直接將工作新增到作業中。</span><span class="sxs-lookup"><span data-stu-id="f9dae-193">Your `Split()` implementation does not need to add tasks to the job directly.</span></span> <span data-ttu-id="f9dae-194">相反地，程式碼應傳回一連串的 CloudTask 物件，並由叫用作業分割器的架構類別自動新增至作業中。</span><span class="sxs-lookup"><span data-stu-id="f9dae-194">Instead, your code should return a sequence of CloudTask objects, and these will be added to the job automatically by the framework classes that invoke the job splitter.</span></span> <span data-ttu-id="f9dae-195">通常會使用 C# 的迭代器 (`yield return`) 功能來實作作業分割器，因為這可讓工作盡快開始執行，而非等候所有要計算的工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-195">It's common to use C#'s iterator (`yield return`) feature to implement job splitters as this allows the tasks to start running as soon as possible rather than waiting for all tasks to be calculated.</span></span>

<span data-ttu-id="f9dae-196">**作業分割器失敗**</span><span class="sxs-lookup"><span data-stu-id="f9dae-196">**Job splitter failure**</span></span>

<span data-ttu-id="f9dae-197">如果作業分割器發生錯誤，它應該︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-197">If your job splitter encounters an error, it should either:</span></span>

* <span data-ttu-id="f9dae-198">使用 C# `yield break` 陳述式終止序列，在此情況下，會將作業管理員視為成功；或者</span><span class="sxs-lookup"><span data-stu-id="f9dae-198">Terminate the sequence using the C# `yield break` statement, in which case the job manager will be treated as successful; or</span></span>
* <span data-ttu-id="f9dae-199">擲回例外狀況，在此情況下，會將作業管理員視為失敗，並可能會根據用戶端對它的組態進行重試。</span><span class="sxs-lookup"><span data-stu-id="f9dae-199">Throw an exception, in which case the job manager will be treated as failed and may be retried depending on how the client has configured it).</span></span>

<span data-ttu-id="f9dae-200">在這兩種情況下，作業分割器已傳回並新增到 Batch 作業的任何工作都有資格執行。</span><span class="sxs-lookup"><span data-stu-id="f9dae-200">In both cases, any tasks already returned by the job splitter and added to the Batch job will be eligible to run.</span></span> <span data-ttu-id="f9dae-201">如果您不想讓此情況發生，則可以︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-201">If you don't want this to happen, then you could:</span></span>

* <span data-ttu-id="f9dae-202">終止作業，不讓它從作業分割器傳回</span><span class="sxs-lookup"><span data-stu-id="f9dae-202">Terminate the job before returning from the job splitter</span></span>
* <span data-ttu-id="f9dae-203">先編寫整個工作集合再將它傳回 (也就是傳回 `ICollection<CloudTask>`  `IList<CloudTask>` instead of implementing your job splitter using a C# iterat)</span><span class="sxs-lookup"><span data-stu-id="f9dae-203">Formulate the entire task collection before returning it (that is, return an `ICollection<CloudTask>` or `IList<CloudTask>` instead of implementing your job splitter using a C# iterator)</span></span>
* <span data-ttu-id="f9dae-204">使用工作相依性讓所有工作相依於成功完成作業管理員</span><span class="sxs-lookup"><span data-stu-id="f9dae-204">Use task dependencies to make all tasks depend on the successful completion of the job manager</span></span>

<span data-ttu-id="f9dae-205">**作業管理員重試**</span><span class="sxs-lookup"><span data-stu-id="f9dae-205">**Job manager retries**</span></span>

<span data-ttu-id="f9dae-206">視用戶端重試設定而定，如果作業管理員失敗，Batch 服務可能會予以重試。</span><span class="sxs-lookup"><span data-stu-id="f9dae-206">If the job manager fails, it may be retried by the Batch service depending on the client retry settings.</span></span> <span data-ttu-id="f9dae-207">一般來說這很安全，因為當架構將工作新增至作業時，會忽略任何已存在的工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-207">In general, this is safe, because when the framework adds tasks to the job, it ignores any tasks that already exist.</span></span> <span data-ttu-id="f9dae-208">不過，如果計算工作需要很高的成本，您可能不希望因為重新計算已新增至作業的工作而產生成本，相反地，如果重新執行不保證會產生相同的工作識別碼，則「略過重複項目」的行為不會開始運作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-208">However, if calculating tasks is expensive, you may not wish to incur the cost of recalculating tasks that have already been added to the job; conversely, if the re-run is not guaranteed to generate the same task IDs then the 'ignore duplicates' behavior will not kick in.</span></span> <span data-ttu-id="f9dae-209">在這些情況下，您應該將作業分割器設計為會偵測已完成的工作而不加以重複，例如，藉由在開始產生工作之前先執行 CloudJob.ListTasks。</span><span class="sxs-lookup"><span data-stu-id="f9dae-209">In these cases you should design your job splitter to detect the work that has already been done and not repeat it, for example by performing a CloudJob.ListTasks before starting to yield tasks.</span></span>

### <a name="exit-codes-and-exceptions-in-the-job-manager-template"></a><span data-ttu-id="f9dae-210">作業管理員範本中的結束代碼和例外狀況</span><span class="sxs-lookup"><span data-stu-id="f9dae-210">Exit codes and exceptions in the Job Manager template</span></span>
<span data-ttu-id="f9dae-211">結束代碼和例外狀況提供了機制來決定程式的執行結果，並可協助找出任何程式執行問題。</span><span class="sxs-lookup"><span data-stu-id="f9dae-211">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help to identify any problems with the execution of the program.</span></span> <span data-ttu-id="f9dae-212">作業管理員範本會實作本節所述的結束代碼和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-212">The Job Manager template implements the exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="f9dae-213">使用作業管理員範本實作的作業管理員工作會傳回三個可能的結束代碼︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-213">A job manager task that is implemented with the Job Manager template can return three possible exit codes:</span></span>

| <span data-ttu-id="f9dae-214">代碼</span><span class="sxs-lookup"><span data-stu-id="f9dae-214">Code</span></span> | <span data-ttu-id="f9dae-215">說明</span><span class="sxs-lookup"><span data-stu-id="f9dae-215">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9dae-216">0</span><span class="sxs-lookup"><span data-stu-id="f9dae-216">0</span></span> |<span data-ttu-id="f9dae-217">作業管理員順利完成。</span><span class="sxs-lookup"><span data-stu-id="f9dae-217">The job manager completed successfully.</span></span> <span data-ttu-id="f9dae-218">作業分隔器程式碼已執行完成，而且所有工作皆已新增至作業中。</span><span class="sxs-lookup"><span data-stu-id="f9dae-218">Your job splitter code ran to completion, and all tasks were added to the job.</span></span> |
| <span data-ttu-id="f9dae-219">1</span><span class="sxs-lookup"><span data-stu-id="f9dae-219">1</span></span> |<span data-ttu-id="f9dae-220">作業管理員工作失敗，且程式的「預期」部分有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-220">The job manager task failed with an exception in an 'expected' part of the program.</span></span> <span data-ttu-id="f9dae-221">例外狀況已轉譯成 JobManagerException 與診斷資訊，如有可能，也會提供可解決失敗的建議。</span><span class="sxs-lookup"><span data-stu-id="f9dae-221">The exception was translated to a JobManagerException with diagnostic information and, where possible, suggestions for resolving the failure.</span></span> |
| <span data-ttu-id="f9dae-222">2</span><span class="sxs-lookup"><span data-stu-id="f9dae-222">2</span></span> |<span data-ttu-id="f9dae-223">作業管理員工作失敗，並發生「非預期」的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-223">The job manager task failed with an 'unexpected' exception.</span></span> <span data-ttu-id="f9dae-224">例外狀況已記錄至標準輸出，但作業管理員無法新增任何額外的診斷或修復資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dae-224">The exception was logged to standard output, but the job manager was unable to add any additional diagnostic or remediation information.</span></span> |

<span data-ttu-id="f9dae-225">在作業管理員工作失敗的情況下，某些工作可能仍會在錯誤發生之前就已新增至服務中。</span><span class="sxs-lookup"><span data-stu-id="f9dae-225">In the case of job manager task failure, some tasks may still have been added to the service before the error occurred.</span></span> <span data-ttu-id="f9dae-226">這些工作會如常執行。</span><span class="sxs-lookup"><span data-stu-id="f9dae-226">These tasks will run as normal.</span></span> <span data-ttu-id="f9dae-227">請參閱上面的「作業分割器失敗」以取得有關此程式碼路徑的討論。</span><span class="sxs-lookup"><span data-stu-id="f9dae-227">See "Job Splitter Failure" above for discussion of this code path.</span></span>

<span data-ttu-id="f9dae-228">例外狀況所傳回的所有資訊會寫入 stdout.txt 和 stderr.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-228">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="f9dae-229">如需詳細資訊，請參閱 [錯誤處理](batch-api-basics.md#error-handling)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-229">For more information, see [Error Handling](batch-api-basics.md#error-handling).</span></span>

### <a name="client-considerations"></a><span data-ttu-id="f9dae-230">用戶端考量</span><span class="sxs-lookup"><span data-stu-id="f9dae-230">Client considerations</span></span>
<span data-ttu-id="f9dae-231">本節說明在根據此範本叫用作業管理員時的一些用戶端實作需求。</span><span class="sxs-lookup"><span data-stu-id="f9dae-231">This section describes some client implementation requirements when invoking a job manager based on this template.</span></span> <span data-ttu-id="f9dae-232">請參閱 [如何從用戶端程式碼傳遞參數和環境變數](#pass-environment-settings) ，以取得傳遞參數和環境設定的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dae-232">See [How to pass parameters and environment variables from the client code](#pass-environment-settings) for details on passing parameters and environment settings.</span></span>

<span data-ttu-id="f9dae-233">**必要認證**</span><span class="sxs-lookup"><span data-stu-id="f9dae-233">**Mandatory credentials**</span></span>

<span data-ttu-id="f9dae-234">若要將工作新增至 Azure Batch 作業，作業管理員工作需要您的 Azure Batch 帳戶 URL 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="f9dae-234">In order to add tasks to the Azure Batch job, the job manager task requires your Azure Batch account URL and key.</span></span> <span data-ttu-id="f9dae-235">您必須在名為 YOUR_BATCH_URL 和 YOUR_BATCH_KEY 的環境變數中傳遞這些資料。</span><span class="sxs-lookup"><span data-stu-id="f9dae-235">You must pass these in environment variables named YOUR_BATCH_URL and YOUR_BATCH_KEY.</span></span> <span data-ttu-id="f9dae-236">您可以在作業管理員工作的環境設定中設定這些變數。</span><span class="sxs-lookup"><span data-stu-id="f9dae-236">You can set these in the Job Manager task environment settings.</span></span> <span data-ttu-id="f9dae-237">例如，在 C# 用戶端︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-237">For example, in a C# client:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
<span data-ttu-id="f9dae-238">**儲存體認證**</span><span class="sxs-lookup"><span data-stu-id="f9dae-238">**Storage credentials**</span></span>

<span data-ttu-id="f9dae-239">一般而言，用戶端不需要提供連結的儲存體帳戶認證給作業管理員工作，因為 (a) 大多數作業管理員不需要明確存取連結的儲存體帳戶，而且 (b) 連結的儲存體帳戶通常會提供給所有工作，來作為作業的常見環境設定。</span><span class="sxs-lookup"><span data-stu-id="f9dae-239">Typically, the client does not need to provide the linked storage account credentials to the job manager task because (a) most job managers do not need to explicitly access the linked storage account and (b) the linked storage account is often provided to all tasks as a common environment setting for the job.</span></span> <span data-ttu-id="f9dae-240">如果您未透過常見環境設定提供連結的儲存體帳戶，且作業管理員需要存取連結的儲存體，則應如下所示提供連結的儲存體認證︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-240">If you are not providing the linked storage account via the common environment settings, and the job manager requires access to linked storage, then you should supply the linked storage credentials as follows:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="f9dae-241">**作業管理員工作設定**</span><span class="sxs-lookup"><span data-stu-id="f9dae-241">**Job manager task settings**</span></span>

<span data-ttu-id="f9dae-242">用戶端應該將作業管理員的「killJobOnCompletion」  旗標設為 **false**。</span><span class="sxs-lookup"><span data-stu-id="f9dae-242">The client should set the job manager *killJobOnCompletion* flag to **false**.</span></span>

<span data-ttu-id="f9dae-243">用戶端通常可以放心地將「runExclusive」  設為 **false**。</span><span class="sxs-lookup"><span data-stu-id="f9dae-243">It is usually safe for the client to set *runExclusive* to **false**.</span></span>

<span data-ttu-id="f9dae-244">用戶端應使用 *resourceFiles* 或 *applicationPackageReferences* 集合，將作業管理員可執行檔 (和其所需的 DLL) 部署至計算節點。</span><span class="sxs-lookup"><span data-stu-id="f9dae-244">The client should use the *resourceFiles* or *applicationPackageReferences* collection to have the job manager executable (and its required DLLs) deployed to the compute node.</span></span>

<span data-ttu-id="f9dae-245">根據預設，作業管理員在失敗時不會重試。</span><span class="sxs-lookup"><span data-stu-id="f9dae-245">By default, the job manager will not be retried if it fails.</span></span> <span data-ttu-id="f9dae-246">根據作業管理員邏輯，用戶端可能會想透過 *constraints*/*maxTaskRetryCount* 啟用重試。</span><span class="sxs-lookup"><span data-stu-id="f9dae-246">Depending on your job manager logic, the client may want to enable retries via *constraints*/*maxTaskRetryCount*.</span></span>

<span data-ttu-id="f9dae-247">**作業設定**</span><span class="sxs-lookup"><span data-stu-id="f9dae-247">**Job settings**</span></span>

<span data-ttu-id="f9dae-248">如果作業分割器發出具有相依性的工作，用戶端必須將作業的 usesTaskDependencies 設為 true。</span><span class="sxs-lookup"><span data-stu-id="f9dae-248">If the job splitter emits tasks with dependencies, the client must set the job's usesTaskDependencies to true.</span></span>

<span data-ttu-id="f9dae-249">在作業分割器模型中，除了作業分割器所建立的工作外，用戶端通常不會想將工作新增至作業中。</span><span class="sxs-lookup"><span data-stu-id="f9dae-249">In the job splitter model, it is unusual for clients to wish to add tasks to jobs over and above what the job splitter creates.</span></span> <span data-ttu-id="f9dae-250">因此一般來說，用戶端應該會將作業的「onAllTasksComplete」  設為 **terminatejob**。</span><span class="sxs-lookup"><span data-stu-id="f9dae-250">The client should therefore normally set the job's *onAllTasksComplete* to **terminatejob**.</span></span>

## <a name="task-processor-template"></a><span data-ttu-id="f9dae-251">工作處理器範本</span><span class="sxs-lookup"><span data-stu-id="f9dae-251">Task Processor template</span></span>
<span data-ttu-id="f9dae-252">工作處理器範本可協助您實作工作處理器以執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-252">A Task Processor template helps you to implement a task processor that can perform the following actions:</span></span>

* <span data-ttu-id="f9dae-253">設定要讓每個 Batch 工作執行所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dae-253">Set up the information required by each Batch task to run.</span></span>
* <span data-ttu-id="f9dae-254">執行每個 Batch 工作所需的所有動作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-254">Run all actions required by each Batch task.</span></span>
* <span data-ttu-id="f9dae-255">將工作輸出儲存至永續性儲存體。</span><span class="sxs-lookup"><span data-stu-id="f9dae-255">Save task outputs to persistent storage.</span></span>

<span data-ttu-id="f9dae-256">雖然不需要工作處理器就能在 Batch 上執行工作，但使用工作處理器的主要優點是，它會提供包裝函式以在一個位置實作所有工作執行動作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-256">Although a task processor is not required to run tasks on Batch, the key advantage of using a task processor is that it provides a wrapper to implement all task execution actions in one location.</span></span> <span data-ttu-id="f9dae-257">例如，如果您需要在每個工作的內容中執行數個應用程式，或者如果您需要在完成各項工作之後將資料複製到永續性儲存體。</span><span class="sxs-lookup"><span data-stu-id="f9dae-257">For example, if you need to run several applications in the context of each task, or if you need to copy data to persistent storage after completing each task.</span></span>

<span data-ttu-id="f9dae-258">工作處理器所執行的動作可依工作負載所需調整為任意複雜性程度和數量。</span><span class="sxs-lookup"><span data-stu-id="f9dae-258">The actions performed by the task processor can be as simple or complex, and as many or as few, as required by your workload.</span></span> <span data-ttu-id="f9dae-259">此外，藉由將所有工作動作實作到一個工作處理器中，您可以根據應用程式或工作負載需求的變更，輕易地更新或新增動作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-259">Additionally, by implementing all task actions into one task processor, you can readily update or add actions based on changes to applications or workload requirements.</span></span> <span data-ttu-id="f9dae-260">不過，在某些情況下，工作處理器可能不是最適合您的實作的方案，因為它會增加不必要的複雜度，例如，在執行可以從簡單命令列快速啟動的作業時。</span><span class="sxs-lookup"><span data-stu-id="f9dae-260">However, in some cases a task processor might not be the optimal solution for your implementation as it can add unnecessary complexity, for example when running jobs that can be quickly started from a simple command line.</span></span>

### <a name="create-a-task-processor-using-the-template"></a><span data-ttu-id="f9dae-261">使用範本建立工作處理器</span><span class="sxs-lookup"><span data-stu-id="f9dae-261">Create a Task Processor using the template</span></span>
<span data-ttu-id="f9dae-262">若要在稍早建立的方案中新增工作處理器，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-262">To add a task processor to the solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="f9dae-263">在 Visual Studio 中開啟現有方案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-263">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="f9dae-264">在 [方案總管] 中，以滑鼠右鍵按一下方案、按一下 [新增]，然後按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="f9dae-264">In Solution Explorer, right-click the solution, click **Add**, and then click **New Project**.</span></span>
3. <span data-ttu-id="f9dae-265">在 [Visual C#] 底下按一下 [雲端]，然後按一下 [Azure Batch 工作處理器]。</span><span class="sxs-lookup"><span data-stu-id="f9dae-265">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Task Processor**.</span></span>
4. <span data-ttu-id="f9dae-266">輸入可描述應用程式並將此專案識別為工作處理器的名稱 (例如"LitwareTaskProcessor")。</span><span class="sxs-lookup"><span data-stu-id="f9dae-266">Type a name that describes your application and identifies this project as the task processor (e.g. "LitwareTaskProcessor").</span></span>
5. <span data-ttu-id="f9dae-267">若要建立專案，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f9dae-267">To create the project, click **OK**.</span></span>
6. <span data-ttu-id="f9dae-268">最後，建置專案來強制 Visual Studio 載入所有參考的 NuGet 套件，以及確認專案是否有效以便能開始對其進行修改。</span><span class="sxs-lookup"><span data-stu-id="f9dae-268">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span></span>

### <a name="task-processor-template-files-and-their-purpose"></a><span data-ttu-id="f9dae-269">工作處理器範本檔案及其用途</span><span class="sxs-lookup"><span data-stu-id="f9dae-269">Task Processor template files and their purpose</span></span>
<span data-ttu-id="f9dae-270">當您使用工作處理器範本建立專案時，它會產生三組程式碼檔案︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-270">When you create a project using the task processor template, it generates three groups of code files:</span></span>

* <span data-ttu-id="f9dae-271">主要程式檔 (Program.cs)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-271">The main program file (Program.cs).</span></span> <span data-ttu-id="f9dae-272">這包含程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="f9dae-272">This contains the program entry point and top-level exception handling.</span></span> <span data-ttu-id="f9dae-273">通常來說，您應該不需要修改此檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-273">You shouldn't normally need to modify this.</span></span>
* <span data-ttu-id="f9dae-274">架構目錄。</span><span class="sxs-lookup"><span data-stu-id="f9dae-274">The Framework directory.</span></span> <span data-ttu-id="f9dae-275">其所包含的檔案負責處理作業管理員程式所進行的「重複使用」工作，像是解壓縮參數、在 Batch 作業中新增工作等。通常來說，您應該不需要修改這些檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-275">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span></span>
* <span data-ttu-id="f9dae-276">工作處理器檔案 (TaskProcessor.cs)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-276">The task processor file (TaskProcessor.cs).</span></span> <span data-ttu-id="f9dae-277">此檔案可供存放用於執行工作的應用程式特定邏輯 (通常是藉由向外呼叫現有的可執行檔)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-277">This is where you will put your application-specific logic for executing a task (typically by calling out to an existing executable).</span></span> <span data-ttu-id="f9dae-278">前置和後置處理程式碼 (例如下載額外資料或上傳結果檔案) 也存放在此。</span><span class="sxs-lookup"><span data-stu-id="f9dae-278">Pre- and post-processing code, such as downloading additional data or uploading result files, also goes here.</span></span>

<span data-ttu-id="f9dae-279">當然，您可以根據作業分割邏輯的複雜度，視需要新增其他檔案來支援工作處理器程式碼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-279">Of course you can add additional files as required to support your task processor code, depending on the complexity of the job splitting logic.</span></span>

<span data-ttu-id="f9dae-280">範本也會產生標準的 .NET 專案檔案，例如 .csproj 檔案、app.config、packages.config 等等。</span><span class="sxs-lookup"><span data-stu-id="f9dae-280">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="f9dae-281">本節其餘部分會說明不同檔案和其程式碼結構，並解釋每個類別的用途。</span><span class="sxs-lookup"><span data-stu-id="f9dae-281">The rest of this section describes the different files and their code structure, and explains what each class does.</span></span>

![顯示工作處理器範本方案的 Visual Studio 方案總管][solution_explorer02]

<span data-ttu-id="f9dae-283">**架構檔案**</span><span class="sxs-lookup"><span data-stu-id="f9dae-283">**Framework files**</span></span>

* <span data-ttu-id="f9dae-284">`Configuration.cs`︰封裝作業組態資料的載入，例如 Batch 帳戶詳細資料、連結的儲存體帳戶認證、作業和工作資訊，以及作業參數。</span><span class="sxs-lookup"><span data-stu-id="f9dae-284">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="f9dae-285">它也會透過 Configuration.EnvironmentVariable 類別提供 Batch 定義的環境變數 (請參閱 Batch 文件中適用於工作的「環境」設定) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="f9dae-285">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="f9dae-286">`IConfiguration.cs`︰摘要組態類別的實作，以便您可以使用假的或模擬的組態物件對作業分割器進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="f9dae-286">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="f9dae-287">`TaskProcessorException.cs`︰代表需要由作業管理員終止的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f9dae-287">`TaskProcessorException.cs`: Represents an error that requires the job manager to terminate.</span></span> <span data-ttu-id="f9dae-288">TaskProcessorException 會用來包裝可在終止過程中提供特定診斷資訊的「預期」錯誤。</span><span class="sxs-lookup"><span data-stu-id="f9dae-288">TaskProcessorException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>

<span data-ttu-id="f9dae-289">**工作處理器**</span><span class="sxs-lookup"><span data-stu-id="f9dae-289">**Task Processor**</span></span>

* <span data-ttu-id="f9dae-290">`TaskProcessor.cs`︰執行工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-290">`TaskProcessor.cs`: Runs the task.</span></span> <span data-ttu-id="f9dae-291">架構會叫用 TaskProcessor.Run 方法。</span><span class="sxs-lookup"><span data-stu-id="f9dae-291">The framework invokes the TaskProcessor.Run method.</span></span> <span data-ttu-id="f9dae-292">這是您將在其中插入工作的應用程式特定邏輯的類別。</span><span class="sxs-lookup"><span data-stu-id="f9dae-292">This is the class where you will inject the application-specific logic of your task.</span></span> <span data-ttu-id="f9dae-293">實作 Run 方法以便︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-293">Implement the Run method to:</span></span>
  * <span data-ttu-id="f9dae-294">剖析及驗證任何工作參數</span><span class="sxs-lookup"><span data-stu-id="f9dae-294">Parse and validate any task parameters</span></span>
  * <span data-ttu-id="f9dae-295">針對要叫用的任何外部程式撰寫命令列</span><span class="sxs-lookup"><span data-stu-id="f9dae-295">Compose the command line for any external program you want to invoke</span></span>
  * <span data-ttu-id="f9dae-296">記錄為了偵錯所可能需要的任何診斷資訊</span><span class="sxs-lookup"><span data-stu-id="f9dae-296">Log any diagnostic information you may require for debugging purposes</span></span>
  * <span data-ttu-id="f9dae-297">使用該命令列開始處理序</span><span class="sxs-lookup"><span data-stu-id="f9dae-297">Start a process using that command line</span></span>
  * <span data-ttu-id="f9dae-298">等候處理序結束</span><span class="sxs-lookup"><span data-stu-id="f9dae-298">Wait for the process to exit</span></span>
  * <span data-ttu-id="f9dae-299">擷取處理序的結束碼以判斷其已成功或失敗</span><span class="sxs-lookup"><span data-stu-id="f9dae-299">Capture the exit code of the process to determine if it succeeded or failed</span></span>
  * <span data-ttu-id="f9dae-300">儲存所有想要保留在永續性儲存體的輸出檔案</span><span class="sxs-lookup"><span data-stu-id="f9dae-300">Save any output files you want to keep to persistent storage</span></span>

<span data-ttu-id="f9dae-301">**標準 .NET 命令列專案檔**</span><span class="sxs-lookup"><span data-stu-id="f9dae-301">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="f9dae-302">`App.config`︰標準的 .NET 應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="f9dae-302">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="f9dae-303">`Packages.config`︰標準的 NuGet 套件相依性檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-303">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="f9dae-304">`Program.cs`：包含程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="f9dae-304">`Program.cs`: Contains the program entry point and top-level exception handling.</span></span>

## <a name="implementing-the-task-processor"></a><span data-ttu-id="f9dae-305">實作工作處理器</span><span class="sxs-lookup"><span data-stu-id="f9dae-305">Implementing the task processor</span></span>
<span data-ttu-id="f9dae-306">當您開啟工作處理器範本專案時，專案依預設會開啟 TaskProcessor.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-306">When you open the Task Processor template project, the project will have the TaskProcessor.cs file open by default.</span></span> <span data-ttu-id="f9dae-307">您可以如下所示使用 Run() 方法為工作負載中的工作實作執行邏輯︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-307">You can implement the run logic for the tasks in your workload by using the Run() method shown below:</span></span>

```csharp
/// <summary>
/// Runs the task processing logic. This is where you inject
/// your application-specific logic for decomposing the job into tasks.
///
/// The task processor framework invokes the Run method for you; you need
/// only to implement it, not to call it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check the exit code of that program and
/// save output files to persistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for the task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> <span data-ttu-id="f9dae-308">Run() 方法中的註解區段是工作處理器範本程式碼中唯一可供您修改的區段，方法是為工作負載中的工作新增執行邏輯。</span><span class="sxs-lookup"><span data-stu-id="f9dae-308">The annotated section in the Run() method is the only section of the Task Processor template code that is intended for you to modify by adding the run logic for the tasks in your workload.</span></span> <span data-ttu-id="f9dae-309">如果您想要修改範本的其他區段，請先熟悉 Batch 的運作方式，方法是檢閱 Batch 文件並在幾個 Batch 程式碼範例上進行嘗試。</span><span class="sxs-lookup"><span data-stu-id="f9dae-309">If you want to modify a different section of the template, please first familiarize yourself with how Batch works by reviewing the Batch documentation and trying out a few of the Batch code samples.</span></span>
> 
> 

<span data-ttu-id="f9dae-310">Run() 方法負責啟動命令列、啟動一或多個處理序、等候所有處理序完成、儲存結果，以及在最後傳回結束碼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-310">The Run() method is responsible for launching the command line, starting one or more processes, waiting for all process to complete, saving the results, and finally returning with an exit code.</span></span> <span data-ttu-id="f9dae-311">Run() 方法可供您實作工作的處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="f9dae-311">The Run() method is where you implement the processing logic for your tasks.</span></span> <span data-ttu-id="f9dae-312">工作處理器架構會為您叫用 Run() 方法；您不需要自己呼叫。</span><span class="sxs-lookup"><span data-stu-id="f9dae-312">The task processor framework invokes the Run() method for you; you do not need to call it yourself.</span></span>

<span data-ttu-id="f9dae-313">Run() 實作具有下列項目的存取權︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-313">Your Run() implementation has access to:</span></span>

* <span data-ttu-id="f9dae-314">工作參數，透過 `_parameters` 欄位。</span><span class="sxs-lookup"><span data-stu-id="f9dae-314">The task parameters, via the `_parameters` field.</span></span>
* <span data-ttu-id="f9dae-315">作業和工作識別碼，透過 `_jobId` 和 `_taskId` 欄位。</span><span class="sxs-lookup"><span data-stu-id="f9dae-315">The job and task ids, via the `_jobId` and `_taskId` fields.</span></span>
* <span data-ttu-id="f9dae-316">工作組態，透過 `_configuration` 欄位。</span><span class="sxs-lookup"><span data-stu-id="f9dae-316">The task configuration, via the `_configuration` field.</span></span>

<span data-ttu-id="f9dae-317">**工作失敗**</span><span class="sxs-lookup"><span data-stu-id="f9dae-317">**Task failure**</span></span>

<span data-ttu-id="f9dae-318">萬一發生失敗，您可以擲回例外狀況以結束 Run() 方法，但這會導致最上層的例外狀況處理常式繼續控制工作結束代碼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-318">In case of failure, you can exit the Run() method by throwing an exception, but this leaves the top level exception handler in control of the task exit code.</span></span> <span data-ttu-id="f9dae-319">如果您需要控制結束代碼以便分辨不同類型的失敗，例如為了進行診斷或因為某些失敗模式應終止作業，某些則不應該，則您應該藉由傳回非零結束代碼來結束 Run() 方法。</span><span class="sxs-lookup"><span data-stu-id="f9dae-319">If you need to control the exit code so that you can distinguish different types of failure, for example for diagnostic purposes or because some failure modes should terminate the job and others should not, then you should exit the Run() method by returning a non-zero exit code.</span></span> <span data-ttu-id="f9dae-320">這會成為工作結束代碼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-320">This becomes the task exit code.</span></span>

### <a name="exit-codes-and-exceptions-in-the-task-processor-template"></a><span data-ttu-id="f9dae-321">工作處理器範本中的結束代碼和例外狀況</span><span class="sxs-lookup"><span data-stu-id="f9dae-321">Exit codes and exceptions in the Task Processor template</span></span>
<span data-ttu-id="f9dae-322">結束代碼和例外狀況提供了機制來決定程式的執行結果，並可協助找出任何程式執行問題。</span><span class="sxs-lookup"><span data-stu-id="f9dae-322">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help identify any problems with the execution of the program.</span></span> <span data-ttu-id="f9dae-323">工作處理器範本會實作本節所述的結束代碼和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-323">The Task Processor template implements the exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="f9dae-324">使用工作處理器範本實作的工作處理器工作會傳回三個可能的結束代碼︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-324">A task processor task that is implemented with the Task Processor template can return three possible exit codes:</span></span>

| <span data-ttu-id="f9dae-325">代碼</span><span class="sxs-lookup"><span data-stu-id="f9dae-325">Code</span></span> | <span data-ttu-id="f9dae-326">說明</span><span class="sxs-lookup"><span data-stu-id="f9dae-326">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9dae-327">[Process.ExitCode][process_exitcode]</span><span class="sxs-lookup"><span data-stu-id="f9dae-327">[Process.ExitCode][process_exitcode]</span></span> |<span data-ttu-id="f9dae-328">工作處理器已執行完成。</span><span class="sxs-lookup"><span data-stu-id="f9dae-328">The task processor ran to completion.</span></span> <span data-ttu-id="f9dae-329">請注意，這並非表示您叫用的程式已成功，只表示工作處理器已成功叫用程式並執行任何後置處理，而沒有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-329">Note that this does not imply that the program you invoked was successful – only that the task processor invoked it successfully and performed any post-processing without exceptions.</span></span> <span data-ttu-id="f9dae-330">結束代碼的意義取決於所叫用的程式，一般來說，結束代碼 0 表示程式已成功，任何其他結束代碼則表示程式失敗。</span><span class="sxs-lookup"><span data-stu-id="f9dae-330">The meaning of the exit code depends on the invoked program – typically exit code 0 means the program succeeded and any other exit code means the program failed.</span></span> |
| <span data-ttu-id="f9dae-331">1</span><span class="sxs-lookup"><span data-stu-id="f9dae-331">1</span></span> |<span data-ttu-id="f9dae-332">工作處理器失敗，且程式的「預期」部分有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-332">The task processor failed with an exception in an 'expected' part of the program.</span></span> <span data-ttu-id="f9dae-333">例外狀況已轉譯成 `TaskProcessorException` 與診斷資訊，如有可能，也會提供可解決失敗的建議。</span><span class="sxs-lookup"><span data-stu-id="f9dae-333">The exception was translated to a `TaskProcessorException` with diagnostic information and, where possible, suggestions for resolving the failure.</span></span> |
| <span data-ttu-id="f9dae-334">2</span><span class="sxs-lookup"><span data-stu-id="f9dae-334">2</span></span> |<span data-ttu-id="f9dae-335">工作處理器失敗，並發生「非預期」的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-335">The task processor failed with an 'unexpected' exception.</span></span> <span data-ttu-id="f9dae-336">例外狀況已記錄至標準輸出，但工作處理器無法新增任何額外的診斷或修復資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dae-336">The exception was logged to standard output, but the task processor was unable to add any additional diagnostic or remediation information.</span></span> |

> [!NOTE]
> <span data-ttu-id="f9dae-337">如果您叫用的程式使用結束代碼 1 和 2 來指出特定失敗模式，則使用結束代碼 1 和 2 來代表工作處理器錯誤將造成模稜兩可的狀況。</span><span class="sxs-lookup"><span data-stu-id="f9dae-337">If the program you invoke uses exit codes 1 and 2 to indicate specific failure modes, then using exit codes 1 and 2 for task processor errors is ambiguous.</span></span> <span data-ttu-id="f9dae-338">您可以編輯 Program.cs 檔案中的例外狀況案例，將這些工作處理器錯誤碼變更為可資區分的結束代碼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-338">You can change these task processor error codes to distinctive exit codes by editing the exception cases in the Program.cs file.</span></span>
> 
> 

<span data-ttu-id="f9dae-339">例外狀況所傳回的所有資訊會寫入 stdout.txt 和 stderr.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dae-339">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="f9dae-340">如需詳細資訊，請參閱 Batch 文件中的＜錯誤處理＞。</span><span class="sxs-lookup"><span data-stu-id="f9dae-340">For more information, see Error Handling, in the Batch documentation.</span></span>

### <a name="client-considerations"></a><span data-ttu-id="f9dae-341">用戶端考量</span><span class="sxs-lookup"><span data-stu-id="f9dae-341">Client considerations</span></span>
<span data-ttu-id="f9dae-342">**儲存體認證**</span><span class="sxs-lookup"><span data-stu-id="f9dae-342">**Storage credentials**</span></span>

<span data-ttu-id="f9dae-343">如果工作處理器會使用 Azure Blob 儲存體來保存輸出 (例如使用檔案慣例協助程式程式庫)，則它需要存取雲端儲存體帳戶認證或包含共用存取簽章 (SAS) 的 Blob 容器 URL。</span><span class="sxs-lookup"><span data-stu-id="f9dae-343">If your task processor uses Azure blob storage to persist outputs, for example using the file conventions helper library, then it needs access to *either* the cloud storage account credentials *or* a blob container URL that includes a shared access signature (SAS).</span></span> <span data-ttu-id="f9dae-344">範本支援透過常見環境變數來提供認證。</span><span class="sxs-lookup"><span data-stu-id="f9dae-344">The template includes support for providing credentials via common environment variables.</span></span> <span data-ttu-id="f9dae-345">用戶端可以如下所示傳遞儲存體認證︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-345">Your client can pass the storage credentials as follows:</span></span>

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="f9dae-346">然後，就可以透過 `_configuration.StorageAccount` 屬性在 TaskProcessor 類別中使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9dae-346">The storage account is then available in the TaskProcessor class via the `_configuration.StorageAccount` property.</span></span>

<span data-ttu-id="f9dae-347">如果您想要使用具有 SAS 的容器 URL，您也可以透過作業的常見環境設定傳遞此 URL，但工作處理器範本目前未內建支援此 URL。</span><span class="sxs-lookup"><span data-stu-id="f9dae-347">If you prefer to use a container URL with SAS, you can also pass this via an job common environment setting, but the task processor template does not currently include built-in support for this.</span></span>

<span data-ttu-id="f9dae-348">**儲存體設定**</span><span class="sxs-lookup"><span data-stu-id="f9dae-348">**Storage setup**</span></span>

<span data-ttu-id="f9dae-349">建議用戶端或作業管理員工作先建立工作所需的任何容器，再將工作新增至作業。</span><span class="sxs-lookup"><span data-stu-id="f9dae-349">It is recommended that the client or job manager task create any containers required by tasks before adding the tasks to the job.</span></span> <span data-ttu-id="f9dae-350">如果您使用具有 SAS 的容器 URL 就必須這麼做，因為這樣的 URL 並未包含建立容器的權限。</span><span class="sxs-lookup"><span data-stu-id="f9dae-350">This is mandatory if you use a container URL with SAS, as such a URL does not include permission to create the container.</span></span> <span data-ttu-id="f9dae-351">即使您傳遞的是儲存體帳戶認證仍建議您這麼做，因為它會儲存每一項必須在容器上呼叫 CloudBlobContainer.CreateIfNotExistsAsync 的工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-351">It is recommended even if you pass storage account credentials, as it saves every task having to call CloudBlobContainer.CreateIfNotExistsAsync on the container.</span></span>

## <a name="pass-parameters-and-environment-variables"></a><span data-ttu-id="f9dae-352">傳遞參數和環境變數</span><span class="sxs-lookup"><span data-stu-id="f9dae-352">Pass parameters and environment variables</span></span>
### <a name="pass-environment-settings"></a><span data-ttu-id="f9dae-353">傳遞環境設定</span><span class="sxs-lookup"><span data-stu-id="f9dae-353">Pass environment settings</span></span>
<span data-ttu-id="f9dae-354">用戶端可以環境設定的形式將資訊傳遞給作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-354">A client can pass information to the job manager task in the form of environment settings.</span></span> <span data-ttu-id="f9dae-355">接著，作業管理員工作可在產生做為計算作業一部分來執行的工作處理器工作時使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dae-355">This information can then be used by the job manager task when generating the task processor tasks that will run as part of the compute job.</span></span> <span data-ttu-id="f9dae-356">可以環境設定形式傳遞的資訊範例如下︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-356">Examples of the information that you can pass as environment settings are:</span></span>

* <span data-ttu-id="f9dae-357">儲存體帳戶名稱和帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="f9dae-357">Storage account name and account keys</span></span>
* <span data-ttu-id="f9dae-358">Batch 帳戶 URL</span><span class="sxs-lookup"><span data-stu-id="f9dae-358">Batch account URL</span></span>
* <span data-ttu-id="f9dae-359">Batch 帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="f9dae-359">Batch account key</span></span>

<span data-ttu-id="f9dae-360">Batch 服務具有簡單的機制，可在 [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask] 中使用 `EnvironmentSettings` 屬性，將環境設定傳遞至作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-360">The Batch service has a simple mechanism to pass environment settings to a job manager task by using the `EnvironmentSettings` property in [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].</span></span>

<span data-ttu-id="f9dae-361">例如，若要取得 Batch 帳戶的 `BatchClient` 執行個體，您可以環境變數的形式從用戶端程式碼傳遞 Batch 帳戶的 URL 和共用金鑰認證。</span><span class="sxs-lookup"><span data-stu-id="f9dae-361">For example, to get the `BatchClient` instance for a Batch account, you can pass as environment variables from the client code the URL and shared key credentials for the Batch account.</span></span> <span data-ttu-id="f9dae-362">同樣地，若要存取連結至 Batch 帳戶的儲存體帳戶，您可使用環境變數的形式傳遞儲存體帳戶名稱和儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="f9dae-362">Likewise, to access the storage account that is linked to the Batch account, you can pass the storage account name and the storage account key as environment variables.</span></span>

### <a name="pass-parameters-to-the-job-manager-template"></a><span data-ttu-id="f9dae-363">將參數傳遞至作業管理員範本</span><span class="sxs-lookup"><span data-stu-id="f9dae-363">Pass parameters to the Job Manager template</span></span>
<span data-ttu-id="f9dae-364">在許多情況下，最好將每個作業的參數傳遞至作業管理員工作，以便控制作業分割處理序或是設定作業的工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-364">In many cases, it's useful to pass per-job parameters to the job manager task, either to control the job splitting process or to configure the tasks for the job.</span></span> <span data-ttu-id="f9dae-365">若要這麼做，可以將名為 parameters.json 的 JSON 檔案上傳做為作業管理員工作的資源檔。</span><span class="sxs-lookup"><span data-stu-id="f9dae-365">You can do this by uploading a JSON file named parameters.json as a resource file for the job manager task.</span></span> <span data-ttu-id="f9dae-366">然後，參數就可以在作業管理員範本的 `JobSplitter._parameters` 欄位中變為可供使用。</span><span class="sxs-lookup"><span data-stu-id="f9dae-366">The parameters can then become available in the `JobSplitter._parameters` field in the Job Manager template.</span></span>

> [!NOTE]
> <span data-ttu-id="f9dae-367">內建的參數處理常式只支援字串對字串的字典。</span><span class="sxs-lookup"><span data-stu-id="f9dae-367">The built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="f9dae-368">如果您想要以參數值的形式傳遞複雜 JSON 值，就必須以字串形式傳遞並在作業分割器中進行剖析，或是修改架構的 `Configuration.GetJobParameters` 方法。</span><span class="sxs-lookup"><span data-stu-id="f9dae-368">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the job splitter, or modify the framework's `Configuration.GetJobParameters` method.</span></span>
> 
> 

### <a name="pass-parameters-to-the-task-processor-template"></a><span data-ttu-id="f9dae-369">將參數傳遞給工作處理器範本</span><span class="sxs-lookup"><span data-stu-id="f9dae-369">Pass parameters to the Task Processor template</span></span>
<span data-ttu-id="f9dae-370">您也可以使用工作處理器範本將參數傳遞至所實作的個別工作。</span><span class="sxs-lookup"><span data-stu-id="f9dae-370">You can also pass parameters to individual tasks implemented using the Task Processor template.</span></span> <span data-ttu-id="f9dae-371">就像使用作業管理員範本一樣，工作處理器範本會尋找名為</span><span class="sxs-lookup"><span data-stu-id="f9dae-371">Just as with the job manager template, the task processor template looks for a resource file named</span></span>

<span data-ttu-id="f9dae-372">parameters.json 的資源檔案，如果找到，即會將它載入以做為參數字典。</span><span class="sxs-lookup"><span data-stu-id="f9dae-372">parameters.json, and if found it loads it as the parameters dictionary.</span></span> <span data-ttu-id="f9dae-373">有幾個選項可用來將參數傳遞給工作處理器工作︰</span><span class="sxs-lookup"><span data-stu-id="f9dae-373">There are a couple of options for how to pass parameters to the task processor tasks:</span></span>

* <span data-ttu-id="f9dae-374">重複使用作業參數 JSON。</span><span class="sxs-lookup"><span data-stu-id="f9dae-374">Reuse the job parameters JSON.</span></span> <span data-ttu-id="f9dae-375">這適用於唯一的參數都是全作業參數時 (例如轉譯高度和寬度)。</span><span class="sxs-lookup"><span data-stu-id="f9dae-375">This works well if the only parameters are job-wide ones (for example, a render height and width).</span></span> <span data-ttu-id="f9dae-376">若要這樣做，請於在作業分割器中建立 CloudTask 時，從作業管理員工作的 ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) 將 parameters.json 資源檔物件的參考新增至 CloudTask 的 ResourceFiles 集合。</span><span class="sxs-lookup"><span data-stu-id="f9dae-376">To do this, when creating a CloudTask in the job splitter, add a reference to the parameters.json resource file object from the job manager task's ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) to the CloudTask's ResourceFiles collection.</span></span>
* <span data-ttu-id="f9dae-377">產生和上傳工作特定的 parameters.json 文件做為作業分隔器執行的一部分，並在工作的資源檔集合中參考該 Blob。</span><span class="sxs-lookup"><span data-stu-id="f9dae-377">Generate and upload a task-specific parameters.json document as part of job splitter execution, and reference that blob in the task's resource files collection.</span></span> <span data-ttu-id="f9dae-378">如果不同的工作有不同的參數，就必須這麼做。</span><span class="sxs-lookup"><span data-stu-id="f9dae-378">This is necessary if different tasks have different parameters.</span></span> <span data-ttu-id="f9dae-379">以參數形式將畫面索引傳遞至工作的 3D 轉譯案例便是可能的範例。</span><span class="sxs-lookup"><span data-stu-id="f9dae-379">An example might be a 3D rendering scenario where the frame index is passed to the task as a parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="f9dae-380">內建的參數處理常式只支援字串對字串的字典。</span><span class="sxs-lookup"><span data-stu-id="f9dae-380">The built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="f9dae-381">如果您想要以參數值的形式傳遞複雜 JSON 值，就必須以字串形式傳遞並在工作處理器中進行剖析，或是修改架構的 `Configuration.GetTaskParameters` 方法。</span><span class="sxs-lookup"><span data-stu-id="f9dae-381">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the task processor, or modify the framework's `Configuration.GetTaskParameters` method.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f9dae-382">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9dae-382">Next steps</span></span>
### <a name="persist-job-and-task-output-to-azure-storage"></a><span data-ttu-id="f9dae-383">將作業和工作輸出保存到 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="f9dae-383">Persist job and task output to Azure Storage</span></span>
<span data-ttu-id="f9dae-384">開發 Batch 解決方案時的另一個實用工具是 [Azure Batch 檔案慣例][nuget_package]。</span><span class="sxs-lookup"><span data-stu-id="f9dae-384">Another helpful tool in Batch solution development is [Azure Batch File Conventions][nuget_package].</span></span> <span data-ttu-id="f9dae-385">在 Batch .NET 應用程式中使用此 .NET 類別庫 (目前為預覽版) 可在 Azure 儲存體中輕鬆地儲存或擷取工作輸出。</span><span class="sxs-lookup"><span data-stu-id="f9dae-385">Use this .NET class library (currently in preview) in your Batch .NET applications to easily store and retrieve task outputs to and from Azure Storage.</span></span> <span data-ttu-id="f9dae-386">[保存 Azure Batch 作業和工作輸出](batch-task-output.md) 包含類別庫及其使用方式的完整討論。</span><span class="sxs-lookup"><span data-stu-id="f9dae-386">[Persist Azure Batch job and task output](batch-task-output.md) contains a full discussion of the library and its usage.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="f9dae-387">Batch 論壇</span><span class="sxs-lookup"><span data-stu-id="f9dae-387">Batch Forum</span></span>
<span data-ttu-id="f9dae-388">MSDN 上的 [Azure Batch 論壇][forum]是一個很棒的地方，可以討論 Batch 和詢問有關此服務的問題。</span><span class="sxs-lookup"><span data-stu-id="f9dae-388">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="f9dae-389">請前去查看很有幫助的「便利貼」文章，在建立 Batch 解決方案時，出現問題就張貼。</span><span class="sxs-lookup"><span data-stu-id="f9dae-389">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
