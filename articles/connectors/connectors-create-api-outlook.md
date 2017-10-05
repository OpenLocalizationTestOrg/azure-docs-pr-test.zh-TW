---
title: "Azure Logic Apps 中的 Outlook.com 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 Outlook.com 連接器可讓您管理您的郵件、行事曆和連絡人。 您可以執行各種動作，例如傳送郵件、排程會議、新增連絡人等等。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="c0369-105">開始使用 Outlook.com 連接器</span><span class="sxs-lookup"><span data-stu-id="c0369-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="c0369-106">Outlook.com 連接器可讓您管理您的郵件、行事曆和連絡人。</span><span class="sxs-lookup"><span data-stu-id="c0369-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="c0369-107">您可以執行各種動作，例如傳送郵件、排程會議、新增連絡人等等。</span><span class="sxs-lookup"><span data-stu-id="c0369-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="c0369-108">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="c0369-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="c0369-109">建立 Outlook.com 的連線</span><span class="sxs-lookup"><span data-stu-id="c0369-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="c0369-110">若要使用 Outlook.com 建立邏輯應用程式，您必須先建立**連接**，然後提供下列屬性的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="c0369-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="c0369-111">屬性</span><span class="sxs-lookup"><span data-stu-id="c0369-111">Property</span></span> | <span data-ttu-id="c0369-112">必要</span><span class="sxs-lookup"><span data-stu-id="c0369-112">Required</span></span> | <span data-ttu-id="c0369-113">說明</span><span class="sxs-lookup"><span data-stu-id="c0369-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0369-114">權杖</span><span class="sxs-lookup"><span data-stu-id="c0369-114">Token</span></span> |<span data-ttu-id="c0369-115">是</span><span class="sxs-lookup"><span data-stu-id="c0369-115">Yes</span></span> |<span data-ttu-id="c0369-116">提供 Outlook.com 認證</span><span class="sxs-lookup"><span data-stu-id="c0369-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="c0369-117">建立連線後，您就可以用它執行動作，並接聽本文所述的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c0369-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="c0369-118">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="c0369-118">Connector-specific details</span></span>

<span data-ttu-id="c0369-119">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/outlook/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="c0369-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c0369-120">其他連接器</span><span class="sxs-lookup"><span data-stu-id="c0369-120">More connectors</span></span>
<span data-ttu-id="c0369-121">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="c0369-121">Go back to the [APIs list](apis-list.md).</span></span>