### <span data-ttu-id="65bbe-101"><a name="gwipnoconnection"></a>修改區域網路閘道 'GatewayIpAddress' - 沒有閘道連線</span><span class="sxs-lookup"><span data-stu-id="65bbe-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="65bbe-102">如果您想要連線的 VPN 裝置已變更其公用 IP 位址，您需要修改區域網路閘道，以反映該變更。</span><span class="sxs-lookup"><span data-stu-id="65bbe-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="65bbe-103">使用範例來修改沒有閘道連線的區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="65bbe-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="65bbe-104">修改此值時，您也可以同時修改位址首碼。</span><span class="sxs-lookup"><span data-stu-id="65bbe-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="65bbe-105">務必使用區域網路閘道的現有名稱，以便覆寫目前的設定。</span><span class="sxs-lookup"><span data-stu-id="65bbe-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="65bbe-106">如果您使用不同的名稱，您會建立新的區域網路閘道，而不是覆寫現有閘道。</span><span class="sxs-lookup"><span data-stu-id="65bbe-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="65bbe-107"><a name="gwipwithconnection"></a>修改區域網路閘道 'GatewayIpAddress' - 現有閘道連線</span><span class="sxs-lookup"><span data-stu-id="65bbe-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="65bbe-108">如果您想要連線的 VPN 裝置已變更其公用 IP 位址，您需要修改區域網路閘道，以反映該變更。</span><span class="sxs-lookup"><span data-stu-id="65bbe-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="65bbe-109">如果閘道連線已存在，您需要先移除連線。</span><span class="sxs-lookup"><span data-stu-id="65bbe-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="65bbe-110">連線移除之後，您可以修改閘道 IP 位址，然後重新建立新連線。</span><span class="sxs-lookup"><span data-stu-id="65bbe-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="65bbe-111">您也可以同時修改位址首碼。</span><span class="sxs-lookup"><span data-stu-id="65bbe-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="65bbe-112">這會導致您 VPN 連線的停機時間。</span><span class="sxs-lookup"><span data-stu-id="65bbe-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="65bbe-113">修改閘道 IP 位址時，您不需要刪除 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="65bbe-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="65bbe-114">您只需要移除連線。</span><span class="sxs-lookup"><span data-stu-id="65bbe-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="65bbe-115">移除連線。</span><span class="sxs-lookup"><span data-stu-id="65bbe-115">Remove the connection.</span></span> <span data-ttu-id="65bbe-116">您可以使用 'Get-AzureRmVirtualNetworkGatewayConnection' Cmdlet 來找到連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="65bbe-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="65bbe-117">修改 'GatewayIpAddress' 值。</span><span class="sxs-lookup"><span data-stu-id="65bbe-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="65bbe-118">您也可以同時修改位址首碼。</span><span class="sxs-lookup"><span data-stu-id="65bbe-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="65bbe-119">請務必使用區域網路閘道的現有名稱來覆寫目前的設定。</span><span class="sxs-lookup"><span data-stu-id="65bbe-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="65bbe-120">否則，您會建立新的區域網路閘道，而不是覆寫現有閘道。</span><span class="sxs-lookup"><span data-stu-id="65bbe-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="65bbe-121">建立連線。</span><span class="sxs-lookup"><span data-stu-id="65bbe-121">Create the connection.</span></span> <span data-ttu-id="65bbe-122">在此範例中，我們會設定 IPsec 連線類型。</span><span class="sxs-lookup"><span data-stu-id="65bbe-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="65bbe-123">當您重新建立連線時，請使用針對設定指定的連線類型。</span><span class="sxs-lookup"><span data-stu-id="65bbe-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="65bbe-124">對於其他連線類型，請參閱 [PowerShell Cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) 頁面。</span><span class="sxs-lookup"><span data-stu-id="65bbe-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="65bbe-125">若要取得 VirtualNetworkGateway 名稱，您可以執行 'Get-AzureRmVirtualNetworkGateway' Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="65bbe-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="65bbe-126">設定變數。</span><span class="sxs-lookup"><span data-stu-id="65bbe-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="65bbe-127">建立連線。</span><span class="sxs-lookup"><span data-stu-id="65bbe-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```