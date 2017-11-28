---
title: "開始使用 Visual Studio WebApi 專案中的 Azure AD aaaGet |Microsoft 文件"
description: "Tooget 啟動 WebApi 專案中使用 Azure Active Directory 連接 tooor 建立 Azure AD 使用 Visual Studio 之後，已連接服務"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 21413a71a2fd61f31268bf6d5e4d86b8be5bd16a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="bcfb8-103">開始使用 Azure Active Directory 和 Visual Studio 已連接服務 (WebApi 專案)</span><span class="sxs-lookup"><span data-stu-id="bcfb8-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcfb8-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="bcfb8-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="bcfb8-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="bcfb8-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a><span data-ttu-id="bcfb8-106">需要驗證 tooaccess 控制站</span><span class="sxs-lookup"><span data-stu-id="bcfb8-106">Requiring authentication tooaccess controllers</span></span>
<span data-ttu-id="bcfb8-107">在您的專案中的所有控制站已裝飾以 hello**授權**屬性。</span><span class="sxs-lookup"><span data-stu-id="bcfb8-107">All controllers in your project were adorned with hello **Authorize** attribute.</span></span> <span data-ttu-id="bcfb8-108">此屬性需要驗證存取 hello Api 定義的這些控制站之前 hello 使用者 toobe。</span><span class="sxs-lookup"><span data-stu-id="bcfb8-108">This attribute requires hello user toobe authenticated before accessing hello APIs defined by these controllers.</span></span> <span data-ttu-id="bcfb8-109">以匿名方式，存取 tooallow hello 控制器 toobe 從 hello 控制器移除這個屬性。</span><span class="sxs-lookup"><span data-stu-id="bcfb8-109">tooallow hello controller toobe accessed anonymously, remove this attribute from hello controller.</span></span> <span data-ttu-id="bcfb8-110">如果您想 tooset hello 權限，在更細微的層級，套用 hello 屬性 tooeach 方法，會要求授權，而不是套用它 toohello 控制器類別。</span><span class="sxs-lookup"><span data-stu-id="bcfb8-110">If you want tooset hello permissions at a more granular level, apply hello attribute tooeach method that requires authorization instead of applying it toohello controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcfb8-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcfb8-111">Next steps</span></span>
[<span data-ttu-id="bcfb8-112">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bcfb8-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

