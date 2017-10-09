---
title: "aaaAzure 虛擬機器擴展集概觀 |Microsoft 文件"
description: "深入了解 Azure 虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>什麼是 Azure 中的虛擬機器擴展集？
虛擬機器擴展集是 Azure 計算資源，您可以使用 toodeploy 和管理一組相同的 Vm。 並將所有的 Vm 設定 hello 相同、 規模集是設計的 toosupport 自動調整，則為 true，而且沒有預先佈建的 Vm 需要。 因此，您更輕鬆 toobuild 中大規模服務 big compute、 大型資料，以及進行容器化工作負載為目標。

需要 tooscale 計算資源，且在標尺的應用程式的作業會隱含地平衡容錯網域和更新網域。 如進一步介紹 tooscale 設定，請參閱 toohello [Azure 部落格通知](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/)。

如需擴展集的詳細資訊，請觀看下列影片：

* [Mark Russinovich 講述 Azure 擴展集](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)  
* [Guy Bowerman 與虛擬機器擴展集](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>建立和管理擴展集
您可以建立在擴展集在 hello [Azure 入口網站](https://portal.azure.com)選取**新**輸入**標尺**hello 搜尋列上。 **虛擬機器規模集**列出 hello 結果中。 從該處，您可以填寫必要的 hello 欄位 toocustomize 和部署規模集。 您也可以選項 tooset hello 入口網站的 CPU 使用量為基礎的基本的自動調整規模規則。

您可以使用 JSON 範本和 [REST API](https://msdn.microsoft.com/library/mt589023.aspx) 來定義和部署擴展集，如同個別的 Azure Resource Manager VM 一樣。 因此，您可以使用任何標準 Azure Resource Manager 部署方法。 如需範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。

您可以找到一組範例範本的虛擬機器規模集中 hello [Azure 快速入門範本 GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates)。 (尋找範本**vmss** hello 標題中。)

如需 hello 快速入門範本範例，hello 讀我檔案，每個範本中的 「 部署 tooAzure 」 按鈕連結 toohello 入口網站部署功能。 toodeploy hello 小數位數設定、 按一下 [hello] 按鈕，然後填入 hello 入口網站中所需的任何參數。 

## <a name="scaling-a-scale-set-out-and-in"></a>相應放大和相應縮小擴展集
您可以變更在擴展集 hello Azure 入口網站中，依序按一下 hello hello 容量**調整**區段**設定**。 

toochange 標尺 hello 命令列上設定容量，請使用 hello**標尺**命令[Azure CLI](https://github.com/Azure/azure-cli)。 例如，使用此命令 tooset 10 部 Vm 的小數位數組 tooa 容量：

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

tooset hello Vm 數目的小數位數中使用 PowerShell 設定，請使用 hello**更新 AzureRmVmss**命令：

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

tooincrease 或減少 hello 數小數位數中的虛擬機器使用 Azure Resource Manager 範本設定，變更 hello**容量**屬性後再重新部署的 hello 範本。 這種可讓 Azure 自動調整規模，或您自己自訂的縮放層級如果您需要 Azure 自動調整 toodefine 自訂縮放比例事件不支援的 toowrite 輕鬆 toointegrate 規模集。 

如果您重新部署的 Azure Resource Manager 範本 toochange hello 容量時，您可以定義較小包含的範本只 hello **SKU**屬性封包以 hello 更新容量。 [以下是範例](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing)。

## <a name="autoscale"></a>Autoscale

建立 hello Azure 入口網站中時，擴展集，可以選擇性地設定自動調整設定。 hello Vm 數目可以再提高或降低根據平均 CPU 使用量。 

許多 hello 調整集範本中 hello [Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)定義自動調整規模設定。 您也可以加入現有的擴展集自動調整規模設定 tooan。 例如，此 Azure PowerShell 指令碼將 CPU 型自動調整規模 tooa 規模集：

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

您可以找到有效的度量 tooscale 清單上[支援的 Azure 監視的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)下 hello 標題"Microsoft.Compute/virtualMachineScaleSets。 」 也可以使用，包括排程為基礎的自動調整規模，以及與警示系統使用 webhook toointegrate 更進階的自動調整規模選項。

## <a name="monitoring-your-scale-set"></a>監視擴展集
hello [Azure 入口網站](https://portal.azure.com)清單縮放設定，並顯示其屬性。 hello 入口網站也支援管理作業。 您可以同時針對擴展集和擴展集內的個別 VM 執行管理作業。 hello 入口網站也提供可自訂的資源使用量圖表。 

如果您需要 toosee 或編輯 hello 基礎的 Azure 資源的 JSON 定義時，您也可以使用[Azure 資源總管](https://resources.azure.com)。 小數位數均為 hello Microsoft.Compute Azure 資源提供者下的資源。 從這個站台，您可以看到它們展開 hello 下列連結：

訂用帳戶 > 您的訂用帳戶 > resourceGroups > 提供者 > Microsoft.Compute > virtualMachineScaleSets > 您的擴展集 > 等等

## <a name="scale-set-scenarios"></a>擴展集案例
本節列出一些典型的擴展集案例。 某些較高階的 Azure 服務 (例如 Batch、Service Fabric 和 Container Service) 會使用這些案例。

* **使用 RDP 或 SSH tooconnect tooscale 設定執行個體**： 規模集建立內部虛擬網路，且 hello 規模集中的個別 Vm 依預設不會配置的公用 IP 位址。 此原則可避免 hello 費用，以及管理負擔的配置不同的公用 IP 位址 tooall hello 節點計算方格中。 如果您需要直接外部連接 tooscale 設定 Vm，您可以設定小數位數組 tooautomatically 指派公用 IP 位址 toonew Vm。 或者您可以從其他資源連線 tooVMs 虛擬網路中可獲配置的公用 IP 位址，例如，負載平衡器和獨立虛擬機器。 
* **使用 NAT 規則連線 tooVMs**： 您可以建立公用 IP 位址、 將它指派 tooa 負載平衡器，並定義傳入的 NAT 集區。 這些動作將 hello IP 位址 tooa 的連接埠上的 VM hello 規模集中的連接埠對應。 例如：
  
  | 來源 | 來源連接埠 | 目的地 | 目的地連接埠 |
  | --- | --- | --- | --- |
  |  公用 IP |連接埠 50000 |vmss\_0 |連接埠 22 |
  |  公用 IP |連接埠 50001 |vmss\_1 |連接埠 22 |
  |  公用 IP |連接埠 50002 |vmss\_2 |連接埠 22 |
  
   在[本例](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat)，NAT 規則會定義的 tooenable 規模集中的 SSH 連線 tooevery VM，使用單一公用 IP 位址。
  
   [這個範例](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat)未透過 RDP 和 Windows hello 相同。
* **使用 「 jumpbox 」 連線 tooVMs**： 如果您在相同虛擬網路，hello hello 中建立 小數位數，以及獨立 VM 獨立 VM 和 hello 擴展集 VM 可以連接的 tooone 另一個使用其內部 IP 位址時，所定義的 hello 虛擬網路或子網路。 如果您建立的公用 IP 位址，並將它指派 toohello 獨立 VM，您可以使用 RDP 或 SSH tooconnect toohello 獨立 VM。 您可以連接從機器 tooyour 規模設定執行個體。 此時您可能會發現，簡易擴展集在本質上比在預設組態中設定了公用 IP 位址的獨立 VM 來得安全。
  
   例如，[此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox)會部署具有一部獨立 VM 的簡單擴展集。 
* **負載平衡 tooscale 集執行個體**： 如果您想 toodeliver 工作 tooa 運算叢集的 Vm 使用的循環配置資源方法，您可以設定 Azure 負載平衡器與第 4 層負載平衡規則據以。 您可以定義探查您應用程式正在執行 ping tooverify 連接埠與指定的通訊協定、 間隔和要求路徑。 [Azure 應用程式閘道](https://azure.microsoft.com/services/application-gateway/)也支援擴展集，以及第 7 層和更複雜的負載平衡案例。
  
   [這個範例](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl)建立執行 Apache web 伺服器，並使用每個 VM 收到負載平衡器 toobalance hello 負載規模集。 （看看 hello Microsoft.Network/loadBalancers 資源類型和 networkProfile extensionProfile virtualMachineScaleSet 中的）。

   [此 Linux 範例](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway)和[此 Windows 範例](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway)均使用應用程式閘道。  

* **在 PaaS 叢集管理員中，將擴展集部署為計算叢集**：擴展集有時會被稱為新一代的背景工作角色。 有效的描述，但它未風險 hello 令人混淆的小數位數的設定功能與 Azure 雲端服務功能。 就某方面來說，擴展集提供了真正的背景工作角色或背景工作資源。 因為它們是不會隨平台/執行階段而改變、可自訂且整合至 Azure Resource Manager IaaS 的一般化計算資源。
  
   雲端服務背景工作角色的平台/執行階段支援有限 (僅限 Windows 平台映像)。 但它也包含一些服務，例如 VIP 交換、可設定的升級設定，以及執行階段/應用程式部署特定設定。 這些服務「尚未」在擴展集中提供，或由其他較高層級的 PaaS 服務 (例如 Azure Service Fabric) 傳遞。 您可以將擴展集視為可支援 PaaS 的基礎結構。 [Service Fabric](https://azure.microsoft.com/services/service-fabric/) 之類的 PaaS 解決方案會建置在這個基礎結構上。
  
   在這個方法的[此範例](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)中，[Azure Container Service](https://azure.microsoft.com/services/container-service/) 會根據具有容器協調器的擴展集來部署叢集。

## <a name="scale-set-performance-and-scale-guidance"></a>擴展集的效能和調整指南
* 擴展集支援 too1，000 Vm 上。 如果您建立並上傳您自己自訂的 VM 映像，hello 限制為 100。 如需大型擴展集的使用考量，請參閱[使用大型的虛擬機器擴展集](virtual-machine-scale-sets-placement-groups.md)。
* 您不需要 toopre-建立 Azure 儲存體帳戶 toouse 規模集。 小數位數設定支援 Azure 受管理磁碟、 變換正負號的每個儲存體帳戶的磁碟的 hello 數目的相關效能問題。 如需詳細資訊，請參閱 [Azure 虛擬機器擴展集和受控磁碟](virtual-machine-scale-sets-managed-disks.md)。
* 請考慮使用 Azure 進階儲存體而非 Azure 儲存體，來提升 VM 佈建時間的速度和可預測性，並改善 IO 效能。
* 在您要部署的 hello 區域中的 hello 核心配額限制您可以建立的 Vm 的 hello 數目。 您需要 toocontact 客戶支援 tooincrease 您計算的配額限制，即使您目前有高限制的 Azure 雲端服務搭配使用的核心。 tooquery 配額限制，請執行下列 Azure CLI 命令： `azure vm list-usage`。 或者，執行此 PowerShell 命令︰`Get-AzureRmVMUsage`。

## <a name="frequently-asked-questions-for-scale-sets"></a>擴展集的常見問題集
**問：** 擴展集內可以有多少部 VM？

**答：** 擴展集可以有 0 too1、 000 Vm 為基礎平台映像，或 0 too100 Vm 為基礎的自訂映像。 

**問：** 在擴展集內是否支援資料磁碟？

**答：** 是。 擴展集可以定義適用於 hello 集中 tooall Vm 連接的資料磁碟組態。 如需詳細資訊，請參閱 [Azure 擴展集和連結的資料磁碟](virtual-machine-scale-sets-attached-disks.md)。 其他用於儲存資料的選項包括：

* Azure 檔案 (SMB 共用磁碟機)
* OS 磁碟機
* 暫存磁碟機 (本機，未受 Azure 儲存體支援)
* Azure 資料服務 (例如 Azure 資料表、Azure Blob)
* 外部資料服務 (例如遠端資料庫)

**問：** 哪些 Azure 區域支援擴展集？

**答：** 所有區域都支援擴展集。

**問：** 如何使用自訂映像建立擴展集？

**答：** 根據自訂映像 VHD 建立受控磁碟，並在擴展集範本中參考它。 [以下是範例](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os)。

**問：** 如果我降低我的小數位數會從 20 too15，Vm 會移除設定產能？

**答：** 虛擬機器會移除從 hello 擴展集更新網域和故障網域 toomaximize 可用性之間的平均。 以最高識別碼會先移除的 hello 的 Vm。

**問：** 如果再增加從 15 too18 hello 容量？

**答：** 如果您增加容量 too18 時，會建立 3 個新 Vm。 每次從 hello 前一個最高值 （例如 20、 21、 22），會遞增 hello VM 執行個體識別碼。 VM 會平衡分散到容錯網域和更新網域。

**問：** 在擴展集內使用多個延伸模組時，是否可以強制執行「執行順序」？

**答：** Hello customScript 延伸模組，但無法直接管理，您的指令碼可以等候另一個延伸模組 toofinish。 您可以取得其他指示上 hello 部落格文章中的擴充功能順序[在 Azure VM 規模集的擴充功能順序](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/)。

**問：** 擴展集是否可與 Azure 可用性設定組組搭配使用？

**答：** 是。 擴展集是隱含的可用性設定組，具有 5 個容錯網域和 5 個更新網域。 小數位數的 100 個以上的 Vm 設定跨多個*放置群組*，這是對等 toomultiple 可用性設定組。 如需放置群組的詳細資訊，請參閱[使用大型的虛擬機器擴展集](virtual-machine-scale-sets-placement-groups.md)。 Vm 的可用性設定組中可能存在 hello 相同虛擬網路的 Vm 規模集。 常見組態是 tooput 控制節點 （這通常需要唯一的組態） 的 Vm 的可用性中設定，並將資料節點放在 hello 規模集。

您可以找到有關小數位數的多個答案 tooquestions 設定中 hello [Azure 虛擬機器規模設定常見問題集](virtual-machine-scale-sets-faq.md)。
