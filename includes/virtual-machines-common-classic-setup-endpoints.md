
每個端點都有一個公用連接埠和一個私人連接埠：

* hello 公用連接埠正由 hello Azure 負載平衡器 toolisten hello 網際網路從連入流量 toohello 虛擬機器。
* hello 私用連接埠是由 hello 虛擬機器 toolisten 用於連入流量，通常預定的 tooan 應用程式或服務 hello 虛擬機器上執行。

預設值為 hello IP 通訊協定，TCP 或 UDP 連接埠為已知的網路通訊協定提供當您建立端點以 hello Azure 入口網站。 自訂端點，您將需要 toospecify hello 正確 IP 通訊協定 （TCP 或 UDP） 和 hello 公用和私用連接埠。 toodistribute 隨機跨越多部虛擬機器的連入流量，您將需要 toocreate 組成的多個端點的負載平衡集。

建立端點後，您可以使用存取控制清單 (ACL) toodefine 規則來允許或拒絕 hello 連入流量 toohello 根據其來源 IP 位址的 hello 端點的公用連接埠。 不過，如果 hello 虛擬機器是在 Azure 虛擬網路，您應該改為使用網路安全性群組。 如需詳細資訊，請參閱 [關於網路安全性群組](../articles/virtual-network/virtual-networks-nsg.md)。

> [!NOTE]
> Azure 虛擬機器的防火牆組態會針對連接埠自動完成，該連接埠與 Azure 自動設定的遠端連線端點相關聯。 指定針對所有其他端點通訊埠，不會自動進行組態 toohello 防火牆 hello 虛擬機器。 當您建立 hello 虛擬機器的端點時，您將需要 tooensure hello hello 虛擬機器的防火牆，也可讓 hello 流量 hello 通訊協定和私人連接埠對應 toohello 端點組態。 tooconfigure hello 防火牆，請參閱 hello 文件或 hello 虛擬機器上執行的 hello 作業系統的線上說明。
>
>

## <a name="create-an-endpoint"></a>建立端點
1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**虛擬機器**，然後按一下您想 tooconfigure hello 虛擬機器的 hello 名稱。
3. 按一下**端點**在 hello**設定**群組。 hello**端點**頁面會列出所有的 hello 目前端點的 hello 虛擬機器。 Linux VM 依預設會顯示 SSH 的端點。 )

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![端點](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. 在 hello hello 端點項目的上方命令列，按一下 **新增**。
5. 在 hello**加入端點**頁面上，輸入的名稱中的 hello 端點**名稱**。
6. 在 [通訊協定] 中選擇 [TCP] 或 [UDP]。
7. 在**公用連接埠**，輸入 hello hello 的 hello 網際網路的連入流量的連接埠號碼。 在**私用連接埠**，輸入 hello 的 hello 虛擬機器所接聽的連接埠號碼。 這些連接埠號碼可以不同。 請確定該 hello hello 虛擬機器上的防火牆已設定的 tooallow hello 流量對應 toohello 通訊協定 （在步驟 6） 和私人連接埠。
10. 按一下 [確定] 。

hello 新端點就會列在 hello**端點**頁面。

![端點建立成功](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>管理端點上的 ACL hello
toodefine hello 組可以傳送流量的電腦，在端點上的 hello ACL 可以限制根據來源 IP 位址的流量。 請遵循這些步驟 tooadd、 修改或移除端點 ACL。

> [!NOTE]
> 如果 hello 端點是一組負載平衡的一部分，任何您所做變更 toohello 端點上的 ACL 是套用的 tooall 端點 hello 集合中。
>
>

如果 hello 虛擬機器是在 Azure 虛擬網路，而不是 Acl 的網路安全性群組建議。 如需詳細資訊，請參閱 [關於網路安全性群組](../articles/virtual-network/virtual-networks-nsg.md)。

1. 如果您尚未這樣做，請登入 toohello Azure 入口網站。
2. 按一下**虛擬機器**，然後按一下您想 tooconfigure hello 虛擬機器的 hello 名稱。
3. 按一下 [端點] 。 從 hello 清單中，選取 hello 適當的端點。 hello ACL 清單位於 hello hello 頁面的底部。

   ![指定 ACL 詳細資料](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. 使用 hello 清單 tooadd、 刪除或編輯規則中的資料列的 acl 並變更其順序。 hello**遠端子網路**值為 hello hello Azure 負載平衡器會使用 toopermit 或拒絕 hello 流量根據其來源 IP 位址的網際網路的連入流量的 IP 位址範圍。 採用 CIDR 格式，也就是位址首碼格式是確定 toospecify hello IP 位址範圍。 例如 `10.1.0.0/8`。

 ![新增 ACL 項目](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


您可以使用從特定的電腦對應 tooyour 電腦上，從特定的已知位址範圍的 hello 網際網路或 toodeny 流量規則 tooallow 唯一流量。

hello 規則會 hello 第一個規則的開始和結束與 hello 上一個規則的順序進行評估。 這表示，應該從最不嚴格 toomost 嚴格排序規則。 如需範例和詳細資訊，請參閱[什麼是網路存取控制清單](../articles/virtual-network/virtual-networks-acl.md)。
