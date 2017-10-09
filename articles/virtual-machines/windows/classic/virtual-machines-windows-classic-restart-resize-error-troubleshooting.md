---
title: "重新啟動或調整大小問題 aaaVM |Microsoft 文件"
description: "針對在 Azure 中重新啟動或調整現有 Windows 虛擬機器大小的傳統部署問題進行疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a>針對在 Azure 中重新啟動或調整現有 Windows 虛擬機器大小的傳統部署問題進行疑難排解
> [!div class="op_single_selector"]
> * [傳統](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [資源管理員](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

當您嘗試 toostart 停止 Azure 虛擬機器 (VM)，或將現有的 Azure VM 調整時，hello 常見的錯誤，您會遇到為配置失敗。 當 hello 叢集或區域可能沒有可用的資源或無法支援 hello 要求的 VM 大小，就會產生這個錯誤。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。  本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>收集稽核記錄檔
troubleshooting，toostart 收集 hello 稽核記錄與 hello 問題相關聯的 tooidentify hello 錯誤。

在 hello Azure 入口網站，按一下 **瀏覽** > **虛擬機器** > *Windows 虛擬機器* >  **設定** > **稽核記錄檔**。

## <a name="issue-error-when-starting-a-stopped-vm"></a>問題：啟動已停止的 VM 時發生錯誤
您嘗試 toostart 已停止的 VM，但配置失敗。

### <a name="cause"></a>原因
hello 要求 toostart hello 停止 VM 有 toobe 嘗試裝載 hello 雲端服務的 hello 原始叢集中。 不過，hello 叢集沒有可用的空間可用 toofulfill hello 要求。

### <a name="resolution"></a>解決方案
* 建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯，但不是和同質群組。
* 刪除 hello 停止 VM。
* 使用 hello 磁碟重新建立 hello 新的雲端服務中的 hello VM。
* 啟動 hello 重新建立 VM。

如果嘗試 toocreate 新的雲端服務時，您會收到錯誤，請稍後重試，或變更 hello 雲端服務的 hello 地區。

> [!IMPORTANT]
> hello 新的雲端服務必須在新的名稱和 VIP，因此您需要 toochange 該資訊的所有使用該資訊 hello 現有雲端服務的 hello 相依性。
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>問題：調整現有 VM 的大小時發生錯誤
您嘗試 tooresize 現有 VM，但配置失敗。

### <a name="cause"></a>原因
hello 要求 tooresize hello VM 有 toobe 嘗試 hello 原始叢集在該主機 hello 雲端服務。 不過，不支援 hello 叢集 hello 要求的 VM 大小。

### <a name="resolution"></a>解決方案
減少 hello 要求的 VM 大小和重試 hello 調整大小的要求。

* 按一下 [全部瀏覽]  >  [虛擬機器 (傳統)]  >  *您的虛擬機器*  >  [設定]  >  [大小]。 如需詳細步驟，請參閱[調整 hello 虛擬機器大小](https://msdn.microsoft.com/library/dn168976.aspx)。

如果不可能 tooreduce hello VM 大小，請遵循下列步驟：

* 建立新的雲端服務中，確定它不連結 tooan 同質群組不相關聯的虛擬網路，且連結的 tooan 同質群組。
* 在其中建立新的、較大的 VM。

您可以將合併所有 Vm 都在 hello 相同雲端服務。 如果您現有的雲端服務與區域為基礎的虛擬網路相關聯，您可以連接 hello 新雲端服務 toohello 現有的虛擬網路。

如果找不到與區域為基礎的虛擬網路相關聯的 hello 現有雲端服務，您擁有 toodelete hello Vm hello 現有雲端服務中的，並且在 hello 新的雲端服務從其磁碟重新建立它們。 不過，它是重要 tooremember，hello 新的雲端服務會有新名稱和 VIP，因此您需要 tooupdate 供所有目前使用這項資訊為 hello 現有雲端服務的 hello 相依性。

## <a name="next-steps"></a>後續步驟
如果您在 Azure 中建立 Windows VM 時遇到問題，請參閱[針對在 Azure 中建立 Windows 虛擬機器的部署問題進行疑難排解](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

