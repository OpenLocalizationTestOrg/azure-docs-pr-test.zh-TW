---
title: "在邏輯應用程式中新增 Google 雲端硬碟連接器 | Microsoft Docs"
description: "搭配 REST API 參數來使用 Google 雲端硬碟連接器的概觀"
services: 
suite: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2bcebc5-02d2-435b-b0da-ef53bc51c4b6
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c066a10b33e172eb5f16eede43ec407794000c90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-google-drive-connector"></a><span data-ttu-id="7e17c-103">開始使用 Google 雲端硬碟連接器</span><span class="sxs-lookup"><span data-stu-id="7e17c-103">Get started with the Google Drive connector</span></span>
<span data-ttu-id="7e17c-104">連線到 Google 雲端硬碟來建立檔案、取得資料列等等。</span><span class="sxs-lookup"><span data-stu-id="7e17c-104">Connect to Google Drive to create files, get rows, and more.</span></span> <span data-ttu-id="7e17c-105">您可以利用 Google 雲端硬碟來：</span><span class="sxs-lookup"><span data-stu-id="7e17c-105">With Google Drive, you can:</span></span> 

* <span data-ttu-id="7e17c-106">根據您透過搜尋所取得的資料，來建置您的商務流程。</span><span class="sxs-lookup"><span data-stu-id="7e17c-106">Build your business flow based on the data you get from your search.</span></span> 
* <span data-ttu-id="7e17c-107">使用動作來搜尋圖像、搜尋新聞等等。</span><span class="sxs-lookup"><span data-stu-id="7e17c-107">Use actions to search images, search the news, and more.</span></span> <span data-ttu-id="7e17c-108">這些動作會收到回應，然後輸出能讓其他動作使用的資料。</span><span class="sxs-lookup"><span data-stu-id="7e17c-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="7e17c-109">舉例來說，您可以搜尋某支影片，然後利用 Twitter 把該影片張貼在某個 Twitter 摘要上。</span><span class="sxs-lookup"><span data-stu-id="7e17c-109">For example, you can search for a video, and then use Twitter to post that video to a Twitter feed.</span></span>

<span data-ttu-id="7e17c-110">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="7e17c-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-the-connection-to-google-drive"></a><span data-ttu-id="7e17c-111">建立至 Google 雲端硬碟的連線</span><span class="sxs-lookup"><span data-stu-id="7e17c-111">Create the connection to Google Drive</span></span>
<span data-ttu-id="7e17c-112">當您將這個 API 新增到邏輯應用程式時，您必須授權邏輯應用程式，使其能夠連線到您的 Google 雲端硬碟。</span><span class="sxs-lookup"><span data-stu-id="7e17c-112">When you add this connector to your logic apps, you must authorize logic apps to connect to your Google Drive.</span></span>

> [!INCLUDE [Steps to create a connection to googledrive](../../includes/connectors-create-api-googledrive.md)]
> 
> 

<span data-ttu-id="7e17c-113">當您建立連線之後，請輸入 Google 雲端硬碟的屬性，例如資料夾路徑或檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="7e17c-113">After you create the connection, you enter the Google Drive properties, like the folder path or file name.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="7e17c-114">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="7e17c-114">Connector-specific details</span></span>

<span data-ttu-id="7e17c-115">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/googledrive/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="7e17c-115">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/googledrive/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7e17c-116">其他連接器</span><span class="sxs-lookup"><span data-stu-id="7e17c-116">More connectors</span></span>
<span data-ttu-id="7e17c-117">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="7e17c-117">Go back to the [APIs list](apis-list.md).</span></span>
