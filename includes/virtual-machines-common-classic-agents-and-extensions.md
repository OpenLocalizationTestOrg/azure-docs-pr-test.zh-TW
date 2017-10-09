

VM 擴充功能可協助您：

* 修改安全性與身分識別的功能，例如重設帳戶值和使用反惡意程式碼
* 啟動、停止或設定監視和診斷
* 重設或安裝連線功能，例如 RDP 和 SSH
* 診斷、監視和管理您的 VM

也有許多其他功能。 會定期發行新的 VM 擴充功能。 本文說明 hello Azure VM 代理程式的 Windows 和 Linux 及它們如何支援 VM 延伸模組功能。 如需依功能分類的 VM 延伸模組清單，請參閱 [Azure VM 延伸模組與功能](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="azure-vm-agents-for-windows-and-linux"></a>適用於 Windows 和 Linux 的 Azure VM 代理程式
hello Azure 虛擬機器代理程式 （VM 代理程式） 的安全、 輕量級程序是安裝、 設定和移除執行個體的 Azure 虛擬機器上的 VM 擴充功能。 hello VM 代理程式做為 Azure VM 的 hello 安全本機控制服務。 hello 代理程式載入的 hello 延伸模組所提供特定功能 tooincrease 產能使用 hello 執行個體。

有兩個 Azure VM 代理程式存在，一個適用於 Windows VM，一個適用於 Linux VM。

如果您想要虛擬機器執行個體 toouse 一或多個 VM 擴充功能，hello 執行個體必須已安裝的 VM 代理程式。 使用 hello Azure 入口網站和從 hello 映像建立的虛擬機器映像**Marketplace**會自動安裝 VM 代理程式在 hello 建立程序。 如果虛擬機器執行個體缺少 VM 代理程式，您可以在建立 hello 虛擬機器執行個體之後，安裝 hello VM 代理程式。 或者，您可以安裝 hello 代理程式，然後上傳自訂 VM 映像中。

> [!IMPORTANT]
> 這些 VM 代理程式非常精簡的服務，能夠進行虛擬機器執行個體的安全管理。 可能不想 hello VM 代理程式所在的情況。 如果是這樣，是確定 toocreate Vm 沒有 hello 使用 hello Azure CLI 或 PowerShell 安裝 VM 代理程式。 雖然可以實際移除 hello VM 代理程式，但是 hello 執行個體上的 VM 擴充功能的 hello 行為未定義。 因此，不支援移除已安裝的 VM 代理程式。
>

在下列情況下的 hello 中啟用 hello VM 代理程式：

* 當您建立的 VM 執行個體使用 hello Azure 入口網站，然後選取映像從 hello **Marketplace**，
* 當您建立的 VM 執行個體使用 hello [New-azurevm](https://msdn.microsoft.com/library/azure/dn495254.aspx)或 hello [New-azurequickvm](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet。 您可以建立的 VM 沒有 VM 代理程式藉由新增 hello **– DisableGuestAgent**參數 toohello [Add-azureprovisioningconfig](https://msdn.microsoft.com/library/azure/dn495299.aspx)指令程式，

* 當您手動下載及 hello VM 代理程式安裝在現有的 VM 執行個體，並設定 hello **ProvisionGuestAgent**值太**true**。 您可以藉由使用 PowerShell 命令或 REST 呼叫，針對 Windows 和 Linux 代理程式使用這項技術。 (如果您未設定 hello **ProvisionGuestAgent**手動安裝 VM 代理程式，VM 代理程式未正確地偵測到的 hello hello 新增 hello 之後的值。) hello 下列程式碼範例顯示如何 toodo 這其中 hello 使用 PowerShell`$svc`和`$name`已經決定引數：

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* 當您建立 VM 映像時，會包含已安裝的 VM 代理程式。 一旦 hello 映像以 hello VM 代理程式已存在，您可以上傳該映像 tooAzure。 針對 Windows VM，下載 hello [Windows VM 代理程式.msi 檔案](http://go.microsoft.com/fwlink/?LinkID=394789)並安裝 VM 代理程式 hello。 針對 Linux VM，安裝 VM 代理程式從 hello GitHub 儲存機制位於的 hello <https://github.com/Azure/WALinuxAgent>。 如需有關如何 tooinstall hello Linux 上的 VM 代理程式的詳細資訊，請參閱 hello [Azure Linux VM 代理程式使用者指南](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

> [!NOTE]
> 在 PaaS hello VM 代理程式稱為**WindowsAzureGuestAgent**，而且一律適用於 Web 和背景工作角色 Vm。 (如需詳細資訊，請參閱[Azure 角色架構](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx)。) hello 角色 Vm 的 VM 代理程式現在可以在 hello 中加入擴充功能 toohello 雲端服務 Vm 相同的方式，它會為永續性虛擬機器。 hello 最大持續性 Vm 角色 Vm 上的 VM 擴充功能之間的差異時，會加入 hello VM 擴充功能。 使用角色 Vm，擴充功能會加入第一個 toohello 雲端服務，然後 toohello 部署雲端服務內。
>
> 使用[Get-azureserviceavailableextension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet toolist 所有可用角色 VM 擴充功能。
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>尋找、加入、更新和移除 VM 擴充功能
如需這些工作的詳細資訊，請參閱[加入、尋找、更新及移除 Azure VM 延伸模組](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
