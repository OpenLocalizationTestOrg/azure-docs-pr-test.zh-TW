<span data-ttu-id="95f05-101">在部署期間，資源 tootag 新增 hello`tags`您要部署的項目 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="95f05-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="95f05-102">提供 hello 標記名稱和值。</span><span class="sxs-lookup"><span data-stu-id="95f05-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="95f05-103">套用常值 toohello 標記名稱</span><span class="sxs-lookup"><span data-stu-id="95f05-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="95f05-104">hello 下列範例示範兩個標記的儲存體帳戶 (`Dept`和`Environment`) 設定 tooliteral 值：</span><span class="sxs-lookup"><span data-stu-id="95f05-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

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

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="95f05-105">適用於物件 toohello 標記項目</span><span class="sxs-lookup"><span data-stu-id="95f05-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="95f05-106">您可以定義物件參數，其中儲存數個標記，並套用該物件 toohello 標記項目。</span><span class="sxs-lookup"><span data-stu-id="95f05-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="95f05-107">Hello 物件中的每個屬性會變成 hello 資源個別標記。</span><span class="sxs-lookup"><span data-stu-id="95f05-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="95f05-108">hello 下列範例有一個名為參數`tagValues`也就是套用的 toohello 標記項目。</span><span class="sxs-lookup"><span data-stu-id="95f05-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

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

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="95f05-109">適用於 JSON 字串 toohello 標記名稱</span><span class="sxs-lookup"><span data-stu-id="95f05-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="95f05-110">toostore 許多值，在單一標記中，適用於表示 hello 值的 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="95f05-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="95f05-111">hello 整個 JSON 字串都會儲存為一個標籤，不能超過 256 個字元。</span><span class="sxs-lookup"><span data-stu-id="95f05-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="95f05-112">hello 下列範例具有名為單一標記`CostCenter`，其中包含從 JSON 字串的數個值：</span><span class="sxs-lookup"><span data-stu-id="95f05-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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