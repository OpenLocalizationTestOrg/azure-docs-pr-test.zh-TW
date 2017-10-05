---
title: "BizTalk 服務中的簽發者名稱和簽發者金鑰 | Microsoft Docs"
description: "了解如何在 BizTalk 服務中擷取服務匯流排或存取控制 (ACS) 的簽發者名稱和簽發者金鑰。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="341bf-104">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="341bf-105">Azure BizTalk 服務使用服務匯流排簽發者名稱和簽發者金鑰，以及存取控制簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="341bf-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="341bf-106">具體而言：</span><span class="sxs-lookup"><span data-stu-id="341bf-106">Specifically:</span></span>

| <span data-ttu-id="341bf-107">工作</span><span class="sxs-lookup"><span data-stu-id="341bf-107">Task</span></span> | <span data-ttu-id="341bf-108">什麼簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="341bf-109">從 Visual Studio 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="341bf-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="341bf-110">存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="341bf-111">設定 Azure BizTalk 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="341bf-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="341bf-112">存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="341bf-113">在 Visual Studio 中使用 BizTalk 配接器服務建立 LOB 轉送</span><span class="sxs-lookup"><span data-stu-id="341bf-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="341bf-114">服務匯流排簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="341bf-115">本主題列出擷取簽發者名稱和簽發者金鑰的步驟。</span><span class="sxs-lookup"><span data-stu-id="341bf-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="341bf-116">存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="341bf-117">下列項目會使用存取控制簽發者名稱和簽發者金鑰：</span><span class="sxs-lookup"><span data-stu-id="341bf-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="341bf-118">在 Visual Studio 中建立的 Azure BizTalk 服務應用程式：若要在 Visual Studio 中成功將您的 BizTalk 服務應用程式部署至 Azure，請輸入存取控制簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="341bf-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="341bf-119">Azure BizTalk 服務入口網站：在您建立 BizTalk 服務且開啟 BizTalk 服務入口網站時，系統會使用相同的存取控制值，自動為您的部署註冊您的存取控制簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="341bf-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="341bf-120">取得存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="341bf-121">若要使用 ACS 進行驗證，並取得簽發者名稱和簽發者金鑰值，整體步驟包括：</span><span class="sxs-lookup"><span data-stu-id="341bf-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="341bf-122">安裝 [Azure PowerShell Cmdlet](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="341bf-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="341bf-123">新增您的 Azure 帳戶：`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="341bf-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="341bf-124">傳回您的訂用帳戶名稱：`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="341bf-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="341bf-125">選取您的訂用帳戶：`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="341bf-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="341bf-126">建立新的命名空間：`new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="341bf-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="341bf-127">範例：`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="341bf-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="341bf-128">建立新的 ACS 命名空間時 (這可能要花幾分鐘的時間)，會在連接字串中列出簽發者名稱和簽發者金鑰值：</span><span class="sxs-lookup"><span data-stu-id="341bf-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="341bf-129">總結：</span><span class="sxs-lookup"><span data-stu-id="341bf-129">To summarize:</span></span>  
<span data-ttu-id="341bf-130">簽發者名稱 = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="341bf-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="341bf-131">簽發者金鑰 = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="341bf-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="341bf-132">如需更多資訊，請參閱 [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="341bf-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="341bf-133">服務匯流排簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="341bf-134">BizTalk 配接器服務會使用服務匯流排簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="341bf-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="341bf-135">在 Visual Studio 中，您在 BizTalk 服務專案中使用 BizTalk 配接器服務來連線至內部部署企業營運 (LOB) 系統。</span><span class="sxs-lookup"><span data-stu-id="341bf-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="341bf-136">若要連線，您需要建立 LOB 轉送並輸入 LOB 系統詳細資料。</span><span class="sxs-lookup"><span data-stu-id="341bf-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="341bf-137">如果這樣做，則您也需要輸入服務匯流排簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="341bf-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="341bf-138">擷取服務匯流排簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="341bf-139">登入 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="341bf-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="341bf-140">在左導覽窗格中，選取 [ **服務匯流排**]。</span><span class="sxs-lookup"><span data-stu-id="341bf-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="341bf-141">選取您的命名空間。</span><span class="sxs-lookup"><span data-stu-id="341bf-141">Select your namespace.</span></span> <span data-ttu-id="341bf-142">在工作列中，選取 [ **連線資訊**]。</span><span class="sxs-lookup"><span data-stu-id="341bf-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="341bf-143">這會顯示 **預設簽發者** (簽發者名稱) 和 **預設金鑰** (簽發者金鑰)。</span><span class="sxs-lookup"><span data-stu-id="341bf-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="341bf-144">您可以複製這些值。</span><span class="sxs-lookup"><span data-stu-id="341bf-144">Their values can be copied.</span></span>  

<span data-ttu-id="341bf-145">總結：</span><span class="sxs-lookup"><span data-stu-id="341bf-145">To summarize:</span></span>  
<span data-ttu-id="341bf-146">簽發者名稱 = 預設簽發者</span><span class="sxs-lookup"><span data-stu-id="341bf-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="341bf-147">簽發者金鑰 = 預設金鑰</span><span class="sxs-lookup"><span data-stu-id="341bf-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="341bf-148">下一步</span><span class="sxs-lookup"><span data-stu-id="341bf-148">Next</span></span>
<span data-ttu-id="341bf-149">其他 Azure BizTalk 服務主題：</span><span class="sxs-lookup"><span data-stu-id="341bf-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="341bf-150">安裝 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="341bf-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="341bf-151">教學課程：Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="341bf-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="341bf-152">如何開始使用 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="341bf-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="341bf-153">Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="341bf-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="341bf-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="341bf-154">See Also</span></span>
* [<span data-ttu-id="341bf-155">做法：使用 ACS 管理服務來設定服務身分識別</span><span class="sxs-lookup"><span data-stu-id="341bf-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="341bf-156">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="341bf-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="341bf-157">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="341bf-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="341bf-158">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="341bf-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="341bf-159">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="341bf-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="341bf-160">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="341bf-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="341bf-161">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="341bf-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

