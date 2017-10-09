---
title: "aaaRun Linux 虛擬機器上的計算節點-Azure 批次 |Microsoft 文件"
description: "了解如何 tooprocess 平行計算工作負載上的 Azure 批次中的 Linux 虛擬機器的集區。"
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="5acbc-103">在 Batch 集區中佈建 Linux 計算節點</span><span class="sxs-lookup"><span data-stu-id="5acbc-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="5acbc-104">您可以在 Linux 和 Windows 虛擬機器上使用 Azure Batch toorun 平行計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="5acbc-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="5acbc-105">這篇文章說明如何的 Linux toocreate 集區中的計算節點 hello 批次服務使用這兩個 hello[批次 Python] [ py_batch_package]和[批次.NET] [ api_net]用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="5acbc-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="5acbc-106">在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="5acbc-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="5acbc-107">只有建立 hello 集區時使用的雲端服務組態，10 年 3 月 2016年和 5 年 7 月 2017年之間建立的批次集區中支援它們。</span><span class="sxs-lookup"><span data-stu-id="5acbc-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="5acbc-108">建立先前 too10 2016 年 3 月的批次集區不支援應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="5acbc-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="5acbc-109">如需有關使用應用程式套件 toodeploy 您應用程式 tooyour 批次的節點，請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="5acbc-110">虛擬機器組態</span><span class="sxs-lookup"><span data-stu-id="5acbc-110">Virtual machine configuration</span></span>
<span data-ttu-id="5acbc-111">當您在批次中建立計算節點的集區時，您有兩個選項其中 tooselect hello 節點大小和作業系統： 雲端服務組態和虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="5acbc-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="5acbc-112">**雲端服務組態**「只」提供 Windows 計算節點。</span><span class="sxs-lookup"><span data-stu-id="5acbc-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="5acbc-113">可執行的運算節點大小會列在[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)，而且可用的作業系統會列於 hello [Azure 客體作業系統版本與 SDK 相容性比較表](../cloud-services/cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="5acbc-114">當您建立包含 Azure 雲端服務節點的集區時，您指定 hello 節點大小和 hello 作業系統系列，如下所述 hello 先前所述的發行項。</span><span class="sxs-lookup"><span data-stu-id="5acbc-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="5acbc-115">針對 Windows 計算節點的集區，最常使用的是雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5acbc-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="5acbc-116">**虛擬機器組態** 可提供適用於計算節點的 Linux 和 Windows 映像。</span><span class="sxs-lookup"><span data-stu-id="5acbc-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="5acbc-117">可用的計算節點大小列於 [Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) 和 [Azure 中的虛擬機器大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="5acbc-118">當您建立包含虛擬機器組態節點的集區時，您必須指定 hello 大小 hello 節點、 hello 虛擬機器映像參考，以及 hello 批次節點代理程式 SKU toobe hello 節點上安裝。</span><span class="sxs-lookup"><span data-stu-id="5acbc-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="5acbc-119">虛擬機器映像參考</span><span class="sxs-lookup"><span data-stu-id="5acbc-119">Virtual machine image reference</span></span>
<span data-ttu-id="5acbc-120">hello 批次服務會使用[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)tooprovide Linux 計算節點。</span><span class="sxs-lookup"><span data-stu-id="5acbc-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="5acbc-121">您可以指定映像從 hello [Azure Marketplace][vm_marketplace]，或提供您準備自訂映像。</span><span class="sxs-lookup"><span data-stu-id="5acbc-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="5acbc-122">如需自訂映像的詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#pool)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="5acbc-123">當您設定的虛擬機器映像參考時，您會指定 hello hello 虛擬機器映像內容。</span><span class="sxs-lookup"><span data-stu-id="5acbc-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="5acbc-124">當您建立的虛擬機器映像參考時，還需要下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="5acbc-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="5acbc-125">**映像參考屬性**</span><span class="sxs-lookup"><span data-stu-id="5acbc-125">**Image reference properties**</span></span> | <span data-ttu-id="5acbc-126">**範例**</span><span class="sxs-lookup"><span data-stu-id="5acbc-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="5acbc-127">發行者</span><span class="sxs-lookup"><span data-stu-id="5acbc-127">Publisher</span></span> |<span data-ttu-id="5acbc-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="5acbc-128">Canonical</span></span> |
| <span data-ttu-id="5acbc-129">提供項目</span><span class="sxs-lookup"><span data-stu-id="5acbc-129">Offer</span></span> |<span data-ttu-id="5acbc-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-130">UbuntuServer</span></span> |
| <span data-ttu-id="5acbc-131">SKU</span><span class="sxs-lookup"><span data-stu-id="5acbc-131">SKU</span></span> |<span data-ttu-id="5acbc-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="5acbc-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="5acbc-133">版本</span><span class="sxs-lookup"><span data-stu-id="5acbc-133">Version</span></span> |<span data-ttu-id="5acbc-134">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="5acbc-135">您可以進一步了解這些屬性和 toolist Marketplace 中的映像[瀏覽並選取使用 CLI 或 PowerShell 的 Azure 中的 Linux 虛擬機器映像](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5acbc-136">請注意，並非所有 Marketplace 映像目前都與 Batch 相容。</span><span class="sxs-lookup"><span data-stu-id="5acbc-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="5acbc-137">如需詳細資訊，請參閱 [節點代理程式 SKU](#node-agent-sku)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="5acbc-138">節點代理程式 SKU</span><span class="sxs-lookup"><span data-stu-id="5acbc-138">Node agent SKU</span></span>
<span data-ttu-id="5acbc-139">hello 批次節點代理程式是 hello 集區中的每個節點上執行，並提供 hello 節點與 hello 批次服務之間的 hello 命令控制項介面的程式。</span><span class="sxs-lookup"><span data-stu-id="5acbc-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="5acbc-140">有不同的實作方式的 hello 節點代理程式，稱為不同作業系統的 Sku。</span><span class="sxs-lookup"><span data-stu-id="5acbc-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="5acbc-141">基本上，當您建立虛擬機器組態，您首先要指定 hello 虛擬機器映像參考，，然後指定 hello 節點代理程式 tooinstall hello 映像上。</span><span class="sxs-lookup"><span data-stu-id="5acbc-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="5acbc-142">一般而言，每個節點代理程式可與多個虛擬機器映像 SKU 相容。</span><span class="sxs-lookup"><span data-stu-id="5acbc-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="5acbc-143">以下是一些節點代理程式的 SKU 的範例︰</span><span class="sxs-lookup"><span data-stu-id="5acbc-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="5acbc-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="5acbc-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="5acbc-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-145">batch.node.centos 7</span></span>
* <span data-ttu-id="5acbc-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="5acbc-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5acbc-147">並非所有 hello Marketplace 中都可用的虛擬機器映像都都相容 hello 目前可用批次 節點的代理程式。</span><span class="sxs-lookup"><span data-stu-id="5acbc-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="5acbc-148">使用 hello 批次 Sdk toolist hello 可用的節點代理程式 Sku 和 hello 與它們彼此相容的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="5acbc-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="5acbc-149">請參閱 hello[清單的虛擬機器映像](#list-of-virtual-machine-images)本文稍後如需詳細資訊和方式的範例 tooretrieve 有效的映像，在執行階段清單。</span><span class="sxs-lookup"><span data-stu-id="5acbc-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="5acbc-150">建立 Linux 集區︰Batch Python</span><span class="sxs-lookup"><span data-stu-id="5acbc-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="5acbc-151">hello 下列程式碼片段示範如何 toouse hello [Microsoft Azure 批次用戶端程式庫的 Python] [ py_batch_package] toocreate Ubuntu 伺服器集區計算節點。</span><span class="sxs-lookup"><span data-stu-id="5acbc-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="5acbc-152">參考文件以 hello 批次 Python 模組，請參閱[azure.batch 封裝][ py_batch_docs]上讀取 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="5acbc-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="5acbc-153">此程式碼片段會明確建立 [ImageReference][py_imagereference]，並指定其每一個屬性 (發行者、優惠、SKU、版本)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="5acbc-154">在實際執行程式碼，不過，我們建議您使用 hello [list_node_agent_skus] [ py_list_skus]方法 toodetermine，然後選取從 hello 可用映像和節點代理程式 SKU 組合在執行階段。</span><span class="sxs-lookup"><span data-stu-id="5acbc-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="5acbc-155">如先前所述，我們建議，而不是建立 hello [ImageReference] [ py_imagereference]您明確地使用 hello [list_node_agent_skus] [ py_list_skus]從 hello 方法 toodynamically 選取目前支援的節點代理程式/Marketplace 映像的組合。</span><span class="sxs-lookup"><span data-stu-id="5acbc-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="5acbc-156">hello 下列 Python 程式碼片段說明如何 toouse 這個方法。</span><span class="sxs-lookup"><span data-stu-id="5acbc-156">hello following Python snippet shows how toouse this method.</span></span>

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="5acbc-157">建立 Linux 集區︰Batch .NET</span><span class="sxs-lookup"><span data-stu-id="5acbc-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="5acbc-158">hello 下列程式碼片段示範如何 toouse hello[批次.NET] [ nuget_batch_net]用戶端程式庫 toocreate Ubuntu 伺服器集區計算節點。</span><span class="sxs-lookup"><span data-stu-id="5acbc-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="5acbc-159">您可以找到 hello[批次.NET 參考文件][ api_net] MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="5acbc-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="5acbc-160">hello 下列程式碼片段會使用 hello [PoolOperations][net_pool_ops]。[ListNodeAgentSkus] [ net_list_skus]方法 tooselect hello 清單中的目前支援 Marketplace 映像和節點代理程式 SKU 的組合。</span><span class="sxs-lookup"><span data-stu-id="5acbc-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="5acbc-161">這項技術是合理的因為 hello 清單支援的組合可能會從時間 tootime 變更。</span><span class="sxs-lookup"><span data-stu-id="5acbc-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="5acbc-162">最常見的是新增支援的組合。</span><span class="sxs-lookup"><span data-stu-id="5acbc-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

<span data-ttu-id="5acbc-163">雖然 hello 先前程式碼片段使用 hello [PoolOperations][net_pool_ops]。[ListNodeAgentSkus] [ net_list_skus]方法 toodynamically 清單，然後選取從支援 （建議選項） 的映像和節點代理程式 SKU 組合，您也可以設定[ImageReference] [ net_imagereference]明確：</span><span class="sxs-lookup"><span data-stu-id="5acbc-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="5acbc-164">虛擬機器映像的清單</span><span class="sxs-lookup"><span data-stu-id="5acbc-164">List of virtual machine images</span></span>
<span data-ttu-id="5acbc-165">hello 下表列出 hello Marketplace 虛擬機器映像與相容的 hello 可用批次 節點的代理程式上次更新此文件。</span><span class="sxs-lookup"><span data-stu-id="5acbc-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="5acbc-166">這份清單不可靠，因為映像和節點代理程式可能會加入或移除在任何時間的重要 toonote 它。</span><span class="sxs-lookup"><span data-stu-id="5acbc-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="5acbc-167">我們建議您批次應用程式和服務永遠使用[list_node_agent_skus] [ py_list_skus] (Python) 和[ListNodeAgentSkus] [ net_list_skus]Toodetermine （批次.NET），然後選取從 hello 目前可用的 Sku。</span><span class="sxs-lookup"><span data-stu-id="5acbc-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="5acbc-168">下列清單中的 hello 可能隨時變更。</span><span class="sxs-lookup"><span data-stu-id="5acbc-168">hello following list may change at any time.</span></span> <span data-ttu-id="5acbc-169">一律使用 hello**清單節點代理程式 SKU** hello 批次 Api toolist 中可用的方法 hello 相容的虛擬機器和節點代理程式 Sku 當您執行批次作業。</span><span class="sxs-lookup"><span data-stu-id="5acbc-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="5acbc-170">**發行者**</span><span class="sxs-lookup"><span data-stu-id="5acbc-170">**Publisher**</span></span> | <span data-ttu-id="5acbc-171">**提供項目**</span><span class="sxs-lookup"><span data-stu-id="5acbc-171">**Offer**</span></span> | <span data-ttu-id="5acbc-172">**映像 SKU**</span><span class="sxs-lookup"><span data-stu-id="5acbc-172">**Image SKU**</span></span> | <span data-ttu-id="5acbc-173">**版本**</span><span class="sxs-lookup"><span data-stu-id="5acbc-173">**Version**</span></span> | <span data-ttu-id="5acbc-174">**節點代理程式 SKU 識別碼**</span><span class="sxs-lookup"><span data-stu-id="5acbc-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="5acbc-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="5acbc-175">Canonical</span></span> | <span data-ttu-id="5acbc-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-176">UbuntuServer</span></span> | <span data-ttu-id="5acbc-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="5acbc-177">14.04.5-LTS</span></span> | <span data-ttu-id="5acbc-178">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-178">latest</span></span> | <span data-ttu-id="5acbc-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="5acbc-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="5acbc-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="5acbc-180">Canonical</span></span> | <span data-ttu-id="5acbc-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-181">UbuntuServer</span></span> | <span data-ttu-id="5acbc-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="5acbc-182">16.04.0-LTS</span></span> | <span data-ttu-id="5acbc-183">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-183">latest</span></span> | <span data-ttu-id="5acbc-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="5acbc-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="5acbc-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="5acbc-185">Credativ</span></span> | <span data-ttu-id="5acbc-186">Debian</span><span class="sxs-lookup"><span data-stu-id="5acbc-186">Debian</span></span> | <span data-ttu-id="5acbc-187">8</span><span class="sxs-lookup"><span data-stu-id="5acbc-187">8</span></span> | <span data-ttu-id="5acbc-188">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-188">latest</span></span> | <span data-ttu-id="5acbc-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="5acbc-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="5acbc-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="5acbc-190">OpenLogic</span></span> | <span data-ttu-id="5acbc-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="5acbc-191">CentOS</span></span> | <span data-ttu-id="5acbc-192">7.0</span><span class="sxs-lookup"><span data-stu-id="5acbc-192">7.0</span></span> | <span data-ttu-id="5acbc-193">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-193">latest</span></span> | <span data-ttu-id="5acbc-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="5acbc-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="5acbc-195">OpenLogic</span></span> | <span data-ttu-id="5acbc-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="5acbc-196">CentOS</span></span> | <span data-ttu-id="5acbc-197">7.1</span><span class="sxs-lookup"><span data-stu-id="5acbc-197">7.1</span></span> | <span data-ttu-id="5acbc-198">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-198">latest</span></span> | <span data-ttu-id="5acbc-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="5acbc-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="5acbc-200">OpenLogic</span></span> | <span data-ttu-id="5acbc-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="5acbc-201">CentOS-HPC</span></span> | <span data-ttu-id="5acbc-202">7.1</span><span class="sxs-lookup"><span data-stu-id="5acbc-202">7.1</span></span> | <span data-ttu-id="5acbc-203">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-203">latest</span></span> | <span data-ttu-id="5acbc-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="5acbc-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="5acbc-205">OpenLogic</span></span> | <span data-ttu-id="5acbc-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="5acbc-206">CentOS</span></span> | <span data-ttu-id="5acbc-207">7.2</span><span class="sxs-lookup"><span data-stu-id="5acbc-207">7.2</span></span> | <span data-ttu-id="5acbc-208">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-208">latest</span></span> | <span data-ttu-id="5acbc-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="5acbc-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="5acbc-210">Oracle</span></span> | <span data-ttu-id="5acbc-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="5acbc-211">Oracle-Linux</span></span> | <span data-ttu-id="5acbc-212">7.0</span><span class="sxs-lookup"><span data-stu-id="5acbc-212">7.0</span></span> | <span data-ttu-id="5acbc-213">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-213">latest</span></span> | <span data-ttu-id="5acbc-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="5acbc-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="5acbc-215">Oracle</span></span> | <span data-ttu-id="5acbc-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="5acbc-216">Oracle-Linux</span></span> | <span data-ttu-id="5acbc-217">7.2</span><span class="sxs-lookup"><span data-stu-id="5acbc-217">7.2</span></span> | <span data-ttu-id="5acbc-218">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-218">latest</span></span> | <span data-ttu-id="5acbc-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="5acbc-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="5acbc-220">SUSE</span></span> | <span data-ttu-id="5acbc-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="5acbc-221">openSUSE</span></span> | <span data-ttu-id="5acbc-222">13.2</span><span class="sxs-lookup"><span data-stu-id="5acbc-222">13.2</span></span> | <span data-ttu-id="5acbc-223">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-223">latest</span></span> | <span data-ttu-id="5acbc-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="5acbc-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="5acbc-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="5acbc-225">SUSE</span></span> | <span data-ttu-id="5acbc-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="5acbc-226">openSUSE-Leap</span></span> | <span data-ttu-id="5acbc-227">42.1</span><span class="sxs-lookup"><span data-stu-id="5acbc-227">42.1</span></span> | <span data-ttu-id="5acbc-228">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-228">latest</span></span> | <span data-ttu-id="5acbc-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="5acbc-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="5acbc-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="5acbc-230">SUSE</span></span> | <span data-ttu-id="5acbc-231">SLES</span><span class="sxs-lookup"><span data-stu-id="5acbc-231">SLES</span></span> | <span data-ttu-id="5acbc-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="5acbc-232">12-SP1</span></span> | <span data-ttu-id="5acbc-233">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-233">latest</span></span> | <span data-ttu-id="5acbc-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="5acbc-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="5acbc-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="5acbc-235">SUSE</span></span> | <span data-ttu-id="5acbc-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="5acbc-236">SLES-HPC</span></span> | <span data-ttu-id="5acbc-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="5acbc-237">12-SP1</span></span> | <span data-ttu-id="5acbc-238">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-238">latest</span></span> | <span data-ttu-id="5acbc-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="5acbc-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="5acbc-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="5acbc-240">microsoft-ads</span></span> | <span data-ttu-id="5acbc-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="5acbc-241">linux-data-science-vm</span></span> | <span data-ttu-id="5acbc-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="5acbc-242">linuxdsvm</span></span> | <span data-ttu-id="5acbc-243">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-243">latest</span></span> | <span data-ttu-id="5acbc-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="5acbc-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="5acbc-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="5acbc-245">microsoft-ads</span></span> | <span data-ttu-id="5acbc-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="5acbc-246">standard-data-science-vm</span></span> | <span data-ttu-id="5acbc-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="5acbc-247">standard-data-science-vm</span></span> | <span data-ttu-id="5acbc-248">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-248">latest</span></span> | <span data-ttu-id="5acbc-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="5acbc-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="5acbc-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="5acbc-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-251">WindowsServer</span></span> | <span data-ttu-id="5acbc-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="5acbc-252">2008-R2-SP1</span></span> | <span data-ttu-id="5acbc-253">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-253">latest</span></span> | <span data-ttu-id="5acbc-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="5acbc-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="5acbc-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="5acbc-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-256">WindowsServer</span></span> | <span data-ttu-id="5acbc-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="5acbc-257">2012-Datacenter</span></span> | <span data-ttu-id="5acbc-258">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-258">latest</span></span> | <span data-ttu-id="5acbc-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="5acbc-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="5acbc-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="5acbc-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-261">WindowsServer</span></span> | <span data-ttu-id="5acbc-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="5acbc-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="5acbc-263">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-263">latest</span></span> | <span data-ttu-id="5acbc-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="5acbc-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="5acbc-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="5acbc-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-266">WindowsServer</span></span> | <span data-ttu-id="5acbc-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="5acbc-267">2016-Datacenter</span></span> | <span data-ttu-id="5acbc-268">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-268">latest</span></span> | <span data-ttu-id="5acbc-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="5acbc-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="5acbc-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="5acbc-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5acbc-271">WindowsServer</span></span> | <span data-ttu-id="5acbc-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="5acbc-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="5acbc-273">最新</span><span class="sxs-lookup"><span data-stu-id="5acbc-273">latest</span></span> | <span data-ttu-id="5acbc-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="5acbc-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="5acbc-275">連接使用 SSH tooLinux 節點</span><span class="sxs-lookup"><span data-stu-id="5acbc-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="5acbc-276">在開發期間或問題進行疑難排解時，您可能會發現需要 toosign toohello 集區中的節點中。</span><span class="sxs-lookup"><span data-stu-id="5acbc-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="5acbc-277">不同於 Windows 計算節點，您無法使用遠端桌面通訊協定 (RDP) tooconnect tooLinux 節點。</span><span class="sxs-lookup"><span data-stu-id="5acbc-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="5acbc-278">相反地，hello 批次服務可讓您遠端連線的每個節點上的 SSH 存取。</span><span class="sxs-lookup"><span data-stu-id="5acbc-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="5acbc-279">hello 下列 Python 程式碼片段會建立使用者所需的遠端連線集區中的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="5acbc-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="5acbc-280">接著，它會列印每個節點的 hello 安全殼層 (SSH) 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="5acbc-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="5acbc-281">以下是包含四個 Linux 節點集區 hello 先前的程式碼的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="5acbc-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="5acbc-282">在節點上建立使用者時，不要使用密碼，而是可以指定 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="5acbc-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="5acbc-283">在 hello Python SDK，使用 hello **ssh_public_key**參數[ComputeNodeUser][py_computenodeuser]。</span><span class="sxs-lookup"><span data-stu-id="5acbc-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="5acbc-284">在.NET 中，使用 hello [ComputeNodeUser][net_computenodeuser]。[SshPublicKey] [ net_ssh_key]屬性。</span><span class="sxs-lookup"><span data-stu-id="5acbc-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="5acbc-285">價格</span><span class="sxs-lookup"><span data-stu-id="5acbc-285">Pricing</span></span>
<span data-ttu-id="5acbc-286">Azure Batch 採用 Azure 雲端服務和 Azure 虛擬機器技術。</span><span class="sxs-lookup"><span data-stu-id="5acbc-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="5acbc-287">hello 批次服務本身則提供給不花一毛錢，這表示您必須只支付 hello 計算您批次的解決方案使用的資源。</span><span class="sxs-lookup"><span data-stu-id="5acbc-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="5acbc-288">當您選擇**雲端服務設定**，您的收費依據 hello[雲端服務定價][ cloud_services_pricing]結構。</span><span class="sxs-lookup"><span data-stu-id="5acbc-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="5acbc-289">當您選擇**虛擬機器組態**，您的收費依據 hello[虛擬機器定價][ vm_pricing]結構。</span><span class="sxs-lookup"><span data-stu-id="5acbc-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="5acbc-290">如果您部署應用程式使用的 tooyour 批次節點[應用程式封裝](batch-application-packages.md)，您也需要付費 hello Azure 儲存體資源的應用程式封裝使用。</span><span class="sxs-lookup"><span data-stu-id="5acbc-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="5acbc-291">一般情況下，hello Azure 儲存體成本很低。</span><span class="sxs-lookup"><span data-stu-id="5acbc-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5acbc-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5acbc-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="5acbc-293">Batch Python 教學課程</span><span class="sxs-lookup"><span data-stu-id="5acbc-293">Batch Python tutorial</span></span>
<span data-ttu-id="5acbc-294">更深入的教學課程中，有關如何使用 Python，簽出與批次 toowork[開始 hello Azure 批次 Python 用戶端使用](batch-python-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="5acbc-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="5acbc-295">其附屬[程式碼範例][ github_samples_pyclient]包含協助程式函式， `get_vm_config_for_distro`，它會顯示另一個技術 tooobtain 虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="5acbc-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="5acbc-296">Batch Python 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="5acbc-296">Batch Python code samples</span></span>
<span data-ttu-id="5acbc-297">hello [Python 程式碼範例][ github_samples_py]在 hello [azure 批次範例][ github_samples] GitHub 上的儲存機制包含指令碼，教您如何 tooperform一般批次作業，例如集區、 工作和工作的建立。</span><span class="sxs-lookup"><span data-stu-id="5acbc-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="5acbc-298">hello[讀我檔案][ github_py_readme] ，伴隨著 hello Python 範例包含有關如何 tooinstall hello 所需封裝的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5acbc-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="5acbc-299">批次論壇</span><span class="sxs-lookup"><span data-stu-id="5acbc-299">Batch forum</span></span>
<span data-ttu-id="5acbc-300">hello [Azure Batch 論壇][ forum] MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。</span><span class="sxs-lookup"><span data-stu-id="5acbc-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="5acbc-301">請閱讀實用的「釘選」文章，並在建置 Batch 解決方案時，若發生問題就張貼問題。</span><span class="sxs-lookup"><span data-stu-id="5acbc-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
