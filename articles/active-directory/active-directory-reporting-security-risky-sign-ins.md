---
title: "aaaRisky hello Azure Active Directory 入口網站中的登入報表 |Microsoft 文件"
description: "深入了解 hello Azure Active Directory 入口網站中的 hello 危險的登入報表"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory 入口網站中的高風險的登入報表

使用 Azure Active Directory (Azure AD) 中的 hello 安全性報告中，您可以取得 hello 機率盜用的使用者帳戶的深入了解您的環境中。 

Azure AD 會偵測到可疑相關的 tooyour 使用者帳戶的動作。 針對每個偵測到的動作，將會建立一筆稱為「風險事件」的記錄。 如需詳細資訊，請參閱 [Azure Active 風險事件](active-directory-identity-protection-risk-events.md)。 

hello 偵測到有使用的 toocalculate 風險事件：

- **高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。 如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。 

- **標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。 如需詳細資訊，請參閱[標幟為有風險的使用者](active-directory-identityprotection.md#users-flagged-for-risk)。  

在[hello Azure 入口網站](https://portal.azure.com)，您可以找到 hello 安全性報告 hello **Azure Active Directory**刀鋒視窗中 hello**安全性**> 一節。 

![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Azure AD 授權您需要 tooaccess 安全性報表嗎？  

所有 Azure Active Directory 版本都會為您提供有風險的登入報告。  
不過，報表資料粒度層級 hello hello 版本而異： 

- 在 hello **Azure Active Directory Free 和 Basic 版本**，您已取得高風險的登入的清單。 

- hello **Azure Active Directory Premium 1**版本擴充這個模型也啟用 tooexamine hello 已偵測到每個報表的風險事件的基礎部分。 

- hello **Azure Active Directory Premium 2**版本會提供您以 hello 最詳盡的所有基礎的風險事件的相關資訊，而且它也可讓您自動回應 tooconfigured tooconfigure 安全性原則風險層級。



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory 免費和基本版本

hello Azure Active Directory free 和 basic 版提供您有風險的登入偵測到的清單為您的使用者。 此報告會列出：

- **使用者**-hello hello 使用者 hello 登入作業期間，所使用的名稱
- **IP** -hello 已使用的 tooconnect tooAzure Active Directory 的 hello 裝置的 IP 位址
- **位置**-使用 tooconnect tooAzure Active Directory hello 位置。
- **登入時間**-hello hello 登入執行時的時間
- **狀態**-hello hello 登入的狀態


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/01.png)

根據您調查 hello 風險登入，您可以提供意見反應 tooAzure Active Directory 中的下列動作的 hello 形式：

- 解決
- 標記為誤判
- 略過
- 重新啟動

![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/21.png)

如需詳細資訊，請參閱[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)。

此報告會提供選項以便：

- 搜尋資源
- 下載 hello 報表資料


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory Premium Edition

hello Azure Active Directory premium edition 中的 hello 危險的登入報告可讓您使用：

- 彙總資訊 hello[風險事件類型](active-directory-identity-protection-risk-events.md)偵測到的

- 選項 toodownload hello 報表


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/456.png)


當您選取風險事件時，即會取得這個風險事件的詳細報告檢視，讓您能夠：

- 選項 tooconfigure[使用者風險補救原則](active-directory-identityprotection.md#user-risk-security-policy)  

- 檢閱 hello hello 風險事件的偵測時間軸  

- 檢閱已偵測到此風險事件的使用者清單

- [手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)或重新啟動已手動關閉的風險事件。 


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/457.png)

當您選取使用者時，即會取得這位使用者的詳細報告檢視，讓您能夠：

- 開啟 檢視所有登入的 hello

- 重設 hello 使用者密碼

- 關閉所有事件

- 調查 hello 使用者報告的風險事件。 


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate 風險事件，從清單選取一個 hello。  
這會開啟 hello**詳細資料**這個風險事件刀鋒視窗。 在 hello**詳細資料**刀鋒視窗中，您已擁有 hello 選項 tooeither[手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)或重新啟動已手動關閉的風險事件。 


![有風險的登入](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>後續步驟

- 如需 Azure Active Directory Identity Protection 的詳細資訊，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。

