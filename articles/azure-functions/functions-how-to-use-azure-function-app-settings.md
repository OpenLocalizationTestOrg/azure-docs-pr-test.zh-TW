---
title: "aaaConfigure Azure 函式應用程式設定 |Microsoft 文件"
description: "了解 tooconfigure Azure 應用程式設定的運作方式。"
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
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="014d7-103">如何 toomanage 函式中的應用程式 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="014d7-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="014d7-104">Azure 功能中的函式應用程式會提供個別函式 hello 執行內容。</span><span class="sxs-lookup"><span data-stu-id="014d7-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="014d7-105">函式應用程式行為套用 tooall 函式所指定的函式應用程式裝載。</span><span class="sxs-lookup"><span data-stu-id="014d7-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="014d7-106">本主題描述如何 tooconfigure 及管理在 hello Azure 入口網站應用程式函式。</span><span class="sxs-lookup"><span data-stu-id="014d7-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="014d7-107">toobegin，移 toohello [Azure 入口網站](http://portal.azure.com)並登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="014d7-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="014d7-108">在 hello 在 hello hello 入口網站頂端搜尋列中輸入 hello 函式應用程式名稱，並從 hello 清單中選取。</span><span class="sxs-lookup"><span data-stu-id="014d7-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="014d7-109">選取函式應用程式之後, 您會看到下列頁面的 hello:</span><span class="sxs-lookup"><span data-stu-id="014d7-109">After selecting your function app, you see hello following page:</span></span>

![在 hello Azure 入口網站中的函式應用程式概觀](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="014d7-111"><a name="manage-app-service-settings"></a>函數應用程式設定索引標籤</span><span class="sxs-lookup"><span data-stu-id="014d7-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![函式在 hello Azure 入口網站應用程式概觀。](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="014d7-113">hello**設定** 索引標籤是您可以在其中更新函式應用程式所使用的 hello 函式執行階段版本。</span><span class="sxs-lookup"><span data-stu-id="014d7-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="014d7-114">它也是您用來管理 hello 主機使用的索引鍵 toorestrict HTTP 存取 tooall 函式 hello 函式應用程式所裝載。</span><span class="sxs-lookup"><span data-stu-id="014d7-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="014d7-115">Functions 支援「取用」主控方案和 App Service 主控方案。</span><span class="sxs-lookup"><span data-stu-id="014d7-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="014d7-116">如需詳細資訊，請參閱[Azure 函式選擇 hello 正確的服務方案](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="014d7-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="014d7-117">可預測性更好 hello 耗用量計劃中，函式可讓您藉由設定以 gb 為單位秒為單位的每日使用量配額，限制平台使用。</span><span class="sxs-lookup"><span data-stu-id="014d7-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="014d7-118">一旦達到 hello 每日使用量配額，就會停止 hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="014d7-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="014d7-119">已停止，因為達到消費配額的 hello 函式應用程式可以從 hello 重新啟用相同的內容，做為建立每日花配額 hello。</span><span class="sxs-lookup"><span data-stu-id="014d7-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="014d7-120">請參閱 hello [Azure 函式定價頁面](http://azure.microsoft.com/pricing/details/functions/)如需計費的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="014d7-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="014d7-121">平台功能索引標籤</span><span class="sxs-lookup"><span data-stu-id="014d7-121">Platform features tab</span></span>

![函數應用程式平台功能索引標籤。](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="014d7-123">函式應用程式中，執行，並且會維護，hello Azure 應用程式服務平台。</span><span class="sxs-lookup"><span data-stu-id="014d7-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="014d7-124">因此，您的函式應用程式可以存取 toomost hello Azure 的核心 web 裝載平台的功能。</span><span class="sxs-lookup"><span data-stu-id="014d7-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="014d7-125">hello**平台功能** 索引標籤是您存取其中 hello hello 應用程式服務的平台，您可以使用函式應用程式中的許多功能。</span><span class="sxs-lookup"><span data-stu-id="014d7-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="014d7-126">Hello 耗用量主控方案執行的函式應用程式時，並非所有應用程式服務功能所提供。</span><span class="sxs-lookup"><span data-stu-id="014d7-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="014d7-127">本主題的 hello 其餘著重於 hello 遵循 hello 中的應用程式服務功能可用於函式的 Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="014d7-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="014d7-128">App Service 編輯器</span><span class="sxs-lookup"><span data-stu-id="014d7-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="014d7-129">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="014d7-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="014d7-130">Console</span><span class="sxs-lookup"><span data-stu-id="014d7-130">Console</span></span>](#console)
+ [<span data-ttu-id="014d7-131">進階工具 (Kudu)</span><span class="sxs-lookup"><span data-stu-id="014d7-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="014d7-132">部署選項</span><span class="sxs-lookup"><span data-stu-id="014d7-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="014d7-133">CORS</span><span class="sxs-lookup"><span data-stu-id="014d7-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="014d7-134">驗證</span><span class="sxs-lookup"><span data-stu-id="014d7-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="014d7-135">API 定義</span><span class="sxs-lookup"><span data-stu-id="014d7-135">API definition</span></span>](#swagger)

<span data-ttu-id="014d7-136">如需有關如何 toowork 應用程式服務設定，請參閱[設定 Azure 應用程式服務設定](../app-service-web/web-sites-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="014d7-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="014d7-137"><a name="editor"></a>App Service 編輯器</span><span class="sxs-lookup"><span data-stu-id="014d7-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![函數應用程式 App Service 編輯器。](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="014d7-139">hello 應用程式服務編輯器是進階的入口網站中編輯器，您可以使用 toomodify JSON 組態檔和類似的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="014d7-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="014d7-140">選擇此選項會啟動一個含有基本編輯器的個別瀏覽器索引標籤。</span><span class="sxs-lookup"><span data-stu-id="014d7-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="014d7-141">這可讓您與 hello Git 儲存機制、 執行和偵錯程式碼，toointegrate，並修改函式應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="014d7-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="014d7-142">此編輯器提供增強的部署環境函式相較於 hello 預設函式應用程式 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="014d7-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![hello 應用程式服務編輯器](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="014d7-144"><a name="settings"></a>應用程式設定</span><span class="sxs-lookup"><span data-stu-id="014d7-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![函數應用程式的應用程式設定。](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="014d7-146">應用程式服務的 hello**應用程式設定**刀鋒視窗是您設定及管理 framework 版本中，遠端偵錯、 應用程式設定和連接字串。</span><span class="sxs-lookup"><span data-stu-id="014d7-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="014d7-147">當您將函數應用程式與其他 Azure 和協力廠商服務整合時，可以在這裡修改那些設定值。</span><span class="sxs-lookup"><span data-stu-id="014d7-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![設定應用程式設定](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="014d7-149"><a name="console"></a>主控台</span><span class="sxs-lookup"><span data-stu-id="014d7-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![在 hello Azure 入口網站中的函式應用程式主控台](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="014d7-151">hello 入口網站中主控台時，理想的開發人員工具與函式應用程式偏好 toointeract 從 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="014d7-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="014d7-152">常用命令包含目錄和檔案建立與瀏覽，以及執行批次檔和指令碼。</span><span class="sxs-lookup"><span data-stu-id="014d7-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![函數應用程式主控台](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="014d7-154"><a name="kudu"></a>進階工具 (Kudu)</span><span class="sxs-lookup"><span data-stu-id="014d7-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Hello Azure 入口網站中的應用程式 Kudu 函式](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="014d7-156">hello 應用程式服務 (也稱為 Kudu) 的進階的工具提供存取 tooadvanced 函式應用程式的系統管理功能。</span><span class="sxs-lookup"><span data-stu-id="014d7-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="014d7-157">從 Kudu，您可以管理系統資訊、應用程式設定、環境變數、網站擴充功能、HTTP 標頭，以及伺服器變數。</span><span class="sxs-lookup"><span data-stu-id="014d7-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="014d7-158">您也可以啟動**Kudu** like 瀏覽應用程式的函式，toohello SCM 端點`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="014d7-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![設定 Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="014d7-160"><a name="deployment">部署選項</span><span class="sxs-lookup"><span data-stu-id="014d7-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Hello Azure 入口網站中的函式應用程式部署選項](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="014d7-162">Functions 可讓您在本機電腦上開發函數程式碼。</span><span class="sxs-lookup"><span data-stu-id="014d7-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="014d7-163">然後，您可以上傳您的區域函式應用程式專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="014d7-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="014d7-164">此外 tootraditional FTP 上傳，函式可讓您部署使用常用的連續整合解決方案，如 GitHub、 VSTS、 Dropbox、 Bitbucket 和其他應用程式函式。</span><span class="sxs-lookup"><span data-stu-id="014d7-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="014d7-165">如需詳細資訊，請參閱 [Azure Functions 的持續部署](functions-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="014d7-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="014d7-166">tooupload 手動使用 FTP 或本機 Git，您也必須[設定您的部署認證](functions-continuous-deployment.md#credentials)。</span><span class="sxs-lookup"><span data-stu-id="014d7-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="014d7-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="014d7-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![函式中應用程式，CORS hello Azure 入口網站](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="014d7-169">tooprevent 執行您的服務中的惡意程式碼，應用程式服務區塊呼叫 tooyour 函式應用程式從外部來源。</span><span class="sxs-lookup"><span data-stu-id="014d7-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="014d7-170">函式支援跨原始資源共用 (CORS) toolet 定義 」 的允許清單 」 允許您的函式將從該處接受遠端要求的來源。</span><span class="sxs-lookup"><span data-stu-id="014d7-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![設定函數應用程式的 CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="014d7-172"><a name="auth"></a>驗證</span><span class="sxs-lookup"><span data-stu-id="014d7-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![在 hello Azure 入口網站中的函式應用程式驗證](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="014d7-174">當函式使用的 HTTP 觸發程序時，您可以要求呼叫 toofirst 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="014d7-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="014d7-175">App Service 支援 Azure Active Directory 驗證，以及使用社交提供者 (例如 Facebook、Microsoft 及 Twitter) 來登入。</span><span class="sxs-lookup"><span data-stu-id="014d7-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="014d7-176">如需設定特定驗證提供者的詳細資訊，請參閱 [Azure App Service 驗證概觀](../app-service/app-service-authentication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="014d7-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![設定函數應用程式的驗證](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="014d7-178"><a name="swagger"></a>API 定義</span><span class="sxs-lookup"><span data-stu-id="014d7-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![函式應用程式 API swagger 定義中 hello Azure 入口網站](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="014d7-180">函式支援 Swagger tooallow 用戶端 toomore 輕鬆使用 HTTP 觸發函式。</span><span class="sxs-lookup"><span data-stu-id="014d7-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="014d7-181">如需有關如何使用 Swagger 建立 API 定義的詳細資訊，請瀏覽[在 Azure 中開始使用 API Apps、ASP.NET 和 Swagger](../app-service-api/app-service-api-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="014d7-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="014d7-182">您也可以使用多個函式的函式 Proxy toodefine 單一的 API 介面。</span><span class="sxs-lookup"><span data-stu-id="014d7-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="014d7-183">如需詳細資訊，請參閱[使用 Azure Functions Proxy](functions-proxies.md)。</span><span class="sxs-lookup"><span data-stu-id="014d7-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![設定函數應用程式的 API](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="014d7-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="014d7-185">Next steps</span></span>

+ [<span data-ttu-id="014d7-186">設定 Azure App Service 設定</span><span class="sxs-lookup"><span data-stu-id="014d7-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="014d7-187">Azure Functions 的持續部署</span><span class="sxs-lookup"><span data-stu-id="014d7-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



