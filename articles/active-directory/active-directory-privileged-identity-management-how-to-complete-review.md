---
title: "aaaHow toocomplete 存取檢閱 |Microsoft 文件"
description: "您在 Azure AD Privileged Identity Management 啟動存取檢閱後，了解如何 toocomplete 它並檢視 hello 結果"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>如何 toocomplete 存取檢閱在 Azure AD Privileged Identity Management
在 [開始安全性檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)之後，特殊權限角色管理員就可以檢閱特殊權限存取權。 Azure AD Privileged Identity Management (PIM) 將會自動傳送電子郵件提示使用者 tooreview 其存取權。 如果使用者未取得電子郵件，您可以傳送 hello 說明[如何 tooperform 安全性檢閱](active-directory-privileged-identity-management-how-to-perform-security-review.md)。

Hello 安全性檢閱時間已經結束，或 hello 的所有使用者都完成其自我檢閱之後，請遵循在這個發行項 toomanage hello 檢閱中的 hello 步驟，並查看 hello 結果。

## <a name="manage-security-reviews"></a>管理安全性檢閱
1. 移 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello **Azure AD Privileged Identity Management**儀表板上的應用程式。
2. 選取 hello**存取檢閱**hello 儀表板的區段。
3. 選取您想 toomanage hello 存取檢閱。

Hello 存取檢閱的詳細資料 刀鋒視窗中，有數字的選項，來管理該檢閱。

![PIM 存取權檢閱按鈕 - 螢幕擷取畫面][1]

### <a name="remind"></a>提醒
如果設定存取檢閱使 hello 使用者檢閱本身，hello**提醒**按鈕送出通知。 

### <a name="stop"></a>停止
所有存取檢閱都有結束日期，但是您可以使用 hello**停止**按鈕 toofinish 早期它。 如果尚未經過這次檢閱任何使用者，他們不是能 tooafter 停止 hello 檢閱。 在停止檢閱之後，即無法重新開始該檢閱。

### <a name="apply"></a>套用
存取檢閱已完成之後，是因為您達到 hello 結束日期，或手動停止它 hello**套用**按鈕實作 hello hello 檢閱結果。 如果使用者的存取被拒 hello 檢閱中，這會是 hello 步驟，將會移除其角色指派。  

### <a name="export"></a>匯出
若要手動 tooapply hello hello 安全性檢閱結果，您可以匯出 hello 檢閱。 hello**匯出**按鈕開始下載 CSV 檔案。 您可以管理在 Excel 或其他程式，開啟 CSV 檔案中的 hello 結果。

### <a name="delete"></a>刪除
如果您不感興趣 hello 進一步檢閱任何，將它刪除。 hello**刪除**按鈕會移除 hello PIM 應用程式中的 hello 檢閱。

> [!IMPORTANT]
> 您不會收到警告，就會刪除之前，因此請確定您想要檢閱的 toodelete。 

## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
