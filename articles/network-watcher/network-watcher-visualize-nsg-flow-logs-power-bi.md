---
title: "使用 Power BI 記錄 aaaVisualizing Azure 網路安全性小組流程 |Microsoft 文件"
description: "此頁面描述 toovisualize NSG 流程記錄使用 Power BI 的方式。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>使用 Power BI 將網路安全性群組流程記錄視覺化

網路安全性小組流程記錄檔可讓您 tooview 資訊 ingress 和 egress IP 流量的網路安全性群組。 這些流程記錄檔會顯示輸出，以每個規則為基礎的輸入的流量，hello NIC hello 流程套，hello 流程 (來源/目的地 IP，來源/目的地連接埠通訊協定)，和如果允許或拒絕 hello 流量的 5 個 tuple 資訊。

可能很難 toogain 深入了解藉由手動搜尋 hello 記錄檔記錄資料的資料流程。 在本文中，我們會提供方案 toovisualize 您最新流程記錄，並了解您的網路上的流量。

## <a name="scenario"></a>案例

在 hello 遵照案例，我們連接 Power BI 桌面 toohello 儲存體帳戶，我們已經設定成 hello 接收 NSG 流程記錄資料。 我們連接 tooour 儲存體帳戶之後，Power BI 會下載並剖析 hello 記錄 tooprovide hello 流量記錄的網路安全性群組的視覺表示法。

使用中，您可以檢查 hello 範本所提供的 hello 視覺效果：

* 熱門 IP
* 依方向和規則決策的時間序列資料流程
* 依網路介面 MAC 位址的流程
* 依 NSG 和規則的流程
* 依目的地連接埠的流程

提供 hello 範本是可編輯，因此您可以修改它 tooadd 新資料，視覺效果，或編輯查詢 toosuit 您的需求。

## <a name="setup"></a>設定

開始之前，您必須在帳戶中的一或多個網路安全性群組上，啟用網路安全性群組流程記錄。 如需有關啟用網路安全性指示傳送記錄檔，請參閱下列文章 toohello:[網路安全性群組的簡介 tooflow 記錄](network-watcher-nsg-flow-logging-overview.md)。

您也必須 hello Power BI Desktop 用戶端安裝在您的電腦，以及足夠可用空間對機器 toodownload 和負載 hello 記錄資料位於儲存體帳戶。

![Visio 圖表][1]

### <a name="steps"></a>步驟

1. 下載並開啟下列 hello Power BI Desktop 的應用程式中的 Power BI 範本的 hello[網路監看員 PowerBI 流程記錄範本](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. 輸入所需的 hello 查詢參數
    1. **StorageAccountName** – hello 包含 hello NSG 流程記錄，您的儲存體帳戶指定 toohello 名稱會喜歡 tooload 和視覺化。
    1. **NumberOfLogFiles** – 指定記錄檔，您會想 toodownload，並在 Power BI 中視覺化的 hello 數目。 例如，如果指定 50，則 hello 50 個最新的記錄檔。 我們有 2 Nsg ff 啟用並設定 toosend NSG 流量記錄 toothis 帳戶，然後 hello 過去 25 小時的記錄檔可以檢視。

    ![power BI 主畫面][2]

1. 輸入 hello 儲存體帳戶存取金鑰。 您可以藉由瀏覽 tooyour hello Azure 入口網站與選取的儲存體帳戶中找到有效的存取金鑰**便捷鍵**hello 設定 功能表中。 按一下 [連線]，然後套用變更。

    ![access keys][3]

    ![存取金鑰 2][4]

4.  您記錄已下載並剖析，現在，您可以利用 hello 預先建立視覺效果。

## <a name="understanding-hello-visuals"></a>了解 hello 視覺效果

提供在 hello 範本是一組視覺效果，協助意義的 hello NSG 流程記錄資料。 hello 下列影像顯示哪些 hello 儀表板看起來像當填入資料的範例。 接下來，我們更詳細地探討每個視覺效果 

![powerbi][5]
 
hello 頂端說話者包括代表視覺顯示 hello Ip 已起始的一段指定期間的 hello hello 大多數的連線。 hello hello 方塊大小對應 toohello 相對連接數目。 

![toptalkers][6]

hello 下列時間序列圖形顯示 hello hello 段流程數目。 hello 文字方向，區隔 hello 上方圖表和較低的 hello hello 決定 （允許或拒絕） 區隔。 此視覺效果可讓您檢查一段時間的流量趨勢，並找出流量或流量分割中的任何異常暴增或遽減情況。

![flowsoverperiod][7]

hello 下圖顯示 hello 流量每個網路介面，hello 左上區隔文字方向與 hello 較低的區隔所做的決策。 使用這項資訊，您可以取得深入了解哪些 Vm 通訊 hello 大部分相對 tooothers，而且如果流量 tooa 特定 VM 是允許或拒絕。

![flowspernic][8]

hello 遵循甜甜圈滾輪圖表會顯示由目的地連接埠的流量的細目。 利用此資訊，您可以檢視最常用的 hello 目的地連接埠中指定的 hello 使用期限。

![環圈][9]

hello 下列橫條圖顯示 hello NSG 及規則的流量。 利用此資訊，您可以看到 hello Nsg 負責 hello 大部分的流量，以及 hello 分解的流量上 NSG 規則。

![barchart][10]
 
hello 下列參考用的圖表顯示 hello Nsg hello 記錄檔中、 資訊 hello 流程擷取透過 hello 期間 hello 的日期和 hello 擷取最早的記錄數目。 這項資訊可讓您了解哪些 Nsg 會記錄和 hello 流程的日期範圍。

![infochart1][11]

![infochart2][12]

此範本包括 hello 下列交叉分析篩選器 tooallow 您 tooview 您最感興趣只有 hello 資料。 您可以依資源群組、NSG 和規則來篩選。 您也可以篩選 5-tuple 資訊、 決策、 hello hello 記錄寫入時和時間。

![交叉分析篩選器][13]

## <a name="conclusion"></a>結論

我們也示範了在此案例中，藉由使用網路安全性群組流網路監看員和 Power BI 所提供的記錄檔，我們可以 toovisualize 而了解 hello 流量。 使用提供的 hello 範本時，Power BI 直接從儲存體下載 hello 記錄檔，並在本機處理它們。 所花費時間 tooload hello 範本而有所不同 hello 數目所要求的檔案和下載檔案的大小總計。

您可用 toocustomize 此範本符合您的需求。 Power BI 和網路安全性群組流程記錄互相搭配有許多做法。 

## <a name="notes"></a>注意事項

* 記錄依預設儲存於 `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * 如果有另一個目錄中的其他資料在 hello 查詢 toopull，必須修改處理程序 hello 資料。

* 提供的 hello 範本不是建議使用具有 1 GB 以上的記錄檔。

* 如果您有大量的記錄，我們建議您探尋使用其他資料存放區的解決方案，例如 Data Lake 或 SQL Server。

## <a name="next-steps"></a>後續步驟

了解 toovisualize NSG 流程記錄的方式以 hello Elastick 堆疊造訪[視覺化網路流量模式 tooand 從您的 Vm 使用開放原始碼工具](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
