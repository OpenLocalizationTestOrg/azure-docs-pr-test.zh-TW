---
title: "aaaInstall 在內部部署資料閘道 Azure 邏輯應用程式 |Microsoft 文件"
description: "您存取在內部部署資料來源之前，安裝 hello 在內部部署資料閘道進行快速的資料傳輸和在內部部署資料來源與邏輯應用程式之間的加密"
keywords: "存取資料, 內部部署, 資料傳輸, 加密, 資料來源"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="e4202-104">Azure 邏輯應用程式安裝 hello 在內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="e4202-105">您的 logic apps 可以存取在內部部署資料來源之前，您必須安裝並設定 hello 在內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="e4202-106">hello 閘道作為橋接器，提供快速的資料傳輸和內部部署系統與應用程式邏輯之間的加密。</span><span class="sxs-lookup"><span data-stu-id="e4202-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="e4202-107">hello 閘道轉送上 hello Azure Service Bus 透過加密通道在內部部署來源的資料。</span><span class="sxs-lookup"><span data-stu-id="e4202-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="e4202-108">所有流量都來自為 hello 閘道代理程式的安全輸出流量。</span><span class="sxs-lookup"><span data-stu-id="e4202-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="e4202-109">深入了解[hello 資料閘道的運作方式](#gateway-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="e4202-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="e4202-110">hello 閘道支援連線 toothese 資料來源，在內部部署：</span><span class="sxs-lookup"><span data-stu-id="e4202-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="e4202-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="e4202-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="e4202-112">DB2</span><span class="sxs-lookup"><span data-stu-id="e4202-112">DB2</span></span>  
*   <span data-ttu-id="e4202-113">檔案系統</span><span class="sxs-lookup"><span data-stu-id="e4202-113">File System</span></span>
*   <span data-ttu-id="e4202-114">Informix</span><span class="sxs-lookup"><span data-stu-id="e4202-114">Informix</span></span>
*   <span data-ttu-id="e4202-115">MQ</span><span class="sxs-lookup"><span data-stu-id="e4202-115">MQ</span></span>
*   <span data-ttu-id="e4202-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="e4202-116">MySQL</span></span>
*   <span data-ttu-id="e4202-117">Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="e4202-117">Oracle Database</span></span>
*   <span data-ttu-id="e4202-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e4202-118">PostgreSQL</span></span>
*   <span data-ttu-id="e4202-119">SAP 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="e4202-119">SAP Application Server</span></span> 
*   <span data-ttu-id="e4202-120">SAP 訊息伺服器</span><span class="sxs-lookup"><span data-stu-id="e4202-120">SAP Message Server</span></span>
*   <span data-ttu-id="e4202-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="e4202-121">SharePoint</span></span>
*   <span data-ttu-id="e4202-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e4202-122">SQL Server</span></span>
*   <span data-ttu-id="e4202-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="e4202-123">Teradata</span></span>

