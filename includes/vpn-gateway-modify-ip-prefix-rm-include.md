### <span data-ttu-id="4b62e-101"><a name="noconnection"></a>修改區域網路閘道 IP 位址首碼 - 沒有閘道連線</span><span class="sxs-lookup"><span data-stu-id="4b62e-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="4b62e-102">若要新增其他位址首碼：</span><span class="sxs-lookup"><span data-stu-id="4b62e-102">To add additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="4b62e-103">若要移除位址首碼：</span><span class="sxs-lookup"><span data-stu-id="4b62e-103">To remove address prefixes:</span></span><br>
<span data-ttu-id="4b62e-104">省略您不再需要的首碼。</span><span class="sxs-lookup"><span data-stu-id="4b62e-104">Leave out the prefixes that you no longer need.</span></span> <span data-ttu-id="4b62e-105">此範例中不再需要首碼 20.0.0.0/24 (來自先前的範例)，因此我們將更新區域網路閘道，並排除該首碼。</span><span class="sxs-lookup"><span data-stu-id="4b62e-105">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we update the local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="4b62e-106"><a name="withconnection"></a>修改區域網路閘道 IP 位址首碼 - 現有閘道連線</span><span class="sxs-lookup"><span data-stu-id="4b62e-106"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="4b62e-107">如果您有閘道連線並想要新增或移除包含在區域網路閘道中的 IP 位址首碼，您必須依序執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4b62e-107">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="4b62e-108">這會導致您 VPN 連線的停機時間。</span><span class="sxs-lookup"><span data-stu-id="4b62e-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="4b62e-109">修改 IP 位址首碼時，您不需要刪除 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="4b62e-109">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="4b62e-110">您只需要移除連線。</span><span class="sxs-lookup"><span data-stu-id="4b62e-110">You only need to remove the connection.</span></span>


1. <span data-ttu-id="4b62e-111">移除連線。</span><span class="sxs-lookup"><span data-stu-id="4b62e-111">Remove the connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="4b62e-112">修改區域網路閘道的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="4b62e-112">Modify the address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="4b62e-113">設定 LocalNetworkGateway 的變數。</span><span class="sxs-lookup"><span data-stu-id="4b62e-113">Set the variable for the LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="4b62e-114">修改首碼。</span><span class="sxs-lookup"><span data-stu-id="4b62e-114">Modify the prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="4b62e-115">建立連線。</span><span class="sxs-lookup"><span data-stu-id="4b62e-115">Create the connection.</span></span> <span data-ttu-id="4b62e-116">在此範例中，我們會設定 IPsec 連線類型。</span><span class="sxs-lookup"><span data-stu-id="4b62e-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="4b62e-117">當您重新建立連線時，請使用針對設定指定的連線類型。</span><span class="sxs-lookup"><span data-stu-id="4b62e-117">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="4b62e-118">對於其他連線類型，請參閱 [PowerShell Cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) 頁面。</span><span class="sxs-lookup"><span data-stu-id="4b62e-118">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="4b62e-119">設定 VirtualNetworkGateway 的變數。</span><span class="sxs-lookup"><span data-stu-id="4b62e-119">Set the variable for the VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="4b62e-120">建立連線。</span><span class="sxs-lookup"><span data-stu-id="4b62e-120">Create the connection.</span></span> <span data-ttu-id="4b62e-121">此範例使用您在步驟 2 中設定的 $local 變數。</span><span class="sxs-lookup"><span data-stu-id="4b62e-121">This example uses the variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```