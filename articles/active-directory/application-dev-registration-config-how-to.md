---
title: "如何為指定的 API 選取權限 | Microsoft Docs"
description: "如何為針對 Azure AD 開發的應用程式或要向 Azure AD 註冊的自訂應用程式尋找驗證端點。"
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
ms.openlocfilehash: 6966cf145375bf3d830d476564c428502ae40fd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="61b36-103">如何為指定的 API 選取權限</span><span class="sxs-lookup"><span data-stu-id="61b36-103">How to select permissions for a given API</span></span>

<span data-ttu-id="61b36-104">您可以在 [Azure 入口網站](https://portal.azure.com)尋找應用程式的驗證端點。</span><span class="sxs-lookup"><span data-stu-id="61b36-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="61b36-105">瀏覽至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="61b36-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="61b36-106">從左方的瀏覽窗格，按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="61b36-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="61b36-107">按一下 [應用程式註冊]，然後選擇 [端點]。</span><span class="sxs-lookup"><span data-stu-id="61b36-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="61b36-108">這樣會開啟 [端點] 頁面，其中列出您租用戶的所有驗證端點。</span><span class="sxs-lookup"><span data-stu-id="61b36-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="61b36-109">使用您所使用之驗證通訊協定特定的端點搭配應用程式識別碼，來製作您應用程式的特定驗證要求。</span><span class="sxs-lookup"><span data-stu-id="61b36-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61b36-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61b36-110">Next steps</span></span>
[<span data-ttu-id="61b36-111">Azure Active Directory 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="61b36-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
