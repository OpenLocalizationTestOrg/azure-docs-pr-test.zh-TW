您可以連接 tooa 是已部署的 tooyour VNet 建立遠端桌面連線 tooyour VM 的 VM。 hello 最佳方式 tooinitially 確認您可以連線的 VM 是由 tooconnect tooyour 使用其私人 IP 位址，而非電腦名稱。 這樣一來，您要測試 toosee 如果您可以連接，不是否名稱解析設定正確。 

1. 找到您的 VM hello 私人 IP 位址。 請查看 hello hello Azure 入口網站中 VM 的 hello 屬性，或使用 PowerShell，您可以找到 VM 的 hello 私人 IP 位址。
2. 確認您是否已連線的 tooyour VNet 使用 hello 點對站 VPN 連線。 
3. 開啟遠端桌面連線 hello 工作列上的 hello 搜尋方塊中輸入"RDP 」 或 「 遠端桌面連線 」，然後選取 遠端桌面連線。 您也可以開啟 遠端桌面連線在 PowerShell 中使用 hello 'mstsc' 命令。 
3. 在遠端桌面連線中，輸入 hello VM 的 hello 私人 IP 位址。 您可以按一下 [顯示選項] tooadjust 其他設定，然後連接。

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot RDP 連線 tooa VM

如果您無法透過 VPN 連線連線 tooa 虛擬機器，有幾件事，您可以檢查。 如需詳細的疑難排解資訊，請參閱[疑難排解遠端桌面連線 tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)。

- 確認您的 VPN 連線成功。
- 請確認您所連接的 hello VM toohello 私人 IP 位址。
- 使用 'ipconfig' toocheck hello 分派 toohello hello 從中您所連接的電腦上的乙太網路介面卡的 IPv4 位址。 如果您要連接到的 VNet hello hello 位址範圍內，或您 VPNClientAddressPool hello 位址範圍內 hello IP 位址，這是參照的 tooas 重疊的位址空間。 當您的位址空間重疊，如此一來時，hello 網路流量不會連線到 Azure 時，它將會存留在 hello 區域網路。
- 如果您可以連接 toohello VM 使用 hello 私人 IP 位址，但不是 hello 電腦名稱，請確認已正確設定 DNS。 如需 VM 的名稱解析運作方式的詳細資訊，請參閱 [VM 的名稱解析](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。
- 請確認該 hello VPN 用戶端組態封裝產生之後指定 hello VNet hello DNS 伺服器 IP 位址。 如果您更新 hello DNS 伺服器 IP 位址時，產生並安裝新的 VPN 用戶端組態封裝。
