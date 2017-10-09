---
title: "透過在 Azure 上的 Linux Cassandra aaaRun |Microsoft 文件"
description: "如何 toorun Cassandra on Linux 的 Azure 虛擬機器中從叢集 Node.js 應用程式"
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>在 Azure 上執行 Cassandra 搭配 Linux 並透過 Node.js 進行存取
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 請參閱 [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) 的 Resource Manager 範本和 [CentOS 上的 Spark 叢集和 Cassandra](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/)。

## <a name="overview"></a>概觀
Microsoft Azure 是一個開放雲端平台，可執行 Microsoft 和非 Microsoft 軟體，包括作業系統、應用程式伺服器、傳訊中介軟體，以及來自商業和開放原始碼模型的 SQL 和 NoSQL 資料庫。 如果要在包括 Azure 在內的公用雲端上建立具有恢復功能的服務，應用程式伺服器和儲存層都必須要有仔細的規劃和審慎的架構。 Cassandra 的分散式儲存架構天生就有助於建置可針對叢集失敗容錯的高可用性系統。 Cassandra 是一種雲端等級的 NoSQL 資料庫，由 Apache Software Foundation 維護 (網址 cassandra.apache.org)；Cassandra 以 Java 撰寫，因此可以在 Windows 與 Linux 平台上執行。

這篇文章 hello 重點是 tooshow Cassandra 部署在 Ubuntu 上的做為單一及多資料中心叢集，利用 Microsoft Azure 虛擬機器和虛擬網路。 hello 叢集部署的實際執行最佳化工作負載超出本文的範圍因為它需要多重磁碟的節點設定，適當的環形拓撲設計和資料模型化 toosupport hello 需要複寫資料一致性、 輸送量和高可用性需求。

建置 hello Cassandra 叢集的相關內容的基本方法 tooshow 比較 Docker、 Chef 或 Puppet 這可以讓您輕鬆許多 hello 基礎結構部署這個發行項會使用。  

## <a name="hello-deployment-models"></a>hello 部署模型
Microsoft Azure 網路允許隔離私用的叢集，可以在其中的 hello 存取限制的 tooattain 正常更細緻的網路安全性的 hello 的部署。  這篇文章是關於顯示在基本層級的 hello Cassandra 部署，因為我們將不著重在 hello 一致性層級和輸送量的 hello 最佳的儲存體設計中。 以下是我們假設叢集的網路需求的 hello 清單：

* 外部系統無法從 Azure 內部或外部存取 Cassandra 資料庫
* Cassandra 叢集中有 toobe thrift 流量負載平衡器後方
* 在每個資料中心部署 Cassandra 節點為兩個群組以提高叢集可用性
* 鎖定 hello 叢集因此，只有應用程式伺服器陣列具有存取 toohello 資料庫直接
* 除了 SSH 以外，沒有其他公用網路端點
* 每個 Cassandra 節點需要固定的內部 IP 位址

Cassandra 可以部署的 tooa 單一 Azure 區域，或是根據 hello 分散式本質 hello 工作負載的 toomultiple 區域。 多區域部署模型可運用 tooserve 使用者更接近 tooa 特定地理位置透過 hello 相同 Cassandra 基礎結構。 Cassandra 的內建節點複寫會負責 hello 同步處理的多重主機寫入來自多個資料中心，並顯示 hello 資料 tooapplications 一致檢視。 多區域部署也會協助 hello 風險降低的 hello 更廣泛的 Azure 服務中斷。 Cassandra 的可微調一致性和複寫拓撲有助於滿足應用程式不同的 RPO 需求。

### <a name="single-region-deployment"></a>單一區域部署
我們將開始的單一區域部署和蒐集 hello datacenter 中建立多區域模型的知識。 Azure 虛擬網路將會使用的 toocreate 隔離子網路，如此即可符合上述 hello 網路安全性需求。  建立 hello 單一區域部署中所述的 hello 程序會使用 Ubuntu 14.04 LTS 和 Cassandra 2.08;不過，hello 程序很容易就會採用的 toohello 其他 Linux 變異。 hello 以下是一些 hello 單一區域部署的 hello 系統特性。  

