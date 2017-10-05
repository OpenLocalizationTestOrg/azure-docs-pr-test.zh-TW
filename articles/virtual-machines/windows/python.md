---
title: "在 Azure 中使用 Python 建立並管理 Windows VM | Microsoft Docs"
description: "了解如何在 Azure 中使用 Python 建立並管理 Windows VM。"
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
ms.openlocfilehash: bb777d41570d7b1dc97402d532519488912948e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="a1f7a-103">在 Azure 中使用 Python 建立並管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="a1f7a-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="a1f7a-104">[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="a1f7a-105">本文涵蓋使用 Python 建立、管理和刪除 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="a1f7a-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a1f7a-107">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="a1f7a-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="a1f7a-108">安裝套件</span><span class="sxs-lookup"><span data-stu-id="a1f7a-108">Install packages</span></span>
> * <span data-ttu-id="a1f7a-109">建立認證</span><span class="sxs-lookup"><span data-stu-id="a1f7a-109">Create credentials</span></span>
> * <span data-ttu-id="a1f7a-110">建立資源</span><span class="sxs-lookup"><span data-stu-id="a1f7a-110">Create resources</span></span>
> * <span data-ttu-id="a1f7a-111">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="a1f7a-111">Perform management tasks</span></span>
> * <span data-ttu-id="a1f7a-112">刪除資源</span><span class="sxs-lookup"><span data-stu-id="a1f7a-112">Delete resources</span></span>
> * <span data-ttu-id="a1f7a-113">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="a1f7a-113">Run the application</span></span>

<span data-ttu-id="a1f7a-114">執行這些步驟大約需要 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="a1f7a-115">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="a1f7a-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="a1f7a-116">如果您尚未安裝 [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)，請進行安裝。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="a1f7a-117">在 [工作負載] 頁面上選取 [Python 開發]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-117">Select **Python development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="a1f7a-118">在摘要中，您可以看到會自動為您選擇 **Python 3 64 位元 (3.6.0)**。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-118">In the summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="a1f7a-119">如果您已安裝 Visual Studio，您可以使用 Visual Studio Launcher 新增 Python 工作負載。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-119">If you have already installed Visual Studio, you can add the Python workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="a1f7a-120">安裝並啟動 Visual Studio 後，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="a1f7a-121">按一下 [範本] > [Python] > [Python 應用程式]，輸入 myPythonProject 作為專案的名稱，選取專案的位置，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="a1f7a-122">安裝套件</span><span class="sxs-lookup"><span data-stu-id="a1f7a-122">Install packages</span></span>

1. <span data-ttu-id="a1f7a-123">在 [方案總管] 的 myPythonProject 下，以滑鼠右鍵按一下 [Python 環境]，然後選取 [新增虛擬環境]。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="a1f7a-124">在 [新增虛擬環境] 畫面上，接受 env 的預設名稱、確定選取 Python 3.6 (64 位元) 作為基底解譯器，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-124">On the Add Virtual Environment screen, accept the default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for the base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="a1f7a-125">以滑鼠右鍵按一下您所建立的 env 環境、按一下 [安裝 Python 套件]、在搜尋方塊中輸入 azure，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-125">Right-click the *env* environment that you created, click **Install Python Package**, enter *azure* in the search box, and then press Enter.</span></span>

<span data-ttu-id="a1f7a-126">您應該會在輸出視窗中看到已成功安裝的 azure 套件。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-126">You should see in the output windows that the azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="a1f7a-127">建立認證</span><span class="sxs-lookup"><span data-stu-id="a1f7a-127">Create credentials</span></span>

