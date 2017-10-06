---
title: "aaaTroubleshoot Linux VM 部署 RM |Microsoft 文件"
description: "針對在 Azure 中建立新 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>針對在 Azure 中建立新 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>常見問題
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

如需了解其他 VM 部署問題，請參閱[針對 Azure 中的 Linux 虛擬機器部署問題進行疑難排解](troubleshoot-deploy-vm.md)。
## <a name="collect-activity-logs"></a>收集活動記錄
疑難排解，toostart 收集 hello 活動與 hello 問題相關聯的 tooidentify hello 錯誤的記錄。 hello 下列連結包含 hello 程序 toofollow 的詳細的資訊。

[檢視部署作業](../../azure-resource-manager/resource-manager-deployment-operations.md)

[檢視活動記錄檔 toomanage Azure 資源](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:**如果 hello 作業系統一般化，Linux 和它已上傳及/或所擷取的 hello 一般化設定，則不會有任何錯誤。 同樣地，如果 hello OS Linux 特製化，且它已上傳及/或所擷取的 hello 特製化的設定，則不會有任何錯誤。

**上傳錯誤：**

**N<sup>1</sup>:**如果 hello OS Linux 一般化，而且會當做上傳的特製化，就會發生佈建的逾時錯誤因為 hello VM 停駐在 hello 佈建階段。

**N<sup>2</sup>:**如果 hello OS Linux 特製化，和上傳為一般化，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。

**解決方案：**

tooresolve 這兩個這些錯誤上, 傳 hello 原始 VHD，內部使用，與 hello 相同設定，與 hello OS （一般化/特製化）。 tooupload 為一般化，請記住 toorun-取消佈建第一次。

**擷取錯誤：**

**N<sup>3</sup>:**如果 hello OS Linux 一般化，而且都擷取成特製化，就會發生佈建的逾時錯誤因為 hello 原始 VM 就無法使用為它標示為一般化。

**N<sup>4</sup>:**是否 hello OS Linux 特製化，然後為一般化擷取，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。 此外，hello 原始 VM 並未使用因為它已標示為特製化。

**解決方案：**

tooresolve 這兩個這些錯誤，從 hello 入口網站中，刪除 hello 目前映像和[收復 hello 從目前的 Vhd](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)與 hello 相同設定，與 hello OS （一般化/特製化）。

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>問題︰自訂/資源庫/Marketplace 映像；配置失敗
Hello 新 VM 要求時無法支援所要求的 hello VM 大小或沒有可用的空間 tooaccommodate hello 要求已釘選的 tooa 叢集的情況下發生此錯誤。

**原因 1:** hello 叢集無法支援 hello 要求的 VM 大小。

**解決方式 1：**

* 重試 hello 要求使用較小的 VM 大小。
* 如果 hello hello 的大小會要求無法變更 VM:
  * 停止 hello 可用性設定組中的所有 hello Vm。
    按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。
  * 所有 hello Vm 停止之後，建立 hello hello 中新的 VM 所需的大小。
  * 啟動第一次，hello 新的 VM，然後選取每個 hello 停止 Vm，然後按一下**啟動**。

**原因 2:** hello 叢集沒有釋出資源。

**解決方式 2：**

* 稍後，重試 hello 要求。
* 如果 hello 新的 VM 可以屬於不同的可用性設定嗎
  * 在不同的可用性設定組中建立新的 VM (hello 中相同的區域)。
  * 加入新 VM toohello hello 相同虛擬網路。

## <a name="next-steps"></a>後續步驟
如果您在啟動已停止的 Linux VM，或重新調整 Azure 中現有的 Linux VM 大小時遇到問題，請參閱 [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的 Resource Manager 部署問題進行疑難排解](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