**高可用性：** hello Cassandra 節點顯示在圖 1 所部署的 hello tootwo 可用性設定組，以便 hello 節點高可用性的多個容錯網域之間分佈。 標註具有每個可用性設定組的 Vm 是對應的 too2 容錯網域。  容錯網域 toomanage 意外關機時 hello 概念，例如主機或客體 OS 修補程式/升級 （應用程式升級） 的升級網域的時間 （例如硬體或軟體失敗） 的 Microsoft Azure 會使用 hello 概念用來管理排定停機時間。 請參閱[災害復原與高可用性 Azure 應用程式](http://msdn.microsoft.com/library/dn251004.aspx)hello 角色容錯網域和升級網域中取得高可用性。

![單一區域部署](./media/cassandra-nodejs/cassandra-linux1.png)

圖 1：單一區域部署

請注意在 hello 撰寫本文時，Azure 將不允許的一組 Vm tooa 特定容錯網域; hello 明確對應因此，即使與圖 1 所示的 hello 部署模型，它是統計上可能 hello 的所有虛擬機器都可能對應的 tootwo 容錯網域，而不是四個。

**負載平衡 Thrift 流量：** Thrift hello web 伺服器內的用戶端程式庫 toohello 叢集連線透過內部負載平衡器。 這需要新增 hello 內部負載平衡器 toohello 「 資料 」 的子網路的 hello 程序 （請參閱圖 1） hello hello 雲端服務裝載 hello Cassandra 叢集內容中。 一旦定義 hello 內部負載平衡器之後，每個節點會需要 hello 負載平衡端點 toobe 加入 hello 註解的負載平衡集與先前定義的負載平衡器名稱。 如需詳細資訊，請參閱 [Azure內部負載平衡 ](../../../load-balancer/load-balancer-internal-overview.md)。

**叢集種子：**很重要的種子為 hello 新節點會與種子節點 toodiscover hello 拓樸 hello 叢集的通訊，tooselect hello 大多數的高可用性節點。 從每個可用性設定組的一個節點指定為種子節點 tooavoid 單一失敗點。

**複寫因數和一致性層級：** Cassandra 的內建高可用性和資料耐久性的特點在於 hello 複寫因數 (RF-複本儲存在 hello 叢集上每個資料列數目) 和一致性層級 （數目讀取/寫入，再傳回 hello 結果 toohello 呼叫端複本 toobe)。 而 hello 一致性層級指定時發出 hello CRUD 查詢 hello KEYSPACE （類似 tooa 關聯式資料庫） 建立期間指定複寫因數。 請參閱 Cassandra 文件，網址[設定的一致性](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html)一致性的詳細資料和 hello 仲裁計算公式。

Cassandra 支援兩種類型的資料完整性模型 – 一致性和最終一致性。hello 複寫因數和一致性層級會一起判斷 hello 資料會一致儘速寫入作業已完成，或將最終保持一致。 例如，指定仲裁 hello 一致性層級將一律可確保資料一致性，同時 hello 數目複本 toobe 撰寫成所需的 tooattain 底下的任何一致性層仲裁 （例如一個） 會導致取得一致的最終結果的資料。

如上所示，以複寫因數 3 及仲裁的 hello 8 個節點叢集 （2 個節點讀取或寫入的一致性） 讀取/寫入一致性層級，可以繼續執行的 hello 理論上遺失在 hello hello 應用程式啟動之前的大部分 1 的節點，每個複寫群組請注意 hello 失敗。 這是假設所有的 hello 空格有對稱讀取/寫入要求。  hello 以下是我們將會用於叢集部署的 hello hello 參數：

單一區域 Cassandra 叢集設定：

| 叢集參數 | 值 | 備註 |
| --- | --- | --- |
| 節點數目 (N) |8 |Hello 叢集中的節點總數 |
| 複寫因素 (RF) |3 |指定資料列的複本數目 |
| 一致性層級 (寫入) |QUORUM[(RF/2) +1) = 2] hello 結果的 hello 公式無條件捨去 |寫入在 hello 大部分 2 個複本之前傳送 hello 回應 toohello 呼叫端;第 3 個複本會寫入最終一致的方式。 |
| 一致性層級 (讀取) |仲裁 [(RF/2) + 1 = 2] hello 公式的結果 hello 無條件捨去 |讀取傳送回應 toohello 呼叫端之前的 2 個複本。 |
| 複寫策略 |如需 NetworkTopologyStrategy 的詳細資訊，請參閱 Cassandra 文件中的 [資料複寫](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) (英文) |了解 hello 部署拓撲，並將複本放在節點上，使所有 hello 複本不都會出現在 hello 相同機架 |
| Snitch |如需 GossipingPropertyFileSnitch 的詳細資訊，請參閱 Cassandra 文件中的 [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) (英文) |NetworkTopologyStrategy 使用告密者 toounderstand hello 拓撲的概念。 GossipingPropertyFileSnitch 可提供更好的控制權，對應每個節點 toodata 置中與機架中。 hello 叢集然後使用八卦 toopropagate 這項資訊。 這是在動態 IP 設定相對 tooPropertyFileSnitch 更簡單 |

**Cassandra 叢集的 Azure 考量：** Microsoft Azure 虛擬機器功能會使用 Azure Blob 儲存體來取得磁碟持續性；Azure 儲存體會基於高持久性因素來為每個磁碟儲存 3 個複本。 這表示每個插入 Cassandra 資料表的資料列已經儲存在 3 個複本，因此資料的一致性是已處理即使 hello 複寫因數 (RF) 為 1。 複寫因數是 1 hello 主要問題是 hello 應用程式將會經歷停機時間，即使單一 Cassandra 節點失敗。 不過，如果節點已關閉的 hello 問題 （例如硬體、 系統軟體失敗） 辨識由 Azure 網狀架構控制器，它將會提供新的節點在它的地方使用 hello 相同的存放磁碟機。 佈建新節點 tooreplace hello 舊其中一個可能需要幾分鐘的時間。  同樣地，對於客體作業系統變更這類的計劃性的維護活動，Cassandra 升級和應用程式變更 Azure 網狀架構控制器執行輪流升級的 hello 節點 hello 叢集中。  輪流升級也可能需要幾個節點下一次，因此 hello 叢集可能會遇到短暫的停機時間為幾個資料分割。 不過，hello 資料不會遺失到期 toohello 內建的 Azure 儲存體備援。  

