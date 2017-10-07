---
title: "aaaHow toogrant tooa 自訂開發應用程式權限 |Microsoft 文件"
description: "如何 toogrant 權限 tooyour 自訂開發的應用程式使用 hello Azure AD 入口網站或 URL 參數"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>如何 toogrant 權限 tooa 自訂開發的應用程式

如果您事先在您的應用程式上想 toogrant 同意或執行時發生錯誤，您不同意 tooan 應用程式，請嘗試下面這些步驟。

## <a name="how-tooperform-admin-consent-for-your-application"></a>如何 tooperform 獲得管理員同意應用程式

這有授與您的組織中的所有使用者同意 toohello 應用程式的 hello 效果。

1. 瀏覽 toohello**應用程式註冊**刀鋒視窗為**全域管理員**，然後選取 hello 應用程式。

2. 選取**必要的使用權限**，最後達到 hello 和**授與權限**在 hello hello 刀鋒視窗頂端的按鈕。

或者，您可以建構要求太*login.microsoftonline.com*與應用程式設定並附加上*& 提示 = admin\_同意*。 登入系統管理員認證之後, hello 應用程式已獲得同意的所有使用者。

## <a name="how-tooforce-user-consent-for-your-application"></a>如何 tooforce 使用者同意應用程式

* 附加到驗證要求*& 提示 = 同意*需要使用者 tooconsent 它們會驗證每一次。

## <a name="next-steps"></a>後續步驟

[TooAzureAD 同意和整合應用程式](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[適用於 AzureAD v2.0 交集應用程式的同意與權限](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow (英文)](http://stackoverflow.com/questions/tagged/azure-active-directory)
