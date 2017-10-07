---
title: "aaaUsers 標示風險安全性報告 hello Azure Active Directory 入口網站中為 |Microsoft 文件"
description: "深入了解 hello 使用者標示為在 hello Azure Active Directory 入口網站的風險安全性報告"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>標示為進行風險安全性報告 hello Azure Active Directory 入口網站中的使用者

與 hello Azure Active Directory (Azure AD) 中的 hello 安全性報表，您可以深入了 hello 機率盜用的使用者帳戶，您的環境中。 

Azure Active Directory 偵測到可疑相關的 tooyour 使用者帳戶的動作。 針對每個偵測到的動作，將會建立一筆稱為「風險事件」的記錄。 如需詳細資訊，請參閱 [Azure Active Directory 風險事件](active-directory-identity-protection-risk-events.md)。 

hello 偵測到有使用的 toocalculate 風險事件：

- **高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。 如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。 

- **標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。 如需詳細資訊，請參閱[標幟為有風險的使用者](active-directory-identityprotection.md#users-flagged-for-risk)。  

在 hello Azure 入口網站，您可以找到 hello 安全性報告 hello **Azure Active Directory**刀鋒視窗中 hello**安全性**> 一節。  

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Azure AD 授權您需要 tooaccess 安全性報表嗎？  

所有 Azure Active Directory 版本都會為您提供標幟為有風險的使用者報告。  
不過，報表資料粒度層級 hello hello 版本而異： 

- 在 hello **Azure Active Directory Free 和 Basic 版本**，您已取得使用者針對風險加上旗標的清單。 

- hello **Azure Active Directory Premium 1**版本擴充這個模型也啟用 tooexamine hello 已偵測到每個報表的風險事件的基礎部分。 

- hello **Azure Active Directory Premium 2**版本會提供您與 hello 所有基礎的風險事件的最詳細的資訊，並可讓您 tooconfigure 自動回應 tooconfigured 風險的安全性原則層級。



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory 免費和基本版本

hello 風險 hello Azure Active Directory free 和 basic 版本的報表加上旗標的使用者提供您可能已受到危害的使用者帳戶的清單。 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/03.png)

選取使用者開啟 hello 相關的使用者資料刀鋒視窗。
針對有風險的使用者，您可以檢閱 hello 使用者的登入歷程記錄，並且如有必要，請重設 hello 密碼。

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/46.png)


此對話方塊會提供選項以便：

- 下載 hello 報表

- 搜尋使用者

![有風險的登入](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory Premium Edition

hello hello Azure Active Directory premium edition 中，風險報表加上旗標的使用者提供讓您：

- 可能已遭盜用的[使用者帳戶清單](active-directory-identityprotection.md#users-flagged-for-risk) 

- 彙總資訊 hello[風險事件類型](active-directory-identity-protection-risk-events.md)偵測到的

- 選項 toodownload hello 報表

- 選項 tooconfigure[使用者風險補救原則](active-directory-identityprotection.md#user-risk-security-policy)  


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/71.png)

當您選取使用者時，即會取得這位使用者的詳細報告檢視，讓您能夠：

- 開啟 檢視所有登入的 hello

- 重設 hello 使用者密碼

- 關閉所有事件

- 調查 hello 使用者報告的風險事件。 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate 風險事件，從選取一個 hello 清單 tooopen hello**詳細資料**這個風險事件刀鋒視窗。 在 hello**詳細資料**刀鋒視窗中，您已擁有 hello 選項 tooeither[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)或重新啟動已手動關閉的風險事件。 


![有風險的登入](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>後續步驟

- 如需 Azure Active Directory Identity Protection 的詳細資訊，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。

