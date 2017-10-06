---
title: "aaaManage Visual Studio 中的應用程式 |Microsoft 文件"
description: "使用 Visual Studio toocreate、 開發，封裝、 部署和偵錯您的 Service Fabric 應用程式和服務。"
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
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="bc222-103">使用 Visual Studio toosimplify 撰寫和管理您的 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc222-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="bc222-104">您可以透過 Visual Studio 管理 Azure Service Fabric 應用程式與服務。</span><span class="sxs-lookup"><span data-stu-id="bc222-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="bc222-105">一旦您[設定開發環境](service-fabric-get-started.md)，您可以使用 Visual Studio toocreate Service Fabric 應用程式、 加入服務或封裝時，暫存器，並在本機開發叢集部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc222-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="bc222-106">部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc222-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="bc222-107">根據預設，部署應用程式結合了下列插入一個簡單的作業步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc222-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="bc222-108">建立 hello 應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="bc222-108">Creating hello application package</span></span>
2. <span data-ttu-id="bc222-109">上傳 hello 應用程式封裝 toohello 映像存放區</span><span class="sxs-lookup"><span data-stu-id="bc222-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="bc222-110">註冊 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="bc222-110">Registering hello application type</span></span>
4. <span data-ttu-id="bc222-111">移除任何執行中的應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="bc222-111">Removing any running application instances</span></span>
5. <span data-ttu-id="bc222-112">建立應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="bc222-112">Creating an application instance</span></span>

