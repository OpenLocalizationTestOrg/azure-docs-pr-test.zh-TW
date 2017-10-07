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
# <a name="deploy-multiple-guest-executables"></a>部署多個來賓可執行檔
本文將說明如何 toopackage 及部署多個客體可執行檔 tooAzure Service Fabric。 建置和部署單一的 Service Fabric 封裝閱讀如何太[部署客體可執行檔 tooService 網狀架構](service-fabric-deploy-existing-app.md)。

雖然本逐步解說示範如何 toodeploy 的 Node.js 前端，會使用 MongoDB 作為 hello 資料存放區的應用程式，您可以套用 hello 步驟 tooany 應用程式具有另一個應用程式的相依性。   

您可以使用 Visual Studio tooproduce hello 應用程式套件包含多個客體可執行檔。 請參閱[使用 Visual Studio toopackage 現有的應用程式](service-fabric-deploy-existing-app.md)。 加入 hello 第一個客體可執行檔之後，以滑鼠右鍵按一下 hello 應用程式專案，並選取 hello**新增]-> [新的 Service Fabric 服務**tooadd hello 第二個客體可執行檔專案 toohello 方案。 注意： 如果您選擇 toolink hello Visual Studio 專案，建置 hello 的 Visual Studio 方案中的 hello 來源會確定您的應用程式封裝已啟動 toodate hello 來源中的變更。 

## <a name="samples"></a>範例
* [封裝和部署來賓可執行檔的範例](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>手動封裝 hello 多個客體可執行的應用程式
或者您可以手動將封裝 hello 客體可執行檔。 Hello 手動封裝，如本文使用 hello Service Fabric 封裝工具，它將會位於[http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool)。

### <a name="packaging-hello-nodejs-application"></a>封裝 hello Node.js 應用程式
本文章假設 hello hello Service Fabric 叢集中節點上未安裝 Node.js。 因此，您需要 tooadd Node.exe toohello 根目錄的應用程式節點，再封裝。 hello 目錄結構的 hello Node.js 應用程式 （使用快速 web 架構，而且 Jade 範本引擎） 下看起來應該類似 toohello 其中一個：

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

在下一個步驟中，您可以建立 hello Node.js 應用程式的應用程式套件。 hello 的下列程式碼會建立包含 hello Node.js 應用程式的 Service Fabric 應用程式封裝。

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

以下是正在使用的 hello 參數說明：

* **來源/**點 toohello 目錄應封裝的 hello 應用程式。
* **/target**定義 hello 目錄中的 hello 應該建立封裝。 此目錄已 toobe 不同於 hello 來源目錄。
* **/appname**定義 hello hello 現有應用程式的應用程式名稱。 它是重要 toounderstand，這會轉譯 toohello 服務名稱中的 hello 資訊，而不 toohello Service Fabric 應用程式的名稱。
* **/exe**定義可執行服務的網狀架構在此情況下應該 toolaunch，hello `node.exe`。
* **/ma**定義正在使用的 toolaunch hello 可執行檔的 hello 引數。 Service Fabric 因為未安裝 Node.js，需要執行 toolaunch hello Node.js web 伺服器`node.exe bin/www`。  `/ma:'bin/www'`會告知 hello 封裝工具 toouse`bin/ma`為 node.exe hello 引數。
* **/ AppType**定義 hello Service Fabric 應用程式類型名稱。

如果您瀏覽 toohello hello /target 參數中指定的目錄，您可以看到該 hello 工具已建立功能完整的 Service Fabric 封裝，如下所示：

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
hello 產生的 ServiceManifest.xml 現在有一個區段，描述如何啟動 hello Node.js web 伺服器，下列的 hello 程式碼片段所示：

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
在此範例中，hello Node.js web 伺服器會接聽 tooport 3000，因此您需要 tooupdate hello 端點資訊，如下所示的 hello ServiceManifest.xml 檔案中。   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>封裝 hello MongoDB 應用程式
既然您已在 hello Node.js 應用程式封裝，您可以繼續，並封裝 MongoDB。 如前所述，您現在瀏覽的 hello 步驟都不是特定 tooNode.js 且 MongoDB。 事實上，它們會套用 tooall 應用程式預定 toobe 當作一個 Service Fabric 應用程式一起封裝。  

toopackage MongoDB，想要確定您封裝 Mongod.exe 和 Mongo.exe toomake。 這兩個二進位檔位於 hello `bin` MongoDB 安裝目錄的目錄。 hello 目錄結構看起來類似 toohello 一個下方。

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric 需要使用其中一個命令類似 toohello toostart MongoDB，因此您需要 toouse hello`/ma`參數封裝 MongoDB 時。

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> 不會被 hello 資料保留在 hello 的節點失敗的情況下，如果 hello MongoDB 資料目錄置於 hello 的 hello 節點的本機目錄。 您應該使用永久性儲存裝置，或是實作 MongoDB 複本集順序 tooprevent 資料遺失。  
>
>

在 PowerShell 或 hello 命令殼層中我們要執行 hello 封裝工具以 hello 下列參數：

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

順序 tooadd MongoDB tooyour Service Fabric 應用程式封裝中，您必須確定該 hello /target 參數指向 toohello toomake 已經包含 hello 以及 hello Node.js 應用程式的應用程式資訊清單的相同目錄。 您也需要確定您使用 toomake hello ApplicationType 名稱相同。

讓我們來瀏覽 toohello 目錄，並檢查哪些 hello 工具已建立。

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
如您所見，hello 工具就會加入新的資料夾，MongoDB，toohello 目錄包含 hello MongoDB 二進位檔。 如果您開啟 hello`ApplicationManifest.xml`檔案中，您可以看到該 hello 封裝現在包含 hello Node.js 應用程式和 MongoDB。 下列程式碼 hello 顯示 hello hello 應用程式資訊清單的內容。

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

### <a name="publishing-hello-application"></a>發行 hello 應用程式
hello 最後一個步驟是使用下列的 hello PowerShell 指令碼 toopublish hello 應用程式 toohello 本機 Service Fabric 叢集：

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

一旦 hello 應用程式已成功發行的 toohello 本機叢集，您可以存取 hello Node.js 應用程式，我們輸入 hello Node.js 應用程式--例如 http://localhost:3000 hello 服務資訊清單中的 hello 連接埠上。

在本教學課程中，您已經知道如何 tooeasily 封裝成一個 Service Fabric 應用程式的兩個現有的應用程式。 您也學到如何 toodeploy 它 tooService 網狀架構，讓它可以受益於某些 hello Service Fabric 功能，例如高可用性和健全狀況的系統整合。


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>新增更多客體可執行檔 tooan 現有應用程式使用 Yeoman on Linux

tooadd 另一個 tooan 建立服務應用程式已經使用`yo`，執行下列步驟的 hello: 
1. 變更 hello 現有應用程式的根目錄 toohello。  例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。
2. 執行`yo azuresfguest:AddService`並提供 hello 必要詳細資料。

## <a name="next-steps"></a>後續步驟
* 了解如何使用 [Service Fabric 部署容器和容器概觀](service-fabric-containers-overview.md)
* [封裝和部署來賓可執行檔的範例](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
