---
title: "aaaService 網狀架構和部署的容器，在 Linux 中 |Microsoft 文件"
description: "Service Fabric 和 hello 使用 Linux 容器 toodeploy 微服務應用程式。 本文說明 Service Fabric 提供容器和如何 toodeploy Linux 容器映像到叢集中的 hello 功能"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>部署 Linux 容器 tooService 網狀架構
> [!div class="op_single_selector"]
> * [部署 Windows 容器](service-fabric-deploy-container.md)
> * [部署 Linux 容器](service-fabric-deploy-container-linux.md)
>
>

本文將引導您在 Linux 上的 Docker 容器中建置容器化服務。

Service Fabric 有數個容器功能可協助您建置由容器化微服務組成的應用程式。 這些服務稱為容器化服務。

hello 功能包括：

* 容器映像部署和啟用
* 資源管理
* 儲存機制驗證
* 容器連接埠 toohost 連接埠對應
* 容器至容器的探索及通訊
* 能力 tooconfigure 並設定環境變數

## <a name="packaging-a-docker-container-with-yeoman"></a>使用 Yeoman 封裝 Docker 容器
當封裝在 Linux 上的容器，您可以選擇任一 toouse yeoman 範本或[手動建立 hello 應用程式封裝](#manually)。

Service Fabric 應用程式可以包含一個或多個容器，每個都有特定角色中傳送嗨應用程式的功能。 hello Service Fabric SDK for Linux 包含[Yeoman](http://yeoman.io/)產生器，可讓您輕鬆 toocreate 您的應用程式並加入容器映像。 讓我們使用具有單一的 Docker 容器的應用程式呼叫 Yeoman toocreate *SimpleContainerApp*。 您可以稍後新增更多服務，藉由編輯 hello 產生資訊清單檔案。

## <a name="install-docker-on-your-development-box"></a>在您的開發電腦上安裝 Docker

Hello 執行的下列命令 tooinstall Linux 開發機器上的 docker （如果您在 OSX 上使用 hello vagrant 映像，docker 已安裝）：

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>建立 hello 應用程式
1. 在終端機中，輸入 `yo azuresfcontainer`。
2. 為應用程式命名，例如 mycontainerap
3. 提供從 DockerHub 儲存機制的 hello 容器映像 hello URL。 hello 映像參數會採用 hello 表單 [儲存機制] / [映像名稱]
4. 如果 hello 映像沒有定義，為工作負載進入點，則您需要 tooexplicitly 輸入的命令以逗號分隔一組指定命令 toorun hello 容器，將會保留在啟動之後執行的 hello 容器內。

![容器的 Service Fabric Yeoman 產生器][sf-yeoman]

## <a name="deploy-hello-application"></a>部署 hello 應用程式

### <a name="using-xplat-cli"></a>使用 XPlat CLI
建置 hello 應用程式之後，您可以使用 Azure CLI hello toohello 本機叢集對它進行部署。

1. Toohello 本機 Service Fabric 叢集連線。

    ```bash
    azure servicefabric cluster connect
    ```

2. 使用 hello 安裝指令碼，提供在 hello 範本 toocopy hello 應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型，以及建立 hello 應用程式的執行個體。

    ```bash
    ./install.sh
    ```

3. 開啟瀏覽器，並瀏覽 tooService Fabric 總管在 http://localhost:19080 總管 (hello 私用 ip 的 hello VM，如果在 Mac OS X 使用 Vagrant 取代 localhost)。
4. 展開 [hello 應用程式] 節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。
5. 使用 hello 解除安裝指令碼 hello 範本 toodelete hello 應用程式執行個體中所提供，並取消登錄 hello 應用程式類型。

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>使用 Azure CLI 2.0

請參閱 hello 參考文件管理[應用程式生命週期使用 hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md)。

範例應用程式， [GitHub 上的簽出 hello Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>新增更多服務 tooan 現有應用程式

tooadd 另一個容器服務 tooan 應用程式使用已建立`yo`，執行下列步驟的 hello:

1. 變更 hello 現有應用程式的根目錄 toohello。  例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。
2. 執行 `yo azuresfcontainer:AddService`

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

您可以提供輸入的命令，藉由指定選擇性的 hello`Commands`組逗號分隔的命令 toorun hello 容器內的項目。

> [!NOTE]
> 如果 hello 映像沒有定義，為工作負載進入點，則您需要 tooexplicitly 指定內輸入的命令`Commands`組逗號分隔的命令 toorun hello 容器，將會保留執行的 hello 容器內的項目啟動。

## <a name="understand-resource-governance"></a>了解資源管理
資源管理機制是，限制 hello 容器的 hello 資源 hello 容器的功能可以使用 hello 主機上。 hello `ResourceGovernancePolicy`，其中指定 hello 應用程式資訊清單中的就是使用的 toodeclare 資源限制，服務程式碼封裝。 您可以設定資源限制 hello 下列資源：

* 記憶體
* MemorySwap
* CpuShares (CPU 相對權數)
* MemoryReservationInMB  
* BlkioWeight (BlockIO 相對權數)。

> [!NOTE]
> 在未來版本中，會加入支援指定特定的區塊 IO 限制，例如 IOP、讀取/寫入 BPS 及其他限制。
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

## <a name="configure-container-port-to-host-port-mapping"></a>設定容器連接埠至主機連接埠的對應
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
使用 hello`PortBinding`原則，您可以將對應的容器連接埠 tooan `Endpoint` hello 服務資訊清單中。 hello 端點`Endpoint1`可以指定固定通訊埠 （例如，連接埠 80）。 也可以指定任何連接埠，在此情況下針對您選擇 hello 叢集應用程式連接埠範圍的隨機連接埠。

如果您指定端點，使用 hello `Endpoint` hello 客體容器，Service Fabric 服務資訊清單中的標記可以自動發佈此端點 toohello 命名服務。 因此，hello 叢集中執行的其他服務可以探索使用 hello REST 查詢以解析此容器。

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

以 hello 命名服務註冊，步驟很容易在 hello 程式碼中的容器-容器通訊您容器內使用 hello[反向 proxy](service-fabric-reverseproxy.md)。 通訊是由提供 hello 反向 proxy http 接聽連接埠和 hello 名稱要與 toocommunicate 視為環境變數的 hello 服務執行。 如需詳細資訊，請參閱 hello 下一節。

## <a name="configure-and-set-environment-variables"></a>設定環境變數
環境變數可以指定每個程式碼封裝中的 hello 服務資訊，同時在容器中部署的服務或服務與處理程序/客體可執行檔部署。 這些環境變數的值可以覆寫，特別是在 hello 應用程式資訊清單或做為應用程式參數的部署期間指定。

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
* [互動使用 hello Azure CLI Service Fabric 叢集](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>相關文章

* [開始使用 Service Fabric 和 Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [開始使用 Service Fabric XPlat CLI](service-fabric-azure-cli.md)
