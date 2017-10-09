您可以確認您的連線成功，不論使用 ' Get AzureRmVirtualNetworkGatewayConnection' hello cmdlet '-偵錯 '。 

1. 下列 cmdlet 範例中，設定 hello 值 toomatch 使用 hello 自己。 如果出現提示，請選取 'A' 中順序 toorun 'All'。 在 hello 範例中，'-名稱 ' 指的是您想 tootest hello 連接 toohello 名稱。

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Hello 指令程式完成之後，檢視 hello 值。 在 hello 面範例中，「 持續連線 」，而且您可以看到 ingress 和 egress 位元組顯示 hello 連線狀態。
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```