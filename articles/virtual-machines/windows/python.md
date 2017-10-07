---
title: "aaaCreate 和管理 Windows VM 在 Azure 中使用 Python |Microsoft 文件"
description: "了解 toouse Python toocreate 和管理 Azure 中的 Windows VM。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="97ce6-103">在 Azure 中使用 Python 建立並管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="97ce6-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="97ce6-104">[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="97ce6-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="97ce6-105">本文涵蓋使用 Python 建立、管理和刪除 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="97ce6-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="97ce6-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="97ce6-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="97ce6-107">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="97ce6-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="97ce6-108">安裝套件</span><span class="sxs-lookup"><span data-stu-id="97ce6-108">Install packages</span></span>
> * <span data-ttu-id="97ce6-109">建立認證</span><span class="sxs-lookup"><span data-stu-id="97ce6-109">Create credentials</span></span>
> * <span data-ttu-id="97ce6-110">建立資源</span><span class="sxs-lookup"><span data-stu-id="97ce6-110">Create resources</span></span>
> * <span data-ttu-id="97ce6-111">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="97ce6-111">Perform management tasks</span></span>
> * <span data-ttu-id="97ce6-112">刪除資源</span><span class="sxs-lookup"><span data-stu-id="97ce6-112">Delete resources</span></span>
> * <span data-ttu-id="97ce6-113">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="97ce6-113">Run hello application</span></span>

<span data-ttu-id="97ce6-114">它會採用約 20 分鐘 toodo 這些步驟。</span><span class="sxs-lookup"><span data-stu-id="97ce6-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="97ce6-115">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="97ce6-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="97ce6-116">如果您尚未安裝 [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)，請進行安裝。</span><span class="sxs-lookup"><span data-stu-id="97ce6-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="97ce6-117">選取**Python 開發**在 hello 工作負載頁面，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="97ce6-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="97ce6-118">在 hello 摘要，您可以看到**Python 3 64 位元 (3.6.0)**會自動為您選擇。</span><span class="sxs-lookup"><span data-stu-id="97ce6-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="97ce6-119">如果您已安裝 Visual Studio，您可以新增使用 Visual Studio 啟動器 hello hello Python 工作負載。</span><span class="sxs-lookup"><span data-stu-id="97ce6-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="97ce6-120">安裝並啟動 Visual Studio 後，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="97ce6-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="97ce6-121">按一下**範本** > **Python** > **Python 應用程式**，輸入*myPythonProject* hello 名稱hello 專案中，選取 hello hello 專案位置，再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="97ce6-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="97ce6-122">安裝套件</span><span class="sxs-lookup"><span data-stu-id="97ce6-122">Install packages</span></span>

1. <span data-ttu-id="97ce6-123">在 [方案總管] 的 myPythonProject 下，以滑鼠右鍵按一下 [Python 環境]，然後選取 [新增虛擬環境]。</span><span class="sxs-lookup"><span data-stu-id="97ce6-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="97ce6-124">Hello 加入虛擬環境在畫面上，接受預設名稱 hello *env*，請確定*Python 3.6 （64 位元）*選取 hello 基底直譯器，然後按一下**建立**.</span><span class="sxs-lookup"><span data-stu-id="97ce6-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="97ce6-125">以滑鼠右鍵按一下 hello *env*您所建立的環境按一下**安裝 Python 封裝**，輸入*azure*在 hello 搜尋方塊，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="97ce6-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="97ce6-126">您應該會看到在 hello 輸出 windows hello azure 封裝已成功安裝。</span><span class="sxs-lookup"><span data-stu-id="97ce6-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="97ce6-127">建立認證</span><span class="sxs-lookup"><span data-stu-id="97ce6-127">Create credentials</span></span>

<span data-ttu-id="97ce6-128">在開始此步驟之前，請確定您具有 [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="97ce6-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="97ce6-129">您也應該在稍後步驟中，記錄 hello 應用程式識別碼、 hello 驗證金鑰，以及您需要的 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="97ce6-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="97ce6-130">開啟*myPythonProject.py*所建立的檔案，然後新增此程式碼 tooenable 應用程式 toorun:</span><span class="sxs-lookup"><span data-stu-id="97ce6-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="97ce6-131">tooimport hello 程式碼所需，新增這些陳述式 toohello 檔案的頂端 hello.py:</span><span class="sxs-lookup"><span data-stu-id="97ce6-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="97ce6-132">接下來在 hello.py 檔案中加入變數之後 hello 匯入陳述式中使用 toospecify 常見的值 hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="97ce6-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="97ce6-133">以您的訂用帳戶識別碼取代 **subscription-id**。</span><span class="sxs-lookup"><span data-stu-id="97ce6-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="97ce6-134">toocreate hello Active Directory 認證，您需要 toomake 要求 hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="97ce6-135">取代**應用程式識別碼**，**驗證金鑰**，和**租用戶識別碼**先前收集當您建立 Azure Active Directory 的 hello 值服務主體。</span><span class="sxs-lookup"><span data-stu-id="97ce6-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="97ce6-136">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="97ce6-137">建立資源</span><span class="sxs-lookup"><span data-stu-id="97ce6-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="97ce6-138">初始化管理用戶端</span><span class="sxs-lookup"><span data-stu-id="97ce6-138">Initialize management clients</span></span>

<span data-ttu-id="97ce6-139">管理用戶端所需的 toocreate 和 hello Python SDK 使用 Azure 中管理資源。</span><span class="sxs-lookup"><span data-stu-id="97ce6-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="97ce6-140">toocreate hello 管理用戶端，此程式碼下新增 hello**如果**然後 hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="97ce6-141">建立 hello VM 和支援資源</span><span class="sxs-lookup"><span data-stu-id="97ce6-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="97ce6-142">所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="97ce6-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="97ce6-143">toocreate 資源群組、 hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="97ce6-144">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="97ce6-145">[可用性設定組](tutorial-availability-sets.md)方便您應用程式所使用的 toomaintain hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97ce6-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="97ce6-146">toocreate 可用性設定之後，加入此函式 hello.py 檔中的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="97ce6-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="97ce6-147">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="97ce6-148">A[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)是需要的 toocommunicate 與 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97ce6-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="97ce6-149">toocreate 公用 IP 位址 hello 虛擬機器，hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="97ce6-150">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="97ce6-151">虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。</span><span class="sxs-lookup"><span data-stu-id="97ce6-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="97ce6-152">toocreate 虛擬網路，hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="97ce6-153">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="97ce6-154">tooadd 子 toohello 虛擬網路，hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="97ce6-155">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="97ce6-156">需要網路介面 toocommunicate hello 虛擬網路上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97ce6-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="97ce6-157">toocreate 網路介面，hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="97ce6-158">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="97ce6-159">現在，您會建立所有 hello 支援的資源，您可以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97ce6-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="97ce6-160">toocreate hello 虛擬機器之後，加入此函式 hello.py 檔中的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="97ce6-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="97ce6-161">本教學課程中建立虛擬機器執行 hello Windows Server 作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="97ce6-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="97ce6-162">toolearn 有關選取其他映像的詳細資訊請參閱[瀏覽並選取 Azure 虛擬機器映像使用 Windows PowerShell 與 hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="97ce6-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="97ce6-163">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="97ce6-164">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="97ce6-164">Perform management tasks</span></span>

<span data-ttu-id="97ce6-165">在虛擬機器的 hello 生命週期，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97ce6-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="97ce6-166">此外，您可能想 toocreate 程式碼 tooautomate 重複或複雜工作。</span><span class="sxs-lookup"><span data-stu-id="97ce6-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="97ce6-167">取得 hello VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="97ce6-167">Get information about hello VM</span></span>

1. <span data-ttu-id="97ce6-168">tooget 資訊 hello 虛擬機器，hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="97ce6-169">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="97ce6-170">停止 hello VM</span><span class="sxs-lookup"><span data-stu-id="97ce6-170">Stop hello VM</span></span>

<span data-ttu-id="97ce6-171">您可以停止虛擬機器並保留其所有設定，但繼續 toobe 支付，或您可以停止虛擬機器和解除配置。</span><span class="sxs-lookup"><span data-stu-id="97ce6-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="97ce6-172">當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。</span><span class="sxs-lookup"><span data-stu-id="97ce6-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="97ce6-173">toostop hello 虛擬機器，而不取消配置，hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="97ce6-174">如果您想 toodeallocate hello 虛擬機器，變更 hello power_off 呼叫 toothis 程式碼：</span><span class="sxs-lookup"><span data-stu-id="97ce6-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="97ce6-175">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="97ce6-176">啟動 VM hello</span><span class="sxs-lookup"><span data-stu-id="97ce6-176">Start hello VM</span></span>

1. <span data-ttu-id="97ce6-177">toostart hello 虛擬機器之後，加入此函式 hello.py 檔中的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="97ce6-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="97ce6-178">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="97ce6-179">調整大小 hello VM</span><span class="sxs-lookup"><span data-stu-id="97ce6-179">Resize hello VM</span></span>

<span data-ttu-id="97ce6-180">決定虛擬機器的大小時，應該考慮部署的許多層面。</span><span class="sxs-lookup"><span data-stu-id="97ce6-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="97ce6-181">如需詳細資訊，請參閱 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="97ce6-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="97ce6-182">hello 虛擬機器，toochange hello 大小 hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="97ce6-183">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="97ce6-184">新增資料磁碟 toohello VM</span><span class="sxs-lookup"><span data-stu-id="97ce6-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="97ce6-185">虛擬機器可以有一或多個[資料磁碟](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，而這些磁碟會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="97ce6-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="97ce6-186">tooadd 資料磁碟 toohello 虛擬機器，hello.py 檔中的 hello 變數後，新增此函式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="97ce6-187">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="97ce6-188">刪除資源</span><span class="sxs-lookup"><span data-stu-id="97ce6-188">Delete resources</span></span>

<span data-ttu-id="97ce6-189">因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。</span><span class="sxs-lookup"><span data-stu-id="97ce6-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="97ce6-190">如果您想 toodelete hello 虛擬機器，而且所有 hello 支援的資源，您都有 toodo 是刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="97ce6-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="97ce6-191">toodelete hello 資源群組和所有資源，請新增此函式之後 hello.py 檔中的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="97ce6-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="97ce6-192">您先前加入的 toocall hello 函式加入下列的程式碼，在 hello**如果**hello hello.py 檔結尾的陳述式：</span><span class="sxs-lookup"><span data-stu-id="97ce6-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="97ce6-193">儲存 myPythonProject.py。</span><span class="sxs-lookup"><span data-stu-id="97ce6-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="97ce6-194">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="97ce6-194">Run hello application</span></span>

1. <span data-ttu-id="97ce6-195">toorun hello 主控台應用程式中，按一下 **啟動**Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="97ce6-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="97ce6-196">按**Enter**之後傳回每個資源的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="97ce6-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="97ce6-197">在 hello 狀態資訊，您應該會看到**Succeeded**佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="97ce6-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="97ce6-198">建立 hello 虛擬機器之後，您必須 hello 機會 toodelete 所建立的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="97ce6-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="97ce6-199">再按**Enter** toostart 刪除資源，您可能需要幾分鐘的時間 tooverify 及其建立 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="97ce6-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="97ce6-200">如果您擁有 hello Azure 入口網站開啟，您可能必須 toorefresh hello 刀鋒視窗 toosee 新資源。</span><span class="sxs-lookup"><span data-stu-id="97ce6-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="97ce6-201">它應該完全從開始 toofinish 此主控台應用程式 toorun 大約五分鐘。</span><span class="sxs-lookup"><span data-stu-id="97ce6-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="97ce6-202">可能需要幾分鐘的時間 hello 應用程式完成之前 hello 的所有資源，並且會刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="97ce6-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="97ce6-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97ce6-203">Next steps</span></span>

- <span data-ttu-id="97ce6-204">如果有一些與 hello 部署的問題下, 一個步驟會在 toolook[疑難排解資源群組部署，以及 Azure 入口網站](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="97ce6-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="97ce6-205">深入了解 hello [Azure Python 程式庫](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="97ce6-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

