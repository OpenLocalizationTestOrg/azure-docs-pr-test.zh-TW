---
title: "aaaCreate on Linux 的 Azure Service Fabric 容器應用程式 |Microsoft 文件"
description: "在 Azure Service Fabric 上建立第一個 Linux 容器應用程式。  建立 Docker 映像，您的應用程式，推入 hello 映像 tooa 容器登錄中、 建置和部署 Service Fabric 容器應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>在 Linux 建立第一個 Service Fabric 容器應用程式
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Service Fabric 叢集上執行 Linux 容器中的現有應用程式不需要任何變更 tooyour 應用程式。 本文將指導您完成建立 Docker 映像包含 Python[酒瓶](http://flask.pocoo.org/)web 應用程式和部署 tooa Service Fabric 叢集。  您也將透過 [Azure Container Registry](/azure/container-registry/) 共用容器化應用程式。  本文假設您對 Docker 有基本認識。 您可以透過讀取 hello 深入了解 Docker [Docker 概觀](https://docs.docker.com/engine/understanding-docker/)。

## <a name="prerequisites"></a>必要條件
* 執行下列項目的開發電腦︰
  * [Service Fabric SDK 和工具](service-fabric-get-started-linux.md)。
  * [Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [Service Fabric CLI](service-fabric-cli.md)

* Azure Container Registry 中的登錄 - 在 Azure 訂用帳戶中[建立容器登錄](../container-registry/container-registry-get-started-portal.md)。 

## <a name="define-hello-docker-container"></a>定義 hello Docker 容器
建置 hello 為基礎的映像[Python 的映像](https://hub.docker.com/_/python/)位於 Docker Hub。 

在 Dockerfile 中定義您的 Docker 容器。 hello Dockerfile 包含指示設定您的容器內的 hello 環境、 載入 hello 應用程式想 toorun，和對應的連接埠。 hello Dockerfile 是 hello 輸入的 toohello`docker build`命令，建立 hello 映像。 

建立空的目錄，並建立 hello 檔案*Dockerfile* （不含檔案副檔名）。 Hello 太之後加入*Dockerfile*並儲存變更：

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
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

## <a name="build-hello-image"></a>建立 hello 映像
執行 hello`docker build`命令 toocreate hello 映像，執行您 web 應用程式。 開啟 PowerShell 視窗並瀏覽過*c:\temp\helloworldapp*。 執行下列命令的 hello:

```bash
docker build -t helloworldapp .
```

此組建 hello hello 指示使用 Dockerfile 中，在新的映像的命令命名 (-t 標記) hello 映像 」 helloworldapp"。 建置映像從 Docker Hub 提取的 hello 基底映像，並建立新的映像，將它新增 hello 基底映像之上的應用程式。  

Hello 建置命令完成之後，請執行 hello`docker images`命令 toosee hello 新映像的詳細資訊：

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>在本機執行 hello 應用程式
請確認您容器化應用程式執行本機之前將它推送 hello 容器登錄中。  

執行 hello 應用程式，對應您的電腦連接埠 4000 toohello 容器的公開連接埠 80:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*名稱*提供名稱 toohello 執行容器 （而不是 hello 容器識別碼）。

連接 toohello 執行容器。  開啟網頁瀏覽器指向所傳回的連接埠 4000，例如"http://localhost:4000"toohello IP 位址。 您應該會看見 hello 標題"Hello World ！" 在 hello 瀏覽器中顯示。

![Hello World!][hello-world]

toostop 您執行的容器：

```bash
docker stop my-web-site
```

從開發電腦刪除 hello 容器：

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>推播 hello 映像 toohello 容器登錄中
確認在 Docker 中執行 hello 應用程式後，推送 hello 映像 tooyour 登錄 Azure 容器登錄中。

執行`docker login`toolog tooyour 容器登錄中以在您[登錄認證](../container-registry/container-registry-authentication.md)。

hello 下列範例會傳遞 hello ID 和 Azure Active Directory 密碼[服務主體](../active-directory/active-directory-application-objects.md)。 例如，您可能已指派服務主體 tooyour 登錄所需自動化案例。  或者，您可以使用登錄使用者名稱和密碼進行登入。

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

hello 下列命令會建立標記或別名，hello 影像的完整的路徑 tooyour 登錄。 此範例中位置 hello hello 中的映像`samples`hello hello 登錄根目錄中的命名空間 tooavoid 雜亂。

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

推送 hello 映像 tooyour 容器登錄中：

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>封裝具有 Yeoman hello Docker 映像
hello Service Fabric SDK for Linux 包含[Yeoman](http://yeoman.io/)產生器，可讓您輕鬆 toocreate 您的應用程式並加入容器映像。 讓我們使用具有單一的 Docker 容器的應用程式呼叫 Yeoman toocreate *SimpleContainerApp*。

toocreate Service Fabric 容器應用程式，開啟終端機視窗，然後執行`yo azuresfcontainer`。  

為應用程式命名 (例如 "mycontainer")。 

在容器登錄中的 hello 容器映像提供 hello 的 URL (例如，"")。 

此映像的工作負載進入點定義，因此需要 tooexplicitly 指定輸入的命令 （在 hello 的容器，將會保留在啟動之後執行的 hello 容器內執行的命令）。 

指定執行個體計數為 "1"。

![容器的 Service Fabric Yeoman 產生器][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>設定連接埠對應和容器存放庫驗證
您的容器化服務需要端點進行通訊。  現在，加入 hello 通訊協定、 連接埠和型別 tooan `Endpoint` hello ServiceManifest.xml 檔案中。 這個發行項，容器化的 hello 服務會接聽連接埠 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
提供 hello`UriScheme`暫存器會自動以 hello Service Fabric 命名服務的發現能力 hello 容器端點。 這篇文章的 hello 結尾會提供完整的 ServiceManifest.xml 範例檔案。 

藉由指定設定 hello 容器連接埠-主機連接埠對應`PortBinding`中的原則`ContainerHostPolicies`的 hello ApplicationManifest.xml 檔案。  這個發行項，`ContainerPort`為 80 （hello 容器中所指定的 hello Dockerfile 以公開連接埠 80） 和`EndpointRef`是"myserviceTypeEndpoint 」 （hello 端點 hello 服務資訊清單中定義）。  內送要求連接埠 4000 toohello 服務對應 tooport 80 hello 容器上。  如果您的容器需要 tooauthenticate 與私用儲存機制，然後新增`RepositoryCredentials`。  如本文中，新增 hello 帳戶名稱和密碼的 hello myregistry.azurecr.io 容器登錄中。 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>建置和封裝 hello Service Fabric 應用程式
hello 服務網狀架構 Yeoman 範本包括的組建指令碼[Gradle](https://gradle.org/)，而您可以使用從終端機 hello toobuild hello 應用程式。 toobuild 和套件 hello 應用程式，執行下列 hello:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>部署 hello 應用程式
建置 hello 應用程式之後，您可以部署使用 hello 服務網狀架構 CLI toohello 本機叢集。

Toohello 本機 Service Fabric 叢集連線。

```bash
sfctl cluster select --endpoint http://localhost:19080
```

使用 hello 安裝指令碼，提供在 hello 範本 toocopy hello 應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型，以及建立 hello 應用程式的執行個體。

```bash
./install.sh
```

開啟瀏覽器，並瀏覽 tooService Fabric 總管在 http://localhost:19080 總管 (hello 私用 ip 的 hello VM，如果在 Mac OS X 使用 Vagrant 取代 localhost)。 展開 [hello 應用程式] 節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。

連接 toohello 執行容器。  開啟網頁瀏覽器指向所傳回的連接埠 4000，例如"http://localhost:4000"toohello IP 位址。 您應該會看見 hello 標題"Hello World ！" 在 hello 瀏覽器中顯示。

![Hello World!][hello-world]

## <a name="clean-up"></a>清除
使用 hello 解除安裝指令碼提供 hello 範本 toodelete hello 應用程式執行個體中從 hello 本機開發叢集，並取消登錄 hello 應用程式類型。

```bash
./uninstall.sh
```

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
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>新增更多服務 tooan 現有應用程式

tooadd 另一個容器 tooan 建立服務應用程式已經使用 yeoman，執行下列步驟 hello:

1. 變更 hello 現有應用程式的根目錄 toohello。  例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。
2. 執行 `yo azuresfcontainer:AddService`

<a id="manually"></a>


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

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
