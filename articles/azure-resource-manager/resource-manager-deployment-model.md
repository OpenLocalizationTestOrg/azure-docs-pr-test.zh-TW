---
title: "aaaResource 管理員和傳統部署 |Microsoft 文件"
description: "描述 hello hello Resource Manager 部署模型和傳統 hello （或服務管理） 之間的差異部署模型。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Azure Resource Manager vs.傳統部署： 了解部署模型及 hello 資源的狀態
本主題中，在您了解 Azure 資源管理員和傳統部署模型，您的資源，hello 狀態和原因其他 hello 或其中一種部署您的資源。 資源管理員 hello 和傳統部署模型代表部署及管理 Azure 解決方案的兩個不同的方式。 您與它們透過兩個不同的 API 集，並部署的 hello 資源可以包含重要的差異。 hello 兩個模型不是彼此完全相容。 本主題說明這些差異。

toosimplify hello 部署及管理的資源，Microsoft 建議您針對所有新的資源使用資源管理員。 可能的話，Microsoft 建議您透過 Resource Manager 重新部署現有的資源。

如果您是新 tooResource 管理員，您可以定義在 hello toofirst 檢閱 hello 術語[Azure 資源管理員概觀](resource-group-overview.md)。

## <a name="history-of-hello-deployment-models"></a>Hello 部署模型的歷程記錄
Azure 中原本提供 hello 傳統部署模型。 在此模型中，每個資源存在於獨立;沒有方法 toogroup 相互關聯的資源。 相反地，您必須追蹤組成您的方案或應用程式中，哪些資源，並請記得 toomanage toomanually 中協調的方式。 toodeploy 方案，您必須建立個別透過 hello 傳統入口網站的每個資源，或建立指令碼部署 hello 正確的順序中的所有 hello 資源 tooeither。 toodelete 方案，您必須 toodelete 每個資源個別。 您無法輕易套用和更新相關資源的存取控制原則。 最後，您無法套用標籤 tooresources toolabel 這些條款，可協助您監視您的資源和管理計費。

在 2014 中，Azure 會導入了資源管理員，加入的資源群組的 hello 概念。 資源群組是共用共同生命週期的資源容器。 hello Resource Manager 部署模型有數個優點：

* 您可以部署、 管理及監視所有的 hello 服務，您的解決方案，為群組，而不是個別處理這些服務。
* 您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。
* 您可以套用存取控制 tooall 資源在資源群組中，而且這些原則會自動套用新的資源新增 toohello 資源群組時。
* 您可以將標籤套用 tooresources toologically 組織您的訂用帳戶中的所有 hello 資源。
* 您可以使用 JavaScript Object Notation (JSON) toodefine hello 基礎結構，您的解決方案。 hello JSON 檔案稱為 Resource Manager 範本。
* 您可以定義 hello 資源，所以它們部署在 hello 正確的順序之間的相依性。

資源管理員已加入時，所有資源、 追溯性都加入 toodefault 資源群組。 如果您建立透過傳統部署現在是資源時，會自動建立 hello 資源中預設的資源群組，該服務，即使您未指定該資源群組，在部署。 不過，只要現有的資源群組內不代表 hello 資源已轉換的 toohello 資源管理員的模型。 我們會探討每個服務如何處理 hello 兩種部署模型 hello 下一節。 

## <a name="understand-support-for-hello-models"></a>了解支援 hello 模型
在決定哪些部署模型 toouse，為您的資源時，有三個案例 toobe 留意：

1. hello 服務支援資源管理員，並提供單一類型。
2. hello 服務支援資源管理員，但提供兩種類型的資源管理員，一個用於傳統的其中一個。 此案例適用於 toovirtual 機器、 儲存體帳戶和虛擬網路。
3. hello 服務不支援資源管理員。

toodiscover 服務是支援資源管理員，請參閱[資源提供者和類型](resource-manager-supported-services.md)。

如果您想 toouse hello 服務不支援資源管理員，您必須繼續使用傳統部署。

如果 hello 服務支援資源管理員和**不**虛擬機器、 儲存體帳戶或虛擬網路，您可以使用資源管理員，而任何複雜。

