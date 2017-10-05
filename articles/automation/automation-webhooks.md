---
title: "使用 Webhook 啟動 Azure 自動化 Runbook | Microsoft Docs"
description: "可讓用戶端透過 HTTP 呼叫在 Azure 自動化中啟動 Runbook 的 Webhook。  本文說明如何建立 Webhook，以及如何進行呼叫以啟動 Runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="784b5-104">使用 Webhook 啟動 Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="784b5-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="784b5-105">*Webhook* 可讓您在 Azure 自動化中透過單一 HTTP 要求啟動特定的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="784b5-106">這可讓外部服務，例如 Visual Studio Team Services、GitHub、Microsoft Operations Management Suite Log Analytics 或自訂應用程式，不需使用 Azure 自動化 API 實作完整的解決方案，即可啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="784b5-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="784b5-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="784b5-108">您可以透過 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="784b5-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="784b5-109">Webhook 的詳細資料</span><span class="sxs-lookup"><span data-stu-id="784b5-109">Details of a webhook</span></span>
<span data-ttu-id="784b5-110">下表描述您必須為 Webhook 設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="784b5-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="784b5-111">屬性</span><span class="sxs-lookup"><span data-stu-id="784b5-111">Property</span></span> | <span data-ttu-id="784b5-112">說明</span><span class="sxs-lookup"><span data-stu-id="784b5-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="784b5-113">名稱</span><span class="sxs-lookup"><span data-stu-id="784b5-113">Name</span></span> |<span data-ttu-id="784b5-114">您可以為 Webhook 提供任何想要的名稱，因為這並不會向用戶端公開。</span><span class="sxs-lookup"><span data-stu-id="784b5-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="784b5-115">該名稱僅供您用來識別 Azure 自動化中的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="784b5-116">最佳做法是您給予 Webhook 的名稱應該與會使用其的用戶端相關。</span><span class="sxs-lookup"><span data-stu-id="784b5-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="784b5-117">URL</span><span class="sxs-lookup"><span data-stu-id="784b5-117">URL</span></span> |<span data-ttu-id="784b5-118">Webhook 的 URL 是一種唯一性的位址，即用戶端用來呼叫 HTTP POST 以啟動連結至 Webhook的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="784b5-119">當您建立 Webhook 時其會自動產生。</span><span class="sxs-lookup"><span data-stu-id="784b5-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="784b5-120">您無法指定自訂 URL。</span><span class="sxs-lookup"><span data-stu-id="784b5-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="784b5-121">URL 包含可讓協力廠商系統不需進一步驗證即可叫用 Runbook 的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="784b5-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="784b5-122">基於這個原因，應該將其視為一種密碼。</span><span class="sxs-lookup"><span data-stu-id="784b5-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="784b5-123">基於安全性原因，您僅能於 Webhook 建立時在 Azure 入口網站中檢視 URL。</span><span class="sxs-lookup"><span data-stu-id="784b5-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="784b5-124">您應該在安全的位置記下 URL 以供日後使用。</span><span class="sxs-lookup"><span data-stu-id="784b5-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="784b5-125">到期日期</span><span class="sxs-lookup"><span data-stu-id="784b5-125">Expiration date</span></span> |<span data-ttu-id="784b5-126">例如憑證，每個 Webhook 都會有一個到期日期，到期後便無法再使用。</span><span class="sxs-lookup"><span data-stu-id="784b5-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="784b5-127">此到期日期可在 Webhook 建立後加以修改。</span><span class="sxs-lookup"><span data-stu-id="784b5-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="784b5-128">已啟用</span><span class="sxs-lookup"><span data-stu-id="784b5-128">Enabled</span></span> |<span data-ttu-id="784b5-129">建立 Runbook 時 Webhook 會預設為啟用。</span><span class="sxs-lookup"><span data-stu-id="784b5-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="784b5-130">如果您將其設定為 [停用]，則任何用戶端皆無法使用。</span><span class="sxs-lookup"><span data-stu-id="784b5-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="784b5-131">當您建立 Webhook 時或在建立後的任何時候，您可以設定 [ **啟用** ] 屬性。</span><span class="sxs-lookup"><span data-stu-id="784b5-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="784b5-132">參數</span><span class="sxs-lookup"><span data-stu-id="784b5-132">Parameters</span></span>
<span data-ttu-id="784b5-133">Webhook 可以定義由該 Webhook 啟動 Runbook 時所使用的 Runbook 參數值。</span><span class="sxs-lookup"><span data-stu-id="784b5-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="784b5-134">Webhook 必須包含任何 Runbook 的強制參數值，且可能包含選擇性的參數值。</span><span class="sxs-lookup"><span data-stu-id="784b5-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="784b5-135">甚至在建立 Webhoook 之後，可以對為 Webhook 設定的參數值進行修改。</span><span class="sxs-lookup"><span data-stu-id="784b5-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="784b5-136">多個 Webhook 連結至單一 Runbook 時，可以個別使用不同的參數值。</span><span class="sxs-lookup"><span data-stu-id="784b5-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="784b5-137">當用戶端使用 Webhook 啟動 Runbook 時，其無法覆寫 Webhook 中定義的參數值。</span><span class="sxs-lookup"><span data-stu-id="784b5-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="784b5-138">若要從用戶端接收資料，Runbook 可以接受單一參數，稱之為 **$WebhookData** 的 [物件] 類型，其中包含用戶端在 POST 要求中所包含的資料。</span><span class="sxs-lookup"><span data-stu-id="784b5-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Webhookdata 屬性](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="784b5-140">**$WebhookData** 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="784b5-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="784b5-141">屬性</span><span class="sxs-lookup"><span data-stu-id="784b5-141">Property</span></span> | <span data-ttu-id="784b5-142">說明</span><span class="sxs-lookup"><span data-stu-id="784b5-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="784b5-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="784b5-143">WebhookName</span></span> |<span data-ttu-id="784b5-144">Webhook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="784b5-144">The name of the webhook.</span></span> |
| <span data-ttu-id="784b5-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="784b5-145">RequestHeader</span></span> |<span data-ttu-id="784b5-146">雜湊表包含傳入 POST 要求的標頭。</span><span class="sxs-lookup"><span data-stu-id="784b5-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="784b5-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="784b5-147">RequestBody</span></span> |<span data-ttu-id="784b5-148">傳入 POST 要求的本文。</span><span class="sxs-lookup"><span data-stu-id="784b5-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="784b5-149">這會保留任何的格式，如字串、JSON、XML，或表單已編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="784b5-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="784b5-150">Runbook 必須撰寫用來搭配預期的資料格式。</span><span class="sxs-lookup"><span data-stu-id="784b5-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="784b5-151">支援 **$WebhookData** 參數不需要 Webhook 的組態，且 Runbook 不需要接受其。</span><span class="sxs-lookup"><span data-stu-id="784b5-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="784b5-152">若 Runbook 並未定義參數，則會忽略從用戶端所傳送要求的任何詳細資料。</span><span class="sxs-lookup"><span data-stu-id="784b5-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="784b5-153">若您在建立 Webhook 時指定 $WebhookData 的值，即使用戶端在要求本文中並未包含任何資料，該值將會在 Webhook 使用用戶端 POST 要求的資料來啟動 Runbook 時遭到覆寫。</span><span class="sxs-lookup"><span data-stu-id="784b5-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="784b5-154">若您使用 Webhook 以外的方式啟動具有 $WebhookData 的 Runbook，您可以提供可讓 Runbook 識別的 $WebhookData 值。</span><span class="sxs-lookup"><span data-stu-id="784b5-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="784b5-155">這個值應該是 [屬性](#details-of-a-webhook) 相同皆為 $Webhookdata 的物件，Runbook 如此即可正確地與其一起運作，就像是其使用 webhook 所傳遞的實際 WebhookData 一般。</span><span class="sxs-lookup"><span data-stu-id="784b5-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="784b5-156">例如，如果要從 Azure 入口網站啟動下列 Runbook，並想要傳遞一些 WebhookData 範例進行測試，因為 WebhookData 為物件，所以應以 UI 中的 JSON 加以傳遞。</span><span class="sxs-lookup"><span data-stu-id="784b5-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![來自 UI 的 WebhookData 參數](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="784b5-158">針對上述 Runbook，如果您對 WebhookData 參數具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="784b5-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="784b5-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="784b5-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="784b5-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="784b5-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="784b5-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="784b5-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="784b5-162">則應對 WebhookData 參數傳遞下列 UI 中的 JSON 值：</span><span class="sxs-lookup"><span data-stu-id="784b5-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="784b5-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="784b5-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![啟動來自 UI 的 WebhookData 參數](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="784b5-165">所有輸入參數的值會使用 Runbook 工作進行記錄。</span><span class="sxs-lookup"><span data-stu-id="784b5-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="784b5-166">這表示，任何由用戶端在 Webhook 要求中提供的輸入將會進行記錄，並可讓任何有自動化工作存取權的人使用。</span><span class="sxs-lookup"><span data-stu-id="784b5-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="784b5-167">基於這個原因，您在 Webhook 呼叫中包含機密資訊時應該特別謹慎。</span><span class="sxs-lookup"><span data-stu-id="784b5-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="784b5-168">安全性</span><span class="sxs-lookup"><span data-stu-id="784b5-168">Security</span></span>
<span data-ttu-id="784b5-169">Webhook 的安全性仰賴其 URL 的隱私權，其中包含可允許其接受叫用的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="784b5-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="784b5-170">只要針對正確的 URL 進行要求，Azure 自動化就不會對要求執行任何驗證。</span><span class="sxs-lookup"><span data-stu-id="784b5-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="784b5-171">基於這個原因，若不使用驗證要求的替代方式時，Webhooks 不應用於執行高度機密功能的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="784b5-172">您可以透過檢查 $WebhookData 參數的 **WebhookName** 屬性，在 Runbook 中包含邏輯來判斷其是否由 Webhook 所呼叫。</span><span class="sxs-lookup"><span data-stu-id="784b5-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="784b5-173">Runbook 可以透過尋找 **RequestHeader** 或 **RequestBody** 屬性中的特定資訊來執行進一步的驗證。</span><span class="sxs-lookup"><span data-stu-id="784b5-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="784b5-174">另一個策略是當 Runbook 收到 Webhook 要求時，使其執行某些外部條件的驗證。</span><span class="sxs-lookup"><span data-stu-id="784b5-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="784b5-175">例如，當 GitHub 儲存機制出現新的認可時，考慮使用由 GitHub 呼叫的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="784b5-176">Runbook 可能會連接到 GitHub 以驗證在繼續之前實際上已出現新的認可。</span><span class="sxs-lookup"><span data-stu-id="784b5-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="784b5-177">建立 Webhook</span><span class="sxs-lookup"><span data-stu-id="784b5-177">Creating a webhook</span></span>
<span data-ttu-id="784b5-178">使用下列程序在 Azure 入口網站中建立連結至 Runbook 的全新 Webhook。</span><span class="sxs-lookup"><span data-stu-id="784b5-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="784b5-179">從 Azure 入口網站的 **Runbook 刀鋒視窗** 中，按一下 Webhook 將開始檢視詳細資料刀鋒視窗的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="784b5-180">按一下刀鋒視窗頂端的 [Webhook] 以開啟 [新增 Webhook] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="784b5-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="784b5-181">
   ![Webhook 按鈕](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="784b5-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="784b5-182">按一下 [建立新的 Webhook] 以開啟 [建立 Webhook 刀鋒視窗]。</span><span class="sxs-lookup"><span data-stu-id="784b5-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="784b5-183">指定 Webhook 的 [名稱]、[到期日期] 以及是否應該啟用。</span><span class="sxs-lookup"><span data-stu-id="784b5-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="784b5-184">請參閱 [Webhook 的詳細資料](#details-of-a-webhook) 以取得這些屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="784b5-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="784b5-185">按一下複製圖示，然後按 Ctrl + C 以複製 Webhook 的 URL。</span><span class="sxs-lookup"><span data-stu-id="784b5-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="784b5-186">然後將其記錄在安全的地方。</span><span class="sxs-lookup"><span data-stu-id="784b5-186">Then record it in a safe place.</span></span>  <span data-ttu-id="784b5-187">**一旦您建立 Webhook，即無法再次擷取 URL。**</span><span class="sxs-lookup"><span data-stu-id="784b5-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="784b5-188">
   ![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="784b5-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="784b5-189">按一下 [參數]  來提供 Runbook 的參數值。</span><span class="sxs-lookup"><span data-stu-id="784b5-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="784b5-190">如果 Runbook 有強制參數，除非提供該值，否則您將無法建立 Webhook。</span><span class="sxs-lookup"><span data-stu-id="784b5-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="784b5-191">按一下 [ **建立** ] 來建立 Webhook。</span><span class="sxs-lookup"><span data-stu-id="784b5-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="784b5-192">使用 Webhook</span><span class="sxs-lookup"><span data-stu-id="784b5-192">Using a webhook</span></span>
<span data-ttu-id="784b5-193">建立 Webhook 之後若要使用它，您的用戶端應用程式必須使用 Webhook 的 URL 來發出 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="784b5-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="784b5-194">Webhook 的語法將遵循以下列格式。</span><span class="sxs-lookup"><span data-stu-id="784b5-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="784b5-195">用戶端將會從 POST 要求中接收下列其中一個傳回代碼。</span><span class="sxs-lookup"><span data-stu-id="784b5-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="784b5-196">代碼</span><span class="sxs-lookup"><span data-stu-id="784b5-196">Code</span></span> | <span data-ttu-id="784b5-197">文字</span><span class="sxs-lookup"><span data-stu-id="784b5-197">Text</span></span> | <span data-ttu-id="784b5-198">說明</span><span class="sxs-lookup"><span data-stu-id="784b5-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="784b5-199">202</span><span class="sxs-lookup"><span data-stu-id="784b5-199">202</span></span> |<span data-ttu-id="784b5-200">已接受</span><span class="sxs-lookup"><span data-stu-id="784b5-200">Accepted</span></span> |<span data-ttu-id="784b5-201">已接受要求，且 Runbook 已經成功排入佇列。</span><span class="sxs-lookup"><span data-stu-id="784b5-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="784b5-202">400</span><span class="sxs-lookup"><span data-stu-id="784b5-202">400</span></span> |<span data-ttu-id="784b5-203">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="784b5-203">Bad Request</span></span> |<span data-ttu-id="784b5-204">基於下列原因之一不接受此要求。</span><span class="sxs-lookup"><span data-stu-id="784b5-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="784b5-205">Webhook 已過期。</span><span class="sxs-lookup"><span data-stu-id="784b5-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="784b5-206">Webhook 已停用。</span><span class="sxs-lookup"><span data-stu-id="784b5-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="784b5-207">URL 中的權杖無效。</span><span class="sxs-lookup"><span data-stu-id="784b5-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="784b5-208">404</span><span class="sxs-lookup"><span data-stu-id="784b5-208">404</span></span> |<span data-ttu-id="784b5-209">找不到</span><span class="sxs-lookup"><span data-stu-id="784b5-209">Not Found</span></span> |<span data-ttu-id="784b5-210">基於下列原因之一不接受此要求。</span><span class="sxs-lookup"><span data-stu-id="784b5-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="784b5-211">找不到該 Webhook。</span><span class="sxs-lookup"><span data-stu-id="784b5-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="784b5-212">找不到該 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="784b5-213">找不到帳戶。</span><span class="sxs-lookup"><span data-stu-id="784b5-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="784b5-214">500</span><span class="sxs-lookup"><span data-stu-id="784b5-214">500</span></span> |<span data-ttu-id="784b5-215">內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="784b5-215">Internal Server Error</span></span> |<span data-ttu-id="784b5-216">URL 有效，但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="784b5-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="784b5-217">請重新提交要求。</span><span class="sxs-lookup"><span data-stu-id="784b5-217">Please resubmit the request.</span></span> |

<span data-ttu-id="784b5-218">假設要求成功，Webhook 會回應包含 JSON 格式的工作識別碼，如下所示。</span><span class="sxs-lookup"><span data-stu-id="784b5-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="784b5-219">它會包含單一的工作識別碼，但是 JSON 格式允許未來可能的增強功能。</span><span class="sxs-lookup"><span data-stu-id="784b5-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="784b5-220">用戶端無法從 Webhook 判斷 Runbook 的工作何時完成或完成狀態。</span><span class="sxs-lookup"><span data-stu-id="784b5-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="784b5-221">這項資訊可使用工作識別碼搭配其他方法 (例如 [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) 或 [Azure 自動化 API](https://msdn.microsoft.com/library/azure/mt163826.aspx)) 來判斷。</span><span class="sxs-lookup"><span data-stu-id="784b5-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="784b5-222">範例</span><span class="sxs-lookup"><span data-stu-id="784b5-222">Example</span></span>
<span data-ttu-id="784b5-223">下列範例使用 Windows PowerShell 搭配 Webhook 來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="784b5-224">請注意，任何可以進行 HTTP 要求的語言都可以使用 Webhook；Windows PowerShell 在這裡僅作為範例使用。</span><span class="sxs-lookup"><span data-stu-id="784b5-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="784b5-225">Runbook 預期在要求的主體中有 JSON 格式的虛擬機器清單。</span><span class="sxs-lookup"><span data-stu-id="784b5-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="784b5-226">我們也在要求的標頭中，列入了有關於啟動 Runbook 的人員、啟動的日期和時間資訊。</span><span class="sxs-lookup"><span data-stu-id="784b5-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="784b5-227">下圖顯示來自要求的標頭資訊 (使用 [Fiddler](http://www.telerik.com/fiddler) 追蹤)。</span><span class="sxs-lookup"><span data-stu-id="784b5-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="784b5-228">這包括了 HTTP 要求的標準標頭，除此之外，還有我們加入的自訂「日期」和「時間」標頭。</span><span class="sxs-lookup"><span data-stu-id="784b5-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="784b5-229">這些值都可在 **WebhookData** 的**RequestHeaders** 屬性中提供給 Runbook 使用。</span><span class="sxs-lookup"><span data-stu-id="784b5-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Webhook 按鈕](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="784b5-231">下圖顯示要求的主體 (使用 [Fiddler](http://www.telerik.com/fiddler) 追蹤) 可在 **WebhookData** 的 **RequestBody** 屬性中提供給 Runbook 使用。</span><span class="sxs-lookup"><span data-stu-id="784b5-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="784b5-232">格式化為 JSON 是因為其格式是要求的主體中所包含之格式。</span><span class="sxs-lookup"><span data-stu-id="784b5-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Webhook 按鈕](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="784b5-234">下圖顯示由 Windows PowerShell 送出的要求以及產生的回應。</span><span class="sxs-lookup"><span data-stu-id="784b5-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="784b5-235">工作識別碼從回應中擷取，再轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="784b5-235">The job id is extracted from the response and converted to a string.</span></span>

![Webhook 按鈕](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="784b5-237">下列範例 Runbook 接受之前的範例要求，並啟動要求主體中指定的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="784b5-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="784b5-238">啟動 Runbook 以回應 Azure 警示</span><span class="sxs-lookup"><span data-stu-id="784b5-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="784b5-239">啟用 Webhook 的 Runbook 可用以回應 [Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="784b5-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="784b5-240">Azure 中的資源可以透過 Azure 警示的協助，藉由收集如效能、可用性和使用方式的統計資料進行監視。</span><span class="sxs-lookup"><span data-stu-id="784b5-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="784b5-241">您可以收到根據監視您 Azure 資源的計量或事件的警示，目前自動化帳戶僅支援度量。</span><span class="sxs-lookup"><span data-stu-id="784b5-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="784b5-242">當指定的計量值超過指派的閾值，或者如果觸發了設定的事件，就會傳送通知給服務管理員或共同管理員以解決該警示，如需計量與事件的詳細資訊，請參閱 [Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="784b5-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="784b5-243">除了使用 Azure 的警示做為通知系統，也可以使用 Runbook 回應警示。</span><span class="sxs-lookup"><span data-stu-id="784b5-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="784b5-244">Azure 自動化可讓您使用 Azure 警示執行啟用 Webhook 的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="784b5-245">當計量超過設定的閾值時，警示規則就會變成作用中，並且觸發自動化 Webhook，連帶執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="784b5-247">警示內容</span><span class="sxs-lookup"><span data-stu-id="784b5-247">Alert context</span></span>
<span data-ttu-id="784b5-248">考量如虛擬機器的 Azure 資源，這台電腦的 CPU 使用率是其中一個關鍵效能計量。</span><span class="sxs-lookup"><span data-stu-id="784b5-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="784b5-249">如果 CPU 使用率是 100% 或者在一段長時間超過某個量，您可能會想要重新啟動虛擬機器以修正問題。</span><span class="sxs-lookup"><span data-stu-id="784b5-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="784b5-250">這可以藉由設定虛擬機器的警示規則來解決，而此規則可以使用 CPU 百分比做為計量。</span><span class="sxs-lookup"><span data-stu-id="784b5-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="784b5-251">這裡的 CPU 百分比只是一個範例，但是還有許多您可以對 Azure 資源設定的其他計量，重新啟動虛擬機器是修正此問題所採取的一個動作，您可以設定 Runbook 採取其他動作。</span><span class="sxs-lookup"><span data-stu-id="784b5-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="784b5-252">當此警示規則變成作用中並且觸發啟用 Webhook 的 Runbook 時，會傳送警示內容到 Runbook。</span><span class="sxs-lookup"><span data-stu-id="784b5-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="784b5-253">[警示內容](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)包含的詳細資料包括 **SubscriptionID**、**ResourceGroupName**、**ResourceName**、**ResourceType**、**ResourceId** 和 **Timestamp**，這些都是 Runbook 識別要在其上採取動作的資源所需的項目。</span><span class="sxs-lookup"><span data-stu-id="784b5-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="784b5-254">警示內容內嵌在傳送至 Runbook 的 **WebhookData** 物件的內文部分，可以使用 **Webhook.RequestBody** 屬性存取</span><span class="sxs-lookup"><span data-stu-id="784b5-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="784b5-255">範例</span><span class="sxs-lookup"><span data-stu-id="784b5-255">Example</span></span>
<span data-ttu-id="784b5-256">在訂用帳戶中建立 Azure 虛擬機器，並關聯[警示以監視 CPU 百分比計量](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="784b5-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="784b5-257">建立警示時，請確定以建立 Webhook 時所產生的 Webhook URL 填入 Webhook 欄位。</span><span class="sxs-lookup"><span data-stu-id="784b5-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="784b5-258">下列範例 Runbook 會在警示規則變成作用中時觸發，而且會收集 Runbook 識別在上面採取動作的資源所需的警示內容參數。</span><span class="sxs-lookup"><span data-stu-id="784b5-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="784b5-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="784b5-259">Next steps</span></span>
* <span data-ttu-id="784b5-260">如需以不同方式啟動 Runbook 的詳細資訊，請參閱[啟動 Runbook](automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="784b5-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="784b5-261">如需檢視 Runbook 作業狀態的相關資訊，請參閱 [Azure 自動化中的 Runbook 執行](automation-runbook-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="784b5-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="784b5-262">若要了解如何使用 Azure 自動化來對 Azure 警示採取動作，請參閱[使用自動化 Runbook 修復 Azure VM 警示](automation-azure-vm-alert-integration.md)。</span><span class="sxs-lookup"><span data-stu-id="784b5-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
