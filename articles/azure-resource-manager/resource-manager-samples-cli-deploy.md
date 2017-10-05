---
title: "Azure CLI 指令碼範例 - 部署範本 | Microsoft Docs"
description: "部署 Azure Resource Manager 範本的範例指令碼。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 974230f349aec46fde58e69658e05a13bff4296f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---azure-cli-script"></a><span data-ttu-id="8e19f-103">Azure Resource Manager 範本部署 - Azure CLI 指令碼</span><span class="sxs-lookup"><span data-stu-id="8e19f-103">Azure Resource Manager template deployment - Azure CLI script</span></span>

<span data-ttu-id="8e19f-104">此指令碼會將 Resource Manager 範本部署到您的訂用帳戶中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8e19f-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8e19f-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="8e19f-105">Sample script</span></span>

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
az account set --subscription $subscriptionId

#Check for existing RG
if [ $(az group exists --name $resourceGroupName) == 'false' ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
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

## <a name="clean-up-deployment"></a><span data-ttu-id="8e19f-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="8e19f-106">Clean up deployment</span></span> 

<span data-ttu-id="8e19f-107">執行下列命令來移除資源群組和其所有資源。</span><span class="sxs-lookup"><span data-stu-id="8e19f-107">Run the following command to remove the resource group and all its resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8e19f-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="8e19f-108">Script explanation</span></span>

<span data-ttu-id="8e19f-109">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="8e19f-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="8e19f-110">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="8e19f-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8e19f-111">命令</span><span class="sxs-lookup"><span data-stu-id="8e19f-111">Command</span></span> | <span data-ttu-id="8e19f-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="8e19f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8e19f-113">az group exists</span><span class="sxs-lookup"><span data-stu-id="8e19f-113">az group exists</span></span>](/cli/azure/group#exists) | <span data-ttu-id="8e19f-114">檢查資源群組是否存在。</span><span class="sxs-lookup"><span data-stu-id="8e19f-114">Checks whether resource group exists.</span></span> |
| [<span data-ttu-id="8e19f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="8e19f-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="8e19f-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8e19f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8e19f-117">az group deployment create</span><span class="sxs-lookup"><span data-stu-id="8e19f-117">az group deployment create</span></span>](/cli/azure/group/deployment#create) | <span data-ttu-id="8e19f-118">開始部署。</span><span class="sxs-lookup"><span data-stu-id="8e19f-118">Start a deployment.</span></span>  |
| [<span data-ttu-id="8e19f-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="8e19f-119">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="8e19f-120">刪除資源群組，包括其所有資源。</span><span class="sxs-lookup"><span data-stu-id="8e19f-120">Deletes a resource group including all its resources.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="8e19f-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e19f-121">Next steps</span></span>
* <span data-ttu-id="8e19f-122">如需部署範本的簡介，請參閱[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="8e19f-122">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="8e19f-123">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-cli-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="8e19f-123">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="8e19f-124">若要在範本中定義參數，請參閱 [編寫範本](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="8e19f-124">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="8e19f-125">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="8e19f-125">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

