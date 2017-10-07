---
title: "aaaConnect 應用程式 tooyour 虛擬網路使用 PowerShell"
description: "說明如何 tooconnect tooand 搭配虛擬網路使用 PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>使用 PowerShell 來連線應用程式 tooyour 虛擬網路
## <a name="overview"></a>概觀
在 Azure 應用程式服務，您可以連接您的應用程式 （web、 mobile 或應用程式開發介面） tooan Azure 虛擬網路 (VNet) 您的訂用帳戶中。 這項功能稱為 VNet 整合。 hello VNet 整合功能不應與 hello App Service 環境功能，可讓您 toorun 虛擬網路中的 Azure 應用程式服務執行個體產生混淆。

hello VNet 整合功能具有使用者介面 (UI) hello 新入口網站中，您可以搭配 toointegrate 使用 hello 傳統部署模型或 hello Azure Resource Manager 部署模型所部署的虛擬網路。 如果您想 toolearn 更多關於 hello 功能，請參閱[整合您的應用程式與 Azure 虛擬網路](web-sites-integrate-with-vnet.md)。

本文是不需 toouse hello UI 的方式，但而有關如何使用 PowerShell tooenable 整合。 因為每種部署模型的 hello 命令不同，這份文件會具有每種部署模型區段。  

繼續閱讀本文之前，請確定您有︰

* 安裝最新的 Azure PowerShell SDK hello。 您可以將它安裝以 hello Web Platform Installer。
* 在標準或進階 SKU 執行的 Azure App Service 中的應用程式。

## <a name="classic-virtual-networks"></a>傳統虛擬網路
本節說明使用 hello 傳統部署模型的虛擬網路的三項工作：

1. 連接應用程式 tooa 預先存在之虛擬網路閘道，而且已設定點對站連線能力。
2. 更新應用程式的虛擬網路整合資訊。
3. 中斷連接您的應用程式與虛擬網路。

### <a name="connect-an-app-tooa-classic-vnet"></a>連接應用程式 tooa 傳統的 VNet
tooconnect 應用程式 tooa 的虛擬網路，請依照下列這三個步驟：

1. 宣告 toohello web 應用程式，它將會加入特定的虛擬網路。 hello 應用程式將會產生憑證，您會獲得 toohello 虛擬網路的點對站連線能力。
2. 上傳 hello web 應用程式憑證 toohello 虛擬網路，然後再擷取 hello 點對站 VPN 封裝 URI。
3. 更新 hello web 應用程式的虛擬網路連線與 hello 點對站台封裝 URI。

hello 第一個和第三個步驟是完全可編寫指令碼，但 hello 第二個步驟需要一次性手動動作透過 hello 入口網站或存取 tooperform**放**或**修補**hello 虛擬網路上的動作Azure 資源管理員端點。 請連絡 Azure 支援 toohave 啟用。 開始之前，請確定您的傳統虛擬網路已啟用點對站連接並已部署閘道器。 toocreate hello 閘道，並啟用點對站連線，您需要 toouse hello 入口網站所述在[建立 VPN 閘道][createvpngateway]。

hello 傳統虛擬網路需要 toobe hello 相同訂用帳戶您應用程式服務計劃要整合該保存 hello 應用程式。

##### <a name="set-up-azure-powershell-sdk"></a>設定 Azure PowerShell SDK
使用下列方式，開啟 PowerShell 視窗，並設定您的 Azure 帳戶和訂用帳戶︰

    Login-AzureRmAccount

該命令會開啟您的 Azure 認證的提示 tooget。 登入之後，使用下列命令 tooselect hello 想 toouse 的訂用帳戶的 hello。 請確定您使用的虛擬網路與應用程式服務方案中的 hello 訂用帳戶。

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

或

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>本文中使用的變數
toosimplify 命令，我們會設定**$Configuration** hello 特定組態 PowerShell 變數。

以下列參數的 hello 在 PowerShell 中，如下所示設定變數：

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

hello 應用程式位置應該在 hello 位置不包含任何空格。 例如，美國西部是 westus。

    $Configuration.WebAppLocation = "[Your web app Location]"

hello 下一個項目會寫入 hello 憑證的位置。 它應該是您的本機電腦上的可寫入路徑。 請確定 tooinclude.cer hello 結尾。

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee 您設定為何，型別**$Configuration**。

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

hello 本節其餘部分，假設您有建立為上述的變數。

##### <a name="declare-hello-virtual-network-toohello-app"></a>宣告 hello 虛擬網路 toohello 應用程式
使用下列命令 tootell hello 應用程式，它會使用這個特定的虛擬網路的 hello。 這會導致 hello 應用程式 toogenerate 必要的憑證：

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

