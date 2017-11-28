---
title: "使用 Azure 範本與 Azure CLI 1.0 建立 Linux VM | Microsoft Docs"
description: "使用 Azure CLI 1.0 和 Azure Resource Manager 範本在 Azure 上建立 Linux VM。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="6d29d-103">如何使用 Azure CLI 1.0 和 Azure Resource Manager 範本建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="6d29d-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="6d29d-104">本文示範如何使用 Azure CLI 1.0 和 Azure Resource Manager 範本快速部署 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6d29d-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="6d29d-105">本文需要：</span><span class="sxs-lookup"><span data-stu-id="6d29d-105">The article requires:</span></span>

* <span data-ttu-id="6d29d-106">一個 Azure 帳戶 ([取得免費試用帳戶](https://azure.microsoft.com/pricing/free-trial/))。</span><span class="sxs-lookup"><span data-stu-id="6d29d-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="6d29d-107">使用 `azure login` 登入的 [Azure CLI 1.0](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="6d29d-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="6d29d-108">Azure CLI *必須處於* Azure Resource Manager 模式 `azure config mode arm`。</span><span class="sxs-lookup"><span data-stu-id="6d29d-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="6d29d-109">您也可以使用 [Azure 入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)來快速部署 Linux VM 範本。</span><span class="sxs-lookup"><span data-stu-id="6d29d-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6d29d-110">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="6d29d-110">CLI versions to complete the task</span></span>
<span data-ttu-id="6d29d-111">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="6d29d-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6d29d-112">[Azure CLI 1.0](#quick-command-summary) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="6d29d-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6d29d-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="6d29d-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="6d29d-114">快速命令摘要</span><span class="sxs-lookup"><span data-stu-id="6d29d-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="6d29d-115">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="6d29d-115">Detailed Walkthrough</span></span>
<span data-ttu-id="6d29d-116">範本可讓您在 Azure 上使用要在啟動期間自訂的設定 (如使用者名稱和主機名稱等設定) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="6d29d-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="6d29d-117">在本文中，我們推出的 Azure 範本會利用 Ubuntu VM 以及連接埠 22 對 SSH 開放的網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="6d29d-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="6d29d-118">Azure Resource Manager 範本是 JSON 檔案，可用於進行簡單的一次性工作 (如本文中的啟動 Ubuntu VM)。</span><span class="sxs-lookup"><span data-stu-id="6d29d-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="6d29d-119">Azure 範本也可用來建構整個環境的複雜 Azure 組態，例如測試、開發或生產部署堆疊。</span><span class="sxs-lookup"><span data-stu-id="6d29d-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="6d29d-120">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="6d29d-120">Create the Linux VM</span></span>
<span data-ttu-id="6d29d-121">下列程式碼範例示範如何呼叫 `azure group create` ，以使用 [此 Azure Resource Manager 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)同時建立資源群組和部署受 SSH 保護的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="6d29d-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="6d29d-122">請記住，在您的範例中您必須使用環境中唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d29d-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="6d29d-123">此範例則以 myResourceGroup 作做為資源群組名稱，並以 myVM 作為 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="6d29d-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="6d29d-124">輸出應該看起來像下列的輸出區塊：</span><span class="sxs-lookup"><span data-stu-id="6d29d-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="6d29d-125">該範例使用 `--template-uri` 參數部署 VM。</span><span class="sxs-lookup"><span data-stu-id="6d29d-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="6d29d-126">您也可以使用 `--template-file` 參數並以範本檔案路徑做為引數，在本機下載或建立範本並傳遞範本。</span><span class="sxs-lookup"><span data-stu-id="6d29d-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="6d29d-127">Azure CLI 會提示您輸入範本所需的參數。</span><span class="sxs-lookup"><span data-stu-id="6d29d-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d29d-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d29d-128">Next steps</span></span>
<span data-ttu-id="6d29d-129">請搜尋 [範本庫](https://azure.microsoft.com/documentation/templates/) 以探索接下來要部署哪些應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="6d29d-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

