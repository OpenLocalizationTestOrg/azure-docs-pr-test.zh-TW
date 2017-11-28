---
title: "Azure 的範本與 SAS 權杖和 Azure CLI aaaDeploy |Microsoft 文件"
description: "從範本所保護的 Azure 資源管理員和 Azure CLI toodeploy 資源 tooAzure 使用 SAS 權杖。"
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
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="26612-103">使用 SAS 權杖和 Azure CLI 部署私用 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="26612-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="26612-104">當您的範本位於儲存體帳戶時，就可以限制存取 toohello 範本，並在部署期間提供的共用的存取簽章 (SAS) token。</span><span class="sxs-lookup"><span data-stu-id="26612-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="26612-105">本主題說明如何使用資源管理員範本 tooprovide SAS 權杖，在部署期間 toouse Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="26612-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="26612-106">加入私用的範本 toostorage 帳戶</span><span class="sxs-lookup"><span data-stu-id="26612-106">Add private template toostorage account</span></span>

<span data-ttu-id="26612-107">您可以新增範本 tooa 儲存體帳戶，並將 toothem 連結在部署期間使用 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="26612-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26612-108">下列 hello 步驟，包含 hello 範本的 hello blob 是可存取 tooonly hello 帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="26612-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="26612-109">不過，當您建立 hello blob SAS 權杖，hello blob 是可存取 tooanyone 與該 URI。</span><span class="sxs-lookup"><span data-stu-id="26612-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="26612-110">另一位使用者攔截 hello URI，該使用者能 tooaccess hello 範本。</span><span class="sxs-lookup"><span data-stu-id="26612-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="26612-111">使用 SAS 權杖是限制存取 tooyour 範本的好方法，但您不應該直接在 hello 範本中包含機密資料，例如密碼。</span><span class="sxs-lookup"><span data-stu-id="26612-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="26612-112">hello 下列範例設定私人儲存體帳戶容器並上傳範本：</span><span class="sxs-lookup"><span data-stu-id="26612-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="26612-113">在部署期間提供 SAS Token</span><span class="sxs-lookup"><span data-stu-id="26612-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="26612-114">toodeploy 私用儲存體帳戶中，範本會產生 SAS 權杖，並將它包括 hello URI hello 範本中。</span><span class="sxs-lookup"><span data-stu-id="26612-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="26612-115">設定 hello 到期時間 tooallow 足夠時間 toocomplete hello 部署。</span><span class="sxs-lookup"><span data-stu-id="26612-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="26612-116">如需使用包含已連結範本的 SAS Token 範例，請參閱 [透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="26612-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="26612-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26612-117">Next steps</span></span>
* <span data-ttu-id="26612-118">如簡介 toodeploying 範本，請參閱[部署資源與資源管理員範本和 Azure PowerShell](resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="26612-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="26612-119">如需部署範本的完整範例指令碼，請參閱[部署 Resource Manager 範本指令碼](resource-manager-samples-cli-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="26612-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="26612-120">toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="26612-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="26612-121">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="26612-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
