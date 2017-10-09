---
title: "開發 Azure 函式 aaaGuidance |Microsoft 文件"
description: "了解 hello Azure 函式概念和技術，您需要在 Azure 中，所有的程式語言和繫結之間的 toodevelop 函式。"
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
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a><span data-ttu-id="f6ec8-104">Azure Functions 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="f6ec8-104">Azure Functions developers guide</span></span>
<span data-ttu-id="f6ec8-105">在 Azure 功能中，特定的功能會共用一些核心技術概念和元件，不論語言 hello 或您使用的繫結。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-105">In Azure Functions, specific functions share a few core technical concepts and components, regardless of hello language or binding you use.</span></span> <span data-ttu-id="f6ec8-106">您跳至了解給定的語言或繫結的詳細資料特定 tooa，先確定 tooread 透過適用於這些 tooall 本概觀。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-106">Before you jump into learning details specific tooa given language or binding, be sure tooread through this overview that applies tooall of them.</span></span>

<span data-ttu-id="f6ec8-107">本文章假設，您已閱讀 hello [Azure 函式概觀](functions-overview.md)並十分熟悉[WebJobs SDK 的概念，例如觸發程序，繫結和 hello JobHost 執行階段](../app-service-web/websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-107">This article assumes that you've already read hello [Azure Functions overview](functions-overview.md) and are familiar with [WebJobs SDK concepts such as triggers, bindings, and hello JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span> <span data-ttu-id="f6ec8-108">Azure 的函式根據 hello WebJobs SDK。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-108">Azure Functions is based on hello WebJobs SDK.</span></span> 

## <a name="function-code"></a><span data-ttu-id="f6ec8-109">函式程式碼</span><span class="sxs-lookup"><span data-stu-id="f6ec8-109">Function code</span></span>
<span data-ttu-id="f6ec8-110">A*函式*是 hello Azure 函式中的主要概念。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-110">A *function* is hello primary concept in Azure Functions.</span></span> <span data-ttu-id="f6ec8-111">您選擇的語言撰寫的函式的程式碼並儲存 hello 程式碼和組態檔中的 hello 相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-111">You write code for a function in a language of your choice and save hello code and configuration files in hello same folder.</span></span> <span data-ttu-id="f6ec8-112">hello 組態會命名為`function.json`，其中包含 JSON 組態資料。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-112">hello configuration is named `function.json`, which contains JSON configuration data.</span></span> <span data-ttu-id="f6ec8-113">支援各種不同的語言，和每個都有稍微不同的體驗最佳化 toowork 最適合該語言。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-113">Various languages are supported, and each one has a slightly different experience optimized toowork best for that language.</span></span> 

<span data-ttu-id="f6ec8-114">hello function.json 檔案定義 hello 函式繫結和其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-114">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="f6ec8-115">hello runtime 使用這個檔案 toodetermine hello 事件 toomonitor 和如何 toopass 資料到傳回的資料，從函式執行。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-115">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="f6ec8-116">hello 以下為範例 function.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-116">hello following is an example function.json file.</span></span>

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

<span data-ttu-id="f6ec8-117">設定 hello`disabled`屬性太`true`tooprevent hello 函式不會執行。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-117">Set hello `disabled` property too`true` tooprevent hello function from being executed.</span></span>

<span data-ttu-id="f6ec8-118">hello`bindings`屬性可讓您設定觸發程序和繫結。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-118">hello `bindings` property is where you configure both triggers and bindings.</span></span> <span data-ttu-id="f6ec8-119">每個繫結共用一些常見的設定和某些設定，這是特定 tooa 特定類型的繫結。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-119">Each binding shares a few common settings and some settings, which are specific tooa particular type of binding.</span></span> <span data-ttu-id="f6ec8-120">每一個繫結需要 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="f6ec8-120">Every binding requires hello following settings:</span></span>

| <span data-ttu-id="f6ec8-121">屬性</span><span class="sxs-lookup"><span data-stu-id="f6ec8-121">Property</span></span> | <span data-ttu-id="f6ec8-122">值/類型</span><span class="sxs-lookup"><span data-stu-id="f6ec8-122">Values/Types</span></span> | <span data-ttu-id="f6ec8-123">註解</span><span class="sxs-lookup"><span data-stu-id="f6ec8-123">Comments</span></span> |
| --- | --- | --- |
| `type` |<span data-ttu-id="f6ec8-124">string</span><span class="sxs-lookup"><span data-stu-id="f6ec8-124">string</span></span> |<span data-ttu-id="f6ec8-125">繫結類型。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-125">Binding type.</span></span> <span data-ttu-id="f6ec8-126">例如， `queueTrigger`。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-126">For example, `queueTrigger`.</span></span> |
| `direction` |<span data-ttu-id="f6ec8-127">'in'、'out'</span><span class="sxs-lookup"><span data-stu-id="f6ec8-127">'in', 'out'</span></span> |<span data-ttu-id="f6ec8-128">指出 hello 繫結是否接收到 hello 函式的資料或傳送的資料，從 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-128">Indicates whether hello binding is for receiving data into hello function or sending data from hello function.</span></span> |
| `name` |<span data-ttu-id="f6ec8-129">字串</span><span class="sxs-lookup"><span data-stu-id="f6ec8-129">string</span></span> |<span data-ttu-id="f6ec8-130">用於 hello hello 名稱繫結 hello 函式中的資料。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-130">hello name that is used for hello bound data in hello function.</span></span> <span data-ttu-id="f6ec8-131">C# 中，這是引數名稱;javascript，它的索引鍵/值清單中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-131">For C#, this is an argument name; for JavaScript, it's hello key in a key/value list.</span></span> |

## <a name="function-app"></a><span data-ttu-id="f6ec8-132">函式應用程式</span><span class="sxs-lookup"><span data-stu-id="f6ec8-132">Function app</span></span>
<span data-ttu-id="f6ec8-133">函式應用程式是由一或多個由 Azure App Service 一起管理的個別函式所組成。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-133">A function app is comprised of one or more individual functions that are managed together by Azure App Service.</span></span> <span data-ttu-id="f6ec8-134">所有函式應用程式共用中的 hello 函式 hello 相同定價計劃、 連續部署和執行階段版本。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-134">All of hello functions in a function app share hello same pricing plan, continuous deployment and runtime version.</span></span> <span data-ttu-id="f6ec8-135">函式的所有共用 hello 以多個語言可以撰寫相同函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-135">Functions written in multiple languages can all share hello same function app.</span></span> <span data-ttu-id="f6ec8-136">請將函式應用程式，為方法 tooorganize 來共同管理您的函式。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-136">Think of a function app as a way tooorganize and collectively manage your functions.</span></span> 

## <a name="runtime-script-host-and-web-host"></a><span data-ttu-id="f6ec8-137">執行階段 (指令碼主機和 Web 主機)</span><span class="sxs-lookup"><span data-stu-id="f6ec8-137">Runtime (script host and web host)</span></span>
<span data-ttu-id="f6ec8-138">hello 執行階段或指令碼主機是 hello 基礎 WebJobs SDK host 接聽事件，會收集並傳送資料，及最終會執行您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-138">hello runtime, or script host, is hello underlying WebJobs SDK host that listens for events, gathers and sends data, and ultimately runs your code.</span></span> 

<span data-ttu-id="f6ec8-139">toofacilitate HTTP 觸發程序，也是設計的 toosit 前面 hello 指令碼裝載在實際執行案例中的 web 主機。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-139">toofacilitate HTTP triggers, there is also a web host that is designed toosit in front of hello script host in production scenarios.</span></span> <span data-ttu-id="f6ec8-140">有兩部主機，可幫助 tooisolate hello script host hello 前端流量由 hello web 主機所管理。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-140">Having two hosts helps tooisolate hello script host from hello front end traffic managed by hello web host.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="f6ec8-141">資料夾結構</span><span class="sxs-lookup"><span data-stu-id="f6ec8-141">Folder Structure</span></span>
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="f6ec8-142">當設定 Azure App Service 中的函式 tooa 函式應用程式部署的專案，您可以將此資料夾結構與站台碼。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-142">When setting-up a project for deploying functions tooa function app in Azure App Service, you can treat this folder structure as your site code.</span></span> <span data-ttu-id="f6ec8-143">您可以使用現有工具 (如持續整合和部署) 或自訂部署指令碼來執行部署時間封裝安裝或程式碼 Transpilation。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-143">You can use existing tools like continuous integration and deployment, or custom deployment scripts for doing deploy time package installation or code transpilation.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ec8-144">請確定 toodeploy 您`host.json`檔案和函式資料夾直接 toohello`wwwroot`資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-144">Make sure toodeploy your `host.json` file and function folders directly toohello `wwwroot` folder.</span></span> <span data-ttu-id="f6ec8-145">不包含 hello`wwwroot`中您的部署資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-145">Do not include hello `wwwroot` folder in your deployments.</span></span> <span data-ttu-id="f6ec8-146">否則，您會得到 `wwwroot\wwwroot` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-146">Otherwise, you end up with `wwwroot\wwwroot` folders.</span></span> 
> 
> 

## <span data-ttu-id="f6ec8-147"><a id="fileupdate"></a>Tooupdate 應用程式檔案的運作方式</span><span class="sxs-lookup"><span data-stu-id="f6ec8-147"><a id="fileupdate"></a> How tooupdate function app files</span></span>
<span data-ttu-id="f6ec8-148">hello Azure 入口網站內建的 hello 函式編輯器可讓您更新 hello *function.json*檔案和 hello 函式的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-148">hello function editor built into hello Azure portal lets you update hello *function.json* file and hello code file for a function.</span></span> <span data-ttu-id="f6ec8-149">tooupload 或其他更新檔，例如*package.json*或*project.json*或相依性，您有 toouse 其他部署方法。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-149">tooupload or update other files such as *package.json* or *project.json* or dependencies, you have toouse other deployment methods.</span></span>

<span data-ttu-id="f6ec8-150">函式應用程式已內建應用程式服務，因此所有 hello[部署選項可用 toostandard web 應用程式](../app-service-web/web-sites-deploy.md)還有適用於函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-150">Function apps are built on App Service, so all hello [deployment options available toostandard web apps](../app-service-web/web-sites-deploy.md) are also available for function apps.</span></span> <span data-ttu-id="f6ec8-151">以下是一些您可以使用 tooupload 或更新函式應用程式檔案的方法。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-151">Here are some methods you can use tooupload or update function app files.</span></span> 

#### <a name="toouse-app-service-editor"></a><span data-ttu-id="f6ec8-152">toouse 應用程式服務編輯器</span><span class="sxs-lookup"><span data-stu-id="f6ec8-152">toouse App Service Editor</span></span>
1. <span data-ttu-id="f6ec8-153">在 hello Azure 函式入口網站中，按一下 **函式應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-153">In hello Azure Functions portal, click **Function app settings**.</span></span>
2. <span data-ttu-id="f6ec8-154">在 hello**進階設定**區段中，按一下**移 tooApp 服務設定**。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-154">In hello **Advanced Settings** section, click **Go tooApp Service Settings**.</span></span>
3. <span data-ttu-id="f6ec8-155">在 [應用程式功能表導覽] 中的 [開發工具] 底下，按一下 [App Service 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-155">Click **App Service Editor** in App Menu Nav under **DEVELOPMENT TOOLS**.</span></span>
4. <span data-ttu-id="f6ec8-156">按一下 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-156">click **Go**.</span></span>
   
   <span data-ttu-id="f6ec8-157">應用程式服務編輯器載入後，您會看到 hello *host.json*下的檔案和函式資料夾*wwwroot*。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-157">After App Service Editor loads, you'll see hello *host.json* file and function folders under *wwwroot*.</span></span> 
5. <span data-ttu-id="f6ec8-158">開啟檔案 tooedit 它們，或從拖放您開發機器 tooupload 檔案。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-158">Open files tooedit them, or drag and drop from your development machine tooupload files.</span></span>

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a><span data-ttu-id="f6ec8-159">toouse hello 函式應用程式的 SCM (Kudu) 端點</span><span class="sxs-lookup"><span data-stu-id="f6ec8-159">toouse hello function app's SCM (Kudu) endpoint</span></span>
1. <span data-ttu-id="f6ec8-160">瀏覽至 `https://<function_app_name>.scm.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-160">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span></span>
2. <span data-ttu-id="f6ec8-161">按一下 [偵錯主控台] > [CMD]。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-161">Click **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="f6ec8-162">瀏覽過`D:\home\site\wwwroot\`tooupdate *host.json*或`D:\home\site\wwwroot\<function_name>`tooupdate 函式的檔案。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-162">Navigate too`D:\home\site\wwwroot\` tooupdate *host.json* or `D:\home\site\wwwroot\<function_name>` tooupdate a function's files.</span></span>
4. <span data-ttu-id="f6ec8-163">拖放檔案，您想成 hello tooupload 適當 hello 檔案方格中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-163">Drag-and-drop a file you want tooupload into hello appropriate folder in hello file grid.</span></span> <span data-ttu-id="f6ec8-164">您將可以卸除檔案的 hello 檔案方格中有兩個區域。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-164">There are two areas in hello file grid where you can drop a file.</span></span> <span data-ttu-id="f6ec8-165">如*.zip*檔案，與 hello 標籤會出現一個方塊 」 將拖曳到此處 tooupload 與解壓縮。 」</span><span class="sxs-lookup"><span data-stu-id="f6ec8-165">For *.zip* files, a box appears with hello label "Drag here tooupload and unzip."</span></span> <span data-ttu-id="f6ec8-166">針對其他檔案類型，卸除 hello 檔案方格中，但 hello 」 解壓縮"方塊外。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-166">For other file types, drop in hello file grid but outside hello "unzip" box.</span></span>

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a><span data-ttu-id="f6ec8-167">toouse 連續部署</span><span class="sxs-lookup"><span data-stu-id="f6ec8-167">toouse continuous deployment</span></span>
<span data-ttu-id="f6ec8-168">請遵循 hello 主題中的 hello 指示[Azure 函式的連續部署](functions-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-168">Follow hello instructions in hello topic [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span>

## <a name="parallel-execution"></a><span data-ttu-id="f6ec8-169">平行執行</span><span class="sxs-lookup"><span data-stu-id="f6ec8-169">Parallel execution</span></span>
<span data-ttu-id="f6ec8-170">多個觸發事件發生時速度快過單一執行緒的函式執行階段可以處理它們，hello 執行階段可能會叫用數次以平行方式的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-170">When multiple triggering events occur faster than a single-threaded function runtime can process them, hello runtime may invoke hello function multiple times in parallel.</span></span>  <span data-ttu-id="f6ec8-171">如果函式的應用程式使用 hello[裝載計劃的耗用量](functions-scale.md#how-the-consumption-plan-works)，hello 函式應用程式無法自動向外擴充。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-171">If a function app is using hello [Consumption hosting plan](functions-scale.md#how-the-consumption-plan-works), hello function app could scale out automatically.</span></span>  <span data-ttu-id="f6ec8-172">Hello 函式應用程式，每個執行個體是否 hello 應用程式上執行 hello 裝載計劃或一般的耗用量[應用程式服務裝載計劃](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)，可能會處理透過多個執行緒並行函式引動過程。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-172">Each instance of hello function app, whether hello app runs on hello Consumption hosting plan or a regular [App Service hosting plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), might process concurrent function invocations in parallel using multiple threads.</span></span>  <span data-ttu-id="f6ec8-173">hello 並行函式引動過程中每個函式應用程式執行個體的數目上限依據觸發程序正由其他函式 hello 函式應用程式中的 hello 資源以及 hello 類型而異。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-173">hello maximum number of concurrent function invocations in each function app instance varies based on hello type of trigger being used as well as hello resources used by other functions within hello function app.</span></span>

## <a name="functions-runtime-versioning"></a><span data-ttu-id="f6ec8-174">Functions 執行階段版本設定</span><span class="sxs-lookup"><span data-stu-id="f6ec8-174">Functions runtime versioning</span></span>

<span data-ttu-id="f6ec8-175">您可以設定的 hello 函式執行階段使用 hello hello 版本`FUNCTIONS_EXTENSION_VERSION`應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-175">You can configure hello version of hello Functions runtime using hello `FUNCTIONS_EXTENSION_VERSION` app setting.</span></span> <span data-ttu-id="f6ec8-176">例如，hello 值"~ 1"表示函式應用程式會使用 1，因為它的主要版本。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-176">For example, hello value "~1" indicates that your Function App will use 1 as its major version.</span></span> <span data-ttu-id="f6ec8-177">函式應用程式的發行是升級的 tooeach 新次要版本。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-177">Function Apps are upgraded tooeach new minor version as they are released.</span></span> <span data-ttu-id="f6ec8-178">您可以在 hello 檢視 hello 函式應用程式的確切版本**設定**hello Azure 入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-178">You can view hello exact version of your Function App in hello **Settings** tab in hello Azure Portal.</span></span>

## <a name="repositories"></a><span data-ttu-id="f6ec8-179">儲存機制</span><span class="sxs-lookup"><span data-stu-id="f6ec8-179">Repositories</span></span>
<span data-ttu-id="f6ec8-180">hello Azure 函式的程式碼是開放原始碼，並儲存在 GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="f6ec8-180">hello code for Azure Functions is open source and stored in GitHub repositories:</span></span>

* [<span data-ttu-id="f6ec8-181">Azure Functions 執行階段</span><span class="sxs-lookup"><span data-stu-id="f6ec8-181">Azure Functions runtime</span></span>](https://github.com/Azure/azure-webjobs-sdk-script/)
* [<span data-ttu-id="f6ec8-182">Azure Functions 入口網站</span><span class="sxs-lookup"><span data-stu-id="f6ec8-182">Azure Functions portal</span></span>](https://github.com/projectkudu/AzureFunctionsPortal)
* [<span data-ttu-id="f6ec8-183">Azure Functions 範本</span><span class="sxs-lookup"><span data-stu-id="f6ec8-183">Azure Functions templates</span></span>](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [<span data-ttu-id="f6ec8-184">Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="f6ec8-184">Azure WebJobs SDK</span></span>](https://github.com/Azure/azure-webjobs-sdk/)
* [<span data-ttu-id="f6ec8-185">Azure WebJobs SDK 延伸模組</span><span class="sxs-lookup"><span data-stu-id="f6ec8-185">Azure WebJobs SDK Extensions</span></span>](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a><span data-ttu-id="f6ec8-186">繫結</span><span class="sxs-lookup"><span data-stu-id="f6ec8-186">Bindings</span></span>
<span data-ttu-id="f6ec8-187">以下是所有已支援繫結的表格。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-187">Here is a table of all supported bindings.</span></span>

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a><span data-ttu-id="f6ec8-188">報告問題</span><span class="sxs-lookup"><span data-stu-id="f6ec8-188">Reporting Issues</span></span>
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a><span data-ttu-id="f6ec8-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6ec8-189">Next steps</span></span>
<span data-ttu-id="f6ec8-190">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="f6ec8-190">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="f6ec8-191">Azure Functions 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="f6ec8-191">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="f6ec8-192">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="f6ec8-192">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="f6ec8-193">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="f6ec8-193">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="f6ec8-194">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="f6ec8-194">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="f6ec8-195">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="f6ec8-195">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* <span data-ttu-id="f6ec8-196">[Azure 的函式： hello 旅程](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/)hello Azure 應用程式服務團隊部落格上。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-196">[Azure Functions: hello Journey](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) on hello Azure App Service team blog.</span></span> <span data-ttu-id="f6ec8-197">Azure Functions 的開發歷史。</span><span class="sxs-lookup"><span data-stu-id="f6ec8-197">A history of how Azure Functions was developed.</span></span>

