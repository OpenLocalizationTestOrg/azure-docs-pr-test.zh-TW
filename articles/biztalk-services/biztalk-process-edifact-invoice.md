---
title: "教學課程：使用 Azure BizTalk 服務處理 EDIFACT 發票 | Microsoft Docs"
description: "如何建立並設定 Box 連接器或 API 應用程式，並在 Azure App Service 的邏輯應用程式中使用它"
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
ms.openlocfilehash: 4597ee28e4c3b797c0ab050b21a126a95d9e8191
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a><span data-ttu-id="195ac-103">教學課程：使用 Azure BizTalk 服務處理 EDIFACT 發票</span><span class="sxs-lookup"><span data-stu-id="195ac-103">Tutorial: Process EDIFACT invoices using Azure BizTalk Services</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="195ac-104">您可以使用 BizTalk 服務入口網站設定和部署 X12 與 EDIFACT 協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-104">You can use the BizTalk Services Portal to configure and deploy X12 and EDIFACT agreements.</span></span> <span data-ttu-id="195ac-105">在本教學課程中，我們將說明如何建立 EDIFACT 協議以讓交易夥伴彼此交換發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-105">In this tutorial, we look at how to create an EDIFACT agreement for exchanging invoices between trading partners.</span></span> <span data-ttu-id="195ac-106">本教學課程描述端對端商務方案，內容涉及兩個交易夥伴，分別是 Northwind 和 Contoso，他們會交換 EDIFACT 訊息。</span><span class="sxs-lookup"><span data-stu-id="195ac-106">This tutorial is written around an end-to-end business solution involving two trading partners, Northwind and Contoso that exchange EDIFACT messages.</span></span>  

