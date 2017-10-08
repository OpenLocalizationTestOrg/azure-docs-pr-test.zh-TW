---
title: "使用 Visual Studio 在 Azure 中的第一個函式的 aaaCreate |Microsoft 文件"
description: "建立及使用 Azure 函式 Tools for Visual Studio 發行簡單的 HTTP 觸發函式 tooAzure。"
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
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="458e4-104">使用 Visual Studio 建立第一個函式</span><span class="sxs-lookup"><span data-stu-id="458e4-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="458e4-105">Azure 的函式可讓您在無伺服器環境中執行您的程式碼，而不需要 toofirst 建立 VM，或發行 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="458e4-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="458e4-106">在本主題中，您將學會如何 toouse hello Azure 函式 toocreate 的 Visual Studio 2017 工具及測試在本機上的"hello world"函式。</span><span class="sxs-lookup"><span data-stu-id="458e4-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="458e4-107">然後，您將發行 hello 函式程式碼 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="458e4-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="458e4-108">這些工具可在 Visual Studio 2017 版本 15.3，hello Azure 的開發工作負載的部分或更新版本。</span><span class="sxs-lookup"><span data-stu-id="458e4-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Visual Studio 專案中的 Azure Functions 程式碼](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="458e4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="458e4-110">Prerequisites</span></span>

