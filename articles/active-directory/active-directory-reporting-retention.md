---
title: "aaaAzure Active Directory 報告保留原則 |Microsoft 文件"
description: "Azure Active Directory 中報告資料的保留原則"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Azure Active Directory 報告保留原則


本主題提供您的解答 toohello 搭配 hello 資料保留在 Azure Active Directory 中的 hello 不同的活動報表的最常見的問題。 

**問： 如何取得活動資料入門 hello 集合？**

**答：**

| Azure AD 版本 | 開始收集 |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | 當您註冊訂用帳戶時 |
| Azure AD Free | hello 第一次開啟 hello [Azure Active Directory 刀鋒視窗](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)或使用 hello[報告 Api](https://aka.ms/aadreports)  |

---
**問： 當有活動資料 hello Azure 入口網站？**

**答：**

- **立即**-如果您已使用 hello Azure 傳統入口網站中的報表
- **在 2 小時內**-如果您尚未開啟 reporting hello Azure 傳統入口網站中

---
**問： 如何取得啟動安全性訊號 hello 集合？**  

**答：**安全性訊號 hello 收集處理程序啟動時您選擇加入的 toouse hello 識別防護中心。 


---
**問： 多久會 hello 收集的資料儲存？**

**答：**

**活動報告**    

| 報告                 | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| 目錄稽核        | 7 天        | 30 天             | 30 天             |
| 登入活動       | 7 天        | 30 天             | 30 天             |

**安全性訊號**

| 報告         | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| 有風險的使用者  | 7 天        | 30 天             | 90 天             |
| 有風險的登入 | 7 天        | 30 天             | 90 天             |

---