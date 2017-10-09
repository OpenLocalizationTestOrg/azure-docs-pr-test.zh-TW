---
title: "與 Azure 網路監看員 aaaPacket 檢查 |Microsoft 文件"
description: "本文說明如何從 VM 收集 toouse 網路監看員 tooperform 深度封包檢查"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>使用 Azure 網路監看員進行封包檢查

使用網路監看員 hello 封包擷取功能，可以起始，並在您的 Azure Vm 從 hello 網站、 PowerShell、 CLI，並以程式設計方式透過 hello SDK 和 REST API 管理擷取工作階段。 封包擷取可讓您需要藉由提供立即可用的格式中的 hello 資訊的封包層級資料的 tooaddress 案例。 運用 「 免費工具 tooinspect hello 資料，您可以檢查 tooand 傳送您的 Vm 所傳來的通訊，並深入了解您的網路流量。 使用封包擷取資料的一些範例包括︰調查網路或應用程式問題、偵測網路遭誤用及入侵嘗試，或維護法規合規性。 在本文中，我們會示範如何 tooopen 封包擷取檔案所提供網路監看員使用熱門開放原始碼工具。 我們也會提供範例來示範 toocalculate 連線延遲時間識別異常的流量，並檢查網路統計資料的方式。

## <a name="before-you-begin"></a>開始之前

