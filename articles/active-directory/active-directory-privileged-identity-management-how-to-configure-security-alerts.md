---
title: "如何設定安全性警示 | Microsoft Docs"
description: "了解如何為 Azure Privileged Identity Management 擴充功能設定安全性警示。"
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 52a03624b8e3841f559caef564712ff74a614365
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-configure-security-alerts-in-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management：如何設定安全性警示
## <a name="security-alerts"></a>安全性警示
當您環境中有可疑或不安全的活動時，Azure Privileged Identity Management (PIM) 會產生警示。 觸發警示時，會顯示在 PIM 儀表板上。 選取警示，以查看詳列觸發警示之使用者或角色的報告。

![PIM 儀表板安全性警示 - 螢幕擷取畫面][1]

| 警示 | 觸發程序 | 建議 |
| --- | --- | --- |
| **在 PIM 外指派角色** |在 PIM 介面外將系統管理員永久指派給了某個角色。 |請檢閱新的角色指派。 由於其他服務只能指派永久系統管理員，因此請視需要將它變更成合格指派。 |
| **啟用角色的次數太頻繁** |在設定所允許的時間內，重複啟用相同角色的次數過多。 |請連絡使用者以了解他們啟用角色這麼多次的原因。 可能是時間限制太短以致於他們無法完成其工作，或可能是他們使用指令碼來自動啟用角色。 |
| **角色不需要多重要素驗證來進行啟用** |設定中有一些未啟用 MFA 功能的角色。 |針對特殊權限最高的角色，我們要求必須啟用 MFA，但強烈建議您針對所有角色的啟用都啟用 MFA。 |
| **系統管理員未使用其特殊權限角色** |有合格的系統管理員最近尚未啟用其角色。 |請開始存取權檢閱，以判斷出不再需要存取權的使用者。 |
| **全域管理員太多** |全域管理員的數目超過建議的數目。 |如果您有大量的全域管理員，使用者可能會取得超過其所需的權限。 請將使用者移至特殊權限較低的角色，或將部分使用者設為符合該角色資格，而不是永久指派。 |

## <a name="configure-security-alert-settings"></a>設定安全性警示設定
您可以在 PIM 中自訂一些安全性警示，以便配合您的環境和安全性目標。 請依照下列步驟來前往 [設定] 刀鋒視窗︰

1. 登入 [Azure 入口網站](https://portal.azure.com/)，然後從儀表板中選取 [Azure AD Privileged Identity Management] 磚。
2. 選取 [受控的特殊權限角色] > [設定] > [警示設定]。
   
    ![瀏覽至安全性警示設定][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>「啟用角色的次數太頻繁」警示
當使用者在指定期間內多次啟用相同的特殊權限角色時，就會觸發此警示。 您可以同時設定時段和啟用次數。

* **啟用更新時間範圍**︰以天、小時、分鐘及秒為單位，指定您想要用來追蹤可疑更新的時段。
* **啟用更新次數**︰指定在您選擇的時間範圍內，您視為值得發出警示的啟用次數 (從 2 到 100)。 您可以移動滑桿或在文字方塊中輸入數字，以變更此設定。

### <a name="there-are-too-many-global-administrators-alert"></a>「全域管理員太多」警示
當符合兩個不同的條件時，PIM 就會觸發此警示，而您可以同時設定這兩個條件。 首先，您必須達到特定的全域管理員臨界值。 其次，角色指派總數中必須有特定百分比是全域管理員。 如果只符合這些測量結果其中之一，就不會出現警示。  

* **全域管理員數目下限**︰指定您視為不安全數量的全域管理員數目 (從 2 到 100)。
* **全域管理員百分比**：指定在您環境中視為不安全、擔任全域管理員的系統管理員百分比 (從 0% 到 100%)。

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>「系統管理員未使用其特殊權限角色」警示
當使用者在經過一段特定時間後仍未啟用角色，就會觸發此警示。

* **天數**︰指定使用者可以維持不啟用角色的天數 (從 0 到 100)。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
