---
title: "現有的可執行檔 tooAzure Service Fabric aaaDeploy |Microsoft 文件"
description: "逐步解說如何 toopackage 客體可執行檔，讓它可以是現有的應用程式部署 tooa Service Fabric 叢集"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>部署客體可執行檔 tooService 網狀架構
您可以在 Azure Service Fabric 中將任何類型的程式碼 (例如 Node.js、Java 或 C++) 當作服務來執行。 Service Fabric 是指 toothese 類型的服務，做為客體可執行檔。

Service Fabric 將來賓可執行檔視為無狀態服務。 因此會根據可用性和其他度量將它們放在叢集的節點上。 本文說明如何 toopackage 和客體可執行檔 tooa Service Fabric 叢集，部署使用 Visual Studio 或命令列公用程式。

在本文中，我們會涵蓋 hello 步驟 toopackage 客體可執行檔，並將其部署 tooService 網狀架構。  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>在 Service Fabric 中執行來賓可執行檔的優點
有數個優點 toorunning 客體可執行檔中的 Service Fabric 叢集：

* 高可用性。 在 Service Fabric 中執行的應用程式都會具有高可用性。 Service Fabric 會確保應用程式執行個體正在執行。
* 健康狀況監視。 Service Fabric 健全狀況監控會偵測應用程式是否正在執行，如果發生失敗情況，則會提供診斷資訊。   
* 應用程式生命週期管理。 除了提供沒有停機的升級，Service Fabric 會提供自動回復 toohello 先前的版本，如果沒有在升級期間所報告的錯誤健全狀況事件。    
* 密度。 您可以在叢集中，這麼做可免除在自己的硬體上的每個應用程式 toorun hello 需要執行多個應用程式。
* 探索： 使用 REST 可以呼叫 hello Service Fabric 命名服務 toofind 其他服務 hello 叢集中。 

## <a name="samples"></a>範例
* [封裝和部署來賓可執行檔的範例](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>應用程式和服務資訊清單檔案的概觀
部署客體可執行檔的一部分，它是有用的 toounderstand hello Service Fabric 封裝和部署模型中所述[應用程式模型](service-fabric-application-model.md)。 hello Service Fabric 封裝模型依賴兩個 XML 檔案： hello 應用程式和服務資訊清單。 hello 結構描述定義的 hello ApplicationManifest.xml 和 ServiceManifest.xml 檔案會隨 hello 到 Service Fabric SDK *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **應用程式資訊清單**hello 應用程式資訊清單是使用的 toodescribe hello 應用程式。 它會列出 hello 服務組成和使用方式的一或多個服務應部署，例如 hello 執行個體數目的 toodefine 其他參數。

  在 Service Fabric 中，應用程式是部署和升級的單位。 應用程式可以當作單一單位來升級，而得以掌控可能的失敗和可能需要的回復。 Service Fabric 可以確保 hello 升級程序將會是成功，或如果 hello 升級失敗，並不會讓 hello 應用程式處於不明或不穩定的狀態。
* **服務資訊清單**hello 服務資訊清單會描述服務的 hello 元件。 它包含資料，例如 hello 名稱和服務類型，其程式碼和組態。 hello 服務資訊清單也包含一些額外的參數可能是一旦部署之後使用 tooconfigure hello 服務。

## <a name="application-package-file-structure"></a>應用程式套件檔案結構
toodeploy 應用程式 tooService 網狀架構，hello 應用程式應依照預先定義的目錄結構。 hello 以下是該結構的範例。

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

hello ApplicationPackageRoot 包含定義 hello 應用程式的 hello ApplicationManifest.xml 檔案。 Hello 應用程式中包含每一個服務子目錄是使用的 toocontain 所有 hello hello 服務所需的成品。 這些子目錄的 hello ServiceManifest.xml 和，一般而言，下列的 hello:

* *Code*。 此目錄包含 hello 服務程式碼。
* *Config*。此目錄包含 Settings.xml 檔案 （和其他檔案，如有必要） hello 服務可以存取在執行階段 tooretrieve 特定的組態設定。
* *Data*。 這是其他目錄 toostore 其他本機資料可能需要 hello 服務。 資料應該是使用的 toostore 只是暫時的資料。 Service Fabric 會複製或 replicate 變更 toohello 資料目錄，如果 hello 服務需要 toobe 重新配置 （例如，在容錯移轉期間）。

> [!NOTE]
> 您不需要 toocreate hello`config`和`data`目錄，如果您不需要它們。
>
>

## <a name="package-an-existing-executable"></a>封裝現有的執行檔
當封裝客體可執行檔，您可以選擇任一 toouse Visual Studio 專案範本或太[手動建立 hello 應用程式封裝](#manually)。 使用 Visual Studio，hello 應用程式封裝的結構，並為您建立資訊清單檔案的 hello 新的專案範本。

> [!TIP]
> 最簡單方式 toopackage hello 現有的 Windows 服務可執行檔是 toouse Visual Studio 在 Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>使用 Visual Studio toopackage 及部署現有的可執行檔
Visual Studio 提供 Service Fabric 服務範本 toohelp 部署客體可執行檔 tooa Service Fabric 叢集。

1. 選擇 [檔案]  >  [新增專案]，然後建立 Service Fabric 應用程式。
2. 選擇**客體可執行檔**作為 hello 服務範本。
3. 按一下**瀏覽**tooselect hello 資料夾與您的可執行檔中的 hello 參數 toocreate hello 服務的 hello 其餘部分填滿。
   * 「Code Package Behavior」。 可以是集合 toocopy 您資料夾 toohello Visual Studio 專案中，所有 hello 內容會很有用，如果 hello 可執行檔不會變更。 如果您預期 hello 可執行檔 toochange，且想 hello 能力 toopick 新組建上的以動態方式，您可以改為選擇 toolink toohello 資料夾。 在 Visual Studio 中建立 hello 應用程式專案時，您可以使用連結的資料夾。 這會連結 toohello 來源位置，從在 hello 專案中，讓您 tooupdate hello 客體可執行檔在其來源的目的地。 這些更新會成為 hello 上建置的應用程式套件的一部分。
   * *程式*指定應執行 toostart hello 服務的 hello 可執行檔。
   * *引數*指定 hello 傳遞引數應該 toohello 可執行檔。 這可以是具有引數的參數清單。
   * *WorkingFolder*指定 hello 即將啟動 toobe hello 程序的工作目錄。 您可以指定三個值：
     * `CodeBase`指定該 hello 工作目錄即將 toobe hello 應用程式封裝中設定 toohello 程式碼目錄 (`Code` hello 前面檔案結構中顯示的目錄)。
     * `CodePackage`指定該 hello 工作目錄即將 toobe 設定 toohello 根 hello 應用程式封裝 (`GuestService1Pkg` hello 前面檔案結構所示)。
     * `Work`指定 hello 檔案會放置於稱為工作的子目錄。
4. 指定服務的名稱，然後按一下 [確定]。
5. 如果您的服務端點需要通訊，您現在可以新增 hello 通訊協定、 連接埠和型別 toohello ServiceManifest.xml 檔案。 例如： `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`。
6. 您現在可以使用 hello 封裝，並對本機叢集發行動作的偵錯 Visual Studio 中的 hello 方案。 準備就緒時，您可以發行 hello 應用程式 tooa 遠端叢集，或檢查 hello 方案 toosource 控制項中。
7. 如何移 toohello 結尾此發行項 toosee tooview Service Fabric 總管中執行您客體可執行服務。

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>使用 Yoeman toopackage 及部署 Linux 上的現有可執行檔

用於建立及部署可在 Linux 上執行客體 hello 程序是 hello 與部署 csharp 或 java 應用程式相同。

1. 在終端機中，輸入 `yo azuresfguest`。
2. 為您的應用程式命名。
3. 命名您的服務，並提供包括 hello 可執行檔的路徑和 hello 參數必須以叫用的 hello 詳細資料。

Yeoman 與 hello 適當的應用程式建立應用程式套件和資訊清單檔案，以及安裝和解除安裝指令碼。

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>手動封裝和部署現有執行檔
hello 程序手動封裝客體可執行檔為基礎 hello 下列一般步驟：

1. 建立 hello 封裝目錄結構。
2. 新增 hello 應用程式的程式碼和組態檔。
3. 編輯 hello 服務資訊清單檔。
4. 編輯 hello 應用程式資訊清單檔案。

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>建立 hello 封裝目錄結構
您可以在 hello 前面一節中所述建立 hello 目錄結構，啟動 「 應用程式套件檔案結構。 」

### <a name="add-hello-applications-code-and-configuration-files"></a>新增 hello 應用程式的程式碼和組態檔
建立 hello 目錄結構之後，您可以加入 hello 程式碼和組態目錄下的 hello 應用程式的程式碼和組態檔案。 您也可以建立其他目錄或 hello 程式碼或設定目錄下的子目錄。

Service Fabric 沒有`xcopy`的 hello hello 應用程式根目錄，因此沒有任何的預先定義的結構 toouse 以外建立兩個最上層目錄、 程式碼和設定的內容。 (您可以選擇不同的名稱。 更多詳細資料位於 hello 下一節。）

> [!NOTE]
> 請確定您包含所有 hello 檔案和 hello 應用程式所需的相依性。 Service Fabric hello 應用程式服務的部署進行 toobe hello 叢集中複製 hello hello 應用程式套件的所有節點上的內容。 hello 套件應該包含所有 hello 應用程式需要 toorun hello 程式碼。 請勿假設已安裝的 hello 相依性。
>
>

### <a name="edit-hello-service-manifest-file"></a>編輯 hello 服務資訊清單檔
hello 下一個步驟是 tooedit hello 服務資訊清單檔案 tooinclude hello 下列資訊：

* hello hello 服務型別名稱。 這是 Service Fabric 使用 tooidentify 服務識別碼。
* hello 命令 toouse toolaunch hello 應用程式 (ExeHost)。
* 需要執行 toobe tooset hello 應用程式 (SetupEntrypoint) 的任何指令碼。

hello 的範例如下的`ServiceManifest.xml`檔案：

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

下列各節的 hello 介紹 hello 您需要 tooupdate 的 hello 檔案的不同部分。

#### <a name="update-servicetypes"></a>更新 ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* 您可以挑選任何您要用於 `ServiceTypeName` 的名稱。 hello 值是否會在 hello`ApplicationManifest.xml`檔案 tooidentify hello 服務。
* 指定 `UseImplicitHost="true"`。 這個屬性會告知 Service Fabric hello 服務為基礎的獨立應用程式，因此所有的 Service Fabric 需要 toodo 是 toolaunch 它做為處理序並監視其健康情況。

#### <a name="update-codepackage"></a>更新 CodePackage
hello CodePackage 元素會指定 hello 服務的程式碼 hello 位置 （和版本）。

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

hello`Name`項目是使用的 toospecify hello hello 包含 hello 服務的程式碼的應用程式封裝中的 hello 目錄名稱。 `CodePackage`也有 hello`version`屬性。 這可以是使用的 toospecify hello 版本 hello 程式碼，而且可以也可能會利用 Service Fabric 中的 hello 應用程式生命週期管理基礎結構使用 tooupgrade hello 服務的程式碼。

#### <a name="optional-update-setupentrypoint"></a>選擇性︰更新 SetupEntrypoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
hello SetupEntryPoint 項目是使用的 toospecify hello 服務的程式碼啟動前應該執行的任何可執行檔或批次檔案。 是選擇性步驟中，因此不需要 toobe 包含如果有任何需要的初始化。 hello SetupEntryPoint 執行每次 hello 服務重新啟動。

沒有一個 SetupEntryPoint，因此安裝程式指令碼需要 toobe 分組在單一批次檔中，如果 hello 應用程式的安裝程式需要多個指令碼。 hello SetupEntryPoint 能夠執行任何類型的檔案： 可執行檔、 批次檔，以及 PowerShell 指令程式。 如需詳細資訊，請參閱[設定 SetupEntryPoint](service-fabric-application-runas-security.md)。

在上述範例中的 hello，hello SetupEntryPoint 執行批次檔呼叫`LaunchConfig.cmd`也就是位於的 hello `scripts` hello （假設 hello WorkingFolder 元素設定 tooCodeBase） 的程式碼目錄的子目錄。

#### <a name="update-entrypoint"></a>更新 EntryPoint
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

hello `EntryPoint` hello 服務資訊清單檔中的項目，則使用的 toospecify 如何 toolaunch hello 服務。 hello`ExeHost`項目會指定可執行檔的 hello （和引數），應該使用 toolaunch hello 服務。

* `Program`指定 hello 應該啟動 hello 服務的 hello 可執行檔名稱。
* `Arguments`指定應該傳遞 toohello 可執行檔的 hello 引數。 這可以是具有引數的參數清單。
* `WorkingFolder`指定即將啟動 toobe hello 處理序的 hello 工作目錄。 您可以指定三個值：
  * `CodeBase`指定該 hello 工作目錄即將 toobe hello 應用程式封裝中設定 toohello 程式碼目錄 (`Code`目錄 hello 前面檔案結構中)。
  * `CodePackage`指定該 hello 工作目錄即將 toobe 設定 toohello 根 hello 應用程式封裝 (`GuestService1Pkg` hello 前面檔案結構中)。
    * `Work`指定 hello 檔案會放置於稱為工作的子目錄。

hello WorkingFolder 是有用的 tooset hello 正確的工作目錄，以便可以使用相對路徑，由任一 hello 應用程式或初始化指令碼。

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>更新端點，並向命名服務註冊以進行通訊
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
在上述範例中的 hello，hello`Endpoint`項目會指定 hello hello 應用程式可以接聽的端點。 在此範例中，hello Node.js 應用程式會接聽連接埠 3000 的 http。

此外您可以要求 Service Fabric toopublish 這個端點 toohello 命名服務讓其他服務可以探索 hello 端點位址 toothis 服務。 這可讓您 toobe 無法 toocommunicate 客體可執行檔的服務之間。
hello 已發行的端點位址是 hello 表單的`UriScheme://IPAddressOrFQDN:Port/PathSuffix`。 `UriScheme` 和 `PathSuffix` 是選擇性的屬性。 `IPAddressOrFQDN`是 hello IP 位址或完整的網域名稱的 hello 節點取得置於這個可執行檔，而且它會針對您計算。

在 hello 下列範例中，一次 hello 服務部署，請在 Service Fabric 總管您會看到類似端點太`http://10.1.4.92:3000/myapp/`發行 hello 服務執行個體。 或者，如果這是本機電腦，則您會看到 `http://localhost:3000/myapp/`。

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
您可以使用這些位址與[反向 proxy](service-fabric-reverseproxy.md) toocommunicate 服務之間。

### <a name="edit-hello-application-manifest-file"></a>編輯 hello 應用程式資訊清單檔
一旦設定 hello`Servicemanifest.xml`檔案中，您需要某些變更 toohello toomake`ApplicationManifest.xml`檔案 hello 的 tooensure 正確使用的服務類型和名稱。

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
在 hello`ServiceManifestImport`項目，您可以指定您想 tooinclude hello 應用程式中的一或多個服務。 服務使用參考`ServiceManifestName`，以指定 hello hello 目錄名稱，其中 hello`ServiceManifest.xml`檔所在。

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>設定記錄
針對客體可執行檔，如果就會很有用的 toobe 無法 toosee 主控台記錄檔 toofind 出 hello 應用程式和組態指令碼會顯示任何錯誤。
主控台重新導向可以設定在 hello`ServiceManifest.xml`檔案使用 hello`ConsoleRedirection`項目。

> [!WARNING]
> 絕對不要使用的應用程式，因為這可能會影響 hello 應用程式容錯移轉，在生產環境中部署的 hello 主控台重新導向原則。 僅將此原則用於本機開發及偵錯。  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`可以使用的 tooredirect 主控台輸出 （stdout 與 stderr） tooa 工作目錄。 這會提供 hello 能力 tooverify hello 安裝程式或 hello hello Service Fabric 叢集中的應用程式執行期間沒有任何錯誤。

`FileRetentionCount`決定多少檔案會儲存在 hello 工作目錄。 值為 5，比方說，表示 hello hello 先前五個執行的記錄檔會儲存在 hello 工作目錄。

`FileMaxSizeInKb`指定 hello hello 記錄檔的大小上限。

記錄檔會儲存在其中一個 hello 服務的工作目錄。 toodetermine hello 檔案位於何處，使用 Service Fabric 總管 toodetermine 哪一種節點 hello 服務正在執行，且正在使用的工作目錄。 本文稍後會說明此程序。

## <a name="deployment"></a>部署
最後一個步驟中 hello 太[部署您的應用程式](service-fabric-deploy-remove-applications.md)。 hello 下列 PowerShell 指令碼顯示如何 toodeploy 您的應用程式 toohello 本機開發叢集，並啟動新的 Service Fabric 服務。

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區，如果 hello 套件很大，或具有許多檔案之前。 請在[這裡](service-fabric-deploy-remove-applications.md#upload-the-application-package)閱讀更多資訊。
>

Service Fabric 服務可以各種「組態」部署。 例如，它可以部署為單一或多個執行個體，或它可以部署的方式會有一個 hello hello Service Fabric 叢集的每個節點上的服務執行個體。

hello `InstanceCount` hello 參數`New-ServiceFabricService`指令程式是使用的 toospecify 多少個 hello 服務執行個體應該啟動 hello Service Fabric 叢集中。 您可以設定 hello`InstanceCount`值，視您要部署的應用程式的 hello 類型而定。 hello 兩個最常見情況包括：

* `InstanceCount = "1"`。 在此情況下，只有一個 hello 服務執行個體被部署在 hello 叢集中。 Service Fabric 排程器會決定哪一種節點 hello 服務即將 toobe 上部署。
* `InstanceCount ="-1"`。 在此情況下，一個 hello 服務執行個體部署的 hello Service Fabric 叢集中的每個節點。 hello 結果 hello 叢集中有一個 （且只有一個） 的每個節點的 hello 服務的執行個體。

這是前端應用程式 （例如，REST 端點），如有用的組態，因為用戶端應用程式需要太 「 連接 」 tooany hello 叢集 toouse hello 端點中的 hello 節點。 這項設定也可用時，例如 hello Service Fabric 叢集的所有節點連線的 tooa 負載平衡器。 用戶端流量然後分散 hello 服務 hello 叢集中所有節點上執行。

## <a name="check-your-running-application"></a>來查執行中的應用程式
在 Service Fabric 總管，識別 hello hello 服務執行所在的節點。 在此範例中，它是在 Node1 上執行：

![服務執行所在的節點](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

如果您瀏覽 toohello 節點，並瀏覽 toohello 應用程式，您會看到 hello 不可或缺的節點資訊，包括其磁碟上的位置。

![在磁碟上的位置](./media/service-fabric-deploy-existing-app/locationondisk2.png)

如果使用伺服器總管瀏覽 toohello 目錄，您可以找到 hello 工作目錄和 hello 服務記錄檔資料夾中 hello 下列螢幕擷取畫面所示： 

![記錄檔的位置](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>後續步驟
在本文中，您已經學會如何 toopackage 客體可執行檔並將其部署 tooService 網狀架構。 請參閱下列文章中的相關的資訊和工作的 hello。

* [範例封裝和部署客體可執行檔](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)，包括連結 toohello 發行前版本的 hello 封裝工具
* [兩個客體可執行檔 （C# 和 nodejs） 通訊透過 hello 命名服務使用 REST 範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [部署多個來賓可執行檔](service-fabric-deploy-multiple-apps.md)
* [使用 Visual Studio 建立第一個 Service Fabric 應用程式](service-fabric-create-your-first-application-in-visual-studio.md)
