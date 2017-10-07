---
title: "在 Azure 中發出重新啟動或調整大小的 aaaVM |Microsoft 文件"
description: "針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>針對在 Azure 中重新啟動或調整現有 Linux VM 大小的部署問題進行疑難排解
當您嘗試 toostart 停止 Azure 虛擬機器 (VM)，或將現有的 Azure VM 調整時，hello 常見的錯誤，您會遇到為配置失敗。 當 hello 叢集或區域可能沒有可用的資源或無法支援 hello 要求的 VM 大小，就會產生這個錯誤。

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>收集活動記錄
疑難排解，toostart 收集 hello 活動與 hello 問題相關聯的 tooidentify hello 錯誤的記錄。 下列連結查看 hello 包含 hello 程序的詳細的資訊：

[檢視部署作業](../../azure-resource-manager/resource-manager-deployment-operations.md)

[檢視活動記錄檔 toomanage Azure 資源](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>問題：啟動已停止的 VM 時發生錯誤
您嘗試 toostart 已停止的 VM，但配置失敗。

### <a name="cause"></a>原因
hello 要求 toostart hello 停止 VM 有 toobe 嘗試裝載 hello 雲端服務的 hello 原始叢集中。 不過，hello 叢集沒有可用的空間可用 toofulfill hello 要求。

### <a name="resolution"></a>解決方案
* 停止所有 hello hello 可用性中的 Vm 設定，然後再重新啟動每個 VM。
  
  1. 按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。
  2. 在所有 hello Vm 停止，並選取每個 hello 停止 Vm，然後按一下 開始。
* 稍後，重試 hello 重新啟動要求。

## <a name="issue-error-when-resizing-an-existing-vm"></a>問題：調整現有 VM 的大小時發生錯誤
您嘗試 tooresize 現有 VM，但配置失敗。

### <a name="cause"></a>原因
hello 要求 tooresize hello VM 有 toobe 嘗試 hello 原始叢集在該主機 hello 雲端服務。 不過，不支援 hello 叢集 hello 要求的 VM 大小。

### <a name="resolution"></a>解決方案
* 重試 hello 要求使用較小的 VM 大小。
* 如果 hello hello 的大小會要求無法變更 VM:
  
  1. 停止 hello 可用性設定組中的所有 hello Vm。
     
     * 按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。
  2. 在所有 hello Vm 停止，調整大小所需的 hello VM tooa 較大的大小。
  3. 選取 hello 調整大小的 VM，然後按一下**啟動**，然後啟動每一部 hello 停止 Vm。

## <a name="next-steps"></a>後續步驟
如果您在 Azure 中建立新的 Linux VM 時遇到問題，請參閱[針對在 Azure 中建立新 Linux 虛擬機器的部署問題進行疑難排解](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

