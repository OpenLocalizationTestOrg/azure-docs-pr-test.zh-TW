## <a name="scenario"></a>案例
使用單一 NIC VM 是 tooa 建立且已連線虛擬網路。 hello VM 需要有三個不同*私人*IP 位址和兩個*公用*IP 位址。 hello IP 位址指派 toohello IP 設定：

* **IPConfig-1：**指派「靜態」私人 IP 位址和「靜態」公用 IP 位址。
* **IPConfig-2：**指派「靜態」私人 IP 位址和「靜態」公用 IP 位址。
* **IPConfig-3：**指派「靜態」私人 IP 位址，不指派任何公用 IP 位址。
  
    ![多個 IP 位址](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

當建立 NIC 的 hello 與 hello NIC 附加的 toohello VM hello VM 建立時，hello IP 組態會關聯的 toohello NIC。 hello 案例使用的 IP 位址的 hello 型別是為了說明。 您可以指派您需要的任何 IP 位址和作業類型。

> [!NOTE]
> 這篇文章雖然 hello 中步驟指派所有 IP 組態 tooa 單一 NIC，您也可以指派多個 IP 組態 tooany 多個 NIC VM 中的 NIC。 toolearn toocreate 具有多個 Nic，VM 的讀取方式 hello[建立具有多個 Nic VM](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md)發行項。