系統部署不需要高可用性的 tooAzure (例如大約 99.9 即相等 too8.76 小時/年，請參閱 <<c0> [ 高可用性](http://en.wikipedia.org/wiki/High_availability)如需詳細資訊) 可能無法與 RF toorun = 1 且一致性層級 = 其中一個。  應用程式具有高可用性需求，RF = 3 和一致性層級 = 仲裁可以容忍 hello 的其中一個 hello 節點 hello 複本的停機。 RF = 1 在傳統的部署 （例如內部部署） 不能因為 toohello 可能會遺失資料造成磁碟故障時提供類似的問題。   

## <a name="multi-region-deployment"></a>多重區域部署
Cassandra 的資料中心感知的複寫和有助於 hello 多區域部署不含 hello hello 現成上面所述的一致性模型需要的任何外部工具。 這是相當不同 hello 傳統關聯式資料庫中可能相當複雜的多重主機寫入的資料庫鏡像的 hello 安裝程式。 Cassandra 中設定多區域可協助進行 hello 使用案例包括下列 hello:

**鄰近性基礎的部署：**多租用戶應用程式，以清除對應的租用戶使用者-到-區域，可以發展的 hello 多區域叢集的低延遲。 例如學習管理系統的教育機構可以分散式的叢集部署在美國東部和美國西部地區 tooserve hello 個別園區針對交易式，以及分析。 hello 資料可以在 hello 時間讀取和寫入本機一致，而且可以是跨兩個 hello 區最終保持一致。 其他的範例還有媒體發佈、電子商務，以及可為地理位置集中之使用者提供服務的一切 (這是此部署模型的絕佳使用案例)。

**高可用性：**備援是取得軟體和硬體高可用性的關鍵因數；如需詳細資訊，請參閱＜在 Microsoft Azure 上建置可靠的雲端系統＞。 Microsoft Azure 上 hello 達成，則為 true 的備援性的唯一可靠方式就是藉由部署多區域叢集。 應用程式可以部署在主動-主動或主動-被動模式中，如果其中一個 hello 區域已關閉，Azure Traffic Manager 可以將重新導向流量 toohello 使用中的區域。  使用 hello 單一區域部署時，如果 hello 可用性是 99.9，兩個區域部署可以達到 99.9999 hello 公式所計算的可用性: (1-(1-0.999) * (1-0.999)) * 100)。hello 上方紙張，如需詳細資訊，請參閱。

**災害復原：**如果設計正確，多區域的 Cassandra 叢集就能承受重大的資料中心中斷。 如果一個區域已關閉，hello 部署應用程式 tooother 區域可以開始處理 hello 終端使用者。 類似的任何商務持續性實作，hello 應用程式有 toobe 的 hello 非同步管線中的 hello 資料造成部分資料遺失容錯。 不過，Cassandra 讓 hello 復原更 swifter 於 hello 傳統資料庫復原程序所花費的時間。 圖 2 顯示 hello 一般多區域部署模型，具有八個節點，在每個區域。 這兩個區域是彼此的 hello 的鏡像映像相同的對稱。真實世界的設計是根據 hello 工作負載類型 （例如交易式或分析）、 RPO、 RTO、 資料一致性和可用性需求而定。

![多區域部署](./media/cassandra-nodejs/cassandra-linux2.png)

圖 2：多區域 Cassandra 部署

### <a name="network-integration"></a>網路整合
設定虛擬機器位於兩個區域部署的 tooprivate 網路與彼此通訊使用 VPN 通道。 hello VPN 通道連接兩個的軟體閘道 hello 網路部署程序期間佈建。 兩個區域有類似的網路架構，以"web"和"data"的子網路。Azure 網路可讓 hello 建立所需數量的子網路，並視需要透過網路安全性套用 Acl。 設計 hello 叢集拓撲時間的資料中心的通訊延遲與 hello 經濟影響 hello 網路流量需要 toobe 視為。

### <a name="data-consistency-for-multi-data-center-deployment"></a>多重資料中心部署的資料一致性
分散式部署需要 toobe 留意 hello 叢集拓撲影響產能和高可用性。 hello RF 和一致性層級需要 toobe hello 仲裁的方式選取不需要依賴的所有 hello 資料中心的 hello 可用性。
針對需要高的一致性，LOCAL_QUORUM 一致性層級 （適用於讀取和寫入） 將會確認該 hello 本機系統讀取和寫入符合從本機 hello 節點，而資料是以非同步方式複寫 toohello 遠端資料中心。  表 2 摘述 hello 設定寫 hello hello 稍後所述的多地區叢集的詳細資料。

**兩個區域的 Cassandra 叢集組態**

| 叢集參數 | 值 | 備註 |
| --- | --- | --- |
| 節點數目 (N) |8 + 8 |Hello 叢集中的節點總數 |
| 複寫因素 (RF) |3 |指定資料列的複本數目 |
| 一致性層級 (寫入) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] hello 公式的結果 hello 無條件捨去 |2 個節點將會寫入 toohello 第一個資料中心以同步方式;hello 額外 2 個節點所需的仲裁會撰寫以非同步方式 toohello 第 2 個資料中心。 |
| 一致性層級 (讀取) |LOCAL_QUORUM ((RF/2) + 1) = 2 會無條件捨去 hello 公式的結果 hello |讀取要求符合從只有一個區域。傳送後 toohello 用戶端 hello 回應之前，會讀取的 2 個節點。 |
| 複寫策略 |如需 NetworkTopologyStrategy 的詳細資訊，請參閱 Cassandra 文件中的 [資料複寫](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) (英文) |了解 hello 部署拓撲，並將複本放在節點上，使所有 hello 複本不都會出現在 hello 相同機架 |
| Snitch |如需 GossipingPropertyFileSnitch 的詳細資訊，請參閱 Cassandra 文件中的 [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) (英文) |NetworkTopologyStrategy 使用告密者 toounderstand hello 拓撲的概念。 GossipingPropertyFileSnitch 可提供更好的控制權，對應每個節點 toodata 置中與機架中。 hello 叢集然後使用八卦 toopropagate 這項資訊。 這是在動態 IP 設定相對 tooPropertyFileSnitch 更簡單 |

