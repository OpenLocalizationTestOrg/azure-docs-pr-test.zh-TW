---
title: "建立應用程式 Proxy 應用程式時發生問題 | Microsoft Docs"
description: "如何針對在 Azure AD 管理入口網站中建立應用程式 Proxy 應用程式時所發生的問題進行疑難排解"
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="30188-103">建立應用程式 Proxy 應用程式時發生問題</span><span class="sxs-lookup"><span data-stu-id="30188-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="30188-104">以下是建立新的應用程式 Proxy 應用程式時會遇到的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="30188-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="30188-105">建議的文件</span><span class="sxs-lookup"><span data-stu-id="30188-105">Recommended documents</span></span> 

<span data-ttu-id="30188-106">若要深入了解透過管理入口網站建立應用程式 Proxy 應用程式，請參閱[使用 Azure AD 應用程式 Proxy 發佈應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="30188-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="30188-107">如果您依照該文件中的步驟，並在建立應用程式時發生錯誤，請查看錯誤詳細資料，以取得修正應用程式的資訊及建議。</span><span class="sxs-lookup"><span data-stu-id="30188-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="30188-108">大部分的錯誤訊息都包含建議的修正。</span><span class="sxs-lookup"><span data-stu-id="30188-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="30188-109">要檢查的特定事項</span><span class="sxs-lookup"><span data-stu-id="30188-109">Specific things to check</span></span>

<span data-ttu-id="30188-110">若要避免常見的錯誤，請確認：</span><span class="sxs-lookup"><span data-stu-id="30188-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="30188-111">您是具有建立應用程式 Proxy 應用程式權限的系統管理員</span><span class="sxs-lookup"><span data-stu-id="30188-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="30188-112">內部 URL 是唯一的</span><span class="sxs-lookup"><span data-stu-id="30188-112">The internal URL is unique</span></span>

-   <span data-ttu-id="30188-113">外部 URL 是唯一的</span><span class="sxs-lookup"><span data-stu-id="30188-113">The external URL is unique</span></span>

-   <span data-ttu-id="30188-114">URL 開頭為 http 或 https，且結尾為 “/”</span><span class="sxs-lookup"><span data-stu-id="30188-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="30188-115">URL 應該是網域名稱，而非 IP 位址</span><span class="sxs-lookup"><span data-stu-id="30188-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="30188-116">當您建立應用程式時，錯誤訊息應該會在右上角顯示。</span><span class="sxs-lookup"><span data-stu-id="30188-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="30188-117">您也可以選取通知圖示來查看錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="30188-117">You can also select the notification icon to see the error messages.</span></span>

   ![通知提示](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="30188-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30188-119">Next steps</span></span>
[<span data-ttu-id="30188-120">在 Azure 入口網站中啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="30188-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
