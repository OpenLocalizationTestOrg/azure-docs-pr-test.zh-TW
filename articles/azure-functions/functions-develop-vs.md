---
title: "aaaDevelop Azure 函式使用 Visual Studio |Microsoft 文件"
description: "深入了解如何使用 Azure 函式 Tools for Visual Studio 2017 toodevelop 和測試 Azure 函式。"
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="24aed-103">Azure Functions Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24aed-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="24aed-104">Azure 的函式 Tools for Visual Studio 2017 是可讓您開發、 測試及部署 C# 函式 tooAzure 的 Visual Studio 的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="24aed-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions tooAzure.</span></span> <span data-ttu-id="24aed-105">如果這是您 Azure 函式的第一個體驗，您可以深入[簡介 tooAzure 函式](functions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="24aed-105">If this is your first experience with Azure Functions, you can learn more at [An introduction tooAzure Functions](functions-overview.md).</span></span>

<span data-ttu-id="24aed-106">hello Azure 函式工具提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="24aed-106">hello Azure Functions Tools provides hello following benefits:</span></span> 

* <span data-ttu-id="24aed-107">在本機開發電腦上編輯、建置及執行函數。</span><span class="sxs-lookup"><span data-stu-id="24aed-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="24aed-108">發行您的 Azure 函式直接專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="24aed-108">Publish your Azure Functions project directly tooAzure.</span></span> 
* <span data-ttu-id="24aed-109">直接在 hello 而不是維護個別 function.json 繫結定義的 C# 程式碼中使用 WebJobs 屬性 toodeclare 函式繫結。</span><span class="sxs-lookup"><span data-stu-id="24aed-109">Use WebJobs attributes toodeclare function bindings directly in hello C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="24aed-110">開發及部署預先編譯的 C# 函數。</span><span class="sxs-lookup"><span data-stu-id="24aed-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="24aed-111">預先編譯的函數提供的冷啟動效能比 C# 指令碼型函數更好。</span><span class="sxs-lookup"><span data-stu-id="24aed-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="24aed-112">同時有所有的 Visual Studio 開發的 hello 優點的程式碼在 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="24aed-112">Code your functions in C# while having all of hello benefits of Visual Studio development.</span></span> 

<span data-ttu-id="24aed-113">本主題說明如何 toouse hello Azure 函式工具的 Visual Studio 2017 toodevelop 您在 C# 中的函式。</span><span class="sxs-lookup"><span data-stu-id="24aed-113">This topic shows you how toouse hello Azure Functions Tools for Visual Studio 2017 toodevelop your functions in C#.</span></span> <span data-ttu-id="24aed-114">您也學到如何 toopublish 您的專案 tooAzure 做為.NET 組件。</span><span class="sxs-lookup"><span data-stu-id="24aed-114">You also learn how toopublish your project tooAzure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24aed-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="24aed-115">Prerequisites</span></span>