## <a name="hello-software-configuration"></a>hello 軟體組態
hello 部署可以使用下列軟體版本的 hello:

<table>
<tr><th>軟體</th><th>來源</th><th>版本</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

因為下載 JRE 需要手動接受 Oracle 授權、 toosimplify hello 部署下載所有 hello 稍後上傳到 hello Ubuntu 範本映像，我們將建立為前兆 toohello 叢集所需的軟體 toohello 桌面部署。

下載軟體上方 hello hello 本機電腦上的已知的下載目錄 （例如在 Windows 上的 %TEMP%/downloads 或 ~/Downloads 多數 Linux 散發套件或 Mac 上的）。

### <a name="create-ubuntu-vm"></a>建立 UBUNTU VM
在此步驟中的 hello 程序我們將使用 hello 先決條件軟體建立 Ubuntu 映像以便 hello 映像可重複用於佈建 Cassandra 的數個節點。  

#### <a name="step-1-generate-ssh-key-pair"></a>步驟 1：產生 SSH 金鑰組
Azure 需要的 X509 公開金鑰 PEM 或 DER 編碼 hello 佈建時間。 產生公開/私密金鑰的金鑰組，使用位於如何 hello 指示 tooUse SSH 與 Azure 上的 Linux。 如果您打算 toouse putty.exe 為 Windows 或 Linux 上的 SSH 用戶端時，您會有 tooconvert hello PEM 編碼 RSA 私用金鑰 tooPPK 格式使用 puttygen.exe;hello 這個指示 hello 上方網頁中。

#### <a name="step-2-create-ubuntu-template-vm"></a>步驟 2：建立 Ubuntu 範本 VM
登入 hello Azure 傳統入口網站並使用 hello 下列順序的 toocreate hello 範本 VM： 按一下 [新增]、 計算、 虛擬機器，從組件庫、 UBUNTU、 Ubuntu Server 14.04 LTS、，然後按一下hello 向右箭號。 描述如何 toocreate Linux VM，請參閱教學課程建立執行 Linux 之虛擬機器。

輸入下列資訊在 hello 「 虛擬機器設定 」 畫面 #1 hello:

<table>
<tr><th>欄位名稱              </td><td>       欄位值               </td><td>         備註                </td><tr>
<tr><td>版本發行日期    </td><td> 選取的日期，從 hello 下拉式清單</td><td></td><tr>
<tr><td>[虛擬機器名稱]    </td><td> cass-template                   </td><td> 這是 hello hello VM 主機名稱 </td><tr>
<tr><td>層次                     </td><td> 標準                           </td><td> 保留預設值，hello              </td><tr>
<tr><td>大小                     </td><td> A1                              </td><td>必須選取 VM 根據 hello IO 的 hello;針對此用途保留 hello 預設值， </td><tr>
<tr><td> [新使用者名稱] 中             </td><td> localadmin                       </td><td> "admin" 在 Ubuntu 12.xx 以及更新版本中是保留的使用者名稱</td><tr>
<tr><td> 驗證         </td><td> 按一下核取方塊                 </td><td>檢查您是否 toosecure 使用 SSH 金鑰 </td><tr>
<tr><td> 憑證             </td><td> hello 公開金鑰憑證檔案名稱 </td><td> 使用 hello 先前產生的公開金鑰</td><tr>
<tr><td> 新密碼    </td><td> 強式密碼 </td><td> </td><tr>
<tr><td> 確認密碼    </td><td> 強式密碼 </td><td></td><tr>
</table>

輸入下列資訊在 hello 「 虛擬機器設定 」 畫面 #2 的 hello:

<table>
<tr><th>欄位名稱             </th><th> 欄位值                       </th><th> 備註                                 </th></tr>
<tr><td> 雲端服務    </td><td> 建立新的雲端服務    </td><td>雲端服務是一個運算如虛擬機器等資源的容器</td></tr>
<tr><td> 雲端服務 DNS 名稱    </td><td>ubuntu-template.cloudapp.net    </td><td>提供一個機器中立的負載平衡器名稱</td></tr>
<tr><td> [區域/同質群組/虛擬網路] </td><td>    美國西部    </td><td> 選取 web 應用程式存取 hello Cassandra 叢集中的區域</td></tr>
<tr><td>儲存體帳戶 </td><td>    使用預設值    </td><td>使用 hello 預設儲存體帳戶或特定區域的預先建立的儲存體帳戶</td></tr>
<tr><td>可用性集合 </td><td>    None </td><td>    保留為空白</td></tr>
<tr><td>端點    </td><td>使用預設值 </td><td>    使用 hello 預設 SSH 組態 </td></tr>
</table>

按一下向右箭號，保留 hello 預設值 #3 的 hello 畫面上，按 hello 「 檢查 」 按鈕 toocomplete hello VM 佈建程序。 請稍候幾分鐘 hello VM 與 hello 名稱 「 ubuntu-範本 」 應該是 「 執行 」 狀態。

