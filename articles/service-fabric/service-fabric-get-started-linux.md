---
title: "在 Linux 上設定開發環境 | Microsoft Docs"
description: "在 Linux 上安裝執行階段和 SDK，並建立本機開發叢集。 完成此設定之後，您就可以開始建置應用程式。"
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
ms.openlocfilehash: 58c6bbbb16d7008e6b573cf8dbc8cf62da9789f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="b74f4-104">在 Linux 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="b74f4-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b74f4-105">Windows</span><span class="sxs-lookup"><span data-stu-id="b74f4-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="b74f4-106">Linux</span><span class="sxs-lookup"><span data-stu-id="b74f4-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="b74f4-107">OSX</span><span class="sxs-lookup"><span data-stu-id="b74f4-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="b74f4-108">若要在 Linux 開發機器上部署和執行 [Azure Service Fabric 應用程式](service-fabric-application-model.md) ，請安裝執行階段和通用 SDK。</span><span class="sxs-lookup"><span data-stu-id="b74f4-108">To deploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install the runtime and common SDK.</span></span> <span data-ttu-id="b74f4-109">您也可以安裝 Java 和 .NET Core 的選擇性 SDK。</span><span class="sxs-lookup"><span data-stu-id="b74f4-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b74f4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b74f4-110">Prerequisites</span></span>

<span data-ttu-id="b74f4-111">下列為支援開發的作業系統版本：</span><span class="sxs-lookup"><span data-stu-id="b74f4-111">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="b74f4-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="b74f4-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="b74f4-113">更新 APT 來源</span><span class="sxs-lookup"><span data-stu-id="b74f4-113">Update your APT sources</span></span>
<span data-ttu-id="b74f4-114">若要透過 apt-get 命令列工具安裝 SDK 和相關聯的執行階段套件，您必須先更新 Advanced Packaging Tool (APT) 來源。</span><span class="sxs-lookup"><span data-stu-id="b74f4-114">To install the SDK and the associated runtime package via the apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="b74f4-115">開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="b74f4-115">Open a terminal.</span></span>
2. <span data-ttu-id="b74f4-116">將 Service Fabric 存放庫新增至來源清單。</span><span class="sxs-lookup"><span data-stu-id="b74f4-116">Add the Service Fabric repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="b74f4-117">將 `dotnet` 存放庫新增至來源清單。</span><span class="sxs-lookup"><span data-stu-id="b74f4-117">Add the `dotnet` repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="b74f4-118">將新的 Gnu Privacy Guard (GnuPG 或 GPG) 金鑰新增至 APT keyring。</span><span class="sxs-lookup"><span data-stu-id="b74f4-118">Add the new Gnu Privacy Guard (GnuPG, or GPG) key to your APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="b74f4-119">將官方的 Docker GPG 金鑰新增至 APT keyring。</span><span class="sxs-lookup"><span data-stu-id="b74f4-119">Add the official Docker GPG key to your APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="b74f4-120">設定 Docker 存放庫。</span><span class="sxs-lookup"><span data-stu-id="b74f4-120">Set up the Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="b74f4-121">根據新增的存放庫重新整理套件清單。</span><span class="sxs-lookup"><span data-stu-id="b74f4-121">Refresh your package lists based on the newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-the-sdk-for-local-cluster-setup"></a><span data-ttu-id="b74f4-122">針對本機叢集設定安裝和設定 SDK</span><span class="sxs-lookup"><span data-stu-id="b74f4-122">Install and set up the SDK for local cluster setup</span></span>