<span data-ttu-id="a1f7a-128">在開始此步驟之前，請確定您具有 [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a1f7a-129">您也應該記錄應用程式識別碼、驗證金鑰以及租用戶識別碼，您在稍後的步驟會需要這些項目。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="a1f7a-130">開啟所建立的 myPythonProject.py 檔案，然後新增此程式碼，讓您的應用程式可執行：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-130">Open *myPythonProject.py* file that was created, and then add this code to enable your application to run:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="a1f7a-131">若要匯入所需的程式碼，請將這些陳述式新增至 .py 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-131">To import the code that is needed, add these statements to the top of the .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="a1f7a-132">接著在 .py 檔案中，在匯入陳述式之後新增變數，來指定用於程式碼中的一般值：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-132">Next in the .py file, add variables after the import statements to specify common values used in the code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="a1f7a-133">以您的訂用帳戶識別碼取代 **subscription-id**。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="a1f7a-134">若要建立您提出要求所需的 Active Directory 認證，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-134">To create the Active Directory credentials that you need to make requests, add this function after the variables in the .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="a1f7a-135">將 **application-id**、**authentication-key** 和 **tenant-id** 取代為您先前建立 Azure Active Directory 服務主體時收集的值。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-135">Replace **application-id**, **authentication-key**, and **tenant-id** with the values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="a1f7a-136">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-136">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="a1f7a-137">建立資源</span><span class="sxs-lookup"><span data-stu-id="a1f7a-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="a1f7a-138">初始化管理用戶端</span><span class="sxs-lookup"><span data-stu-id="a1f7a-138">Initialize management clients</span></span>

<span data-ttu-id="a1f7a-139">需要管理用戶端才能在 Azure 中使用 Python SDK 建立及管理資源。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-139">Management clients are needed to create and manage resources using the Python SDK in Azure.</span></span> <span data-ttu-id="a1f7a-140">若要建立管理用戶端，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-140">To create the management clients, add this code under the **if** statement at then end of the .py file:</span></span>

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

### <a name="create-the-vm-and-supporting-resources"></a><span data-ttu-id="a1f7a-141">建立 VM 和支援的資源</span><span class="sxs-lookup"><span data-stu-id="a1f7a-141">Create the VM and supporting resources</span></span>

<span data-ttu-id="a1f7a-142">所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="a1f7a-143">若要建立資源群組，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-143">To create a resource group, add this function after the variables in the .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="a1f7a-144">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-144">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter to continue...')
    ```

<span data-ttu-id="a1f7a-145">維護您應用程式所使用的虛擬機器時，使用[可用性設定組](tutorial-availability-sets.md)可讓您更加輕鬆。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-145">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

1. <span data-ttu-id="a1f7a-146">若要建立可用性設定組，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-146">To create an availability set, add this function after the variables in the .py file:</span></span>
   
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

2. <span data-ttu-id="a1f7a-147">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-147">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter to continue...')
    ```

<span data-ttu-id="a1f7a-148">必須要有[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)才能與虛擬機器進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

1. <span data-ttu-id="a1f7a-149">若要建立虛擬機器的公用 IP 位址，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-149">To create a public IP address for the virtual machine, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="a1f7a-150">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-150">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="a1f7a-151">虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a1f7a-152">若要建立虛擬網路，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-152">To create a virtual network, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="a1f7a-153">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-153">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

3. <span data-ttu-id="a1f7a-154">若要將子網路新增至虛擬網路，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-154">To add a subnet to the virtual network, add this function after the variables in the .py file:</span></span>
    
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
        
4. <span data-ttu-id="a1f7a-155">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-155">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="a1f7a-156">虛擬機器需要網路介面以在虛擬網路上通訊。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-156">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

1. <span data-ttu-id="a1f7a-157">若要建立網路介面，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-157">To create a network interface, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="a1f7a-158">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-158">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="a1f7a-159">既然您已經建立所有支援的資源，您可以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-159">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="a1f7a-160">若要建立虛擬機器，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-160">To create the virtual machine, add this function after the variables in the .py file:</span></span>
   
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
    > <span data-ttu-id="a1f7a-161">本教學課程中會建立執行 Windows Server 作業系統版本的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-161">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="a1f7a-162">若要深入了解如何選取其他映像，請參閱 [使用 Windows PowerShell 和 Azure CLI 來瀏覽和選取 Azure 虛擬機器映像](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-162">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="a1f7a-163">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-163">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="a1f7a-164">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="a1f7a-164">Perform management tasks</span></span>

<span data-ttu-id="a1f7a-165">在虛擬機器的生命週期內，您可以執行一些管理工作，例如啟動、停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-165">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="a1f7a-166">此外，您可以建立程式碼來自動執行重複或複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-166">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

### <a name="get-information-about-the-vm"></a><span data-ttu-id="a1f7a-167">取得 VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="a1f7a-167">Get information about the VM</span></span>

1. <span data-ttu-id="a1f7a-168">若要取得虛擬機器的相關資訊，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-168">To get information about the virtual machine, add this function after the variables in the .py file:</span></span>

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
2. <span data-ttu-id="a1f7a-169">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-169">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter to continue...')
    ```

### <a name="stop-the-vm"></a><span data-ttu-id="a1f7a-170">停止 VM</span><span class="sxs-lookup"><span data-stu-id="a1f7a-170">Stop the VM</span></span>

<span data-ttu-id="a1f7a-171">您可以停止虛擬機器並保留其所有的設定，但仍繼續計費，或您可以停止虛擬機器並將其解除配置。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-171">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="a1f7a-172">當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="a1f7a-173">若要停止虛擬機器而不解除配置，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-173">To stop the virtual machine without deallocating it, add this function after the variables in the .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="a1f7a-174">如果您想要解除配置虛擬機器，請將 PowerOff 呼叫變更為下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="a1f7a-174">If you want to deallocate the virtual machine, change the power_off call to this code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="a1f7a-175">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-175">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="start-the-vm"></a><span data-ttu-id="a1f7a-176">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="a1f7a-176">Start the VM</span></span>

1. <span data-ttu-id="a1f7a-177">若要啟動虛擬機器，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-177">To start the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="a1f7a-178">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-178">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="resize-the-vm"></a><span data-ttu-id="a1f7a-179">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="a1f7a-179">Resize the VM</span></span>

<span data-ttu-id="a1f7a-180">決定虛擬機器的大小時，應該考慮部署的許多層面。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="a1f7a-181">如需詳細資訊，請參閱 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="a1f7a-182">若要變更虛擬機器的大小，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-182">To change the size of the virtual machine, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="a1f7a-183">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-183">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter to continue...')
    ```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="a1f7a-184">將資料磁碟新增至 VM</span><span class="sxs-lookup"><span data-stu-id="a1f7a-184">Add a data disk to the VM</span></span>

<span data-ttu-id="a1f7a-185">虛擬機器可以有一或多個[資料磁碟](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，而這些磁碟會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="a1f7a-186">若要將資料磁碟新增至虛擬機器，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-186">To add a data disk to the virtual machine, add this function after the variables in the .py file:</span></span> 

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

2. <span data-ttu-id="a1f7a-187">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-187">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter to continue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="a1f7a-188">刪除資源</span><span class="sxs-lookup"><span data-stu-id="a1f7a-188">Delete resources</span></span>

<span data-ttu-id="a1f7a-189">您將為 Azure 中所使用的資源支付費用，因此，將不再需要的資源刪除永遠是最好的做法。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-189">Because you are charged for resources used in Azure, it's always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="a1f7a-190">如果您想要刪除虛擬機器及所有支援的資源，您只需要刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-190">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="a1f7a-191">若要刪除資源群組及所有資源，請在 .py 檔案的變數之後新增此函式：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-191">To delete the resource group and all resources, add this function after the variables in the .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="a1f7a-192">若要呼叫您先前新增的函式，請在 .py 檔案結尾的 **if** 陳述式下新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f7a-192">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="a1f7a-193">儲存 myPythonProject.py。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-193">Save *myPythonProject.py*.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="a1f7a-194">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="a1f7a-194">Run the application</span></span>

1. <span data-ttu-id="a1f7a-195">若要執行主控台應用程式，請在 Visual Studio 中按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-195">To run the console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="a1f7a-196">傳回每個資源的狀態之後，按下 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-196">Press **Enter** after the status of each resource is returned.</span></span> <span data-ttu-id="a1f7a-197">在狀態資訊中，您應該會看到「成功」佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-197">In the status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="a1f7a-198">建立虛擬機器之後，您可以將所建立的所有資源刪除。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-198">After the virtual machine is created, you have the opportunity to delete all the resources that you create.</span></span> <span data-ttu-id="a1f7a-199">在您按下 **Enter** 鍵以開始刪除資源之前，可以先花幾分鐘的時間來確認 Azure 入口網站中的建立情況。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-199">Before you press **Enter** to start deleting resources, you could take a few minutes to verify their creation in the Azure portal.</span></span> <span data-ttu-id="a1f7a-200">如果您讓 Azure 入口網站維持開啟，可能必須重新整理刀鋒視窗以便查看新的資源。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-200">If you have the Azure portal open, you might have to refresh the blade to see new resources.</span></span>  

    <span data-ttu-id="a1f7a-201">此主控台應用程式從開始到完成的完整執行應該需要五分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-201">It should take about five minutes for this console application to run completely from start to finish.</span></span> <span data-ttu-id="a1f7a-202">應用程式已完成之後、所有資源和資源群組刪除之前，可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a1f7a-202">It may take several minutes after the application has finished before all the resources and the resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a1f7a-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1f7a-203">Next steps</span></span>

- <span data-ttu-id="a1f7a-204">如果部署有問題，下一個步驟就是查看 [使用 Azure 入口網站針對資源群組部署進行疑難排解](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a1f7a-204">If there were issues with the deployment, a next step would be to look at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="a1f7a-205">深入了解 [Azure Python 程式庫](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="a1f7a-205">Learn more about the [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

