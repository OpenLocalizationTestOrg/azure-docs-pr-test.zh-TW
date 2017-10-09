如果您無法透過 VPN 連線連線 tooa 虛擬機器，請檢查 hello 下列：

- 確認您的 VPN 連線成功。
- 請確認您所連接的 hello VM toohello 私人 IP 位址。
- 如果您可以連接 toohello VM 使用 hello 私人 IP 位址，但不是 hello 電腦名稱，請確認已正確設定 DNS。 如需 VM 的名稱解析運作方式的詳細資訊，請參閱 [VM 的名稱解析](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。

當您透過點對站連線時，請檢查下列其他項目 hello:

- 使用 'ipconfig' toocheck hello 分派 toohello hello 從中您所連接的電腦上的乙太網路介面卡的 IPv4 位址。 如果您要連接到的 VNet hello hello 位址範圍內，或您 VPNClientAddressPool hello 位址範圍內 hello IP 位址，這是參照的 tooas 重疊的位址空間。 當您的位址空間重疊，如此一來時，hello 網路流量不會連線到 Azure 時，它將會存留在 hello 區域網路。
- 請確認該 hello VPN 用戶端組態封裝產生之後指定 hello VNet hello DNS 伺服器 IP 位址。 如果您更新 hello DNS 伺服器 IP 位址時，產生並安裝新的 VPN 用戶端組態封裝。

如需疑難排解 RDP 連線的詳細資訊，請參閱[疑難排解遠端桌面連線 tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)。
