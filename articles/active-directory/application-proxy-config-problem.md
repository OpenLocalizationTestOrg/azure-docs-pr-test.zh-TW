---
title: "建立應用程式 Proxy 應用程式的 aaaProblem |Microsoft 文件"
description: "Tootroubleshoot 如何發出在 hello Azure AD 管理入口網站中建立的應用程式 Proxy 應用程式"
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
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="8427c-103">建立應用程式 Proxy 應用程式時發生問題</span><span class="sxs-lookup"><span data-stu-id="8427c-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="8427c-104">以下是一些 hello 常見問題人臉時建立新的應用程式 proxy 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8427c-104">Below are some of hello common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="8427c-105">建議的文件</span><span class="sxs-lookup"><span data-stu-id="8427c-105">Recommended documents</span></span> 

<span data-ttu-id="8427c-106">toolearn 進一步了解建立應用程式 Proxy 應用程式透過 hello 管理入口網站，請參閱[使用 Azure AD Application Proxy 發行應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="8427c-106">toolearn more about creating an Application Proxy application through hello Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="8427c-107">如果您要遵照 hello 該文件中的步驟，並取得建立 hello 應用程式時發生錯誤，請參閱 hello 錯誤詳細資料的資訊及如何 toofix hello 應用程式的建議。</span><span class="sxs-lookup"><span data-stu-id="8427c-107">If you are following hello steps in that document and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="8427c-108">大部分的錯誤訊息都包含建議的修正。</span><span class="sxs-lookup"><span data-stu-id="8427c-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-toocheck"></a><span data-ttu-id="8427c-109">特定項目 toocheck</span><span class="sxs-lookup"><span data-stu-id="8427c-109">Specific things toocheck</span></span>

<span data-ttu-id="8427c-110">tooavoid 常見的錯誤，請確認：</span><span class="sxs-lookup"><span data-stu-id="8427c-110">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="8427c-111">您是系統管理員的權限 toocreate 應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="8427c-111">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="8427c-112">是唯一的 hello 內部 URL</span><span class="sxs-lookup"><span data-stu-id="8427c-112">hello internal URL is unique</span></span>

-   <span data-ttu-id="8427c-113">hello 外部 URL 是唯一的</span><span class="sxs-lookup"><span data-stu-id="8427c-113">hello external URL is unique</span></span>

-   <span data-ttu-id="8427c-114">hello http 或 https 的 Url 開頭和結尾為"/"</span><span class="sxs-lookup"><span data-stu-id="8427c-114">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="8427c-115">hello URL 應該是網域名稱而不是 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8427c-115">hello URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="8427c-116">當您建立 hello 應用程式時應該顯示 hello 右上角 hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="8427c-116">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="8427c-117">您也可以選取 hello 通知圖示 toosee hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="8427c-117">You can also select hello notification icon toosee hello error messages.</span></span>

   ![通知提示](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="8427c-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8427c-119">Next steps</span></span>
[<span data-ttu-id="8427c-120">在 hello Azure 入口網站中啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="8427c-120">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
