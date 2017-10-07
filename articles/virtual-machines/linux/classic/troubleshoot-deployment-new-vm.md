---
title: "aaaTroubleshoot Linux VM 部署傳統 |Microsoft 文件"
description: "針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: a642bfd9a543cd6d2104b03fe04193d9352ccae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如需這篇文章 hello 資源管理員版本，請參閱[這裡](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>收集稽核記錄檔
troubleshooting，toostart 收集 hello 稽核記錄與 hello 問題相關聯的 tooidentify hello 錯誤。

在 hello Azure 入口網站，按一下 **瀏覽** > **虛擬機器** > *Windows 虛擬機器* >  **設定** > **稽核記錄檔**。

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:**如果 hello 作業系統一般化，Linux 和它已上傳及/或所擷取的 hello 一般化設定，則不會有任何錯誤。 同樣地，如果 hello OS Linux 特製化，且它已上傳及/或所擷取的 hello 特製化的設定，則不會有任何錯誤。

**上傳錯誤：**

**N<sup>1</sup>:**如果 hello OS Linux 一般化，而且會當做上傳的特製化，就會發生佈建的逾時錯誤因為 hello VM 停駐在 hello 佈建階段。

**N<sup>2</sup>:**如果 hello OS Linux 特製化，和上傳為一般化，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。

**解決方案：**

tooresolve 這兩個這些錯誤上, 傳 hello 原始 VHD，內部使用，與 hello 相同設定，與 hello OS （一般化/特製化）。 tooupload 為一般化，請記住 toorun-取消佈建第一次。 請參閱[建立及上傳虛擬硬碟的 Contains hello Linux Operating System](create-upload-vhd.md)如需詳細資訊。

**擷取錯誤：**

**N<sup>3</sup>:**如果 hello OS Linux 一般化，而且都擷取成特製化，就會發生佈建的逾時錯誤因為 hello 原始 VM 就無法使用為它標示為一般化。

**N<sup>4</sup>:**是否 hello OS Linux 特製化，然後為一般化擷取，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。 此外，hello 原始 VM 並未使用因為它已標示為特製化。

**解決方案：**

tooresolve 這兩個這些錯誤，從 hello 入口網站中，刪除 hello 目前映像和[收復 hello 從目前的 Vhd](capture-image.md)與 hello 相同設定，與 hello OS （一般化/特製化）。

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>問題︰自訂/資源庫/Marketplace 映像；配置失敗
會發生這個錯誤情況時傳送 hello 新的 VM 要求 tooa 叢集可能沒有可用的空間 tooaccommodate hello 要求，或無法支援所要求的 hello VM 大小。 不可能 toomix 不同序列 hello 中 Vm 的相同雲端服務。 因此如果您想 toocreate 比您的雲端服務可支援不同大小的新的 VM，hello 計算要求將會失敗。

您可以根據 hello hello 雲端服務的條件約束使用 toocreate hello 新的 VM，您可能會遇到的其中兩個情況造成錯誤。

**原因 1:** hello 雲端服務是已釘選的 tooa 特定叢集，或者它是連結的 tooan 同質群組，並因此釘選的 tooa 特定群集的設計。 因此在該同質群組中，要求新的計算資源會嘗試在 hello 相同叢集 hello 現有資源的裝載位置。 不過，hello 相同叢集可能不支援 hello 要求的 VM 大小，或有可用空間不足，造成配置錯誤。 透過新的雲端服務或透過現有的雲端服務的 hello 新資源建立是否為 true。

**解決方式 1：**

* 建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯。
* Hello 新的雲端服務中建立新的 VM。
  如果嘗試 toocreate 新的雲端服務時，您會收到錯誤，稍後再試一次，或變更 hello 雲端服務的 hello 地區。

> [!IMPORTANT]
> 如果您嘗試 toocreate 中現有的雲端服務的新 VM，但無法，而且產生 toocreate 新的雲端服務，新的 vm，您可以選擇 tooconsolidate 您所有的 Vm 中 hello 相同雲端服務。 因此 toodo 刪除 hello 現有雲端服務中的 hello Vm，然後重新加以擷取其 hello 新的雲端服務中的磁碟。 不過，它是重要 tooremember，hello 新的雲端服務會有新名稱和 VIP，因此您需要 tooupdate 供所有目前使用這項資訊為 hello 現有雲端服務的 hello 相依性。
> 
> 

**原因 2:** hello 雲端服務可以是連結的 tooan 同質群組，所以它是已釘選的 tooa 所設計的特定叢集的虛擬網路相關聯。 相同叢集 hello 現有資源的裝載位置的 hello 因此會嘗試在該同質群組中的所有新計算資源要求。 不過，hello 相同叢集可能不支援 hello 要求的 VM 大小，或有可用空間不足，造成配置錯誤。 透過新的雲端服務或透過現有的雲端服務的 hello 新資源建立是否為 true。

**解決方式 2：**

* 建立新的區域虛擬網路。
* 建立 hello hello 新的虛擬網路中的新 VM。
* [您現有的虛擬網路連線](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)toohello 新的虛擬網路。 深入了解 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)。 或者，您可以[將同質群組為基礎的虛擬網路 tooa 地區虛擬網路移轉](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)，然後再建立 hello 新的 VM。

## <a name="next-steps"></a>後續步驟
如果您在啟動已停止的 Linux VM，或重新調整 Azure 中現有 Linux VM 的大小時遇到問題，請參閱 [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的傳統部署問題進行疑難排解](restart-resize-error-troubleshooting.md)。

