---
title: "安裝 hello 應用程式存取面板瀏覽器延伸模組的 aaaProblem |Microsoft 文件"
description: "安裝 hello 存取面板瀏覽器延伸模組時，toofix 常見錯誤如何發生"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>安裝 hello 應用程式存取面板瀏覽器延伸模組的問題

hello 存取面板是網頁型入口網站讓使用者具有工作或學校帳戶在 Azure Active Directory (Azure AD) tooview 並啟動雲端型應用程式中的 hello Azure AD 系統管理員已被授與存取權。 自助式群組並透過 hello 存取面板應用程式管理功能，也可以使用具有 Azure AD 版本的使用者。 hello 存取面板是分開 hello Azure 入口網站，而且不需要使用者 toohave Azure 訂用帳戶。

toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。 當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>會議 hello 存取面板 的瀏覽器需求

存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。 toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。 當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。

針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：

-   Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上

-   Windows 10 Anniversary Edition 或更新版本上的 Edge 

-   Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上

-   Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>如何 tooinstall hello 存取面板瀏覽器延伸模組

tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：

1.  開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。

2.  按一下**password SSO 應用程式**hello 存取面板中。

3.  在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。

4.  根據您的瀏覽器就導向的 toohello 下載連結。 **新增**hello 延伸 tooyour 瀏覽器。

5.  如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。

6.  安裝之後，**重新啟動**瀏覽器工作階段。

7.  到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式

您可能也 hello 從下載擴充功能的 Chrome 和邊緣 hello 以下的直接連結：

-   [Chrome 存取面板延伸模組](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Edge 存取面板延伸模組](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>設定適用於 Internet Explorer 的群組原則

您可以設定群組原則可讓您 tooremotely 安裝 hello 存取面板延伸模組的 Internet Explorer 上使用者的機器。

hello 的先決條件包括：

-   您已設定[Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，及您已加入您的使用者機器 tooyour 網域。

-   您必須擁有 hello [編輯設定] 的權限 tooedit hello 群組原則物件 (GPO)。 根據預設，hello 下列安全性群組的成員擁有此權限： 網域系統管理員、 企業系統管理員和 Group Policy Creator Owners。 [深入了解](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。

請遵循 hello 教學課程[如何 tooDeploy hello 存取面板延伸模組使用群組原則設定 Internet Explorer](active-directory-saas-ie-group-policy.md)如需有關如何 tooconfigure hello 群組原則，並將其部署 toousers 的逐步指示。

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>疑難排解 hello Internet Explorer 中的 存取面板

請遵循 hello[疑難排解 hello Internet explorer 的 存取面板延伸模組](active-directory-saas-ie-troubleshooting.md)引導存取診斷工具和逐步指示在 ie 設定 hello 延伸模組。

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>如果這些疑難排解步驟無法解決 hello 問題

開啟支援票證以 hello 如果有的話，下列資訊：

-   相互關聯錯誤 ID

-   UPN (使用者電子郵件地址)

-   TenantID

-   瀏覽器類型

-   錯誤發生期間的時區和時間/時間範圍

-   Fiddler 追蹤

## <a name="next-steps"></a>後續步驟
[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
