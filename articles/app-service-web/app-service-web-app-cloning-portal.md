---
title: "使用 Azure 入口網站的應用程式複製 aaaWeb"
description: "深入了解如何 tooclone 您 Web 應用程式 toonew 使用 Azure 入口網站的 Web 應用程式。"
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
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="9dcc3-103">使用 Azure 入口網站的 Azure App Service 應用程式複製</span><span class="sxs-lookup"><span data-stu-id="9dcc3-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="9dcc3-104">複製功能中的 hello [Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)可讓您輕鬆地複製現有 web 應用程式 tooa 新建立的應用程式或不同的區域中的 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="9dcc3-105">這可讓客戶 toodeploy 的應用程式的數字跨越不同地區，快速且輕鬆地。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="9dcc3-106">應用程式複製目前僅支援 Premium 層 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="9dcc3-107">新功能使用 hello hello 相同限制 Web 應用程式備份功能，請參閱 <<c0> [ 備份 web 應用程式在 Azure App Service 中](web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="9dcc3-108">複製現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="9dcc3-108">Cloning an existing App</span></span>
<span data-ttu-id="9dcc3-109">hello web 應用程式必須執行在 hello **Premium**順序 toocreate hello web 應用程式的複製模式。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="9dcc3-110">在 [hello [Azure 入口網站](https://portal.azure.com/)，開啟您的 web 應用程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="9dcc3-111">按一下 [工具] 。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-111">Click **Tools**.</span></span> <span data-ttu-id="9dcc3-112">然後，在 hello**工具**刀鋒視窗中，按一下 **複製應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="9dcc3-113">如果 hello web 應用程式已不在 hello **Premium**模式中，您會收到訊息，指出應用程式複製的 hello 支援模式。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="9dcc3-114">此時，您擁有 hello 選項 tooselect**升級**。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="9dcc3-115">在 hello**複製應用程式**刀鋒視窗中提供的 hello 新 web 應用程式、 資源群組和應用程式服務方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="9dcc3-116">也 hello 使用者將能夠 toochoose 是否 tooclone 的來源 web 應用程式設定的數字或不。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="9dcc3-117">按一下後**建立**hello 平台就會開始建立 hello 來源 web 應用程式的複製工作。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="9dcc3-118">複製現有的應用程式 tooan App Service 環境</span><span class="sxs-lookup"><span data-stu-id="9dcc3-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="9dcc3-119">在 hello**複製應用程式**刀鋒視窗 hello 客戶會有 hello 選項 toochoose 現有的 App Service 環境中的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="9dcc3-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="9dcc3-120">目前的限制</span><span class="sxs-lookup"><span data-stu-id="9dcc3-120">Current Restrictions</span></span>
<span data-ttu-id="9dcc3-121">這項功能目前為預覽狀態，我們目前正在處理 tooadd 新功能經過一段時間，hello 清單後面是 hello hello 目前支援的 Azure 入口網站中複製的應用程式的已知的限制：</span><span class="sxs-lookup"><span data-stu-id="9dcc3-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="9dcc3-122">不會複製 Azure 流量管理員設定</span><span class="sxs-lookup"><span data-stu-id="9dcc3-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="9dcc3-123">不會複製自動調整設定</span><span class="sxs-lookup"><span data-stu-id="9dcc3-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="9dcc3-124">不會複製備份排程設定</span><span class="sxs-lookup"><span data-stu-id="9dcc3-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="9dcc3-125">不會複製 VNET 設定</span><span class="sxs-lookup"><span data-stu-id="9dcc3-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="9dcc3-126">App Insights 不會自動上設定 hello 目的地 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9dcc3-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="9dcc3-127">不會複製簡單驗證設定</span><span class="sxs-lookup"><span data-stu-id="9dcc3-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="9dcc3-128">不會複製 Kudu 延伸模組</span><span class="sxs-lookup"><span data-stu-id="9dcc3-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="9dcc3-129">不會複製 TiP 規則</span><span class="sxs-lookup"><span data-stu-id="9dcc3-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="9dcc3-130">不會複製資料庫內容</span><span class="sxs-lookup"><span data-stu-id="9dcc3-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="9dcc3-131">參考</span><span class="sxs-lookup"><span data-stu-id="9dcc3-131">References</span></span>
* [<span data-ttu-id="9dcc3-132">使用 PowerShell 複製 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9dcc3-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="9dcc3-133">在 Azure App Service 中備份 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9dcc3-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="9dcc3-134">如何 tooCreate App Service 環境</span><span class="sxs-lookup"><span data-stu-id="9dcc3-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="9dcc3-135">在 App Service 環境中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9dcc3-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="9dcc3-136">簡介 tooApp Service 環境</span><span class="sxs-lookup"><span data-stu-id="9dcc3-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
