---
title: "在 Azure AD 傳統入口網站上開始使用 Azure AD 報告 API | Microsoft Docs"
description: "如何開始使用 Azure Active Directory 報告 API"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a>在 Azure AD 傳統入口網站上開始使用 Azure Active Directory 報告 API
*本主題是 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)的一部分。*

Azure Active Directory 提供各種報告給您。 這些報告的資料對您的應用程式 (例如 SIEM 系統、稽核和商業智慧工具) 可能非常有用。 Azure AD 報告 API 透過一組以 REST 為基礎的 API 提供資料的程式設計方式存取。 您可以從各種程式設計語言和工具呼叫這些 API。

本文提供給您開始使用 Azure AD 報告 API 所需的資訊。
在下一節中，您可尋找更多有關使用稽核和登入 API 的詳細資訊。 對於其他所有 API，請參閱 [Azure AD 報告和事件 (預覽)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) 一文。

如有相關疑問、問題或意見，請連絡 [AAD 報告協助](mailto:aadreportinghelp@microsoft.com)。

## <a name="learning-map"></a>學習圖
1. **準備** - 您必須先完成 [存取 Azure AD 報告 API 的必要條件](active-directory-reporting-api-prerequisites.md)，才能測試 API 範例。
2. **瀏覽** - 取得報告 API 的第一印象：
   
   * [使用稽核 API 的範例](active-directory-reporting-api-audit-samples.md) 
   * [使用登入活動報告 API 的範例](active-directory-reporting-api-sign-in-activity-samples.md)
3. **自訂** - 建立您自己的解決方案︰ 
   
   * [使用稽核 API 參考](active-directory-reporting-api-audit-reference.md) 
   * [使用登入活動報告 API 參考](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a>後續步驟
如果您想要查看所有可用的 Azure AD 圖形 API 端點，請瀏覽至 [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta)。

