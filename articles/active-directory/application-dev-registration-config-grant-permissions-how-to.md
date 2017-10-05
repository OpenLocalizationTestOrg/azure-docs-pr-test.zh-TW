---
title: "如何為自訂開發的應用程式授與權限 | Microsoft Docs"
description: "如何使用 Azure AD 入口網站或 URL 參數來為自訂開發的應用程式授與權限"
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
ms.openlocfilehash: 336b945929f80e1a566f7cf71b40fd799a98c12d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="2f32e-103">如何為自訂開發的應用程式授與權限</span><span class="sxs-lookup"><span data-stu-id="2f32e-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="2f32e-104">如果您希望在應用程式上事先獲得同意，或遇到您尚未同意應用程式的錯誤，請嘗試下列步驟。</span><span class="sxs-lookup"><span data-stu-id="2f32e-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="2f32e-105">如何讓管理員同意您的應用程式</span><span class="sxs-lookup"><span data-stu-id="2f32e-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="2f32e-106">這樣就能讓組織內的所有使用者獲得同意來使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f32e-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="2f32e-107">以**全域管理員**身分瀏覽至 [應用程式註冊] 刀鋒視窗，然後選取應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f32e-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="2f32e-108">選取 [需要的權限]，最後點選刀鋒視窗頂端的 [授與權限] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f32e-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="2f32e-109">或者，您可以利用您的應用程式設定來建構對 *login.microsoftonline.com* 的要求，並附加於 *&prompt=admin\_consent* 上。</span><span class="sxs-lookup"><span data-stu-id="2f32e-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="2f32e-110">使用系統管理員認證登入之後，就已同意所有使用者使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f32e-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="2f32e-111">如何強制使用者同意您的應用程式</span><span class="sxs-lookup"><span data-stu-id="2f32e-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="2f32e-112">附加至授權要求 *&prompt=consent* 上，這會在使用者每次驗證時要求他們同意。</span><span class="sxs-lookup"><span data-stu-id="2f32e-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f32e-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f32e-113">Next steps</span></span>

[<span data-ttu-id="2f32e-114">同意並將應用程式整合到 AzureAD</span><span class="sxs-lookup"><span data-stu-id="2f32e-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="2f32e-115">適用於 AzureAD v2.0 交集應用程式的同意與權限</span><span class="sxs-lookup"><span data-stu-id="2f32e-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="2f32e-116">AzureAD StackOverflow (英文)</span><span class="sxs-lookup"><span data-stu-id="2f32e-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