<span data-ttu-id="e4202-124">這些步驟顯示如何 toofirst 安裝 hello 內部部署資料閘道，才能[hello 閘道和您的 logic apps 之間的連接設定](./logic-apps-gateway-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="e4202-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="e4202-125">如需所支援連接器的詳細資訊，請參閱 [Azure Logic Apps 的連接器](https://docs.microsoft.com/azure/connectors/apis-list)。</span><span class="sxs-lookup"><span data-stu-id="e4202-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="e4202-126">如需如何 toouse hello 閘道與其他服務資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="e4202-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="e4202-127">Microsoft Power BI 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="e4202-128">Azure Analysis Services 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="e4202-129">Microsoft Flow 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="e4202-130">Microsoft PowerApps 內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="e4202-131">需求</span><span class="sxs-lookup"><span data-stu-id="e4202-131">Requirements</span></span>

<span data-ttu-id="e4202-132">**最低**：</span><span class="sxs-lookup"><span data-stu-id="e4202-132">**Minimum**:</span></span>

* <span data-ttu-id="e4202-133">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="e4202-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="e4202-134">64 位元版本的 Windows 7 或 Windows Server 2008 R2 (或更新版本)</span><span class="sxs-lookup"><span data-stu-id="e4202-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="e4202-135">**建議**：</span><span class="sxs-lookup"><span data-stu-id="e4202-135">**Recommended**:</span></span>

* <span data-ttu-id="e4202-136">8 核心 CPU</span><span class="sxs-lookup"><span data-stu-id="e4202-136">8 Core CPU</span></span>
* <span data-ttu-id="e4202-137">8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="e4202-137">8 GB Memory</span></span>
* <span data-ttu-id="e4202-138">64 位元版本的 Windows 2012 R2 (或更新版本)</span><span class="sxs-lookup"><span data-stu-id="e4202-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="e4202-139">**重要考量**︰</span><span class="sxs-lookup"><span data-stu-id="e4202-139">**Important considerations**:</span></span>

* <span data-ttu-id="e4202-140">只能在本機電腦上安裝 hello 在內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="e4202-141">您無法在網域控制站上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="e4202-142">您沒有在 hello tooinstall hello 閘道做為資料來源的同一部電腦。</span><span class="sxs-lookup"><span data-stu-id="e4202-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="e4202-143">toominimize 延遲，您可以安裝接近以可能 tooyour 資料來源，或在 hello 上相同的 hello 閘道電腦，假設您有權限。</span><span class="sxs-lookup"><span data-stu-id="e4202-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="e4202-144">請勿關閉、 toosleep，或並不會因為 hello 閘道器無法在這些情況下執行時連接 toohello 網際網路的電腦上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="e4202-145">此外，透過無線網路的閘道效能可能會受到影響。</span><span class="sxs-lookup"><span data-stu-id="e4202-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="e4202-146">在安裝期間，您必須登入[公司或學校帳戶](https://docs.microsoft.com/azure/active-directory/sign-up-organization)，該帳戶是由 Azure Active Directory (Azure AD) 所管理，而非 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4202-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="e4202-147">您有 toouse hello 相同的工作或學校帳戶稍後在 hello Azure 入口網站，當您建立並關聯閘道安裝閘道資源。</span><span class="sxs-lookup"><span data-stu-id="e4202-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="e4202-148">當您建立 hello 連線之間邏輯應用程式與 hello 在內部部署資料來源，然後選取此閘道資源。</span><span class="sxs-lookup"><span data-stu-id="e4202-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="e4202-149">為何必須使用公司或學校的 Azure AD 帳戶？</span><span class="sxs-lookup"><span data-stu-id="e4202-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="e4202-150">如果您註冊 Office 365 供應項目，但是未提供實際的公司電子郵件，您的登入位址看起來可能會像 jeff@contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="e4202-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="e4202-151">如果您有現有的閘道設定與之前版本 14.16.6317.4 的安裝程式，您無法變更您的閘道執行 hello 最新的安裝程式的位置。</span><span class="sxs-lookup"><span data-stu-id="e4202-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="e4202-152">不過，您可以使用 hello 最新安裝程式 tooset 註冊新的閘道與 hello 改為您想要的位置。</span><span class="sxs-lookup"><span data-stu-id="e4202-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="e4202-153">如果您有閘道安裝程式之前版本 14.16.6317.4，但您尚未安裝您的閘道，您可以下載並使用 hello 最新的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="e4202-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="e4202-154">安裝 hello 部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="e4202-155">[下載並在本機電腦上執行 hello 閘道安裝程式](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="e4202-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="e4202-156">檢閱並接受 hello 使用條款和隱私權聲明。</span><span class="sxs-lookup"><span data-stu-id="e4202-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="e4202-157">指定您想要 tooinstall hello 閘道在本機電腦上的 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="e4202-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="e4202-158">在系統提示時，使用公司或學校的 Azure 帳戶而非 Microsoft 帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="e4202-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![使用 Azure 公司或學校帳戶登入](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="e4202-160">現在您已安裝的閘道註冊 hello[閘道器雲端服務](#gateway-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="e4202-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="e4202-161">選擇**在這部電腦上註冊新的閘道**。</span><span class="sxs-lookup"><span data-stu-id="e4202-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="e4202-162">hello 閘道器雲端服務會加密，並將您的資料來源認證和閘道器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e4202-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="e4202-163">hello 服務也會將查詢和它們的結果，應用程式邏輯、 hello 在內部部署資料閘道和您的資料來源之間路由在內部部署。</span><span class="sxs-lookup"><span data-stu-id="e4202-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="e4202-164">為閘道安裝提供名稱。</span><span class="sxs-lookup"><span data-stu-id="e4202-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="e4202-165">建立復原金鑰，然後確認復原金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4202-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="e4202-166">修復金鑰必須至少包含 8 個字元。</span><span class="sxs-lookup"><span data-stu-id="e4202-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="e4202-167">請確定您儲存，並將 hello 金鑰保存在安全的地方。</span><span class="sxs-lookup"><span data-stu-id="e4202-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="e4202-168">您也需要此金鑰，當您想 toomigrate，還原或取代現有的閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="e4202-169">hello 閘道器雲端服務和您的閘道安裝所使用的 Azure 服務匯流排 toochange hello 預設區域選擇**變更區域**。</span><span class="sxs-lookup"><span data-stu-id="e4202-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![變更區域](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="e4202-171">hello 預設區域是與 Azure AD 租用戶相關聯的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="e4202-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="e4202-172">在 hello 下一步] 窗格中，開啟 [hello**選取地區**太選擇不同的區域。</span><span class="sxs-lookup"><span data-stu-id="e4202-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![選取其他區域](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="e4202-174">例如，您可能會選取 hello 與應用程式邏輯，相同的區域，或選取 hello 區域最接近 tooyour 在內部部署資料來源，以便您可以減少延遲。</span><span class="sxs-lookup"><span data-stu-id="e4202-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="e4202-175">閘道資源和邏輯應用程式可位於不同位置。</span><span class="sxs-lookup"><span data-stu-id="e4202-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="e4202-176">安裝完成後就無法變更此區域。</span><span class="sxs-lookup"><span data-stu-id="e4202-176">You can't change this region after installation.</span></span> <span data-ttu-id="e4202-177">這個區域也會決定，並限制 hello 位置，您可以在其中建立閘道 hello Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="e4202-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="e4202-178">因此當您在 Azure 中建立閘道資源，請確定 hello 資源位置符合您在閘道安裝期間選取的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="e4202-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="e4202-179">如果您想 toouse 不同的區域閘道之後，您必須設定新的閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="e4202-180">準備就緒時，請選擇 [完成]。</span><span class="sxs-lookup"><span data-stu-id="e4202-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="e4202-181">現在遵循 hello Azure 入口網站中的這些步驟，這樣您就可以[建立閘道的 Azure 資源](../logic-apps/logic-apps-gateway-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="e4202-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="e4202-182">深入了解[hello 資料閘道的運作方式](#gateway-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="e4202-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="e4202-183">移轉、還原或取代現有閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="e4202-184">tooperform 這些工作，您必須擁有 hello hello 閘道已安裝時所指定的修復金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4202-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="e4202-185">在電腦的 [開始] 功能表中，選擇 [內部部署資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="e4202-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="e4202-186">Hello 安裝程式隨即開啟，來登入之後 hello 相同 Azure 工作或學校帳戶，先前已使用 tooinstall hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="e4202-187">選擇**移轉、還原或取代現有閘道**。</span><span class="sxs-lookup"><span data-stu-id="e4202-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="e4202-188">提供您想透過 toomigrate、 還原或接受的 hello 閘道的 hello 名稱及修復金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4202-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="e4202-189">重新啟動 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="e4202-189">Restart hello gateway</span></span>

<span data-ttu-id="e4202-190">hello 閘道會當做 Windows 服務來執行。</span><span class="sxs-lookup"><span data-stu-id="e4202-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="e4202-191">與其他任何 Windows 服務，您可以啟動和停止 hello 服務有多個。</span><span class="sxs-lookup"><span data-stu-id="e4202-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="e4202-192">比方說，您可以 hello hello 閘道執行所在的電腦上提高權限開啟命令提示字元並執行下列任一命令：</span><span class="sxs-lookup"><span data-stu-id="e4202-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="e4202-193">toostop hello 服務，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="e4202-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="e4202-194">toostart hello 服務，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="e4202-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="e4202-195">Windows 服務帳戶</span><span class="sxs-lookup"><span data-stu-id="e4202-195">Windows service account</span></span>

<span data-ttu-id="e4202-196">hello 在內部部署資料閘道設定 toouse `NT SERVICE\PBIEgwService` hello windows 服務的登入認證。</span><span class="sxs-lookup"><span data-stu-id="e4202-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="e4202-197">根據預設，hello 閘道具有 hello hello 機器的 「 以服務方式登入 」 權限 hello 閘道的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="e4202-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="e4202-198">hello Windows 服務帳戶與從 hello 帳戶用來連線 tooon 內部部署資料來源，以及從 hello Azure 工作或學校帳戶用於 toosign toocloud 服務中。</span><span class="sxs-lookup"><span data-stu-id="e4202-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="e4202-199">設定防火牆或 Proxy</span><span class="sxs-lookup"><span data-stu-id="e4202-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="e4202-200">hello 閘道建立輸出連線太[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="e4202-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="e4202-201">您的閘道的 tooprovide proxy 資訊，請參閱[設定 proxy 設定](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/)。</span><span class="sxs-lookup"><span data-stu-id="e4202-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="e4202-202">toocheck 是否您防火牆或 proxy 時，可能會封鎖連線，確認您的電腦是否可以實際連線 toohello 網際網路和 hello [Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="e4202-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="e4202-203">從 PowerShell 命令提示字元中，執行此命令︰</span><span class="sxs-lookup"><span data-stu-id="e4202-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="e4202-204">此命令只會測試網路連線和連線 toohello Azure 服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="e4202-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="e4202-205">因此 hello 命令不會動用 toodo hello 閘道或 hello 閘道器雲端服務加密並儲存您的認證和閘道器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e4202-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="e4202-206">此外，這個命令僅適用於 Windows Server 2012 R2 或更新版本，以及 Windows 8.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e4202-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="e4202-207">在舊的 OS 版本中，您可以使用 Telnet 太測試連線。</span><span class="sxs-lookup"><span data-stu-id="e4202-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="e4202-208">深入了解 [Azure 服務匯流排和混合式解決方案](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="e4202-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="e4202-209">您的結果應該看起來類似 toothis 範例：</span><span class="sxs-lookup"><span data-stu-id="e4202-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="e4202-210">如果**TcpTestSucceeded**未設定太**True**，您可能會被防火牆封鎖。</span><span class="sxs-lookup"><span data-stu-id="e4202-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="e4202-211">如果您想 toobe 完整，以取代 hello **ComputerName**和**連接埠**底下所列的值與 hello 值[設定連接埠](#configure-ports)本主題中。</span><span class="sxs-lookup"><span data-stu-id="e4202-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="e4202-212">hello 防火牆也可能會封鎖連接該 hello Azure 服務匯流排可讓 toohello Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="e4202-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="e4202-213">如果發生這種情況下，請核准 （解除封鎖） 所有 hello 這些資料中心區域中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e4202-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="e4202-214">為 IP 位址， [get hello Azure IP 位址清單這裡](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="e4202-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="e4202-215">設定連接埠</span><span class="sxs-lookup"><span data-stu-id="e4202-215">Configure ports</span></span>

<span data-ttu-id="e4202-216">hello 閘道建立輸出連線太[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)並在輸出連接埠與通訊： TCP 443 （預設）、 5671、 5672、 9350 到 9354。</span><span class="sxs-lookup"><span data-stu-id="e4202-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="e4202-217">hello 閘道不需要輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="e4202-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="e4202-218">深入了解 [Azure 服務匯流排和混合式解決方案](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="e4202-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="e4202-219">網域名稱</span><span class="sxs-lookup"><span data-stu-id="e4202-219">DOMAIN NAMES</span></span> | <span data-ttu-id="e4202-220">輸出連接埠</span><span class="sxs-lookup"><span data-stu-id="e4202-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="e4202-221">描述</span><span class="sxs-lookup"><span data-stu-id="e4202-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e4202-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="e4202-222">*.analysis.windows.net</span></span> | <span data-ttu-id="e4202-223">443</span><span class="sxs-lookup"><span data-stu-id="e4202-223">443</span></span> | <span data-ttu-id="e4202-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e4202-224">HTTPS</span></span> | 
| <span data-ttu-id="e4202-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="e4202-225">*.login.windows.net</span></span> | <span data-ttu-id="e4202-226">443</span><span class="sxs-lookup"><span data-stu-id="e4202-226">443</span></span> | <span data-ttu-id="e4202-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e4202-227">HTTPS</span></span> | 
| <span data-ttu-id="e4202-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e4202-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="e4202-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="e4202-229">5671-5672</span></span> | <span data-ttu-id="e4202-230">進階訊息佇列通訊協定 (AMQP)</span><span class="sxs-lookup"><span data-stu-id="e4202-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="e4202-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e4202-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="e4202-232">443、9350-9354</span><span class="sxs-lookup"><span data-stu-id="e4202-232">443, 9350-9354</span></span> | <span data-ttu-id="e4202-233">透過 TCP 之服務匯流排轉送上的接聽程式 (需要 443 才能取得「存取控制」權杖)</span><span class="sxs-lookup"><span data-stu-id="e4202-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="e4202-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="e4202-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="e4202-235">443</span><span class="sxs-lookup"><span data-stu-id="e4202-235">443</span></span> | <span data-ttu-id="e4202-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e4202-236">HTTPS</span></span> | 
| <span data-ttu-id="e4202-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e4202-237">*.core.windows.net</span></span> | <span data-ttu-id="e4202-238">443</span><span class="sxs-lookup"><span data-stu-id="e4202-238">443</span></span> | <span data-ttu-id="e4202-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e4202-239">HTTPS</span></span> | 
| <span data-ttu-id="e4202-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e4202-240">login.microsoftonline.com</span></span> | <span data-ttu-id="e4202-241">443</span><span class="sxs-lookup"><span data-stu-id="e4202-241">443</span></span> | <span data-ttu-id="e4202-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e4202-242">HTTPS</span></span> | 
| <span data-ttu-id="e4202-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="e4202-243">*.msftncsi.com</span></span> | <span data-ttu-id="e4202-244">443</span><span class="sxs-lookup"><span data-stu-id="e4202-244">443</span></span> | <span data-ttu-id="e4202-245">無法連到 hello Power BI 服務的 hello 閘道時，請使用 tootest 網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="e4202-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="e4202-246">如果您有 tooapprove IP 位址而非 hello 定義域時，您可以下載並使用 hello [Microsoft Azure Datacenter IP 範圍清單](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="e4202-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="e4202-247">在某些情況下，hello Azure 服務匯流排連線的 IP 位址，而不是完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e4202-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="e4202-248">Hello 資料閘道的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="e4202-248">How does hello data gateway work?</span></span>

<span data-ttu-id="e4202-249">hello 資料閘道，協助應用程式邏輯、 hello 閘道器雲端服務和內部部署資料來源之間快速且安全的通訊。</span><span class="sxs-lookup"><span data-stu-id="e4202-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="e4202-251">因此 hello 雲端中的 hello 使用者互動的項目，已連線 tooyour 內部部署資料來源：</span><span class="sxs-lookup"><span data-stu-id="e4202-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="e4202-252">hello 閘道器雲端服務建立查詢，以及加密 hello 認證 hello 資料來源，並傳送嗨閘道 tooprocess hello 查詢 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="e4202-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="e4202-253">hello 閘道器雲端服務會分析 hello 查詢，並將推送 hello 要求 toohello Azure 服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="e4202-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="e4202-254">hello 在內部部署資料閘道會輪詢 hello 適用於 Azure 服務匯流排擱置的要求。</span><span class="sxs-lookup"><span data-stu-id="e4202-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="e4202-255">hello 閘道取得 hello 查詢、 解密 hello 認證，並利用這些認證連接 toohello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="e4202-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="e4202-256">hello 閘道會傳送 hello 查詢 toohello 資料來源執行。</span><span class="sxs-lookup"><span data-stu-id="e4202-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="e4202-257">hello 結果會傳送 hello 資料來源、 回復 toohello 閘道和 toohello 閘道器雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e4202-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="e4202-258">hello 閘道器雲端服務接著會使用 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e4202-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="e4202-259">常見問題集</span><span class="sxs-lookup"><span data-stu-id="e4202-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="e4202-260">一般</span><span class="sxs-lookup"><span data-stu-id="e4202-260">General</span></span>

<span data-ttu-id="e4202-261">**問：**： 我需要閘道 hello 雲端，例如 SQL Azure 中的資料來源嗎？</span><span class="sxs-lookup"><span data-stu-id="e4202-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="e4202-262">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="e4202-262">
**A**: No.</span></span> <span data-ttu-id="e4202-263">閘道正在連接只 tooon 內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="e4202-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="e4202-264">**問：**: hello 閘道是否有 toobe hello 做 hello 資料來源相同電腦上安裝？</span><span class="sxs-lookup"><span data-stu-id="e4202-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="e4202-265">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="e4202-265">
**A**: No.</span></span> <span data-ttu-id="e4202-266">hello 閘道正在連接 toohello 資料來源使用所提供的 hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="e4202-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="e4202-267">Hello 閘道視為用戶端應用程式，這方面。</span><span class="sxs-lookup"><span data-stu-id="e4202-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="e4202-268">hello 閘道只需要 hello 功能 tooconnect toohello 伺服器所提供名稱。</span><span class="sxs-lookup"><span data-stu-id="e4202-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="e4202-269">**問：**： 為什麼必須使用 Azure 的工作或學校帳戶 toosign 中的？</span><span class="sxs-lookup"><span data-stu-id="e4202-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="e4202-270">
**A**： 您只能使用 Azure 的工作或學校帳戶，當您安裝 hello 在內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="e4202-271">登入帳戶會儲存在由 Azure Active Directory (Azure AD) 所管理的租用戶中。</span><span class="sxs-lookup"><span data-stu-id="e4202-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e4202-272">通常，您的 Azure AD 帳戶的使用者主要名稱 (UPN) 符合 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e4202-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="e4202-273">**問**︰我的認證儲存在哪裡？</span><span class="sxs-lookup"><span data-stu-id="e4202-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="e4202-274">
**A**： 您輸入的資料來源的 hello 認證會加密並儲存在 hello 閘道器雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e4202-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="e4202-275">hello 認證會在 hello 在內部部署資料閘道進行解密。</span><span class="sxs-lookup"><span data-stu-id="e4202-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="e4202-276">**問**︰網路頻寬是否有任何需求？</span><span class="sxs-lookup"><span data-stu-id="e4202-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="e4202-277">
**答**︰我們的建議是，您的網路連線要有良好的輸送量。</span><span class="sxs-lookup"><span data-stu-id="e4202-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="e4202-278">每個環境都不同，並傳送資料的 hello 數量會影響 hello 的結果。</span><span class="sxs-lookup"><span data-stu-id="e4202-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="e4202-279">使用 ExpressRoute 有利於 tooguarantee 的內部部署與 hello Azure 資料中心之間的輸送量層級。</span><span class="sxs-lookup"><span data-stu-id="e4202-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="e4202-280">您可以使用您的輸送量 hello 協力廠商工具 Azure Speed Test 應用程式 toohelp 量測計。</span><span class="sxs-lookup"><span data-stu-id="e4202-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="e4202-281">**問：**: hello 延遲執行查詢 tooa 資料來源，從 hello 閘道是什麼？</span><span class="sxs-lookup"><span data-stu-id="e4202-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="e4202-282">Hello 最佳架構為何？</span><span class="sxs-lookup"><span data-stu-id="e4202-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="e4202-283">
**A**: tooreduce 網路延遲，安裝 hello 閘道為盡可能關閉 toohello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="e4202-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="e4202-284">您可以安裝 hello 閘道 hello 實際的資料來源上，如果此相近延遲降至最低 hello 導入。</span><span class="sxs-lookup"><span data-stu-id="e4202-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="e4202-285">太考慮 hello 資料中心。</span><span class="sxs-lookup"><span data-stu-id="e4202-285">Consider hello datacenters too.</span></span> <span data-ttu-id="e4202-286">例如，如果您的服務會使用 hello 美國西部的資料中心，而且您的 Azure VM 中裝載 SQL Server，Azure VM 應該在 hello 美國西部太。</span><span class="sxs-lookup"><span data-stu-id="e4202-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="e4202-287">此接近延遲降至最低，並避免 hello Azure VM 的輸出流量費用。</span><span class="sxs-lookup"><span data-stu-id="e4202-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="e4202-288">**問：**： 的結果傳送後 toohello 雲端方式？</span><span class="sxs-lookup"><span data-stu-id="e4202-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="e4202-289">
**A**: hello Azure Service Bus 透過傳送結果。</span><span class="sxs-lookup"><span data-stu-id="e4202-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="e4202-290">**問：**： 是否有任何輸入的連線 toohello 閘道在 hello 雲端？</span><span class="sxs-lookup"><span data-stu-id="e4202-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="e4202-291">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="e4202-291">
**A**: No.</span></span> <span data-ttu-id="e4202-292">hello 閘道會使用輸出連線 tooAzure Service Bus。</span><span class="sxs-lookup"><span data-stu-id="e4202-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="e4202-293">**問**︰如果我封鎖輸出連線會如何？</span><span class="sxs-lookup"><span data-stu-id="e4202-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="e4202-294">怎麼我需要 tooopen？</span><span class="sxs-lookup"><span data-stu-id="e4202-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="e4202-295">
**A**: hello 連接埠和主控件以 hello 閘道使用，請參閱。</span><span class="sxs-lookup"><span data-stu-id="e4202-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="e4202-296">**問：**: hello 實際的 Windows 服務稱為？</span><span class="sxs-lookup"><span data-stu-id="e4202-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="e4202-297">
**A**: hello 閘道呼叫 Power BI Enterprise Gateway 服務在 [服務]。</span><span class="sxs-lookup"><span data-stu-id="e4202-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="e4202-298">**問：**： 可以 hello 使用 Azure Active Directory 帳戶來執行閘道 Windows 服務嗎？</span><span class="sxs-lookup"><span data-stu-id="e4202-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="e4202-299">
**答**：否。</span><span class="sxs-lookup"><span data-stu-id="e4202-299">
**A**: No.</span></span> <span data-ttu-id="e4202-300">hello Windows 服務必須有有效的 Windows 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4202-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="e4202-301">根據預設，hello 服務會以 hello 服務 SID NT SERVICE\PBIEgwService 執行。</span><span class="sxs-lookup"><span data-stu-id="e4202-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="e4202-302">高可用性和災害復原</span><span class="sxs-lookup"><span data-stu-id="e4202-302">High availability and disaster recovery</span></span>

<span data-ttu-id="e4202-303">**問**︰災害復原有哪些選項？</span><span class="sxs-lookup"><span data-stu-id="e4202-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="e4202-304">
**A**： 您可以使用 hello 修復金鑰 toorestore 或移動閘道。</span><span class="sxs-lookup"><span data-stu-id="e4202-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="e4202-305">當您安裝 hello 閘道時，指定 hello 修復金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4202-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="e4202-306">**問：**: hello hello 修復金鑰的優點為何？</span><span class="sxs-lookup"><span data-stu-id="e4202-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="e4202-307">
**A**: hello 修復金鑰提供方式 toomigrate 或損毀狀況之後復原您的閘道設定。</span><span class="sxs-lookup"><span data-stu-id="e4202-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="e4202-308">**問：**： 是否有任何的計劃，以啟用高可用性案例的 hello 閘道？</span><span class="sxs-lookup"><span data-stu-id="e4202-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="e4202-309">
**A**： 這些案例在 hello 藍圖上，但我們尚未時間軸。</span><span class="sxs-lookup"><span data-stu-id="e4202-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e4202-310">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e4202-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="e4202-311">**問：**： 如何查看哪些查詢會傳送 toohello 在內部部署資料來源嗎？</span><span class="sxs-lookup"><span data-stu-id="e4202-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="e4202-312">
**A**： 您可以啟用查詢追蹤，其中包括傳送嗨查詢。</span><span class="sxs-lookup"><span data-stu-id="e4202-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="e4202-313">請記住 toochange 查詢後追蹤 toohello 完成疑難排解後的原始值。</span><span class="sxs-lookup"><span data-stu-id="e4202-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="e4202-314">讓查詢追蹤保持開啟會產生較大的記錄。</span><span class="sxs-lookup"><span data-stu-id="e4202-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="e4202-315">您也可以查看資料來源具備的工具是否有追蹤查詢。</span><span class="sxs-lookup"><span data-stu-id="e4202-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="e4202-316">例如，您可以使用 SQL Server 和 Analysis Services 的擴充事件或 SQL Profiler。</span><span class="sxs-lookup"><span data-stu-id="e4202-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="e4202-317">**問：**： 所在 hello 閘道記錄檔？</span><span class="sxs-lookup"><span data-stu-id="e4202-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="e4202-318">
**答**：請參閱本主題稍後的「工具」。</span><span class="sxs-lookup"><span data-stu-id="e4202-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="e4202-319">更新 toohello 最新版本</span><span class="sxs-lookup"><span data-stu-id="e4202-319">Update toohello latest version</span></span>

<span data-ttu-id="e4202-320">Hello 閘道器版本過期時，就會出現許多問題。</span><span class="sxs-lookup"><span data-stu-id="e4202-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="e4202-321">良好一般做法，請確定您使用 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="e4202-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="e4202-322">如果您超過一個月或更久沒有更新 hello 閘道，您可能會考慮安裝 hello hello 閘道最新版本，並查看可否重現 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="e4202-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="e4202-323">錯誤： 無法 tooadd 使用者 toogroup。</span><span class="sxs-lookup"><span data-stu-id="e4202-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="e4202-324">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="e4202-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="e4202-325">如果您嘗試 tooinstall hello 閘道不支援的網域控制站上，您可能會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="e4202-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="e4202-326">請確定您部署的 hello 閘道不是網域控制站的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e4202-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="e4202-327">工具</span><span class="sxs-lookup"><span data-stu-id="e4202-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="e4202-328">從 hello 閘道 configurer 收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="e4202-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="e4202-329">您可以收集 hello 閘道的數個記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e4202-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="e4202-330">一律與 hello 記錄檔開始 ！</span><span class="sxs-lookup"><span data-stu-id="e4202-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="e4202-331">安裝程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="e4202-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="e4202-332">組態記錄檔</span><span class="sxs-lookup"><span data-stu-id="e4202-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="e4202-333">企業閘道服務記錄檔</span><span class="sxs-lookup"><span data-stu-id="e4202-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="e4202-334">事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="e4202-334">Event logs</span></span>

<span data-ttu-id="e4202-335">您可以找到 hello 下的資料管理閘道器和 PowerBIGateway 記錄**Application and Services Logs**。</span><span class="sxs-lookup"><span data-stu-id="e4202-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="e4202-336">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="e4202-336">Fiddler Trace</span></span>

<span data-ttu-id="e4202-337">[Fiddler](http://www.telerik.com/fiddler) 是一個 Telerik 公司開發，用來監視 HTTP 流量的免費工具。</span><span class="sxs-lookup"><span data-stu-id="e4202-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="e4202-338">您可以看到這個流量以 hello hello 用戶端電腦從 Power BI 服務。</span><span class="sxs-lookup"><span data-stu-id="e4202-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="e4202-339">此服務可能會顯示錯誤和其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e4202-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4202-340">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4202-340">Next steps</span></span>
    
* [<span data-ttu-id="e4202-341">邏輯應用程式從連接 tooon 內部部署資料</span><span class="sxs-lookup"><span data-stu-id="e4202-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="e4202-342">企業整合功能</span><span class="sxs-lookup"><span data-stu-id="e4202-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="e4202-343">適用於 Azure Logic Apps 的連接器</span><span class="sxs-lookup"><span data-stu-id="e4202-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
