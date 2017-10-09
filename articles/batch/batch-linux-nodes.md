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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>在 Batch 集區中佈建 Linux 計算節點

您可以在 Linux 和 Windows 虛擬機器上使用 Azure Batch toorun 平行計算工作負載。 這篇文章說明如何的 Linux toocreate 集區中的計算節點 hello 批次服務使用這兩個 hello[批次 Python] [ py_batch_package]和[批次.NET] [ api_net]用戶端程式庫。

> [!NOTE]
> 在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。 只有建立 hello 集區時使用的雲端服務組態，10 年 3 月 2016年和 5 年 7 月 2017年之間建立的批次集區中支援它們。 建立先前 too10 2016 年 3 月的批次集區不支援應用程式封裝。 如需有關使用應用程式套件 toodeploy 您應用程式 tooyour 批次的節點，請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。
>
>

## <a name="virtual-machine-configuration"></a>虛擬機器組態
當您在批次中建立計算節點的集區時，您有兩個選項其中 tooselect hello 節點大小和作業系統： 雲端服務組態和虛擬機器組態。

**雲端服務組態**「只」提供 Windows 計算節點。 可執行的運算節點大小會列在[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)，而且可用的作業系統會列於 hello [Azure 客體作業系統版本與 SDK 相容性比較表](../cloud-services/cloud-services-guestos-update-matrix.md)。 當您建立包含 Azure 雲端服務節點的集區時，您指定 hello 節點大小和 hello 作業系統系列，如下所述 hello 先前所述的發行項。 針對 Windows 計算節點的集區，最常使用的是雲端服務。

**虛擬機器組態** 可提供適用於計算節點的 Linux 和 Windows 映像。 可用的計算節點大小列於 [Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) 和 [Azure 中的虛擬機器大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)。 當您建立包含虛擬機器組態節點的集區時，您必須指定 hello 大小 hello 節點、 hello 虛擬機器映像參考，以及 hello 批次節點代理程式 SKU toobe hello 節點上安裝。

### <a name="virtual-machine-image-reference"></a>虛擬機器映像參考
hello 批次服務會使用[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)tooprovide Linux 計算節點。 您可以指定映像從 hello [Azure Marketplace][vm_marketplace]，或提供您準備自訂映像。 如需自訂映像的詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#pool)。

當您設定的虛擬機器映像參考時，您會指定 hello hello 虛擬機器映像內容。 當您建立的虛擬機器映像參考時，還需要下列屬性的 hello:

| **映像參考屬性** | **範例** |
| --- | --- |
| 發行者 |Canonical |
| 提供項目 |UbuntuServer |
| SKU |14.04.4-LTS |
| 版本 |最新 |

