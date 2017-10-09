---
title: "Azure 虛擬網路 （傳統） 的網路組態檔 aaaConfigure |Microsoft 文件"
description: "深入了解如何 toocreate 和匯出、 變更和匯入網路組態檔來修改虛擬網路 （傳統）。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="0c80e-103">使用網路組態檔來設定虛擬網路 (傳統)</span><span class="sxs-lookup"><span data-stu-id="0c80e-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0c80e-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0c80e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0c80e-105">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0c80e-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="0c80e-106">Microsoft 建議最新的部署使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="0c80e-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="0c80e-107">您可以建立及使用 Azure 命令列介面 (CLI) 1.0 hello 或 Azure PowerShell 所使用的網路組態檔設定虛擬網路 （傳統）。</span><span class="sxs-lookup"><span data-stu-id="0c80e-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="0c80e-108">您無法建立或修改透過 hello Azure Resource Manager 部署模型使用網路組態檔的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0c80e-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="0c80e-109">您無法使用 Azure 入口網站 toocreate hello 或修改使用網路組態檔的虛擬網路 （傳統），不過您可以使用 hello Azure 入口網站 toocreate 虛擬網路 （傳統），而不使用網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="0c80e-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="0c80e-110">建立和使用網路組態檔設定虛擬網路 （傳統） 需要匯出、 變更和匯入 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c80e-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="0c80e-111"><a name="export"></a>匯出網路組態檔</span><span class="sxs-lookup"><span data-stu-id="0c80e-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="0c80e-112">您可以使用 PowerShell 或 hello Azure CLI tooexport 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="0c80e-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="0c80e-113">PowerShell 匯出 XML 檔案，而 hello Azure CLI 匯出 json 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c80e-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="0c80e-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c80e-114">PowerShell</span></span>
 
