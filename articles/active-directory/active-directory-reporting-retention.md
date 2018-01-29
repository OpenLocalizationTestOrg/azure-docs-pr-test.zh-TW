---
title: "Azure Active Directory 報告保留原則 | Microsoft Docs"
description: "Azure Active Directory 中報告資料的保留原則"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: identity
ms.date: 12/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 61d3e8fbe26ab24ba0b551e52be0769228f09a11
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/16/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Azure Active Directory 報告保留原則


本主題為您提供 Azure Active Directory 中各種活動報告的資料保留相關常見問題的解答。 

**問：如何才能開始收集活動資料？**

**答：**

| Azure AD 版本 | 開始收集 |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | 當您註冊訂用帳戶時 |
| Azure AD Free | 首次開啟 [Azure Active Directory 刀鋒視窗](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)或使用[報告 API](https://aka.ms/aadreports)  |

---
**問：何時可在 Azure 入口網站中取得您的活動資料？**

**答：**

- **立即**-如果您已使用 Azure 入口網站中的報表
- **在 2 小時內**-如果您尚未開啟報告在 Azure 入口網站

---
**問：如何才能開始收集安全性訊號？**  

**答：**對於安全性訊號，收集程序會在您選擇使用 Identity Protection 中心時啟動。 


---
**問：收集的資料會儲存多久？**

**答：**

**活動報告**    

| 報告                 | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| 目錄稽核        | 7 天        | 30 天             | 30 天             |
| 登入活動       | N/A           | 30 天             | 30 天             |
| Azure MFA 使用        | 30 天       | 30 天             | 30 天             |

**安全性訊號**

| 報告         | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| 有風險的使用者  | 7 天        | 30 天             | 90 天             |
| 有風險的登入 | 7 天        | 30 天             | 90 天             |

---
