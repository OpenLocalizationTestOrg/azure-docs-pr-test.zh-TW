---
title: "建立 Azure Service Fabric 容器應用程式 | Microsoft Docs"
description: "在 Azure Service Fabric 上建立第一個 Windows 容器應用程式。  使用 Python 應用程式建置 Docker 映像、將映像推送到容器登錄，建置和部署 Service Fabric 容器應用程式。"
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
ms.openlocfilehash: 025bde02b3f342ec3399d51819d1fa8a91f11374
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="da75c-104">在 Windows 建立第一個 Service Fabric 容器應用程式</span><span class="sxs-lookup"><span data-stu-id="da75c-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da75c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="da75c-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="da75c-106">Linux</span><span class="sxs-lookup"><span data-stu-id="da75c-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="da75c-107">在 Service Fabric 叢集上的 Windows 容器中執行現有的應用程式，不需要變更您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da75c-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="da75c-108">本文會逐步引導您建立包含 Python [Flask](http://flask.pocoo.org/) Web 應用程式的 Docker 映像，並將它部署到 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="da75c-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="da75c-109">您也將透過 [Azure Container Registry](/azure/container-registry/) 共用容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="da75c-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="da75c-110">本文假設您對 Docker 有基本認識。</span><span class="sxs-lookup"><span data-stu-id="da75c-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="da75c-111">您可藉由閱讀 [Docker 概觀](https://docs.docker.com/engine/understanding-docker/)來了解 Docker。</span><span class="sxs-lookup"><span data-stu-id="da75c-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da75c-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="da75c-112">Prerequisites</span></span>
<span data-ttu-id="da75c-113">執行下列項目的開發電腦︰</span><span class="sxs-lookup"><span data-stu-id="da75c-113">A development computer running:</span></span>
* <span data-ttu-id="da75c-114">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="da75c-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="da75c-115">[Service Fabric SDK 和工具](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="da75c-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="da75c-116">Docker for Windows。</span><span class="sxs-lookup"><span data-stu-id="da75c-116">Docker for Windows.</span></span>  <span data-ttu-id="da75c-117">[取得 Docker CE for Windows (穩定)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description)。</span><span class="sxs-lookup"><span data-stu-id="da75c-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="da75c-118">安裝並啟動 Docker 之後，以滑鼠右鍵按一下系統匣圖示，然後選取 [切換至 Windows 容器]。</span><span class="sxs-lookup"><span data-stu-id="da75c-118">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="da75c-119">這是執行以 Windows 為基礎的 Docker 映像時的必要動作。</span><span class="sxs-lookup"><span data-stu-id="da75c-119">This is required to run Docker images based on Windows.</span></span>

<span data-ttu-id="da75c-120">有三個或更多節點在具有容器的 Windows Server 2016 上執行的 Windows 叢集 - [建立叢集](service-fabric-cluster-creation-via-portal.md)或[免費試用 Service Fabric](https://aka.ms/tryservicefabric)。</span><span class="sxs-lookup"><span data-stu-id="da75c-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="da75c-121">Azure Container Registry 中的登錄 - 在 Azure 訂用帳戶中[建立容器登錄](../container-registry/container-registry-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="da75c-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-the-docker-container"></a><span data-ttu-id="da75c-122">定義 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="da75c-122">Define the Docker container</span></span>
<span data-ttu-id="da75c-123">根據位於 Docker 中樞的 [Python 映像](https://hub.docker.com/_/python/)建立映像。</span><span class="sxs-lookup"><span data-stu-id="da75c-123">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="da75c-124">在 Dockerfile 中定義您的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="da75c-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="da75c-125">Dockerfile 包含下列相關指示：設定您容器內的環境、載入您要執行的應用程式，以及對應連接埠。</span><span class="sxs-lookup"><span data-stu-id="da75c-125">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="da75c-126">Dockerfile 是 `docker build` 命令的輸入，該命令可建立映像。</span><span class="sxs-lookup"><span data-stu-id="da75c-126">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="da75c-127">建立空的目錄並建立 Dockerfile 檔案 (沒有副檔名)。</span><span class="sxs-lookup"><span data-stu-id="da75c-127">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="da75c-128">將下列內容新增至 Dockerfile 並儲存變更：</span><span class="sxs-lookup"><span data-stu-id="da75c-128">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="da75c-129">如需詳細資訊，請參閱 [Dockerfile 參考](https://docs.docker.com/engine/reference/builder/)。</span><span class="sxs-lookup"><span data-stu-id="da75c-129">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="da75c-130">建立簡單 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="da75c-130">Create a simple web application</span></span>
<span data-ttu-id="da75c-131">建立 Flask Web 應用程式，其會在連接埠 80 上接聽並傳回 "Hello World!"。</span><span class="sxs-lookup"><span data-stu-id="da75c-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="da75c-132">在相同的目錄中，建立 requirements.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="da75c-132">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="da75c-133">新增下列內容並儲存變更：</span><span class="sxs-lookup"><span data-stu-id="da75c-133">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="da75c-134">此外，建立 app.py 檔案並新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="da75c-134">Also create the *app.py* file and add the following:</span></span>

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
## <a name="build-the-image"></a><span data-ttu-id="da75c-135">建立映像</span><span class="sxs-lookup"><span data-stu-id="da75c-135">Build the image</span></span>
<span data-ttu-id="da75c-136">執行 `docker build` 命令來建立可執行 Web 應用程式的映像。</span><span class="sxs-lookup"><span data-stu-id="da75c-136">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="da75c-137">開啟 PowerShell 視窗，然後瀏覽至包含 Dockerfile 的目錄。</span><span class="sxs-lookup"><span data-stu-id="da75c-137">Open a PowerShell window and navigate to the directory containing the Dockerfile.</span></span> <span data-ttu-id="da75c-138">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="da75c-138">Run the following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="da75c-139">此命令會使用 Dockerfile 中的指示建立新映像，將此映像命名 (-t 標記) 為 "helloworldapp"。</span><span class="sxs-lookup"><span data-stu-id="da75c-139">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="da75c-140">建置映像時，會從 Docker 中樞向下提取基底映像，並根據基底映像建立可新增應用程式的新映像。</span><span class="sxs-lookup"><span data-stu-id="da75c-140">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="da75c-141">建置命令完成後，執行 `docker images` 命令以查看新映像的資訊︰</span><span class="sxs-lookup"><span data-stu-id="da75c-141">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="da75c-142">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="da75c-142">Run the application locally</span></span>
<span data-ttu-id="da75c-143">先確認您的映像在本機，再將它推送至容器登錄。</span><span class="sxs-lookup"><span data-stu-id="da75c-143">Verify your image locally before pushing it the container registry.</span></span>  

<span data-ttu-id="da75c-144">執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="da75c-144">Run the application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="da75c-145">name - 提供執行中容器的名稱 (而不是容器識別碼)。</span><span class="sxs-lookup"><span data-stu-id="da75c-145">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="da75c-146">容器啟動後，尋找其 IP 位址，以便您從瀏覽器連線到執行中的容器︰</span><span class="sxs-lookup"><span data-stu-id="da75c-146">Once the container starts, find its IP address so that you can connect to your running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="da75c-147">連線到執行中的容器。</span><span class="sxs-lookup"><span data-stu-id="da75c-147">Connect to the running container.</span></span>  <span data-ttu-id="da75c-148">開啟 Web 瀏覽器並指向傳回的 IP 位址，例如 " http://172.31.194.61 "。</span><span class="sxs-lookup"><span data-stu-id="da75c-148">Open a web browser pointing to the IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="da75c-149">您應該會看到 "Hello World!" 標題</span><span class="sxs-lookup"><span data-stu-id="da75c-149">You should see the heading "Hello World!"</span></span> <span data-ttu-id="da75c-150">顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="da75c-150">display in the browser.</span></span>

<span data-ttu-id="da75c-151">若要停止您的容器，請執行︰</span><span class="sxs-lookup"><span data-stu-id="da75c-151">To stop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="da75c-152">從您的開發電腦刪除容器：</span><span class="sxs-lookup"><span data-stu-id="da75c-152">Delete the container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="da75c-153">將映像推送至容器登錄</span><span class="sxs-lookup"><span data-stu-id="da75c-153">Push the image to the container registry</span></span>
<span data-ttu-id="da75c-154">確認容器在開發電腦上執行後，將映像發送到 Azure Container Registry 中您的登錄。</span><span class="sxs-lookup"><span data-stu-id="da75c-154">After you verify that the container runs on your development machine, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="da75c-155">使用您的[登錄認證](../container-registry/container-registry-authentication.md)執行 ``docker login`` 登入容器登錄庫。</span><span class="sxs-lookup"><span data-stu-id="da75c-155">Run ``docker login`` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="da75c-156">下列範例會傳遞 Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md) 的識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="da75c-156">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="da75c-157">例如，您可能基於自動化案例已指派服務主體到您的登錄庫。</span><span class="sxs-lookup"><span data-stu-id="da75c-157">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span> <span data-ttu-id="da75c-158">或者，您可以使用登錄使用者名稱和密碼進行登入。</span><span class="sxs-lookup"><span data-stu-id="da75c-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="da75c-159">下列命令會建立映像的標籤或別名，包含登錄的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="da75c-159">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="da75c-160">這個範例會指定 ```samples``` 命名空間中的映像，以避免登錄根目錄雜亂。</span><span class="sxs-lookup"><span data-stu-id="da75c-160">This example places the image in the ```samples``` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="da75c-161">將映像推送至容器登錄：</span><span class="sxs-lookup"><span data-stu-id="da75c-161">Push the image to your container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-the-containerized-service-in-visual-studio"></a><span data-ttu-id="da75c-162">在 Visual Studio 中建立容器化服務</span><span class="sxs-lookup"><span data-stu-id="da75c-162">Create the containerized service in Visual Studio</span></span>
<span data-ttu-id="da75c-163">Service Fabric SDK 和工具會提供一個服務範本，協助您建立容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="da75c-163">The Service Fabric SDK and tools provide a service template to help you create a containerized application.</span></span>

1. <span data-ttu-id="da75c-164">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="da75c-164">Start Visual Studio.</span></span>  <span data-ttu-id="da75c-165">選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="da75c-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="da75c-166">選取 [Service Fabric 應用程式]，將它命名為 "MyFirstContainer"，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="da75c-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="da75c-167">從 [服務範本] 的清單中選取 [來賓容器]。</span><span class="sxs-lookup"><span data-stu-id="da75c-167">Select **Guest Container** from the list of **service templates**.</span></span>
4. <span data-ttu-id="da75c-168">在 [映像名稱] 中輸入 "myregistry.azurecr.io/samples/helloworldapp"，也就是您推送至容器存放庫的映像。</span><span class="sxs-lookup"><span data-stu-id="da75c-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", the image you pushed to your container repository.</span></span>
5. <span data-ttu-id="da75c-169">指定服務的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="da75c-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="da75c-170">設定通訊</span><span class="sxs-lookup"><span data-stu-id="da75c-170">Configure communication</span></span>
<span data-ttu-id="da75c-171">容器化服務需要端點進行通訊。</span><span class="sxs-lookup"><span data-stu-id="da75c-171">The containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="da75c-172">將 `Endpoint` 元素以及通訊協定、連接埠和類型新增至 ServiceManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="da75c-172">Add an `Endpoint` element with the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="da75c-173">在本文中，容器化服務會接聽連接埠 8081。</span><span class="sxs-lookup"><span data-stu-id="da75c-173">For this article, the containerized service listens on port 8081.</span></span>  <span data-ttu-id="da75c-174">在此範例中，會使用固定的連接埠 8081。</span><span class="sxs-lookup"><span data-stu-id="da75c-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="da75c-175">若未指定連接埠，則會從應用程式連接埠範圍中隨機選擇連接埠。</span><span class="sxs-lookup"><span data-stu-id="da75c-175">If no port is specified, a random port from the application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="da75c-176">透過定義端點，Service Fabric 會將端點發佈至名稱服務。</span><span class="sxs-lookup"><span data-stu-id="da75c-176">By defining an endpoint, Service Fabric publishes the endpoint to the Naming service.</span></span>  <span data-ttu-id="da75c-177">在叢集中執行的其他服務可以解析容器。</span><span class="sxs-lookup"><span data-stu-id="da75c-177">Other services running in the cluster can resolve this container.</span></span>  <span data-ttu-id="da75c-178">您也可以使用[反向 Proxy](service-fabric-reverseproxy.md)來執行容器對容器通訊。</span><span class="sxs-lookup"><span data-stu-id="da75c-178">You can also perform container-to-container communication using the [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="da75c-179">將 HTTP 接聽連接埠和您想要與之通訊的服務名稱提供給反向 Proxy，並將這些都設為環境變數，便可進行通訊。</span><span class="sxs-lookup"><span data-stu-id="da75c-179">Communication is performed by providing the reverse proxy HTTP listening port and the name of the services that you want to communicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="da75c-180">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="da75c-180">Configure and set environment variables</span></span>
<span data-ttu-id="da75c-181">可以為服務資訊清單中的每個程式碼套件指定環境變數。</span><span class="sxs-lookup"><span data-stu-id="da75c-181">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="da75c-182">所有服務都有這項功能，無論是部署為容器或處理程序或來賓可執行檔。</span><span class="sxs-lookup"><span data-stu-id="da75c-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="da75c-183">您可以覆寫應用程式資訊清單中環境變數的值，或在部署期間將它們指定為應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="da75c-183">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="da75c-184">下列服務資訊清單 XML 程式碼片段示範如何指定程式碼封裝的環境變數：</span><span class="sxs-lookup"><span data-stu-id="da75c-184">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="da75c-185">在應用程式資訊清單中可以覆寫這些環境變數︰</span><span class="sxs-lookup"><span data-stu-id="da75c-185">These environment variables can be overridden in the application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="da75c-186">設定容器連接埠對主機連接埠對應，以及容器對容器探索</span><span class="sxs-lookup"><span data-stu-id="da75c-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="da75c-187">設定用來與容器通訊的主機連接埠。</span><span class="sxs-lookup"><span data-stu-id="da75c-187">Configure a host port used to communicate  with the container.</span></span> <span data-ttu-id="da75c-188">連接埠繫結會將服務在容器內接聽的連接埠，對應至主機上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="da75c-188">The port binding maps the port on which the service is listening inside the container to a port on the host.</span></span> <span data-ttu-id="da75c-189">在 ApplicationManifest.xml 檔案的 `ContainerHostPolicies` 元素中，新增 `PortBinding` 元素。</span><span class="sxs-lookup"><span data-stu-id="da75c-189">Add a `PortBinding` element in `ContainerHostPolicies` element of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="da75c-190">在本文中，`ContainerPort` 為 80 (如 Dockerfile 所指定，容器會公開連接埠 80)，而 `EndpointRef` 為 "Guest1TypeEndpoint" (先前在服務資訊清單中定義的端點)。</span><span class="sxs-lookup"><span data-stu-id="da75c-190">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (the endpoint previously defined in the service manifest).</span></span>  <span data-ttu-id="da75c-191">通訊埠 8081 上服務的連入要求會對應到容器上的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="da75c-191">Incoming requests to the service on port 8081 are mapped to port 80 on the container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="da75c-192">設定容器登錄驗證</span><span class="sxs-lookup"><span data-stu-id="da75c-192">Configure container registry authentication</span></span>
<span data-ttu-id="da75c-193">將 `RepositoryCredentials` 新增至 ApplicationManifest.xml 檔案的 `ContainerHostPolicies` 中，以設定容器登錄驗證。</span><span class="sxs-lookup"><span data-stu-id="da75c-193">Configure container registry authentication by adding `RepositoryCredentials` to `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span> <span data-ttu-id="da75c-194">為 myregistry.azurecr.io 容器登錄新增帳戶和密碼，讓服務從存放庫中下載容器映像。</span><span class="sxs-lookup"><span data-stu-id="da75c-194">Add the account and password for the myregistry.azurecr.io container registry, which allows the service to download the container image from the repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="da75c-195">建議您使用已部署至叢集中所有節點的加密憑證，加密存放庫密碼。</span><span class="sxs-lookup"><span data-stu-id="da75c-195">We recommend that you encrypt the repository password by using an encipherment certificate that's deployed to all nodes of the cluster.</span></span> <span data-ttu-id="da75c-196">當 Service Fabric 將服務套件部署至叢集時，會使用加密憑證將加密文字解密。</span><span class="sxs-lookup"><span data-stu-id="da75c-196">When Service Fabric deploys the service package to the cluster, the encipherment certificate is used to decrypt the cipher text.</span></span>  <span data-ttu-id="da75c-197">Invoke-ServiceFabricEncryptText Cmdlet 會用來建立密碼的加密文字，其已新增至 ApplicationManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="da75c-197">The Invoke-ServiceFabricEncryptText cmdlet is used to create the cipher text for the password, which is added to the ApplicationManifest.xml file.</span></span>

<span data-ttu-id="da75c-198">下列指令碼會建立新的自我簽署憑證，並將其匯出為 PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="da75c-198">The following script creates a new self-signed certificate and exports it to a PFX file.</span></span>  <span data-ttu-id="da75c-199">憑證已匯入現有的金鑰保存庫，接著已部署至 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="da75c-199">The certificate is imported into an existing key vault and then deployed to the Service Fabric cluster.</span></span>

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

# Create a self signed cert, export to PFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import the certificate to an existing key vault.  The key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add the certificate to all the VMs in the cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="da75c-200">使用 [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) Cmdlet 加密密碼。</span><span class="sxs-lookup"><span data-stu-id="da75c-200">Encrypt the password using the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="da75c-201">以 [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) Cmdlet 傳回的加密文字來取代密碼，並將 `PasswordEncrypted` 設定為 "true"。</span><span class="sxs-lookup"><span data-stu-id="da75c-201">Replace the password with the cipher text returned by the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` to "true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="da75c-202">設定隔離模式</span><span class="sxs-lookup"><span data-stu-id="da75c-202">Configure isolation mode</span></span>
<span data-ttu-id="da75c-203">Windows 支援兩種容器隔離模式：分別為處理序和 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="da75c-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="da75c-204">在處理序隔離模式中，在相同主機電腦上執行的所有容器都與主機共用核心。</span><span class="sxs-lookup"><span data-stu-id="da75c-204">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="da75c-205">在 Hyper-V 隔離模式中，會在每個 Hyper-V 容器與容器主機之間隔離核心。</span><span class="sxs-lookup"><span data-stu-id="da75c-205">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="da75c-206">隔離模式是在應用程式資訊清單檔中指定的 `ContainerHostPolicies` 元素。</span><span class="sxs-lookup"><span data-stu-id="da75c-206">The isolation mode is specified in the `ContainerHostPolicies` element in the application manifest file.</span></span> <span data-ttu-id="da75c-207">可以指定的隔離模式有 `process`、`hyperv` 和 `default`。</span><span class="sxs-lookup"><span data-stu-id="da75c-207">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="da75c-208">Windows Server 主機上的隔離模式預設為 `process`，Windows 10 主機上的預設值則為 `hyperv`。</span><span class="sxs-lookup"><span data-stu-id="da75c-208">The default isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="da75c-209">下列程式碼片段顯示如何在應用程式資訊清單檔中指定隔離模式。</span><span class="sxs-lookup"><span data-stu-id="da75c-209">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="da75c-210">設定資源控管</span><span class="sxs-lookup"><span data-stu-id="da75c-210">Configure resource governance</span></span>
<span data-ttu-id="da75c-211">[資源控管](service-fabric-resource-governance.md)可限制容器在主機上可使用的資源。</span><span class="sxs-lookup"><span data-stu-id="da75c-211">[Resource governance](service-fabric-resource-governance.md) restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="da75c-212">應用程式資訊清單中指定的 `ResourceGovernancePolicy` 元素是用於宣告服務程式碼封裝的資源限制。</span><span class="sxs-lookup"><span data-stu-id="da75c-212">The `ResourceGovernancePolicy` element, which is specified in the application manifest, is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="da75c-213">下列資源可設定資源限制：記憶體、MemorySwap、CpuShares (CPU relative weight)、MemoryReservationInMB、BlkioWeight (BlockIO 相對權數)。</span><span class="sxs-lookup"><span data-stu-id="da75c-213">Resource limits can be set for the following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="da75c-214">在此範例中，service package Guest1Pkg 會在其所在的叢集節點上獲得一個核心。</span><span class="sxs-lookup"><span data-stu-id="da75c-214">In this example, service package Guest1Pkg gets one core on the cluster nodes where it is placed.</span></span>  <span data-ttu-id="da75c-215">記憶體限制是絕對的，因此程式碼封裝會限制為 1024MB 的記憶體 (並具有同樣的彈性保證保留)。</span><span class="sxs-lookup"><span data-stu-id="da75c-215">Memory limits are absolute, so the code package is limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="da75c-216">程式碼套件 (容器或處理序) 無法配置超過此限制的記憶體，如果嘗試這麼做，將會導致發生記憶體不足的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="da75c-216">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="da75c-217">若要讓資源限制強制能夠運作，應該為服務套件內的所有程式碼套件都指定記憶體限制。</span><span class="sxs-lookup"><span data-stu-id="da75c-217">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-the-container-application"></a><span data-ttu-id="da75c-218">部署容器應用程式</span><span class="sxs-lookup"><span data-stu-id="da75c-218">Deploy the container application</span></span>
<span data-ttu-id="da75c-219">儲存所有變更，並建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="da75c-219">Save all your changes and build the application.</span></span> <span data-ttu-id="da75c-220">若要發佈您的應用程式，以滑鼠右鍵按一下 [方案總管] 中的 **MyFirstContainer**，然後選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="da75c-220">To publish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="da75c-221">在 [連線端點] 中，輸入叢集的管理端點。</span><span class="sxs-lookup"><span data-stu-id="da75c-221">In **Connection Endpoint**, enter the management endpoint for the cluster.</span></span>  <span data-ttu-id="da75c-222">例如，"containercluster.westus2.cloudapp.azure.com:19000"。</span><span class="sxs-lookup"><span data-stu-id="da75c-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="da75c-223">在 [Azure 入口網站](https://portal.azure.com)中，您可以在叢集的 [概觀] 刀鋒視窗中找到用戶端連線端點。</span><span class="sxs-lookup"><span data-stu-id="da75c-223">You can find the client connection endpoint in the Overview blade for your cluster in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="da75c-224">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="da75c-224">Click **Publish**.</span></span>

<span data-ttu-id="da75c-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個 Web 型工具，可檢查和管理 Service Fabric 叢集中的應用程式與節點。</span><span class="sxs-lookup"><span data-stu-id="da75c-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="da75c-226">開啟瀏覽器並瀏覽至 http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ 然後遵循應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="da75c-226">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow the application deployment.</span></span>  <span data-ttu-id="da75c-227">此應用程式會進行部署，但在叢集節點中下載映像之前 (視映像大小而定，這可能需要一些時間) 會處於錯誤狀態︰![錯誤][1]</span><span class="sxs-lookup"><span data-stu-id="da75c-227">The application deploys but is in an error state until the image is downloaded on the cluster nodes (which can take some time, depending on the image size): ![Error][1]</span></span>

<span data-ttu-id="da75c-228">應用程式處於 ```Ready``` 狀態時便已準備就緒︰![就緒][2]</span><span class="sxs-lookup"><span data-stu-id="da75c-228">The application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="da75c-229">開啟瀏覽器並瀏覽至 http://containercluster.westus2.cloudapp.azure.com:8081 。</span><span class="sxs-lookup"><span data-stu-id="da75c-229">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="da75c-230">您應該會看到 "Hello World!" 標題</span><span class="sxs-lookup"><span data-stu-id="da75c-230">You should see the heading "Hello World!"</span></span> <span data-ttu-id="da75c-231">顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="da75c-231">display in the browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="da75c-232">清除</span><span class="sxs-lookup"><span data-stu-id="da75c-232">Clean up</span></span>
<span data-ttu-id="da75c-233">當叢集在執行時，您需要繼續支付費用，請考慮[刪除您的叢集](service-fabric-get-started-azure-cluster.md#remove-the-cluster)。</span><span class="sxs-lookup"><span data-stu-id="da75c-233">You continue to incur charges while the cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="da75c-234">[合作對象叢集](http://tryazureservicefabric.westus.cloudapp.azure.com/)會在幾個小時後自動刪除。</span><span class="sxs-lookup"><span data-stu-id="da75c-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="da75c-235">將映像推送至容器登錄之後，您可以從開發電腦刪除本機映像︰</span><span class="sxs-lookup"><span data-stu-id="da75c-235">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="da75c-236">完整範例 Service Fabric 應用程式和服務資訊清單</span><span class="sxs-lookup"><span data-stu-id="da75c-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="da75c-237">以下是本文中使用的完整服務和應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="da75c-237">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="da75c-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="da75c-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="da75c-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="da75c-239">ApplicationManifest.xml</span></span>
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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
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
    <!-- The section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="da75c-240">在容器被迫終止前設定時間間隔</span><span class="sxs-lookup"><span data-stu-id="da75c-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="da75c-241">您可以在啟動服務刪除 (或移至另一個節點) 之後，設定執行階段在容器移除前所要等候的間隔時間。</span><span class="sxs-lookup"><span data-stu-id="da75c-241">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="da75c-242">設定時間間隔可將 `docker stop <time in seconds>` 命令傳送至容器。</span><span class="sxs-lookup"><span data-stu-id="da75c-242">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="da75c-243">如需更多詳細資訊，請參閱 [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)。</span><span class="sxs-lookup"><span data-stu-id="da75c-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="da75c-244">所要等候的時間間隔指定於 `Hosting` 區段之下。</span><span class="sxs-lookup"><span data-stu-id="da75c-244">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="da75c-245">下列叢集資訊清單程式碼片段示範如何設定等候間隔：</span><span class="sxs-lookup"><span data-stu-id="da75c-245">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="da75c-246">預設時間間隔會設定為 10 秒。</span><span class="sxs-lookup"><span data-stu-id="da75c-246">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="da75c-247">因為此組態是動態的，所以叢集的僅限組態升級會更新逾時。</span><span class="sxs-lookup"><span data-stu-id="da75c-247">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="da75c-248">將執行階段設定為移除未使用的容器映像</span><span class="sxs-lookup"><span data-stu-id="da75c-248">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="da75c-249">您可以將 Service Fabric 叢集設定為從節點移除未使用的容器映像。</span><span class="sxs-lookup"><span data-stu-id="da75c-249">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="da75c-250">如果節點上存在太多容器映像，此組態允許重新擷取磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="da75c-250">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="da75c-251">若要啟用此功能，請更新叢集資訊清單中的 `Hosting` 區段，如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="da75c-251">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="da75c-252">對於不應刪除的映像，您可以在 `ContainerImagesToSkip` 參數之下加以指定。</span><span class="sxs-lookup"><span data-stu-id="da75c-252">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="da75c-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da75c-253">Next steps</span></span>
* <span data-ttu-id="da75c-254">深入了解如何[在 Service Fabric 上執行容器](service-fabric-containers-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="da75c-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="da75c-255">閱讀[在容器中部署 .NET 應用程式](service-fabric-host-app-in-a-container.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="da75c-255">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="da75c-256">深入了解 Service Fabric [應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="da75c-256">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="da75c-257">請查看 GitHub 上的[ Service Fabric 容器程式碼範例](https://github.com/Azure-Samples/service-fabric-dotnet-containers)。</span><span class="sxs-lookup"><span data-stu-id="da75c-257">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
