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
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="85500-103">在 Azure 中的 Windows 虛擬機器上使用 SSL 憑證來保護 IIS 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="85500-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="85500-104">toosecure web 伺服器，安全通訊端稍後 (SSL) 憑證可以是使用 tooencrypt 網路流量。</span><span class="sxs-lookup"><span data-stu-id="85500-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="85500-105">這些 SSL 憑證可以儲存在 Azure 金鑰保存庫，並在 Azure 中允許的憑證 tooWindows 虛擬機器 (Vm) 的安全部署。</span><span class="sxs-lookup"><span data-stu-id="85500-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="85500-106">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="85500-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85500-107">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="85500-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="85500-108">產生或上傳憑證 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="85500-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="85500-109">建立 VM，並且安裝 hello IIS 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="85500-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="85500-110">插入 hello VM 中的 hello 憑證和設定 IIS 的 SSL 繫結</span><span class="sxs-lookup"><span data-stu-id="85500-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="85500-111">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="85500-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="85500-112">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="85500-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="85500-113">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="85500-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="85500-114">概觀</span><span class="sxs-lookup"><span data-stu-id="85500-114">Overview</span></span>
<span data-ttu-id="85500-115">Azure Key Vault 會保護密碼編譯金鑰和祕密，這類憑證或密碼。</span><span class="sxs-lookup"><span data-stu-id="85500-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="85500-116">金鑰保存庫可協助簡化 hello 憑證管理程序，並讓您存取那些憑證的索引鍵的 toomaintain 控制項。</span><span class="sxs-lookup"><span data-stu-id="85500-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="85500-117">您可以在 Key Vault 內建立自我簽署憑證，或上傳您目前已經擁有的受信任憑證。</span><span class="sxs-lookup"><span data-stu-id="85500-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="85500-118">您不必使用包含了內建憑證的自訂 VM 映像，而是要將憑證插入執行中的 VM。</span><span class="sxs-lookup"><span data-stu-id="85500-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="85500-119">此程序可確保 hello 最新的憑證會在部署期間安裝網頁伺服器上。</span><span class="sxs-lookup"><span data-stu-id="85500-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="85500-120">如果您更新或取代憑證時，您還沒有 toocreate 新的自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="85500-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="85500-121">當您建立其他的 Vm 會自動插入 hello 最新的憑證。</span><span class="sxs-lookup"><span data-stu-id="85500-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="85500-122">Hello 整個程序期間 hello 憑證永遠不會保留 hello Azure 平台，或會公開在指令碼、 命令列的歷程記錄或範本。</span><span class="sxs-lookup"><span data-stu-id="85500-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="85500-123">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="85500-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="85500-124">建立 Key Vault 和憑證之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="85500-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="85500-125">hello 下列範例會建立名為的資源群組*myResourceGroupSecureWeb*在 hello*美國東部*位置：</span><span class="sxs-lookup"><span data-stu-id="85500-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="85500-126">接著，使用 [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) 建立 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="85500-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="85500-127">每個 Key Vault 需要唯一的名稱，而且應該全部小寫。</span><span class="sxs-lookup"><span data-stu-id="85500-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="85500-128">取代`<mykeyvault>`在下列範例使用您自己的唯一金鑰保存庫名稱 hello:</span><span class="sxs-lookup"><span data-stu-id="85500-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="85500-129">產生憑證並儲存於 Key Vault</span><span class="sxs-lookup"><span data-stu-id="85500-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="85500-130">若要在生產環境中使用，您應該使用 [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate) 來匯入由受信任的提供者所簽署的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="85500-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="85500-131">本教學課程，hello 下列範例示範如何產生自我簽署的憑證與[新增 AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate)使用 hello 來自預設憑證原則[新 AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy)。</span><span class="sxs-lookup"><span data-stu-id="85500-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="85500-132">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="85500-132">Create a virtual machine</span></span>
<span data-ttu-id="85500-133">集合的系統管理員使用者名稱及密碼 hello 與 VM [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="85500-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="85500-134">現在您可以建立 hello 與 VM[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="85500-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="85500-135">hello 下列範例會建立所需的 hello 虛擬網路的元件，hello 作業系統組態，然後建立名為的 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="85500-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="85500-136">花幾分鐘，讓建立 hello VM toobe。</span><span class="sxs-lookup"><span data-stu-id="85500-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="85500-137">hello 最後一個步驟會使用 hello Azure 自訂指令碼擴充 tooinstall hello IIS web 伺服器上的使用[組 AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension)。</span><span class="sxs-lookup"><span data-stu-id="85500-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="85500-138">新增憑證 tooVM 從金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="85500-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="85500-139">tooadd hello 憑證從金鑰保存庫 tooa VM，取得您的憑證與 hello 識別碼[Get AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret)。</span><span class="sxs-lookup"><span data-stu-id="85500-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="85500-140">新增 hello 憑證 toohello VM 與[新增 AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="85500-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="85500-141">設定 IIS toouse hello 憑證</span><span class="sxs-lookup"><span data-stu-id="85500-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="85500-142">使用 hello 一次使用自訂指令碼擴充[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS 設定。</span><span class="sxs-lookup"><span data-stu-id="85500-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="85500-143">此更新適用於從金鑰保存庫 tooIIS 插入 hello 憑證，並設定 hello 網站繫結：</span><span class="sxs-lookup"><span data-stu-id="85500-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

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


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="85500-144">測試 hello 安全的 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="85500-144">Test hello secure web app</span></span>
<span data-ttu-id="85500-145">取得具有您 VM 的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress)。</span><span class="sxs-lookup"><span data-stu-id="85500-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="85500-146">hello 下列範例會取得 IP 位址 hello`myPublicIP`稍早建立：</span><span class="sxs-lookup"><span data-stu-id="85500-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="85500-147">現在您可以開啟網頁瀏覽器並輸入`https://<myPublicIP>`hello 網址列中。</span><span class="sxs-lookup"><span data-stu-id="85500-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="85500-148">如果您使用自我簽署的憑證，tooaccept hello 安全性警告選取**詳細資料**，然後**toohello 網頁上移**:</span><span class="sxs-lookup"><span data-stu-id="85500-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![接受 Web 瀏覽器安全性警告](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="85500-150">受保護的 IIS 網站接著會顯示如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="85500-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![檢視執行中安全的 IIS 網站](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="85500-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85500-152">Next steps</span></span>

<span data-ttu-id="85500-153">在本教學課程中，您已使用儲存在 Azure Key Vault 中的 SSL 憑證來保護 IIS 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="85500-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="85500-154">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="85500-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85500-155">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="85500-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="85500-156">產生或上傳憑證 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="85500-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="85500-157">建立 VM，並且安裝 hello IIS 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="85500-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="85500-158">插入 hello VM 中的 hello 憑證和設定 IIS 的 SSL 繫結</span><span class="sxs-lookup"><span data-stu-id="85500-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="85500-159">請依照此連結 toosee，預先建立的虛擬機器指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="85500-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="85500-160">Windows 虛擬機器指令碼範例</span><span class="sxs-lookup"><span data-stu-id="85500-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)