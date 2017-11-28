---
title: "使用 REST API 和範本 aaaDeploy 資源 |Microsoft 文件"
description: "使用 Azure 資源管理員和資源管理員 REST API toodeploy 資源 tooAzure。 hello 資源的資源管理員範本中定義。"
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
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="13551-104">使用 Resource Manager 範本和 Resource Manager REST API 部署資源</span><span class="sxs-lookup"><span data-stu-id="13551-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13551-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13551-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="13551-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="13551-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="13551-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="13551-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="13551-108">REST API</span><span class="sxs-lookup"><span data-stu-id="13551-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="13551-109">本文說明如何 toouse hello 資源管理員 REST API 與資源管理員範本 toodeploy 資源 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="13551-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="13551-110">如需部署期間偵錯錯誤的說明，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="13551-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="13551-111">[檢視部署作業](resource-manager-deployment-operations.md)toolearn 有關取得資訊可協助您疑難排解您的錯誤</span><span class="sxs-lookup"><span data-stu-id="13551-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="13551-112">[部署資源 tooAzure 與 Azure 資源管理員時，針對常見錯誤進行疑難排解](resource-manager-common-deployment-errors.md)toolearn 如何 tooresolve 常見的部署錯誤</span><span class="sxs-lookup"><span data-stu-id="13551-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="13551-113">您的範本可以是本機檔案，或者是透過 URI 提供使用的外部檔案。</span><span class="sxs-lookup"><span data-stu-id="13551-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="13551-114">當您的範本位於儲存體帳戶時，就可以限制存取 toohello 範本，並在部署期間提供的共用的存取簽章 (SAS) token。</span><span class="sxs-lookup"><span data-stu-id="13551-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="13551-115">部署以 hello REST API</span><span class="sxs-lookup"><span data-stu-id="13551-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="13551-116">設定[一般參數和標頭](https://docs.microsoft.com/rest/api/index) (包括驗證權杖)。</span><span class="sxs-lookup"><span data-stu-id="13551-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="13551-117">如果您沒有現有資源群組，請建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="13551-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="13551-118">提供您的訂用帳戶 ID、 hello 名稱 hello 新的資源群組，以及您需要為您的方案的位置。</span><span class="sxs-lookup"><span data-stu-id="13551-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="13551-119">如需詳細資訊，請參閱[建立資源群組](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate)。</span><span class="sxs-lookup"><span data-stu-id="13551-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="13551-120">驗證您的部署之前先執行 hello[驗證範本部署](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate)作業。</span><span class="sxs-lookup"><span data-stu-id="13551-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="13551-121">在測試 hello 部署時，提供參數，相同的方式執行 hello 部署 （顯示 hello 下一個步驟中） 時。</span><span class="sxs-lookup"><span data-stu-id="13551-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="13551-122">建立部署。</span><span class="sxs-lookup"><span data-stu-id="13551-122">Create a deployment.</span></span> <span data-ttu-id="13551-123">提供您的訂用帳戶 ID、 hello hello 資源群組名稱、 hello 部署的 hello 名稱和連結 tooyour 範本。</span><span class="sxs-lookup"><span data-stu-id="13551-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="13551-124">Hello 範本檔案的相關資訊，請參閱[參數檔](#parameter-file)。</span><span class="sxs-lookup"><span data-stu-id="13551-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="13551-125">如需 hello REST API toocreate 資源群組的詳細資訊，請參閱[建立範本部署](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate)。</span><span class="sxs-lookup"><span data-stu-id="13551-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="13551-126">請注意 hello**模式**設定得**Incremental**。</span><span class="sxs-lookup"><span data-stu-id="13551-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="13551-127">toorun 完整部署，設定**模式**太**完成**。</span><span class="sxs-lookup"><span data-stu-id="13551-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="13551-128">請小心使用 hello 完整模式，您可以不小心刪除不在範本中的資源時。</span><span class="sxs-lookup"><span data-stu-id="13551-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="13551-129">如果您想要 toolog 回應內容、 要求內容，或兩者，包含**debugSetting** hello 要求中。</span><span class="sxs-lookup"><span data-stu-id="13551-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="13551-130">您可以設定您的儲存體帳戶 toouse 共用的存取簽章 (SAS) token。</span><span class="sxs-lookup"><span data-stu-id="13551-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="13551-131">如需詳細資訊，請參閱[使用共用存取簽章委派存取](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)。</span><span class="sxs-lookup"><span data-stu-id="13551-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="13551-132">取得 hello 範本部署的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="13551-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="13551-133">如需詳細資訊，請參閱[取得範本部署的相關資訊](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)。</span><span class="sxs-lookup"><span data-stu-id="13551-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="13551-134">參數檔案</span><span class="sxs-lookup"><span data-stu-id="13551-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="13551-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13551-135">Next steps</span></span>
* <span data-ttu-id="13551-136">toolearn 有關處理非同步 REST 作業，請參閱[追蹤非同步的 Azure 作業](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="13551-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="13551-137">如需部署透過 hello.NET 用戶端程式庫資源的範例，請參閱[部署使用.NET 程式庫和範本的資源](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="13551-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="13551-138">toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="13551-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="13551-139">如需部署解決方案 toodifferent 環境需求的指引，請參閱[Microsoft Azure 中的開發和測試環境](solution-dev-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="13551-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="13551-140">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="13551-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

