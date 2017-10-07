---
title: "aaaHow tooconfigure 安全性警示 |Microsoft 文件"
description: "了解如何 tooconfigure 安全性警示 Azure Privileged Identity Management 延伸模組。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
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
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>在 Azure AD Privileged Identity Management tooconfigure 安全性警示的方式
## <a name="security-alerts"></a>安全性警示
當您環境中有可疑或不安全的活動時，Azure Privileged Identity Management (PIM) 會產生警示。 警示觸發時，會出現在 hello PIM 儀表板。 選取 hello 警示 toosee 清單 hello 使用者或角色觸發 hello 警示報表。

![PIM 儀表板安全性警示 - 螢幕擷取畫面][1]

| 警示 | 觸發程序 | 建議 |
| --- | --- | --- |
| **在 PIM 外指派角色** |系統管理員已永久指派 tooa 角色，hello PIM 介面之外。 |檢閱 hello 新增角色指派。 因為其他服務只可以指派永久系統管理員，請視需要變更它 tooan 合格的指派。 |
| **啟用角色的次數太頻繁** |沒有太多重新啟動的 hello 的時間內的相同角色允許 hello 設定中的 hello。 |請連絡 hello 使用者 toosee 為何他們已啟用 hello 角色太多次。 或許 hello 時間限制太短，toocomplete 其工作，也可能使用指令碼 tooautomatically 啟用角色。 |
| **角色不需要多重要素驗證來進行啟用** |有沒有 hello 設定中啟用 MFA 的角色。 |我們要求使用 MFA 進行 hello 最高特殊權限角色，但強烈建議您啟用所有角色的啟用 MFA。 |
| **系統管理員未使用其特殊權限角色** |有合格的系統管理員最近尚未啟用其角色。 |啟動不再需要存取存取檢閱 toodetermine hello 使用者。 |
| **全域管理員太多** |全域管理員的數目超過建議的數目。 |如果您有大量的全域管理員，使用者可能會取得超過其所需的權限。 移動使用者 tooless 特殊權限角色，或其中部分適合 hello 角色，而不是永久指派。 |

## <a name="configure-security-alert-settings"></a>設定安全性警示設定
您可以自訂一些 PIM toowork 與您的環境安全性目標中的 hello 安全性警示。 請遵循這些步驟 tooreach hello 設定 刀鋒視窗：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello **Azure AD Privileged Identity Management**從 hello 儀表板磚。
2. 選取 [受管理的特殊權限角色] > [設定] > [警示設定]。
   
    ![瀏覽 toosecurity 警示設定][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>「啟用角色的次數太頻繁」警示
如果使用者啟動觸發程序在指定期間內多次 hello 相同的特殊權限的角色此警示。 您可以設定這兩個 hello 時間期限和 hello 啟用次數。

* **啟動更新的時間範圍內**： 指定在天、 小時、 分鐘，而且第二個 hello 時間週期希望 toouse tootrack 可疑續訂。
* **啟用更新次數**： 指定 hello 的啟用數，從 2 too100，考量的警示，您所選擇的 hello 時間範圍內。 您可以變更此設定所移動的 hello 滑桿，或在 hello 文字方塊中輸入數字。

### <a name="there-are-too-many-global-administrators-alert"></a>「全域管理員太多」警示
當符合兩個不同的條件時，PIM 就會觸發此警示，而您可以同時設定這兩個條件。 首先，您需要 tooreach 特定的臨界值的全域管理員。 其次，角色指派總數中必須有特定百分比是全域管理員。 如果您只符合這些度量的其中一項，hello 警示未出現。  

* **全域管理員數目下限**： 指定的全域管理員，從 2 too100，請考慮不安全的數量的 hello 數目。
* **全域管理員佔**： 指定的系統管理員是全域管理員，從 0%的 hello 百分比 too100%不安全環境中。

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>「系統管理員未使用其特殊權限角色」警示
當使用者在經過一段特定時間後仍未啟用角色，就會觸發此警示。

* **天數**： 指定的天數，從 0 too100，使用者可以前往不啟動角色的 hello。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
