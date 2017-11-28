---
title: "在 Azure 中使用 SSL 憑證來保護 IIS | Microsoft Docs"
description: "了解如何在 Azure 中的 Windows VM 上使用 SSL 憑證來保護 IIS 網頁伺服器"
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
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="a7808-103">在 Azure 中的 Windows 虛擬機器上使用 SSL 憑證來保護 IIS 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="a7808-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="a7808-104">若要保護網頁伺服器，您可以使用安全通訊端層 (SSL) 憑證來將網路流量加密。</span><span class="sxs-lookup"><span data-stu-id="a7808-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="a7808-105">這些 SSL 憑證可儲存在 Azure Key Vault，並且能夠讓您將憑證安全地部署到 Azure 中的 Windows 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="a7808-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="a7808-106">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="a7808-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7808-107">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a7808-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="a7808-108">產生或上傳憑證至 Key Vault</span><span class="sxs-lookup"><span data-stu-id="a7808-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="a7808-109">建立 VM 並安裝 IIS 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="a7808-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="a7808-110">將憑證插入 VM 並使用 SSL 繫結來設定 IIS</span><span class="sxs-lookup"><span data-stu-id="a7808-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="a7808-111">本教學課程需要 Azure PowerShell 模組 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a7808-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="a7808-112">執行 ` Get-Module -ListAvailable AzureRM` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="a7808-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="a7808-113">如果您需要升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="a7808-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="a7808-114">概觀</span><span class="sxs-lookup"><span data-stu-id="a7808-114">Overview</span></span>
<span data-ttu-id="a7808-115">Azure Key Vault 會保護密碼編譯金鑰和祕密，這類憑證或密碼。</span><span class="sxs-lookup"><span data-stu-id="a7808-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="a7808-116">Key Vault 有助於簡化憑證管理程序，並可讓您掌控用來存取這些憑證的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a7808-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="a7808-117">您可以在 Key Vault 內建立自我簽署憑證，或上傳您目前已經擁有的受信任憑證。</span><span class="sxs-lookup"><span data-stu-id="a7808-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="a7808-118">您不必使用包含了內建憑證的自訂 VM 映像，而是要將憑證插入執行中的 VM。</span><span class="sxs-lookup"><span data-stu-id="a7808-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="a7808-119">此程序可確保您在部署期間安裝在網頁伺服器上的憑證會是最新的。</span><span class="sxs-lookup"><span data-stu-id="a7808-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="a7808-120">如果您更新或取代憑證，您就不必另外再建立新的自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="a7808-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="a7808-121">當您建立其他 VM 時，系統會自動插入最新的憑證。</span><span class="sxs-lookup"><span data-stu-id="a7808-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="a7808-122">在整個過程中，憑證絕對不會離開 Azure 平台，或在指令碼、命令列記錄或範本中公開。</span><span class="sxs-lookup"><span data-stu-id="a7808-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="a7808-123">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a7808-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="a7808-124">建立 Key Vault 和憑證之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="a7808-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="a7808-125">下列範例會在「美國東部」位置建立名為 myResourceGroupSecureWeb 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="a7808-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="a7808-126">接著，使用 [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) 建立 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="a7808-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="a7808-127">每個 Key Vault 需要唯一的名稱，而且應該全部小寫。</span><span class="sxs-lookup"><span data-stu-id="a7808-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="a7808-128">使用您自己唯一的 Key Vault 名稱來取代下列範例中的 `<mykeyvault>`：</span><span class="sxs-lookup"><span data-stu-id="a7808-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="a7808-129">產生憑證並儲存於 Key Vault</span><span class="sxs-lookup"><span data-stu-id="a7808-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="a7808-130">若要在生產環境中使用，您應該使用 [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate) 來匯入由受信任的提供者所簽署的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="a7808-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="a7808-131">在本教學課程中，下列範例示範如何使用 [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) 來產生自我簽署憑證，而且該憑證會使用透過 [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy) 所得到的預設憑證原則。</span><span class="sxs-lookup"><span data-stu-id="a7808-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="a7808-132">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a7808-132">Create a virtual machine</span></span>
<span data-ttu-id="a7808-133">使用 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) 來設定 VM 的系統管理員使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="a7808-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="a7808-134">現在您可以使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="a7808-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="a7808-135">下列範例會建立必要的虛擬網路元件、作業系統設定，然後建立名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="a7808-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

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

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="a7808-136">系統需要花幾分鐘的時間來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="a7808-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="a7808-137">最後一個步驟會使用 Azure 自訂指令碼擴充功能，利用 [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension) 來安裝 IIS 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="a7808-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="a7808-138">將憑證從 Key Vault 新增至 VM</span><span class="sxs-lookup"><span data-stu-id="a7808-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="a7808-139">若要將憑證從 Key Vault 新增至 VM，請使用 [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret) 來取得憑證的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a7808-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="a7808-140">使用 [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret) 將憑證新增至 VM：</span><span class="sxs-lookup"><span data-stu-id="a7808-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="a7808-141">設定 IIS 以使用憑證</span><span class="sxs-lookup"><span data-stu-id="a7808-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="a7808-142">再次搭配 [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) 來使用自訂指令碼擴充功能，以更新 IIS 組態。</span><span class="sxs-lookup"><span data-stu-id="a7808-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="a7808-143">這次的更新會套用從 Key Vault 插入到 IIS 的憑證，並設定 Web 繫結：</span><span class="sxs-lookup"><span data-stu-id="a7808-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

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


### <a name="test-the-secure-web-app"></a><span data-ttu-id="a7808-144">測試安全的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7808-144">Test the secure web app</span></span>
<span data-ttu-id="a7808-145">使用 [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress) 取得 VM 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a7808-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="a7808-146">下列範例會取得稍早建立之 `myPublicIP` 的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="a7808-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="a7808-147">現在，您可以開啟 Web 瀏覽器，並在網址列輸入 `https://<myPublicIP>`。</span><span class="sxs-lookup"><span data-stu-id="a7808-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="a7808-148">若要在使用自我簽署憑證時接受安全性警告，請依序按一下 [詳細資料] 與 [繼續瀏覽網頁]：</span><span class="sxs-lookup"><span data-stu-id="a7808-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![接受 Web 瀏覽器安全性警告](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="a7808-150">接著會顯示受保護的 IIS 網站，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="a7808-150">Your secured IIS website is then displayed as in the following example:</span></span>

![檢視執行中安全的 IIS 網站](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="a7808-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7808-152">Next steps</span></span>

<span data-ttu-id="a7808-153">在本教學課程中，您已使用儲存在 Azure Key Vault 中的 SSL 憑證來保護 IIS 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="a7808-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="a7808-154">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="a7808-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7808-155">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a7808-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="a7808-156">產生或上傳憑證至 Key Vault</span><span class="sxs-lookup"><span data-stu-id="a7808-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="a7808-157">建立 VM 並安裝 IIS 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="a7808-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="a7808-158">將憑證插入 VM 並使用 SSL 繫結來設定 IIS</span><span class="sxs-lookup"><span data-stu-id="a7808-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="a7808-159">用以下連結查看預先建立的虛擬機器指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="a7808-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7808-160">Windows 虛擬機器指令碼範例</span><span class="sxs-lookup"><span data-stu-id="a7808-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)