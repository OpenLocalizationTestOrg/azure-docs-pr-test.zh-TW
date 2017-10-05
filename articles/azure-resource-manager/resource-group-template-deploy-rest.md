---
title: "使用 REST API 和範本部署資源 | Microsoft Docs"
description: "使用 Azure Resource Manager 和 Resource Manager REST API 將資源部署到 Azure。 資源會定義在 Resource Manager 範本中。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 46856a25fb57bb2c5a3c1aeae13c11655e1a58a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="b7d2b-104">使用 Resource Manager 範本和 Resource Manager REST API 部署資源</span><span class="sxs-lookup"><span data-stu-id="b7d2b-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7d2b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7d2b-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="b7d2b-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b7d2b-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="b7d2b-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="b7d2b-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="b7d2b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="b7d2b-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="b7d2b-109">這篇文章說明如何使用 Resource Manager REST API 與 Resource Manager 範本來將您的資源部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> <span data-ttu-id="b7d2b-110">如需部署期間偵錯錯誤的說明，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="b7d2b-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="b7d2b-111">[檢視部署作業](resource-manager-deployment-operations.md)，以了解有關取得可協助您針對錯誤進行疑難排解的資訊</span><span class="sxs-lookup"><span data-stu-id="b7d2b-111">[View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="b7d2b-112">[針對使用 Azure Resource Manager 將資源部署至 Azure 時常見的錯誤進行疑難排解](resource-manager-common-deployment-errors.md) ，以了解如何解決常見的部署錯誤</span><span class="sxs-lookup"><span data-stu-id="b7d2b-112">[Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="b7d2b-113">您的範本可以是本機檔案，或者是透過 URI 提供使用的外部檔案。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="b7d2b-114">當您的範本位於儲存體帳戶中時，您可以限制範本的存取權，並在部署期間提供共用存取簽章 (SAS) Token</span><span class="sxs-lookup"><span data-stu-id="b7d2b-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="b7d2b-115">使用 REST API 部署</span><span class="sxs-lookup"><span data-stu-id="b7d2b-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="b7d2b-116">設定[一般參數和標頭](https://docs.microsoft.com/rest/api/index) (包括驗證權杖)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="b7d2b-117">如果您沒有現有資源群組，請建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="b7d2b-118">提供您的訂用帳戶識別碼、新資源群組的名稱，以及需要解決方案的位置。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="b7d2b-119">如需詳細資訊，請參閱[建立資源群組](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="b7d2b-120">請先執行[驗證範本部署作業](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate)來驗證部署，然後再執行部署。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="b7d2b-121">測試部署時，請提供與執行部署時完全一致的參數 (如下個步驟所示)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="b7d2b-122">建立部署。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-122">Create a deployment.</span></span> <span data-ttu-id="b7d2b-123">提供您的訂用帳戶識別碼、資源群組的名稱、部署的名稱，以及範本的連結。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="b7d2b-124">如需範本檔案的相關資訊，請參閱[參數檔案](#parameter-file)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="b7d2b-125">如需以 REST API 建立資源群組的相關詳細資訊，請參閱[建立範本部署](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="b7d2b-126">請注意，**mode** 是設為 **Incremental**。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="b7d2b-127">若要執行完整部署，請將 **mode** 設為 **Complete**。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="b7d2b-128">使用完整模式時請務必謹慎，因為您可能會不小心刪除不在範本中的資源。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="b7d2b-129">如果您想要記錄回應內容及/或要求內容，可在要求中包括 **debugSetting** 。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="b7d2b-130">您可以設定儲存體帳戶以使用共用存取簽章 (SAS) Token。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="b7d2b-131">如需詳細資訊，請參閱[使用共用存取簽章委派存取](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="b7d2b-132">取得範本部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-132">Get the status of the template deployment.</span></span> <span data-ttu-id="b7d2b-133">如需詳細資訊，請參閱[取得範本部署的相關資訊](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="b7d2b-134">參數檔案</span><span class="sxs-lookup"><span data-stu-id="b7d2b-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="b7d2b-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7d2b-135">Next steps</span></span>
* <span data-ttu-id="b7d2b-136">若要了解如何處理非同步 REST 作業，請參閱[追蹤非同步 Azure 作業 (英文)](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="b7d2b-137">如需透過 .NET 用戶端程式庫部署資源的範例，請參閱 [使用 .NET 程式庫與範本部署資源](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="b7d2b-138">若要在範本中定義參數，請參閱 [編寫範本](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="b7d2b-139">如需將您的方案部署到不同環境的指引，請參閱 [Microsoft Azure 中的開發和測試環境](solution-dev-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="b7d2b-140">如需關於企業如何使用 Resource Manager 有效地管理訂用帳戶的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="b7d2b-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

