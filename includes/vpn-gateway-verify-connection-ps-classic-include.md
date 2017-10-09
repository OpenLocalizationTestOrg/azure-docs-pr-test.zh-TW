您可以確認您的連線成功使用 ' Get AzureVNetConnection' hello 指令程式。

1. 下列 cmdlet 範例中，設定 hello 值 toomatch 使用 hello 自己。 如果包含空格，hello hello 虛擬網路名稱必須以引號括住。

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Hello 指令程式完成之後，檢視 hello 值。 在 hello 下列範例中，hello 連線狀態會顯示成 「 持續連線 」，而且您可以看到 ingress 和 egress 位元組。

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal