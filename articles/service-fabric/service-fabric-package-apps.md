---
title: "aaaPackage Azure Service Fabric 應用程式 |Microsoft 文件"
description: "如何 toopackage Service Fabric 應用程式，才能部署 tooa 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a>封裝應用程式
本文說明如何 toopackage Service Fabric 應用程式並讓它準備好進行部署。

## <a name="package-layout"></a>封裝版面配置
hello 應用程式資訊清單、 一個或多個服務資訊清單和其他檔案必須依照特定的版面配置，以部署至 Service Fabric 叢集所需的套件。 本文章中的 hello 範例資訊清單需要 toobe 組織 hello 下列目錄結構中：

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

hello 資料夾名為 toomatch hello**名稱**屬性的每個對應的項目。 例如，如果 hello 服務資訊清單包含與 hello 名稱的兩個程式碼封裝**MyCodeA**和**MyCodeB**，則兩個資料夾都包含相同名稱的 hello 與 hello 每個程式碼所需的二進位檔封裝。

## <a name="use-setupentrypoint"></a>使用 SetupEntryPoint
使用的典型案例**SetupEntryPoint**是當您需要 toorun hello 服務啟動之前可執行檔或需要 tooperform 使用更高權限的作業。 例如：

* 設定及初始化 hello 服務可執行檔需要的環境變數。 不限制的 tooonly hello Service Fabric 程式設計模型透過撰寫的可執行檔。 例如，npm.exe 部署 node.js 應用程式，需要設定某些環境變數。
* 透過安裝安全性憑證設定存取控制。

