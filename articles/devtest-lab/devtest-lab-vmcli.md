---
title: "aaaCreate 及管理虛擬機器中使用 Azure CLI DevTest Labs |Microsoft 文件"
description: "深入了解如何 toouse Azure DevTest Labs toocreate 及管理 Azure CLI 2.0 的虛擬機器"
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
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="d345b-103">建立和管理與使用 Azure CLI hello 的 DevTest Labs 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d345b-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="d345b-104">本快速入門會引導您完成建立、啟動、連線、更新和清理實驗室中的開發電腦。</span><span class="sxs-lookup"><span data-stu-id="d345b-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="d345b-105">開始之前：</span><span class="sxs-lookup"><span data-stu-id="d345b-105">Before you begin:</span></span>

* <span data-ttu-id="d345b-106">若尚未建立實驗室，請參閱[這裡](devtest-lab-create-lab.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="d345b-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="d345b-107">[安裝 CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d345b-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="d345b-108">toostart 執行 az 登入 toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="d345b-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="d345b-109">建立並確認 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d345b-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="d345b-110">使用 SSH 驗證從 Marketplace 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="d345b-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="d345b-111">Put hello **lab 的資源群組**hello-資源群組參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="d345b-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="d345b-112">如果您想 toocreate 使用公式的 VM，請使用 hello-公式中的參數[az 實驗室 vm 建立](https://docs.microsoft.com/cli/azure/lab/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="d345b-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="d345b-113">請確認該 hello VM。</span><span class="sxs-lookup"><span data-stu-id="d345b-113">Verify that hello VM is available.</span></span>
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

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="d345b-114">啟動並連接 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d345b-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="d345b-115">啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="d345b-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="d345b-116">Put hello **lab 的資源群組**hello-資源群組參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="d345b-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="d345b-117">連接 tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md)或[遠端桌面](../virtual-machines/windows/connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="d345b-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="d345b-118">更新 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d345b-118">Update hello virtual machine</span></span>
<span data-ttu-id="d345b-119">套用成品 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="d345b-119">Apply artifacts tooa VM.</span></span>
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

<span data-ttu-id="d345b-120">列出可用 hello 實驗室中的成品。</span><span class="sxs-lookup"><span data-stu-id="d345b-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="d345b-121">停止並刪除 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d345b-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="d345b-122">停止 VM。</span><span class="sxs-lookup"><span data-stu-id="d345b-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="d345b-123">刪除 VM。</span><span class="sxs-lookup"><span data-stu-id="d345b-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]