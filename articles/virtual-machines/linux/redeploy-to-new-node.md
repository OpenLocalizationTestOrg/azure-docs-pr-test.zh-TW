---
title: "在 Azure 中 Linux 虛擬機器 aaaRedeploy |Microsoft 文件"
description: "如何 tooredeploy Linux 虛擬機器中 Azure toomitigate SSH 連線問題。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>重新部署 Linux 虛擬機器 toonew Azure 節點
如果您遇到困難疑難排解 SSH 或應用程式在 Azure 中存取 tooa Linux 虛擬機器 (VM)，重新部署 hello VM 可能幫助。 當您重新部署 VM 時，它會移 hello Azure 基礎結構中的 hello VM tooa 新節點，並再開啟它回到上的電源。 您所有組態選項和相關聯的資源都會加以保留。 本文章將示範如何使用 Azure CLI 或 hello Azure 入口網站的 VM 的 tooredeploy。

> [!NOTE]
> 您重新部署 VM 之後，hello 暫存磁碟遺失，且會更新虛擬網路介面相關聯的動態 IP 位址。 

您可以重新部署 VM，使用其中一種 hello 下列選項。 您只需要一個選項 tooredeploy toochoose VM:

- [Azure CLI 2.0](#azure-cli-20)
- [Azure CLI 1.0](#azure-cli-10)
- [Azure 入口網站](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>使用 Azure CLI 2.0 hello
最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。

使用 [az vm redeploy](/cli/azure/vm#redeploy) 來重新部署 VM。 下列範例重新部署的 hello hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>使用 Azure CLI 1.0 hello
安裝 hello[最新的 Azure CLI 1.0](../../cli-install-nodejs.md)，登入 tooan Azure 帳戶，並確定您是在 Resource Manager 模式 (`azure config mode arm`)。

下列範例重新部署的 hello hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>後續步驟
如果您有連接 tooyour VM 的問題，您可以在找到特定說明[SSH 連接的疑難排解](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或[詳細的疑難排解步驟的 SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 如果無法存取在您 VM 上執行的應用程式，您也可以參閱[應用程式疑難排解問題](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

