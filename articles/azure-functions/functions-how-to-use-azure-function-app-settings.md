---
title: "設定 Azure 函數應用程式的設定 | Microsoft Docs"
description: "了解如何設定 Azure Functions 應用程式設定。"
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="c6d1c-103">如何在 Azure 入口網站中管理函數應用程式</span><span class="sxs-lookup"><span data-stu-id="c6d1c-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="c6d1c-104">在 Azure Functions 中，函數應用程式會提供個別函數的執行內容。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="c6d1c-105">函數應用程式行為會套用至指定之函數應用程式所裝載的所有函數。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="c6d1c-106">本主題說明如何在 Azure 入口網站中，設定和管理您的函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="c6d1c-107">若要開始，請移至 [Azure 入口網站](http://portal.azure.com)，然後登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="c6d1c-108">在入口網站頂端的搜尋列中，輸入函數應用程式的名稱，然後從清單中選取它。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="c6d1c-109">選取函數應用程式之後，您會看到下列頁面：</span><span class="sxs-lookup"><span data-stu-id="c6d1c-109">After selecting your function app, you see the following page:</span></span>

![Azure 入口網站中的函數應用程式概觀](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="c6d1c-111"><a name="manage-app-service-settings"></a>函數應用程式設定索引標籤</span><span class="sxs-lookup"><span data-stu-id="c6d1c-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Azure 入口網站中的函數應用程式概觀。](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="c6d1c-113">[設定] 索引標籤可供您更新函數應用程式所使用的 Functions 執行階段版本。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="c6d1c-114">您也可以在此處管理主機金鑰，這些金鑰可用來限制對函數應用程式所裝載之所有函數的 HTTP 存取。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="c6d1c-115">Functions 支援「取用」主控方案和 App Service 主控方案。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="c6d1c-116">如需詳細資訊，請參閱[選擇正確的 Azure Functions 服務方案](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="c6d1c-117">為了在「取用」方案中提升可預測性，Functions 可讓您設定每日使用量配額 (以 GB-秒為單位) 來限制平台使用量。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="c6d1c-118">一旦達到每日使用量配額，系統就會停止函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="c6d1c-119">針對因達到花費配額而停止運作的函數應用程式，您可以從與建立每日花費配額相同的內容中予以重新啟用。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="c6d1c-120">如需有關計費的詳細資料，請參閱 [Azure Functions 定價頁面](http://azure.microsoft.com/pricing/details/functions/)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="c6d1c-121">平台功能索引標籤</span><span class="sxs-lookup"><span data-stu-id="c6d1c-121">Platform features tab</span></span>

![函數應用程式平台功能索引標籤。](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="c6d1c-123">函數應用程式是在 Azure App Service 平台中執行並由此平台維護。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="c6d1c-124">因此，您的函數應用程式可以存取 Azure 核心虛擬主機平台的大多數功能。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="c6d1c-125">[平台功能] 索引標籤可供您存取許多可在函數應用程式中使用的 App Service 平台功能。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="c6d1c-126">當函數應用程式在「取用」主控方案上執行時，並非所有 App Service 功能都可供使用。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="c6d1c-127">本主題的其餘部分將把焦點放在 Azure 入口網站中對 Functions 實用的下列 App Service 功能：</span><span class="sxs-lookup"><span data-stu-id="c6d1c-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="c6d1c-128">App Service 編輯器</span><span class="sxs-lookup"><span data-stu-id="c6d1c-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="c6d1c-129">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="c6d1c-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="c6d1c-130">Console</span><span class="sxs-lookup"><span data-stu-id="c6d1c-130">Console</span></span>](#console)
+ [<span data-ttu-id="c6d1c-131">進階工具 (Kudu)</span><span class="sxs-lookup"><span data-stu-id="c6d1c-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="c6d1c-132">部署選項</span><span class="sxs-lookup"><span data-stu-id="c6d1c-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="c6d1c-133">CORS</span><span class="sxs-lookup"><span data-stu-id="c6d1c-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="c6d1c-134">驗證</span><span class="sxs-lookup"><span data-stu-id="c6d1c-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="c6d1c-135">API 定義</span><span class="sxs-lookup"><span data-stu-id="c6d1c-135">API definition</span></span>](#swagger)

<span data-ttu-id="c6d1c-136">如需有關如何使用 App Service 設定的詳細資訊，請參閱[設定 Azure App Service 設定](../app-service-web/web-sites-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="c6d1c-137"><a name="editor"></a>App Service 編輯器</span><span class="sxs-lookup"><span data-stu-id="c6d1c-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![函數應用程式 App Service 編輯器。](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="c6d1c-139">App Service 編輯器是一個進階的入口網站內編輯器，可供您用來修改 JSON 組態檔和類似的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="c6d1c-140">選擇此選項會啟動一個含有基本編輯器的個別瀏覽器索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="c6d1c-141">這可讓您與 Git 存放庫整合、執行程式碼和進行偵錯，以及修改函數應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="c6d1c-142">與預設的函數應用程式刀鋒視窗相比，此編輯器為您的函數提供一個強化的開發環境。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![App Service 編輯器](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="c6d1c-144"><a name="settings"></a>應用程式設定</span><span class="sxs-lookup"><span data-stu-id="c6d1c-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![函數應用程式的應用程式設定。](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="c6d1c-146">App Service [應用程式設定] 刀鋒視窗可供您設定和管理架構版本、遠端偵錯、應用程式設定及連接字串。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="c6d1c-147">當您將函數應用程式與其他 Azure 和協力廠商服務整合時，可以在這裡修改那些設定值。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![設定應用程式設定](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="c6d1c-149"><a name="console"></a>主控台</span><span class="sxs-lookup"><span data-stu-id="c6d1c-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Azure 入口網站中的函數應用程式主控台](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="c6d1c-151">當您偏好從命令列與函數應用程式進行互動時，入口網站內主控台是一個理想的開發人員工具。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="c6d1c-152">常用命令包含目錄和檔案建立與瀏覽，以及執行批次檔和指令碼。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![函數應用程式主控台](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="c6d1c-154"><a name="kudu"></a>進階工具 (Kudu)</span><span class="sxs-lookup"><span data-stu-id="c6d1c-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Azure 入口網站中的函數應用程式 Kudu](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="c6d1c-156">App Service 的進階工具 (也稱為 Kudu) 可讓您存取函數應用程式的進階系統管理功能。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="c6d1c-157">從 Kudu，您可以管理系統資訊、應用程式設定、環境變數、網站擴充功能、HTTP 標頭，以及伺服器變數。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="c6d1c-158">您也可以透過瀏覽至函數應用程式的 SCM 端點 (例如 `https://<myfunctionapp>.scm.azurewebsites.net/`) 來啟動 **Kudu**</span><span class="sxs-lookup"><span data-stu-id="c6d1c-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![設定 Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="c6d1c-160"><a name="deployment">部署選項</span><span class="sxs-lookup"><span data-stu-id="c6d1c-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Azure 入口網站中的函數應用程式部署選項](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="c6d1c-162">Functions 可讓您在本機電腦上開發函數程式碼。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="c6d1c-163">您可以接著將本機函數應用程式專案上傳到 Azure。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="c6d1c-164">除了傳統 FTP 上傳之外，Functions 還可讓您使用常用的持續整合解決方案 (例如 GitHub、VSTS、Dropbox、Bitbucket 等) 來部署函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="c6d1c-165">如需詳細資訊，請參閱 [Azure Functions 的持續部署](functions-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="c6d1c-166">若要使用 FTP 或本機 Git 來手動上傳，您還必須[設定您的部署認證](functions-continuous-deployment.md#credentials)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="c6d1c-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="c6d1c-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Azure 入口網站中的函數應用程式 CORS](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="c6d1c-169">為了防止惡意程式碼在您的服務中執行，App Service 會封鎖外部來源對您函數應用程式的呼叫。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="c6d1c-170">Functions 支援跨原始來源資源共用 (CORS)，可讓您定義您函數可從中接受遠端要求的允許原始來源「白名單」。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![設定函數應用程式的 CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="c6d1c-172"><a name="auth"></a>驗證</span><span class="sxs-lookup"><span data-stu-id="c6d1c-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Azure 入口網站中的函數應用程式驗證](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="c6d1c-174">當函數使用 HTTP 觸發程序時，您可以要求呼叫必須先經過驗證。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="c6d1c-175">App Service 支援 Azure Active Directory 驗證，以及使用社交提供者 (例如 Facebook、Microsoft 及 Twitter) 來登入。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="c6d1c-176">如需設定特定驗證提供者的詳細資訊，請參閱 [Azure App Service 驗證概觀](../app-service/app-service-authentication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![設定函數應用程式的驗證](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="c6d1c-178"><a name="swagger"></a>API 定義</span><span class="sxs-lookup"><span data-stu-id="c6d1c-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Azure 入口網站中的函數應用程式 API Swagger](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="c6d1c-180">Functions 支援 Swagger，可讓用戶端更容易使用 HTTP 觸發的函數。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="c6d1c-181">如需有關如何使用 Swagger 建立 API 定義的詳細資訊，請瀏覽[在 Azure 中開始使用 API Apps、ASP.NET 和 Swagger](../app-service-api/app-service-api-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="c6d1c-182">您也可以使用 Functions Proxy 來為多個函數定義一個單一的 API 介面。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="c6d1c-183">如需詳細資訊，請參閱[使用 Azure Functions Proxy](functions-proxies.md)。</span><span class="sxs-lookup"><span data-stu-id="c6d1c-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![設定函數應用程式的 API](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="c6d1c-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6d1c-185">Next steps</span></span>

+ [<span data-ttu-id="c6d1c-186">設定 Azure App Service 設定</span><span class="sxs-lookup"><span data-stu-id="c6d1c-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="c6d1c-187">Azure Functions 的持續部署</span><span class="sxs-lookup"><span data-stu-id="c6d1c-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



