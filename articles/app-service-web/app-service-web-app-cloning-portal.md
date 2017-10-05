---
title: "使用 Azure 入口網站複製 Web 應用程式"
description: "了解如何使用 Azure 入口網站，將您的 Web Apps 複製到新的 Web Apps。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="4d917-103">使用 Azure 入口網站的 Azure App Service 應用程式複製</span><span class="sxs-lookup"><span data-stu-id="4d917-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="4d917-104">[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) 中的複製功能，可讓您輕鬆地將現有的 Web 應用程式複製到位於不同區域或相同區域的新建立 app。</span><span class="sxs-lookup"><span data-stu-id="4d917-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="4d917-105">這可讓客戶輕鬆且快速地跨不同區域部署許多 app。</span><span class="sxs-lookup"><span data-stu-id="4d917-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="4d917-106">應用程式複製目前僅支援 Premium 層 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d917-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="4d917-107">新的功能使用與 Web Apps 備份功能相同的限制，請參閱 [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="4d917-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="4d917-108">複製現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="4d917-108">Cloning an existing App</span></span>
<span data-ttu-id="4d917-109">Web 應用程式必須在 [進階]  模式中執行，您才能為 Web 應用程式建立複製。</span><span class="sxs-lookup"><span data-stu-id="4d917-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="4d917-110">在 [Azure 入口網站](https://portal.azure.com/)中，開啟 Web 應用程式的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4d917-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="4d917-111">按一下 [工具] 。</span><span class="sxs-lookup"><span data-stu-id="4d917-111">Click **Tools**.</span></span> <span data-ttu-id="4d917-112">然後，在 [工具] 刀鋒視窗中，按一下 [複製應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4d917-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="4d917-113">如果 Web 應用程式尚未處於 [進階] 模式，您將會收到訊息，指出支援應用程式複製的模式。</span><span class="sxs-lookup"><span data-stu-id="4d917-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="4d917-114">此時，您可以選取 [升級] 。</span><span class="sxs-lookup"><span data-stu-id="4d917-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="4d917-115">在 [複製應用程式]  刀鋒視窗中，提供新 Web 應用程式的名稱、資源群組和 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d917-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="4d917-116">使用者也可以選擇是否複製多個來源 Web 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="4d917-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="4d917-117">按一下 [建立]  之後，平台會開始建立來源 Web 應用程式的複製。</span><span class="sxs-lookup"><span data-stu-id="4d917-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="4d917-118">複製現有應用程式至 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="4d917-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="4d917-119">在 [複製應用程式]  刀鋒視窗中，客戶可以在現有 App Service 環境中選擇應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="4d917-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="4d917-120">目前的限制</span><span class="sxs-lookup"><span data-stu-id="4d917-120">Current Restrictions</span></span>
<span data-ttu-id="4d917-121">這項功能目前僅供預覽，我們正努力在日後加入新功能，以下是 Azure 入口網站中目前應用程式複製支援的已知限制：</span><span class="sxs-lookup"><span data-stu-id="4d917-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="4d917-122">不會複製 Azure 流量管理員設定</span><span class="sxs-lookup"><span data-stu-id="4d917-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="4d917-123">不會複製自動調整設定</span><span class="sxs-lookup"><span data-stu-id="4d917-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="4d917-124">不會複製備份排程設定</span><span class="sxs-lookup"><span data-stu-id="4d917-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="4d917-125">不會複製 VNET 設定</span><span class="sxs-lookup"><span data-stu-id="4d917-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="4d917-126">未自動在目的地 Web 應用程式上設定 App Insights </span><span class="sxs-lookup"><span data-stu-id="4d917-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="4d917-127">不會複製簡單驗證設定</span><span class="sxs-lookup"><span data-stu-id="4d917-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="4d917-128">不會複製 Kudu 延伸模組</span><span class="sxs-lookup"><span data-stu-id="4d917-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="4d917-129">不會複製 TiP 規則</span><span class="sxs-lookup"><span data-stu-id="4d917-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="4d917-130">不會複製資料庫內容</span><span class="sxs-lookup"><span data-stu-id="4d917-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="4d917-131">參考</span><span class="sxs-lookup"><span data-stu-id="4d917-131">References</span></span>
* [<span data-ttu-id="4d917-132">使用 PowerShell 複製 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d917-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="4d917-133">在 Azure App Service 中備份 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d917-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="4d917-134">如何建立 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="4d917-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="4d917-135">在 App Service 環境中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d917-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="4d917-136">App Service 環境簡介</span><span class="sxs-lookup"><span data-stu-id="4d917-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
