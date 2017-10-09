---
title: "在 Azure 時間數列 Insights aaaData 存取原則 |Microsoft 文件"
description: "在本教學課程，了解時間序列 Insights 中的 toomanage 資料存取原則"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>授與使用 Azure 入口網站的資料存取 tooa 時間數列 Insights 環境

Time Series Insights 環境有兩種獨立的存取原則︰

* 管理存取原則
* 資料存取原則

這兩種原則可將特定環境的各種權限授與給 Azure Active Directory 主體 (使用者和應用程式)。 hello 主體 （使用者和應用程式） 必須屬於 toohello active directory （或 「 Azure 租用戶 「） 包含 hello 環境的 hello 訂用帳戶相關聯。

管理存取權原則授與 hello 環境的權限相關的 toohello 設定例如
*   建立和刪除 hello 環境中，事件來源的參考資料集和
*   Hello 資料存取原則的管理。

資料存取原則授與權限 tooissue 資料查詢、 處理 hello 環境中的參考資料和共用儲存的查詢和檢視方塊與 hello 環境相關聯。

hello 兩種原則允許存取 toohello hello 環境管理，以及存取 toohello hello 環境內的資料之間有清楚的區隔。 比方說，它是可能 toosetup 環境，使 hello 擁有者/的建立者 hello 環境移除 hello 資料存取。 使用者和服務可從 hello 環境 tooread 資料以及可能會被授與 hello 環境的任何存取 toohello 組態。

## <a name="grant-data-access"></a>授與資料存取
hello 下列步驟顯示如何 toogrant 資料存取的使用者主體：

1.  登入 toohello [Azure 入口網站](https://portal.azure.com)。
2.  按一下 [所有資源] 功能表中的 hello 左邊 hello hello Azure 入口網站。
3.  選取 Time Series Insights 環境。

  ![管理 hello 時間數列 Insights 來源-環境](media/data-access/getstarted-grant-data-access1.png)

4.  選取 [資料層存取]，按一下 [新增]

  ![管理 hello 時間數列 Insights 來源-新增](media/data-access/getstarted-grant-data-access2.png)

5.  按一下 [選取使用者]。
6.  搜尋並選取以 hello 電子郵件的使用者。
7.  在 [選取使用者] 刀鋒視窗中按一下 [選取]。

  ![管理 hello 時間數列 Insights 來源選取的使用者](media/data-access/getstarted-grant-data-access3.png)

8.  按一下 [選取角色]。
9.  如果您想 tooallow 使用者 toochange 參考資料，並且與 hello 環境的其他使用者共用已儲存的查詢和檢視方塊，請選取 「 著作人 」。 否則選取 hello 環境中的 「 讀取 」 tooallow 使用者查詢資料並儲存在 hello 環境中的個人 （不共用） 的查詢。
10. 在 hello 「 選取的角色 」 刀鋒視窗中，按一下 確定。

  ![管理 hello 時間數列 Insights 來源選取的角色](media/data-access/getstarted-grant-data-access4.png)

11. 在 hello 「 選取使用者角色 」 刀鋒視窗中，按一下 確定。
12. 您應該會看到：

  ![管理 hello 時間數列 Insights 來源結果](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>後續步驟

* [建立事件來源](time-series-insights-add-event-source.md)
* [傳送事件](time-series-insights-send-events.md)toohello 事件來源
* 在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境
