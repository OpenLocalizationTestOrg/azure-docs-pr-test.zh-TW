---
title: "aaaEncode 或解碼 Azure 邏輯應用程式中的一般檔案 |Microsoft 文件"
description: "如何 toouse hello 檔案檔案編碼器或解碼器在邏輯應用程式中的 hello 企業版整合套件"
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
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a><span data-ttu-id="4721f-103">企業與一般檔案整合概觀</span><span class="sxs-lookup"><span data-stu-id="4721f-103">Overview of enterprise integration with flat files</span></span>

<span data-ttu-id="4721f-104">然後再傳送 tooa 協力廠商企業對企業 (B2B) 案例中的，您可能想 tooencode XML 內容。</span><span class="sxs-lookup"><span data-stu-id="4721f-104">You may want tooencode XML content before you send it tooa business partner in a business-to-business (B2B) scenario.</span></span> <span data-ttu-id="4721f-105">在邏輯應用程式中，您可以使用這編碼連接器 toodo hello 一般檔案。</span><span class="sxs-lookup"><span data-stu-id="4721f-105">In a logic app, you can use hello flat file encoding connector toodo this.</span></span> <span data-ttu-id="4721f-106">hello 您所建立的邏輯應用程式可以取得其 XML 內容從各種來源，包括從 HTTP 要求的觸發程序、 從另一個應用程式，或甚至是從一個 hello 許多[連接器](../connectors/apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="4721f-106">hello logic app that you create can get its XML content from a variety of sources, including from an HTTP request trigger, from another application, or even from one of hello many [connectors](../connectors/apis-list.md).</span></span> <span data-ttu-id="4721f-107">如需邏輯應用程式的詳細資訊，請參閱 hello[邏輯應用程式文件](logic-apps-what-are-logic-apps.md "深入了解 Logic apps")。</span><span class="sxs-lookup"><span data-stu-id="4721f-107">For more information about logic apps, see hello [logic apps documentation](logic-apps-what-are-logic-apps.md "Learn more about Logic apps").</span></span>  

## <a name="create-hello-flat-file-encoding-connector"></a><span data-ttu-id="4721f-108">建立 hello 一般檔案編碼連接器</span><span class="sxs-lookup"><span data-stu-id="4721f-108">Create hello flat file encoding connector</span></span>
<span data-ttu-id="4721f-109">請遵循這些步驟 tooadd 編碼連接器 tooyour 邏輯應用程式的一般檔案。</span><span class="sxs-lookup"><span data-stu-id="4721f-109">Follow these steps tooadd a flat file encoding connector tooyour logic app.</span></span>

1. <span data-ttu-id="4721f-110">建立邏輯應用程式和[tooyour 整合帳戶連結到](logic-apps-enterprise-integration-accounts.md "toolink 整合帳戶 tooa 邏輯應用程式了解")。</span><span class="sxs-lookup"><span data-stu-id="4721f-110">Create a logic app and [link it tooyour integration account](logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app").</span></span> <span data-ttu-id="4721f-111">此帳戶包含您將使用 tooencode hello XML 資料的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="4721f-111">This account contains hello schema you will use tooencode hello XML data.</span></span>  
2. <span data-ttu-id="4721f-112">新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="4721f-112">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>  
   <span data-ttu-id="4721f-113">![觸發程序 tooselect 的螢幕擷取畫面](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="4721f-113">![Screenshot of trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
3. <span data-ttu-id="4721f-114">加入 hello 一般檔案編碼動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4721f-114">Add hello flat file encoding action, as follows:</span></span>
   
    <span data-ttu-id="4721f-115">a.</span><span class="sxs-lookup"><span data-stu-id="4721f-115">a.</span></span> <span data-ttu-id="4721f-116">選取 hello**加上**符號。</span><span class="sxs-lookup"><span data-stu-id="4721f-116">Select hello **plus** sign.</span></span>
   
    <span data-ttu-id="4721f-117">b.</span><span class="sxs-lookup"><span data-stu-id="4721f-117">b.</span></span> <span data-ttu-id="4721f-118">選取 hello**將動作加入**（會顯示您選取加號 hello 之後） 的連結。</span><span class="sxs-lookup"><span data-stu-id="4721f-118">Select hello **Add an action** link (appears after you have selected hello plus sign).</span></span>
   
    <span data-ttu-id="4721f-119">c.</span><span class="sxs-lookup"><span data-stu-id="4721f-119">c.</span></span> <span data-ttu-id="4721f-120">在 [hello] 搜尋方塊中，輸入*一般*toofilter 所有 hello 動作 toohello 其中一個要 toouse。</span><span class="sxs-lookup"><span data-stu-id="4721f-120">In hello search box, enter *Flat* toofilter all hello actions toohello one that you want toouse.</span></span>
   
    <span data-ttu-id="4721f-121">d.</span><span class="sxs-lookup"><span data-stu-id="4721f-121">d.</span></span> <span data-ttu-id="4721f-122">選取 hello**一般檔案編碼方式**hello 清單中的選項。</span><span class="sxs-lookup"><span data-stu-id="4721f-122">Select hello **Flat File Encoding** option from hello list.</span></span>   
   <span data-ttu-id="4721f-123">![一般檔案編碼選項的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="4721f-123">![Screenshot of Flat File Encoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
4. <span data-ttu-id="4721f-124">在 hello**一般檔案編碼方式**對話方塊中，選取 hello**內容**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4721f-124">On hello **Flat File Encoding** dialog box, select hello **Content** text box.</span></span>  
   <span data-ttu-id="4721f-125">![內容文字方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span><span class="sxs-lookup"><span data-stu-id="4721f-125">![Screenshot of Content text box](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span></span>  
5. <span data-ttu-id="4721f-126">選取要作為內容的 tooencode hello hello body 標記。</span><span class="sxs-lookup"><span data-stu-id="4721f-126">Select hello body tag as hello content that you want tooencode.</span></span> <span data-ttu-id="4721f-127">hello body 標記將會填入 hello 內容 欄位。</span><span class="sxs-lookup"><span data-stu-id="4721f-127">hello body tag will populate hello content field.</span></span>     
   ![內文標記的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. <span data-ttu-id="4721f-129">選取 hello**結構描述名稱**清單方塊中，，然後選擇您想要 toouse tooencode hello hello 結構描述輸入內容。</span><span class="sxs-lookup"><span data-stu-id="4721f-129">Select hello **Schema Name** list box, and choose hello schema you want toouse tooencode hello input content.</span></span>    
   <span data-ttu-id="4721f-130">![結構描述名稱清單方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span><span class="sxs-lookup"><span data-stu-id="4721f-130">![Screenshot of Schema Name list box](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span></span>  
7. <span data-ttu-id="4721f-131">儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="4721f-131">Save your work.</span></span>   
   ![儲存圖示的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

<span data-ttu-id="4721f-133">此時，您已完成設定一般檔案編碼連接器。</span><span class="sxs-lookup"><span data-stu-id="4721f-133">At this point, you are finished setting up your flat file encoding connector.</span></span> <span data-ttu-id="4721f-134">在真實世界應用程式中，您可能想在特定業務應用程式，例如 Salesforce toostore hello 編碼資料。</span><span class="sxs-lookup"><span data-stu-id="4721f-134">In a real world application, you may want toostore hello encoded data in a line-of-business application, such as Salesforce.</span></span> <span data-ttu-id="4721f-135">或者，您可以傳送該交易夥伴的編碼的資料 tooa。</span><span class="sxs-lookup"><span data-stu-id="4721f-135">Or you can send that encoded data tooa trading partner.</span></span> <span data-ttu-id="4721f-136">您可以輕鬆加入動作 toosend hello 的 hello 輸出編碼方式使用任何一個 hello 的動作 tooSalesforce 或 tooyour 交易夥伴，提供其他連接器。</span><span class="sxs-lookup"><span data-stu-id="4721f-136">You can easily add an action toosend hello output of hello encoding action tooSalesforce, or tooyour trading partner, by using any one of hello other connectors provided.</span></span>

<span data-ttu-id="4721f-137">您現在可以測試您的連接器的要求 toohello HTTP 結束點，包括 hello hello 要求主體中的 hello XML 內容。</span><span class="sxs-lookup"><span data-stu-id="4721f-137">You can now test your connector by making a request toohello HTTP endpoint, and including hello XML content in hello body of hello request.</span></span>  

## <a name="create-hello-flat-file-decoding-connector"></a><span data-ttu-id="4721f-138">建立 hello 解碼連接器的一般檔案</span><span class="sxs-lookup"><span data-stu-id="4721f-138">Create hello flat file decoding connector</span></span>

> [!NOTE]
> <span data-ttu-id="4721f-139">toocomplete 這些步驟，您需要的 toohave 結構描述檔案已上傳到您整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="4721f-139">toocomplete these steps, you need toohave a schema file already uploaded into you integration account.</span></span>

1. <span data-ttu-id="4721f-140">新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="4721f-140">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>  
   <span data-ttu-id="4721f-141">![觸發程序 tooselect 的螢幕擷取畫面](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="4721f-141">![Screenshot of trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
2. <span data-ttu-id="4721f-142">加入 hello 一般檔案解碼動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4721f-142">Add hello flat file decoding action, as follows:</span></span>
   
    <span data-ttu-id="4721f-143">a.</span><span class="sxs-lookup"><span data-stu-id="4721f-143">a.</span></span> <span data-ttu-id="4721f-144">選取 hello**加上**符號。</span><span class="sxs-lookup"><span data-stu-id="4721f-144">Select hello **plus** sign.</span></span>
   
    <span data-ttu-id="4721f-145">b.</span><span class="sxs-lookup"><span data-stu-id="4721f-145">b.</span></span> <span data-ttu-id="4721f-146">選取 hello**將動作加入**（會顯示您選取加號 hello 之後） 的連結。</span><span class="sxs-lookup"><span data-stu-id="4721f-146">Select hello **Add an action** link (appears after you have selected hello plus sign).</span></span>
   
    <span data-ttu-id="4721f-147">c.</span><span class="sxs-lookup"><span data-stu-id="4721f-147">c.</span></span> <span data-ttu-id="4721f-148">在 [hello] 搜尋方塊中，輸入*一般*toofilter 所有 hello 動作 toohello 其中一個要 toouse。</span><span class="sxs-lookup"><span data-stu-id="4721f-148">In hello search box, enter *Flat* toofilter all hello actions toohello one that you want toouse.</span></span>
   
    <span data-ttu-id="4721f-149">d.</span><span class="sxs-lookup"><span data-stu-id="4721f-149">d.</span></span> <span data-ttu-id="4721f-150">選取 hello**一般檔案解碼**hello 清單中的選項。</span><span class="sxs-lookup"><span data-stu-id="4721f-150">Select hello **Flat File Decoding** option from hello list.</span></span>   
   <span data-ttu-id="4721f-151">![一般檔案解碼選項的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="4721f-151">![Screenshot of Flat File Decoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
3. <span data-ttu-id="4721f-152">選取 hello**內容**控制項。</span><span class="sxs-lookup"><span data-stu-id="4721f-152">Select hello **Content** control.</span></span> <span data-ttu-id="4721f-153">這會產生從先前的步驟，可作為 hello 內容 toodecode hello 內容的清單。</span><span class="sxs-lookup"><span data-stu-id="4721f-153">This produces a list of hello content from earlier steps that you can use as hello content toodecode.</span></span> <span data-ttu-id="4721f-154">請注意該 hello*主體*hello 從傳入的 HTTP 要求是做為 hello 內容 toodecode 可用 toobe。</span><span class="sxs-lookup"><span data-stu-id="4721f-154">Notice that hello *Body* from hello incoming HTTP request is available toobe used as hello content toodecode.</span></span> <span data-ttu-id="4721f-155">您也可以直接在 hello 輸入 hello 內容 toodecode**內容**控制項。</span><span class="sxs-lookup"><span data-stu-id="4721f-155">You can also enter hello content toodecode directly into hello **Content** control.</span></span>     
4. <span data-ttu-id="4721f-156">選取 hello*主體*標記。</span><span class="sxs-lookup"><span data-stu-id="4721f-156">Select hello *Body* tag.</span></span> <span data-ttu-id="4721f-157">請注意 hello body 標記已在 hello**內容**控制項。</span><span class="sxs-lookup"><span data-stu-id="4721f-157">Notice hello body tag is now in hello **Content** control.</span></span>
5. <span data-ttu-id="4721f-158">選取 hello hello 想 toouse toodecode hello 內容的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="4721f-158">Select hello name of hello schema that you want toouse toodecode hello content.</span></span> <span data-ttu-id="4721f-159">hello 下列螢幕擷取畫面顯示*OrderFile* hello 選取的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="4721f-159">hello following screenshot shows that *OrderFile* is hello selected schema name.</span></span> <span data-ttu-id="4721f-160">這個結構描述名稱已上傳到 hello 整合帳戶之前。</span><span class="sxs-lookup"><span data-stu-id="4721f-160">This schema name had been uploaded into hello integration account previously.</span></span>
   
   ![一般檔案解碼對話方塊的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. <span data-ttu-id="4721f-162">儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="4721f-162">Save your work.</span></span>  
   ![儲存圖示的螢幕擷取畫面](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

<span data-ttu-id="4721f-164">此時，您已完成設定一般檔案解碼連接器。</span><span class="sxs-lookup"><span data-stu-id="4721f-164">At this point, you are finished setting up your flat file decoding connector.</span></span> <span data-ttu-id="4721f-165">在真實世界應用程式中，您可能想在特定業務應用程式，例如 Salesforce toostore hello 已解碼的資料。</span><span class="sxs-lookup"><span data-stu-id="4721f-165">In a real world application, you may want toostore hello decoded data in a line-of-business application such as Salesforce.</span></span> <span data-ttu-id="4721f-166">您可以輕鬆加入動作 toosend hello 輸出的解碼動作 tooSalesforce hello。</span><span class="sxs-lookup"><span data-stu-id="4721f-166">You can easily add an action toosend hello output of hello decoding action tooSalesforce.</span></span>

<span data-ttu-id="4721f-167">您現在可以藉由要求 toohello HTTP 端點來測試您的連接器，且想 hello XML 內容包括 toodecode hello hello 要求主體中。</span><span class="sxs-lookup"><span data-stu-id="4721f-167">You can now test your connector by making a request toohello HTTP endpoint and including hello XML content you want toodecode in hello body of hello request.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4721f-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4721f-168">Next steps</span></span>
* <span data-ttu-id="4721f-169">[深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")。</span><span class="sxs-lookup"><span data-stu-id="4721f-169">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack").</span></span>  

