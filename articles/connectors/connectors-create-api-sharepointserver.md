---
title: "在 Logic Apps 中使用 SharePoint Server 連接器 | Microsoft Docs"
description: "開始在 Logic Apps 中使用 SharePoint Server 連接器"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="9eacc-103">開始使用 SharePoint 連接器</span><span class="sxs-lookup"><span data-stu-id="9eacc-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="9eacc-104">SharePoint 連接器提供一種方式，讓您能夠使用 SharePoint 上的清單。</span><span class="sxs-lookup"><span data-stu-id="9eacc-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="9eacc-105">從建立邏輯應用程式開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9eacc-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="9eacc-106">建立至 SharePoint 的連線</span><span class="sxs-lookup"><span data-stu-id="9eacc-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="9eacc-107">如要使用 SharePoint 連接器，您必須先建立 **連線** ，然後提供下列屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="9eacc-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="9eacc-108">屬性</span><span class="sxs-lookup"><span data-stu-id="9eacc-108">Property</span></span> | <span data-ttu-id="9eacc-109">必要</span><span class="sxs-lookup"><span data-stu-id="9eacc-109">Required</span></span> | <span data-ttu-id="9eacc-110">說明</span><span class="sxs-lookup"><span data-stu-id="9eacc-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eacc-111">權杖</span><span class="sxs-lookup"><span data-stu-id="9eacc-111">Token</span></span> |<span data-ttu-id="9eacc-112">是</span><span class="sxs-lookup"><span data-stu-id="9eacc-112">Yes</span></span> |<span data-ttu-id="9eacc-113">提供 SharePoint 的認證</span><span class="sxs-lookup"><span data-stu-id="9eacc-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="9eacc-114">若要連接到 **SharePoint** ，請向 SharePoint 提供您的身分識別 (使用者名稱和密碼、智慧卡認證等等)。</span><span class="sxs-lookup"><span data-stu-id="9eacc-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="9eacc-115">通過驗證之後，您就可以在邏輯應用程式中使用 SharePoint 連接器。</span><span class="sxs-lookup"><span data-stu-id="9eacc-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="9eacc-116">在邏輯應用程式的設計工具中，請依照下列步驟來登入 SharePoint，以便建立 **連接** 供您的邏輯應用程式使用：</span><span class="sxs-lookup"><span data-stu-id="9eacc-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="9eacc-117">在搜尋方塊中輸入 SharePoint，等候搜尋傳回名稱中有 SharePoint 的所有項目：</span><span class="sxs-lookup"><span data-stu-id="9eacc-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![設定 SharePoint][1]  
2. <span data-ttu-id="9eacc-119">選取 [SharePoint - 當檔案建立時]</span><span class="sxs-lookup"><span data-stu-id="9eacc-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="9eacc-120">選取 [登入 SharePoint]：</span><span class="sxs-lookup"><span data-stu-id="9eacc-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="9eacc-121">![設定 SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="9eacc-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="9eacc-122">提供您的 SharePoint 認證來登入向 SharePoint 進行驗證 </span><span class="sxs-lookup"><span data-stu-id="9eacc-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![設定 SharePoint][3]     
5. <span data-ttu-id="9eacc-124">驗證完成後，您會被重新導向至邏輯應用程式，設定 SharePoint 的 [當檔案建立時]  對話方塊後即可完成。</span><span class="sxs-lookup"><span data-stu-id="9eacc-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="9eacc-125">![設定 SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="9eacc-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="9eacc-126">接著，您可以新增所需的其他觸發和動作來完成邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9eacc-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="9eacc-127">選取上方功能表列的 [儲存]  來儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="9eacc-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="9eacc-128">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="9eacc-128">Connector-specific details</span></span>

<span data-ttu-id="9eacc-129">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/sharepoint/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="9eacc-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="9eacc-130">其他連接器</span><span class="sxs-lookup"><span data-stu-id="9eacc-130">More connectors</span></span>
<span data-ttu-id="9eacc-131">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="9eacc-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
