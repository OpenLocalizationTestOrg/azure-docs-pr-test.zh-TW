## <a name="application-gateway"></a><span data-ttu-id="70d4f-101">應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="70d4f-101">Application Gateway</span></span>
<span data-ttu-id="70d4f-102">應用程式閘道會根據第 7 層負載平衡，提供 Azure 管理的 HTTP 負載平衡解決方案。</span><span class="sxs-lookup"><span data-stu-id="70d4f-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="70d4f-103">應用程式負載平衡可讓 hello 使用 HTTP 為基礎的網路流量路由規則。</span><span class="sxs-lookup"><span data-stu-id="70d4f-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="70d4f-104">屬性</span><span class="sxs-lookup"><span data-stu-id="70d4f-104">Property</span></span> | <span data-ttu-id="70d4f-105">說明</span><span class="sxs-lookup"><span data-stu-id="70d4f-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="70d4f-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="70d4f-106">**backendAddressPools**</span></span> |<span data-ttu-id="70d4f-107">hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="70d4f-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="70d4f-108">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP VIP 或私人 IP</span><span class="sxs-lookup"><span data-stu-id="70d4f-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="70d4f-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="70d4f-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="70d4f-110">每個集區都有一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質。</span><span class="sxs-lookup"><span data-stu-id="70d4f-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="70d4f-111">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器</span><span class="sxs-lookup"><span data-stu-id="70d4f-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="70d4f-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="70d4f-112">**frontendPorts**</span></span> |<span data-ttu-id="70d4f-113">此連接埠是 hello 應用程式閘道上開啟 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="70d4f-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="70d4f-114">流量叫用這個連接埠，接著再取得重新導向 tooone 的 hello 後端伺服器</span><span class="sxs-lookup"><span data-stu-id="70d4f-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="70d4f-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="70d4f-115">**httpListeners**</span></span> |<span data-ttu-id="70d4f-116">接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）</span><span class="sxs-lookup"><span data-stu-id="70d4f-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="70d4f-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="70d4f-117">**requestRoutingRules**</span></span> |<span data-ttu-id="70d4f-118">hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義應該由哪一個後端伺服器集區 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="70d4f-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="70d4f-119">目前只有以循環配置資源的方式運作</span><span class="sxs-lookup"><span data-stu-id="70d4f-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="70d4f-120">範例應用程式閘道 Json 範本：</span><span class="sxs-lookup"><span data-stu-id="70d4f-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
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
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="70d4f-121">其他資源</span><span class="sxs-lookup"><span data-stu-id="70d4f-121">Additional resources</span></span>
<span data-ttu-id="70d4f-122">如需詳細資訊，請閱讀 [ 應用程式閘道 REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="70d4f-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