### <a name="install-hello-necessary-software"></a>安裝必要軟體 hello
#### <a name="step-1-upload-tarballs"></a>步驟 1：上傳 tarball
使用 scp 或 pscp，複製 hello 先前下載的軟體太 ~ / [下載] 目錄使用下列命令格式的 hello:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gz localadmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
重複與 hello Cassandra 位元也 JRE hello 上述命令。

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>步驟 2： 準備 hello 目錄結構，並擷取 hello 封存
登入 hello VM 及建立 hello 目錄結構並擷取軟體做為進階使用者，使用下列的 hello bash 指令碼：

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


如果您將此指令碼貼到 vim 視窗時，請確定 tooremove hello 歸位字元傳回 ('\r 」) 使用下列命令的 hello:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>步驟 3：編輯 etc/profile
附加 hello 下列 hello 結尾：

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>步驟 4：安裝適用於實際執行系統的 JNA
使用 hello 下列命令順序： hello 下列命令將會安裝 jna 3.2.7.jar 和 jna-平台-3.2.7.jar too/usr/share.java 目錄 sudo apt-get 安裝 libjna java

在 $CASS_HOME/lib 目錄中建立符號連結，以便 Cassandra 啟動指令碼可以找到這些 jar：

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>步驟 5：設定 cassandra.yaml
編輯 cassandra.yaml 上 [我們將調整這 hello 實際佈建期間] 所有 hello 虛擬機器所需的每個 VM tooreflect 組態：

<table>
<tr><th>欄位名稱   </th><th> 值  </th><th>    備註 </th></tr>
<tr><td>cluster_name </td><td>    “CustomerService”    </td><td> 使用 hello 名稱反映您的部署</td></tr>
<tr><td>listen_address    </td><td>[保留為空白]    </td><td> 刪除 “localhost” </td></tr>
<tr><td>rpc_addres   </td><td>[保留為空白]    </td><td> 刪除 “localhost” </td></tr>
<tr><td>種子    </td><td>"10.1.2.4、10.1.2.6、10.1.2.8"    </td><td>指定為種子所有 hello IP 位址的清單。</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> 這是由用於 hello NetworkTopologyStrateg 推斷 hello 資料中心和 hello 的 hello VM 的機架</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>步驟 6： 擷取 hello VM 映像
登入 hello 使用 hello 主機名稱 (hk-ca-template.cloudapp.net) 和 hello SSH 私密金鑰先前建立的虛擬機器。 請參閱如何 tooUse Linux 的 Azure 上的 SSH 詳細說明如何在使用 toolog hello 命令 ssh 或 putty.exe 上。

執行下列一連串動作 toocapture hello 映像的 hello:

##### <a name="1-deprovision"></a>1.取消佈建
使用 hello 命令"sudo waagent-取消佈建 + 使用者 」 tooremove 虛擬機器執行個體的特定資訊。 請參閱 < >[如何 tooCapture Linux 虛擬機器](capture-image.md)tooUse 做為範本的詳細 hello 映像擷取程序上。

##### <a name="2-shutdown-hello-vm"></a>2： 關閉 hello VM
請確定該 hello 虛擬機器會反白顯示，然後按一下 hello 底部命令列中的 hello 關機連結。

##### <a name="3-capture-hello-image"></a>3： 擷取 hello 映像
請確定該 hello 虛擬機器會反白顯示，然後按一下 hello 底部命令列中的 hello 擷取連結。 在 hello 下一個畫面中提供的映像名稱 (例如 hk-cas-2-08-ub-14-04-2014071)、 適當的映像的描述，然後按一下 hello 「 檢查 」 標記 toofinish hello 擷取程序。

這需要幾秒鐘的時間和 hello 映像應出現在 hello 映像庫的 我的映像 > 一節。 hello 映像成功擷取後，就會自動刪除 hello 來源 VM。 

## <a name="single-region-deployment-process"></a>單一區域部署程序
**步驟 1： 建立虛擬網路 hello**登入 hello Azure 入口網站並建立虛擬網路 （傳統） 與 hello 屬性 hello 下表所示。 請參閱[建立使用 hello Azure 入口網站的虛擬網路 （傳統）](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) hello 程序的詳細步驟。      

<table>
<tr><th>VM 屬性名稱</th><th>值</th><th>備註</th></tr>
<tr><td>Name</td><td>vnet-cass-west-us</td><td></td></tr>
<tr><td>區域</td><td>美國西部</td><td></td></tr>
<tr><td>DNS 伺服器</td><td>None</td><td>請忽略此項，因為我們不使用 DNS 伺服器</td></tr>
<tr><td>位址空間</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>起始 IP</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

新增下列子網路的 hello:

<table>
<tr><th>名稱</th><th>起始 IP</th><th>CIDR</th><th>備註</th></tr>
<tr><td>Web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Hello web 伺服陣列的子網路</td></tr>
<tr><td>data</td><td>10.1.2.0</td><td>/24 (251)</td><td>Hello 資料庫節點的子網路</td></tr>
</table>

資料和網頁的子網路可以保護透過網路安全性群組 hello 涵蓋範圍，其中超出本文的範圍。  

**步驟 2： 佈建虛擬機器**使用先前建立的 hello 映像，我們將建立下列 hello 雲端中虛擬機器的 hello 伺服器 」 hk-c-svc-西 」 並將其繫結 toohello 各自的子網路如下所示：

<table>
<tr><th>機器名稱    </th><th>子網路    </th><th>IP 位址    </th><th>可用性集合</th><th>DC/機架</th><th>是否為種子？</th></tr>
<tr><td>hk-c1-west-us    </td><td>data    </td><td>10.1.2.4    </td><td>hk-c-aset-1    </td><td>dc=WESTUS 機架=rack1 </td><td>是</td></tr>
<tr><td>hk-c2-west-us    </td><td>data    </td><td>10.1.2.5    </td><td>hk-c-aset-1    </td><td>dc=WESTUS 機架=rack1    </td><td>否 </td></tr>
<tr><td>hk-c3-west-us    </td><td>data    </td><td>10.1.2.6    </td><td>hk-c-aset-1    </td><td>dc=WESTUS 機架=rack2    </td><td>是</td></tr>
<tr><td>hk-c4-west-us    </td><td>data    </td><td>10.1.2.7    </td><td>hk-c-aset-1    </td><td>dc=WESTUS 機架=rack2    </td><td>否 </td></tr>
<tr><td>hk-c5-west-us    </td><td>data    </td><td>10.1.2.8    </td><td>hk-c-aset-2    </td><td>dc=WESTUS 機架=rack3    </td><td>是</td></tr>
<tr><td>hk-c6-west-us    </td><td>data    </td><td>10.1.2.9    </td><td>hk-c-aset-2    </td><td>dc=WESTUS 機架=rack3    </td><td>否 </td></tr>
<tr><td>hk-c7-west-us    </td><td>data    </td><td>10.1.2.10    </td><td>hk-c-aset-2    </td><td>dc=WESTUS 機架=rack4    </td><td>是</td></tr>
<tr><td>hk-c8-west-us    </td><td>data    </td><td>10.1.2.11    </td><td>hk-c-aset-2    </td><td>dc=WESTUS 機架=rack4    </td><td>否 </td></tr>
<tr><td>hk-w1-west-us    </td><td>Web    </td><td>10.1.1.4    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/A</td></tr>
<tr><td>hk-w2-west-us    </td><td>Web    </td><td>10.1.1.5    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/A</td></tr>
</table>

建立的 Vm 清單上方的 hello 必須遵循的程序的 hello:

1. 在特定區域中建立空的雲端服務
2. 從 hello 先前擷取的映像建立 VM，並將它附加 toohello 先前; 建立的虛擬網路重複此步驟對於所有 hello Vm
3. 加入內部負載平衡器 toohello 雲端服務，並將它附加 toohello 「 資料 」 的子網路
4. 如先前所建立的每個 VM，新增 thrift 流量透過負載平衡集連接 toohello 先前建立內部負載平衡器的負載平衡端點

可以使用 Azure 傳統入口網站，執行上述程序的 hello使用 Windows 電腦 （使用的 Azure，如果您沒有存取 tooa Windows 電腦上的 VM），自動使用下列 PowerShell 指令碼 tooprovision hello 所有 8 部 Vm。

**清單 1：佈建虛擬機器的 PowerShell 指令碼**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**步驟 3：在每個 VM 上設定 Cassandra**

登入 hello VM，並執行下列 hello:

* 編輯 $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello 資料中心和機架屬性：
  
       dc =EASTUS, rack =rack1
* 編輯 cassandra.yaml tooconfigure 種子節點，如下所示：
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**步驟 4： 啟動 hello Vm，然後測試 hello 叢集**

登入的其中一個 hello 節點 （例如 hk-c1-西-我們） 並執行的 hello 遵循 hello 叢集命令 toosee hello 狀態：

       nodetool –h 10.1.2.4 –p 7199 status

您應該會看到 hello 顯示類似 toohello 其中一個下的 8 個節點叢集：

<table>
<tr><th>狀態</th><th>位址    </th><th>載入    </th><th>權杖    </th><th>擁有 </th><th>主機識別碼    </th><th>機架</th></tr>
<tr><th>UN    </td><td>10.1.2.4     </td><td>87.81 KB    </td><td>256    </td><td>38.0%    </td><td>Guid (已移除)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.5     </td><td>41.08 KB    </td><td>256    </td><td>68.9%    </td><td>Guid (已移除)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.6     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (已移除)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.7     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (已移除)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.8     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (已移除)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.9     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (已移除)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.10     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (已移除)</td><td>rack4</td></tr>
<tr><th>UN    </td><td>10.1.2.11     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (已移除)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>測試 hello 單一區域叢集
使用下列步驟 tootest hello 叢集 hello:

1. 使用 hello Powershell 命令 Get-azureinternalloadbalancer commandlet，（例如取得 hello hello 內部負載平衡器的 IP 位址 10.1.2.101)。 hello hello 命令語法如下所示： Get AzureLoadbalancer-ServiceName"hk-c-svc-西-我們"[顯示 hello hello 內部負載平衡器，以及其 IP 位址的詳細資料]
2. 登入 hello web 伺服陣列 (例如 hk-w1-西-us) 的 VM 使用 Putty 或 ssh
3. 執行 $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. 使用下列 CQL 命令 tooverify 如果 hello 叢集正在運作的 hello:
   
     CREATE KEYSPACE customers_ks WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');
   
     SELECT * FROM Customers;

