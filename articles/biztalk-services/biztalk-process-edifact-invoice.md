---
title: "教學課程：使用 Azure BizTalk 服務處理 EDIFACT 發票 | Microsoft Docs"
description: "如何 toocreate 並設定 hello 方塊連接器或應用程式開發介面應用程式在 Azure App Service 中的邏輯應用程式中使用"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a><span data-ttu-id="da181-103">教學課程：使用 Azure BizTalk 服務處理 EDIFACT 發票</span><span class="sxs-lookup"><span data-stu-id="da181-103">Tutorial: Process EDIFACT invoices using Azure BizTalk Services</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="da181-104">您可以使用 hello BizTalk 服務入口網站 tooconfigure 和部署 X12 和 EDIFACT 協議。</span><span class="sxs-lookup"><span data-stu-id="da181-104">You can use hello BizTalk Services Portal tooconfigure and deploy X12 and EDIFACT agreements.</span></span> <span data-ttu-id="da181-105">在本教學課程中，我們會探討如何 toocreate 交換的 EDIFACT 協議發票交易夥伴之間。</span><span class="sxs-lookup"><span data-stu-id="da181-105">In this tutorial, we look at how toocreate an EDIFACT agreement for exchanging invoices between trading partners.</span></span> <span data-ttu-id="da181-106">本教學課程描述端對端商務方案，內容涉及兩個交易夥伴，分別是 Northwind 和 Contoso，他們會交換 EDIFACT 訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-106">This tutorial is written around an end-to-end business solution involving two trading partners, Northwind and Contoso that exchange EDIFACT messages.</span></span>  

## <a name="sample-based-on-this-tutorial"></a><span data-ttu-id="da181-107">根據本教學課程所建立的範例</span><span class="sxs-lookup"><span data-stu-id="da181-107">Sample based on this tutorial</span></span>
<span data-ttu-id="da181-108">此教學課程以範例，**傳送 EDIFACT Invoices Using BizTalk Services**，也就是從 hello 可用 toodownload [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005)。</span><span class="sxs-lookup"><span data-stu-id="da181-108">This tutorial is written around a sample, **Sending EDIFACT Invoices Using BizTalk Services**, which is available toodownload from hello [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005).</span></span> <span data-ttu-id="da181-109">您無法使用 hello 範例，並瀏覽此教學課程 toounderstand hello 範例的建置方式。</span><span class="sxs-lookup"><span data-stu-id="da181-109">You could use hello sample and go through this tutorial toounderstand how hello sample was built.</span></span> <span data-ttu-id="da181-110">或者，您可以使用這個教學課程 toocreate 從頭自己的解決方案。</span><span class="sxs-lookup"><span data-stu-id="da181-110">Or, you could use this tutorial toocreate your own solution ground-up.</span></span> <span data-ttu-id="da181-111">本教學課程的目標傾向 hello 第二種方法，讓您了解這個方案的建置方式。</span><span class="sxs-lookup"><span data-stu-id="da181-111">This tutorial is targeted towards hello second approach so that you understand how this solution was built.</span></span> <span data-ttu-id="da181-112">此外，盡可能，hello 教學課程與 hello 範例一致，而且使用 hello 相同的 hello 範例中的成品 （例如，結構描述、 轉換） 名稱。</span><span class="sxs-lookup"><span data-stu-id="da181-112">Also, as much as possible, hello tutorial is consistent with hello sample and uses hello same names for artifacts (for example, schemas, transforms) as used in hello sample.</span></span>  

> [!NOTE]
> <span data-ttu-id="da181-113">此解決方案牽涉到從 EAI 橋接器 tooan EDI 橋接器傳送訊息，因為它會重複使用 hello [BizTalk Services 橋接器鏈結範例](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104)範例。</span><span class="sxs-lookup"><span data-stu-id="da181-113">Because this solution involves sending a message from an EAI bridge tooan EDI bridge, it reuses hello [BizTalk Services Bridge chaining sample](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) sample.</span></span>  
> 
> 

## <a name="what-does-hello-solution-do"></a><span data-ttu-id="da181-114">Hello 解決方案有哪些功能？</span><span class="sxs-lookup"><span data-stu-id="da181-114">What does hello solution do?</span></span>
<span data-ttu-id="da181-115">在此方案中，Northwind 會從 Contoso 收到 EDIFACT 發票。</span><span class="sxs-lookup"><span data-stu-id="da181-115">In this solution, Northwind receives EDIFACT invoices from Contoso.</span></span> <span data-ttu-id="da181-116">這些發票未採用標準 EDI 格式。</span><span class="sxs-lookup"><span data-stu-id="da181-116">These invoices are not in a standard EDI format.</span></span> <span data-ttu-id="da181-117">因此，在傳送之前 hello 發票 tooNorthwind，它必須是已轉換的 tooan EDIFACT 發票 （也稱為 INVOIC） 文件。</span><span class="sxs-lookup"><span data-stu-id="da181-117">So, before sending hello invoice tooNorthwind, it must be transformed tooan EDIFACT invoice (also called INVOIC) document.</span></span> <span data-ttu-id="da181-118">在收到時，Northwind 必須處理 hello EDIFACT 發票，並傳回控制訊息 （也稱為 CONTRL） tooContoso。</span><span class="sxs-lookup"><span data-stu-id="da181-118">On receipt, Northwind must process hello EDIFACT invoice, and return a control message (also called CONTRL) tooContoso.</span></span>

![][1]  

<span data-ttu-id="da181-119">tooachieve 此商務案例中，Contoso 會使用提供的 Microsoft Azure BizTalk 服務的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="da181-119">tooachieve this business scenario, Contoso uses hello features provided with Microsoft Azure BizTalk Services.</span></span>

* <span data-ttu-id="da181-120">Contoso 使用 EAI 橋接器 tootransform hello 原始發票 tooEDIFACT INVOIC。</span><span class="sxs-lookup"><span data-stu-id="da181-120">Contoso uses EAI bridges tootransform hello original invoice tooEDIFACT INVOIC.</span></span>
* <span data-ttu-id="da181-121">hello EAI 橋接器接著會傳送 hello 訊息 tooan EDI 傳送橋接器部署 hello BizTalk 服務入口網站中設定之協議的一部分。</span><span class="sxs-lookup"><span data-stu-id="da181-121">hello EAI bridge then sends hello message tooan EDI send bridge deployed as part of an agreement configured in hello BizTalk Services Portal.</span></span>
* <span data-ttu-id="da181-122">hello EDI 傳送橋接器會處理 hello EDIFACT INVOIC 並將其路由 tooNorthwind。</span><span class="sxs-lookup"><span data-stu-id="da181-122">hello EDI send bridge processes hello EDIFACT INVOIC and routes it tooNorthwind.</span></span>
* <span data-ttu-id="da181-123">之後收到 hello 發票，Northwind 會傳回 CONTRL 訊息 toohello EDI 接收橋接器部署為 hello 協議的一部分。</span><span class="sxs-lookup"><span data-stu-id="da181-123">After receiving hello invoice, Northwind returns a CONTRL message toohello EDI receive bridge deployed as part of hello agreement.</span></span>  

