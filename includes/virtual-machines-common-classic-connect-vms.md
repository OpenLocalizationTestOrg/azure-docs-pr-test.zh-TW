

![獨立雲端服務中的虛擬機器](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

如果您將虛擬機器放在虛擬網路中，您可以決定多少的雲端服務，您想要針對 toouse 負載平衡和可用性集。 此外，您可以將組織 hello 虛擬機器在 hello 的子網路上相同方式與您內部網路，而且連線 hello 虛擬網路 tooyour 內部部署網路。 以下是範例：

![虛擬網路中的虛擬機器](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

虛擬網路是建議的方式 tooconnect Azure 虛擬機器中的 hello。 hello 最佳作法是 tooconfigure 個別的雲端服務中的應用程式的每一層。 不過，您可能需要 toocombine 部分虛擬機器從 hello 到不同的應用程式層相同雲端服務 tooremain hello 最大值為 200 的雲端服務，每個訂用帳戶內。 tooreview 這和其他限制，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../articles/azure-subscription-service-limits.md)。

## <a name="connect-vms-in-a-virtual-network"></a>連接虛擬網路中的 VM
tooconnect 虛擬網路中的虛擬機器：

1. 建立 hello 虛擬網路中 hello [Azure 入口網站](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md)並指定 '傳統部署'。
2. 建立用於部署 tooreflect 的雲端服務的 hello 組您的設計為可用性設定組和負載平衡。 在 hello Azure 入口網站，按一下 **新增 > 計算 > 雲端服務**每個雲端服務。

  當您填寫 hello 雲端服務詳細資料，請選擇 hello 相同_資源群組_搭配 hello 虛擬網路。

3. toocreate 每個新虛擬機器，請按一下**新增 > 計算**，然後選取 hello 適當的 VM 映像從 hello**熱門應用程式**。

  在 hello VM**基本概念**刀鋒視窗中，選擇 hello 相同_資源群組_搭配 hello 虛擬網路。

  ![使用 VNet 時的 VM 基本概念刀鋒視窗](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. 當您填寫 hello VM**設定**，選擇正確的 hello_雲端服務_或_虛擬網路_hello VM。

  Azure 將會選取 hello 其他項目會根據您選取。

  ![使用 VNet 時的 VM 設定刀鋒視窗](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>連接獨立雲端服務中的 VM
tooconnect 獨立雲端服務中的虛擬機器：

1. 建立 hello 的雲端服務中 hello [Azure 入口網站](http://portal.azure.com)。 按一下 [新增] > [計算] > [雲端服務]。 或者，當您建立您第一部虛擬機器時，您可以建立您的部署的 hello 雲端服務。
2. 當您建立 hello 虛擬機器時，請選擇的 hello 與 hello 雲端服務使用相同的資源群組。

  ![新增虛擬機器 tooan 現有雲端服務](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  當您填寫 hello VM 詳細資料時，選擇 hello hello 第一個步驟中建立的雲端服務名稱。

  ![選取虛擬機器的雲端服務](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
