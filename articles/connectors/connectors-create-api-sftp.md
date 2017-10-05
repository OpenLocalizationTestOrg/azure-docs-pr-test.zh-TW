---
title: "了解如何在您的邏輯應用程式中使用 SFTP 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 連接到 SFTP API 來傳送及接收檔案。 您可以執行各種作業，例如建立、更新、取得或刪除檔案。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="5110b-105">開始使用 SFTP 連接器</span><span class="sxs-lookup"><span data-stu-id="5110b-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="5110b-106">使用 SFTP 連接器存取 SFTP 帳戶來傳送及接收檔案。</span><span class="sxs-lookup"><span data-stu-id="5110b-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="5110b-107">您可以執行各種作業，例如建立、更新、取得或刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="5110b-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="5110b-108">若要使用[任何連接器](apis-list.md)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="5110b-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="5110b-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="5110b-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="5110b-110">連接至 SFTP</span><span class="sxs-lookup"><span data-stu-id="5110b-110">Connect to SFTP</span></span>
<span data-ttu-id="5110b-111">您必須先建立與服務的連線，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="5110b-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="5110b-112">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="5110b-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="5110b-113">建立至 SFTP 的連線</span><span class="sxs-lookup"><span data-stu-id="5110b-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="5110b-114">使用 SFTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="5110b-114">Use an SFTP trigger</span></span>
<span data-ttu-id="5110b-115">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="5110b-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="5110b-116">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="5110b-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="5110b-117">在此範例中，當在 SFTP 伺服器上新增或修改檔案時，就會使用 **SFTP - 新增或修改檔案時**觸發程序起始邏輯應用程式工作流程。</span><span class="sxs-lookup"><span data-stu-id="5110b-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="5110b-118">您也可以新增會檢查新的或修改之檔案內容的條件，並在使用內容之前如果檔案指出它應該要解壓縮時，決定將檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="5110b-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="5110b-119">最後，新增動作以解壓縮檔案的內容，並將解壓縮的內容放在 SFTP 伺服器上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5110b-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="5110b-120">在企業範例中，您可以使用此觸發程序來監視代表客戶訂單的新檔案 SFTP 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5110b-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="5110b-121">然後，您可以使用 SFTP 連接器動作 (例如**取得檔案內容**) 取得訂單的內容以進一步處理並儲存在訂單資料庫中。</span><span class="sxs-lookup"><span data-stu-id="5110b-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="5110b-122">新增條件</span><span class="sxs-lookup"><span data-stu-id="5110b-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="5110b-123">使用 SFTP 動作</span><span class="sxs-lookup"><span data-stu-id="5110b-123">Use an SFTP action</span></span>
<span data-ttu-id="5110b-124">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="5110b-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="5110b-125">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="5110b-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="5110b-126">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="5110b-126">Connector-specific details</span></span>

<span data-ttu-id="5110b-127">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/sftpconnector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="5110b-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="5110b-128">其他連接器</span><span class="sxs-lookup"><span data-stu-id="5110b-128">More connectors</span></span>
<span data-ttu-id="5110b-129">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="5110b-129">Go back to the [APIs list](apis-list.md).</span></span>