---
title: "中的 Logic Apps aaaAdd hello Office 365 使用者連接器 |Microsoft 文件"
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
ms.openlocfilehash: 2fae1c80d195a368b5f6c1ad650905a0d6e94c83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-users-connector"></a><span data-ttu-id="cddf3-103">開始使用 hello Office 365 使用者連接器</span><span class="sxs-lookup"><span data-stu-id="cddf3-103">Get started with hello Office 365 Users connector</span></span>
<span data-ttu-id="cddf3-104">連接 tooOffice 365 使用者 tooget 設定檔、 搜尋使用者等等。</span><span class="sxs-lookup"><span data-stu-id="cddf3-104">Connect tooOffice 365 Users tooget profiles, search users, and more.</span></span> <span data-ttu-id="cddf3-105">您可以利用 Office 365 使用者來：</span><span class="sxs-lookup"><span data-stu-id="cddf3-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="cddf3-106">建立根據 hello 資料從 Office 365 使用者取得您業務流程。</span><span class="sxs-lookup"><span data-stu-id="cddf3-106">Build your business flow based on hello data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="cddf3-107">使用可取得直屬員工、取得管理員的使用者設定檔等等的動作。</span><span class="sxs-lookup"><span data-stu-id="cddf3-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="cddf3-108">這些動作取得回應，然後再 hello 輸出適用於其他動作。</span><span class="sxs-lookup"><span data-stu-id="cddf3-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="cddf3-109">例如，取得某人的直屬員工，然後利用此資訊更新 SQL Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="cddf3-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="cddf3-110">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="cddf3-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toooffice-365-users"></a><span data-ttu-id="cddf3-111">建立連接 tooOffice 365 使用者</span><span class="sxs-lookup"><span data-stu-id="cddf3-111">Create a connection tooOffice 365 Users</span></span>
<span data-ttu-id="cddf3-112">當您新增此連接器 tooyour 邏輯應用程式時，您必須登入 tooyour Office 365 使用者帳戶，並允許的 logic apps tooconnect tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cddf3-112">When you add this connector tooyour logic apps, you must sign-in tooyour Office 365 Users account and allow logic apps tooconnect tooyour account.</span></span>

> [!INCLUDE [Steps toocreate a connection tooOffice 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="cddf3-113">建立 hello 連線之後，您輸入 hello Office 365 使用者的內容，像是 hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="cddf3-113">After you create hello connection, you enter hello Office 365 Users properties, like hello user ID.</span></span> <span data-ttu-id="cddf3-114">hello **REST API 參考**本主題說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="cddf3-114">hello **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="cddf3-115">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="cddf3-115">Connector-specific details</span></span>

<span data-ttu-id="cddf3-116">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/officeusers/)。</span><span class="sxs-lookup"><span data-stu-id="cddf3-116">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="cddf3-117">其他連接器</span><span class="sxs-lookup"><span data-stu-id="cddf3-117">More connectors</span></span>
<span data-ttu-id="cddf3-118">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="cddf3-118">Go back toohello [APIs list](apis-list.md).</span></span>
