## <a name="load-balancer"></a><span data-ttu-id="c2a35-101">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c2a35-101">Load Balancer</span></span>
<span data-ttu-id="c2a35-102">當您想 tooscale 應用程式時，會使用負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c2a35-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="c2a35-103">典型部署案例包含在多個 VM 執行個體上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2a35-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="c2a35-104">hello VM 執行個體被 fronted 負載平衡器，可協助 toodistribute 網路流量 toohello 不同執行個體。</span><span class="sxs-lookup"><span data-stu-id="c2a35-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![單一 VM 上的 NIC](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="c2a35-106">屬性</span><span class="sxs-lookup"><span data-stu-id="c2a35-106">Property</span></span> | <span data-ttu-id="c2a35-107">說明</span><span class="sxs-lookup"><span data-stu-id="c2a35-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2a35-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="c2a35-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="c2a35-109">負載平衡器可以包括一個或多個前端 IP 位址 (亦稱為虛擬 IP (VIP))。</span><span class="sxs-lookup"><span data-stu-id="c2a35-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="c2a35-110">這些 IP 位址做為輸入 hello 流量，而且可以是公用 IP 或私人 IP</span><span class="sxs-lookup"><span data-stu-id="c2a35-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="c2a35-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="c2a35-111">*backendAddressPools*</span></span> |<span data-ttu-id="c2a35-112">這些是與 hello VM Nic toowhich 負載會分散到相關聯的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c2a35-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="c2a35-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="c2a35-113">*loadBalancingRules*</span></span> |<span data-ttu-id="c2a35-114">規則屬性對應指定的前端 IP 和連接埠組合 tooa 組的後端 IP 位址和連接埠組合。</span><span class="sxs-lookup"><span data-stu-id="c2a35-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="c2a35-115">使用負載平衡器資源的單一定義，您可以定義多個負載平衡規則，而每個規則都會反映與虛擬機器相關聯的前端 IP 與連接埠以及後端 IP 與連接埠組合。</span><span class="sxs-lookup"><span data-stu-id="c2a35-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="c2a35-116">hello 規則是 hello 前端集區 toomany 在虛擬機器中 hello 後端集區中的一個連接埠</span><span class="sxs-lookup"><span data-stu-id="c2a35-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="c2a35-117">*探查*</span><span class="sxs-lookup"><span data-stu-id="c2a35-117">*Probes*</span></span> |<span data-ttu-id="c2a35-118">探查可讓您追蹤 tookeep hello 的 VM 執行個體的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="c2a35-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="c2a35-119">Hello 虛擬機器執行個體如果健全狀況探查失敗，會自動帶離輪替</span><span class="sxs-lookup"><span data-stu-id="c2a35-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="c2a35-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="c2a35-120">*inboundNatRules*</span></span> |<span data-ttu-id="c2a35-121">NAT 規則定義 hello 輸入流量流經 hello 前端 IP 和分散式 toohello 後端 IP tooa 特定虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="c2a35-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="c2a35-122">NAT 規則是 hello 前端集區 tooone 虛擬機器中 hello 後端集區中的一個連接埠</span><span class="sxs-lookup"><span data-stu-id="c2a35-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="c2a35-123">Json 格式的負載平衡器範本範例：</span><span class="sxs-lookup"><span data-stu-id="c2a35-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[parameters('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[parameters('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="c2a35-124">其他資源</span><span class="sxs-lookup"><span data-stu-id="c2a35-124">Additional resources</span></span>
<span data-ttu-id="c2a35-125">如需詳細資訊，請參閱 [負載平衡器 REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="c2a35-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

