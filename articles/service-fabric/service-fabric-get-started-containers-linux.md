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
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="986bb-104">在 Linux 建立第一個 Service Fabric 容器應用程式</span><span class="sxs-lookup"><span data-stu-id="986bb-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="986bb-105">Windows</span><span class="sxs-lookup"><span data-stu-id="986bb-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="986bb-106">Linux</span><span class="sxs-lookup"><span data-stu-id="986bb-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="986bb-107">Service Fabric 叢集上執行 Linux 容器中的現有應用程式不需要任何變更 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="986bb-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="986bb-108">本文將指導您完成建立 Docker 映像包含 Python[酒瓶](http://flask.pocoo.org/)web 應用程式和部署 tooa Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="986bb-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="986bb-109">您也將透過 [Azure Container Registry](/azure/container-registry/) 共用容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="986bb-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="986bb-110">本文假設您對 Docker 有基本認識。</span><span class="sxs-lookup"><span data-stu-id="986bb-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="986bb-111">您可以透過讀取 hello 深入了解 Docker [Docker 概觀](https://docs.docker.com/engine/understanding-docker/)。</span><span class="sxs-lookup"><span data-stu-id="986bb-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="986bb-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="986bb-112">Prerequisites</span></span>
* <span data-ttu-id="986bb-113">執行下列項目的開發電腦︰</span><span class="sxs-lookup"><span data-stu-id="986bb-113">A development computer running:</span></span>
  * <span data-ttu-id="986bb-114">[Service Fabric SDK 和工具](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="986bb-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="986bb-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="986bb-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="986bb-116">Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="986bb-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="986bb-117">Azure Container Registry 中的登錄 - 在 Azure 訂用帳戶中[建立容器登錄](../container-registry/container-registry-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="986bb-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="986bb-118">定義 hello Docker 容器</span><span class="sxs-lookup"><span data-stu-id="986bb-118">Define hello Docker container</span></span>
<span data-ttu-id="986bb-119">建置 hello 為基礎的映像[Python 的映像](https://hub.docker.com/_/python/)位於 Docker Hub。</span><span class="sxs-lookup"><span data-stu-id="986bb-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="986bb-120">在 Dockerfile 中定義您的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="986bb-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="986bb-121">hello Dockerfile 包含指示設定您的容器內的 hello 環境、 載入 hello 應用程式想 toorun，和對應的連接埠。</span><span class="sxs-lookup"><span data-stu-id="986bb-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="986bb-122">hello Dockerfile 是 hello 輸入的 toohello`docker build`命令，建立 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="986bb-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="986bb-123">建立空的目錄，並建立 hello 檔案*Dockerfile* （不含檔案副檔名）。</span><span class="sxs-lookup"><span data-stu-id="986bb-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="986bb-124">Hello 太之後加入*Dockerfile*並儲存變更：</span><span class="sxs-lookup"><span data-stu-id="986bb-124">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="986bb-125">讀取 hello[的 Dockerfile 參考](https://docs.docker.com/engine/reference/builder/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="986bb-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="986bb-126">建立簡單 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="986bb-126">Create a simple web application</span></span>
<span data-ttu-id="986bb-127">建立 Flask Web 應用程式，其會在連接埠 80 上接聽並傳回 "Hello World!"。</span><span class="sxs-lookup"><span data-stu-id="986bb-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="986bb-128">在 hello 相同的目錄中建立 hello 檔案*requirements.txt*。</span><span class="sxs-lookup"><span data-stu-id="986bb-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="986bb-129">新增下列 hello 和儲存您的變更：</span><span class="sxs-lookup"><span data-stu-id="986bb-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="986bb-130">也會建立 hello *app.py*檔案，然後加入下列 hello:</span><span class="sxs-lookup"><span data-stu-id="986bb-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="986bb-131">建立 hello 映像</span><span class="sxs-lookup"><span data-stu-id="986bb-131">Build hello image</span></span>
<span data-ttu-id="986bb-132">執行 hello`docker build`命令 toocreate hello 映像，執行您 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="986bb-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="986bb-133">開啟 PowerShell 視窗並瀏覽過*c:\temp\helloworldapp*。</span><span class="sxs-lookup"><span data-stu-id="986bb-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="986bb-134">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="986bb-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="986bb-135">此組建 hello hello 指示使用 Dockerfile 中，在新的映像的命令命名 (-t 標記) hello 映像 」 helloworldapp"。</span><span class="sxs-lookup"><span data-stu-id="986bb-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="986bb-136">建置映像從 Docker Hub 提取的 hello 基底映像，並建立新的映像，將它新增 hello 基底映像之上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="986bb-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="986bb-137">Hello 建置命令完成之後，請執行 hello`docker images`命令 toosee hello 新映像的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="986bb-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="986bb-138">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="986bb-138">Run hello application locally</span></span>
<span data-ttu-id="986bb-139">請確認您容器化應用程式執行本機之前將它推送 hello 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="986bb-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="986bb-140">執行 hello 應用程式，對應您的電腦連接埠 4000 toohello 容器的公開連接埠 80:</span><span class="sxs-lookup"><span data-stu-id="986bb-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="986bb-141">*名稱*提供名稱 toohello 執行容器 （而不是 hello 容器識別碼）。</span><span class="sxs-lookup"><span data-stu-id="986bb-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="986bb-142">連接 toohello 執行容器。</span><span class="sxs-lookup"><span data-stu-id="986bb-142">Connect toohello running container.</span></span>  <span data-ttu-id="986bb-143">開啟網頁瀏覽器指向所傳回的連接埠 4000，例如"http://localhost:4000"toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="986bb-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="986bb-144">您應該會看見 hello 標題"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="986bb-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="986bb-145">在 hello 瀏覽器中顯示。</span><span class="sxs-lookup"><span data-stu-id="986bb-145">display in hello browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="986bb-147">toostop 您執行的容器：</span><span class="sxs-lookup"><span data-stu-id="986bb-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="986bb-148">從開發電腦刪除 hello 容器：</span><span class="sxs-lookup"><span data-stu-id="986bb-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="986bb-149">推播 hello 映像 toohello 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="986bb-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="986bb-150">確認在 Docker 中執行 hello 應用程式後，推送 hello 映像 tooyour 登錄 Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="986bb-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="986bb-151">執行`docker login`toolog tooyour 容器登錄中以在您[登錄認證](../container-registry/container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="986bb-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="986bb-152">hello 下列範例會傳遞 hello ID 和 Azure Active Directory 密碼[服務主體](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="986bb-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="986bb-153">例如，您可能已指派服務主體 tooyour 登錄所需自動化案例。</span><span class="sxs-lookup"><span data-stu-id="986bb-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="986bb-154">或者，您可以使用登錄使用者名稱和密碼進行登入。</span><span class="sxs-lookup"><span data-stu-id="986bb-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="986bb-155">hello 下列命令會建立標記或別名，hello 影像的完整的路徑 tooyour 登錄。</span><span class="sxs-lookup"><span data-stu-id="986bb-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="986bb-156">此範例中位置 hello hello 中的映像`samples`hello hello 登錄根目錄中的命名空間 tooavoid 雜亂。</span><span class="sxs-lookup"><span data-stu-id="986bb-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="986bb-157">推送 hello 映像 tooyour 容器登錄中：</span><span class="sxs-lookup"><span data-stu-id="986bb-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="986bb-158">封裝具有 Yeoman hello Docker 映像</span><span class="sxs-lookup"><span data-stu-id="986bb-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="986bb-159">hello Service Fabric SDK for Linux 包含[Yeoman](http://yeoman.io/)產生器，可讓您輕鬆 toocreate 您的應用程式並加入容器映像。</span><span class="sxs-lookup"><span data-stu-id="986bb-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="986bb-160">讓我們使用具有單一的 Docker 容器的應用程式呼叫 Yeoman toocreate *SimpleContainerApp*。</span><span class="sxs-lookup"><span data-stu-id="986bb-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="986bb-161">toocreate Service Fabric 容器應用程式，開啟終端機視窗，然後執行`yo azuresfcontainer`。</span><span class="sxs-lookup"><span data-stu-id="986bb-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="986bb-162">為應用程式命名 (例如 "mycontainer")。</span><span class="sxs-lookup"><span data-stu-id="986bb-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="986bb-163">在容器登錄中的 hello 容器映像提供 hello 的 URL (例如，"")。</span><span class="sxs-lookup"><span data-stu-id="986bb-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="986bb-164">此映像的工作負載進入點定義，因此需要 tooexplicitly 指定輸入的命令 （在 hello 的容器，將會保留在啟動之後執行的 hello 容器內執行的命令）。</span><span class="sxs-lookup"><span data-stu-id="986bb-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="986bb-165">指定執行個體計數為 "1"。</span><span class="sxs-lookup"><span data-stu-id="986bb-165">Specify an instance count of "1".</span></span>

![容器的 Service Fabric Yeoman 產生器][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="986bb-167">設定連接埠對應和容器存放庫驗證</span><span class="sxs-lookup"><span data-stu-id="986bb-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="986bb-168">您的容器化服務需要端點進行通訊。</span><span class="sxs-lookup"><span data-stu-id="986bb-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="986bb-169">現在，加入 hello 通訊協定、 連接埠和型別 tooan `Endpoint` hello ServiceManifest.xml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="986bb-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="986bb-170">這個發行項，容器化的 hello 服務會接聽連接埠 4000:</span><span class="sxs-lookup"><span data-stu-id="986bb-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="986bb-171">提供 hello`UriScheme`暫存器會自動以 hello Service Fabric 命名服務的發現能力 hello 容器端點。</span><span class="sxs-lookup"><span data-stu-id="986bb-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="986bb-172">這篇文章的 hello 結尾會提供完整的 ServiceManifest.xml 範例檔案。</span><span class="sxs-lookup"><span data-stu-id="986bb-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="986bb-173">藉由指定設定 hello 容器連接埠-主機連接埠對應`PortBinding`中的原則`ContainerHostPolicies`的 hello ApplicationManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="986bb-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="986bb-174">這個發行項，`ContainerPort`為 80 （hello 容器中所指定的 hello Dockerfile 以公開連接埠 80） 和`EndpointRef`是"myserviceTypeEndpoint 」 （hello 端點 hello 服務資訊清單中定義）。</span><span class="sxs-lookup"><span data-stu-id="986bb-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="986bb-175">內送要求連接埠 4000 toohello 服務對應 tooport 80 hello 容器上。</span><span class="sxs-lookup"><span data-stu-id="986bb-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="986bb-176">如果您的容器需要 tooauthenticate 與私用儲存機制，然後新增`RepositoryCredentials`。</span><span class="sxs-lookup"><span data-stu-id="986bb-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="986bb-177">如本文中，新增 hello 帳戶名稱和密碼的 hello myregistry.azurecr.io 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="986bb-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="986bb-178">建置和封裝 hello Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="986bb-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="986bb-179">hello 服務網狀架構 Yeoman 範本包括的組建指令碼[Gradle](https://gradle.org/)，而您可以使用從終端機 hello toobuild hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="986bb-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="986bb-180">toobuild 和套件 hello 應用程式，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="986bb-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="986bb-181">部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="986bb-181">Deploy hello application</span></span>
<span data-ttu-id="986bb-182">建置 hello 應用程式之後，您可以部署使用 hello 服務網狀架構 CLI toohello 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="986bb-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="986bb-183">Toohello 本機 Service Fabric 叢集連線。</span><span class="sxs-lookup"><span data-stu-id="986bb-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="986bb-184">使用 hello 安裝指令碼，提供在 hello 範本 toocopy hello 應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型，以及建立 hello 應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="986bb-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="986bb-185">開啟瀏覽器，並瀏覽 tooService Fabric 總管在 http://localhost:19080 總管 (hello 私用 ip 的 hello VM，如果在 Mac OS X 使用 Vagrant 取代 localhost)。</span><span class="sxs-lookup"><span data-stu-id="986bb-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="986bb-186">展開 [hello 應用程式] 節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="986bb-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="986bb-187">連接 toohello 執行容器。</span><span class="sxs-lookup"><span data-stu-id="986bb-187">Connect toohello running container.</span></span>  <span data-ttu-id="986bb-188">開啟網頁瀏覽器指向所傳回的連接埠 4000，例如"http://localhost:4000"toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="986bb-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="986bb-189">您應該會看見 hello 標題"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="986bb-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="986bb-190">在 hello 瀏覽器中顯示。</span><span class="sxs-lookup"><span data-stu-id="986bb-190">display in hello browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="986bb-192">清除</span><span class="sxs-lookup"><span data-stu-id="986bb-192">Clean up</span></span>
<span data-ttu-id="986bb-193">使用 hello 解除安裝指令碼提供 hello 範本 toodelete hello 應用程式執行個體中從 hello 本機開發叢集，並取消登錄 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="986bb-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="986bb-194">Hello 映像 toohello 容器登錄中是您推送之後您可以從開發電腦刪除 hello 本機映像：</span><span class="sxs-lookup"><span data-stu-id="986bb-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="986bb-195">完整範例 Service Fabric 應用程式和服務資訊清單</span><span class="sxs-lookup"><span data-stu-id="986bb-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="986bb-196">以下是 hello 完整服務以及在本文中使用的應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="986bb-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="986bb-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="986bb-197">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="986bb-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="986bb-198">ApplicationManifest.xml</span></span>
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
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="986bb-199">新增更多服務 tooan 現有應用程式</span><span class="sxs-lookup"><span data-stu-id="986bb-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="986bb-200">tooadd 另一個容器 tooan 建立服務應用程式已經使用 yeoman，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="986bb-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="986bb-201">變更 hello 現有應用程式的根目錄 toohello。</span><span class="sxs-lookup"><span data-stu-id="986bb-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="986bb-202">例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="986bb-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="986bb-203">執行 `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="986bb-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="986bb-204">在容器被迫終止前設定時間間隔</span><span class="sxs-lookup"><span data-stu-id="986bb-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="986bb-205">Hello 服務刪除 （或移動 tooanother 節點） 啟動後移除 hello 容器之前，您可以設定 hello 執行階段 toowait 的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="986bb-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="986bb-206">設定 hello 時間間隔傳送嗨`docker stop <time in seconds>`命令 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="986bb-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="986bb-207">如需更多詳細資訊，請參閱 [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)。</span><span class="sxs-lookup"><span data-stu-id="986bb-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="986bb-208">hello 下指定 hello 時間間隔 toowait `Hosting` > 一節。</span><span class="sxs-lookup"><span data-stu-id="986bb-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="986bb-209">hello 下列叢集資訊清單的程式碼片段顯示如何 tooset hello 等待間隔：</span><span class="sxs-lookup"><span data-stu-id="986bb-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="986bb-210">hello 預設時間間隔是否設定 too10 秒。</span><span class="sxs-lookup"><span data-stu-id="986bb-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="986bb-211">此組態是動態的因為組態只能升級 hello 叢集更新 hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="986bb-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="986bb-212">設定 hello 執行階段 tooremove 未使用的容器映像</span><span class="sxs-lookup"><span data-stu-id="986bb-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="986bb-213">您可以設定 hello Service Fabric 叢集 tooremove 從 hello 節點未使用的容器映像。</span><span class="sxs-lookup"><span data-stu-id="986bb-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="986bb-214">此設定可讓磁碟空間 toobe 捕捉如果 hello 節點上有太多的容器映像。</span><span class="sxs-lookup"><span data-stu-id="986bb-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="986bb-215">tooenable 此功能，更新 hello`Hosting`區段 hello 叢集資訊清單中，hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="986bb-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="986bb-216">針對不應該刪除的映像，您可以指定下 hello 它們`ContainerImagesToSkip`參數。</span><span class="sxs-lookup"><span data-stu-id="986bb-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="986bb-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="986bb-217">Next steps</span></span>
* <span data-ttu-id="986bb-218">深入了解如何[在 Service Fabric 上執行容器](service-fabric-containers-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="986bb-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="986bb-219">讀取 hello[部署.NET 應用程式容器中的](service-fabric-host-app-in-a-container.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="986bb-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="986bb-220">深入了解 hello Service Fabric[應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="986bb-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="986bb-221">簽出 hello [Service Fabric 程式碼範例容器](https://github.com/Azure-Samples/service-fabric-dotnet-containers)GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="986bb-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