1. <span data-ttu-id="0c80e-115">[安裝 Azure PowerShell 並登入 tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0c80e-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="0c80e-116">變更 hello 目錄 （及確保它存在），並在 hello 的檔名遵循與所需，然後執行 hello 命令 tooexport hello 網路組態檔的命令：</span><span class="sxs-lookup"><span data-stu-id="0c80e-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="0c80e-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0c80e-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="0c80e-118">[安裝 hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0c80e-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0c80e-119">完成剩餘步驟，Azure CLI 1.0 的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="0c80e-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="0c80e-120">輸入 hello 登入 tooAzure`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="0c80e-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="0c80e-121">確認您是在 asm 模式中，輸入 hello`azure config mode asm`命令。</span><span class="sxs-lookup"><span data-stu-id="0c80e-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="0c80e-122">變更 hello 目錄 （及確保它存在），並在 hello 的檔名遵循與所需，然後執行 hello 命令 tooexport hello 網路組態檔的命令：</span><span class="sxs-lookup"><span data-stu-id="0c80e-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="0c80e-123">建立或修改網路組態檔</span><span class="sxs-lookup"><span data-stu-id="0c80e-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="0c80e-124">網路組態檔是 XML 檔案 （當使用 PowerShell） 或 json 檔案 （當使用 Azure CLI hello）。</span><span class="sxs-lookup"><span data-stu-id="0c80e-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="0c80e-125">您可以編輯任何文字或 XML/json 編輯器中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c80e-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="0c80e-126">hello[網路組態檔結構描述設定](https://msdn.microsoft.com/library/azure/jj157100.aspx)文章包含的所有設定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0c80e-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="0c80e-127">如 hello 設定其他說明，請參閱[檢視虛擬網路與設定](virtual-network-manage-network.md#view-vnet)。</span><span class="sxs-lookup"><span data-stu-id="0c80e-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="0c80e-128">hello 作 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="0c80e-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="0c80e-129">必須符合與 hello 結構描述或匯入 hello 網路組態檔將會失敗。</span><span class="sxs-lookup"><span data-stu-id="0c80e-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="0c80e-130">會覆寫您訂用帳戶的任何現有網路設定，因此在進行修改時請特別小心。</span><span class="sxs-lookup"><span data-stu-id="0c80e-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="0c80e-131">例如，參考 hello 範例網路組態檔，請遵循。</span><span class="sxs-lookup"><span data-stu-id="0c80e-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="0c80e-132">說出 hello 原始檔案包含兩個**VirtualNetworkSite**執行個體，以及您已變更，hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="0c80e-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="0c80e-133">Hello 檔案時，Azure 會刪除 hello 虛擬網路的 hello **VirtualNetworkSite**您移除 hello 檔案中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="0c80e-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="0c80e-134">這個簡化的案例假設沒有任何資源都在 hello 虛擬網路，因為如果有的話，無法刪除 hello 虛擬網路，以及 hello 匯入將會失敗。</span><span class="sxs-lookup"><span data-stu-id="0c80e-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c80e-135">Azure 會考慮的項目具有子網路部署為 tooit**使用**。</span><span class="sxs-lookup"><span data-stu-id="0c80e-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="0c80e-136">使用中的子網路無法加以修改。</span><span class="sxs-lookup"><span data-stu-id="0c80e-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="0c80e-137">在修改之前網路組態檔中的子網路資訊，移動任何您已部署 toohello 子網路 tooa 不同的子網路的未修改的項目。</span><span class="sxs-lookup"><span data-stu-id="0c80e-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="0c80e-138">請參閱[移動 VM 或角色執行個體 tooa 不同的子網路](virtual-networks-move-vm-role-to-subnet.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0c80e-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="0c80e-139">與 PowerShell 搭配使用的範例 XML</span><span class="sxs-lookup"><span data-stu-id="0c80e-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="0c80e-140">hello 下列的範例網路組態檔建立虛擬網路，名為*myVirtualNetwork*與位址空間的*10.0.0.0/16*在 hello*美國東部*Azure區域。</span><span class="sxs-lookup"><span data-stu-id="0c80e-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="0c80e-141">hello 虛擬網路包含一個名為的子網路*mySubnet*位址前置詞的*10.0.0.0/24*。</span><span class="sxs-lookup"><span data-stu-id="0c80e-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="0c80e-142">如果您匯出的 hello 網路組態檔不包含任何內容，您可以複製 hello 先前範例中的 hello XML，並將它貼到新的檔案。</span><span class="sxs-lookup"><span data-stu-id="0c80e-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="0c80e-143">範例 JSON hello Azure CLI 1.0 搭配使用</span><span class="sxs-lookup"><span data-stu-id="0c80e-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="0c80e-144">hello 下列的範例網路組態檔建立虛擬網路，名為*myVirtualNetwork*與位址空間的*10.0.0.0/16*在 hello*美國東部*Azure區域。</span><span class="sxs-lookup"><span data-stu-id="0c80e-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="0c80e-145">hello 虛擬網路包含一個名為的子網路*mySubnet*位址前置詞的*10.0.0.0/24*。</span><span class="sxs-lookup"><span data-stu-id="0c80e-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="0c80e-146">如果您匯出的 hello 網路組態檔不包含任何內容，您可以複製 hello 先前範例中的 hello json，並將它貼到新的檔案。</span><span class="sxs-lookup"><span data-stu-id="0c80e-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="0c80e-147"><a name="import"></a>匯入網路組態檔</span><span class="sxs-lookup"><span data-stu-id="0c80e-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="0c80e-148">您可以使用 PowerShell 或 hello Azure CLI tooimport 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="0c80e-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="0c80e-149">Hello Azure CLI 匯入 json 檔案時，PowerShell 會匯入 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c80e-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="0c80e-150">如果 hello 匯入失敗，請確認該 hello 檔案符合 hello[網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0c80e-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="0c80e-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c80e-151">PowerShell</span></span>
 
1. <span data-ttu-id="0c80e-152">[安裝 Azure PowerShell 並登入 tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0c80e-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="0c80e-153">變更 hello 目錄和檔案名稱中 hello 下列命令，如有必要，然後再執行 hello 命令 tooimport hello 網路組態檔：</span><span class="sxs-lookup"><span data-stu-id="0c80e-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="0c80e-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0c80e-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="0c80e-155">[安裝 hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0c80e-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0c80e-156">完成剩餘步驟，Azure CLI 1.0 的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="0c80e-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="0c80e-157">輸入 hello 登入 tooAzure`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="0c80e-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="0c80e-158">確認您是在 asm 模式中，輸入 hello`azure config mode asm`命令。</span><span class="sxs-lookup"><span data-stu-id="0c80e-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="0c80e-159">變更 hello 目錄和檔案名稱中 hello 下列命令，如有必要，然後再執行 hello 命令 tooimport hello 網路組態檔：</span><span class="sxs-lookup"><span data-stu-id="0c80e-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
