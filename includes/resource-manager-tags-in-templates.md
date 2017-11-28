<span data-ttu-id="94283-101">若要在部署期間標記資源，請將 `tags` 元素新增到您正在部署的資源。</span><span class="sxs-lookup"><span data-stu-id="94283-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="94283-102">提供標籤名稱和值。</span><span class="sxs-lookup"><span data-stu-id="94283-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="94283-103">將常值套用至標記名稱</span><span class="sxs-lookup"><span data-stu-id="94283-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="94283-104">下列範例說明含有兩個標籤 (`Dept` 和 `Environment`) 並設為常值的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="94283-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="94283-105">將物件套用至標記元素</span><span class="sxs-lookup"><span data-stu-id="94283-105">Apply an object to the tag element</span></span>
<span data-ttu-id="94283-106">您可定義存放數個標籤的物件參數，並將該物件套用至標籤元素。</span><span class="sxs-lookup"><span data-stu-id="94283-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="94283-107">物件中的每個屬性會變成資源的個別標籤。</span><span class="sxs-lookup"><span data-stu-id="94283-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="94283-108">下列範例具有名為 `tagValues` 且套用至標籤元素的參數。</span><span class="sxs-lookup"><span data-stu-id="94283-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="94283-109">將 JSON 字串套用至標記名稱</span><span class="sxs-lookup"><span data-stu-id="94283-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="94283-110">若要將多個值儲存於單一標籤，請套用代表這些值的 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="94283-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="94283-111">整個 JSON 字串會儲存為一個不得超過 256 個字元的標籤。</span><span class="sxs-lookup"><span data-stu-id="94283-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="94283-112">下列範例具有名為 `CostCenter` 的單一標籤，其中包含 JSON 字串中的數個值︰</span><span class="sxs-lookup"><span data-stu-id="94283-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```