---
title: "aaaUse hello 邏輯應用程式中的 SharePoint 伺服器連接器 |Microsoft 文件"
description: "開始使用邏輯應用程式中的 hello hello SharePoint 伺服器連接器"
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
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="16864-103">開始使用 hello SharePoint 連接器</span><span class="sxs-lookup"><span data-stu-id="16864-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="16864-104">hello SharePoint 連接器提供清單方式的 toowork SharePoint 上。</span><span class="sxs-lookup"><span data-stu-id="16864-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="16864-105">從建立邏輯應用程式開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="16864-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="16864-106">建立連接 tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="16864-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="16864-107">toouse hello SharePoint 連接器，請先建立**連接**然後提供這些屬性中的 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="16864-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="16864-108">屬性</span><span class="sxs-lookup"><span data-stu-id="16864-108">Property</span></span> | <span data-ttu-id="16864-109">必要</span><span class="sxs-lookup"><span data-stu-id="16864-109">Required</span></span> | <span data-ttu-id="16864-110">說明</span><span class="sxs-lookup"><span data-stu-id="16864-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16864-111">權杖</span><span class="sxs-lookup"><span data-stu-id="16864-111">Token</span></span> |<span data-ttu-id="16864-112">是</span><span class="sxs-lookup"><span data-stu-id="16864-112">Yes</span></span> |<span data-ttu-id="16864-113">提供 SharePoint 的認證</span><span class="sxs-lookup"><span data-stu-id="16864-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="16864-114">tooconnect 太**SharePoint**，輸入您的身分識別 （使用者名稱和密碼、 智慧卡認證等） tooSharePoint。</span><span class="sxs-lookup"><span data-stu-id="16864-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="16864-115">一旦您已驗證，您可以繼續 toouse hello SharePoint 連接器應用程式邏輯中。</span><span class="sxs-lookup"><span data-stu-id="16864-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="16864-116">在 hello 設計工具中的應用程式邏輯，請依照這些步驟 toosign SharePoint toocreate hello 連線到**連接**邏輯應用程式中使用：</span><span class="sxs-lookup"><span data-stu-id="16864-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="16864-117">輸入 SharePoint hello [搜尋] 方塊中，並等候 hello 搜尋 tooreturn hello 名稱中在與 SharePoint 的所有項目：</span><span class="sxs-lookup"><span data-stu-id="16864-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![設定 SharePoint][1]  
2. <span data-ttu-id="16864-119">選取 [SharePoint - 當檔案建立時]</span><span class="sxs-lookup"><span data-stu-id="16864-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="16864-120">選取**登入 tooSharePoint**:</span><span class="sxs-lookup"><span data-stu-id="16864-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="16864-121">![設定 SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="16864-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="16864-122">提供與 SharePoint 中 tooauthenticate 您 SharePoint 認證 toosign</span><span class="sxs-lookup"><span data-stu-id="16864-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![設定 SharePoint][3]     
5. <span data-ttu-id="16864-124">Hello 驗證完成後，您應該重新導向的 tooyour 邏輯應用程式 toocomplete 它藉由設定 SharePoint 的**會建立一個檔案**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="16864-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="16864-125">![設定 SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="16864-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="16864-126">然後，您可以加入其他觸發程序，您需要 toocomplete 邏輯應用程式的動作。</span><span class="sxs-lookup"><span data-stu-id="16864-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="16864-127">儲存您的工作，藉由選取**儲存**hello 上方的功能表列上。</span><span class="sxs-lookup"><span data-stu-id="16864-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="16864-128">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="16864-128">Connector-specific details</span></span>

<span data-ttu-id="16864-129">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/sharepoint/)。</span><span class="sxs-lookup"><span data-stu-id="16864-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="16864-130">其他連接器</span><span class="sxs-lookup"><span data-stu-id="16864-130">More connectors</span></span>
<span data-ttu-id="16864-131">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="16864-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
