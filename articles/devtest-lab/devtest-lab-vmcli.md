---
title: "使用 Azure CLI 在 DevTest Labs 中建立和管理虛擬機器 | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 在 Azure DevTest Labs 中建立和管理虛擬機器"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 42b0448c1bcdfa909715abd5075353d63cab8389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="c183b-103">使用 Azure CLI 在 DevTest Labs 中建立和管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c183b-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="c183b-104">本快速入門會引導您完成建立、啟動、連線、更新和清理實驗室中的開發電腦。</span><span class="sxs-lookup"><span data-stu-id="c183b-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="c183b-105">開始之前：</span><span class="sxs-lookup"><span data-stu-id="c183b-105">Before you begin:</span></span>

* <span data-ttu-id="c183b-106">若尚未建立實驗室，請參閱[這裡](devtest-lab-create-lab.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="c183b-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="c183b-107">[安裝 CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="c183b-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="c183b-108">若要開始，請執行 az login 建立 Azure 連線。</span><span class="sxs-lookup"><span data-stu-id="c183b-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="c183b-109">建立並確認虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c183b-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="c183b-110">使用 SSH 驗證從 Marketplace 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="c183b-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="c183b-111">在 --resource-group 參數中放入**實驗室的資源群組**名稱。</span><span class="sxs-lookup"><span data-stu-id="c183b-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="c183b-112">如果您想要使用公式建立 VM，請在 [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create) 中使用 --formula 參數。</span><span class="sxs-lookup"><span data-stu-id="c183b-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="c183b-113">確認有可用的 VM。</span><span class="sxs-lookup"><span data-stu-id="c183b-113">Verify that the VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="c183b-114">啟動並連接至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c183b-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="c183b-115">啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="c183b-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="c183b-116">在 --resource-group 參數中放入**實驗室的資源群組**名稱。</span><span class="sxs-lookup"><span data-stu-id="c183b-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="c183b-117">連接到 VM：[SSH](../virtual-machines/linux/mac-create-ssh-keys.md) 或[遠端桌面](../virtual-machines/windows/connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="c183b-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="c183b-118">更新虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c183b-118">Update the virtual machine</span></span>
<span data-ttu-id="c183b-119">將構件套用至 VM。</span><span class="sxs-lookup"><span data-stu-id="c183b-119">Apply artifacts to a VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="c183b-120">列出實驗室中可用的構件。</span><span class="sxs-lookup"><span data-stu-id="c183b-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="c183b-121">停止並刪除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c183b-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="c183b-122">停止 VM。</span><span class="sxs-lookup"><span data-stu-id="c183b-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="c183b-123">刪除 VM。</span><span class="sxs-lookup"><span data-stu-id="c183b-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]