<span data-ttu-id="458e4-111">toocomplete 此教學課程，安裝：</span><span class="sxs-lookup"><span data-stu-id="458e4-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="458e4-112">[Visual Studio 2017 版本 15.3](https://www.visualstudio.com/vs/preview/)，包括 hello **Azure 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="458e4-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![安裝 Visual Studio 2017 hello Azure 開發的工作負載](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="458e4-114">您安裝或升級 tooVisual Studio 2017 15.3 版本之後，您可能也需要 toomanually update hello Visual Studio 2017 工具 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="458e4-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="458e4-115">您可以更新從 hello hello 工具**工具**下的單**擴充功能和更新...**  > **更新** > **Visual Studio Marketplace** > **Azure 函式和 Web 工作工具** > **更新**。</span><span class="sxs-lookup"><span data-stu-id="458e4-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="458e4-116">在 Visual Studio 中建立 Azure Functions 專案</span><span class="sxs-lookup"><span data-stu-id="458e4-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="458e4-117">既然您已經建立 hello 專案，您可以建立您的第一個函式。</span><span class="sxs-lookup"><span data-stu-id="458e4-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="458e4-118">建立 hello 函式</span><span class="sxs-lookup"><span data-stu-id="458e4-118">Create hello function</span></span>

1. <span data-ttu-id="458e4-119">在 [方案總管] 中，於專案節點上按一下滑鼠右鍵，然後選取 [新增] > [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="458e4-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="458e4-120">選取 [Azure Function]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="458e4-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="458e4-121">選取 [HttpTrigger]，輸入 [函式名稱]，針對 [存取權限] 選取 [匿名]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="458e4-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="458e4-122">從任何用戶端的 HTTP 要求來存取建立 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="458e4-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![建立新的 Azure Function](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="458e4-124">程式碼檔案會加入 tooyour 專案，其中包含實作您的函式程式碼的類別。</span><span class="sxs-lookup"><span data-stu-id="458e4-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="458e4-125">此程式碼是以範本為基礎，會接收名稱值並將其回應回去。</span><span class="sxs-lookup"><span data-stu-id="458e4-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="458e4-126">hello **FunctionName**屬性設定函式的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="458e4-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="458e4-127">hello **HttpTrigger**屬性會指出觸發 hello 函式的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="458e4-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![函式程式碼檔案](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="458e4-129">您現在已建立 HTTP 觸發的函式，可以在本機電腦上進行測試。</span><span class="sxs-lookup"><span data-stu-id="458e4-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="458e4-130">在本機測試 hello 函式</span><span class="sxs-lookup"><span data-stu-id="458e4-130">Test hello function locally</span></span>

<span data-ttu-id="458e4-131">Azure Functions Core Tools 可讓您在本機開發電腦上執行 Azure Functions 專案。</span><span class="sxs-lookup"><span data-stu-id="458e4-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="458e4-132">您必須提示的 tooinstall 這些工具 hello 從 Visual Studio 啟動函式的第一次。</span><span class="sxs-lookup"><span data-stu-id="458e4-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="458e4-133">tootest 您的函式，請按 F5。</span><span class="sxs-lookup"><span data-stu-id="458e4-133">tootest your function, press F5.</span></span> <span data-ttu-id="458e4-134">如果出現提示，請接受從 Visual Studio toodownload hello 要求，並安裝 Azure 函式核心 (CLI) 工具。</span><span class="sxs-lookup"><span data-stu-id="458e4-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="458e4-135">您也可能需要 tooenable 防火牆例外，好讓 hello 工具可以處理 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="458e4-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="458e4-136">複製 hello URL 從 hello Azure 函式執行階段函式的輸出。</span><span class="sxs-lookup"><span data-stu-id="458e4-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Azure 本機執行階段](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="458e4-138">貼入您的瀏覽器位址列中的 hello hello HTTP 要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="458e4-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="458e4-139">附加 hello 查詢字串`&name=<yourname>`toothis URL，然後執行 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="458e4-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="458e4-140">hello 下列顯示 hello 回應 hello 瀏覽器 toohello 本機 GET 要求傳回的 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="458e4-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![函式 localhost 回應 hello 瀏覽器中](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="458e4-142">按一下 偵錯，toostop hello**停止**hello Visual Studio 工具列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="458e4-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="458e4-143">確認 hello 函式會在本機電腦上正確地執行之後，它是時間 toopublish hello 專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="458e4-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="458e4-144">發行 hello 專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="458e4-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="458e4-145">您的 Azure 訂用帳戶中必須具有函式應用程式，才可以發佈您的專案。</span><span class="sxs-lookup"><span data-stu-id="458e4-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="458e4-146">您可以直接從 Visual Studio 建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="458e4-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="458e4-147">在 Azure 中測試您的函式</span><span class="sxs-lookup"><span data-stu-id="458e4-147">Test your function in Azure</span></span>

1. <span data-ttu-id="458e4-148">複製 hello 發行設定檔 頁面中的 hello 的 hello 函式應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="458e4-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="458e4-149">取代 hello `localhost:port` hello URL 測試與 hello 新的基底 URL 在本機的 hello 函式時所使用的部分。</span><span class="sxs-lookup"><span data-stu-id="458e4-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="458e4-150">如往常一般，請確定 tooappend hello 查詢字串`&name=<yourname>`toothis URL，然後執行 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="458e4-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="458e4-151">呼叫您的 HTTP hello URL 觸發函式看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="458e4-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="458e4-152">貼入您的瀏覽器位址列中的 hello HTTP 要求的這個新的 URL。</span><span class="sxs-lookup"><span data-stu-id="458e4-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="458e4-153">hello 下列顯示 hello 回應 hello 瀏覽器 toohello 遠端 GET 要求傳回的 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="458e4-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Hello 瀏覽器中回應時間函式](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="458e4-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="458e4-155">Next steps</span></span>

<span data-ttu-id="458e4-156">您使用 Visual Studio toocreate C# 函式應用程式使用的簡單 HTTP 觸發函式。</span><span class="sxs-lookup"><span data-stu-id="458e4-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="458e4-157">toolearn 如何 tooconfigure 專案 toosupport 其他類型的觸發程序，以及繫結，請參閱 hello[設定 hello 專案以進行本機開發](functions-develop-vs.md#configure-the-project-for-local-development)一節中[Azure 函式 Tools for Visual Studio](functions-develop-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="458e4-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="458e4-158">toolearn 深入了解本機測試和偵錯使用 hello Azure 函式的核心工具，請參閱[程式碼和在本機測試 Azure 函式](functions-run-local.md)。</span><span class="sxs-lookup"><span data-stu-id="458e4-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="458e4-159">toolearn 進一步了解開發函式做為.NET 類別庫，請參閱[使用.NET 類別庫來搭配 Azure 函式](functions-dotnet-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="458e4-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

