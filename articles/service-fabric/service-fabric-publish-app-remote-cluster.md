---
title: "使用 Visual Studio 將應用程式發佈至遠端叢集 |Microsoft Docs"
description: "了解如何使用 Visual Studio 將應用程式發佈至遠端 Service Fabric 叢集。"
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
ms.openlocfilehash: c440c520d84fc503ff9e705555449e92555d4721
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a><span data-ttu-id="52a8b-103">使用 Visual Studio 來部署和移除應用程式</span><span class="sxs-lookup"><span data-stu-id="52a8b-103">Deploy and remove applications using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52a8b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52a8b-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="52a8b-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52a8b-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="52a8b-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="52a8b-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="52a8b-107">Azure Service Fabric extension for Visual Studio 提供簡單、可重複且可編寫指令碼的方式，將應用程式發佈至 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="52a8b-107">The Azure Service Fabric extension for Visual Studio provides an easy, repeatable, and scriptable way to publish an application to a Service Fabric cluster.</span></span>

## <a name="the-artifacts-required-for-publishing"></a><span data-ttu-id="52a8b-108">發佈所需的構件</span><span class="sxs-lookup"><span data-stu-id="52a8b-108">The artifacts required for publishing</span></span>
### <a name="deploy-fabricapplicationps1"></a><span data-ttu-id="52a8b-109">Deploy-FabricApplication.ps1</span><span class="sxs-lookup"><span data-stu-id="52a8b-109">Deploy-FabricApplication.ps1</span></span>
<span data-ttu-id="52a8b-110">這是 PowerShell 指令碼，使用發佈設定檔路徑做為參數，以發佈 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52a8b-110">This is a PowerShell script that uses a publish profile path as a parameter for publishing Service Fabric applications.</span></span> <span data-ttu-id="52a8b-111">由於此指令碼是您的應用程式的一部分，您可以視需要為應用程式修改。</span><span class="sxs-lookup"><span data-stu-id="52a8b-111">Since this script is part of your application, you are welcome to modify it as necessary for your application.</span></span>

### <a name="publish-profiles"></a><span data-ttu-id="52a8b-112">發佈設定檔</span><span class="sxs-lookup"><span data-stu-id="52a8b-112">Publish profiles</span></span>
<span data-ttu-id="52a8b-113">名為 **PublishProfiles** 的 Service Fabric 應用程式專案中的資料夾包含 XML 檔案，可儲存用以發佈應用程式的基本資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="52a8b-113">A folder in the Service Fabric application project called **PublishProfiles** contains XML files that store essential information for publishing an application, such as:</span></span>

* <span data-ttu-id="52a8b-114">Service Fabric 叢集連線參數</span><span class="sxs-lookup"><span data-stu-id="52a8b-114">Service Fabric cluster connection parameters</span></span>
* <span data-ttu-id="52a8b-115">應用程式參數檔案的路徑</span><span class="sxs-lookup"><span data-stu-id="52a8b-115">Path to an application parameter file</span></span>
* <span data-ttu-id="52a8b-116">升級設定</span><span class="sxs-lookup"><span data-stu-id="52a8b-116">Upgrade settings</span></span>

