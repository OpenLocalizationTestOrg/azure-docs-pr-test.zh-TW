# 概觀
## [虛擬網路](virtual-networks-overview.md)
## [使用者定義的路由和 IP 轉送](virtual-networks-udr-overview.md)
## [虛擬網路對等互連](virtual-network-peering-overview.md)
## [商務持續性](virtual-network-disaster-recovery-guidance.md)
## [常見問題集](virtual-networks-faq.md)
## [IP 定址](virtual-network-ip-addresses-overview-arm.md)
## 傳統
### [IP 定址](virtual-network-ip-addresses-overview-classic.md)
### [存取控制清單](virtual-networks-acl.md)

# 開始使用
## [建立您的第一個虛擬網路](virtual-network-get-started-vnet-subnet.md)

# 作法
## 規劃和設計
### [虛擬網路](virtual-network-vnet-plan-design-arm.md)
### [網路安全性群組](virtual-networks-nsg.md)

## 部署
### [虛擬網路](virtual-networks-create-vnet-arm-pportal.md)
#### [PowerShell](virtual-networks-create-vnet-arm-ps.md)
#### [CLI](virtual-networks-create-vnet-arm-cli.md)
#### [範本](virtual-networks-create-vnet-arm-template-click.md)

### 網路安全性群組
#### [入口網站](virtual-networks-create-nsg-arm-pportal.md)
#### [PowerShell](virtual-networks-create-nsg-arm-ps.md)
#### [CLI](virtual-networks-create-nsg-arm-cli.md)
#### [範本](virtual-networks-create-nsg-arm-template.md)
#### 傳統
##### [PowerShell](virtual-networks-create-nsg-classic-ps.md)
##### [CLI](virtual-networks-create-nsg-classic-cli.md)

### 使用者定義的路由
#### [PowerShell](virtual-network-create-udr-arm-ps.md)
#### [CLI](virtual-network-create-udr-arm-cli.md)
#### [範本](virtual-network-create-udr-arm-template.md)
#### 傳統
##### [PowerShell](virtual-network-create-udr-classic-ps.md)
##### [CLI](virtual-network-create-udr-classic-cli.md)

### 虛擬網路對等互連
#### [相同的部署模型 - 相同的訂用帳戶](virtual-network-create-peering.md)
#### [相同的部署模型 - 不同的訂用帳戶](create-peering-different-subscriptions.md)
#### [不同的部署模型 - 相同的訂用帳戶](create-peering-different-deployment-models.md)
#### [不同的部署模型 - 不同的訂用帳戶](create-peering-different-deployment-models-subscriptions.md)

### 虛擬機器
#### 建立具有靜態公用 IP 位址的 VM
##### [入口網站](virtual-network-deploy-static-pip-arm-portal.md)
##### [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
##### [CLI](virtual-network-deploy-static-pip-arm-cli.md)
##### [範本](virtual-network-deploy-static-pip-arm-template.md)
##### 傳統
###### [PowerShell](virtual-networks-reserved-public-ip.md)

#### 建立具有靜態私人 IP 位址的 VM
##### [入口網站](virtual-networks-static-private-ip-arm-pportal.md)
##### [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
##### [CLI](virtual-networks-static-private-ip-arm-cli.md)
##### 傳統
###### [入口網站](virtual-networks-static-private-ip-classic-pportal.md)
###### [PowerShell](virtual-networks-static-private-ip-classic-ps.md)
###### [CLI](virtual-networks-static-private-ip-classic-cli.md)

#### 建立具有多個網路介面的 VM
##### [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### 傳統
###### [PowerShell](virtual-network-deploy-multinic-classic-ps.md)
###### [CLI](virtual-network-deploy-multinic-classic-cli.md)

#### 建立具有多個 IP 位址的 VM
##### [Azure 入口網站](virtual-network-multiple-ip-addresses-portal.md)
##### [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)
##### [CLI](virtual-network-multiple-ip-addresses-cli.md)
##### [範本](virtual-network-multiple-ip-addresses-template.md)

#### [建立使用加速網路的 VM](virtual-network-create-vm-accelerated-networking.md)

### 連線能力案例
#### [虛擬網路 (VNet) tooVNet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [VNet （資源管理員） tooa VNet （傳統）](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [VNet tooon 內部部署網路 (VPN)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [VNet tooon 內部部署網路 (ExpressRoute)](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [高可用性的混合式網路架構](../guidance/guidance-hybrid-network-expressroute-vpn-failover.md?toc=%2fazure%2fvirtual-network%2ftoc.json)

