---
title: "使用 Visual Studio 在 Azure 中建立第一個函式 | Microsoft Docs"
description: "使用 Azure Functions Tools for Visual Studio，建立簡單 HTTP 觸發函式並發行至 Azure。"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, 計算, 無伺服器架構"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 04370558725d76ffe83d8aaf5d16c88fd2803ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="5659c-104">使用 Visual Studio 建立第一個函式</span><span class="sxs-lookup"><span data-stu-id="5659c-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="5659c-105">Azure Functions 可讓您在無伺服器環境中執行程式碼，而不需要先建立 VM 或發佈 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5659c-105">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="5659c-106">在本主題中，您將了解如何使用 Visual Studio 2017 Tools for Azure Functions 在本機建立及測試 "hello world" 函式。</span><span class="sxs-lookup"><span data-stu-id="5659c-106">In this topic, you learn how to use the Visual Studio 2017 tools for Azure Functions to create and test a "hello world" function locally.</span></span> <span data-ttu-id="5659c-107">您接著會將函式程式碼發行至 Azure。</span><span class="sxs-lookup"><span data-stu-id="5659c-107">You will then publish the function code to Azure.</span></span> <span data-ttu-id="5659c-108">這些工具可在 Visual Studio 2017 15.3 版或更新版本的 Azure 開發工作負載中取得。</span><span class="sxs-lookup"><span data-stu-id="5659c-108">These tools are available as part of the Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Visual Studio 專案中的 Azure Functions 程式碼](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="5659c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5659c-110">Prerequisites</span></span>

<span data-ttu-id="5659c-111">若要完成本教學課程，請安裝：</span><span class="sxs-lookup"><span data-stu-id="5659c-111">To complete this tutorial, install:</span></span>