<span data-ttu-id="bc222-113">在 Visual Studio 中，按下**F5**部署您的應用程式，並附加 hello 偵錯工具 tooall 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="bc222-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="bc222-114">您可以使用**Ctrl + F5** toodeploy 而不偵錯，或您的應用程式可以發佈 tooa 本機或遠端叢集使用 hello 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="bc222-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="bc222-115">如需詳細資訊，請參閱[使用 Visual Studio 發行應用程式 tooa 遠端叢集](service-fabric-publish-app-remote-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="bc222-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="bc222-116">應用程式偵錯模式</span><span class="sxs-lookup"><span data-stu-id="bc222-116">Application Debug Mode</span></span>
<span data-ttu-id="bc222-117">Visual Studio 提供屬性，稱為**應用程式偵錯模式**，這會控制所需的 Visual Studio toohandle 應用程式部署為偵錯的一部分。</span><span class="sxs-lookup"><span data-stu-id="bc222-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="bc222-118">tooset hello 應用程式偵錯模式屬性</span><span class="sxs-lookup"><span data-stu-id="bc222-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="bc222-119">Hello Service Fabric 應用程式的專案 (*.sfproj) 上快顯功能表上，選擇**屬性**(或按 hello **F4**索引鍵)。</span><span class="sxs-lookup"><span data-stu-id="bc222-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="bc222-120">在 hello**屬性**視窗中，設定 hello**應用程式偵錯模式**屬性。</span><span class="sxs-lookup"><span data-stu-id="bc222-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![設定應用程式偵錯模式屬性][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="bc222-122">應用程式偵錯模式</span><span class="sxs-lookup"><span data-stu-id="bc222-122">Application Debug Modes</span></span>

1. <span data-ttu-id="bc222-123">**重新整理應用程式**這個模式可讓您 tooquickly 變更，並且偵錯程式碼和偵錯時編輯靜態網頁檔案的支援。</span><span class="sxs-lookup"><span data-stu-id="bc222-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="bc222-124">這種模式僅適用於您的本機開發叢集為 [1 個節點模式](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode)的情況。</span><span class="sxs-lookup"><span data-stu-id="bc222-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="bc222-125">**移除應用程式**原因 hello 應用程式 toobe hello 偵錯工作階段結束時移除。</span><span class="sxs-lookup"><span data-stu-id="bc222-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="bc222-126">**自動升級**hello 應用程式會繼續 toorun hello 偵錯工作階段結束時。</span><span class="sxs-lookup"><span data-stu-id="bc222-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="bc222-127">hello 下一個偵錯工作階段會視為 hello 部署升級。</span><span class="sxs-lookup"><span data-stu-id="bc222-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="bc222-128">hello 升級程序會保留您在先前的偵錯工作階段中輸入任何資料。</span><span class="sxs-lookup"><span data-stu-id="bc222-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="bc222-129">**保留應用程式**hello 時 hello hello 叢集中執行的應用程式會保留偵錯工作階段隨即結束。</span><span class="sxs-lookup"><span data-stu-id="bc222-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="bc222-130">在 hello 開頭 hello 下一個偵錯工作階段，將會移除 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc222-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="bc222-131">如**自動升級**資料會保留以供套用 hello 的 Service Fabric 應用程式升級功能。</span><span class="sxs-lookup"><span data-stu-id="bc222-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="bc222-132">如需有關升級應用程式和如何在實際環境中執行升級的詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="bc222-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="bc222-133">新增服務 tooyour Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc222-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="bc222-134">您可以加入新的服務 tooyour 應用程式 tooextend 其功能。</span><span class="sxs-lookup"><span data-stu-id="bc222-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="bc222-135">tooensure hello 服務隨附於您的應用程式封裝，加入 hello 服務透過 hello**新增 Fabric 服務...**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="bc222-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![新增 Service Fabric 服務][newservice]

<span data-ttu-id="bc222-137">選取 Service Fabric 專案類型 tooadd tooyour 應用程式，並指定 hello 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc222-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="bc222-138">請參閱[選擇您的服務的架構](service-fabric-choose-framework.md)toohelp 您決定哪一種服務類型 toouse。</span><span class="sxs-lookup"><span data-stu-id="bc222-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![選取 Service Fabric 服務專案類型 tooadd tooyour 應用程式][addserviceproject]

<span data-ttu-id="bc222-140">hello 新服務會加入 tooyour 解決方案與現有應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="bc222-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="bc222-141">hello 服務參考和預設的服務執行個體將會加入的 toohello 應用程式資訊清單，導致 hello 服務 toobe 建立並啟動 hello 部署 hello 應用程式的下一次。</span><span class="sxs-lookup"><span data-stu-id="bc222-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![加入 tooyour 應用程式資訊清單的 hello 新的服務][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="bc222-143">封裝 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc222-143">Package your Service Fabric application</span></span>
<span data-ttu-id="bc222-144">toodeploy hello 應用程式和其服務 tooa 叢集，您會需要 toocreate 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="bc222-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="bc222-145">hello 封裝組織 hello 應用程式資訊清單、 服務資訊清單，然後以特定配置其他必要的檔案。</span><span class="sxs-lookup"><span data-stu-id="bc222-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="bc222-146">Visual Studio 設定及管理 hello 套件 hello 'byok-kek-pkg' 目錄中的 hello 應用程式專案的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="bc222-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="bc222-147">按一下**封裝**從 hello**應用程式**內容功能表建立或更新 hello 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="bc222-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="bc222-148">使用 Cloud Explorer 移除應用程式和應用程式類型</span><span class="sxs-lookup"><span data-stu-id="bc222-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="bc222-149">您可以執行基本的叢集管理作業從 Visual Studio 中使用 Cloud Explorer，您可以從 hello 啟動**檢視**功能表。</span><span class="sxs-lookup"><span data-stu-id="bc222-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="bc222-150">例如，您可以在本機或遠端叢集上刪除應用程式和解除佈建應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="bc222-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![移除應用程式][removeapplication]

> [!TIP]
> <span data-ttu-id="bc222-152">如需更豐富的叢集管理功能，請參閱 [使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="bc222-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="bc222-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc222-153">Next steps</span></span>
* [<span data-ttu-id="bc222-154">Service Fabric 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="bc222-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="bc222-155">Service Fabric 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="bc222-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="bc222-156">管理多個環境的應用程式參數</span><span class="sxs-lookup"><span data-stu-id="bc222-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="bc222-157">偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc222-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="bc222-158">使用 Service Fabric 總管視覺化叢集</span><span class="sxs-lookup"><span data-stu-id="bc222-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png