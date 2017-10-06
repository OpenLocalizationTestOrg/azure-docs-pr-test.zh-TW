---
title: "開始使用 Azure AD Privileged Identity Management 的 aaaGet |Microsoft 文件"
description: "了解如何 toomanage 特殊權限身分識別與 Azure 入口網站中的 hello Azure Active Directory Privileged Identity Management 應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>開始使用 Azure AD Privileged Identity Management
您可以利用 Azure Active Directory (AD) Privileged Identity Management 來管理、控制和監視組織內的存取行為。 此範圍包括存取 tooresources 在 Azure AD 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。

這篇文章會告訴您如何 tooadd hello Azure AD PIM 應用程式 tooyour Azure 入口網站的儀表板。

## <a name="add-hello-privileged-identity-management-application"></a>新增 hello Privileged Identity Management 的應用程式
使用 Azure AD Privileged Identity Management 之前，您會需要 tooadd hello 應用程式 tooyour Azure 入口網站的儀表板。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)您目錄的全域管理員身分。
2. 如果您的組織具有多個目錄，選取您的使用者名稱 hello 右上角的 hello Azure 入口網站。 選取您希望 toouse PIM hello 目錄。
3. 選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。
4. 請檢查**Pin toodashboard** ，然後按一下 [**建立**。 hello Privileged Identity Management 的應用程式會開啟。

如果您正在 hello 第一個人 toouse Azure AD Privileged Identity Management 目錄中，您會自動指派給 hello**安全性系統管理員**和**特殊權限的角色管理員**角色在 [hello 目錄。 只有特殊權限角色管理員才能管理使用者的角色指派。 此外，您可以選擇 toorun hello[安全性精靈 」。](active-directory-privileged-identity-management-security-wizard.md) 會引導您經由 hello 初始探索與指派體驗。

## <a name="navigate-tooyour-tasks"></a>瀏覽 tooyour 工作
一旦設定 Azure AD Privileged Identity Management 之後，每當您開啟 hello 應用程式時看到 hello 瀏覽] 刀鋒視窗。 使用此刀鋒視窗 tooaccomplish 身分識別管理工作。

![PIM 的最上層工作 - 螢幕擷取畫面](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **我角色**會帶您角色指派 tooyou tooa 清單。 您可以在此區段中啟動任何您具備資格的角色。
* **核准要求 (預覽)** 會顯示目錄中來自使用者的擱置啟用要求清單。 [深入了解。](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **擱置的要求 （預覽）**會顯示任何目前的要求進行 toohave tooactivate。
* **檢閱存取**採用 tooany 暫止的存取會檢閱您需要 toocomplete，是否在檢閱您自己或其他人的存取。
* **Azure AD 目錄角色**位於 hello '管理' 區段是特殊權限的角色 admins toomanage 角色指派、 變更角色的啟用設定、 開始存取檢閱等等 hello 儀表板。 此儀表板中的 hello 選項會停用不是特殊權限的角色系統管理員的人。

## <a name="next-steps"></a>後續步驟
hello [Azure AD Privileged Identity Management 概觀](active-directory-privileged-identity-management-configure.md)包含上如何管理系統管理存取權，以及在組織中的更多詳細資料。

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
