---
title: "aaaAzure Service Fabric 應用程式部署 |Microsoft 文件"
description: "如何使用 PowerShell 的 Service Fabric toodeploy 及移除應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>使用 PowerShell 部署與移除應用程式
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

[封裝應用程式類型][10]後，即可將它部署至 Azure Service Fabric 叢集中。 部署包含下列三個步驟的 hello:

1. 上傳 hello 應用程式封裝 toohello 映像存放區
2. 註冊 hello 應用程式類型
3. 建立 hello 應用程式執行個體

部署應用程式的執行個體正在執行中 hello 叢集後，您可以刪除 hello 應用程式執行個體和其應用程式類型。 toocompletely 移除從 hello 叢集中的應用程式牽涉到 hello 下列步驟：

1. 移除 （或刪除） 執行應用程式執行個體的 hello
2. 如果您不再需要取消註冊 hello 應用程式類型
3. 移除 hello 映像存放區中的 hello 應用程式套件

如果您使用[用於部署和偵錯應用程式的 Visual Studio](service-fabric-publish-app-remote-cluster.md)在本機開發叢集上，所有 hello 前面的步驟都是透過 PowerShell 指令碼會自動處理。  此指令碼位於 hello*指令碼*hello 應用程式專案的資料夾。 這篇文章提供背景資訊，讓您可以執行，該指令碼內容正在進行 hello Visual Studio 之外，相同的作業。 
 
## <a name="connect-toohello-cluster"></a>Toohello 叢集連線
在本文中執行任何 PowerShell 命令之前，一律使用啟動[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric 叢集。 tooconnect toohello 本機開發叢集，請執行下列 hello:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

如需範例連接 tooa 遠端叢集或叢集使用 Azure Active Directory，X509 保護的憑證或 Windows Active Directory，請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md)。

