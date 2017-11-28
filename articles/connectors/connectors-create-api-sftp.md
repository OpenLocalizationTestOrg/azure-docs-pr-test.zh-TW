---
title: "aaaLearn toouse hello SFTP 連接器邏輯應用程式中的方式 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooSFTP API toosend 及接收檔案。 您可以執行各種作業，例如建立、更新、取得或刪除檔案。"
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="b5eb2-105">開始使用 hello SFTP 連接器</span><span class="sxs-lookup"><span data-stu-id="b5eb2-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="b5eb2-106">使用 hello SFTP 連接器 tooaccess SFTP 帳戶 toosend 及接收檔案。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="b5eb2-107">您可以執行各種作業，例如建立、更新、取得或刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="b5eb2-108">toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="b5eb2-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="b5eb2-110">連接 tooSFTP</span><span class="sxs-lookup"><span data-stu-id="b5eb2-110">Connect tooSFTP</span></span>
<span data-ttu-id="b5eb2-111">邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="b5eb2-112">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="b5eb2-113">建立連接 tooSFTP</span><span class="sxs-lookup"><span data-stu-id="b5eb2-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="b5eb2-114">使用 SFTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b5eb2-114">Use an SFTP trigger</span></span>
<span data-ttu-id="b5eb2-115">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="b5eb2-116">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="b5eb2-117">在此範例中，hello **SFTP-時加入或修改檔案**觸發程序時，才能使用的 tooinitiate 邏輯應用程式工作流程檔案，加入或修改 SFTP 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="b5eb2-118">您也可以加入條件會檢查 hello hello 新增或修改檔案內容，而且如果其內容會指出它應該擷取使用 hello 內容之前，可以讓決策 tooextract hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="b5eb2-119">最後，新增動作 tooextract hello 檔案的內容，並置於 hello SFTP 伺服器上的資料夾中的 hello 擷取內容。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="b5eb2-120">在企業範例中，您可以使用此觸發程序 toomonitor SFTP 資料夾代表客戶訂單的新檔案。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="b5eb2-121">您無法再使用 SFTP 連接器動作，例如**取得檔案內容**，進一步處理 」 和 「 訂單 」 資料庫中的儲存體的 hello 順序 tooget hello 內容。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="b5eb2-122">新增條件</span><span class="sxs-lookup"><span data-stu-id="b5eb2-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="b5eb2-123">使用 SFTP 動作</span><span class="sxs-lookup"><span data-stu-id="b5eb2-123">Use an SFTP action</span></span>
<span data-ttu-id="b5eb2-124">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="b5eb2-125">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="b5eb2-126">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="b5eb2-126">Connector-specific details</span></span>

<span data-ttu-id="b5eb2-127">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/sftpconnector/)。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="b5eb2-128">其他連接器</span><span class="sxs-lookup"><span data-stu-id="b5eb2-128">More connectors</span></span>
<span data-ttu-id="b5eb2-129">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="b5eb2-129">Go back toohello [APIs list](apis-list.md).</span></span>
