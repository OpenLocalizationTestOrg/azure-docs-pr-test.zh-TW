---
title: "使用 XSLT 對應來轉換 XML - Azure Logic Apps | Microsoft Docs"
description: "新增 XSLT 對應來轉換 XML 資料以搭配 Azure Logic Apps 與企業整合套件使用"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="28b73-103">針對 XML 資料轉換新增對應</span><span class="sxs-lookup"><span data-stu-id="28b73-103">Add maps for XML data transform</span></span>

<span data-ttu-id="28b73-104">企業整合會使用對應在各種格式之間轉換 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="28b73-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="28b73-105">對應是一份 XML 文件，可定義應該將文件中的哪些資料轉換成其他格式。</span><span class="sxs-lookup"><span data-stu-id="28b73-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="28b73-106">為什麼要使用對應？</span><span class="sxs-lookup"><span data-stu-id="28b73-106">Why use maps?</span></span>

<span data-ttu-id="28b73-107">假設您會定期收到客戶的 B2B 訂單或發票，而該客戶使用 YYYMMDD 格式的日期。</span><span class="sxs-lookup"><span data-stu-id="28b73-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="28b73-108">不過，在您的組織中，您是以 MMDDYYY 格式儲存日期。</span><span class="sxs-lookup"><span data-stu-id="28b73-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="28b73-109">您可以使用對應，先將 YYYMMDD 日期格式*轉換*為 MMDDYYY，然後再將訂單或發票儲存於客戶活動資料庫中。</span><span class="sxs-lookup"><span data-stu-id="28b73-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="28b73-110">如何建立對應？</span><span class="sxs-lookup"><span data-stu-id="28b73-110">How do I create a map?</span></span>

<span data-ttu-id="28b73-111">您可以使用適用於 Visual Studio 2015 的[企業整合套件](logic-apps-enterprise-integration-overview.md "了解企業整合套件")來建立 BizTalk 整合專案。</span><span class="sxs-lookup"><span data-stu-id="28b73-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="28b73-112">接著，您可以建立整合對應檔案，以便以視覺方式對應兩個 XML 結構描述檔案中的項目。</span><span class="sxs-lookup"><span data-stu-id="28b73-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="28b73-113">建置此專案之後，您將擁有 XSLT 文件。</span><span class="sxs-lookup"><span data-stu-id="28b73-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="28b73-114">如何新增對應？</span><span class="sxs-lookup"><span data-stu-id="28b73-114">How do I add a map?</span></span>

1. <span data-ttu-id="28b73-115">在 Azure 入口網站中，選取 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="28b73-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="28b73-116">在篩選搜尋方塊中輸入**整合**，然後從結果清單選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="28b73-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="28b73-117">選取要將對應新增到其中的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="28b73-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="28b73-118">選取 [對應] 圖格。</span><span class="sxs-lookup"><span data-stu-id="28b73-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="28b73-119">在 [對應] 刀鋒視窗開啟之後，選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="28b73-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="28b73-120">在 [名稱] 中輸入對應的名稱。</span><span class="sxs-lookup"><span data-stu-id="28b73-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="28b73-121">若要上傳對應檔案，請選擇 [對應] 文字方塊右邊的資料夾圖示。</span><span class="sxs-lookup"><span data-stu-id="28b73-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="28b73-122">上傳程序完成之後，請選擇 [確定]。</span><span class="sxs-lookup"><span data-stu-id="28b73-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="28b73-123">在 Azure 將您的對應新增到您的整合帳戶之後，您會看到螢幕上出現一個訊息，該訊息說明您的對應檔案是否已新增。</span><span class="sxs-lookup"><span data-stu-id="28b73-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="28b73-124">取得此訊息之後，請選擇 [對應]**Maps** 圖格，以便檢視新增的對應。</span><span class="sxs-lookup"><span data-stu-id="28b73-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="28b73-125">如何編輯對應？</span><span class="sxs-lookup"><span data-stu-id="28b73-125">How do I edit a map?</span></span>

<span data-ttu-id="28b73-126">您必須上傳具有您要之變更的新對應檔案。</span><span class="sxs-lookup"><span data-stu-id="28b73-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="28b73-127">您可以先下載對應以進行編輯。</span><span class="sxs-lookup"><span data-stu-id="28b73-127">You can first download the map for editing.</span></span>

<span data-ttu-id="28b73-128">若要上傳將取代現有對應的新對應，請依照這些步驟執行。</span><span class="sxs-lookup"><span data-stu-id="28b73-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="28b73-129">選擇 [對應] 圖格。</span><span class="sxs-lookup"><span data-stu-id="28b73-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="28b73-130">在 [對應] 刀鋒視窗開啟之後，選取您要編輯的對應。</span><span class="sxs-lookup"><span data-stu-id="28b73-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="28b73-131">在 [對應] 刀鋒視窗上，選擇 [更新]。</span><span class="sxs-lookup"><span data-stu-id="28b73-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="28b73-132">在檔案選擇器中，選取您要上傳的對應檔案，然後選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="28b73-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="28b73-133">如何刪除對應？</span><span class="sxs-lookup"><span data-stu-id="28b73-133">How to delete a map?</span></span>

1. <span data-ttu-id="28b73-134">選擇 [對應] 圖格。</span><span class="sxs-lookup"><span data-stu-id="28b73-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="28b73-135">在 [對應] 刀鋒視窗開啟之後，選取您要刪除的對應。</span><span class="sxs-lookup"><span data-stu-id="28b73-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="28b73-136">選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="28b73-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="28b73-137">確認您要刪除該對應。</span><span class="sxs-lookup"><span data-stu-id="28b73-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="28b73-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28b73-138">Next Steps</span></span>
* [<span data-ttu-id="28b73-139">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="28b73-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "了解企業整合套件")  
* [<span data-ttu-id="28b73-140">深入了解合約</span><span class="sxs-lookup"><span data-stu-id="28b73-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  
* [<span data-ttu-id="28b73-141">深入了解轉換</span><span class="sxs-lookup"><span data-stu-id="28b73-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "了解企業整合轉換")  

