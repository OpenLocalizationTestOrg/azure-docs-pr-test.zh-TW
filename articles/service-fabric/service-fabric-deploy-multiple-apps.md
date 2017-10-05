---
title: "部署使用 MongoDB 的 Node.js 應用程式 | Microsoft Docs"
description: "如何封裝多個來賓可執行檔以部署至 Azure Service Fabric 叢集的逐步解說"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: b71723034e5f663986c49481072bfd6779d3d57b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="58186-103">部署多個來賓可執行檔</span><span class="sxs-lookup"><span data-stu-id="58186-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="58186-104">本文說明如何封裝多個來賓可執行檔並部署至 Azure Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="58186-104">This article shows how to package and deploy multiple guest executables to Azure Service Fabric.</span></span> <span data-ttu-id="58186-105">若要建置和部署單一 Service Fabric 套件，請閱讀如何[將來賓可執行檔部署至 Service Fabric](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="58186-105">For building and deploying a single Service Fabric package read how to [deploy a guest executable to Service Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="58186-106">雖然本逐步解說示範的是如何部署使用 MongoDB 做為資料存放區並具有 Node.js 前端的應用程式，但是您可以將這些步驟套用到任何與另一個應用程式具有相依性的應用程式。</span><span class="sxs-lookup"><span data-stu-id="58186-106">While this walkthrough shows how to deploy an application with a Node.js front end that uses MongoDB as the data store, you can apply the steps to any application that has dependencies on another application.</span></span>   