您應該會看到類似下面其中一個 hello 顯示：

<table>
  <tr><th> customer_id </th><th> firstname </th><th> lastname </th></tr>
  <tr><td> 1 </td><td> John </td><td> Doe </td></tr>
  <tr><td> 2 </td><td> Jane </td><td> Doe </td></tr>
</table>

請注意在步驟 4 中建立該 hello keyspace SimpleStrategy 使用 replication_factor 為 3。 如果是單一資料中心部署，建議使用 SimpleStrategy，如果是多重資料中心部署，則建議使用 NetworkTopologyStrategy。 replication_factor 為 3 將針對節點失敗提供容錯。

## <a id="tworegion"> </a>多區域部署程序
會利用 hello 單一區域部署已完成，並重複相同的處理序的 hello 安裝 hello 第二個區域。 hello hello 單一和多個區域部署之間的主要差異是區域間通訊; hello VPN 通道設定即將 hello 網路安裝的開頭、 hello Vm 佈建及設定 Cassandra。

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>步驟 1： 建立 hello 虛擬網路在 hello 第 2 個區域
登入 hello Azure 傳統入口網站，並建立具有 hello 屬性顯示 hello 資料表中的虛擬網路。 請參閱[hello Azure 傳統入口網站中設定純雲端虛擬網路](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md)hello 程序的詳細步驟。      