如需有關如何 tooconfigure hello **SetupEntryPoint**，請參閱[設定服務安裝程式的進入點的 hello 原則](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>設定
### <a name="build-a-package-by-using-visual-studio"></a>使用 Visual Studio 建置封裝
如果您使用 Visual Studio 2015 toocreate 您的應用程式，您可以使用 hello 命令 tooautomatically 建立符合上面所述的 hello 版面配置的封裝的封裝。

toocreate 封裝時，以滑鼠右鍵按一下方案總管 中的 hello 應用程式專案，並選擇 hello 套件 命令，如下所示：

![使用 Visual Studio 封裝應用程式][vs-package-command]

封裝完成後，您可以在 hello 找到 hello 封裝的 hello 位置**輸出**視窗。 當您部署或偵錯 Visual Studio 中的應用程式時，會自動發生 hello 封裝步驟。

### <a name="build-a-package-by-command-line"></a>透過命令列建置封裝
它也是您的應用程式使用的可能 tooprogrammatically 封裝`msbuild.exe`。 Hello 原理，Visual Studio 執行它因此 hello 輸出會相同。

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>測試 hello 封裝
您可以確認 hello 封裝結構，透過 PowerShell 在本機使用 hello[測試 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps)命令。
此命令會檢查有無資訊清單剖析問題，並驗證所有參考。 此命令只會驗證 hello hello 封裝中的 hello 目錄和檔案結構的正確性。
它不會驗證任何 hello 程式碼或資料封裝的內容超過檢查所有必要的檔案都存在。

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

這項錯誤顯示該 hello *MySetup.bat* hello 服務資訊清單中所參考的檔案**SetupEntryPoint** hello 程式碼封裝中遺漏。 加入 hello 遺失檔案之後，會將 $ hello 應用程式驗證：

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

如果您的應用程式已定義[應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)，您可以在 [Test-ServiceFabricApplicationPackage (英文)](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) 中傳遞它們以進行適當的驗證。

如果您知道 hello 應用程式將會部署的 hello 叢集，則建議您傳入 hello`ImageStoreConnectionString`參數。 在此情況下，hello 封裝也會針對舊版 hello 應用程式已在 hello 叢集中執行驗證。 例如，封裝是否可以偵測到 hello 驗證 hello 與相同的版本，但內容不同已部署。  

評估 hello 應用程式正確的封裝，並通過驗證，視壓縮，根據 hello 大小與 hello 檔案數目。

## <a name="compress-a-package"></a>壓縮封裝
當封裝很大或有許多檔案時，您可以壓縮它以加快部署速度。 壓縮會減少 hello 的檔案數目與 hello 封裝大小。
壓縮的應用程式封裝，[上傳 hello 應用程式封裝](service-fabric-deploy-remove-applications.md#upload-the-application-package)可能需要再比較的 toouploading hello 未壓縮的封裝 （特別如果壓縮時間分解出來），但[註冊](service-fabric-deploy-remove-applications.md#register-the-application-package)和[取消註冊 hello 應用程式類型](service-fabric-deploy-remove-applications.md#unregister-an-application-type)更快，壓縮的應用程式封裝。

hello 部署機制是相同的壓縮和未壓縮的封裝。 如果 hello 封裝已壓縮，因此儲存 hello 叢集映像存放區中，而且執行 hello 應用程式之前，hello 節點上進行壓縮。
hello 壓縮取代 hello 壓縮版的 hello 有效 Service Fabric 封裝。 hello 資料夾必須允許寫入權限。 在已經壓縮的封裝上執行壓縮將不會產生任何變化。

您可以藉由執行 hello Powershell 命令來壓縮封裝[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)與`CompressPackage`切換。 您可以解壓縮 hello 相同封裝以 hello 命令，使用`UncompressPackage`切換。

hello 下列命令壓縮 hello 封裝但不複製該項 toohello 映像存放區。 您可以壓縮的封裝 tooone 或複製多個 Service Fabric 叢集，視需要使用[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)沒有 hello`SkipCopy`旗標。
hello 封裝現在包含 hello 的 zip 的檔案`code`， `config`，和`data`封裝。 不壓縮 hello 應用程式資訊清單和 hello 服務資訊清單，因為它們所需的許多內部的作業 （例如共用、 應用程式類型名稱和版本擷取針對特定的驗證封裝）。
壓縮 hello 資訊清單會使這些操作效率不佳。

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

或者，您可以壓縮並複製 hello 封裝[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)以一個步驟。
如果 hello 套件很大，提供 hello 封裝壓縮和 hello 上載 toohello 叢集夠高的逾時 tooallow 時間。
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

就內部而言，Service Fabric 計算總和檢查碼驗證的 hello 應用程式封裝。 當使用壓縮，hello 總和檢查碼計算 hello 壓縮每個封裝的版本上。
如果您複製到未壓縮的版本，您的應用程式封裝，而且您想 hello toouse 壓縮相同的封裝，您必須變更 hello hello 版本`code`， `config`，和`data`封裝 tooavoid 總和檢查碼不符。 如果 hello 封裝不會變更，而不是變更 hello 版本，您可以使用[差異佈建](service-fabric-application-upgrade-advanced.md)。 使用此選項時，不包括 hello 不變的封裝而從 hello 服務資訊清單參考它。

同樣地，如果您上傳 hello 封裝的壓縮的版本，而且您想 toouse 未壓縮的封裝，您必須更新 hello 版本 tooavoid hello 總和檢查碼不符。

hello 封裝是現在正確封裝、 驗證，且壓縮的 （如有需要），讓它可供[部署](service-fabric-deploy-remove-applications.md)tooone 或多個 Service Fabric 叢集。

### <a name="compress-packages-when-deploying-using-visual-studio"></a>使用 Visual Studio 進行部署時壓縮套件
您可以指示 Visual Studio toocompress 套件部署中，藉由新增 hello`CopyPackageParameters`元素 tooyour 發行設定檔，並設定 hello`CompressPackage`屬性太`true`。

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>後續步驟
[部署和移除應用程式][ 10]描述如何 toouse PowerShell toomanage 應用程式執行個體

[管理應用程式參數的多個環境][ 11]描述如何 tooconfigure 參數和環境變數不同的應用程式執行個體。

[設定您的應用程式的安全性原則][ 12]描述 toorun 下安全性原則 toorestrict 存取服務的方式。

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
