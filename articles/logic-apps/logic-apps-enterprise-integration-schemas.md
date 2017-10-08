---
title: "XML 驗證-Azure 邏輯應用程式的 aaaSchemas |Microsoft 文件"
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
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="aa20f-103">使用結構描述驗證 XML，為 Azure 邏輯應用程式與 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="aa20f-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="aa20f-104">結構描述確認收到 hello XML 文件都有效，而且有 hello 預期的資料中預先定義的格式。</span><span class="sxs-lookup"><span data-stu-id="aa20f-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="aa20f-105">結構描述也可用來驗證在 B2B 案例中交換的訊息。</span><span class="sxs-lookup"><span data-stu-id="aa20f-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="aa20f-106">新增結構描述</span><span class="sxs-lookup"><span data-stu-id="aa20f-106">Add a schema</span></span>

1. <span data-ttu-id="aa20f-107">在 hello Azure 入口網站，選取 **更多服務**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-107">In hello Azure portal, select **More services**.</span></span>

    ![Azure 入口網站，[更多服務]](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="aa20f-109">在 hello 篩選搜尋方塊中，輸入**整合**，然後選取**整合帳戶**hello 結果清單中。</span><span class="sxs-lookup"><span data-stu-id="aa20f-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![篩選搜尋方塊](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="aa20f-111">選取 hello**整合帳戶**想 tooadd hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="aa20f-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![整合帳戶清單](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="aa20f-113">選擇 hello**結構描述**磚。</span><span class="sxs-lookup"><span data-stu-id="aa20f-113">Choose hello **Schemas** tile.</span></span>

    ![範例整合帳戶 "Schemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="aa20f-115">新增小於 2 MB 的結構描述檔案</span><span class="sxs-lookup"><span data-stu-id="aa20f-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="aa20f-116">在 hello**結構描述**刀鋒視窗中開啟 （從 hello 先前步驟)，選擇**新增**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![[結構描述] 刀鋒視窗，[新增]](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="aa20f-118">輸入結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="aa20f-118">Enter a name for your schema.</span></span> <span data-ttu-id="aa20f-119">Hello 結構描述檔案上傳選取 hello 資料夾圖示的 下一步 toohello**結構描述**方塊。</span><span class="sxs-lookup"><span data-stu-id="aa20f-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="aa20f-120">Hello 上傳程序完成之後，請選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-120">After hello upload process completes, select **OK**.</span></span>

    ![[新增結構描述] 的螢幕擷取畫面，反白顯示了 [小型檔案]](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="aa20f-122">加入結構描述檔案超過 2 MB （向上 too8 MB 最大值）</span><span class="sxs-lookup"><span data-stu-id="aa20f-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="aa20f-123">這些步驟會有所不同 hello blob 容器的存取層級：**公用**或**沒有匿名存取**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="aa20f-124">**toodetermine 此存取層級**</span><span class="sxs-lookup"><span data-stu-id="aa20f-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="aa20f-125">開啟 [Azure 儲存體總管]。</span><span class="sxs-lookup"><span data-stu-id="aa20f-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="aa20f-126">在下**Blob 容器**，選取您想要的 hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="aa20f-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="aa20f-127">選取 [安全性]、[存取層級]。</span><span class="sxs-lookup"><span data-stu-id="aa20f-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="aa20f-128">如果 hello blob 安全性存取層級為**公用**，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="aa20f-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Azure 儲存體總管，已反白選取 [Blob 容器]、[安全性] 與 [公開]](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="aa20f-130">上傳 hello 結構描述 tooyour 儲存體帳戶，並複製 hello URI。</span><span class="sxs-lookup"><span data-stu-id="aa20f-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![儲存體帳戶，已反白顯示 URI](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="aa20f-132">在**新增結構描述**，選取**大型檔案**，並提供在 hello hello URI**內容 URI**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="aa20f-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![[結構描述]，已反白顯示 [新增] 按鈕和 [大型檔案]](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="aa20f-134">如果 hello blob 安全性存取層級為**沒有匿名存取**，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="aa20f-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure 儲存體總管，已反白顯示 [Blob 容器]、[安全性] 和 [無匿名存取]](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="aa20f-136">上傳 hello 結構描述 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa20f-136">Upload hello schema tooyour storage account.</span></span>

    ![儲存體帳戶](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="aa20f-138">產生 hello 結構描述的共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="aa20f-138">Generate a shared access signature for hello schema.</span></span>

    ![儲存體帳戶，已反白顯示 [共用存取簽章] 索引標籤](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="aa20f-140">在**新增結構描述**，選取**大型檔案**，並提供在 hello hello 共用的存取簽章 URI**內容 URI**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="aa20f-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![[結構描述]，已反白顯示 [新增] 按鈕和 [大型檔案]](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="aa20f-142">在 hello**結構描述**刀鋒視窗中的整合帳戶，您新增的結構描述應該會出現。</span><span class="sxs-lookup"><span data-stu-id="aa20f-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![您的 「 結構描述 」 和 hello 反白顯示的新結構描述的整合帳戶](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="aa20f-144">編輯結構描述</span><span class="sxs-lookup"><span data-stu-id="aa20f-144">Edit schemas</span></span>

1. <span data-ttu-id="aa20f-145">選擇 hello**結構描述**磚。</span><span class="sxs-lookup"><span data-stu-id="aa20f-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="aa20f-146">之後 hello**結構描述**刀鋒視窗隨即開啟，您想 tooedit 選取 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="aa20f-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="aa20f-147">在 hello**結構描述**刀鋒視窗中，選擇**編輯**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![[結構描述] 刀鋒視窗](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="aa20f-149">您想 tooedit，然後選取 選取 hello 結構描述檔案**開啟**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![開啟結構描述檔案 tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="aa20f-151">已成功上傳 azure 便會顯示訊息的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="aa20f-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="aa20f-152">刪除結構描述</span><span class="sxs-lookup"><span data-stu-id="aa20f-152">Delete schemas</span></span>

1. <span data-ttu-id="aa20f-153">選擇 hello**結構描述**磚。</span><span class="sxs-lookup"><span data-stu-id="aa20f-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="aa20f-154">之後 hello**結構描述**刀鋒視窗隨即開啟，您想要 toodelete 選取 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="aa20f-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="aa20f-155">在 hello**結構描述**刀鋒視窗中，選擇**刪除**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![[結構描述] 刀鋒視窗](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="aa20f-157">您想 toodelete hello tooconfirm 選取的結構描述中，選擇 **是**。</span><span class="sxs-lookup"><span data-stu-id="aa20f-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![[刪除結構描述] 確認訊息](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="aa20f-159">在 hello**結構描述**刀鋒視窗中，重新整理 hello 結構描述清單中，不再包含您所刪除的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="aa20f-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![您的整合帳戶，已反白顯示 [結構描述]](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="aa20f-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa20f-161">Next steps</span></span>
* <span data-ttu-id="aa20f-162">[深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 hello 企業版整合套件")。</span><span class="sxs-lookup"><span data-stu-id="aa20f-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

