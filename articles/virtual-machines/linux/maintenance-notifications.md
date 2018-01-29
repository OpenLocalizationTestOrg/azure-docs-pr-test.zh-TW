---
title: "處理 Azure 中 Linux VM 的維修通知 | Microsoft Docs"
description: "檢視 Azure 中執行的 Linux 虛擬機器的維修通知，並開始自助維修。"
services: virtual-machines-linux
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: zivr
ms.openlocfilehash: d551a62a59e0a7f63f5fd4862680a271de659a19
ms.sourcegitcommit: 7d4b3cf1fc9883c945a63270d3af1f86e3bfb22a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="handling-planned-maintenance-notifications-for-linux-virtual-machines"></a>處理 Linux 虛擬機器預定進行的維修作業通知

為提升虛擬機器之主機基礎結構的可靠性、效能和安全性，Azure 會定期執行更新。 更新會變更，例如裝載環境的修補或將硬體升級與解除委任。 這些更新大多數都會在不影響託管虛擬機器的情況下執行。 不過，更新在某些情況下確實會造成影響：

- 如果維護不需要重新開機，Azure 會在主機更新時使用就地移轉來暫停 VM。

- 如果維護需要重新開機，您會在規劃維護時收到通知。 在這些情況下，您會獲得一段時間，供您在適合的時間自行開始維修。


預定進行的維護作業若需要重新開機，會排定在不同波段。 每一波段有不同的範圍 (區域)。

- 波段開始時會傳送通知給客戶。 根據預設，通知會傳送給訂用帳戶擁有者和共同擁有者。 您可以使用 Azure [活動記錄警示](../../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)，對通知新增更多收件者和傳訊選項，例如電子郵件、SMS 和 Webhook。  
- 接獲通知時，即可使用「自助期間」。 在此期間，您可以找到此波段中包含的虛擬機器，並根據自己的排程需求主動開始維護。
- 在自助期間之後，「排定維護期間」隨即開始。 在此期間的某個時間點，Azure 會排定並將必要的維護套用於您的虛擬機器。 

有兩個期間的目標是要讓您在知道 Azure 何時將會自動開始維修的同時，有足夠時間開始維修，並將虛擬機器重新啟動。


您可以使用 Azure 入口網站、PowerShell、REST API 和 CLI 來查詢您的 VM 的維修期間，並開始自助維修。

 > [!NOTE]
 > 如果您嘗試開始維護且要求失敗，Azure 會將您的虛擬機器標示為 [已略過]。 您再也無法使用由客戶所起始的維護選項。 您的虛擬機器必須由 Azure 在排定維護階段期間重新啟動。


 
## <a name="should-you-start-maintenance-using-during-the-self-service-window"></a>您是否應該在自助期間開始維護？  

下列方針應可協助您判斷是否應該使用這項功能，並且在自己的時間開始維護。

> [!NOTE] 
> 自助式維護可能不適用於所有的虛擬機器。 若要判斷主動式重新部署是否可供您的虛擬機器使用，請在維護狀態中尋找 [立即開始]。 雲端服務 (Web/背景工作角色)、Service Fabric 和虛擬機器擴展集目前無法使用自助式維護。


不建議將自助式維護用於採用**可用性設定組**的部署，因為這些都是高可用性安裝，在任何指定的時間，其中只有一個更新網域會受影響。 
    - 讓 Azure 觸發維護作業，但請注意，受影響的更新網域順序不一定會循序發生，而且更新網域之間有 30 分鐘的暫停時間。
    - 如果擔心暫時無法使用某些容量 (1/更新網域計數)，在維護期間配置其他執行個體，即可輕鬆補足。 

在下列情況，**請勿**使用自助式維護： 
    - 如果您經常關閉虛擬機器，不論是手動、使用 DevTest 實驗室、使用自動關閉，或依照排程，都可能還原維護狀態，因而造成額外的停機時間。
    - 在您知道將會在維護波段結束前遭到刪除的短期存留虛擬機器上。 
    - 在具有大量狀態的工作負載中，其大量狀態儲存在想要於更新時進行維護的本機 (暫時) 磁碟中。 
    - 在您時常調整虛擬機器大小的情況下，因為這可能會還原維護狀態。 
    - 如果您採用的排定事件能夠在維護關機開始前 15 分鐘，讓您的工作負載主動容錯移轉或正常關機。