* <span data-ttu-id="5659c-112">[Visual Studio 2017 15.3 版](https://www.visualstudio.com/vs/preview/)，包括 **Azure 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="5659c-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>

    ![安裝包含 Azure 開發工作負載的 Visual Studio 2017](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="5659c-114">安裝或升級至 Visual Studio 2017 版本 15.3 之後，您可能也需要手動更新 Visual Studio 2017 Tools for Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="5659c-114">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="5659c-115">您可以從 [工具] 功能表的 [延伸模組和更新...] 下的 > [更新] > [Visual Studio Marketplace] > [Azure Functions and Web Jobs Tools] > [更新] 更新工具。</span><span class="sxs-lookup"><span data-stu-id="5659c-115">You can update the tools from the **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="5659c-116">在 Visual Studio 中建立 Azure Functions 專案</span><span class="sxs-lookup"><span data-stu-id="5659c-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="5659c-117">您現在已建立專案，即可建立第一個函式。</span><span class="sxs-lookup"><span data-stu-id="5659c-117">Now that you have created the project, you can create your first function.</span></span>

## <a name="create-the-function"></a><span data-ttu-id="5659c-118">建立函式</span><span class="sxs-lookup"><span data-stu-id="5659c-118">Create the function</span></span>

1. <span data-ttu-id="5659c-119">在 [方案總管] 中，於專案節點上按一下滑鼠右鍵，然後選取 [新增] > [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="5659c-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="5659c-120">選取 [Azure Function]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5659c-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="5659c-121">選取 [HttpTrigger]，輸入 [函式名稱]，針對 [存取權限] 選取 [匿名]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5659c-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="5659c-122">建立的函式會由任何用戶端的 HTTP 要求存取。</span><span class="sxs-lookup"><span data-stu-id="5659c-122">The function created is accessed by an HTTP request from any client.</span></span> 

    ![建立新的 Azure Function](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="5659c-124">這會將一個程式碼檔案新增至您的專案，其中包含實作函式程式碼的類別。</span><span class="sxs-lookup"><span data-stu-id="5659c-124">A code file is added to your project that contains a class that implements your function code.</span></span> <span data-ttu-id="5659c-125">此程式碼是以範本為基礎，會接收名稱值並將其回應回去。</span><span class="sxs-lookup"><span data-stu-id="5659c-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="5659c-126">**FunctionName** 屬性會設定您的函式名稱。</span><span class="sxs-lookup"><span data-stu-id="5659c-126">The **FunctionName** attribute sets the name of your function.</span></span> <span data-ttu-id="5659c-127">**HttpTrigger** 屬性表示觸發函式的訊息。</span><span class="sxs-lookup"><span data-stu-id="5659c-127">The **HttpTrigger** attribute indicates the message that triggers the function.</span></span> 

    ![函式程式碼檔案](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="5659c-129">您現在已建立 HTTP 觸發的函式，可以在本機電腦上進行測試。</span><span class="sxs-lookup"><span data-stu-id="5659c-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="5659c-130">在本機測試函式</span><span class="sxs-lookup"><span data-stu-id="5659c-130">Test the function locally</span></span>

<span data-ttu-id="5659c-131">Azure Functions Core Tools 可讓您在本機開發電腦上執行 Azure Functions 專案。</span><span class="sxs-lookup"><span data-stu-id="5659c-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="5659c-132">第一次從 Visual Studio 啟動函式時，系統會提示您安裝這些工具。</span><span class="sxs-lookup"><span data-stu-id="5659c-132">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="5659c-133">若要測試您的函式，請按 F5。</span><span class="sxs-lookup"><span data-stu-id="5659c-133">To test your function, press F5.</span></span> <span data-ttu-id="5659c-134">如果出現提示，接受來自 Visual Studio 之下載及安裝 Azure Functions Core (CLI) 工具的要求。</span><span class="sxs-lookup"><span data-stu-id="5659c-134">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="5659c-135">您可能也需要啟用防火牆例外狀況，工具才能處理 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="5659c-135">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="5659c-136">從 Azure Functions 執行階段輸出複製函式的 URL。</span><span class="sxs-lookup"><span data-stu-id="5659c-136">Copy the URL of your function from the Azure Functions runtime output.</span></span>  

    ![Azure 本機執行階段](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="5659c-138">將 HTTP 要求的 URL 貼到瀏覽器的網址列。</span><span class="sxs-lookup"><span data-stu-id="5659c-138">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="5659c-139">將查詢字串 `&name=<yourname>` 附加至此 URL 並執行要求。</span><span class="sxs-lookup"><span data-stu-id="5659c-139">Append the query string `&name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="5659c-140">下圖顯示瀏覽器中對於函式傳回之本機 GET 要求所做出的回應︰</span><span class="sxs-lookup"><span data-stu-id="5659c-140">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![瀏覽器中的函式 localhost 回應](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="5659c-142">若要停止偵錯，請按一下 Visual Studio 工具列上的 [停止] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5659c-142">To stop debugging, click the **Stop** button on the Visual Studio toolbar.</span></span>

<span data-ttu-id="5659c-143">確認函式在本機電腦上正確執行之後，就可以將專案發佈到 Azure。</span><span class="sxs-lookup"><span data-stu-id="5659c-143">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="5659c-144">將專案發佈到 Azure</span><span class="sxs-lookup"><span data-stu-id="5659c-144">Publish the project to Azure</span></span>

<span data-ttu-id="5659c-145">您的 Azure 訂用帳戶中必須具有函式應用程式，才可以發佈您的專案。</span><span class="sxs-lookup"><span data-stu-id="5659c-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="5659c-146">您可以直接從 Visual Studio 建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5659c-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="5659c-147">在 Azure 中測試您的函式</span><span class="sxs-lookup"><span data-stu-id="5659c-147">Test your function in Azure</span></span>

1. <span data-ttu-id="5659c-148">從發行設定檔頁面複製函式應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="5659c-148">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="5659c-149">使用新的基底 URL，取代在本機測試函式時所使用之 URL 的 `localhost:port` 部分。</span><span class="sxs-lookup"><span data-stu-id="5659c-149">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="5659c-150">如同以往，務必將查詢字串 `&name=<yourname>` 附加至此 URL 並執行要求。</span><span class="sxs-lookup"><span data-stu-id="5659c-150">As before, make sure to append the query string `&name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="5659c-151">呼叫 HTTP URL 觸發函式的 URL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="5659c-151">The URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="5659c-152">將 HTTP 要求的新 URL 貼到瀏覽器的網址列。</span><span class="sxs-lookup"><span data-stu-id="5659c-152">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="5659c-153">下圖顯示瀏覽器中對於函式傳回之遠端 GET 要求所做出的回應︰</span><span class="sxs-lookup"><span data-stu-id="5659c-153">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![瀏覽器中的函式回應](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="5659c-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5659c-155">Next steps</span></span>

<span data-ttu-id="5659c-156">您已透過 Visual Studio，使用簡單的 HTTP 觸發函式建立 C# 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5659c-156">You have used Visual Studio to create a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="5659c-157">若要了解如何設定專案以支援其他類型的觸發程序和繫結，請參閱 [Azure Functions Tools for Visual Studio](functions-develop-vs.md) 中的[設定專案以進行本機開發](functions-develop-vs.md#configure-the-project-for-local-development)一節。</span><span class="sxs-lookup"><span data-stu-id="5659c-157">To learn how to configure your project to support other types of triggers and bindings, see the [Configure the project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="5659c-158">若要深入了解如何使用 Azure Functions Core Tools 進行本機測試和偵錯，請參閱[在本機編碼和測試 Azure Functions](functions-run-local.md)。</span><span class="sxs-lookup"><span data-stu-id="5659c-158">To learn more about local testing and debugging using the Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="5659c-159">若要深入了解如何將函式開發為 .NET 類別庫，請參閱[搭配使用 .NET 類別庫與 Azure Functions](functions-dotnet-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="5659c-159">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

