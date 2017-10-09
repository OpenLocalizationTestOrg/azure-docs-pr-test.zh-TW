---
title: "aaaCreate 工作流程，從 範本-Azure 邏輯應用程式 |Microsoft 文件"
description: "快速入門-利用 Azure 邏輯應用程式範本 tooconnect 應用程式，快速建立工作流程和整合資料。"
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a><span data-ttu-id="0e033-103">設定使用預先建立的範本或模式 tooget 快速入門工作流程</span><span class="sxs-lookup"><span data-stu-id="0e033-103">Configure a workflow using a pre-built template or pattern tooget started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="0e033-104">何謂邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="0e033-104">What are logic app templates</span></span>
<span data-ttu-id="0e033-105">邏輯應用程式範本是預先建立的邏輯應用程式，您可以使用 tooquickly 開始建立您自己的工作流程。</span><span class="sxs-lookup"><span data-stu-id="0e033-105">A logic app template is a pre-built logic app that you can use tooquickly get started creating your own workflow.</span></span> 

<span data-ttu-id="0e033-106">這些範本是很好的方式 toodiscover 各種可以使用邏輯應用程式建立的模式。</span><span class="sxs-lookup"><span data-stu-id="0e033-106">These templates are a good way toodiscover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="0e033-107">您可以使用這些範本做為修改它們 toofit 您的案例。</span><span class="sxs-lookup"><span data-stu-id="0e033-107">You can either use these templates as-is or modify them toofit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="0e033-108">可用範本概觀</span><span class="sxs-lookup"><span data-stu-id="0e033-108">Overview of available templates</span></span>
<span data-ttu-id="0e033-109">有許多可用的範本目前已發行的 hello 邏輯應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="0e033-109">There are many available templates currently published in hello logic app platform.</span></span> <span data-ttu-id="0e033-110">以下列出一些範例類別以及 hello 的連接器，使用的型別。</span><span class="sxs-lookup"><span data-stu-id="0e033-110">Some example categories, as well as hello type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="0e033-111">企業雲端範本</span><span class="sxs-lookup"><span data-stu-id="0e033-111">Enterprise cloud templates</span></span>
<span data-ttu-id="0e033-112">此範本會整合 Dynamics CRM、Salesforce、Box、Azure Blob 及其他連接器，以滿足您的企業雲端需求。</span><span class="sxs-lookup"><span data-stu-id="0e033-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="0e033-113">部分可使用這些範本來進行的範例包含組織您的潛在客戶和備份企業檔案資料。</span><span class="sxs-lookup"><span data-stu-id="0e033-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="0e033-114">企業整合套件範本</span><span class="sxs-lookup"><span data-stu-id="0e033-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="0e033-115">VETER 的組態 （驗證、 擷取、 轉換、 充實、 路由傳送） 管線，接收的 X12 EDI 透過 AS2 文件，並將其轉換 tooXML，以及做為 X12 和 AS2 訊息處理。</span><span class="sxs-lookup"><span data-stu-id="0e033-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it tooXML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="0e033-116">通訊協定模式範本</span><span class="sxs-lookup"><span data-stu-id="0e033-116">Protocol pattern templates</span></span>
<span data-ttu-id="0e033-117">這些範本由包含通訊協定模式的邏輯應用程式所組成，例如透過 HTTP 的要求回應以及跨 FTP 和 SFTP 的整合。</span><span class="sxs-lookup"><span data-stu-id="0e033-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="0e033-118">使用這些現存模式，或將它們做為基礎來建立更複雜的通訊協定模式。</span><span class="sxs-lookup"><span data-stu-id="0e033-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="0e033-119">個人生產力範本</span><span class="sxs-lookup"><span data-stu-id="0e033-119">Personal productivity templates</span></span>
<span data-ttu-id="0e033-120">模式 toohelp 改善個人的產能包含範本設定每日提醒，重要的工作項目變成待辦事項清單，以及向 tooa 單一使用者核准步驟的冗長工作自動化。</span><span class="sxs-lookup"><span data-stu-id="0e033-120">Patterns toohelp improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down tooa single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="0e033-121">取用者雲端範本</span><span class="sxs-lookup"><span data-stu-id="0e033-121">Consumer cloud templates</span></span>
<span data-ttu-id="0e033-122">與社交媒體服務 (如 Twitter、Slack 和電子郵件) 整合的簡單範本，最終能夠強化社交媒體行銷計劃。</span><span class="sxs-lookup"><span data-stu-id="0e033-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="0e033-123">其中也包含多雲複製之類的範本，其可透過節省花在傳統重複性工作的時間來協助提高生產力。</span><span class="sxs-lookup"><span data-stu-id="0e033-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-toocreate-a-logic-app-using-a-template"></a><span data-ttu-id="0e033-124">如何 toocreate 邏輯應用程式使用的範本</span><span class="sxs-lookup"><span data-stu-id="0e033-124">How toocreate a logic app using a template</span></span>
<span data-ttu-id="0e033-125">使用邏輯應用程式範本時，啟動 tooget 進入 hello 邏輯應用程式的設計工具。</span><span class="sxs-lookup"><span data-stu-id="0e033-125">tooget started using a logic app template, go into hello logic app designer.</span></span> <span data-ttu-id="0e033-126">如果您正在輸入 hello 設計工具開啟現有的邏輯應用程式，hello 邏輯應用程式會自動載入設計工具檢視中。</span><span class="sxs-lookup"><span data-stu-id="0e033-126">If you're entering hello designer by opening an existing logic app, hello logic app automatically loads in your designer view.</span></span> <span data-ttu-id="0e033-127">不過，如果您要建立新的邏輯應用程式，您會看到下列囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="0e033-127">However, if you're creating a new logic app, you see hello screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="0e033-128">在這個畫面上，您可以選擇 toostart 空白邏輯應用程式或預先建立的範本。</span><span class="sxs-lookup"><span data-stu-id="0e033-128">From this screen, you can either choose toostart with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="0e033-129">如果您選取其中一個 hello 範本，您會提供其他資訊。</span><span class="sxs-lookup"><span data-stu-id="0e033-129">If you select one of hello templates, you are provided with additional information.</span></span> <span data-ttu-id="0e033-130">在此範例中，我們使用 hello *Dropbox 中建立新的檔案時，將它複製 tooOneDrive*範本。</span><span class="sxs-lookup"><span data-stu-id="0e033-130">In this example, we use hello *When a new file is created in Dropbox, copy it tooOneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="0e033-131">如果您選擇 toouse hello 範本，只要選取 hello*使用此範本* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e033-131">If you choose toouse hello template, just select hello *use this template* button.</span></span> <span data-ttu-id="0e033-132">系統會詢問 toosign tooyour 根據哪一個連接器 hello 範本使用的帳戶中。</span><span class="sxs-lookup"><span data-stu-id="0e033-132">You'll be asked toosign in tooyour accounts based on which connectors hello template utilizes.</span></span> <span data-ttu-id="0e033-133">或者，如果您先前已建立使用這些連接器的連線，您可以選取 [繼續]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0e033-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="0e033-134">建立 hello 連接，並選取後*繼續*，hello 邏輯應用程式在設計工具的檢視中開啟。</span><span class="sxs-lookup"><span data-stu-id="0e033-134">After establishing hello connection and selecting *continue*, hello logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="0e033-135">Hello 上述範例中，在許多範本，使用的 hello 案例一些 hello 必要的屬性欄位可能填滿 hello 連接器; 內不過，部分可能仍需要值，才能 tooproperly 部署 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e033-135">In hello example above, as is hello case with many templates, some of hello mandatory property fields may be filled out within hello connectors; however, some might still require a value before being able tooproperly deploy hello logic app.</span></span> <span data-ttu-id="0e033-136">如果您嘗試 toodeploy 而不需輸入一些 hello 遺漏的欄位，並出現錯誤訊息就會通知您。</span><span class="sxs-lookup"><span data-stu-id="0e033-136">If you try toodeploy without entering some of hello missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="0e033-137">如果您想 tooreturn toohello 範本檢視器，選取 hello*範本*hello 上方導覽列中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e033-137">If you wish tooreturn toohello template viewer, select hello *Templates* button in hello top navigation bar.</span></span> <span data-ttu-id="0e033-138">藉由切換後 toohello 範本檢視器，您會遺失任何未儲存的進度。</span><span class="sxs-lookup"><span data-stu-id="0e033-138">By switching back toohello template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="0e033-139">至範本檢視器的先前 tooswitching，您會看到警告訊息，通知您。</span><span class="sxs-lookup"><span data-stu-id="0e033-139">Prior tooswitching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="0e033-140">如何 toodeploy 邏輯應用程式範本所建立的</span><span class="sxs-lookup"><span data-stu-id="0e033-140">How toodeploy a logic app created from a template</span></span>
<span data-ttu-id="0e033-141">一旦您已載入您的範本，並進行任何所需的變更，選取儲存按鈕的 hello hello 左上角。</span><span class="sxs-lookup"><span data-stu-id="0e033-141">Once you have loaded your template and made any desired changes, select hello save button in hello upper left corner.</span></span> <span data-ttu-id="0e033-142">這可儲存並發佈邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e033-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="0e033-143">如果您會喜歡上如何 tooadd 多步驟到現有的邏輯應用程式範本的詳細資訊，或在一般情況下進行編輯，閱讀更多在[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="0e033-143">If you would like more information on how tooadd more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

