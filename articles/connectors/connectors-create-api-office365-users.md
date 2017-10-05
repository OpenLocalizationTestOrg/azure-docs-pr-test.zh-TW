---
title: "在 Logic Apps 中新增 Office 365 使用者連接器 | Microsoft Docs"
description: "搭配 REST API 參數來使用 Office 365 使用者連接器的概觀"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="da6f5-103">開始使用 Office 365 使用者連接器</span><span class="sxs-lookup"><span data-stu-id="da6f5-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="da6f5-104">連接至 Office 365 使用者，以取得設定檔、搜尋使用者等等。</span><span class="sxs-lookup"><span data-stu-id="da6f5-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="da6f5-105">您可以利用 Office 365 使用者來：</span><span class="sxs-lookup"><span data-stu-id="da6f5-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="da6f5-106">根據您從 Office 365 使用者所取得的資料，來建置您的商務流程。</span><span class="sxs-lookup"><span data-stu-id="da6f5-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="da6f5-107">使用可取得直屬員工、取得管理員的使用者設定檔等等的動作。</span><span class="sxs-lookup"><span data-stu-id="da6f5-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="da6f5-108">這些動作會收到回應，然後輸出能讓其他動作使用的資料。</span><span class="sxs-lookup"><span data-stu-id="da6f5-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="da6f5-109">例如，取得某人的直屬員工，然後利用此資訊更新 SQL Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="da6f5-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="da6f5-110">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="da6f5-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="da6f5-111">建立至 Office 365 使用者的連線</span><span class="sxs-lookup"><span data-stu-id="da6f5-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="da6f5-112">當您將這個連接器新增到邏輯應用程式時，您必須登入您的 Office 365 使用者帳戶，並允許邏輯應用程式連線到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="da6f5-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="da6f5-113">連線建立之後，您需要輸入 Office 365 使用者屬性，像是使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="da6f5-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="da6f5-114">本主題的＜REST API 參考＞  一節說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="da6f5-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="da6f5-115">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="da6f5-115">Connector-specific details</span></span>

<span data-ttu-id="da6f5-116">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/officeusers/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="da6f5-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="da6f5-117">其他連接器</span><span class="sxs-lookup"><span data-stu-id="da6f5-117">More connectors</span></span>
<span data-ttu-id="da6f5-118">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="da6f5-118">Go back to the [APIs list](apis-list.md).</span></span>