---
title: "aaaWhat 是 Azure 排程器？ | Microsoft Docs"
description: "Azure 排程器可讓您 toodeclaratively 描述動作 toorun hello 雲端中的。 然後它會排程這些動作並且自動執行。"
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
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>何謂 Azure 排程器？
Azure 排程器可讓您 toodeclaratively 描述動作 toorun hello 雲端中的。 然後它會排程這些動作並且自動執行。  排程器的做法是使用[hello Azure 入口網站](scheduler-get-started-portal.md)，程式碼中， [REST API](https://msdn.microsoft.com/library/mt629143.aspx)，或 Azure PowerShell。

排程器會建立、 維護和叫用已排程的工作。  排程器不會裝載任何工作負載或執行任何程式碼。 它只會叫用  其他位置裝載的程式碼：裝載於 Azure、內部部署或另一個提供者。 它會透過 HTTP、HTTPS、儲存體佇列、服務匯流排佇列或服務匯流排主題叫用。

排程器排程[作業](scheduler-concepts-terms.md)，會保留工作執行結果的其中一個可以檢閱，並排程工作負載 toobe 決定性且可靠地執行。 Azure WebJobs （hello Azure App Service 中的 Web 應用程式功能的一部分） 和其他 Azure 排程功能使用排程器在 hello 背景。 hello[排程器 REST API](https://msdn.microsoft.com/library/mt629143.aspx)可協助管理這些動作的 hello 通訊。 因此，排程器可輕鬆地支援 [複雜的排程和進階週期](scheduler-advanced-complexity.md) 。

有數個應用程式為自己的排程器的 toohello 用法的案例。 例如：

* 週期性應用程式動作：定期將 Twitter 中的資料收集到摘要中。
* 每日維護：每日剪除記錄、執行備份及其他維護工作。 例如，系統管理員可以選擇 tooback hello 資料庫上午 1:00 每日 hello 未來 9 個月。

排程器可讓您 toocreate、 更新、 刪除、 檢視和管理工作和[工作集合](scheduler-concepts-terms.md)以程式設計的方式，利用指令碼，並在 hello 入口網站。

## <a name="see-also"></a>另請參閱
 [Azure 排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [開始在 hello Azure 入口網站中使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [排程 toobuild 複雜的方式與進階循環使用 Azure 排程器](scheduler-advanced-complexity.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)

