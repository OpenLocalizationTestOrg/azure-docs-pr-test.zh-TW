## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>如何使用 Azure CLI 傳統 VNet toocreate
您可以使用 hello Azure CLI toomanage hello 命令提示字元，從任何執行 Windows、 Linux 或是 OSX 電腦從您的 Azure 資源。 toocreate VNet 使用 hello Azure CLI，請遵循下列 hello 步驟。

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../articles/cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello **azure 網路 vnet 建立**命令 toocreate VNet 和子網路，如下所示。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    預期的輸出：
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**。 建立 hello VNet toobe 的名稱。 在本文案例中為 *TestVNet*
   * **-e (或 --address-space)**。 VNet 位址空間。 在本文案例中為 *192.168.0.0*
   * **-i (或 -cidr)**。 CIDR 格式的網路遮罩。 在本文案例中為 *16*。
   * **-n (或 --subnet-name**)。 Hello 第一個子網路的名稱。 在本文案例中為 *FrontEnd*。
   * **-p (或 --subnet-start-ip)**。 子網路的起始 IP 位址或子網路位址空間。 在本文案例中為 *192.168.1.0*。
   * **-r (或 --subnet-cidr)**。 CIDR 格式的子網路網路遮罩。 在本文案例中為 *24*。
   * **-l (或 --location)**。 將會建立 hello VNet 的 azure 區域。 在本文案例中為「美國中部」 。
3. 執行 hello **azure 網路 vnet 子網路建立**命令 toocreate 如下所示的子網路。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    以下是 hello 上述命令中的 hello 預期輸出：
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (或 --vnet-name)**。 Hello hello 子網路將會建立的 VNet 的名稱。 在本文案例中為 *TestVNet*。
   * **-n (or --name)**。 Hello 新的子網路的名稱。 在本文案例中為 *BackEnd*。
   * **-a (或 --address-prefix)**。 子網路 CIDR 區塊。 在本文案例中為 *192.168.2.0/24*。
4. 執行 hello **azure 網路 vnet 顯示**命令 hello 新的 vnet tooview hello 屬性，如下所示。
   
            azure network vnet show
   
    以下是 hello 上述命令中的 hello 預期輸出：
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

