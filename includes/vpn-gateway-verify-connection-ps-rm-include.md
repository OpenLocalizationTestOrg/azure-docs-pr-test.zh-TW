<span data-ttu-id="34d37-101">您可以使用 'Get-AzureRmVirtualNetworkGatewayConnection' Cmdlet，並在搭配或不搭配 '-Debug' 的情況下驗證連線是否成功。</span><span class="sxs-lookup"><span data-stu-id="34d37-101">You can verify that your connection succeeded by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="34d37-102">請使用下列 Cmdlet 範例，並將值設定為與您狀況相符的值。</span><span class="sxs-lookup"><span data-stu-id="34d37-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="34d37-103">出現提示時，請選取 [A] 以執行 [全部]。</span><span class="sxs-lookup"><span data-stu-id="34d37-103">If prompted, select 'A' in order to run 'All'.</span></span> <span data-ttu-id="34d37-104">在範例中，'-Name' 是指您想要測試之連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="34d37-104">In the example, '-Name' refers to the name of the connection that you want to test.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="34d37-105">完成 Cmdlet 之後，請檢視值。</span><span class="sxs-lookup"><span data-stu-id="34d37-105">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="34d37-106">在下列範例中，連接狀態會顯示為 [已連接]，且您可以看見輸入和輸出位元組。</span><span class="sxs-lookup"><span data-stu-id="34d37-106">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```