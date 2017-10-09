* **PolicyBased:** PolicyBased Vpn 之前已呼叫 hello 傳統部署模型中的靜態路由閘道。 原則式 Vpn 會加密，並直接透過 IPsec 通道的封包根據 hello 搭配 hello 組合的位址前置詞，您的內部部署網路與 hello Azure VNet 之間設定 IPsec 原則。 hello 原則 （或傳輸選取器） 通常定義為存取清單中 hello VPN 裝置組態。 hello PolicyBased VPN 類型的值是*PolicyBased*。 使用時 PolicyBased VPN，請注意下列限制的 hello:
  
  * PolicyBased Vpn 可以**只**hello 基本閘道 SKU 上使用。 這個 VPN 類型與其他閘道 SKU 不相容。
  * 使用 PolicyBased VPN 時，您只能有 1 個通道。
  * 您只能將 PolicyBased VPN 用於 S2S 連線，而且僅限用於特定組態。 大多數「VPN 閘道」組態都需要一個 RouteBased VPN。
* **RouteBased**: RouteBased Vpn 之前已呼叫 hello 傳統部署模型中的動態路由閘道。 RouteBased Vpn hello IP 轉送或路由資料表 toodirect 封包傳送至其相對應的通道介面中使用 「 路由 」。 然後 hello 通道介面加密或解密出 hello 通道 hello 封包。 hello 原則 （或傳輸選取器），針對設定為任何-到-any RouteBased Vpn （或萬用字元）。 hello RouteBased VPN 類型的值是*RouteBased*。

