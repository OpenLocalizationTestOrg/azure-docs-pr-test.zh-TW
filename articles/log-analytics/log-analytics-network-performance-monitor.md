---
title: "aaaNetwork 中 Azure 記錄分析的效能監視器解決方案 |Microsoft 文件"
description: "網路效能監視器中 Azure Log Analytics 可協助您監視您網路中靠近即時單次 toodetect hello 效能，並找出網路效能瓶頸。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Log Analytics 中的網路效能監視器解決方案

![網路效能監控符號](./media/log-analytics-network-performance-monitor/npm-symbol.png)

本文件說明如何 tooset 向上和向下使用 hello 網路效能監視器方案中記錄分析，可協助您監視您網路中靠近即時單次 toodetect hello 效能，並找出網路效能瓶頸。 以 hello 網路效能監視器方案，您可以監視 hello 中斷和子網路或伺服器的兩個網路之間的延遲。 網路效能監視器會偵測網路問題，例如流量 blackholing、 路由錯誤，以及傳統網路監視的方法不能 toodetect 的問題。 網路效能監視器會產生警示，並違反網路連結的臨界值時發生通知。 這些閾值可以自動學習 hello 系統或您可以設定它們 toouse 自訂警示規則。 網路效能監視器可確保及時偵測的網路效能問題和當地語系化 hello 問題 tooa 特定網路區段或裝置 hello 來源。

您可以偵測到與 hello 方案儀表板會顯示摘要的資訊，包括最近使用的網路健全狀況事件、 狀況不良的網路連結和子網路連結遇到高的封包中斷和延遲的網路相關的網路問題。 您可以向下鑽研功能網路連結 tooview hello 目前健全狀況狀態的子網路連結，以及節點對節點連結。 您也可以檢視 hello 的中斷和延遲在 hello 網路、 子網路及節點對節點層級的歷史趨勢。 您可以藉由檢視封包遺失和延遲的歷史趨勢圖表來偵測暫時性網路問題，並找出拓撲圖上的網路瓶頸。 hello 互動式拓撲圖表可讓您 toovisualize hello 躍點的躍點的網路路由，並判斷 hello hello 問題來源。 像任何其他方案，您可以使用各種分析記錄搜尋需求 toocreate 自訂報告根據網路效能監視器所收集的 hello 資料。

hello 解決方案使用綜合交易當做主要機制 toodetect 網路錯誤。 因此，您可以使用它，而不需考慮特定網路裝置的廠商或模型。 其適用於內部部署、雲端 (IaaS) 和混合式環境。 hello 方案會自動探索 hello 網路拓撲和網路中的各種路由。

一般網路監視產品著重在監視 hello 網路裝置 （路由器、 交換器等等） 的健全狀況，但不是提供深入了解 hello 實際品質之間沒有網路效能監視器中的兩個點的網路連線。

### <a name="using-hello-solution-standalone"></a>使用 hello 方案獨立
如果您想 toomonitor hello 品質重要的工作負載之間的網路連線時，網路、 資料中心或站台，然後您可以使用 hello 網路效能監視器方案本身 toomonitor 之間的連線健全狀況：

* 使用公用或私人網路連接的多個資料中心或公司網站
* 執行企業營運應用程式的重要工作負載
* 公用雲端服務，例如 Microsoft Azure 或 Amazon Web Services (AWS) 和內部部署網路，如果您有 IaaS (VM) 使用，而且您有閘道設定 tooallow 在內部部署網路和雲端網路之間的通訊
* 當您使用 ExpressRoute 時的 Azure 與內部部署網路

### <a name="using-hello-solution-with-other-networking-tools"></a>搭配其他網路功能的工具使用 hello 方案
如果您想 toomonitor 企業營運應用程式，您可以使用網路效能監視器方案 hello 附屬方案 tooother 網路工具。 較慢的網路可能會導致 tooslow 應用程式和網路效能監視器可協助您調查應用程式基礎網路問題所造成的效能問題。 Hello 方案不需要任何存取 toonetwork 裝置，因為 hello 應用程式系統管理員不需要 toorely hello 網路如何影響應用程式的相關網路小組 tooprovide 資訊。

