### <span data-ttu-id="3272b-101"><a name="noconnection"></a>toomodify 區域網路閘道 IP 位址首碼不閘道連線</span><span class="sxs-lookup"><span data-stu-id="3272b-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="3272b-102">tooadd 其他位址前置詞：</span><span class="sxs-lookup"><span data-stu-id="3272b-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="3272b-103">tooremove 位址首碼：</span><span class="sxs-lookup"><span data-stu-id="3272b-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="3272b-104">會省略您不再需要的 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="3272b-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="3272b-105">在此範例中，我們不再需要的前置詞 20.0.0.0/24 （從 hello 上述範例中），因此，我們更新 hello 區域網路閘道，但不包括該前置詞。</span><span class="sxs-lookup"><span data-stu-id="3272b-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="3272b-106"><a name="withconnection"></a>toomodify 區域網路閘道的 IP 位址首碼為現有的閘道連線</span><span class="sxs-lookup"><span data-stu-id="3272b-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="3272b-107">如果您有閘道連接和要 tooadd 或移除 hello IP 位址前置詞包含在您的本機網路閘道，您會需要 toodo hello 依照依順序的步驟。</span><span class="sxs-lookup"><span data-stu-id="3272b-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="3272b-108">這會導致您 VPN 連線的停機時間。</span><span class="sxs-lookup"><span data-stu-id="3272b-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="3272b-109">修改 IP 位址前置詞，您無須 toodelete hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="3272b-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="3272b-110">您只需要 tooremove hello 連線。</span><span class="sxs-lookup"><span data-stu-id="3272b-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="3272b-111">移除 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="3272b-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="3272b-112">修改您的本機網路閘道的 hello 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="3272b-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="3272b-113">設定 hello LocalNetworkGateway hello 變數。</span><span class="sxs-lookup"><span data-stu-id="3272b-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="3272b-114">修改 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="3272b-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="3272b-115">建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="3272b-115">Create hello connection.</span></span> <span data-ttu-id="3272b-116">在此範例中，我們會設定 IPsec 連線類型。</span><span class="sxs-lookup"><span data-stu-id="3272b-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="3272b-117">當您重新建立您的連線時，使用指定的 hello 連接類型來設定。</span><span class="sxs-lookup"><span data-stu-id="3272b-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="3272b-118">其他連接類型，請參閱 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="3272b-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="3272b-119">設定 hello VirtualNetworkGateway hello 變數。</span><span class="sxs-lookup"><span data-stu-id="3272b-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="3272b-120">建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="3272b-120">Create hello connection.</span></span> <span data-ttu-id="3272b-121">這個範例會使用 hello 變數 $local 您在步驟 2 中設定。</span><span class="sxs-lookup"><span data-stu-id="3272b-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```