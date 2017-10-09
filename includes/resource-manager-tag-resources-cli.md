tooadd 標記 tooa 資源群組、 使用**azure 群組集**。 如果 hello 資源群組並沒有任何現有的標記，傳入 hello 標記。

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

標記會以整體方式更新。 如果您想要 tooadd 標記 tooa 資源群組具有現有的標記，傳遞所有 hello 標記。 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

資源群組中的資源不會繼承標籤。 tooadd 標記 tooa 資源時，使用**azure 資源集**。 傳遞 hello hello 資源類型，您要加入 hello 標記加入至應用程式開發介面版本號碼。 如果您需要 tooretrieve hello API 版本，請使用下列命令與 hello hello 類型的資源提供者，您要設定的 hello:

```azurecli
azure provider show -n Microsoft.Storage --json
```

在 hello 結果中，尋找您想要的 hello 資源類型。

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

現在，提供該 API 版本、資源群組名稱、資源名稱、資源類型、標籤值做為參數值。

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

標記是直接存在於資源和資源群組中。 toosee hello 現有的標籤，取得資源群組和其資源與**azure 群組顯示**。

```azurecli
azure group show -n tag-demo-group --json
```

它會傳回有關 hello 資源群組，包括任何標籤套用 tooit 中繼資料。

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

使用檢視的特定資源的 hello 標記**azure 資源顯示**。

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve 所有 hello 資源標記值，都使用：

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve 標記值，所有的 hello 資源群組使用：

```azurecli
azure group list -t Dept=Finance
```

您可以檢視您的訂用帳戶中的 hello 現有的標記以 hello 下列命令：

```azurecli
azure tag list
```
