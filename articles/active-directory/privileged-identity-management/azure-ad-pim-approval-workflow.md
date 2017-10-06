---
title: "aaaAzure Privileged Identity Management 核准工作流程 |Microsoft 文件"
description: "了解 Privileged Identity Management (PIM) 中的核准工作流程"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>核准 (預覽)

## <a name="overview"></a>概觀

具有 Privileged Identity Management 的核准，您可以設定來啟動角色 toorequire 核准，並選擇一個或多個使用者或群組為委派的核准者。 如何保留讀取 toolearn tooconfigure 角色選取核准者。

>[!NOTE]
請記住，這項功能仍處於開發階段，而您可能會遇到 Bug。 hello 功能，包括文字和命名慣例可能會有所變更，而且不應視為最後。


## <a name="key-terminology"></a>重要術語

*符合資格的角色使用者*– 符合資格的角色的使用者是使用已被指派為合格 tooan Azure AD 角色您組織內 （角色需要啟用）。

*委派核准者*：委派核准者是您 Azure AD 內的一或多個個人或群組，其負責核准啟用角色的要求。

## <a name="scenarios"></a>案例

hello 私人預覽支援下列案例的 hello:

**身為特殊權限角色管理員 (PRA)，您可以：**

-   [啟用特定角色的核准](#enable-approval-for-specific-roles)

-   [指定核准者 tooapprove 要求使用者和/或群組](#specify-approver-users-and/or-groups-to-approve-requests)

-   [檢視所有特殊權限角色的要求和核准歷程記錄](#view-request-and-approval-history-for-all-privileged-roles)

**身為指定的核准者，您可以：**

-   [檢視待決的核准 (要求)](#view-pending-approvals-requests)

-   [核准或拒絕提高角色權限 (單一和/或大量) 的要求](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [提供我的核准/拒絕理由](#provide-justification-for-my-approval/rejection) 

**身為合格角色使用者，您可以：**

-   [要求啟用需要核准的角色](#request-activation-of-a-role-that-requires-approval)

-   [檢視要求 tooactivate hello 狀態](#view-the-status-of-your-request-to-activate)

-   [如果已核准啟用，在 Azure AD 中完成您的工作](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>導覽

我們已更新 hello 瀏覽 toosupport 核准

![](media/azure-ad-pim-approval-workflow/image001.png)

hello 預設登陸頁面會提供方便的方式存取 tooinformation 有關 PIM 和 hello 新核准文件。

![](media/azure-ad-pim-approval-workflow/image002.png)

我們也針對 PIM [我的稽核歷程記錄] 的所有使用者新增了新的區段。 您可以在這裡找到所有 hello 資訊相關 tooyour 身分識別。 這包括所有擱置中和已完成要求，任何有關 hello 要求您解決時，所做的決策和您過去的角色啟用在一個方便的位置。

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>啟用特定角色的核准

tooenable 核准對於特定的角色，請先選取從 hello 左方瀏覽的目錄角色。

![](media/azure-ad-pim-approval-workflow/image004.png)

尋找並選取 hello 左側瀏覽目錄角色中的設定

![](media/azure-ad-pim-approval-workflow/image006.png)

選取 [特殊權限角色]：

![](media/azure-ad-pim-approval-workflow/image009.png)

選取 [啟用] 在 hello 需要核准章節：

![](media/azure-ad-pim-approval-workflow/image011.png)

一旦啟用，hello 刀鋒視窗會展開 tooshow hello 下列詳細資料：

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
如果您不指定任何核准者，hello PRA(s) 變成 hello 預設核准者。 PRA(s) 就是所有的啟用要求此角色的必要的 tooapprove。

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>指定核准者 tooapprove 要求使用者和/或群組

toodelegate 核准按一下 hello 選項太 「 選取核准者 」:

![](media/azure-ad-pim-approval-workflow/image015.png)

刀鋒視窗中選取的核准者 hello 載入時，您可能會搜尋特定使用者或群組使用 hello 搜尋列 hello 上方，或從 hello 預先填入的清單中選取，然後按一下 「 選取 」 完成時：

![](media/azure-ad-pim-approval-workflow/image017.png)

注意︰您可以同時選取多個使用者或群組。

您的選擇會顯示在選取的核准者的 hello 清單中，如下所示：

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove 核准者，只要按一下 hello 移除按鈕下一步 tootheir 的名稱。

tooadd 其他核准者，重複 hello 程序。

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>檢視所有特殊權限角色的要求和核准歷程記錄

對於所有特殊權限的角色，tooview 要求和核准歷程記錄選取稽核歷程從 hello 儀表板：

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
您可以 hello 依排序資料的動作，並尋找"Approved 啟用"

### <a name="view-pending-approvals-requests"></a>檢視待決的核准 (要求)

身為委派核准者，當要求正在等待您的核准時，您將會收到電子郵件通知。 tooview hello PIM 入口網站，從 hello （在 hello 新的瀏覽） 的儀表板選取 hello 「 暫止核准要求 」 索引標籤中的這些要求左導覽列。

![](media/azure-ad-pim-approval-workflow/image023.png)

您將在該處看到一份等待核准的要求清單：

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>核准或拒絕提高角色權限 (單一和/或大量) 的要求

選取您想 tooapprove 或拒絕的 hello 要求，再按一下對應於您的決定動作列中的 hello 按鈕：

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>提供我的核准/拒絕理由

這將會開啟新的刀鋒視窗 tooapprove 或拒絕多個要求一次。 輸入您的決策，讓您的理由，並按一下核准 （或拒絕） 在 hello 底部或 hello 刀鋒視窗中：

![](media/azure-ad-pim-approval-workflow/image029.png)

Hello 狀態符號 hello 要求程序完成時，會反映您所做的決定 （在此範例中，hello 決策是核准）：

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>要求啟用需要核准的角色

要求需要核准，可能會起始從 hello 舊 PIM 瀏覽或 hello 新瀏覽角色的啟用，為 hello 程序會維持為角色啟動 hello 相同。 從 hello 要啟動之角色的清單，只需選取角色：

![](media/azure-ad-pim-approval-workflow/image033.png)

如果特殊權限角色需要 Multi-Factor Authentication，系統將提示您先完成該工作：

![](media/azure-ad-pim-approval-workflow/image035.png)

完成之後，按一下 [啟用] 並提供理由 (如有必要)：

![](media/azure-ad-pim-approval-workflow/image037.png)

hello 要求者會看到通知，hello 要求正在等待核准：

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>檢視連線的要求 tooactivate hello 狀態

從新的瀏覽必須存取檢視的暫止要求 tooactivate hello 狀態。 從 hello 左的導覽列中，選取 hello 「 我的要求 」 索引標籤：

![](media/azure-ad-pim-approval-workflow/image041.png)

hello 要求狀態太預設 「 擱置 」，但您可以切換所有 toosee 或拒絕要求。

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>如果已核准啟用，在 Azure AD 中完成您的工作

Hello 要求獲得核准後，一旦 hello 角色作用中，您就可以進行任何需要的工作，此角色。

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>後續步驟

您的意見反應會很有價值 toous。 請隨時可用 tooshare 註解或意見反應與我們這裡 ！
