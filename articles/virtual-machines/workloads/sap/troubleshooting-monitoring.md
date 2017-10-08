---
title: "aaaTroubleshooting 與監視的 SAP HANA Azure （大型執行個體） 上 |Microsoft 文件"
description: "針對 SAP HANA on Azure (大型執行個體) 進行疑難排解和監視。"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Tootroubleshoot 和監視器的 SAP HANA （大型執行個體），在 Azure 上


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>SAP HANA on Azure (大型執行個體) 中的監視

在 Azure （大型執行個體） 上的 SAP HANA 並無不同之任何其他 IaaS 部署中，您需要 toomonitor 什麼 hello OS，hello 應用程式是這麼做，而這些取用 hello 下列資源的方式：

- CPU
- 記憶體
- 網路頻寬
- 磁碟空間

視需要 toofigure 出 hello 上述指定的資源類別是否足夠，或是否這些取得耗盡與 Azure 虛擬機器。 以下是更多詳細資料上的每個 hello 不同類別：

**CPU 資源耗用量：** SAP HANA 針對特定工作負載所定義的 hello 比例是強制的 toomake 確定應該使用透過儲存在記憶體中的 hello 資料 toowork 足夠 CPU 資源。 不過，可能會其中 HANA 會消耗大量 CPU 執行查詢，因為 toomissing 索引或類似問題的情況。 這表示您應該監視 CPU 的 hello HANA 大型執行個體單位為 hello 特定 HANA 服務所耗用的 CPU 資源的資源耗用量。

**記憶體耗用量：**是重要 toomonitor 從 HANA 中,，以及外部 HANA hello 單元上的。 內 HANA，監視 hello 資料配置的記憶體中順序 toostay 內 hello 所需大小的指導方針的 SAP HANA 中的特殊使用。 您也想 toomonitor hello 大型執行個體層級 toomake 確定其他已安裝非-HANA 軟體未不耗用太多的記憶體，因此與 HANA 爭用記憶體的記憶體耗用量。

**網路頻寬：** hello Azure VNet 閘道的資料移到 hello Azure VNet 的頻寬有限，因此您很有幫助 toomonitor hello 資料所有收到 hello VNet toofigure 出如何關閉您的 hello Azure toohello 限制內的 Azure Vm您選取的 SKU 的閘道。 Hello HANA 大型執行個體的單位，但卻可讓意義 toomonitor 傳入和傳出網路流量及 tookeep 追蹤一段時間所處理的 hello 磁碟區。

**磁碟空間：**磁碟空間耗用量通常會隨著時間增加。 其原因有許多，但最重要的包括：資料量增加、執行交易記錄備份、儲存追蹤檔案，以及執行儲存體快照。 因此，它會是重要的 toomonitor 磁碟空間使用量，並管理 hello 與 hello HANA 大型執行個體單元相關聯的磁碟空間。

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>從 HANA 端進行監視和疑難排解

在訂單 tooeffectively 分析問題相關的 tooSAP HANA Azure （大型執行個體） 上，有用 toonarrow 向 hello 有問題的根本原因。 SAP 發行大量的文件 toohelp 您。

適用的常見問題集相關的 tooSAP HANA 效能可以在 hello 遵循 SAP 附註：

