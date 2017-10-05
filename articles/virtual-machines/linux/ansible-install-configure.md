---
title: "安裝及設定 Ansible 以搭配 Azure 虛擬機器使用 | Microsoft Docs"
description: "了解如何安裝及設定 Ansible，以便管理 Ubuntu、CentOS 和 SLES 上的 Azure 資源"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: 52b763274437961dccfc862c8a45fbd57ea9fc4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-ansible-to-manage-virtual-machines-in-azure"></a><span data-ttu-id="5d59e-103">安裝及設定 Ansible 來管理 Azure 中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d59e-103">Install and configure Ansible to manage virtual machines in Azure</span></span>
<span data-ttu-id="5d59e-104">本文詳細說明如何針對某些最常見的 Linux 發行版，安裝 Ansible 和必要的 Azure Python SDK 模組。</span><span class="sxs-lookup"><span data-stu-id="5d59e-104">This article details how to install Ansible and required Azure Python SDK modules for some of the most common Linux distros.</span></span> <span data-ttu-id="5d59e-105">您可以配合特定的平台調整安裝的套件，來將 Ansible 安裝在其他發行版上。</span><span class="sxs-lookup"><span data-stu-id="5d59e-105">You can install Ansible on other distros by adjusting the installed packages to fit your particular platform.</span></span> <span data-ttu-id="5d59e-106">為了以安全的方式建立 Azure 資源，您也將了解如何建立及定義 Ansible 所要使用的認證。</span><span class="sxs-lookup"><span data-stu-id="5d59e-106">To create Azure resources in a secure manner, you also learn how to create and define credentials for Ansible to use.</span></span> 

