---
title: "aaaService 網狀架構和部署容器 |Microsoft 文件"
description: "Service Fabric 和 hello 使用容器 toodeploy 微服務應用程式。 本文說明 Service Fabric 提供容器和如何 toodeploy Windows 容器映像到叢集中的 hello 功能。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>部署 Windows 容器 tooService 網狀架構
> [!div class="op_single_selector"]
> * [部署 Windows 容器](service-fabric-deploy-container.md)
> * [部署 Docker 容器](service-fabric-deploy-container-linux.md)
> 
> 

這篇文章會引導您建立 Windows 容器中的容器化的服務的 hello 程序。

Service Fabric 有數個功能可協助您建置由容器內執行之微服務組成的應用程式。 

hello 功能包括：

* 容器映像部署和啟用
* 資源管理
* 儲存機制驗證
* 容器連接埠至主機連接埠的對應
* 容器至容器的探索及通訊
* 能力 tooconfigure 並設定環境變數

讓我們看看您要封裝包含在您的應用程式容器化的服務 toobe 時，每個功能的運作方式。

## <a name="package-a-windows-container"></a>封裝 Windows 容器
當您封裝的容器時，您可以選擇 toouse Visual Studio 專案範本或[手動建立 hello 應用程式封裝](#manually)。  當您使用 Visual Studio，hello 應用程式封裝的結構，並為您建立資訊清單檔案的 hello 新的專案範本。

> [!TIP]
> 最簡單方式 toopackage hello 現有的容器映像服務是 toouse Visual Studio。

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>使用 Visual Studio toopackage 現有的容器映像
Visual Studio 提供 Service Fabric 服務範本 toohelp 部署容器 tooa Service Fabric 叢集。

1. 選擇 [檔案]  >  [新增專案]，然後建立 Service Fabric 應用程式。
2. 選擇**客體容器**作為 hello 服務範本。
3. 選擇**映像名稱**並提供您的容器儲存機制中的 hello 路徑 toohello 映像。 例如，https://hub.docker.com 中的 `myrepo/myimage:v1`
4. 指定服務的名稱，然後按一下 [確定]。
5. 如果您容器化的服務端點需要通訊，您現在可以新增 hello 通訊協定、 連接埠和型別 toohello ServiceManifest.xml 檔案。 例如： 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    藉由提供 hello `UriScheme`，Service Fabric 會自動以 hello 的發現能力命名服務註冊 hello 容器端點。 hello 連接埠可以固定的 （如同 hello 前面範例所示） 或動態配置。 如果您未指定連接埠，會以動態方式配置從 hello 應用程式連接埠範圍 （如同發生與任何服務）。
    您也需要 tooconfigure hello 容器 toohost 連接埠對應藉由指定`PortBinding`hello 應用程式資訊清單中的原則。 如需詳細資訊，請參閱[設定容器 toohost 連接埠對應](#Portsection)。
6. 如果您的容器需要資源管理，則請新增 `ResourceGovernancePolicy`。
8. 如果您的容器需要 tooauthenticate 與私用儲存機制，然後新增`RepositoryCredentials`。
7. 如果您沒有啟用容器支援執行 Windows Server 2016 電腦上，您可以使用 hello 封裝和發行動作 toodeploy tooyour 本機叢集。 
8. 準備就緒時，您可以發行 hello 應用程式 tooa 遠端叢集，或檢查 hello 方案 toosource 控制項中。 

例如，簽出 hello [GitHub 上的 Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>建立 Windows Server 2016 叢集
toodeploy 容器化的應用程式時，您需要的 toocreate 啟用容器支援執行 Windows Server 2016 的叢集。 您的叢集可能會在本機執行，或透過 Azure Resource Manager 部署在 Azure 中。 

toodeploy 叢集中使用 Azure 資源管理員 中，選擇 hello**與容器的 Windows Server 2016**映像在 Azure 中的選項。 請參閱 hello 文章[使用 Azure Resource Manager 建立 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。 請確定您使用下列 Azure 資源管理員設定的 hello:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
您也可以使用 hello[五個節點的 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)toocreate 叢集。 或者，閱讀社群中的[部落格文章](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html)以了解如何使用 Service Fabric 和 Windows 容器。

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>手動封裝和部署容器映像
hello 程序手動封裝進行容器化的服務根據 hello 下列步驟：

1. 發行 hello 容器 tooyour 儲存機制。
2. 建立 hello 封裝目錄結構。
3. 編輯 hello 服務資訊清單檔。
4. 編輯 hello 應用程式資訊清單檔案。

## <a name="deploy-and-activate-a-container-image"></a>部署和啟用容器映像
在 hello Service Fabric[應用程式模型](service-fabric-application-model.md)，容器代表複本會放在哪一種多個服務應用程式主機。 toodeploy 並啟動容器，put 的 hello 名稱 hello 容器映像到`ContainerHost`hello 服務資訊清單中的項目。

在 hello 服務資訊清單中，加入`ContainerHost`hello 進入點。 然後組 hello `ImageName` toobe hello 名稱 hello 容器儲存機制和映像。 hello 下列部分的資訊清單示範如何呼叫 toodeploy hello 容器`myimage:v1`從儲存機制稱為`myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

您可以指定啟動 hello hello 容器時的選擇性命令 toorun`Commands`項目。 若有多個命令，用逗號分隔它們。 

## <a name="understand-resource-governance"></a>了解資源管理
資源管理機制是，限制 hello 容器的 hello 資源 hello 容器的功能可以使用 hello 主機上。 hello `ResourceGovernancePolicy`，其中指定 hello 應用程式資訊清單中的就是使用的 toodeclare 資源限制，服務程式碼封裝。 您可以設定資源限制 hello 下列資源：

* 記憶體
* MemorySwap
* CpuShares (CPU 相對權數)
* MemoryReservationInMB  
* BlkioWeight (BlockIO 相對權數)。

> [!NOTE]
> 我們規劃在未來支援指定特定的區塊 IO 限制，例如 IOP、讀取/寫入 BPS 及其他限制。
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>驗證儲存機制
toodownload 容器，您可能必須 tooprovide 登入認證 toohello 容器儲存機制。 hello 登入認證，在 hello 應用程式資訊清單中指定會使用的 toospecify hello 登入資訊或下載 hello 容器映像從 hello 映像儲存機制的 SSH 金鑰。 hello 下列範例將示範名為帳戶*TestUser*以及 hello 密碼以純文字 (*不*建議使用):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

我們建議您在使用已部署 toohello 機器的憑證來加密 hello 密碼。

hello 下列範例將示範名為帳戶*TestUser*、 其中 hello 密碼加密所使用的憑證稱為*MyCert*。 您可以使用 hello `Invoke-ServiceFabricEncryptText` PowerShell 命令 toocreate hello 密碼加密文字 hello 密碼。 如需詳細資訊，請參閱 hello 文章[管理 Service Fabric 應用程式中的機密](service-fabric-application-secret-management.md)。

hello hello 憑證私密金鑰用 toodecrypt hello 密碼必須是已部署的 toohello 本機電腦的頻外方法中。 (在 Azure 中，這個方法就是 Azure Resource Manager。)然後，當 Service Fabric 部署 hello 服務封裝 toohello 機器，它可以解密 hello 密碼。 藉由使用 hello 密碼以及 hello 帳戶名稱，它可以再向 hello 容器儲存機制。

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name ="Portsection"></a>設定容器 toohost 連接埠對應
您也可以指定與 hello 容器設定主機使用的連接埠 toocommunicate `PortBinding` hello 應用程式資訊清單中。 hello 連接埠繫結對應 hello 連接埠 toowhich hello 服務會接聽內部 hello 主機上的 hello 容器 tooa 通訊埠。

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>設定容器至容器的探索及通訊
您可以使用 hello`PortBinding`元素 toomap hello 服務資訊清單中的容器連接埠 tooan 端點。 在下列範例的 hello，hello 端點`Endpoint1`8905 指定固定通訊埠。 也可以指定任何連接埠，在此情況下針對您選擇 hello 叢集應用程式連接埠範圍的隨機連接埠。


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
如果您指定端點，使用 hello `Endpoint` hello 客體容器，Service Fabric 服務資訊清單中的標記可以自動發佈此端點 toohello 命名服務。 因此，hello 叢集中執行的其他服務可以探索使用 hello REST 查詢以解析此容器。

註冊以 hello 命名服務後，您可以執行容器的容器通訊您容器內使用 hello[反向 proxy](service-fabric-reverseproxy.md)。 通訊是由提供 hello 反向 proxy http 接聽連接埠和 hello 名稱要與 toocommunicate 視為環境變數的 hello 服務執行。 如需詳細資訊，請參閱 hello 下一節。 

## <a name="configure-and-set-environment-variables"></a>設定環境變數
環境變數可以指定每個程式碼封裝 hello 服務資訊清單中。 所有服務都有這項功能，無論是部署為容器或處理程序或來賓可執行檔。 您可以覆寫資訊清單 hello 應用程式中的值，或做為應用程式參數的部署期間指定這些環境變數。

hello 下列服務資訊清單 XML 程式碼片段示範如何的範例程式碼封裝的 toospecify 環境變數：

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

這些環境變數會覆寫 hello 應用程式層級資訊清單：

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

在 hello 前一個範例中，我們已指定明確的值為 hello`HttpGateway`環境變數 (19000)，而我們將設定為 hello 值`BackendServiceName`參數透過 hello`[BackendSvc]`應用程式參數。 這些設定可讓您 toospecify hello 值`BackendServiceName`時部署 hello 應用程式和 hello 資訊清單中沒有固定的值的值。

## <a name="configure-isolation-mode"></a>設定隔離模式

Windows 支援兩種容器隔離模式 - 處理序和 Hyper-V。  Hello 處理序隔離模式中，所有的 hello 容器上執行 hello 相同主機電腦共用 hello 核心與 hello 主機。 Hello HYPER-V 隔離模式中，hello 核心會隔離每個 HYPER-V 容器與 hello 容器主機之間。 指定在 hello hello 隔離模式`ContainerHostPolicies`hello 應用程式資訊清單檔中的標記。  hello 隔離模式可指定為`process`， `hyperv`，和`default`。 hello`default`太預設隔離模式`process`Windows 伺服器上裝載，且預設值太`hyperv`Windows 10 主機上。  hello 下列程式碼片段示範如何指定 hello 應用程式資訊清單檔中的 hello 隔離模式。

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>應用程式和服務資訊清單的完整範例

以下是應用程式資訊清單：

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

（在 hello 前面應用程式資訊清單中指定） 的範例服務資訊清單如下：

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>後續步驟
既然您已部署的容器化的服務，了解如何 toomanage 藉由讀取週期[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)。

* [Service Fabric 和容器的概觀](service-fabric-containers-overview.md)
* 如需範例，請查看 [GitHub 上的 Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
