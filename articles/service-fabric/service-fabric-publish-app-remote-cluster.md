---
title: "Visual Studio 的應用程式 tooa 遠端叢集 aaaPublish |Microsoft 文件"
description: "了解如何使用 Visual Studio toopublish 應用程式 tooa 遠端服務網狀架構叢集。"
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a><span data-ttu-id="a3117-103">使用 Visual Studio 來部署和移除應用程式</span><span class="sxs-lookup"><span data-stu-id="a3117-103">Deploy and remove applications using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3117-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3117-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="a3117-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3117-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="a3117-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="a3117-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="a3117-107">hello Azure Service Fabric Visual Studio 擴充功能提供簡單、 可重複、 可編寫指令碼的方式 toopublish 應用程式 tooa Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="a3117-107">hello Azure Service Fabric extension for Visual Studio provides an easy, repeatable, and scriptable way toopublish an application tooa Service Fabric cluster.</span></span>

## <a name="hello-artifacts-required-for-publishing"></a><span data-ttu-id="a3117-108">為發行所需的 hello 成品</span><span class="sxs-lookup"><span data-stu-id="a3117-108">hello artifacts required for publishing</span></span>
### <a name="deploy-fabricapplicationps1"></a><span data-ttu-id="a3117-109">Deploy-FabricApplication.ps1</span><span class="sxs-lookup"><span data-stu-id="a3117-109">Deploy-FabricApplication.ps1</span></span>
<span data-ttu-id="a3117-110">這是 PowerShell 指令碼，使用發佈設定檔路徑做為參數，以發佈 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3117-110">This is a PowerShell script that uses a publish profile path as a parameter for publishing Service Fabric applications.</span></span> <span data-ttu-id="a3117-111">此指令碼是您的應用程式的一部分，因為您是  褖畫惎 toomodify 它視您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3117-111">Since this script is part of your application, you are welcome toomodify it as necessary for your application.</span></span>

### <a name="publish-profiles"></a><span data-ttu-id="a3117-112">發佈設定檔</span><span class="sxs-lookup"><span data-stu-id="a3117-112">Publish profiles</span></span>
<span data-ttu-id="a3117-113">Hello Service Fabric 應用程式專案的資料夾內呼叫**PublishProfiles**包含 XML 檔案來儲存重要資訊發佈應用程式，例如：</span><span class="sxs-lookup"><span data-stu-id="a3117-113">A folder in hello Service Fabric application project called **PublishProfiles** contains XML files that store essential information for publishing an application, such as:</span></span>

* <span data-ttu-id="a3117-114">Service Fabric 叢集連線參數</span><span class="sxs-lookup"><span data-stu-id="a3117-114">Service Fabric cluster connection parameters</span></span>
* <span data-ttu-id="a3117-115">路徑 tooan 應用程式參數檔案</span><span class="sxs-lookup"><span data-stu-id="a3117-115">Path tooan application parameter file</span></span>
* <span data-ttu-id="a3117-116">升級設定</span><span class="sxs-lookup"><span data-stu-id="a3117-116">Upgrade settings</span></span>

