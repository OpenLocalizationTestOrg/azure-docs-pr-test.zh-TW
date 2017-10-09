在部署期間，資源 tootag 新增 hello`tags`您要部署的項目 toohello 資源。 提供 hello 標記名稱和值。

### <a name="apply-a-literal-value-toohello-tag-name"></a>套用常值 toohello 標記名稱
hello 下列範例示範兩個標記的儲存體帳戶 (`Dept`和`Environment`) 設定 tooliteral 值：

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

### <a name="apply-an-object-toohello-tag-element"></a>適用於物件 toohello 標記項目
您可以定義物件參數，其中儲存數個標記，並套用該物件 toohello 標記項目。 Hello 物件中的每個屬性會變成 hello 資源個別標記。 hello 下列範例有一個名為參數`tagValues`也就是套用的 toohello 標記項目。

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

### <a name="apply-a-json-string-toohello-tag-name"></a>適用於 JSON 字串 toohello 標記名稱

toostore 許多值，在單一標記中，適用於表示 hello 值的 JSON 字串。 hello 整個 JSON 字串都會儲存為一個標籤，不能超過 256 個字元。 hello 下列範例具有名為單一標記`CostCenter`，其中包含從 JSON 字串的數個值：  

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