## <a name="upload-hello-application-package"></a>上傳 hello 應用程式套件
正在上傳的 hello 應用程式封裝會將它放在內部的 Service Fabric 元件所存取的位置。
如果您想 tooverify hello 應用程式封裝在本機，使用 hello[測試 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet。

hello[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)命令上傳 hello 應用程式封裝 toohello 叢集映像存放區。
hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet，這是 hello Service Fabric SDK PowerShell 模組的一部分，是使用的 tooget hello 映像儲存連接字串。  tooimport hello SDK 模組，執行：

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

假設您在 Visual Studio 2015 中建置並封裝名為 *MyApplication* 的應用程式。 根據預設，hello hello ApplicationManifest.xml 中列出的應用程式類型名稱是"MyApplicationType"。  hello 應用程式封裝，其中包含 hello 必要的應用程式資訊清單、 服務資訊清單，以及程式碼/config/資料的封裝，位於*C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*。 

hello 下列命令會列出 hello hello 應用程式封裝內容：

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

如果 hello 應用程式套件很大且/或有許多檔案，您可以[壓縮](service-fabric-package-apps.md#compress-a-package)。 hello 壓縮會減少 hello 大小和檔案的 hello 數目。
hello 副作用就是該註冊和取消註冊 hello 應用程式類型為更快。 上傳時間可能較慢目前，特別是當您包含 hello 階段 toocompress hello 封裝。 

toocompress 封裝時，使用 hello 相同[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)命令。 壓縮可以個別從完成上傳、 使用 hello`SkipCopy`旗標，或與 hello 一起上傳作業。 在壓縮封裝上套用壓縮為無作業。
toouncompress 壓縮封裝，使用 hello 相同[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)命令與 hello`UncompressPackage`切換。

hello 下列指令程式會壓縮 hello 封裝但不複製該項 toohello 映像存放區。 hello 封裝現在包含 hello 的 zip 的檔案`Code`和`Config`封裝。 不壓縮 hello 應用程式和 hello 服務資訊清單，因為它們所需的許多內部的作業 （例如共用、 應用程式類型名稱和版本擷取針對特定的驗證封裝）。 壓縮 hello 資訊清單會使這些操作效率不佳。

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

針對大型應用程式封裝，hello 壓縮會使用時間。 為了獲得最佳結果，請使用快速的 SSD 磁碟機。 hello 壓縮時間和 hello hello 壓縮封裝大小也有所不同 hello 套件內容。
例如，以下是某些封裝，以顯示 hello 初始和 hello 與 hello 壓縮時間的壓縮的套件大小的壓縮統計資料。

|初始大小 (MB)|檔案計數|壓縮時間|壓縮的封裝大小 (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

一旦封裝壓縮檔，它可以上傳的 tooone 或視需要的多個 Service Fabric 叢集。 hello 部署機制是相同的壓縮和未壓縮的封裝。 如果 hello 封裝已壓縮，因此儲存 hello 叢集映像存放區中，而且執行 hello 應用程式之前，hello 節點上進行壓縮。


hello 下列範例會上傳 hello 封裝 toohello 映像存放區，名為"MyApplicationV1 」 的資料夾：

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet，這是 hello Service Fabric SDK PowerShell 模組的一部分，是使用的 tooget hello 映像儲存連接字串。  tooimport hello SDK 模組，執行：

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

如果您未指定 hello *-ApplicationPackagePathInImageStore*參數，hello 應用程式套件複製到 hello"Debug"資料夾中 hello 映像存放區中。

hello 花的時間 tooupload 封裝多個因素而有所不同。 這些因素有些 hello 中 hello 封裝、 hello 封裝大小，以及 hello 檔案大小的檔案數目。 hello hello 來源電腦與 hello Service Fabric 叢集之間的網路速度也會影響 hello 上傳時間。 hello 預設逾時[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)為 30 分鐘。
視 hello 所述的因素，您可能必須 tooincrease hello 逾時。 如果您壓縮 hello hello 複製呼叫中的封裝，您需要 tooalso 考慮 hello 壓縮時間。

請參閱[hello 映像存放區連接字串了解](service-fabric-image-store-connection-string.md)如需關於 hello 映像存放區，以及映像存放區連接字串的補充資訊。

## <a name="register-hello-application-package"></a>註冊 hello 應用程式套件
hello 應用程式類型和版本 hello 註冊 hello 應用程式封裝時變成可供使用的應用程式資訊清單中宣告。 hello 系統讀取 hello 封裝上傳 hello 上一個步驟中，會驗證 hello 封裝、 處理 hello 套件內容，以及複製 hello 處理封裝 tooan 內部系統位置。  

執行 hello[暫存器 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello hello 叢集中的應用程式類型，並使其可供部署：

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

「 MyApplicationV1 」 是 hello hello 應用程式封裝所在位置的映像存放區中的 hello 資料夾。 hello 應用程式類型具有名稱"MyApplicationType"和"1.0.0 版 」 （兩者都在 hello 應用程式資訊清單中找到） 現在會 hello 叢集中註冊。

hello[暫存器 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) hello 系統已成功註冊的 hello 應用程式封裝之後，才會傳回命令。 時間長度，註冊會取決於 hello 大小和 hello 應用程式套件的內容。 如有需要 hello **-TimeoutSec**參數可以是使用的 toosupply 較長逾時 （hello 預設逾時為 60 秒）。

如果您有大型應用程式套件，或者如果您遇到逾時，使用 hello **-Async**參數。 hello 叢集接受 hello 註冊命令，並視需要 hello 處理作業會繼續時，就會傳回 hello 命令。
hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps)命令列出所有已成功註冊應用程式類型版本及其註冊狀態。 您可以使用這個命令 toodetermine hello 註冊完成。

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>建立 hello 應用程式
您可以從已成功註冊使用 hello 任何應用程式類型版本的應用程式具現化[新增 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet。 每個應用程式的 hello 名稱必須以 hello 開頭*"fabric:"*配置，而且必須是唯一的每個應用程式執行個體。 也會建立任何 hello hello 目標應用程式類型的應用程式資訊清單中定義的預設服務。

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
多個應用程式執行個體可以針對任何指定的已註冊應用程式類型版本來建立。 每個應用程式執行個體將在隔離狀態下執行，包含本身的工作目錄和程序。

toosee 名為應用程式和服務正在執行 hello 的 hello 叢集中[Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication)和[Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>移除應用程式
當不再需要應用程式執行個體時，您可以永久移除它的名稱使用 hello[移除 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet。 [移除 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps)會自動移除屬於 toohello 應用程式以及，永久移除所有的服務狀態的所有服務。 

> [!WARNING]
> 此作業無法回復，且應用程式狀態無法復原。

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>取消註冊應用程式類型
當不再需要特定版本的應用程式類型時，您應該取消註冊 hello 應用程式類型使用 hello[取消註冊 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet。 取消登錄未使用的應用程式類型版本所使用儲存空間 hello 映像存放區。 只要沒有對應的應用程式針對應用程式類型進行具現化，且沒有擱置中的應用程式升級進行參考該類性，便可取消註冊該應用程式類型。

執行[Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello 應用程式類型目前已登錄在 hello 叢集中：

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

執行[取消註冊 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister 特定應用程式類型：

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>移除 hello 映像存放區中的應用程式套件
當不再需要的應用程式封裝時，您可以將它刪除 hello 映像存放區 toofree 系統資源。

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>疑難排解
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage 要求 ImageStoreConnectionString
hello Service Fabric SDK 環境應該已經有 hello 正確設定預設值。 但所有命令的 hello ImageStoreConnectionString 如有需要應符合 hello 值該 hello Service Fabric 叢集所使用。 您可以在 hello 叢集資訊清單中找到 hello ImageStoreConnectionString 使用 hello 擷取[Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps)和 Get ImageStoreConnectionStringFromClusterManifest 命令：

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet，這是 hello Service Fabric SDK PowerShell 模組的一部分，是使用的 tooget hello 映像儲存連接字串。  tooimport hello SDK 模組，執行：

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

hello ImageStoreConnectionString hello 叢集資訊清單中找到：

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

請參閱[hello 映像存放區連接字串了解](service-fabric-image-store-connection-string.md)如需關於 hello 映像存放區，以及映像存放區連接字串的補充資訊。

### <a name="deploy-large-application-package"></a>部署大型應用程式封裝
問題︰大型應用程式封裝 (GB 的順序) 的 [Copy-servicefabricapplicationpackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 逾時。
請嘗試︰
- 使用`TimeoutSec`參數指定 [Copy-servicefabricapplicationpackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令的較大逾時。 根據預設，hello 逾時為 30 分鐘的時間。
- 請檢查您的來源電腦與叢集之間的 hello 網路連線。 如果 hello 連接相當緩慢，請考慮使用較佳的網路連線的機器。
如果 hello 用戶端電腦 hello 叢集以外的另一個區域中，請考慮在接近或相同區域內的用戶端電腦使用為 hello 叢集。
- 請檢查是否到達外部節流。 例如，設定的 toouse azure 儲存體 hello 映像存放區時，可能會進行節流處理上傳。

問題︰上傳封裝順利完成，但 [Register-servicefabricapplicationtype](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 逾時。請嘗試︰
- [壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區之前。
hello 壓縮會減少 hello 大小，必須執行 hello 檔案數目，而後者可減少流量的 hello 數量和使用該服務的網狀架構。 hello 上傳作業可能會變慢 （特別是如果您包含 hello 壓縮時間），但註冊和取消註冊 hello 應用程式類型時，速度加快。
- 使用 `TimeoutSec` 參數指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的較大逾時。
- 指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的 `Async` 參數。 hello 叢集接受 hello 命令並 hello 應用程式類型的 hello 註冊會以非同步方式繼續時，就會傳回 hello 命令。 基於這個理由，沒有任何需要 toospecify 較高的逾時在此情況下。 hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps)命令列出所有已成功註冊應用程式類型版本及其註冊狀態。 您可以使用這個命令 toodetermine hello 註冊完成。

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>部署具有很多檔案的應用程式封裝
問題︰具有很多檔案的應用程式封裝 (以千計的順序) [Register-servicefabricapplicationtype](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的逾時。
請嘗試︰
- [壓縮 hello 封裝](service-fabric-package-apps.md#compress-a-package)複製 toohello 映像存放區之前。 hello 壓縮會減少檔案的 hello 數目。
- 使用 `TimeoutSec` 參數指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的較大逾時。
- 指定 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 的 `Async` 參數。 hello 叢集接受 hello 命令並 hello 應用程式類型的 hello 註冊會以非同步方式繼續時，就會傳回 hello 命令。
基於這個理由，沒有任何需要 toospecify 較高的逾時在此情況下。 hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps)命令列出所有已成功註冊應用程式類型版本及其註冊狀態。 您可以使用這個命令 toodetermine hello 註冊完成。

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>後續步驟
[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)

[Service Fabric 健康狀態簡介](service-fabric-health-introduction.md)

[診斷和疑難排解 Service Fabric 服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[在 Service Fabric 中模型化應用程式](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
