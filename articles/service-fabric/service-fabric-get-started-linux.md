---
title: "您在 Linux 上的開發環境 aaaSet |Microsoft 文件"
description: "安裝 hello 執行階段和 SDK，並在 Linux 上建立本機開發叢集。 完成此安裝之後，您將準備 toobuild 應用程式。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="659df-104">在 Linux 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="659df-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="659df-105">Windows</span><span class="sxs-lookup"><span data-stu-id="659df-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="659df-106">Linux</span><span class="sxs-lookup"><span data-stu-id="659df-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="659df-107">OSX</span><span class="sxs-lookup"><span data-stu-id="659df-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="659df-108">toodeploy 並執行[Azure Service Fabric 應用程式](service-fabric-application-model.md)Linux 開發電腦上安裝 hello 執行階段和通用的 SDK。</span><span class="sxs-lookup"><span data-stu-id="659df-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="659df-109">您也可以安裝 Java 和 .NET Core 的選擇性 SDK。</span><span class="sxs-lookup"><span data-stu-id="659df-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="659df-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="659df-110">Prerequisites</span></span>

<span data-ttu-id="659df-111">開發可支援下列作業系統版本的 hello:</span><span class="sxs-lookup"><span data-stu-id="659df-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="659df-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="659df-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="659df-113">更新 APT 來源</span><span class="sxs-lookup"><span data-stu-id="659df-113">Update your APT sources</span></span>
<span data-ttu-id="659df-114">tooinstall hello SDK 和 hello 相關聯的執行階段封裝透過 hello apt get 命令列工具，您必須先更新進階封裝工具 (APT) 來源。</span><span class="sxs-lookup"><span data-stu-id="659df-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="659df-115">開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="659df-115">Open a terminal.</span></span>
2. <span data-ttu-id="659df-116">加入 hello Service Fabric 儲存機制 tooyour 來源清單。</span><span class="sxs-lookup"><span data-stu-id="659df-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="659df-117">新增 hello`dotnet`儲存機制 tooyour 來源清單。</span><span class="sxs-lookup"><span data-stu-id="659df-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="659df-118">新增 hello 新 Gnu 隱私防護 （GnuPG 或 GPG） 索引鍵 tooyour APT keyring。</span><span class="sxs-lookup"><span data-stu-id="659df-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="659df-119">新增 hello 官方 Docker GPG 金鑰 tooyour APT keyring。</span><span class="sxs-lookup"><span data-stu-id="659df-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="659df-120">設定 hello Docker 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="659df-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="659df-121">重新整理您的封裝列出 hello 新加入的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="659df-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="659df-122">安裝並設定好 hello SDK 本機叢集安裝程式</span><span class="sxs-lookup"><span data-stu-id="659df-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="659df-123">您已更新您的來源之後，您可以安裝 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="659df-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="659df-124">安裝 hello Service Fabric SDK 封裝並確認 hello 安裝同意 toohello 授權合約。</span><span class="sxs-lookup"><span data-stu-id="659df-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="659df-125">hello 下列命令自動接受 hello 授權 Service Fabric 封裝：</span><span class="sxs-lookup"><span data-stu-id="659df-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="659df-126">設定本機叢集</span><span class="sxs-lookup"><span data-stu-id="659df-126">Set up a local cluster</span></span>
  <span data-ttu-id="659df-127">如果 hello 安裝成功，您應該能夠 toostart 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="659df-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="659df-128">執行 hello 叢集安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="659df-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="659df-129">開啟網頁瀏覽器並移過[Service Fabric 總管](http://localhost:19080/Explorer)。</span><span class="sxs-lookup"><span data-stu-id="659df-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="659df-130">如果啟動 hello 叢集後，您應該會看到 hello Service Fabric 總管儀表板。</span><span class="sxs-lookup"><span data-stu-id="659df-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Linux 上的 Service Fabric Explorer][sfx-linux]

  <span data-ttu-id="659df-132">此時，您可以根據客體容器或來賓可執行檔，部署預先建置的 Service Fabric 應用程式套件或新的套件。</span><span class="sxs-lookup"><span data-stu-id="659df-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="659df-133">toobuild 新服務使用 hello Java 或.NET Core Sdk，請遵循 hello 後續各節提供的選用設定步驟。</span><span class="sxs-lookup"><span data-stu-id="659df-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="659df-134">Linux 不支援獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="659df-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="659df-135">hello 預覽支援只有一個方塊，而且 Azure Linux 多電腦叢集。</span><span class="sxs-lookup"><span data-stu-id="659df-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="659df-136">設定服務網狀架構 CLI hello</span><span class="sxs-lookup"><span data-stu-id="659df-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="659df-137">hello[服務網狀架構 CLI](service-fabric-cli.md)有 Service Fabric 實體，包括叢集和應用程式與互動的命令。</span><span class="sxs-lookup"><span data-stu-id="659df-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="659df-138">它根據 python，因此請務必確定 toohave python 和 pip 安裝才能繼續進行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="659df-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="659df-139">安裝並設定好 hello 容器和客體可執行檔的產生器</span><span class="sxs-lookup"><span data-stu-id="659df-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="659df-140">Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="659df-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="659df-141">請遵循下列 tooensure 您擁有 hello Service Fabric yeoman 範本產生器，用於您的電腦上的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="659df-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="659df-142">在電腦上安裝 nodejs 和 NPM</span><span class="sxs-lookup"><span data-stu-id="659df-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="659df-143">在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器</span><span class="sxs-lookup"><span data-stu-id="659df-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="659df-144">從 NPM 安裝 hello 服務網狀架構 Yeo 容器產生器和來賓 execuatble 產生器</span><span class="sxs-lookup"><span data-stu-id="659df-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="659df-145">產生器上方 hello 安裝之後，您應該能夠 toocreate 客體可執行檔或容器服務的應用程式執行`yo azuresfguest`或`yo azuresfcontainer`分別。</span><span class="sxs-lookup"><span data-stu-id="659df-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="659df-146">安裝 hello 必要 Java 成品 （選擇性，如果您想 toouse hello Java 程式設計模型）</span><span class="sxs-lookup"><span data-stu-id="659df-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="659df-147">toobuild Service Fabric 服務使用 Java，請確定您有隨用來執行建置工作的 Gradle 一起安裝的 JDK 1.8。</span><span class="sxs-lookup"><span data-stu-id="659df-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="659df-148">下列程式碼片段的 hello 安裝以及 Gradle 的 Open JDK 1.8。</span><span class="sxs-lookup"><span data-stu-id="659df-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="659df-149">hello 服務網狀架構 Java 文件庫會從 Maven 提取。</span><span class="sxs-lookup"><span data-stu-id="659df-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="659df-150">安裝 hello Eclipse Neon 外掛程式 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="659df-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="659df-151">您可以在 hello 適用於從 Service Fabric 安裝 hello Eclipse 外掛程式**Eclipse IDE for Java 開發人員**。</span><span class="sxs-lookup"><span data-stu-id="659df-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="659df-152">您可以使用 Eclipse toocreate Service Fabric 客體可執行應用程式和容器應用程式中加入 tooService 網狀架構 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="659df-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="659df-153">在 Eclipse 中，確定您有最新的 Eclipse Neon hello Buildship 新版 (1.0.17 或更新版本) 安裝。</span><span class="sxs-lookup"><span data-stu-id="659df-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="659df-154">您可以選取來查看 hello 版本已安裝的元件**協助** > **安裝詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="659df-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="659df-155">您可以使用 hello 指示來更新 Buildship [Eclipse Buildship: Eclipse 外掛程式 Gradle][buildship-update]。</span><span class="sxs-lookup"><span data-stu-id="659df-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="659df-156">tooinstall hello Service Fabric 外掛程式，請選取**協助** > **安裝新軟體**。</span><span class="sxs-lookup"><span data-stu-id="659df-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="659df-157">在 hello**搭配**方塊中，輸入**http://dl.microsoft.com/eclipse**。</span><span class="sxs-lookup"><span data-stu-id="659df-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="659df-158">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="659df-158">Click **Add**.</span></span>

    ![hello 可用的軟體 頁面][sf-eclipse-plugin]

5. <span data-ttu-id="659df-160">選取 hello **ServiceFabric**外掛程式，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="659df-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="659df-161">完成 hello 安裝步驟，並接受 hello 使用者授權合約。</span><span class="sxs-lookup"><span data-stu-id="659df-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="659df-162">如果您已經有 hello 服務網狀架構 Eclipse 外掛程式安裝，請確定您已擁有 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="659df-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="659df-163">您可以選取查看**協助** > **安裝詳細資料**和 hello 清單中搜尋適用於 Service Fabric 安裝外掛程式。如果有可用的較新版本，請選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="659df-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="659df-164">如需詳細資訊，請參閱[適用於 Eclipse Java 應用程式開發的 Service Fabric 外掛程式](service-fabric-get-started-eclipse.md)。</span><span class="sxs-lookup"><span data-stu-id="659df-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="659df-165">安裝 hello.NET Core SDK （選擇性，如果您想 toouse hello.NET Core 的程式設計模型）</span><span class="sxs-lookup"><span data-stu-id="659df-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="659df-166">hello.NET Core SDK 提供 hello 程式庫和.NET core 必要的 toobuild Service Fabric 服務的範本。</span><span class="sxs-lookup"><span data-stu-id="659df-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="659df-167">安裝執行 hello 以下 hello.NET Core SDK 封裝</span><span class="sxs-lookup"><span data-stu-id="659df-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="659df-168">更新 hello SDK 和執行階段</span><span class="sxs-lookup"><span data-stu-id="659df-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="659df-169">tooupdate toohello 最新版本的 hello SDK 和執行階段中，執行下列命令的 hello （取消選取您不想 hello Sdk）：</span><span class="sxs-lookup"><span data-stu-id="659df-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="659df-170">tooupdate 從 Maven 的 hello Java SDK 二進位檔，您需要 tooupdate hello 版本的詳細資訊的 hello 中的 hello 對應二進位檔``build.gradle``檔案 toopoint toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="659df-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="659df-171">tooknow 確實需要 tooupdate hello 版本，您可以使用參照 tooany ``build.gradle`` Service Fabric 快速入門範例中的檔案[這裡](https://github.com/Azure-Samples/service-fabric-java-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="659df-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="659df-172">更新 hello 封裝可能會導致您執行的本機開發叢集 toostop。</span><span class="sxs-lookup"><span data-stu-id="659df-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="659df-173">下列 hello 指示此頁面上升級後重新啟動本機叢集。</span><span class="sxs-lookup"><span data-stu-id="659df-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="659df-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="659df-174">Next steps</span></span>

* [<span data-ttu-id="659df-175">使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="659df-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="659df-176">在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="659df-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="659df-177">在 Linux 上建立第一個 CSharp 應用程式</span><span class="sxs-lookup"><span data-stu-id="659df-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="659df-178">在 OSX 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="659df-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="659df-179">使用 hello 服務網狀架構 CLI toomanage 您應用程式</span><span class="sxs-lookup"><span data-stu-id="659df-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="659df-180">Service Fabric Windows/Linux 的差異</span><span class="sxs-lookup"><span data-stu-id="659df-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="659df-181">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="659df-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