<table>
<tr><th>屬性名稱    </th><th>值    </th><th>備註</th></tr>
<tr><td>名稱    </td><td>vnet-cass-east-us</td><td></td></tr>
<tr><td>區域    </td><td>美國東部</td><td></td></tr>
<tr><td>DNS 伺服器        </td><td></td><td>請忽略此項，因為我們不使用 DNS 伺服器</td></tr>
<tr><td>設定點對站 VPN</td><td></td><td>        略過此項</td></tr>
<tr><td>設定站台對站台 VPN</td><td></td><td>        略過此項</td></tr>
<tr><td>位址空間    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>起始 IP    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

新增下列子網路的 hello:

<table>
<tr><th>名稱    </th><th>起始 IP    </th><th>CIDR    </th><th>備註</th></tr>
<tr><td>Web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Hello web 伺服陣列的子網路</td></tr>
<tr><td>data    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Hello 資料庫節點的子網路</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>步驟 2：建立區域網路
Azure 虛擬網路中的區域網路是對應 tooa 遠端站台，包括私人雲端或另一個 Azure 區域的 proxy 位址空間。 這個 proxy 的位址空間是繫結的 tooa 遠端閘道的路由網路 toohello 直接網路目的地。 請參閱[設定 VNet tooVNet 連接](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)hello 需建立 VNET 對 VNET 連線。

建立 hello 下列詳細資料每兩個本機網路：

| 網路名稱 | VPN 閘道位址 | 位址空間 | 備註 |
| --- | --- | --- | --- |
| hk-lnet-map-to-east-us |23.1.1.1 |10.2.0.0/16 |建立 hello 區域網路時提供預留位置閘道位址。 建立 hello 閘道之後，會自動填入 hello 真實的閘道位址。 請確定 hello 位址空間完全相符 hello 個別遠端 VNET。在此情況下 hello VNET 中建立 hello 美東地區。 |
| hk-lnet-map-to-west-us |23.2.2.2 |10.1.0.0/16 |建立 hello 區域網路時提供預留位置閘道位址。 建立 hello 閘道之後，會自動填入 hello 真實的閘道位址。 請確定 hello 位址空間完全相符 hello 個別遠端 VNET。在此情況下 hello VNET 中建立 hello 美國西部地區。 |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>步驟 3： 對應網路 「 區域 」 toohello 個別 Vnet
從 hello Azure 傳統入口網站，選取每個 vnet、 按一下 [設定]、 檢查 「 連線 toohello 本機網路 」，然後選取 hello 區域網路，每個 hello 下列詳細資料：

| 虛擬網路 | 區域網路 |
| --- | --- |
| hk-vnet-west-us |hk-lnet-map-to-east-us |
| hk-vnet-east-us |hk-lnet-map-to-west-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>步驟 4：在 VNET1 和 VNET2 上建立閘道
從這兩個 hello 虛擬網路的 hello 儀表板，按一下 建立閘道，其會觸發 hello VPN 閘道的佈建程序。 幾分鐘的時間 hello 儀表板的每個虛擬網路之後應該會顯示 hello 實際的閘道位址。

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>步驟 5: Hello 個別 「 閘道 」 位址更新 「 本機 」 網路
編輯兩個 hello 區域網路 tooreplace hello 預留位置閘道 IP 位址與 hello 實際 IP 位址的 hello 只佈建閘道。 使用下列對應的 hello:

