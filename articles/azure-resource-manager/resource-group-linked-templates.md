---
title: "連結 Azure 部署的範本 | Microsoft Docs"
description: "描述如何在「Azure 資源管理員」範本中使用連結的範本，以建立模組化範本方案。 示範如何傳遞參數值、指定參數檔案，以及動態建立 URL。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="e883b-104">部署 Azure 資源時使用連結的範本</span><span class="sxs-lookup"><span data-stu-id="e883b-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="e883b-105">您可以從某個 Azure Resource Manager 範本連結到另一個範本，這樣可讓您將部署分解成一組具有目標與特定目的的範本。</span><span class="sxs-lookup"><span data-stu-id="e883b-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="e883b-106">就像將應用程式分解為數個程式碼類別，分解有利於測試、重複使用和可讀性。</span><span class="sxs-lookup"><span data-stu-id="e883b-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="e883b-107">您可以從主要範本傳遞參數到連結的範本，且那些參數可以直接對應到由發出呼叫之範本所公開的參數或變數。</span><span class="sxs-lookup"><span data-stu-id="e883b-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="e883b-108">連結的範本也可以將輸出變數傳遞回來源範本，讓範本之間可進行雙向資料交換。</span><span class="sxs-lookup"><span data-stu-id="e883b-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="e883b-109">連結至範本</span><span class="sxs-lookup"><span data-stu-id="e883b-109">Linking to a template</span></span>
<span data-ttu-id="e883b-110">您可以透過在主要範本中新增指向連結的範本之部署資源，以在兩個範本之間建立連結。</span><span class="sxs-lookup"><span data-stu-id="e883b-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="e883b-111">將 **templateLink** 屬性設為連結的範本之 URI。</span><span class="sxs-lookup"><span data-stu-id="e883b-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="e883b-112">您可以直接在範本或參數檔中為連結的範本提供參數值。</span><span class="sxs-lookup"><span data-stu-id="e883b-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="e883b-113">以下範例會使用 **parameters** 屬性直接指定參數值。</span><span class="sxs-lookup"><span data-stu-id="e883b-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="e883b-114">如同其他資源類型，您可以設定連結的範本和其他資源之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="e883b-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="e883b-115">因此，當其他資源需要來自連結的範本的輸出值時，您就能夠確定已在資源需要之前部署連結的範本。</span><span class="sxs-lookup"><span data-stu-id="e883b-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="e883b-116">或者，當連結的範本仰賴其他資源時，您可以確定已在連結的範本之前先部署其他資源。</span><span class="sxs-lookup"><span data-stu-id="e883b-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="e883b-117">您可以使用下列語法，擷取連結的範本的值：</span><span class="sxs-lookup"><span data-stu-id="e883b-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="e883b-118">Azure Resource Manager 服務必須能夠存取連結的範本。</span><span class="sxs-lookup"><span data-stu-id="e883b-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="e883b-119">您無法為連結的範本指定本機檔案或只可在本機網路存取的檔案。</span><span class="sxs-lookup"><span data-stu-id="e883b-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="e883b-120">您可以只提供 URI 值，其中包含 **http** 或 **https**。</span><span class="sxs-lookup"><span data-stu-id="e883b-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="e883b-121">有一個選項是將連結的範本放在儲存體帳戶中，並將 URI 用於該項目，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e883b-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="e883b-122">雖然連結的範本必須可從外部存取，但它不必供大眾存取。</span><span class="sxs-lookup"><span data-stu-id="e883b-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="e883b-123">您可以將您的範本新增至只有儲存體帳戶擁有者可以存取的私人儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e883b-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="e883b-124">接著，在部署期間建立共用存取簽章 (SAS) Token 來啟用存取權。</span><span class="sxs-lookup"><span data-stu-id="e883b-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="e883b-125">您會將該 SAS Token 加入連結範本的 URI。</span><span class="sxs-lookup"><span data-stu-id="e883b-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="e883b-126">如需在儲存體帳戶中設定範本並產生 SAS Token 的步驟，請參閱[使用 Resource Manager 範本與 Azure PowerShell 部署資源](resource-group-template-deploy.md)或 [Deploy resources with Resource Manager templates and Azure CLI (使用 Resource Manager 範本和 Azure CLI 部署資源)](resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="e883b-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="e883b-127">以下範例顯示連結到其他範本的父範本。</span><span class="sxs-lookup"><span data-stu-id="e883b-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="e883b-128">連結的範本是透過以參數傳遞的 SAS Token 來存取。</span><span class="sxs-lookup"><span data-stu-id="e883b-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="e883b-129">即使該 Token 是以安全字串來傳遞，連結範本的 URI (包括 SAS Token) 還是會記錄在部署作業中。</span><span class="sxs-lookup"><span data-stu-id="e883b-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="e883b-130">為了限制公開的程度，請為該 Token 設定到期日。</span><span class="sxs-lookup"><span data-stu-id="e883b-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="e883b-131">Resource Manager 會以個別部署的方式來處理每一個連結的範本。</span><span class="sxs-lookup"><span data-stu-id="e883b-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="e883b-132">在資源群組的部署歷程記錄中，您會看到父項範本和巢狀範本的個別部署。</span><span class="sxs-lookup"><span data-stu-id="e883b-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![部署歷程記錄](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="e883b-134">連結到參數檔案</span><span class="sxs-lookup"><span data-stu-id="e883b-134">Linking to a parameter file</span></span>
<span data-ttu-id="e883b-135">下一個範例會使用 **parametersLink** 屬性連接至參數檔案。</span><span class="sxs-lookup"><span data-stu-id="e883b-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="e883b-136">連結參數檔案的 URI 值不能是本機檔案，而且必須包含 **http** 或 **https**。</span><span class="sxs-lookup"><span data-stu-id="e883b-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="e883b-137">當然，也可以將參數檔案限制為透過 SAS Token 存取。</span><span class="sxs-lookup"><span data-stu-id="e883b-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="e883b-138">使用變數來連結範本</span><span class="sxs-lookup"><span data-stu-id="e883b-138">Using variables to link templates</span></span>
<span data-ttu-id="e883b-139">先前的範例示範了範本連結的硬式編碼 URL 值。</span><span class="sxs-lookup"><span data-stu-id="e883b-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="e883b-140">這種方法可能適用於簡單的範本，但不適合一組大型的模組化範本。</span><span class="sxs-lookup"><span data-stu-id="e883b-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="e883b-141">不過，您可以建立一個儲存主要範本之基底 URL 的靜態變數，然後再從該基底 URL 連結動態建立連結的範本之 URL。</span><span class="sxs-lookup"><span data-stu-id="e883b-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="e883b-142">這個方法的好處是您可以輕鬆地移動範本或建立分支範本，因為您只需要變更主要範本中的靜態變數。</span><span class="sxs-lookup"><span data-stu-id="e883b-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="e883b-143">主要範本會於整個分解的範本傳遞正確的 URI。</span><span class="sxs-lookup"><span data-stu-id="e883b-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="e883b-144">下列範例示範如何使用基底 URL 來為連結的範本 (**sharedTemplateUrl** 和 **vmTemplate**) 建立兩個 URL。</span><span class="sxs-lookup"><span data-stu-id="e883b-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="e883b-145">您也可以使用 [deployment()](resource-group-template-functions-deployment.md#deployment) 取得目前範本的基底 URL，用來取得相同位置中其他範本的 URL。</span><span class="sxs-lookup"><span data-stu-id="e883b-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="e883b-146">如果您的範本位置變更 (可能是版本不同所造成)，或您想要避免在範本檔案中使用硬式編碼 URL，這十分實用。</span><span class="sxs-lookup"><span data-stu-id="e883b-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="e883b-147">完整範例</span><span class="sxs-lookup"><span data-stu-id="e883b-147">Complete example</span></span>
<span data-ttu-id="e883b-148">以下範例範本顯示連結範本的簡化設定，以說明本文章中的幾個概念。</span><span class="sxs-lookup"><span data-stu-id="e883b-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="e883b-149">範例會假設已經將範本新增到儲存體帳戶中的同一個容器，且已經關閉公開存取。</span><span class="sxs-lookup"><span data-stu-id="e883b-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="e883b-150">連結的範本會在 **outputs** 區段中將一個值傳遞給主範本。</span><span class="sxs-lookup"><span data-stu-id="e883b-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="e883b-151">**parent.json** 檔案的組成：</span><span class="sxs-lookup"><span data-stu-id="e883b-151">The **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="e883b-152">**helloworld.json** 檔案的組成：</span><span class="sxs-lookup"><span data-stu-id="e883b-152">The **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="e883b-153">在 PowerShell 中，您會取得容器的 Token 並使用下列方式部署範本：</span><span class="sxs-lookup"><span data-stu-id="e883b-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="e883b-154">在 Azure CLI 2.0 中，您會取得容器的 Token 並使用下列指令碼部署範本：</span><span class="sxs-lookup"><span data-stu-id="e883b-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="e883b-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e883b-155">Next steps</span></span>
* <span data-ttu-id="e883b-156">若要了解如何定義您資源的部署順序，請參閱 [定義 Azure Resource Manager 範本中的相依性](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="e883b-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="e883b-157">若要了解如何定義一個資源，但建立它的多個執行個體，請參閱 [在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="e883b-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

