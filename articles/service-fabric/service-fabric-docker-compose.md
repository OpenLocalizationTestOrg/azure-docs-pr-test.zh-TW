---
title: "Azure Service Fabric Docker Compose 預覽"
description: "Azure Service Fabric 接受 Docker Compose 格式，可讓您更輕鬆地使用 Service Fabric 來協調現有容器。 這項支援目前只能預覽。"
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
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="c865e-104">Azure Service Fabric 中 Docker Compose 的應用程式支援 (預覽)</span><span class="sxs-lookup"><span data-stu-id="c865e-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="c865e-105">Docker 使用 [docker-compose.yml](https://docs.docker.com/compose) 檔案定義多容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="c865e-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="c865e-106">為了讓客戶能夠輕鬆地熟悉 Docker 以協調 Azure Service Fabric 上的現有容器，因此我們在平台中原生提供 Docker Compose 的預覽支援。</span><span class="sxs-lookup"><span data-stu-id="c865e-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="c865e-107">Service Fabric 可接受版本 3 以上的 `docker-compose.yml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c865e-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="c865e-108">此支援目前只能預覽，因此僅支援 Compose 指示詞子集。</span><span class="sxs-lookup"><span data-stu-id="c865e-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="c865e-109">例如，不支援應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="c865e-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="c865e-110">但是，您一律能夠移除與部署應用程式，而非升級。</span><span class="sxs-lookup"><span data-stu-id="c865e-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="c865e-111">若要使用此預覽，請透過 Azure 入口網站和對應的 SDK，以 Service Fabric 執行階段 5.7 版或更新版本建立您的叢集。</span><span class="sxs-lookup"><span data-stu-id="c865e-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="c865e-112">此功能目前只能預覽，尚未在生產環境中受到支援。</span><span class="sxs-lookup"><span data-stu-id="c865e-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="c865e-113">在 Service Fabric 上部署 Docker Compose 檔案</span><span class="sxs-lookup"><span data-stu-id="c865e-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="c865e-114">下列命令會建立一個 Service Fabric 應用程式 (在上述範例中名為 `fabric:/TestContainerApp`)，而監視及管理此應用程式的方式與任何其他 Service Fabric 應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="c865e-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="c865e-115">可使用指定的應用程式名稱查詢健康情況。</span><span class="sxs-lookup"><span data-stu-id="c865e-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="c865e-116">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="c865e-116">Use PowerShell</span></span>

<span data-ttu-id="c865e-117">透過在 PowerShell 中執行下列命令，從 docker-compose.yml 檔案建立 Service Fabric Compose 應用程式：</span><span class="sxs-lookup"><span data-stu-id="c865e-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="c865e-118">`RegistryUserName` 和 `RegistryPassword` 是指容器登錄使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="c865e-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="c865e-119">您完成應用程式之後，可以使用下列命令檢查其狀態：</span><span class="sxs-lookup"><span data-stu-id="c865e-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="c865e-120">若要透過 PowerShell 刪除 Compose 應用程式，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="c865e-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="c865e-121">使用 Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="c865e-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="c865e-122">或者，您也可以使用下列 Service Fabric CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="c865e-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="c865e-123">您建立應用程式之後，可以使用下列命令檢查其狀態：</span><span class="sxs-lookup"><span data-stu-id="c865e-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="c865e-124">若要刪除該 Compose 應用程式，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="c865e-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="c865e-125">支援的撰寫指示詞</span><span class="sxs-lookup"><span data-stu-id="c865e-125">Supported Compose directives</span></span>

<span data-ttu-id="c865e-126">此預覽支援 Compose 第 3 版格式的組態選項子集，包括下列基本項目：</span><span class="sxs-lookup"><span data-stu-id="c865e-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="c865e-127">服務 > 部署 > 複本</span><span class="sxs-lookup"><span data-stu-id="c865e-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="c865e-128">服務 > 部署 > 放置 > 條件約束</span><span class="sxs-lookup"><span data-stu-id="c865e-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="c865e-129">服務 > 部署 > 資源 > 限制</span><span class="sxs-lookup"><span data-stu-id="c865e-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="c865e-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="c865e-130">-cpu-shares</span></span>
    * <span data-ttu-id="c865e-131">-memory</span><span class="sxs-lookup"><span data-stu-id="c865e-131">-memory</span></span>
    * <span data-ttu-id="c865e-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="c865e-132">-memory-swap</span></span>
