---
title: "使用 SAS 權杖與 PowerShell 部署 Azure 範本 | Microsoft Docs"
description: "使用 Azure Resource Manager 和 Azure PowerShell，將受 SAS 權杖保護之範本中的資源部署到 Azure。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 1e3cea027b599e2b1af1ced0fdf14e2cc8a0db82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="b31c8-103">使用 SAS 權杖和 Azure PowerShell 部署私用 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="b31c8-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="b31c8-104">當您的範本位於儲存體帳戶中時，您可以限制範本的存取權，並在部署期間提供共用存取簽章 (SAS) Token</span><span class="sxs-lookup"><span data-stu-id="b31c8-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="b31c8-105">本主題說明如何在部署期間使用 Azure PowerShell 與 Resource Manager 範本提供 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="b31c8-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="b31c8-106">將私人範本新增至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b31c8-106">Add private template to storage account</span></span>

<span data-ttu-id="b31c8-107">您可以將範本加入儲存體帳戶，並在部署期間使用 SAS Token 連結它們。</span><span class="sxs-lookup"><span data-stu-id="b31c8-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b31c8-108">遵循下列步驟，則僅有帳戶擁有者可以存取包含範本的 Blob。</span><span class="sxs-lookup"><span data-stu-id="b31c8-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="b31c8-109">不過，當您建立 Blob 的 SAS Token 時，具備該 URI 的任何人都可以存取該 Blob。</span><span class="sxs-lookup"><span data-stu-id="b31c8-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="b31c8-110">如果另一位使用者攔截了 URI，該使用者也能存取範本。</span><span class="sxs-lookup"><span data-stu-id="b31c8-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="b31c8-111">使用 SAS Token 是限制存取您的範本的好方法，但您不應該將機密資料 (如密碼) 直接包含在範本中。</span><span class="sxs-lookup"><span data-stu-id="b31c8-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="b31c8-112">下列範例會設定私用儲存體帳戶容器並上傳範本︰</span><span class="sxs-lookup"><span data-stu-id="b31c8-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="b31c8-113">在部署期間提供 SAS Token</span><span class="sxs-lookup"><span data-stu-id="b31c8-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="b31c8-114">若要在儲存體帳戶中部署私人範本，請產生 SAS Token 並將它包含在範本的 URI 中。</span><span class="sxs-lookup"><span data-stu-id="b31c8-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="b31c8-115">設定到期時間，以允許足夠的時間來完成部署。</span><span class="sxs-lookup"><span data-stu-id="b31c8-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get the URI with the SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="b31c8-116">如需使用包含已連結範本的 SAS Token 範例，請參閱 [透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="b31c8-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b31c8-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b31c8-117">Next steps</span></span>
* <span data-ttu-id="b31c8-118">如需部署範本的簡介，請參閱[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="b31c8-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="b31c8-119">如需部署範本的完整範例指令碼，請參閱[部署 Resource Manager 範本指令碼](resource-manager-samples-powershell-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="b31c8-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="b31c8-120">若要在範本中定義參數，請參閱 [編寫範本](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="b31c8-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="b31c8-121">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="b31c8-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

