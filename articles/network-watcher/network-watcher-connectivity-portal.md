---
title: "與 Azure 網路監看員-Azure 入口網站的 aaaCheck 連線 |Microsoft 文件"
description: "此頁面說明 toouse 連線如何與網路監看員使用 hello Azure 入口網站檢查"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>請檢查與 Azure 網路監看員使用 hello Azure 入口網站的連線

> [!div class="op_single_selector"]
> - [入口網站](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

了解可以如何建立 toouse 連線 tooverify 如果從虛擬機器 tooa 指定端點的直接 TCP 連接。

## <a name="before-you-begin"></a>開始之前

本文假設您擁有 hello 下列資源：

* 執行個體要 toocheck 連線的網路監看員 hello 區域中。

* 虛擬機器與 toocheck 連線。

> [!IMPORTANT]
> 連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。 Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>請檢查連線 tooa 虛擬機器

這個範例會檢查透過連接埠 80 連線 tooa 目的地虛擬機器。

瀏覽 tooyour 網路監看員，並按一下**連線能力檢查 （預覽）**。 從虛擬機器 toocheck 連線選取 hello。 在 hello**目的地**區段中，選擇**選取虛擬機器**，並選擇 hello 正確的虛擬機器與連接埠 tootest。

一旦您按一下**檢查**，會檢查 hello hello hello 指定的連接埠上的虛擬機器之間的連線。 在 hello 範例 hello 目的地 VM 是無法連線，躍點的清單會顯示。

![查看虛擬機器的連線能力結果][1]

## <a name="check-remote-endpoint-connectivity"></a>檢查遠端端點的連線能力

toocheck hello 連線和延遲 tooa 遠端端點，請選擇 hello**手動指定**hello 中的選項按鈕**目的地**區段中，輸入 hello url 和 hello 連接埠並按一下**檢查**.  這會用於網站與儲存體端點之類的遠端端點。

![查看網站的連線能力結果][2]

## <a name="next-steps"></a>後續步驟

了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)

造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
