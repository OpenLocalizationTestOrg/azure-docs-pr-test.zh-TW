---
title: "aaaCreate Azure Service Fabric 容器應用程式 |Microsoft 文件"
description: "在 Azure Service Fabric 上建立第一個 Windows 容器應用程式。  建立 Docker 映像與 Python 應用程式，推入 hello 映像 tooa 容器登錄中、 建置和部署 Service Fabric 容器應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>在 Windows 建立第一個 Service Fabric 容器應用程式
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Service Fabric 叢集上執行 Windows 容器中的現有應用程式不需要任何變更 tooyour 應用程式。 本文將指導您完成建立 Docker 映像包含 Python[酒瓶](http://flask.pocoo.org/)web 應用程式和部署 tooa Service Fabric 叢集。  您也將透過 [Azure Container Registry](/azure/container-registry/) 共用容器化應用程式。  本文假設您對 Docker 有基本認識。 您可以透過讀取 hello 深入了解 Docker [Docker 概觀](https://docs.docker.com/engine/understanding-docker/)。

## <a name="prerequisites"></a>必要條件
執行下列項目的開發電腦︰
* Visual Studio 2015 或 Visual Studio 2017。
* [Service Fabric SDK 和工具](service-fabric-get-started.md)。
*  Docker for Windows。  [取得 Docker CE for Windows (穩定)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description)。 安裝及啟動 Docker hello 系統匣圖示上按一下滑鼠右鍵，然後選取後**切換 tooWindows 容器**。 這是根據 Windows 的必要的 toorun Docker 映像。

有三個或更多節點在具有容器的 Windows Server 2016 上執行的 Windows 叢集 - [建立叢集](service-fabric-cluster-creation-via-portal.md)或[免費試用 Service Fabric](https://aka.ms/tryservicefabric)。

Azure Container Registry 中的登錄 - 在 Azure 訂用帳戶中[建立容器登錄](../container-registry/container-registry-get-started-portal.md)。

## <a name="define-hello-docker-container"></a>定義 hello Docker 容器
建置 hello 為基礎的映像[Python 的映像](https://hub.docker.com/_/python/)位於 Docker Hub。

在 Dockerfile 中定義您的 Docker 容器。 hello Dockerfile 包含指示設定您的容器內的 hello 環境、 載入 hello 應用程式想 toorun，和對應的連接埠。 hello Dockerfile 是 hello 輸入的 toohello`docker build`命令，建立 hello 映像。

建立空的目錄，並建立 hello 檔案*Dockerfile* （不含檔案副檔名）。 Hello 太之後加入*Dockerfile*並儲存變更：

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

讀取 hello[的 Dockerfile 參考](https://docs.docker.com/engine/reference/builder/)如需詳細資訊。

## <a name="create-a-simple-web-application"></a>建立簡單 Web 應用程式
建立 Flask Web 應用程式，其會在連接埠 80 上接聽並傳回 "Hello World!"。  在 hello 相同的目錄中建立 hello 檔案*requirements.txt*。  新增下列 hello 和儲存您的變更：
```
Flask
```

也會建立 hello *app.py*檔案，然後加入下列 hello:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>建立 hello 映像
執行 hello`docker build`命令 toocreate hello 映像，執行您 web 應用程式。 開啟 PowerShell 視窗並瀏覽包含 hello Dockerfile toohello 目錄。 執行下列命令的 hello:

```
docker build -t helloworldapp .
```

此組建 hello hello 指示使用 Dockerfile 中，在新的映像的命令命名 (-t 標記) hello 映像 」 helloworldapp"。 建置映像從 Docker Hub 提取的 hello 基底映像，並建立新的映像，將它新增 hello 基底映像之上的應用程式。  

Hello 建置命令完成之後，請執行 hello`docker images`命令 toosee hello 新映像的詳細資訊：

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>在本機執行 hello 應用程式
請確認您的映像在本機，再將它推送 hello 容器登錄中。  

執行 hello 應用程式：

```
docker run -d --name my-web-site helloworldapp
```

*名稱*提供名稱 toohello 執行容器 （而不是 hello 容器識別碼）。

Hello 容器會啟動一次，尋找其 IP 位址，以便您可以連接 tooyour 從瀏覽器執行容器：
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

連接 toohello 執行容器。  開啟網頁瀏覽器指向 toohello 傳回 IP 位址，例如"http://172.31.194.61"。 您應該會看見 hello 標題"Hello World ！" 在 hello 瀏覽器中顯示。

toostop 您執行的容器：

```
docker stop my-web-site
```

從開發電腦刪除 hello 容器：

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>推播 hello 映像 toohello 容器登錄中
在您確認該 hello 容器會在開發電腦上執行之後，推送 hello 映像 tooyour 登錄 Azure 容器登錄中。

執行``docker login``toolog tooyour 容器登錄中以在您[登錄認證](../container-registry/container-registry-authentication.md)。

hello 下列範例會傳遞 hello ID 和 Azure Active Directory 密碼[服務主體](../active-directory/active-directory-application-objects.md)。 例如，您可能已指派服務主體 tooyour 登錄所需自動化案例。 或者，您可以使用登錄使用者名稱和密碼進行登入。

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

hello 下列命令會建立標記或別名，hello 影像的完整的路徑 tooyour 登錄。 此範例中位置 hello hello 中的映像```samples```hello hello 登錄根目錄中的命名空間 tooavoid 雜亂。

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

推送 hello 映像 tooyour 容器登錄中：

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Visual Studio 中建立 hello 容器化服務
hello Service Fabric SDK 和工具可提供服務範本 toohelp 建立容器化應用程式。

1. 啟動 Visual Studio。  選取 [檔案] > [新增] > [專案]。
2. 選取 [Service Fabric 應用程式]，將它命名為 "MyFirstContainer"，然後按一下 [確定]。
3. 選取**客體容器**從 hello 清單**服務範本**。
4. 在**映像名稱**輸入"myregistry.azurecr.io/samples/helloworldapp"，推送 tooyour 容器儲存機制的 hello 映像。
5. 指定服務的名稱，然後按一下 [確定]。

## <a name="configure-communication"></a>設定通訊
hello 容器化服務需要端點進行通訊。 新增`Endpoint`hello 通訊協定、 連接埠，與類型 toohello ServiceManifest.xml 檔案項目。 這個發行項，容器化的 hello 服務會接聽連接埠 8081。  在此範例中，會使用固定的連接埠 8081。  如果未不指定任何連接埠，則會選擇 hello 應用程式連接埠範圍的隨機連接埠。  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

藉由定義端點，Service Fabric 發行 hello 端點 toohello 命名服務。  Hello 叢集中執行的其他服務可以解決這個容器。  您也可以執行使用 hello 的容器-容器通訊[反向 proxy](service-fabric-reverseproxy.md)。  通訊是由提供 hello 反向 proxy HTTP 接聽連接埠和 hello 名稱要與 toocommunicate 視為環境變數的 hello 服務執行。

## <a name="configure-and-set-environment-variables"></a>設定環境變數
環境變數可以指定每個程式碼封裝 hello 服務資訊清單中。 所有服務都有這項功能，無論是部署為容器或處理程序或來賓可執行檔。 您可以覆寫資訊清單 hello 應用程式中的值，或做為應用程式參數的部署期間指定這些環境變數。

hello 下列服務資訊清單 XML 程式碼片段示範如何的範例程式碼封裝的 toospecify 環境變數：
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

這些環境變數會覆寫 hello 應用程式資訊清單中：

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>設定容器連接埠對主機連接埠對應，以及容器對容器探索
設定主機使用的連接埠 toocommunicate 與 hello 容器。 hello 連接埠繫結對應 hello 的 hello 服務正在接聽連接埠內 hello 主機上的 hello 容器 tooa 通訊埠。 新增`PortBinding`中的項目`ContainerHostPolicies`hello ApplicationManifest.xml 檔案項目。  這個發行項，`ContainerPort`為 80 （hello 容器中所指定的 hello Dockerfile 以公開連接埠 80） 和`EndpointRef`是"Guest1TypeEndpoint 」 (hello hello 服務資訊清單中預先定義的端點)。  內送要求連接埠 8081 toohello 服務對應 tooport 80 hello 容器上。

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>設定容器登錄驗證
藉由新增設定容器登錄驗證`RepositoryCredentials`太`ContainerHostPolicies`的 hello ApplicationManifest.xml 檔案。 加入 hello 帳戶和密碼 hello myregistry.azurecr.io 容器登錄中，可讓 hello 服務 toodownload hello 容器映像從 hello 儲存機制。

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

我們建議您在使用已部署 tooall hello 叢集節點的加密憑證來加密 hello 儲存機制的密碼。 Service Fabric 部署 hello 服務封裝 toohello 叢集 hello 加密憑證時，使用的 toodecrypt hello 加密文字。  hello Invoke ServiceFabricEncryptText cmdlet 是針對 hello 密碼，它會加入 toohello ApplicationManifest.xml 檔案使用的 toocreate hello 加密文字。

hello 下列指令碼會建立新的自我簽署的憑證並將它匯出 tooa PFX 檔案。  hello 憑證匯入到現有的金鑰保存庫，然後再部署 toohello Service Fabric 叢集。

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
使用 hello hello 密碼加密[Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet。

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Hello 密碼取代 hello 加密文字傳回 hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet，並設定`PasswordEncrypted`太"，則為 true 」。

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>設定隔離模式
Windows 支援兩種容器隔離模式：分別為處理序和 Hyper-V。 Hello 處理序隔離模式中，所有的 hello 容器上執行 hello 相同主機電腦共用 hello 核心與 hello 主機。 Hello HYPER-V 隔離模式中，hello 核心會隔離每個 HYPER-V 容器與 hello 容器主機之間。 指定在 hello hello 隔離模式`ContainerHostPolicies`hello 應用程式資訊清單檔中的項目。 hello 隔離模式可指定為`process`， `hyperv`，和`default`。 hello 預設隔離模式預設太`process`Windows 伺服器上裝載，且預設值太`hyperv`Windows 10 主機上。 hello 下列程式碼片段示範如何指定 hello 應用程式資訊清單檔中的 hello 隔離模式。

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>設定資源控管
[資源監管](service-fabric-resource-governance.md)限制的 hello hello 容器的資源可以使用 hello 主機。 hello`ResourceGovernancePolicy`元素，其 hello 應用程式資訊清單中指定，就是使用的 toodeclare 資源限制，服務程式碼封裝。 可以設定資源限制 hello 下列資源： 記憶體、 MemorySwap、 CpuShares （CPU 相對權數）、 MemoryReservationInMB，BlkioWeight （BlockIO 相對權數）。  在此範例中，服務套件 Guest1Pkg 會取得一個核心 hello 叢集節點放置的位置上。  記憶體限制是絕對的因此 hello 程式碼封裝是有限的 too1024 MB 的記憶體 （和 hello 相同的軟體保證保留）。 程式碼封裝 （容器或處理程序） 不能 tooallocate 記憶體超過此限制，而嘗試 toodo 因此會導致記憶體不足例外狀況。 資源限制強制 toowork，所有的程式碼封裝在服務封裝內必須有指定記憶體限制。

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>部署 hello 容器應用程式
儲存所有變更，並建置 hello 應用程式。 toopublish 您的應用程式，以滑鼠右鍵按一下**MyFirstContainer**在方案總管，然後選取**發行**。

在**連接端點**，輸入 hello 叢集 hello 管理端點。  例如，"containercluster.westus2.cloudapp.azure.com:19000"。 您可以找到 hello 用戶端連接您的叢集在 hello hello 概觀刀鋒視窗中的端點[Azure 入口網站](https://portal.azure.com)。

按一下 [發行] 。

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個 Web 型工具，可檢查和管理 Service Fabric 叢集中的應用程式與節點。 開啟瀏覽器和瀏覽 toohttp://containercluster.westus2.cloudapp.azure.com:19080/總管/並遵循 hello 應用程式部署。  hello 應用程式部署，而處於錯誤狀態 （這可能需要一些時間，視 hello 映像大小而定） hello 叢集節點上下載 hello 映像之前：![錯誤][1]

hello 應用程式時，準備在```Ready```狀態：![準備][2]

開啟瀏覽器，並瀏覽 toohttp://containercluster.westus2.cloudapp.azure.com:8081。 您應該會看見 hello 標題"Hello World ！" 在 hello 瀏覽器中顯示。

## <a name="clean-up"></a>清除
您可以繼續 tooincur 費用 hello 叢集正在執行，請考慮[刪除您的叢集](service-fabric-get-started-azure-cluster.md#remove-the-cluster)。  [合作對象叢集](http://tryazureservicefabric.westus.cloudapp.azure.com/)會在幾個小時後自動刪除。

Hello 映像 toohello 容器登錄中是您推送之後您可以從開發電腦刪除 hello 本機映像：

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>完整範例 Service Fabric 應用程式和服務資訊清單
以下是 hello 完整服務以及在本文中使用的應用程式資訊清單。

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a>在容器被迫終止前設定時間間隔

Hello 服務刪除 （或移動 tooanother 節點） 啟動後移除 hello 容器之前，您可以設定 hello 執行階段 toowait 的時間間隔。 設定 hello 時間間隔傳送嗨`docker stop <time in seconds>`命令 toohello 容器。   如需更多詳細資訊，請參閱 [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)。 hello 下指定 hello 時間間隔 toowait `Hosting` > 一節。 hello 下列叢集資訊清單的程式碼片段顯示如何 tooset hello 等待間隔：

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
hello 預設時間間隔是否設定 too10 秒。 此組態是動態的因為組態只能升級 hello 叢集更新 hello 逾時。 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>設定 hello 執行階段 tooremove 未使用的容器映像

您可以設定 hello Service Fabric 叢集 tooremove 從 hello 節點未使用的容器映像。 此設定可讓磁碟空間 toobe 捕捉如果 hello 節點上有太多的容器映像。  tooenable 此功能，更新 hello`Hosting`區段 hello 叢集資訊清單中，hello 下列程式碼片段所示： 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

針對不應該刪除的映像，您可以指定下 hello 它們`ContainerImagesToSkip`參數。 



## <a name="next-steps"></a>後續步驟
* 深入了解如何[在 Service Fabric 上執行容器](service-fabric-containers-overview.md)。
* 讀取 hello[部署.NET 應用程式容器中的](service-fabric-host-app-in-a-container.md)教學課程。
* 深入了解 hello Service Fabric[應用程式生命週期](service-fabric-application-lifecycle.md)。
* 簽出 hello [Service Fabric 程式碼範例容器](https://github.com/Azure-Samples/service-fabric-dotnet-containers)GitHub 上。

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
