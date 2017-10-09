3.0 版的 hello AzureRm.Resources 模組包含在使用標記的重大變更。 繼續之前，請檢查您的版本︰

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

如果您的結果會顯示版本 3.0 或更新版本，本主題中的 hello 範例會使用您的環境。 如果版本不是 3.0 或更新版本，在進行本主題之前，請先使用 PowerShell 資源庫或 Web Platform Installer 來[更新版本](/powershell/azureps-cmdlets-docs/)。

```powershell
Version
-------
3.5.0
```

toosee hello 的現有標籤*資源群組*，使用：

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

該指令碼會傳回下列格式的 hello:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee hello 的現有標籤*資源具有指定的資源識別碼*，使用：

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

或 toosee hello 的現有標籤*具有指定的名稱和資源群組的資源*，使用：

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget*具有特定標記的資源群組*，使用：

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget*具有特定標記的資源*，使用：

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

每次您套用標籤 tooa 資源或資源群組，您就會覆寫 hello 現有資源或資源群組上的標記。 因此，您必須使用不同的方式根據 hello 資源或資源群組是否擁有現有的標記。 

tooadd 標記 tooa*沒有現有的標記的資源群組*，使用：

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd 標記 tooa*有現有的標記的資源群組*、 擷取 hello 現有的標記、 新增 hello 新標記，以及重新套用 hello 標籤：

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd 標記 tooa*沒有現有的標記資源*，使用：

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd 標記 tooa*具有現有的標記資源*，使用：

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

資源群組 tooits，從資源標記的所有 tooapply 和*不會保留現有的都標記 hello 資源*，使用下列指令碼的 hello:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

資源群組 tooits，從資源標記的所有 tooapply 和*保留現有的都標記，不會有重複的資源上*，使用下列指令碼的 hello:

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

tooremove 所有標籤，將都傳遞空的雜湊表：

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



