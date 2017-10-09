---
title: "aaaOMS 適用於 Linux 的 Azure 虛擬機器擴充功能 |Microsoft 文件"
description: "部署 hello 使用虛擬機器擴充功能的 Linux 虛擬機器上的 OMS 代理程式。"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>適用於 Linux 的 OMS 虛擬機器擴充功能

## <a name="overview"></a>概觀

Operations Management Suite (OMS) 可提供雲端和內部部署資產的監視、警示和警示補救功能。 發行 hello OMS Agent for Linux 的虛擬機器擴充功能和 Microsoft 支援。 hello 延伸模組會安裝 Azure 的虛擬機器上的 hello OMS 代理程式，並註冊到現有的 OMS 工作區的虛擬機器。 此文件詳細資料 hello 支援平台、 組態和部署選項 hello OMS 虛擬機器擴充功能適用於 Linux。

## <a name="prerequisites"></a>必要條件

### <a name="operating-system"></a>作業系統

hello OMS 代理程式延伸模組可以執行這些 Linux 散發套件。

| 配送映像 | 版本 |
|---|---|
| CentOS Linux | 5、6 和 7 |
| Oracle Linux | 5、6 和 7 |
| Red Hat Enterprise Linux Server | 5、6 和 7 |
| Debian GNU/Linux | 6、7 和 8 |
| Ubuntu | 12.04 LTS、14.04 LTS、15.04、15.10、16.04 LTS |
| SUSE Linux Enterprise Server | 11 和 12 |

### <a name="internet-connectivity"></a>網際網路連線

hello 適用於 Linux 的 OMS 代理程式延伸模組需要該 hello 目標虛擬機器已連接的 toohello 網際網路。 

## <a name="extension-schema"></a>擴充功能結構描述

hello 下列 JSON 顯示 hello hello OMS 代理程式延伸結構描述。 hello 延伸模組需要 hello 工作區識別碼和工作區金鑰從 hello 目標 OMS 工作區。hello OMS 入口網站中可以找到這些值。 Hello 工作區金鑰應該視為機密資料，因為它應該儲存在受保護的設定。 Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。 請注意，**workspaceId** 和 **workspaceKey** 區分大小寫。

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>屬性值

| 名稱 | 值 / 範例 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| 類型 | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (例如) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (例如) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |


## <a name="template-deployment"></a>範本部署

也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。 部署一或多個虛擬機器需要 post 部署設定，例如登入 tooOMS 時，範本很理想。 包含 hello OMS 代理程式 VM 擴充功能的範例資源管理員範本可找到 hello [Azure 快速入門圖庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm)。 

可以巢狀方式置於 hello 虛擬機器的資源，或放在 hello 根或資源管理員 JSON 範本的最上層 hello JSON 設定虛擬機器擴充功能。 hello 放置 hello JSON 組態會影響 hello hello 資源名稱和類型的值。 如需詳細資訊，請參閱[設定子資源的名稱和類型](../../azure-resource-manager/resource-manager-template-child-resource.md)。 

hello 下列範例假設 hello OMS 擴充功能位於 hello 虛擬機器資源。 巢狀 hello 延伸模組資源、 hello JSON 會放置於 hello `"resources": []` hello 虛擬機器的物件。

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

根目錄 hello hello 範本 hello 擴充 JSON 時，hello 資源名稱包含參考 toohello 父虛擬機器，並 hello 類型會反映 hello 巢狀的組態。  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Azure CLI 部署

hello Azure CLI 可以是使用的 toodeploy hello OMS 代理程式 VM 延伸模組 tooan 現有的虛擬機器。 取代為 hello OMS 金鑰和 OMS 識別碼從 OMS 工作區。 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>疑難排解與支援

### <a name="troubleshoot"></a>疑難排解

從 hello Azure 入口網站，也可以使用 Azure CLI hello，可以擷取有關 hello 部署狀態的延伸模組的資料。 toosee hello 部署狀態的延伸模組指定的 vm，執行下列命令使用 hello hello Azure CLI。

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

延伸模組執行輸出記錄的 toohello 之後，檔案：

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>錯誤碼及其意義

| 錯誤碼 | 意義 | 可能的動作 |
| :---: | --- | --- |
| 10 | VM 已連接的 tooan OMS 工作區 | tooconnect hello VM toohello 工作區中 hello 延伸結構描述，指定在公用的設定中設定 stopOnMultipleConnections toofalse 或移除這個屬性。 針對此 VM 所連線的每個工作區都會向此 VM 計費一次。 |
| 11 | 無效的設定提供 toohello 延伸模組 | 請遵循 hello 前面範例 tooset 部署所需的所有屬性值。 |
| 12 | 已鎖定 hello 以 dpkg 封裝管理員 | 請確定所有以 dpkg 更新作業 hello 電腦上的完成，然後重試。 |
| 20 | 啟用提前呼叫 | [更新 hello Azure Linux 代理程式](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent)toohello 最新可用版本。 |
| 51 | Hello VM 的作業系統不支援這項擴充功能 | |
| 55 | 無法連接 toohello Microsoft Operations Management Suite 服務 | 核取 hello 系統有網際網路存取權，或已提供有效的 HTTP proxy。 此外，請檢查 hello 正確性的 hello 工作區識別碼。 |

其他疑難排解資訊位於 hello [OMS 的代理程式-為-Linux 疑難排解指南](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#)。

### <a name="support"></a>支援

如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello 上 hello Azure 專家[MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。 使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。
