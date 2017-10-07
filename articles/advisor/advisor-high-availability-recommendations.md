---
title: "aaaAzure Advisor 高可用性建議 |Microsoft 文件"
description: "使用您的 Azure 部署的 Azure Advisor tooimprove 高可用性。"
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>建議程式高可用性建議

Azure Advisor 可協助您確保和改善的業務關鍵應用程式的 hello 持續性。 您可以從 hello 取得高可用性建議 advisor**高可用性**hello Advisor 儀表板 索引標籤。

![Hello Advisor 儀表板上高可用性 按鈕](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>確保虛擬機器的容錯

建議程式會識別不屬於可用性設定組的虛擬機器，並建議將它們移至某個可用性設定組中。 若要提供備援 tooyour 應用程式，我們建議您群組的可用性設定組中的兩個或多個虛擬機器。 此組態可確保任一個計劃或非計劃性維護事件期間，至少一部虛擬機器可變更，同時符合 hello Azure 虛擬機器 SLA。 您可以選擇任一 toocreate 可用性設定組的 hello 虛擬機器或 tooadd hello 虛擬機器 tooan 現有可用性設定組。

> [!NOTE]
> 如果您選擇 toocreate 可用性設定，您必須將一個以上的多個虛擬機器加入它。 我們建議您分兩個或更多虛擬機器的可用性集 tooensure 發生中斷時可使用至少一部電腦。

![Advisor 建議︰為了獲得虛擬機器備援功能，請使用可用性設定組](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>確保可用性設定組的容錯 

Advisor 可識別包含單一虛擬機器的可用性設定組，並建議將一或多個虛擬機器 tooit。 若要提供備援 tooyour 應用程式，我們建議您群組的可用性設定組中的兩個或多個虛擬機器。 此組態可確保任一個計劃或非計劃性維護事件期間，至少一部虛擬機器可變更，同時符合 hello Azure 虛擬機器 SLA。 您可以在虛擬機器或 toouse 現有的虛擬機器和 tooadd 選擇任一 toocreate 它 toohello 可用性設定組。  

![Advisor 建議： 加入一或多個 Vm toothis 可用性設定組](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>確保應用程式閘道的容錯
tooensure hello 的關鍵任務應用程式由應用程式閘道所形成的業務續航力，Advisor 識別未設定為允許容錯功能的應用程式閘道器執行個體，並建議您可以採取的修復動作. Advisor 可識別中型或大型的單一執行個體應用程式閘道，並建議再新增至少一個執行個體。 它也會識別單一或多重 instance 小型應用程式閘道，並建議移轉 toomedium 或大型的 Sku。 Advisor 建議這些動作 tooensure 應用程式的閘道器執行個體所設定的 toosatisfy hello 目前 SLA 的需求，這些資源。

![Advisor 建議︰部署兩個以上的中型或大型應用程式閘道執行個體](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>改善 hello 效能和可靠性的虛擬機器磁碟

Advisor 可識別標準磁碟的虛擬機器，並建議升級 toopremium 磁碟。
 
針對執行時需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」可提供高效能、低延遲的磁碟支援。 使用進階儲存體帳戶的虛擬機器磁碟會將資料儲存在固態硬碟 (SSD) 上。 Hello 應用程式的最佳效能，我們建議您移轉需要高 IOPS toopremium 儲存任何虛擬機器磁碟。 

如果您的磁碟不需要高 IOPS，您可以讓磁碟留在標準儲存體中以節省成本。 標準儲存體會將虛擬機器磁碟資料儲存在硬碟機 (HDD) 而非 SSD 上。 您可以選擇 toomigrate 虛擬機器磁碟 toopremium 磁碟。 大部分的虛擬機器 SKU 都支援進階磁碟。 不過，在某些情況下，如果您想 toouse 高階磁碟，您可能需要 tooupgrade 您的虛擬機器的 Sku 以及。

![Advisor 建議： 升級 toopremium 磁碟來改善您的虛擬機器磁碟 hello 可靠性](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>防止意外刪除虛擬機器的資料
Advisor 會識別未啟用備份的虛擬機器，並建議啟用備份。 設定虛擬機器備份可確保業務關鍵資料的 hello 可用性，以及提供防止被意外刪除或損毀。

![Advisor 建議： 設定虛擬機器備份 tooprotect 重要的資料](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>在 Advisor 中取得高可用性建議

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 在 hello 左窗格中，按一下 **更多服務**。

3. 在 hello 服務功能表窗格底下**監視及管理**，按一下  **Azure Advisor**。  
 hello Advisor 儀表板會顯示。

4. 在 hello Advisor 儀表板上按一下 hello**高可用性**索引標籤，然後再選取您想要的 tooreceive 建議的 hello 訂用帳戶。

> [!NOTE]
> tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。 已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。 此作業「只需要執行一次」。 Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。

## <a name="next-steps"></a>後續步驟

如需 Advisor 建議的詳細資訊，請參閱：
* [簡介 tooAzure Advisor](advisor-overview.md)
* [開始使用建議程式](advisor-get-started.md)
* [建議程式成本建議](advisor-performance-recommendations.md)
* [建議程式效能建議](advisor-performance-recommendations.md)
* [建議程式安全性建議](advisor-security-recommendations.md)

