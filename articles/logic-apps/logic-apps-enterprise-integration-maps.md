---
title: "使用 XSLT 對應-Azure Logic Apps aaaTransform XML |Microsoft 文件"
description: "加入 XSLT 對應 tootransform Azure 邏輯應用程式與 hello 企業版整合套件的 XML 資料"
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
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="d5b33-103">針對 XML 資料轉換新增對應</span><span class="sxs-lookup"><span data-stu-id="d5b33-103">Add maps for XML data transform</span></span>

<span data-ttu-id="d5b33-104">企業整合會使用對應 tootransform 格式之間的 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="d5b33-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="d5b33-105">對應是定義 hello 資料應該轉換成其他格式的文件中的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="d5b33-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="d5b33-106">為什麼要使用對應？</span><span class="sxs-lookup"><span data-stu-id="d5b33-106">Why use maps?</span></span>

<span data-ttu-id="d5b33-107">假設您定期 B2B 訂單或發票從接收的客戶使用 hello YYYMMDD 格式的日期。</span><span class="sxs-lookup"><span data-stu-id="d5b33-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="d5b33-108">不過，您的組織，在您儲存 hello MMDDYYY 格式的日期。</span><span class="sxs-lookup"><span data-stu-id="d5b33-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="d5b33-109">您也可以使用對應*轉換*hello MMDDYYY hello 訂單或發票詳細資料儲存在您的客戶活動資料庫之前 hello YYYMMDD 日期格式。</span><span class="sxs-lookup"><span data-stu-id="d5b33-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="d5b33-110">如何建立對應？</span><span class="sxs-lookup"><span data-stu-id="d5b33-110">How do I create a map?</span></span>

<span data-ttu-id="d5b33-111">您可以建立 BizTalk 整合專案以 hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 hello 企業版整合套件")for Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="d5b33-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="d5b33-112">接著，您可以建立整合對應檔案，以便以視覺方式對應兩個 XML 結構描述檔案中的項目。</span><span class="sxs-lookup"><span data-stu-id="d5b33-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="d5b33-113">建置此專案之後，您將擁有 XSLT 文件。</span><span class="sxs-lookup"><span data-stu-id="d5b33-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="d5b33-114">如何新增對應？</span><span class="sxs-lookup"><span data-stu-id="d5b33-114">How do I add a map?</span></span>

1. <span data-ttu-id="d5b33-115">在 hello Azure 入口網站，選取 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="d5b33-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="d5b33-116">在 hello 篩選搜尋方塊中，輸入**整合**，然後選取**整合帳戶**hello 結果清單中。</span><span class="sxs-lookup"><span data-stu-id="d5b33-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="d5b33-117">選取您想要 tooadd hello 對應 hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5b33-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="d5b33-118">選取 hello**對應**磚。</span><span class="sxs-lookup"><span data-stu-id="d5b33-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="d5b33-119">Hello 對應刀鋒視窗開啟後，請選擇**新增**。</span><span class="sxs-lookup"><span data-stu-id="d5b33-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="d5b33-120">在 [名稱] 中輸入對應的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5b33-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="d5b33-121">tooupload hello 對應檔案中，選擇右側 hello hello hello 資料夾圖示**對應**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="d5b33-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="d5b33-122">Hello 上傳程序完成之後，請選擇**確定**。</span><span class="sxs-lookup"><span data-stu-id="d5b33-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="d5b33-123">Azure 會新增 hello 對應 tooyour 整合帳戶之後，您會取得對應檔是否已加入或不會顯示在螢幕上訊息。</span><span class="sxs-lookup"><span data-stu-id="d5b33-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="d5b33-124">您會收到此訊息之後，請選擇 hello**對應**磚，使您可以檢視 hello 新加入的對應。</span><span class="sxs-lookup"><span data-stu-id="d5b33-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="d5b33-125">如何編輯對應？</span><span class="sxs-lookup"><span data-stu-id="d5b33-125">How do I edit a map?</span></span>

<span data-ttu-id="d5b33-126">您必須上傳新的對應檔具有您想要的 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="d5b33-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="d5b33-127">您可以先下載 hello 編輯對應。</span><span class="sxs-lookup"><span data-stu-id="d5b33-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="d5b33-128">tooupload 新的對應，以取代 hello 現有對應，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d5b33-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="d5b33-129">選擇 hello**對應**磚。</span><span class="sxs-lookup"><span data-stu-id="d5b33-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="d5b33-130">Hello 對應刀鋒視窗開啟後，請選取您想 tooedit hello 對應。</span><span class="sxs-lookup"><span data-stu-id="d5b33-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="d5b33-131">在 hello**對應**刀鋒視窗中，選擇**更新**。</span><span class="sxs-lookup"><span data-stu-id="d5b33-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="d5b33-132">在 hello 檔案選擇器中，選取 hello 對應檔案，tooupload，然後選取**開啟**。</span><span class="sxs-lookup"><span data-stu-id="d5b33-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="d5b33-133">如何 toodelete 對應嗎？</span><span class="sxs-lookup"><span data-stu-id="d5b33-133">How toodelete a map?</span></span>

1. <span data-ttu-id="d5b33-134">選擇 hello**對應**磚。</span><span class="sxs-lookup"><span data-stu-id="d5b33-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="d5b33-135">Hello 對應刀鋒視窗開啟之後，選取您想要 toodelete hello 對應。</span><span class="sxs-lookup"><span data-stu-id="d5b33-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="d5b33-136">選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d5b33-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="d5b33-137">確認您想 toodelete hello 對應。</span><span class="sxs-lookup"><span data-stu-id="d5b33-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="d5b33-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5b33-138">Next Steps</span></span>
* [<span data-ttu-id="d5b33-139">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d5b33-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  
* [<span data-ttu-id="d5b33-140">深入了解合約</span><span class="sxs-lookup"><span data-stu-id="d5b33-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  
* [<span data-ttu-id="d5b33-141">深入了解轉換</span><span class="sxs-lookup"><span data-stu-id="d5b33-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "了解企業整合轉換")  

