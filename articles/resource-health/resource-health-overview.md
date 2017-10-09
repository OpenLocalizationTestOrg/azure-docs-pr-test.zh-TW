---
title: "aaaAzure 資源健全狀況概觀 |Microsoft 文件"
description: "Azure 資源健康狀態的概觀"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Azure 資源健康狀態概觀
 
當 Azure 問題影響到您的資源健康狀態時，協助進行診斷並取得支援。 它會通知您有關 hello 目前和過去健康情況的資源，並協助您解決問題。 資源健康狀態會在您需要解決 Azure 服務問題時提供技術支援。

而[Azure 狀態](https://status.azure.com)通知服務問題會影響一組廣泛的 Azure 客戶、 資源健全狀況可提供您個人化的資源的 hello 健全狀況儀表板。 資源健全狀況會顯示您的資源已在 hello 中無法使用的所有 hello 時間逾期未付 tooAzure 服務問題。 這使得您 toounderstand 簡單如果已違反 SLA。 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>何謂資源，以及資源健康狀態如何決定資源健康與否？
資源是 Azure 服務透過 Azure Resource Manager 所提供之資源類型的執行個體，例如︰虛擬機器、Web 應用程式或 SQL Database。

資源健全狀況依賴於資源是否狀況良好，hello 不同的 Azure 服務 tooassess 所發出的訊號。 如果資源會處於狀況不良，資源健全狀況會分析 hello 問題的其他資訊 toodetermine hello 來源。 它也可以識別 Microsoft 正在 toofix hello 問題，或是您可以採取 tooaddress hello 造成 hello 問題的動作。 

檢閱 hello 完整資源類型和健全狀況檢查清單[Azure 資源健全狀況](resource-health-checks-resource-types.md)的健全狀況評估的方式的其他詳細資料。

## <a name="health-status-provided-by-resource-health"></a>資源健康狀態所提供的健全狀態
資源的 hello 健全狀況是 hello 下列狀態其中之一：

### <a name="available"></a>可用
hello 服務偵測不到任何事件影響 hello hello 資源健全狀況。 萬一其中 hello 資源剛從非計劃性停機期間 hello 最後 24 小時，您會看到 hello**最近復原**通知。

![資源健康狀態可用的虛擬機器](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>無法使用
hello 服務偵測到的進行中的平台或影響 hello 健全狀況的 hello 資源的非平台事件。

#### <a name="platform-events"></a>平台事件
這些事件所觸發的多個元件的 hello Azure 基礎結構，而且包含排程的動作，如 預定的維護和未計劃的主機重新開機類似的非預期的事件都。

資源健全狀況 hello 事件，hello 復原程序提供其他詳細資料，並讓您有 toocontact 支援即使沒有使用中的 Microsoft 支援合約。

![資源健全狀況無法使用虛擬機器因為 tooplatform 事件](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>非平台事件
由使用者，例如停止虛擬機器，或是達到 hello 連線 tooa Redis 快取的數目上限，所採取的動作會觸發這些事件。

![資源健全狀況無法使用虛擬機器因為 toonon 平台事件](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>不明
此健全狀態表示資源健康狀態超過 10 分鐘未收到此資源的相關資訊。 雖然這個狀態不是 hello hello 資源狀態的明確指示，它會是 hello 疑難排解程序中的重要資料點：
* 如果 hello 資源是否如預期的 hello 的 hello 資源將會更新狀態 tooAvailable 幾分鐘後執行。
* 如果您遇到的問題與 hello 資源，hello 不明健康情況狀態可能會建議 hello 資源受到 hello 平台事件。

![資源健康狀態未知的虛擬機器](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>報告不正確的狀態
如果在任何時間點您認為 hello 目前的健全狀況狀態不正確，您可以讓我們知道，依序按一下**報告不正確的健全狀況狀態**。 在您受到影響的 Azure 問題的情況下，我們建議您 toocontact 支援 hello 資源健全狀況刀鋒視窗。 

![資源健康狀態報告不正確的狀態](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>歷程記錄資訊
您可以存取向上 too14 天的健全狀況歷程記錄資料，依序按一下**檢視記錄**hello 資源健全狀況刀鋒視窗中。 

![資源健康狀態報表歷程記錄](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>開始使用
tooopen 一個資源的資源健全狀況
1.  登入到 hello Azure 入口網站。
2.  瀏覽 tooyour 資源。
3.  在位於 hello 左手邊 hello 資源功能表上，按一下**資源健全狀況**。

![從 [資源] 刀鋒視窗將資源健康狀態開啟](./media/resource-health-overview/from-resource-blade.png)

您也可以存取資源健全狀況，依序按一下**更多服務**，並輸入**資源健全狀況**中篩選文字方塊 tooopen hello**說明 + 支援**刀鋒視窗。 最後按一下 [**資源健康狀態**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth) 。

![從 [更多服務] 將資源健康狀態開啟](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>後續步驟

請參閱這些資源 toolearn，深入了解資源健全狀況：
-  [Azure 資源健康狀態中的資源類型和健康情況檢查](resource-health-checks-resource-types.md)
-  [關於 Azure 資源健康狀態的常見問題集](resource-health-faq.md)