<span data-ttu-id="58186-107">您可以使用 Visual Studio 來產生包含多個來賓可執行檔的應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="58186-107">You can use Visual Studio to produce the application package that contains multiple guest executables.</span></span> <span data-ttu-id="58186-108">請參閱[使用 Visual Studio 封裝現有應用程式](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="58186-108">See [Using Visual Studio to package an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="58186-109">新增第一個來賓可執行檔之後，在應用程式專案上按一下滑鼠右鍵，然後選取 [新增] -> [新的 Service Fabric 服務] 將第二個來賓可執行檔專案新增至方案。</span><span class="sxs-lookup"><span data-stu-id="58186-109">After you have added the first guest executable, right click on the application project and select the **Add->New Service Fabric service** to add the second guest executable project to the solution.</span></span> <span data-ttu-id="58186-110">請注意：如果您選擇在 Visual Studio 專案中連結來源，則建置 Visual Studio 方案將可確保應用程式封裝是最新的，並且含有來源中的變更。</span><span class="sxs-lookup"><span data-stu-id="58186-110">Note: If you choose to link the source in the Visual Studio project, building the Visual Studio solution, will make sure that your application package is up to date with changes in the source.</span></span> 

## <a name="samples"></a><span data-ttu-id="58186-111">範例</span><span class="sxs-lookup"><span data-stu-id="58186-111">Samples</span></span>
* [<span data-ttu-id="58186-112">封裝和部署來賓可執行檔的範例</span><span class="sxs-lookup"><span data-stu-id="58186-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="58186-113">兩個客體可執行檔 (C# 和 nodejs) 使用 REST 透過命名服務進行通訊的範例</span><span class="sxs-lookup"><span data-stu-id="58186-113">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-the-multiple-guest-executable-application"></a><span data-ttu-id="58186-114">手動封裝多個來賓可執行檔應用程式</span><span class="sxs-lookup"><span data-stu-id="58186-114">Manually package the multiple guest executable application</span></span>
<span data-ttu-id="58186-115">或者，您可以手動封裝來賓可執行檔。</span><span class="sxs-lookup"><span data-stu-id="58186-115">Alternatively you can manually package the guest executable.</span></span> <span data-ttu-id="58186-116">對於手動封裝，本文使用 Service Fabric 封裝工具，您可在 [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool) 取得。</span><span class="sxs-lookup"><span data-stu-id="58186-116">For the manual packaging, this article uses the Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-the-nodejs-application"></a><span data-ttu-id="58186-117">封裝 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="58186-117">Packaging the Node.js application</span></span>
<span data-ttu-id="58186-118">本文假設 Service Fabric 叢集中的節點上未安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="58186-118">This article assumes that Node.js is not installed on the nodes in the Service Fabric cluster.</span></span> <span data-ttu-id="58186-119">因此，您需要在封裝之前，先將 Node.exe 新增至您節點應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="58186-119">As a consequence, you need to add Node.exe to the root directory of your node application before packaging.</span></span> <span data-ttu-id="58186-120">Node.js 應用程式 (使用 Express Web 架構和 Jade 範本引擎) 的目錄結構看起來應該與以下類似：</span><span class="sxs-lookup"><span data-stu-id="58186-120">The directory structure of the Node.js application (using Express web framework and Jade template engine) should look similar to the one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="58186-121">在下一個步驟中，您將為 Node.js 應用程式建立應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="58186-121">As a next step, you create an application package for the Node.js application.</span></span> <span data-ttu-id="58186-122">以下程式碼會建立包含 Node.js 應用程式的 Service Fabric 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="58186-122">The code below creates a Service Fabric application package that contains the Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="58186-123">以下是所使用之參數的描述：</span><span class="sxs-lookup"><span data-stu-id="58186-123">Below is a description of the parameters that are being used:</span></span>

* <span data-ttu-id="58186-124">**/source** 指向應封裝之應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="58186-124">**/source** points to the directory of the application that should be packaged.</span></span>
* <span data-ttu-id="58186-125">**/target** 定義應在其中建立封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="58186-125">**/target** defines the directory in which the package should be created.</span></span> <span data-ttu-id="58186-126">這個目錄必須是與來源目錄不同的目錄。</span><span class="sxs-lookup"><span data-stu-id="58186-126">This directory has to be different from the source directory.</span></span>
* <span data-ttu-id="58186-127">**/appname** 定義現有應用程式的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="58186-127">**/appname** defines the application name of the existing application.</span></span> <span data-ttu-id="58186-128">請務必了解這會轉譯成資訊清單中的服務名稱，而不是轉譯成 Service Fabric 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="58186-128">It's important to understand that this translates to the service name in the manifest, and not to the Service Fabric application name.</span></span>
* <span data-ttu-id="58186-129">**/exe** 定義 Service Fabric 應啟動的可執行檔，在此例中為 `node.exe`。</span><span class="sxs-lookup"><span data-stu-id="58186-129">**/exe** defines the executable that Service Fabric is supposed to launch, in this case `node.exe`.</span></span>
* <span data-ttu-id="58186-130">**/ma** 定義要用來啟動可執行檔的引數。</span><span class="sxs-lookup"><span data-stu-id="58186-130">**/ma** defines the argument that is being used to launch the executable.</span></span> <span data-ttu-id="58186-131">由於未安裝 Node.js，因此 Service Fabric 需要執行 `node.exe bin/www`來啟動 Node.js Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="58186-131">As Node.js is not installed, Service Fabric needs to launch the Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="58186-132">`/ma:'bin/www'` 會告訴封裝工具使用 `bin/ma` 當做 node.exe 的引數。</span><span class="sxs-lookup"><span data-stu-id="58186-132">`/ma:'bin/www'` tells the packaging tool to use `bin/ma` as the argument for node.exe.</span></span>
* <span data-ttu-id="58186-133">**/AppType** 定義 Service Fabric 應用程式類型名稱。</span><span class="sxs-lookup"><span data-stu-id="58186-133">**/AppType** defines the Service Fabric application type name.</span></span>

<span data-ttu-id="58186-134">如果您瀏覽至 /target 參數中指定的目錄，您可以看到工具已建立可完整運作的 Service Fabric 封裝，如以下所示：</span><span class="sxs-lookup"><span data-stu-id="58186-134">If you browse to the directory that was specified in the /target parameter, you can see that the tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="58186-135">所產生的 ServiceManifest.xml 現在有個描述應該如何啟動 Node.js Web 伺服器的區段，如以下程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="58186-135">The generated ServiceManifest.xml now has a section that describes how the Node.js web server should be launched, as shown in the code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="58186-136">在此範例中，Node.js Web 伺服器會接聽通訊埠 3000，所以您需要更新 ServiceManifest.xml 檔案中的端點資訊，如以下所示。</span><span class="sxs-lookup"><span data-stu-id="58186-136">In this sample, the Node.js web server listens to port 3000, so you need to update the endpoint information in the ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-the-mongodb-application"></a><span data-ttu-id="58186-137">封裝 MongoDB 應用程式</span><span class="sxs-lookup"><span data-stu-id="58186-137">Packaging the MongoDB application</span></span>
<span data-ttu-id="58186-138">既然您已封裝 Node.js 應用程式，您可以繼續封裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="58186-138">Now that you have packaged the Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="58186-139">如先前所提到的，您現在進行的步驟並非 Node.js 和 MongoDB 專用的步驟。</span><span class="sxs-lookup"><span data-stu-id="58186-139">As mentioned before, the steps that you go through now are not specific to Node.js and MongoDB.</span></span> <span data-ttu-id="58186-140">事實上，它們適用於所有要封裝在一起以做為一個 Service Fabric 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="58186-140">In fact, they apply to all applications that are meant to be packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="58186-141">為了封裝 MongoDB，您會想要確定您封裝 Mongod.exe 和 Mongo.exe。</span><span class="sxs-lookup"><span data-stu-id="58186-141">To package MongoDB, you want to make sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="58186-142">這兩個二進位檔都位於 MongoDB 安裝目錄的 `bin` 目錄中。</span><span class="sxs-lookup"><span data-stu-id="58186-142">Both binaries are located in the `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="58186-143">目錄結構類似於下方的結構。</span><span class="sxs-lookup"><span data-stu-id="58186-143">The directory structure looks similar to the one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="58186-144">Service Fabric 需要使用類似於下方的命令來啟動 MongoDB，因此封裝 MongoDB 時，您需要使用 `/ma` 參數。</span><span class="sxs-lookup"><span data-stu-id="58186-144">Service Fabric needs to start MongoDB with a command similar to the one below, so you need to use the `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path to data]
```
> [!NOTE]
> <span data-ttu-id="58186-145">如果您將 MongoDB 資料目錄放在節點的本機目錄中，當節點發生失敗時，將不會保留資料。</span><span class="sxs-lookup"><span data-stu-id="58186-145">The data is not being preserved in the case of a node failure if you put the MongoDB data directory on the local directory of the node.</span></span> <span data-ttu-id="58186-146">您應該使用永久性儲存體或實作 MongoDB 複本集以防止資料遺失。</span><span class="sxs-lookup"><span data-stu-id="58186-146">You should either use durable storage or implement a MongoDB replica set in order to prevent data loss.</span></span>  
>
>

<span data-ttu-id="58186-147">在 PowerShell 或命令殼層中，我們會使用下列參數來執行封裝工具：</span><span class="sxs-lookup"><span data-stu-id="58186-147">In PowerShell or the command shell, we run the packaging tool with the following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path to data]' /AppType:NodeAppType
```

<span data-ttu-id="58186-148">為了將 MongoDB 新增至您的 Service Fabric 應用程式封裝，您必須確定 /target 參數指向已經包含應用程式資訊清單及 Node.js 應用程式的同一個目錄。</span><span class="sxs-lookup"><span data-stu-id="58186-148">In order to add MongoDB to your Service Fabric application package, you need to make sure that the /target parameter points to the same directory that already contains the application manifest along with the Node.js application.</span></span> <span data-ttu-id="58186-149">您也需要確定您是使用相同的 ApplicationType 名稱。</span><span class="sxs-lookup"><span data-stu-id="58186-149">You also need to make sure that you are using the same ApplicationType name.</span></span>

<span data-ttu-id="58186-150">讓我們瀏覽至該目錄並檢查已建立的工具。</span><span class="sxs-lookup"><span data-stu-id="58186-150">Let's browse to the directory and examine what the tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="58186-151">如您所見，工具已將新資料夾 [MongoDB] 新增至包含 MongoDB 二進位檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="58186-151">As you can see, the tool added a new folder, MongoDB, to the directory that contains the MongoDB binaries.</span></span> <span data-ttu-id="58186-152">如果您開啟 `ApplicationManifest.xml` 檔案，您將可以看到封裝現在包含 Node.js 應用程式和 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="58186-152">If you open the `ApplicationManifest.xml` file, you can see that the package now contains both the Node.js application and MongoDB.</span></span> <span data-ttu-id="58186-153">以下程式碼會顯示應用程式資訊清單的內容。</span><span class="sxs-lookup"><span data-stu-id="58186-153">The code below shows the content of the application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-the-application"></a><span data-ttu-id="58186-154">發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="58186-154">Publishing the application</span></span>
<span data-ttu-id="58186-155">最後一個步驟是要使用以下 PowerShell 指令碼，將應用程式發佈至本機 Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="58186-155">The last step is to publish the application to the local Service Fabric cluster by using the PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="58186-156">將應用程式順利發佈至本機叢集之後，您便可以透過我們在 Node.js 應用程式的服務資訊清單中輸入的連接埠 (例如 http://localhost:3000) 存取 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58186-156">Once the application is successfully published to the local cluster, you can access the Node.js application on the port that we have entered in the service manifest of the Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="58186-157">在本教學課程中，您已看到如何輕鬆地將兩個現有應用程式封裝成一個 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58186-157">In this tutorial, you have seen how to easily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="58186-158">您也會了解如何將其部署到 Service Fabric，以便讓它能夠從一些 Service Fabric 功能 (例如高可用性和健康情況系統整合) 獲益。</span><span class="sxs-lookup"><span data-stu-id="58186-158">You have also learned how to deploy it to Service Fabric so that it can benefit from some of the Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-to-an-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="58186-159">在 Linux 上使用 Yeoman 將更多來賓可執行檔新增至現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="58186-159">Adding more guest executables to an existing application using Yeoman on Linux</span></span>

<span data-ttu-id="58186-160">若要將其他服務新增至已使用 `yo` 建立的應用程式，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="58186-160">To add another service to an application already created using `yo`, perform the following steps:</span></span> 
1. <span data-ttu-id="58186-161">將目錄變更為現有應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="58186-161">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="58186-162">例如，如果 `MyApplication` 是 Yeoman 所建立的應用程式，則為 `cd ~/YeomanSamples/MyApplication`。</span><span class="sxs-lookup"><span data-stu-id="58186-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="58186-163">執行 `yo azuresfguest:AddService` 並提供必要的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="58186-163">Run `yo azuresfguest:AddService` and provide the necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58186-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58186-164">Next steps</span></span>
* <span data-ttu-id="58186-165">了解如何使用 [Service Fabric 部署容器和容器概觀](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="58186-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="58186-166">封裝和部署來賓可執行檔的範例</span><span class="sxs-lookup"><span data-stu-id="58186-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="58186-167">兩個客體可執行檔 (C# 和 nodejs) 使用 REST 透過命名服務進行通訊的範例</span><span class="sxs-lookup"><span data-stu-id="58186-167">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
