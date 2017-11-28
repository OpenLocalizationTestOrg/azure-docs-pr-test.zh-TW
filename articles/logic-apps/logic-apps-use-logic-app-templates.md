---
title: "從範本建立工作流程 - Azure Logic Apps | Microsoft Docs"
description: "入門 - 使用 Azure 邏輯應用程式範本快速建立工作流程，來連接應用程式並整合資料。"
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
ms.openlocfilehash: 89272869f7dfaa34cbd2ad32d67dca0955e6158b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-to-get-started-quickly"></a><span data-ttu-id="189e4-103">使用預先建置的範本或模式設定工作流程，以便快速開始</span><span class="sxs-lookup"><span data-stu-id="189e4-103">Configure a workflow using a pre-built template or pattern to get started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="189e4-104">何謂邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="189e4-104">What are logic app templates</span></span>
<span data-ttu-id="189e4-105">邏輯應用程式範本是預先建置的邏輯應用程式，可供您快速開始建立自己的工作流程。</span><span class="sxs-lookup"><span data-stu-id="189e4-105">A logic app template is a pre-built logic app that you can use to quickly get started creating your own workflow.</span></span> 

<span data-ttu-id="189e4-106">這些範本非常適合用來探索各種可使用邏輯應用程式建置的模式。</span><span class="sxs-lookup"><span data-stu-id="189e4-106">These templates are a good way to discover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="189e4-107">您可以直接使用這些範本，或者修改它們以符合您的案例。</span><span class="sxs-lookup"><span data-stu-id="189e4-107">You can either use these templates as-is or modify them to fit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="189e4-108">可用範本概觀</span><span class="sxs-lookup"><span data-stu-id="189e4-108">Overview of available templates</span></span>
<span data-ttu-id="189e4-109">邏輯應用程式平台目前已發佈了許多可用的範本。</span><span class="sxs-lookup"><span data-stu-id="189e4-109">There are many available templates currently published in the logic app platform.</span></span> <span data-ttu-id="189e4-110">以下列出一些範例類別以及其中所使用的連接器類型。</span><span class="sxs-lookup"><span data-stu-id="189e4-110">Some example categories, as well as the type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="189e4-111">企業雲端範本</span><span class="sxs-lookup"><span data-stu-id="189e4-111">Enterprise cloud templates</span></span>
<span data-ttu-id="189e4-112">此範本會整合 Dynamics CRM、Salesforce、Box、Azure Blob 及其他連接器，以滿足您的企業雲端需求。</span><span class="sxs-lookup"><span data-stu-id="189e4-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="189e4-113">部分可使用這些範本來進行的範例包含組織您的潛在客戶和備份企業檔案資料。</span><span class="sxs-lookup"><span data-stu-id="189e4-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="189e4-114">企業整合套件範本</span><span class="sxs-lookup"><span data-stu-id="189e4-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="189e4-115">VETER (驗證、擷取、轉換、擴充、路由) 管線的組態、透過 AS2 接收 X12 EDI 文件並將其轉換為 XML，以及 X12 和 AS2 訊息處理。</span><span class="sxs-lookup"><span data-stu-id="189e4-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it to XML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="189e4-116">通訊協定模式範本</span><span class="sxs-lookup"><span data-stu-id="189e4-116">Protocol pattern templates</span></span>
<span data-ttu-id="189e4-117">這些範本由包含通訊協定模式的邏輯應用程式所組成，例如透過 HTTP 的要求回應以及跨 FTP 和 SFTP 的整合。</span><span class="sxs-lookup"><span data-stu-id="189e4-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="189e4-118">使用這些現存模式，或將它們做為基礎來建立更複雜的通訊協定模式。</span><span class="sxs-lookup"><span data-stu-id="189e4-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="189e4-119">個人生產力範本</span><span class="sxs-lookup"><span data-stu-id="189e4-119">Personal productivity templates</span></span>
<span data-ttu-id="189e4-120">用來協助提升個人生產力的模式所包含的範本會設定每日提醒、將重要的工作項目轉換成待辦事項清單，並將冗長的工作自動縮減為一個使用者核准步驟。</span><span class="sxs-lookup"><span data-stu-id="189e4-120">Patterns to help improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down to a single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="189e4-121">取用者雲端範本</span><span class="sxs-lookup"><span data-stu-id="189e4-121">Consumer cloud templates</span></span>
<span data-ttu-id="189e4-122">與社交媒體服務 (如 Twitter、Slack 和電子郵件) 整合的簡單範本，最終能夠強化社交媒體行銷計劃。</span><span class="sxs-lookup"><span data-stu-id="189e4-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="189e4-123">其中也包含多雲複製之類的範本，其可透過節省花在傳統重複性工作的時間來協助提高生產力。</span><span class="sxs-lookup"><span data-stu-id="189e4-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-to-create-a-logic-app-using-a-template"></a><span data-ttu-id="189e4-124">使用範本建立邏輯應用程式的方式</span><span class="sxs-lookup"><span data-stu-id="189e4-124">How to create a logic app using a template</span></span>
<span data-ttu-id="189e4-125">若要開始使用邏輯應用程式範本，請進入邏輯應用程式設計工具。</span><span class="sxs-lookup"><span data-stu-id="189e4-125">To get started using a logic app template, go into the logic app designer.</span></span> <span data-ttu-id="189e4-126">如果您透過開啟現有邏輯應用程式來進入設計工具，邏輯應用程式會自動載入設計工具檢視中。</span><span class="sxs-lookup"><span data-stu-id="189e4-126">If you're entering the designer by opening an existing logic app, the logic app automatically loads in your designer view.</span></span> <span data-ttu-id="189e4-127">不過，如果您要建立新的邏輯應用程式，您會看到下列畫面。</span><span class="sxs-lookup"><span data-stu-id="189e4-127">However, if you're creating a new logic app, you see the screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="189e4-128">在此畫面中，您可以選擇以空白邏輯應用程式或預先建置的範本來開始著手。</span><span class="sxs-lookup"><span data-stu-id="189e4-128">From this screen, you can either choose to start with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="189e4-129">如果您選取其中一個範本，系統會提供其他資訊給您。</span><span class="sxs-lookup"><span data-stu-id="189e4-129">If you select one of the templates, you are provided with additional information.</span></span> <span data-ttu-id="189e4-130">在此範例中，我們使用「在 Dropbox 中建立新檔案時，將它複製到 OneDrive」  範本。</span><span class="sxs-lookup"><span data-stu-id="189e4-130">In this example, we use the *When a new file is created in Dropbox, copy it to OneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="189e4-131">如果您選擇使用此範本，則只要選取 [使用此範本]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="189e4-131">If you choose to use the template, just select the *use this template* button.</span></span> <span data-ttu-id="189e4-132">系統會要求您根據範本所使用的連接器登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="189e4-132">You'll be asked to sign in to your accounts based on which connectors the template utilizes.</span></span> <span data-ttu-id="189e4-133">或者，如果您先前已建立使用這些連接器的連線，您可以選取 [繼續]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="189e4-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="189e4-134">建立連線並選取 [繼續] 之後，邏輯應用程式便會在設計工具檢視中開啟。</span><span class="sxs-lookup"><span data-stu-id="189e4-134">After establishing the connection and selecting *continue*, the logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="189e4-135">在上述範例中，和許多範本所遇到的狀況相同，連接器內的某些必要屬性欄位可能已填入資料；不過，有些仍可能需要填入值，然後才能正確部署邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="189e4-135">In the example above, as is the case with many templates, some of the mandatory property fields may be filled out within the connectors; however, some might still require a value before being able to properly deploy the logic app.</span></span> <span data-ttu-id="189e4-136">如果您嘗試不輸入遺漏的欄位就進行部署，將會出現錯誤訊息來通知您。</span><span class="sxs-lookup"><span data-stu-id="189e4-136">If you try to deploy without entering some of the missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="189e4-137">如果您想要返回範本檢視器，請選取頂端導覽列中的 [範本]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="189e4-137">If you wish to return to the template viewer, select the *Templates* button in the top navigation bar.</span></span> <span data-ttu-id="189e4-138">切換回範本檢視器將會讓您遺失任何未儲存的進度。</span><span class="sxs-lookup"><span data-stu-id="189e4-138">By switching back to the template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="189e4-139">在切換回範本檢視器之前，您會看到警告訊息來告知您這一點。</span><span class="sxs-lookup"><span data-stu-id="189e4-139">Prior to switching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-to-deploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="189e4-140">如何部署從範本建立的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="189e4-140">How to deploy a logic app created from a template</span></span>
<span data-ttu-id="189e4-141">載入範本並進行所需的任何變更之後，請選取左上角的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="189e4-141">Once you have loaded your template and made any desired changes, select the save button in the upper left corner.</span></span> <span data-ttu-id="189e4-142">這可儲存並發佈邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="189e4-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="189e4-143">如果您需要如何對現有邏輯應用程式範本新增更多步驟或進行一般編輯的詳細資訊，請參閱 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="189e4-143">If you would like more information on how to add more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