> [!TIP]
> 您可以進一步了解這些屬性和 toolist Marketplace 中的映像[瀏覽並選取使用 CLI 或 PowerShell 的 Azure 中的 Linux 虛擬機器映像](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 請注意，並非所有 Marketplace 映像目前都與 Batch 相容。 如需詳細資訊，請參閱 [節點代理程式 SKU](#node-agent-sku)。
>
>

### <a name="node-agent-sku"></a>節點代理程式 SKU
hello 批次節點代理程式是 hello 集區中的每個節點上執行，並提供 hello 節點與 hello 批次服務之間的 hello 命令控制項介面的程式。 有不同的實作方式的 hello 節點代理程式，稱為不同作業系統的 Sku。 基本上，當您建立虛擬機器組態，您首先要指定 hello 虛擬機器映像參考，，然後指定 hello 節點代理程式 tooinstall hello 映像上。 一般而言，每個節點代理程式可與多個虛擬機器映像 SKU 相容。 以下是一些節點代理程式的 SKU 的範例︰

* batch.node.ubuntu 14.04
* batch.node.centos 7
* batch.node.windows amd64

> [!IMPORTANT]
> 並非所有 hello Marketplace 中都可用的虛擬機器映像都都相容 hello 目前可用批次 節點的代理程式。 使用 hello 批次 Sdk toolist hello 可用的節點代理程式 Sku 和 hello 與它們彼此相容的虛擬機器映像。 請參閱 hello[清單的虛擬機器映像](#list-of-virtual-machine-images)本文稍後如需詳細資訊和方式的範例 tooretrieve 有效的映像，在執行階段清單。
>
>

## <a name="create-a-linux-pool-batch-python"></a>建立 Linux 集區︰Batch Python
hello 下列程式碼片段示範如何 toouse hello [Microsoft Azure 批次用戶端程式庫的 Python] [ py_batch_package] toocreate Ubuntu 伺服器集區計算節點。 參考文件以 hello 批次 Python 模組，請參閱[azure.batch 封裝][ py_batch_docs]上讀取 hello 文件。

此程式碼片段會明確建立 [ImageReference][py_imagereference]，並指定其每一個屬性 (發行者、優惠、SKU、版本)。 在實際執行程式碼，不過，我們建議您使用 hello [list_node_agent_skus] [ py_list_skus]方法 toodetermine，然後選取從 hello 可用映像和節點代理程式 SKU 組合在執行階段。

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

如先前所述，我們建議，而不是建立 hello [ImageReference] [ py_imagereference]您明確地使用 hello [list_node_agent_skus] [ py_list_skus]從 hello 方法 toodynamically 選取目前支援的節點代理程式/Marketplace 映像的組合。 hello 下列 Python 程式碼片段說明如何 toouse 這個方法。

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

## <a name="create-a-linux-pool-batch-net"></a>建立 Linux 集區︰Batch .NET
hello 下列程式碼片段示範如何 toouse hello[批次.NET] [ nuget_batch_net]用戶端程式庫 toocreate Ubuntu 伺服器集區計算節點。 您可以找到 hello[批次.NET 參考文件][ api_net] MSDN 上。

hello 下列程式碼片段會使用 hello [PoolOperations][net_pool_ops]。[ListNodeAgentSkus] [ net_list_skus]方法 tooselect hello 清單中的目前支援 Marketplace 映像和節點代理程式 SKU 的組合。 這項技術是合理的因為 hello 清單支援的組合可能會從時間 tootime 變更。 最常見的是新增支援的組合。

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

雖然 hello 先前程式碼片段使用 hello [PoolOperations][net_pool_ops]。[ListNodeAgentSkus] [ net_list_skus]方法 toodynamically 清單，然後選取從支援 （建議選項） 的映像和節點代理程式 SKU 組合，您也可以設定[ImageReference] [ net_imagereference]明確：

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>虛擬機器映像的清單
hello 下表列出 hello Marketplace 虛擬機器映像與相容的 hello 可用批次 節點的代理程式上次更新此文件。 這份清單不可靠，因為映像和節點代理程式可能會加入或移除在任何時間的重要 toonote 它。 我們建議您批次應用程式和服務永遠使用[list_node_agent_skus] [ py_list_skus] (Python) 和[ListNodeAgentSkus] [ net_list_skus]Toodetermine （批次.NET），然後選取從 hello 目前可用的 Sku。

> [!WARNING]
> 下列清單中的 hello 可能隨時變更。 一律使用 hello**清單節點代理程式 SKU** hello 批次 Api toolist 中可用的方法 hello 相容的虛擬機器和節點代理程式 Sku 當您執行批次作業。
>
>

| **發行者** | **提供項目** | **映像 SKU** | **版本** | **節點代理程式 SKU 識別碼** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | 最新 | batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | 最新 | batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | 最新 | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | 最新 | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | 最新 | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1 | 最新 | batch.node.centos 7 |
| OpenLogic | CentOS | 7.2 | 最新 | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.0 | 最新 | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.2 | 最新 | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | 最新 | batch.node.opensuse 13.2 |
| SUSE | openSUSE-Leap | 42.1 | 最新 | batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | 最新 | batch.node.opensuse 42.1 |
| SUSE | SLES-HPC | 12-SP1 | 最新 | batch.node.opensuse 42.1 |
| microsoft-ads | linux-data-science-vm | linuxdsvm | 最新 | batch.node.centos 7 |
| microsoft-ads | standard-data-science-vm | standard-data-science-vm | 最新 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008-R2-SP1 | 最新 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | 最新 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | 最新 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter | 最新 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter-with-Containers | 最新 | batch.node.windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>連接使用 SSH tooLinux 節點
在開發期間或問題進行疑難排解時，您可能會發現需要 toosign toohello 集區中的節點中。 不同於 Windows 計算節點，您無法使用遠端桌面通訊協定 (RDP) tooconnect tooLinux 節點。 相反地，hello 批次服務可讓您遠端連線的每個節點上的 SSH 存取。

hello 下列 Python 程式碼片段會建立使用者所需的遠端連線集區中的每個節點上。 接著，它會列印每個節點的 hello 安全殼層 (SSH) 連接資訊。

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

以下是包含四個 Linux 節點集區 hello 先前的程式碼的範例輸出：

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

在節點上建立使用者時，不要使用密碼，而是可以指定 SSH 公開金鑰。 在 hello Python SDK，使用 hello **ssh_public_key**參數[ComputeNodeUser][py_computenodeuser]。 在.NET 中，使用 hello [ComputeNodeUser][net_computenodeuser]。[SshPublicKey] [ net_ssh_key]屬性。

## <a name="pricing"></a>價格
Azure Batch 採用 Azure 雲端服務和 Azure 虛擬機器技術。 hello 批次服務本身則提供給不花一毛錢，這表示您必須只支付 hello 計算您批次的解決方案使用的資源。 當您選擇**雲端服務設定**，您的收費依據 hello[雲端服務定價][ cloud_services_pricing]結構。 當您選擇**虛擬機器組態**，您的收費依據 hello[虛擬機器定價][ vm_pricing]結構。 

如果您部署應用程式使用的 tooyour 批次節點[應用程式封裝](batch-application-packages.md)，您也需要付費 hello Azure 儲存體資源的應用程式封裝使用。 一般情況下，hello Azure 儲存體成本很低。 

## <a name="next-steps"></a>後續步驟
### <a name="batch-python-tutorial"></a>Batch Python 教學課程
更深入的教學課程中，有關如何使用 Python，簽出與批次 toowork[開始 hello Azure 批次 Python 用戶端使用](batch-python-tutorial.md)。 其附屬[程式碼範例][ github_samples_pyclient]包含協助程式函式， `get_vm_config_for_distro`，它會顯示另一個技術 tooobtain 虛擬機器組態。

### <a name="batch-python-code-samples"></a>Batch Python 程式碼範例
hello [Python 程式碼範例][ github_samples_py]在 hello [azure 批次範例][ github_samples] GitHub 上的儲存機制包含指令碼，教您如何 tooperform一般批次作業，例如集區、 工作和工作的建立。 hello[讀我檔案][ github_py_readme] ，伴隨著 hello Python 範例包含有關如何 tooinstall hello 所需封裝的詳細資料。

### <a name="batch-forum"></a>批次論壇
hello [Azure Batch 論壇][ forum] MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。 請閱讀實用的「釘選」文章，並在建置 Batch 解決方案時，若發生問題就張貼問題。

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
