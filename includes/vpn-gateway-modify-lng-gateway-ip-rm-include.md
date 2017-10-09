### <span data-ttu-id="b1c36-101"><a name="gwipnoconnection"></a>toomodify hello 區域網路閘道 'GatewayIpAddress'-沒有閘道連線</span><span class="sxs-lookup"><span data-stu-id="b1c36-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="b1c36-102">如果您想 tooconnect toohas hello VPN 裝置變更其公用 IP 位址，您會需要 toomodify hello 區域網路閘道 tooreflect 變更。</span><span class="sxs-lookup"><span data-stu-id="b1c36-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="b1c36-103">使用 hello 範例 toomodify 沒有閘道連線的區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b1c36-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="b1c36-104">當修改這個值，您也可以修改在 hello hello 位址前置詞相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b1c36-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="b1c36-105">確定 toouse hello 現有名稱區域網路閘道處於順序 toooverwrite hello 目前設定。</span><span class="sxs-lookup"><span data-stu-id="b1c36-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="b1c36-106">如果您使用不同的名稱，您會建立新的區域網路閘道，而非覆寫 hello 現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="b1c36-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="b1c36-107"><a name="gwipwithconnection"></a>toomodify hello 區域網路閘道 'GatewayIpAddress'-現有的閘道連線</span><span class="sxs-lookup"><span data-stu-id="b1c36-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="b1c36-108">如果您想 tooconnect toohas hello VPN 裝置變更其公用 IP 位址，您會需要 toomodify hello 區域網路閘道 tooreflect 變更。</span><span class="sxs-lookup"><span data-stu-id="b1c36-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="b1c36-109">如果閘道連線已存在，您必須先 tooremove hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b1c36-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="b1c36-110">移除 hello 連線之後，您可以修改 hello 閘道 IP 位址，並重新建立新的連接。</span><span class="sxs-lookup"><span data-stu-id="b1c36-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="b1c36-111">您也可以修改在 hello hello 位址前置詞相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b1c36-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="b1c36-112">這會導致您 VPN 連線的停機時間。</span><span class="sxs-lookup"><span data-stu-id="b1c36-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="b1c36-113">當修改 hello 閘道 IP 位址，您不需要 toodelete hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="b1c36-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="b1c36-114">您只需要 tooremove hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b1c36-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="b1c36-115">移除 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b1c36-115">Remove hello connection.</span></span> <span data-ttu-id="b1c36-116">您可以使用 ' Get AzureRmVirtualNetworkGatewayConnection' hello cmdlet 找到 hello 您連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1c36-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="b1c36-117">修改 hello 'GatewayIpAddress' 值。</span><span class="sxs-lookup"><span data-stu-id="b1c36-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="b1c36-118">您也可以修改在 hello hello 位址前置詞相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b1c36-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="b1c36-119">是確定 toouse hello 現有名稱區域網路閘道 toooverwrite hello 目前的設定。</span><span class="sxs-lookup"><span data-stu-id="b1c36-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="b1c36-120">如果沒有，您會建立新的區域網路閘道，而非覆寫 hello 現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="b1c36-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="b1c36-121">建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b1c36-121">Create hello connection.</span></span> <span data-ttu-id="b1c36-122">在此範例中，我們會設定 IPsec 連線類型。</span><span class="sxs-lookup"><span data-stu-id="b1c36-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="b1c36-123">當您重新建立您的連線時，使用指定的 hello 連接類型來設定。</span><span class="sxs-lookup"><span data-stu-id="b1c36-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="b1c36-124">其他連接類型，請參閱 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="b1c36-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="b1c36-125">tooobtain hello VirtualNetworkGateway 名稱，您可以執行 hello ' Get AzureRmVirtualNetworkGateway' 指令程式。</span><span class="sxs-lookup"><span data-stu-id="b1c36-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="b1c36-126">設定 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="b1c36-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="b1c36-127">建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b1c36-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```