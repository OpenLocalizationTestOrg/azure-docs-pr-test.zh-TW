---
title: "在 Azure 中 aaaUsing 負載平衡服務 |Microsoft 文件"
description: "此教學課程會示範如何 toocreate 案例中，使用 hello Azure 負載平衡的 portfolio： 流量管理員、 應用程式閘道和負載平衡器。"
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>在 Azure 中使用負載平衡服務

## <a name="introduction"></a>簡介

Microsoft Azure 提供多個服務，可管理分配網路流量和負載平衡的方式。 您可以個別使用這些服務，或結合其方法，請根據您的需求，toobuild hello 最好的解決方案。

在本教學課程中，我們先定義客戶使用案例，看到如何可以設為更強固和高效能使用下列 Azure 負載平衡 portfolio hello： 流量管理員、 應用程式閘道和負載平衡器。 我們提供逐步指示，建立部署的地理備援、 分散流量 tooVMs 且可協助您管理不同類型的要求。

在概念層級中，每個服務扮演 hello 負載平衡的階層中不同角色。

* **流量管理員**提供全域 DNS 負載平衡。 它會查看連入 DNS 要求和回應狀況良好的端點，根據 hello 選取路由原則 hello 客戶。 路由方法的選項如下︰
  * 效能路由 toosend hello 要求者 toohello 最靠近的端點依據延遲。
  * 路由 toodirect 所有流量 tooan 端點，與其他端點做為備份的優先權。
  * 加權的循環路由，這會根據 hello 加權指派 tooeach 端點的流量。

  hello 用戶端會直接連接 toothat 端點。 Azure Traffic Manager 會偵測端點狀況不良，然後重新導向 hello 用戶端 tooanother 狀況良好的執行個體。 請參閱太[Azure Traffic Manager 文件](traffic-manager-overview.md)toolearn 更多關於 hello 服務。
* **應用程式閘道**會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。 它可讓客戶 toooptimize web 伺服陣列產能卸載 CPU 運算密集 SSL 終止 toohello 應用程式閘道。 其他 7 層路由功能包括循環配置資源發佈的連入流量，cookie 為基礎的工作階段親和性，路徑為基礎的路由 URL，和 hello 能力 toohost 背後的單一應用程式閘道的多個網站。 應用程式閘道可以設定為連結網際網路的閘道、內部專用閘道或兩者混合。 應用程式閘道完全由 Azure 管理、可調整且可用性極高。 它提供一組豐富的診斷和記錄功能，很好管理。
* **負載平衡器**是 hello Azure SDN 堆疊，提供高效能、 低延遲第 4 層負載平衡服務所有 UDP 和 TCP 通訊協定不可或缺的一部分。 它會管理輸入及輸出連線。 您可以設定公用和內部負載平衡的端點，並定義規則 toomap 輸入連線 tooback 後端集區目的地使用 TCP 和 HTTP 健全狀況探查選項 toomanage 服務可用性。

## <a name="scenario"></a>案例

在此範例案例中，我們使用簡單的網站提供兩種類型的內容︰影像及動態呈現的網頁。 hello 網站必須是地理備援，並且應該提供其使用者 hello 最接近 （最低延遲） 從位置 toothem。 hello 應用程式開發人員決定，比對任何 Url hello 模式映像 / * 來自 vm 的不同 hello 其餘 hello web 伺服陣列的專用集區。

此外，提供 hello 動態內容的 hello 預設 VM 集區必須裝載在高可用性叢集 tootalk tooa 後端資料庫。 hello 整個部署設定透過 Azure 資源管理員。

使用流量管理員、 應用程式閘道和負載平衡器可讓此網站 tooachieve 這些設計目標：

