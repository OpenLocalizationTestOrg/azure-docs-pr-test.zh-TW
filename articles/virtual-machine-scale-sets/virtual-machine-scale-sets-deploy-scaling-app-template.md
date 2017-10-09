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
# <a name="deploy-an-autoscaling-app-using-a-template"></a>使用範本部署自動調整應用程式

[Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)是很好的方法 toodeploy 相關資源的群組。 本教學課程是[部署簡單的小數位數組](virtual-machine-scale-sets-mvss-start.md)，並說明如何 toodeploy 標尺上的簡單的自動調整應用程式設定使用 Azure Resource Manager 範本。  您也可以設定使用 PowerShell、 CLI 或 hello 入口網站的自動調整。 如需詳細資訊，請參閱[自動調整概觀](virtual-machine-scale-sets-autoscale-overview.md)。

## <a name="two-quickstart-templates"></a>兩個快速入門範本
當您部署擴展集時，您可以使用 [VM 擴充功能](../virtual-machines/virtual-machines-windows-extensions-features.md)在平台映像上安裝新軟體。 VM 擴充功能是小型的應用程式，可在 Azure 虛擬機器上提供部署後設定和自動化工作，例如部署應用程式。 中所提供的兩個不同的範例範本[Azure/azure 快速入門-範本](https://github.com/Azure/azure-quickstart-templates)toodeploy 到標尺上的自動調整應用程式設定使用 VM 擴充功能的方式是用來顯示。

### <a name="python-http-server-on-linux"></a>Linux 上的 Python HTTP 伺服器
hello [Python HTTP 伺服器在 Linux 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)範例範本部署 Linux 規模集上執行簡單的自動調整應用程式。  [Bottle](http://bottlepy.org/docs/dev/)、 Python web 架構，而且簡單的 HTTP 伺服器部署中使用自訂指令碼 VM 延伸模組設定的 hello 標尺每個 VM 上。 hello 小數位數時，設定標尺所有 Vm 之間的平均 CPU 使用率超過 60%，並按比例減少 hello 平均 CPU 使用率時少於 30%。

此外 toohello 規模調整集合資源，hello *azuredeploy.json*虛擬網路、 公用 IP 位址、 負載平衡和自動調整規模設定的資源，也會宣告範例範本。  如需在範本中建立這些資源的詳細資訊，請參閱[具備自動調整功能的 Linux 擴展集](virtual-machine-scale-sets-linux-autoscale.md)。

在 hello *azuredeploy.json*範本、 hello `extensionProfile` hello 屬性`Microsoft.Compute/virtualMachineScaleSets`資源會指定自訂指令碼延伸。 `fileUris`指定 hello 指令碼位置。 在此情況下，兩個檔案： *workserver.py*，而後者可定義簡單的 HTTP 伺服器，和*installserver.sh*，這會安裝 Bottle 和啟動 hello HTTP 伺服器。 `commandToExecute`部署 hello 規模集之後，請指定 hello 命令 toorun。

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

### <a name="aspnet-mvc-application-on-windows"></a>Windows 上的 ASP.NET MVC 應用程式
hello [ASP.NET MVC 應用程式在 Windows 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)範例範本部署簡單的 ASP.NET MVC 應用程式執行於 IIS 上 Windows 規模集。  IIS hello MVC 應用程式部署和使用 hello [PowerShell 預期狀態設定 (DSC)](virtual-machine-scale-sets-dsc.md) VM 延伸模組。  hello 小數位數設定的標尺 （在上一次的 VM 執行個體） 當 CPU 使用量大於 50 %5 分鐘。 

此外 toohello 規模調整集合資源，hello *azuredeploy.json*虛擬網路、 公用 IP 位址、 負載平衡和自動調整規模設定的資源，也會宣告範例範本。 此範本也會示範應用程式升級。  如需在範本中建立這些資源的詳細資訊，請參閱[具備自動調整的 Windows 擴展集](virtual-machine-scale-sets-windows-autoscale.md)。

在 hello *azuredeploy.json*範本、 hello`extensionProfile`屬性 hello`Microsoft.Compute/virtualMachineScaleSets`資源會指定[預期的狀態設定 (DSC)](virtual-machine-scale-sets-dsc.md)延伸模組，這會安裝 IIS 和預設值WebDeploy 封裝中的 web 應用程式。  hello *IISInstall.ps1*指令碼會在 hello 虛擬機器上安裝 IIS，而且位於 hello *DSC*資料夾。  hello MVC web 應用程式位於 hello *WebDeploy*資料夾。  hello 路徑 toohello 安裝指令碼和 hello web 應用程式會定義在 hello`powershelldscZip`和`webDeployPackage`參數在 hello *azuredeploy.parameters.json*檔案。 

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

## <a name="deploy-hello-template"></a>部署 hello 範本
最簡單方式 toodeploy hello hello [Python HTTP 伺服器在 Linux 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)或[ASP.NET MVC 應用程式在 Windows 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)範本為 toouse hello**部署 tooAzure**按鈕位於 hello在 GitHub 中的 hello 讀我檔案。  您也可以使用 PowerShell 或 Azure CLI toodeploy hello 範例範本。

### <a name="powershell"></a>PowerShell
複製 hello [Python HTTP 伺服器在 Linux 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)或[ASP.NET MVC 應用程式在 Windows 上的](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale)hello GitHub 儲存機制 tooa 資料夾從本機電腦上的檔案。  開啟 hello *azuredeploy.parameters.json*檔案並更新 hello 預設值的 hello `vmssName`， `adminUsername`，和`adminPassword`參數。 儲存下列 PowerShell 指令碼太 hello*deploy.ps1* hello 在 hello 與相同的資料夾*azuredeploy.json*範本。 toodeploy hello 範例範本執行 hello *deploy.ps1*從 PowerShell 命令視窗的指令碼。

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

### <a name="azure-cli"></a>Azure CLI
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

## <a name="next-steps"></a>後續步驟

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
