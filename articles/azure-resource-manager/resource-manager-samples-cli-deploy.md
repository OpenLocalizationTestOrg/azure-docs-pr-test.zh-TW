---
title: "CLI 指令碼範例-aaaAzure 部署範本 |Microsoft 文件"
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
ms.openlocfilehash: 5a94eedbd898ced29d67f8ce3023ca5c65f83af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---azure-cli-script"></a><span data-ttu-id="5fb37-103">Azure Resource Manager 範本部署 - Azure CLI 指令碼</span><span class="sxs-lookup"><span data-stu-id="5fb37-103">Azure Resource Manager template deployment - Azure CLI script</span></span>

<span data-ttu-id="5fb37-104">此指令碼會將部署您的訂用帳戶中資源管理員範本 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="5fb37-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5fb37-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5fb37-105">Sample script</span></span>

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

## <a name="clean-up-deployment"></a><span data-ttu-id="5fb37-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="5fb37-106">Clean up deployment</span></span> 

<span data-ttu-id="5fb37-107">Hello 執行的下列命令 tooremove hello 資源群組和其所有資源。</span><span class="sxs-lookup"><span data-stu-id="5fb37-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5fb37-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5fb37-108">Script explanation</span></span>

<span data-ttu-id="5fb37-109">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="5fb37-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="5fb37-110">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="5fb37-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5fb37-111">命令</span><span class="sxs-lookup"><span data-stu-id="5fb37-111">Command</span></span> | <span data-ttu-id="5fb37-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="5fb37-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5fb37-113">az group exists</span><span class="sxs-lookup"><span data-stu-id="5fb37-113">az group exists</span></span>](/cli/azure/group#exists) | <span data-ttu-id="5fb37-114">檢查資源群組是否存在。</span><span class="sxs-lookup"><span data-stu-id="5fb37-114">Checks whether resource group exists.</span></span> |
| [<span data-ttu-id="5fb37-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5fb37-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="5fb37-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5fb37-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5fb37-117">az group deployment create</span><span class="sxs-lookup"><span data-stu-id="5fb37-117">az group deployment create</span></span>](/cli/azure/group/deployment#create) | <span data-ttu-id="5fb37-118">開始部署。</span><span class="sxs-lookup"><span data-stu-id="5fb37-118">Start a deployment.</span></span>  |
| [<span data-ttu-id="5fb37-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="5fb37-119">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="5fb37-120">刪除資源群組，包括其所有資源。</span><span class="sxs-lookup"><span data-stu-id="5fb37-120">Deletes a resource group including all its resources.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="5fb37-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5fb37-121">Next steps</span></span>
* <span data-ttu-id="5fb37-122">如簡介 toodeploying 範本，請參閱[部署資源與資源管理員範本和 Azure PowerShell](resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5fb37-122">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="5fb37-123">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-cli-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="5fb37-123">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="5fb37-124">toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="5fb37-124">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="5fb37-125">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="5fb37-125">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