本文逐步引導您完成先前執行的封包擷取上之一些預先設定的情況。 這些案例說明可藉由檢閱封包擷取進行存取的功能。 此案例使用[WireShark](https://www.wireshark.org/) tooinspect hello 封包擷取。

本案例假設您已經在虛擬機器上執行封包擷取。 toolearn toocreate 封包擷取的瀏覽[hello 入口網站擷取管理封包](network-watcher-packet-capture-manage-portal.md)或與其他造訪[使用 REST API 管理封包擷取](network-watcher-packet-capture-manage-rest.md)。

## <a name="scenario"></a>案例

在此案例中，您將會：

* 檢閱封包擷取

## <a name="calculate-network-latency"></a>計算網路延遲

在此案例中，我們會示範如何 tooview hello 發生兩個端點之間的傳輸控制通訊協定 (TCP) 交談的初始來回行程時間 (RTT)。

建立 TCP 連線時，hello 傳送嗨連接中的前三個封包遵循模式一般是指 tooas hello 三向交握。 藉由檢查傳送的此信號交換、 來自 hello 用戶端的初始要求和伺服器 hello 回應 hello 前兩個封包，我們可以在建立此連接時，計算 hello 延遲。 這個延遲是參照的 tooas hello 來回行程時間 (RTT)。 如需 hello TCP 通訊協定和 hello 三向交握的詳細資訊，請參閱 toohello 下列資源。 https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip

### <a name="step-1"></a>步驟 1

啟動 WireShark

### <a name="step-2"></a>步驟 2

負載 hello **.cap**從封包擷取的檔案。 這個檔案位於 hello blob 儲存在我們儲存在本機上的虛擬機器 hello，根據您設定的方式。

### <a name="step-3"></a>步驟 3

tooview hello TCP 交談中的初始來回行程時間 (RTT)，我們將只會查看 hello 前兩個封包參與 hello TCP 交握。 我們將使用 hello 前兩個封包中 hello 三向信號交換期間，也就是 hello [SYN]、 [SYN、 ACK] 封包。 Hello TCP 標頭中設定的旗標的名稱。 hello hello 信號交換期間，[通知] hello 封包來說，在最後一個封包不會用於此案例。 [同步] hello 封包傳送 hello 用戶端。 一旦收到 hello 伺服器 hello [通知] 將封包傳送做為接收從 hello 用戶端 hello SYN 的認可。 我們運用 hello 回應 hello 伺服器需要極少的額外負荷的事實，計算的 hello hello 用戶端所送出 RTT 減去 hello hello 用戶端已收到 hello [SYN、 ACK] 封包的 hello 時間 [SYN] 封包的時間。

使用 WireShark，系統會為我們計算此值。

toomore hello TCP 三向交握中輕鬆地檢視 hello 前兩個封包中，我們將利用 hello 篩選 WireShark 所提供的功能。

在 WireShark tooapply hello 篩選器展開 hello 「 傳輸控制通訊協定 」 區段的 [同步處理] 中的封包將擷取，並檢查設定 hello TCP 標頭中的 hello 旗標。

因為我們會查看 toofilter 上所有 [SYN] 和 [SYN、 ACK] 下的旗標的封包 cofirm hello Syn 位元會設 too1，，然後以滑鼠右鍵按一下 hello Syn 元上的-> 套用篩選]-> [選取。

![圖 7][7]

### <a name="step-4"></a>步驟 4

既然您已經篩選 hello 視窗 tooonly，請參閱封包與 hello [SYN] 設定位元，您可以輕鬆地選取您感興趣 tooview 交談 hello 初始 RTT。 簡單的方式 tooview hello RTT WireShark 中只需按一下 hello 下拉式清單中標示為 「 SEQ/通知 」 分析。 然後，您會看到 RTT 顯示的 hello。 在此情況下，hello RTT 已 0.0022114 秒或 2.211 ms。

![圖 8][8]

## <a name="unwanted-protocols"></a>不必要的通訊協定

您可以在已部署於 Azure 中的虛擬機器執行個體上執行許多應用程式。 這些應用程式的許多通訊透過 hello 網路，可能是不明確的權限。 使用封包擷取 toostore 網路通訊，我們可以研究如何應用程式會提到 hello 網路上尋找有任何問題。

在此範例中，我們檢視先前執行之不必要通訊協定的封包擷取，其可能表示來自您電腦上執行之應用程式的未授權通訊。

### <a name="step-1"></a>步驟 1

使用 hello 在 hello 中前一個案例中，按一下相同的擷取**統計資料** > **通訊協定階層**

![通訊協定階層功能表][2]

hello 通訊協定階層視窗隨即出現。 此檢視會提供一份 hello 擷取工作階段和傳輸及使用 hello 通訊協定所接收的封包的 hello 數目期間使用的所有 hello 通訊協定。 此檢視可用於找出您的虛擬機器或網路上不需要的網路流量。

![開啟的通訊協定階層][3]

您可以看到 hello 下列螢幕擷取畫面中，沒有使用 hello BitTorrent 通訊協定，可用於對等 toopeer 檔案共用的流量。 身為系統管理員不想 toosee BitTorrent 流量這個特定的虛擬機器上。 現在您知道這個流量，您可以移除 hello 對等 toopeer 軟體安裝在此虛擬機器或區塊 hello 流量使用網路安全性群組或防火牆。 此外，您可以選擇 toorun 封包擷取排程，讓您可以 hello 通訊協定使用定期檢閱在您的虛擬機器上。 如需 tooautomate 網路瀏覽 azure 中的工作範例[監視網路資源，使用 azure 自動化](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>尋找最上層目的地和連接埠

了解 hello 類型的流量，hello 端點，並透過進行通訊的 hello 連接埠，請務必監視或疑難排解應用程式和網路上的資源時。 使用上述的封包擷取檔案，我們可以快速地了解 hello 最前面的目的地我們 VM 通訊的與 hello 正在使用的連接埠。

### <a name="step-1"></a>步驟 1

使用 hello 在 hello 中前一個案例中，按一下相同的擷取**統計資料** > **IPv4 統計資料** > **目的地和連接埠**

![封包擷取視窗][4]

### <a name="step-2"></a>步驟 2

當我們查看 hello 結果列凸顯出來時，發生多個連接上連接埠 111。 hello 最常使用的連接埠是 3389，這是遠端桌面，而剩餘的 hello RPC 動態連接埠。

雖然此流量可能表示執行任何動作，它是連接埠已用於多個連接，並且為未知的 toohello 系統管理員。

![圖 5][5]

### <a name="step-3"></a>步驟 3

既然我們已經決定外的地方我們可以篩選根據 hello 的連接埠我們擷取的連接埠。

會在此案例中的 hello 篩選：

```
tcp.port == 111
```

我們在 hello 篩選 文字方塊中輸入 hello 上述的篩選條件文字，並按 enter 鍵。

![圖 6][6]

從 hello 結果中，我們可以看到所有的 hello 流量來自本機的虛擬機器上 hello 相同子網路。 如果我們仍不了解此流量發生的原因，我們可以進一步檢查 hello 封包 toodetermine 為什麼它呼叫這些連接埠 111。 這項資訊可以採取 hello 適當的動作。

## <a name="next-steps"></a>後續步驟

深入了解造訪 hello 網路監看員的其他診斷功能[Azure 網路監視概觀](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













