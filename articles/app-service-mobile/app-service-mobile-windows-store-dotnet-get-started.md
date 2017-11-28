---
title: "通用 Windows 平台 (UWP) 上行動應用程式使用 aaaCreate |Microsoft 文件"
description: "請遵循此教學課程 tooget 開始使用 Azure 行動應用程式後端在 C#、 Visual Basic 或 JavaScript 開發通用 Windows 平台 (UWP) 應用程式。"
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="d7846-103">建立 Windows 應用程式</span><span class="sxs-lookup"><span data-stu-id="d7846-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="d7846-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d7846-104">Overview</span></span>
<span data-ttu-id="d7846-105">本教學課程會示範如何 tooadd 雲端架構後端服務 tooa 通用 Windows 平台 (UWP) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7846-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="d7846-106">如需詳細資訊，請參閱 [什麼是 Mobile Apps？](app-service-mobile-value-prop.md)。</span><span class="sxs-lookup"><span data-stu-id="d7846-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="d7846-107">hello 下面是從 hello 完成應用程式的螢幕擷取：</span><span class="sxs-lookup"><span data-stu-id="d7846-107">hello following are screen captures from hello completed app:</span></span>

![完成的電腦桌面應用程式](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="d7846-109">在電腦桌面上執行。</span><span class="sxs-lookup"><span data-stu-id="d7846-109">Running on a desktop.</span></span>

![完成的手機應用程式](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="d7846-111">在手機上執行</span><span class="sxs-lookup"><span data-stu-id="d7846-111">Running on a phone</span></span>

<span data-ttu-id="d7846-112">完成本教學課程是 UWP 應用程式的所有其他行動應用程式教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="d7846-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7846-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="d7846-113">Prerequisites</span></span>
<span data-ttu-id="d7846-114">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="d7846-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d7846-115">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d7846-115">An active Azure account.</span></span> <span data-ttu-id="d7846-116">如果您沒有帳戶，您可以註冊 Azure 的試用版，並取得向上 too10 可用的行動應用程式，即使您在試用結束後，仍可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="d7846-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="d7846-117">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d7846-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d7846-118">[Visual Studio Community 2015] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d7846-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="d7846-119">建立新的 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="d7846-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="d7846-120">請遵循這些步驟 toocreate 新的行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="d7846-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="d7846-121">您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="d7846-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="d7846-122">接下來，您將會下載 「 todo 清單 」 的簡單的伺服器專案後端，將其發行 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d7846-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="d7846-123">設定 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="d7846-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="d7846-124">下載並執行 hello 用戶端專案</span><span class="sxs-lookup"><span data-stu-id="d7846-124">Download and run hello client project</span></span>
<span data-ttu-id="d7846-125">一旦您已設定您的行動裝置應用程式後端，您可以建立新的用戶端應用程式，或修改現有的應用程式 tooconnect tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d7846-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="d7846-126">本節中，您可以下載為自訂的 tooconnect tooyour 行動裝置應用程式後端的 UWP 應用程式範本專案。</span><span class="sxs-lookup"><span data-stu-id="d7846-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="d7846-127">在 hello**快速入門**刀鋒視窗中的行動裝置應用程式後端中，按一下**建立新的應用程式** > **下載**，解壓縮壓縮的 hello 專案檔案tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="d7846-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![下載 Windows 快速入門專案](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="d7846-129">（選擇性）新增 hello UWP 應用程式專案 toohello hello 伺服器專案與相同的方案。</span><span class="sxs-lookup"><span data-stu-id="d7846-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="d7846-130">這讓您更輕鬆 toodebug 兩者 hello 應用程式與 hello 後的端中的測試 hello 相同的 Visual Studio 方案中，如果您選擇 toodo 操作。</span><span class="sxs-lookup"><span data-stu-id="d7846-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="d7846-131">tooadd UWP 應用程式專案 toohello 方案，您必須使用 Visual Studio 2015 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d7846-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="d7846-132">Hello UWP 應用程式為 hello 啟始專案，然後按 hello F5 鍵 toodeploy 和執行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7846-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="d7846-133">在 hello 應用程式中，輸入有意義的文字，例如*完成 hello 教學課程*，在 hello**插入 TodoItem**文字方塊，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d7846-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Windows 快速入門完整桌面](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="d7846-135">這可以傳送 POST 要求 toohello 新行動裝置應用程式的後端裝載在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="d7846-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="d7846-136">（選擇性）停止 hello 應用程式，並在不同的裝置或行動模擬器上重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="d7846-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Windows 快速入門完整手機](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="d7846-138">請注意在 hello UWP 應用程式啟動之後，會從 Azure 載入 hello 先前步驟中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="d7846-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7846-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7846-139">Next steps</span></span>
* [<span data-ttu-id="d7846-140">新增驗證 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="d7846-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="d7846-141">深入了解如何 tooauthenticate 使用者身分識別提供者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7846-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="d7846-142">新增推播通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="d7846-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="d7846-143">了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動裝置應用程式後端 toouse Azure 通知中樞 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="d7846-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="d7846-144">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="d7846-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="d7846-145">了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7846-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="d7846-146">離線同步處理可讓使用者使用行動應用程式的 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="d7846-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