如果此命令成功，**$vnet** 中應該有 **Properties** 變數。 hello**屬性**變數應該包含這兩個憑證指紋和 hello 憑證資料。

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>上傳 hello web 應用程式憑證 toohello 虛擬網路
每個訂用帳戶和虛擬網路組合都需要執行手動一次性步驟。 也就是說，如果您要連接訂閱 A tooVirtual 網路 A 中的應用程式，當您將需要 toodo 這個步驟只不論多少應用程式設定。 如果您要加入新的應用程式 tooanother 虛擬網路，您將需要 toodo 這一次。 在訂用帳戶中的層級 Azure 應用程式服務，產生的憑證集，而 hello 組 hello 應用程式將會連接到每個虛擬網路，產生一次 hello 這個錯誤的原因。

hello 憑證將已經設定如果遵循下列步驟，或如果您以 hello 整合相同虛擬網路使用 hello 入口網站。

hello 第一個步驟是 toogenerate hello.cer 檔案。 hello 第二個步驟是 tooupload hello.cer 檔案 tooyour 虛擬網路。 toogenerate hello.cer 檔案，從在 hello hello API 呼叫先前步驟中，執行下列命令的 hello。

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

hello 憑證將在 hello 位置找到的**$Configuration.GeneratedCertificatePath**指定。

tooupload hello 憑證手動使用 hello [Azure 入口網站][ azureportal]和**瀏覽的虛擬網路 （傳統）** > **的VPN連線** > **點對站** > **管理憑證**。 從這裡上傳您的憑證。

##### <a name="get-hello-point-to-site-package"></a>Hello 點對站台的套件
hello 中設定虛擬網路連接 web 應用程式上的下一個步驟是 tooget hello 點對站台的套件，並提供它 tooyour web 應用程式。

Hello 儲存下列範本 tooa 檔案稱為 GetNetworkPackageUri.json 某處，例如 C:\Azure\Templates\GetNetworkPackageUri.json 您電腦上。

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


設定輸入參數：

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

呼叫 hello 指令碼：

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


hello 變數**$output。Outputs.packageUri**現在會包含 hello 封裝 URI toobe 指定 tooyour web 應用程式。

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>上傳 hello 點對站台封裝 tooyour 應用程式
hello 最後一個步驟是 tooprovide hello 應用程式，此套件。 只要執行 hello 下一個命令：

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

如果訊息要求您 tooconfirm 您要覆寫現有的資源，請確定 tooallow 它。

此命令執行成功之後，您的應用程式現在應該連接的 toohello 虛擬網路。 tooconfirm 成功移 tooyour 應用程式主控台 中，與 hello 下列輸入：

    SET WEBSITE_

如果沒有環境變數呼叫 WEBSITE_VNETNAME 具有符合 hello hello 目標虛擬網路名稱的值，所有組態都成功。

### <a name="update-classic-vnet-integration-information"></a>更新傳統 VNet 整合資訊
tooupdate 或重新同步處理您的資訊，只需重複 hello hello 第一個就地建立 hello 整合時，您會遵循的步驟。 這些步驟如下︰

1. 定義您的組態資訊。
2. 宣告 hello 虛擬網路 toohello 應用程式。
3. 取得 hello 點對站台的套件。
4. 上傳 hello 點對站台封裝 tooyour 應用程式。

### <a name="disconnect-your-app-from-a-classic-vnet"></a>中斷連接您的應用程式與傳統 VNet
toodisconnect hello 應用程式，您需要虛擬網路整合期間所設定的 hello 組態資訊。 使用該資訊，還有然後一個命令 toodisconnect 應用程式從您的虛擬網路。

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Resource Manager 虛擬網路
Resource Manager 虛擬網路有 Azure Resource Manager API，可簡化某些處理程序 (相較於傳統虛擬網路)。 我們有一個指令碼，可協助您完成下列工作的 hello:

* 建立 Resource Manager 虛擬網路並您的應用程式整合。
* 建立閘道器，在既存的 Resource Manager 虛擬網路中設定點對站連接，然後與您的應用程式整合。
* 將您的應用程式與已啟用閘道器和點對站連接的既存 Resource Manager 虛擬網路整合。
* 中斷連接您的應用程式與虛擬網路。

### <a name="resource-manager-vnet-app-service-integration-script"></a>Resource Manager VNet App Service 整合指令碼
複製下列指令碼，並將它儲存 tooa 檔案 hello。 如果您不想 toouse hello 指令碼，則可以從它的免費 toolearn toosee 如何 tooset 進行與資源管理員的虛擬網路。

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

