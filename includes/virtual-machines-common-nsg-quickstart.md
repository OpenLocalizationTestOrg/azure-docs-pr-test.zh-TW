您開啟通訊埠，或建立端點，tooa Azure 虛擬機器 (VM) 中藉由建立子網路或 VM 網路介面上的網路篩選條件。 您收到 hello 流量的網路安全性群組附加 toohello 資源上放置控制輸入與輸出流量，這些篩選器。

讓我們使用連接埠 80 上的 Web 流量的常見範例。 一旦您擁有已設定的 tooserve hello 標準 TCP 連接埠 80 上的 web 要求的 VM （請記住 toostart hello 適當的服務並開啟任何作業系統上的防火牆規則以及 hello VM），您：

1. 建立網路安全性群組。
2. 建立輸入規則允許具有下列項目的流量︰
   * 為"80"hello 目的地連接埠範圍
   * hello 來源連接埠範圍的"*"（允許任何來源的連接埠）
   * 優先順序值小於 65,500 (toobe 較高的優先順序比 hello 預設所有拒絕傳入的規則)
3. Hello 網路安全性群組關聯 hello VM 網路介面或子網路。

您可以建立複雜的網路組態 toosecure 環境使用網路安全性群組規則和規則。 我們的範例僅使用一個或兩個規則，允許 HTTP 流量或遠端管理。 如需詳細資訊，請參閱 hello 下列[「 詳細資訊 」](#more-information-on-network-security-groups)區段或[什麼是網路安全性小組？](../articles/virtual-network/virtual-networks-nsg.md)

