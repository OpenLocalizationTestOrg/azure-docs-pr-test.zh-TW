---
title: "Azure 部署的 aaaLink 範本 |Microsoft 文件"
description: "描述如何 toouse 會連結中的 Azure Resource Manager 範本 toocreate 範本模組化的範本方案。 說明如何 toopass 參數值，指定參數檔案，並動態地被建立 Url。"
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
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="8bb95-104">部署 Azure 資源時使用連結的範本</span><span class="sxs-lookup"><span data-stu-id="8bb95-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="8bb95-105">從在一個 Azure 資源管理員範本，您可以連結 tooanother 範本，可讓您 toodecompose 您部署至一組目標、 目的特定範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="8bb95-106">就像將應用程式分解為數個程式碼類別，分解有利於測試、重複使用和可讀性。</span><span class="sxs-lookup"><span data-stu-id="8bb95-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="8bb95-107">您可以從主要範本 tooa 連結的範本，傳遞參數，這些參數可以直接對應 tooparameters 或 hello 呼叫範本所公開的變數。</span><span class="sxs-lookup"><span data-stu-id="8bb95-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="8bb95-108">hello 連結的範本也可以傳遞的輸出變數後 toohello 來源範本，請啟用雙向資料之間交換的範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="8bb95-109">連結 tooa 範本</span><span class="sxs-lookup"><span data-stu-id="8bb95-109">Linking tooa template</span></span>
<span data-ttu-id="8bb95-110">您建立兩個範本加入該點 toohello 連結的範本內 hello 主要範本部署資源之間的連結。</span><span class="sxs-lookup"><span data-stu-id="8bb95-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="8bb95-111">設定 hello **templateLink**屬性 toohello hello 連結範本的 URI。</span><span class="sxs-lookup"><span data-stu-id="8bb95-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="8bb95-112">直接在您的範本或參數檔案中，您可以提供參數值為 hello 連結的範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="8bb95-113">hello 下列範例會使用 hello**參數**屬性 toospecify 直接的參數值。</span><span class="sxs-lookup"><span data-stu-id="8bb95-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

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

<span data-ttu-id="8bb95-114">如同其他資源類型，您可以設定 hello 連結的範本和其他資源之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="8bb95-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="8bb95-115">因此，當其他資源需要從 hello 連結的範本輸出值，您可以確定 hello 連結的範本部署之前。</span><span class="sxs-lookup"><span data-stu-id="8bb95-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="8bb95-116">或者，您也可以在 hello 連結的範本會依賴其他資源，您可以確定之前 hello 連結的範本部署其他資源。</span><span class="sxs-lookup"><span data-stu-id="8bb95-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="8bb95-117">您可以從連結的範本中擷取值，以 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="8bb95-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="8bb95-118">hello 資源管理員服務必須能夠 tooaccess hello 連結的範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="8bb95-119">您無法指定本機檔案或只適用於 hello 連結的範本的區域網路的檔案。</span><span class="sxs-lookup"><span data-stu-id="8bb95-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="8bb95-120">您可以只提供 URI 值，其中包含 **http** 或 **https**。</span><span class="sxs-lookup"><span data-stu-id="8bb95-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="8bb95-121">其中一個選項是的 tooplace 您連結的範本，在儲存體帳戶，並使用該項目，例如 hello 下列範例所示為 hello URI:</span><span class="sxs-lookup"><span data-stu-id="8bb95-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="8bb95-122">雖然 hello 連結的範本必須可從外部使用，但它不需要 toobe 上市 toohello 公用。</span><span class="sxs-lookup"><span data-stu-id="8bb95-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="8bb95-123">您可以加入範本 tooa 私用儲存體帳戶可存取 tooonly hello 儲存體帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="8bb95-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="8bb95-124">然後，在部署期間建立的共用的存取簽章 (SAS) 權杖 tooenable 存取。</span><span class="sxs-lookup"><span data-stu-id="8bb95-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="8bb95-125">您加入 hello 連結的範本的 SAS 權杖 toohello URI。</span><span class="sxs-lookup"><span data-stu-id="8bb95-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="8bb95-126">如需在儲存體帳戶中設定範本並產生 SAS Token 的步驟，請參閱[使用 Resource Manager 範本與 Azure PowerShell 部署資源](resource-group-template-deploy.md)或 [Deploy resources with Resource Manager templates and Azure CLI (使用 Resource Manager 範本和 Azure CLI 部署資源)](resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="8bb95-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="8bb95-127">hello 下列範例會顯示該連結 tooanother 範本父範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="8bb95-128">當做參數傳入的 SAS 權杖來存取 hello 連結的範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="8bb95-129">即使傳入 hello 語彙基元為安全字串，hello hello 連結的範本，包括 hello SAS 權杖，URI 會記錄在 hello 部署作業。</span><span class="sxs-lookup"><span data-stu-id="8bb95-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="8bb95-130">toolimit 曝光設定 hello 權杖到期日。</span><span class="sxs-lookup"><span data-stu-id="8bb95-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="8bb95-131">Resource Manager 會以個別部署的方式來處理每一個連結的範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="8bb95-132">在 hello hello 資源群組的部署歷程記錄，您會看到個別的 hello 父系和巢狀的範本部署。</span><span class="sxs-lookup"><span data-stu-id="8bb95-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![部署歷程記錄](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="8bb95-134">連結 tooa 參數檔案</span><span class="sxs-lookup"><span data-stu-id="8bb95-134">Linking tooa parameter file</span></span>
<span data-ttu-id="8bb95-135">hello 下一個範例會使用 hello **parametersLink**屬性 toolink tooa 參數檔案。</span><span class="sxs-lookup"><span data-stu-id="8bb95-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

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

