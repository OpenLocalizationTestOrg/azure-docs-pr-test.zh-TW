---
title: "aaaAzure 服務網狀架構 Docker 撰寫預覽"
description: "Azure Service Fabric 接受 Docker Compose 格式 toomake 它更容易使用 Service Fabric tooorchestrate 現有容器。 這項支援目前只能預覽。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="9eb01-104">Azure Service Fabric 中 Docker Compose 的應用程式支援 (預覽)</span><span class="sxs-lookup"><span data-stu-id="9eb01-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="9eb01-105">Docker 使用 hello [docker compose.yml](https://docs.docker.com/compose)定義多個容器應用程式的檔案。</span><span class="sxs-lookup"><span data-stu-id="9eb01-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="9eb01-106">toomake 它熟悉 Docker tooorchestrate 現有容器應用程式在 Azure Service Fabric 的客戶輕鬆，我們要加入的 Docker Compose 的預覽支援原生 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="9eb01-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="9eb01-107">Service Fabric 可接受版本 3 以上的 `docker-compose.yml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="9eb01-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="9eb01-108">此支援目前只能預覽，因此僅支援 Compose 指示詞子集。</span><span class="sxs-lookup"><span data-stu-id="9eb01-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="9eb01-109">例如，不支援應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="9eb01-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="9eb01-110">但是，您一律能夠移除與部署應用程式，而非升級。</span><span class="sxs-lookup"><span data-stu-id="9eb01-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="9eb01-111">此預覽 toouse，5.7 或更高的 hello Service Fabric 執行階段透過 hello hello 對應 SDK 以及 Azure 入口網站，建立您的叢集與版本。</span><span class="sxs-lookup"><span data-stu-id="9eb01-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="9eb01-112">此功能目前只能預覽，尚未在生產環境中受到支援。</span><span class="sxs-lookup"><span data-stu-id="9eb01-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="9eb01-113">在 Service Fabric 上部署 Docker Compose 檔案</span><span class="sxs-lookup"><span data-stu-id="9eb01-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="9eb01-114">hello 下列命令會建立 Service Fabric 應用程式 (名為`fabric:/TestContainerApp`hello 前面範例中)，您可以監視並管理任何其他的 Service Fabric 應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="9eb01-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="9eb01-115">您可以使用健康狀態查詢的 hello 指定的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9eb01-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="9eb01-116">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="9eb01-116">Use PowerShell</span></span>

<span data-ttu-id="9eb01-117">建立 Service Fabric 撰寫的應用程式從 docker compose.yml 檔案，藉由執行下列命令在 PowerShell 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="9eb01-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="9eb01-118">`RegistryUserName`和`RegistryPassword`toohello 容器登錄使用者名稱和密碼，請參閱。</span><span class="sxs-lookup"><span data-stu-id="9eb01-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="9eb01-119">Hello 應用程式完成之後，您可以使用下列命令的 hello 檢查其狀態：</span><span class="sxs-lookup"><span data-stu-id="9eb01-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="9eb01-120">toodelete hello 撰寫應用程式，透過 PowerShell，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9eb01-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="9eb01-121">使用 Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="9eb01-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="9eb01-122">或者，您可以使用下列服務網狀架構 CLI 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9eb01-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="9eb01-123">在您建立 hello 應用程式後，您可以使用下列命令的 hello 檢查其狀態：</span><span class="sxs-lookup"><span data-stu-id="9eb01-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="9eb01-124">toodelete hello 撰寫應用程式，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9eb01-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="9eb01-125">支援的撰寫指示詞</span><span class="sxs-lookup"><span data-stu-id="9eb01-125">Supported Compose directives</span></span>

<span data-ttu-id="9eb01-126">本預覽版支援從 hello 撰寫第 3 版格式，包括下列基本類型的 hello hello 組態選項的子集：</span><span class="sxs-lookup"><span data-stu-id="9eb01-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="9eb01-127">服務 > 部署 > 複本</span><span class="sxs-lookup"><span data-stu-id="9eb01-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="9eb01-128">服務 > 部署 > 放置 > 條件約束</span><span class="sxs-lookup"><span data-stu-id="9eb01-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="9eb01-129">服務 > 部署 > 資源 > 限制</span><span class="sxs-lookup"><span data-stu-id="9eb01-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="9eb01-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="9eb01-130">-cpu-shares</span></span>
    * <span data-ttu-id="9eb01-131">-memory</span><span class="sxs-lookup"><span data-stu-id="9eb01-131">-memory</span></span>
    * <span data-ttu-id="9eb01-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="9eb01-132">-memory-swap</span></span>
* <span data-ttu-id="9eb01-133">服務 > 命令</span><span class="sxs-lookup"><span data-stu-id="9eb01-133">Services > Commands</span></span>
* <span data-ttu-id="9eb01-134">服務 > 環境</span><span class="sxs-lookup"><span data-stu-id="9eb01-134">Services > Environment</span></span>
* <span data-ttu-id="9eb01-135">服務 > 連接埠</span><span class="sxs-lookup"><span data-stu-id="9eb01-135">Services > Ports</span></span>
* <span data-ttu-id="9eb01-136">服務 > 映像</span><span class="sxs-lookup"><span data-stu-id="9eb01-136">Services > Image</span></span>
* <span data-ttu-id="9eb01-137">服務 > 隔離 (僅適用於 Windows)</span><span class="sxs-lookup"><span data-stu-id="9eb01-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="9eb01-138">服務 > 記錄 > 驅動程式</span><span class="sxs-lookup"><span data-stu-id="9eb01-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="9eb01-139">服務 > 記錄 > 驅動程式 > 選項</span><span class="sxs-lookup"><span data-stu-id="9eb01-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="9eb01-140">磁碟區與部署 > 磁碟區</span><span class="sxs-lookup"><span data-stu-id="9eb01-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="9eb01-141">中所述，設定強制執行資源限制的 hello 叢集[Service Fabric 資源控管](service-fabric-resource-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="9eb01-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="9eb01-142">此預覽不支援所有其他的 Docker Compose 指示詞。</span><span class="sxs-lookup"><span data-stu-id="9eb01-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="9eb01-143">ServiceDnsName 計算</span><span class="sxs-lookup"><span data-stu-id="9eb01-143">ServiceDnsName computation</span></span>

<span data-ttu-id="9eb01-144">如果您在撰寫檔案中指定的 hello 服務名稱是完整的網域名稱 （也就是它包含點 [.]），註冊 Service Fabric hello DNS 名稱是`<ServiceName>`（包括 hello 點）。</span><span class="sxs-lookup"><span data-stu-id="9eb01-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="9eb01-145">否則，每個路徑區段 hello 應用程式名稱會成為網域中的標籤與 hello 成為 hello 最上層網域標籤第一個路徑區段，hello 服務 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="9eb01-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="9eb01-146">例如，如果 hello 指定應用程式名稱是`fabric:/SampleApp/MyComposeApp`，`<ServiceName>.MyComposeApp.SampleApp`會 hello 已註冊的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="9eb01-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="9eb01-147">Compose (執行個體定義) 與 Service Fabric 應用程式模型 (類型定義) 之間的差異</span><span class="sxs-lookup"><span data-stu-id="9eb01-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="9eb01-148">docker-compose.yml 檔案描述一組可部署的容器，包括其屬性與組態。</span><span class="sxs-lookup"><span data-stu-id="9eb01-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="9eb01-149">例如，hello 檔案可以包含環境變數和連接埠。</span><span class="sxs-lookup"><span data-stu-id="9eb01-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="9eb01-150">您也可以在 hello docker compose.yml 檔案中指定部署參數，例如安置限制、 資源限制，以及 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="9eb01-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="9eb01-151">hello [Service Fabric 應用程式模型](service-fabric-application-model.md)使用服務類型和應用程式類型，您可以在其中有許多應用程式執行個體的 hello 相同的型別。</span><span class="sxs-lookup"><span data-stu-id="9eb01-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="9eb01-152">例如，可以讓每個客戶有一個應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="9eb01-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="9eb01-153">此類型為基礎的模型支援多個版本的 hello 已向 hello 執行階段的相同應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="9eb01-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="9eb01-154">例如，客戶 A 」 可以有型別 1.0 AppTypeA，使用具現化的應用程式和客戶 B 」 可以有另一個應用程式使用 hello 具現化相同的類型和版本。</span><span class="sxs-lookup"><span data-stu-id="9eb01-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="9eb01-155">您定義 hello 應用程式類型在 hello 應用程式資訊清單，並建立 hello 應用程式時，指定 hello 應用程式名稱和部署參數。</span><span class="sxs-lookup"><span data-stu-id="9eb01-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="9eb01-156">雖然這種模型提供的彈性，我們也計劃 toosupport 更簡單、 執行個體為基礎的部署模型類型的隱含從 hello 資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="9eb01-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="9eb01-157">在此模型中，每個應用程式會取得自己的獨立資訊清單。</span><span class="sxs-lookup"><span data-stu-id="9eb01-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="9eb01-158">我們正在透過新增對 docker-compose.yml (這是以執行個體為基礎的部署格式) 的支援來預覽此成果。</span><span class="sxs-lookup"><span data-stu-id="9eb01-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9eb01-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9eb01-159">Next steps</span></span>

* <span data-ttu-id="9eb01-160">Hello 上讀取[Service Fabric 應用程式模型](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="9eb01-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="9eb01-161">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="9eb01-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
