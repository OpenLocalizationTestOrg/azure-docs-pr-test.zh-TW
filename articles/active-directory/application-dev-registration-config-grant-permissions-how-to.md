---
title: "如何為自訂開發的應用程式授與權限 | Microsoft Docs"
description: "如何使用 Azure AD 入口網站或 URL 參數來為自訂開發的應用程式授與權限"
services: active-directory
documentationcenter: 
author: ajamess
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0f13efd5e629bde592a3ab3a3e2db4a22180b5bb
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a>如何為自訂開發的應用程式授與權限

如果您希望在應用程式上事先獲得同意，或遇到您尚未同意應用程式的錯誤，請嘗試下列步驟。

## <a name="how-to-perform-admin-consent-for-your-application"></a>如何讓管理員同意您的應用程式

這樣就能讓組織內的所有使用者獲得同意來使用應用程式。

1. 以**全域管理員**身分瀏覽至 [應用程式註冊] 刀鋒視窗，然後選取應用程式。

2. 選取 [需要的權限]，最後點選刀鋒視窗頂端的 [授與權限] 按鈕。

或者，您可以利用您的應用程式設定來建構對 *login.microsoftonline.com* 的要求，並附加於 *&prompt=admin\_consent* 上。 使用系統管理員認證登入之後，就已同意所有使用者使用應用程式。

## <a name="how-to-force-user-consent-for-your-application"></a>如何強制使用者同意您的應用程式

* 附加至授權要求 *&prompt=consent* 上，這會在使用者每次驗證時要求他們同意。

## <a name="next-steps"></a>後續步驟

[同意並將應用程式整合到 AzureAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

[適用於 AzureAD v2.0 交集應用程式的同意與權限](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow (英文)](http://stackoverflow.com/questions/tagged/azure-active-directory)
