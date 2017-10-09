<span data-ttu-id="de051-101">3.0 版的 hello AzureRm.Resources 模組包含在使用標記的重大變更。</span><span class="sxs-lookup"><span data-stu-id="de051-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="de051-102">繼續之前，請檢查您的版本︰</span><span class="sxs-lookup"><span data-stu-id="de051-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="de051-103">如果您的結果會顯示版本 3.0 或更新版本，本主題中的 hello 範例會使用您的環境。</span><span class="sxs-lookup"><span data-stu-id="de051-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="de051-104">如果版本不是 3.0 或更新版本，在進行本主題之前，請先使用 PowerShell 資源庫或 Web Platform Installer 來[更新版本](/powershell/azureps-cmdlets-docs/)。</span><span class="sxs-lookup"><span data-stu-id="de051-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="de051-105">toosee hello 的現有標籤*資源群組*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="de051-106">該指令碼會傳回下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="de051-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="de051-107">toosee hello 的現有標籤*資源具有指定的資源識別碼*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="de051-108">或 toosee hello 的現有標籤*具有指定的名稱和資源群組的資源*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="de051-109">tooget*具有特定標記的資源群組*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="de051-110">tooget*具有特定標記的資源*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="de051-111">每次您套用標籤 tooa 資源或資源群組，您就會覆寫 hello 現有資源或資源群組上的標記。</span><span class="sxs-lookup"><span data-stu-id="de051-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="de051-112">因此，您必須使用不同的方式根據 hello 資源或資源群組是否擁有現有的標記。</span><span class="sxs-lookup"><span data-stu-id="de051-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="de051-113">tooadd 標記 tooa*沒有現有的標記的資源群組*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="de051-114">tooadd 標記 tooa*有現有的標記的資源群組*、 擷取 hello 現有的標記、 新增 hello 新標記，以及重新套用 hello 標籤：</span><span class="sxs-lookup"><span data-stu-id="de051-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="de051-115">tooadd 標記 tooa*沒有現有的標記資源*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="de051-116">tooadd 標記 tooa*具有現有的標記資源*，使用：</span><span class="sxs-lookup"><span data-stu-id="de051-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="de051-117">資源群組 tooits，從資源標記的所有 tooapply 和*不會保留現有的都標記 hello 資源*，使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="de051-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="de051-118">資源群組 tooits，從資源標記的所有 tooapply 和*保留現有的都標記，不會有重複的資源上*，使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="de051-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="de051-119">tooremove 所有標籤，將都傳遞空的雜湊表：</span><span class="sxs-lookup"><span data-stu-id="de051-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



