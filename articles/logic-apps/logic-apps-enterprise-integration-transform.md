---
title: "aaaConvert XML 資料轉換為 Azure 邏輯應用程式與 |Microsoft 文件"
description: "建立轉換或 mapps tooconvert 在邏輯應用程式中使用 hello 企業整合 SDK 的格式之間的 XML 資料"
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
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="40bb5-103">具備 XML 轉換的企業整合</span><span class="sxs-lookup"><span data-stu-id="40bb5-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="40bb5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="40bb5-104">Overview</span></span>
<span data-ttu-id="40bb5-105">hello 企業整合轉換連接器將資料轉換從一種格式 tooanother 格式。</span><span class="sxs-lookup"><span data-stu-id="40bb5-105">hello Enterprise integration Transform connector converts data from one format tooanother format.</span></span> <span data-ttu-id="40bb5-106">比方說，您可能包含目前的日期，格式為 hello YearMonthDay hello 內送訊息。</span><span class="sxs-lookup"><span data-stu-id="40bb5-106">For example, you may have an incoming message that contains hello current date in hello YearMonthDay format.</span></span> <span data-ttu-id="40bb5-107">您可以使用轉換 tooreformat hello 日期 toobe hello MonthDayYear 格式。</span><span class="sxs-lookup"><span data-stu-id="40bb5-107">You can use a transform tooreformat hello date toobe in hello MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="40bb5-108">轉換的作用為何？</span><span class="sxs-lookup"><span data-stu-id="40bb5-108">What does a transform do?</span></span>
<span data-ttu-id="40bb5-109">轉換就是所謂的對應，是由來源 XML 結構描述 (輸入 hello) 和目標的 XML 結構描述 （hello 輸出） 所組成。</span><span class="sxs-lookup"><span data-stu-id="40bb5-109">A Transform, which is also known as a map, consists of a Source XML schema (hello input) and a Target XML schema (hello output).</span></span> <span data-ttu-id="40bb5-110">您可以使用不同的內建函數 toohelp 操作，或控制 hello 資料，包括字串操作、 條件式指派、 算術運算式、 日期時間格式子，即使迴圈建構。</span><span class="sxs-lookup"><span data-stu-id="40bb5-110">You can use different built-in functions toohelp manipulate or control hello data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-toocreate-a-transform"></a><span data-ttu-id="40bb5-111">如何 toocreate 轉換嗎？</span><span class="sxs-lookup"><span data-stu-id="40bb5-111">How toocreate a transform?</span></span>
<span data-ttu-id="40bb5-112">您可以使用 hello Visual Studio，以建立轉換/對應[企業整合 SDK](https://aka.ms/vsmapsandschemas)。</span><span class="sxs-lookup"><span data-stu-id="40bb5-112">You can create a transform/map by using hello Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="40bb5-113">當您完成建立和測試 hello 轉換，您上傳到整合帳戶 hello 轉換。</span><span class="sxs-lookup"><span data-stu-id="40bb5-113">When you are finished creating and testing hello transform, you upload hello transform into your integration account.</span></span> 

## <a name="how-toouse-a-transform"></a><span data-ttu-id="40bb5-114">如何 toouse 轉換</span><span class="sxs-lookup"><span data-stu-id="40bb5-114">How toouse a transform</span></span>
<span data-ttu-id="40bb5-115">您將 hello 轉換/對應上傳到整合帳戶之後，您可以使用它 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="40bb5-115">After you upload hello transform/map into your integration account, you can use it toocreate a Logic app.</span></span> <span data-ttu-id="40bb5-116">hello 邏輯應用程式會執行轉換時，就會觸發 hello 邏輯應用程式 （和需要 toobe 轉換的輸入內容）。</span><span class="sxs-lookup"><span data-stu-id="40bb5-116">hello Logic app runs your transformations whenever hello Logic app is triggered (and there is input content that needs toobe transformed).</span></span>

<span data-ttu-id="40bb5-117">**以下是轉換 hello 步驟 toouse**:</span><span class="sxs-lookup"><span data-stu-id="40bb5-117">**Here are hello steps toouse a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="40bb5-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="40bb5-118">Prerequisites</span></span>

* <span data-ttu-id="40bb5-119">建立整合帳戶並新增地圖 tooit</span><span class="sxs-lookup"><span data-stu-id="40bb5-119">Create an integration account and add a map tooit</span></span>  

<span data-ttu-id="40bb5-120">既然您已經處理的 hello 必要元件，它是時間 toocreate 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="40bb5-120">Now that you've taken care of hello prerequisites, it's time toocreate your Logic app:</span></span>  

1. <span data-ttu-id="40bb5-121">建立邏輯應用程式和[tooyour 整合帳戶連結到](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 整合帳戶 tooa 邏輯應用程式了解")包含 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="40bb5-121">Create a Logic app and [link it tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that contains hello map.</span></span>
2. <span data-ttu-id="40bb5-122">新增**要求**觸發程序 tooyour 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="40bb5-122">Add a **Request** trigger tooyour Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="40bb5-123">新增 hello**轉換 XML**第一個選取的動作**加入的動作** </span><span class="sxs-lookup"><span data-stu-id="40bb5-123">Add hello **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="40bb5-124">輸入 hello 字*轉換*hello 搜尋方塊 toofilter 中所有 hello 動作 toohello 其中一個要 toouse</span><span class="sxs-lookup"><span data-stu-id="40bb5-124">Enter hello word *transform* in hello search box toofilter all hello actions toohello one that you want toouse</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="40bb5-125">選取 hello**轉換 XML**動作</span><span class="sxs-lookup"><span data-stu-id="40bb5-125">Select hello **Transform XML** action</span></span>   
6. <span data-ttu-id="40bb5-126">新增 hello XML**內容**您轉換。</span><span class="sxs-lookup"><span data-stu-id="40bb5-126">Add hello XML **CONTENT** that you transform.</span></span> <span data-ttu-id="40bb5-127">您可以使用任何您收到 hello 與 hello HTTP 要求中的 XML 資料**內容**。</span><span class="sxs-lookup"><span data-stu-id="40bb5-127">You can use any XML data you receive in hello HTTP request as hello **CONTENT**.</span></span> <span data-ttu-id="40bb5-128">在此範例中，選取 hello hello 觸發 hello 邏輯應用程式的 HTTP 要求主體。</span><span class="sxs-lookup"><span data-stu-id="40bb5-128">In this example, select hello body of hello HTTP request that triggered hello Logic app.</span></span>
7. <span data-ttu-id="40bb5-129">選取 hello 名稱 hello**對應**想要 toouse tooperform hello 轉換。</span><span class="sxs-lookup"><span data-stu-id="40bb5-129">Select hello name of hello **MAP** that you want toouse tooperform hello transformation.</span></span> <span data-ttu-id="40bb5-130">hello 對應必須已經是整合帳戶中。</span><span class="sxs-lookup"><span data-stu-id="40bb5-130">hello map must already be in your integration account.</span></span> <span data-ttu-id="40bb5-131">在先前步驟中，您已經為您的邏輯應用程式存取 tooyour 整合帳戶包含您的對應。</span><span class="sxs-lookup"><span data-stu-id="40bb5-131">In an earlier step, you already gave your Logic app access tooyour integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="40bb5-132">儲存您的工作 </span><span class="sxs-lookup"><span data-stu-id="40bb5-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="40bb5-133">此時，您已完成設定對應。</span><span class="sxs-lookup"><span data-stu-id="40bb5-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="40bb5-134">在真實世界應用程式中，您可能想 toostore hello 轉換資料，例如 SalesForce 的 LOB 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="40bb5-134">In a real world application, you may want toostore hello transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="40bb5-135">您可以輕鬆地為動作 toosend hello 輸出的 hello 轉換 tooSalesforce。</span><span class="sxs-lookup"><span data-stu-id="40bb5-135">You can easily as an action toosend hello output of hello transform tooSalesforce.</span></span> 

<span data-ttu-id="40bb5-136">您現在可以藉由要求 toohello HTTP 端點測試轉換。</span><span class="sxs-lookup"><span data-stu-id="40bb5-136">You can now test your transform by making a request toohello HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="40bb5-137">功能和使用案例</span><span class="sxs-lookup"><span data-stu-id="40bb5-137">Features and use cases</span></span>
* <span data-ttu-id="40bb5-138">建立在對應中的 hello 轉換可以很簡單，例如從一個文件 tooanother 複製名稱和地址。</span><span class="sxs-lookup"><span data-stu-id="40bb5-138">hello transformation created in a map can be simple, such as copying a name and address from one document tooanother.</span></span> <span data-ttu-id="40bb5-139">或者，您可以建立更複雜的轉換使用 hello 的方塊外對應作業。</span><span class="sxs-lookup"><span data-stu-id="40bb5-139">Or, you can create more complex transformations using hello out-of-the-box map operations.</span></span>  
* <span data-ttu-id="40bb5-140">目前有多個對應作業或函數可供使用，包括字串、日期時間函數等等。</span><span class="sxs-lookup"><span data-stu-id="40bb5-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="40bb5-141">您可以 hello 結構描述之間的直接資料複本。</span><span class="sxs-lookup"><span data-stu-id="40bb5-141">You can do a direct data copy between hello schemas.</span></span> <span data-ttu-id="40bb5-142">在對應工具包含在 hello SDK 中的 hello，這很簡單，只繪製一條線連接 hello hello 來源結構描述中的項目與其 hello 目的結構描述中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="40bb5-142">In hello Mapper included in hello SDK, this is as simple as drawing a line that connects hello elements in hello source schema with their counterparts in hello destination schema.</span></span>  
* <span data-ttu-id="40bb5-143">在建立對應時，您會檢視 hello 地圖，顯示所有 hello 關聯性和您所建立的連結的圖形表示法。</span><span class="sxs-lookup"><span data-stu-id="40bb5-143">When creating a map, you view a graphical representation of hello map, which shows all hello relationships and links you create.</span></span>
* <span data-ttu-id="40bb5-144">使用 hello 測試對應功能 tooadd 範例 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="40bb5-144">Use hello Test Map feature tooadd a sample XML message.</span></span> <span data-ttu-id="40bb5-145">簡單按一下滑鼠，您可以測試 hello 對應您建立，並查看 hello 產生輸出。</span><span class="sxs-lookup"><span data-stu-id="40bb5-145">With a simple click, you can test hello map you created, and see hello generated output.</span></span>  
* <span data-ttu-id="40bb5-146">上傳現有的對應</span><span class="sxs-lookup"><span data-stu-id="40bb5-146">Upload existing maps</span></span>  
* <span data-ttu-id="40bb5-147">包含 hello XML 格式的支援。</span><span class="sxs-lookup"><span data-stu-id="40bb5-147">Includes support for hello XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="40bb5-148">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="40bb5-148">Learn more</span></span>
* [<span data-ttu-id="40bb5-149">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="40bb5-149">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  
* [<span data-ttu-id="40bb5-150">深入了解對應</span><span class="sxs-lookup"><span data-stu-id="40bb5-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "了解企業整合對應")  

