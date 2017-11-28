---
title: "在虛擬機器計算節點上執行 Linux - Azure Batch | Microsoft Docs"
description: "了解如何在 Azure Batch 中處理您的 Linux 虛擬機器集區的平行計算工作負載。"
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
ms.openlocfilehash: 9b2257917e2368478beb75957677de23d4157865
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="1d717-103">在 Batch 集區中佈建 Linux 計算節點</span><span class="sxs-lookup"><span data-stu-id="1d717-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="1d717-104">您可以使用 Azure Batch 同時在 Linux 和 Windows 虛擬機器上執行平行計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="1d717-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="1d717-105">本文將詳細說明如何使用 [Batch Python][py_batch_package] 和 [Batch .NET][api_net] 用戶端程式庫，在 Batch 服務中建立 Linux 計算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="1d717-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="1d717-106">在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="1d717-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="1d717-107">只有在使用雲端服務設定建立集區時，在 2016 年 3 月 10 日與 2017 年 7 月 5 日之間所建立的 Batch 集區上才支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="1d717-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="1d717-108">在 2016 年 3 月 10 日之前建立的 Batch 集區不支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="1d717-108">Batch pools created prior to 10 March 2016 do not support application packages.</span></span> <span data-ttu-id="1d717-109">如需使用應用程式套件將應用程式部署至 Batch 節點的詳細資訊，請參閱[使用 Batch 應用程式套件將應用程式部署至計算節點](batch-application-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="1d717-109">For more information about using application packages to deploy your applications to your Batch nodes, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="1d717-110">虛擬機器組態</span><span class="sxs-lookup"><span data-stu-id="1d717-110">Virtual machine configuration</span></span>
<span data-ttu-id="1d717-111">在 Batch 中建立計算節點集區時，有兩個選項可選取節點大小和作業系統︰雲端服務組態和虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="1d717-111">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="1d717-112">**雲端服務組態**「只」提供 Windows 計算節點。</span><span class="sxs-lookup"><span data-stu-id="1d717-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="1d717-113">可用的計算節點大小列於[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)，而可用的作業系統則列於 [Azure 客體 OS 版次與 SDK 相容性矩陣](../cloud-services/cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="1d717-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="1d717-114">在建立包含 Azure 雲端服務節點的集區時，您要指定節點大小和其 OS 系列，先前提到的文章中會說明這些內容。</span><span class="sxs-lookup"><span data-stu-id="1d717-114">When you create a pool that contains Azure Cloud Services nodes, you specify the node size and the OS family, which are described in the previously mentioned articles.</span></span> <span data-ttu-id="1d717-115">針對 Windows 計算節點的集區，最常使用的是雲端服務。</span><span class="sxs-lookup"><span data-stu-id="1d717-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="1d717-116">**虛擬機器組態** 可提供適用於計算節點的 Linux 和 Windows 映像。</span><span class="sxs-lookup"><span data-stu-id="1d717-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="1d717-117">可用的計算節點大小列於 [Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) 和 [Azure 中的虛擬機器大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)。</span><span class="sxs-lookup"><span data-stu-id="1d717-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="1d717-118">在建立包含虛擬機器組態節點的集區時，您必須指定節點大小、虛擬機器映像參考以及要在節點上安裝的 Batch 節點代理程式 SKU。</span><span class="sxs-lookup"><span data-stu-id="1d717-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="1d717-119">虛擬機器映像參考</span><span class="sxs-lookup"><span data-stu-id="1d717-119">Virtual machine image reference</span></span>
<span data-ttu-id="1d717-120">Batch 服務使用[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)來提供 Linux 計算節點。</span><span class="sxs-lookup"><span data-stu-id="1d717-120">The Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide Linux compute nodes.</span></span> <span data-ttu-id="1d717-121">您可以指定來自 [Azure Marketplace][vm_marketplace] 的映像，或提供您準備好的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="1d717-121">You can specify an image from the [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="1d717-122">如需自訂映像的詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#pool)。</span><span class="sxs-lookup"><span data-stu-id="1d717-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="1d717-123">設定虛擬機器映像參考時，您會指定虛擬機器映像的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d717-123">When you configure a virtual machine image reference, you specify the properties of the virtual machine image.</span></span> <span data-ttu-id="1d717-124">建立虛擬機器映像參考時，會需要下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="1d717-124">The following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="1d717-125">**映像參考屬性**</span><span class="sxs-lookup"><span data-stu-id="1d717-125">**Image reference properties**</span></span> | <span data-ttu-id="1d717-126">**範例**</span><span class="sxs-lookup"><span data-stu-id="1d717-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="1d717-127">發行者</span><span class="sxs-lookup"><span data-stu-id="1d717-127">Publisher</span></span> |<span data-ttu-id="1d717-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="1d717-128">Canonical</span></span> |
| <span data-ttu-id="1d717-129">提供項目</span><span class="sxs-lookup"><span data-stu-id="1d717-129">Offer</span></span> |<span data-ttu-id="1d717-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1d717-130">UbuntuServer</span></span> |
| <span data-ttu-id="1d717-131">SKU</span><span class="sxs-lookup"><span data-stu-id="1d717-131">SKU</span></span> |<span data-ttu-id="1d717-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="1d717-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="1d717-133">版本</span><span class="sxs-lookup"><span data-stu-id="1d717-133">Version</span></span> |<span data-ttu-id="1d717-134">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="1d717-135">您可以在[使用 CLI 或 PowerShell 在 Azure 中巡覽並選取 Linux 虛擬機器映像](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中深入了解這些屬性，以及如何列出 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="1d717-135">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1d717-136">請注意，並非所有 Marketplace 映像目前都與 Batch 相容。</span><span class="sxs-lookup"><span data-stu-id="1d717-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="1d717-137">如需詳細資訊，請參閱 [節點代理程式 SKU](#node-agent-sku)。</span><span class="sxs-lookup"><span data-stu-id="1d717-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="1d717-138">節點代理程式 SKU</span><span class="sxs-lookup"><span data-stu-id="1d717-138">Node agent SKU</span></span>
<span data-ttu-id="1d717-139">Batch 節點代理程式是一項程式，會在集區中的每個節點上執行，並在節點與 Batch 服務之間提供命令和控制介面。</span><span class="sxs-lookup"><span data-stu-id="1d717-139">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="1d717-140">節點代理程式對不同作業系統有不同的實作方式，稱為 SKU。</span><span class="sxs-lookup"><span data-stu-id="1d717-140">There are different implementations of the node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="1d717-141">基本上，建立虛擬機器組態時，您必須先指定虛擬機器映像參考，然後指定要在其上安裝映像的代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="1d717-141">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span></span> <span data-ttu-id="1d717-142">一般而言，每個節點代理程式可與多個虛擬機器映像 SKU 相容。</span><span class="sxs-lookup"><span data-stu-id="1d717-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="1d717-143">以下是一些節點代理程式的 SKU 的範例︰</span><span class="sxs-lookup"><span data-stu-id="1d717-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="1d717-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="1d717-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="1d717-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-145">batch.node.centos 7</span></span>
* <span data-ttu-id="1d717-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1d717-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d717-147">並非 Marketplace 中所有可用的虛擬機器映像都與目前可用的 Batch 節點代理程式相容。</span><span class="sxs-lookup"><span data-stu-id="1d717-147">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span></span> <span data-ttu-id="1d717-148">使用 Batch SDK 來列出可用的節點代理程式 SKU 和其相容的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="1d717-148">Use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span></span> <span data-ttu-id="1d717-149">如需詳細資訊及如何在執行階段擷取有效映像清單的範例，請參閱本文稍後的[虛擬機器映像清單](#list-of-virtual-machine-images)。</span><span class="sxs-lookup"><span data-stu-id="1d717-149">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how to retrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="1d717-150">建立 Linux 集區︰Batch Python</span><span class="sxs-lookup"><span data-stu-id="1d717-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="1d717-151">下列程式碼片段舉例示範如何使用 [Python 適用的 Microsoft Azure Batch 用戶端程式庫][py_batch_package]來建立 Ubuntu Server 計算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="1d717-151">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="1d717-152">您可以在「閱讀文件」的 [azure.batch 套件][py_batch_docs]中找到 Batch Python 模組的參考文件。</span><span class="sxs-lookup"><span data-stu-id="1d717-152">Reference documentation for the Batch Python module can be found at [azure.batch package][py_batch_docs] on Read the Docs.</span></span>

<span data-ttu-id="1d717-153">此程式碼片段會明確建立 [ImageReference][py_imagereference]，並指定其每一個屬性 (發行者、優惠、SKU、版本)。</span><span class="sxs-lookup"><span data-stu-id="1d717-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="1d717-154">不過，在實際執行程式碼中，我們建議您使用 [list_node_agent_skus][py_list_skus] 方法，在執行階段判斷並從可用的映像和節點代理程式 SKU 組合中選取。</span><span class="sxs-lookup"><span data-stu-id="1d717-154">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span></span>

```python
# Import the required modules from the
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

# Initialize the Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure the start task for the pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies the Marketplace
# virtual machine image to install on the nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="1d717-155">如先前所述，我們建議不要明確建立 [ImageReference][py_imagereference]，而是使用 [list_node_agent_skus][py_list_skus] 方法，從目前支援的節點代理程式/Marketplace 映像組合中動態選取。</span><span class="sxs-lookup"><span data-stu-id="1d717-155">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="1d717-156">下列 Python 程式碼片段說明這個方法的使用方式。</span><span class="sxs-lookup"><span data-stu-id="1d717-156">The following Python snippet shows how to use this method.</span></span>

```python
# Get the list of node agents from the Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain the desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick the first image reference from the list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create the VirtualMachineConfiguration, specifying the VM image
# reference and the Batch node agent to be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="1d717-157">建立 Linux 集區︰Batch .NET</span><span class="sxs-lookup"><span data-stu-id="1d717-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="1d717-158">下列程式碼片段舉例示範如何使用 [Batch .NET][nuget_batch_net] 用戶端程式庫來建立 Ubuntu Server 計算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="1d717-158">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="1d717-159">您可以在 MSDN 上找到 [Batch .NET 參考文件][api_net]。</span><span class="sxs-lookup"><span data-stu-id="1d717-159">You can find the [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="1d717-160">下列程式碼片段使用 [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] 方法，從目前支援的 Marketplace 映像和節點代理程式 SKU 組合清單中選取。</span><span class="sxs-lookup"><span data-stu-id="1d717-160">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="1d717-161">這項技術最理想，因為支援的組合清單可能會隨著時間變更。</span><span class="sxs-lookup"><span data-stu-id="1d717-161">This technique is desirable because the list of supported combinations may change from time to time.</span></span> <span data-ttu-id="1d717-162">最常見的是新增支援的組合。</span><span class="sxs-lookup"><span data-stu-id="1d717-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us to select from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image
// that we wish to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the VirtualMachineConfiguration for use when actually
// creating the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create the unbound pool object using the VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit the pool to the Batch service
await pool.CommitAsync();
```

<span data-ttu-id="1d717-163">雖然先前的程式碼片段使用 [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] 方法，以動態列出並從支援的映像和節點代理程式 SKU 組合中選取 (建議)，您也可以明確設定 [ImageReference][net_imagereference]：</span><span class="sxs-lookup"><span data-stu-id="1d717-163">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="1d717-164">虛擬機器映像的清單</span><span class="sxs-lookup"><span data-stu-id="1d717-164">List of virtual machine images</span></span>
<span data-ttu-id="1d717-165">下表列出本文最後一次更新時，與可用 Batch 節點代理程式相容的 Marketplace 虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="1d717-165">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="1d717-166">請務必注意，此清單並非永久不變，因為可能隨時新增或移除映像和節點代理程式。</span><span class="sxs-lookup"><span data-stu-id="1d717-166">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="1d717-167">我們建議您的 Batch 應用程式和服務一律使用 [list_node_agent_skus][py_list_skus] (Python) 和 [ListNodeAgentSkus][net_list_skus] (Batch .NET)，以判斷並從目前可用的 SKU 中選取。</span><span class="sxs-lookup"><span data-stu-id="1d717-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="1d717-168">下列清單可能會隨時變更。</span><span class="sxs-lookup"><span data-stu-id="1d717-168">The following list may change at any time.</span></span> <span data-ttu-id="1d717-169">一律使用 Batch API 中提供的 **清單節點代理程式 SKU** 方法，在執行 Batch 作業時，列出相容的虛擬機器和節點代理程式的 SKU。</span><span class="sxs-lookup"><span data-stu-id="1d717-169">Always use the **list node agent SKU** methods available in the Batch APIs to list the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="1d717-170">**發行者**</span><span class="sxs-lookup"><span data-stu-id="1d717-170">**Publisher**</span></span> | <span data-ttu-id="1d717-171">**提供項目**</span><span class="sxs-lookup"><span data-stu-id="1d717-171">**Offer**</span></span> | <span data-ttu-id="1d717-172">**映像 SKU**</span><span class="sxs-lookup"><span data-stu-id="1d717-172">**Image SKU**</span></span> | <span data-ttu-id="1d717-173">**版本**</span><span class="sxs-lookup"><span data-stu-id="1d717-173">**Version**</span></span> | <span data-ttu-id="1d717-174">**節點代理程式 SKU 識別碼**</span><span class="sxs-lookup"><span data-stu-id="1d717-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="1d717-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="1d717-175">Canonical</span></span> | <span data-ttu-id="1d717-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1d717-176">UbuntuServer</span></span> | <span data-ttu-id="1d717-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="1d717-177">14.04.5-LTS</span></span> | <span data-ttu-id="1d717-178">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-178">latest</span></span> | <span data-ttu-id="1d717-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="1d717-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="1d717-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="1d717-180">Canonical</span></span> | <span data-ttu-id="1d717-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1d717-181">UbuntuServer</span></span> | <span data-ttu-id="1d717-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="1d717-182">16.04.0-LTS</span></span> | <span data-ttu-id="1d717-183">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-183">latest</span></span> | <span data-ttu-id="1d717-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1d717-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="1d717-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="1d717-185">Credativ</span></span> | <span data-ttu-id="1d717-186">Debian</span><span class="sxs-lookup"><span data-stu-id="1d717-186">Debian</span></span> | <span data-ttu-id="1d717-187">8</span><span class="sxs-lookup"><span data-stu-id="1d717-187">8</span></span> | <span data-ttu-id="1d717-188">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-188">latest</span></span> | <span data-ttu-id="1d717-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="1d717-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="1d717-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1d717-190">OpenLogic</span></span> | <span data-ttu-id="1d717-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="1d717-191">CentOS</span></span> | <span data-ttu-id="1d717-192">7.0</span><span class="sxs-lookup"><span data-stu-id="1d717-192">7.0</span></span> | <span data-ttu-id="1d717-193">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-193">latest</span></span> | <span data-ttu-id="1d717-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="1d717-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1d717-195">OpenLogic</span></span> | <span data-ttu-id="1d717-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="1d717-196">CentOS</span></span> | <span data-ttu-id="1d717-197">7.1</span><span class="sxs-lookup"><span data-stu-id="1d717-197">7.1</span></span> | <span data-ttu-id="1d717-198">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-198">latest</span></span> | <span data-ttu-id="1d717-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="1d717-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1d717-200">OpenLogic</span></span> | <span data-ttu-id="1d717-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="1d717-201">CentOS-HPC</span></span> | <span data-ttu-id="1d717-202">7.1</span><span class="sxs-lookup"><span data-stu-id="1d717-202">7.1</span></span> | <span data-ttu-id="1d717-203">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-203">latest</span></span> | <span data-ttu-id="1d717-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="1d717-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1d717-205">OpenLogic</span></span> | <span data-ttu-id="1d717-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="1d717-206">CentOS</span></span> | <span data-ttu-id="1d717-207">7.2</span><span class="sxs-lookup"><span data-stu-id="1d717-207">7.2</span></span> | <span data-ttu-id="1d717-208">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-208">latest</span></span> | <span data-ttu-id="1d717-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="1d717-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="1d717-210">Oracle</span></span> | <span data-ttu-id="1d717-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="1d717-211">Oracle-Linux</span></span> | <span data-ttu-id="1d717-212">7.0</span><span class="sxs-lookup"><span data-stu-id="1d717-212">7.0</span></span> | <span data-ttu-id="1d717-213">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-213">latest</span></span> | <span data-ttu-id="1d717-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="1d717-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="1d717-215">Oracle</span></span> | <span data-ttu-id="1d717-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="1d717-216">Oracle-Linux</span></span> | <span data-ttu-id="1d717-217">7.2</span><span class="sxs-lookup"><span data-stu-id="1d717-217">7.2</span></span> | <span data-ttu-id="1d717-218">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-218">latest</span></span> | <span data-ttu-id="1d717-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="1d717-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="1d717-220">SUSE</span></span> | <span data-ttu-id="1d717-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="1d717-221">openSUSE</span></span> | <span data-ttu-id="1d717-222">13.2</span><span class="sxs-lookup"><span data-stu-id="1d717-222">13.2</span></span> | <span data-ttu-id="1d717-223">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-223">latest</span></span> | <span data-ttu-id="1d717-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="1d717-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="1d717-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="1d717-225">SUSE</span></span> | <span data-ttu-id="1d717-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="1d717-226">openSUSE-Leap</span></span> | <span data-ttu-id="1d717-227">42.1</span><span class="sxs-lookup"><span data-stu-id="1d717-227">42.1</span></span> | <span data-ttu-id="1d717-228">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-228">latest</span></span> | <span data-ttu-id="1d717-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="1d717-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="1d717-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="1d717-230">SUSE</span></span> | <span data-ttu-id="1d717-231">SLES</span><span class="sxs-lookup"><span data-stu-id="1d717-231">SLES</span></span> | <span data-ttu-id="1d717-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="1d717-232">12-SP1</span></span> | <span data-ttu-id="1d717-233">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-233">latest</span></span> | <span data-ttu-id="1d717-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="1d717-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="1d717-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="1d717-235">SUSE</span></span> | <span data-ttu-id="1d717-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="1d717-236">SLES-HPC</span></span> | <span data-ttu-id="1d717-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="1d717-237">12-SP1</span></span> | <span data-ttu-id="1d717-238">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-238">latest</span></span> | <span data-ttu-id="1d717-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="1d717-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="1d717-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="1d717-240">microsoft-ads</span></span> | <span data-ttu-id="1d717-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="1d717-241">linux-data-science-vm</span></span> | <span data-ttu-id="1d717-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="1d717-242">linuxdsvm</span></span> | <span data-ttu-id="1d717-243">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-243">latest</span></span> | <span data-ttu-id="1d717-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1d717-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="1d717-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="1d717-245">microsoft-ads</span></span> | <span data-ttu-id="1d717-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="1d717-246">standard-data-science-vm</span></span> | <span data-ttu-id="1d717-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="1d717-247">standard-data-science-vm</span></span> | <span data-ttu-id="1d717-248">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-248">latest</span></span> | <span data-ttu-id="1d717-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1d717-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1d717-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1d717-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-251">WindowsServer</span></span> | <span data-ttu-id="1d717-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="1d717-252">2008-R2-SP1</span></span> | <span data-ttu-id="1d717-253">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-253">latest</span></span> | <span data-ttu-id="1d717-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1d717-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1d717-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1d717-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-256">WindowsServer</span></span> | <span data-ttu-id="1d717-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="1d717-257">2012-Datacenter</span></span> | <span data-ttu-id="1d717-258">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-258">latest</span></span> | <span data-ttu-id="1d717-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1d717-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1d717-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1d717-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-261">WindowsServer</span></span> | <span data-ttu-id="1d717-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="1d717-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="1d717-263">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-263">latest</span></span> | <span data-ttu-id="1d717-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1d717-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1d717-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1d717-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-266">WindowsServer</span></span> | <span data-ttu-id="1d717-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="1d717-267">2016-Datacenter</span></span> | <span data-ttu-id="1d717-268">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-268">latest</span></span> | <span data-ttu-id="1d717-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1d717-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1d717-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1d717-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1d717-271">WindowsServer</span></span> | <span data-ttu-id="1d717-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="1d717-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="1d717-273">最新</span><span class="sxs-lookup"><span data-stu-id="1d717-273">latest</span></span> | <span data-ttu-id="1d717-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1d717-274">batch.node.windows amd64</span></span> |

## <a name="connect-to-linux-nodes-using-ssh"></a><span data-ttu-id="1d717-275">使用 SSH 連線至 Linux 節點</span><span class="sxs-lookup"><span data-stu-id="1d717-275">Connect to Linux nodes using SSH</span></span>
<span data-ttu-id="1d717-276">在開發期間或問題進行疑難排解時，您可能會發現需要登入您的集區中的節點。</span><span class="sxs-lookup"><span data-stu-id="1d717-276">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span></span> <span data-ttu-id="1d717-277">不同於 Windows 計算節點，您無法使用遠端桌面通訊協定 (RDP) 連線到 Linux 節點。</span><span class="sxs-lookup"><span data-stu-id="1d717-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span></span> <span data-ttu-id="1d717-278">相反地，Batch 服務可讓您遠端連線的每個節點上的 SSH 存取。</span><span class="sxs-lookup"><span data-stu-id="1d717-278">Instead, the Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="1d717-279">下列 Python 程式碼片段會在集區中的每個節點上建立使用者 (遠端連線所需)。</span><span class="sxs-lookup"><span data-stu-id="1d717-279">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="1d717-280">接著，它會列印每個節點的安全殼層 (SSH) 連線資訊。</span><span class="sxs-lookup"><span data-stu-id="1d717-280">It then prints the secure shell (SSH) connection information for each node.</span></span>

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

# Specify the ID of an existing pool containing Linux nodes
# currently in the 'idle' state
pool_id = ''

# Specify the username and prompt for a password
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

# Create the user that will be added to each node in the pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get the list of nodes in the pool
nodes = batch_client.compute_node.list(pool_id)

# Add the user to each node in the pool and print
# the connection information for the node
for node in nodes:
    # Add the user to the node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for the node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print the connection info for the node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="1d717-281">以下是包含四個 Linux 節點之集區的先前程式碼的範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="1d717-281">Here is sample output for the previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="1d717-282">在節點上建立使用者時，不要使用密碼，而是可以指定 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="1d717-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="1d717-283">在 Python SDK 中，使用 [ComputeNodeUser][py_computenodeuser] 上的 **ssh_public_key** 參數。</span><span class="sxs-lookup"><span data-stu-id="1d717-283">In the Python SDK, use the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="1d717-284">在 .NET 中，使用 [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] 屬性。</span><span class="sxs-lookup"><span data-stu-id="1d717-284">In .NET, use the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="1d717-285">價格</span><span class="sxs-lookup"><span data-stu-id="1d717-285">Pricing</span></span>
<span data-ttu-id="1d717-286">Azure Batch 採用 Azure 雲端服務和 Azure 虛擬機器技術。</span><span class="sxs-lookup"><span data-stu-id="1d717-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="1d717-287">Batch 服務本身為免費提供，這表示您僅需支付 Batch 解決方案所使用的計算資源。</span><span class="sxs-lookup"><span data-stu-id="1d717-287">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="1d717-288">選擇**雲端服務組態**時，將會根據[雲端服務定價][cloud_services_pricing]結構向您收費。</span><span class="sxs-lookup"><span data-stu-id="1d717-288">When you choose **Cloud Services Configuration**, you are charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="1d717-289">選擇**虛擬機器組態**時，將會根據[虛擬機器定價][vm_pricing]結構向您收費。</span><span class="sxs-lookup"><span data-stu-id="1d717-289">When you choose **Virtual Machine Configuration**, you are charged based on the [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="1d717-290">如果您是使用[應用程式套件](batch-application-packages.md)將應用程式部署到您的 Batch 節點，也需要支付應用程式套件使用的 Azure 儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="1d717-290">If you deploy applications to your Batch nodes using [application packages](batch-application-packages.md), you are also charged for the Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="1d717-291">一般情況下，Azure 儲存體成本很低。</span><span class="sxs-lookup"><span data-stu-id="1d717-291">In general, the Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1d717-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d717-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="1d717-293">Batch Python 教學課程</span><span class="sxs-lookup"><span data-stu-id="1d717-293">Batch Python tutorial</span></span>
<span data-ttu-id="1d717-294">如需如何透過 Python 使用 Batch 的深入教學課程，請參閱 [開始使用 Azure Batch Python 用戶端](batch-python-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="1d717-294">For a more in-depth tutorial about how to work with Batch by using Python, check out [Get started with the Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="1d717-295">隨附的[程式碼範例][github_samples_pyclient]包含 Helper 函式 `get_vm_config_for_distro`，展示另一種技術來取得虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="1d717-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique to obtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="1d717-296">Batch Python 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="1d717-296">Batch Python code samples</span></span>
<span data-ttu-id="1d717-297">GitHub 上 [azure-batch-samples][github_samples] 存放庫中的 [Python 程式碼範例][github_samples_py]包含幾個指令碼，會示範如何執行一般 Batch 作業 (例如建立集區、作業和工作)。</span><span class="sxs-lookup"><span data-stu-id="1d717-297">The [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how to perform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="1d717-298">Python 範例隨附的[讀我檔案][github_py_readme]詳細說明如何安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="1d717-298">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="1d717-299">批次論壇</span><span class="sxs-lookup"><span data-stu-id="1d717-299">Batch forum</span></span>
<span data-ttu-id="1d717-300">MSDN 上的 [Azure Batch 論壇][forum]是一個很棒的地方，可以討論 Batch 和詢問有關此服務的問題。</span><span class="sxs-lookup"><span data-stu-id="1d717-300">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="1d717-301">請閱讀實用的「釘選」文章，並在建置 Batch 解決方案時，若發生問題就張貼問題。</span><span class="sxs-lookup"><span data-stu-id="1d717-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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
