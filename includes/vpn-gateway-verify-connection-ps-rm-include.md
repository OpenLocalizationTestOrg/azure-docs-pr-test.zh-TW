<span data-ttu-id="4a73a-101">您可以確認您的連線成功，不論使用 ' Get AzureRmVirtualNetworkGatewayConnection' hello cmdlet '-偵錯 '。</span><span class="sxs-lookup"><span data-stu-id="4a73a-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="4a73a-102">下列 cmdlet 範例中，設定 hello 值 toomatch 使用 hello 自己。</span><span class="sxs-lookup"><span data-stu-id="4a73a-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="4a73a-103">如果出現提示，請選取 'A' 中順序 toorun 'All'。</span><span class="sxs-lookup"><span data-stu-id="4a73a-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="4a73a-104">在 hello 範例中，'-名稱 ' 指的是您想 tootest hello 連接 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="4a73a-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="4a73a-105">Hello 指令程式完成之後，檢視 hello 值。</span><span class="sxs-lookup"><span data-stu-id="4a73a-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="4a73a-106">在 hello 面範例中，「 持續連線 」，而且您可以看到 ingress 和 egress 位元組顯示 hello 連線狀態。</span><span class="sxs-lookup"><span data-stu-id="4a73a-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```