- [SAP 附註 #2222200 - 常見問題集：SAP HANA 網路](https://launchpad.support.sap.com/#/notes/2222200)
- [SAP 附註 #2100040 - 常見問題集：SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)
- [SAP 附註 #199997 - 常見問題集：SAP HANA 記憶體](https://launchpad.support.sap.com/#/notes/2177064)
- [SAP 附註 #200000 - 常見問題集：SAP HANA 效能最佳化](https://launchpad.support.sap.com/#/notes/2000000)
- [SAP 附註 #199930 - 常見問題集：SAP HANA I/O 分析](https://launchpad.support.sap.com/#/notes/1999930)
- [SAP 附註 #2177064 - 常見問題集：SAP HANA 服務重新啟動和當機](https://launchpad.support.sap.com/#/notes/2177064)

**SAP HANA 警示**

第一個步驟是檢查 hello 目前 SAP HANA 警示記錄檔。 在 SAP HANA Studio 中，移太**管理主控台： 警示： 顯示： 所有警示**。 此索引標籤會顯示所有的 SAP HANA 臨界值的範圍之外 hello 設定最小和最大臨界值的特定值 （可用的實體記憶體、 CPU 使用率等）。 根據預設，檢查會每隔 15 分鐘自動重新整理一次。

![在 SAP HANA Studio 中，移 tooAdministration 主控台： 警示： 顯示： 所有警示](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

由於 tooimproper 臨界值 設定觸發警示，解析是 tooreset toohello 預設值或較合理的臨界值。

![重設 toohello 預設值或較合理的臨界值](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

hello 下列警示可能表示 CPU 資源的問題：

- Host CPU Usage (Alert 5) (主機 CPU 使用率 (警示 5))
- Most recent savepoint operation (Alert 28) (最新的儲存點作業 (警示 28))
- Savepoint duration (Alert 54) (儲存點持續時間 (警示 54))

從 hello 下列其中一種在 SAP HANA 資料庫上，您可能會發現高 CPU 耗用率：

- 針對目前和過去的 CPU 使用率，引發了「警示 5」(主機 CPU 使用率)
- hello hello 概觀畫面上顯示 CPU 使用量

![Hello 概觀畫面上顯示 CPU 使用量](./media/troubleshooting-monitoring/image3-cpu-usage.png)

在過去的 hello hello 負載圖形可能會顯示高 CPU 耗用率或高耗用量：

![hello 負載圖形可能會顯示高 CPU 耗用率或高耗用量在過去的 hello](./media/troubleshooting-monitoring/image4-load-graph.png)

警示觸發到期 toohigh CPU 使用率可能因多種原因造成，包括但不是限於： 特定交易、 載入資料、 停滯的作業，長時間執行的 SQL 陳述式和不正確的查詢效能 （例如，BW HANA 上執行cube)。

請參閱 toohello [SAP HANA 疑難排解： CPU 相關導致和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false)網站詳細的疑難排解步驟。

**作業系統**

其中一個最重要的 hello 檢查在 Linux 上的 SAP HANA toomake 確定已停用透明龐大的頁面，請參閱[SAP 附註 #2131662 透明龐大頁面 (THP) 在 SAP HANA 伺服器](https://launchpad.support.sap.com/#/notes/2131662)。

- 您可以檢查透明龐大的頁面是否已啟用透過下列 Linux 命令 hello:**數據機 /sys/kernel/mm/transparent\_hugepage/啟用**
- 如果_一律_會括在方括號，如下所示，它表示 hello 透明龐大的頁面已啟用: [永遠] madvise 永遠不會; 如果_永遠不會_會括在括號內，如下所示，這表示該 hello 透明龐大的頁面已停用： 一律 madvise [永不]

hello 下列 Linux 命令應傳回任何項目： **rpm qa | grep ulimit。** 如果顯示安裝的是 _ulimit_，請立即將它解除安裝。

**記憶體**

您可能會注意到 hello 數量的記憶體配置的 hello SAP HANA 資料庫高於預期。 hello 下列警示指出的高記憶體使用量問題：

- Host physical memory usage (Alert 1) (主機實體記憶體使用量 (警示 1))
- Memory usage of name server (Alert 12) (名稱伺服器的記憶體使用量 (警示 12))
- Total memory usage of Column Store tables (Alert 40) (資料行存放區資料表的總記憶體使用量 (警示 40))
- Memory usage of services (Alert 43) (服務的記憶體使用量 (警示 43))
- Memory usage of main storage of Column Store tables (Alert 45) (資料行存放區資料表的主要儲存體記憶體使用量 (警示 45))
- Runtime dump files (Alert 46) (執行階段傾印檔案 (警示 46))

請參閱 toohello [SAP HANA 疑難排解： 記憶體問題](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false)網站詳細的疑難排解步驟。

**網路**

請參閱太[SAP 附註 #2081065 疑難排解 SAP HANA 網路](https://launchpad.support.sap.com/#/notes/2081065)並執行 hello 網路疑難排解步驟，在此 SAP 附註。

1. 分析伺服器與用戶端之間的來回時間。
  A. 執行 hello SQL 指令碼[ _HANA\_網路\_用戶端_](https://launchpad.support.sap.com/#/notes/1969700)_。_
  
2. 分析節點間的通訊。
  A. 執行 SQL 指令碼 [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_。_

3. 執行 Linux 指令**ifconfig** （hello 輸出會顯示是否發生任何封包遺失）。
4. 執行 Linux 命令 **tcpdump**。

此外，使用開放原始碼 hello [IPERF](https://iperf.fr/)工具 （或類似） toomeasure 實際的應用程式的網路效能。

請參閱 toohello [SAP HANA 疑難排解： 網路效能和連線問題](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false)網站詳細的疑難排解步驟。

**儲存體**

從使用者的觀點而言，應用程式 （或 hello 整體系統） 變得緩慢執行、 沒有回應，或甚至似乎 toohang，如果 I/O 效能的問題。 在 [hello**磁碟區**] 索引標籤在 SAP HANA Studio 中，您可以看到 hello 附加磁碟區，以及每個服務所使用的磁碟區。

![在 hello SAP HANA Studio 中的磁碟區索引標籤，您可以看到 hello 附加磁碟區，以及每個服務所使用的磁碟區](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

連接的磁碟區的詳細資料請參閱 < 囉 」 畫面 hello 下半部 hello 磁碟區，例如檔案和 I/O 統計資料。

![連接的磁碟區的詳細資料請參閱 < 囉 」 畫面 hello 下半部 hello 磁碟區，例如檔案和 I/O 統計資料](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

請參閱 toohello [SAP HANA 疑難排解： I/O 相關的根本原因和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false)和[SAP HANA 疑難排解： 磁碟相關的根本原因和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false)網站詳細的疑難排解步驟。

**診斷工具**

您可以透過 HANA\_Configuration\_Minichecks 執行「SAP HANA 健康情況檢查」。 此工具會傳回應該已在 SAP HANA Studio 中引發成警示的潛在重大技術問題。

請參閱太[SAP 附註 #1969700 SAP HANA 的 SQL 陳述式集合](https://launchpad.support.sap.com/#/notes/1969700)並下載 hello SQL Statements.zip 檔案附加的 toothat 附註。 此.zip 檔案儲存在 hello 本機硬碟上。

在 SAP HANA Studio 中，在 hello**系統資訊**索引標籤上，以滑鼠右鍵按一下 hello**名稱**資料行，然後選取**匯入 SQL 陳述式**。

![在 hello 系統資訊 索引標籤上的 SAP HANA Studio hello 名稱資料行中以滑鼠右鍵按一下並選取匯入 SQL 陳述式](./media/troubleshooting-monitoring/image7-import-statements-a.png)

選取 hello SQL Statements.zip 檔案儲存在本機，並將匯入具有 hello 對應的 SQL 陳述式的資料夾。 此時，hello 可以執行許多不同的診斷檢查，以這些 SQL 陳述式。

Tootest SAP HANA 系統複寫的頻寬需求，例如，滑鼠右鍵按一下 hello**頻寬**陳述式**複寫： 頻寬**選取**開啟**在 SQL 主控台中。

hello 完整的 SQL 陳述式會開啟 允許的輸入的參數 （修改區段） toobe 變更，然後執行。

![hello 完整的 SQL 陳述式會開啟 允許的輸入的參數 （修改區段） toobe 變更，然後執行](./media/troubleshooting-monitoring/image8-import-statements-b.png)

另一個範例是以滑鼠右鍵按一下底下的 hello 陳述式**複寫： 概觀**。 選取**Execute** hello 內容功能表：

![另一個範例是以滑鼠右鍵按一下複寫下 hello 陳述式： 概觀。 Execute hello 內容功能表中選取](./media/troubleshooting-monitoring/image9-import-statements-c.png)

這會產生可協助進行疑難排解的資訊：

![這會產生可協助進行疑難排解的資訊](./media/troubleshooting-monitoring/image10-import-statements-d.png)

請勿 hello 相同 hana\_組態\_Minichecks 和任何核取_X_ hello 中的標記_C_ (Critical) 資料行。

範例輸出：

**HANA\_Configuration\_MiniChecks\_Rev102.01+1**：適用於一般 SAP HANA 檢查。

![HANA\_Configuration\_MiniChecks\_Rev102.01+1：適用於一般 SAP HANA 檢查](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Services\_Overview**：適用於 SAP HANA 服務目前執行情況的概觀。

![HANA\_Services\_Overview：適用於 SAP HANA 服務目前執行情況的概觀](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Services\_Statistics**：適用於 SAP HANA 服務資訊 (CPU、記憶體等)。

![HANA\_Services\_Statistics：適用於 SAP HANA 服務資訊 ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_組態\_概觀\_Rev110 +** hello SAP HANA 執行個體上的一般資訊。

![HANA\_組態\_概觀\_Rev110 + hello SAP HANA 執行個體上的一般資訊](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_組態\_參數\_Rev70 +** toocheck SAP HANA 參數。

![HANA\_組態\_參數\_Rev70 + toocheck SAP HANA 參數](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