## <a name="sample-based-on-this-tutorial"></a><span data-ttu-id="195ac-107">根據本教學課程所建立的範例</span><span class="sxs-lookup"><span data-stu-id="195ac-107">Sample based on this tutorial</span></span>
<span data-ttu-id="195ac-108">本教學課程描述 **使用 BizTalk 服務傳送 EDIFACT 發票**的範例，您可以從 [MSDN 程式碼資源庫](http://go.microsoft.com/fwlink/?LinkId=401005)下載此範例。</span><span class="sxs-lookup"><span data-stu-id="195ac-108">This tutorial is written around a sample, **Sending EDIFACT Invoices Using BizTalk Services**, which is available to download from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005).</span></span> <span data-ttu-id="195ac-109">您可以使用此範例來完成本教學課程，以了解此範例的建置方式。</span><span class="sxs-lookup"><span data-stu-id="195ac-109">You could use the sample and go through this tutorial to understand how the sample was built.</span></span> <span data-ttu-id="195ac-110">或者，您可以使用本教學課程從頭建立自己的方案。</span><span class="sxs-lookup"><span data-stu-id="195ac-110">Or, you could use this tutorial to create your own solution ground-up.</span></span> <span data-ttu-id="195ac-111">本教學課程鎖定第二種方法，以便您能夠了解此方案的建置方式。</span><span class="sxs-lookup"><span data-stu-id="195ac-111">This tutorial is targeted towards the second approach so that you understand how this solution was built.</span></span> <span data-ttu-id="195ac-112">此外，本教學課程會盡可能與範例保持一致，並對構件使用範例中所使用的相同名稱 (例如，結構描述、轉換)。</span><span class="sxs-lookup"><span data-stu-id="195ac-112">Also, as much as possible, the tutorial is consistent with the sample and uses the same names for artifacts (for example, schemas, transforms) as used in the sample.</span></span>  

> [!NOTE]
> <span data-ttu-id="195ac-113">此方案牽涉到從 EAI 橋接器傳送訊息至 EDI 橋接器，因此會重複使用 [BizTalk 服務橋接器鏈結範例](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) 的範例。</span><span class="sxs-lookup"><span data-stu-id="195ac-113">Because this solution involves sending a message from an EAI bridge to an EDI bridge, it reuses the [BizTalk Services Bridge chaining sample](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) sample.</span></span>  
> 
> 

## <a name="what-does-the-solution-do"></a><span data-ttu-id="195ac-114">此方案有哪些功能？</span><span class="sxs-lookup"><span data-stu-id="195ac-114">What does the solution do?</span></span>
<span data-ttu-id="195ac-115">在此方案中，Northwind 會從 Contoso 收到 EDIFACT 發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-115">In this solution, Northwind receives EDIFACT invoices from Contoso.</span></span> <span data-ttu-id="195ac-116">這些發票未採用標準 EDI 格式。</span><span class="sxs-lookup"><span data-stu-id="195ac-116">These invoices are not in a standard EDI format.</span></span> <span data-ttu-id="195ac-117">因此在將發票傳送至 Northwind 之前，必須先將它轉換為 EDIFACT 發票 (也稱為 INVOIC) 文件。</span><span class="sxs-lookup"><span data-stu-id="195ac-117">So, before sending the invoice to Northwind, it must be transformed to an EDIFACT invoice (also called INVOIC) document.</span></span> <span data-ttu-id="195ac-118">在收到時，Northwind 必須處理 EDIFACT 發票，並回傳控制訊息 (也稱為 CONTRL) 給 Contoso。</span><span class="sxs-lookup"><span data-stu-id="195ac-118">On receipt, Northwind must process the EDIFACT invoice, and return a control message (also called CONTRL) to Contoso.</span></span>

![][1]  

<span data-ttu-id="195ac-119">為了達成此商務案例，Contoso 使用 Microsoft Azure BizTalk 服務所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="195ac-119">To achieve this business scenario, Contoso uses the features provided with Microsoft Azure BizTalk Services.</span></span>

* <span data-ttu-id="195ac-120">Contoso 使用 EAI 橋接器將原始發票轉換為 EDIFACT INVOIC。</span><span class="sxs-lookup"><span data-stu-id="195ac-120">Contoso uses EAI bridges to transform the original invoice to EDIFACT INVOIC.</span></span>
* <span data-ttu-id="195ac-121">EAI 橋接器接著傳送訊息至部署為 BizTalk 服務入口網站中所設定之協議一部分的 EDI 傳送橋接器。</span><span class="sxs-lookup"><span data-stu-id="195ac-121">The EAI bridge then sends the message to an EDI send bridge deployed as part of an agreement configured in the BizTalk Services Portal.</span></span>
* <span data-ttu-id="195ac-122">EDI 傳送橋接器處理 EDIFACT INVOIC 並將其路由傳送至 Northwind。</span><span class="sxs-lookup"><span data-stu-id="195ac-122">The EDI send bridge processes the EDIFACT INVOIC and routes it to Northwind.</span></span>
* <span data-ttu-id="195ac-123">接收到發票之後，Northwind 回傳 CONTRL 訊息給部署為協議一部分的 EDI 接收橋接器。</span><span class="sxs-lookup"><span data-stu-id="195ac-123">After receiving the invoice, Northwind returns a CONTRL message to the EDI receive bridge deployed as part of the agreement.</span></span>  

> [!NOTE]
> <span data-ttu-id="195ac-124">(選擇性) 此方案也會示範如何使用批次功能來批次傳送發票，而不是個別傳送每張發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-124">Optionally, this solution also demonstrates how to use batching to send the invoices in batches, instead of sending each invoice separately.</span></span>  
> 
> 

<span data-ttu-id="195ac-125">為了完成案例，我們使用服務匯流排佇列將發票從 Contoso 傳送至 Northwind，或從 Northwind 接收通知。</span><span class="sxs-lookup"><span data-stu-id="195ac-125">To complete the scenario, we use Service Bus queues to send invoice from Contoso to Northwind or receive acknowledgement from Northwind.</span></span> <span data-ttu-id="195ac-126">這些佇列可以透過用戶端應用程式 (可經由下載取得) 來予以建立，並且會包含在本教學課程所提供的範例封裝中。</span><span class="sxs-lookup"><span data-stu-id="195ac-126">These queues can be created using a client application, which is available as a download and is included in the sample package that is available as part of this tutorial.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="195ac-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="195ac-127">Prerequisites</span></span>
* <span data-ttu-id="195ac-128">您必須具有服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="195ac-128">You must have a Service Bus namespace.</span></span> <span data-ttu-id="195ac-129">如需建立命名空間的指示，請參閱 [作法：建立或修改服務匯流排服務命名空間](https://msdn.microsoft.com/library/azure/hh674478.aspx)。</span><span class="sxs-lookup"><span data-stu-id="195ac-129">For instructions on creating a namespace, see [How To: Create or Modify a Service Bus Service Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx).</span></span> <span data-ttu-id="195ac-130">讓我們假設您已佈建服務匯流排命名空間，且其名稱為 **edifactbts**。</span><span class="sxs-lookup"><span data-stu-id="195ac-130">Let us assume that you already have a Service Bus namespace provisioned, called **edifactbts**.</span></span>
* <span data-ttu-id="195ac-131">您必須擁有 BizTalk 服務訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="195ac-131">You must have a BizTalk Services subscription.</span></span> <span data-ttu-id="195ac-132">如需相關指示，請參閱 [使用 Azure 傳統入口網站建立 BizTalk 服務](http://go.microsoft.com/fwlink/?LinkID=302280)。</span><span class="sxs-lookup"><span data-stu-id="195ac-132">For instructions, see [Create a BizTalk Service using Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=302280).</span></span> <span data-ttu-id="195ac-133">在本教學課程中，讓我們假設您擁有 BizTalk 服務訂用帳戶，且其名稱為 **contosowabs**。</span><span class="sxs-lookup"><span data-stu-id="195ac-133">For this tutorial, let us assume you have a BizTalk Services subscription, called **contosowabs**.</span></span>
* <span data-ttu-id="195ac-134">在 BizTalk 服務入口網站註冊 BizTalk 服務訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="195ac-134">Register your BizTalk Services subscription on the BizTalk Services Portal.</span></span> <span data-ttu-id="195ac-135">如需相關指示，請參閱 [在 BizTalk 服務入口網站註冊 BizTalk 服務部署](https://msdn.microsoft.com/library/hh689837.aspx)</span><span class="sxs-lookup"><span data-stu-id="195ac-135">For instructions, see [Registering a BizTalk Service Deployment on the BizTalk Services Portal](https://msdn.microsoft.com/library/hh689837.aspx)</span></span>
* <span data-ttu-id="195ac-136">您必須安裝 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="195ac-136">You must have Visual Studio installed.</span></span>
* <span data-ttu-id="195ac-137">您必須安裝 BizTalk 服務 SDK。</span><span class="sxs-lookup"><span data-stu-id="195ac-137">You must have BizTalk Services SDK installed.</span></span> <span data-ttu-id="195ac-138">您可以從 [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)</span><span class="sxs-lookup"><span data-stu-id="195ac-138">You can download the SDK from [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)</span></span>  

## <a name="step-1-create-the-service-bus-queues"></a><span data-ttu-id="195ac-139">步驟 1：建立服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="195ac-139">Step 1: Create the Service Bus queues</span></span>
<span data-ttu-id="195ac-140">此方案使用服務匯流排佇列以讓交易夥伴彼此交換訊息。</span><span class="sxs-lookup"><span data-stu-id="195ac-140">This solution uses Service Bus queues to exchange messages between trading partners.</span></span> <span data-ttu-id="195ac-141">Contoso 和 Northwind 會傳送訊息至 EAI 和 (或) EDI 橋接器從中取用訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="195ac-141">Contoso and Northwind send messages to the queues from where the EAI and/or EDI bridges consume them.</span></span> <span data-ttu-id="195ac-142">在此方案中，您需要三個服務匯流排佇列：</span><span class="sxs-lookup"><span data-stu-id="195ac-142">For this solution, you need three Service Bus queues:</span></span>

* <span data-ttu-id="195ac-143">**northwindreceive** – Northwind 透過此佇列從 Contoso 接收發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-143">**northwindreceive** – Northwind receives the invoice from Contoso over this queue.</span></span>
* <span data-ttu-id="195ac-144">**contosoreceive** – Contoso 透過此佇列從 Northwind 接收通知。</span><span class="sxs-lookup"><span data-stu-id="195ac-144">**contosoreceive** – Contoso receives the acknowledgement from Northwind over this queue.</span></span>
* <span data-ttu-id="195ac-145">**suspended** – 所有擱置的訊息會路由傳送至此佇列。</span><span class="sxs-lookup"><span data-stu-id="195ac-145">**suspended** – All suspended messages are routed to this queue.</span></span> <span data-ttu-id="195ac-146">如果訊息在處理期間失敗，則會加以擱置。</span><span class="sxs-lookup"><span data-stu-id="195ac-146">Messages are suspended if they fail during processing.</span></span>

<span data-ttu-id="195ac-147">您可以使用範例封裝中包含的用戶端應用程式建立這些服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="195ac-147">You can create these Service Bus queues by using a client application included in the sample package.</span></span>  

1. <span data-ttu-id="195ac-148">從您下載範例的位置，開啟 **使用 BizTalk 服務 EDI Bridges.sln 傳送發票的教學課程**。</span><span class="sxs-lookup"><span data-stu-id="195ac-148">From the location where you downloaded the sample, open **Tutorial Sending Invoices Using BizTalk Services EDI Bridges.sln**.</span></span>
2. <span data-ttu-id="195ac-149">按 **F5** 以建置並啟動 **Tutorial Client** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="195ac-149">Press **F5** to build and start the **Tutorial Client** application.</span></span>
3. <span data-ttu-id="195ac-150">在畫面中輸入服務匯流排 ACS 命名空間、簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="195ac-150">In the screen, enter the Service Bus ACS namespace, issuer name, and issuer key.</span></span>
   
   ![][2]  
4. <span data-ttu-id="195ac-151">隨即出現訊息方塊提示，指出將會在服務匯流排命名空間中建立三個佇列。</span><span class="sxs-lookup"><span data-stu-id="195ac-151">A message box prompts that three queues will be created in your Service Bus namespace.</span></span> <span data-ttu-id="195ac-152">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-152">Click **OK**.</span></span>
5. <span data-ttu-id="195ac-153">讓 Tutorial Client 保持執行狀態。</span><span class="sxs-lookup"><span data-stu-id="195ac-153">Leave the Tutorial Client running.</span></span> <span data-ttu-id="195ac-154">開啟，按一下 [服務匯流排] > 您的服務匯流排命名空間 > [佇列]，然後驗證是否已建立這三個佇列。</span><span class="sxs-lookup"><span data-stu-id="195ac-154">Open the , click **Service Bus** > ***your Service Bus namespace*** > **Queues**, and verify that the three queues are created.</span></span>  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a><span data-ttu-id="195ac-155">步驟 2：建立和部署交易夥伴協議</span><span class="sxs-lookup"><span data-stu-id="195ac-155">Step 2: Create and deploy trading partner agreement</span></span>
<span data-ttu-id="195ac-156">建立 Contoso 與 Northwind 之間的交易夥伴協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-156">Create a trading partner agreement between Contoso and Northwind.</span></span> <span data-ttu-id="195ac-157">交易夥伴協議定義兩個商務夥伴之間的交易協議，例如要使用的訊息結構描述、要使用的訊息通訊協定等等。交易夥伴協議包含兩個 EDI 橋接器，一個用來傳送訊息給交易夥伴 (稱為 **EDI 傳送橋接器**)，另一個接收來自交易夥伴的訊息 (稱為 **EDI 接收橋接器**)。</span><span class="sxs-lookup"><span data-stu-id="195ac-157">A trading partner agreement defines a trade contract between the two business partners, such as which message schema to use, which messaging protocol to use, etc. A trading partner agreement includes two EDI bridges, one to send messages to trading partners (called the **EDI Send bridge**) and one to receive messages from trading partners (called the **EDI Receive bridge**).</span></span>

<span data-ttu-id="195ac-158">在此方案的內容中，EDI 傳送橋接器對應到協議的傳送端，並且會用來將 EDIFACT 發票從 Contoso 傳送至 Northwind。</span><span class="sxs-lookup"><span data-stu-id="195ac-158">In the context of this solution, the EDI send bridge corresponds to the send-side of the agreement and is used to send the EDIFACT invoice from Contoso to Northwind.</span></span> <span data-ttu-id="195ac-159">同樣地，EDI 接收橋接器則對應到協議的接收端，並且會用來從 Northwind 接收通知。</span><span class="sxs-lookup"><span data-stu-id="195ac-159">Similarly, the EDI receive bridge corresponds to the receive-side of the agreement and is used to receive acknowledgements from Northwind.</span></span>  

### <a name="create-the-trading-partners"></a><span data-ttu-id="195ac-160">建立交易夥伴</span><span class="sxs-lookup"><span data-stu-id="195ac-160">Create the trading partners</span></span>
<span data-ttu-id="195ac-161">若要開始，請建立 Contoso 和 Northwind 的交易夥伴。</span><span class="sxs-lookup"><span data-stu-id="195ac-161">To start with, create trading partners for Contoso and Northwind.</span></span>  

1. <span data-ttu-id="195ac-162">在 BizTalk 服務入口網站的 [夥伴] 索引標籤上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="195ac-162">In the BizTalk Services Portal, on the **Partners** tab, click **Add**.</span></span>
2. <span data-ttu-id="195ac-163">在 [新增夥伴] 頁面上，輸入 **Contoso** 當做夥伴名稱，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="195ac-163">In the New partner page, enter **Contoso** as a partner name, and then click **Save**.</span></span>
3. <span data-ttu-id="195ac-164">重複此步驟來建立第二個夥伴 ( **Northwind**)。</span><span class="sxs-lookup"><span data-stu-id="195ac-164">Repeat the step to create the second partner, **Northwind**.</span></span>  

### <a name="create-the-agreement"></a><span data-ttu-id="195ac-165">建立協議</span><span class="sxs-lookup"><span data-stu-id="195ac-165">Create the agreement</span></span>
<span data-ttu-id="195ac-166">交易夥伴的商務設定檔之間會建立交易夥伴協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-166">Trading partner agreements are created between business profiles of trading partners.</span></span> <span data-ttu-id="195ac-167">此方案會使用我們建立夥伴時自動建立的預設夥伴設定檔。</span><span class="sxs-lookup"><span data-stu-id="195ac-167">This solution uses the default partner profiles that are automatically created when we created the partners.</span></span>  

1. <span data-ttu-id="195ac-168">在 BizTalk 服務入口網站中，按一下 [協議] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="195ac-168">In the BizTalk Services Portal, click **Agreements** > **Add**.</span></span>
2. <span data-ttu-id="195ac-169">在新協議的 [一般設定] 頁面上指定值 (如下圖所示)，然後按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="195ac-169">In the new agreement’s **General Settings** page, specify the values as shown in the image below, and then click **Continue**.</span></span>
   
   ![][3]  
   
   <span data-ttu-id="195ac-170">按一下 [繼續] 之後，[接收設定] 和 [傳送設定] 這兩個索引標籤會變成可用狀態。</span><span class="sxs-lookup"><span data-stu-id="195ac-170">After you click **Continue**, two tabs, **Receive Settings** and **Send Settings** become available.</span></span>
3. <span data-ttu-id="195ac-171">建立 Contoso 與 Northwind 之間的傳送協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-171">Create the send agreement between Contoso and Northwind.</span></span> <span data-ttu-id="195ac-172">此協議控管 Contoso 如何將 EDIFACT 發票傳送至 Northwind。</span><span class="sxs-lookup"><span data-stu-id="195ac-172">This agreement governs how Contoso sends the EDIFACT invoice to Northwind.</span></span>
   
   1. <span data-ttu-id="195ac-173">按一下 [傳送設定] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-173">Click **Send Settings**.</span></span>
   2. <span data-ttu-id="195ac-174">保留 [輸入 URL]、[轉換] 和 [批次處理] 索引標籤上的預設值。</span><span class="sxs-lookup"><span data-stu-id="195ac-174">Retain the default values on the **Inbound URL**, **Transform**, and **Batching** tabs.</span></span>
   3. <span data-ttu-id="195ac-175">在 [通訊協定] 索引標籤的 [結構描述] 區段底下，上傳 **EFACT_D93A_INVOIC.xsd** 結構描述。</span><span class="sxs-lookup"><span data-stu-id="195ac-175">On the **Protocol** tab, under the **Schemas** section, upload the **EFACT_D93A_INVOIC.xsd** schema.</span></span> <span data-ttu-id="195ac-176">此結構描述可在範例封裝內取得。</span><span class="sxs-lookup"><span data-stu-id="195ac-176">This schema is available with the sample package.</span></span>
      
      ![][4]  
   4. <span data-ttu-id="195ac-177">在 [傳輸] 索引標籤上，指定服務匯流排佇列的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="195ac-177">On the **Transport** tab, specify the details for the Service Bus queues.</span></span> <span data-ttu-id="195ac-178">對於傳送端協議，我們使用 **northwindreceive** 佇列來將 EDIFACT 發票傳送至 Northwind，並使用 **suspended** 佇列來路由傳送任何在處理期間失敗且因而擱置的訊息。</span><span class="sxs-lookup"><span data-stu-id="195ac-178">For the send-side agreement, we use the **northwindreceive** queue to send the EDIFACT invoice to Northwind, and the **suspended** queue to route any messages that fail during processing and are suspended.</span></span> <span data-ttu-id="195ac-179">您已在**步驟 1：建立服務匯流排佇列** (在本主題) 中建立這些佇列。</span><span class="sxs-lookup"><span data-stu-id="195ac-179">You created these queues in **Step 1: Create the Service Bus queues** (in this topic).</span></span>
      
      ![][5]  
      
      <span data-ttu-id="195ac-180">在 [傳輸設定] > [傳輸類型] 和 [訊息擱置設定] > [傳輸類型] 底下，選取 [Azure 服務匯流排] 並提供值 (如上圖所示)。</span><span class="sxs-lookup"><span data-stu-id="195ac-180">Under **Transport Settings > Transport type** and **Message Suspension Settings > Transport type**, select Azure Service Bus and provide the values as shown in the image.</span></span>
4. <span data-ttu-id="195ac-181">建立 Contoso 與 Northwind 之間的接收協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-181">Create the receive agreement between Contoso and Northwind.</span></span> <span data-ttu-id="195ac-182">此協議控管 Contoso 如何從 Northwind 接收通知。</span><span class="sxs-lookup"><span data-stu-id="195ac-182">This agreement governs how Contoso receives the acknowledgement from Northwind.</span></span>
   
   1. <span data-ttu-id="195ac-183">按一下 [接收設定] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-183">Click **Receive Settings**.</span></span>
   2. <span data-ttu-id="195ac-184">保留 [傳輸] 和 [轉換] 索引標籤上的預設值。</span><span class="sxs-lookup"><span data-stu-id="195ac-184">Retain the default values on the **Transport** and **Transform** tabs.</span></span>
   3. <span data-ttu-id="195ac-185">在 [通訊協定] 索引標籤的 [結構描述] 區段底下，上傳 **EFACT_4.1_CONTRL.xsd** 結構描述。</span><span class="sxs-lookup"><span data-stu-id="195ac-185">On the **Protocol** tab, under the **Schemas** section, upload the **EFACT_4.1_CONTRL.xsd** schema.</span></span> <span data-ttu-id="195ac-186">此結構描述可在範例封裝內取得。</span><span class="sxs-lookup"><span data-stu-id="195ac-186">This schema is available with the sample package.</span></span>
   4. <span data-ttu-id="195ac-187">在 [路由]  索引標籤上，建立篩選器以確保只有來自 Northwind 的通知會路由傳送至 Contoso。</span><span class="sxs-lookup"><span data-stu-id="195ac-187">On the **Route** tab, create a filter to ensure that only acknowledgements from Northwind are routed to Contoso.</span></span> <span data-ttu-id="195ac-188">在 [路由設定] 底下，按一下 [新增] 以建立路由篩選條件。</span><span class="sxs-lookup"><span data-stu-id="195ac-188">Under **Route Settings**, click **Add** to create the routing filter.</span></span>
      
      ![][6]  
      
      1. <span data-ttu-id="195ac-189">提供 [規則名稱]、[路由規則] 和 [路由目的地] 的值 (如上圖所示)。</span><span class="sxs-lookup"><span data-stu-id="195ac-189">Provide values for **Rule Name**, **Route rule**, and **Route destination** as shown in the image.</span></span>
      2. <span data-ttu-id="195ac-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-190">Click **Save**.</span></span>
   5. <span data-ttu-id="195ac-191">再次在 [路由] 索引標籤中，指定要將擱置的通知 (在處理期間失敗的通知) 傳送到哪裡。</span><span class="sxs-lookup"><span data-stu-id="195ac-191">On the **Route** tab again, specify where suspended acknowledgements (acknowledgements that fail during processing) are routed to.</span></span> <span data-ttu-id="195ac-192">將傳輸類型設為 [Azure 服務匯流排]、將路由目的地類型設為 [佇列]、將驗證類型設為 [共用存取簽章] \(SAS)、提供服務匯流排命名空間的 SAS 連接字串，然後在佇列名稱中輸入 **suspended**。</span><span class="sxs-lookup"><span data-stu-id="195ac-192">Set the transport type to Azure Service Bus, route destination type to **Queue**, authentication type to **Shared Access Signature** (SAS), provide the SAS connection string for the Service Bus namespace, and then enter the queue name as **suspended**.</span></span>
5. <span data-ttu-id="195ac-193">最後，按一下 [部署]  來部署協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-193">Finally, click **Deploy** to deploy the agreement.</span></span> <span data-ttu-id="195ac-194">請記下傳送和接收協議部署所在的端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-194">Note the endpoints where the send and receive agreements get deployed.</span></span>
   
   * <span data-ttu-id="195ac-195">在 [傳送設定] 索引標籤的 [輸入 URL] 底下，記下該端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-195">On the **Send Settings** tab, under **Inbound URL**, note the endpoint.</span></span> <span data-ttu-id="195ac-196">若要使用 EDI 傳送橋接器將訊息從 Contoso 傳送至 Northwind，您必須傳送訊息給此端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-196">To send a message from Contoso to Northwind using the EDI send bridge, you must send a message to this endpoint.</span></span>
   * <span data-ttu-id="195ac-197">在 [接收設定] 索引標籤的 [傳輸] 底下，記下該端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-197">On the **Receive Settings** tab, under **Transport**, note the endpoint.</span></span> <span data-ttu-id="195ac-198">若要使用 EDI 接收橋接器將訊息從 Northwind 傳送至 Contoso，您必須傳送訊息給此端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-198">To send a message from Northwind to Contoso using the EDI receive bridge, you must send a message to this endpoint.</span></span>  

## <a name="step-3-create-and-deploy-the-biztalk-services-project"></a><span data-ttu-id="195ac-199">步驟 3：建立和部署 BizTalk 服務專案</span><span class="sxs-lookup"><span data-stu-id="195ac-199">Step 3: Create and deploy the BizTalk Services project</span></span>
<span data-ttu-id="195ac-200">在上一個步驟中，您部署了 EDI 傳送和接收協議，以處理 EDIFACT 發票和通知。</span><span class="sxs-lookup"><span data-stu-id="195ac-200">In the previous step, you deployed the EDI send and receive agreements to process EDIFACT invoices and acknowledgements.</span></span> <span data-ttu-id="195ac-201">這些協議只可以處理符合標準 EDIFACT 訊息結構描述的訊息。</span><span class="sxs-lookup"><span data-stu-id="195ac-201">These agreements can only process messages that conform to the standard EDIFACT message schema.</span></span> <span data-ttu-id="195ac-202">不過，根據此方案的案例，Contoso 會以內部專屬的結構描述傳送發票給 Northwind。</span><span class="sxs-lookup"><span data-stu-id="195ac-202">However, per the scenario for this solution, Contoso sends an invoice to Northwind in an in-house proprietary schema.</span></span> <span data-ttu-id="195ac-203">因此，訊息在傳送給 EDI 傳送橋接器之前，必須先從內部結構描述轉換為標準 EDIFACT 發票結構描述。</span><span class="sxs-lookup"><span data-stu-id="195ac-203">So, before the message is sent to the EDI send bridge, it must be transformed from the in-house schema to the standard EDIFACT invoice schema.</span></span> <span data-ttu-id="195ac-204">BizTalk 服務 EAI 專案會負責執行此工作。</span><span class="sxs-lookup"><span data-stu-id="195ac-204">The BizTalk Services EAI project does that.</span></span>

<span data-ttu-id="195ac-205">負責轉換訊息的 BizTalk 服務專案 **InvoiceProcessingBridge**也包含在您下載的範例中。</span><span class="sxs-lookup"><span data-stu-id="195ac-205">The BizTalk Services project, **InvoiceProcessingBridge**, that transforms the message is also included as part of the sample you downloaded.</span></span> <span data-ttu-id="195ac-206">此專案包括下列構件：</span><span class="sxs-lookup"><span data-stu-id="195ac-206">The project includes the following artifacts:</span></span>

* <span data-ttu-id="195ac-207">**INHOUSEINVOICE.XSD** – 傳送至 Northwind 之內部發票的結構描述。</span><span class="sxs-lookup"><span data-stu-id="195ac-207">**INHOUSEINVOICE.XSD** – Schema of the in-house invoice that is sent to Northwind.</span></span>
* <span data-ttu-id="195ac-208">**EFACT_D93A_INVOIC.XSD** – 標準 EDIFACT 發票的結構描述。</span><span class="sxs-lookup"><span data-stu-id="195ac-208">**EFACT_D93A_INVOIC.XSD** – Schema of the standard EDIFACT invoice.</span></span>
* <span data-ttu-id="195ac-209">**EFACT_4.1_CONTRL.XSD** – Northwind 傳送給 Contoso 之 EDIFACT 通知的結構描述。</span><span class="sxs-lookup"><span data-stu-id="195ac-209">**EFACT_4.1_CONTRL.XSD** – Schema of the EDIFACT acknowledgement that Northwind sends to Contoso.</span></span>
* <span data-ttu-id="195ac-210">**INHOUSEINVOICE_to_D93AINVOIC.TRFM** – 將內部發票結構描述對應至標準 EDIFACT 發票結構描述的轉換。</span><span class="sxs-lookup"><span data-stu-id="195ac-210">**INHOUSEINVOICE_to_D93AINVOIC.TRFM** – The transform that maps the in-house invoice schema to the standard EDIFACT invoice schema.</span></span>  

### <a name="create-the-biztalk-services-project"></a><span data-ttu-id="195ac-211">建立 BizTalk 服務專案</span><span class="sxs-lookup"><span data-stu-id="195ac-211">Create the BizTalk Services project</span></span>
1. <span data-ttu-id="195ac-212">在 Visual Studio 方案中，展開 InvoiceProcessingBridge 專案，然後開啟 **MessageFlowItinerary.bcs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="195ac-212">In the Visual Studio solution, expand the InvoiceProcessingBridge project, and then open the **MessageFlowItinerary.bcs** file.</span></span>
2. <span data-ttu-id="195ac-213">在畫布上任何位置按一下，然後在屬性方塊中設定 [BizTalk 服務 URL]  ，以指定 BizTalk 服務訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="195ac-213">Click anywhere on the canvas and set the **BizTalk Service URL** in the property box to specify your BizTalk Services subscription name.</span></span> <span data-ttu-id="195ac-214">例如， `https://contosowabs.biztalk.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="195ac-214">For example, `https://contosowabs.biztalk.windows.net`.</span></span>
   
   ![][7]  
3. <span data-ttu-id="195ac-215">從工具箱拖曳 **Xml 單向橋接器** 到畫布上。</span><span class="sxs-lookup"><span data-stu-id="195ac-215">From the toolbox, drag an **Xml One-Way Bridge** to the canvas.</span></span> <span data-ttu-id="195ac-216">將橋接器的 [實體名稱] 和 [相對位址] 屬性設定為 [ProcessInvoiceBridge]。</span><span class="sxs-lookup"><span data-stu-id="195ac-216">Set the **Entity Name** and **Relative Address** properties of the bridge to **ProcessInvoiceBridge**.</span></span> <span data-ttu-id="195ac-217">按兩下 [ProcessInvoiceBridge]  以開啟橋接器設定介面。</span><span class="sxs-lookup"><span data-stu-id="195ac-217">Double-click **ProcessInvoiceBridge** to open the bridge configuration surface.</span></span>
4. <span data-ttu-id="195ac-218">在 [訊息類型] 方塊中，按一下加號 (**+**) 按鈕，以指定傳入訊息的結構描述。</span><span class="sxs-lookup"><span data-stu-id="195ac-218">Within the **Message Types** box, click the plus (**+**) button to specify the schema of the incoming message.</span></span> <span data-ttu-id="195ac-219">因為 EAI 橋接器的傳入訊息一律是內部發票，因此請將此項目設為 [INHOUSEINVOICE] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-219">Because the incoming message for the EAI bridge is always the in-house invoice, set this to **INHOUSEINVOICE**.</span></span>
   
   ![][8]  
5. <span data-ttu-id="195ac-220">按一下 [Xml 轉換] 圖形，並在屬性方塊中，針對 [對應] 屬性按一下省略符號 (**...**) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="195ac-220">Click the **Xml Transform** shape, and in the property box, for the **Maps** property, click the ellipsis (**...**) button.</span></span> <span data-ttu-id="195ac-221">在 [選取對應] 對話方塊中，選取 **INHOUSEINVOICE_to_D93AINVOIC** 轉換檔案，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="195ac-221">In the **Maps Selection** dialog box, select the **INHOUSEINVOICE_to_D93AINVOIC** transform file, and then click **OK**.</span></span>
   
   ![][9]  
6. <span data-ttu-id="195ac-222">返回 **MessageFlowItinerary.bcs**，然後將 [雙向外部服務端點] 從工具箱拖曳至 **ProcessInvoiceBridge** 右邊。</span><span class="sxs-lookup"><span data-stu-id="195ac-222">Go back to **MessageFlowItinerary.bcs**, and from the toolbox, drag a **Two-Way External Service Endpoint** to the right of the **ProcessInvoiceBridge**.</span></span> <span data-ttu-id="195ac-223">將其 [實體名稱] 屬性設為 [EDIBridge]。</span><span class="sxs-lookup"><span data-stu-id="195ac-223">Set its **Entity Name** property to **EDIBridge**.</span></span>
7. <span data-ttu-id="195ac-224">在 [方案總管] 中，展開 **MessageFlowItinerary.bcs**，然後按兩下 **EDIBridge.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="195ac-224">In the Solution Explorer, expand the **MessageFlowItinerary.bcs** and double-click the **EDIBridge.config** file.</span></span> <span data-ttu-id="195ac-225">將 **EDIBridge.config** 的內容更換為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="195ac-225">Replace the content of the **EDIBridge.config** with the following.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="195ac-226">為何需要編輯 .config 檔案？</span><span class="sxs-lookup"><span data-stu-id="195ac-226">Why do I need to edit the .config file?</span></span> <span data-ttu-id="195ac-227">我們新增至橋接器設計工具畫布上的外部服務端點代表我們稍早部署的 EDI 橋接器。</span><span class="sxs-lookup"><span data-stu-id="195ac-227">The external service endpoint that we added to the bridge designer canvas represents the EDI bridges that we deployed earlier.</span></span> <span data-ttu-id="195ac-228">EDI 橋接器是具有傳送和接收端的雙向橋接器。</span><span class="sxs-lookup"><span data-stu-id="195ac-228">EDI bridges are two-way bridges, with a send and receive side.</span></span> <span data-ttu-id="195ac-229">不過，我們新增至橋接器設計工具的 EAI 橋接器是單向橋接器。</span><span class="sxs-lookup"><span data-stu-id="195ac-229">However, the EAI bridge that we added to the bridge designer is a one-way bridge.</span></span> <span data-ttu-id="195ac-230">因此，為了處理兩個橋接器的不同訊息交換模式，我們使用自訂的橋接器行為，將其設定納入 .config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="195ac-230">So, to handle the different message exchange patterns of the two bridges, we use a custom bridge behavior by including its configuration in the .config file.</span></span> <span data-ttu-id="195ac-231">此外，自訂行為也會處理 EDI 傳送橋接器端點的驗證。這個自訂行為是可從 [BizTalk 服務橋接器鏈結範例 - EAI 到 EDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) 中取得的另一個範例。</span><span class="sxs-lookup"><span data-stu-id="195ac-231">Additionally, the custom behavior also handles the authentication to the EDI send bridge endpoint.This custom behavior is available as a separate sample at [BizTalk Services Bridge chaining sample - EAI to EDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104).</span></span> <span data-ttu-id="195ac-232">此方案重複使用該範例。</span><span class="sxs-lookup"><span data-stu-id="195ac-232">This solution reuses the sample.</span></span>  
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
             <!-- Enter the ACS namespace, issuer name and issuer secret of the BizTalk Services deployment -->
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
           Copy the Endpoint URL and paste it in the below address field
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
8. <span data-ttu-id="195ac-233">更新 EDIBridge.config 檔案以納入設定詳細資料</span><span class="sxs-lookup"><span data-stu-id="195ac-233">Update the EDIBridge.config file to include configuration details</span></span>
   
   * <span data-ttu-id="195ac-234">在 [傳輸設定] &gt; [傳輸類型] *<behaviors>*下，提供與 BizTalk 服務訂用帳戶相關聯的 ACS 命名空間和金鑰。</span><span class="sxs-lookup"><span data-stu-id="195ac-234">Under *<behaviors>*, provide the ACS namespace and key associated with the BizTalk Services subscription.</span></span>
   * <span data-ttu-id="195ac-235">在 [傳輸設定] &gt; [傳輸類型] *<client>*下，提供 EDI 傳送協議部署所在的端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-235">Under *<client>*, provide the endpoint where the EDI send agreement is deployed.</span></span>
   
   <span data-ttu-id="195ac-236">儲存變更並關閉設定檔。</span><span class="sxs-lookup"><span data-stu-id="195ac-236">Save changes and close the configuration file.</span></span>
9. <span data-ttu-id="195ac-237">從 [工具箱] 中按一下 [連接器]，然後聯結 [ProcessInvoiceBridge] 和 [EDIBridge] 元件。</span><span class="sxs-lookup"><span data-stu-id="195ac-237">From the Toolbox, click the **Connector** and join the **ProcessInvoiceBridge** and **EDIBridge** components.</span></span> <span data-ttu-id="195ac-238">選取連接器，然後在 [屬性] 方塊中將 [篩選條件] 設定為 [全部符合]。</span><span class="sxs-lookup"><span data-stu-id="195ac-238">Select the connector, and in Properties box, set **Filter Condition** to **Match All**.</span></span> <span data-ttu-id="195ac-239">這可確保 EAI 橋接器處理的所有訊息都會路由傳送至 EDI 橋接器。</span><span class="sxs-lookup"><span data-stu-id="195ac-239">This ensures that all messages processed by the EAI bridge are routed to the EDI bridge.</span></span>
   
   ![][10]  
10. <span data-ttu-id="195ac-240">儲存方案的變更。</span><span class="sxs-lookup"><span data-stu-id="195ac-240">Save changes to the solution.</span></span>  

### <a name="deploy-the-project"></a><span data-ttu-id="195ac-241">部署專案</span><span class="sxs-lookup"><span data-stu-id="195ac-241">Deploy the project</span></span>
1. <span data-ttu-id="195ac-242">在您建立 BizTalk 服務專案的電腦上，下載並安裝您 BizTalk 服務訂用帳戶的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="195ac-242">On the computer where you created the BizTalk Services project, download and install the SSL certificate for your BizTalk Services subscription.</span></span> <span data-ttu-id="195ac-243">從 [BizTalk 服務] 底下按一下 [儀表板]，然後按一下 [下載 SSL 憑證]。</span><span class="sxs-lookup"><span data-stu-id="195ac-243">From , under BizTalk Services, click **Dashboard**, and then click **Download SSL Certificate**.</span></span> <span data-ttu-id="195ac-244">按兩下憑證，並依照提示來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="195ac-244">Double-click the certificate and follow the prompt to complete the installation.</span></span> <span data-ttu-id="195ac-245">確定您是在 [受信任的根憑證授權單位] 憑證存放區底下安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="195ac-245">Make sure you install the certificate under **Trusted Root Certification Authorities** certificate store.</span></span>
2. <span data-ttu-id="195ac-246">在 Visual Studio 的 [方案總管] 中，以滑鼠右鍵按一下 **InvoiceProcessingBridge** 專案，然後按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="195ac-246">In Visual Studio Solution Explorer, right-click the **InvoiceProcessingBridge** project, and then click **Deploy**.</span></span>
3. <span data-ttu-id="195ac-247">提供如下圖所示的值，然後按一下 [部署] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-247">Provide the values as shown in the image, and then click **Deploy**.</span></span> <span data-ttu-id="195ac-248">您可以從 BizTalk 服務儀表板按一下 [連接資訊]  ，以取得 BizTalk 服務的 ACS 認證。</span><span class="sxs-lookup"><span data-stu-id="195ac-248">You can get the ACS credentials for BizTalk Services by clicking **Connection Information** from the BizTalk Services dashboard.</span></span>
   
   ![][11]  
   
   <span data-ttu-id="195ac-249">從輸出窗格中，複製 EAI 橋接器部署所在的端點，比方說 `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`。</span><span class="sxs-lookup"><span data-stu-id="195ac-249">From the output pane, copy the endpoint where the EAI bridge is deployed, for example, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`.</span></span> <span data-ttu-id="195ac-250">您稍後將需要此端點 URL。</span><span class="sxs-lookup"><span data-stu-id="195ac-250">You will need this endpoint URL later.</span></span>  

## <a name="step-4-test-the-solution"></a><span data-ttu-id="195ac-251">步驟 4：測試方案</span><span class="sxs-lookup"><span data-stu-id="195ac-251">Step 4: Test the solution</span></span>
<span data-ttu-id="195ac-252">在本主題中，我們將說明如何使用範例中提供的 **Tutorial Client** 應用程式來測試方案。</span><span class="sxs-lookup"><span data-stu-id="195ac-252">In this topic, we look at how to test the solution by using the **Tutorial Client** application provided as part of the sample.</span></span>  

1. <span data-ttu-id="195ac-253">在 Visual Studio 中，按 F5 以啟動 **Tutorial Client**。</span><span class="sxs-lookup"><span data-stu-id="195ac-253">In Visual Studio, press F5 to start the **Tutorial Client**.</span></span>
2. <span data-ttu-id="195ac-254">畫面上必須已預先填入我們用來建立服務匯流排佇列之步驟所指定的值。</span><span class="sxs-lookup"><span data-stu-id="195ac-254">The screen must have the values prepopulated from the step where we created the Service Bus queues.</span></span> <span data-ttu-id="195ac-255">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-255">Click **Next**.</span></span>
3. <span data-ttu-id="195ac-256">在下一個視窗中，提供 BizTalk 服務訂用帳戶的 ACS 認證，以及 EAI 和 EDI (接收) 橋接器部署所在的端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-256">In the next window, provide ACS credentials for BizTalk Services subscription, and the endpoints where EAI and EDI (receive) bridges are deployed.</span></span>
   
   <span data-ttu-id="195ac-257">您已在上一個步驟中複製 EAI 橋接器端點。</span><span class="sxs-lookup"><span data-stu-id="195ac-257">You had copied the EAI bridge endpoint in the previous step.</span></span> <span data-ttu-id="195ac-258">至於 EDI 接收橋接器端點，請在 BizTalk 服務入口網站中，移至 [協議] > [接收設定] > [傳輸] > [端點]。</span><span class="sxs-lookup"><span data-stu-id="195ac-258">For EDI receive bridge endpoint, in the BizTalk Services Portal, go to the agreement > Receive Settings > Transport > Endpoint.</span></span>
   
   ![][12]  
4. <span data-ttu-id="195ac-259">在下一個視窗中，於 Contoso 底下按一下 [傳送內部發票]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="195ac-259">In the next window, under Contoso, click the **Send In-house Invoice** button.</span></span> <span data-ttu-id="195ac-260">在 [檔案開啟] 對話方塊中，開啟 INHOUSEINVOICE.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="195ac-260">In the File open dialog box, open the INHOUSEINVOICE.txt file.</span></span> <span data-ttu-id="195ac-261">檢查檔案的內容，然後按一下 [確定]  以傳送發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-261">Examine the content of the file and then click **OK** to send the invoice.</span></span>
   
   ![][13]  
5. <span data-ttu-id="195ac-262">幾秒鐘內 Northwind 就會收到發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-262">In a few seconds the invoice is received at Northwind.</span></span> <span data-ttu-id="195ac-263">按一下 [檢視訊息]  連結以查看 Northwind 收到的發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-263">Click the **View Message** link to see the invoice received by Northwind.</span></span> <span data-ttu-id="195ac-264">請注意在 Contoso 所傳送的發票是內部結構描述的情況下，Northwind 所收到的發票是如何變成標準 EDIFACT 結構描述的。</span><span class="sxs-lookup"><span data-stu-id="195ac-264">Notice how the invoice received by Northwind is in standard EDIFACT schema while the one sent by Contoso was an in-house schema.</span></span>
   
   ![][14]  
6. <span data-ttu-id="195ac-265">選取發票，然後按一下 [傳送通知] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-265">Select the invoice and then click **Send Acknowledgement**.</span></span> <span data-ttu-id="195ac-266">在彈出的對話方塊中，請注意所收到的發票和所傳送的通知中，有相同的交換 ID。</span><span class="sxs-lookup"><span data-stu-id="195ac-266">In the dialog box that pops up, notice that the interchange ID is same in the received invoice and the acknowledgement being sent.</span></span> <span data-ttu-id="195ac-267">在 [傳送通知]  對話方塊中按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="195ac-267">Click OK in the **Send Acknowledgement** dialog box.</span></span>
   
   ![][15]  
7. <span data-ttu-id="195ac-268">幾秒後，Contoso 就會成功收到通知。</span><span class="sxs-lookup"><span data-stu-id="195ac-268">In a few seconds, the acknowledgement is successfully received at Contoso.</span></span>
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a><span data-ttu-id="195ac-269">步驟 5 (選用)：批次傳送 EDIFACT 發票</span><span class="sxs-lookup"><span data-stu-id="195ac-269">Step 5 (optional): Send EDIFACT invoice in batches</span></span>
<span data-ttu-id="195ac-270">BizTalk 服務 EDI 橋接器也支援批次處理傳出訊息。</span><span class="sxs-lookup"><span data-stu-id="195ac-270">BizTalk Services EDI bridges also supports batching of outgoing messages.</span></span> <span data-ttu-id="195ac-271">對於想要接收一批訊息 (符合特定條件) 而非個別訊息的接收夥伴，這項功能很實用。</span><span class="sxs-lookup"><span data-stu-id="195ac-271">This feature is useful for receiving partners that prefer to receive a batch of messages (meeting certain criterion) instead of individual messages.</span></span>

<span data-ttu-id="195ac-272">在處理批次時最重要的一點是批次的實際釋放，也稱為釋放準則。</span><span class="sxs-lookup"><span data-stu-id="195ac-272">The most important aspect when working with batches is the actual release of the batch, also called the release criteria.</span></span> <span data-ttu-id="195ac-273">釋放準則可以是依據接收夥伴想要接收訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="195ac-273">The release criteria can be based on how the receiving partner wants to receive messages.</span></span> <span data-ttu-id="195ac-274">如果啟用批次處理，則要等到符合釋放準則後，EDI 橋接器才會傳送傳出訊息給接收夥伴。</span><span class="sxs-lookup"><span data-stu-id="195ac-274">If batching is enabled, the EDI bridge does not send the outgoing message to the receiving partner until the release criteria is fulfilled.</span></span> <span data-ttu-id="195ac-275">例如，依據訊息大小的批次準則只會在批次處理 'n' 則訊息時才分派批次。</span><span class="sxs-lookup"><span data-stu-id="195ac-275">For example, a batching criteria based on message size dispatches a batch only when ‘n’ messages are batched.</span></span> <span data-ttu-id="195ac-276">批次準則也可以是依據時間，以便在每天固定時間傳送批次。</span><span class="sxs-lookup"><span data-stu-id="195ac-276">A batch criteria can also be time-based, such that a batch is sent at a fixed time every day.</span></span> <span data-ttu-id="195ac-277">在此方案中，我們嘗試以訊息大小為基礎的準則。</span><span class="sxs-lookup"><span data-stu-id="195ac-277">In this solution, we try the message-size based criteria.</span></span>

1. <span data-ttu-id="195ac-278">在 BizTalk 服務入口網站中，按一下您稍早建立的協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-278">In the BizTalk Services Portal, click the agreement you created earlier.</span></span> <span data-ttu-id="195ac-279">按一下 [傳送設定] > [批次處理] > [新增批次]。</span><span class="sxs-lookup"><span data-stu-id="195ac-279">Click Send Settings > Batching > Add Batch.</span></span>
2. <span data-ttu-id="195ac-280">對批次名稱輸入 **InvoiceBatch**、提供描述，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="195ac-280">For batch name, enter **InvoiceBatch**, provide a description, and then click **Next**.</span></span>
3. <span data-ttu-id="195ac-281">指定定義必須批次處理哪些訊息的批次準則。</span><span class="sxs-lookup"><span data-stu-id="195ac-281">Specify a batch criteria, that defines which messages must be batched.</span></span> <span data-ttu-id="195ac-282">在此方案中，我們會批次處理所有訊息。</span><span class="sxs-lookup"><span data-stu-id="195ac-282">In this solution, we batch all messages.</span></span> <span data-ttu-id="195ac-283">因此，請選取 [使用進階定義] 選項，然後輸入 **1 = 1**。</span><span class="sxs-lookup"><span data-stu-id="195ac-283">So, select the Use advanced definitions option, and enter **1 = 1**.</span></span> <span data-ttu-id="195ac-284">這個條件永遠會成立，因此會批次處理所有訊息。</span><span class="sxs-lookup"><span data-stu-id="195ac-284">This is a condition which will always be true, and hence all messages will be batched.</span></span> <span data-ttu-id="195ac-285">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-285">Click **Next**.</span></span>
   
   ![][17]  
4. <span data-ttu-id="195ac-286">指定批次釋放準則。</span><span class="sxs-lookup"><span data-stu-id="195ac-286">Specify a batch release criteria.</span></span> <span data-ttu-id="195ac-287">從下拉式方塊中，選取 [MessageCountBased]，然後在 [計數] 中指定 **3**。</span><span class="sxs-lookup"><span data-stu-id="195ac-287">From the drop-box, select **MessageCountBased**, and for **Count**, specify **3**.</span></span> <span data-ttu-id="195ac-288">這表示每批次會傳送三個訊息至 Northwind。</span><span class="sxs-lookup"><span data-stu-id="195ac-288">This means that a batch of three messages will be sent to Northwind.</span></span> <span data-ttu-id="195ac-289">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-289">Click **Next**.</span></span>
   
   ![][18]  
5. <span data-ttu-id="195ac-290">檢閱摘要，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="195ac-290">Review the summary and then click **Save**.</span></span> <span data-ttu-id="195ac-291">按一下 [部署]  來重新部署協議。</span><span class="sxs-lookup"><span data-stu-id="195ac-291">Click **Deploy** to redeploy the agreement.</span></span>
6. <span data-ttu-id="195ac-292">返回 **Tutorial Client**，按一下 [傳送內部發票]，並遵循提示以傳送發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-292">Go back to the **Tutorial Client**, click **Send In-house Invoice**, and follow the prompts to send the invoice.</span></span> <span data-ttu-id="195ac-293">您會發現 Northwind 未收到任何發票，因為批次大小不符。</span><span class="sxs-lookup"><span data-stu-id="195ac-293">You will notice that no invoice is received at Northwind because the batch size is not met.</span></span> <span data-ttu-id="195ac-294">再重複此步驟兩次，以便將三則發票訊息傳送至 Northwind。</span><span class="sxs-lookup"><span data-stu-id="195ac-294">Repeat this step two more times, so that you have three invoice messages sent to Northwind.</span></span> <span data-ttu-id="195ac-295">這就符合 3 則訊息的批次釋放準則，您現在應該會在 Northwind 看到發票。</span><span class="sxs-lookup"><span data-stu-id="195ac-295">This satisfies the batch release criteria of 3 messages and you should now see an invoice at Northwind.</span></span>

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

