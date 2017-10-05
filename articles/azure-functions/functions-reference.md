---
title: "Azure Functions 開發指引 | Microsoft Docs"
description: "了解在 Azure 中開發函式所需的 Azure Functions 概念與技術，其中包含所有的程式設計語言和繫結。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "開發指南, azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 879be48150cfe13e31064475aa637f13f5f5f9d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-developers-guide"></a><span data-ttu-id="b4dc9-104">Azure Functions 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="b4dc9-104">Azure Functions developers guide</span></span>
<span data-ttu-id="b4dc9-105">在 Azure Functions 中，不論您使用何種語言或繫結，特定函式都會共用一些核心技術概念和元件。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-105">In Azure Functions, specific functions share a few core technical concepts and components, regardless of the language or binding you use.</span></span> <span data-ttu-id="b4dc9-106">閱讀指定語言或繫結特有的詳細資料之前，請務必詳閱這份適用於所有語言或繫結的概觀。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-106">Before you jump into learning details specific to a given language or binding, be sure to read through this overview that applies to all of them.</span></span>

<span data-ttu-id="b4dc9-107">本文假設您已閱讀過 [Azure Functions 概觀](functions-overview.md)，並熟悉 [WebJobs SDK 概念 (例如觸發程序、繫結和 JobHost 執行階段)](../app-service-web/websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-107">This article assumes that you've already read the [Azure Functions overview](functions-overview.md) and are familiar with [WebJobs SDK concepts such as triggers, bindings, and the JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span> <span data-ttu-id="b4dc9-108">Azure Functions 是以 WebJobs SDK 為基礎。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-108">Azure Functions is based on the WebJobs SDK.</span></span> 

## <a name="function-code"></a><span data-ttu-id="b4dc9-109">函式程式碼</span><span class="sxs-lookup"><span data-stu-id="b4dc9-109">Function code</span></span>
<span data-ttu-id="b4dc9-110">「函數」  是 Azure Functions 中的主要概念。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-110">A *function* is the primary concept in Azure Functions.</span></span> <span data-ttu-id="b4dc9-111">您使用選擇的語言撰寫函式的程式碼，並將程式碼和組態檔儲存在相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-111">You write code for a function in a language of your choice and save the code and configuration files in the same folder.</span></span> <span data-ttu-id="b4dc9-112">組態會命名為 `function.json`，其中包含 JSON 組態資料。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-112">The configuration is named `function.json`, which contains JSON configuration data.</span></span> <span data-ttu-id="b4dc9-113">支援各種語言，而且每種語言的最適合最佳化經驗稍有不同。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-113">Various languages are supported, and each one has a slightly different experience optimized to work best for that language.</span></span> 

<span data-ttu-id="b4dc9-114">function.json 檔案會定義函式繫結和其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-114">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="b4dc9-115">執行階段使用此檔案來判斷要監視的事件，以及如何傳入資料並從函式執行傳回資料。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-115">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="b4dc9-116">以下是範例 function.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-116">The following is an example function.json file.</span></span>

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

<span data-ttu-id="b4dc9-117">將 `disabled` 屬性設定為 `true` 以防止函式執行。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-117">Set the `disabled` property to `true` to prevent the function from being executed.</span></span>

<span data-ttu-id="b4dc9-118">`bindings` 屬性可讓您設定觸發程序和繫結。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-118">The `bindings` property is where you configure both triggers and bindings.</span></span> <span data-ttu-id="b4dc9-119">每個繫結都共用一些共用設定，以及特定類別的繫結特有的一些設定。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-119">Each binding shares a few common settings and some settings, which are specific to a particular type of binding.</span></span> <span data-ttu-id="b4dc9-120">每個繫結都需要下列設定︰</span><span class="sxs-lookup"><span data-stu-id="b4dc9-120">Every binding requires the following settings:</span></span>

| <span data-ttu-id="b4dc9-121">屬性</span><span class="sxs-lookup"><span data-stu-id="b4dc9-121">Property</span></span> | <span data-ttu-id="b4dc9-122">值/類型</span><span class="sxs-lookup"><span data-stu-id="b4dc9-122">Values/Types</span></span> | <span data-ttu-id="b4dc9-123">註解</span><span class="sxs-lookup"><span data-stu-id="b4dc9-123">Comments</span></span> |
| --- | --- | --- |
| `type` |<span data-ttu-id="b4dc9-124">string</span><span class="sxs-lookup"><span data-stu-id="b4dc9-124">string</span></span> |<span data-ttu-id="b4dc9-125">繫結類型。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-125">Binding type.</span></span> <span data-ttu-id="b4dc9-126">例如， `queueTrigger`。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-126">For example, `queueTrigger`.</span></span> |
| `direction` |<span data-ttu-id="b4dc9-127">'in'、'out'</span><span class="sxs-lookup"><span data-stu-id="b4dc9-127">'in', 'out'</span></span> |<span data-ttu-id="b4dc9-128">表示繫結用於將資料接收到函數，還是從函數傳送資料。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-128">Indicates whether the binding is for receiving data into the function or sending data from the function.</span></span> |
| `name` |<span data-ttu-id="b4dc9-129">string</span><span class="sxs-lookup"><span data-stu-id="b4dc9-129">string</span></span> |<span data-ttu-id="b4dc9-130">用於函式中所繫結資料的名稱。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-130">The name that is used for the bound data in the function.</span></span> <span data-ttu-id="b4dc9-131">在 C# 中，這是引數名稱；在 JavaScript 中，這是索引鍵/值清單中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-131">For C#, this is an argument name; for JavaScript, it's the key in a key/value list.</span></span> |

## <a name="function-app"></a><span data-ttu-id="b4dc9-132">函式應用程式</span><span class="sxs-lookup"><span data-stu-id="b4dc9-132">Function app</span></span>
<span data-ttu-id="b4dc9-133">函式應用程式是由一或多個由 Azure App Service 一起管理的個別函式所組成。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-133">A function app is comprised of one or more individual functions that are managed together by Azure App Service.</span></span> <span data-ttu-id="b4dc9-134">函式應用程式中的所有函式會共用相同的定價方案、持續部署和執行階段版本。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-134">All of the functions in a function app share the same pricing plan, continuous deployment and runtime version.</span></span> <span data-ttu-id="b4dc9-135">以多種語言撰寫的函式全都可以共用相同的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-135">Functions written in multiple languages can all share the same function app.</span></span> <span data-ttu-id="b4dc9-136">請將函式應用程式視為用來組織及集體管理函式的方式。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-136">Think of a function app as a way to organize and collectively manage your functions.</span></span> 

## <a name="runtime-script-host-and-web-host"></a><span data-ttu-id="b4dc9-137">執行階段 (指令碼主機和 Web 主機)</span><span class="sxs-lookup"><span data-stu-id="b4dc9-137">Runtime (script host and web host)</span></span>
<span data-ttu-id="b4dc9-138">執行階段 (或指令碼主機) 是基礎 WebJobs SDK 主機，可接聽事件、收集和傳送資料，最後執行您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-138">The runtime, or script host, is the underlying WebJobs SDK host that listens for events, gathers and sends data, and ultimately runs your code.</span></span> 

<span data-ttu-id="b4dc9-139">為了簡化 HTTP 觸發程序，還可以使用 Web 主機，其設計是位在實際執行案例中指令碼主機的前面。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-139">To facilitate HTTP triggers, there is also a web host that is designed to sit in front of the script host in production scenarios.</span></span> <span data-ttu-id="b4dc9-140">擁有兩部主機有助於隔離指令碼主機與 Web 主機所管理的前端流量。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-140">Having two hosts helps to isolate the script host from the front end traffic managed by the web host.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="b4dc9-141">資料夾結構</span><span class="sxs-lookup"><span data-stu-id="b4dc9-141">Folder Structure</span></span>
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="b4dc9-142">設定專案以將函式部署至 Azure App Service 中的函式應用程式時，您可以將此資料夾結構視為您的網站程式碼。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-142">When setting-up a project for deploying functions to a function app in Azure App Service, you can treat this folder structure as your site code.</span></span> <span data-ttu-id="b4dc9-143">您可以使用現有工具 (如持續整合和部署) 或自訂部署指令碼來執行部署時間封裝安裝或程式碼 Transpilation。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-143">You can use existing tools like continuous integration and deployment, or custom deployment scripts for doing deploy time package installation or code transpilation.</span></span>

> [!NOTE]
> <span data-ttu-id="b4dc9-144">請務必將 `host.json` 檔案和函式資料夾直接部署至 `wwwroot` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-144">Make sure to deploy your `host.json` file and function folders directly to the `wwwroot` folder.</span></span> <span data-ttu-id="b4dc9-145">您的部署中請勿包含 `wwwroot` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-145">Do not include the `wwwroot` folder in your deployments.</span></span> <span data-ttu-id="b4dc9-146">否則，您會得到 `wwwroot\wwwroot` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-146">Otherwise, you end up with `wwwroot\wwwroot` folders.</span></span> 
> 
> 

## <span data-ttu-id="b4dc9-147"><a id="fileupdate"></a> 如何更新函式應用程式檔案</span><span class="sxs-lookup"><span data-stu-id="b4dc9-147"><a id="fileupdate"></a> How to update function app files</span></span>
<span data-ttu-id="b4dc9-148">Azure 入口網站內建的函式編輯器可讓您更新「function.json」  檔案和函式的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-148">The function editor built into the Azure portal lets you update the *function.json* file and the code file for a function.</span></span> <span data-ttu-id="b4dc9-149">若要上傳或更新其他檔案 (例如 *package.json*、*project.json* 或相依項目)，您必須使用其他部署方法。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-149">To upload or update other files such as *package.json* or *project.json* or dependencies, you have to use other deployment methods.</span></span>

<span data-ttu-id="b4dc9-150">函式應用程式建置於 App Service 之上，因此[標準 Web 應用程式可用的部署選項](../app-service-web/web-sites-deploy.md)也可供函式應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-150">Function apps are built on App Service, so all the [deployment options available to standard web apps](../app-service-web/web-sites-deploy.md) are also available for function apps.</span></span> <span data-ttu-id="b4dc9-151">以下是一些您可以用來上傳或更新函式應用程式檔案的方法。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-151">Here are some methods you can use to upload or update function app files.</span></span> 

#### <a name="to-use-app-service-editor"></a><span data-ttu-id="b4dc9-152">使用 App Service 編輯器</span><span class="sxs-lookup"><span data-stu-id="b4dc9-152">To use App Service Editor</span></span>
1. <span data-ttu-id="b4dc9-153">在 Azure Functions 入口網站中，按一下 [函式應用程式設定] 。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-153">In the Azure Functions portal, click **Function app settings**.</span></span>
2. <span data-ttu-id="b4dc9-154">在 [進階設定] 區段中，按一下 [前往 App Service 設定]。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-154">In the **Advanced Settings** section, click **Go to App Service Settings**.</span></span>
3. <span data-ttu-id="b4dc9-155">在 [應用程式功能表導覽] 中的 [開發工具] 底下，按一下 [App Service 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-155">Click **App Service Editor** in App Menu Nav under **DEVELOPMENT TOOLS**.</span></span>
4. <span data-ttu-id="b4dc9-156">按一下 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-156">click **Go**.</span></span>
   
   <span data-ttu-id="b4dc9-157">在「App Service 編輯器」載入之後，您將會在 [wwwroot] 底下看見 *host.json* 檔案和函式資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-157">After App Service Editor loads, you'll see the *host.json* file and function folders under *wwwroot*.</span></span> 
5. <span data-ttu-id="b4dc9-158">開啟檔案加以編輯，或從您的開發電腦拖放檔案以上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-158">Open files to edit them, or drag and drop from your development machine to upload files.</span></span>

#### <a name="to-use-the-function-apps-scm-kudu-endpoint"></a><span data-ttu-id="b4dc9-159">使用函式應用程式的 SCM (Kudu) 端點</span><span class="sxs-lookup"><span data-stu-id="b4dc9-159">To use the function app's SCM (Kudu) endpoint</span></span>
1. <span data-ttu-id="b4dc9-160">瀏覽至 `https://<function_app_name>.scm.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-160">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span></span>
2. <span data-ttu-id="b4dc9-161">按一下 [偵錯主控台] > [CMD]。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-161">Click **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="b4dc9-162">瀏覽至 `D:\home\site\wwwroot\` 以更新 *host.json*，或瀏覽至 `D:\home\site\wwwroot\<function_name>` 以更新函式的檔案。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-162">Navigate to `D:\home\site\wwwroot\` to update *host.json* or `D:\home\site\wwwroot\<function_name>` to update a function's files.</span></span>
4. <span data-ttu-id="b4dc9-163">將您要上傳的檔案拖放至檔案方格中適當資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-163">Drag-and-drop a file you want to upload into the appropriate folder in the file grid.</span></span> <span data-ttu-id="b4dc9-164">在檔案方格上您有兩個區域可以拖放檔案。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-164">There are two areas in the file grid where you can drop a file.</span></span> <span data-ttu-id="b4dc9-165">對於「.zip」  檔案，方塊顯示且具有標籤「拖曳到這裡以上傳和解壓縮」。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-165">For *.zip* files, a box appears with the label "Drag here to upload and unzip."</span></span> <span data-ttu-id="b4dc9-166">對於其他檔案類型，在檔案方格上但是在「解壓縮」方塊外拖放。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-166">For other file types, drop in the file grid but outside the "unzip" box.</span></span>

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on the consumption plan --DonnaM -->

#### <a name="to-use-continuous-deployment"></a><span data-ttu-id="b4dc9-167">使用持續部署</span><span class="sxs-lookup"><span data-stu-id="b4dc9-167">To use continuous deployment</span></span>
<span data-ttu-id="b4dc9-168">請依照 [Azure Functions 的持續部署](functions-continuous-deployment.md)主題中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-168">Follow the instructions in the topic [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span>

## <a name="parallel-execution"></a><span data-ttu-id="b4dc9-169">平行執行</span><span class="sxs-lookup"><span data-stu-id="b4dc9-169">Parallel execution</span></span>
<span data-ttu-id="b4dc9-170">發生速度比單一執行緒函數執行階段快的多個觸發事件可以處理它們時，執行階段可能會平行多次叫用函數。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-170">When multiple triggering events occur faster than a single-threaded function runtime can process them, the runtime may invoke the function multiple times in parallel.</span></span>  <span data-ttu-id="b4dc9-171">如果函式應用程式使用[取用主控方案](functions-scale.md#how-the-consumption-plan-works)，則函式應用程式可以自動相應放大。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-171">If a function app is using the [Consumption hosting plan](functions-scale.md#how-the-consumption-plan-works), the function app could scale out automatically.</span></span>  <span data-ttu-id="b4dc9-172">不論應用程式是在取用主控方案還是一般 [App Service 主控方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)上執行，函式應用程式的每個執行個體可能都會使用多個執行緒平行處理並行函式引動。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-172">Each instance of the function app, whether the app runs on the Consumption hosting plan or a regular [App Service hosting plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), might process concurrent function invocations in parallel using multiple threads.</span></span>  <span data-ttu-id="b4dc9-173">每個函式應用程式執行個體中的並行函式叫用次數上限，根據使用的觸發程序類型及函式應用程式內其他函式所使用的資源而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-173">The maximum number of concurrent function invocations in each function app instance varies based on the type of trigger being used as well as the resources used by other functions within the function app.</span></span>

## <a name="functions-runtime-versioning"></a><span data-ttu-id="b4dc9-174">Functions 執行階段版本設定</span><span class="sxs-lookup"><span data-stu-id="b4dc9-174">Functions runtime versioning</span></span>

<span data-ttu-id="b4dc9-175">您可以使用 `FUNCTIONS_EXTENSION_VERSION` 應用程式設定來設定 Functions 執行階段的版本。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-175">You can configure the version of the Functions runtime using the `FUNCTIONS_EXTENSION_VERSION` app setting.</span></span> <span data-ttu-id="b4dc9-176">例如，值 "~1" 表示您的函數應用程式會使用 1 做為主要版本。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-176">For example, the value "~1" indicates that your Function App will use 1 as its major version.</span></span> <span data-ttu-id="b4dc9-177">函數應用程式會在發行時升級為每個新的次要版本。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-177">Function Apps are upgraded to each new minor version as they are released.</span></span> <span data-ttu-id="b4dc9-178">您可以在 Azure 入口網站的 [設定] 索引標籤中檢視函數應用程式的正確版本。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-178">You can view the exact version of your Function App in the **Settings** tab in the Azure Portal.</span></span>

## <a name="repositories"></a><span data-ttu-id="b4dc9-179">儲存機制</span><span class="sxs-lookup"><span data-stu-id="b4dc9-179">Repositories</span></span>
<span data-ttu-id="b4dc9-180">Azure Functions 的程式碼是開放原始碼，儲存於 GitHub 儲存機制中︰</span><span class="sxs-lookup"><span data-stu-id="b4dc9-180">The code for Azure Functions is open source and stored in GitHub repositories:</span></span>

* [<span data-ttu-id="b4dc9-181">Azure Functions 執行階段</span><span class="sxs-lookup"><span data-stu-id="b4dc9-181">Azure Functions runtime</span></span>](https://github.com/Azure/azure-webjobs-sdk-script/)
* [<span data-ttu-id="b4dc9-182">Azure Functions 入口網站</span><span class="sxs-lookup"><span data-stu-id="b4dc9-182">Azure Functions portal</span></span>](https://github.com/projectkudu/AzureFunctionsPortal)
* [<span data-ttu-id="b4dc9-183">Azure Functions 範本</span><span class="sxs-lookup"><span data-stu-id="b4dc9-183">Azure Functions templates</span></span>](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [<span data-ttu-id="b4dc9-184">Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="b4dc9-184">Azure WebJobs SDK</span></span>](https://github.com/Azure/azure-webjobs-sdk/)
* [<span data-ttu-id="b4dc9-185">Azure WebJobs SDK 延伸模組</span><span class="sxs-lookup"><span data-stu-id="b4dc9-185">Azure WebJobs SDK Extensions</span></span>](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a><span data-ttu-id="b4dc9-186">繫結</span><span class="sxs-lookup"><span data-stu-id="b4dc9-186">Bindings</span></span>
<span data-ttu-id="b4dc9-187">以下是所有已支援繫結的表格。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-187">Here is a table of all supported bindings.</span></span>

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a><span data-ttu-id="b4dc9-188">報告問題</span><span class="sxs-lookup"><span data-stu-id="b4dc9-188">Reporting Issues</span></span>
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a><span data-ttu-id="b4dc9-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4dc9-189">Next steps</span></span>
<span data-ttu-id="b4dc9-190">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="b4dc9-190">For more information, see the following resources:</span></span>

* [<span data-ttu-id="b4dc9-191">Azure Functions 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="b4dc9-191">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="b4dc9-192">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="b4dc9-192">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="b4dc9-193">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="b4dc9-193">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="b4dc9-194">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="b4dc9-194">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="b4dc9-195">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="b4dc9-195">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* <span data-ttu-id="b4dc9-196">[Azure Functions︰Azure App Service 團隊部落格上的旅程](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) 。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-196">[Azure Functions: The Journey](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) on the Azure App Service team blog.</span></span> <span data-ttu-id="b4dc9-197">Azure Functions 的開發歷史。</span><span class="sxs-lookup"><span data-stu-id="b4dc9-197">A history of how Azure Functions was developed.</span></span>

