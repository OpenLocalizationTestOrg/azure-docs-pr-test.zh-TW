<span data-ttu-id="2cb27-101">您可以確認您的連線成功使用 ' Get AzureVNetConnection' hello 指令程式。</span><span class="sxs-lookup"><span data-stu-id="2cb27-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="2cb27-102">下列 cmdlet 範例中，設定 hello 值 toomatch 使用 hello 自己。</span><span class="sxs-lookup"><span data-stu-id="2cb27-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="2cb27-103">如果包含空格，hello hello 虛擬網路名稱必須以引號括住。</span><span class="sxs-lookup"><span data-stu-id="2cb27-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="2cb27-104">Hello 指令程式完成之後，檢視 hello 值。</span><span class="sxs-lookup"><span data-stu-id="2cb27-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="2cb27-105">在 hello 下列範例中，hello 連線狀態會顯示成 「 持續連線 」，而且您可以看到 ingress 和 egress 位元組。</span><span class="sxs-lookup"><span data-stu-id="2cb27-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal