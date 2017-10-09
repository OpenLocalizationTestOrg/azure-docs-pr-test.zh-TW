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
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>建立和管理與使用 Azure CLI hello 的 DevTest Labs 虛擬機器
本快速入門會引導您完成建立、啟動、連線、更新和清理實驗室中的開發電腦。 

開始之前：

* 若尚未建立實驗室，請參閱[這裡](devtest-lab-create-lab.md)的指示。

* [安裝 CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。 toostart 執行 az 登入 toocreate 與 Azure 的連線。 

## <a name="create-and-verify-hello-virtual-machine"></a>建立並確認 hello 虛擬機器 
使用 SSH 驗證從 Marketplace 映像建立 VM。
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Put hello **lab 的資源群組**hello-資源群組參數的名稱。
>

如果您想 toocreate 使用公式的 VM，請使用 hello-公式中的參數[az 實驗室 vm 建立](https://docs.microsoft.com/cli/azure/lab/vm#create)。


請確認該 hello VM。
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

## <a name="start-and-connect-toohello-virtual-machine"></a>啟動並連接 toohello 虛擬機器
啟動 VM。
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Put hello **lab 的資源群組**hello-資源群組參數的名稱。
>

連接 tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md)或[遠端桌面](../virtual-machines/windows/connect-logon.md)。
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>更新 hello 虛擬機器
套用成品 tooa VM。
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

列出可用 hello 實驗室中的成品。
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>停止並刪除 hello 虛擬機器    
停止 VM。
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

刪除 VM。
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]