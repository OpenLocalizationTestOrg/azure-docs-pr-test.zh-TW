您可以連接 tooa 是已部署的 tooyour VNet 建立遠端桌面連線 tooyour VM 的 VM。 hello 最佳方式 tooinitially 確認您可以連線的 VM 是由 tooconnect tooyour 使用其私人 IP 位址，而非電腦名稱。 這樣一來，您要測試 toosee 如果您可以連接，不是否名稱解析設定正確。

1. 找出 hello 私人 IP 位址。 您可以用多種方式找到 VM 的 hello 私人 IP 位址。 以下，我們會顯示 hello 步驟 hello Azure 入口網站和 PowerShell。

  - Azure 入口網站位在 hello Azure 入口網站中尋找您的虛擬機器。 檢視 hello hello VM 的屬性。 會列出 hello 私用 IP 位址。

  - PowerShell-使用 hello 範例 tooview Vm 和私人 IP 位址，從資源群組的清單。 您不需要 toomodify 此範例中，再使用它。

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. 確認您是否已連線的 tooyour VNet 使用 hello VPN 連線。
3. 開啟**遠端桌面連線**hello hello 工作列上的搜尋方塊中輸入"RDP 」 或 「 遠端桌面連線 」，然後選取 遠端桌面連線。 您也可以開啟 遠端桌面連線在 PowerShell 中使用 hello 'mstsc' 命令。 
4. 在遠端桌面連線中，輸入 hello VM 的 hello 私人 IP 位址。 您可以按一下 [顯示選項] tooadjust 其他設定，然後連接。

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot RDP 連線 tooa VM

如果您無法透過 VPN 連線連線 tooa 虛擬機器，請檢查 hello 下列：

- 確認您的 VPN 連線成功。
- 請確認您所連接的 hello VM toohello 私人 IP 位址。
- 如果您可以連接 toohello VM 使用 hello 私人 IP 位址，但不是 hello 電腦名稱，請確認已正確設定 DNS。 如需 VM 的名稱解析運作方式的詳細資訊，請參閱 [VM 的名稱解析](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。
- 如需 RDP 連線的詳細資訊，請參閱[疑難排解遠端桌面連線 tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)。
