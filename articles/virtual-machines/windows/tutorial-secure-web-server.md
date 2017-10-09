---
title: "aaaSecure IIS 以 SSL 憑證在 Azure 中 |Microsoft 文件"
description: "了解如何 toosecure hello IIS web 伺服器與 Azure 中的 Windows VM 上的 SSL 憑證"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>在 Azure 中的 Windows 虛擬機器上使用 SSL 憑證來保護 IIS 網頁伺服器
toosecure web 伺服器，安全通訊端稍後 (SSL) 憑證可以是使用 tooencrypt 網路流量。 這些 SSL 憑證可以儲存在 Azure 金鑰保存庫，並在 Azure 中允許的憑證 tooWindows 虛擬機器 (Vm) 的安全部署。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 Azure Key Vault
> * 產生或上傳憑證 toohello 金鑰保存庫
> * 建立 VM，並且安裝 hello IIS 網頁伺服器
> * 插入 hello VM 中的 hello 憑證和設定 IIS 的 SSL 繫結

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。


## <a name="overview"></a>概觀
Azure Key Vault 會保護密碼編譯金鑰和祕密，這類憑證或密碼。 金鑰保存庫可協助簡化 hello 憑證管理程序，並讓您存取那些憑證的索引鍵的 toomaintain 控制項。 您可以在 Key Vault 內建立自我簽署憑證，或上傳您目前已經擁有的受信任憑證。

您不必使用包含了內建憑證的自訂 VM 映像，而是要將憑證插入執行中的 VM。 此程序可確保 hello 最新的憑證會在部署期間安裝網頁伺服器上。 如果您更新或取代憑證時，您還沒有 toocreate 新的自訂 VM 映像。 當您建立其他的 Vm 會自動插入 hello 最新的憑證。 Hello 整個程序期間 hello 憑證永遠不會保留 hello Azure 平台，或會公開在指令碼、 命令列的歷程記錄或範本。


## <a name="create-an-azure-key-vault"></a>建立 Azure Key Vault
建立 Key Vault 和憑證之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupSecureWeb*在 hello*美國東部*位置：

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

接著，使用 [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) 建立 Key Vault。 每個 Key Vault 需要唯一的名稱，而且應該全部小寫。 取代`<mykeyvault>`在下列範例使用您自己的唯一金鑰保存庫名稱 hello:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>產生憑證並儲存於 Key Vault
若要在生產環境中使用，您應該使用 [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate) 來匯入由受信任的提供者所簽署的有效憑證。 本教學課程，hello 下列範例示範如何產生自我簽署的憑證與[新增 AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate)使用 hello 來自預設憑證原則[新 AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy)。 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a>建立虛擬機器
集合的系統管理員使用者名稱及密碼 hello 與 VM [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

現在您可以建立 hello 與 VM[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。 hello 下列範例會建立所需的 hello 虛擬網路的元件，hello 作業系統組態，然後建立名為的 VM *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

花幾分鐘，讓建立 hello VM toobe。 hello 最後一個步驟會使用 hello Azure 自訂指令碼擴充 tooinstall hello IIS web 伺服器上的使用[組 AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension)。


## <a name="add-a-certificate-toovm-from-key-vault"></a>新增憑證 tooVM 從金鑰保存庫
tooadd hello 憑證從金鑰保存庫 tooa VM，取得您的憑證與 hello 識別碼[Get AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret)。 新增 hello 憑證 toohello VM 與[新增 AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>設定 IIS toouse hello 憑證
使用 hello 一次使用自訂指令碼擴充[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS 設定。 此更新適用於從金鑰保存庫 tooIIS 插入 hello 憑證，並設定 hello 網站繫結：

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a>測試 hello 安全的 web 應用程式
取得具有您 VM 的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress)。 hello 下列範例會取得 IP 位址 hello`myPublicIP`稍早建立：

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

現在您可以開啟網頁瀏覽器並輸入`https://<myPublicIP>`hello 網址列中。 如果您使用自我簽署的憑證，tooaccept hello 安全性警告選取**詳細資料**，然後**toohello 網頁上移**:

![接受 Web 瀏覽器安全性警告](./media/tutorial-secure-web-server/browser-warning.png)

受保護的 IIS 網站接著會顯示如 hello 下列範例所示：

![檢視執行中安全的 IIS 網站](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已使用儲存在 Azure Key Vault 中的 SSL 憑證來保護 IIS 網頁伺服器。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Azure Key Vault
> * 產生或上傳憑證 toohello 金鑰保存庫
> * 建立 VM，並且安裝 hello IIS 網頁伺服器
> * 插入 hello VM 中的 hello 憑證和設定 IIS 的 SSL 繫結

請依照此連結 toosee，預先建立的虛擬機器指令碼範例。

> [!div class="nextstepaction"]
> [Windows 虛擬機器指令碼範例](./powershell-samples.md)