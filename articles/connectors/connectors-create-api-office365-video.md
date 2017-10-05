---
title: "在您的邏輯應用程式中新增 Office 365 影片連接器 | Microsoft Docs"
description: "開始在您的 Microsoft Azure App Service Logic Apps 中使用 Office 365 影片連接器"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 738e5aa7-2523-4116-8b65-211b9063852d
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: f0e3613d4a3fd5478787c0365eb7a0bcde886c81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office365-video-connector"></a><span data-ttu-id="f8676-103">開始使用 Office 365 影片連接器</span><span class="sxs-lookup"><span data-stu-id="f8676-103">Get started with the Office365 Video connector</span></span>
<span data-ttu-id="f8676-104">連接至 Office 365 影片，以取得 Office 365 影片的相關資訊、影片清單等。</span><span class="sxs-lookup"><span data-stu-id="f8676-104">Connect to Office 365 Video to get information about an Office 365 video, get a list of videos, and more.</span></span> <span data-ttu-id="f8676-105">有了 Office 365 影片，您可以：</span><span class="sxs-lookup"><span data-stu-id="f8676-105">With Office 365 Video, you can:</span></span>

* <span data-ttu-id="f8676-106">根據您從 Office 365 影片所取得的資料，來建置您的商務流程。</span><span class="sxs-lookup"><span data-stu-id="f8676-106">Build your business flow based on the data you get from Office 365 Video.</span></span> 
* <span data-ttu-id="f8676-107">檢查影片入口網站狀態、取得頻道影片清單等動作。</span><span class="sxs-lookup"><span data-stu-id="f8676-107">Use actions that check the video portal status, get a list of all video in a channel, and more.</span></span> <span data-ttu-id="f8676-108">這些動作會收到回應，然後輸出能讓其他動作使用的資料。</span><span class="sxs-lookup"><span data-stu-id="f8676-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="f8676-109">例如，您可以使用 Bing 搜尋連接器來搜尋 Office 365 影片，然後使用 Office 365 影片連接器取得該影片的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f8676-109">For example, you can use the Bing Search connector to search for Office 365 videos, and then use the Office 365 video connector to get information about that video.</span></span> <span data-ttu-id="f8676-110">如果影片符合您的需求，您可以將該影片張貼在 Facebook 上。</span><span class="sxs-lookup"><span data-stu-id="f8676-110">If the video meets your requirements, you can post this video on Facebook.</span></span> 

<span data-ttu-id="f8676-111">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f8676-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office365-video-connector"></a><span data-ttu-id="f8676-112">建立至 Office365 影片連接器的連線</span><span class="sxs-lookup"><span data-stu-id="f8676-112">Create a connection to Office365 Video connector</span></span>
<span data-ttu-id="f8676-113">當您將這個連接器新增到邏輯應用程式時，您必須登入您的 Office 365 影片帳戶，並允許邏輯應用程式連線到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8676-113">When you add this connector to your logic apps, you must sign-in to your Office 365 Video account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Video](../../includes/connectors-create-api-office365video.md)]
> 
> 

<span data-ttu-id="f8676-114">當您建立連線之後，請輸入 Office 365 影片的屬性，例租用戶名稱或頻道識別碼。</span><span class="sxs-lookup"><span data-stu-id="f8676-114">After you create the connection, you enter the Office 365 video properties, like the tenant name or channel ID.</span></span> 


## <a name="connector-specific-details"></a><span data-ttu-id="f8676-115">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="f8676-115">Connector-specific details</span></span>

<span data-ttu-id="f8676-116">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/office365videoconnector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="f8676-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365videoconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f8676-117">其他連接器</span><span class="sxs-lookup"><span data-stu-id="f8676-117">More connectors</span></span>
<span data-ttu-id="f8676-118">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="f8676-118">Go back to the [APIs list](apis-list.md).</span></span>