> [!NOTE]
> <span data-ttu-id="da181-124">（選擇性） 此解決方案也會示範如何批次處理 toosend hello toouse 發票批次，而不是個別傳送每張發票。</span><span class="sxs-lookup"><span data-stu-id="da181-124">Optionally, this solution also demonstrates how toouse batching toosend hello invoices in batches, instead of sending each invoice separately.</span></span>  
> 
> 

<span data-ttu-id="da181-125">toocomplete hello 案例中，我們會使用服務匯流排佇列 toosend 發票從 Contoso tooNorthwind，或從 Northwind 接收通知。</span><span class="sxs-lookup"><span data-stu-id="da181-125">toocomplete hello scenario, we use Service Bus queues toosend invoice from Contoso tooNorthwind or receive acknowledgement from Northwind.</span></span> <span data-ttu-id="da181-126">您可以使用用戶端應用程式，其可供下載，並包含在可用的 hello 範例套件中建立這些佇列做為本教學課程的一部分。</span><span class="sxs-lookup"><span data-stu-id="da181-126">These queues can be created using a client application, which is available as a download and is included in hello sample package that is available as part of this tutorial.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="da181-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="da181-127">Prerequisites</span></span>
* <span data-ttu-id="da181-128">您必須具有服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="da181-128">You must have a Service Bus namespace.</span></span> <span data-ttu-id="da181-129">如需建立命名空間的指示，請參閱 [作法：建立或修改服務匯流排服務命名空間](https://msdn.microsoft.com/library/azure/hh674478.aspx)。</span><span class="sxs-lookup"><span data-stu-id="da181-129">For instructions on creating a namespace, see [How To: Create or Modify a Service Bus Service Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx).</span></span> <span data-ttu-id="da181-130">讓我們假設您已佈建服務匯流排命名空間，且其名稱為 **edifactbts**。</span><span class="sxs-lookup"><span data-stu-id="da181-130">Let us assume that you already have a Service Bus namespace provisioned, called **edifactbts**.</span></span>
* <span data-ttu-id="da181-131">您必須擁有 BizTalk 服務訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="da181-131">You must have a BizTalk Services subscription.</span></span> <span data-ttu-id="da181-132">如需相關指示，請參閱 [使用 Azure 傳統入口網站建立 BizTalk 服務](http://go.microsoft.com/fwlink/?LinkID=302280)。</span><span class="sxs-lookup"><span data-stu-id="da181-132">For instructions, see [Create a BizTalk Service using Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=302280).</span></span> <span data-ttu-id="da181-133">在本教學課程中，讓我們假設您擁有 BizTalk 服務訂用帳戶，且其名稱為 **contosowabs**。</span><span class="sxs-lookup"><span data-stu-id="da181-133">For this tutorial, let us assume you have a BizTalk Services subscription, called **contosowabs**.</span></span>
* <span data-ttu-id="da181-134">註冊您的 BizTalk 服務訂閱 hello BizTalk 服務入口網站上。</span><span class="sxs-lookup"><span data-stu-id="da181-134">Register your BizTalk Services subscription on hello BizTalk Services Portal.</span></span> <span data-ttu-id="da181-135">如需指示，請參閱[註冊 hello BizTalk 服務入口網站上的 BizTalk 服務部署](https://msdn.microsoft.com/library/hh689837.aspx)</span><span class="sxs-lookup"><span data-stu-id="da181-135">For instructions, see [Registering a BizTalk Service Deployment on hello BizTalk Services Portal](https://msdn.microsoft.com/library/hh689837.aspx)</span></span>
* <span data-ttu-id="da181-136">您必須安裝 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="da181-136">You must have Visual Studio installed.</span></span>
* <span data-ttu-id="da181-137">您必須安裝 BizTalk 服務 SDK。</span><span class="sxs-lookup"><span data-stu-id="da181-137">You must have BizTalk Services SDK installed.</span></span> <span data-ttu-id="da181-138">您可以下載 hello 從 SDK [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)</span><span class="sxs-lookup"><span data-stu-id="da181-138">You can download hello SDK from [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)</span></span>  

## <a name="step-1-create-hello-service-bus-queues"></a><span data-ttu-id="da181-139">步驟 1： 建立 hello 服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="da181-139">Step 1: Create hello Service Bus queues</span></span>
<span data-ttu-id="da181-140">此解決方案會使用交易夥伴之間的服務匯流排佇列 tooexchange 訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-140">This solution uses Service Bus queues tooexchange messages between trading partners.</span></span> <span data-ttu-id="da181-141">Contoso 與 Northwind 從傳送訊息 toohello 佇列 hello EAI 和/或 EDI 橋接器位置使用它們。</span><span class="sxs-lookup"><span data-stu-id="da181-141">Contoso and Northwind send messages toohello queues from where hello EAI and/or EDI bridges consume them.</span></span> <span data-ttu-id="da181-142">在此方案中，您需要三個服務匯流排佇列：</span><span class="sxs-lookup"><span data-stu-id="da181-142">For this solution, you need three Service Bus queues:</span></span>

* <span data-ttu-id="da181-143">**northwindreceive** – Northwind hello 發票從 Contoso 接收透過此佇列。</span><span class="sxs-lookup"><span data-stu-id="da181-143">**northwindreceive** – Northwind receives hello invoice from Contoso over this queue.</span></span>
* <span data-ttu-id="da181-144">**contosoreceive** -Contoso 透過此佇列從 Northwind 接收 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="da181-144">**contosoreceive** – Contoso receives hello acknowledgement from Northwind over this queue.</span></span>
* <span data-ttu-id="da181-145">**暫止**-所有擱置的訊息會路由的 toothis 佇列。</span><span class="sxs-lookup"><span data-stu-id="da181-145">**suspended** – All suspended messages are routed toothis queue.</span></span> <span data-ttu-id="da181-146">如果訊息在處理期間失敗，則會加以擱置。</span><span class="sxs-lookup"><span data-stu-id="da181-146">Messages are suspended if they fail during processing.</span></span>

<span data-ttu-id="da181-147">您可以使用 hello 範例封裝中包含的用戶端應用程式建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="da181-147">You can create these Service Bus queues by using a client application included in hello sample package.</span></span>  

1. <span data-ttu-id="da181-148">從您下載 hello 範例的 hello 位置，開啟**教學課程傳送發票使用 BizTalk 服務 EDI Bridges.sln**。</span><span class="sxs-lookup"><span data-stu-id="da181-148">From hello location where you downloaded hello sample, open **Tutorial Sending Invoices Using BizTalk Services EDI Bridges.sln**.</span></span>
2. <span data-ttu-id="da181-149">按**F5** toobuild 並開始 hello **Tutorial Client**應用程式。</span><span class="sxs-lookup"><span data-stu-id="da181-149">Press **F5** toobuild and start hello **Tutorial Client** application.</span></span>
3. <span data-ttu-id="da181-150">在 [hello] 畫面上，輸入 hello 服務匯流排 ACS 命名空間、 簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="da181-150">In hello screen, enter hello Service Bus ACS namespace, issuer name, and issuer key.</span></span>
   
   ![][2]  
4. <span data-ttu-id="da181-151">隨即出現訊息方塊提示，指出將會在服務匯流排命名空間中建立三個佇列。</span><span class="sxs-lookup"><span data-stu-id="da181-151">A message box prompts that three queues will be created in your Service Bus namespace.</span></span> <span data-ttu-id="da181-152">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="da181-152">Click **OK**.</span></span>
5. <span data-ttu-id="da181-153">保持 hello 教學課程用戶端正在執行。</span><span class="sxs-lookup"><span data-stu-id="da181-153">Leave hello Tutorial Client running.</span></span> <span data-ttu-id="da181-154">開啟 [hello]，按一下**Service Bus** > ***您的服務匯流排命名空間*** > **佇列**，並確認已建立 hello 三個佇列。</span><span class="sxs-lookup"><span data-stu-id="da181-154">Open hello , click **Service Bus** > ***your Service Bus namespace*** > **Queues**, and verify that hello three queues are created.</span></span>  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a><span data-ttu-id="da181-155">步驟 2：建立和部署交易夥伴協議</span><span class="sxs-lookup"><span data-stu-id="da181-155">Step 2: Create and deploy trading partner agreement</span></span>
<span data-ttu-id="da181-156">建立 Contoso 與 Northwind 之間的交易夥伴協議。</span><span class="sxs-lookup"><span data-stu-id="da181-156">Create a trading partner agreement between Contoso and Northwind.</span></span> <span data-ttu-id="da181-157">交易夥伴協議定義 trade 合約的訊息結構描述 toouse，例如 hello 兩個商業夥伴之間的傳訊通訊協定 toouse 等等。交易夥伴協議包含兩個 EDI 橋接器、 一個 toosend 訊息 tootrading 夥伴 (稱為 hello **EDI 傳送橋接器**) 和一個 tooreceive 從交易夥伴的訊息 (稱為 hello **EDI 接收橋接器**).</span><span class="sxs-lookup"><span data-stu-id="da181-157">A trading partner agreement defines a trade contract between hello two business partners, such as which message schema toouse, which messaging protocol toouse, etc. A trading partner agreement includes two EDI bridges, one toosend messages tootrading partners (called hello **EDI Send bridge**) and one tooreceive messages from trading partners (called hello **EDI Receive bridge**).</span></span>

<span data-ttu-id="da181-158">Hello 在內容中此解決方案，hello EDI 傳送橋接器對應 toohello 傳送端的 hello 協議，並是使用的 toosend hello EDIFACT 發票從 Contoso tooNorthwind。</span><span class="sxs-lookup"><span data-stu-id="da181-158">In hello context of this solution, hello EDI send bridge corresponds toohello send-side of hello agreement and is used toosend hello EDIFACT invoice from Contoso tooNorthwind.</span></span> <span data-ttu-id="da181-159">同樣地，hello EDI 接收橋接器對應 toohello 接收端的 hello 協議並是使用的 tooreceive Northwind 的確認。</span><span class="sxs-lookup"><span data-stu-id="da181-159">Similarly, hello EDI receive bridge corresponds toohello receive-side of hello agreement and is used tooreceive acknowledgements from Northwind.</span></span>  

### <a name="create-hello-trading-partners"></a><span data-ttu-id="da181-160">建立交易夥伴的 hello</span><span class="sxs-lookup"><span data-stu-id="da181-160">Create hello trading partners</span></span>
<span data-ttu-id="da181-161">toostart，會建立交易夥伴 Contoso 和 Northwind。</span><span class="sxs-lookup"><span data-stu-id="da181-161">toostart with, create trading partners for Contoso and Northwind.</span></span>  

1. <span data-ttu-id="da181-162">在 hello BizTalk 服務入口網站，在 hello**夥伴**索引標籤上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="da181-162">In hello BizTalk Services Portal, on hello **Partners** tab, click **Add**.</span></span>
2. <span data-ttu-id="da181-163">在 [hello 新增夥伴] 頁面，輸入**Contoso**作為夥伴名稱，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="da181-163">In hello New partner page, enter **Contoso** as a partner name, and then click **Save**.</span></span>
3. <span data-ttu-id="da181-164">重複的 hello 步驟 toocreate hello 第二個夥伴， **Northwind**。</span><span class="sxs-lookup"><span data-stu-id="da181-164">Repeat hello step toocreate hello second partner, **Northwind**.</span></span>  

### <a name="create-hello-agreement"></a><span data-ttu-id="da181-165">建立 hello 協議</span><span class="sxs-lookup"><span data-stu-id="da181-165">Create hello agreement</span></span>
<span data-ttu-id="da181-166">交易夥伴的商務設定檔之間會建立交易夥伴協議。</span><span class="sxs-lookup"><span data-stu-id="da181-166">Trading partner agreements are created between business profiles of trading partners.</span></span> <span data-ttu-id="da181-167">這個解決方案使用 hello 預設夥伴設定檔，當我們建立 hello 夥伴會自動建立。</span><span class="sxs-lookup"><span data-stu-id="da181-167">This solution uses hello default partner profiles that are automatically created when we created hello partners.</span></span>  

1. <span data-ttu-id="da181-168">在 hello BizTalk 服務入口網站，按一下 **協議** > **新增**。</span><span class="sxs-lookup"><span data-stu-id="da181-168">In hello BizTalk Services Portal, click **Agreements** > **Add**.</span></span>
2. <span data-ttu-id="da181-169">在 hello 新協議的**一般設定**頁面上，指定在 hello 圖，顯示 hello 值，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="da181-169">In hello new agreement’s **General Settings** page, specify hello values as shown in hello image below, and then click **Continue**.</span></span>
   
   ![][3]  
   
   <span data-ttu-id="da181-170">按一下 [繼續] 之後，[接收設定] 和 [傳送設定] 這兩個索引標籤會變成可用狀態。</span><span class="sxs-lookup"><span data-stu-id="da181-170">After you click **Continue**, two tabs, **Receive Settings** and **Send Settings** become available.</span></span>
3. <span data-ttu-id="da181-171">建立 Contoso 與 Northwind 之間的 hello 傳送協議。</span><span class="sxs-lookup"><span data-stu-id="da181-171">Create hello send agreement between Contoso and Northwind.</span></span> <span data-ttu-id="da181-172">此協議控管 Contoso 如何傳送嗨 EDIFACT 發票 tooNorthwind。</span><span class="sxs-lookup"><span data-stu-id="da181-172">This agreement governs how Contoso sends hello EDIFACT invoice tooNorthwind.</span></span>
   
   1. <span data-ttu-id="da181-173">按一下 [傳送設定] 。</span><span class="sxs-lookup"><span data-stu-id="da181-173">Click **Send Settings**.</span></span>
   2. <span data-ttu-id="da181-174">保留 hello 預設值在 hello**輸入 URL**，**轉換**，和**批次處理**索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da181-174">Retain hello default values on hello **Inbound URL**, **Transform**, and **Batching** tabs.</span></span>
   3. <span data-ttu-id="da181-175">在 [hello**通訊協定**] 索引標籤下 hello**結構描述**區段中上, 傳 hello **EFACT_D93A_INVOIC.xsd**結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-175">On hello **Protocol** tab, under hello **Schemas** section, upload hello **EFACT_D93A_INVOIC.xsd** schema.</span></span> <span data-ttu-id="da181-176">此結構描述可與 hello 範例封裝。</span><span class="sxs-lookup"><span data-stu-id="da181-176">This schema is available with hello sample package.</span></span>
      
      ![][4]  
   4. <span data-ttu-id="da181-177">在 hello**傳輸**索引標籤上，指定 hello hello 服務匯流排佇列的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="da181-177">On hello **Transport** tab, specify hello details for hello Service Bus queues.</span></span> <span data-ttu-id="da181-178">Hello 傳送端協議中，我們使用 hello **northwindreceive**佇列 toosend hello EDIFACT 發票 tooNorthwind 並 hello**暫停**佇列 tooroute 時處理而失敗的任何訊息暫止。</span><span class="sxs-lookup"><span data-stu-id="da181-178">For hello send-side agreement, we use hello **northwindreceive** queue toosend hello EDIFACT invoice tooNorthwind, and hello **suspended** queue tooroute any messages that fail during processing and are suspended.</span></span> <span data-ttu-id="da181-179">建立這些佇列中的**步驟 1： 建立 Service Bus 佇列 hello** （在本主題中）。</span><span class="sxs-lookup"><span data-stu-id="da181-179">You created these queues in **Step 1: Create hello Service Bus queues** (in this topic).</span></span>
      
      ![][5]  
      
      <span data-ttu-id="da181-180">在下**傳輸設定 > 傳輸類型**和**訊息暫停設定 > 傳輸類型**，選取 Azure 服務匯流排，然後提供 hello 值 hello 影像所示。</span><span class="sxs-lookup"><span data-stu-id="da181-180">Under **Transport Settings > Transport type** and **Message Suspension Settings > Transport type**, select Azure Service Bus and provide hello values as shown in hello image.</span></span>
4. <span data-ttu-id="da181-181">建立 hello 接收 Contoso 與 Northwind 之間的協議。</span><span class="sxs-lookup"><span data-stu-id="da181-181">Create hello receive agreement between Contoso and Northwind.</span></span> <span data-ttu-id="da181-182">此協議控管 Contoso 如何從 Northwind 接收 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="da181-182">This agreement governs how Contoso receives hello acknowledgement from Northwind.</span></span>
   
   1. <span data-ttu-id="da181-183">按一下 [接收設定] 。</span><span class="sxs-lookup"><span data-stu-id="da181-183">Click **Receive Settings**.</span></span>
   2. <span data-ttu-id="da181-184">保留 hello 預設值在 hello**傳輸**和**轉換**索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da181-184">Retain hello default values on hello **Transport** and **Transform** tabs.</span></span>
   3. <span data-ttu-id="da181-185">在 [hello**通訊協定**] 索引標籤下 hello**結構描述**區段中上, 傳 hello **EFACT_4.1_CONTRL.xsd**結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-185">On hello **Protocol** tab, under hello **Schemas** section, upload hello **EFACT_4.1_CONTRL.xsd** schema.</span></span> <span data-ttu-id="da181-186">此結構描述可與 hello 範例封裝。</span><span class="sxs-lookup"><span data-stu-id="da181-186">This schema is available with hello sample package.</span></span>
   4. <span data-ttu-id="da181-187">在 hello**路由**索引標籤上，建立篩選器 tooensure，只有路由的 tooContoso Northwind 的確認。</span><span class="sxs-lookup"><span data-stu-id="da181-187">On hello **Route** tab, create a filter tooensure that only acknowledgements from Northwind are routed tooContoso.</span></span> <span data-ttu-id="da181-188">在下**路由設定**，按一下 **新增**toocreate hello 路由篩選條件。</span><span class="sxs-lookup"><span data-stu-id="da181-188">Under **Route Settings**, click **Add** toocreate hello routing filter.</span></span>
      
      ![][6]  
      
      1. <span data-ttu-id="da181-189">提供的值**規則名稱**，**路由規則**，和**路由目的地**hello 映像中所示。</span><span class="sxs-lookup"><span data-stu-id="da181-189">Provide values for **Rule Name**, **Route rule**, and **Route destination** as shown in hello image.</span></span>
      2. <span data-ttu-id="da181-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="da181-190">Click **Save**.</span></span>
   5. <span data-ttu-id="da181-191">在 hello**路由**再次索引標籤，指定已擱置的通知 （在處理期間失敗的通知） 傳送至其中。</span><span class="sxs-lookup"><span data-stu-id="da181-191">On hello **Route** tab again, specify where suspended acknowledgements (acknowledgements that fail during processing) are routed to.</span></span> <span data-ttu-id="da181-192">設定 hello 傳輸類型 tooAzure 服務匯流排時，將路由目的地類型太**佇列**，驗證輸入太**共用存取簽章**(SAS)，提供 hello Service Bus hello SAS 連接字串命名空間，然後輸入 hello 佇列名稱**暫停**。</span><span class="sxs-lookup"><span data-stu-id="da181-192">Set hello transport type tooAzure Service Bus, route destination type too**Queue**, authentication type too**Shared Access Signature** (SAS), provide hello SAS connection string for hello Service Bus namespace, and then enter hello queue name as **suspended**.</span></span>
5. <span data-ttu-id="da181-193">最後，按一下 **部署**toodeploy hello 協議。</span><span class="sxs-lookup"><span data-stu-id="da181-193">Finally, click **Deploy** toodeploy hello agreement.</span></span> <span data-ttu-id="da181-194">取得部署注意 hello 端點 hello 傳送和接收協議的位置。</span><span class="sxs-lookup"><span data-stu-id="da181-194">Note hello endpoints where hello send and receive agreements get deployed.</span></span>
   
   * <span data-ttu-id="da181-195">在 hello**傳送設定**索引標籤，下方**輸入 URL**，注意 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="da181-195">On hello **Send Settings** tab, under **Inbound URL**, note hello endpoint.</span></span> <span data-ttu-id="da181-196">toosend EDI 傳送橋接器將訊息從 Contoso tooNorthwind 使用 hello，您必須傳送訊息 toothis 端點。</span><span class="sxs-lookup"><span data-stu-id="da181-196">toosend a message from Contoso tooNorthwind using hello EDI send bridge, you must send a message toothis endpoint.</span></span>
   * <span data-ttu-id="da181-197">在 hello**接收設定**索引標籤，下方**傳輸**，注意 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="da181-197">On hello **Receive Settings** tab, under **Transport**, note hello endpoint.</span></span> <span data-ttu-id="da181-198">toosend 將訊息從 Northwind tooContoso 使用 hello EDI 接收橋接器，您必須傳送訊息 toothis 端點。</span><span class="sxs-lookup"><span data-stu-id="da181-198">toosend a message from Northwind tooContoso using hello EDI receive bridge, you must send a message toothis endpoint.</span></span>  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a><span data-ttu-id="da181-199">步驟 3： 建立和部署 hello BizTalk 服務專案</span><span class="sxs-lookup"><span data-stu-id="da181-199">Step 3: Create and deploy hello BizTalk Services project</span></span>
<span data-ttu-id="da181-200">在 hello 先前步驟中，您可以部署的 hello EDI 傳送和接收協議 tooprocess EDIFACT 發票和確認函。</span><span class="sxs-lookup"><span data-stu-id="da181-200">In hello previous step, you deployed hello EDI send and receive agreements tooprocess EDIFACT invoices and acknowledgements.</span></span> <span data-ttu-id="da181-201">這些合約可以只處理符合 toohello 標準 EDIFACT 訊息結構描述的訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-201">These agreements can only process messages that conform toohello standard EDIFACT message schema.</span></span> <span data-ttu-id="da181-202">不過，每個針對此解決方案的 hello 案例，Contoso 傳送發票 tooNorthwind 內部專屬結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-202">However, per hello scenario for this solution, Contoso sends an invoice tooNorthwind in an in-house proprietary schema.</span></span> <span data-ttu-id="da181-203">所以，EDI 傳送橋接器的 toohello 傳送 hello 訊息之前，它必須轉換從 hello 內部結構描述 toohello 標準 EDIFACT 發票結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-203">So, before hello message is sent toohello EDI send bridge, it must be transformed from hello in-house schema toohello standard EDIFACT invoice schema.</span></span> <span data-ttu-id="da181-204">hello BizTalk 服務 EAI 專案會這樣做。</span><span class="sxs-lookup"><span data-stu-id="da181-204">hello BizTalk Services EAI project does that.</span></span>

<span data-ttu-id="da181-205">hello BizTalk 服務專案， **InvoiceProcessingBridge**，轉換 hello 訊息也是您所下載的 hello 範例的一部分。</span><span class="sxs-lookup"><span data-stu-id="da181-205">hello BizTalk Services project, **InvoiceProcessingBridge**, that transforms hello message is also included as part of hello sample you downloaded.</span></span> <span data-ttu-id="da181-206">hello 專案包括下列成品的 hello:</span><span class="sxs-lookup"><span data-stu-id="da181-206">hello project includes hello following artifacts:</span></span>

* <span data-ttu-id="da181-207">**INHOUSEINVOICE。XSD** – tooNorthwind 傳送嗨內部發票的結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-207">**INHOUSEINVOICE.XSD** – Schema of hello in-house invoice that is sent tooNorthwind.</span></span>
* <span data-ttu-id="da181-208">**EFACT_D93A_INVOIC。XSD** – hello 標準 EDIFACT 發票的結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-208">**EFACT_D93A_INVOIC.XSD** – Schema of hello standard EDIFACT invoice.</span></span>
* <span data-ttu-id="da181-209">**EFACT_4.1_CONTRL。XSD** -Northwind 傳送 tooContoso hello EDIFACT 通知的結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-209">**EFACT_4.1_CONTRL.XSD** – Schema of hello EDIFACT acknowledgement that Northwind sends tooContoso.</span></span>
* <span data-ttu-id="da181-210">**INHOUSEINVOICE_to_D93AINVOIC。TRFM** – hello 對應 hello 內部發票結構描述 toohello 標準 EDIFACT 發票結構描述的轉換。</span><span class="sxs-lookup"><span data-stu-id="da181-210">**INHOUSEINVOICE_to_D93AINVOIC.TRFM** – hello transform that maps hello in-house invoice schema toohello standard EDIFACT invoice schema.</span></span>  

### <a name="create-hello-biztalk-services-project"></a><span data-ttu-id="da181-211">建立 hello BizTalk 服務專案</span><span class="sxs-lookup"><span data-stu-id="da181-211">Create hello BizTalk Services project</span></span>
1. <span data-ttu-id="da181-212">Hello Visual Studio 方案，在展開 hello InvoiceProcessingBridge 專案，然後再開啟 hello **MessageFlowItinerary.bcs**檔案。</span><span class="sxs-lookup"><span data-stu-id="da181-212">In hello Visual Studio solution, expand hello InvoiceProcessingBridge project, and then open hello **MessageFlowItinerary.bcs** file.</span></span>
2. <span data-ttu-id="da181-213">Hello 畫布上任何位置按一下，並設定 hello **BizTalk 服務 URL**在 hello 屬性方塊 toospecify 您 BizTalk 服務的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="da181-213">Click anywhere on hello canvas and set hello **BizTalk Service URL** in hello property box toospecify your BizTalk Services subscription name.</span></span> <span data-ttu-id="da181-214">例如： `https://contosowabs.biztalk.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="da181-214">For example, `https://contosowabs.biztalk.windows.net`.</span></span>
   
   ![][7]  
3. <span data-ttu-id="da181-215">從 hello 工具箱，拖曳**Xml 單向橋接器**toohello 畫布。</span><span class="sxs-lookup"><span data-stu-id="da181-215">From hello toolbox, drag an **Xml One-Way Bridge** toohello canvas.</span></span> <span data-ttu-id="da181-216">設定 hello**實體名稱**和**相對位址**hello 的屬性太橋接器**ProcessInvoiceBridge**。</span><span class="sxs-lookup"><span data-stu-id="da181-216">Set hello **Entity Name** and **Relative Address** properties of hello bridge too**ProcessInvoiceBridge**.</span></span> <span data-ttu-id="da181-217">按兩下**ProcessInvoiceBridge** tooopen hello 橋接器組態介面。</span><span class="sxs-lookup"><span data-stu-id="da181-217">Double-click **ProcessInvoiceBridge** tooopen hello bridge configuration surface.</span></span>
4. <span data-ttu-id="da181-218">Hello 內**訊息類型**方塊中，按一下加號 hello (**+**) 按鈕 toospecify hello 結構描述的 hello 內送訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-218">Within hello **Message Types** box, click hello plus (**+**) button toospecify hello schema of hello incoming message.</span></span> <span data-ttu-id="da181-219">因為 hello EAI 橋接器的 hello 連入訊息一律是 hello 內部發票，設定此太**INHOUSEINVOICE**。</span><span class="sxs-lookup"><span data-stu-id="da181-219">Because hello incoming message for hello EAI bridge is always hello in-house invoice, set this too**INHOUSEINVOICE**.</span></span>
   
   ![][8]  
5. <span data-ttu-id="da181-220">按一下 hello **Xml 轉換**圖形，並在 hello 屬性方塊中的 hello**對應**屬性，按一下 hello 省略符號 (**...**) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da181-220">Click hello **Xml Transform** shape, and in hello property box, for hello **Maps** property, click hello ellipsis (**...**) button.</span></span> <span data-ttu-id="da181-221">在 hello**對應選取範圍**對話方塊中，選取 hello **INHOUSEINVOICE_to_D93AINVOIC**轉換檔案，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="da181-221">In hello **Maps Selection** dialog box, select hello **INHOUSEINVOICE_to_D93AINVOIC** transform file, and then click **OK**.</span></span>
   
   ![][9]  
6. <span data-ttu-id="da181-222">返回太**MessageFlowItinerary.bcs**，並從 hello 工具箱，拖曳**雙向外部服務端點**方 hello toohello **ProcessInvoiceBridge**。</span><span class="sxs-lookup"><span data-stu-id="da181-222">Go back too**MessageFlowItinerary.bcs**, and from hello toolbox, drag a **Two-Way External Service Endpoint** toohello right of hello **ProcessInvoiceBridge**.</span></span> <span data-ttu-id="da181-223">設定其**實體名稱**屬性太**EDIBridge**。</span><span class="sxs-lookup"><span data-stu-id="da181-223">Set its **Entity Name** property too**EDIBridge**.</span></span>
7. <span data-ttu-id="da181-224">在 hello 方案總管 中，展開 hello **MessageFlowItinerary.bcs**按兩下 hello **EDIBridge.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="da181-224">In hello Solution Explorer, expand hello **MessageFlowItinerary.bcs** and double-click hello **EDIBridge.config** file.</span></span> <span data-ttu-id="da181-225">取代的 hello 的 hello 內容**EDIBridge.config** hello 下列。</span><span class="sxs-lookup"><span data-stu-id="da181-225">Replace hello content of hello **EDIBridge.config** with hello following.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da181-226">為什麼需要 tooedit hello.config 檔案？我們加入 toohello 橋接器設計工具畫布的 hello 外部服務端點會代表我們稍早部署的 hello EDI 橋接器。</span><span class="sxs-lookup"><span data-stu-id="da181-226">Why do I need tooedit hello .config file? hello external service endpoint that we added toohello bridge designer canvas represents hello EDI bridges that we deployed earlier.</span></span> <span data-ttu-id="da181-227">EDI 橋接器是具有傳送和接收端的雙向橋接器。</span><span class="sxs-lookup"><span data-stu-id="da181-227">EDI bridges are two-way bridges, with a send and receive side.</span></span> <span data-ttu-id="da181-228">不過，hello 我們加入 toohello 橋接器設計工具的 EAI 橋接器是單向橋接器。</span><span class="sxs-lookup"><span data-stu-id="da181-228">However, hello EAI bridge that we added toohello bridge designer is a one-way bridge.</span></span> <span data-ttu-id="da181-229">因此，toohandle hello 不同訊息交換模式的 hello 這兩種橋接器，我們使用自訂橋接器行為其組態納入 hello.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="da181-229">So, toohandle hello different message exchange patterns of hello two bridges, we use a custom bridge behavior by including its configuration in hello .config file.</span></span> <span data-ttu-id="da181-230">此外，hello 自訂行為也會處理 hello 驗證 toohello EDI 傳送橋接器端點。這個自訂行為可做為個別的範例： [BizTalk Services 橋接器鏈結範例-EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104)。</span><span class="sxs-lookup"><span data-stu-id="da181-230">Additionally, hello custom behavior also handles hello authentication toohello EDI send bridge endpoint.This custom behavior is available as a separate sample at [BizTalk Services Bridge chaining sample - EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104).</span></span> <span data-ttu-id="da181-231">此解決方案會重複使用 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="da181-231">This solution reuses hello sample.</span></span>  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. <span data-ttu-id="da181-232">更新 hello EDIBridge.config 檔案 tooinclude 組態詳細資料</span><span class="sxs-lookup"><span data-stu-id="da181-232">Update hello EDIBridge.config file tooinclude configuration details</span></span>
   
   * <span data-ttu-id="da181-233">在下 *<behaviors>* 、 提供 hello ACS 命名空間和索引鍵相關聯 hello BizTalk 服務訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="da181-233">Under *<behaviors>*, provide hello ACS namespace and key associated with hello BizTalk Services subscription.</span></span>
   * <span data-ttu-id="da181-234">在下 *<client>* ，提供 hello hello EDI 傳送協議部署所在的端點。</span><span class="sxs-lookup"><span data-stu-id="da181-234">Under *<client>*, provide hello endpoint where hello EDI send agreement is deployed.</span></span>
   
   <span data-ttu-id="da181-235">儲存變更並關閉 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="da181-235">Save changes and close hello configuration file.</span></span>
9. <span data-ttu-id="da181-236">從 hello 工具箱中，按一下 hello**連接器**和聯結 hello **ProcessInvoiceBridge**和**EDIBridge**元件。</span><span class="sxs-lookup"><span data-stu-id="da181-236">From hello Toolbox, click hello **Connector** and join hello **ProcessInvoiceBridge** and **EDIBridge** components.</span></span> <span data-ttu-id="da181-237">選取 hello 連接器，然後在 [屬性] 方塊中，設定**篩選條件**太**全部符合**。</span><span class="sxs-lookup"><span data-stu-id="da181-237">Select hello connector, and in Properties box, set **Filter Condition** too**Match All**.</span></span> <span data-ttu-id="da181-238">這可確保由 hello EAI 橋接器處理的所有訊息都會路由都傳送 toohello EDI 橋接器。</span><span class="sxs-lookup"><span data-stu-id="da181-238">This ensures that all messages processed by hello EAI bridge are routed toohello EDI bridge.</span></span>
   
   ![][10]  
10. <span data-ttu-id="da181-239">將變更儲存 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="da181-239">Save changes toohello solution.</span></span>  

### <a name="deploy-hello-project"></a><span data-ttu-id="da181-240">部署 hello 專案</span><span class="sxs-lookup"><span data-stu-id="da181-240">Deploy hello project</span></span>
1. <span data-ttu-id="da181-241">Hello 在電腦上建立 hello BizTalk 服務專案的位置，下載並安裝您的 BizTalk 服務訂閱 hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="da181-241">On hello computer where you created hello BizTalk Services project, download and install hello SSL certificate for your BizTalk Services subscription.</span></span> <span data-ttu-id="da181-242">從 BizTalk 服務 底下按一下 儀表板，然後按一下下載 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="da181-242">From , under BizTalk Services, click **Dashboard**, and then click **Download SSL Certificate**.</span></span> <span data-ttu-id="da181-243">按兩下 hello 憑證，並遵循 hello 提示 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="da181-243">Double-click hello certificate and follow hello prompt toocomplete hello installation.</span></span> <span data-ttu-id="da181-244">請確定您已安裝 hello 憑證**受信任的根憑證授權單位**憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="da181-244">Make sure you install hello certificate under **Trusted Root Certification Authorities** certificate store.</span></span>
2. <span data-ttu-id="da181-245">在 Visual Studio 方案總管 中，以滑鼠右鍵按一下 hello **InvoiceProcessingBridge**專案，然後再按一下**部署**。</span><span class="sxs-lookup"><span data-stu-id="da181-245">In Visual Studio Solution Explorer, right-click hello **InvoiceProcessingBridge** project, and then click **Deploy**.</span></span>
3. <span data-ttu-id="da181-246">提供 hello 值 hello 影像所示，然後按**部署**。</span><span class="sxs-lookup"><span data-stu-id="da181-246">Provide hello values as shown in hello image, and then click **Deploy**.</span></span> <span data-ttu-id="da181-247">您也可以按一下 BizTalk 服務取得 hello ACS 認證**連接資訊**從 hello BizTalk 服務儀表板。</span><span class="sxs-lookup"><span data-stu-id="da181-247">You can get hello ACS credentials for BizTalk Services by clicking **Connection Information** from hello BizTalk Services dashboard.</span></span>
   
   ![][11]  
   
   <span data-ttu-id="da181-248">從 hello 輸出窗格中，複製 hello 端點 hello EAI 橋接器部署所在，比方說， `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`。</span><span class="sxs-lookup"><span data-stu-id="da181-248">From hello output pane, copy hello endpoint where hello EAI bridge is deployed, for example, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`.</span></span> <span data-ttu-id="da181-249">您稍後將需要此端點 URL。</span><span class="sxs-lookup"><span data-stu-id="da181-249">You will need this endpoint URL later.</span></span>  

## <a name="step-4-test-hello-solution"></a><span data-ttu-id="da181-250">步驟 4： 測試 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="da181-250">Step 4: Test hello solution</span></span>
<span data-ttu-id="da181-251">在本主題中，我們查看 tootest 如何使用 hello hello 方案**Tutorial Client** hello 範例的一部分的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da181-251">In this topic, we look at how tootest hello solution by using hello **Tutorial Client** application provided as part of hello sample.</span></span>  

1. <span data-ttu-id="da181-252">在 Visual Studio 中，按下 F5 toostart hello **Tutorial Client**。</span><span class="sxs-lookup"><span data-stu-id="da181-252">In Visual Studio, press F5 toostart hello **Tutorial Client**.</span></span>
2. <span data-ttu-id="da181-253">囉 」 畫面必須 hello 值預先填入的 hello 步驟中，我們建立 hello 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="da181-253">hello screen must have hello values prepopulated from hello step where we created hello Service Bus queues.</span></span> <span data-ttu-id="da181-254">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="da181-254">Click **Next**.</span></span>
3. <span data-ttu-id="da181-255">在 hello 下一步 視窗中，BizTalk 服務訂閱提供 ACS 認證和 hello 端點其中 EAI 和 EDI （接收） 橋接器部署。</span><span class="sxs-lookup"><span data-stu-id="da181-255">In hello next window, provide ACS credentials for BizTalk Services subscription, and hello endpoints where EAI and EDI (receive) bridges are deployed.</span></span>
   
   <span data-ttu-id="da181-256">Hello 上一個步驟中，您必須複製 hello EAI 橋接器端點。</span><span class="sxs-lookup"><span data-stu-id="da181-256">You had copied hello EAI bridge endpoint in hello previous step.</span></span> <span data-ttu-id="da181-257">EDI 接收橋接器端點 hello BizTalk 服務入口網站中，移 toohello 協議 > 接收的設定 > 傳輸 > 端點。</span><span class="sxs-lookup"><span data-stu-id="da181-257">For EDI receive bridge endpoint, in hello BizTalk Services Portal, go toohello agreement > Receive Settings > Transport > Endpoint.</span></span>
   
   ![][12]  
4. <span data-ttu-id="da181-258">在 hello 下一步] 視窗中的 [Contoso 底下，按一下 [hello**傳送內部發票**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da181-258">In hello next window, under Contoso, click hello **Send In-house Invoice** button.</span></span> <span data-ttu-id="da181-259">在 hello 檔案開啟對話方塊，請開啟 hello INHOUSEINVOICE.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="da181-259">In hello File open dialog box, open hello INHOUSEINVOICE.txt file.</span></span> <span data-ttu-id="da181-260">檢查 hello hello 檔案內容，然後按一下**確定**toosend hello 發票。</span><span class="sxs-lookup"><span data-stu-id="da181-260">Examine hello content of hello file and then click **OK** toosend hello invoice.</span></span>
   
   ![][13]  
5. <span data-ttu-id="da181-261">在幾秒 hello Northwind 就會收到發票。</span><span class="sxs-lookup"><span data-stu-id="da181-261">In a few seconds hello invoice is received at Northwind.</span></span> <span data-ttu-id="da181-262">按一下 hello**檢視訊息**Northwind 所收到的連結 toosee hello 發票。</span><span class="sxs-lookup"><span data-stu-id="da181-262">Click hello **View Message** link toosee hello invoice received by Northwind.</span></span> <span data-ttu-id="da181-263">請注意，contoso 傳送一個 hello 時的標準 EDIFACT 結構描述中的 hello Northwind 收到的發票的方式是在內部結構描述。</span><span class="sxs-lookup"><span data-stu-id="da181-263">Notice how hello invoice received by Northwind is in standard EDIFACT schema while hello one sent by Contoso was an in-house schema.</span></span>
   
   ![][14]  
6. <span data-ttu-id="da181-264">選取 hello 發票，然後按一下**傳送認可**。</span><span class="sxs-lookup"><span data-stu-id="da181-264">Select hello invoice and then click **Send Acknowledgement**.</span></span> <span data-ttu-id="da181-265">在快顯的 hello 對話方塊中，請注意該識別碼是在 hello 接收發票與 hello 認可傳送相同的 hello 交換。</span><span class="sxs-lookup"><span data-stu-id="da181-265">In hello dialog box that pops up, notice that hello interchange ID is same in hello received invoice and hello acknowledgement being sent.</span></span> <span data-ttu-id="da181-266">按一下 確定 在 hello**傳送認可** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="da181-266">Click OK in hello **Send Acknowledgement** dialog box.</span></span>
   
   ![][15]  
7. <span data-ttu-id="da181-267">幾分鐘後，在 Contoso 成功收到 hello 確認。</span><span class="sxs-lookup"><span data-stu-id="da181-267">In a few seconds, hello acknowledgement is successfully received at Contoso.</span></span>
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a><span data-ttu-id="da181-268">步驟 5 (選用)：批次傳送 EDIFACT 發票</span><span class="sxs-lookup"><span data-stu-id="da181-268">Step 5 (optional): Send EDIFACT invoice in batches</span></span>
<span data-ttu-id="da181-269">BizTalk 服務 EDI 橋接器也支援批次處理傳出訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-269">BizTalk Services EDI bridges also supports batching of outgoing messages.</span></span> <span data-ttu-id="da181-270">這項功能可用於接收夥伴想 tooreceive 一批訊息 （符合特定條件），而不是個別的訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-270">This feature is useful for receiving partners that prefer tooreceive a batch of messages (meeting certain criterion) instead of individual messages.</span></span>

<span data-ttu-id="da181-271">處理批次時，即 hello 最重要層面是 hello 實際釋放 hello 批次，也稱為 hello 釋放準則。</span><span class="sxs-lookup"><span data-stu-id="da181-271">hello most important aspect when working with batches is hello actual release of hello batch, also called hello release criteria.</span></span> <span data-ttu-id="da181-272">hello 釋放準則可以根據 hello 接收夥伴想 tooreceive 訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="da181-272">hello release criteria can be based on how hello receiving partner wants tooreceive messages.</span></span> <span data-ttu-id="da181-273">如果啟用批次處理時，EDI 橋接器 hello 就不會傳送 hello hello 符合釋放準則後，直到接收夥伴外寄訊息 toohello。</span><span class="sxs-lookup"><span data-stu-id="da181-273">If batching is enabled, hello EDI bridge does not send hello outgoing message toohello receiving partner until hello release criteria is fulfilled.</span></span> <span data-ttu-id="da181-274">例如，依據訊息大小的批次準則只會在批次處理 'n' 則訊息時才分派批次。</span><span class="sxs-lookup"><span data-stu-id="da181-274">For example, a batching criteria based on message size dispatches a batch only when ‘n’ messages are batched.</span></span> <span data-ttu-id="da181-275">批次準則也可以是依據時間，以便在每天固定時間傳送批次。</span><span class="sxs-lookup"><span data-stu-id="da181-275">A batch criteria can also be time-based, such that a batch is sent at a fixed time every day.</span></span> <span data-ttu-id="da181-276">在此解決方案中，我們嘗試 hello 訊息大小基礎的準則。</span><span class="sxs-lookup"><span data-stu-id="da181-276">In this solution, we try hello message-size based criteria.</span></span>

1. <span data-ttu-id="da181-277">在 hello BizTalk 服務入口網站，按一下您稍早建立的 hello 協議。</span><span class="sxs-lookup"><span data-stu-id="da181-277">In hello BizTalk Services Portal, click hello agreement you created earlier.</span></span> <span data-ttu-id="da181-278">按一下 [傳送設定] > [批次處理] > [新增批次]。</span><span class="sxs-lookup"><span data-stu-id="da181-278">Click Send Settings > Batching > Add Batch.</span></span>
2. <span data-ttu-id="da181-279">對批次名稱輸入 **InvoiceBatch**、提供描述，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="da181-279">For batch name, enter **InvoiceBatch**, provide a description, and then click **Next**.</span></span>
3. <span data-ttu-id="da181-280">指定定義必須批次處理哪些訊息的批次準則。</span><span class="sxs-lookup"><span data-stu-id="da181-280">Specify a batch criteria, that defines which messages must be batched.</span></span> <span data-ttu-id="da181-281">在此方案中，我們會批次處理所有訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-281">In this solution, we batch all messages.</span></span> <span data-ttu-id="da181-282">因此，選取 hello 使用進階定義 選項，並輸入**1 = 1**。</span><span class="sxs-lookup"><span data-stu-id="da181-282">So, select hello Use advanced definitions option, and enter **1 = 1**.</span></span> <span data-ttu-id="da181-283">這個條件永遠會成立，因此會批次處理所有訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-283">This is a condition which will always be true, and hence all messages will be batched.</span></span> <span data-ttu-id="da181-284">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="da181-284">Click **Next**.</span></span>
   
   ![][17]  
4. <span data-ttu-id="da181-285">指定批次釋放準則。</span><span class="sxs-lookup"><span data-stu-id="da181-285">Specify a batch release criteria.</span></span> <span data-ttu-id="da181-286">從 hello 下拉式方塊，選取**MessageCountBased**，以及**計數**，指定**3**。</span><span class="sxs-lookup"><span data-stu-id="da181-286">From hello drop-box, select **MessageCountBased**, and for **Count**, specify **3**.</span></span> <span data-ttu-id="da181-287">這表示 tooNorthwind 會傳送三個訊息的批次。</span><span class="sxs-lookup"><span data-stu-id="da181-287">This means that a batch of three messages will be sent tooNorthwind.</span></span> <span data-ttu-id="da181-288">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="da181-288">Click **Next**.</span></span>
   
   ![][18]  
5. <span data-ttu-id="da181-289">檢閱 hello 摘要，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="da181-289">Review hello summary and then click **Save**.</span></span> <span data-ttu-id="da181-290">按一下**部署**tooredeploy hello 協議。</span><span class="sxs-lookup"><span data-stu-id="da181-290">Click **Deploy** tooredeploy hello agreement.</span></span>
6. <span data-ttu-id="da181-291">返回 toohello **Tutorial Client**，按一下 **傳送內部發票**，並遵循 hello 提示 toosend hello 發票。</span><span class="sxs-lookup"><span data-stu-id="da181-291">Go back toohello **Tutorial Client**, click **Send In-house Invoice**, and follow hello prompts toosend hello invoice.</span></span> <span data-ttu-id="da181-292">您會注意到因為 hello 批次大小不符，就會在 Northwind 上收到任何發票。</span><span class="sxs-lookup"><span data-stu-id="da181-292">You will notice that no invoice is received at Northwind because hello batch size is not met.</span></span> <span data-ttu-id="da181-293">重複此步驟兩次，所以您需要傳送 tooNorthwind 三則發票訊息。</span><span class="sxs-lookup"><span data-stu-id="da181-293">Repeat this step two more times, so that you have three invoice messages sent tooNorthwind.</span></span> <span data-ttu-id="da181-294">這就符合 hello 3 則訊息的批次釋放準則，您現在應該會看到在 Northwind 上的發票。</span><span class="sxs-lookup"><span data-stu-id="da181-294">This satisfies hello batch release criteria of 3 messages and you should now see an invoice at Northwind.</span></span>

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

