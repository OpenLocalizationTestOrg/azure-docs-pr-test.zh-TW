---
title: "aaaHow toouse hello 稽核登入 Azure AD Privileged Identity Management |Microsoft 文件"
description: "了解如何 toouse hello 稽核登入 hello Azure Privileged Identity Management 延伸模組。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>使用 PIM 中的 hello 稽核記錄檔
您可以使用 hello 特殊權限身分識別管理 (PIM) 稽核記錄檔 toosee 所有 hello 使用者指派和啟用在給定的時間範圍內。 如果您想 toosee hello 完整的稽核記錄的活動，包括系統管理員、 使用者和同步處理活動，在您的租用戶中，您就可以使用 hello [Azure Active Directory 存取和使用方式報表。](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>瀏覽 toohello 稽核記錄檔
從 hello [Azure 入口網站](https://portal.azure.com)儀表板、 選取 hello **Azure AD Privileged Identity Management**應用程式。 在這裡，即可存取 hello 稽核記錄檔**管理特殊權限的角色** > **稽核歷程**hello PIM 儀表板中。

## <a name="hello-audit-log-graph"></a>hello 稽核記錄圖形
在折線圖中，您可以使用 hello 稽核記錄檔 tooview hello 啟用總數、 最大啟動每天和每日平均啟用。  您也可以篩選由角色 hello 資料，如果 hello 稽核歷程記錄中有多個角色。

使用 hello**時間**，**動作**，和**角色**按鈕 toosort hello 記錄檔。

## <a name="hello-audit-log-list"></a>hello 稽核記錄檔清單
hello hello 稽核記錄檔清單中的資料行如下：

* **要求者**-hello 使用者 hello 角色啟用或變更要求。  如果 hello 值 「 Azure 系統 」，請檢查 hello Azure 稽核記錄檔，如需詳細資訊。
* **使用者**-hello 啟動或使用者 tooa 角色指派。
* **角色**-hello 角色指派，或由 hello 使用者啟動。
* **動作**-hello hello 要求者所採取的動作。 這可包括指派、解除指派、啟用或停用。
* **時間**-hello 動作發生時。
* **推理**-如果在啟用期間到 hello [原因] 欄位輸入任何文字，它會出現。
* **到期** - 只與角色啟用相關。

## <a name="filter-hello-audit-log"></a>篩選 hello 稽核記錄檔
您可以篩選 hello 資訊會出現在 [hello 稽核記錄檔中依序按一下 hello**篩選**] 按鈕。  hello**更新圖表參數刀鋒視窗**會出現。

您設定 hello 篩選之後，請按一下**更新**toofilter hello 資料 hello 記錄檔中的。  如果沒有立即顯示 hello 資料，重新整理 hello 頁面。

### <a name="change-hello-date-range"></a>變更 hello 日期範圍
使用 hello**今天**，**過去一週**，**過去一個月**，或**自訂**按鈕 toochange hello 時間範圍的 hello 稽核記錄檔。

當您選擇 hello**自訂** 按鈕，您會獲得**從**日期欄位和**至**日期欄位 toospecify hello 記錄的日期範圍。  您可以以 MM/DD/YYYY 格式輸入 hello 日期，或按一下 hello**行事曆**圖示，並從行事曆選擇日期 hello。

### <a name="change-hello-roles-included-in-hello-log"></a>變更包含在 hello 記錄中的 hello 角色
選取或取消選取 hello**角色**核取方塊下一步 tooeach 角色 tooinclude 或排除它從 hello 記錄。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

