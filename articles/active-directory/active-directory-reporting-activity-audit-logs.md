---
title: "aaaAudit 活動報告會在 hello Azure Active Directory 入口網站 |Microsoft 文件"
description: "簡介 toohello 稽核 hello Azure Active Directory 入口網站中的活動報告"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>稽核 hello Azure Active Directory 入口網站中的活動報告 

您可以使用 Azure Active Directory (Azure AD) 中的報表，取得您需要您的環境執行的方式 toodetermine hello 資訊。

hello Azure AD 中的報表架構包含下列元件的 hello:

- **活動** 
    - **登入活動**– hello 使用量資訊的受管理的應用程式和使用者登入活動
    - **稽核記錄** - 關於使用者和群組管理、受管理應用程式和目錄活動的系統活動資訊。
- **安全性** 
    - **高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。 如需詳細資訊，請參閱＜有風險的登入＞。
    - **標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。 如需詳細資訊，請參閱＜標幟為有風險的使用者＞。

本主題提供 hello 稽核活動的概觀。
 
## <a name="who-can-access-hello-data"></a>誰可以存取 hello 資料？
* Hello 安全性系統管理員或安全性 Reader 角色中的使用者
* 全域管理員
* 個別使用者 (非系統管理員) 可以看到自己的活動


## <a name="audit-logs"></a>稽核記錄檔

Azure Active Directory 中的 hello 稽核記錄檔提供的相容性的系統活動記錄。  
稽核資料您第一個項目點 tooall 是**稽核記錄檔**在 hello**活動**區段**Azure Active Directory**。

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/61.png "稽核記錄")

稽核記錄的預設清單檢視顯示︰

- hello 日期和時間 hello 出現項目
- hello 啟動器 / 動作項目 (*人員*) 的活動 
- hello 活動 (*什麼*) 
- hello 目標

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/18.png "稽核記錄")

您可以自訂 hello 清單檢視中，依序按一下**資料行**hello 工具列中。

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/19.png "稽核記錄")

這可讓您 toodisplay 其他欄位，或移除已顯示的欄位。

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/21.png "稽核記錄")


依序按一下 hello 清單檢視中的項目，您會取得所有可用的詳細資訊。

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/22.png "稽核記錄")


## <a name="filtering-audit-logs"></a>篩選稽核記錄檔

向下 hello toonarrow 報告資料 tooa 層級，適用於您，您可以篩選 hello 稽核資料，使用下列欄位的 hello:

- 日期範圍
- 啟動者 (執行者)
- 類別
- 活動資源類型
- 活動

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/23.png "稽核記錄")


hello**日期範圍**篩選器可讓 tooyou toodefine hello 的時間範圍內傳回的資料。  
可能的值包括：

- 1 個月
- 7 天
- 24 小時
- 自訂

當您選取自訂時間範圍時，可以設定開始時間和結束時間。

hello**由起始**篩選器可讓您 toodefine 演員姓名或其通用主要名稱 (UPN)。

hello**類別**篩選器可讓您的下列篩選器的 hello tooselect 其中一個：

- 全部
- 核心類別
- 核心目錄
- 自助式密碼管理
- 自助式群組管理
- 帳戶佈建 - 自動密碼變換
- 受邀的使用者
- MIM 服務
- 身分識別保護
- B2C

hello**活動資源類型**篩選器可讓您 tooselect hello 下列其中一種篩選：

- 全部 
- 群組
- 目錄
- User
- 應用程式
- 原則
- 裝置
- 其他

當您選取**群組**為**活動資源類型**，tooalso 取得額外的篩選條件分類，可讓您提供**來源**:

- Azure AD
- O365


hello**活動**篩選根據 hello 類別和活動資源類型進行的選取項目。 您可以選取您想要 toosee 或選擇所有的特定活動。 

您可以取得所有的稽核活動 hello 清單使用 auditActivityTypes/tenantdomain/活動 hello Graph API https://graph.windows.net/$？ api 版本 = beta，其中 $tenantdomain = 網域名稱，或參閱 toohello 文章[稽核報告事件](active-directory-reporting-audit-events.md)。


## <a name="audit-logs-shortcuts"></a>稽核記錄快速鍵

此外太**Azure Active Directory**，hello Azure 入口網站為您提供兩個其他的進入點 tooaudit 資料：

- 使用者和群組
- 企業應用程式

### <a name="users-and-groups-audit-logs"></a>使用者和群組稽核記錄檔

與使用者和群組為基礎的稽核報表，您可以取得答案 tooquestions，例如：

- 哪些類型的更新已套用的 hello 使用者？

- 有多少使用者已變更？

- 有多少密碼已變更？

- 系統管理員已在目錄中執行哪些作業？

- 已加入的 hello 群組有哪些？

- 群組有成員資格變更嗎？

- 已變更群組的 hello 擁有者嗎？

- Tooa 群組或使用者已指派給哪些授權？

如果您只想 tooreview 稽核相關的 toousers 和群組的資料，您可以找到篩選過的檢視之下**稽核記錄檔**在 hello**活動**區段 hello**使用者和群組**. 此進入點將 [使用者和群組] 作為預先選取的 [活動資源類型]。

![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/93.png "稽核記錄檔")

### <a name="enterprise-applications-audit-logs"></a>企業應用程式稽核記錄

與應用程式為基礎的稽核報告，您可以取得答案 tooquestions，例如：

* 已新增或更新的 hello 應用程式有哪些？
* 已移除的 hello 應用程式有哪些？
* 應用程式的服務原則已變更嗎？
* Hello 應用程式名稱已經變更？
* 使用者提供同意 tooan 應用程式？

如果您只想 tooreview 稽核相關的 tooyour 應用程式的資料，您可以找到篩選過的檢視之下**稽核記錄檔**在 hello**活動**區段 hello**企業應用程式**刀鋒視窗。 此進入點將 [企業應用程式] 當作預先選取的 [活動資源類型]。

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/134.png "稽核記錄")

您可以篩選此檢視進一步向下 toojust**群組**或簡稱**使用者**。

![稽核記錄](./media/active-directory-reporting-activity-audit-logs/25.png "稽核記錄")


## <a name="next-steps"></a>後續步驟

如需報告的概觀，請參閱 hello [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。

