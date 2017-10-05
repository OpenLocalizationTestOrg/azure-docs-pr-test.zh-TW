---
title: SendGrid | Microsoft Docs
description: "使用 Azure App Service 建立邏輯應用程式。 SendGrid 連線提供者可讓您傳送電子郵件及管理收件者清單。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 9ff0591741899d65b8274fb14ab3f3c8db9abe36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sendgrid-connector"></a><span data-ttu-id="1893a-104">開始使用 SendGrid 連接器</span><span class="sxs-lookup"><span data-stu-id="1893a-104">Get started with the SendGrid connector</span></span>
<span data-ttu-id="1893a-105">SendGrid 連線提供者可讓您傳送電子郵件及管理收件者清單。</span><span class="sxs-lookup"><span data-stu-id="1893a-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span></span>

<span data-ttu-id="1893a-106">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="1893a-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sendgrid"></a><span data-ttu-id="1893a-107">建立 SendGrid 的連線</span><span class="sxs-lookup"><span data-stu-id="1893a-107">Create a connection to SendGrid</span></span>
<span data-ttu-id="1893a-108">若要使用 SendGrid 建立邏輯應用程式，您必須先建立**連接**，然後提供下列屬性的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="1893a-108">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="1893a-109">屬性</span><span class="sxs-lookup"><span data-stu-id="1893a-109">Property</span></span> | <span data-ttu-id="1893a-110">必要</span><span class="sxs-lookup"><span data-stu-id="1893a-110">Required</span></span> | <span data-ttu-id="1893a-111">說明</span><span class="sxs-lookup"><span data-stu-id="1893a-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1893a-112">ApiKey</span><span class="sxs-lookup"><span data-stu-id="1893a-112">ApiKey</span></span> |<span data-ttu-id="1893a-113">是</span><span class="sxs-lookup"><span data-stu-id="1893a-113">Yes</span></span> |<span data-ttu-id="1893a-114">提供您的 SendGrid API 金鑰</span><span class="sxs-lookup"><span data-stu-id="1893a-114">Provide Your SendGrid Api Key</span></span> |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 


<span data-ttu-id="1893a-115">建立連線後，您就可以用它執行動作，並接聽觸發程序。</span><span class="sxs-lookup"><span data-stu-id="1893a-115">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="1893a-116">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="1893a-116">Connector-specific details</span></span>

<span data-ttu-id="1893a-117">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/sendgrid/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="1893a-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sendgrid/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="1893a-118">其他連接器</span><span class="sxs-lookup"><span data-stu-id="1893a-118">More connectors</span></span>
<span data-ttu-id="1893a-119">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="1893a-119">Go back to the [APIs list](apis-list.md).</span></span>