如果您打算在排定維護階段連續不中斷地執行您的虛擬機器，而且上述的反指標都不適用，則**使用**自助式維護。 

在下列情況下，最好使用自助式維護：
    - 您需要向管理階層或一般客戶傳達確切的維護期間。 
    - 您需要在指定的日期前完成維護作業。 
    - 您需要控制維護序列 (例如多層式應用程式) 以保證安全復原。
    - 在兩個更新網域 (UD) 之間，您需要超過 30 分鐘的虛擬機器復原時間。 若要控制更新網域之間的時間，您必須在虛擬機器上觸發維護 (一次一個更新網域 (UD))。



## <a name="find-vms-scheduled-for-maintenance-using-cli"></a>使用 CLI 尋找排定維修的 VM

您可以使用 [azure vm get-instance-view](/cli/azure/vm?view=azure-cli-latest#az_vm_get_instance_view) 來查看預定進行的維修作業資訊。
 
只在有預定進行的維修作業時，才會傳回維修資訊。 如果沒有會影響 VM 的排定維修，則命令不會傳回任何維修資訊。 

```azure-cli
az vm get-instance-view -g rgName -n vmName
```

下列是 MaintenanceRedeployStatus 下傳回的值： 

| 值 | 描述   |
|-------|---------------|
| IsCustomerInitiatedMaintenanceAllowed | 指出您目前是否可以在 VM 上開始維修 ||
| PreMaintenanceWindowStartTime         | 維修自助期間的開始，此時您可以在 VM 上起始維修 ||
| PreMaintenanceWindowEndTime           | 維修自助期間的結束，此時您可以在 VM 上起始維修 ||
| MaintenanceWindowStartTime            | 排定維護期間開始，此時 Azure 會在您的虛擬機器上起始維護 ||
| MaintenanceWindowEndTime              | 排定維護期間結束，此時 Azure 會在您的虛擬機器上停止維護 ||
| LastOperationResultCode               | 前次嘗試在 VM 上起始維修的結果 ||




## <a name="start-maintenance-on-your-vm-using-cli"></a>使用 CLI 在 VM 上開始維修

如果 `IsCustomerInitiatedMaintenanceAllowed` 設為 true，則下列呼叫會在 VM 上起始維修。

```azure-cli
az vm perform-maintenance rgName vmName 
```

[!INCLUDE [virtual-machines-common-maintenance-notifications](../../../includes/virtual-machines-common-maintenance-notifications.md)]

## <a name="classic-deployments"></a>傳統部署

如果您仍有使用傳統部署模型部署的舊版 VM，可以使用 CLI 1.0 查詢 VM 並起始維護。

請鍵入下列項目，以確認您使用傳統 VM 的模式正確：

```
azure config mode asm
```

若要取得名為 *myVM* 的 VM 維護狀態，請鍵入：

```
azure vm show myVM 
``` 

若要開始維護 *myService* 服務和 *myDeployment* 部署中名為 *myVM* 的傳統虛擬機器，請鍵入：

```
azure compute virtual-machine initiate-maintenance --service-name myService --name myDeployment --virtual-machine-name myVM
```


## <a name="faq"></a>常見問題集


**問：為什麼需要立即重新啟動我的虛擬機器？**

**答：**雖然對 Azure 平台的大部分更新與升級不會影響虛擬機器的可用性，但是有時候我們無法避免重新啟動裝載於 Azure 的虛擬機器。 我們已經累積幾項變更，需要我們重新啟動伺服器，這會導致虛擬機器重新開機。

**問：如果我遵循建議針對高可用性使用可用性設定組，是否安全？**

**答：**部署在可用性設定組或虛擬機器擴展集的虛擬機器，具有更新網域 (UD) 的概念。 執行維護時，Azure 會接受 UD 條件約束，並且不會從不同的 UD (在相同的可用性設定組內) 重新啟動虛擬機器。  Azure 也會等候至少 30 分鐘，再移至下一個虛擬機器群組。 

如需有關高可用性的詳細資訊，請參閱 [Azure 中虛擬機器的區域和可用性](regions-and-availability.MD)。

**問：我如何取得規劃維護的通知？**

**答：**規劃的維護是從對一或多個 Azure 區域設定排程開始。 之後，電子郵件通知會傳送至訂用帳戶擁有者 (每個訂用帳戶一封電子郵件)。 可以使用「活動記錄警示」來設定此通知的其他通道和收件者。 如果您將虛擬機器部署到已排程規劃的維護之區域，您不會收到通知，但是需要檢查 VM 的維護狀態。

**問：我在入口網站、Powershell 或 CLI 中都看不到任何關於規劃的維護之指示，發生什麼情況？**

**答：**與規劃的維護相關之資訊僅在規劃的維護期間，適用於受到該維護影響的 VM。 也就是說，如果您看不到資料，可能是維護已完成 (或尚未啟動)，或者您的虛擬機器是裝載在更新的伺服器上。

**問：是否有方法可以確切知道我的虛擬機器何時會受到影響？**

**答：**設定排程時，我們會定義數天的時間期間。 不過，此期間內伺服器 (和 VM) 的確切順序則未知。 想要知道其虛擬機器確切時間的客戶，可以使用[排定事件](scheduled-events.md)並且從虛擬機器內查詢，而後會在虛擬機器重新啟動前 15 分鐘收到通知。

**問：重新啟動我的虛擬機器需要多久時間？**

**答：**根據您的虛擬機器大小，在自助式維護期間重新啟動最長可能需要幾分鐘的時間。 在 Azure 於排定維護期間起始重新啟動期間，重新啟動通常需要大約 25 分鐘。 請注意，如果您使用雲端服務 (Web/背景工作角色)、虛擬機器擴展集或可用性設定組，在排定維護期間每個虛擬機器群組 (UD) 之間有 30 分鐘。

**答：在雲端服務 (Web/背景工作角色)、Service Fabric 和虛擬機器擴展集的案例下會有什麼體驗？**

**答：**這些平台會受到規劃的維護影響，使用這些平台的客戶是安全的，因為只有單一升級網域 (UD) 中的 VM 會在任何指定時間受到影響。 雲端服務 (Web/背景工作角色)、Service Fabric 和虛擬機器擴展集目前無法使用自助式維護。

**問：我收到一封關於硬體解除委任的電子郵件，這與規劃的維護相同嗎？**

**答：**硬體解除委任是規劃的維護事件，我們尚未讓這個使用案例上架到新的體驗。  

**問：我在我的 VM 上看不到任何維護資訊。哪裡發生錯誤？**

**答：**您在 VM 上看不到任何維護資訊有以下幾個原因：
1.  您使用標示為 Microsoft 內部的訂用帳戶。
2.  您的 VM 未排程進行維護。 可能是維護已經結束、取消或修改，所以您的 VM 不再受到它的影響。
3.  您尚未將 [維護] 資料行新增至您的虛擬機器清單檢視。 雖然我們已將此資料行新增至預設檢視，但是設定為查看非預設資料行的客戶必須將 [維護] 資料行手動新增至其 VM 清單檢視。

**問：我的 VM 第二次排程進行維護。原因為何？**

**答：**有數個使用案例，您會在您已完成維護重新部署之後，看到 VM 排程進行維護：
1.  我們已取消維護，並且使用不同的裝載重新啟動它。 可能是我們偵測到發生錯誤的裝載，只是需要部署額外承載。
2.  因為硬體故障，您的 VM 已「服務修復」到另一個節點
3.  您已選取停止 (解除配置)，然後重新啟動 VM
4.  您已為 VM 開啟 [自動關機]


**問：我的可用性設定組維護需要較長的時間，而我現在看到某些可用性設定組執行個體上顯示 [已略過] 狀態。原因為何？** 

**答：**如果您已按一下來短期連續更新可用性設定組中的多個執行個體，Azure 會將這些要求排入佇列並開始更新虛擬機器 (一次只更新一個更新網域 (UD) 中的虛擬機器)。 不過，因為更新網域之間可能會暫停，所以更新可能需要更長的時間。 如果更新佇列需要超過 60 分鐘的時間，即使有些佇列已成功更新，這些佇列仍會顯示 [已略過] 狀態。 為了避免此錯誤狀態，只要按一下一個可用性設定組內的一個執行個體並等候該虛擬機器更新完成，再按一下不同更新網域中的下一個虛擬機器，即可更新您的可用性設定組。


## <a name="next-steps"></a>後續步驟

了解如何使用[排定的事件](scheduled-events.md)從 VM 內註冊取得維修事件。
