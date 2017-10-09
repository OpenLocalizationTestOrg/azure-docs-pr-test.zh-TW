
診斷問題的 Microsoft Azure 雲端服務需要 hello 問題發生時收集 hello 服務的虛擬機器上的記錄檔。 您可以使用 hello AzureLogCollector 延伸隨 tooperfom 單次收集記錄檔從一或多個雲端服務 Vm （從 web 角色和背景工作角色） 和傳送嗨收集檔案 tooan Azure 儲存體帳戶 – 完全不需要從遠端登入tooany 的 hello Vm。

> [!NOTE]
> 可以在 http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp 找到大部分的 hello 記錄資訊的描述。
> 
> 

有兩個模式的集合收集檔案 toobe hello 類型而定。

* 僅限 Azure 客體代理程式記錄檔 (GA)。 這個收集模式包含所有 hello 記錄相關的 tooAzure 客體代理程式及其他 Azure 元件。
* 所有的記錄檔 (完整)。 此收集模式將會收集 GA 模式中的所有檔案，外加：
  
  * 系統和應用程式事件記錄檔
  * HTTP 錯誤記錄檔
  * IIS 記錄檔
  * 安裝記錄檔
  * 其他系統記錄檔

在這兩個集合模式中，使用下列結構的 hello 的集合可以指定其他資料集合資料夾：

* **名稱**: hello 名稱 hello 集合將用於做為子資料夾內 hello zip 檔案 toobe hello 名稱的收集。
* **位置**: hello 路徑 toohello 資料夾 hello 虛擬機器上的收集檔案的位置。
* **SearchPattern**: hello 模式的檔案 toobe hello 名稱的收集。 預設值為 "*"
* **遞迴**： 如果將會收集的遞迴 hello 資料夾下的 hello 檔案。

## <a name="prerequisites"></a>必要條件
* 您需要 toohave 儲存體帳戶的延伸模組產生的 toosave zip 檔案。
* 您必須確定使用的是 Azure PowerShell Cmdlet V0.8.0 或更新版本。 如需詳細資訊，請參閱 [Azure 下載](https://azure.microsoft.com/downloads/)。

## <a name="add-hello-extension"></a>加入 hello 擴充功能
您可以使用[Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet 或[服務管理 REST Api](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector 延伸模組。

雲端服務的 hello 現有的 Azure Powershell cmdlet， **Set-azureserviceextension**，可以是雲端服務角色執行個體上的使用的 tooenable hello 延伸模組。 每次透過這個 cmdlet 會啟用這項擴充功能，所選角色的 hello 選取角色執行個體觸發記錄檔集合。

虛擬機器的 hello 現有的 Azure Powershell cmdlet，**組 AzureVMExtension**，可以是虛擬機器上的使用的 tooenable hello 延伸模組。 每次透過 hello cmdlet 會啟用此延伸模組，每個執行個體觸發記錄檔集合。

就內部而言，此延伸模組所使用的 JSON 型 PublicConfiguration hello 和 PrivateConfiguration。 hello 以下是範例 JSON 公用和私用組態的 hello 版面配置。

### <a name="publicconfiguration"></a>PublicConfiguration
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> 此延伸模組不需要 **privateConfiguration**。 您可以只提供空的結構 hello **– PrivateConfiguration**引數。
> 
> 

您可以遵循下列其中一個 hello 兩個步驟 tooadd hello AzureLogCollector tooone 或雲端服務或虛擬機器的觸發程序 hello 上每個 VM toorun 集合和傳送嗨收集檔案 tooAzure 帳戶所選角色的多個執行個體指定。

## <a name="adding-as-a-service-extension"></a>新增為服務延伸模組
1. 請遵循 hello 指示 tooconnect Azure PowerShell tooyour 訂用帳戶。
2. 指定 hello 服務名稱、 位置、 角色和角色執行個體 toowhich tooadd 並啟用 hello AzureLogCollector 延伸模組。
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. 指定要收集檔案的 hello 其他資料資料夾 （這是選擇性步驟）。
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > 您可以使用語彙基元`%roleroot%`toospecify hello 角色根磁碟機因為它不會使用固定磁碟機。
   > 
   > 
4. 提供將上傳 hello Azure 儲存體帳戶名稱和金鑰 toowhich 收集檔案。
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. 雲端服務，如下所示 tooenable hello AzureLogCollector 延伸模組為呼叫 hello SetAzureServiceLogCollector.ps1 （包含在 hello hello 文章結尾處）。 Hello 執行完成後，您可以找到下的 hello 上傳檔案`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

hello 下列是 hello 傳遞 toohello 指令碼的 hello 參數定義。 (也可以從下方加以複製。)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* *ServiceName*：您的雲端服務名稱。
* *Roles*：一份角色清單，例如 “WebRole1” 或 ”WorkerRole1”。
* *執行個體*： 逗號分隔清單的 hello 角色執行個體名稱--請使用 hello 萬用字元字串 ("*") 的所有角色執行個體。
* *Slot*：位置名稱。 「生產」或「預備」。
* *Mode*：收集模式。 「完整」或「GA」。
* *StorageAccountName*：用來儲存收集之資料的 Azure 儲存體帳戶名稱。
* *StorageAccountKey*：Azure 儲存體帳戶金鑰的名稱。
* *AdditionalDataLocationList*: hello 下列結構的清單：
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>新增為 VM 延伸模組
請遵循 hello 指示 tooconnect Azure PowerShell tooyour 訂用帳戶。

1. 指定 hello 服務名稱、 VM 和 hello 收集模式。
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. 提供將上傳 hello Azure 儲存體帳戶名稱和金鑰 toowhich 收集檔案。
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. 雲端服務，如下所示 tooenable hello AzureLogCollector 延伸模組為呼叫 hello SetAzureVMLogCollector.ps1 （包含在 hello hello 文章結尾處）。 Hello 執行完成後，您可以找到下 https://YouareStorageAccountName.blob.core.windows.net/vmlogs hello 上傳檔案

hello 下列是 hello 傳遞 toohello 指令碼的 hello 參數定義。 (也可以從下方加以複製。)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* ServiceName：您的雲端服務名稱。
* VMName hello hello VM 名稱。
* Mode：收集模式。 「完整」或「GA」。
* StorageAccountName：用來儲存收集之資料的 Azure 儲存體帳戶名稱。
* StorageAccountKey：Azure 儲存體帳戶金鑰的名稱。
* AdditionalDataLocationList: Hello 下列結構的清單：

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>延伸模組 PowerShell 指令碼檔案
SetAzureServiceLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


SetAzureVMLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a>後續步驟
現在，您可以從一個非常簡單的位置檢查或複製您的記錄檔。

