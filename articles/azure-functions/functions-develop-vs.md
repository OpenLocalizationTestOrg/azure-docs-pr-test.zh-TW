---
title: "使用 Visual Studio 開發 Azure Functions |Microsoft 文件"
description: "了解如何使用 Azure Functions Tools for Visual Studio 2017 開發和測試 Azure Functions。"
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
ms.openlocfilehash: 1e0568bc58e8879cabe409cf8e9b5866f922e7c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="dcb85-103">Azure Functions Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dcb85-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="dcb85-104">Azure Functions Tools for Visual Studio 2017 是 Visual Studio 的延伸模組，可讓您開發、測試 C# 函數及將它部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="dcb85-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="dcb85-105">如果這是您第一次體驗 Azure Functions，可至 [Azure Functions 簡介](functions-overview.md)深入了解。</span><span class="sxs-lookup"><span data-stu-id="dcb85-105">If this is your first experience with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="dcb85-106">Azure Functions Tools 提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="dcb85-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="dcb85-107">在本機開發電腦上編輯、建置及執行函數。</span><span class="sxs-lookup"><span data-stu-id="dcb85-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="dcb85-108">直接將 Azure Functions 專案發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="dcb85-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="dcb85-109">使用 WebJobs 屬性直接在 C# 程式碼中宣告函數繫結，而不必針對繫結定義維護個別的 function.json。</span><span class="sxs-lookup"><span data-stu-id="dcb85-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="dcb85-110">開發及部署預先編譯的 C# 函數。</span><span class="sxs-lookup"><span data-stu-id="dcb85-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="dcb85-111">預先編譯的函數提供的冷啟動效能比 C# 指令碼型函數更好。</span><span class="sxs-lookup"><span data-stu-id="dcb85-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="dcb85-112">在 C# 中編寫函數，同時享有 Visual Studio 開發的所有優點。</span><span class="sxs-lookup"><span data-stu-id="dcb85-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="dcb85-113">本主題示範如何使用 Azure Functions Tools for Visual Studio 2017 在 C# 中開發函數。</span><span class="sxs-lookup"><span data-stu-id="dcb85-113">This topic shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="dcb85-114">您也會了解如何將專案發佈到 Azure 成為 .NET 組件。</span><span class="sxs-lookup"><span data-stu-id="dcb85-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcb85-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="dcb85-115">Prerequisites</span></span>

