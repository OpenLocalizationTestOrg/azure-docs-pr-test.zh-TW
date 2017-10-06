---
title: "使用自助式應用程式存取 aaaProblem |Microsoft 文件"
description: "疑難排解問題相關的 tooself 服務應用程式存取"
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
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a>使用自助應用程式存取時遇到問題

自助應用程式的存取是很好的方法 tooallow 使用者 tooself-探索應用程式，請選擇性地允許 hello 商務群組 tooapprove 存取 toothose 應用程式。 您可以允許 hello 商務群組 toomanage hello 認證指派 toothose 使用者從他們的存取面板的密碼單一登入應用程式權限。

您的使用者可以自行探索從他們的存取面板應用程式之前，您需要 tooenable**自助式應用程式存取**tooany 應用程式，您會希望 tooallow 使用者 tooself-探索及要求的存取權。

## <a name="general-issues-toocheck-first"></a>一般會先發出 toocheck

-   請確定已正確設定自助應用程式存取。 請參閱 「 如何 tooconfigure 自助應用程式存取 」。

-   請確定 hello 使用者或群組已啟用 toorequest 自助式應用程式存取。

-   請確定 hello 使用者造訪 hello 自助應用程式存取正確的位置。 使用者可瀏覽 tootheir[應用程式存取面板](https://myapps.microsoft.com/)按一下 hello **+ 加**按鈕 toofind hello 應用程式 toowhich 您已啟用自助存取。

-   如果最近已設定自助應用程式的存取，toosign 入和登出再試一次到 hello 使用者的存取面板後幾分鐘的時間 toosee 如果 hello 自助存取變更已出現。

## <a name="how-tooconfigure-self-service-application-access"></a>Tooconfigure 自助應用程式的存取方式

tooenable 自助應用程式存取 tooan 應用程式，下列的後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想要 tooenable 自助存取 toofrom hello 清單 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **自助**從 hello 應用程式的左導覽功能表。

8.  tooenable 自助式應用程式存取此應用程式中，開啟 hello**允許使用者應用程式的存取 toothis toorequest？**太切換**[是]。**

9.  Tooselect hello 群組 toowhich 要求使用者應加入 toothis 應用程式的存取，接下來，按一下 hello 選取器下一個 toohello 標籤**toowhich 群組應該指派給新增的使用者？**並選取一個群組。

10. **選擇性：**如果您想 toorequire 商務核准允許使用者存取之前，設定 hello**之前授與存取 toothis 應用程式需要核准？**太切換**是**。

11. **選用： 為應用程式上，使用密碼單一登**如果您想 tooallow toothis 應用程式的核准的使用者傳送這些商務核准者 toospecify hello 密碼時，設定 hello**允許核准者 tooset此應用程式的使用者的密碼嗎？**太切換**是**。

12. **選擇性：** toospecify hello 公司核准者允許 tooapprove 存取 toothis 應用程式中，按一下 hello 選取器下一個 toohello 標籤**誰 tooapprove 存取 toothis 應用程式？** tooselect 向上too10 個別商務核准者。

 >[!NOTE]
 > 不支援群組。
 >
 >

13. **選擇性：** **的應用程式的公開角色**，如果您想 tooa tooassign 自助核准的使用者的角色，按一下 下一步 toohello 的 hello 選取器**toowhich 角色應該指派給使用者在此應用程式嗎？** tooselect hello 角色 toowhich 應該指派這些使用者。

14. 按一下 hello**儲存**在 hello 刀鋒視窗 toofinish hello 最上方的按鈕。

一旦您完成自助應用程式組態設定，使用者可以瀏覽 tootheir[應用程式存取面板](https://myapps.microsoft.com/)按一下 hello **+ 加**按鈕 toofind hello 應用程式 toowhich 已啟用自助存取。 商務核准者在其[應用程式存取面板](https://myapps.microsoft.com/)中也會看到通知。 您可以啟用在使用者要求存取 tooan 應用程式需要核准時，通知他們的電子郵件。 

這些核准支援單一核准工作流程，這表示如果您指定多個核准者，任何單一核准者可能會核准存取 toohello 應用程式。

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>如果這些疑難排解步驟無法解決 hello 問題 

開啟支援票證以 hello 如果有的話，下列資訊：

-   相互關聯錯誤 ID

-   UPN (使用者電子郵件地址)

-   TenantID

-   瀏覽器類型

-   錯誤發生期間的時區和時間/時間範圍

-   Fiddler 追蹤

## <a name="next-steps"></a>後續步驟
[設定 Azure Active Directory 進行自助服務群組管理](active-directory-accessmanagement-self-service-group-management.md)
