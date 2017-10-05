---
title: "XML 驗證的結構描述 - Azure Logic Apps | Microsoft Docs"
description: "使用適用於 Azure Logic Apps 與企業整合套件的結構描述來驗證 XML 文件"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="fad9a-103">使用適用於 Azure Logic Apps 與企業整合套件的結構描述來驗證 XML</span><span class="sxs-lookup"><span data-stu-id="fad9a-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="fad9a-104">結構描述可確認您收到的 XML 文件都有效，而且包含具有預先定義格式的預期資料。</span><span class="sxs-lookup"><span data-stu-id="fad9a-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="fad9a-105">結構描述也可用來驗證在 B2B 案例中交換的訊息。</span><span class="sxs-lookup"><span data-stu-id="fad9a-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="fad9a-106">新增結構描述</span><span class="sxs-lookup"><span data-stu-id="fad9a-106">Add a schema</span></span>

1. <span data-ttu-id="fad9a-107">在 Azure 入口網站中，選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-107">In the Azure portal, select **More services**.</span></span>

    ![Azure 入口網站，[更多服務]](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="fad9a-109">在篩選搜尋方塊中輸入**整合**，然後從結果清單中選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![篩選搜尋方塊](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="fad9a-111">選取要在其中新增結構描述的**整合帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fad9a-111">Select the **integration account** where you want to add the schema.</span></span>

    ![整合帳戶清單](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="fad9a-113">選擇 [結構描述] 圖格。</span><span class="sxs-lookup"><span data-stu-id="fad9a-113">Choose the **Schemas** tile.</span></span>

    ![範例整合帳戶 "Schemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="fad9a-115">新增小於 2 MB 的結構描述檔案</span><span class="sxs-lookup"><span data-stu-id="fad9a-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="fad9a-116">在開啟的 [結構描述] 刀鋒視窗中 (從先前的步驟)，選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![[結構描述] 刀鋒視窗，[新增]](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="fad9a-118">輸入結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="fad9a-118">Enter a name for your schema.</span></span> <span data-ttu-id="fad9a-119">選取 [結構描述] 方塊旁的資料夾圖示以上傳結構描述檔案。</span><span class="sxs-lookup"><span data-stu-id="fad9a-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="fad9a-120">上傳程序完成之後，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-120">After the upload process completes, select **OK**.</span></span>

    ![[新增結構描述] 的螢幕擷取畫面，反白顯示了 [小型檔案]](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="fad9a-122">新增大於 2 MB 的結構描述檔案 (最大 8 MB)</span><span class="sxs-lookup"><span data-stu-id="fad9a-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="fad9a-123">這些步驟視 Blob 容器存取層級而異：[公開] 或 [無匿名存取]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="fad9a-124">**判斷此存取層級**</span><span class="sxs-lookup"><span data-stu-id="fad9a-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="fad9a-125">開啟 [Azure 儲存體總管]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="fad9a-126">在 [Blob 容器] 下，選取您要的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="fad9a-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="fad9a-127">選取 [安全性]、[存取層級]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="fad9a-128">如果 blob 安全性存取層級為**公用**，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fad9a-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Azure 儲存體總管，已反白選取 [Blob 容器]、[安全性] 與 [公開]](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="fad9a-130">將結構描述上傳至儲存體帳戶，並複製 URI。</span><span class="sxs-lookup"><span data-stu-id="fad9a-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![儲存體帳戶，已反白顯示 URI](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="fad9a-132">在 [新增結構描述] 中選取 [大型檔案]，然後在 [內容 URI] 文字方塊中提供 URI。</span><span class="sxs-lookup"><span data-stu-id="fad9a-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![[結構描述]，已反白顯示 [新增] 按鈕和 [大型檔案]](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="fad9a-134">如果 blob 安全性存取層級為**無匿名存取**，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fad9a-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure 儲存體總管，已反白顯示 [Blob 容器]、[安全性] 和 [無匿名存取]](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="fad9a-136">將結構描述上傳至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fad9a-136">Upload the schema to your storage account.</span></span>

    ![儲存體帳戶](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="fad9a-138">產生結構描述的共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="fad9a-138">Generate a shared access signature for the schema.</span></span>

    ![儲存體帳戶，已反白顯示 [共用存取簽章] 索引標籤](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="fad9a-140">在 [新增結構描述] 中選取 [大型檔案]，然後在 [內容 URI] 文字方塊中提供共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="fad9a-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![[結構描述]，已反白顯示 [新增] 按鈕和 [大型檔案]](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="fad9a-142">在整合帳戶的 [結構描述] 刀鋒視窗中，您現在應該會看到新增的結構描述。</span><span class="sxs-lookup"><span data-stu-id="fad9a-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![整合帳戶，已反白顯示 [結構描述] 和新的結構描述](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="fad9a-144">編輯結構描述</span><span class="sxs-lookup"><span data-stu-id="fad9a-144">Edit schemas</span></span>

1. <span data-ttu-id="fad9a-145">選擇 [結構描述] 圖格。</span><span class="sxs-lookup"><span data-stu-id="fad9a-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="fad9a-146">在 [結構描述] 刀鋒視窗開啟之後，選取您要編輯的結構描述。</span><span class="sxs-lookup"><span data-stu-id="fad9a-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="fad9a-147">在 [結構描述] 刀鋒視窗上，選擇 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![[結構描述] 刀鋒視窗](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="fad9a-149">選取您要編輯的結構描述檔案，然後選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![開啟要編輯的結構描述檔案](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="fad9a-151">Azure 會顯示訊息，說明結構描述已順利上傳。</span><span class="sxs-lookup"><span data-stu-id="fad9a-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="fad9a-152">刪除結構描述</span><span class="sxs-lookup"><span data-stu-id="fad9a-152">Delete schemas</span></span>

1. <span data-ttu-id="fad9a-153">選擇 [結構描述] 圖格。</span><span class="sxs-lookup"><span data-stu-id="fad9a-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="fad9a-154">在 [結構描述] 刀鋒視窗開啟之後，選取您要刪除的結構描述。</span><span class="sxs-lookup"><span data-stu-id="fad9a-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="fad9a-155">在 [結構描述] 刀鋒視窗上，選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![[結構描述] 刀鋒視窗](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="fad9a-157">若要確認您要刪除選取的結構描述，請選擇 [是]。</span><span class="sxs-lookup"><span data-stu-id="fad9a-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    ![[刪除結構描述] 確認訊息](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="fad9a-159">在 [結構描述] 刀鋒視窗中，結構描述清單會重新整理，而且已不再包含您刪除的結構描述。</span><span class="sxs-lookup"><span data-stu-id="fad9a-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![您的整合帳戶，已反白顯示 [結構描述]](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="fad9a-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fad9a-161">Next steps</span></span>
* <span data-ttu-id="fad9a-162">[深入了解企業整合套件](logic-apps-enterprise-integration-overview.md "了解企業整合套件")。</span><span class="sxs-lookup"><span data-stu-id="fad9a-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

