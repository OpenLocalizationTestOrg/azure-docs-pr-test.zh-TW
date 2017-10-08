---
title: "aaaAdd hello Azure 邏輯應用程式中的 Yammer 連接器 |Microsoft 文件"
description: "使用 REST API 參數 hello Yammer 連接器的概觀"
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
ms.openlocfilehash: be75df770a8062d839926dff8c0195d2647f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-yammer-connector"></a><span data-ttu-id="9dc5b-103">開始使用 hello Yammer 連接器</span><span class="sxs-lookup"><span data-stu-id="9dc5b-103">Get started with hello Yammer connector</span></span>
<span data-ttu-id="9dc5b-104">連接您的企業網路中的 tooYammer tooaccess 交談。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-104">Connect tooYammer tooaccess conversations in your enterprise network.</span></span> <span data-ttu-id="9dc5b-105">您可以利用 Yammer 來：</span><span class="sxs-lookup"><span data-stu-id="9dc5b-105">With Yammer, you can:</span></span>

* <span data-ttu-id="9dc5b-106">建置您的商務流程根據您取得 Yammer hello 資料。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-106">Build your business flow based on hello data you get from Yammer.</span></span> 
* <span data-ttu-id="9dc5b-107">在群組或您追蹤的摘要中有新訊息時使用觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="9dc5b-108">使用動作 toopost 一則訊息，取得所有訊息等等。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-108">Use actions toopost a message, get all messages, and more.</span></span> <span data-ttu-id="9dc5b-109">這些動作取得回應，然後再 hello 輸出適用於其他動作。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-109">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="9dc5b-110">舉例來說，當新訊息出現時，您可以利用 Office 365 來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="9dc5b-111">立即開始建立邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooyammer"></a><span data-ttu-id="9dc5b-112">建立連接 tooYammer</span><span class="sxs-lookup"><span data-stu-id="9dc5b-112">Create a connection tooYammer</span></span>
<span data-ttu-id="9dc5b-113">toouse hello Yammer 連接器，您先建立**連接**然後提供這些屬性中的 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="9dc5b-113">toouse hello Yammer connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="9dc5b-114">屬性</span><span class="sxs-lookup"><span data-stu-id="9dc5b-114">Property</span></span> | <span data-ttu-id="9dc5b-115">必要</span><span class="sxs-lookup"><span data-stu-id="9dc5b-115">Required</span></span> | <span data-ttu-id="9dc5b-116">說明</span><span class="sxs-lookup"><span data-stu-id="9dc5b-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dc5b-117">權杖</span><span class="sxs-lookup"><span data-stu-id="9dc5b-117">Token</span></span> |<span data-ttu-id="9dc5b-118">是</span><span class="sxs-lookup"><span data-stu-id="9dc5b-118">Yes</span></span> |<span data-ttu-id="9dc5b-119">提供 Yammer 的認證</span><span class="sxs-lookup"><span data-stu-id="9dc5b-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps toocreate a connection tooYammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="9dc5b-120">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="9dc5b-120">Connector-specific details</span></span>

<span data-ttu-id="9dc5b-121">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/yammer/)。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-121">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="9dc5b-122">其他連接器</span><span class="sxs-lookup"><span data-stu-id="9dc5b-122">More connectors</span></span>
<span data-ttu-id="9dc5b-123">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="9dc5b-123">Go back toohello [APIs list](apis-list.md).</span></span>
