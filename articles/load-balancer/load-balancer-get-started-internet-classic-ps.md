---
title: "aaaCreate 網際網路對向負載平衡器-傳統的 Azure PowerShell |Microsoft 文件"
description: "了解如何的 toocreate 網際網路向負載平衡器中使用 PowerShell 的傳統模式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>開始在 PowerShell 中建立網際網路面向的負載平衡器 (傳統)

> [!div class="op_single_selector"]
> * [Azure 傳統入口網站](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 雲端服務](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> 您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。 在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。 您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。 本文涵蓋 hello 傳統部署模型。 您也可以[toocreate 網際網路向負載平衡器使用 Azure 資源管理員的如何了解](load-balancer-get-started-internet-arm-ps.md)。

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>使用 PowerShell 設定負載平衡器

tooset 設定負載平衡器使用 powershell，請遵循下列 hello 步驟：

1. 如果您從未使用過 Azure PowerShell，請參閱[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示所有 hello 方式 toohello 結束 toosign 至 Azure，然後選取您的訂用帳戶。
2. 建立虛擬機器之後，您可以使用 PowerShell cmdlet tooadd 負載平衡器 tooa 虛擬機器內 hello 相同雲端服務。

在 hello 下列的範例，您將加入負載平衡器集稱為 「 web 伺服陣列 」 toocloud 服務 」 mytestcloud 」 （或 myctestcloud.cloudapp.net），加入 hello hello 端點負載平衡器 toovirtual 機器命名為"web1"和"web2"。 hello 負載平衡器會接收連接埠 80 上的網路流量並 hello hello 本機端點 （在本案例通訊埠 80） 所定義的虛擬機器之間進行負載平衡使用 TCP。

### <a name="step-1"></a>步驟 1

建立 hello 第一個 VM 「 web1 」 的負載平衡端點

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>步驟 2

建立另一個端點 hello 第二個 VM 「 web2 」 使用 hello 相同負載平衡器集名稱

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>從負載平衡器移除虛擬機器

您可以使用移除 AzureEndpoint tooremove 從 hello 負載平衡器虛擬機器端點

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>後續步驟

您也可以[開始建立內部負載平衡器](load-balancer-get-started-ilb-classic-ps.md)，以及為特定負載平衡器的網路流量行為設定何種[分配模式](load-balancer-distribution-mode.md)。

如果您的應用程式需要 tookeep 連線運作的負載平衡器後方的伺服器，您可以瞭解多[閒置 TCP 逾時設定的負載平衡器](load-balancer-tcp-idle-timeout.md)。 當您使用 Azure 負載平衡器，它會協助 toolearn 有關閒置連線行為。
