---
title: "Azure AD Connect 同步： 變更 hello AD DS 帳戶密碼 |Microsoft 文件"
description: "此主題說明如何變更 tooupdate 之後 hello hello AD DS 帳戶密碼的 Azure AD Connect。"
services: active-directory
keywords: "AD DS 帳戶, Active Directory 帳戶, 密碼"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>變更 hello AD DS 帳戶的密碼
hello AD DS 帳戶指的是使用內部部署 Active Directory 與 Azure AD Connect toocommunicate toohello 使用者帳戶。 如果您變更 hello 的 hello AD DS 帳戶的密碼，您必須更新 Azure AD Connect 同步處理服務與 hello 新密碼。 否則，同步處理可以不再正確同步處理以 hello hello 內部部署 Active Directory，您將會遇到下列錯誤 hello:

* 在 hello 與同步處理服務管理員、 匯入或匯出作業在內部部署 AD 失敗，並**無開始認證**錯誤。

* 在 Windows 事件檢視器，hello 應用程式事件記錄檔包含與錯誤**事件識別碼 6000**和訊息**'hello 管理代理程式"contoso.com"hello 認證無效，因為無法 toorun'**.


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>如何 tooupdate hello 與 AD DS 帳戶的新密碼的同步處理服務
使用新密碼的 hello tooupdate hello 同步服務：

1. 啟動 hello Synchronization Service Manager （開始 → 同步處理服務）。
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. 移 toohello**連接器** 索引標籤。

3. 選取 hello **AD 連接器**對應已變更其密碼的 toohello AD DS 帳戶。

4. 選取 [動作] 下方的 [屬性]。

5. 在 hello 快顯對話方塊中，選取 **連接 tooActive Directory 樹系**:

6. 輸入 hello hello hello AD DS 帳戶新密碼**密碼**文字方塊。

7. 按一下**確定**toosave hello 新密碼] 和 [關閉 hello 快顯對話方塊。

8. 重新啟動 hello Azure AD Connect 同步處理服務在 Windows 服務控制管理員。 這是 tooensure hello 記憶體快取中已移除任何參照 toohello 舊密碼。

## <a name="next-steps"></a>後續步驟
**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)

* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
