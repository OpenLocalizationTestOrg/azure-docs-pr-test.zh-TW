### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>是否所有的 Azure VPN 閘道 SKU 都支援自訂 IPsec/IKE 原則？
Azure **VpnGw1、VpnGw2、VpnGw3、標準**和**高效能** VPN 閘道可支援自訂 IPsec/IKE 原則。 **基本** SKU。

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>可以對連線指定多少個原則？
每個給定的連線只能指定***一個***原則組合。

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>可以對連線指定部分原則嗎？ (例如，只指定 IKE 演算法，而不指定 IPsec)
不行，您必須同時對 IKE (主要模式) 和 IPsec (快速模式) 指定所有的演算法和參數。 系統不允許只指定一部分原則。

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Hello 演算法和支援 hello 自訂原則中的索引鍵強度為何？
hello 下表列出 hello 支援密碼編譯演算法和金鑰長度可設定 hello 客戶。 每個欄位都必須選取一個選項。

| **IPsec/IKEv2**  | **選項**                                                                   |
| ---              | ---                                                                           |
| IKEv2 加密 | AES256、AES192、AES128、DES3、DES                                             |
| IKEv2 完整性  | SHA384、SHA256、SHA1、MD5                                                     |
| DH 群組         | DHGroup24、ECP384、ECP256、DHGroup14 (DHGroup2048)、DHGroup2、DHGroup1、無 |
| IPsec 加密 | GCMAES256、GCMAES192、GCMAES128、AES256、AES192、AES128、DES3、DES、無      |
| IPsec 完整性  | GCMAES256、GCMAES192、GCMAES128、SHA256、SHA1、MD5                            |
| PFS 群組        | PFS24、ECP384、ECP256、PFS2048、PFS2、PFS1、無                              |
| QM SA 存留期   | 秒 (整數；**最小 300**/預設值 27000 秒)<br>KB 數 (整數；**最小 1024**/預設值 102400000 KB 數)           |
| 流量選取器 | UsePolicyBasedTrafficSelectors ($True/$False；預設為 $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 是 hello 相同 Diffie-hellman 群組為**14** IKE 和 IPsec PFS。 請參閱[Diffie-hellman 群組](#DH)hello 完成對應。
> 2. 您必須指定 GCMAES 演算法 hello IPsec 加密及完整性 GCMAES 演算法和金鑰長度相同。
> 3. IKEv2 主要模式 SA 存留期會固定為 28,800 秒 hello Azure VPN 閘道
> 4. QM SA 存留期是選擇性參數。 如果未指定，則會使用預設值 27,000 秒 (7.5 小時) 和 102400000 KB (102 GB)。
> 5. UsePolicyBasedTrafficSelector 是 hello 連線選項參數。 Hello 下一個常見問題集，請參閱 「 UsePolicyBasedTrafficSelectors"的項目

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>所有項目需要 toomatch 之間 hello Azure VPN 閘道原則和我的內部部署 VPN 裝置組態嗎？
在內部部署 VPN 裝置組態必須符合或包含下列演算法 hello 和您在指定的參數 hello Azure IPsec/IKE 原則：

* IKE 加密演算法
* IKE 完整性演算法
* DH 群組
* IPsec 加密演算法
* IPsec 完整性演算法
* PFS 群組
* 流量選取器 (*)

只有本機規格 hello SA 存留期，但不需要 toomatch。

如果您啟用**UsePolicyBasedTrafficSelectors**，需要您的 VPN 裝置具有比對具有所有您在內部部署網路 （區域網路閘道） 的前置詞從 hello 的組合所定義的傳輸選取器的 hello tooensureAzure 虛擬網路首碼，而不是任何為 any。 例如，如果您在內部部署網路的前置詞為 10.1.0.0/16 和 10.2.0.0/16，而且您虛擬網路的前置詞為 192.168.0.0/16 和 172.16.0.0/16，您需要下列流量選取器 toospecify hello:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

請參閱太[連接多個內部部署以原則為基礎的 VPN 裝置](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md)如需有關如何 toouse 此選項。

### <a name ="DH"></a>支援的 Diffie-Hellman 群組為何？
hello 下表列出支援 hello Diffie-hellman 群組 IKE (DHGroup) 和 IPsec (PFSGroup):

| **Diffie-Hellman 群組**  | **DHGroup**              | **PFSGroup** | **金鑰長度** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | 768 位元 MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024 位元 MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048 位元 MODP  |
| 19                        | ECP256                   | ECP256       | 256 位元 ECP    |
| 20                        | ECP384                   | ECP284       | 384 位元 ECP    |
| 24                        | DHGroup24                | PFS24        | 2048 位元 MODP  |
|                           |                          |              |                |

請參閱太[RFC3526](https://tools.ietf.org/html/rfc3526)和[RFC5114](https://tools.ietf.org/html/rfc5114)如需詳細資訊。

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Hello 自訂原則是否取代 hello IPsec/IKE 原則預設 Azure VPN 閘道？
是，一旦在連接上指定自訂原則，Azure VPN 閘道只會使用 hello 原則 hello 連線時，同時為 IKE 啟動器和 IKE 回應。

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>如果我移除自訂 IPsec/IKE 原則時，不會 hello 連線成為未受保護？
否，hello 連線將仍然會受到 IPsec/IKE。 一旦您從連線移除 hello 自訂原則，hello Azure VPN 閘道將還原後 toohello [IPsec/IKE 提案徵求書的預設清單](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md)和重新啟動 hello 一次與內部部署 VPN 裝置的 IKE 信號交換。

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>新增或更新 IPsec/IKE 原則是否會中斷 VPN 連線？
是，它可能會導致小中斷 （幾秒鐘） 因為 hello Azure VPN 閘道會終止 hello 現有連接並重新啟動 hello IKE 交握 toore-建立 hello IPsec 通道以 hello 新的密碼編譯演算法和參數。 請確定您的內部部署 VPN 裝置也設有 hello 比對演算法和金鑰長度 toominimize hello 中斷。

### <a name="can-i-use-different-policies-on-different-connections"></a>是否可以對不同連線使用不同原則？
是。 自訂原則會按照個別連線來套用。 您可以對不同連線建立和套用不同的 IPsec/IKE 原則。 您也可以選擇 tooapply 連線子集的自訂原則。 剩餘的 hello 將會使用 hello Azure 預設 IPsec/IKE 原則集。

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>可以使用 hello 自訂原則以及 VNet 對 VNet 連線嗎？
是，IPsec 跨單位連線或 VNet 對 VNet 連線皆可套用自訂原則。

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>我需要 toospecify hello 上兩個 VNet 對 VNet 連線資源相同的原則嗎？
是。 VNet 對 VNet 通道在 Azure 中包含兩個連線資源，這兩個資源各自應對一個方向。 您需要這兩個連線的資源具有的 tooensure hello 相同的原則，將不會建立 othereise hello VNet 對 VNet 連線。

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>自訂 IPsec/IKE 原則是否適用於 ExpressRoute 連線？
否。 IPsec/IKE 原則只適用於 S2S VPN 和 VNet 對 VNet 連線透過 hello Azure VPN 閘道。