<span data-ttu-id="dcb85-116">[Visual Studio 2017 15.3](https://www.visualstudio.com/vs/) 及其以上版本之 Azure 開發工作負載包含了 Azure Functions 工具。</span><span class="sxs-lookup"><span data-stu-id="dcb85-116">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="dcb85-117">在安裝 Visual Studio 2017 15.3 版時，務必包含 **Azure 開發**工作負載：</span><span class="sxs-lookup"><span data-stu-id="dcb85-117">Make sure you include the **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![安裝包含 Azure 開發工作負載的 Visual Studio 2017](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="dcb85-119">若要建立及部署函數，您也需要：</span><span class="sxs-lookup"><span data-stu-id="dcb85-119">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="dcb85-120">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dcb85-120">An active Azure subscription.</span></span> <span data-ttu-id="dcb85-121">如果您還沒有 Azure 訂用帳戶，可以使用[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="dcb85-122">Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dcb85-122">An Azure Storage account.</span></span> <span data-ttu-id="dcb85-123">若要建立儲存體帳戶，請參閱[儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-123">To create a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="dcb85-124">建立 Azure Functions 專案</span><span class="sxs-lookup"><span data-stu-id="dcb85-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="dcb85-125">設定專案以進行本機開發</span><span class="sxs-lookup"><span data-stu-id="dcb85-125">Configure the project for local development</span></span>

<span data-ttu-id="dcb85-126">當您使用 Azure Functions 範本建立新專案時，會取得空 C# 專案，其中包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="dcb85-126">When you create a new project using the Azure Functions template, you get an empty C# project that contains the following files:</span></span>

* <span data-ttu-id="dcb85-127">**host.json**：讓您設定 Functions 主機。</span><span class="sxs-lookup"><span data-stu-id="dcb85-127">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="dcb85-128">這些設定同時適用於在本機執行及在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="dcb85-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="dcb85-129">如需詳細資訊，請參閱 [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) \(英文\) 參考文章。</span><span class="sxs-lookup"><span data-stu-id="dcb85-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="dcb85-130">**local.settings.json**：維持在本機執行函數時所使用的設定。</span><span class="sxs-lookup"><span data-stu-id="dcb85-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="dcb85-131">Azure 不會使用這些設定，[Azure Functions Core Tools](functions-run-local.md) 會使用這些設定。</span><span class="sxs-lookup"><span data-stu-id="dcb85-131">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="dcb85-132">使用此檔案來指定設定，例如連至其他 Azure 服務的連接字串。</span><span class="sxs-lookup"><span data-stu-id="dcb85-132">Use this file to specify settings, such as connection strings to other Azure services.</span></span> <span data-ttu-id="dcb85-133">針對專案中函數所需的每個連接，將新機碼新增至 [值] 陣列。</span><span class="sxs-lookup"><span data-stu-id="dcb85-133">Add a new key to the **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="dcb85-134">如需詳細資訊，請參閱＜Azure Functions Core Tools＞主題中的[本機設定檔](functions-run-local.md#local-settings-file)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="dcb85-135">函數執行階段會在內部使用 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dcb85-135">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="dcb85-136">針對 HTTP 和 Webhook 以外的所有觸發程序類型，您必須將 **Values.AzureWebJobsStorage** 機碼設定為有效的 Azure 儲存體帳戶連接字串。</span><span class="sxs-lookup"><span data-stu-id="dcb85-136">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="dcb85-137">設定儲存體帳戶連接字串：</span><span class="sxs-lookup"><span data-stu-id="dcb85-137">To set the storage account connection string:</span></span>

1. <span data-ttu-id="dcb85-138">在 Visual Studio 中，開啟 [Cloud Explorer]，展開 [儲存體帳戶] > 「您的儲存體帳戶」，然後選取 [屬性] 並複製 [主要連接字串] 值。</span><span class="sxs-lookup"><span data-stu-id="dcb85-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="dcb85-139">在您的專案中，開啟 local.settings.json 專案檔案並將 **AzureWebJobsStorage** 機碼的值設定為您所複製的連接字串。</span><span class="sxs-lookup"><span data-stu-id="dcb85-139">In your project, open the local.settings.json project file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="dcb85-140">重複上一步，針對函數所需的其他任何連接，將唯一機碼新增至 [值] 陣列。</span><span class="sxs-lookup"><span data-stu-id="dcb85-140">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="dcb85-141">建立函式</span><span class="sxs-lookup"><span data-stu-id="dcb85-141">Create a function</span></span>

<span data-ttu-id="dcb85-142">在預先編譯的函數中，函數所使用的繫結是透過在程式碼中套用屬性來定義的。</span><span class="sxs-lookup"><span data-stu-id="dcb85-142">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="dcb85-143">當您使用 Azure Functions Tools 從提供的範本建立函數時，會為您套用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="dcb85-143">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="dcb85-144">在 [方案總管] 中，於專案節點上按一下滑鼠右鍵，然後選取 [新增]  > [新項目]。</span><span class="sxs-lookup"><span data-stu-id="dcb85-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="dcb85-145">選取 [Azure 函數]，輸入類別的 [名稱]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="dcb85-145">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="dcb85-146">選擇您的觸發程序，設定繫結屬性，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="dcb85-146">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="dcb85-147">下列範例顯示建立佇列儲存體觸發之函數時的設定。</span><span class="sxs-lookup"><span data-stu-id="dcb85-147">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="dcb85-148">會提供名為 **QueueStorage** 的連接字串機碼，它是在 local.settings.json 檔案中定義的。</span><span class="sxs-lookup"><span data-stu-id="dcb85-148">A connection string key named **QueueStorage** is supplied, which is defined in the local.settings.json file.</span></span> 
 
3. <span data-ttu-id="dcb85-149">檢查新加入的類別。</span><span class="sxs-lookup"><span data-stu-id="dcb85-149">Examine the newly added class.</span></span> <span data-ttu-id="dcb85-150">您會看到靜態 [執行] 方法，它是使用 **FunctionName** 屬性來屬性化。</span><span class="sxs-lookup"><span data-stu-id="dcb85-150">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="dcb85-151">這個屬性指出該方法是函數的進入點。</span><span class="sxs-lookup"><span data-stu-id="dcb85-151">This attribute indicates that the method is the entry point for the function.</span></span> 

    <span data-ttu-id="dcb85-152">例如，下列 C# 類別代表基本佇列儲存體觸發的函數：</span><span class="sxs-lookup"><span data-stu-id="dcb85-152">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

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
 
    <span data-ttu-id="dcb85-153">會將繫結特定屬性套用至提供給進入點方法的每個繫結參數。</span><span class="sxs-lookup"><span data-stu-id="dcb85-153">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="dcb85-154">屬性會將繫結資訊作為參數使用。</span><span class="sxs-lookup"><span data-stu-id="dcb85-154">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="dcb85-155">在上述範例中，第一個參數套用了 **QueueTrigger** 屬性，指出佇列觸發的函數。</span><span class="sxs-lookup"><span data-stu-id="dcb85-155">In the previous example, The first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="dcb85-156">佇列名稱和連接字串設定名稱會作為參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="dcb85-156">The queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="dcb85-157">測試函式</span><span class="sxs-lookup"><span data-stu-id="dcb85-157">Testing functions</span></span>

<span data-ttu-id="dcb85-158">Azure Functions Core Tools 可讓您在本機開發電腦上執行 Azure Functions 專案。</span><span class="sxs-lookup"><span data-stu-id="dcb85-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="dcb85-159">第一次從 Visual Studio 啟動函式時，系統會提示您安裝這些工具。</span><span class="sxs-lookup"><span data-stu-id="dcb85-159">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="dcb85-160">若要測試您的函式，請按 F5。</span><span class="sxs-lookup"><span data-stu-id="dcb85-160">To test your function, press F5.</span></span> <span data-ttu-id="dcb85-161">如果出現提示，接受來自 Visual Studio 之下載及安裝 Azure Functions Core (CLI) 工具的要求。</span><span class="sxs-lookup"><span data-stu-id="dcb85-161">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="dcb85-162">您可能也需要啟用防火牆例外狀況，工具才能處理 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="dcb85-162">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="dcb85-163">隨著專案的執行，您可以像測試部署函數一樣測試程式碼。</span><span class="sxs-lookup"><span data-stu-id="dcb85-163">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="dcb85-164">如需詳細資訊，請參閱[在 Azure Functions 中測試程式碼的策略](functions-test-a-function.md)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="dcb85-165">在偵錯模式下執行時，會依預期在 Visual Studio 中遇到中斷點。</span><span class="sxs-lookup"><span data-stu-id="dcb85-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="dcb85-166">如需如何測試佇列觸發函數的範例，請參閱[佇列觸發函數快速入門教學課程](functions-create-storage-queue-triggered-function.md#test-the-function)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-166">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="dcb85-167">若要深入了解如何使用 Azure Functions Core Tools，請參閱[在本機撰寫和測試 Azure Functions 程式碼](functions-run-local.md)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-167">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="dcb85-168">發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="dcb85-168">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="dcb85-169">您在 local.settings.json 中所新增的所有設定，也必須新增至 Azure 中的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="dcb85-169">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="dcb85-170">系統並不會自動新增這些設定。</span><span class="sxs-lookup"><span data-stu-id="dcb85-170">These settings are not added automatically.</span></span> <span data-ttu-id="dcb85-171">您可以透過下列方法將必要的設定新增至函式應用程式：</span><span class="sxs-lookup"><span data-stu-id="dcb85-171">You can add required settings to your function app in one of these ways:</span></span>
>
>* <span data-ttu-id="dcb85-172">[使用 Azure 入口網站](functions-how-to-use-azure-function-app-settings.md#settings)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-172">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="dcb85-173">[使用 Azure Functions Core Tools 中的 `--publish-local-settings` 發行選項](functions-run-local.md#publish)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-173">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="dcb85-174">[使用 Azure CLI](/cli/azure/functionapp/config/appsettings#set)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-174">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dcb85-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcb85-175">Next steps</span></span>

<span data-ttu-id="dcb85-176">如需 Azure Functions Tools 的詳細資訊，請參閱 [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) \(英文\) 部落格文章的＜常見問題＞一節。</span><span class="sxs-lookup"><span data-stu-id="dcb85-176">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="dcb85-177">若要深入了解 Azure Functions Core Tools，請參閱[在本機撰寫和測試 Azure Functions 程式碼](functions-run-local.md)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-177">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="dcb85-178">若要深入了解如何將函式開發為 .NET 類別庫，請參閱[搭配使用 .NET 類別庫與 Azure Functions](functions-dotnet-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="dcb85-178">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="dcb85-179">本主題也提供範例以示範如何使用屬性宣告 Azure Functions 所支援的各種繫結類型。</span><span class="sxs-lookup"><span data-stu-id="dcb85-179">This topic also provides examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    