虛擬機器、 儲存體帳戶和虛擬網路，如果已建立 hello 資源，透過傳統部署，您必須繼續 toooperate 上透過傳統的作業。 如果 hello 虛擬機器、 儲存體帳戶或虛擬網路建立資源管理員部署，您必須繼續使用資源管理員作業。 當您的訂用帳戶包含透過 Resource Manager 和傳統部署建立的各種資源時，此區別可能讓您困惑。 此資源的組合可以建立非預期的結果，因為不支援 hello 資源 hello 相同的作業。

在某些情況下，資源管理員命令可以擷取透過傳統部署中，建立資源的相關資訊，或可以執行系統管理工作，例如移動傳統資源 tooanother 資源群組。 但是，這種情況下不應將 hello 印象 hello 類型支援資源管理員作業。 例如，假設您的資源群組包含使用傳統部署所建立的虛擬機器。 如果您要執行 hello 下列資源管理員 PowerShell 命令：

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

它會傳回 hello 虛擬機器：

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

不過，hello 資源管理員 cmdlet **Get AzureRmVM**只會傳回部署透過資源管理員的虛擬機器。 hello 下列命令不會傳回建立透過傳統部署的 hello 虛擬機器。

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

只有透過資源管理員建立的資源支援標記。 您無法套用標籤 tooclassic 資源。

## <a name="resource-manager-characteristics"></a>資源管理員特性
您了解兩個 hello toohelp 模型，請讓我們來檢視資源管理員類型的 hello 特性：

