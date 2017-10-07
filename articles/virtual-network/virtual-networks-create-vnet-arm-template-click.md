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
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="6ca4d-103">使用 Azure Resource Manager 範本建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6ca4d-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="6ca4d-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6ca4d-105">Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="6ca4d-106">深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="6ca4d-107">本文說明如何 toocreate hello 資源管理員部署到 VNet 模型使用 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="6ca4d-108">您也可以建立 VNet 資源管理員 」 透過使用其他工具，或從 hello 下列清單中選取不同的選項來建立 VNet 透過 hello 傳統部署模型：</span><span class="sxs-lookup"><span data-stu-id="6ca4d-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="6ca4d-109">入口網站</span><span class="sxs-lookup"><span data-stu-id="6ca4d-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="6ca4d-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ca4d-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="6ca4d-111">CLI</span><span class="sxs-lookup"><span data-stu-id="6ca4d-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="6ca4d-112">範本</span><span class="sxs-lookup"><span data-stu-id="6ca4d-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="6ca4d-113">入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="6ca4d-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="6ca4d-114">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="6ca4d-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="6ca4d-115">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="6ca4d-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="6ca4d-116">您將學習如何 toodownload 和修改與現有 ARM 範本從 GitHub，並部署從 GitHub、 PowerShell 和 hello Azure CLI hello 範本。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="6ca4d-117">如果您只想要部署 hello ARM 範本，直接從 GitHub，不進行任何變更，請略過太[部署範本，以從 github](#deploy-the-arm-template-by-using-click-to-deploy)。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="6ca4d-118">下載並了解 hello Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6ca4d-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="6ca4d-119">您可以下載從 GitHub 建立 VNet 和兩個子網路的 hello 現有範本，進行任何變更，您可能會想要並重複使用它。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="6ca4d-120">toodo，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="6ca4d-121">瀏覽過[hello 範例範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="6ca4d-122">依序按一下 [azuredeploy.json] 和 [RAW]。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="6ca4d-123">在電腦上儲存 hello 檔案 tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="6ca4d-124">如果您已熟悉範本，請略過 toostep 7。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="6ca4d-125">開啟您剛才儲存的 hello 檔案，並查看下 hello 內容**參數**第 5 行中。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="6ca4d-126">ARM 範本的參數提供值的預留位置，可以在部署期間填寫。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="6ca4d-127">參數</span><span class="sxs-lookup"><span data-stu-id="6ca4d-127">Parameter</span></span> | <span data-ttu-id="6ca4d-128">說明</span><span class="sxs-lookup"><span data-stu-id="6ca4d-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6ca4d-129">**位置**</span><span class="sxs-lookup"><span data-stu-id="6ca4d-129">**location**</span></span> |<span data-ttu-id="6ca4d-130">將會建立 hello VNet 的 azure 地區</span><span class="sxs-lookup"><span data-stu-id="6ca4d-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="6ca4d-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="6ca4d-131">**vnetName**</span></span> |<span data-ttu-id="6ca4d-132">名稱 hello 新的 VNet</span><span class="sxs-lookup"><span data-stu-id="6ca4d-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="6ca4d-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="6ca4d-133">**addressPrefix**</span></span> |<span data-ttu-id="6ca4d-134">Hello VNet，採用 CIDR 格式的位址空間</span><span class="sxs-lookup"><span data-stu-id="6ca4d-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="6ca4d-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="6ca4d-135">**subnet1Name**</span></span> |<span data-ttu-id="6ca4d-136">Hello 名稱第一個 VNet</span><span class="sxs-lookup"><span data-stu-id="6ca4d-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="6ca4d-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="6ca4d-137">**subnet1Prefix**</span></span> |<span data-ttu-id="6ca4d-138">Hello 第一個子網路的 CIDR 區塊</span><span class="sxs-lookup"><span data-stu-id="6ca4d-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="6ca4d-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="6ca4d-139">**subnet2Name**</span></span> |<span data-ttu-id="6ca4d-140">Hello 名稱的第二個 VNet</span><span class="sxs-lookup"><span data-stu-id="6ca4d-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="6ca4d-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="6ca4d-141">**subnet2Prefix**</span></span> |<span data-ttu-id="6ca4d-142">Hello 第二個子網路的 CIDR 區塊</span><span class="sxs-lookup"><span data-stu-id="6ca4d-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="6ca4d-143">GitHub 所維護的 Azure 資源管理員範本可能會隨著時間改變。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="6ca4d-144">請確定您使用之前，先檢查 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="6ca4d-145">檢查下的 hello 內容**資源**，並注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6ca4d-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="6ca4d-146">**type**。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-146">**type**.</span></span> <span data-ttu-id="6ca4d-147">Hello 範本所建立的資源類型。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="6ca4d-148">在此案例中為 **Microsoft.Network/virtualNetworks**，代表 VNet。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="6ca4d-149">**名稱**。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-149">**name**.</span></span> <span data-ttu-id="6ca4d-150">Hello 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-150">Name for hello resource.</span></span> <span data-ttu-id="6ca4d-151">請注意 hello 使用**[parameters('vnetName')]**，它表示 hello 名稱會在部署期間提供做為輸入 hello 使用者或參數檔案。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="6ca4d-152">**屬性**。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-152">**properties**.</span></span> <span data-ttu-id="6ca4d-153">Hello 資源屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-153">List of properties for hello resource.</span></span> <span data-ttu-id="6ca4d-154">此範本會在 VNet 建立期間使用 hello 位址空間和子網路屬性。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="6ca4d-155">瀏覽回太[hello 範例範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="6ca4d-156">依序按一下 [azuredeploy-paremeters.json] 和 [RAW]。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="6ca4d-157">在電腦上儲存 hello 檔案 tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="6ca4d-158">開啟您剛才儲存的 hello 檔案並編輯 hello hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="6ca4d-159">使用下列值低於 toodeploy hello hello 案例中所描述的 VNet hello:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

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

11. <span data-ttu-id="6ca4d-160">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="6ca4d-161">部署使用 PowerShell 的 hello 範本</span><span class="sxs-lookup"><span data-stu-id="6ca4d-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="6ca4d-162">完成下列步驟 toodeploy hello 範本，而您使用 PowerShell 下載 hello:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="6ca4d-163">安裝和設定 Azure PowerShell hello 中的 hello 步驟[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="6ca4d-164">新的資源群組執行下列命令 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="6ca4d-165">hello 命令會建立名為的資源群組*TestRG*在 hello*美國中部*azure 區域。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="6ca4d-166">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="6ca4d-167">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca4d-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="6ca4d-168">執行下列命令 toodeploy hello 新的 VNet 使用 hello 範本和參數檔案下載，並修改上述的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="6ca4d-169">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca4d-169">Expected output:</span></span>
   
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
4. <span data-ttu-id="6ca4d-170">Hello 執行的下列命令的 hello tooview hello 屬性新的 VNet:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="6ca4d-171">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca4d-171">Expected output:</span></span>

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

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="6ca4d-172">部署使用按一下部署的 hello 範本</span><span class="sxs-lookup"><span data-stu-id="6ca4d-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="6ca4d-173">您可以重複使用預先定義的 Azure 資源管理員範本上傳的 tooa GitHub 儲存機制由 Microsoft 和社群開啟 toohello 維護。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="6ca4d-174">這些範本可以直接從 GitHub，部署或下載並修改 toofit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="6ca4d-175">toodeploy 範本建立 VNet 兩個子網路，以完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="6ca4d-176">從瀏覽器中，瀏覽過[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="6ca4d-177">向下捲動 hello 清單的範本，然後按一下**101-vnet-兩個子網路**。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="6ca4d-178">檢查 hello **README.md**檔案，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-178">Check hello **README.md** file, as shown below.</span></span>

    ![Github 中的 READEME.md 檔案](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="6ca4d-180">按一下**部署 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="6ca4d-181">如有必要，請輸入您的 Azure 登入認證。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="6ca4d-182">在 hello**參數**刀鋒視窗中，輸入您想 toouse toocreate 新的 VNet，然後再按一下 hello 值**確定**。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="6ca4d-183">hello 如下圖所示為 hello 案例 hello 值：</span><span class="sxs-lookup"><span data-stu-id="6ca4d-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![ARM 範本參數](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="6ca4d-185">按一下**資源群組**，然後選取資源群組 tooadd hello VNet，或按一下**建立新**tooadd hello VNet tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="6ca4d-186">hello 如下圖所示 hello 資源群組設定新的資源群組，稱為**TestRG**:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![資源群組](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="6ca4d-188">如有必要，變更 hello**訂用帳戶**和**位置**設定您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="6ca4d-189">如果您不想 toosee hello VNet 當做一個磚中 hello**開始面板**，停用**Pin tooStartboard**。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="6ca4d-190">按一下**法律條款**，閱讀 hello 條款，然後按一下**購買**tooagree。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="6ca4d-191">按一下**建立**toocreate hello VNet。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![在 Preview 入口網站中提交部署磚](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="6ca4d-193">Hello 部署完成之後，請在 hello Azure 入口網站按一下**更多服務**，型別*虛擬網路*在 hello 篩選出現的方塊，然後按一下 虛擬網路 toosee hello 虛擬網路刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="6ca4d-194">在 hello 刀鋒視窗中，按一下  *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="6ca4d-195">在 hello *TestVNet*刀鋒視窗中，按一下 **子網路**toosee hello 建立子網路，hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="6ca4d-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![在 Preview 入口網站中建立 VNet](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="6ca4d-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ca4d-197">Next steps</span></span>

<span data-ttu-id="6ca4d-198">深入了解如何 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="6ca4d-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="6ca4d-199">虛擬機器 (VM) tooa 虛擬網路讀取 hello[建立 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md)或[建立 Linux VM](../virtual-machines/linux/quick-create-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="6ca4d-200">而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="6ca4d-201">藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="6ca4d-202">使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="6ca4d-203">深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-arm.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ca4d-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