將儲存一份 hello 指令碼。 在本文中，其名稱為 V2VnetAllinOne.ps1，但您可以使用其他名稱。 此指令碼沒有引數。 您只需要執行它。 hello 首先 hello 指令碼會執行會提示您 toosign 中的。 登入之後，hello 指令碼會取得您的帳戶相關的詳細資料，並傳回訂用帳戶的清單。 不計算 hello 要求您提供認證，執行 hello 初始的指令碼看起來像這樣：

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) 示範訂用帳戶 (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS 測試 (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) 紫色示範訂用帳戶 (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    選擇選項：3

    帳戶      : ccompy@microsoft.com 環境      : AzureCloud 訂用帳戶: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d 租用戶       : 722278f-fef1-499f-91ab-2323d011db47

    請輸入您的應用程式的資源群組 hello: hcdemo rg 請輸入 hello 應用程式名稱： v2vnetpowershell 您該怎麼想 toodo？

    1) 加入新的虛擬網路 tooan 應用程式
    2) 加入現有的虛擬網路 tooan 應用程式
    3) 從應用程式移除虛擬網路

hello 本章節的其餘部分將說明這些三個選項。

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>建立 Resource Manager VNet 並與其整合
新的虛擬網路使用 hello Resource Manager 部署模型，並將其整合應用程式，選取 toocreate **1) 加入應用程式的新的虛擬網路 tooan**。 這會提示您輸入 hello hello 虛擬網路名稱。 在這個案例中，如 hello 下列設定，我使用 v2pshell hello 名稱。

hello 指令碼會為 hello hello 正在建立的虛擬網路的詳細資料。 如果我想，我可以變更任何 hello 值。 在此範例執行時，我建立的虛擬網路，具有下列設定的 hello:

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

如果您想要 toochange 任何 hello 值**Y** hello 變更。 當您滿意 hello 虛擬網路設定時，請輸入**N**或是直接按 Enter，當系統提示您需變更 hello 設定。 從上到完成為止，hello 指令碼將會告訴您一些決定其 ' i 執行直到它啟動 toocreate hello 虛擬網路閘道。 該步驟可能會佔用 tooan 小時。 在這個階段中，沒有任何進度列指示器，但是 hello 指令碼會讓您知道何時建立 hello 閘道。

Hello 指令碼完成時，它會顯示**已經完成**。 此時，您將有資源管理員的虛擬網路，hello 名稱與您選取的設定。 這個新的虛擬網路也會與您的應用程式整合。

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>將您的應用程式與既存的 Resource Manager VNet 整合
當您正在整合與預先存在的虛擬網路，如果您提供資源管理員的虛擬網路沒有閘道或點對站連線能力時，hello 指令碼會設定的。 如果 hello VNET 中已經有設定這些項目，hello 指令碼也會直接 toohello 應用程式整合。 toostart 此程序，只需選取**2) 加入現有的虛擬網路 tooan 應用程式**。

此選項只適用於您有預先存在的資源管理員虛擬網路中 hello 與您的應用程式相同的訂閱。 您選取 hello 選項之後，您會顯示您的資源管理員虛擬網路的清單。   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    選擇選項：5

只要選取您想要使用 toointegrate hello 虛擬網路。 如果您已經有具有已啟用點對站連線的閘道，hello 指令碼將會直接與虛擬網路整合您的應用程式。 如果您沒有閘道，您將需要 toospecify hello 閘道子網路。 您的閘道器子網路必須位於您的虛擬網路位址空間，而且它不能在任何其他子網路中。 如果您的虛擬網路沒有閘道器且您執行此步驟，則結果如下所示︰

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

在此範例中，建立虛擬網路閘道具有 hello 下列設定：

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

如果您想要 toochange 任何這些設定，您可以這樣做。 否則，請按下 Enter，hello 指令碼將會建立您的閘道，並附加您的應用程式 tooyour 虛擬網路。 hello 閘道建立時間仍然是一小時，不過，因此請確定您記住。 當所有項目完成時，會顯示 hello 指令碼**已經完成**。

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>中斷連接您的應用程式與 Resource Manager VNet
從您的虛擬網路中斷連接您的應用程式不會使 hello 閘道中斷或停用 點對站連線能力。 畢竟，您可能將它使用於其他項目。 它也不會中斷它 hello 以外的任何其他應用程式從您提供的其中一個。 tooperform 此動作，選取**3) 移除應用程式的虛擬網路**。 在您這麼做時，您會看到如下的畫面：

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

雖然 hello 指令碼說明刪除，但它不會刪除 hello 虛擬網路。 它只移除 hello 整合。 這是您想要確認之後 toodo，hello 命令相當快速地進行處理，並告訴您**True**完成時。

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
