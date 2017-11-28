---
title: "在 Azure Logic Apps 中編碼或解碼一般檔案 | Microsoft Docs"
description: "如何在您的邏輯應用程式中使用企業整合套件內的一般檔案編碼器或解碼器"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bc3430624844cdeb92958433fba295f67a8ae0ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a><span data-ttu-id="d14d5-103">企業與一般檔案整合概觀</span><span class="sxs-lookup"><span data-stu-id="d14d5-103">Overview of enterprise integration with flat files</span></span>

<span data-ttu-id="d14d5-104">在企業對企業 (B2B) 案例中，您可能會希望先將 XML 內容編碼，然後再傳送給企業夥伴。</span><span class="sxs-lookup"><span data-stu-id="d14d5-104">You may want to encode XML content before you send it to a business partner in a business-to-business (B2B) scenario.</span></span> <span data-ttu-id="d14d5-105">在邏輯應用程式中，您可以使用一般檔案編碼連接器來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="d14d5-105">In a logic app, you can use the flat file encoding connector to do this.</span></span> <span data-ttu-id="d14d5-106">您所建立的邏輯應用程式可從各種來源取得其 XML 內容，包括 HTTP 要求觸發程序、另一個應用程式，或甚至是這其中任一種 [連接器](../connectors/apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="d14d5-106">The logic app that you create can get its XML content from a variety of sources, including from an HTTP request trigger, from another application, or even from one of the many [connectors](../connectors/apis-list.md).</span></span> <span data-ttu-id="d14d5-107">如需邏輯應用程式的詳細資訊，請參閱[邏輯應用程式文件](logic-apps-what-are-logic-apps.md "深入了解 Logic Apps")。</span><span class="sxs-lookup"><span data-stu-id="d14d5-107">For more information about logic apps, see the [logic apps documentation](logic-apps-what-are-logic-apps.md "Learn more about Logic apps").</span></span>  

## <a name="create-the-flat-file-encoding-connector"></a><span data-ttu-id="d14d5-108">建立一般檔案編碼連接器</span><span class="sxs-lookup"><span data-stu-id="d14d5-108">Create the flat file encoding connector</span></span>
<span data-ttu-id="d14d5-109">請遵循下列步驟，將一般檔案編碼連接器新增到邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d14d5-109">Follow these steps to add a flat file encoding connector to your logic app.</span></span>

1. <span data-ttu-id="d14d5-110">建立邏輯應用程式，並[將它連結到您的整合帳戶](logic-apps-enterprise-integration-accounts.md "了解如何將整合帳戶連結到邏輯應用程式")。</span><span class="sxs-lookup"><span data-stu-id="d14d5-110">Create a logic app and [link it to your integration account](logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app").</span></span> <span data-ttu-id="d14d5-111">此帳戶包含您將用來編碼 XML 資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d14d5-111">This account contains the schema you will use to encode the XML data.</span></span>  
2. <span data-ttu-id="d14d5-112">將 [要求 - 收到 HTTP 要求時]  觸發程序新增到您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d14d5-112">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>  
   <span data-ttu-id="d14d5-113">![要選取之觸發程序的螢幕擷取畫面](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="d14d5-113">![Screenshot of trigger to select](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
3. <span data-ttu-id="d14d5-114">新增一般檔案編碼動作，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="d14d5-114">Add the flat file encoding action, as follows:</span></span>
   
    <span data-ttu-id="d14d5-115">a.</span><span class="sxs-lookup"><span data-stu-id="d14d5-115">a.</span></span> <span data-ttu-id="d14d5-116">選取**加號**。</span><span class="sxs-lookup"><span data-stu-id="d14d5-116">Select the **plus** sign.</span></span>
   
    <span data-ttu-id="d14d5-117">b.</span><span class="sxs-lookup"><span data-stu-id="d14d5-117">b.</span></span> <span data-ttu-id="d14d5-118">選取 [新增動作] 連結 (會在選取加號之後出現)。</span><span class="sxs-lookup"><span data-stu-id="d14d5-118">Select the **Add an action** link (appears after you have selected the plus sign).</span></span>
   
    <span data-ttu-id="d14d5-119">c.</span><span class="sxs-lookup"><span data-stu-id="d14d5-119">c.</span></span> <span data-ttu-id="d14d5-120">在搜尋方塊中輸入「一般」，篩選所有動作以取得您想要使用的動作。</span><span class="sxs-lookup"><span data-stu-id="d14d5-120">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span></span>
   
    <span data-ttu-id="d14d5-121">d.</span><span class="sxs-lookup"><span data-stu-id="d14d5-121">d.</span></span> <span data-ttu-id="d14d5-122">從清單中選取 [一般檔案編碼] 選項。</span><span class="sxs-lookup"><span data-stu-id="d14d5-122">Select the **Flat File Encoding** option from the list.</span></span>   
   <span data-ttu-id="d14d5-123">![一般檔案編碼選項的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="d14d5-123">![Screenshot of Flat File Encoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
4. <span data-ttu-id="d14d5-124">在 [一般檔案編碼] 對話方塊上選取 [內容] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="d14d5-124">On the **Flat File Encoding** dialog box, select the **Content** text box.</span></span>  
   <span data-ttu-id="d14d5-125">![內容文字方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span><span class="sxs-lookup"><span data-stu-id="d14d5-125">![Screenshot of Content text box](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span></span>  
5. <span data-ttu-id="d14d5-126">選取內文標記做為您想要編碼的內容。</span><span class="sxs-lookup"><span data-stu-id="d14d5-126">Select the body tag as the content that you want to encode.</span></span> <span data-ttu-id="d14d5-127">內文標記將會填入內容欄位。</span><span class="sxs-lookup"><span data-stu-id="d14d5-127">The body tag will populate the content field.</span></span>     
   ![內文標記的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. <span data-ttu-id="d14d5-129">選取 [結構描述名稱]  清單方塊，然後選擇您想要用來將輸入內容編碼的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d14d5-129">Select the **Schema Name** list box, and choose the schema you want to use to encode the input content.</span></span>    
   <span data-ttu-id="d14d5-130">![結構描述名稱清單方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span><span class="sxs-lookup"><span data-stu-id="d14d5-130">![Screenshot of Schema Name list box](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span></span>  
7. <span data-ttu-id="d14d5-131">儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="d14d5-131">Save your work.</span></span>   
   ![儲存圖示的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

<span data-ttu-id="d14d5-133">此時，您已完成設定一般檔案編碼連接器。</span><span class="sxs-lookup"><span data-stu-id="d14d5-133">At this point, you are finished setting up your flat file encoding connector.</span></span> <span data-ttu-id="d14d5-134">在真實世界應用程式中，您可能想要在企業營運應用程式 (例如 Salesforce) 中儲存已編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="d14d5-134">In a real world application, you may want to store the encoded data in a line-of-business application, such as Salesforce.</span></span> <span data-ttu-id="d14d5-135">或者，您也可以將該編碼資料傳送給交易夥伴。</span><span class="sxs-lookup"><span data-stu-id="d14d5-135">Or you can send that encoded data to a trading partner.</span></span> <span data-ttu-id="d14d5-136">您可以使用所提供的任一個其他連接器，輕鬆地新增動作來將編碼動作的輸出傳送到 Salesforce，或傳送給交易夥伴。</span><span class="sxs-lookup"><span data-stu-id="d14d5-136">You can easily add an action to send the output of the encoding action to Salesforce, or to your trading partner, by using any one of the other connectors provided.</span></span>

<span data-ttu-id="d14d5-137">您現在可以測試連接器，方法是向 HTTP 端點提出要求，並在要求內文中包含 XML 內容。</span><span class="sxs-lookup"><span data-stu-id="d14d5-137">You can now test your connector by making a request to the HTTP endpoint, and including the XML content in the body of the request.</span></span>  

## <a name="create-the-flat-file-decoding-connector"></a><span data-ttu-id="d14d5-138">建立一般檔案解碼連接器</span><span class="sxs-lookup"><span data-stu-id="d14d5-138">Create the flat file decoding connector</span></span>

> [!NOTE]
> <span data-ttu-id="d14d5-139">為了完成這些步驟，您必須已將結構描述檔案上傳到您的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="d14d5-139">To complete these steps, you need to have a schema file already uploaded into you integration account.</span></span>

1. <span data-ttu-id="d14d5-140">將 [要求 - 收到 HTTP 要求時]  觸發程序新增到您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d14d5-140">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>  
   <span data-ttu-id="d14d5-141">![要選取之觸發程序的螢幕擷取畫面](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="d14d5-141">![Screenshot of trigger to select](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
2. <span data-ttu-id="d14d5-142">新增一般檔案解碼動作，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="d14d5-142">Add the flat file decoding action, as follows:</span></span>
   
    <span data-ttu-id="d14d5-143">a.</span><span class="sxs-lookup"><span data-stu-id="d14d5-143">a.</span></span> <span data-ttu-id="d14d5-144">選取**加號**。</span><span class="sxs-lookup"><span data-stu-id="d14d5-144">Select the **plus** sign.</span></span>
   
    <span data-ttu-id="d14d5-145">b.</span><span class="sxs-lookup"><span data-stu-id="d14d5-145">b.</span></span> <span data-ttu-id="d14d5-146">選取 [新增動作] 連結 (會在選取加號之後出現)。</span><span class="sxs-lookup"><span data-stu-id="d14d5-146">Select the **Add an action** link (appears after you have selected the plus sign).</span></span>
   
    <span data-ttu-id="d14d5-147">c.</span><span class="sxs-lookup"><span data-stu-id="d14d5-147">c.</span></span> <span data-ttu-id="d14d5-148">在搜尋方塊中輸入「一般」，篩選所有動作以取得您想要使用的動作。</span><span class="sxs-lookup"><span data-stu-id="d14d5-148">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span></span>
   
    <span data-ttu-id="d14d5-149">d.</span><span class="sxs-lookup"><span data-stu-id="d14d5-149">d.</span></span> <span data-ttu-id="d14d5-150">從清單中選取 [一般檔案解碼] 選項。</span><span class="sxs-lookup"><span data-stu-id="d14d5-150">Select the **Flat File Decoding** option from the list.</span></span>   
   <span data-ttu-id="d14d5-151">![一般檔案解碼選項的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="d14d5-151">![Screenshot of Flat File Decoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
3. <span data-ttu-id="d14d5-152">選取 [內容]  控制項。</span><span class="sxs-lookup"><span data-stu-id="d14d5-152">Select the **Content** control.</span></span> <span data-ttu-id="d14d5-153">這會從先前步驟中產生一份內容清單，讓您可用來做為要解碼的內容。</span><span class="sxs-lookup"><span data-stu-id="d14d5-153">This produces a list of the content from earlier steps that you can use as the content to decode.</span></span> <span data-ttu-id="d14d5-154">請注意，來自傳入 HTTP 要求的「內文」  可用來做為要解碼的內容。</span><span class="sxs-lookup"><span data-stu-id="d14d5-154">Notice that the *Body* from the incoming HTTP request is available to be used as the content to decode.</span></span> <span data-ttu-id="d14d5-155">您也可以將要解碼的內容直接輸入於 [內容]  控制項中。</span><span class="sxs-lookup"><span data-stu-id="d14d5-155">You can also enter the content to decode directly into the **Content** control.</span></span>     
4. <span data-ttu-id="d14d5-156">選取 [內文]  標記。</span><span class="sxs-lookup"><span data-stu-id="d14d5-156">Select the *Body* tag.</span></span> <span data-ttu-id="d14d5-157">請注意，內文標記目前位於 [內容]  控制項中。</span><span class="sxs-lookup"><span data-stu-id="d14d5-157">Notice the body tag is now in the **Content** control.</span></span>
5. <span data-ttu-id="d14d5-158">選取您想要用來將內容解碼的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="d14d5-158">Select the name of the schema that you want to use to decode the content.</span></span> <span data-ttu-id="d14d5-159">下列螢幕擷取畫面顯示選取的結構描述名稱是「OrderFile」  。</span><span class="sxs-lookup"><span data-stu-id="d14d5-159">The following screenshot shows that *OrderFile* is the selected schema name.</span></span> <span data-ttu-id="d14d5-160">此結構描述名稱先前已上傳到整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="d14d5-160">This schema name had been uploaded into the integration account previously.</span></span>
   
   ![一般檔案解碼對話方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. <span data-ttu-id="d14d5-162">儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="d14d5-162">Save your work.</span></span>  
   ![儲存圖示的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

<span data-ttu-id="d14d5-164">此時，您已完成設定一般檔案解碼連接器。</span><span class="sxs-lookup"><span data-stu-id="d14d5-164">At this point, you are finished setting up your flat file decoding connector.</span></span> <span data-ttu-id="d14d5-165">在真實世界應用程式中，您可能想要在企業營運應用程式 (例如 Salesforce) 中儲存已解碼的資料。</span><span class="sxs-lookup"><span data-stu-id="d14d5-165">In a real world application, you may want to store the decoded data in a line-of-business application such as Salesforce.</span></span> <span data-ttu-id="d14d5-166">您可以輕鬆新增動作，來將解碼動作的輸出傳送到 Salesforce。</span><span class="sxs-lookup"><span data-stu-id="d14d5-166">You can easily add an action to send the output of the decoding action to Salesforce.</span></span>

<span data-ttu-id="d14d5-167">您現在可以測試連接器，方法是向 HTTP 端點提出要求，並在要求內文中包含您想要解碼的 XML 內容。</span><span class="sxs-lookup"><span data-stu-id="d14d5-167">You can now test your connector by making a request to the HTTP endpoint and including the XML content you want to decode in the body of the request.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d14d5-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d14d5-168">Next steps</span></span>
* <span data-ttu-id="d14d5-169">[深入了解企業整合套件](logic-apps-enterprise-integration-overview.md "了解企業整合套件")。</span><span class="sxs-lookup"><span data-stu-id="d14d5-169">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack").</span></span>  

