---
title: "使用轉換來轉換 XML 資料 - Azure Logic Apps | Microsoft Docs"
description: "在邏輯應用程式中使用企業整合 SDK 來建立轉換或對應，以轉換 XML 資料格式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="6d528-103">具備 XML 轉換的企業整合</span><span class="sxs-lookup"><span data-stu-id="6d528-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="6d528-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6d528-104">Overview</span></span>
<span data-ttu-id="6d528-105">企業整合轉換連接器會將資料從某種格式轉換成其他格式。</span><span class="sxs-lookup"><span data-stu-id="6d528-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="6d528-106">例如，傳入訊息中目前包含的日期是 YearMonthDay 格式。</span><span class="sxs-lookup"><span data-stu-id="6d528-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="6d528-107">您可以使用轉換，將日期重新格式化為 MonthDayYear 格式。</span><span class="sxs-lookup"><span data-stu-id="6d528-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="6d528-108">轉換的作用為何？</span><span class="sxs-lookup"><span data-stu-id="6d528-108">What does a transform do?</span></span>
<span data-ttu-id="6d528-109">轉換 (亦稱為對應) 由來源 XML 結構描述 (輸入) 和目標 XML 結構描述 (輸出) 所組成。</span><span class="sxs-lookup"><span data-stu-id="6d528-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="6d528-110">您可以利用不同的內建功能來操控或控制資料，包括字串操作、條件式協議、算術運算式、日期時間格式器，甚至迴圈建構。</span><span class="sxs-lookup"><span data-stu-id="6d528-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="6d528-111">如何建立轉換？</span><span class="sxs-lookup"><span data-stu-id="6d528-111">How to create a transform?</span></span>
<span data-ttu-id="6d528-112">您可以使用 Visual Studio [企業整合 SDK](https://aka.ms/vsmapsandschemas)來建立轉換/對應。</span><span class="sxs-lookup"><span data-stu-id="6d528-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="6d528-113">當您完成建立及測試轉換之後，可將轉換上傳到整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d528-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="6d528-114">如何使用轉換</span><span class="sxs-lookup"><span data-stu-id="6d528-114">How to use a transform</span></span>
<span data-ttu-id="6d528-115">當您將轉換/對應上傳到整合帳戶之後，您可以使用它來建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d528-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="6d528-116">每當觸發邏輯應用程式 (而且還有需要轉換的輸入內容) 時，邏輯應用程式接著便會執行您的轉換。</span><span class="sxs-lookup"><span data-stu-id="6d528-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="6d528-117">**以下是使用轉換的步驟**：</span><span class="sxs-lookup"><span data-stu-id="6d528-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6d528-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="6d528-118">Prerequisites</span></span>

* <span data-ttu-id="6d528-119">建立整合帳戶，並加入對應</span><span class="sxs-lookup"><span data-stu-id="6d528-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="6d528-120">既然您已完成必要元件，就可以建立邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="6d528-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="6d528-121">建立邏輯應用程式並[將它連結到包含對應的整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md "了解如何將整合帳戶連結到邏輯應用程式")。</span><span class="sxs-lookup"><span data-stu-id="6d528-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="6d528-122">將**要求**觸發程序新增至邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="6d528-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="6d528-123">先選取 [新增動作] 來新增 [轉換 XML] 動作 </span><span class="sxs-lookup"><span data-stu-id="6d528-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="6d528-124">在搜尋方塊中輸入「轉換」，篩選所有動作以取得您想要使用的動作</span><span class="sxs-lookup"><span data-stu-id="6d528-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="6d528-125">選取 [轉換 XML] 動作</span><span class="sxs-lookup"><span data-stu-id="6d528-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="6d528-126">新增您將轉換的 XML **內容**。</span><span class="sxs-lookup"><span data-stu-id="6d528-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="6d528-127">您可以使用在 HTTP 要求中收到的任何 XML 資料做為 **內容**。</span><span class="sxs-lookup"><span data-stu-id="6d528-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="6d528-128">在此範例中，選取觸發邏輯應用程式的 HTTP 要求本文。</span><span class="sxs-lookup"><span data-stu-id="6d528-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="6d528-129">選取您想要用來執行轉換的 **對應** 名稱。</span><span class="sxs-lookup"><span data-stu-id="6d528-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="6d528-130">對應必須已經位於您的整合帳戶中。</span><span class="sxs-lookup"><span data-stu-id="6d528-130">The map must already be in your integration account.</span></span> <span data-ttu-id="6d528-131">在先前步驟中，您已經為邏輯應用程式提供權限來存取包含對應的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d528-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="6d528-132">儲存您的工作 </span><span class="sxs-lookup"><span data-stu-id="6d528-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="6d528-133">此時，您已完成設定對應。</span><span class="sxs-lookup"><span data-stu-id="6d528-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="6d528-134">在真實世界應用程式中，您可能想要在 LOB 應用程式 (例如 SalesForce) 中儲存已轉換的資料。</span><span class="sxs-lookup"><span data-stu-id="6d528-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="6d528-135">您可以輕鬆新增動作，來將轉換的輸出傳送到 Salesforce。</span><span class="sxs-lookup"><span data-stu-id="6d528-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="6d528-136">您現在可以藉由向 HTTP 端點提出要求來測試轉換。</span><span class="sxs-lookup"><span data-stu-id="6d528-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="6d528-137">功能和使用案例</span><span class="sxs-lookup"><span data-stu-id="6d528-137">Features and use cases</span></span>
* <span data-ttu-id="6d528-138">在對應中建立轉換並不難，例如，只要在不同文件之間複製名稱和位址，即可完成。</span><span class="sxs-lookup"><span data-stu-id="6d528-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="6d528-139">或者，您可以使用內建的對應作業，建立更複雜的轉換。</span><span class="sxs-lookup"><span data-stu-id="6d528-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="6d528-140">目前有多個對應作業或函數可供使用，包括字串、日期時間函數等等。</span><span class="sxs-lookup"><span data-stu-id="6d528-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="6d528-141">您可以在結構描述間執行直接的資料複製。</span><span class="sxs-lookup"><span data-stu-id="6d528-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="6d528-142">在 SDK 內含的對應程式中，只要繪製一條線連接來源結構描述中的元素與其目的地結構描述中的對等項目，即可完成此動作。</span><span class="sxs-lookup"><span data-stu-id="6d528-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="6d528-143">建立對應時，您可以檢視圖形化對應，其中會顯示您所建立的所有關聯性和連結。</span><span class="sxs-lookup"><span data-stu-id="6d528-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="6d528-144">使用 [測試對應] 功能，以新增範例 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="6d528-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="6d528-145">只要按一下滑鼠，您即可測試已建立的對應，並檢視產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="6d528-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="6d528-146">上傳現有的對應</span><span class="sxs-lookup"><span data-stu-id="6d528-146">Upload existing maps</span></span>  
* <span data-ttu-id="6d528-147">包括對 XML 格式的支援。</span><span class="sxs-lookup"><span data-stu-id="6d528-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="6d528-148">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="6d528-148">Learn more</span></span>
* [<span data-ttu-id="6d528-149">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="6d528-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "了解企業整合套件")  
* [<span data-ttu-id="6d528-150">深入了解對應</span><span class="sxs-lookup"><span data-stu-id="6d528-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "了解企業整合對應")  

