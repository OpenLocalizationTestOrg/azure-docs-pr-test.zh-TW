### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>可以使用哪些用戶端作業系統來搭配點對站台？

支援下列用戶端作業系統的 hello:

* Windows 7 (32 位元和 64 位元)
* Windows Server 2008 R2 (僅限 64 位元)
* Windows 8 (32 位元和 64 位元)
* Windows 8.1 (32 位元和 64 位元)
* Windows Server 2012 (僅限 64 位元)
* Windows Server 2012 R2 (僅限 64 位元)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>是否可以對支援 SSTP 的點對站台使用任何軟體 VPN 用戶端？

否。 支援是限制只有 toohello Windows 作業系統版本上面所列。

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>在我的點對站台組態中可以有多少個 VPN 用戶端端點？

我們 too128 VPN 用戶端 toobe 無法 tooconnect tooa 虛擬網路在 hello 支援相同的時間。

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>是否可以使用自己的內部 PKI 根 CA 進行點對站台連線？

是。 先前只能使用自我簽署的根憑證。 您仍然可以上傳 20 個根憑證。

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>是否可以使用點對站台功能周遊 Proxy 和防火牆？

是。 我們使用 SSTP （安全通訊端通道通訊協定） tootunnel 通過防火牆。 此通道將會顯示為 HTTPs 連線。

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>如果我重新啟動設定點對站用戶端電腦時，會 hello VPN 自動重新連線嗎？

根據預設，hello 用戶端電腦將不重新建立 hello VPN 連線自動。

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>沒有點對站台支援自動重新連接和 DDNS 上的 hello VPN 用戶端嗎？

點對站台 VPN 目前不支援自動重新連接和 DDNS。

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>我可以有站對站和點對站組態共存 hello 相同虛擬網路嗎？

是。 如果閘道是路由式 VPN 類型，這兩個解決方案都可正常運作。 Hello 傳統部署模型，您需要動態閘道。 我們做了不支援點對站靜態路由 VPN 閘道或使用 hello 閘道`-VpnType PolicyBased`cmdlet。

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>可以設定點對站台用戶端 tooconnect toomultiple 虛擬網路在 hello 相同的時間？

是，可以的。 但是 hello 虛擬網路不能有重疊的 IP 首碼，而且 hello 點對站位址空間不得重疊 hello 虛擬網路之間。

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>透過網站間或點對站台連線可以獲得多少輸送量？

很難 toomaintain hello 確切的輸送量的 hello VPN 通道。 IPsec 和 SSTP 為加密嚴謹的 VPN 通訊協定。 輸送量也受到 hello 延遲和內部部署與 hello 網際網路之間的頻寬。
