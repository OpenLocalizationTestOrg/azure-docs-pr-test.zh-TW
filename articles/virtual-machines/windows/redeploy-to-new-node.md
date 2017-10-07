---
title: "aaaRedeploy Windows Azure 中虛擬機器 |Microsoft 文件"
description: "如何 tooredeploy Windows 虛擬機器中 Azure toomitigate RDP 連線問題。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>重新部署 Windows 虛擬機器 toonew Azure 節點
如果您有已遇到問題疑難排解遠端桌面 (RDP) 連線或應用程式存取 tooWindows 型 Azure 虛擬機器 (VM)，重新部署 VM 可能有助於的 hello。 當您重新部署 VM 時，它移動 hello Azure 基礎結構中的 hello VM tooa 新節點，然後開啟其電源上，保留所有組態選項及相關聯的資源。 本文章將示範如何 tooredeploy 的 VM 使用 Azure PowerShell 或 hello Azure 入口網站。

> [!NOTE]
> 您重新部署 VM 之後，hello 暫存磁碟遺失，且會更新虛擬網路介面相關聯的動態 IP 位址。 


## <a name="using-azure-powershell"></a>使用 Azure PowerShell
請確定您擁有 hello 最新 Azure PowerShell 1.x 安裝在您的電腦上。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

hello 下列範例會將部署 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>後續步驟
如果您有連接 tooyour VM 的問題，您可以在找到特定說明[疑難排解 RDP 連線](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[詳細的疑難排解步驟的 RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如果無法存取在您 VM 上執行的應用程式，您也可以參閱[應用程式疑難排解問題](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

