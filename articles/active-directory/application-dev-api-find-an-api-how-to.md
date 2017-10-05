---
title: "如何尋找自訂開發應用程式所需的特定 API | Microsoft Docs"
description: "如何在您的自訂開發 Azure AD 應用程式中設定存取特定 API 所需的權限"
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
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="eb75d-103">如何尋找自訂開發應用程式所需的特定 API</span><span class="sxs-lookup"><span data-stu-id="eb75d-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="eb75d-104">存取 API 需要設定存取範圍和角色。</span><span class="sxs-lookup"><span data-stu-id="eb75d-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="eb75d-105">如果您想要將資源應用程式 Web API 公開給用戶端應用程式，您需要設定 API 的存取範圍和角色。</span><span class="sxs-lookup"><span data-stu-id="eb75d-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="eb75d-106">如果您想要讓用戶端應用程式存取 Web API，您需要設定權限以存取應用程式註冊中的 API。</span><span class="sxs-lookup"><span data-stu-id="eb75d-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="eb75d-107">設定資源應用程式以公開 Web API</span><span class="sxs-lookup"><span data-stu-id="eb75d-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="eb75d-108">當您公開 Web API 時，該 API 會在將權限新增到應用程式註冊時顯示於 [選取 API] 清單中。</span><span class="sxs-lookup"><span data-stu-id="eb75d-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="eb75d-109">若要新增存取範圍，請依照[新增資源應用程式的存取範圍](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application)中概述的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="eb75d-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="eb75d-110">設定用戶端應用程式以存取 Web API</span><span class="sxs-lookup"><span data-stu-id="eb75d-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="eb75d-111">當您將權限新增到應用程式註冊時，您可以**新增 API 存取**以公開 Web API。</span><span class="sxs-lookup"><span data-stu-id="eb75d-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="eb75d-112">若要存取 Web API，請依照[新增認證或權限以存取 Web API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis) 中概述的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="eb75d-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb75d-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb75d-113">Next steps</span></span>

-   [<span data-ttu-id="eb75d-114">整合應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb75d-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="eb75d-115">了解 Azure Active Directory 應用程式資訊清單</span><span class="sxs-lookup"><span data-stu-id="eb75d-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


