## <a name="load-balancer-differences"></a>負載平衡器的差異

有不同的選項 toodistribute 網路流量使用 Microsoft Azure。 這些選項的運作方式彼此間會有差異，其具備不同的功能組合並支援不同的案例。 它們每個都可單獨使用，或組合在一起。

* **Azure 負載平衡器**hello 傳輸層 (hello OSI 網路參考堆疊中的層級 4) 在運作。 它提供網路層級的流量分配跨 hello 中執行的應用程式的執行個體相同的 Azure 資料中心。
* **應用程式閘道**在 hello 應用程式層級 (hello OSI 網路參考堆疊中的圖層 7) 的運作方式。 它會充當反向 proxy 服務時，終止 hello 用戶端連線，並轉送要求 tooback 端端點。
* **Traffic Manager**在 hello DNS 層級運作。  它會使用 DNS 回應 toodirect 使用者流量分散 tooglobally 端點。 用戶端，直接連接 toothose 端點。

hello 下表摘要說明每個服務所提供的 hello 功能：

| 服務 | Azure Load Balancer | 應用程式閘道 | 流量管理員 |
| --- | --- | --- | --- |
| Technology |傳輸層級 (第 4 層) |應用程式層級 (第 7 層) |DNS 層級 |
| 支援的應用程式通訊協定 |任意 |HTTP、HTTPS 和 WebSockets |任意 (HTTP 端點是端點監視所需的必要項目) |
| 端點 |Azure VM 和雲端服務角色執行個體 |任何 Azure 內部 IP 位址、公用網際網路 IP 位址、Azure VM 或 Azure 雲端服務 |Azure VM、雲端服務、Azure Web Apps 和外部端點 |
| Vnet 支援 |可用於網際網路面向和內部 (Vnet) 應用程式 |可用於網際網路面向和內部 (Vnet) 應用程式 |只支援網際網路面向的應用程式 |
| 端點監視 |透過探查支援 |透過探查支援 |透過 HTTP/HTTPS GET 支援 |

Azure 負載平衡器和應用程式閘道路由網路流量 tooendpoints 但具有不同的使用案例 toowhich 流量 toohandle。 hello 表有助於了解 hello 差異 hello 兩個負載平衡器：

| 類型 | Azure Load Balancer | 應用程式閘道 |
| --- | --- | --- |
| 通訊協定 |UDP/TCP |HTTP、HTTPS 和 WebSockets |
| IP 保留區 |支援 |不支援 |
| 負載平衡模式 |5 個 Tuple (來源 IP、來源連接埠、目的地 IP、目的地連接埠、通訊協定類型) |循環配置資源<br>根據 URL 路由 |
| 負載平衡模式 (來源 IP / 相黏工作階段) |2 個 Tuple (來源 IP 和目的地 IP)、3 個 Tuple (來源 IP、目的地 IP 和連接埠)。 可相應增加或減少根據 hello 的虛擬機器的數目 |以 Cookie 為基礎的同質性<br>根據 URL 路由 |
| 健康狀態探查 |預設值︰探查間隔 - 15 秒。 不進入輪替︰2 個連續的失敗。 支援使用者定義的探查 |閒置探查間隔 30 秒。 在 5 個連續的即時流量失敗或處於閒置模式的單一探查失敗之後結束。 支援使用者定義的探查 |
| SSL 卸載 |不支援 |支援 |
| URL 型路由 | 不支援 | 支援|
| SSL 原則 | 不支援 | 支援|
