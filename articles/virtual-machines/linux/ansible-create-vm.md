---
title: "使用 Ansible 在 Azure 中建立基本 Linux VM | Microsoft Docs"
description: "了解如何使用 Ansible 在 Azure 中建立及管理基本 Linux 虛擬機器"
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
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="61abf-103">使用 Ansible 在 Azure 中建立基本虛擬機器</span><span class="sxs-lookup"><span data-stu-id="61abf-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="61abf-104">Ansible 可讓您將環境中的資源部署和設定自動化。</span><span class="sxs-lookup"><span data-stu-id="61abf-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="61abf-105">您可以使用 Ansible 在 Azure 中管理虛擬機器 (VM)，就像是任何其他資源一樣。</span><span class="sxs-lookup"><span data-stu-id="61abf-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="61abf-106">本文示範如何使用 Ansible 建立基本 VM。</span><span class="sxs-lookup"><span data-stu-id="61abf-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="61abf-107">您也可以了解如何[使用 Ansible 建立完整的 VM 環境](ansible-create-complete-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="61abf-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="61abf-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="61abf-108">Prerequisites</span></span>
<span data-ttu-id="61abf-109">若要使用 Ansible 管理 Azure 資源，您需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="61abf-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="61abf-110">在您的主機系統上安裝 Ansible 和 Azure Python SDK 模組。</span><span class="sxs-lookup"><span data-stu-id="61abf-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="61abf-111">在 [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts)、[CentOS 7.3](ansible-install-configure.md#centos-73) 和 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2) 上安裝 Ansible</span><span class="sxs-lookup"><span data-stu-id="61abf-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="61abf-112">Azure 認證，並設定 Ansible 使用這些認證。</span><span class="sxs-lookup"><span data-stu-id="61abf-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="61abf-113">建立 Azure 認證和設定 Ansible</span><span class="sxs-lookup"><span data-stu-id="61abf-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="61abf-114">Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="61abf-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="61abf-115">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="61abf-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="61abf-116">如果您需要升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="61abf-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="61abf-117">您也可以在瀏覽器中使用 [Cloud Shell](/azure/cloud-shell/quickstart)。</span><span class="sxs-lookup"><span data-stu-id="61abf-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="61abf-118">建立支援的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="61abf-118">Create supporting Azure resources</span></span>
<span data-ttu-id="61abf-119">在此範例中，我們會建立一個 Runbook 來將 VM 部署到現有的基礎結構中。</span><span class="sxs-lookup"><span data-stu-id="61abf-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="61abf-120">首先，使用 [az group create](/cli/azure/vm#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="61abf-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="61abf-121">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="61abf-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="61abf-122">使用 [az network vnet create](/cli/azure/network/vnet#create) 為您的 VM 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="61abf-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="61abf-123">下列範例會建立名為 *myVnet* 的虛擬網路和名為 *mySubnet* 的子網路：</span><span class="sxs-lookup"><span data-stu-id="61abf-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="61abf-124">建立及執行 Ansible 腳本</span><span class="sxs-lookup"><span data-stu-id="61abf-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="61abf-125">建立名為 **azure_create_vm.yml** 的 Ansible 腳本，然後貼上下列內容。</span><span class="sxs-lookup"><span data-stu-id="61abf-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="61abf-126">此範例會建立單一 VM 並設定 SSH 認證。</span><span class="sxs-lookup"><span data-stu-id="61abf-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="61abf-127">在 *key_data* 配對中輸入您自己的公開金鑰資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="61abf-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="61abf-128">若要使用 Ansible 建立 VM，請如下所示執行腳本：</span><span class="sxs-lookup"><span data-stu-id="61abf-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="61abf-129">輸出看起來會類似下列範例，顯示已成功建立 VM：</span><span class="sxs-lookup"><span data-stu-id="61abf-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="61abf-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61abf-130">Next steps</span></span>
<span data-ttu-id="61abf-131">此範例會在現有的資源群組中建立 VM，並已部署虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="61abf-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="61abf-132">如需如何使用 Ansible 建立支援資源 (例如虛擬網路和網路安全性群組規則) 的更詳細範例，請參閱[使用 Ansible 建立完整的 VM 環境](ansible-create-complete-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="61abf-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>