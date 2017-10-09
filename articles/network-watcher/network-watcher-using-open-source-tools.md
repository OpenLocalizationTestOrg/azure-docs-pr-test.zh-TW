---
title: "Azure 網路監看員與開放原始碼工具 aaaVisualize 網路流量模式 |Microsoft 文件"
description: "此頁面描述 toouse 網路監看員封包如何擷取與 Capanalysis toovisualize 流量模式 tooand 從您的 Vm。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>以視覺化方式檢視您使用開放原始碼工具的 Vm 所傳來的網路流量模式 tooand

封包擷取包含 tooperform 網路鑑證和深度封包檢查可讓您的網路資料。 有許多開啟原始碼工具，您可以使用 tooanalyze 封包擷取 toogain insights 解您的網路。 例如 CapAnalysis，一個開放原始碼封包擷取視覺效果工具。 視覺化封包擷取資料是 tooquickly 衍生的模式和網路中的異常狀況的洞察能力的重要方法。 視覺效果也可讓您輕鬆分享這種深入解析。

Azure 的網路監看員會提供您在網路上 hello 能力 toocapture 此寶貴的資料，可讓您 tooperform 封包擷取。 在本文中，我們會提供 toovisualize 並取得深入資訊從封包擷取 CapAnalysis 使用網路監看員的逐步解說。

## <a name="scenario"></a>案例

您已部署的簡單 web 應用程式上的 VM 中 Azure 想 toouse 開放原始碼工具 toovisualize 其網路流量 tooquickly 識別流量模式和可能的異常狀況。 您可以利用網路監看員取得網路環境的封包擷取，並直接儲存在儲存體帳戶中。 CapAnalysis 可以內嵌 hello 封包擷取直接從 hello 儲存體 blob，並以視覺化方式檢視其內容。

![案例][1]

## <a name="steps"></a>步驟

### <a name="install-capanalysis"></a>安裝 CapAnalysis

tooinstall CapAnalysis 虛擬機器上的，您可以參考 toohello 官方指示這裡 https://www.capanalysis.net/ca/how-to-install-capanalysis。
順序 CapAnalysis 遠端存取，我們需要您的 VM 上 tooopen 連接埠 9877 藉由新增新的連入的安全性規則。 如需建立網路安全性群組中的規則相關資訊，請參閱太[建立現有 NSG 中的規則](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg)。 已成功新增 hello 規則，您應該能夠 tooaccess CapAnalysis 從`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>使用 Azure 網路監看員 toostart 封包擷取工作階段

網路監看員，可讓您 toocapture 封包 tootrack 流量進出虛擬機器。 您可以使用參照 toohello 指示[網路監看員擷取管理封包](network-watcher-packet-capture-manage-portal.md)toostart 封包擷取工作階段。 此封包擷取可以儲存在儲存體 blob toobe CapAnalysis 所存取。

### <a name="upload-a-packet-capture-toocapanalysis"></a>上傳封包擷取 tooCapAnalysis
您可以直接上傳所網路監看員使用 hello 「 匯入從 URL 索引標籤並提供連結 toohello 儲存體 blob 儲存 hello 封包擷取封包擷取。

當提供連結 tooCapAnalysis，請確定 tooappend SAS 權杖 toohello 儲存體 blob URL。  toodo，導覽 tooShared hello 儲存體帳戶的存取簽章、 指定 hello 允許權限，然後按 hello 產生 SAS 按鈕 toocreate 語彙基元。 然後，您可以附加此 SAS 權杖 toohello 封包擷取儲存體 blob URL。

hello 產生 URL 看起來會像這樣： http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>分析封包擷取

CapAnalysis 提供各種選項 toovisualize 封包擷取，每個提供的分析，以不同的觀點。 這些視覺化摘要可讓您了解網路流量趨勢，並快速找出任何不尋常的活動。 這些功能的一些顯示 hello 清單後面：

1. 流程資料表

    此資料表提供 hello hello 封包資料流的清單、 hello 與 hello 流程相關聯的時間戳記和 hello 與 hello 流程，以及來源和目的地 IP 相關聯的各種通訊協定。

    ![capanalysis 流程頁面][5]

1. 通訊協定概觀

    此窗格可讓您 tooquickly 會查看一段 hello 網路流量的 hello 分佈各種通訊協定和地理位置。

    ![capanalysis 通訊協定概觀][6]

1. 統計資料

    此窗格可讓您 tooview 網路流量統計資料-位元組傳送並接收來自來源和目的地的 hello 來源和目的地 Ip 時，每個流量的 Ip 通訊協定用於各種流程和流程 hello 持續時間。

    ![capanalysis 統計資料][7]

1. Geomap

    這個窗格您提供的網路流量，地圖檢視使用色彩調整 toohello 磁碟區中每個國家/地區的流量。 您可以選取反白顯示國家/地區 tooview 其他流程統計資料，例如 hello 比例的資料傳送和接收從該國家/地區中的 Ip。

    ![geomap][8]

1. 篩選器

    CapAnalysis 提供一組可快速分析特定封包的篩選器。 例如，您可以選擇 toofilter hello 資料由該子集的傳輸通訊協定 toogain 特定 insights。

    ![filters][11]

    請瀏覽[https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn 深入了解所有 CapAnalysis 功能。

## <a name="conclusion"></a>結論

監看員網路封包擷取功能可讓您 toocapture hello 資料所需的 tooperform 網路鑑識調查，並深入了解您的網路流量。 在此案例中，我們示範如何使用開放原始碼視覺效果工具，輕鬆地整合來自網路監看員的封包擷取。 使用開放原始碼工具，例如 CapAnalysis toovisualize 封包擷取，您可以執行深度封包檢查，並快速識別在您的網路流量的趨勢。

## <a name="next-steps"></a>後續步驟

toolearn 進一步了解 NSG 流程記錄檔，請瀏覽[NSG 流程記錄](network-watcher-nsg-flow-logging-overview.md)

了解 toovisualize NSG 流程記錄的方式有了 Power BI 瀏覽[視覺化 NSG 流動 Power BI 的記錄檔](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
