

## <a name="multi-and-single-instance-vms"></a>多重和單一執行個體 VM
許多客戶執行於 Azure 計數重大其 Vm 經歷 toohello 停機時間-因為計劃性的維護時可以排程大約 15 分鐘-，就會發生在維護期間。 佈建的 Vm 接收計劃性的維護時，您可以使用可用性集合 toohelp 控制項。

有兩個可能的 VM 設定在 Azure 上執行。 VM 可能會設定為多重執行個體或單一執行個體。 如果 VM 在可用性設定組中，它們會隨後設定為多重執行個體。 請注意，即使單一 VM 也可以部署在可用性設定組中，所以才會被視為多重執行個體。 如果 VM 不在可用性設定組中，它們會隨後設定為單一執行個體。  如需可用性設定組的詳細資訊，請參閱[管理 hello 可用性的 Windows 虛擬機器](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[管理 hello 可用性的 Linux 虛擬機器](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

規劃的維護更新 toosingle 執行個體，且多個執行個體的 Vm 會個別進行。 藉由重新設定您的 Vm toobe 單一執行個體 （如果它們是多重執行個體） 或 toobe 多重執行個體 （如果它們是單一執行個體），您可以控制其 Vm 當收到 hello 計劃的維護。 如需 Azure VM 計劃性維護的詳細資料，請參閱 [Azure Linux 虛擬機器的維護計劃](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或 [Azure Windows 虛擬機器的維護計劃](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="for-multi-instance-configuration"></a>對於多重執行個體組態
您可以選取 hello 時間計劃性的維護，將會影響您在可用性設定組的組態中部署可用性設定組中移除這些 Vm 的 Vm。

1. 電子郵件會傳送 tooyou hello 計劃在多個執行個體設定的維護 tooyour Vm 之前的七個行事曆日期。 hello 訂用帳戶 Id 和 hello 電子郵件的 hello 主體中未包含 hello 影響多個執行個體 Vm 的名稱。
2. 在這些七天，您可以選擇 hello 時間將執行個體從其可用性設定組，在該區域中移除多個執行個體 Vm 會更新。 這項變更的設定會導致重新開機，為 hello 虛擬機器移動從一部實體主機，以維護，不是針對維護 tooanother 實體主機為目標。
3. 您可以從其可用性設定組中 hello Azure 入口網站移除 hello VM。

   1. 在 hello 入口網站中，選取 hello VM tooremove 從 hello 可用性設定組。  

   2. 在 [設定] 之下，按一下 [可用性設定組]。

      ![可用性設定組選取](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. 在 hello 可用性設定下拉式功能表中，選取 「 不屬於可用性設定組。 」

      ![從設定組移除](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. 在 hello 頂端，按一下**儲存**。 按一下**是**這個動作會重新啟動的 tooacknowledge hello VM。

   >[!TIP]
   >您可以選取其中一個列出的 hello 可用性設定組稍後重新設定 hello VM toomulti 執行個體。

4. 從可用性設定組中移除的 Vm 主機移動的 tooSingle 執行個體且 hello 計劃的維護 tooAvailability 設定組態期間未更新。
5. 一旦完成 hello 更新 tooAvailability 設定 Vm （依據 tooschedule hello 原始電子郵件中所述），您應該將 hello Vm 回其可用性設定組。 可用性設定組的一部分而變得重新 hello Vm 設定為多執行個體，並會導致重新開機。 一般而言，一旦完成所有的多個執行個體更新 hello 整個 Azure 環境之間，單一執行個體維護遵循。

使用 Azure PowerShell 也可以達成從可用性設定組中移除 VM：

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>對於單一執行個體組態
您可以選取 hello 計劃性的維護，將會影響您 Vm 單一執行個體組態中將這些 Vm 新增至可用性設定組的時間。

逐步說明

1. 電子郵件會傳送 tooyou hello 計劃的維護 tooVMs 單一執行個體組態中的前七個的行事曆日期。 hello 訂用帳戶 Id 和 hello 電子郵件的 hello 主體中未包含的受影響的 hello 單一執行個體 Vm 的名稱。
2. 在這些七天，您可以選擇 hello 時間執行個體中該相同的地區設定加入您的單一執行個體 Vm tooan 可用性的重新開機。 這項變更的設定會導致重新開機，為 hello 虛擬機器移動從一部實體主機，以維護，不是針對維護 tooanother 實體主機為目標。
3. 請依照下列指示這裡 tooadd 現有 Vm 到使用 hello Azure 入口網站和 Azure PowerShell 的可用性設定組。 (請參閱 hello Azure PowerShell 範例所示步驟執行。)
4. 一旦這些 Vm 會重新設定為多執行個體，將它們排除 hello 計劃的維護 tooSingle 執行個體 Vm。
5. Hello 單一執行個體 VM 更新完成之後 （依據 tooschedule hello 原始電子郵件），您可以傳回 hello Vm toosingle 執行個體，移除其可用性設定組中的 hello Vm。

新增 VM tooan 可用性設定組，也可以使用 PowerShell 來達成 Azure:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