<span data-ttu-id="24aed-116">Azure 的函式工具隨附於 hello Azure 的開發工作負載的[Visual Studio 2017 版本 15.3](https://www.visualstudio.com/vs/)，或更新版本。</span><span class="sxs-lookup"><span data-stu-id="24aed-116">Azure Functions Tools is included in hello Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="24aed-117">請確定您包含 hello **Azure 開發**Visual Studio 2017 版本 15.3 安裝中的工作負載：</span><span class="sxs-lookup"><span data-stu-id="24aed-117">Make sure you include hello **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![安裝 Visual Studio 2017 hello Azure 開發的工作負載](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="24aed-119">toocreate 和部署函式，您也需要：</span><span class="sxs-lookup"><span data-stu-id="24aed-119">toocreate and deploy functions, you also need:</span></span>

* <span data-ttu-id="24aed-120">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="24aed-120">An active Azure subscription.</span></span> <span data-ttu-id="24aed-121">如果您還沒有 Azure 訂用帳戶，可以使用[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="24aed-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="24aed-122">Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="24aed-122">An Azure Storage account.</span></span> <span data-ttu-id="24aed-123">toocreate 儲存體帳戶，請參閱[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="24aed-123">toocreate a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="24aed-124">建立 Azure Functions 專案</span><span class="sxs-lookup"><span data-stu-id="24aed-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a><span data-ttu-id="24aed-125">設定本機開發的 hello 專案</span><span class="sxs-lookup"><span data-stu-id="24aed-125">Configure hello project for local development</span></span>

<span data-ttu-id="24aed-126">當您建立新的專案使用 hello Azure 函式範本時，您會得到空白 C# 專案，其中包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="24aed-126">When you create a new project using hello Azure Functions template, you get an empty C# project that contains hello following files:</span></span>

* <span data-ttu-id="24aed-127">**host.json**： 可讓您設定 hello 函式的主機。</span><span class="sxs-lookup"><span data-stu-id="24aed-127">**host.json**: Lets you configure hello Functions host.</span></span> <span data-ttu-id="24aed-128">這些設定同時適用於在本機執行及在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="24aed-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="24aed-129">如需詳細資訊，請參閱 [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) \(英文\) 參考文章。</span><span class="sxs-lookup"><span data-stu-id="24aed-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="24aed-130">**local.settings.json**：維持在本機執行函數時所使用的設定。</span><span class="sxs-lookup"><span data-stu-id="24aed-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="24aed-131">Azure 不會使用這些設定，它們由 hello [Azure 函式的核心工具](functions-run-local.md)。</span><span class="sxs-lookup"><span data-stu-id="24aed-131">These settings are not used by Azure, they are used by hello [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="24aed-132">使用此檔案 toospecify 設定，例如連接字串 tooother Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="24aed-132">Use this file toospecify settings, such as connection strings tooother Azure services.</span></span> <span data-ttu-id="24aed-133">加入新的索引鍵 toohello**值**陣列中每個專案中的函式所需的連接。</span><span class="sxs-lookup"><span data-stu-id="24aed-133">Add a new key toohello **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="24aed-134">如需詳細資訊，請參閱[本機設定檔案](functions-run-local.md#local-settings-file)hello Azure 函式的核心工具主題。</span><span class="sxs-lookup"><span data-stu-id="24aed-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in hello Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="24aed-135">hello 函式執行階段會在內部使用的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="24aed-135">hello Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="24aed-136">所有觸發程序 HTTP 和 webhook 以外的類型，您必須設定 hello **Values.AzureWebJobsStorage**金鑰 tooa 有效 Azure 儲存體帳戶連接字串。</span><span class="sxs-lookup"><span data-stu-id="24aed-136">For all trigger types other than HTTP and webhooks, you must set hello **Values.AzureWebJobsStorage** key tooa valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="24aed-137">tooset hello 儲存體帳戶連接字串：</span><span class="sxs-lookup"><span data-stu-id="24aed-137">tooset hello storage account connection string:</span></span>

1. <span data-ttu-id="24aed-138">在 Visual Studio 中開啟**Cloud Explorer**，依序展開**儲存體帳戶** > **儲存體帳戶**，然後選取**屬性**和複製 hello**主要連接字串**值。</span><span class="sxs-lookup"><span data-stu-id="24aed-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy hello **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="24aed-139">在專案中，開啟 hello local.settings.json 專案檔，並設定 hello hello 值**AzureWebJobsStorage** toohello 連接字串複製的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="24aed-139">In your project, open hello local.settings.json project file and set hello value of hello **AzureWebJobsStorage** key toohello connection string you copied.</span></span>

3. <span data-ttu-id="24aed-140">重複 hello 上一個步驟 tooadd 唯一索引鍵 toohello**值**函式所需的任何其他連接的陣列。</span><span class="sxs-lookup"><span data-stu-id="24aed-140">Repeat hello previous step tooadd unique keys toohello **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="24aed-141">建立函式</span><span class="sxs-lookup"><span data-stu-id="24aed-141">Create a function</span></span>

<span data-ttu-id="24aed-142">預先編譯的函式，在 hello hello 函式所使用的繫結會定義套用 hello 程式碼中的屬性。</span><span class="sxs-lookup"><span data-stu-id="24aed-142">In pre-compiled functions, hello bindings used by hello function are defined by applying attributes in hello code.</span></span> <span data-ttu-id="24aed-143">當您使用 hello Azure 函式工具 toocreate 從提供的 hello 範本函式時，這些屬性適用於您。</span><span class="sxs-lookup"><span data-stu-id="24aed-143">When you use hello Azure Functions Tools toocreate your functions from hello provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="24aed-144">在 [方案總管] 中，於專案節點上按一下滑鼠右鍵，然後選取 [新增] > [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="24aed-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="24aed-145">選取**Azure 函式**，輸入**名稱**hello 類別，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="24aed-145">Select **Azure Function**, type a **Name** for hello class, and click **Add**.</span></span>

2. <span data-ttu-id="24aed-146">選擇您的觸發程序，設定 hello 繫結屬性，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="24aed-146">Choose your trigger, set hello binding properties, and click **Create**.</span></span> <span data-ttu-id="24aed-147">hello 下列範例顯示 hello 設定時建立佇列儲存體觸發函式。</span><span class="sxs-lookup"><span data-stu-id="24aed-147">hello following example shows hello settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="24aed-148">連接字串的索引鍵，名為**QueueStorage**提供，就定義在 hello local.settings.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="24aed-148">A connection string key named **QueueStorage** is supplied, which is defined in hello local.settings.json file.</span></span> 
 
3. <span data-ttu-id="24aed-149">檢查 hello 新加入的類別。</span><span class="sxs-lookup"><span data-stu-id="24aed-149">Examine hello newly added class.</span></span> <span data-ttu-id="24aed-150">您會看到靜態**執行**方法中，屬性具有 hello **FunctionName**屬性。</span><span class="sxs-lookup"><span data-stu-id="24aed-150">You see a static **Run** method, that is attributed with hello **FunctionName** attribute.</span></span> <span data-ttu-id="24aed-151">這個屬性表示 hello 方法 hello hello 函式的進入點。</span><span class="sxs-lookup"><span data-stu-id="24aed-151">This attribute indicates that hello method is hello entry point for hello function.</span></span> 

    <span data-ttu-id="24aed-152">比方說，下列 C# 類別的 hello 表示基本佇列儲存體觸發函式：</span><span class="sxs-lookup"><span data-stu-id="24aed-152">For example, hello following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    <span data-ttu-id="24aed-153">繫結特定的屬性會套用的 tooeach 繫結提供參數 toohello 進入點方法。</span><span class="sxs-lookup"><span data-stu-id="24aed-153">A binding-specific attribute is applied tooeach binding parameter supplied toohello entry point method.</span></span> <span data-ttu-id="24aed-154">hello 屬性會採用 hello 做為參數的繫結資訊。</span><span class="sxs-lookup"><span data-stu-id="24aed-154">hello attribute takes hello binding information as parameters.</span></span> <span data-ttu-id="24aed-155">Hello 上述範例中，在 hello 第一個參數具有**QueueTrigger**套用屬性，指出觸發佇列函式。</span><span class="sxs-lookup"><span data-stu-id="24aed-155">In hello previous example, hello first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="24aed-156">hello 佇列名稱和連接字串設定名稱會當做參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="24aed-156">hello queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="24aed-157">測試函式</span><span class="sxs-lookup"><span data-stu-id="24aed-157">Testing functions</span></span>

<span data-ttu-id="24aed-158">Azure Functions Core Tools 可讓您在本機開發電腦上執行 Azure Functions 專案。</span><span class="sxs-lookup"><span data-stu-id="24aed-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="24aed-159">您必須提示的 tooinstall 這些工具 hello 從 Visual Studio 啟動函式的第一次。</span><span class="sxs-lookup"><span data-stu-id="24aed-159">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="24aed-160">tootest 您的函式，請按 F5。</span><span class="sxs-lookup"><span data-stu-id="24aed-160">tootest your function, press F5.</span></span> <span data-ttu-id="24aed-161">如果出現提示，請接受從 Visual Studio toodownload hello 要求，並安裝 Azure 函式核心 (CLI) 工具。</span><span class="sxs-lookup"><span data-stu-id="24aed-161">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="24aed-162">您也可能需要 tooenable 防火牆例外，好讓 hello 工具可以處理 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="24aed-162">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

<span data-ttu-id="24aed-163">Hello 專案時執行，您可以測試您的程式碼，您會測試已部署的函式時。</span><span class="sxs-lookup"><span data-stu-id="24aed-163">With hello project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="24aed-164">如需詳細資訊，請參閱[在 Azure Functions 中測試程式碼的策略](functions-test-a-function.md)。</span><span class="sxs-lookup"><span data-stu-id="24aed-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="24aed-165">在偵錯模式下執行時，會依預期在 Visual Studio 中遇到中斷點。</span><span class="sxs-lookup"><span data-stu-id="24aed-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="24aed-166">如需 tootest 佇列如何觸發函式的範例，請參閱 hello[觸發佇列函式的快速入門教學課程](functions-create-storage-queue-triggered-function.md#test-the-function)。</span><span class="sxs-lookup"><span data-stu-id="24aed-166">For an example of how tootest a queue triggered function, see hello [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="24aed-167">toolearn 進一步了解使用 hello Azure 函式的核心工具，請參閱[程式碼和測試 Azure 函式在本機](functions-run-local.md)。</span><span class="sxs-lookup"><span data-stu-id="24aed-167">toolearn more about using hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-tooazure"></a><span data-ttu-id="24aed-168">發行 tooAzure</span><span class="sxs-lookup"><span data-stu-id="24aed-168">Publish tooAzure</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="24aed-169">您在 hello local.settings.json 中加入任何設定必須也加入 toohello 函式應用程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="24aed-169">Any settings you added in hello local.settings.json must be also added toohello function app in Azure.</span></span> <span data-ttu-id="24aed-170">系統並不會自動新增這些設定。</span><span class="sxs-lookup"><span data-stu-id="24aed-170">These settings are not added automatically.</span></span> <span data-ttu-id="24aed-171">在下列其中一種，您可以加入必要的設定 tooyour 函式應用程式：</span><span class="sxs-lookup"><span data-stu-id="24aed-171">You can add required settings tooyour function app in one of these ways:</span></span>
>
>* <span data-ttu-id="24aed-172">[使用 hello Azure 入口網站](functions-how-to-use-azure-function-app-settings.md#settings)。</span><span class="sxs-lookup"><span data-stu-id="24aed-172">[Using hello Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="24aed-173">[使用 hello`--publish-local-settings`發行選項，在 hello Azure 函式的核心工具](functions-run-local.md#publish)。</span><span class="sxs-lookup"><span data-stu-id="24aed-173">[Using hello `--publish-local-settings` publish option in hello Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="24aed-174">[使用 hello Azure CLI](/cli/azure/functionapp/config/appsettings#set)。</span><span class="sxs-lookup"><span data-stu-id="24aed-174">[Using hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="24aed-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24aed-175">Next steps</span></span>

<span data-ttu-id="24aed-176">如需有關 Azure 函式工具，請參閱 hello 常見的問題 > 一節的 hello [Azure 函式的 Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="24aed-176">For more information about Azure Functions Tools, see hello Common Questions section of hello [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="24aed-177">請參閱 < 了解 hello Azure 函式核心 Tools toolearn[程式碼和測試 Azure 函式在本機](functions-run-local.md)。</span><span class="sxs-lookup"><span data-stu-id="24aed-177">toolearn more about hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="24aed-178">toolearn 進一步了解開發函式做為.NET 類別庫，請參閱[使用.NET 類別庫來搭配 Azure 函式](functions-dotnet-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="24aed-178">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="24aed-179">本主題也提供如何 toouse 屬性 toodeclare hello Azure 函式所支援的繫結的各種類型的範例。</span><span class="sxs-lookup"><span data-stu-id="24aed-179">This topic also provides examples of how toouse attributes toodeclare hello various types of bindings supported by Azure Functions.</span></span>    
