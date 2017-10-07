---
title: "hello Azure Active Directory 入口網站中的 aaaSign 入活動報表 |Microsoft 文件"
description: "在 hello Azure Active Directory 入口網站的簡介 toosign 中活動報告"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory 入口網站中的登入活動報表

使用 Azure Active Directory (Azure AD) 報告 hello [Azure 入口網站](https://portal.azure.com)，您可以取得需要您的環境執行的方式 toodetermine hello 資訊。

hello Azure Active Directory 中的報表架構包含下列元件的 hello:

- **活動** 
    - **登入活動**– hello 使用量資訊的受管理的應用程式和使用者登入活動
    - **稽核記錄** - 關於使用者和群組管理、受管理應用程式和目錄活動的系統活動資訊。
- **安全性** 
    - **高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。 如需詳細資訊，請參閱＜有風險的登入＞。
    - **標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。 如需詳細資訊，請參閱＜標幟為有風險的使用者＞。

本主題提供 hello 登入活動的概觀。

## <a name="pre-requisite"></a>必要條件

### <a name="who-can-access-hello-data"></a>誰可以存取 hello 資料？
* Hello 安全性系統管理員或安全性 Reader 角色中的使用者
* 全域管理員
* 任何使用者 (非系統管理員) 都可以存取自己的登入 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>Azure AD 授權您需要 tooaccess 登入活動嗎？
* 您的租用戶必須有與其相關聯的 Azure AD Premium 授權 toosee hello 所有最多登入活動報表


## <a name="signs-in-activities"></a>登入活動

Hello hello 使用者登入報表所提供的資訊，您可以找到解答 tooquestions，例如：

* Hello 登入使用者的模式是什麼？
* 一週內有多少使用者登入？
* 這些登入的 hello 狀態為何？

第一個項目點 tooall 登入活動資料**登入**hello 活動一節中**Azure Active**。


![登入活動](./media/active-directory-reporting-activity-sign-ins/61.png "登入活動")


稽核記錄的預設清單檢視顯示︰

- hello 相關的使用者
- hello 應用程式 hello 使用者已登入
- hello 登入狀態
- hello 登入時間

![登入活動](./media/active-directory-reporting-activity-sign-ins/41.png "登入活動")

您可以自訂 hello 清單檢視中，依序按一下**資料行**hello 工具列中。

![登入活動](./media/active-directory-reporting-activity-sign-ins/19.png "登入活動")

這可讓您 toodisplay 其他欄位，或移除已顯示的欄位。

![登入活動](./media/active-directory-reporting-activity-sign-ins/42.png "登入活動")

依序按一下 hello 清單檢視中的項目，您會取得所有可用的詳細資訊。

![登入活動](./media/active-directory-reporting-activity-sign-ins/43.png "登入活動")


## <a name="filtering-sign-in-activities"></a>篩選登入活動

關閉 hello toonarrow 報告資料 tooa 層級，適用於您，您可以篩選 hello 登入資料使用 hello 下列欄位：

- 時間間隔
- User
- 應用程式
- 用戶端
- 登入狀態

![登入活動](./media/active-directory-reporting-activity-sign-ins/44.png "登入活動")


hello**時間間隔**篩選器可讓 tooyou toodefine hello 的時間範圍內傳回的資料。  
可能的值包括：

- 1 個月
- 7 天
- 24 小時
- 自訂

當您選取自訂時間範圍時，可以設定開始時間和結束時間。

hello**使用者**篩選器可讓您 toospecify hello 名稱或 hello 使用者主體名稱 (UPN) 您關心的 hello 使用者。

hello**應用程式**篩選器可讓您 toospecify hello 您關心的 hello 應用程式名稱。

hello**用戶端**篩選器可讓您 toospecify hello 裝置，您很重視的資訊。

hello**登入狀態**篩選器可讓您的下列篩選器的 hello tooselect 其中一個：

- 全部
- 成功
- 失敗


## <a name="sign-in-activities-shortcuts"></a>登入活動捷徑

此外 tooAzure Active Directory，hello Azure 入口網站為您提供兩個其他的進入點 toosign 中活動資料：

- 使用者和群組
- 企業應用程式


### <a name="users-and-groups-sign-ins-activities"></a>使用者和群組登入活動

Hello hello 使用者登入報表所提供的資訊，您可以找到解答 tooquestions，例如：

- Hello 登入使用者的模式是什麼？
- 一週內有多少使用者登入？
- 這些登入的 hello 狀態為何？



您的進入點 toothis 資料是 hello 使用者登入在 hello 圖形**概觀**區段**使用者和群組**。

![登入活動](./media/active-directory-reporting-activity-sign-ins/45.png "登入活動")

hello 使用者登入圖表會顯示每週彙總的符號集在給定的時間週期內的所有使用者。 hello 的 hello 預設期間為 30 天。

![登入活動](./media/active-directory-reporting-activity-sign-ins/46.png "登入活動")

當您按一下 hello 登入圖形中的哪一天時，您會取得這一天的 hello 登入活動的詳細的清單。

![登入活動](./media/active-directory-reporting-activity-sign-ins/41.png "登入活動")

每個資料列 hello 登入活動的清單提供 hello hello 選取登入如需詳細的資訊：

* 誰已登入？
* 什麼是 hello 相關 UPN 嗎？
* 哪些應用程式的 hello hello 登入的目標？
* 什麼是 hello hello 登入的 IP 位址？
* Hello hello 登入的狀態是什麼？

hello**登入**選項可讓您所有的使用者登入的完整概觀。

![登入活動](./media/active-directory-reporting-activity-sign-ins/51.png "登入活動")



## <a name="usage-of-managed-applications"></a>受管理應用程式的使用情況

利用登入資料以應用程式為主的檢視，您可以回答下列問題︰

* 誰在使用我的應用程式？
* Hello 前 3 的應用程式在組織中有哪些？
* 我最近已推出一個應用程式。 它的情況為何？

是 hello 前 3 的應用程式在 hello hello 過去 30 天內報表內組織中的項目點 toothis 資料**概觀**區段**企業應用程式**。

![登入活動](./media/active-directory-reporting-activity-sign-ins/64.png "登入活動")

hello 應用程式使用量圖形每週的彙總的前 3 名應用程式在指定的時段內登入。 hello 的 hello 預設期間為 30 天。

![登入活動](./media/active-directory-reporting-activity-sign-ins/47.png "登入活動")

如果您想要您可以設定特定的應用程式的 hello 焦點。


![報告](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "報告")

當您按一下 hello 應用程式使用量圖表中的哪一天時，您會取得 hello 登入活動的詳細的清單。


![登入活動](./media/active-directory-reporting-activity-sign-ins/48.png "登入活動")


hello**登入**選項可讓您所有的登入事件 tooyour 應用程式的完整概觀。

![登入活動](./media/active-directory-reporting-activity-sign-ins/49.png "登入活動")



## <a name="next-steps"></a>後續步驟

如果您想深入了解登入活動錯誤碼 tooknow，請參閱 hello[登入活動報表中的錯誤碼 hello Azure Active Directory 網站](active-directory-reporting-activity-sign-ins-errors.md)。

