---
title: "aaaLearn toouse hello 邏輯應用程式中的 Twitter 連接器的方式 |Microsoft 文件"
description: "搭配 REST API 參數來使用 Twitter 連接器的概觀"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="8a2ae-103">開始使用 hello Twitter 連接器</span><span class="sxs-lookup"><span data-stu-id="8a2ae-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="8a2ae-104">您可以使用 hello Twitter 連接器：</span><span class="sxs-lookup"><span data-stu-id="8a2ae-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="8a2ae-105">張貼推文並取得推文</span><span class="sxs-lookup"><span data-stu-id="8a2ae-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="8a2ae-106">存取時間軸、好友和追隨者</span><span class="sxs-lookup"><span data-stu-id="8a2ae-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="8a2ae-107">執行中的 hello 任何其他動作，如下所述的觸發程序</span><span class="sxs-lookup"><span data-stu-id="8a2ae-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="8a2ae-108">toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="8a2ae-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="8a2ae-110">連接 tooTwitter</span><span class="sxs-lookup"><span data-stu-id="8a2ae-110">Connect tooTwitter</span></span>
<span data-ttu-id="8a2ae-111">邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="8a2ae-112">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="8a2ae-113">建立連接 tooTwitter</span><span class="sxs-lookup"><span data-stu-id="8a2ae-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="8a2ae-114">使用 Twitter 觸發程序</span><span class="sxs-lookup"><span data-stu-id="8a2ae-114">Use a Twitter trigger</span></span>
<span data-ttu-id="8a2ae-115">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="8a2ae-116">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="8a2ae-117">在此範例中，我將示範如何 toouse hello**新推文回傳時**觸發 #Seattle 的 toosearch，而如果找到 #Seattle，更新的檔案中 Dropbox hello 推文中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="8a2ae-118">在企業範例中，您無法搜尋 hello 您的公司名稱，並更新 hello 推文中的 hello 文字的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="8a2ae-119">輸入*twitter* hello hello 邏輯應用程式的設計工具上的搜尋方塊中然後選取 hello **Twitter-張貼新推文時**觸發程序</span><span class="sxs-lookup"><span data-stu-id="8a2ae-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="8a2ae-120">![Twitter 觸發程序圖 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="8a2ae-121">輸入*#Seattle*在 hello**搜尋文字**控制項</span><span class="sxs-lookup"><span data-stu-id="8a2ae-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="8a2ae-122">![Twitter 觸發程序圖 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="8a2ae-123">此時，應用程式邏輯已與其他觸發程序和 hello 工作流程中的動作會開始執行的 hello 的觸發程序設定。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="8a2ae-124">功能的邏輯應用程式 toobe，它必須包含至少一個觸發程序與一個動作。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="8a2ae-125">請遵循下一個區段 tooadd hello 動作中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="8a2ae-126">新增條件</span><span class="sxs-lookup"><span data-stu-id="8a2ae-126">Add a condition</span></span>
<span data-ttu-id="8a2ae-127">因為我們只感興趣的使用者與 50 個以上的使用者推文，條件，以確認 hello 實行項目數目必須先新增 toohello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="8a2ae-128">選取**+ 新增步驟**tooadd hello 動作您希望 tootake #Seattle 新推文中發現時</span><span class="sxs-lookup"><span data-stu-id="8a2ae-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="8a2ae-129">![Twitter 動作圖 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="8a2ae-130">選取 hello**加入條件**連結。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="8a2ae-131">![Twitter 條件圖 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="8a2ae-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="8a2ae-132">這會開啟 hello**條件**控制項，例如檢查條件*等於*，*是小於*，*大於*， *包含*等等。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="8a2ae-133">![Twitter 條件圖 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="8a2ae-134">選取 hello**選擇值**控制項。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="8a2ae-135">在此控制項中，您可以選取一或多個 hello 屬性從任何先前的動作或觸發程序做為其條件會評估的 tootrue 或 false 的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="8a2ae-136">![Twitter 條件圖 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="8a2ae-137">選取 hello **...** tooexpand hello 清單的內容，讓您可以查看所有可用的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="8a2ae-138">![Twitter 條件圖 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="8a2ae-139">選取 hello**實行項目計數**屬性。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="8a2ae-140">![Twitter 條件圖 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="8a2ae-141">請注意 hello 實行項目計數屬性現在位於 hello 值控制項。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Twitter 條件影像 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="8a2ae-143">選取**大於**從 hello 運算子清單。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="8a2ae-144">![Twitter 條件圖 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="8a2ae-145">輸入 50 hello 運算元 hello*大於*運算子。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="8a2ae-146">現在加入 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-146">hello condition is now added.</span></span> <span data-ttu-id="8a2ae-147">儲存工作使用 hello**儲存**上述 hello 功能表上的連結。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="8a2ae-148">![Twitter 條件圖 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="8a2ae-149">使用 Twitter 動作</span><span class="sxs-lookup"><span data-stu-id="8a2ae-149">Use a Twitter action</span></span>
<span data-ttu-id="8a2ae-150">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="8a2ae-151">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="8a2ae-152">既然您已加入觸發程序，請遵循這些步驟 tooadd 會公佈新推文中的 hello 推文 hello 觸發程序所找到的 hello 內容的動作。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="8a2ae-153">基於本逐步解說的 hello 將公佈使用者與 50 個以上的實行項目從的推文。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="8a2ae-154">在 hello 下一個步驟中，您將會公佈推文中使用某些 hello 屬性的每個推文中已有 50 個以上的實行項目之使用者所張貼在 Twitter 動作。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="8a2ae-155">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-155">Select **Add an action**.</span></span> <span data-ttu-id="8a2ae-156">這會開啟 hello 搜尋控制項，您可以搜尋其他動作和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="8a2ae-157">![Twitter 條件圖 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="8a2ae-158">輸入*twitter* hello 搜尋方塊中然後選取 hello **Twitter-張貼推文**動作。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="8a2ae-159">這會開啟 hello**張貼推文**控制您將在其中輸入 hello 推文中公佈的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="8a2ae-160">![Twitter 動作圖 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="8a2ae-161">選取 hello**推文提供文字**控制項。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="8a2ae-162">從上一個動作和 hello 邏輯應用程式中的觸發程序的所有輸出現在都是可見的。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="8a2ae-163">您可以選取其中任何，並將它們當做 hello 新推文中的 hello 推文中文字的一部分使用。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="8a2ae-164">![Twitter 動作圖 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="8a2ae-165">選取 [使用者名稱]</span><span class="sxs-lookup"><span data-stu-id="8a2ae-165">Select **User name**</span></span>   
5. <span data-ttu-id="8a2ae-166">輸入*指出：* hello 推文中的文字控制項中。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="8a2ae-167">在使用者名稱之後執行此動作。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="8a2ae-168">選取「推文文字」。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="8a2ae-169">![Twitter 動作圖 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="8a2ae-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="8a2ae-170">儲存您的工作，並傳送推文中的 hello #Seattle 雜湊標記 tooactivate 與您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="8a2ae-171">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="8a2ae-171">Connector-specific details</span></span>

<span data-ttu-id="8a2ae-172">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/twitterconnector/)。</span><span class="sxs-lookup"><span data-stu-id="8a2ae-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8a2ae-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a2ae-173">Next steps</span></span>
[<span data-ttu-id="8a2ae-174">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="8a2ae-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

