---
title: "aaaQuickly 部署現有的應用程式 tooan Azure Service Fabric 叢集"
description: "使用 Azure Service Fabric 叢集 toohost 現有 Node.js 應用程式與 Visual Studio。"
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="21e1b-103">在 Azure Service Fabric 上裝載 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="21e1b-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="21e1b-104">本快速入門可協助您部署在 Azure 上執行的現有應用程式 (在此範例中的 Node.js) tooa Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="21e1b-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21e1b-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="21e1b-105">Prerequisites</span></span>

<span data-ttu-id="21e1b-106">開始之前，請確定您已 [設定開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="21e1b-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="21e1b-107">這包括安裝 hello Service Fabric SDK 及 Visual Studio 2017 或 2015年。</span><span class="sxs-lookup"><span data-stu-id="21e1b-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="21e1b-108">您也需要 toohave 現有 Node.js 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="21e1b-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="21e1b-109">本快速入門使用可在[這裡][download-sample]下載的簡單 Node.js 網站。</span><span class="sxs-lookup"><span data-stu-id="21e1b-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="21e1b-110">擷取這個檔案 tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` hello 下一個步驟中建立 hello 專案之後的資料夾。</span><span class="sxs-lookup"><span data-stu-id="21e1b-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="21e1b-111">如果您沒有 Azure 訂用帳戶，請建立[免費帳戶][create-account]。</span><span class="sxs-lookup"><span data-stu-id="21e1b-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="21e1b-112">建立 hello 服務</span><span class="sxs-lookup"><span data-stu-id="21e1b-112">Create hello service</span></span>

<span data-ttu-id="21e1b-113">以**系統管理員**身分啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="21e1b-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="21e1b-114">使用 `CTRL`+`SHIFT`+`N` 建立專案</span><span class="sxs-lookup"><span data-stu-id="21e1b-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="21e1b-115">在 [hello**新專案**] 對話方塊中，選擇**雲端 > Service Fabric 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="21e1b-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="21e1b-116">Hello 應用程式命名**MyGuestApp**按**確定**。</span><span class="sxs-lookup"><span data-stu-id="21e1b-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="21e1b-117">Node.js 可以輕易地中斷 hello 260 字元限制為 windows 提供的路徑。</span><span class="sxs-lookup"><span data-stu-id="21e1b-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="21e1b-118">Hello 專案本身使用短路徑，例如**c:\code\svc1**。</span><span class="sxs-lookup"><span data-stu-id="21e1b-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Visual Studio 中的新增專案對話方塊][new-project]

<span data-ttu-id="21e1b-120">您可以從 hello 下一步 對話方塊建立 Service Fabric 服務的任何型別。</span><span class="sxs-lookup"><span data-stu-id="21e1b-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="21e1b-121">在本快速入門中，選擇 [來賓可執行檔]。</span><span class="sxs-lookup"><span data-stu-id="21e1b-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="21e1b-122">Hello 服務名稱**MyGuestService**和 set hello 選項上 hello 右 toohello 下列值：</span><span class="sxs-lookup"><span data-stu-id="21e1b-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="21e1b-123">設定</span><span class="sxs-lookup"><span data-stu-id="21e1b-123">Setting</span></span>                   | <span data-ttu-id="21e1b-124">值</span><span class="sxs-lookup"><span data-stu-id="21e1b-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="21e1b-125">程式碼封裝資料夾</span><span class="sxs-lookup"><span data-stu-id="21e1b-125">Code Package Folder</span></span>       | <span data-ttu-id="21e1b-126">_&lt;Node.js 應用程式的 hello 資料夾&gt;_</span><span class="sxs-lookup"><span data-stu-id="21e1b-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="21e1b-127">程式碼封裝行為</span><span class="sxs-lookup"><span data-stu-id="21e1b-127">Code Package Behavior</span></span>     | <span data-ttu-id="21e1b-128">複製資料夾內容 tooproject</span><span class="sxs-lookup"><span data-stu-id="21e1b-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="21e1b-129">程式</span><span class="sxs-lookup"><span data-stu-id="21e1b-129">Program</span></span>                   | <span data-ttu-id="21e1b-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="21e1b-130">node.exe</span></span> |
| <span data-ttu-id="21e1b-131">引數</span><span class="sxs-lookup"><span data-stu-id="21e1b-131">Arguments</span></span>                 | <span data-ttu-id="21e1b-132">server.js</span><span class="sxs-lookup"><span data-stu-id="21e1b-132">server.js</span></span> |
| <span data-ttu-id="21e1b-133">工作資料夾</span><span class="sxs-lookup"><span data-stu-id="21e1b-133">Working Folder</span></span>            | <span data-ttu-id="21e1b-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="21e1b-134">CodePackage</span></span> |

<span data-ttu-id="21e1b-135">按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="21e1b-135">Press **OK**.</span></span>

![Visual Studio 中的新增服務對話方塊][new-service]

<span data-ttu-id="21e1b-137">Visual Studio 會建立 hello 應用程式專案和 hello 行動服務專案，並顯示在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="21e1b-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="21e1b-138">hello 應用程式專案 (**MyGuestApp**) 直接不包含任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="21e1b-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="21e1b-139">它反而會參考一組服務專案。</span><span class="sxs-lookup"><span data-stu-id="21e1b-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="21e1b-140">此外，它包含三種其他類型的內容：</span><span class="sxs-lookup"><span data-stu-id="21e1b-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="21e1b-141">**發佈設定檔**</span><span class="sxs-lookup"><span data-stu-id="21e1b-141">**Publish profiles**</span></span>  
<span data-ttu-id="21e1b-142">用來管理不同環境的工具喜好設定。</span><span class="sxs-lookup"><span data-stu-id="21e1b-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="21e1b-143">**指令碼**</span><span class="sxs-lookup"><span data-stu-id="21e1b-143">**Scripts**</span></span>  
<span data-ttu-id="21e1b-144">包含用來部署/升級應用程式的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="21e1b-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="21e1b-145">**應用程式定義**</span><span class="sxs-lookup"><span data-stu-id="21e1b-145">**Application definition**</span></span>  
<span data-ttu-id="21e1b-146">包含在 hello 應用程式資訊清單*ApplicationPackageRoot*。</span><span class="sxs-lookup"><span data-stu-id="21e1b-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="21e1b-147">相關聯的應用程式參數檔案受到*ApplicationParameters*，其中定義 hello 應用程式並可讓您 tooconfigure 它專為特定環境。</span><span class="sxs-lookup"><span data-stu-id="21e1b-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="21e1b-148">如需 hello hello 服務專案內容的概觀，請參閱[可靠的服務入門](service-fabric-reliable-services-quick-start.md)。</span><span class="sxs-lookup"><span data-stu-id="21e1b-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="21e1b-149">設定網路</span><span class="sxs-lookup"><span data-stu-id="21e1b-149">Set up networking</span></span>

<span data-ttu-id="21e1b-150">我們要部署 Node.js 應用程式會使用連接埠的 hello 範例**80** ，我們需要 tootell Service Fabric 需要公開連接埠。</span><span class="sxs-lookup"><span data-stu-id="21e1b-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="21e1b-151">開啟 hello **ServiceManifest.xml** hello 專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="21e1b-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="21e1b-152">Hello hello 資訊清單底部，在沒有`<Resources> \ <Endpoints>`利用已定義的項目。</span><span class="sxs-lookup"><span data-stu-id="21e1b-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="21e1b-153">修改的項目 tooadd `Port`， `Protocol`，和`Type`。</span><span class="sxs-lookup"><span data-stu-id="21e1b-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="21e1b-154">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="21e1b-154">Deploy tooAzure</span></span>

<span data-ttu-id="21e1b-155">如果您按下**F5**和執行 hello 專案，它是已部署的 toohello 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="21e1b-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="21e1b-156">不過，讓我們 tooAzure 改為部署。</span><span class="sxs-lookup"><span data-stu-id="21e1b-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="21e1b-157">Hello 專案上按一下滑鼠右鍵，然後選擇 **發行...**以開啟對話方塊 toopublish tooAzure。</span><span class="sxs-lookup"><span data-stu-id="21e1b-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![發行 service fabric 服務的 tooazure 對話方塊][publish]

<span data-ttu-id="21e1b-159">選取 hello **PublishProfiles\Cloud.xml** profile 當做目標。</span><span class="sxs-lookup"><span data-stu-id="21e1b-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="21e1b-160">如果您還沒有做之前，選擇要 Azure 帳戶 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="21e1b-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="21e1b-161">如果您沒有 Azure 帳戶，請[註冊一個][create-account]。</span><span class="sxs-lookup"><span data-stu-id="21e1b-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="21e1b-162">在下**連接端點**，選取 hello 到 Service Fabric 叢集 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="21e1b-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="21e1b-163">如果您沒有其中一個，選取**&lt;建立新的叢集...&gt;** 這會開啟網頁瀏覽器視窗 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="21e1b-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="21e1b-164">如需詳細資訊，請參閱[hello 入口網站中建立叢集](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="21e1b-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="21e1b-165">當您建立 hello Service Fabric 叢集時，請確定 tooset hello**自訂端點**太設定**80**。</span><span class="sxs-lookup"><span data-stu-id="21e1b-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![自訂端點的 Service fabric 節點類型組態][custom-endpoint]

<span data-ttu-id="21e1b-167">建立新的 Service Fabric 叢集需要花一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="21e1b-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="21e1b-168">已建立，移至上一頁 toohello 發行對話方塊，並選取**&lt;重新整理&gt;**。</span><span class="sxs-lookup"><span data-stu-id="21e1b-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="21e1b-169">hello 新叢集會列在 [hello] 下拉式清單方塊中。請選取它。</span><span class="sxs-lookup"><span data-stu-id="21e1b-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="21e1b-170">按**發行**並等候 hello 部署 toofinish。</span><span class="sxs-lookup"><span data-stu-id="21e1b-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="21e1b-171">這可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="21e1b-171">This may take a few minutes.</span></span> <span data-ttu-id="21e1b-172">完成之後，可能需要數分鐘的 hello 應用程式 toobe 完全可供使用。</span><span class="sxs-lookup"><span data-stu-id="21e1b-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="21e1b-173">測試 hello 網站</span><span class="sxs-lookup"><span data-stu-id="21e1b-173">Test hello website</span></span>

<span data-ttu-id="21e1b-174">在服務發佈之後，請在網頁瀏覽器中進行測試。</span><span class="sxs-lookup"><span data-stu-id="21e1b-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="21e1b-175">首先，開啟 hello Azure 入口網站，並尋找您的 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="21e1b-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="21e1b-176">請檢查 hello 概觀刀鋒視窗中的 hello 服務位址。</span><span class="sxs-lookup"><span data-stu-id="21e1b-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="21e1b-177">使用 hello 的網域名稱，從 hello_用戶端連接端點_屬性。</span><span class="sxs-lookup"><span data-stu-id="21e1b-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="21e1b-178">例如： `http://mysvcfab1.westus2.cloudapp.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="21e1b-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![服務網狀架構概觀刀鋒視窗上 hello Azure 入口網站][overview]

<span data-ttu-id="21e1b-180">瀏覽 toothis 位址就可看到 hello`HELLO WORLD`回應。</span><span class="sxs-lookup"><span data-stu-id="21e1b-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="21e1b-181">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="21e1b-181">Delete hello cluster</span></span>

<span data-ttu-id="21e1b-182">不要忘記的 toodelete 所有您為本快速入門，為您所建立的 hello 資源會針對這些資源的收費。</span><span class="sxs-lookup"><span data-stu-id="21e1b-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e1b-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21e1b-183">Next steps</span></span>
<span data-ttu-id="21e1b-184">深入了解[客體可執行檔](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="21e1b-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F