---
title: "自訂開發的應用程式所需的特定 API 的 aaaHow toofind |Microsoft 文件"
description: "您必須在自訂的 tooaccess 特定 API tooconfigure hello 權限如何開發 Azure AD 應用程式"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="dda65-103">如何 toofind 特定 API 所需的自訂開發的應用程式</span><span class="sxs-lookup"><span data-stu-id="dda65-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="dda65-104">存取 tooAPIs 要求設定存取領域和角色。</span><span class="sxs-lookup"><span data-stu-id="dda65-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="dda65-105">如果您想 tooexpose 資源應用程式 web 應用程式開發介面 tooclient 應用程式，您需要 tooconfigure 存取領域和角色 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="dda65-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="dda65-106">如果您想用戶端應用程式 tooaccess web API，您會需要 tooconfigure 權限 tooaccess hello API hello 應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="dda65-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="dda65-107">設定資源應用程式 tooexpose web 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="dda65-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="dda65-108">當您的 web 應用程式開發介面，公開 （expose） hello 應用程式開發介面會顯示在 hello**選取應用程式開發介面**清單加入權限 tooan 應用程式註冊時。</span><span class="sxs-lookup"><span data-stu-id="dda65-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="dda65-109">tooadd 存取領域，請依照下列所述的 hello 步驟[新增存取領域 tooyour 資源應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application)。</span><span class="sxs-lookup"><span data-stu-id="dda65-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="dda65-110">設定用戶端應用程式 tooaccess web 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="dda65-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="dda65-111">當您將權限 tooyour 應用程式註冊時，您可以**加入應用程式開發介面存取**tooexposed web Api。</span><span class="sxs-lookup"><span data-stu-id="dda65-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="dda65-112">tooaccess web 應用程式開發介面，請遵循所述的 hello 步驟[新增認證或權限 tooaccess web Api](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis)。</span><span class="sxs-lookup"><span data-stu-id="dda65-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dda65-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dda65-113">Next steps</span></span>

-   [<span data-ttu-id="dda65-114">整合應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dda65-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="dda65-115">了解 hello Azure Active Directory 應用程式資訊清單</span><span class="sxs-lookup"><span data-stu-id="dda65-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


