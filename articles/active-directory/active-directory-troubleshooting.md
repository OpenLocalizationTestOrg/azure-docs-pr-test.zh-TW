---
title: "疑難排解: 'Active Directory' 項目已遺失或無法使用 |Microsoft 文件"
description: "哪些 toodo 當 Active Directory 功能表項目不會出現在 hello Azure 管理入口網站。"
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>疑難排解：'Active Directory' 項目遺失或無法使用
許多使用 Azure Active Directory 功能和服務的指示 hello 開頭為 「 移 toohello Azure 管理入口網站，然後按一下**Active Directory**。 」 但該怎麼辦如果 hello Active Directory 延伸模組或功能表項目沒有出現，或其標記為**無法使用**嗎？ 本主題是設計的 toohelp。 它描述 hello 條件**Active Directory**不會出現或無法使用，並說明如何 tooproceed。

## <a name="active-directory-is-missing"></a>Active Directory 遺失
一般而言， **Active Directory** hello 左的導覽功能表中的項目隨即出現。 Azure Active Directory 程序中的 hello 指示會假設此項目是在檢視中。

![螢幕擷取畫面：Azure 中的 Active Directory](./media/active-directory-troubleshooting/typical-view.png)

若任何 hello 下列條件為真，hello Active Directory 項目會出現在 hello 左的導覽功能表。 否則，未顯示 hello 項目。

* hello 以 Microsoft 帳戶 （先前稱為 Windows Live ID） 登入目前的使用者。
  
    或
* hello Azure 租用戶具有目錄，而 hello 目前帳戶為目錄管理員。
  
    或
* hello Azure 租用戶具有至少一個 Azure AD 存取控制 (ACS) 命名空間。 如需詳細資訊，請參閱 [存取控制命名空間](https://msdn.microsoft.com/library/azure/gg185908.aspx)。
  
    或
* hello Azure 租用戶具有至少一個 Azure Multi-factor Authentication 提供者。 如需詳細資訊，請參閱 [管理 Azure Multi-Factor Authentication 提供者](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。

toocreate 存取控制命名空間或為多因素驗證提供者中，按一下**+ 新增** > **應用程式服務** > **Active Directory**.

tooget 系統管理權限 tooa 目錄中，有系統管理員指派系統管理員角色 tooyour 帳戶。 如需詳細資訊，請參閱 [指派系統管理員角色](active-directory-assign-admin-roles.md)。

## <a name="active-directory-is-not-available"></a>Active Directory 無法使用
當您按一下 [+新增]  >  [應用程式服務] 時，[Active Directory] 項目即會出現。 具體而言，當任何 hello Active Directory 功能，例如目錄、 存取控制或 Multi-factor Auth 提供者，可以使用 toohello 目前的使用者，就會出現 hello Active Directory 項目。

不過，雖然 hello 頁面載入時，hello 項目會呈暗灰色且標示**無法使用**。 這是暫時性狀態。 如果您需要等候幾秒鐘的時間，hello 項目會變成可用。 如果 hello 延遲太久，重新整理 hello 網頁通常會解決 hello 問題。

![螢幕擷取畫面：Active Directory 無法使用](./media/active-directory-troubleshooting/not-available.png)