<span data-ttu-id="a3117-117">根據預設，您的應用程式會包含三個發佈設定檔：Local.1Node.xml、Local.5Node.xml 和 Cloud.xml。</span><span class="sxs-lookup"><span data-stu-id="a3117-117">By default, your application will include three publish profiles: Local.1Node.xml, Local.5Node.xml, and Cloud.xml.</span></span> <span data-ttu-id="a3117-118">您可以加入多個設定檔複製並貼上的其中一個 hello 預設檔案。</span><span class="sxs-lookup"><span data-stu-id="a3117-118">You can add more profiles by copying and pasting one of hello default files.</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="a3117-119">應用程式參數檔案</span><span class="sxs-lookup"><span data-stu-id="a3117-119">Application parameter files</span></span>
<span data-ttu-id="a3117-120">Hello Service Fabric 應用程式專案的資料夾內呼叫**ApplicationParameters**包含使用者指定的應用程式資訊清單的參數值的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="a3117-120">A folder in hello Service Fabric application project called **ApplicationParameters** contains XML files for user-specified application manifest parameter values.</span></span> <span data-ttu-id="a3117-121">應用程式資訊清單檔案可以參數化，讓您可以針對部署設定使用不同的值。</span><span class="sxs-lookup"><span data-stu-id="a3117-121">Application manifest files can be parameterized so that you can use different values for deployment settings.</span></span> <span data-ttu-id="a3117-122">toolearn 更多關於參數化您的應用程式，請參閱[管理多個環境中 Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="a3117-122">toolearn more about parameterizing your application, see [Manage multiple environments in Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a3117-123">針對行動服務，您應該建立 hello 專案第一次嘗試 tooedit hello 檔案在編輯器中或透過 hello 發行 web 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a3117-123">For actor services, you should build hello project first before attempting tooedit hello file in an editor or through hello publish dialog box.</span></span> <span data-ttu-id="a3117-124">這是因為 hello 建置期間，將產生的 hello 資訊清單檔案的一部分。</span><span class="sxs-lookup"><span data-stu-id="a3117-124">This is because part of hello manifest files will be generated during hello build.</span></span>

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a><span data-ttu-id="a3117-125">toopublish 應用程式使用 hello 發行 Service Fabric 應用程式 對話方塊</span><span class="sxs-lookup"><span data-stu-id="a3117-125">toopublish an application using hello Publish Service Fabric Application dialog box</span></span>
<span data-ttu-id="a3117-126">hello 下列步驟示範如何使用應用程式的 toopublish hello**發行 Service Fabric 應用程式**hello Visual Studio Service Fabric 工具所提供的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a3117-126">hello following steps demonstrate how toopublish an application using hello **Publish Service Fabric Application** dialog box provided by hello Visual Studio Service Fabric Tools.</span></span>

1. <span data-ttu-id="a3117-127">Hello hello Service Fabric 應用程式專案的捷徑功能表，選擇 **發行...**</span><span class="sxs-lookup"><span data-stu-id="a3117-127">On hello shortcut menu of hello Service Fabric Application project, choose **Publish…**</span></span> <span data-ttu-id="a3117-128">tooview hello**發行 Service Fabric 應用程式** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a3117-128">tooview hello **Publish Service Fabric Application** dialog box.</span></span>
   
    ![hello * * 發行 Service Fabric 應用程式 * * 對話方塊][0]
   
    <span data-ttu-id="a3117-130">hello 中選取的 hello 檔案**profile 當做目標**下拉式清單方塊是 where 所有 hello 設定，除了**資訊清單版本**，會儲存。</span><span class="sxs-lookup"><span data-stu-id="a3117-130">hello file selected in hello **Target profile** dropdown list box is where all of hello settings, except **Manifest versions**, are saved.</span></span> <span data-ttu-id="a3117-131">您可以重複使用現有的設定檔，或建立一個新選擇**< 管理設定檔...>**在 hello **profile 當做目標**下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="a3117-131">You can either reuse an existing profile or create a new one by choosing **<Manage Profiles…>** in hello **Target profile** dropdown list box.</span></span> <span data-ttu-id="a3117-132">當您選擇的發行設定檔時，其內容會顯示 hello hello 對話方塊中的對應欄位中。</span><span class="sxs-lookup"><span data-stu-id="a3117-132">When you choose a publish profile, its contents appear in hello corresponding fields of hello dialog box.</span></span> <span data-ttu-id="a3117-133">toosave 您的變更，也可以隨時選擇 hello**儲存設定檔**連結。</span><span class="sxs-lookup"><span data-stu-id="a3117-133">toosave your changes at any time, choose hello **Save Profile** link.</span></span>    
2. <span data-ttu-id="a3117-134">在 hello**連接端點**區段中，指定本機或遠端 Service Fabric 叢集的發行端點。</span><span class="sxs-lookup"><span data-stu-id="a3117-134">In hello **Connection endpoint** section, specify a local or remote Service Fabric cluster’s publishing endpoint.</span></span> <span data-ttu-id="a3117-135">tooadd 或變更 hello 連接端點上，按一下 hello**連接端點**下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="a3117-135">tooadd or change hello connection endpoint, click on hello **Connection Endpoint** dropdown list.</span></span> <span data-ttu-id="a3117-136">hello 清單會顯示 hello 可用 Service Fabric 叢集連線端點 toowhich 可以發佈根據您的 Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="a3117-136">hello list shows hello available Service Fabric cluster connection endpoints toowhich you can publish based on your Azure subscription(s).</span></span> <span data-ttu-id="a3117-137">請注意，是否您沒有已登入 tooVisual Studio，您將會提示的 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="a3117-137">Note that if you are not already logged in tooVisual Studio, you will be prompted toodo so.</span></span>
   
    <span data-ttu-id="a3117-138">使用 hello 叢集選取範圍對話方塊方塊 toochoose 從 hello 組可用的訂閱和叢集。</span><span class="sxs-lookup"><span data-stu-id="a3117-138">Use hello cluster selection dialog box toochoose from hello set of available subscriptions and clusters.</span></span>
   
    ![hello * * 選取 Service Fabric 叢集 * * 對話方塊][1]
   
   > [!NOTE]
   > <span data-ttu-id="a3117-140">如果您想要 toopublish tooan 任意端點 （例如合作對象叢集），請參閱 hello**發佈 tooan 任意叢集端點**下一節。</span><span class="sxs-lookup"><span data-stu-id="a3117-140">If you would like toopublish tooan arbitrary endpoint (such as a party cluster), see hello **Publishing tooan arbitrary cluster endpoint** section below.</span></span>
   > 
   > 
   
    <span data-ttu-id="a3117-141">一旦您選擇端點時，Visual Studio 會驗證 hello 連接 toohello 選取 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="a3117-141">Once you choose an endpoint, Visual Studio validates hello connection toohello selected Service Fabric cluster.</span></span> <span data-ttu-id="a3117-142">如果 hello 叢集不安全，Visual Studio 就可以立即連線 tooit。</span><span class="sxs-lookup"><span data-stu-id="a3117-142">If hello cluster isn't secure, Visual Studio can connect tooit immediately.</span></span> <span data-ttu-id="a3117-143">不過，如果 hello 叢集是安全的您必須先 tooinstall 憑證後再繼續在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="a3117-143">However, if hello cluster is secure, you'll need tooinstall a certificate on your local computer before proceeding.</span></span> <span data-ttu-id="a3117-144">請參閱[tooconfigure 如何保護連線](service-fabric-visualstudio-configure-secure-connections.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a3117-144">See [How tooconfigure secure connections](service-fabric-visualstudio-configure-secure-connections.md) for more information.</span></span> <span data-ttu-id="a3117-145">當您完成時，選擇 hello**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3117-145">When you're done, choose hello **OK** button.</span></span> <span data-ttu-id="a3117-146">hello 選的叢集會出現在 hello**發行 Service Fabric 應用程式** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a3117-146">hello selected cluster appears in hello **Publish Service Fabric Application** dialog box.</span></span>
3. <span data-ttu-id="a3117-147">在 hello**應用程式參數檔案**下拉式清單方塊中，瀏覽 tooan 應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="a3117-147">In hello **Application Parameter File** dropdown list box, navigate tooan application parameter file.</span></span> <span data-ttu-id="a3117-148">應用程式參數檔案保存 hello 應用程式資訊清單檔中的使用者指定之參數的值。</span><span class="sxs-lookup"><span data-stu-id="a3117-148">An application parameter file holds user-specified values for parameters in hello application manifest file.</span></span> <span data-ttu-id="a3117-149">tooadd 或變更參數，選擇 [hello**編輯**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3117-149">tooadd or change a parameter, choose hello **Edit** button.</span></span> <span data-ttu-id="a3117-150">輸入或變更 hello 參數的值，在 hello**參數**方格。</span><span class="sxs-lookup"><span data-stu-id="a3117-150">Enter or change hello parameter's value in hello **Parameters** grid.</span></span> <span data-ttu-id="a3117-151">當您完成時，選擇 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3117-151">When you're done, choose hello **Save** button.</span></span>
   
    ![hello * * 編輯參數 * * 對話方塊][2]
4. <span data-ttu-id="a3117-153">使用 hello**升級 hello 應用程式**核取方塊 toospecify 是否此發行動作會升級。</span><span class="sxs-lookup"><span data-stu-id="a3117-153">Use hello **Upgrade hello Application** checkbox toospecify whether this publish action is an upgrade.</span></span> <span data-ttu-id="a3117-154">升級發佈動作不同於一般發佈動作。</span><span class="sxs-lookup"><span data-stu-id="a3117-154">Upgrade publish actions differ from normal publish actions.</span></span> <span data-ttu-id="a3117-155">如需差異清單，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md) 。</span><span class="sxs-lookup"><span data-stu-id="a3117-155">See [Service Fabric Application Upgrade](service-fabric-application-upgrade.md) for a list of differences.</span></span> <span data-ttu-id="a3117-156">tooconfigure 升級設定中，選擇 hello**設定升級設定**連結。</span><span class="sxs-lookup"><span data-stu-id="a3117-156">tooconfigure upgrade settings, choose hello **Configure Upgrade Settings** link.</span></span> <span data-ttu-id="a3117-157">hello 升級參數編輯器隨即出現。</span><span class="sxs-lookup"><span data-stu-id="a3117-157">hello upgrade parameter editor appears.</span></span> <span data-ttu-id="a3117-158">請參閱[設定 Service Fabric 應用程式的 hello 升級](service-fabric-visualstudio-configure-upgrade.md)toolearn 更多關於升級的參數。</span><span class="sxs-lookup"><span data-stu-id="a3117-158">See [Configure hello upgrade of a Service Fabric application](service-fabric-visualstudio-configure-upgrade.md) toolearn more about upgrade parameters.</span></span>
5. <span data-ttu-id="a3117-159">選擇 hello**資訊清單版本...**</span><span class="sxs-lookup"><span data-stu-id="a3117-159">Choose hello **Manifest Versions…**</span></span> <span data-ttu-id="a3117-160">按鈕 tooview hello**編輯版本** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a3117-160">button tooview hello **Edit Versions** dialog box.</span></span> <span data-ttu-id="a3117-161">您需要 tooupdate 應用程式和服務版本與升級 tootake 位置。</span><span class="sxs-lookup"><span data-stu-id="a3117-161">You need tooupdate application and service versions for an upgrade tootake place.</span></span> <span data-ttu-id="a3117-162">請參閱[Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)toolearn 如何應用程式與服務資訊清單版本會影響升級的程序。</span><span class="sxs-lookup"><span data-stu-id="a3117-162">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) toolearn how application and service manifest versions impact an upgrade process.</span></span>
   
    ![hello * * 編輯版本 * * 對話方塊][3]
   
    <span data-ttu-id="a3117-164">如果 hello 應用程式和服務版本使用語意版本設定，例如 1.0.0 或數值的 1.0.0.0 hello 格式中，選取 hello**自動更新應用程式和服務版本**選項。</span><span class="sxs-lookup"><span data-stu-id="a3117-164">If hello application and service versions use semantic versioning such as 1.0.0 or numerical values in hello format of 1.0.0.0, select hello **Automatically update application and service versions** option.</span></span> <span data-ttu-id="a3117-165">當您選擇此選項，hello 服務和應用程式版本號碼時會自動更新程式碼、 組態中，或資料封裝版本已更新。</span><span class="sxs-lookup"><span data-stu-id="a3117-165">When you choose this option, hello service and application version numbers are automatically updated whenever a code, config, or data package version is updated.</span></span> <span data-ttu-id="a3117-166">如果您手動偏好 tooedit hello 版本，請清除 hello 核取方塊 toodisable 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a3117-166">If you prefer tooedit hello versions manually, clear hello checkbox toodisable this feature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3117-167">所有動作項目專案的封裝項目 tooappear，第一次建立 hello 專案 toogenerate hello hello 服務資訊清單檔案中的項目。</span><span class="sxs-lookup"><span data-stu-id="a3117-167">For all package entries tooappear for an actor project, first build hello project toogenerate hello entries in hello Service Manifest files.</span></span>
   > 
   > 
6. <span data-ttu-id="a3117-168">當您完成指定所有必要的設定，hello 選擇 hello**發行**按鈕選取您的應用程式 toohello toopublish Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="a3117-168">When you're done specifying all of hello necessary settings, choose hello **Publish** button toopublish your application toohello selected Service Fabric cluster.</span></span> <span data-ttu-id="a3117-169">您指定的 hello 設定會套用 toohello 發佈程序。</span><span class="sxs-lookup"><span data-stu-id="a3117-169">hello settings that you specified are applied toohello publish process.</span></span>

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a><span data-ttu-id="a3117-170">發行 tooan 任意叢集端點 （包括合作對象叢集）</span><span class="sxs-lookup"><span data-stu-id="a3117-170">Publish tooan arbitrary cluster endpoint (including party clusters)</span></span>
<span data-ttu-id="a3117-171">hello Visual Studio 發行經驗最適合用於發行 tooremote 叢集與其中一個 Azure 訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="a3117-171">hello Visual Studio publishing experience is optimized for publishing tooremote clusters associated with one of your Azure subscriptions.</span></span> <span data-ttu-id="a3117-172">不過，它是可能 toopublish tooarbitrary 端點 （例如 Service Fabric 合作對象的叢集） 直接編輯 hello 發行設定檔 XML。</span><span class="sxs-lookup"><span data-stu-id="a3117-172">However, it is possible toopublish tooarbitrary endpoints (such as Service Fabric party clusters) by directly editing hello publish profile XML.</span></span> <span data-ttu-id="a3117-173">如上面所述，三個發行設定檔所提供的預設值-**Local.1Node.xml**， **Local.5Node.xml**，和**Cloud.xml**-卻  褖畫惎 toocreate不同環境的其他設定檔。</span><span class="sxs-lookup"><span data-stu-id="a3117-173">As described above, three publish profiles are provided by default--**Local.1Node.xml**, **Local.5Node.xml**, and **Cloud.xml**--but you are welcome toocreate additional profiles for different environments.</span></span> <span data-ttu-id="a3117-174">比方說，您可能希望 toocreate 設定檔發佈 tooparty 叢集，可能名為**Party.xml**。</span><span class="sxs-lookup"><span data-stu-id="a3117-174">For instance, you might want toocreate a profile for publishing tooparty clusters, perhaps named **Party.xml**.</span></span>

<span data-ttu-id="a3117-175">如果您要連接不安全叢集的 tooan，只需要是 hello 叢集連接的端點，如`partycluster1.eastus.cloudapp.azure.com:19000`。</span><span class="sxs-lookup"><span data-stu-id="a3117-175">If you are connecting tooan unsecured cluster, all that's required is hello cluster connection endpoint, such as `partycluster1.eastus.cloudapp.azure.com:19000`.</span></span> <span data-ttu-id="a3117-176">大小寫，在 hello hello 連接端點發行設定檔看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="a3117-176">In that case, hello connection endpoint in hello publish profile would look something like this:</span></span>

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  <span data-ttu-id="a3117-177">如果您要連接 tooa 受保護的叢集，您也需要從 hello 用於驗證的本機存放區 toobe hello 用戶端憑證的 tooprovide hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a3117-177">If you are connecting tooa secured cluster, you will also need tooprovide hello details of hello client certificate from hello local store toobe used for authentication.</span></span> <span data-ttu-id="a3117-178">如需詳細資訊，請參閱[設定安全連接 tooa Service Fabric 叢集](service-fabric-visualstudio-configure-secure-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="a3117-178">For more details, see [Configuring secure connections tooa Service Fabric cluster](service-fabric-visualstudio-configure-secure-connections.md).</span></span>

  <span data-ttu-id="a3117-179">一旦設定您的發行設定檔之後，您可以在中參考它 hello 發行 web 對話方塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a3117-179">Once your publish profile is set up, you can reference it in hello publish dialog box as shown below.</span></span>

  ![發佈對話方塊中的新發行設定檔][4]

  <span data-ttu-id="a3117-181">請注意，在此情況下，新的 hello 發行設定檔點 tooone hello 預設應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="a3117-181">Note that in this case, hello new publish profile points tooone of hello default application parameter files.</span></span> <span data-ttu-id="a3117-182">這是適當 toopublish 如果您想 hello 相同應用程式組態 tooa 數目的環境。</span><span class="sxs-lookup"><span data-stu-id="a3117-182">This is appropriate if you want toopublish hello same application configuration tooa number of environments.</span></span> <span data-ttu-id="a3117-183">相反地，在您希望每個環境，您想要 toopublish toohave 不同組態的情況下，它會使意義 toocreate 相對應的應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="a3117-183">By contrast, in cases where you want toohave different configurations for each environment that you want toopublish to, it would make sense toocreate a corresponding application parameter file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3117-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3117-184">Next steps</span></span>
<span data-ttu-id="a3117-185">如何 tooautomate hello 發佈程序在持續整合環境中，請參閱的 toolearn[設定 Service Fabric 連續整合](service-fabric-set-up-continuous-integration.md)。</span><span class="sxs-lookup"><span data-stu-id="a3117-185">toolearn how tooautomate hello publishing process in a continuous integration environment, see [Set up Service Fabric continuous integration](service-fabric-set-up-continuous-integration.md).</span></span>

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