此外，如果您已投資在其他網路監視工具，然後 hello 方案可以補充這些工具因為大部分傳統網路監視解決方案不提供端對端網路效能計量，例如中斷和延遲的深入剖析。  hello 網路效能監視器解決方案可協助填滿，兩者的差異。

## <a name="installing-and-configuring-agents-for-hello-solution"></a>安裝和設定 hello 解決方案的代理程式
使用 hello 基本程序 tooinstall 代理程式在[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)和[Operations Manager 連線 tooLog 分析](log-analytics-om-agents.md)。

> [!NOTE]
> 您將需要足夠的資料 toodiscover tooinstall 至少 2 toohave 順序中的代理程式，並監視您的網路資源。 否則，hello 方案會保留在 「 設定 」 狀態，直到您安裝及設定其他代理程式。
>
>

### <a name="where-tooinstall-hello-agents"></a>其中 tooinstall hello 代理程式
安裝代理程式之前，請考慮網路拓撲 hello 和 hello 的哪些部分網路您想要 toomonitor。 我們建議您安裝您想 toomonitor 每個子網路的多個代理程式。 換句話說，針對您想 toomonitor 每個子網路，選擇兩個或多個伺服器或 Vm 並且 hello 代理程式上安裝它們。

如果您不確定 hello 網路拓撲，請與您想要 toomonitor hello 網路效能的任務工作負載的伺服器上安裝 hello 代理程式。 例如，您可以 Web 伺服器和執行 SQL Server 的伺服器之間的網路連線的 tookeep 追蹤。 在此範例中，您會在兩部伺服器上安裝代理程式。

代理程式監視主機本身未 hello 主機之間的網路連線 （連結）。 因此，toomonitor 網路連結，您必須在該連結的兩個端點上安裝代理程式。

### <a name="configure-agents"></a>設定代理程式

如果您想要針對綜合交易的 toouse hello ICMP 通訊協定，您需要下列防火牆規則，就能夠可靠地使用 ICMP tooenable hello:

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


如果您想 toouse hello TCP 通訊協定您會需要為這些代理程式可通訊的電腦 tooensure tooopen 防火牆連接埠。 您需要 toodownload，然後執行 hello [EnableRules.ps1 PowerShell 指令碼](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634)不使用任何參數，以系統管理權限的 PowerShell 視窗中。

hello 指令碼會建立 hello 網路效能監視器所需的登錄機碼，它會建立 Windows 防火牆規則 tooallow 代理程式 toocreate TCP 連線彼此。 hello hello 指令碼所建立的登錄機碼也會指定是否 toolog hello 偵錯記錄檔和 hello hello 記錄檔案的路徑。 它也會定義用於通訊的 hello 代理程式 TCP 通訊埠。 這些索引鍵的 hello 值會自動設定 hello 指令碼，所以您不應手動變更這些金鑰。

8084 hello 連接埠預設開啟的。 您可以藉由提供 hello 參數使用自訂連接埠`portNumber`toohello 指令碼。 不過，hello 相同的連接埠應 hello 的所有電腦上執行 hello 指令碼的位置。

> [!NOTE]
> hello EnableRules.ps1 指令碼只能在 hello hello 指令碼執行所在的電腦上設定 Windows 防火牆規則。 如果您有網路防火牆，您應該要確定它可讓目的地為 hello TCP 連接埠正在使用網路效能監視器的流量。
>
>

## <a name="configuring-hello-solution"></a>設定 hello 解決方案
使用下列資訊 tooinstall hello 並設定 hello 方案。

1. hello 網路效能監視器方案取得資料，從執行 Windows Server 2008 SP 1 或更新版本的電腦或 Windows 7 SP1 或更新版本中，這是 hello 相同 hello Microsoft Monitoring Agent (MMA) 的需求。 NPM 代理程式也可以在 Windows 桌面/用戶端作業系統 (Windows 10、Windows 8.1、Windows 8 和 Windows 7) 上執行。
    >[!NOTE]
    >Windows server 作業系統的 hello 代理程式支援 TCP 和 ICMP 視為綜合交易的 hello 通訊協定。 不過，Windows 用戶端作業系統的 hello 代理程式只會支援 ICMP 做為綜合交易的 hello 通訊協定。