<span data-ttu-id="b74f4-123">在您已更新來源後，就可以安裝 SDK。</span><span class="sxs-lookup"><span data-stu-id="b74f4-123">After you have updated your sources, you can install the SDK.</span></span> <span data-ttu-id="b74f4-124">安裝 Service Fabric SDK 套件、確認安裝，並同意授權合約。</span><span class="sxs-lookup"><span data-stu-id="b74f4-124">Install the Service Fabric SDK package, confirm the installation, and agree to the license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="b74f4-125">下列命令會自動接受 Service Fabric 套件的授權︰</span><span class="sxs-lookup"><span data-stu-id="b74f4-125">The following commands automate accepting the license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="b74f4-126">設定本機叢集</span><span class="sxs-lookup"><span data-stu-id="b74f4-126">Set up a local cluster</span></span>
  <span data-ttu-id="b74f4-127">如果安裝順利，您應該能夠啟動本機叢集。</span><span class="sxs-lookup"><span data-stu-id="b74f4-127">If the installation is successful, you should be able to start a local cluster.</span></span>

  1. <span data-ttu-id="b74f4-128">執行叢集安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="b74f4-128">Run the cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="b74f4-129">開啟瀏覽器，前往 [Service Fabric Explorer](http://localhost:19080/Explorer)。</span><span class="sxs-lookup"><span data-stu-id="b74f4-129">Open a web browser and go to [Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="b74f4-130">如果叢集已經啟動，您應會看見 Service Fabric Explorer 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b74f4-130">If the cluster has started, you should see the Service Fabric Explorer dashboard.</span></span>

      ![Linux 上的 Service Fabric Explorer][sfx-linux]

  <span data-ttu-id="b74f4-132">此時，您可以根據客體容器或來賓可執行檔，部署預先建置的 Service Fabric 應用程式套件或新的套件。</span><span class="sxs-lookup"><span data-stu-id="b74f4-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="b74f4-133">若要使用 Java 或 .NET Core SDK 建置新的服務，請遵循後面幾節所提供的選擇性設定步驟。</span><span class="sxs-lookup"><span data-stu-id="b74f4-133">To build new services by using the Java or .NET Core SDKs, follow the optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="b74f4-134">Linux 不支援獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="b74f4-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="b74f4-135">預覽只支援一整體和 Azure Linux 多電腦叢集。</span><span class="sxs-lookup"><span data-stu-id="b74f4-135">The preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-the-service-fabric-cli"></a><span data-ttu-id="b74f4-136">設定 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="b74f4-136">Set up the Service Fabric CLI</span></span>

<span data-ttu-id="b74f4-137">[Service Fabric CLI](service-fabric-cli.md) 包含可供與 Service Fabric 實體 (包括叢集和應用程式) 進行互動的命令。</span><span class="sxs-lookup"><span data-stu-id="b74f4-137">The [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="b74f4-138">它是以 python, 為基礎，所以先確定您已安裝 python 和 pip，再繼續執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b74f4-138">It is based on python, so be sure to have python and pip installed before you proceed with the following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-the-generators-for-containers-and-guest-executables"></a><span data-ttu-id="b74f4-139">安裝並設定容器和來賓可執行檔的產生器</span><span class="sxs-lookup"><span data-stu-id="b74f4-139">Install and set up the generators for containers and guest-executables</span></span>
<span data-ttu-id="b74f4-140">Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b74f4-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="b74f4-141">請遵循下列步驟來確保您有 Service Fabric yeoman 範本產生器可在電腦上運作。</span><span class="sxs-lookup"><span data-stu-id="b74f4-141">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="b74f4-142">在電腦上安裝 nodejs 和 NPM</span><span class="sxs-lookup"><span data-stu-id="b74f4-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="b74f4-143">在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器</span><span class="sxs-lookup"><span data-stu-id="b74f4-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="b74f4-144">從 NPM 安裝 Service Fabric Yeo 容器產生器和來賓可執行檔產生器</span><span class="sxs-lookup"><span data-stu-id="b74f4-144">Install the Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="b74f4-145">在您安裝上述產生器後，就能分別執行 `yo azuresfguest` 或 `yo azuresfcontainer`，以使用來賓可執行檔或容器服務建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="b74f4-145">After you have installed the above generators, you should be able to create apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-the-necessary-java-artifacts-optional-if-you-want-to-use-the-java-programming-models"></a><span data-ttu-id="b74f4-146">安裝所需的 Java 構件 (選擇性，如果您想要使用 Java 程式設計模型)</span><span class="sxs-lookup"><span data-stu-id="b74f4-146">Install the necessary Java artifacts (optional, if you want to use the Java programming models)</span></span>

<span data-ttu-id="b74f4-147">若要使用 Java 建置 Service Fabric 服務，確定您已隨著用來執行建置工作的 Gradle 一起安裝 JDK 1.8。</span><span class="sxs-lookup"><span data-stu-id="b74f4-147">To build Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="b74f4-148">下列程式碼片段會隨著 Gradle 安裝 Open JDK 1.8。</span><span class="sxs-lookup"><span data-stu-id="b74f4-148">The following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="b74f4-149">系統會從 Maven 提取 Service Fabric Java 程式庫。</span><span class="sxs-lookup"><span data-stu-id="b74f4-149">The Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-the-eclipse-neon-plug-in-optional"></a><span data-ttu-id="b74f4-150">安裝 Eclipse Neon 外掛程式 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="b74f4-150">Install the Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="b74f4-151">您可以從**適用於 Java 開發人員的 Eclipse 整合式開發環境 (IDE)** 安裝適用於 Service Fabric 的 Eclipse 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="b74f4-151">You can install the Eclipse plug-in for Service Fabric from within the **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="b74f4-152">除了 Service Fabric Java 應用程式之外，您可以使用 Eclipse 來建立 Service Fabric 來賓可執行檔應用程式和容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="b74f4-152">You can use Eclipse to create Service Fabric guest executable applications and container applications in addition to Service Fabric Java applications.</span></span>

1. <span data-ttu-id="b74f4-153">在 Eclipse 中，確定已安裝最新版 Eclipse Neon 和最新的 Buildship 版本 (1.0.17 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="b74f4-153">In Eclipse, ensure that you have latest Eclipse Neon and the latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="b74f4-154">您可以選取 [說明]  >  [安裝詳細資料]，檢查已安裝的元件版本。</span><span class="sxs-lookup"><span data-stu-id="b74f4-154">You can check the versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="b74f4-155">您可以使用 [Eclipse Buildship：適用於 Gradle 的 Eclipse 外掛程式][buildship-update]的指示來更新 Buildship。</span><span class="sxs-lookup"><span data-stu-id="b74f4-155">You can update Buildship by using the instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="b74f4-156">若要安裝 Service Fabric 外掛程式，請選取 [說明]  >  [安裝新軟體]。</span><span class="sxs-lookup"><span data-stu-id="b74f4-156">To install the Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="b74f4-157">在 [使用] 文字方塊中，輸入 **http://dl.microsoft.com/eclipse**。</span><span class="sxs-lookup"><span data-stu-id="b74f4-157">In the **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="b74f4-158">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b74f4-158">Click **Add**.</span></span>

    ![可用的軟體頁面][sf-eclipse-plugin]

5. <span data-ttu-id="b74f4-160">選取 ServiceFabric 外掛程式，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b74f4-160">Select the **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="b74f4-161">完成安裝步驟，然後接受使用者授權合約。</span><span class="sxs-lookup"><span data-stu-id="b74f4-161">Complete the installation steps, and then accept the end-user license agreement.</span></span>

<span data-ttu-id="b74f4-162">如果您已安裝 Service Fabric Eclipse 外掛程式，請確定您擁有的是最新版本。</span><span class="sxs-lookup"><span data-stu-id="b74f4-162">If you already have the Service Fabric Eclipse plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="b74f4-163">您可以藉由選取 [說明]  >  [安裝詳細資料]，然後在已安裝外掛程式清單中搜尋 Service Fabric 來檢查。如果有可用的較新版本，請選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="b74f4-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in the list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="b74f4-164">如需詳細資訊，請參閱[適用於 Eclipse Java 應用程式開發的 Service Fabric 外掛程式](service-fabric-get-started-eclipse.md)。</span><span class="sxs-lookup"><span data-stu-id="b74f4-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-the-net-core-sdk-optional-if-you-want-to-use-the-net-core-programming-models"></a><span data-ttu-id="b74f4-165">安裝 .NET Core SDK (選擇性，如果您想要使用 .NET Core 程式設計模型)</span><span class="sxs-lookup"><span data-stu-id="b74f4-165">Install the .NET Core SDK (optional, if you want to use the .NET Core programming models)</span></span>
<span data-ttu-id="b74f4-166">.NET Core SDK 提供了使用 .NET Core 建置 Service Fabric 服務所需的程式庫和範本。</span><span class="sxs-lookup"><span data-stu-id="b74f4-166">The .NET Core SDK provides the libraries and templates that are required to build Service Fabric services with .NET Core.</span></span> <span data-ttu-id="b74f4-167">執行下列命令來安裝 .NET Core SDK 套件 -</span><span class="sxs-lookup"><span data-stu-id="b74f4-167">Install the .NET Core SDK package by running the following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-the-sdk-and-runtime"></a><span data-ttu-id="b74f4-168">更新 SDK 和執行階段</span><span class="sxs-lookup"><span data-stu-id="b74f4-168">Update the SDK and runtime</span></span>

<span data-ttu-id="b74f4-169">若要更新為最新版的 SDK 和執行階段，請執行下列命令 (取消選取您不想要的 SDK)︰</span><span class="sxs-lookup"><span data-stu-id="b74f4-169">To update to the latest version of the SDK and runtime, run the following commands (deselect the SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="b74f4-170">若要更新 Maven 提供的 Java SDK 二進位檔，您必須在 ``build.gradle`` 檔案中更新對應二進位檔的版本詳細資料，以指向最新版本。</span><span class="sxs-lookup"><span data-stu-id="b74f4-170">To update the Java SDK binaries from Maven, you need to update the version details of the corresponding binary in the ``build.gradle`` file to point to the latest version.</span></span> <span data-ttu-id="b74f4-171">若想知道您需要更新版本的確切位置，您可以[在此](https://github.com/Azure-Samples/service-fabric-java-getting-started)參考 Service Fabric 快速入門範例中的任何``build.gradle`` 檔案。</span><span class="sxs-lookup"><span data-stu-id="b74f4-171">To know exactly where you need to update the version, you can refer to any ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="b74f4-172">更新套件可能會導致本機開發叢集停止執行。</span><span class="sxs-lookup"><span data-stu-id="b74f4-172">Updating the packages might cause your local development cluster to stop running.</span></span> <span data-ttu-id="b74f4-173">請依照本頁上的指示，在升級之後重新啟動本機叢集。</span><span class="sxs-lookup"><span data-stu-id="b74f4-173">Restart your local cluster after an upgrade by following the instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b74f4-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b74f4-174">Next steps</span></span>

* [<span data-ttu-id="b74f4-175">使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="b74f4-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="b74f4-176">在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="b74f4-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="b74f4-177">在 Linux 上建立第一個 CSharp 應用程式</span><span class="sxs-lookup"><span data-stu-id="b74f4-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="b74f4-178">在 OSX 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="b74f4-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="b74f4-179">使用 Service Fabric CLI 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="b74f4-179">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="b74f4-180">Service Fabric Windows/Linux 的差異</span><span class="sxs-lookup"><span data-stu-id="b74f4-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="b74f4-181">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="b74f4-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
