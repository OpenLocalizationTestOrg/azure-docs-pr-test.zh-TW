<span data-ttu-id="d2ab8-101">此工作會使用 VNet 的 hello 步驟 hello 下列組態的參考清單中的 hello 值為基礎。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="d2ab8-102">其他設定和名稱也會概述於這份清單中。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="d2ab8-103">雖然我們沒有新增根據這份清單中的 hello 值的變數，我們不直接在 hello 步驟中的任何使用這份清單。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="d2ab8-104">您可以複製 hello 清單 toouse，做為參考，取代您自己 hello 值。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="d2ab8-105">**組態參考清單**</span><span class="sxs-lookup"><span data-stu-id="d2ab8-105">**Configuration reference list**</span></span>

* <span data-ttu-id="d2ab8-106">虛擬網路名稱 = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="d2ab8-107">虛擬網路位址空間 = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d2ab8-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="d2ab8-108">資源群組 = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="d2ab8-109">Subnet1 名稱 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="d2ab8-110">Subnet1 位址空間 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="d2ab8-111">閘道器子網路名稱："GatewaySubnet"，您必須一律將閘道器子網路命名為 *GatewaySubnet*。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="d2ab8-112">閘道子網路位址空間 = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="d2ab8-113">區域 = "East US"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-113">Region = "East US"</span></span>
* <span data-ttu-id="d2ab8-114">閘道名稱 = "GW"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="d2ab8-115">閘道 IP 名稱 = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="d2ab8-116">閘道 IP 組態名稱 = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="d2ab8-117">類型 = "ExpressRoute"，ExpressRoute 組態需要有這個類型。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="d2ab8-118">閘道公用 IP 名稱 = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="d2ab8-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="d2ab8-119">新增閘道</span><span class="sxs-lookup"><span data-stu-id="d2ab8-119">Add a gateway</span></span>
1. <span data-ttu-id="d2ab8-120">連接 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="d2ab8-121">宣告您在本練習中使用的變數。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="d2ab8-122">為確定 tooedit 想 toouse hello 範例 tooreflect hello 設定。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="d2ab8-123">以變數儲存在 hello 虛擬網路物件。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="d2ab8-124">加入閘道子網路 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="d2ab8-125">hello 閘道子網路必須命名為"GatewaySubnet"。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="d2ab8-126">您應建立 /27 或更大 (/26、/25 等) 的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="d2ab8-127">將 hello 組態設定。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="d2ab8-128">以變數儲存在 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="d2ab8-129">要求公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-129">Request a public IP address.</span></span> <span data-ttu-id="d2ab8-130">建立 hello 閘道之前，已要求 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="d2ab8-131">您不能指定您想 toouse; hello IP 位址它會動態配置。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="d2ab8-132">Hello 下一個組態區段中，您將使用此 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="d2ab8-133">hello AllocationMethod 必須是動態。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="d2ab8-134">建立您的閘道器的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="d2ab8-135">hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="d2ab8-136">在此步驟中，您要指定您建立 hello 閘道時所使用的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="d2ab8-137">這個步驟實際上不會建立 hello 閘道物件。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="d2ab8-138">使用以下 toocreate hello 範例閘道設定。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="d2ab8-139">建立 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-139">Create hello gateway.</span></span> <span data-ttu-id="d2ab8-140">在此步驟中，hello **-gatewaytype 的授權**尤其重要。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="d2ab8-141">您必須使用 hello 值**ExpressRoute**。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="d2ab8-142">執行這些 cmdlet 之後, hello 閘道可能需要 45 分鐘或更多 toocreate。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="d2ab8-143">確認已建立 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="d2ab8-143">Verify hello gateway was created</span></span>
<span data-ttu-id="d2ab8-144">使用下列命令已建立 hello 閘道的 tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="d2ab8-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="d2ab8-145">調整閘道器大小</span><span class="sxs-lookup"><span data-stu-id="d2ab8-145">Resize a gateway</span></span>
<span data-ttu-id="d2ab8-146">有幾個 [閘道 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="d2ab8-147">您可以使用下列隨時命令 toochange hello 閘道 SKU 的 hello。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2ab8-148">此命令不適用於 UltraPerformance 閘道。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="d2ab8-149">toochange 閘道 tooan UltraPerformance 閘道，先移除現有的 ExpressRoute 閘道的 hello，然後再建立新的 UltraPerformance 閘道。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="d2ab8-150">toodowngrade UltraPerformance 閘道，從您的閘道先移除 hello UltraPerformance 閘道，然後再建立新的閘道。</span><span class="sxs-lookup"><span data-stu-id="d2ab8-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="d2ab8-151">移除閘道器</span><span class="sxs-lookup"><span data-stu-id="d2ab8-151">Remove a gateway</span></span>
<span data-ttu-id="d2ab8-152">使用下列命令 tooremove 閘道 hello:</span><span class="sxs-lookup"><span data-stu-id="d2ab8-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```