2. 新增 hello 網路效能監視器方案 tooyour 從工作區[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。  
   ![網路效能監視器符號](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. 在 hello OMS 入口網站，您會看到標題為新的圖格**網路效能監視器**hello 訊息*解決方案需要其他設定*。 您將需要 tooconfigure hello 方案 tooadd 型網路的子網路，而且探索到的代理程式的節點。 按一下**網路效能監視器**toostart 設定 hello 預設網路。  
   ![方案需要額外設定](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>使用預設網路設定 hello 方案
在 hello 組態 頁面中，您會看到單一網路，名為**預設**。 您尚未定義任何網路，當所有 hello 自動探索子網路會都放置在 hello 預設網路。

每當您建立網路時，您會加入子網路 tooit 和子網路從 hello 預設網路中移除。 如果您刪除網路時，其所有子網路會自動傳回 toohello 預設網路。

換句話說，hello 預設網路是所有 hello 子網路不包含任何使用者定義的網路中的 hello 容器。 您無法編輯或刪除 hello 預設網路。 一定會保持在 hello 系統中。 不果，您可以視需要建立任意數量的網路。

在大部分情況下，組織中的 hello 子網路會排列在一個以上的網路和您應該建立一個或多個網路 toologically 群組您的子網路。

### <a name="create-new-networks"></a>建立新網路
網路效能監視器中的網路是子網路的容器。 您可以使用任何名稱，並新增子網路 toohello 網路建立網路。 例如，您可以建立名為的網路*Building1* ，然後新增子網路，或者您可以建立網路，名為*DMZ*然後加入所有屬於 toodemilitarized 區域 toothis 網路的子網路。

#### <a name="toocreate-a-new-network"></a>toocreate 新網路
1. 按一下**新增網路**，然後輸入 hello 網路名稱和描述。
2. 選取一或多個子網路，然後按一下新增。
3. 按一下**儲存**toosave hello 組態。  
   ![新增網路](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>等候資料彙總
儲存第一次的 hello 組態之後，hello 方案就會開始收集代理程式的安裝位置的 hello 節點之間的網路封包中斷和延遲資訊。 此程序可能需要一些時間，有時候超過 30 分鐘。 在此狀態，hello hello 概觀 頁面中的網路效能監視器磚會顯示訊息，指出*程序中的資料彙總*。

![資料彙總進行中](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

當已上傳 hello 資料時，您會看到 hello 網路效能監視器磚更新顯示的資料。

![網路效能監視器圖格](./media/log-analytics-network-performance-monitor/npm-tile.png)

按一下 hello 磚 tooview hello 網路效能監視器儀表板。

![網路效能監視器儀表板](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>編輯子網路的監視設定
至少一個代理程式安裝所在的所有子網路會列在 hello**網路結構**hello 組態頁面中的索引標籤。

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable 或停用監視的特定子網路
1. 選取或清除 hello 方塊的下一個 toohello**子網路識別碼**然後確定**用於監視**呈選取狀態或已清除，視需要。 您可以選取或清除多個子網路。 停用時，子網路未受監視當 hello 代理程式將會更新的 toostop ping 其他代理程式。
2. 選擇您想要 toomonitor 特定子網路選取 hello 清單，然後將移 hello 子網路的 hello 節點 hello hello 清單包含未受監視和受監視節點之間的必要的節點。
   您可以新增自訂**描述**toohello 子網路，如果您願意的話。
3. 按一下**儲存**toosave hello 組態。  
   ![編輯子網路](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>選擇節點 toomonitor
已在其上安裝代理程式的所有 hello 節點會都列出 hello**節點** 索引標籤。

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable 或停用監視節點
1. 選取或清除您想 toomonitor 或停止監視 hello 節點。
2. 視需要按一下 [用於監視]，或加以清除。
3. 按一下 [儲存] 。  
   ![啟用節點監視](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>設定監視規則
網路效能監視會產生關於 hello 節點或子網路或網路連結，在達到閾值時的一組之間的連線健全狀況事件。 這些閾值可以自動學習 hello 系統，或設定自訂的警示規則。

hello*預設規則*hello 系統由和它建立健全狀況事件時遺失或任何兩個網路或子網路之間的延遲連結漏洞 hello 系統已了解臨界值。 您可以選擇 toodisable hello 預設規則，並建立自訂的監視規則

#### <a name="toocreate-custom-monitoring-rules"></a>toocreate 自訂監視規則
1. 按一下**加入規則**在 hello**監視器**索引標籤，然後輸入 hello 規則名稱和描述。
2. 您可以選取網路或子網路連結 toomonitor hello 的組 hello 清單中。
3. 第一次選取 hello 網路中的 hello 第一個子網路/s 感興趣的包含從 hello 網路下拉式清單中，然後選取 hello 子網路/s 從 hello 對應子網路 下拉式清單。
   選取**所有的子網路**如果您想 toomonitor 所有 hello 中的網路連結的子網路。 同樣地選取 hello 感興趣其他子網路/s。 而且，您可以按一下**新增例外狀況**tooexclude 監視特定的子網路連結從 hello 選取您所做。
4. 在 ICMP 和 TCP 通訊協定之間選擇，供您用來執行綜合交易。
5. 如果您不想 toocreate 健全狀況事件的 hello 您所選取的項目，然後清除**啟用此規則涵蓋 hello 連結上的健全狀況監視**。
6. 選擇監視條件。
   您可以輸入臨界值，以設定健康狀態事件產生的自訂臨界值。 每當 hello hello 條件值超出其 hello 選的網路/子網路對選取的閾值時，會產生健全狀況事件。
7. 按一下**儲存**toosave hello 組態。  
   ![建立自訂監視規則](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

儲存監視規則之後，您可以按一下**建立警示**，使用警示管理整合該規則。 警示規則會自動建立 hello 搜尋查詢，以及其他必要的參數自動填滿的。 使用警示的規則，您可以接收電子郵件為基礎的警示，此外 toohello 現有警示 NPM 內。 警示也會使用 runbook 觸發修復動作，或可以使用 webhook 與現有的服務管理解決方案整合。 您可以按一下**管理警示**tooedit hello 警示設定。

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>選擇 hello 正確的通訊協定 ICMP 或 TCP

網路效能監視器 (NPM) 會使用綜合交易 toocalculate 網路效能計量，例如封包遺失與連結的延遲。 toounderstand 這更好，請考慮 NPM 代理程式連接的 tooone 結尾的網路連結。 此 NPM 代理程式傳送探查封包 tooa 第二個 NPM 代理程式連接的 tooanother 結尾 hello 網路。 hello 第二個代理程式的回覆的回應封包。 此程序會重複幾次。 藉由測量 hello 回覆和所花費時間 tooreceive 數目每個回覆，第一個 hello NPM 代理程式，評估連結延遲和封包會卸除。

hello 格式、 大小以及這些封包的順序取決於您選擇當您建立的監視規則的 hello 通訊協定。 Hello 封包的通訊協定為基礎，hello 中繼網路裝置 （路由器、 交換器等等） 可能會以不同方式處理這些封包。 因此，您的通訊協定選擇會影響 hello 精確度的 hello 結果。 與您通訊協定的選擇也會決定是否部署 hello NPM 方案之後，您必須採取任何手動步驟。

NPM 提供 hello 執行綜合交易的 ICMP 和 TCP 通訊協定之間的選擇。
如果您建立綜合交易規則時，您可以選擇 ICMP，hello NPM 代理程式會使用 ICMP 回應訊息 toocalculate hello 網路延遲和封包遺失。 ICMP 回應使用 hello 相同訊息也就是傳送 hello 傳統 Ping 公用程式。 當您使用 TCP 做為 hello 通訊協定時，NPM 代理程式會傳送 hello 網路上的 TCP SYN 封包。 後面接著 TCP 交握完成，然後再移除 hello 連線使用 RST 封包。

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>選擇 hello 通訊協定之前的點 tooconsider
請考量下列資訊，再選擇通訊協定 toouse hello:

##### <a name="discovering-multiple-network-routes"></a>探索多個網路路由
TCP 在探索多個路由時精確度較高，而且在每個子網路中需要的代理程式較少。 例如，只要有一或二個使用 TCP 的代理程式，就可以探索子網路之間的所有備援路徑。 不過，您會需要數個代理程式使用 ICMP tooachieve 類似的結果。 如果使用 ICMP，假設您在兩個子網路間有 *N* 個路由，您在來源或目標子網路就需要超過 5*N* 個代理程式。

##### <a name="accuracy-of-results"></a>結果的精確度
路由器和交換器通常 tooassign 較低優先順序 tooICMP 回應封包比較 tooTCP 封包。 在某些情況下，網路裝置大量載入時，更仔細地透過 TCP 的 hello 資料會反映 hello 中斷和應用程式所發生的延遲。 這是因為大多數 hello 應用程式流量會透過 TCP 流動。 在這種情況下，ICMP 提供較不精確的比較結果 tooTCP。

##### <a name="firewall-configuration"></a>防火牆設定
TCP 通訊協定需要 TCP 封包傳送 tooa 目的地連接埠。 hello NPM 代理程式所使用的預設連接埠為 8084，不過您可以變更此設定代理程式時。 因此，您需要 tooensure 您的網路防火牆或 （在 Azure) 中的 NSG 規則允許 hello 連接埠的流量。 您也需要 toomake hello 本機防火牆 hello 代理程式安裝所在的電腦上確定已設定此連接埠上的 tooallow 流量。

您可以使用 PowerShell 指令碼 tooconfigure 防火牆規則在執行 Windows，但是必須 tooconfigure 網路防火牆以手動方式。

相反地，ICMP 運作不使用連接埠。 在大部分的企業案例中，透過 hello 防火牆 tooallow toouse 網路診斷工具，例如 hello Ping 公用程式允許 ICMP 流量。 因此，如果您可以 Ping 從另一部電腦，然後您可以使用 hello ICMP 通訊協定而不以手動方式需要 tooconfigure 防火牆。

> [!NOTE]
> 如果您不確定哪些通訊協定 toouse，選擇使用 ICMP toostart。 如果您不滿意 hello 結果，您可以一律切換 tooTCP 更新版本。


#### <a name="how-tooswitch-hello-protocol"></a>如何 tooswitch hello 通訊協定

如果您選擇 toouse ICMP 在部署期間，您可以隨時切換 tooTCP，藉由編輯 hello 預設的監視規則。

##### <a name="tooedit-hello-default-monitoring-rule"></a>tooedit hello 預設監視規則
1.  瀏覽過**網路效能** > **監視器** > **設定** > **監視器**然後按一下**預設規則**。
2.  捲動 toohello**通訊協定**區段，然後選取您想 toouse hello 通訊協定。
3.  按一下**儲存**tooapply hello 設定。

即使 hello 預設規則使用特定的通訊協定，您可以使用不同的通訊協定來建立新規則。 您甚至可以建立的規則，其中一些 hello 規則使用 ICMP，而另一個則使用 TCP 的混合。




## <a name="data-collection-details"></a>資料收集詳細資料
TCP 是選擇 」 和 「 ICMP 回應 ICMP 回應回覆時 ICMP 會被選為 hello 通訊協定 toocollect 中斷和延遲資訊時，網路效能監視器就會使用 TCP SYN-SYNACK-通知信號交換封包。 追蹤路由，也是使用的 tooget 拓撲資訊。

hello 下表顯示資料收集方法，以及如何針對網路效能監視器收集資料的其他詳細資料。

| 平台 | 直接代理程式 | SCOM 代理程式 | Azure 儲存體 | SCOM 是否為必要項目？ | 透過管理群組傳送的 SCOM 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |TCP 交握/ICMP ECHO 訊息會每 5 秒進行一次，而資料會每 3 分鐘傳送一次 |

hello 解決方案會使用綜合交易的 hello 網路 tooassess hello 健全狀況。 OMS 代理程式與另一個在 hello 網路 exchange TCP 封包或 ICMP 回應各種點 （取決於選取要監視的 hello 通訊協定） 一起安裝。 在 hello 過程中，代理程式了解 hello 反覆存取時間和封包遺失，如果有的話。 定期，每個代理程式也會執行所有 hello 必須經過測試的 hello 網路中的各種路由追蹤路由 tooother 代理程式 toofind。 使用此資料 hello 代理程式可以推算 hello 網路延遲和封包遺失數字。 hello 測試會每五秒的時間和資料會彙總一段三分鐘 hello 代理程式之前將它上傳 toohello 記錄分析服務中重複。

> [!NOTE]
> 代理程式與對方進行通訊經常，雖然它們不會產生大量網路流量時執行 hello 測試。 代理程式僅依賴 TCP SYN-SYNACK-通知信號交換封包 toodetermine hello 遺失和延遲-交換封包的任何資料。 在此過程中，代理程式之間的通訊方式只在需要時與 hello 代理程式通訊拓撲已最佳化 tooreduce 網路流量。
>
>

## <a name="using-hello-solution"></a>使用 hello 解決方案
本章節將說明所有 hello 儀表板函式以及 toouse 它們。

### <a name="solution-overview-tile"></a>解決方案概觀圖格
啟用 hello 網路效能監視器方案之後，在 hello OMS 的 [概觀] 頁面上的 hello 方案磚會提供 hello 網路健全狀況的快速概觀。 它會顯示環圈圖，顯示 hello 數目狀況良好和狀況不良的子網路連結。 當您按一下 hello 磚時，它會開啟 hello 方案儀表板。

![網路效能監視器圖格](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>網路效能監視器方案儀表板
hello**網路摘要**刀鋒視窗會顯示 hello 網路以及其相對大小的摘要。 後面磚顯示 hello 系統 （路徑則包含與代理程式的兩部主機和它們之間的所有 hello 躍點 hello IP 位址） 中的網路連結的子網路連結和路徑的總數目。

hello**頂端網路健全狀況事件**刀鋒視窗中列出的最新的健全狀況事件和警示 hello 系統與 hello 時間因為 hello 事件已在使用中。 每當 hello 封包遺失或在網路或子網路連結的延遲超過臨界值時，會產生健全狀況事件或警示。

hello**頂端狀況不良的網路連結**刀鋒視窗會顯示狀況不良的網路連結的清單。 這些是為其具有一或多個健全狀況不良事件，在 hello 時刻 hello 網路連結。

hello**頂端最遺失的子網路連結**和**子網路連結，以最延遲**刀鋒視窗的封包遺失顯示 hello 最上層的子網路連結，並分別的子網路連結前延遲的影響。 特定網路連結上可能會有高度延遲或某些數量的封包遺失。 這類連結會顯示 hello 前十個清單中，但未標示為狀況不良。

hello**常用查詢**刀鋒視窗包含一系列擷取原始的網路直接監視資料的搜尋查詢。 您可以使用這些查詢做為起點，建立自己的查詢以供自訂報告。

![網路效能監視器儀表板](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>深入鑽研
您可以按一下 hello 方案儀表板 toodrill 下拉式更深入的各種連結到任何感興趣的區域。 例如，當您看到警示或 hello 儀表板上出現的狀況不良的網路連結，您可以按一下它進一步 tooinvestigate。 您將會進入 tooa 頁面，其中列出所有 hello 子網路連結 hello 特定的網路連結。 您將會無法 toosee hello 遺失、 延遲和健全狀況狀態的每一個子網路連結，快速找出哪些子網路連結產生 hello 問題。 接著，您可以按一下**檢視節點連結**toosee 所有 hello 節點 hello 狀況不良的子網路連結。 然後，您可以查看個別節點的連結，而尋找 hello 狀況不良的節點連結。

您可以按一下**檢視拓撲**tooview hello 躍點的躍點的拓撲，hello hello 來源與目的節點之間的路由。 hello 狀況不良的路由，或以紅色顯示躍點，讓您能夠快速識別 hello 問題 tooa 特定部分 hello 網路。

![向下鑽研資料](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>網路狀態錄製器

每個檢視會在特定時間點顯示您網路健全狀況的快照集。 依預設，會顯示 hello 最新狀態。 在 hello hello 頁面最上方的 hello 列會顯示 hello 點正在顯示 hello 狀態的時間。 您也可以在 hello 列上按一下回網路健全狀況的時間和檢視 hello 快照中選擇 toogo**動作**。 您也可以選擇 tooenable 或停用自動重新整理的任何頁面，檢視 hello 最新狀態。

![網路狀態](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>趨勢圖
在每個層級，您向下鑽研，您可以看到 hello 趨勢的中斷和延遲的網路連結。 趨勢圖也可以用於子網路和節點連結。 您可以在 hello hello 圖表頂端使用 hello 階段控制項變更 hello 圖形 tooplot hello 時間間隔。

趨勢圖表會顯示 hello 效能的網路連結的歷程記錄檢視方塊。 某些網路問題是暫時性的本質，因此只能藉由查看 hello hello 網路的目前的狀態會永久 toocatch。 這是因為問題可以快速介面，並會消失之前，只有 tooreappear 在稍後的時間。 因為這些問題通常介面應用程式回應時間，即使所有的應用程式元件會出現 toorun 順暢地解釋增加時，這類暫時性的問題可以也很難應用程式系統管理員。

藉由查看趨勢圖表，其中 hello 問題將會顯示為網路延遲或封包遺失中突然出現尖峰，可以輕鬆地偵測這些種類的問題。

![趨勢圖](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>逐一躍點的拓撲圖
網路效能監視器顯示 hello 的互動式拓撲地圖上的兩個節點之間的路由拓撲，躍點的躍點。 您可以檢視 hello 拓樸對應選取的節點連結，然後按一下**檢視拓撲**。 此外，您可以檢視 hello 拓撲對應，即可**路徑**hello 儀表板上的磚。 當您按一下**路徑**hello 儀表板，您必須 tooselect hello 從 hello 左側面板中的來源和目的地節點，然後按一下**繪製**tooplot hello hello 兩個節點之間的路由。

hello 拓撲地圖會顯示多少路由 hello 之間兩個節點，而且是哪個路徑 hello 封包需要的資料。 Hello 拓撲地圖上的紅色標示的網路效能瓶頸。 您可以查看 hello 拓撲地圖上的紅色彩色的元素，以找出故障的網路連線或故障的網路裝置。

當您在 hello 拓撲地圖上，按一下節點或動態顯示透過它時，您會看到像 FQDN 和 IP 位址的 hello 節點的 hello 屬性。 按一下 躍點 toosee 是 IP 位址。 您可以使用 hello 可摺疊動作 窗格中的 hello 篩選器選擇 toofilter 特定路由。 此外，您也可以藉由隱藏 hello 中繼躍點使用 hello 動作 窗格中的 hello 滑桿來簡化 hello 網路拓撲。 您可以放大或使用滑鼠滾輪超出 hello 拓撲地圖。

請注意 hello 地圖中顯示該 hello 拓撲是第 3 層拓撲，而且未包含第 2 層裝置與連接。

![逐一躍點的拓撲圖](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>錯誤局部化
網路效能監視器 」 是可以 toofind hello 網路瓶頸，而不需要連線 toohello 網路裝置。 網路效能監視器 根據 hello 收集資料，它 hello 網路以及 hello 網路圖形上套用進階的演算法，讓 hello 的部分網路 hello 問題最可能 hello 來源的機率估計。

存取 toohops 無法使用，因為它不需要從 hello 網路裝置，例如路由器或交換器收集任何資料 toobe 時，這個方法會很有用的 toodetermine hello 網路瓶頸。 當兩個節點之間的 hello 躍點不在您的系統管理控制，這是也很有用。 例如，hello 躍點可能 ISP 路由器。

### <a name="log-analytics-search"></a>Log Analytics 搜尋
透過 hello 網路效能監視器儀表板和向下鑽研頁面以圖形方式公開的所有資料也都會記錄分析搜尋中原本提供的。 您可以查詢 hello 資料使用 hello 搜尋查詢語言，並藉由匯出 hello 資料 tooExcel 或 power Bi 建立自訂報表。 hello**常用查詢**hello 儀表板中的分頁有一些有用的查詢可作為 hello 起點來建立您自己的查詢和報表。

![搜尋查詢](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>調查 hello 根本原因的健康狀態警示
既然您已閱讀網路效能監視器，讓我們看看 hello 根本原因的健全狀況事件簡單的調查。

1. 在 hello 概觀頁面上，您會取得您網路的 hello 健全狀況的快速快照集觀察 hello**網路效能監視器**磚。 請注意，超出 hello 6 子網路連結受監視的狀況不良 2。 這值得調查一下。 按一下 hello 磚 tooview hello 方案儀表板。  
   ![網路效能監視器圖格](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. 在 hello 範例圖，您會發現沒有健全狀況事件會處於狀況不良的網路連結。 您決定 tooinvestigate hello 問題，然後按一下 hello **DMZ2 DMZ1**網路連結 toofind 出 hello 問題的 hello 根。  
   ![狀況不良的網路連結範例](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. hello 向下鑽研頁面會顯示在所有 hello 子網路連結**DMZ2 DMZ1**網路連結。 您會發現，這兩個 hello 的子網路連結，hello 延遲已越過 hello 閾值進行 hello 網路連結狀況不良。 您也可以查看這兩個 hello 子網路連結的 hello 延遲趨勢。 您可以使用在 hello 圖形 toofocus hello 上的選取控制項所需的時間範圍內的 hello 時間。 您可以看到 hello hello 一天的時間延遲已到達其尖峰。 您可在稍後搜尋這個問題的時間週期 tooinvestigate hello 的 hello 記錄檔。 按一下**檢視節點連結**toodrill 下拉式進一步。  
   ![狀況不良的子網路連結範例](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. 類似 toohello 前一頁，hello 特定子網路連結的 hello 向下鑽研頁面列出其構成的節點連結。 您可以執行類似動作這裡 hello 上一個步驟中一樣。 按一下**檢視拓撲**tooview hello 拓撲 hello 2 節點之間。  
   ![狀況不良的節點連結範例](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Hello 拓撲地圖繪製 hello 2 選取節點之間的所有 hello 路徑。 您可以視覺化 hello 躍點的躍點拓撲的 hello 拓撲地圖上的兩個節點之間的路由。 它可讓您清楚地了解的 hello 兩個節點之間有多少的路由和哪些路徑 hello 資料封包花費的時間。 網路效能瓶頸會標示為紅色。 您可以查看 hello 拓撲地圖上的紅色彩色的元素，以找出故障的網路連線或故障的網路裝置。  
   ![狀況不良的拓撲檢視範例](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. 檢閱 hello 遺失、 延遲和躍點，每個路徑中的 hello 數目 hello**動作**窗格。 使用 hello 捲軸 tooview hello 路徑的詳細資料的狀況不良。  使用 hello 篩選 tooselect hello 路徑使用 hello 狀況不良的躍點的繪製 hello 拓撲只 hello 選取路徑。 您可以使用您的滑鼠滾輪 toozoom 內外 hello 拓撲地圖。

   在影像下方的 hello 您可以清楚地看到藉由查看 hello 路徑和躍點紅色 hello hello 問題區域 toohello 特定區段的 hello 網路的根本原因。 Hello 拓撲 map 中的節點上按一下，就會顯示 hello hello 節點，包含 hello FQDN 和 IP 位址屬性。 按一下 上一個躍點顯示 hello hello 躍點 IP 位址。  
   ![狀況不良的拓撲 - 路徑詳細資料範例](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>提供意見反應

- **UserVoice** -您可以在網路效能監視器功能，您希望我們採取何 toowork 上張貼您的想法。 造訪 [UserVoice 頁面](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring)。
- **加入我們的社群** - 我們竭誠歡迎新客戶加入我們的社群。 它的一部分，您會取得早期存取 toonew 功能，並協助我們改善網路效能監視器。 如果您想加入，請填妥這份[快速問卷調查](https://aka.ms/npmcohort)。

## <a name="next-steps"></a>後續步驟
* [搜尋記錄](log-analytics-log-searches.md)tooview 詳細的網路效能資料記錄。
