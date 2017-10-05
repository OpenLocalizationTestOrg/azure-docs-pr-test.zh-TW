---
title: "在 Visual Studio 中管理應用程式 | Microsoft Docs"
description: "使用 Visual Studio 來建立、開發、封裝、部署和偵錯 Service Fabric 應用程式和服務。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: 3f6a47a15b74a7ceb6504b2834be62e76ab70bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="2ceb7-103">使用 Visual Studio 簡化撰寫及管理 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="2ceb7-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="2ceb7-104">您可以透過 Visual Studio 管理 Azure Service Fabric 應用程式與服務。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="2ceb7-105">[設定開發環境](service-fabric-get-started.md)後，您可以使用 Visual Studio 在本機開發叢集中建立 Service Fabric 應用程式、新增服務，或是封裝、註冊及部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="2ceb7-106">部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="2ceb7-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="2ceb7-107">根據預設，部署應用程式會將以下幾個步驟結合成一個簡單的作業：</span><span class="sxs-lookup"><span data-stu-id="2ceb7-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="2ceb7-108">建立應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="2ceb7-108">Creating the application package</span></span>
2. <span data-ttu-id="2ceb7-109">將應用程式封裝上傳至映像存放區</span><span class="sxs-lookup"><span data-stu-id="2ceb7-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="2ceb7-110">註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="2ceb7-110">Registering the application type</span></span>
4. <span data-ttu-id="2ceb7-111">移除任何執行中的應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="2ceb7-111">Removing any running application instances</span></span>
5. <span data-ttu-id="2ceb7-112">建立應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="2ceb7-112">Creating an application instance</span></span>

<span data-ttu-id="2ceb7-113">在 Visual Studio 中按 **F5** 會部署應用程式，並將偵錯工具附加到所有應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="2ceb7-114">您可以使用 **Ctrl + F5** 來部署應用程式而不進行偵錯，或是使用發佈設定檔來發佈至本機或遠端叢集。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="2ceb7-115">如需詳細資訊，請參閱 [使用 Visual Studio 將應用程式發佈至遠端叢集](service-fabric-publish-app-remote-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="2ceb7-116">應用程式偵錯模式</span><span class="sxs-lookup"><span data-stu-id="2ceb7-116">Application Debug Mode</span></span>
<span data-ttu-id="2ceb7-117">Visual Studio 提供的 **Application Debug Mode** 屬性可讓您控制 Visual Studio 要如何處理應用程式部署作為偵錯的一部分。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="2ceb7-118">設定應用程式偵錯模式屬性</span><span class="sxs-lookup"><span data-stu-id="2ceb7-118">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="2ceb7-119">在 Service Fabric 應用程式專案 (*.sfproj) 的捷徑功能表上，選擇 [屬性]\(或按 **F4** 按鍵)。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-119">On the Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="2ceb7-120">在 [屬性] 視窗中，設定 [應用程式偵錯模式] 屬性。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-120">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![設定應用程式偵錯模式屬性][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="2ceb7-122">應用程式偵錯模式</span><span class="sxs-lookup"><span data-stu-id="2ceb7-122">Application Debug Modes</span></span>

1. <span data-ttu-id="2ceb7-123">**重新整理應用程式** 這個模式可讓您快速變更和偵錯您的程式碼，並支援在偵錯時編輯靜態網頁檔案。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-123">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="2ceb7-124">這種模式僅適用於您的本機開發叢集為 [1 個節點模式](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode)的情況。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="2ceb7-125">**移除應用程式** 會在偵錯工作階段結束時移除應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="2ceb7-126">**自動升級** 偵錯工作階段結束時，應用程式繼續執行。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="2ceb7-127">下一個偵錯工作階段會將部署視為升級。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="2ceb7-128">此升級程序會保留您在前一個偵錯工作階段中輸入的所有資料。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="2ceb7-129">**保留應用程式** 偵錯工作階段結束時，應用程式會在叢集中繼續執行。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="2ceb7-130">在下一個偵錯工作階段開始時，會移除應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="2ceb7-131">如果使用 [自動升級]，資料會藉由套用 Service Fabric 的應用程式升級功能得以保留。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="2ceb7-132">如需有關升級應用程式和如何在實際環境中執行升級的詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="2ceb7-133">將服務加入 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="2ceb7-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="2ceb7-134">您可以將新的服務新增至應用程式以擴充其功能。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-134">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="2ceb7-135">若要確保應用程式封裝中包含該服務，請透過 [新增 Fabric 服務]  功能表項目新增服務。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![新增 Service Fabric 服務][newservice]

<span data-ttu-id="2ceb7-137">選取要新增至應用程式的 Service Fabric 專案類型，並指定服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="2ceb7-138">請參閱 [選擇服務架構](service-fabric-choose-framework.md) ，以協助您決定要使用的服務類型。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![選取要新增至應用程式的 Service Fabric 服務類型][addserviceproject]

<span data-ttu-id="2ceb7-140">新服務會新增到解決方案與現有的應用程式套件中。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="2ceb7-141">服務參照與預設的服務執行個體將會新增到應用程式資訊清單，然後在您下次部署應用程式時建立並啟動服務。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![新服務會新增到應用程式資訊清單][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="2ceb7-143">封裝 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="2ceb7-143">Package your Service Fabric application</span></span>
<span data-ttu-id="2ceb7-144">若要將應用程式及其服務部署到叢集，您需要建立應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="2ceb7-145">套件會以特定的配置來組織應用程式資訊清單、服務資訊清單和其他必要的檔案。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="2ceb7-146">Visual Studio 會在 'pkg' 目錄的應用程式專案資料夾中設定與管理封裝。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="2ceb7-147">從 [應用程式] 操作功能表中按一下 [封裝] 會建立或更新應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="2ceb7-148">使用 Cloud Explorer 移除應用程式和應用程式類型</span><span class="sxs-lookup"><span data-stu-id="2ceb7-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="2ceb7-149">您可以從 Visual Studio 使用 Cloud Explorer (可從 [檢視]  功能表啟動) 執行基本的叢集管理作業。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="2ceb7-150">例如，您可以在本機或遠端叢集上刪除應用程式和解除佈建應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![移除應用程式][removeapplication]

> [!TIP]
> <span data-ttu-id="2ceb7-152">如需更豐富的叢集管理功能，請參閱 [使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="2ceb7-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="2ceb7-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ceb7-153">Next steps</span></span>
* [<span data-ttu-id="2ceb7-154">Service Fabric 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="2ceb7-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="2ceb7-155">Service Fabric 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="2ceb7-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="2ceb7-156">管理多個環境的應用程式參數</span><span class="sxs-lookup"><span data-stu-id="2ceb7-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="2ceb7-157">偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="2ceb7-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="2ceb7-158">使用 Service Fabric 總管視覺化叢集</span><span class="sxs-lookup"><span data-stu-id="2ceb7-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png