---
title: "了解如何在邏輯應用程式中使用 Twitter 連接器 | Microsoft Docs"
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
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="b1ef0-103">開始使用 Twitter 連接器</span><span class="sxs-lookup"><span data-stu-id="b1ef0-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="b1ef0-104">使用 Twitter 連接器，您可以：</span><span class="sxs-lookup"><span data-stu-id="b1ef0-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="b1ef0-105">張貼推文並取得推文</span><span class="sxs-lookup"><span data-stu-id="b1ef0-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="b1ef0-106">存取時間軸、好友和追隨者</span><span class="sxs-lookup"><span data-stu-id="b1ef0-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="b1ef0-107">執行以下所述的任何其他動作和觸發程序</span><span class="sxs-lookup"><span data-stu-id="b1ef0-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="b1ef0-108">若要使用[任何連接器](apis-list.md)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="b1ef0-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="b1ef0-110">連接到 Twitter</span><span class="sxs-lookup"><span data-stu-id="b1ef0-110">Connect to Twitter</span></span>
<span data-ttu-id="b1ef0-111">您必須先建立與服務的連線，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="b1ef0-112">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="b1ef0-113">建立 Twitter 連線</span><span class="sxs-lookup"><span data-stu-id="b1ef0-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="b1ef0-114">使用 Twitter 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b1ef0-114">Use a Twitter trigger</span></span>
<span data-ttu-id="b1ef0-115">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="b1ef0-116">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="b1ef0-117">在此範例中，我將示範如何使用 [當有新推文張貼時] 觸發程序來搜尋 #Seattle，如果找到 #Seattle，就使用推文中的文字來更新 Dropbox 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="b1ef0-118">在企業範例中，您可以搜尋您的公司名稱，並以推文中的文字更新 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="b1ef0-119">在 Logic Apps 設計工具的搜尋方塊中輸入 *twitter*，然後選取 [Twitter - 當有新推文張貼時] 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b1ef0-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="b1ef0-120">![Twitter 觸發程序圖 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="b1ef0-121">在 [搜尋文字] 控制項中輸入 *#Seattle*</span><span class="sxs-lookup"><span data-stu-id="b1ef0-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="b1ef0-122">![Twitter 觸發程序圖 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="b1ef0-123">此時，邏輯應用程式已設有觸發程序，該觸發程序會開始執行工作流程中的其他觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="b1ef0-124">為了讓邏輯應用程式能正常運作，它必須包含至少一個觸發程序和一個動作。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="b1ef0-125">請依照下一節中的步驟新增動作。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="b1ef0-126">新增條件</span><span class="sxs-lookup"><span data-stu-id="b1ef0-126">Add a condition</span></span>
<span data-ttu-id="b1ef0-127">因為我們只對於有 50 個以上跟隨者的使用者的推文有興趣，所以必須先將確認追隨者數目的條件新增至邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="b1ef0-128">選取 [+ 新步驟] 來新增您想要在新推文中找到 #Seattle 時採取的動作</span><span class="sxs-lookup"><span data-stu-id="b1ef0-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="b1ef0-129">![Twitter 動作圖 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="b1ef0-130">選取 [新增條件] 連結。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="b1ef0-131">![Twitter 條件圖 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="b1ef0-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="b1ef0-132">這會開啟可供您檢查條件的 [條件] 控制項，例如「等於」、「小於」、「大於」、「包含」等等。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="b1ef0-133">![Twitter 條件圖 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="b1ef0-134">選取 [選擇值] 控制項。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="b1ef0-135">在此控制項中，您可以從任何先前的動作或觸發程序選取一或多個屬性，做為其條件會評估為 true 或 false 的值。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="b1ef0-136">![Twitter 條件圖 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="b1ef0-137">選取 [...] 展開屬性清單，以便查看所有的可用屬性。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="b1ef0-138">![Twitter 條件圖 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="b1ef0-139">選取 [粉絲計數] 屬性。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="b1ef0-140">![Twitter 條件圖 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="b1ef0-141">請注意，[粉絲計數] 屬性現在位於值控制項中。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Twitter 條件影像 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="b1ef0-143">從運算子清單選取 [大於]。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="b1ef0-144">![Twitter 條件圖 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="b1ef0-145">輸入 50 做為「大於」運算子的運算元。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="b1ef0-146">現已新增此條件。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-146">The condition is now added.</span></span> <span data-ttu-id="b1ef0-147">使用上方功能表的 [儲存] 連結來儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="b1ef0-148">![Twitter 條件圖 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="b1ef0-149">使用 Twitter 動作</span><span class="sxs-lookup"><span data-stu-id="b1ef0-149">Use a Twitter action</span></span>
<span data-ttu-id="b1ef0-150">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="b1ef0-151">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="b1ef0-152">您現已新增觸發程序，請遵循下列步驟來新增動作，該動作將會張貼包含觸發程序所找到之推文內容的新推文。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="b1ef0-153">基於本逐步解說的目的，只會張貼有 50 個以上跟隨者的使用者的推文。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="b1ef0-154">在下一個步驟中，您將新增 Twitter 動作，該動作將使用有 50 個以上跟隨者的使用者所張貼的每則推文的某些屬性來張貼推文。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="b1ef0-155">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-155">Select **Add an action**.</span></span> <span data-ttu-id="b1ef0-156">這會開啟搜尋控制項，您可以在其中搜尋其他動作和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="b1ef0-157">![Twitter 條件圖 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="b1ef0-158">在搜尋方塊中輸入 *twitter*，然後選取 [Twitter - 張貼推文] 動作。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="b1ef0-159">這會開啟 [張貼推文] 控制項，您將在其中輸入所張貼推文的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="b1ef0-160">![Twitter 動作圖 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="b1ef0-161">選取 [推文文字] 控制項。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="b1ef0-162">前述動作和觸發程序的所有輸出現在可顯示在邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="b1ef0-163">您可以選取上述任何輸出，並使用它們做為新推文的部分推文文字。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="b1ef0-164">![Twitter 動作圖 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="b1ef0-165">選取 [使用者名稱]</span><span class="sxs-lookup"><span data-stu-id="b1ef0-165">Select **User name**</span></span>   
5. <span data-ttu-id="b1ef0-166">在推文文字控制項中輸入「說：」。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="b1ef0-167">在使用者名稱之後執行此動作。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="b1ef0-168">選取「推文文字」。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="b1ef0-169">![Twitter 動作圖 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="b1ef0-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="b1ef0-170">儲存您的工作並傳送具有 #Seattle 雜湊標籤的推文，以啟動您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="b1ef0-171">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="b1ef0-171">Connector-specific details</span></span>

<span data-ttu-id="b1ef0-172">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/twitterconnector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="b1ef0-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b1ef0-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1ef0-173">Next steps</span></span>
[<span data-ttu-id="b1ef0-174">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b1ef0-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