<span data-ttu-id="8bb95-136">hello URI 值為 hello 連結的參數檔案不能是本機檔案，且必須包含**http**或**https**。</span><span class="sxs-lookup"><span data-stu-id="8bb95-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="8bb95-137">hello 參數檔案也可以限制的 tooaccess 透過 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="8bb95-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="8bb95-138">使用變數 toolink 範本</span><span class="sxs-lookup"><span data-stu-id="8bb95-138">Using variables toolink templates</span></span>
<span data-ttu-id="8bb95-139">hello 前述範例會示範硬式編碼 hello 範本連結的 URL 值。</span><span class="sxs-lookup"><span data-stu-id="8bb95-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="8bb95-140">這種方法可能適用於簡單的範本，但不適合一組大型的模組化範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="8bb95-141">相反地，您可以建立靜態變數以存放 hello 主要範本的基底 URL，然後從該基底 URL 的連結 hello 範本以動態方式建立 Url。</span><span class="sxs-lookup"><span data-stu-id="8bb95-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="8bb95-142">hello 這個方法的優點是您可以輕鬆地移動或 「 分叉 」 hello 範本，因為您只需要在 hello 主要範本 toochange hello 靜態變數。</span><span class="sxs-lookup"><span data-stu-id="8bb95-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="8bb95-143">hello 主要範本會傳遞 hello 正確 hello 整個 Uri 分解範本。</span><span class="sxs-lookup"><span data-stu-id="8bb95-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="8bb95-144">hello 下列範例示範如何 toouse 基底 URL toocreate 的兩個 Url 連結範本 (**sharedTemplateUrl**和**vmTemplate**)。</span><span class="sxs-lookup"><span data-stu-id="8bb95-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="8bb95-145">您也可以使用[deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello 基底 URL hello 目前的範本，然後將該 tooget hello URL 範本 hello 中相同的位置。</span><span class="sxs-lookup"><span data-stu-id="8bb95-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="8bb95-146">這個方法很有用，如果變更範本位置 (或許到期 tooversioning) 或您想 tooavoid 硬式編碼 hello 範本檔案中的 Url。</span><span class="sxs-lookup"><span data-stu-id="8bb95-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="8bb95-147">完整範例</span><span class="sxs-lookup"><span data-stu-id="8bb95-147">Complete example</span></span>
<span data-ttu-id="8bb95-148">下列範例範本的 hello 顯示連結的範本 tooillustrate 的簡化的排列 hello 概念的數個本文章中。</span><span class="sxs-lookup"><span data-stu-id="8bb95-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="8bb95-149">它會假設已加入 hello 範本 toohello 公用存取的儲存體帳戶中的相同容器已關閉。</span><span class="sxs-lookup"><span data-stu-id="8bb95-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="8bb95-150">hello 連結的範本會將值後 toohello 主要範本傳入 hello**輸出**> 一節。</span><span class="sxs-lookup"><span data-stu-id="8bb95-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="8bb95-151">hello **parent.json**檔案所組成：</span><span class="sxs-lookup"><span data-stu-id="8bb95-151">hello **parent.json** file consists of:</span></span>

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

<span data-ttu-id="8bb95-152">hello **helloworld.json**檔案所組成：</span><span class="sxs-lookup"><span data-stu-id="8bb95-152">hello **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="8bb95-153">在 PowerShell 中，您會取得 hello 容器的語彙基元，並部署與 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="8bb95-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="8bb95-154">在 Azure CLI 2.0 中，您會取得 hello 容器的語彙基元，並將 hello 範本部署以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="8bb95-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8bb95-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8bb95-155">Next steps</span></span>
* <span data-ttu-id="8bb95-156">toolearn 有關 hello 定義 hello 部署讓您的資源，請參閱[Azure Resource Manager 範本中定義的相依性](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="8bb95-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="8bb95-157">toolearn 方式 toodefine 一項資源而建立許多執行個體，請參閱[Azure 資源管理員中建立多個執行個體的資源](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="8bb95-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

