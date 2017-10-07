---
title: "重新啟動適用於 Linux Vm 在 Azure 中的維護 aaaVM |Microsoft 文件"
description: "Linux 虛擬機器的維護造成 VM 重新啟動"
services: virtual-machines-linux
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 41caa2e56740cdfa95d2ea67278e5c1d15a174c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vm-restarting-maintenance"></a>維護造成 VM 重新啟動

有少數的情況下因為 tooplanned 維護 toohello 基礎基礎結構重新啟動 Vm。 在裝載於 Azure Vm 的影響 toothe 可用性，hello 下列現在均可供您 toouse:

-   通知會傳送 hello 影響前至少 30 天。

-   每個每個 VM 的可見性 toohello 維護期間。

-   設定 hello 精確的時間進行維護，以影響您的 Vm 中的控制和彈性。

Microsoft Azure 中的維護會以反覆項目排程。 初始反覆項目具有較小的範圍中順序 tooreduce hello 風險參與推出新的修正程式和功能。 稍後反覆項目可能會跨越多個區域 (hello 絕不會從相同的區域組)。 VM 包含在單一維護反覆項目。 如果反覆項目已中止，剩餘的 VM 會包含在其他日後的反覆項目中。

hello 計劃性的維護反覆項目有兩個階段： Pre-emptive 的維護期間和已排程維護視窗。

hello **Pre-emptive 維護視窗**hello 彈性 tooinitiate hello 維護您的 Vm 上為您提供。 如此一來，您可以判斷您的 Vm 會受到影響，hello hello 更新和維護每個 VM 之間的 hello 時間序列。 您可以查詢每個 VM toosee，是否已規劃的維護，並檢查您的最後一個發出的維護要求 hello 結果。

hello**排程的維護視窗**時，Azure 已排程進行 hello 維護您的 Vm。 這段期間，會遵循先佔式維護期間，您可以仍然 hello 維護視窗，請查詢，但不再是無法 tooorchestrate hello 維護。

## <a name="availability-considerations-during-planned-maintenance"></a>規劃維護期間的可用性考量 

### <a name="paired-regions"></a>配對的區域

每個 Azure 區域搭配另一個地區內 hello 一起進行地區組的相同地理位置。 當執行維護，Azure 只會更新 hello 虛擬機器執行個體在單一區域中的其配對。 例如，在更新 hello 美國中北部的虛擬機器時，Azure 不會更新在美國中南部任何虛擬機器在 hello 相同的時間。 這兩次更新作業會分別排定在不同的時間，以啟用區域之間的容錯移轉或負載平衡功能。 不過，其他地區為北歐可以進行維護在 hello 相同時間為美國東部。
深入了解 [Azure 區域配對](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)。

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>單一執行個體 VM 相較於可用性設定組或 VM 擴展集

在部署在 Azure 中使用虛擬機器工作負載時，您可以建立 hello Vm 內的可用性設定組中訂單 tooprovide 高可用性 tooyour 應用程式。 這項組態可以確保在中斷或維護事件期間，至少有一部虛擬機器可供使用。

在可用性設定組，個別的 Vm 會散佈 too20 更新網域設定。 在規劃維護期間，在任何指定時間只有單一更新網域受影響。 hello 順序受到影響的更新網域可能不會繼續循序計劃性維護期間。 單一執行個體 Vm （不屬於可用性設定組），沒有任何方式 toopredict 或決定哪些，以及多少 Vm 會一起受到影響。

虛擬機器擴展集都可讓您的 Azure 計算資源 toodeploy 和管理一組相同的 Vm 為單一資源。
hello 規模集提供類似的保證 tooan 可用性設定組更新網域的形式。 

