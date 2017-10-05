---
title: "在您的 Logic Apps 中新增 Facebook 連接器 | Microsoft Docs"
description: "搭配 REST API 參數來使用 Facebook 連接器的概觀"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f4d6f0ed-c09b-488c-be1c-8cf2b5b1d4b8
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: e10a30ccef3e81cb3d7749696453d82b8958d076
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-facebook-connector"></a><span data-ttu-id="ddd88-103">開始使用 Facebook 連接器</span><span class="sxs-lookup"><span data-stu-id="ddd88-103">Get started with the Facebook connector</span></span>
<span data-ttu-id="ddd88-104">連線到 Facebook 並張貼在動態時報上、取得頁面摘要等等。</span><span class="sxs-lookup"><span data-stu-id="ddd88-104">Connect to Facebook and post to a timeline, get a page feed, and more.</span></span> <span data-ttu-id="ddd88-105">您可以利用 Facebook 來：</span><span class="sxs-lookup"><span data-stu-id="ddd88-105">With Facebook, you can:</span></span>

* <span data-ttu-id="ddd88-106">根據您從 Facebook 所取得的資料，來建置您的商務流程。</span><span class="sxs-lookup"><span data-stu-id="ddd88-106">Build your business flow based on the data you get from Facebook.</span></span> 
* <span data-ttu-id="ddd88-107">在接收到新貼文時使用觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ddd88-107">Use a trigger when a new post is received.</span></span>
* <span data-ttu-id="ddd88-108">使用會張貼到您的動態時報、取得頁面摘要等等的動作。</span><span class="sxs-lookup"><span data-stu-id="ddd88-108">Use actions that post to your timeline, get a page feed, and more.</span></span> <span data-ttu-id="ddd88-109">這些動作會收到回應，然後輸出能讓其他動作使用的資料。</span><span class="sxs-lookup"><span data-stu-id="ddd88-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="ddd88-110">舉例來說，當您的動態時報上有新貼文時，您可以取得該貼文，然後把它推送到您的 Twitter 摘要。</span><span class="sxs-lookup"><span data-stu-id="ddd88-110">For example, when there is a new post on your timeline, you can take that post and push it to your Twitter feed.</span></span> 

<span data-ttu-id="ddd88-111">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd88-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-facebook"></a><span data-ttu-id="ddd88-112">建立至 Facebook 的連線</span><span class="sxs-lookup"><span data-stu-id="ddd88-112">Create a connection to Facebook</span></span>
<span data-ttu-id="ddd88-113">當您將這個連接器新增到邏輯應用程式時，您必須授權邏輯應用程式，使其能夠連線到您的 Facebook。</span><span class="sxs-lookup"><span data-stu-id="ddd88-113">When you add this connector to your logic apps, you must authorize logic apps to connect to your Facebook.</span></span>

1. <span data-ttu-id="ddd88-114">登入您的 Facebook 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd88-114">Sign in to your Facebook account</span></span>
2. <span data-ttu-id="ddd88-115">選取 [授權] ，然後允許您的邏輯應用程式連線並使用您的 Facebook。</span><span class="sxs-lookup"><span data-stu-id="ddd88-115">Select **Authorize**, and allow your logic apps to connect and use your Facebook.</span></span> 

> [!INCLUDE [Steps to create a connection to Facebook](../../includes/connectors-create-api-facebook.md)]
> 


## <a name="connector-specific-details"></a><span data-ttu-id="ddd88-116">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="ddd88-116">Connector-specific details</span></span>

<span data-ttu-id="ddd88-117">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/facebook/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="ddd88-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/facebook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ddd88-118">其他連接器</span><span class="sxs-lookup"><span data-stu-id="ddd88-118">More connectors</span></span>
<span data-ttu-id="ddd88-119">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd88-119">Go back to the [APIs list](apis-list.md).</span></span>