* **多個地理備援性**： 如果一個區域發生問題，Traffic Manager 路由流量順暢地 toohello hello 應用程式擁有者任何介入最接近的區域。
* **降低延遲**： 因為 Traffic Manager 會自動引導 hello 客戶 toohello 最接近的區域、 hello 客戶遇到的延遲較低，當要求 hello 網頁內容。
* **獨立的延展性**: hello web 應用程式工作負載分開的內容類型，因為 hello 應用程式擁有者可以調整 hello 要求工作負載彼此獨立。 應用程式閘道可確保 hello 流量會根據指定的 hello 路由的 toohello 右集區規則和 hello hello 應用程式的健全狀況。
* **內部負載平衡**: hello 資料庫使用中且狀況良好端點公開的 toohello 應用程式只是前面 hello 高可用性叢集，因為的負載平衡器。 此外，資料庫管理員可以最佳化 hello 工作負載分散 hello 前端應用程式的獨立 hello 叢集的主動和被動複本。 負載平衡器會提供連接 toohello 高可用性叢集，而且可確保只有狀況良好的資料庫接收連線要求。

hello 下圖顯示此案例的 hello 架構：

![負載平衡架構的圖表](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> 這個範例是其中一個 hello 負載平衡服務，Azure 提供許多可能的設定。 流量管理員、 應用程式閘道和負載平衡器可以混合和相符的 toobest 符合您負載平衡的需求。 例如，如果 SSL 卸載或第 7 層處理並非必要，則負載平衡器可用以取代應用程式閘道。

## <a name="setting-up-hello-load-balancing-stack"></a>Hello 負載平衡堆疊設定

### <a name="step-1-create-a-traffic-manager-profile"></a>步驟 1︰建立流量管理員設定檔

1. 在 hello Azure 入口網站，按一下 **新增**，，然後搜尋 hello marketplace 中的 「 流量管理員設定檔 」。
2. 在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中，輸入下列基本資訊的 hello:

  * **名稱**：為您的流量管理員設定檔提供一個 DNS 首碼名稱。
  * **路由方法**： 選取 hello 流量路由方法原則。 如需 hello 方法的詳細資訊，請參閱[有關 Traffic Manager 流量路由方式](traffic-manager-routing-methods.md)。
  * **訂用帳戶**： 選取包含 hello 設定檔的 hello 訂用帳戶。
  * **資源群組**: hello 選取資源群組含有 hello 設定檔。 可以是新的或現有的資源群組。
  * **資源群組位置**: Traffic Manager 服務正在全域和未繫結 tooa 位置。 不過，您必須指定 hello 群組 hello 與 hello Traffic Manager 設定檔相關聯的中繼資料所在的區域。 這個位置 hello hello 設定檔的執行階段可用性沒有任何影響。

3. 按一下**建立**toogenerate hello Traffic Manager 設定檔。

  ![[建立流量管理員] 刀鋒視窗](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>步驟 2： 建立 hello 應用程式閘道

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 **新增** > **網路** > **應用程式閘道**。
2. 輸入下列 hello 應用程式閘道的相關基本資訊的 hello:

  * **名稱**: hello hello 應用程式閘道名稱。
  * **SKU 大小**: hello hello 應用程式閘道，可做為小、 中或大的大小。
  * **執行個體計數**: hello 的執行個體的數目，從 2 到 10 的值。
  * **資源群組**: hello 保存 hello 應用程式閘道的資源群組。 它可以是現有的或新的資源群組。
  * **位置**: hello 應用程式閘道 hello 相同的 hello 區域為 hello 資源群組的位置。 hello 位置很重要，因為 hello 虛擬網路與公用 IP 必須在 hello 與 hello 閘道相同的位置。
3. 按一下 [確定] 。
4. 定義 hello 虛擬網路、 子網路、 前端的 IP 和 hello 應用程式閘道的接聽程式組態。 在此案例中，hello 前端 IP 位址是**公用**，可讓它 toobe 稍後新增為端點 toohello Traffic Manager 設定檔。
5. 使用下列選項的 hello 的其中一個設定 hello 接聽程式：
    * 如果您使用 HTTP 時，就無須 tooconfigure。 按一下 [確定] 。
    * 如果您使用 HTTPS，則需要設定進一步的設定。 請參閱太[建立應用程式閘道](../application-gateway/application-gateway-create-gateway-portal.md)開始於步驟 9。 當您完成 hello 組態時，按一下 **確定**。

#### <a name="configure-url-routing-for-application-gateways"></a>設定應用程式閘道的 URL 路由

當您選擇的後端集區時，應用程式閘道設定與路徑規則會接受加法 tooround 環散佈 hello 要求 URL 的路徑模式。 在此案例中，我們新增路徑為基礎的規則 toodirect 任何 URL 與"/images/\*"toohello 映像的伺服器集區。 如需有關設定 URL 路徑為基礎的路由為應用程式的閘道，請參閱太[建立路徑為基礎的應用程式閘道規則](../application-gateway/application-gateway-create-url-route-portal.md)。

![應用程式閘道 Web 層圖表](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. 從您的資源群組移 toohello hello 在 hello 前面一節中所建立的應用程式閘道執行個體。
2. 在下**設定**，選取**後端集區**，然後選取**新增**tooadd hello 想 tooassociate 與 hello web 層後端集區的 Vm。
3. 在 hello**新增後端集區**刀鋒視窗中，輸入 hello hello 後端集區名稱和所有 hello IP 位址位於 hello 集區中的 hello 機器。 在此案例中，我們會連接兩個虛擬機器的後端伺服器集區。

  ![應用程式閘道「新增後端集區」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. 在下**設定**hello 應用程式閘道，請選取**規則**，然後按一下hello**路徑基本**按鈕 tooadd 規則。

  ![應用程式閘道規則「路徑型」按鈕](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. 在 hello**加入路徑為基礎的規則**刀鋒視窗中，可藉由提供下列資訊的 hello 設定 hello 規則。

   基本設定：

   + **名稱**: hello 存取 hello 入口網站中的 hello 規則的好記的名稱。
   + **接聽程式**: hello 規則使用的 hello 接聽程式。
   + **預設 後端集區**: hello 後端集區 toobe 搭配 hello 預設規則。
   + **預設的 HTTP 設定**: hello HTTP 設定 toobe 搭配 hello 預設規則。

   路徑型規則：

   + **名稱**: hello hello 路徑為基礎的規則的好記的名稱。
   + **路徑**: hello 路徑規則用於將流量轉送。
   + **後端集區**: hello 搭配此規則的後端集區 toobe。
   + **HTTP 設定**: hello HTTP 設定 toobe 搭配此規則。

   > [!IMPORTANT]
   > 路徑︰有效的路徑必須以 "/" 開頭。 hello 萬用字元"\*」 只能出現在 hello 結束。 有效範例包括 /xyz、/xyz\* 或 /xyz/\*。

   ![應用程式閘道器「新增路徑型規則」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>步驟 3： 新增應用程式閘道 toohello 流量管理員端點

在此案例中，Traffic Manager 會是位於不同的區域中的連接的 tooapplication 閘道 （如 hello 先前步驟中所設定）。 現在 hello 應用程式閘道的設定，hello 下一個步驟是 tooconnect 它們 tooyour Traffic Manager 設定檔。

1. 開啟流量管理員設定檔。 在您的資源群組或搜尋 hello hello Traffic Manager 設定檔的名稱，尋找 toodo**所有資源**。
2. Hello 左窗格中，選取**端點**，然後按一下**新增**tooadd 端點。

  ![流量管理員端點「新增」按鈕](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. 在 hello**加入端點**刀鋒視窗中，輸入 hello 下列資訊來建立端點：

  * **型別**： 選取 hello tooload 平衡的端點類型。 在此案例中，選取**Azure 端點**因為我們是否連線它 toohello 應用程式閘道器執行個體先前設定的設定。
  * **名稱**： 輸入 hello hello 端點名稱。
  * **目標資源類型**： 選取**公用 IP 位址**然後在**目標資源**，選取 hello 的 hello 先前設定的應用程式閘道的公用 IP。

   ![流量管理員「新增端點」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. 現在您可以藉由存取與您的 Traffic Manager 設定檔的 DNS hello 測試您的設定 (在此範例中： TrafficManagerScenario.trafficmanager.net)。 您可以重送要求、 啟動或關閉 Vm 和 web 伺服器在不同的區域中建立和變更 hello Traffic Manager 設定檔設定 tootest 設定。

### <a name="step-4-create-a-load-balancer"></a>步驟 4：建立負載平衡器

在此案例中，負載平衡器會將來自 hello web 層 toohello 資料庫高可用性叢集內的連接。

如果您的資料庫高可用性叢集使用 SQL Server AlwaysOn，請參閱太[設定一或多個永遠在可用性群組接聽程式](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md)如需逐步指示。

如需有關如何設定內部負載平衡器的詳細資訊，請參閱[hello Azure 入口網站中建立內部負載平衡器](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)。

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 **新增** > **網路** > **負載平衡器**。
2. 在 hello**建立負載平衡器**刀鋒視窗中，選擇您的負載平衡器的名稱。
3. 設定 hello**類型**太**內部**，然後選擇 hello 適當的虛擬網路和子網路中的 hello 負載平衡器 tooreside。
4. 在 [IP 位址指派] 下，選取 [動態] 或 [靜態]。
5. 在下**資源群組**，選擇 hello hello 負載平衡器的資源群組。
6. 在下**位置**，選擇 hello hello 負載平衡器的適當區域。
7. 按一下**建立**toogenerate hello 負載平衡器。

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>連接後端資料庫層 toohello 負載平衡器

1. 從資源群組中，尋找 hello 先前步驟中所建立的 hello 負載平衡器。
2. 在下**設定**，按一下 **後端集區**，然後按一下**新增**tooadd 後端集區。

  ![負載平衡器「新增後端集區」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. 在 hello**新增後端集區**刀鋒視窗中，輸入 hello hello 後端集區名稱。
4. 加入個別的機器或可用性集 toohello 後端集區。

#### <a name="configure-a-probe"></a>設定探查

1. 在您的負載平衡器下**設定**，選取**探查**，然後按一下**新增**tooadd 探查。

 ![負載平衡器「新增探查」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. 在 hello**新增探查**刀鋒視窗中，輸入 hello hello 探查的名稱。
3. 選取 hello**通訊協定**hello 探查。 針對資料庫，您可能想要 TCP 探查，而不是 HTTP 探查。 深入了解負載平衡器探查 toolearn 參照太[了解負載平衡器探查](../load-balancer/load-balancer-custom-probe-overview.md)。
4. 輸入 hello**連接埠**的您用來存取 hello 探查的資料庫 toobe。
5. 在下**間隔**，指定 tooprobe hello 應用程式的頻率。
6. 在下**狀況不良閾值**，指定連續探查失敗發生的 hello 後端 VM toobe 被視為狀況不良的 hello 數目。
7. 按一下**確定**toocreate hello 探查。

#### <a name="configure-hello-load-balancing-rules"></a>設定 hello 負載平衡規則

1. 在下**設定**您負載平衡器中，選取**負載平衡規則**，然後按一下**新增**toocreate 規則。
2. 在 hello**新增負載平衡規則**刀鋒視窗中，輸入 hello**名稱**hello 負載平衡規則。
3. 選擇 hello**前端 IP 位址**hello 的負載平衡器，**通訊協定**，和**連接埠**。
4. 在下**後端連接埠**，指定 hello 連接埠 toobe hello 後端集區中使用。
5. 選取 hello**後端集區**和 hello**探查**在 hello 上一個步驟 tooapply hello 規則所建立。
6. 在下**工作階段持續性**，選擇您要如何 hello 工作階段 toopersist。
7. 在下**閒置逾時**，指定 hello 前的閒置逾時分鐘數。
8. 在 [浮點 IP] 下，選取 [停用] 或 [啟用]。
9. 按一下**確定**toocreate hello 規則。

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>步驟 5： 連接的 web 層 Vm toohello 負載平衡器

現在我們在 hello web 層 Vm 的任何資料庫連接執行的應用程式設定 hello IP 位址和負載平衡器前端連接埠。 此設定是在這些 Vm 執行的特定 toohello 應用程式。 tooconfigure hello 目的地 IP 位址和連接埠，請參閱 toohello 應用程式文件。 toofind hello IP 位址的 hello 前端 hello Azure 入口網站中移 toohello 前端 IP 集區上 hello**負載平衡器設定**刀鋒視窗。

![負載平衡器「前端 IP 集區」瀏覽窗格](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>後續步驟

* [流量管理員概觀](traffic-manager-overview.md)
* [應用程式閘道概觀](../application-gateway/application-gateway-introduction.md)
* [Azure 負載平衡器概觀](../load-balancer/load-balancer-overview.md)
