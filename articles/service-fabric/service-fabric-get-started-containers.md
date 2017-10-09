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
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="3232d-104">在 Windows 建立第一個 Service Fabric 容器應用程式</span><span class="sxs-lookup"><span data-stu-id="3232d-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3232d-105">Windows</span><span class="sxs-lookup"><span data-stu-id="3232d-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="3232d-106">Linux</span><span class="sxs-lookup"><span data-stu-id="3232d-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="3232d-107">Service Fabric 叢集上執行 Windows 容器中的現有應用程式不需要任何變更 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3232d-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="3232d-108">本文將指導您完成建立 Docker 映像包含 Python[酒瓶](http://flask.pocoo.org/)web 應用程式和部署 tooa Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="3232d-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="3232d-109">您也將透過 [Azure Container Registry](/azure/container-registry/) 共用容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="3232d-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="3232d-110">本文假設您對 Docker 有基本認識。</span><span class="sxs-lookup"><span data-stu-id="3232d-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="3232d-111">您可以透過讀取 hello 深入了解 Docker [Docker 概觀](https://docs.docker.com/engine/understanding-docker/)。</span><span class="sxs-lookup"><span data-stu-id="3232d-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3232d-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="3232d-112">Prerequisites</span></span>
<span data-ttu-id="3232d-113">執行下列項目的開發電腦︰</span><span class="sxs-lookup"><span data-stu-id="3232d-113">A development computer running:</span></span>
* <span data-ttu-id="3232d-114">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="3232d-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3232d-115">[Service Fabric SDK 和工具](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3232d-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="3232d-116">Docker for Windows。</span><span class="sxs-lookup"><span data-stu-id="3232d-116">Docker for Windows.</span></span>  <span data-ttu-id="3232d-117">[取得 Docker CE for Windows (穩定)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description)。</span><span class="sxs-lookup"><span data-stu-id="3232d-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="3232d-118">安裝及啟動 Docker hello 系統匣圖示上按一下滑鼠右鍵，然後選取後**切換 tooWindows 容器**。</span><span class="sxs-lookup"><span data-stu-id="3232d-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="3232d-119">這是根據 Windows 的必要的 toorun Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="3232d-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="3232d-120">有三個或更多節點在具有容器的 Windows Server 2016 上執行的 Windows 叢集 - [建立叢集](service-fabric-cluster-creation-via-portal.md)或[免費試用 Service Fabric](https://aka.ms/tryservicefabric)。</span><span class="sxs-lookup"><span data-stu-id="3232d-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="3232d-121">Azure Container Registry 中的登錄 - 在 Azure 訂用帳戶中[建立容器登錄](../container-registry/container-registry-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3232d-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="3232d-122">定義 hello Docker 容器</span><span class="sxs-lookup"><span data-stu-id="3232d-122">Define hello Docker container</span></span>
<span data-ttu-id="3232d-123">建置 hello 為基礎的映像[Python 的映像](https://hub.docker.com/_/python/)位於 Docker Hub。</span><span class="sxs-lookup"><span data-stu-id="3232d-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="3232d-124">在 Dockerfile 中定義您的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="3232d-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="3232d-125">hello Dockerfile 包含指示設定您的容器內的 hello 環境、 載入 hello 應用程式想 toorun，和對應的連接埠。</span><span class="sxs-lookup"><span data-stu-id="3232d-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="3232d-126">hello Dockerfile 是 hello 輸入的 toohello`docker build`命令，建立 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="3232d-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="3232d-127">建立空的目錄，並建立 hello 檔案*Dockerfile* （不含檔案副檔名）。</span><span class="sxs-lookup"><span data-stu-id="3232d-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="3232d-128">Hello 太之後加入*Dockerfile*並儲存變更：</span><span class="sxs-lookup"><span data-stu-id="3232d-128">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="3232d-129">讀取 hello[的 Dockerfile 參考](https://docs.docker.com/engine/reference/builder/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3232d-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="3232d-130">建立簡單 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3232d-130">Create a simple web application</span></span>
<span data-ttu-id="3232d-131">建立 Flask Web 應用程式，其會在連接埠 80 上接聽並傳回 "Hello World!"。</span><span class="sxs-lookup"><span data-stu-id="3232d-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="3232d-132">在 hello 相同的目錄中建立 hello 檔案*requirements.txt*。</span><span class="sxs-lookup"><span data-stu-id="3232d-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="3232d-133">新增下列 hello 和儲存您的變更：</span><span class="sxs-lookup"><span data-stu-id="3232d-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="3232d-134">也會建立 hello *app.py*檔案，然後加入下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3232d-134">Also create hello *app.py* file and add hello following:</span></span>

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
## <a name="build-hello-image"></a><span data-ttu-id="3232d-135">建立 hello 映像</span><span class="sxs-lookup"><span data-stu-id="3232d-135">Build hello image</span></span>
<span data-ttu-id="3232d-136">執行 hello`docker build`命令 toocreate hello 映像，執行您 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3232d-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="3232d-137">開啟 PowerShell 視窗並瀏覽包含 hello Dockerfile toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="3232d-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="3232d-138">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3232d-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="3232d-139">此組建 hello hello 指示使用 Dockerfile 中，在新的映像的命令命名 (-t 標記) hello 映像 」 helloworldapp"。</span><span class="sxs-lookup"><span data-stu-id="3232d-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="3232d-140">建置映像從 Docker Hub 提取的 hello 基底映像，並建立新的映像，將它新增 hello 基底映像之上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3232d-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="3232d-141">Hello 建置命令完成之後，請執行 hello`docker images`命令 toosee hello 新映像的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="3232d-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="3232d-142">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3232d-142">Run hello application locally</span></span>
<span data-ttu-id="3232d-143">請確認您的映像在本機，再將它推送 hello 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="3232d-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="3232d-144">執行 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="3232d-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="3232d-145">*名稱*提供名稱 toohello 執行容器 （而不是 hello 容器識別碼）。</span><span class="sxs-lookup"><span data-stu-id="3232d-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="3232d-146">Hello 容器會啟動一次，尋找其 IP 位址，以便您可以連接 tooyour 從瀏覽器執行容器：</span><span class="sxs-lookup"><span data-stu-id="3232d-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="3232d-147">連接 toohello 執行容器。</span><span class="sxs-lookup"><span data-stu-id="3232d-147">Connect toohello running container.</span></span>  <span data-ttu-id="3232d-148">開啟網頁瀏覽器指向 toohello 傳回 IP 位址，例如"http://172.31.194.61"。</span><span class="sxs-lookup"><span data-stu-id="3232d-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="3232d-149">您應該會看見 hello 標題"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="3232d-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="3232d-150">在 hello 瀏覽器中顯示。</span><span class="sxs-lookup"><span data-stu-id="3232d-150">display in hello browser.</span></span>

<span data-ttu-id="3232d-151">toostop 您執行的容器：</span><span class="sxs-lookup"><span data-stu-id="3232d-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="3232d-152">從開發電腦刪除 hello 容器：</span><span class="sxs-lookup"><span data-stu-id="3232d-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="3232d-153">推播 hello 映像 toohello 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="3232d-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="3232d-154">在您確認該 hello 容器會在開發電腦上執行之後，推送 hello 映像 tooyour 登錄 Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="3232d-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="3232d-155">執行``docker login``toolog tooyour 容器登錄中以在您[登錄認證](../container-registry/container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="3232d-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="3232d-156">hello 下列範例會傳遞 hello ID 和 Azure Active Directory 密碼[服務主體](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="3232d-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="3232d-157">例如，您可能已指派服務主體 tooyour 登錄所需自動化案例。</span><span class="sxs-lookup"><span data-stu-id="3232d-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="3232d-158">或者，您可以使用登錄使用者名稱和密碼進行登入。</span><span class="sxs-lookup"><span data-stu-id="3232d-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="3232d-159">hello 下列命令會建立標記或別名，hello 影像的完整的路徑 tooyour 登錄。</span><span class="sxs-lookup"><span data-stu-id="3232d-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="3232d-160">此範例中位置 hello hello 中的映像```samples```hello hello 登錄根目錄中的命名空間 tooavoid 雜亂。</span><span class="sxs-lookup"><span data-stu-id="3232d-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="3232d-161">推送 hello 映像 tooyour 容器登錄中：</span><span class="sxs-lookup"><span data-stu-id="3232d-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="3232d-162">Visual Studio 中建立 hello 容器化服務</span><span class="sxs-lookup"><span data-stu-id="3232d-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="3232d-163">hello Service Fabric SDK 和工具可提供服務範本 toohelp 建立容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="3232d-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="3232d-164">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3232d-164">Start Visual Studio.</span></span>  <span data-ttu-id="3232d-165">選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="3232d-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="3232d-166">選取 [Service Fabric 應用程式]，將它命名為 "MyFirstContainer"，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3232d-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="3232d-167">選取**客體容器**從 hello 清單**服務範本**。</span><span class="sxs-lookup"><span data-stu-id="3232d-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="3232d-168">在**映像名稱**輸入"myregistry.azurecr.io/samples/helloworldapp"，推送 tooyour 容器儲存機制的 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="3232d-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="3232d-169">指定服務的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3232d-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="3232d-170">設定通訊</span><span class="sxs-lookup"><span data-stu-id="3232d-170">Configure communication</span></span>
<span data-ttu-id="3232d-171">hello 容器化服務需要端點進行通訊。</span><span class="sxs-lookup"><span data-stu-id="3232d-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="3232d-172">新增`Endpoint`hello 通訊協定、 連接埠，與類型 toohello ServiceManifest.xml 檔案項目。</span><span class="sxs-lookup"><span data-stu-id="3232d-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="3232d-173">這個發行項，容器化的 hello 服務會接聽連接埠 8081。</span><span class="sxs-lookup"><span data-stu-id="3232d-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="3232d-174">在此範例中，會使用固定的連接埠 8081。</span><span class="sxs-lookup"><span data-stu-id="3232d-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="3232d-175">如果未不指定任何連接埠，則會選擇 hello 應用程式連接埠範圍的隨機連接埠。</span><span class="sxs-lookup"><span data-stu-id="3232d-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="3232d-176">藉由定義端點，Service Fabric 發行 hello 端點 toohello 命名服務。</span><span class="sxs-lookup"><span data-stu-id="3232d-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="3232d-177">Hello 叢集中執行的其他服務可以解決這個容器。</span><span class="sxs-lookup"><span data-stu-id="3232d-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="3232d-178">您也可以執行使用 hello 的容器-容器通訊[反向 proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="3232d-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="3232d-179">通訊是由提供 hello 反向 proxy HTTP 接聽連接埠和 hello 名稱要與 toocommunicate 視為環境變數的 hello 服務執行。</span><span class="sxs-lookup"><span data-stu-id="3232d-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="3232d-180">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="3232d-180">Configure and set environment variables</span></span>
<span data-ttu-id="3232d-181">環境變數可以指定每個程式碼封裝 hello 服務資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="3232d-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="3232d-182">所有服務都有這項功能，無論是部署為容器或處理程序或來賓可執行檔。</span><span class="sxs-lookup"><span data-stu-id="3232d-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="3232d-183">您可以覆寫資訊清單 hello 應用程式中的值，或做為應用程式參數的部署期間指定這些環境變數。</span><span class="sxs-lookup"><span data-stu-id="3232d-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="3232d-184">hello 下列服務資訊清單 XML 程式碼片段示範如何的範例程式碼封裝的 toospecify 環境變數：</span><span class="sxs-lookup"><span data-stu-id="3232d-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="3232d-185">這些環境變數會覆寫 hello 應用程式資訊清單中：</span><span class="sxs-lookup"><span data-stu-id="3232d-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="3232d-186">設定容器連接埠對主機連接埠對應，以及容器對容器探索</span><span class="sxs-lookup"><span data-stu-id="3232d-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="3232d-187">設定主機使用的連接埠 toocommunicate 與 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="3232d-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="3232d-188">hello 連接埠繫結對應 hello 的 hello 服務正在接聽連接埠內 hello 主機上的 hello 容器 tooa 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="3232d-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="3232d-189">新增`PortBinding`中的項目`ContainerHostPolicies`hello ApplicationManifest.xml 檔案項目。</span><span class="sxs-lookup"><span data-stu-id="3232d-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="3232d-190">這個發行項，`ContainerPort`為 80 （hello 容器中所指定的 hello Dockerfile 以公開連接埠 80） 和`EndpointRef`是"Guest1TypeEndpoint 」 (hello hello 服務資訊清單中預先定義的端點)。</span><span class="sxs-lookup"><span data-stu-id="3232d-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="3232d-191">內送要求連接埠 8081 toohello 服務對應 tooport 80 hello 容器上。</span><span class="sxs-lookup"><span data-stu-id="3232d-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="3232d-192">設定容器登錄驗證</span><span class="sxs-lookup"><span data-stu-id="3232d-192">Configure container registry authentication</span></span>
<span data-ttu-id="3232d-193">藉由新增設定容器登錄驗證`RepositoryCredentials`太`ContainerHostPolicies`的 hello ApplicationManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="3232d-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="3232d-194">加入 hello 帳戶和密碼 hello myregistry.azurecr.io 容器登錄中，可讓 hello 服務 toodownload hello 容器映像從 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3232d-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="3232d-195">我們建議您在使用已部署 tooall hello 叢集節點的加密憑證來加密 hello 儲存機制的密碼。</span><span class="sxs-lookup"><span data-stu-id="3232d-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="3232d-196">Service Fabric 部署 hello 服務封裝 toohello 叢集 hello 加密憑證時，使用的 toodecrypt hello 加密文字。</span><span class="sxs-lookup"><span data-stu-id="3232d-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="3232d-197">hello Invoke ServiceFabricEncryptText cmdlet 是針對 hello 密碼，它會加入 toohello ApplicationManifest.xml 檔案使用的 toocreate hello 加密文字。</span><span class="sxs-lookup"><span data-stu-id="3232d-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="3232d-198">hello 下列指令碼會建立新的自我簽署的憑證並將它匯出 tooa PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="3232d-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="3232d-199">hello 憑證匯入到現有的金鑰保存庫，然後再部署 toohello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="3232d-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

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
<span data-ttu-id="3232d-200">使用 hello hello 密碼加密[Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3232d-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="3232d-201">Hello 密碼取代 hello 加密文字傳回 hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet，並設定`PasswordEncrypted`太"，則為 true 」。</span><span class="sxs-lookup"><span data-stu-id="3232d-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="3232d-202">設定隔離模式</span><span class="sxs-lookup"><span data-stu-id="3232d-202">Configure isolation mode</span></span>
<span data-ttu-id="3232d-203">Windows 支援兩種容器隔離模式：分別為處理序和 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="3232d-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="3232d-204">Hello 處理序隔離模式中，所有的 hello 容器上執行 hello 相同主機電腦共用 hello 核心與 hello 主機。</span><span class="sxs-lookup"><span data-stu-id="3232d-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="3232d-205">Hello HYPER-V 隔離模式中，hello 核心會隔離每個 HYPER-V 容器與 hello 容器主機之間。</span><span class="sxs-lookup"><span data-stu-id="3232d-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="3232d-206">指定在 hello hello 隔離模式`ContainerHostPolicies`hello 應用程式資訊清單檔中的項目。</span><span class="sxs-lookup"><span data-stu-id="3232d-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="3232d-207">hello 隔離模式可指定為`process`， `hyperv`，和`default`。</span><span class="sxs-lookup"><span data-stu-id="3232d-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="3232d-208">hello 預設隔離模式預設太`process`Windows 伺服器上裝載，且預設值太`hyperv`Windows 10 主機上。</span><span class="sxs-lookup"><span data-stu-id="3232d-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="3232d-209">hello 下列程式碼片段示範如何指定 hello 應用程式資訊清單檔中的 hello 隔離模式。</span><span class="sxs-lookup"><span data-stu-id="3232d-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="3232d-210">設定資源控管</span><span class="sxs-lookup"><span data-stu-id="3232d-210">Configure resource governance</span></span>
<span data-ttu-id="3232d-211">[資源監管](service-fabric-resource-governance.md)限制的 hello hello 容器的資源可以使用 hello 主機。</span><span class="sxs-lookup"><span data-stu-id="3232d-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="3232d-212">hello`ResourceGovernancePolicy`元素，其 hello 應用程式資訊清單中指定，就是使用的 toodeclare 資源限制，服務程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="3232d-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="3232d-213">可以設定資源限制 hello 下列資源： 記憶體、 MemorySwap、 CpuShares （CPU 相對權數）、 MemoryReservationInMB，BlkioWeight （BlockIO 相對權數）。</span><span class="sxs-lookup"><span data-stu-id="3232d-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="3232d-214">在此範例中，服務套件 Guest1Pkg 會取得一個核心 hello 叢集節點放置的位置上。</span><span class="sxs-lookup"><span data-stu-id="3232d-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="3232d-215">記憶體限制是絕對的因此 hello 程式碼封裝是有限的 too1024 MB 的記憶體 （和 hello 相同的軟體保證保留）。</span><span class="sxs-lookup"><span data-stu-id="3232d-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="3232d-216">程式碼封裝 （容器或處理程序） 不能 tooallocate 記憶體超過此限制，而嘗試 toodo 因此會導致記憶體不足例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3232d-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="3232d-217">資源限制強制 toowork，所有的程式碼封裝在服務封裝內必須有指定記憶體限制。</span><span class="sxs-lookup"><span data-stu-id="3232d-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="3232d-218">部署 hello 容器應用程式</span><span class="sxs-lookup"><span data-stu-id="3232d-218">Deploy hello container application</span></span>
<span data-ttu-id="3232d-219">儲存所有變更，並建置 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3232d-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="3232d-220">toopublish 您的應用程式，以滑鼠右鍵按一下**MyFirstContainer**在方案總管，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="3232d-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="3232d-221">在**連接端點**，輸入 hello 叢集 hello 管理端點。</span><span class="sxs-lookup"><span data-stu-id="3232d-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="3232d-222">例如，"containercluster.westus2.cloudapp.azure.com:19000"。</span><span class="sxs-lookup"><span data-stu-id="3232d-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="3232d-223">您可以找到 hello 用戶端連接您的叢集在 hello hello 概觀刀鋒視窗中的端點[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3232d-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="3232d-224">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="3232d-224">Click **Publish**.</span></span>

<span data-ttu-id="3232d-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個 Web 型工具，可檢查和管理 Service Fabric 叢集中的應用程式與節點。</span><span class="sxs-lookup"><span data-stu-id="3232d-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="3232d-226">開啟瀏覽器和瀏覽 toohttp://containercluster.westus2.cloudapp.azure.com:19080/總管/並遵循 hello 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="3232d-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="3232d-227">hello 應用程式部署，而處於錯誤狀態 （這可能需要一些時間，視 hello 映像大小而定） hello 叢集節點上下載 hello 映像之前：![錯誤][1]</span><span class="sxs-lookup"><span data-stu-id="3232d-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="3232d-228">hello 應用程式時，準備在```Ready```狀態：![準備][2]</span><span class="sxs-lookup"><span data-stu-id="3232d-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="3232d-229">開啟瀏覽器，並瀏覽 toohttp://containercluster.westus2.cloudapp.azure.com:8081。</span><span class="sxs-lookup"><span data-stu-id="3232d-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="3232d-230">您應該會看見 hello 標題"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="3232d-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="3232d-231">在 hello 瀏覽器中顯示。</span><span class="sxs-lookup"><span data-stu-id="3232d-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="3232d-232">清除</span><span class="sxs-lookup"><span data-stu-id="3232d-232">Clean up</span></span>
<span data-ttu-id="3232d-233">您可以繼續 tooincur 費用 hello 叢集正在執行，請考慮[刪除您的叢集](service-fabric-get-started-azure-cluster.md#remove-the-cluster)。</span><span class="sxs-lookup"><span data-stu-id="3232d-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="3232d-234">[合作對象叢集](http://tryazureservicefabric.westus.cloudapp.azure.com/)會在幾個小時後自動刪除。</span><span class="sxs-lookup"><span data-stu-id="3232d-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="3232d-235">Hello 映像 toohello 容器登錄中是您推送之後您可以從開發電腦刪除 hello 本機映像：</span><span class="sxs-lookup"><span data-stu-id="3232d-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="3232d-236">完整範例 Service Fabric 應用程式和服務資訊清單</span><span class="sxs-lookup"><span data-stu-id="3232d-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="3232d-237">以下是 hello 完整服務以及在本文中使用的應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="3232d-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="3232d-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="3232d-238">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="3232d-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="3232d-239">ApplicationManifest.xml</span></span>
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

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="3232d-240">在容器被迫終止前設定時間間隔</span><span class="sxs-lookup"><span data-stu-id="3232d-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="3232d-241">Hello 服務刪除 （或移動 tooanother 節點） 啟動後移除 hello 容器之前，您可以設定 hello 執行階段 toowait 的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="3232d-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="3232d-242">設定 hello 時間間隔傳送嗨`docker stop <time in seconds>`命令 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="3232d-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="3232d-243">如需更多詳細資訊，請參閱 [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)。</span><span class="sxs-lookup"><span data-stu-id="3232d-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="3232d-244">hello 下指定 hello 時間間隔 toowait `Hosting` > 一節。</span><span class="sxs-lookup"><span data-stu-id="3232d-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="3232d-245">hello 下列叢集資訊清單的程式碼片段顯示如何 tooset hello 等待間隔：</span><span class="sxs-lookup"><span data-stu-id="3232d-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="3232d-246">hello 預設時間間隔是否設定 too10 秒。</span><span class="sxs-lookup"><span data-stu-id="3232d-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="3232d-247">此組態是動態的因為組態只能升級 hello 叢集更新 hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="3232d-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="3232d-248">設定 hello 執行階段 tooremove 未使用的容器映像</span><span class="sxs-lookup"><span data-stu-id="3232d-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="3232d-249">您可以設定 hello Service Fabric 叢集 tooremove 從 hello 節點未使用的容器映像。</span><span class="sxs-lookup"><span data-stu-id="3232d-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="3232d-250">此設定可讓磁碟空間 toobe 捕捉如果 hello 節點上有太多的容器映像。</span><span class="sxs-lookup"><span data-stu-id="3232d-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="3232d-251">tooenable 此功能，更新 hello`Hosting`區段 hello 叢集資訊清單中，hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="3232d-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="3232d-252">針對不應該刪除的映像，您可以指定下 hello 它們`ContainerImagesToSkip`參數。</span><span class="sxs-lookup"><span data-stu-id="3232d-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="3232d-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3232d-253">Next steps</span></span>
* <span data-ttu-id="3232d-254">深入了解如何[在 Service Fabric 上執行容器](service-fabric-containers-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3232d-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="3232d-255">讀取 hello[部署.NET 應用程式容器中的](service-fabric-host-app-in-a-container.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="3232d-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="3232d-256">深入了解 hello Service Fabric[應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="3232d-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="3232d-257">簽出 hello [Service Fabric 程式碼範例容器](https://github.com/Azure-Samples/service-fabric-dotnet-containers)GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="3232d-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
