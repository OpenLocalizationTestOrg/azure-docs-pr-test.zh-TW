---
title: "適用於 Windows Vm 在 Azure 中設定 aaaAvailability |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作指導方針在 Azure 基礎結構服務中部署可用性設定組。"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f9449f58-664b-4d5d-82f6-84c5d083047f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cc35fd1e913434d9facb94116edb1b1c30447c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-windows-vms"></a>適用於 Windows VM 的 Azure 可用性設定組指導方針

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

本文著重在所需的了解 hello 規劃步驟，為可用性設定組 tooensure 應用程式仍然可以存取在計劃性或非計劃性的事件。

## <a name="implementation-guidelines-for-availability-sets"></a>可用性設定組的實作指導方針
决策：

* 多少可用性設定組您需要 hello 各種角色與階層中您的應用程式基礎結構？

工作：

* 您要求每個應用程式層中定義 Vm 的 hello 數目。
* 判斷您是否需要使用您的應用程式的錯誤或更新網域 toobe tooadjust hello 數目。
* 定義使用命名慣例和功能的所需的 hello 可用性設定組的 Vm 位於它們。 一個可用性設定組中只能放置一個 VM。

## <a name="availability-sets"></a>可用性集合
在 Azure 中，虛擬機器 (Vm) 可以置於 tooa 邏輯群組稱為可用性設定組。 當您建立可用性設定組內的 Vm 時，hello Azure 平台會將這些 Vm 的 hello 放置分散 hello 基礎基礎結構。 應該有預定的維護事件 toohello Azure 平台或基礎硬體/基礎結構錯誤，hello 使用可用性設定組可確保至少一個 VM 仍繼續執行。

最佳作法是不將應用程式放置在單一 VM 上。 可用性設定組包含單一 VM 不會取得任何規劃或未規劃的事件內 hello Azure 平台的保護。 hello [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines)需要可用性集 tooallow hello 分配的 Vm hello 基礎基礎結構內的兩個或多個 Vm。 如果您使用[Azure 高階儲存體](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，hello Azure SLA 套用 tooa 單一 VM。

在 Azure 中的 hello 基礎結構就會劃分 toomultiple 硬體叢集中。 每個硬體叢集皆可支援某個 VM 大小範圍。 不論何時，可用性設定組都只能裝載在單一硬體叢集上。 因此，可以存在於一個可用性設定組中的 hello 範圍的 VM 大小是 hello 硬體叢集所支援的限制的 toohello 範圍的 VM 大小。 hello hello 可用性設定組中的第一個 VM 部署時，或啟動 hello hello 停止取消配置狀態目前是所有 Vm 的可用性設定組中的第一個 VM 時，會選取 hello 可用性設定組的 hello 硬體叢集。 下列 PowerShell 命令的 hello 可以是可用的可用性設定組的使用的 toodetermine hello 範圍的 VM 大小:"Get AzureRmVMSize ResourceGroupName\<字串\>-AvailabilitySetName\<字串\>"

每個硬體叢集分割 toomultiple 更新網域和故障網域。 這些網域是會根據主機是共用一般更新週期，或共用類似的實體基礎結構 (例如電源和網路功能) 來定義。 Azure 會自動發佈您的 Vm 內的可用性設定組，跨網域 toomaintain 可用性和容錯功能。 根據應用程式與 hello Vm 數目在可用性集合中的 hello 大小，您可以調整 hello 數目的網域中，您想 toouse。 您可以深入了解[管理更新和容錯網域的可用性及使用](manage-availability.md)。

在設計您的應用程式基礎結構時，規劃您使用的 hello 應用程式層。 群組 Vm 做 hello 相同用途 tooavailability 集，例如可用性設定組為您執行 IIS 的前端 Vm。 為執行 SQL Server 的後端 VM 建立個別的可用性設定組。 hello 目標是 tooensure 應用程式的每個元件受可用性設定組，且至少一次執行個體一定會保持執行。

負載平衡器可以利用每個可用性設定組旁的應用程式層 toowork 前面，並確保流量都可以路由的 tooa 執行執行個體。 沒有負載平衡器 Vm 可能會繼續執行在計劃性與非計劃性的維護事件，但使用者可能無法 tooresolve 它們如果 hello 主要 VM 處於無法使用。

針對儲存層的高可用性設計應用程式。 hello 最佳做法太[的可用性設定組的 Vm 使用受管理磁碟](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set)。 如果您目前使用未受管理的磁碟，我們強烈建議您使用太[轉換中可用性設定組 toouse 管理磁碟 Vm](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set)。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]
