---
title: "aaaAzure Active Directory 報告延遲 |Microsoft 文件"
description: "深入了解 hello 報告事件 tooshow 在 Azure 入口網站所花費的時間量"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Azure Active Directory 報告延遲

與[reporting](active-directory-preview-explainer.md) hello Azure Active Directory，在您取得所有 hello 資訊需要的 toodetermine 您的環境執行的動作。 hello reporting hello Azure 入口網站中的資料 tooshow 總就所謂的延遲所花費的時間量。 

本主題列出 hello Azure 入口網站中的所有報表類別目錄的 hello hello 延遲資訊。 


## <a name="activity-reports"></a>活動報告

有兩個活動報告的區域︰

- **登入活動**– hello 使用量資訊的受管理的應用程式和使用者登入活動
- **稽核記錄檔** - 使用者和群組管理、受管理應用程式和目錄活動的相關系統活動資訊

hello 下表列出 hello 活動報告的延遲資訊。

| 報告 | 最小值 | 平均值 | 最大值 |
| :-- | --- | --- | --- |
| 稽核記錄檔             | 30 分鐘  | 45 分鐘 | 1 小時     |
| 登入               | 15 Minuten  | 15 Minuten | 2 小時*   |

>[!NOTE]
> 對於某些來自舊版 office 應用程式登入活動資料，可能需要報告資料 tooshow hello too8 的小時。 


## <a name="security-reports"></a>安全性報告

有兩個安全性報告的區域︰

- **高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。 
- **標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。 

hello 下表列出 hello 安全性報告的延遲資訊。

| 報告 | 最小值 | 平均值 | 最大值 |
| :-- | --- | --- | --- |
| 有風險的使用者          | 5 分鐘   | 15 Minuten  | 2 小時  |
| 有風險的登入         | 5 分鐘   | 15 Minuten  | 2 小時  |

## <a name="risk-events"></a>風險事件

Azure Active Directory 使用彈性的機器學習演算法和啟發學習法 toodetect 可疑動作相關的 tooyour 使用者帳戶。 偵測到的每個可疑動作都會儲存在名為風險事件的記錄中。

hello 下表列出 hello 風險事件的延遲資訊。

| 報告 | 最小值 | 平均值 | 最大值 |
| :-- | --- | --- | --- |
| 從匿名 IP 位址登入 |5 分鐘 |15 分鐘 |2 小時 |
| 從不熟悉的位置登入 |5 分鐘 |15 分鐘 |2 小時 |
| 認證外洩的使用者 |2 小時 |4 小時 |8 小時 |
| 不可能的旅遊 tooatypical 位置 |5 分鐘 |1 小時 |8 小時  |
| 從受感染的裝置登入 |2 小時 |4 小時 |8 小時  |
| 從具有可疑活動的 IP 位址登入 |2 小時 |4 小時 |8 小時  |



## <a name="next-steps"></a>後續步驟

如果您想 tooknow 更多關於 hello Azure 入口網站中的 hello 活動報告，請參閱：

- [Hello Azure Active Directory 入口網站中的登入活動報表](active-directory-reporting-activity-sign-ins.md)
- [稽核 hello Azure Active Directory 入口網站中的活動報告](active-directory-reporting-activity-audit-logs.md)

如果您想 tooknow 更多關於 hello Azure 入口網站中的 hello 安全性報告，請參閱：

- [使用者在風險中檢視 hello Azure Active Directory 入口網站的安全性報表](active-directory-reporting-security-user-at-risk.md)
- [Hello Azure Active Directory 入口網站中的高風險的登入報表](active-directory-reporting-security-risky-sign-ins.md)

如果您想深入了解風險事件 tooknow，請參閱[Azure Active Directory 風險事件](active-directory-reporting-risk-events.md)。
