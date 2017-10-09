---
title: "aaaDeploy Azure 虛擬機器規模集上的應用程式 |Microsoft 文件"
description: "了解 toodeploy 簡單的自動調整應用程式上的虛擬機器擴展集使用 Azure Resource Manager 範本。"
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="357d9-103">使用範本部署自動調整應用程式</span><span class="sxs-lookup"><span data-stu-id="357d9-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="357d9-104">[Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)是很好的方法 toodeploy 相關資源的群組。</span><span class="sxs-lookup"><span data-stu-id="357d9-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="357d9-105">本教學課程是[部署簡單的小數位數組](virtual-machine-scale-sets-mvss-start.md)，並說明如何 toodeploy 標尺上的簡單的自動調整應用程式設定使用 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="357d9-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="357d9-106">您也可以設定使用 PowerShell、 CLI 或 hello 入口網站的自動調整。</span><span class="sxs-lookup"><span data-stu-id="357d9-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="357d9-107">如需詳細資訊，請參閱[自動調整概觀](virtual-machine-scale-sets-autoscale-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="357d9-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="357d9-108">兩個快速入門範本</span><span class="sxs-lookup"><span data-stu-id="357d9-108">Two quickstart templates</span></span>
<span data-ttu-id="357d9-109">當您部署擴展集時，您可以使用 [VM 擴充功能](../virtual-machines/virtual-machines-windows-extensions-features.md)在平台映像上安裝新軟體。</span><span class="sxs-lookup"><span data-stu-id="357d9-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="357d9-110">VM 擴充功能是小型的應用程式，可在 Azure 虛擬機器上提供部署後設定和自動化工作，例如部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="357d9-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="357d9-111">中所提供的兩個不同的範例範本[Azure/azure 快速入門-範本](https://github.com/Azure/azure-quickstart-templates)toodeploy 到標尺上的自動調整應用程式設定使用 VM 擴充功能的方式是用來顯示。</span><span class="sxs-lookup"><span data-stu-id="357d9-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="357d9-112">Linux 上的 Python HTTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="357d9-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="357d9-113">hello [Python HTTP 伺服器在 Linux 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)範例範本部署 Linux 規模集上執行簡單的自動調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="357d9-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="357d9-114">[Bottle](http://bottlepy.org/docs/dev/)、 Python web 架構，而且簡單的 HTTP 伺服器部署中使用自訂指令碼 VM 延伸模組設定的 hello 標尺每個 VM 上。</span><span class="sxs-lookup"><span data-stu-id="357d9-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="357d9-115">hello 小數位數時，設定標尺所有 Vm 之間的平均 CPU 使用率超過 60%，並按比例減少 hello 平均 CPU 使用率時少於 30%。</span><span class="sxs-lookup"><span data-stu-id="357d9-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="357d9-116">此外 toohello 規模調整集合資源，hello *azuredeploy.json*虛擬網路、 公用 IP 位址、 負載平衡和自動調整規模設定的資源，也會宣告範例範本。</span><span class="sxs-lookup"><span data-stu-id="357d9-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="357d9-117">如需在範本中建立這些資源的詳細資訊，請參閱[具備自動調整功能的 Linux 擴展集](virtual-machine-scale-sets-linux-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="357d9-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="357d9-118">在 hello *azuredeploy.json*範本、 hello `extensionProfile` hello 屬性`Microsoft.Compute/virtualMachineScaleSets`資源會指定自訂指令碼延伸。</span><span class="sxs-lookup"><span data-stu-id="357d9-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="357d9-119">`fileUris`指定 hello 指令碼位置。</span><span class="sxs-lookup"><span data-stu-id="357d9-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="357d9-120">在此情況下，兩個檔案： *workserver.py*，而後者可定義簡單的 HTTP 伺服器，和*installserver.sh*，這會安裝 Bottle 和啟動 hello HTTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="357d9-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="357d9-121">`commandToExecute`部署 hello 規模集之後，請指定 hello 命令 toorun。</span><span class="sxs-lookup"><span data-stu-id="357d9-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="357d9-122">Windows 上的 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="357d9-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="357d9-123">hello [ASP.NET MVC 應用程式在 Windows 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)範例範本部署簡單的 ASP.NET MVC 應用程式執行於 IIS 上 Windows 規模集。</span><span class="sxs-lookup"><span data-stu-id="357d9-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="357d9-124">IIS hello MVC 應用程式部署和使用 hello [PowerShell 預期狀態設定 (DSC)](virtual-machine-scale-sets-dsc.md) VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="357d9-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="357d9-125">hello 小數位數設定的標尺 （在上一次的 VM 執行個體） 當 CPU 使用量大於 50 %5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="357d9-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="357d9-126">此外 toohello 規模調整集合資源，hello *azuredeploy.json*虛擬網路、 公用 IP 位址、 負載平衡和自動調整規模設定的資源，也會宣告範例範本。</span><span class="sxs-lookup"><span data-stu-id="357d9-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="357d9-127">此範本也會示範應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="357d9-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="357d9-128">如需在範本中建立這些資源的詳細資訊，請參閱[具備自動調整的 Windows 擴展集](virtual-machine-scale-sets-windows-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="357d9-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="357d9-129">在 hello *azuredeploy.json*範本、 hello`extensionProfile`屬性 hello`Microsoft.Compute/virtualMachineScaleSets`資源會指定[預期的狀態設定 (DSC)](virtual-machine-scale-sets-dsc.md)延伸模組，這會安裝 IIS 和預設值WebDeploy 封裝中的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="357d9-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="357d9-130">hello *IISInstall.ps1*指令碼會在 hello 虛擬機器上安裝 IIS，而且位於 hello *DSC*資料夾。</span><span class="sxs-lookup"><span data-stu-id="357d9-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="357d9-131">hello MVC web 應用程式位於 hello *WebDeploy*資料夾。</span><span class="sxs-lookup"><span data-stu-id="357d9-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="357d9-132">hello 路徑 toohello 安裝指令碼和 hello web 應用程式會定義在 hello`powershelldscZip`和`webDeployPackage`參數在 hello *azuredeploy.parameters.json*檔案。</span><span class="sxs-lookup"><span data-stu-id="357d9-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a><span data-ttu-id="357d9-133">部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="357d9-133">Deploy hello template</span></span>
<span data-ttu-id="357d9-134">最簡單方式 toodeploy hello hello [Python HTTP 伺服器在 Linux 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)或[ASP.NET MVC 應用程式在 Windows 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)範本為 toouse hello**部署 tooAzure**按鈕位於 hello在 GitHub 中的 hello 讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="357d9-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="357d9-135">您也可以使用 PowerShell 或 Azure CLI toodeploy hello 範例範本。</span><span class="sxs-lookup"><span data-stu-id="357d9-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="357d9-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="357d9-136">PowerShell</span></span>
<span data-ttu-id="357d9-137">複製 hello [Python HTTP 伺服器在 Linux 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)或[ASP.NET MVC 應用程式在 Windows 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)hello GitHub 儲存機制 tooa 資料夾從本機電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="357d9-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="357d9-138">開啟 hello *azuredeploy.parameters.json*檔案並更新 hello 預設值的 hello `vmssName`， `adminUsername`，和`adminPassword`參數。</span><span class="sxs-lookup"><span data-stu-id="357d9-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="357d9-139">儲存下列 PowerShell 指令碼太 hello*deploy.ps1* hello 在 hello 與相同的資料夾*azuredeploy.json*範本。</span><span class="sxs-lookup"><span data-stu-id="357d9-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="357d9-140">toodeploy hello 範例範本執行 hello *deploy.ps1*從 PowerShell 命令視窗的指令碼。</span><span class="sxs-lookup"><span data-stu-id="357d9-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="357d9-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="357d9-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a><span data-ttu-id="357d9-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="357d9-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
