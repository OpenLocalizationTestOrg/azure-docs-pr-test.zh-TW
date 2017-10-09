
* hello 轉換所需的 hello VM 重新啟動，因此排程在預先存在的維護期間的 hello 移轉的 Vm。 

* hello 轉換即無法復原。 

* 為確定 tootest hello 轉換。 在生產環境中執行 hello 移轉之前，先移轉測試虛擬機器。

* Hello 在轉換期間，您將解除配置 hello VM。 hello VM hello 轉換後啟動時，會收到新的 IP 位址。 如有需要您可以[指派靜態 IP 位址](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md)toohello VM。

* hello 原始 Vhd 和 hello hello VM 轉換前所使用的儲存體帳戶不會刪除。 他們繼續 tooincur 費用。 確認 hello 轉換已完成之後，這些成品，需要支付 tooavoid 刪除 hello 原始 VHD blob。
