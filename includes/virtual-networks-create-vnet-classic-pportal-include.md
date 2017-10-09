## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>如何 toocreate hello Azure 入口網站中的傳統 VNet
toocreate 傳統 VNet 根據 hello 案例以上版本，請遵循下列 hello 步驟。

1. 從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。
2. 按一下**新增** > **網路** > **虛擬網路**，請注意該 hello**選取部署模型**列出已顯示**傳統**，然後按一下**建立**、 hello 圖所示。
   
    ![在 Azure 入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. 在 hello**虛擬網路**刀鋒視窗中，型別 hello**名稱**hello VNet，然後再按一下**位址空間**。 設定 hello VNet 和其第一個子網路的位址空間設定，然後按一下 **確定**。 hello 下圖顯示我們的案例中的 hello CIDR 區塊設定。
   
    ![位址空間刀鋒視窗](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. 按一下**資源群組**，然後選取資源群組 tooadd hello VNet，或按一下**建立新的資源群組**tooadd hello VNet tooa 新資源群組。 hello 下圖顯示 hello 資源群組設定新的資源群組，稱為**TestRG**。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)。
   
    ![建立資源群組刀鋒視窗](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. 如有必要，變更 hello**訂用帳戶**和**位置**設定您的 VNet。 
6. 如果您不想 toosee hello VNet 當做一個磚中 hello**開始面板**，停用**Pin tooStartboard**。 
7. 按一下**建立**和名為注意事項 hello 磚**建立虛擬網路**hello 圖所示。
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. 稍候 hello VNet toobe 建立，然後當您看到磚下方，按一下它 tooadd hello 更多子網路。
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. 您應該會看見 hello**組態**為您的 VNet，如下所示。 
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. 依序按一下 子網路  >  新增，然後鍵入 名稱，並指定您子網路的 位址範圍 (CIDR 區塊)，然後按一下確定。 hello 下圖顯示我們目前的案例中的 hello 設定。
    
    ![在 Azure 入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

