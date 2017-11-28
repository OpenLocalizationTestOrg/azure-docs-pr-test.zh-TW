---
title: "Azure 邏輯應用程式中的 aaaUse hello Slack 連接器 |Microsoft 文件"
description: "連接 tooSlack 邏輯應用程式中"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="3f9b5-103">開始使用 hello Slack 連接器</span><span class="sxs-lookup"><span data-stu-id="3f9b5-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="3f9b5-104">Slack 是團隊通訊工具，能把您團隊的通訊都集中在一個地方，讓您不但在何處都可使用，還能搜尋各項記錄。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="3f9b5-105">立即開始建立邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="3f9b5-106">建立連接 tooSlack</span><span class="sxs-lookup"><span data-stu-id="3f9b5-106">Create a connection tooSlack</span></span>
<span data-ttu-id="3f9b5-107">toouse hello Slack 連接器，您先建立**連接**然後提供這些屬性中的 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3f9b5-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="3f9b5-108">屬性</span><span class="sxs-lookup"><span data-stu-id="3f9b5-108">Property</span></span> | <span data-ttu-id="3f9b5-109">必要</span><span class="sxs-lookup"><span data-stu-id="3f9b5-109">Required</span></span> | <span data-ttu-id="3f9b5-110">說明</span><span class="sxs-lookup"><span data-stu-id="3f9b5-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f9b5-111">權杖</span><span class="sxs-lookup"><span data-stu-id="3f9b5-111">Token</span></span> |<span data-ttu-id="3f9b5-112">是</span><span class="sxs-lookup"><span data-stu-id="3f9b5-112">Yes</span></span> |<span data-ttu-id="3f9b5-113">提供 Slack 的認證</span><span class="sxs-lookup"><span data-stu-id="3f9b5-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="3f9b5-114">遵循這些步驟 toosign 到 Slack 和完整 hello hello Slack 設定**連接**邏輯應用程式中：</span><span class="sxs-lookup"><span data-stu-id="3f9b5-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="3f9b5-115">選取 [週期] </span><span class="sxs-lookup"><span data-stu-id="3f9b5-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="3f9b5-116">選取 [頻率] 並輸入 [間隔]</span><span class="sxs-lookup"><span data-stu-id="3f9b5-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="3f9b5-117">選取 [新增動作]</span><span class="sxs-lookup"><span data-stu-id="3f9b5-117">Select **Add an action**</span></span>  
   <span data-ttu-id="3f9b5-118">![設定 Slack][1]</span><span class="sxs-lookup"><span data-stu-id="3f9b5-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="3f9b5-119">Hello [搜尋] 方塊中輸入 Slack，並等候 hello 搜尋 tooreturn hello 名稱中在與 Slack 的所有項目</span><span class="sxs-lookup"><span data-stu-id="3f9b5-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="3f9b5-120">選取 [Slack - 張貼訊息] </span><span class="sxs-lookup"><span data-stu-id="3f9b5-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="3f9b5-121">選取**登入 tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="3f9b5-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="3f9b5-122">![設定 Slack][2]</span><span class="sxs-lookup"><span data-stu-id="3f9b5-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="3f9b5-123">提供您的 Slack 認證 toosign tooauthorize hello 應用程式中</span><span class="sxs-lookup"><span data-stu-id="3f9b5-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![設定 Slack][3]  
8. <span data-ttu-id="3f9b5-125">您將會重新導向的 tooyour 組織的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="3f9b5-126">**授權**Slack toointeract 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="3f9b5-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="3f9b5-127">![設定 Slack][5]</span><span class="sxs-lookup"><span data-stu-id="3f9b5-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="3f9b5-128">Hello 授權完成後，您應該重新導向的 tooyour 邏輯應用程式 toocomplete 它藉由設定 hello**延-取得所有訊息**> 一節。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="3f9b5-129">加入其他所需的觸發和動作。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="3f9b5-130">![設定 Slack][6]</span><span class="sxs-lookup"><span data-stu-id="3f9b5-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="3f9b5-131">儲存您的工作，藉由選取**儲存**hello 上方的功能表列上。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="3f9b5-132">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="3f9b5-132">Connector-specific details</span></span>

<span data-ttu-id="3f9b5-133">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/slack/)。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="3f9b5-134">其他連接器</span><span class="sxs-lookup"><span data-stu-id="3f9b5-134">More connectors</span></span>
<span data-ttu-id="3f9b5-135">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="3f9b5-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
