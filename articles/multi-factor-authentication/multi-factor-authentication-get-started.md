---
title: "Azure MFA 雲端或伺服器之間的 aaaChoose |Microsoft 文件"
description: "選擇最適合您要求，我嘗試 toosecure 以及所在位置，我的使用者位於哪個 am hello 多重要素驗證安全性解決方案。  然後選擇雲端、MFA Server 或 AD FS。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>為您選擇 hello Azure 多因素驗證解決方案
由於有數款的 Azure Multi-factor Authentication (MFA)，我們必須回答幾個問題 toofigure 哪一個版本是 hello 適當一個 toouse。  這些問題如下：

* [什麼試著 toosecure](#what-am-i-trying-to-secure)
* [Hello 使用者位於何處](#where-are-the-users-located)
* [我需要哪些功能？](#what-featured-do-i-need)

hello 下列各節提供指引判斷每個答案。

## <a name="what-am-i-trying-toosecure"></a>什麼試著 toosecure 嗎？
toodetermine hello 正確的雙步驟驗證解決方案前必須回答什麼是您嘗試 toosecure 與驗證的第二個方法的 hello 問題了。  它是 Azure 中的應用程式嗎？  或是遠端存取系統？  藉由判斷我們正在嘗試 toosecure，我們可以回答 hello 的問題必須多因素驗證啟用的 toobe。  

| 您嘗試 toosecure 有哪些？ | Hello 雲端中的 MFA | MFA Server |
| --- |:---:|:---:|
| 第一方 Microsoft 應用程式 |● |● |
| 在 hello 應用程式庫中的 SaaS 應用程式 |● |  |
| 透過 Azure AD App Proxy 發佈的 Web 應用程式 |● |  |
| 非透過 Azure AD App Proxy 發佈的 IIS 應用程式 | |● |
| VPN、RDG 等遠端存取 | ● | ● |

## <a name="where-are-hello-users-located"></a>Hello 使用者位於何處
接下來，查看我們的使用者位於何處 hello 定域機組中是否有助於 toodetermine hello 正確方案 toouse，，或使用內部 hello MFA Server。

| 使用者位置 | Hello 雲端中的 MFA | MFA Server |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD 和使用 AD FS 同盟的內部部署 AD |● |● |
| Azure AD 和使用 DirSync、Azure AD Sync、Azure AD Connect 的內部部署 AD - 而沒有密碼同步 |● |● |
| Azure AD 和使用 DirSync、Azure AD Sync、Azure AD Connect 的內部部署 AD - 使用密碼同步 |● | |
| 內部部署 Active Directory | |● |

## <a name="what-features-do-i-need"></a>我需要哪些功能？
hello 下表比較可用 hello 雲端中的多重要素驗證與 hello Multi-factor Authentication Server 的 hello 功能。

| 功能 | Hello 雲端中的 MFA | MFA Server |
| --- |:---:|:---:|
| 以行動應用程式通知做為第二個因素 | ● | ● |
| 以行動應用程式驗證碼做為第二個因素 | ● | ● |
| 以撥打電話做為第二個因素 | ● | ● |
| 以單向 SMS 做為第二個因素 | ● | ● |
| 以雙向 SMS 做為第二個因素 | | ● |
| 以硬體權杖做為第二個因素 | | ● |
| 不支援 MFA 之 Office 365 用戶端的應用程式密碼 | ● | |
| 系統管理員控制驗證方法 | ● | ● |
| PIN 模式 | | ● |
| 詐騙警示 |● | ● |
| MFA 報告 |● | ● |
| 一次性略過 | | ● |
| 通話的自訂問候語 | ● | ● |
| 可自訂的通話來電者 ID | ● | ● |
| 信任的 IP | ● | ● |
| 記住受信任裝置的 MFA | ● | |
| 條件式存取 | ● | ● |
| 快取 |  | ● |

## <a name="next-steps"></a>後續步驟

既然我們判定是否 toouse 雲端 multi-factor authentication 或 hello MFA Server 內部部署，我們可以開始設定和使用 Azure Multi-factor Authentication。 **選取代表您的實例的 hello 圖示**

<center>




[![雲端](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![伺服器](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
