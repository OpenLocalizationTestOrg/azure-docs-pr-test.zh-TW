---
title: "Azure Active Directory 報告延遲 | Microsoft Docs"
description: "在您的 Azure Active Directory 中針對顯示報告事件所花費的時間長度"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 346b14f8-d16d-4b07-8211-e6c5eec07062
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 9443a00232420d58dea52ed01f31a4ef964a1620
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-report-latencies"></a>Azure Active Directory 報告延遲
*這份文件是 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)的一部分。*

| 報告 | 最小值 | 平均值 | 最大值 |
| --- | --- | --- | --- |
| **安全性報告** | | | |
| 異常的登入活動 |2 小時 |4 小時 |8 小時 |
| 從不明來源登入 |2 小時 |4 小時 |8 小時 |
| 在多次失敗後登入 |2 小時 |4 小時 |8 小時 |
| 從多個地理區域登入 |2 小時 |4 小時 |8 小時 |
| 從具有可疑活動的 IP 位址登入 |2 小時 |4 小時 |8 小時 |
| 從可能受感染的裝置登入 |2 小時 |4 小時 |8 小時 |
| 具有異常登入活動的使用者 |2 小時 |4 小時 |8 小時 |
| 認證外洩的使用者 |2 小時 |4 小時 |8 小時 |
| 所有使用者登入活動 |2 小時 |4 小時 |8 小時 |
| **應用程式報告** | | | |
| 帳戶佈建活動 |2 小時 |4 小時 |8 小時 |
| 帳戶佈建錯誤 |2 小時 |4 小時 |8 小時 |
| 應用程式使用情況 |2 小時 |4 小時 |8 小時 |
| 密碼變換狀態 |2 小時 |4 小時 |8 小時 |
| **稽核與活動報告** | | | |
| 稽核報告 |1 分鐘 |15 Minuten |30 分鐘 |
| 密碼重設活動 (Azure AD) |2 小時 |4 小時 |8 小時 |
| 密碼重設活動 (Identity Manager) |2 小時 |4 小時 |8 小時 |
| 密碼重設登錄活動 (Azure AD) |2 小時 |4 小時 |8 小時 |
| 密碼重設登錄活動 (Identity Manager) |2 小時 |4 小時 |8 小時 |
| 自助服務群組活動 (Azure AD) |2 小時 |4 小時 |8 小時 |
| 自助服務群組活動 (Identity Manager) |2 小時 |4 小時 |8 小時 |
| **RMS 報告** | | | |
| 最活躍的 RMS 使用者 |2 小時 |4 小時 |8 小時 |
| RMS 使用量 |2 小時 |4 小時 |8 小時 |
| RMS 裝置使用量 |2 小時 |4 小時 |8 小時 |
| 啟用 RMS 的應用程式使用量 |2 小時 |4 小時 |8 小時 |

