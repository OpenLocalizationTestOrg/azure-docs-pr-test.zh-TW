---
title: "在 Azure 虛擬機器擴展集上部署應用程式 | Microsoft Docs"
description: "了解如何使用 Azure Resource Manager 範本，在虛擬機器擴展集上部署簡單的自動調整應用程式。"
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
ms.openlocfilehash: 07883a33382cc660b043c99872312a9e77228253
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="27146-103">使用範本部署自動調整應用程式</span><span class="sxs-lookup"><span data-stu-id="27146-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="27146-104">[Azure Resource Manager 範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)是部署相關資源群組的絕佳方式。</span><span class="sxs-lookup"><span data-stu-id="27146-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="27146-105">本教學課程是以[部屬簡單的擴展集](virtual-machine-scale-sets-mvss-start.md)為基礎，並說明如何使用 Azure Resource Manager 範本，在擴展集上部署簡單的自動調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="27146-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how to deploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="27146-106">您也可以使用 PowerShell、CLI 或入口網站設定自動調整。</span><span class="sxs-lookup"><span data-stu-id="27146-106">You can also set up autoscaling using PowerShell, CLI, or the portal.</span></span> <span data-ttu-id="27146-107">如需詳細資訊，請參閱[自動調整概觀](virtual-machine-scale-sets-autoscale-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="27146-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="27146-108">兩個快速入門範本</span><span class="sxs-lookup"><span data-stu-id="27146-108">Two quickstart templates</span></span>
<span data-ttu-id="27146-109">當您部署擴展集時，您可以使用 [VM 擴充功能](../virtual-machines/virtual-machines-windows-extensions-features.md)在平台映像上安裝新軟體。</span><span class="sxs-lookup"><span data-stu-id="27146-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="27146-110">VM 擴充功能是小型的應用程式，可在 Azure 虛擬機器上提供部署後設定和自動化工作，例如部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="27146-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="27146-111">[Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) 中會提供兩個不同的範例範本，其顯示如何使用 VM 擴充功能在擴展集上部署自動調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="27146-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how to deploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="27146-112">Linux 上的 Python HTTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="27146-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="27146-113">[Linux 上的 Python HTTP 伺服器](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)範例範本可部署在 Linux 擴展集上執行的簡單自動調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="27146-113">The [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="27146-114">[Bottle](http://bottlepy.org/docs/dev/)、Python Web 架構以及簡單的 HTTP 伺服器都是使用 VM 擴充功能部署在擴展集中的每部 VM 上。</span><span class="sxs-lookup"><span data-stu-id="27146-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in the scale set using a custom script VM extension.</span></span> <span data-ttu-id="27146-115">當所有 VM 的平均 CPU 使用率大於 60% 時，擴展集會相應放大，而當平均 CPU 使用率小於 30% 時，擴展集會相應縮小。</span><span class="sxs-lookup"><span data-stu-id="27146-115">The scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when the average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="27146-116">除了擴展集資源以外，*azuredeploy.json* 範例範本也會宣告虛擬網路、公用 IP 位址、負載平衡器和自動調整設定資源。</span><span class="sxs-lookup"><span data-stu-id="27146-116">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="27146-117">如需在範本中建立這些資源的詳細資訊，請參閱[具備自動調整功能的 Linux 擴展集](virtual-machine-scale-sets-linux-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="27146-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="27146-118">在 *azuredeploy.json* 範本中，`Microsoft.Compute/virtualMachineScaleSets` 資源的 `extensionProfile` 屬性可指定自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27146-118">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="27146-119">`fileUris` 指定指令碼位置。</span><span class="sxs-lookup"><span data-stu-id="27146-119">`fileUris` specifies the script(s) location.</span></span> <span data-ttu-id="27146-120">在此情況下，兩個檔案︰*workserver.py*可定義簡單的 HTTP 伺服器，以及 *installserver.sh* 可安裝 Bottle 並啟動 HTTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="27146-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts the HTTP server.</span></span> <span data-ttu-id="27146-121">`commandToExecute` 指定要在部署擴展集之後執行的命令。</span><span class="sxs-lookup"><span data-stu-id="27146-121">`commandToExecute` specifies the command to run after the scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="27146-122">Windows 上的 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="27146-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="27146-123">[Windows 上的 ASP.NET MVC 應用程式](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)範例範本可部署一個簡單的 ASP.NET MVC 應用程式，其在 Windows 擴展集上的 IIS 中執行。</span><span class="sxs-lookup"><span data-stu-id="27146-123">The [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="27146-124">IIS 和 MVC 應用程式是使用 [PowerShell 預期狀態設定 (DSC)](virtual-machine-scale-sets-dsc.md) VM 擴充功能進行部署。</span><span class="sxs-lookup"><span data-stu-id="27146-124">IIS and the MVC app are deployed using the [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="27146-125">當 CPU 使用率大於 50% 長達 5 分鐘時，擴展集會 (一度在 VM 執行個體上) 相應增加。</span><span class="sxs-lookup"><span data-stu-id="27146-125">The scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="27146-126">除了擴展集資源以外，*azuredeploy.json* 範例範本也會宣告虛擬網路、公用 IP 位址、負載平衡器和自動調整設定資源。</span><span class="sxs-lookup"><span data-stu-id="27146-126">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="27146-127">此範本也會示範應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="27146-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="27146-128">如需在範本中建立這些資源的詳細資訊，請參閱[具備自動調整的 Windows 擴展集](virtual-machine-scale-sets-windows-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="27146-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="27146-129">在 *azuredeploy.json* 範本中，`Microsoft.Compute/virtualMachineScaleSets` 資源的 `extensionProfile` 屬性會指定[期望狀態組態 (DSC)](virtual-machine-scale-sets-dsc.md) 擴充功能，該功能可從 WebDeploy 套件安裝 IIS 和預設 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27146-129">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="27146-130">*IISInstall.ps1* 指令碼會在虛擬機器上安裝 IIS 並且位於 *DSC* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="27146-130">The *IISInstall.ps1* script installs IIS on the virtual machine and is found in the *DSC* folder.</span></span>  <span data-ttu-id="27146-131">MVC Web 應用程式位於 *WebDeploy* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="27146-131">The MVC web app is found in the *WebDeploy* folder.</span></span>  <span data-ttu-id="27146-132">指令碼的安裝路徑和 Web 應用程式是定義於 *azuredeploy.parameters.json* 檔案的 `powershelldscZip` 和 `webDeployPackage` 參數中。</span><span class="sxs-lookup"><span data-stu-id="27146-132">The paths to the install script and the web app are defined in the `powershelldscZip` and `webDeployPackage` parameters in the *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="27146-133">部署範本</span><span class="sxs-lookup"><span data-stu-id="27146-133">Deploy the template</span></span>
<span data-ttu-id="27146-134">若要部署 [Linux 上的 Python HTTP 伺服器](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)或 [Windows 上的 ASP.NET MVC 應用程式](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)範本，最簡單的方式就是使用 GitHub 讀我檔案中的 [部署至 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27146-134">The simplest way to deploy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is to use the **Deploy to Azure** button found in the in the readme files in GitHub.</span></span>  <span data-ttu-id="27146-135">您也可以使用 PowerShell 或 Azure CLI 來部署範本範例。</span><span class="sxs-lookup"><span data-stu-id="27146-135">You can also use PowerShell or Azure CLI to deploy the sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="27146-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27146-136">PowerShell</span></span>
<span data-ttu-id="27146-137">從 GitHub 儲存機制將 [Linux 上的 Python HTTP 伺服器](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)或 [Windows 上的 ASP.NET MVC 應用程式](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)檔案複製到本機電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="27146-137">Copy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from the GitHub repo to a folder on your local computer.</span></span>  <span data-ttu-id="27146-138">開啟 *azuredeploy.parameters.json* 檔案並更新 `vmssName`、`adminUsername` 和 `adminPassword` 參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="27146-138">Open the *azuredeploy.parameters.json* file and update the default values of the `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="27146-139">將下列 PowerShell 指令碼儲存至相同資料夾中的 *deploy.ps1* 作為 *azuredeploy.json* 範本。</span><span class="sxs-lookup"><span data-stu-id="27146-139">Save the following PowerShell script to *deploy.ps1* in the same folder as the *azuredeploy.json* template.</span></span> <span data-ttu-id="27146-140">若要部署範例範本，請從 PowerShell 命令視窗執行 *deploy.ps1* 指令碼。</span><span class="sxs-lookup"><span data-stu-id="27146-140">To deploy the sample template run the *deploy.ps1* script from a PowerShell command window.</span></span>

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
    Write-Host "Resource group '$resourceGroupName' does not exist. To create a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start the deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="27146-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="27146-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
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

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
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

## <a name="next-steps"></a><span data-ttu-id="27146-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27146-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
