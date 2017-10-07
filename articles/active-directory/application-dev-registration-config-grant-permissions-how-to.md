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
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="310b3-103">如何 toogrant 權限 tooa 自訂開發的應用程式</span><span class="sxs-lookup"><span data-stu-id="310b3-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="310b3-104">如果您事先在您的應用程式上想 toogrant 同意或執行時發生錯誤，您不同意 tooan 應用程式，請嘗試下面這些步驟。</span><span class="sxs-lookup"><span data-stu-id="310b3-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="310b3-105">如何 tooperform 獲得管理員同意應用程式</span><span class="sxs-lookup"><span data-stu-id="310b3-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="310b3-106">這有授與您的組織中的所有使用者同意 toohello 應用程式的 hello 效果。</span><span class="sxs-lookup"><span data-stu-id="310b3-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="310b3-107">瀏覽 toohello**應用程式註冊**刀鋒視窗為**全域管理員**，然後選取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="310b3-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="310b3-108">選取**必要的使用權限**，最後達到 hello 和**授與權限**在 hello hello 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="310b3-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="310b3-109">或者，您可以建構要求太*login.microsoftonline.com*與應用程式設定並附加上*& 提示 = admin\_同意*。</span><span class="sxs-lookup"><span data-stu-id="310b3-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="310b3-110">登入系統管理員認證之後, hello 應用程式已獲得同意的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="310b3-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="310b3-111">如何 tooforce 使用者同意應用程式</span><span class="sxs-lookup"><span data-stu-id="310b3-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="310b3-112">附加到驗證要求*& 提示 = 同意*需要使用者 tooconsent 它們會驗證每一次。</span><span class="sxs-lookup"><span data-stu-id="310b3-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="310b3-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="310b3-113">Next steps</span></span>

[<span data-ttu-id="310b3-114">TooAzureAD 同意和整合應用程式</span><span class="sxs-lookup"><span data-stu-id="310b3-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="310b3-115">適用於 AzureAD v2.0 交集應用程式的同意與權限</span><span class="sxs-lookup"><span data-stu-id="310b3-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="310b3-116">AzureAD StackOverflow (英文)</span><span class="sxs-lookup"><span data-stu-id="310b3-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
