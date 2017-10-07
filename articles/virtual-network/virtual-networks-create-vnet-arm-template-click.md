---
title: "aaaCreate 虛擬網路 |Azure Resource Manager 範本 |Microsoft 文件"
description: "了解如何 toocreate 的虛擬網路，使用 Azure Resource Manager 範本。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本建立虛擬網路

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure 有兩個部署模型：Azure Resource Manager 和傳統。 Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。 深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。
 
本文說明如何 toocreate hello 資源管理員部署到 VNet 模型使用 Azure Resource Manager 範本。 您也可以建立 VNet 資源管理員 」 透過使用其他工具，或從 hello 下列清單中選取不同的選項來建立 VNet 透過 hello 傳統部署模型：

> [!div class="op_single_selector"]
- [入口網站](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [範本](virtual-networks-create-vnet-arm-template-click.md)
- [入口網站 (傳統)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (傳統)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [CLI (傳統)](virtual-networks-create-vnet-classic-cli.md)

您將學習如何 toodownload 和修改與現有 ARM 範本從 GitHub，並部署從 GitHub、 PowerShell 和 hello Azure CLI hello 範本。

如果您只想要部署 hello ARM 範本，直接從 GitHub，不進行任何變更，請略過太[部署範本，以從 github](#deploy-the-arm-template-by-using-click-to-deploy)。

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>下載並了解 hello Azure Resource Manager 範本
您可以下載從 GitHub 建立 VNet 和兩個子網路的 hello 現有範本，進行任何變更，您可能會想要並重複使用它。 toodo，完成下列步驟的 hello:

1. 瀏覽過[hello 範例範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)。
2. 依序按一下 [azuredeploy.json] 和 [RAW]。
3. 在電腦上儲存 hello 檔案 tooa 本機資料夾。
4. 如果您已熟悉範本，請略過 toostep 7。
5. 開啟您剛才儲存的 hello 檔案，並查看下 hello 內容**參數**第 5 行中。 ARM 範本的參數提供值的預留位置，可以在部署期間填寫。
   
   | 參數 | 說明 |
   | --- | --- |
   | **位置** |將會建立 hello VNet 的 azure 地區 |
   | **vnetName** |名稱 hello 新的 VNet |
   | **addressPrefix** |Hello VNet，採用 CIDR 格式的位址空間 |
   | **subnet1Name** |Hello 名稱第一個 VNet |
   | **subnet1Prefix** |Hello 第一個子網路的 CIDR 區塊 |
   | **subnet2Name** |Hello 名稱的第二個 VNet |
   | **subnet2Prefix** |Hello 第二個子網路的 CIDR 區塊 |
   
   > [!IMPORTANT]
   > GitHub 所維護的 Azure 資源管理員範本可能會隨著時間改變。 請確定您使用之前，先檢查 hello 範本。
   > 
   > 
6. 檢查下的 hello 內容**資源**，並注意 hello 下列：
   
   * **type**。 Hello 範本所建立的資源類型。 在此案例中為 **Microsoft.Network/virtualNetworks**，代表 VNet。
   * **名稱**。 Hello 資源的名稱。 請注意 hello 使用**[parameters('vnetName')]**，它表示 hello 名稱會在部署期間提供做為輸入 hello 使用者或參數檔案。
   * **屬性**。 Hello 資源屬性的清單。 此範本會在 VNet 建立期間使用 hello 位址空間和子網路屬性。
7. 瀏覽回太[hello 範例範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)。
8. 依序按一下 [azuredeploy-paremeters.json] 和 [RAW]。
9. 在電腦上儲存 hello 檔案 tooa 本機資料夾。
10. 開啟您剛才儲存的 hello 檔案並編輯 hello hello 參數值。 使用下列值低於 toodeploy hello hello 案例中所描述的 VNet hello:

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. 儲存 hello 檔案。


## <a name="deploy-hello-template-using-powershell"></a>部署使用 PowerShell 的 hello 範本

完成下列步驟 toodeploy hello 範本，而您使用 PowerShell 下載 hello:

1. 安裝和設定 Azure PowerShell hello 中的 hello 步驟[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。
2. 新的資源群組執行下列命令 toocreate hello:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    hello 命令會建立名為的資源群組*TestRG*在 hello*美國中部*azure 區域。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。

    預期的輸出：

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. 執行下列命令 toodeploy hello 新的 VNet 使用 hello 範本和參數檔案下載，並修改上述的 hello:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    預期的輸出：
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. Hello 執行的下列命令的 hello tooview hello 屬性新的 VNet:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    預期的輸出：

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a>部署使用按一下部署的 hello 範本

您可以重複使用預先定義的 Azure 資源管理員範本上傳的 tooa GitHub 儲存機制由 Microsoft 和社群開啟 toohello 維護。 這些範本可以直接從 GitHub，部署或下載並修改 toofit 您的需求。 toodeploy 範本建立 VNet 兩個子網路，以完成下列步驟的 hello:

1. 從瀏覽器中，瀏覽過[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)。
2. 向下捲動 hello 清單的範本，然後按一下**101-vnet-兩個子網路**。 檢查 hello **README.md**檔案，如下所示。

    ![Github 中的 READEME.md 檔案](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. 按一下**部署 tooAzure**。 如有必要，請輸入您的 Azure 登入認證。 
4. 在 hello**參數**刀鋒視窗中，輸入您想 toouse toocreate 新的 VNet，然後再按一下 hello 值**確定**。 hello 如下圖所示為 hello 案例 hello 值：
   
    ![ARM 範本參數](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. 按一下**資源群組**，然後選取資源群組 tooadd hello VNet，或按一下**建立新**tooadd hello VNet tooa 新資源群組。 hello 如下圖所示 hello 資源群組設定新的資源群組，稱為**TestRG**:

    ![資源群組](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. 如有必要，變更 hello**訂用帳戶**和**位置**設定您的 VNet。
7. 如果您不想 toosee hello VNet 當做一個磚中 hello**開始面板**，停用**Pin tooStartboard**。
8. 按一下**法律條款**，閱讀 hello 條款，然後按一下**購買**tooagree。 
9. 按一下**建立**toocreate hello VNet。
   
    ![在 Preview 入口網站中提交部署磚](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Hello 部署完成之後，請在 hello Azure 入口網站按一下**更多服務**，型別*虛擬網路*在 hello 篩選出現的方塊，然後按一下 虛擬網路 toosee hello 虛擬網路刀鋒視窗。 在 hello 刀鋒視窗中，按一下  *TestVNet*。 在 hello *TestVNet*刀鋒視窗中，按一下 **子網路**toosee hello 建立子網路，hello 下列圖片所示：
    
     ![在 Preview 入口網站中建立 VNet](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>後續步驟

深入了解如何 tooconnect:

- 虛擬機器 (VM) tooa 虛擬網路讀取 hello[建立 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md)或[建立 Linux VM](../virtual-machines/linux/quick-create-portal.md)文件。 而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。
- 藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)發行項。
- 使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。 深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-arm.md)文件。
