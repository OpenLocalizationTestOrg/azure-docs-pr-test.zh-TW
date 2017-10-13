---
title: "何謂 Azure 排程器？ | Microsoft Docs"
description: "Azure 排程器可讓您以宣告方式描述在雲端中執行的動作。 然後它會排程這些動作並且自動執行。"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a3bf1aacd6978499d7ef77cbcb451a06b857ac38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-scheduler"></a>何謂 Azure 排程器？
Azure 排程器可讓您以宣告方式描述在雲端中執行的動作。 然後它會排程這些動作並且自動執行。  排程器會使用 [Azure 入口網站](scheduler-get-started-portal.md)、程式碼、[REST API](https://msdn.microsoft.com/library/mt629143.aspx) 或 Azure PowerShell 來完成這個動作。

排程器會建立、 維護和叫用已排程的工作。  排程器不會裝載任何工作負載或執行任何程式碼。 它只會叫用  其他位置裝載的程式碼：裝載於 Azure、內部部署或另一個提供者。 它會透過 HTTP、HTTPS、儲存體佇列、服務匯流排佇列或服務匯流排主題叫用。

排程器會排程 [工作](scheduler-concepts-terms.md)、保留使用者可以檢閱的工作執行結果歷程記錄，並且決定性地和可靠地排程要執行的工作負載。 Azure WebJobs (Azure App Service 之 Web Apps 功能的一部分) 和其他 Azure 排程功能會在背景使用排程器。 [排程器 REST API](https://msdn.microsoft.com/library/mt629143.aspx) 會協助管理這些動作的通訊。 因此，排程器可輕鬆地支援 [複雜的排程和進階週期](scheduler-advanced-complexity.md) 。

需要使用排程器的案例有幾個。 例如：

* 週期性應用程式動作：定期將 Twitter 中的資料收集到摘要中。
* 每日維護：每日剪除記錄、執行備份及其他維護工作。 例如，系統管理員可以選擇早上 1:00 備份資料庫， 期間為接下來九個月的每天。

排程器可讓您使用指令碼，在入口網站中以程式設計方式建立、更新、刪除、檢視及管理工作和 [工作集合](scheduler-concepts-terms.md) 。

## <a name="see-also"></a>另請參閱
 [Azure 排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [在 Azure 入口網站中開始使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [如何使用 Azure 排程器建立複雜的排程和進階週期](scheduler-advanced-complexity.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)

