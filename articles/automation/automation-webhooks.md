---
title: "Azure 自動化 runbook 的 webhook aaaStarting |Microsoft 文件"
description: "Webhook，可讓用戶端 toostart runbook 在 Azure 自動化中從 HTTP 呼叫。  本文說明如何 toocreate webhook 以及 toocall 一個 toostart runbook。"
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="97627-104">使用 Webhook 啟動 Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="97627-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="97627-105">A *webhook*可讓您 toostart 特定 runbook 在 Azure 自動化中透過單一 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="97627-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="97627-106">這可讓外部服務，例如 Visual Studio Team Services、 GitHub、 Microsoft Operations Management Suite 記錄分析或自訂應用程式 toostart runbook 而不需要實作使用 hello Azure 自動化 API 的完整方案。</span><span class="sxs-lookup"><span data-stu-id="97627-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="97627-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="97627-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="97627-108">您可以比較啟動 runbook 的 webhook tooother 方法[Azure 自動化中啟動 runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="97627-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="97627-109">Webhook 的詳細資料</span><span class="sxs-lookup"><span data-stu-id="97627-109">Details of a webhook</span></span>
<span data-ttu-id="97627-110">hello 下表描述您必須設定的 webhook hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="97627-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="97627-111">屬性</span><span class="sxs-lookup"><span data-stu-id="97627-111">Property</span></span> | <span data-ttu-id="97627-112">說明</span><span class="sxs-lookup"><span data-stu-id="97627-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="97627-113">名稱</span><span class="sxs-lookup"><span data-stu-id="97627-113">Name</span></span> |<span data-ttu-id="97627-114">您可以提供任何的名稱的 webhook 因為這是不公開 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="97627-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="97627-115">僅用於您 tooidentify hello Azure 自動化中 runbook。</span><span class="sxs-lookup"><span data-stu-id="97627-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="97627-116">最佳做法，您應該給予 hello webhook 名稱相關的 toohello 用戶端將使用它。</span><span class="sxs-lookup"><span data-stu-id="97627-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="97627-117">URL</span><span class="sxs-lookup"><span data-stu-id="97627-117">URL</span></span> |<span data-ttu-id="97627-118">hello hello webhook URL 是 hello 唯一的位址，用戶端呼叫使用的 HTTP POST toostart hello runbook 連結 toohello webhook。</span><span class="sxs-lookup"><span data-stu-id="97627-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="97627-119">它會自動產生的當您建立 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="97627-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="97627-120">您無法指定自訂 URL。</span><span class="sxs-lookup"><span data-stu-id="97627-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="97627-121">hello URL 包含可讓 hello runbook toobe 叫用由沒有進一步的驗證與第三方系統的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="97627-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="97627-122">基於這個原因，應該將其視為一種密碼。</span><span class="sxs-lookup"><span data-stu-id="97627-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="97627-123">基於安全性理由，您可以只檢視 hello 建立 hello hello 時間 hello webhook 在 Azure 入口網站中的 URL。</span><span class="sxs-lookup"><span data-stu-id="97627-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="97627-124">您應該注意 hello URL 在安全的位置，供日後使用。</span><span class="sxs-lookup"><span data-stu-id="97627-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="97627-125">到期日期</span><span class="sxs-lookup"><span data-stu-id="97627-125">Expiration date</span></span> |<span data-ttu-id="97627-126">例如憑證，每個 Webhook 都會有一個到期日期，到期後便無法再使用。</span><span class="sxs-lookup"><span data-stu-id="97627-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="97627-127">Hello webhook 建立之後，就可以修改此到期日。</span><span class="sxs-lookup"><span data-stu-id="97627-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="97627-128">已啟用</span><span class="sxs-lookup"><span data-stu-id="97627-128">Enabled</span></span> |<span data-ttu-id="97627-129">建立 Runbook 時 Webhook 會預設為啟用。</span><span class="sxs-lookup"><span data-stu-id="97627-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="97627-130">如果設定 tooDisabled，則沒有用戶端可以 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="97627-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="97627-131">您可以設定 hello**啟用**會建立屬性，當您建立 hello webhook 或一次安裝它。</span><span class="sxs-lookup"><span data-stu-id="97627-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="97627-132">參數</span><span class="sxs-lookup"><span data-stu-id="97627-132">Parameters</span></span>
<span data-ttu-id="97627-133">Webhook 可以定義該 webhook 啟動 hello runbook 時所使用的 runbook 參數的值。</span><span class="sxs-lookup"><span data-stu-id="97627-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="97627-134">hello webhook 必須包含 hello runbook 的必要參數的值，而且可能包含選擇性參數的值。</span><span class="sxs-lookup"><span data-stu-id="97627-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="97627-135">參數值設定 tooa webhook 可以修改甚至建立 hello webhoook 之後。</span><span class="sxs-lookup"><span data-stu-id="97627-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="97627-136">多個連結的 webhook tooa 單一 runbook 每個可以使用不同的參數值。</span><span class="sxs-lookup"><span data-stu-id="97627-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="97627-137">當用戶端啟動使用 webhook runbook 時，它無法覆寫 hello hello webhook 中定義的參數值。</span><span class="sxs-lookup"><span data-stu-id="97627-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="97627-138">tooreceive 資料來自 hello 用戶端 hello runbook 可以接受單一參數來呼叫**$WebhookData** hello 用戶端包含 hello POST 要求中的類型 [object]，將包含資料。</span><span class="sxs-lookup"><span data-stu-id="97627-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Webhookdata 屬性](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="97627-140">hello **$WebhookData**物件都有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="97627-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="97627-141">屬性</span><span class="sxs-lookup"><span data-stu-id="97627-141">Property</span></span> | <span data-ttu-id="97627-142">說明</span><span class="sxs-lookup"><span data-stu-id="97627-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="97627-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="97627-143">WebhookName</span></span> |<span data-ttu-id="97627-144">hello hello webhook 名稱。</span><span class="sxs-lookup"><span data-stu-id="97627-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="97627-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="97627-145">RequestHeader</span></span> |<span data-ttu-id="97627-146">包含 hello hello 傳入的 POST 要求的標頭的雜湊資料表。</span><span class="sxs-lookup"><span data-stu-id="97627-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="97627-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="97627-147">RequestBody</span></span> |<span data-ttu-id="97627-148">hello hello 傳入的 POST 要求主體。</span><span class="sxs-lookup"><span data-stu-id="97627-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="97627-149">這會保留任何的格式，如字串、JSON、XML，或表單已編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="97627-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="97627-150">hello runbook 必須寫入 toowork 與 hello 預期的資料格式。</span><span class="sxs-lookup"><span data-stu-id="97627-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="97627-151">沒有任何設定的 hello webhook 必要的 toosupport hello **$WebhookData**參數，而且不需要的 tooaccept hello runbook。 它。</span><span class="sxs-lookup"><span data-stu-id="97627-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="97627-152">如果 hello runbook 未定義 hello 參數，則會忽略任何要求詳細資料的 hello hello 用戶端送出。</span><span class="sxs-lookup"><span data-stu-id="97627-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="97627-153">如果您指定的值 $WebhookData 當您建立 hello webhook 值將會覆寫時 hello webhook 啟動 hello runbook hello 資料 hello 用戶端 POST 要求，即使 hello 用戶端 hello 要求主體中未包含任何資料。</span><span class="sxs-lookup"><span data-stu-id="97627-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="97627-154">如果您啟動 runbook 具有 $WebhookData 使用 webhook 以外的方法，您可以為 hello runbook 可辨識的 $Webhookdata 提供值。</span><span class="sxs-lookup"><span data-stu-id="97627-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="97627-155">這個值應該是以 hello 物件相同[屬性](#details-of-a-webhook)$Webhookdata 以便讓該 hello runbook 可以正確搭配就如同它已使用 webhook 所傳遞的實際 WebhookData 為。</span><span class="sxs-lookup"><span data-stu-id="97627-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="97627-156">例如，如果您正在啟動 hello hello Azure 入口網站中的下列 runbook，而且想要進行測試，因為 WebhookData 是物件的一些範例 WebhookData toopass，它應該中進行傳遞為 JSON hello UI。</span><span class="sxs-lookup"><span data-stu-id="97627-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![來自 UI 的 WebhookData 參數](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="97627-158">Hello 上方的 runbook，如果您擁有 hello hello WebhookData 參數的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="97627-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="97627-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="97627-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="97627-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="97627-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="97627-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="97627-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="97627-162">然後您可以傳遞下列 JSON 值 hello UI hello WebhookData 參數中的 hello:</span><span class="sxs-lookup"><span data-stu-id="97627-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="97627-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="97627-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![啟動來自 UI 的 WebhookData 參數](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="97627-165">hello 的所有輸入參數的值會記錄與 hello runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="97627-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="97627-166">這表示，任何 hello hello webhook 要求中的用戶端所提供的輸入將會記錄並且可 tooanyone 與存取 toohello 自動化工作。</span><span class="sxs-lookup"><span data-stu-id="97627-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="97627-167">基於這個原因，您在 Webhook 呼叫中包含機密資訊時應該特別謹慎。</span><span class="sxs-lookup"><span data-stu-id="97627-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="97627-168">安全性</span><span class="sxs-lookup"><span data-stu-id="97627-168">Security</span></span>
<span data-ttu-id="97627-169">webhook hello 安全性依賴其 URL，其中包含可讓它 toobe 叫用的安全性權杖的 hello 隱私權。</span><span class="sxs-lookup"><span data-stu-id="97627-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="97627-170">Azure 自動化不會執行任何驗證 hello 要求，只要它由 toohello 正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="97627-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="97627-171">基於這個理由，webhook 不應該使用的 runbook，而不使用其他驗證 hello 要求的方式執行高度敏感的功能。</span><span class="sxs-lookup"><span data-stu-id="97627-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="97627-172">您可以將邏輯包含在已呼叫它的 webhook 藉由檢查 hello hello runbook toodetermine **WebhookName** hello $WebhookData 參數的屬性。</span><span class="sxs-lookup"><span data-stu-id="97627-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="97627-173">hello runbook 無法執行進一步來驗證特定中尋找資訊 hello **RequestHeader**或**RequestBody**屬性。</span><span class="sxs-lookup"><span data-stu-id="97627-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="97627-174">另一個策略是 toohave hello runbook 它收到 webhook 要求時，請執行一些外部條件的驗證。</span><span class="sxs-lookup"><span data-stu-id="97627-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="97627-175">例如，請考慮 GitHub 新認可 tooa GitHub 儲存機制時呼叫的 runbook。</span><span class="sxs-lookup"><span data-stu-id="97627-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="97627-176">hello runbook 可能會連線 tooGitHub toovalidate 新認可具有實際上只發生在之前繼續進行。</span><span class="sxs-lookup"><span data-stu-id="97627-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="97627-177">建立 Webhook</span><span class="sxs-lookup"><span data-stu-id="97627-177">Creating a webhook</span></span>
<span data-ttu-id="97627-178">使用下列程序 toocreate hello Azure 入口網站中的新連結的 webhook tooa runbook hello。</span><span class="sxs-lookup"><span data-stu-id="97627-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="97627-179">從 hello **Runbook 刀鋒視窗**hello Azure 入口網站，在按一下 hello webhook 的 hello runbook 將會開始 tooview 其詳細資料 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="97627-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="97627-180">按一下**Webhook**頂端的 hello 刀鋒視窗 tooopen hello hello**新增 Webhook**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="97627-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="97627-181">
   ![Webhook 按鈕](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="97627-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="97627-182">按一下**建立新的 webhook** tooopen hello**建立 webhook 刀鋒視窗**。</span><span class="sxs-lookup"><span data-stu-id="97627-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="97627-183">指定**名稱**，**到期日**hello webhook 和是否應該啟用。</span><span class="sxs-lookup"><span data-stu-id="97627-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="97627-184">請參閱 [Webhook 的詳細資料](#details-of-a-webhook) 以取得這些屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="97627-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="97627-185">按一下 hello 複製圖示，然後按 Ctrl + C toocopy hello URL hello webhook。</span><span class="sxs-lookup"><span data-stu-id="97627-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="97627-186">然後將其記錄在安全的地方。</span><span class="sxs-lookup"><span data-stu-id="97627-186">Then record it in a safe place.</span></span>  <span data-ttu-id="97627-187">**一旦您建立 hello webhook，就無法再次擷取 hello URL。**</span><span class="sxs-lookup"><span data-stu-id="97627-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="97627-188">
   ![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="97627-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="97627-189">按一下**參數**tooprovide hello runbook 參數的值。</span><span class="sxs-lookup"><span data-stu-id="97627-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="97627-190">如果 hello runbook 有強制性參數，然後就可以 toocreate hello webhook 除非提供值。</span><span class="sxs-lookup"><span data-stu-id="97627-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="97627-191">按一下**建立**toocreate hello webhook。</span><span class="sxs-lookup"><span data-stu-id="97627-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="97627-192">使用 Webhook</span><span class="sxs-lookup"><span data-stu-id="97627-192">Using a webhook</span></span>
<span data-ttu-id="97627-193">toouse webhook 建立之後，用戶端應用程式必須發出 HTTP POST 與 hello hello webhook URL。</span><span class="sxs-lookup"><span data-stu-id="97627-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="97627-194">hello webhook hello 語法會以下列格式的 hello。</span><span class="sxs-lookup"><span data-stu-id="97627-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="97627-195">hello 用戶端會收到 hello hello POST 要求中的下列傳回碼的其中一個。</span><span class="sxs-lookup"><span data-stu-id="97627-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="97627-196">代碼</span><span class="sxs-lookup"><span data-stu-id="97627-196">Code</span></span> | <span data-ttu-id="97627-197">文字</span><span class="sxs-lookup"><span data-stu-id="97627-197">Text</span></span> | <span data-ttu-id="97627-198">說明</span><span class="sxs-lookup"><span data-stu-id="97627-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="97627-199">202</span><span class="sxs-lookup"><span data-stu-id="97627-199">202</span></span> |<span data-ttu-id="97627-200">已接受</span><span class="sxs-lookup"><span data-stu-id="97627-200">Accepted</span></span> |<span data-ttu-id="97627-201">已接受 hello 的要求，並已成功排入佇列 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="97627-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="97627-202">400</span><span class="sxs-lookup"><span data-stu-id="97627-202">400</span></span> |<span data-ttu-id="97627-203">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="97627-203">Bad Request</span></span> |<span data-ttu-id="97627-204">其中一個 hello 下列原因而不接受 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="97627-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="97627-205">hello webhook 已到期。</span><span class="sxs-lookup"><span data-stu-id="97627-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="97627-206">hello webhook 已停用。</span><span class="sxs-lookup"><span data-stu-id="97627-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="97627-207">hello URL 中的 hello 語彙基元無效。</span><span class="sxs-lookup"><span data-stu-id="97627-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="97627-208">404</span><span class="sxs-lookup"><span data-stu-id="97627-208">404</span></span> |<span data-ttu-id="97627-209">找不到</span><span class="sxs-lookup"><span data-stu-id="97627-209">Not Found</span></span> |<span data-ttu-id="97627-210">其中一個 hello 下列原因而不接受 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="97627-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="97627-211">找不到 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="97627-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="97627-212">找不到 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="97627-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="97627-213">找不到 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="97627-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="97627-214">500</span><span class="sxs-lookup"><span data-stu-id="97627-214">500</span></span> |<span data-ttu-id="97627-215">內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="97627-215">Internal Server Error</span></span> |<span data-ttu-id="97627-216">hello URL 有效，但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="97627-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="97627-217">請重新送出 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="97627-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="97627-218">假設 hello 要求成功時，hello webhook 回應包含 hello 工作識別碼以 JSON 格式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="97627-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="97627-219">它會包含單一作業識別碼，但 hello JSON 格式允許潛在未來增強功能。</span><span class="sxs-lookup"><span data-stu-id="97627-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="97627-220">hello 用戶端無法判斷 hello runbook 作業完成時，或從 hello webhook 及其完成狀態。</span><span class="sxs-lookup"><span data-stu-id="97627-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="97627-221">它可以判定這項資訊與另一種方法使用 hello 作業識別碼，例如[Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx)或 hello [Azure 自動化 API](https://msdn.microsoft.com/library/azure/mt163826.aspx)。</span><span class="sxs-lookup"><span data-stu-id="97627-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="97627-222">範例</span><span class="sxs-lookup"><span data-stu-id="97627-222">Example</span></span>
<span data-ttu-id="97627-223">hello 下列範例會使用 Windows PowerShell toostart runbook webhook。</span><span class="sxs-lookup"><span data-stu-id="97627-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="97627-224">請注意，任何可以進行 HTTP 要求的語言都可以使用 Webhook；Windows PowerShell 在這裡僅作為範例使用。</span><span class="sxs-lookup"><span data-stu-id="97627-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="97627-225">hello runbook 並收到 hello hello 要求主體中的 JSON 格式的虛擬機器的清單。</span><span class="sxs-lookup"><span data-stu-id="97627-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="97627-226">我們也會包括啟動 hello hello 要求標頭中誰正在啟動 hello runbook 及 hello 日期和時間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="97627-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="97627-227">hello 下列影像顯示 hello 標頭資訊 (使用[Fiddler](http://www.telerik.com/fiddler)追蹤) 從這項要求。</span><span class="sxs-lookup"><span data-stu-id="97627-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="97627-228">這包括標準 HTTP 要求的標頭中加入 toohello 自訂日期和從我們加入的標頭。</span><span class="sxs-lookup"><span data-stu-id="97627-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="97627-229">每個這些值都是可用 toohello runbook 在 hello **RequestHeaders**屬性**WebhookData**。</span><span class="sxs-lookup"><span data-stu-id="97627-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Webhook 按鈕](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="97627-231">hello 下列影像顯示 hello hello 要求主體 (使用[Fiddler](http://www.telerik.com/fiddler)追蹤) 也就是可用 toohello runbook 在 hello **RequestBody**屬性**WebhookData**。</span><span class="sxs-lookup"><span data-stu-id="97627-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="97627-232">這是因為這是包含 hello hello 要求主體中的 hello 格式格式化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="97627-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Webhook 按鈕](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="97627-234">hello 下列影像顯示 hello 要求從 Windows PowerShell 和回應 hello 結果送出。</span><span class="sxs-lookup"><span data-stu-id="97627-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="97627-235">從回應 hello 和轉換的 tooa 字串擷取 hello 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="97627-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Webhook 按鈕](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="97627-237">hello 下列 runbook 範例 hello 先前的範例要求會接受並啟動 hello hello 要求主體中指定的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="97627-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="97627-238">回應 tooAzure 警示中啟動 runbook</span><span class="sxs-lookup"><span data-stu-id="97627-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="97627-239">Webhook 啟用 runbook 可以使用的 tooreact 太[Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="97627-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="97627-240">可以藉由收集 hello 統計資料，例如效能、 可用性及使用量 hello 協助 Azure 警示監視 Azure 中的資源。</span><span class="sxs-lookup"><span data-stu-id="97627-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="97627-241">您可以收到根據監視您 Azure 資源的計量或事件的警示，目前自動化帳戶僅支援度量。</span><span class="sxs-lookup"><span data-stu-id="97627-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="97627-242">當 hello 的值指定標準超過指派的 hello 臨界值，或如果觸發 hello 設定事件則 toohello 服務管理員或共同管理員 tooresolve hello 警示，如需度量資訊會傳送通知和事件，請參閱太[Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="97627-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="97627-243">除了使用 Azure 警示以通知系統，您可以也啟動回應 tooalerts 中的 runbook。</span><span class="sxs-lookup"><span data-stu-id="97627-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="97627-244">Azure 自動化提供 hello 功能 toorun webhook 啟用 runbook 與 Azure 的警示。</span><span class="sxs-lookup"><span data-stu-id="97627-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="97627-245">當標準超過 hello 會設定臨界值，然後 hello 警示規則變成使用中和觸發程序 hello 依次執行 hello runbook 自動化 webhook。</span><span class="sxs-lookup"><span data-stu-id="97627-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="97627-247">警示內容</span><span class="sxs-lookup"><span data-stu-id="97627-247">Alert context</span></span>
<span data-ttu-id="97627-248">Azure 資源，例如虛擬機器，請考慮為此機器的 CPU 使用率 hello 關鍵效能度量的其中一個。</span><span class="sxs-lookup"><span data-stu-id="97627-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="97627-249">如果 hello CPU 使用率很長一段時間是 100%或更多超過特定大小，您可能想 toorestart hello 虛擬機器 toofix hello 問題。</span><span class="sxs-lookup"><span data-stu-id="97627-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="97627-250">這可以解決所設定的警示規則 toohello 虛擬機器，此規則會作為其度量的 CPU 百分比。</span><span class="sxs-lookup"><span data-stu-id="97627-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="97627-251">CPU 百分比這裡只會被視為範例，但有許多其他度量，您可以設定 tooyour Azure 資源，並重新啟動 hello 虛擬機器是動作採取 toofix 此問題，您可以設定 hello runbook tootake 其他動作。</span><span class="sxs-lookup"><span data-stu-id="97627-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="97627-252">當這個 hello 警示規則變成使用中並觸發程序 hello webhook 啟動 runbook 時，它會傳送 hello 警示內容 toohello runbook。</span><span class="sxs-lookup"><span data-stu-id="97627-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="97627-253">[警示內容](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)包含詳細資料包括**SubscriptionID**， **ResourceGroupName**， **ResourceName**， **ResourceType**， **ResourceId**和**時間戳記**所需的 hello runbook tooidentify hello 資源所在它將會採取動作。</span><span class="sxs-lookup"><span data-stu-id="97627-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="97627-254">警示內容內嵌在 hello hello 內文部分**WebhookData**物件傳送的 toohello runbook，並使用可以存取**Webhook.RequestBody**屬性</span><span class="sxs-lookup"><span data-stu-id="97627-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="97627-255">範例</span><span class="sxs-lookup"><span data-stu-id="97627-255">Example</span></span>
<span data-ttu-id="97627-256">建立 Azure 虛擬機器在您的訂用帳戶和相關聯[警示 toomonitor CPU 百分比度量](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="97627-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="97627-257">在建立 hello 警示務必填入 hello webhook hello URL hello webhook 建立 hello webhook 時所產生的欄位。</span><span class="sxs-lookup"><span data-stu-id="97627-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="97627-258">hello 下列 runbook 範例 hello 警示規則變成使用中，並觸發收集 hello 警示的內容參數所需的 hello runbook tooidentify hello 資源所在它將會採取動作。</span><span class="sxs-lookup"><span data-stu-id="97627-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="97627-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97627-259">Next steps</span></span>
* <span data-ttu-id="97627-260">如需不同的方式 toostart runbook 的詳細資訊，請參閱[Starting a Runbook](automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="97627-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="97627-261">如需檢視 hello Runbook 工作的狀態資訊，請參閱太[在 Azure 自動化中的執行 Runbook](automation-runbook-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="97627-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="97627-262">如何 toouse Azure 自動化 tootake 動作 Azure 警示，請參閱的 toolearn[修復 Azure VM 警示與自動化 Runbook](automation-azure-vm-alert-integration.md)。</span><span class="sxs-lookup"><span data-stu-id="97627-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