* 建立透過 hello [Azure 入口網站](https://portal.azure.com/)。
  
     ![Azure 入口網站](./media/resource-manager-deployment-model/portal.png)
  
     計算、 儲存體和網路資源，您必須使用 資源管理員 或 傳統部署的 hello 選項。 選擇 **資源管理員**。
  
     ![資源管理員部署](./media/resource-manager-deployment-model/select-resource-manager.png)
* 建立與 hello 資源管理員版本 hello Azure PowerShell cmdlet。 這些命令有 hello 格式*動詞 AzureRmNoun*。

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* 建立透過 hello [Azure 資源管理員 REST API](https://docs.microsoft.com/rest/api/resources/) REST 作業。
* 透過在 hello 中執行的 Azure CLI 命令建立**arm**模式。
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* hello 資源類型不包含**（傳統）** hello 名稱中。 hello 如下圖所示為 hello 類型**儲存體帳戶**。
  
    ![Web 應用程式](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>傳統部署特性
您也可能知道 hello 傳統部署模型與 hello 服務管理模型。

在下列特性的 hello 傳統部署模型共用 hello 中建立的資源：

* 建立透過 hello[傳統入口網站](https://manage.windowsazure.com)
  
     ![傳統入口網站](./media/resource-manager-deployment-model/classic-portal.png)
  
     或者，hello Azure 入口網站，而且您指定**傳統**（適用於計算、 儲存和網路功能） 的部署。
  
     ![傳統部署](./media/resource-manager-deployment-model/select-classic.png)
* 建立透過 hello 服務管理版本 hello Azure PowerShell cmdlet。 這些命令的名稱具有 hello 格式*動詞 AzureNoun*。

  ```powershell
  New-AzureVM
  ```

* 建立透過 hello[服務管理 REST API](https://msdn.microsoft.com/library/azure/ee460799.aspx) REST 作業。
* 透過在 **asm** 模式中執行的 Azure CLI 命令建立。

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* hello 資源類型包含**（傳統）** hello 名稱中。 hello 如下圖所示為 hello 類型**儲存體帳戶 （傳統）**。
  
    ![傳統類型](./media/resource-manager-deployment-model/classic-type.png)

您可以使用透過傳統部署所建立的 hello Azure 入口網站 toomanage 資源。

## <a name="changes-for-compute-network-and-storage"></a>計算、網路和儲存體的變更
hello 下列圖表顯示部署透過資源管理員的計算、 網路和儲存體資源。

![Resource Manager 架構](./media/resource-manager-deployment-model/arm_arch3.png)

請注意下列 hello 資源之間的關聯性的 hello:

* 資源群組內，存在 hello 的所有資源。
* hello 虛擬機器，取決於特定的儲存體帳戶中 hello 儲存體資源提供者 toostore 定義它的磁碟在 blob 儲存體 （必要）。
* hello 虛擬機器參照 hello 網路資源提供者 （必要） 和可用性設定組定義在 hello 計算資源提供者 （選擇性） 中定義的特定 NIC。
* hello NIC 參考 hello 虛擬機器的指派 IP 位址 （必要），hello hello hello 虛擬機器 （必要） 和 tooa 網路安全性群組 （選擇性） 的虛擬網路子網路。
* 虛擬網路中的 hello 子網路參考網路安全性群組 （選擇性）。
* hello 負載平衡器執行個體參考 hello 後端集區的 IP 位址，包括 hello NIC 的虛擬機器 （選擇性），但參考的負載平衡器公用或私用 IP 位址 （選擇性）。

以下是 hello 元件以及它們的關聯性的傳統部署：

![傳統架構](./media/resource-manager-deployment-model/arm_arch1.png)

裝載虛擬機器的 hello 傳統解決方案包括：

* 用來做為裝載虛擬機器 (計算) 之容器所需的雲端服務。 虛擬機器是利用網路介面卡 (NIC) 和 Azure 所指派的 IP 位址自動提供。 此外，hello 雲端服務包含外部負載平衡器執行個體和公用 IP 位址，以及預設端點 tooallow 遠端桌面和遠端 PowerShell 流量 Windows 型虛擬機器的流量安全殼層 (SSH) 以 Linux 為基礎虛擬機器。
* 需要儲存體帳戶存放區 hello Vhd，虛擬機器，包括 hello 作業系統，暫時性的與其他資料磁碟 （儲存）。
* 做為其他的容器，可以建立子的結構並指定哪些 hello 虛擬機器所在的 hello 子網路的選擇性虛擬網路 （網路）。

hello 下表描述計算、 網路和儲存體資源提供者之間的互動方式的變更：

| Item | 傳統 | Resource Manager |
| --- | --- | --- |
| 虛擬機器的雲端服務 |雲端服務已擁有 hello 需要 hello 平台和負載平衡可用性的虛擬機器的容器。 |雲端服務已經建立虛擬機器使用 hello 新模型所需的物件。 |
| 虛擬網路 |虛擬網路是選擇性的 hello 虛擬機器。 如果包含，hello 虛擬網路，無法部署與資源管理員。 |虛擬機器需要已使用 Resource Manager 部署的虛擬網路。 |
| 儲存體帳戶 |hello 虛擬機器需要儲存 hello hello 作業系統，請暫時的與其他資料磁碟的 Vhd 的儲存體帳戶。 |hello 虛擬機器需要存放裝置帳戶 toostore 它在 blob 儲存體的磁碟。 |
| 可用性設定組 (Availability Sets) |藉由設定指出可用性 toohello 平台 hello 相同"AvailabilitySetName"hello 虛擬機器上的。 hello 的容錯網域計數上限為 2。 |「可用性設定組」是 Microsoft.Compute 提供者公開的資源。 需要高可用性的虛擬機器必須包含在可用性設定組的 hello。 hello 的容錯網域的最大計數現在是 3。 |
| 同質群組 |建立虛擬網路時需要同質群組。 不過，與 hello 介紹地區虛擬網路，，不需要再。 |toosimplify，hello 同質群組的概念，不存在於 hello 公開透過 Azure 資源管理員 Api。 |
| 負載平衡 |建立雲端服務的 hello 部署的虛擬機器提供隱含的負載平衡器。 |hello 負載平衡器是 hello Microsoft.Network 提供者所公開的資源。 hello 的 hello 需要 toobe 負載平衡的虛擬機器的主要網路介面應該參考 hello 負載平衡器。 負載平衡器可以放在內部或外部。 負載平衡器執行個體參考 hello 後端集區的 IP 位址，包括 hello NIC 的虛擬機器 （選擇性），但參考的負載平衡器公用或私用 IP 位址 （選擇性）。 [閱讀更多。](../virtual-network/resource-groups-networking.md) |
| 虛擬 IP 位址 |VM 加入 tooa 雲端服務時，雲端服務會取得預設 VIP （虛擬 IP 位址）。 hello 虛擬 IP 位址是 hello 與 hello 隱含的負載平衡器相關聯的位址。 |公用 IP 位址是 hello Microsoft.Network 提供者所公開的資源。 公用 IP 位址可以是靜態 (保留) 或動態。 動態公用 Ip 可以指派 tooa 負載平衡器。 使用安全性群組可以保護公用 IP。 |
| 保留 IP 位址 |您可以保留在 Azure 和關聯與 hello IP 位址的雲端服務 tooensure 是自黏便箋中 IP 位址。 |公用 IP 位址可由 「 靜態 」 模式，並提供 hello 做為 「 保留的 IP 位址 」 的相同功能。 靜態公用 Ip 只能指派 tooa 負載平衡器目前。 |
| 每一個 VM 的公用 IP 位址 (PIP) |公用 IP 位址也可以直接是相關聯的 tooa VM。 |公用 IP 位址是 hello Microsoft.Network 提供者所公開的資源。 公用 IP 位址可以是靜態 (保留) 或動態。 不過，動態公用 Ip 可以現在是指派的 tooa 網路介面 tooget 每個 VM 的公用 IP。 |
| 端點 |輸入端點所需設定虛擬機器 toobe toobe 開啟特定連接埠的連線。 其中一個 hello 連接 toovirtual 機器完成藉由設定輸入端點的常見的模式。 |輸入的 NAT 規則可以設定負載平衡器上 tooachieve hello 啟用特定的連接埠連接 toohello Vm 上端點的相同功能。 |
| DNS 名稱 |雲端服務會取得隱含的全域唯一 DNS 名稱。 例如： `mycoffeeshop.cloudapp.net`。 |DNS 名稱是可以在公用 IP 位址資源上指定的選用參數。 hello FQDN 處於 hello 以下格式- `<domainlabel>.<region>.cloudapp.azure.com`。 |
| 網路介面 |主要和次要網路介面與其屬性會定義為虛擬機器的網路組態。 |網路介面是 Microsoft.Network 提供者所公開的資源。 hello 生命週期的 hello 網路介面未繫結 tooa 虛擬機器。 它會參考 hello 虛擬機器的指派的 IP 位址 （必要），hello hello hello 虛擬機器 （必要） 和 tooa 網路安全性群組 （選擇性） 的虛擬網路子網路。 |

請參閱 < 關於虛擬網路連接從不同的部署模型 toolearn[連接虛擬網路從 hello 入口網站中不同的部署模型](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)。

## <a name="migrate-from-classic-tooresource-manager"></a>從傳統 tooResource Manager 移轉
如果您已準備好 toomigrate 傳統部署 tooResource 管理員部署、 存取資源，請參閱：

1. [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [使用 Azure PowerShell，從傳統 tooAzure 資源管理員移轉 IaaS 資源](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [從傳統 tooAzure 資源管理員移轉 IaaS 資源，使用 Azure CLI](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>常見問題集
**可以建立使用傳統部署建立虛擬網路中使用 Azure Resource Manager toodeploy 在虛擬機器嗎？**

不支援此做法。 您無法使用 Azure Resource Manager toodeploy 虛擬機器使用傳統部署所建立的虛擬網路中。

**建立虛擬機器使用 hello Azure 資源管理員的使用者映像，使用 hello Azure 服務管理 Api 建立？**

不支援此做法。 不過，您可以複製使用 hello 服務管理 Api，所建立的儲存體帳戶中的 hello VHD 檔案，並將它們加入 tooa 透過 Azure Resource Manager 建立新的帳戶。

**什麼是我的訂閱 hello 配額 hello 影響？**

hello hello 虛擬機器、 虛擬網路以及透過 hello Azure Resource Manager 建立的儲存體帳戶的配額不會從其他配額。 每個訂用帳戶取得配額 toocreate hello 資源使用 hello 新的 Api。 您可以深入了解 hello 其他配額[這裡](../azure-subscription-service-limits.md)。

**可以繼續執行 toouse 我自動化的指令碼佈建虛擬機器、 虛擬網路以及透過 hello 資源管理員 Api 的儲存體帳戶？**

所有的 hello 自動化和您建立的指令碼繼續 toowork hello 的現有虛擬機器，而在 hello Azure 服務管理模式下建立的虛擬網路。 不過，hello 指令碼有 toobe 更新的 toouse hello 新結構描述建立 hello hello Resource Manager 模式透過相同的資源。

**哪裡可以找到 Azure Resource Manager 範本的範例？**

一組完整的入門範本可在 [Azure Resource Manager 快速入門範本](https://azure.microsoft.com/documentation/templates/)中找到。

## <a name="next-steps"></a>後續步驟
* 透過定義虛擬機器、 儲存體帳戶和虛擬網路，請參閱範本建立 hello toowalk[資源管理員範本逐步解說](resource-manager-template-walkthrough.md)。
* toosee hello 命令部署範本，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