<table>
<tr><th>區域網路    </th><th>虛擬網路閘道</th></tr>
<tr><td>hk-lnet-map-to-east-us </td><td>hk-vnet-west-us 的閘道</td></tr>
<tr><td>hk-lnet-map-to-west-us </td><td>hk-vnet-east-us 的閘道</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>步驟 6： 更新 hello 共用的金鑰
使用下列 Powershell 指令碼 tooupdate hello IPSec 金鑰的每個 VPN 閘道 [使用 hello 起見索引鍵的兩個 hello 閘道] 的 hello： 集 AzureVNetGatewayKey VNetName hk-vnet-東部-我們-LocalNetworkSiteName hk-lnet-map-to-west-us-SharedKey D9E76BKK設定 AzureVNetGatewayKey-VNetName hk-vnet-西-我們-LocalNetworkSiteName hk-lnet-map-to-east-us-SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>步驟 7： 建立 hello VNET 對 VNET 連線
Hello Azure 傳統入口網站，從使用這兩個 hello 虛擬網路 tooestablish 閘道對閘道連線的 hello 」 儀表板 功能表。 使用 hello 底部工具列中的 hello [連線] 功能表項目。 幾分鐘後 hello 儀表板應以圖形方式顯示 hello 連接詳細資料。

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>步驟 8： 在區域 #2 中建立 hello 虛擬機器
建立 hello Ubuntu 映像，依據相同的步驟，或複製 hello 映像 VHD 檔案 toohello Azure 儲存體帳戶位於區域 #2 中的下列 hello 區域 #1 部署中所述，建立 hello 映像。 使用此映像，並建立下列清單中的虛擬機器到新的雲端服務 hk-c-svc-東部-我們 hello:

| 機器名稱 | 子網路 | IP 位址 | 可用性集合 | DC/機架 | 是否為種子？ |
| --- | --- | --- | --- | --- | --- |
| hk-c1-east-us |data |10.2.2.4 |hk-c-aset-1 |dc=EASTUS 機架=rack1 |是 |
| hk-c2-east-us |data |10.2.2.5 |hk-c-aset-1 |dc=EASTUS 機架=rack1 |否 |
| hk-c3-east-us |data |10.2.2.6 |hk-c-aset-1 |dc=EASTUS 機架=rack2 |是 |
| hk-c5-east-us |data |10.2.2.8 |hk-c-aset-2 |dc=EASTUS 機架=rack3 |是 |
| hk-c6-east-us |data |10.2.2.9 |hk-c-aset-2 |dc=EASTUS 機架=rack3 |否 |
| hk-c7-east-us |data |10.2.2.10 |hk-c-aset-2 |dc=EASTUS 機架=rack4 |是 |
| hk-c8-east-us |data |10.2.2.11 |hk-c-aset-2 |dc=EASTUS 機架=rack4 |否 |
| hk-w1-east-us |Web |10.2.1.4 |hk-w-aset-1 |N/A |N/A |
| hk-w2-east-us |Web |10.2.1.5 |hk-w-aset-1 |N/A |N/A |

後續 hello 相同為區域 #1 的指示，但使用 10.2.xxx.xxx 位址空間。

### <a name="step-9-configure-cassandra-on-each-vm"></a>步驟 9：在每個 VM 上設定 Cassandra
登入 hello VM，並執行下列 hello:

1. 編輯 $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello 資料中心和機架屬性 hello 格式： dc = EASTUS 機架 = rack1
2. 編輯 cassandra.yaml tooconfigure 種子節點： 之種子的位置:"10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>步驟 10：啟動 Cassandra
登入每個 VM 並啟動 Cassandra hello 背景中執行下列命令的 hello: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>測試 hello 多區域叢集
現在 Cassandra 已部署的 too16 節點含有 8 個節點中每個 Azure 區域。 這些節點位於相同叢集必定 hello 一般的叢集名稱和 hello 種子節點組態的 hello。 使用下列程序 tootest hello 叢集 hello:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>步驟 1： 取得 hello 內部負載平衡器 IP 這兩個 hello 地區使用 PowerShell
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-west-us"
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-east-us"  
  
    請注意 hello IP 位址 (例如西-10.1.2.101，東部-10.2.2.101) 顯示。

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>步驟 2: Hello 西區域中執行 hello 下列登入 hk-w1-西-我們之後
1. 執行 $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. 執行下列 CQL 命令 hello:
   
     CREATE KEYSPACE customers_ks   WITH REPLICATION = { 'class' : 'NetworkToplogyStrategy', 'WESTUS' : 3, 'EASTUS' : 3};   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

您應該會看到類似下面其中一個 hello 顯示：

| customer_id | firstname | lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>步驟 3： 執行之後登入 hk-w1-東部-我們 hello 東部地區 hello 下列：
1. 執行 $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. 執行下列 CQL 命令 hello:
   
     USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

您應該會看到相同顯示 hello 西區域中所看到的 hello:

| customer_id | firstname | lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

執行幾個其他的插入，並查看所取得複寫的 toowest-我們 hello 叢集的一部分。

## <a name="test-cassandra-cluster-from-nodejs"></a>透過 Node.js 測試 Cassandra 叢集
先前使用其中一種 hello Linux Vm 建立 hello"web"層中，我們將會執行簡單的 Node.js 指令碼 tooread hello 之前插入資料

**步驟 1：安裝 Node.js 和 Cassandra 用戶端**

1. 安裝 Node.js 和 npm
2. 使用 npm 安裝節點套件"cassandra-client"
3. 執行下列指令碼在 hello 殼層提示字元會顯示 hello 的 hello 擷取資料的 json 字串 hello:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>結論
Microsoft Azure 是彈性的平台，可讓 hello Microsoft 以及開放原始碼軟體執行，此練習中所示。 高可用性的 Cassandra 叢集可以部署在單一資料中心透過 hello hello 叢集節點散佈跨多個容錯網域中。 您也可以跨越多個地理位置遙遠的 Azure 區域部署 Cassandra 叢集做為災害防禦系統。 Azure 和 Cassandra 一起啟用 hello 建構可高度擴充、 高可用性和災害復原的雲端服務所需的今天的網際網路規模服務。  

## <a name="references"></a>參考
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

