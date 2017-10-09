<span data-ttu-id="f9178-101">tooadd 標記 tooa 資源群組、 使用**azure 群組集**。</span><span class="sxs-lookup"><span data-stu-id="f9178-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="f9178-102">如果 hello 資源群組並沒有任何現有的標記，傳入 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="f9178-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="f9178-103">標記會以整體方式更新。</span><span class="sxs-lookup"><span data-stu-id="f9178-103">Tags are updated as a whole.</span></span> <span data-ttu-id="f9178-104">如果您想要 tooadd 標記 tooa 資源群組具有現有的標記，傳遞所有 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="f9178-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="f9178-105">資源群組中的資源不會繼承標籤。</span><span class="sxs-lookup"><span data-stu-id="f9178-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="f9178-106">tooadd 標記 tooa 資源時，使用**azure 資源集**。</span><span class="sxs-lookup"><span data-stu-id="f9178-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="f9178-107">傳遞 hello hello 資源類型，您要加入 hello 標記加入至應用程式開發介面版本號碼。</span><span class="sxs-lookup"><span data-stu-id="f9178-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="f9178-108">如果您需要 tooretrieve hello API 版本，請使用下列命令與 hello hello 類型的資源提供者，您要設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="f9178-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="f9178-109">在 hello 結果中，尋找您想要的 hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="f9178-109">In hello results, look for hello resource type you want.</span></span>

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

<span data-ttu-id="f9178-110">現在，提供該 API 版本、資源群組名稱、資源名稱、資源類型、標籤值做為參數值。</span><span class="sxs-lookup"><span data-stu-id="f9178-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="f9178-111">標記是直接存在於資源和資源群組中。</span><span class="sxs-lookup"><span data-stu-id="f9178-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="f9178-112">toosee hello 現有的標籤，取得資源群組和其資源與**azure 群組顯示**。</span><span class="sxs-lookup"><span data-stu-id="f9178-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="f9178-113">它會傳回有關 hello 資源群組，包括任何標籤套用 tooit 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f9178-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

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

<span data-ttu-id="f9178-114">使用檢視的特定資源的 hello 標記**azure 資源顯示**。</span><span class="sxs-lookup"><span data-stu-id="f9178-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="f9178-115">tooretrieve 所有 hello 資源標記值，都使用：</span><span class="sxs-lookup"><span data-stu-id="f9178-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="f9178-116">tooretrieve 標記值，所有的 hello 資源群組使用：</span><span class="sxs-lookup"><span data-stu-id="f9178-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="f9178-117">您可以檢視您的訂用帳戶中的 hello 現有的標記以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="f9178-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
