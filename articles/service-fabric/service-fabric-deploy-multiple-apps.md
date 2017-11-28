---
title: "aaaDeploy Node.js 應用程式使用 MongoDB |Microsoft 文件"
description: "逐步解說如何 toopackage 多個客體可執行檔 toodeploy tooan Azure Service Fabric 叢集"
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
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="bc96c-103">部署多個來賓可執行檔</span><span class="sxs-lookup"><span data-stu-id="bc96c-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="bc96c-104">本文將說明如何 toopackage 及部署多個客體可執行檔 tooAzure Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="bc96c-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="bc96c-105">建置和部署單一的 Service Fabric 封裝閱讀如何太[部署客體可執行檔 tooService 網狀架構](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="bc96c-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="bc96c-106">雖然本逐步解說示範如何 toodeploy 的 Node.js 前端，會使用 MongoDB 作為 hello 資料存放區的應用程式，您可以套用 hello 步驟 tooany 應用程式具有另一個應用程式的相依性。</span><span class="sxs-lookup"><span data-stu-id="bc96c-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="bc96c-107">您可以使用 Visual Studio tooproduce hello 應用程式套件包含多個客體可執行檔。</span><span class="sxs-lookup"><span data-stu-id="bc96c-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="bc96c-108">請參閱[使用 Visual Studio toopackage 現有的應用程式](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="bc96c-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="bc96c-109">加入 hello 第一個客體可執行檔之後，以滑鼠右鍵按一下 hello 應用程式專案，並選取 hello**新增]-> [新的 Service Fabric 服務**tooadd hello 第二個客體可執行檔專案 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="bc96c-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="bc96c-110">注意： 如果您選擇 toolink hello Visual Studio 專案，建置 hello 的 Visual Studio 方案中的 hello 來源會確定您的應用程式封裝已啟動 toodate hello 來源中的變更。</span><span class="sxs-lookup"><span data-stu-id="bc96c-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="bc96c-111">範例</span><span class="sxs-lookup"><span data-stu-id="bc96c-111">Samples</span></span>
* [<span data-ttu-id="bc96c-112">封裝和部署來賓可執行檔的範例</span><span class="sxs-lookup"><span data-stu-id="bc96c-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="bc96c-113">兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例</span><span class="sxs-lookup"><span data-stu-id="bc96c-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="bc96c-114">手動封裝 hello 多個客體可執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="bc96c-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="bc96c-115">或者您可以手動將封裝 hello 客體可執行檔。</span><span class="sxs-lookup"><span data-stu-id="bc96c-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="bc96c-116">Hello 手動封裝，如本文使用 hello Service Fabric 封裝工具，它將會位於[http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool)。</span><span class="sxs-lookup"><span data-stu-id="bc96c-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="bc96c-117">封裝 hello Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc96c-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="bc96c-118">本文章假設 hello hello Service Fabric 叢集中節點上未安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="bc96c-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="bc96c-119">因此，您需要 tooadd Node.exe toohello 根目錄的應用程式節點，再封裝。</span><span class="sxs-lookup"><span data-stu-id="bc96c-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="bc96c-120">hello 目錄結構的 hello Node.js 應用程式 （使用快速 web 架構，而且 Jade 範本引擎） 下看起來應該類似 toohello 其中一個：</span><span class="sxs-lookup"><span data-stu-id="bc96c-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

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

<span data-ttu-id="bc96c-121">在下一個步驟中，您可以建立 hello Node.js 應用程式的應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="bc96c-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="bc96c-122">hello 的下列程式碼會建立包含 hello Node.js 應用程式的 Service Fabric 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="bc96c-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="bc96c-123">以下是正在使用的 hello 參數說明：</span><span class="sxs-lookup"><span data-stu-id="bc96c-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="bc96c-124">**來源/**點 toohello 目錄應封裝的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc96c-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="bc96c-125">**/target**定義 hello 目錄中的 hello 應該建立封裝。</span><span class="sxs-lookup"><span data-stu-id="bc96c-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="bc96c-126">此目錄已 toobe 不同於 hello 來源目錄。</span><span class="sxs-lookup"><span data-stu-id="bc96c-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="bc96c-127">**/appname**定義 hello hello 現有應用程式的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="bc96c-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="bc96c-128">它是重要 toounderstand，這會轉譯 toohello 服務名稱中的 hello 資訊，而不 toohello Service Fabric 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc96c-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="bc96c-129">**/exe**定義可執行服務的網狀架構在此情況下應該 toolaunch，hello `node.exe`。</span><span class="sxs-lookup"><span data-stu-id="bc96c-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="bc96c-130">**/ma**定義正在使用的 toolaunch hello 可執行檔的 hello 引數。</span><span class="sxs-lookup"><span data-stu-id="bc96c-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="bc96c-131">Service Fabric 因為未安裝 Node.js，需要執行 toolaunch hello Node.js web 伺服器`node.exe bin/www`。</span><span class="sxs-lookup"><span data-stu-id="bc96c-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="bc96c-132">`/ma:'bin/www'`會告知 hello 封裝工具 toouse`bin/ma`為 node.exe hello 引數。</span><span class="sxs-lookup"><span data-stu-id="bc96c-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="bc96c-133">**/ AppType**定義 hello Service Fabric 應用程式類型名稱。</span><span class="sxs-lookup"><span data-stu-id="bc96c-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="bc96c-134">如果您瀏覽 toohello hello /target 參數中指定的目錄，您可以看到該 hello 工具已建立功能完整的 Service Fabric 封裝，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bc96c-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

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
<span data-ttu-id="bc96c-135">hello 產生的 ServiceManifest.xml 現在有一個區段，描述如何啟動 hello Node.js web 伺服器，下列的 hello 程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="bc96c-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

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
<span data-ttu-id="bc96c-136">在此範例中，hello Node.js web 伺服器會接聽 tooport 3000，因此您需要 tooupdate hello 端點資訊，如下所示的 hello ServiceManifest.xml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="bc96c-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="bc96c-137">封裝 hello MongoDB 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc96c-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="bc96c-138">既然您已在 hello Node.js 應用程式封裝，您可以繼續，並封裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="bc96c-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="bc96c-139">如前所述，您現在瀏覽的 hello 步驟都不是特定 tooNode.js 且 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="bc96c-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="bc96c-140">事實上，它們會套用 tooall 應用程式預定 toobe 當作一個 Service Fabric 應用程式一起封裝。</span><span class="sxs-lookup"><span data-stu-id="bc96c-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="bc96c-141">toopackage MongoDB，想要確定您封裝 Mongod.exe 和 Mongo.exe toomake。</span><span class="sxs-lookup"><span data-stu-id="bc96c-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="bc96c-142">這兩個二進位檔位於 hello `bin` MongoDB 安裝目錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="bc96c-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="bc96c-143">hello 目錄結構看起來類似 toohello 一個下方。</span><span class="sxs-lookup"><span data-stu-id="bc96c-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="bc96c-144">Service Fabric 需要使用其中一個命令類似 toohello toostart MongoDB，因此您需要 toouse hello`/ma`參數封裝 MongoDB 時。</span><span class="sxs-lookup"><span data-stu-id="bc96c-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="bc96c-145">不會被 hello 資料保留在 hello 的節點失敗的情況下，如果 hello MongoDB 資料目錄置於 hello 的 hello 節點的本機目錄。</span><span class="sxs-lookup"><span data-stu-id="bc96c-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="bc96c-146">您應該使用永久性儲存裝置，或是實作 MongoDB 複本集順序 tooprevent 資料遺失。</span><span class="sxs-lookup"><span data-stu-id="bc96c-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="bc96c-147">在 PowerShell 或 hello 命令殼層中我們要執行 hello 封裝工具以 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="bc96c-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="bc96c-148">順序 tooadd MongoDB tooyour Service Fabric 應用程式封裝中，您必須確定該 hello /target 參數指向 toohello toomake 已經包含 hello 以及 hello Node.js 應用程式的應用程式資訊清單的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="bc96c-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="bc96c-149">您也需要確定您使用 toomake hello ApplicationType 名稱相同。</span><span class="sxs-lookup"><span data-stu-id="bc96c-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="bc96c-150">讓我們來瀏覽 toohello 目錄，並檢查哪些 hello 工具已建立。</span><span class="sxs-lookup"><span data-stu-id="bc96c-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

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
<span data-ttu-id="bc96c-151">如您所見，hello 工具就會加入新的資料夾，MongoDB，toohello 目錄包含 hello MongoDB 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="bc96c-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="bc96c-152">如果您開啟 hello`ApplicationManifest.xml`檔案中，您可以看到該 hello 封裝現在包含 hello Node.js 應用程式和 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="bc96c-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="bc96c-153">下列程式碼 hello 顯示 hello hello 應用程式資訊清單的內容。</span><span class="sxs-lookup"><span data-stu-id="bc96c-153">hello code below shows hello content of hello application manifest.</span></span>

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

### <a name="publishing-hello-application"></a><span data-ttu-id="bc96c-154">發行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc96c-154">Publishing hello application</span></span>
<span data-ttu-id="bc96c-155">hello 最後一個步驟是使用下列的 hello PowerShell 指令碼 toopublish hello 應用程式 toohello 本機 Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="bc96c-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="bc96c-156">一旦 hello 應用程式已成功發行的 toohello 本機叢集，您可以存取 hello Node.js 應用程式，我們輸入 hello Node.js 應用程式--例如 http://localhost:3000 hello 服務資訊清單中的 hello 連接埠上。</span><span class="sxs-lookup"><span data-stu-id="bc96c-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="bc96c-157">在本教學課程中，您已經知道如何 tooeasily 封裝成一個 Service Fabric 應用程式的兩個現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc96c-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="bc96c-158">您也學到如何 toodeploy 它 tooService 網狀架構，讓它可以受益於某些 hello Service Fabric 功能，例如高可用性和健全狀況的系統整合。</span><span class="sxs-lookup"><span data-stu-id="bc96c-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="bc96c-159">新增更多客體可執行檔 tooan 現有應用程式使用 Yeoman on Linux</span><span class="sxs-lookup"><span data-stu-id="bc96c-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="bc96c-160">tooadd 另一個 tooan 建立服務應用程式已經使用`yo`，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc96c-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="bc96c-161">變更 hello 現有應用程式的根目錄 toohello。</span><span class="sxs-lookup"><span data-stu-id="bc96c-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="bc96c-162">例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc96c-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="bc96c-163">執行`yo azuresfguest:AddService`並提供 hello 必要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bc96c-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc96c-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc96c-164">Next steps</span></span>
* <span data-ttu-id="bc96c-165">了解如何使用 [Service Fabric 部署容器和容器概觀](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bc96c-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="bc96c-166">封裝和部署來賓可執行檔的範例</span><span class="sxs-lookup"><span data-stu-id="bc96c-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="bc96c-167">兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例</span><span class="sxs-lookup"><span data-stu-id="bc96c-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