如需有關如何設定您的虛擬機器的高可用性的詳細資訊，請參閱[*管理 Windows 虛擬機器的 hello 可用性*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

### <a name="scheduled-events"></a>排定的事件

Azure 的中繼資料服務可讓您 toodiscover 您在 Azure 中裝載的虛擬機器資訊。 排程的事件，其中一個 hello 公開類別、 介面有關即將發生的事件 （例如，在重新開機），才能為其準備您的應用程式，以及限制中斷。

如需排程的事件的詳細資訊，請參閱太[Azure 中繼資料服務-排程的事件](../virtual-machines-scheduled-events.md)。

## <a name="maintenance-discovery-and-notifications"></a>維護探索和通知

維護排程是在 hello 個別 Vm 層的可見 toocustomers。 您可以使用 Azure 入口網站、 API、 PowerShell 或 CLI tooquery 的先佔式與排程的維護期間。 此外，應該會收到通知 （電子郵件） hello 萬一其中一個 （或多個） 您的 Vm 會影響 hello 程序期間。

先佔式維護和排程維護階段開始時會發出通知。 預期 tooreceive 單一通知每個 Azure 訂用帳戶。 hello 通知會傳送預設 toohello 訂用帳戶的系統管理員和共同管理員。 您也可以設定 hello 維護通知的對象。

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Hello 入口網站中檢視 hello 維護視窗 

您可以使用 hello Azure 入口網站，並尋找排程維護的 Vm。

1.  登入 toohello Azure 入口網站。

2.  按一下，然後開啟 hello**虛擬機器**刀鋒視窗。

3.  按一下 hello**資料行**從可用的資料行 toochoose 按鈕 tooopen hello 清單

4.  選取並加入 hello**維護視窗**資料行。 已排程維護的 Vm 有顯示 hello 維護期間。 一旦維護完成或中止，則維護期間將不再顯示。

### <a name="query-maintenance-details-using-hello-azure-api"></a>查詢使用 hello Azure 應用程式開發介面的維護詳細資料

使用 hello[取得 VM 資訊 API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get)並尋找 hello 執行個體檢視 toodiscover hello 維護詳細資料的個別 VM 上。 hello 回應包含下列項目 hello:

  - isCustomerInitiatedMaintenanceAllowed： 指出是否可以立即起始 hello VM 上的先佔式重新部署。

  - preMaintenanceWindowStartTime: hello hello 先佔式維護期間的開始時間。

  - preMaintenanceWindowEndTime: hello hello 先佔式維護視窗結束時間。 在此時間之後, 您將不再能夠 tooinitiate 維護此 VM 上。
    
  - maintenanceWindowStartTime: hello 的開始時間 hello 排程的維護期間時 VM 會受到影響。

  - maintenanceWindowEndTime: hello hello 排程的維護期間的結束時間。
  
  - lastOperationResultCode: hello 最後的維護重新部署作業的結果。
 
  - lastOperationMessage： 訊息的最後一個維護重新部署作業的描述 hello 結果。


## <a name="pre-emptive-redeploy"></a>先佔式重新部署

先佔式重新部署動作提供維護時套用的 tooyour Vm 在 Azure 中的 hello 彈性 toocontrol hello 時間。 計劃性的維護的開頭的先佔式的維護期間，您可以決定為每個重新啟動您的 Vm toobe hello 確切時間。 以下是這類功能很實用的使用案例：

-   維護需要 toobe 協調 hello 一般客戶使用。

-   Azure 所提供的 hello 排程的維護期間並不足夠。
    可能是 hello 視窗發生 toobe 在一週的 hello 忙碌時間或太長。

-   多個執行個體或多層式應用程式，您需要兩個 Vm 或特定順序 toofollow 之間有足夠的時間。

當您呼叫的先佔式重新部署 VM 上時，它會移動 hello VM tooan 已經更新節點，然後開啟電源時它上，保留所有組態選項及相關聯的資源。 雖然這樣做，hello 暫存磁碟會遺失，而且會更新虛擬網路介面相關聯的動態 IP 位址。

系統會對每個 VM 啟用一次先佔式重新部署。 如果 hello 程序期間發生錯誤時，hello 作業已中止，VM 不受影響的 hello 和它被排除 hello 計劃的維護反覆項目。 您會在與新的排程更新的時間內連絡並在您的 Vm 提供新商機 tooschedule 和順序 hello 的影響。
