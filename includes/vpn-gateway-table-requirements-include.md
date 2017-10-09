下列表格列出 hello 需求 PolicyBased 和 RouteBased VPN 閘道的 hello。 此表格適用於 tooboth hello 資源管理員和傳統部署模型。 Hello 傳統的模型，PolicyBased VPN 閘道是靜態閘道，為 hello 相同，並以路由為基礎的閘道是 hello 相同為動態閘道。

|  | **PolicyBased 基本 VPN 閘道** | **RouteBased 基本 VPN 閘道** | **RouteBased 標準 VPN 閘道** | **RouteBased 高效能 VPN 閘道** |
| --- | --- | --- | --- | --- |
| **站對站連線能力 (S2S)** |PolicyBased VPN 組態 |RouteBased VPN 組態 |RouteBased VPN 組態 |RouteBased VPN 組態 |
| **點對站連線 (P2S)** |不支援 |支援 (可與 S2S 並存) |支援 (可與 S2S 並存) |支援 (可與 S2S 並存) |
| **驗證方法** |預先共用金鑰 |S2S 連線的預先共用金鑰，P2S 連線的憑證 |S2S 連線的預先共用金鑰，P2S 連線的憑證 |S2S 連線的預先共用金鑰，P2S 連線的憑證 |
| **S2S 連接的數目上限** |1 |10 |10 |30 |
| **P2S 連接的數目上限** |不支援 |128 |128 |128 |
| **作用中路由支援 (BGP)** |不支援 |不支援 |支援 |支援 |

