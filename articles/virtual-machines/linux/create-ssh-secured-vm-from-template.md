---
title: "從範本 aaaCreate Azure 中的 Linux VM |Microsoft 文件"
description: "如何 toouse 會 hello Azure CLI 2.0 toocreate Resource Manager 範本從 Linux VM"
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
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="82e31-103">如何 toocreate Linux 虛擬機器與 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="82e31-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="82e31-104">本文示範 tooquickly 部署 Linux 虛擬機器 (VM) 與 Azure 資源管理員範本 hello Azure CLI 2.0 的方式。</span><span class="sxs-lookup"><span data-stu-id="82e31-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="82e31-105">您也可以執行下列步驟以 hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="82e31-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="82e31-106">範本概觀</span><span class="sxs-lookup"><span data-stu-id="82e31-106">Templates overview</span></span>
<span data-ttu-id="82e31-107">Azure 資源管理員範本是 hello 基礎結構和 Azure 方案的組態中定義的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="82e31-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="82e31-108">透過範本，您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。</span><span class="sxs-lookup"><span data-stu-id="82e31-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="82e31-109">toolearn 進一步了解 hello 格式 hello 範本和建構它，請參閱[建立第一個 Azure Resource Manager 範本](../../azure-resource-manager/resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="82e31-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="82e31-110">tooview hello JSON 語法資源類型，請參閱[Azure Resource Manager 範本中定義的資源](/azure/templates/)。</span><span class="sxs-lookup"><span data-stu-id="82e31-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="82e31-111">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="82e31-111">Create resource group</span></span>
<span data-ttu-id="82e31-112">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="82e31-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="82e31-113">資源群組必須在虛擬機器之前建立。</span><span class="sxs-lookup"><span data-stu-id="82e31-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="82e31-114">hello 下列範例會建立名為的資源群組*myResourceGroupVM*在 hello *eastus*區域：</span><span class="sxs-lookup"><span data-stu-id="82e31-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="82e31-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="82e31-115">Create virtual machine</span></span>
<span data-ttu-id="82e31-116">hello 下列範例會建立將 VM 從[此 Azure Resource Manager 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)與[az 群組部署建立](/cli/azure/group/deployment#create)。</span><span class="sxs-lookup"><span data-stu-id="82e31-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="82e31-117">提供您自己 SSH 公開金鑰，例如 hello 內容 hello 值*~/.ssh/id_rsa.pub*。</span><span class="sxs-lookup"><span data-stu-id="82e31-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="82e31-118">如果您需要 toocreate 的 SSH 金鑰組，請參閱[如何 toocreate 及使用 SSH 金鑰組適用於在 Azure 中的 Linux Vm](mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="82e31-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="82e31-119">在此範例中，會指定存放在 GitHub 中的範本。</span><span class="sxs-lookup"><span data-stu-id="82e31-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="82e31-120">您也可以下載或建立範本及指定 hello 本機路徑以 hello 相同`--template-file`參數。</span><span class="sxs-lookup"><span data-stu-id="82e31-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="82e31-121">tooSSH tooyour VM，取得與 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="82e31-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="82e31-122">然後，您可以像平常一樣 SSH tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="82e31-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="82e31-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82e31-123">Next steps</span></span>
<span data-ttu-id="82e31-124">在此範例中，您建立基本的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="82e31-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="82e31-125">對於多個資源管理員範本包含應用程式架構，或建立更複雜的環境，瀏覽 hello [Azure 快速入門範本圖庫](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="82e31-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
