


## <a name="using-vm-extensions"></a>使用 VM 擴充功能
Azure VM 延伸模組實作行為或功能，是協助 Azure Vm 上使用其他程式 (例如，hello **WebDeployForVSDevTest**延伸模組可讓 Visual Studio tooWeb 部署解決方案上的 Azure VM)，或提供hello 能力 toointeract hello VM toosupport 與其他的行為 （例如，您可以使用從 PowerShell、 hello Azure CLI 和 REST 用戶端 tooreset hello VM 存取擴充功能或修改 Azure VM 上的遠端存取值）。

> [!IMPORTANT]
> 依其支援的 hello 功能的擴充功能的完整清單，請參閱[Azure VM 延伸模組和功能](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 因為每個 VM 延伸模組支援特定功能，完全什麼您可以與具有副檔名無法執行的動作取決於 hello 延伸模組。 因此，在修改之前您的 VM，請確定您已閱讀 hello 文件以 hello 想 toouse VM 延伸模組。 不支援移除一些 VM 擴充功能。其他則具有已設定來大幅變更 VM 行為的屬性。
> 
> 

hello 最常見的工作如下：

1. 尋找可用的擴充功能
2. 更新已載入的擴充功能
3. 加入擴充功能
4. 移除擴充功能

## <a name="find-available-extensions"></a>尋找可用的擴充功能
您可以使用下列各項找到擴充功能和其他資訊：

* PowerShell
* Azure 跨平台命令列介面 (Azure CLI)
* 服務管理 REST API

### <a name="azure-powershell"></a>Azure PowerShell
有些延伸模組包含 PowerShell cmdlet 的特定 toothem，可能會建立其組態從 PowerShell 更容易。但 hello 下列 cmdlet 適用於所有 VM 擴充功能。

您可以使用下列 cmdlet tooobtain 資訊可用擴充功能的 hello:

* 執行個體的 web 角色或背景工作角色，您可以使用 hello [Get-azureserviceavailableextension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet。
* 執行個體的虛擬機器，您可以使用 hello [Get-azurevmavailableextension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet。
  
   例如，下列程式碼範例顯示如何來 hello toolist hello 的資訊**IaaSDiagnostics**使用 PowerShell 的延伸模組。
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Azure 命令列介面 (Azure CLI)
有些延伸模組包含特定 toothem Azure CLI 命令 （hello Docker VM 擴充功能是一個例子），這可能會讓其組態更容易。但 hello 下列命令的所有 VM 擴充功能的運作。

您可以使用 hello **azure vm 延伸模組清單**命令 tooobtain 資訊可用擴充功能，並使用 hello **--json**選項 toodisplay 一或多個擴充功能的相關的所有可用的資訊。 如果您未使用的副檔名，hello 命令傳回的 JSON 描述所有可用的擴充功能。

例如，hello 下列程式碼範例顯示如何 toolist hello 資訊 hello **IaaSDiagnostics**延伸模組使用 hello Azure CLI **azure vm 延伸模組清單**命令，並使用 hello **--json**選項 tooreturn 完整資訊。

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a>服務管理 REST API
您可以使用下列 REST Api tooobtain 資訊可用擴充功能的 hello:

* 執行個體的 web 角色或背景工作角色，您可以使用 hello[列出可用擴充功能](https://msdn.microsoft.com/library/dn169559.aspx)作業。 toolist hello 版本中可用的擴充功能，您可以使用[列出擴充功能版本](https://msdn.microsoft.com/library/dn495437.aspx)。
* 執行個體的虛擬機器，您可以使用 hello[列出資源擴充功能](https://msdn.microsoft.com/library/dn495441.aspx)作業。 toolist hello 版本中可用的擴充功能，您可以使用[列出資源擴充功能版本](https://msdn.microsoft.com/library/dn495440.aspx)。

## <a name="add-update-or-disable-extensions"></a>加入、更新或停用擴充功能
建立執行個體時，或者可以將它們加入 tooa 執行執行個體，可以加入擴充功能。 可以更新、停用或移除擴充功能。 您可以使用 Azure PowerShell cmdlet 或使用 hello 服務管理 REST API 作業來執行這些動作。 參數是必要的 tooinstall 和設定部分擴充功能。 擴充功能支援公用和私人參數。

### <a name="azure-powershell"></a>Azure PowerShell
使用 Azure PowerShell cmdlet 是 hello 最簡單方式 tooadd 和更新擴充功能。 當您使用 hello 延伸模組的 cmdlet 時，為您完成大部分的 hello 擴充的 hello 組態。 有時候，您可能需要 tooprogrammatically 加入延伸模組。 當您需要 toodo 此時，您必須提供 hello 擴充的 hello 組態。

您可以使用下列 cmdlet tooknow 擴充功能需要公用和私人參數的組態是否 hello:

* 執行個體的 web 角色或背景工作角色，您可以使用 hello **Get-azureserviceavailableextension** cmdlet。
* 執行個體的虛擬機器，您可以使用 hello **Get-azurevmavailableextension** cmdlet。

### <a name="service-management-rest-apis"></a>服務管理 REST API
當您使用 hello REST Api 擷取可用擴充功能清單時，您會收到 hello 延伸模組的 toobe 設定方式的相關資訊。 傳回的 hello 資訊可能會顯示由公用結構描述和私人結構描述表示的參數資訊。 關於 hello 執行個體的查詢會傳回公用參數值。 不會傳回私用參數值。

您可以使用下列 REST Api tooknow 擴充功能需要公用和私人參數的組態是否 hello:

* 針對 web 角色或背景工作角色執行個體 hello **PublicConfigurationSchema**和**PrivateConfigurationSchema**元素包含 hello hello 回應 hello 資訊[清單可用的擴充功能](https://msdn.microsoft.com/library/dn169559.aspx)作業。
* 針對虛擬機器的執行個體 hello **PublicConfigurationSchema**和**PrivateConfigurationSchema**元素包含 hello hello 回應 hello 資訊[清單資源擴充功能](https://msdn.microsoft.com/library/dn495441.aspx)作業。

> [!NOTE]
> 擴充功能也可以使用 JSON 所定義的組態。 當使用這些類型的擴充功能時，只有 hello **SampleConfig**使用項目。
> 
> 

