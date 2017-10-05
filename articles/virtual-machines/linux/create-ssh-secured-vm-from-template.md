---
title: "從範本在 Azure 中建立 Linux VM | Microsoft Docs"
description: "如何使用 Azure CLI 2.0 從 Resource Manager 範本建立 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 908a8a0c82b2d21fb25c9b33dbd714570d1ac272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="aca73-103">如何使用 Azure Resource Manager 範本建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="aca73-103">How to create a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="aca73-104">本文示範如何使用 Azure Resource Manager 範本和 Azure CLI 2.0，快速部署 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="aca73-104">This article shows you how to quickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and the Azure CLI 2.0.</span></span> <span data-ttu-id="aca73-105">您也可以使用 [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="aca73-105">You can also perform these steps with the [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="aca73-106">範本概觀</span><span class="sxs-lookup"><span data-stu-id="aca73-106">Templates overview</span></span>
<span data-ttu-id="aca73-107">Azure Resource Manager 範本是 JSON 檔案，檔案中定義您的 Azure 解決方案的基礎結構和組態。</span><span class="sxs-lookup"><span data-stu-id="aca73-107">Azure Resource Manager templates are JSON files that define the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="aca73-108">透過範本，您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。</span><span class="sxs-lookup"><span data-stu-id="aca73-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="aca73-109">若要深入了解範本格式和其建構方式，請參閱[建立第一個 Azure Resource Manager 範本](../../azure-resource-manager/resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="aca73-109">To learn more about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="aca73-110">若要檢視資源類型的 JSON 語法，請參閱[在 Azure Resource Manager 範本中定義資源](/azure/templates/)。</span><span class="sxs-lookup"><span data-stu-id="aca73-110">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="aca73-111">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="aca73-111">Create resource group</span></span>
<span data-ttu-id="aca73-112">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="aca73-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="aca73-113">資源群組必須在虛擬機器之前建立。</span><span class="sxs-lookup"><span data-stu-id="aca73-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="aca73-114">以下範例會在 eastus 區域建立名為 myResourceGroupVM 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="aca73-114">The following example creates a resource group named *myResourceGroupVM* in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="aca73-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="aca73-115">Create virtual machine</span></span>
<span data-ttu-id="aca73-116">以下範例使用 [az group deployment create](/cli/azure/group/deployment#create)，從[這個 Azure Resource Manager 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)建立 VM︰</span><span class="sxs-lookup"><span data-stu-id="aca73-116">The following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="aca73-117">提供您自己 SSH 公開金鑰的值，例如 ~/.ssh/id_rsa.pub 的內容。</span><span class="sxs-lookup"><span data-stu-id="aca73-117">Provide the value of your own SSH public key, such as the contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="aca73-118">如果您需要建立 SSH 金鑰組，請參閱[如何為 Azure 中的 Linux VM 建立和使用的 SSH 金鑰組](mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="aca73-118">If you need to create an SSH key pair, see [How to create and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="aca73-119">在此範例中，會指定存放在 GitHub 中的範本。</span><span class="sxs-lookup"><span data-stu-id="aca73-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="aca73-120">您也可以下載或建立範本，並用相同 `--template-file` 參數指定本機路徑。</span><span class="sxs-lookup"><span data-stu-id="aca73-120">You can also download or create a template and specify the local path with the same `--template-file` parameter.</span></span>

<span data-ttu-id="aca73-121">若要透過 SSH 連線至您的 VM，使用 [az network public-ip show](/cli/azure/network/public-ip#show) 取公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="aca73-121">To SSH to your VM, obtain the public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="aca73-122">之後您便可以如常透過 SSH 連線至您的 VM︰</span><span class="sxs-lookup"><span data-stu-id="aca73-122">You can then SSH to your VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="aca73-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aca73-123">Next steps</span></span>
<span data-ttu-id="aca73-124">在此範例中，您建立基本的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="aca73-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="aca73-125">如需其他 Resource Manager 範本，包含應用程式架構，或建立更複雜的環境，瀏覽 [Azure 快速入門範本資源庫](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="aca73-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse the [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>