<span data-ttu-id="5d59e-107">如需其他平台的更多安裝選項和步驟，請參閱 [Ansible 安裝指南](https://docs.ansible.com/ansible/intro_installation.html)。</span><span class="sxs-lookup"><span data-stu-id="5d59e-107">For more installation options and steps for additional platforms, see the [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="5d59e-108">安裝 Ansible</span><span class="sxs-lookup"><span data-stu-id="5d59e-108">Install Ansible</span></span>
<span data-ttu-id="5d59e-109">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d59e-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5d59e-110">下列範例會在 *eastus* 位置建立名為 *myResourceGroupAnsible* 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="5d59e-110">The following example creates a resource group named *myResourceGroupAnsible* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="5d59e-111">現在建立 VM，並針對下列其中一個發行版安裝 Ansible：</span><span class="sxs-lookup"><span data-stu-id="5d59e-111">Now create a VM and install Ansible for one of the following distros:</span></span>

- [<span data-ttu-id="5d59e-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="5d59e-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="5d59e-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="5d59e-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="5d59e-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="5d59e-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="5d59e-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="5d59e-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="5d59e-116">使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5d59e-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5d59e-117">下列範例會建立名為 *myVMAnsible* 的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d59e-117">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="5d59e-118">使用 VM 建立作業中的輸出所記錄的 `publicIpAddress` SSH 到您的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d59e-118">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="5d59e-119">在您的 VM 上，安裝 Azure Python SDK 模組和 Ansible 所需的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d59e-119">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="5d59e-120">現在繼續前往[建立 Azure 認證](#create-azure-credentials)。</span><span class="sxs-lookup"><span data-stu-id="5d59e-120">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="5d59e-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="5d59e-121">CentOS 7.3</span></span>
<span data-ttu-id="5d59e-122">使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5d59e-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5d59e-123">下列範例會建立名為 *myVMAnsible* 的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d59e-123">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="5d59e-124">使用 VM 建立作業中的輸出所記錄的 `publicIpAddress` SSH 到您的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d59e-124">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="5d59e-125">在您的 VM 上，安裝 Azure Python SDK 模組和 Ansible 所需的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d59e-125">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="5d59e-126">現在繼續前往[建立 Azure 認證](#create-azure-credentials)。</span><span class="sxs-lookup"><span data-stu-id="5d59e-126">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="5d59e-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="5d59e-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="5d59e-128">使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5d59e-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5d59e-129">下列範例會建立名為 *myVMAnsible* 的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d59e-129">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="5d59e-130">使用 VM 建立作業中的輸出所記錄的 `publicIpAddress` SSH 到您的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d59e-130">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="5d59e-131">在您的 VM 上，安裝 Azure Python SDK 模組和 Ansible 所需的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d59e-131">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="5d59e-132">現在繼續前往[建立 Azure 認證](#create-azure-credentials)。</span><span class="sxs-lookup"><span data-stu-id="5d59e-132">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="5d59e-133">建立 Azure 認證</span><span class="sxs-lookup"><span data-stu-id="5d59e-133">Create Azure credentials</span></span>
<span data-ttu-id="5d59e-134">Ansible 會使用使用者名稱與密碼或服務主體與 Azure 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="5d59e-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="5d59e-135">Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 Ansible 等自動化工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5d59e-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="5d59e-136">您可以控制和定義對於服務主體可以在 Azure 中執行哪些作業的權限。</span><span class="sxs-lookup"><span data-stu-id="5d59e-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="5d59e-137">為了提高只提供使用者名稱和密碼的安全性，此範例會建立基本的服務主體。</span><span class="sxs-lookup"><span data-stu-id="5d59e-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="5d59e-138">使用 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 建立服務主體，並將 Ansible 所需的認證輸出：</span><span class="sxs-lookup"><span data-stu-id="5d59e-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="5d59e-139">上述命令的輸出範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d59e-139">An example of the output from the preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="5d59e-140">若要向 Azure 驗證，您也需要使用 [az account show](/cli/azure/account#show) 取得 Azure 訂用帳戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="5d59e-140">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="5d59e-141">您將在下一個步驟中使用這兩個命令的輸出。</span><span class="sxs-lookup"><span data-stu-id="5d59e-141">You use the output from these two commands in the next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="5d59e-142">建立 Ansible 認證檔案</span><span class="sxs-lookup"><span data-stu-id="5d59e-142">Create Ansible credentials file</span></span>
<span data-ttu-id="5d59e-143">若要提供認證給 Ansible，您可以定義環境變數或建立本機認證檔案。</span><span class="sxs-lookup"><span data-stu-id="5d59e-143">To provide credentials to Ansible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="5d59e-144">如需如何定義 Ansible 認證的詳細資訊，請參閱 [Providing Credentials to Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules) (提供認證給 Azure 模組)。</span><span class="sxs-lookup"><span data-stu-id="5d59e-144">For more information about how to define Ansible credentials, see [Providing Credentials to Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="5d59e-145">針對開發環境，在您的主機 VM 上建立 Ansible 的「認證」檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d59e-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="5d59e-146">「認證」檔案本身結合了訂用帳戶識別碼與建立服務主體的輸出。</span><span class="sxs-lookup"><span data-stu-id="5d59e-146">The *credentials* file itself combines the subscription ID with the output of creating a service principal.</span></span> <span data-ttu-id="5d59e-147">對於 *client_id*、*secret* 和 *tenant*，先前 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 命令的輸出必須是相同順序。</span><span class="sxs-lookup"><span data-stu-id="5d59e-147">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="5d59e-148">下列範例*認證*檔案顯示符合上述輸出的值。</span><span class="sxs-lookup"><span data-stu-id="5d59e-148">The following example *credentials* file shows these values matching the previous output.</span></span> <span data-ttu-id="5d59e-149">輸入您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5d59e-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="5d59e-150">使用 Ansible 環境變數</span><span class="sxs-lookup"><span data-stu-id="5d59e-150">Use Ansible environment variables</span></span>
<span data-ttu-id="5d59e-151">如果您想要使用 Ansible Tower 或 Jenkins 等工具，您可以如下所示定義環境變數。</span><span class="sxs-lookup"><span data-stu-id="5d59e-151">If you are going to use tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="5d59e-152">這些變數結合了訂用帳戶識別碼與建立服務主體的輸出。</span><span class="sxs-lookup"><span data-stu-id="5d59e-152">These variables combine the subscription ID with the output from creating a service principal.</span></span> <span data-ttu-id="5d59e-153">對於 *AZURE_CLIENT_ID*、*AZURE_SECRET* 和 *AZURE_TENANT*，先前 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 命令的輸出必須是相同順序。</span><span class="sxs-lookup"><span data-stu-id="5d59e-153">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="5d59e-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d59e-154">Next steps</span></span>
<span data-ttu-id="5d59e-155">您現在已安裝 Ansible 和必要的 Azure Python SDK 模組，並已定義 Ansible 所要使用的認證。</span><span class="sxs-lookup"><span data-stu-id="5d59e-155">You now have Ansible and the required Azure Python SDK modules installed, and credentials defined for Ansible to use.</span></span> <span data-ttu-id="5d59e-156">了解如何[使用 Ansible 建立 VM](ansible-create-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="5d59e-156">Learn how to [create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="5d59e-157">您也可以了解如何[使用 Ansible 建立完整的 Azure VM 和支援資源](ansible-create-complete-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="5d59e-157">You can also learn how to [create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>