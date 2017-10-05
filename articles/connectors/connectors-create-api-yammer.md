---
title: "在 Azure Logic Apps 中新增 Yammer 連接器 | Microsoft Docs"
description: "搭配 REST API 參數來使用 Yammer 連接器的概觀"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="15545-103">開始使用 Yammer 連接器</span><span class="sxs-lookup"><span data-stu-id="15545-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="15545-104">連線到 Yammer 來存取您企業網路中的交談。</span><span class="sxs-lookup"><span data-stu-id="15545-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="15545-105">您可以利用 Yammer 來：</span><span class="sxs-lookup"><span data-stu-id="15545-105">With Yammer, you can:</span></span>

* <span data-ttu-id="15545-106">根據您從 Yammer 所取得的資料，來建置您的商務流程。</span><span class="sxs-lookup"><span data-stu-id="15545-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="15545-107">在群組或您追蹤的摘要中有新訊息時使用觸發程序。</span><span class="sxs-lookup"><span data-stu-id="15545-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="15545-108">使用動作來張貼訊息、取得所有訊息等等。</span><span class="sxs-lookup"><span data-stu-id="15545-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="15545-109">這些動作會收到回應，然後輸出能讓其他動作使用的資料。</span><span class="sxs-lookup"><span data-stu-id="15545-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="15545-110">舉例來說，當新訊息出現時，您可以利用 Office 365 來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15545-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="15545-111">立即開始建立邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="15545-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="15545-112">建立至 Yammer 的連線</span><span class="sxs-lookup"><span data-stu-id="15545-112">Create a connection to Yammer</span></span>
<span data-ttu-id="15545-113">若要使用 Yammer 連接器，您必須先建立**連接**，然後提供下列屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="15545-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="15545-114">屬性</span><span class="sxs-lookup"><span data-stu-id="15545-114">Property</span></span> | <span data-ttu-id="15545-115">必要</span><span class="sxs-lookup"><span data-stu-id="15545-115">Required</span></span> | <span data-ttu-id="15545-116">說明</span><span class="sxs-lookup"><span data-stu-id="15545-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15545-117">權杖</span><span class="sxs-lookup"><span data-stu-id="15545-117">Token</span></span> |<span data-ttu-id="15545-118">是</span><span class="sxs-lookup"><span data-stu-id="15545-118">Yes</span></span> |<span data-ttu-id="15545-119">提供 Yammer 的認證</span><span class="sxs-lookup"><span data-stu-id="15545-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="15545-120">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="15545-120">Connector-specific details</span></span>

<span data-ttu-id="15545-121">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/yammer/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="15545-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="15545-122">其他連接器</span><span class="sxs-lookup"><span data-stu-id="15545-122">More connectors</span></span>
<span data-ttu-id="15545-123">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="15545-123">Go back to the [APIs list](apis-list.md).</span></span>