### 安全性案例
#### [使用虛擬設備維護網路安全](virtual-network-scenario-udr-gw-nva.md)
#### [Azure 與 hello 網際網路之間的周邊網路](../guidance/guidance-iaas-ra-secure-vnet-dmz.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [雲端服務和網路安全性](../best-practices-network-security.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [具有 NSG 的簡單 DMZ](virtual-networks-dmz-nsg-asm.md)
##### [具有 NSG 和防火牆的 DMZ](virtual-networks-dmz-nsg-fw-asm.md)
##### [具有防火牆、UDR 和 NSG 的 DMZ](virtual-networks-dmz-nsg-fw-udr-asm.md)
##### [範例應用程式](virtual-networks-sample-app.md)

### 傳統
#### [虛擬網路](create-virtual-network-classic.md)
##### [入口網站](virtual-networks-create-vnet-classic-pportal.md)
##### [PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md)
##### [CLI](virtual-networks-create-vnet-classic-cli.md)

## 設定
### 虛擬機器
#### [新增或移除網路介面](virtual-network-network-interface-vm.md)
#### [VM 與雲端服務的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)
#### [最佳化網路輸送量](virtual-network-optimize-network-bandwidth.md)
#### [檢視及修改主機名稱](virtual-networks-viewing-and-modifying-hostnames.md)
### 傳統
#### 存取控制清單
##### [入口網站](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [PowerShell](virtual-networks-acl-powershell.md)

## 管理
### [虛擬網路](virtual-network-manage-network.md)
#### [子網路](virtual-network-manage-subnet.md)
#### [對等互連](virtual-network-manage-peering.md)
#### 傳統
##### [網路組態檔](virtual-networks-using-network-configuration-file.md)
##### [移轉的同質群組 tooa 區域](virtual-networks-migrate-to-regional-vnet.md)
### 網路安全性群組
#### [入口網站](virtual-network-manage-nsg-arm-portal.md)
#### [PowerShell](virtual-network-manage-nsg-arm-ps.md)
#### [CLI](virtual-network-manage-nsg-arm-cli.md)
#### [記錄檔](virtual-network-nsg-manage-log.md)
### 網路介面 (NIC)
#### [建立、變更或刪除 NIC](virtual-network-network-interface.md)
#### [新增、變更或移除 IP 位址](virtual-network-network-interface-addresses.md)
### 虛擬機器
#### [移動 VM tooa 不同子網路](virtual-networks-move-vm-role-to-subnet.md)
### [公用 IP 位址](virtual-network-public-ip-address.md)

## 疑難排解
### 網路安全性群組
#### [入口網站](virtual-network-nsg-troubleshoot-portal.md)
#### [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
### 路由
#### [入口網站](virtual-network-routes-troubleshoot-portal.md)
#### [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
### [輸送量測試](virtual-network-bandwidth-testing.md)
### [無法刪除虛擬網路](virtual-network-troubleshoot-cannot-delete-vnet.md)
### [VM tooVM 連線問題](virtual-network-troubleshoot-connectivity-problem-between-vms.md)

# 參考
## [程式碼範例](https://azure.microsoft.com/en-us/resources/samples/?service=virtual-network)
## [PowerShell (資源管理員)](/powershell/module/azurerm.network)
## [PowerShell (傳統)](/powershell/module/azure/)
## [Azure CLI](/cli/azure/network)
## [Java](/java/api/)
## [REST (Resource Manager)](https://msdn.microsoft.com/library/mt163658.aspx)
## [REST (傳統)](https://msdn.microsoft.com/library/jj157182.aspx)


# 相關參考
## [虛擬機器](/azure/virtual-machines/)
## [應用程式閘道](/azure/application-gateway/)
## [Azure DNS](/azure/dns/)
## [流量管理員](/azure/traffic-manager/)
## [負載平衡器](/azure/load-balancer/)
## [VPN 閘道](/azure/vpn-gateway/)
## [ExpressRoute](/azure/expressroute/)

# 資源
## [Azure 藍圖](https://azure.microsoft.com/roadmap/?category=networking)
## [網路部落格](http://azure.microsoft.com/blog/topics/networking)
## [網路論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesVirtualNetwork)
## [價格](https://azure.microsoft.com/pricing/details/virtual-network)
## [定價計算機](https://azure.microsoft.com/pricing/calculator/)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-virtual-network)
