


可用性設定組可協助您的虛擬機器在停機期間 (例如維護期間) 仍然保持可用狀態。 將兩個以上類似設定的虛擬機器放置於可用性集合建立 hello 需要備援 toomaintain 可用性 hello 應用程式或服務執行您的虛擬機器。 如需有關其運作方式的詳細資訊，請參閱[管理虛擬機器可用性 hello][Manage hello availability of virtual machines]。

它是最佳的作法 toouse 可用性設定組和負載平衡端點 toohelp 確保您的應用程式永遠可用且持續執行有效率。 如需負載平衡端點的詳細資訊，請參閱 [Azure 基礎結構服務的負載平衡][Load balancing for Azure infrastructure services]。

您可以使用下列兩個選項的其中之一，將傳統虛擬機器加入可用性設定組：

* [選項 1： 建立虛擬機器和可用性設定組 hello 在相同時間][Option 1: Create a virtual machine and an availability set at hello same time]。 然後，加入新的虛擬機器 toohello 建立這些虛擬機器時設定。
* [選項 2： 將現有的虛擬機器 tooan 可用性集][Option 2: Add an existing virtual machine tooan availability set]。

> [!NOTE]
> 在 hello 傳統模型中，虛擬機器中所要 tooput hello 相同可用性設定組必須屬於 toohello 相同雲端服務。
> 
> 

## <a id="createset"></a>選項 1： 建立虛擬機器和可用性設定組 hello 在相同時間
您可以使用任一 hello Azure 入口網站或 Azure PowerShell 命令 toodo 這。

toouse hello Azure 入口網站：

1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下  **+ 新增**，然後按一下**虛擬機器**。
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. 選取您想 toouse 的 hello Marketplace 虛擬機器映像。 您可以選擇 toocreate Linux 或 Windows 虛擬機器。
4. Hello 所選虛擬機器，請確認該 hello 部署模型設定得**傳統**，然後按一下**建立**
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. 輸入虛擬機器名稱、使用者名稱和密碼 (Windows 機器) 或 SSH 公開金鑰 (Linux 機器)。 
6. 選擇 hello VM 大小，然後按一下**選取**toocontinue。
7. 選擇**選擇性組態 > 可用性設定組**，然後選取您想要 tooadd hello 虛擬機器的 hello 可用性設定組。
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. 檢閱組態設定。 完成之後，請按一下 [建立] 。
9. 當 Azure 建立虛擬機器時，您可以追蹤在 hello 進度**虛擬機器**hello 中樞功能表中。

toouse Azure PowerShell 命令 toocreate Azure 虛擬機器並將它加入 tooa 新的或現有的可用性設定組，請參閱[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>選項 2： 加入現有的虛擬機器 tooan 可用性集
在 hello Azure 入口網站，您可以新增現有的傳統虛擬機器 tooan 現有的可用性設定組或建立一個新的。 (請記住 hello 中的虛擬機器 hello 相同可用性設定組必須屬於 toohello 相同雲端服務。)hello 步驟幾乎是 hello 相同。 使用 Azure PowerShell，您可以加入 hello 虛擬機器 tooan 現有可用性設定組。

1. 如果您尚未這樣做，登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **虛擬機器 （傳統）**。
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. 從 hello 的虛擬機器的清單，選取 hello 想 tooadd toohello 組的 hello 虛擬機器名稱。
4. 選擇**可用性設定組**hello 虛擬機器從**設定**。
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. 選取您想要 tooadd hello 虛擬機器的 hello 可用性設定組。 hello 虛擬機器必須屬於 toohello 相同雲端服務為 hello 可用性設定組。
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. 按一下 [儲存] 。

toouse Azure PowerShell 命令，開啟管理員層級 Azure PowerShell 工作階段，然後執行下列命令的 hello。 Hello 預留位置 (例如&lt;VmCloudServiceName&gt;)，取代 hello 引號，包括 hello < 和 > 字元內的所有內容，請以 hello 更正名稱。

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> hello 虛擬機器可能必須重新啟動 toobe toofinish 將它加入 toohello 可用性設定組。
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

