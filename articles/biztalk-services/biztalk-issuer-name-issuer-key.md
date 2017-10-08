---
title: "aaaIssuer 名稱和簽發者金鑰，在 BizTalk 服務 |Microsoft 文件"
description: "深入了解如何 tooretrieve 的簽發者名稱和簽發者金鑰的服務匯流排 」 或 「 存取控制 (ACS) 在 BizTalk 服務中。 MABS，WABS"
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
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="5a301-104">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="5a301-105">Hello 服務匯流排簽發者名稱和簽發者金鑰和 hello 存取控制簽發者名稱和簽發者金鑰，則會使用 azure BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="5a301-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="5a301-106">具體而言：</span><span class="sxs-lookup"><span data-stu-id="5a301-106">Specifically:</span></span>

| <span data-ttu-id="5a301-107">工作</span><span class="sxs-lookup"><span data-stu-id="5a301-107">Task</span></span> | <span data-ttu-id="5a301-108">什麼簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="5a301-109">從 Visual Studio 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="5a301-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="5a301-110">存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="5a301-111">設定 hello Azure BizTalk 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="5a301-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="5a301-112">存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="5a301-113">建立 LOB 轉送以 hello Visual Studio 中的 BizTalk 配接器服務</span><span class="sxs-lookup"><span data-stu-id="5a301-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="5a301-114">服務匯流排簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="5a301-115">本主題列出 hello 步驟 tooretrieve hello 簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="5a301-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="5a301-116">存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="5a301-117">hello 存取控制簽發者名稱和簽發者金鑰會使用 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5a301-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="5a301-118">在 Visual Studio 中建立 Azure BizTalk 服務應用程式： toosuccessfully 部署在 Visual Studio tooAzure BizTalk 服務應用程式，您輸入 hello 存取控制簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="5a301-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="5a301-119">hello Azure BizTalk 服務入口網站： 當您建立 BizTalk 服務，再開啟 hello BizTalk 服務入口網站，您的存取控制簽發者名稱和簽發者金鑰就會自動為您的部署與註冊 hello 相同的存取控制值。</span><span class="sxs-lookup"><span data-stu-id="5a301-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="5a301-120">取得 hello 存取控制簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="5a301-121">toouse ACS 驗證和 get hello 簽發者名稱和簽發者金鑰值，hello 整體步驟包括：</span><span class="sxs-lookup"><span data-stu-id="5a301-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="5a301-122">安裝 hello [Azure Powershell cmdlet](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="5a301-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="5a301-123">新增您的 Azure 帳戶：`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="5a301-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="5a301-124">傳回您的訂用帳戶名稱：`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="5a301-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="5a301-125">選取您的訂用帳戶：`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="5a301-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="5a301-126">建立新的命名空間：`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="5a301-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="5a301-127">範例：`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="5a301-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="5a301-128">（這可能要花費幾分鐘的時間） 建立 hello 新 ACS 命名空間時，會列出 hello 連接字串 hello 簽發者名稱和簽發者金鑰值：</span><span class="sxs-lookup"><span data-stu-id="5a301-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

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

<span data-ttu-id="5a301-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="5a301-129">toosummarize:</span></span>  
<span data-ttu-id="5a301-130">簽發者名稱 = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="5a301-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="5a301-131">簽發者金鑰 = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="5a301-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="5a301-132">有更詳細的 hello [New-azuresbnamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5a301-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="5a301-133">服務匯流排簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="5a301-134">BizTalk 配接器服務會使用服務匯流排簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="5a301-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="5a301-135">在 Visual Studio 中 BizTalk 服務專案中，您可以使用 hello BizTalk 配接器服務 tooconnect tooan 在內部部署的特定業務 (LOB) 系統。</span><span class="sxs-lookup"><span data-stu-id="5a301-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="5a301-136">tooconnect，您建立 hello LOB 轉送，並輸入您的 LOB 系統詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5a301-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="5a301-137">如此一來，您也輸入 hello 服務匯流排簽發者名稱和簽發者金鑰。</span><span class="sxs-lookup"><span data-stu-id="5a301-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="5a301-138">tooretrieve hello 服務匯流排簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="5a301-139">登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="5a301-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="5a301-140">在 hello 左側瀏覽窗格中，選取**Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="5a301-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="5a301-141">選取您的命名空間。</span><span class="sxs-lookup"><span data-stu-id="5a301-141">Select your namespace.</span></span> <span data-ttu-id="5a301-142">在 hello 工作列上，選取 **連接資訊**。</span><span class="sxs-lookup"><span data-stu-id="5a301-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="5a301-143">這會顯示 hello**預設簽發者**（簽發者名稱） 和**預設金鑰**（簽發者金鑰）。</span><span class="sxs-lookup"><span data-stu-id="5a301-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="5a301-144">您可以複製這些值。</span><span class="sxs-lookup"><span data-stu-id="5a301-144">Their values can be copied.</span></span>  

<span data-ttu-id="5a301-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="5a301-145">toosummarize:</span></span>  
<span data-ttu-id="5a301-146">簽發者名稱 = 預設簽發者</span><span class="sxs-lookup"><span data-stu-id="5a301-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="5a301-147">簽發者金鑰 = 預設金鑰</span><span class="sxs-lookup"><span data-stu-id="5a301-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="5a301-148">下一步</span><span class="sxs-lookup"><span data-stu-id="5a301-148">Next</span></span>
<span data-ttu-id="5a301-149">其他 Azure BizTalk 服務主題：</span><span class="sxs-lookup"><span data-stu-id="5a301-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="5a301-150">安裝 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="5a301-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="5a301-151">教學課程：Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="5a301-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="5a301-152">開始使用我要如何 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="5a301-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="5a301-153">Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="5a301-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="5a301-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5a301-154">See Also</span></span>
* [<span data-ttu-id="5a301-155">如何： 使用 ACS 管理服務 tooConfigure 服務身分識別</span><span class="sxs-lookup"><span data-stu-id="5a301-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="5a301-156">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="5a301-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="5a301-157">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="5a301-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="5a301-158">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="5a301-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="5a301-159">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="5a301-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="5a301-160">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="5a301-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="5a301-161">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="5a301-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