<span data-ttu-id="52a8b-117">根據預設，您的應用程式會包含三個發佈設定檔：Local.1Node.xml、Local.5Node.xml 和 Cloud.xml。</span><span class="sxs-lookup"><span data-stu-id="52a8b-117">By default, your application will include three publish profiles: Local.1Node.xml, Local.5Node.xml, and Cloud.xml.</span></span> <span data-ttu-id="52a8b-118">您可以藉由複製並貼上其中一個預設檔案，新增更多設定檔。</span><span class="sxs-lookup"><span data-stu-id="52a8b-118">You can add more profiles by copying and pasting one of the default files.</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="52a8b-119">應用程式參數檔案</span><span class="sxs-lookup"><span data-stu-id="52a8b-119">Application parameter files</span></span>
<span data-ttu-id="52a8b-120">名為 **ApplicationParameters** 的 Service Fabric 應用程式專案中的資料夾，包含使用者指定應用程式資訊清單參數值的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="52a8b-120">A folder in the Service Fabric application project called **ApplicationParameters** contains XML files for user-specified application manifest parameter values.</span></span> <span data-ttu-id="52a8b-121">應用程式資訊清單檔案可以參數化，讓您可以針對部署設定使用不同的值。</span><span class="sxs-lookup"><span data-stu-id="52a8b-121">Application manifest files can be parameterized so that you can use different values for deployment settings.</span></span> <span data-ttu-id="52a8b-122">若要深入了解參數化您的應用程式，請參閱 [在 Service Fabric 中管理多個環境](service-fabric-manage-multiple-environment-app-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="52a8b-122">To learn more about parameterizing your application, see [Manage multiple environments in Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

> [!NOTE]
> <span data-ttu-id="52a8b-123">對於動作項目服務，您應該在嘗試使用編輯器或透過 [發佈] 對話方塊編輯檔案之前，先建置專案。</span><span class="sxs-lookup"><span data-stu-id="52a8b-123">For actor services, you should build the project first before attempting to edit the file in an editor or through the publish dialog box.</span></span> <span data-ttu-id="52a8b-124">這是因為在建置期間，將會產生部分資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="52a8b-124">This is because part of the manifest files will be generated during the build.</span></span>

## <a name="to-publish-an-application-using-the-publish-service-fabric-application-dialog-box"></a><span data-ttu-id="52a8b-125">使用 [發佈 Service Fabric 應用程式] 對話方塊發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="52a8b-125">To publish an application using the Publish Service Fabric Application dialog box</span></span>
<span data-ttu-id="52a8b-126">下列步驟示範如何使用 Visual Studio Service Fabric 工具提供的 [發佈 Service Fabric 應用程式]  對話方塊發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="52a8b-126">The following steps demonstrate how to publish an application using the **Publish Service Fabric Application** dialog box provided by the Visual Studio Service Fabric Tools.</span></span>

1. <span data-ttu-id="52a8b-127">在 Service Fabric 應用程式專案的捷徑功能表上，選擇 [發佈...]</span><span class="sxs-lookup"><span data-stu-id="52a8b-127">On the shortcut menu of the Service Fabric Application project, choose **Publish…**</span></span> <span data-ttu-id="52a8b-128">以檢視 [發佈 Service Fabric 應用程式] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="52a8b-128">to view the **Publish Service Fabric Application** dialog box.</span></span>
   
    ![[發佈 Service Fabric 應用程式] 對話方塊][0]
   
    <span data-ttu-id="52a8b-130">在 [目標設定檔] 下拉式清單中選取的檔案，是儲存 [資訊清單版本] 以外所有設定的位置。</span><span class="sxs-lookup"><span data-stu-id="52a8b-130">The file selected in the **Target profile** dropdown list box is where all of the settings, except **Manifest versions**, are saved.</span></span> <span data-ttu-id="52a8b-131">您可以重複使用現有設定檔，或透過選擇 [目標設定檔] 下拉式清單方塊中的 [管理設定檔...] 來建立一個新的設定檔。</span><span class="sxs-lookup"><span data-stu-id="52a8b-131">You can either reuse an existing profile or create a new one by choosing **<Manage Profiles…>** in the **Target profile** dropdown list box.</span></span> <span data-ttu-id="52a8b-132">當您選擇發行設定檔時，其內容會出現在對話方塊的對應欄位中。</span><span class="sxs-lookup"><span data-stu-id="52a8b-132">When you choose a publish profile, its contents appear in the corresponding fields of the dialog box.</span></span> <span data-ttu-id="52a8b-133">若要隨時儲存變更，請選擇 [儲存設定檔]  連結。</span><span class="sxs-lookup"><span data-stu-id="52a8b-133">To save your changes at any time, choose the **Save Profile** link.</span></span>    
2. <span data-ttu-id="52a8b-134">在 [連接端點]  區段中，指定本機或遠端 Service Fabric 叢集的發佈端點。</span><span class="sxs-lookup"><span data-stu-id="52a8b-134">In the **Connection endpoint** section, specify a local or remote Service Fabric cluster’s publishing endpoint.</span></span> <span data-ttu-id="52a8b-135">若要新增或變更連接端點，請按一下 [連接端點]  下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="52a8b-135">To add or change the connection endpoint, click on the **Connection Endpoint** dropdown list.</span></span> <span data-ttu-id="52a8b-136">此清單會根據您的 Azure 訂用帳戶，顯示您可以對其發佈的可用 Service Fabric 叢集連接端點。</span><span class="sxs-lookup"><span data-stu-id="52a8b-136">The list shows the available Service Fabric cluster connection endpoints to which you can publish based on your Azure subscription(s).</span></span> <span data-ttu-id="52a8b-137">請注意，如果您尚未登入 Visual Studio，系統將會提示您登入。</span><span class="sxs-lookup"><span data-stu-id="52a8b-137">Note that if you are not already logged in to Visual Studio, you will be prompted to do so.</span></span>
   
    <span data-ttu-id="52a8b-138">使用 [叢集選項] 對話方塊從一組可用的訂用帳戶和叢集中選擇。</span><span class="sxs-lookup"><span data-stu-id="52a8b-138">Use the cluster selection dialog box to choose from the set of available subscriptions and clusters.</span></span>
   
    ![[選取 Service Fabric 叢集] 對話方塊][1]
   
   > [!NOTE]
   > <span data-ttu-id="52a8b-140">如果您想要發佈至任意端點 (例如合作對象叢集)，請參閱下面的＜發佈到任意叢集端點＞一節。</span><span class="sxs-lookup"><span data-stu-id="52a8b-140">If you would like to publish to an arbitrary endpoint (such as a party cluster), see the **Publishing to an arbitrary cluster endpoint** section below.</span></span>
   > 
   > 
   
    <span data-ttu-id="52a8b-141">一旦您選擇端點，Visual Studio 會驗證與選取的 Service Fabric 叢集的連線。</span><span class="sxs-lookup"><span data-stu-id="52a8b-141">Once you choose an endpoint, Visual Studio validates the connection to the selected Service Fabric cluster.</span></span> <span data-ttu-id="52a8b-142">如果叢集未受到保護，Visual Studio 可以立即與其連線。</span><span class="sxs-lookup"><span data-stu-id="52a8b-142">If the cluster isn't secure, Visual Studio can connect to it immediately.</span></span> <span data-ttu-id="52a8b-143">不過，如果叢集受到保護，您必須在本機電腦上安裝憑證才能繼續。</span><span class="sxs-lookup"><span data-stu-id="52a8b-143">However, if the cluster is secure, you'll need to install a certificate on your local computer before proceeding.</span></span> <span data-ttu-id="52a8b-144">如需詳細資訊，請參閱 [如何設定安全連接](service-fabric-visualstudio-configure-secure-connections.md) 。</span><span class="sxs-lookup"><span data-stu-id="52a8b-144">See [How to configure secure connections](service-fabric-visualstudio-configure-secure-connections.md) for more information.</span></span> <span data-ttu-id="52a8b-145">完成時，選擇 [確定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="52a8b-145">When you're done, choose the **OK** button.</span></span> <span data-ttu-id="52a8b-146">選取的叢集會出現在 [發佈 Service Fabric 應用程式]  對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="52a8b-146">The selected cluster appears in the **Publish Service Fabric Application** dialog box.</span></span>
3. <span data-ttu-id="52a8b-147">在 [應用程式參數檔案]  下拉式清單方塊中，瀏覽至應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="52a8b-147">In the **Application Parameter File** dropdown list box, navigate to an application parameter file.</span></span> <span data-ttu-id="52a8b-148">應用程式參數檔案會保留應用程式資訊清單檔案中參數的使用者指定值。</span><span class="sxs-lookup"><span data-stu-id="52a8b-148">An application parameter file holds user-specified values for parameters in the application manifest file.</span></span> <span data-ttu-id="52a8b-149">若要新增或變更參數，請選擇 [編輯]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="52a8b-149">To add or change a parameter, choose the **Edit** button.</span></span> <span data-ttu-id="52a8b-150">在 [參數]  方格中輸入或變更參數值。</span><span class="sxs-lookup"><span data-stu-id="52a8b-150">Enter or change the parameter's value in the **Parameters** grid.</span></span> <span data-ttu-id="52a8b-151">完成時，請選擇 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="52a8b-151">When you're done, choose the **Save** button.</span></span>
   
    ![[編輯參數] 對話方塊][2]
4. <span data-ttu-id="52a8b-153">使用 [升級應用程式]  核取方塊指定此發佈動作是否為升級。</span><span class="sxs-lookup"><span data-stu-id="52a8b-153">Use the **Upgrade the Application** checkbox to specify whether this publish action is an upgrade.</span></span> <span data-ttu-id="52a8b-154">升級發佈動作不同於一般發佈動作。</span><span class="sxs-lookup"><span data-stu-id="52a8b-154">Upgrade publish actions differ from normal publish actions.</span></span> <span data-ttu-id="52a8b-155">如需差異清單，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md) 。</span><span class="sxs-lookup"><span data-stu-id="52a8b-155">See [Service Fabric Application Upgrade](service-fabric-application-upgrade.md) for a list of differences.</span></span> <span data-ttu-id="52a8b-156">若要設定升級設定，請選擇 [設定升級設定]  連結。</span><span class="sxs-lookup"><span data-stu-id="52a8b-156">To configure upgrade settings, choose the **Configure Upgrade Settings** link.</span></span> <span data-ttu-id="52a8b-157">升級參數編輯器隨即出現。</span><span class="sxs-lookup"><span data-stu-id="52a8b-157">The upgrade parameter editor appears.</span></span> <span data-ttu-id="52a8b-158">若要深入了解升級參數，請參閱 [設定 Service Fabric 應用程式的升級](service-fabric-visualstudio-configure-upgrade.md) 。</span><span class="sxs-lookup"><span data-stu-id="52a8b-158">See [Configure the upgrade of a Service Fabric application](service-fabric-visualstudio-configure-upgrade.md) to learn more about upgrade parameters.</span></span>
5. <span data-ttu-id="52a8b-159">選擇 [資訊清單版本...]</span><span class="sxs-lookup"><span data-stu-id="52a8b-159">Choose the **Manifest Versions…**</span></span> <span data-ttu-id="52a8b-160">按鈕，以檢視 [編輯版本] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="52a8b-160">button to view the **Edit Versions** dialog box.</span></span> <span data-ttu-id="52a8b-161">您需要更新應用程式和服務版本才能進行升級。</span><span class="sxs-lookup"><span data-stu-id="52a8b-161">You need to update application and service versions for an upgrade to take place.</span></span> <span data-ttu-id="52a8b-162">請參閱 [Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md) ，以了解應用程式和服務資訊清單版本如何影響升級程序。</span><span class="sxs-lookup"><span data-stu-id="52a8b-162">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) to learn how application and service manifest versions impact an upgrade process.</span></span>
   
    ![[編輯版本] 對話方塊][3]
   
    <span data-ttu-id="52a8b-164">如果應用程式和服務版本使用例如 1.0.0 的語意版本設定，或格式為 1.0.0.0 的數值，請選取 [自動更新應用程式和服務版本]  選項。</span><span class="sxs-lookup"><span data-stu-id="52a8b-164">If the application and service versions use semantic versioning such as 1.0.0 or numerical values in the format of 1.0.0.0, select the **Automatically update application and service versions** option.</span></span> <span data-ttu-id="52a8b-165">當您選擇這個選項時，服務和應用程式版本號碼會在程式碼、組態中或資料封裝版本更新時自動更新。</span><span class="sxs-lookup"><span data-stu-id="52a8b-165">When you choose this option, the service and application version numbers are automatically updated whenever a code, config, or data package version is updated.</span></span> <span data-ttu-id="52a8b-166">如果您想要以手動方式編輯版本，請清除核取方塊以停用此功能。</span><span class="sxs-lookup"><span data-stu-id="52a8b-166">If you prefer to edit the versions manually, clear the checkbox to disable this feature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="52a8b-167">對於針對動作項目專案出現的所有封裝項目，首先建置專案來產生服務資訊清單檔案中的項目。</span><span class="sxs-lookup"><span data-stu-id="52a8b-167">For all package entries to appear for an actor project, first build the project to generate the entries in the Service Manifest files.</span></span>
   > 
   > 
6. <span data-ttu-id="52a8b-168">當您完成指定所有必要的設定，選擇 [發佈]  按鈕以將應用程式發佈至所選的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="52a8b-168">When you're done specifying all of the necessary settings, choose the **Publish** button to publish your application to the selected Service Fabric cluster.</span></span> <span data-ttu-id="52a8b-169">您指定的設定會套用至發佈程序。</span><span class="sxs-lookup"><span data-stu-id="52a8b-169">The settings that you specified are applied to the publish process.</span></span>

## <a name="publish-to-an-arbitrary-cluster-endpoint-including-party-clusters"></a><span data-ttu-id="52a8b-170">發佈至任意叢集端點 (包括合作對象叢集)</span><span class="sxs-lookup"><span data-stu-id="52a8b-170">Publish to an arbitrary cluster endpoint (including party clusters)</span></span>
<span data-ttu-id="52a8b-171">Visual Studio 發佈體驗已針對發佈至遠端叢集 (與您的其中一個 Azure 訂用帳戶相關聯) 最佳化。</span><span class="sxs-lookup"><span data-stu-id="52a8b-171">The Visual Studio publishing experience is optimized for publishing to remote clusters associated with one of your Azure subscriptions.</span></span> <span data-ttu-id="52a8b-172">不過，可以發佈至任意端點 (例如 Service Fabric 合作對象叢集)，方法是直接編輯發行設定檔 XML。</span><span class="sxs-lookup"><span data-stu-id="52a8b-172">However, it is possible to publish to arbitrary endpoints (such as Service Fabric party clusters) by directly editing the publish profile XML.</span></span> <span data-ttu-id="52a8b-173">如上所述，預設會提供三個發佈設定檔 (**Local.1Node.xml**、**Local.5Node.xml** 和 **Cloud.xml**)，但是您可以針對不同的環境建立其他設定檔。</span><span class="sxs-lookup"><span data-stu-id="52a8b-173">As described above, three publish profiles are provided by default--**Local.1Node.xml**, **Local.5Node.xml**, and **Cloud.xml**--but you are welcome to create additional profiles for different environments.</span></span> <span data-ttu-id="52a8b-174">例如，您可能想要建立設定檔以發佈至合作對象叢集，也許命名為 **Party.xml**。</span><span class="sxs-lookup"><span data-stu-id="52a8b-174">For instance, you might want to create a profile for publishing to party clusters, perhaps named **Party.xml**.</span></span>

<span data-ttu-id="52a8b-175">如果您要連線到不安全的叢集，只需要叢集連線端點，例如 `partycluster1.eastus.cloudapp.azure.com:19000`。</span><span class="sxs-lookup"><span data-stu-id="52a8b-175">If you are connecting to an unsecured cluster, all that's required is the cluster connection endpoint, such as `partycluster1.eastus.cloudapp.azure.com:19000`.</span></span> <span data-ttu-id="52a8b-176">在該情況下，發行設定檔中的連接端點看起來會類似：</span><span class="sxs-lookup"><span data-stu-id="52a8b-176">In that case, the connection endpoint in the publish profile would look something like this:</span></span>

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  <span data-ttu-id="52a8b-177">如果您要連接到安全的叢集，您也必須提供要用於驗證的本機存放區中的用戶端憑證的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52a8b-177">If you are connecting to a secured cluster, you will also need to provide the details of the client certificate from the local store to be used for authentication.</span></span> <span data-ttu-id="52a8b-178">如需詳細資訊，請參閱 [設定對 Service Fabric 叢集的安全連線](service-fabric-visualstudio-configure-secure-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="52a8b-178">For more details, see [Configuring secure connections to a Service Fabric cluster](service-fabric-visualstudio-configure-secure-connections.md).</span></span>

  <span data-ttu-id="52a8b-179">發行設定檔設定完畢後，您可以在發佈對話方塊中參考它，如下所示。</span><span class="sxs-lookup"><span data-stu-id="52a8b-179">Once your publish profile is set up, you can reference it in the publish dialog box as shown below.</span></span>

  ![發佈對話方塊中的新發行設定檔][4]

  <span data-ttu-id="52a8b-181">請注意，在此情況下，新的發行設定檔會指向其中一個預設應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="52a8b-181">Note that in this case, the new publish profile points to one of the default application parameter files.</span></span> <span data-ttu-id="52a8b-182">如果您想要將相同應用程式組態發佈至數個環境，這是適合的。</span><span class="sxs-lookup"><span data-stu-id="52a8b-182">This is appropriate if you want to publish the same application configuration to a number of environments.</span></span> <span data-ttu-id="52a8b-183">相反地，如果您要發佈的每個環境有不同的組態，建立對應的應用程式參數檔案比較合理。</span><span class="sxs-lookup"><span data-stu-id="52a8b-183">By contrast, in cases where you want to have different configurations for each environment that you want to publish to, it would make sense to create a corresponding application parameter file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52a8b-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52a8b-184">Next steps</span></span>
<span data-ttu-id="52a8b-185">若要了解如何在連續整合環境中自動化發佈程序，請參閱 [設定 Service Fabric 連續整合](service-fabric-set-up-continuous-integration.md)。</span><span class="sxs-lookup"><span data-stu-id="52a8b-185">To learn how to automate the publishing process in a continuous integration environment, see [Set up Service Fabric continuous integration](service-fabric-set-up-continuous-integration.md).</span></span>

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