* <span data-ttu-id="c865e-133">服務 > 命令</span><span class="sxs-lookup"><span data-stu-id="c865e-133">Services > Commands</span></span>
* <span data-ttu-id="c865e-134">服務 > 環境</span><span class="sxs-lookup"><span data-stu-id="c865e-134">Services > Environment</span></span>
* <span data-ttu-id="c865e-135">服務 > 連接埠</span><span class="sxs-lookup"><span data-stu-id="c865e-135">Services > Ports</span></span>
* <span data-ttu-id="c865e-136">服務 > 映像</span><span class="sxs-lookup"><span data-stu-id="c865e-136">Services > Image</span></span>
* <span data-ttu-id="c865e-137">服務 > 隔離 (僅適用於 Windows)</span><span class="sxs-lookup"><span data-stu-id="c865e-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="c865e-138">服務 > 記錄 > 驅動程式</span><span class="sxs-lookup"><span data-stu-id="c865e-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="c865e-139">服務 > 記錄 > 驅動程式 > 選項</span><span class="sxs-lookup"><span data-stu-id="c865e-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="c865e-140">磁碟區與部署 > 磁碟區</span><span class="sxs-lookup"><span data-stu-id="c865e-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="c865e-141">設定叢集，以便強制執行資源限制，如 [Service Fabric 資源管理](service-fabric-resource-governance.md) (英文) 中所述。</span><span class="sxs-lookup"><span data-stu-id="c865e-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="c865e-142">此預覽不支援所有其他的 Docker Compose 指示詞。</span><span class="sxs-lookup"><span data-stu-id="c865e-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="c865e-143">ServiceDnsName 計算</span><span class="sxs-lookup"><span data-stu-id="c865e-143">ServiceDnsName computation</span></span>

<span data-ttu-id="c865e-144">如果在 Compose 檔案中指定的服務名稱是完整的網域名稱 (亦即包含點 [.])，則由 Service Fabric 註冊的 DNS 名稱為 `<ServiceName>` (包含點)。</span><span class="sxs-lookup"><span data-stu-id="c865e-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="c865e-145">如果不是，則應用程式名稱中的每個路徑線段會變成服務 DNS 名稱中的網域標籤，其中的第一個路徑線段會變成最上層的網域標籤。</span><span class="sxs-lookup"><span data-stu-id="c865e-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="c865e-146">例如，如果指定的應用程式名稱是 `fabric:/SampleApp/MyComposeApp`，則 `<ServiceName>.MyComposeApp.SampleApp` 會是註冊的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="c865e-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="c865e-147">Compose (執行個體定義) 與 Service Fabric 應用程式模型 (類型定義) 之間的差異</span><span class="sxs-lookup"><span data-stu-id="c865e-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="c865e-148">docker-compose.yml 檔案描述一組可部署的容器，包括其屬性與組態。</span><span class="sxs-lookup"><span data-stu-id="c865e-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="c865e-149">例如，此檔案可包含環境變數與連接埠。</span><span class="sxs-lookup"><span data-stu-id="c865e-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="c865e-150">您也可以在 docker-compose.yml 檔案中指定放置條件約束、資源限制及 DNS 名稱等部署參數。</span><span class="sxs-lookup"><span data-stu-id="c865e-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="c865e-151">[Service Fabric 應用程式模型](service-fabric-application-model.md)使用服務類型與應用程式類型，其中您可以有許多相同類型的應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="c865e-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="c865e-152">例如，可以讓每個客戶有一個應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="c865e-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="c865e-153">這個以類型為基礎的模型支援同一個向執行階段註冊之應用程式的多個版本。</span><span class="sxs-lookup"><span data-stu-id="c865e-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="c865e-154">例如，客戶 A 可以有一個以類型 1.0 的 AppTypeA 具現化的應用程式，客戶 B 可以有另一個以相同類型與版本具現化的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c865e-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="c865e-155">您在應用程式資訊清單中定義應用程式類型，並且在建立應用程式時指定應用程式名稱與部署參數。</span><span class="sxs-lookup"><span data-stu-id="c865e-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="c865e-156">雖然此模型提供彈性，但我們也正在規劃支援更簡單、以執行個體為基礎的部署類型，其中類型在資訊清單檔案中是隱含的。</span><span class="sxs-lookup"><span data-stu-id="c865e-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="c865e-157">在此模型中，每個應用程式會取得自己的獨立資訊清單。</span><span class="sxs-lookup"><span data-stu-id="c865e-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="c865e-158">我們正在透過新增對 docker-compose.yml (這是以執行個體為基礎的部署格式) 的支援來預覽此成果。</span><span class="sxs-lookup"><span data-stu-id="c865e-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c865e-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c865e-159">Next steps</span></span>

* <span data-ttu-id="c865e-160">參閱 [Service Fabric 應用程式模型](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="c865e-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="c865e-161">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="c865e-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
