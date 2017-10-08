---
title: "aaaAzure 角色屬性"
description: "了解 toouse hello Azure Toolkit for Eclipse tooconfigure Azure 角色設定的方式。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a><span data-ttu-id="5c444-103">Azure 角色屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-103">Azure Role Properties</span></span>
<span data-ttu-id="5c444-104">您的 Azure 角色的各種組態設定可以設定 hello Azure Toolkit for Eclipse 內。</span><span class="sxs-lookup"><span data-stu-id="5c444-104">Various configuration settings for your Azure role can be set within hello Azure Toolkit for Eclipse.</span></span>

## <a name="configuring-azure-role-properties"></a><span data-ttu-id="5c444-105">設定 Azure 角色屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-105">Configuring Azure Role Properties</span></span>
<span data-ttu-id="5c444-106">透過背景工作角色的 hello 屬性對話方塊，來完成設定您的 Azure 角色屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-106">Configuring your Azure Role Properties is accomplished through hello property dialogs for your worker role.</span></span> <span data-ttu-id="5c444-107">開啟 hello 內容功能表上的 Eclipse 的專案總管 窗格中選取 hello hello 角色**Azure**子功能表。</span><span class="sxs-lookup"><span data-stu-id="5c444-107">Open hello context menu for hello role in Eclipse's Project Explorer pane and select hello **Azure** sub-menu.</span></span> <span data-ttu-id="5c444-108">（如果您沒有看到 hello 角色 hello Eclipse [專案總管] 中的，展開 [專案總管] 中的 Azure 專案）。</span><span class="sxs-lookup"><span data-stu-id="5c444-108">(If you don't see hello role in hello Eclipse Project Explorer, expand your Azure project in Project Explorer.)</span></span>

![][ic789599]

<span data-ttu-id="5c444-109">hello hello 可設定的各種屬性**屬性**對話方塊以本主題所述。</span><span class="sxs-lookup"><span data-stu-id="5c444-109">hello various properties that can be set from hello **Properties** dialogs are described in this topic.</span></span> <span data-ttu-id="5c444-110">要注意的是，在您建立新的 Azure 部署專案時，系統會自動填入其中的許多屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-110">Note that many properties are filled in automatically when you create a new Azure deployment project.</span></span>

<span data-ttu-id="5c444-111">下列屬性頁的 hello 可供 Azure 角色。</span><span class="sxs-lookup"><span data-stu-id="5c444-111">hello following property pages are available for Azure roles.</span></span>

* [<span data-ttu-id="5c444-112">虛擬機器屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-112">Virtual machine properties</span></span>](#virtual_machine_properties)
* [<span data-ttu-id="5c444-113">快取屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-113">Caching properties</span></span>](#caching_properties)
* [<span data-ttu-id="5c444-114">憑證屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-114">Certificates properties</span></span>](#certificates_properties)
* [<span data-ttu-id="5c444-115">元件屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-115">Components properties</span></span>](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [<span data-ttu-id="5c444-116">端點屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-116">Endpoints properties</span></span>](#endpoints_properties)
* [<span data-ttu-id="5c444-117">環境變數屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-117">Environment variables properties</span></span>](#environment_variables_properties)
* [<span data-ttu-id="5c444-118">負載平衡/工作階段親和性 (也稱為「黏性工作階段」) 屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-118">Load balancing / session affinity (a.k.a "sticky sessions") properties</span></span>](#session_affinity_properties)
* [<span data-ttu-id="5c444-119">本機儲存體屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-119">Local storage properties</span></span>](#local_storage_properties)
* [<span data-ttu-id="5c444-120">伺服器組態屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-120">Server configuration properties</span></span>](#server_configuration_properties)
* [<span data-ttu-id="5c444-121">SSL 卸載屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-121">SSL offloading properties</span></span>](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a><span data-ttu-id="5c444-122">虛擬機器屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-122">Virtual machine properties</span></span>
<span data-ttu-id="5c444-123">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**屬性**，，而且您將擁有 hello 能力 toochange hello 虛擬機器大小，也會變更hello 執行個體數目、 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="5c444-123">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Properties**, and you will have hello ability toochange hello virtual machine size, and also change hello number of instances, as shown in hello following image.</span></span>

![][ic719499]

> [!NOTE]
> <span data-ttu-id="5c444-124">僅限 Windows： 當您將執行個體數目 hello tooa 值大於 1，您也可以設定應用程式伺服器 hello toolkit 將允許只有 1 的角色執行個體 toorun 在 hello 模擬器中，不論此設定為何。</span><span class="sxs-lookup"><span data-stu-id="5c444-124">Windows only: when you set hello number of instances tooa value greater than 1 and you also configure an application server, hello toolkit will allow only 1 role instance toorun in hello emulator, regardless of this setting.</span></span> <span data-ttu-id="5c444-125">這是 tooavoid 連接埠繫結衝突 hello 不同的伺服器執行個體 (例如，所有嘗試 toobind tooport 8080) 之間執行上 hello 時相同的電腦。</span><span class="sxs-lookup"><span data-stu-id="5c444-125">This is tooavoid port binding conflicts between hello different server instances (for example, all trying toobind tooport 8080) when they run on hello same computer.</span></span> <span data-ttu-id="5c444-126">設定您想要的執行個體計數會保留，但只有在您部署 toohello 雲端時，才會生效。</span><span class="sxs-lookup"><span data-stu-id="5c444-126">Your desired instance count setting is preserved, but it goes into effect only when you deploy toohello cloud.</span></span>
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a><span data-ttu-id="5c444-127">快取屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-127">Caching properties</span></span>
<span data-ttu-id="5c444-128">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**快取**。</span><span class="sxs-lookup"><span data-stu-id="5c444-128">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Caching**.</span></span> <span data-ttu-id="5c444-129">在這個對話方塊中，您可以啟用具名共置的 memcache 相容快取，可讓您 web 應用程式設定的 toohelp 速度。</span><span class="sxs-lookup"><span data-stu-id="5c444-129">Within this dialog, you can enable named co-located memcache-compatible caches, allowing you toohelp speed up your web applications.</span></span>

![][ic719483]

<span data-ttu-id="5c444-130">在 hello**快取**屬性頁面中，您可以指定下列的 hello 的全域設定：</span><span class="sxs-lookup"><span data-stu-id="5c444-130">Within hello **Caching** property page, you can specify global settings for hello following:</span></span>

* <span data-ttu-id="5c444-131">是否啟用共置快取。</span><span class="sxs-lookup"><span data-stu-id="5c444-131">whether co-located caching is enabled.</span></span>
* <span data-ttu-id="5c444-132">hello 快取大小之記憶體的百分比。</span><span class="sxs-lookup"><span data-stu-id="5c444-132">hello cache size as a percent of memory.</span></span>
* <span data-ttu-id="5c444-133">如果您不想要讓 toosave hello 快取狀態為雲端服務，或無執行應用程式時儲存 hello 快取狀態的 hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5c444-133">hello storage account name for saving hello cache state when your application runs as a cloud service, or none if you do not want toosave hello cache state.</span></span> <span data-ttu-id="5c444-134">（hello 儲存體帳戶名稱不是使用 hello 計算模擬器中執行您的應用程式時）。如果您將設定 hello 儲存體帳戶名稱太**（自動）** （此為 hello 預設值），快取組態會自動使用 hello 相同儲存體帳戶，因為您在 hello 中選取一個 hello**發行 tooAzure**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-134">(hello storage account name is not used when you run your application in hello compute emulator.) If you set hello storage account name too**(auto)** (which is hello default), your caching configuration will automatically use hello same storage account as hello one you select in hello **Publish tooAzure** dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="5c444-135">hello **（自動）**設定會影響 hello 預期只有當您發行您的部署使用 hello Eclipse 工具組的發行精靈。</span><span class="sxs-lookup"><span data-stu-id="5c444-135">hello **(auto)** setting will have hello desired effect only if you publish your deployment using hello Eclipse toolkit's publish wizard.</span></span> <span data-ttu-id="5c444-136">如果您改為發行 hello.cspkg 檔案，以手動方式使用外部機制，例如 hello [Azure 管理入口網站][Azure Management Portal]，hello 部署將無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="5c444-136">If instead you publish hello .cspkg file manually using an external mechanism, such as hello [Azure Management Portal][Azure Management Portal], hello deployment will not function properly.</span></span>
> 
> 

<span data-ttu-id="5c444-137">hello 下列對話方塊顯示一個快取的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-137">hello following dialog shows hello properties for a cache.</span></span>

![][ic719501]

* <span data-ttu-id="5c444-138">**名稱：** hello hello 名稱共置快取。</span><span class="sxs-lookup"><span data-stu-id="5c444-138">**Name:** hello name of hello co-located cache.</span></span>
* <span data-ttu-id="5c444-139">**連接埠號碼：** hello hello 快取的連接埠號碼 toouse。</span><span class="sxs-lookup"><span data-stu-id="5c444-139">**Port number:** hello port number toouse for hello cache.</span></span>
* <span data-ttu-id="5c444-140">**到期原則：** hello 下列值，指定何時到期 hello 快取中的索引鍵的其中一個。</span><span class="sxs-lookup"><span data-stu-id="5c444-140">**Expiration policy:** One of hello following values that specifies when a key in hello cache expires.</span></span>
  * <span data-ttu-id="5c444-141">**絕對值：** hello 金鑰到期時所指定的 hello 時間**分鐘 toolive**為止。</span><span class="sxs-lookup"><span data-stu-id="5c444-141">**Absolute:** hello key expires when hello time specified by **Minutes toolive** is reached.</span></span>
  * <span data-ttu-id="5c444-142">**NeverExpires:** hello 金鑰沒有到期時間。</span><span class="sxs-lookup"><span data-stu-id="5c444-142">**NeverExpires:** hello key does not have an expiration time.</span></span>
  * <span data-ttu-id="5c444-143">**SlidingWindow:** hello 金鑰到期，如果未存取所指定的時間量 hello**分鐘 toolive**; 每次存取時，hello 到期時鐘會重設。</span><span class="sxs-lookup"><span data-stu-id="5c444-143">**SlidingWindow:** hello key expires if it has not been accessed for hello amount of time specified by **Minutes toolive**; each time it is accessed, hello expiration clock is reset.</span></span>
* <span data-ttu-id="5c444-144">**分鐘 toolive:**最大分鐘數的金鑰存活 toolive，主旨 toohello 到期原則。</span><span class="sxs-lookup"><span data-stu-id="5c444-144">**Minutes toolive:** Maximum number of minutes for a memcached key toolive, subject toohello expiration policy.</span></span>
* <span data-ttu-id="5c444-145">**在不同角色執行個體上複寫備份以提供高可用性：** 啟用時，有助於利用在不同角色執行個體上複寫備份以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="5c444-145">**High availability with replicated backups on different role instances:** If enabled, helps provide high availability utilizing replicated backups on different role instances.</span></span> <span data-ttu-id="5c444-146">請注意這項功能 toowork 您部署至少兩個角色執行個體必須作用中。</span><span class="sxs-lookup"><span data-stu-id="5c444-146">Note that at least two role instances must be in effect for your deployment for this feature toowork.</span></span>

<span data-ttu-id="5c444-147">tooadd 新的快取中，按一下 hello**新增**按鈕在 hello**快取**屬性頁和**設定具名快取**隨即會開啟對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-147">tooadd a new cache, click hello **Add** button in hello **Caching** property page, and a **Configure Named Cache** dialog will be opened.</span></span> <span data-ttu-id="5c444-148">提供為上述 hello 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="5c444-148">Provide values for hello properties which are described above.</span></span>

<span data-ttu-id="5c444-149">toomodify 具名快取中，選取 hello 快取，然後按一下 hello**編輯**按鈕在 hello**快取**屬性頁。</span><span class="sxs-lookup"><span data-stu-id="5c444-149">toomodify a named cache, select hello cache and click hello **Edit** button in hello **Caching** property page.</span></span> <span data-ttu-id="5c444-150">隨即會開啟對話方塊允許您 toomodify hello 快取屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-150">A dialog will be opened allowing you toomodify hello cache properties.</span></span> <span data-ttu-id="5c444-151">按**確定**toosave hello 快取值。</span><span class="sxs-lookup"><span data-stu-id="5c444-151">Press **OK** toosave hello cache values.</span></span>

<span data-ttu-id="5c444-152">toodelete 快取中，選取 hello 快取，然後按一下 hello**移除**按鈕在 hello**快取**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="5c444-152">toodelete a cache, select hello cache and click hello **Remove** button in hello **Caching** property page, and then click **Yes** tooconfirm hello deletion.</span></span>

<span data-ttu-id="5c444-153">如需有關如何 toouse 快取，請參閱[tooUse 共置於快取][How tooUse Co-located Caching]。</span><span class="sxs-lookup"><span data-stu-id="5c444-153">For more information on how toouse caching, see [How tooUse Co-located Caching][How tooUse Co-located Caching].</span></span>

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a><span data-ttu-id="5c444-154">憑證屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-154">Certificates properties</span></span>
<span data-ttu-id="5c444-155">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**憑證**。</span><span class="sxs-lookup"><span data-stu-id="5c444-155">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Certificates**.</span></span>

![][ic710964]

<span data-ttu-id="5c444-156">在這個對話方塊中，您可以新增或移除 Eclipse 專案所參考的憑證。</span><span class="sxs-lookup"><span data-stu-id="5c444-156">Within this dialog, you can add or remove certificates referenced by your Eclipse project.</span></span> <span data-ttu-id="5c444-157">請注意，此處所列的 hello 憑證並不會自動儲存於任何 Java 金鑰存放區，因此不會自動使用於任何從 Java 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5c444-157">Note that hello certificates listed here are not automatically stored inside any Java keystore, and therefore are not automatically available for any use from within a Java application.</span></span> <span data-ttu-id="5c444-158">它們只會向 Azure，以便它們可以由其他 Windows 軟體預先載入至 hello Windows 憑證存放區上執行您的部署的 hello 虛擬機器和後續使用。</span><span class="sxs-lookup"><span data-stu-id="5c444-158">They are only registered with Azure so that they can be preloaded into hello Windows certificate store on hello virtual machines running your deployment and subsequently used by other Windows software.</span></span> <span data-ttu-id="5c444-159">目前，hello 功能 hello 工具組使用 hello 憑證參考 hello 這種方式只**憑證**對話是[SSL 卸載][SSL Offloading]，由於 tooits網際網路資訊服務 (IIS) 和應用程式要求路由 (ARR)，需要依賴 hello 以這種方式提供適當的憑證 toobe。</span><span class="sxs-lookup"><span data-stu-id="5c444-159">Currently, hello only feature of hello toolkit that uses hello certificates referenced this way in hello **Certificates** dialog is [SSL Offloading][SSL Offloading], due tooits reliance on Internet Information Services (IIS) and Application Request Routing (ARR), which require hello proper certificate toobe made available in this manner.</span></span>

<span data-ttu-id="5c444-160">當您部署您的專案 tooAzure 使用 hello 發行精靈時，您將無法在 hello 個人資訊交換 (PFX) 檔案對應 toothese 憑證，以及他們的密碼，順序 tooautomatically 上載 toohello 提示的 toopointAzure 服務，但前提是它們不已上傳那里先前。</span><span class="sxs-lookup"><span data-stu-id="5c444-160">When you deploy your project tooAzure using hello Publish wizard, you will be prompted toopoint at hello Personal Information Exchange (PFX) files corresponding toothese certificates, along with their passwords, in order tooautomatically upload them toohello Azure service, but only if they have not been uploaded there previously.</span></span>

<a name="components_properties"></a> 

### <a name="components-properties"></a><span data-ttu-id="5c444-161">元件屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-161">Components properties</span></span>
<span data-ttu-id="5c444-162">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**元件**。</span><span class="sxs-lookup"><span data-stu-id="5c444-162">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Components**.</span></span> <span data-ttu-id="5c444-163">在這個對話方塊中，您擁有 hello 能力 tooadd、 修改或移除 hello 元件的角色，以及變更 hello 順序處理的。</span><span class="sxs-lookup"><span data-stu-id="5c444-163">Within this dialog, you have hello ability tooadd, modify, or remove hello components of your role, as well as change hello order in which they are processed.</span></span>

![][ic719502]

<span data-ttu-id="5c444-164">hello 元件功能可讓您 tooadd 相依性 tooyour Azure 部署專案中，例如 Java 應用程式專案、 特殊的檔案和可執行的命令列陳述式所需的部署。</span><span class="sxs-lookup"><span data-stu-id="5c444-164">hello components feature enables you tooadd dependencies tooyour Azure deployment project, such as Java application projects, special files, and executable command line statements that are needed by your deployment.</span></span>

<span data-ttu-id="5c444-165">針對每個元件，您可以指定：</span><span class="sxs-lookup"><span data-stu-id="5c444-165">For each component, you can specify:</span></span>

* <span data-ttu-id="5c444-166">hello 時將您的 Azure 部署專案匯入 hello 元件，會在建立時所採取的步驟 toobe。</span><span class="sxs-lookup"><span data-stu-id="5c444-166">hello step toobe taken when importing hello component into your Azure deployment project when it is built.</span></span>
* <span data-ttu-id="5c444-167">hello 部署 hello Azure 雲端中的元件時所採取的步驟 toobe。</span><span class="sxs-lookup"><span data-stu-id="5c444-167">hello step toobe taken when deploying that component in hello Azure cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="5c444-168">當指定元件的檔案或命令列，請記住您的部署將會發行的 tooa Windows 虛擬機器，因此您自訂的步驟必須適用於 windows 的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5c444-168">When specifying component files or command lines, keep in mind that your deployment will be published tooa Windows virtual machine, so your custom steps must be valid for a Windows-based operating system.</span></span> 
> 
> 

<span data-ttu-id="5c444-169">元件有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="5c444-169">Components have hello following properties:</span></span>

* <span data-ttu-id="5c444-170">**匯入：**指出 hello 元件如何將匯入 hello 專案 hello 專案建立時的方法。</span><span class="sxs-lookup"><span data-stu-id="5c444-170">**Import:** Method that indicates how hello component will be imported into hello project when hello project is built.</span></span> <span data-ttu-id="5c444-171">這可以是 hello 的下列值的其中一個：</span><span class="sxs-lookup"><span data-stu-id="5c444-171">This can be one of hello following values:</span></span>
  * <span data-ttu-id="5c444-172">**複製：** hello 元件會從指定 hello hello 本機路徑複製**從**成 hello 角色屬性**approot**目錄。</span><span class="sxs-lookup"><span data-stu-id="5c444-172">**copy:** hello component is copied from hello local path specified by hello **From** property into hello role's **approot** directory.</span></span>
  * <span data-ttu-id="5c444-173">**EAR:** hello 元件是 Java 企業封存檔 (EAR) 從在 hello hello 所指定的本機路徑企業應用程式專案匯入**從**屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-173">**EAR:** hello component is a Java enterprise archive (EAR) imported from an Enterprise Application Project at hello local path specified by hello **From** property.</span></span> <span data-ttu-id="5c444-174">（這是自動偵測 hello hello hello 專案，在該位置的性質為基礎的工具組）。</span><span class="sxs-lookup"><span data-stu-id="5c444-174">(This is detected automatically by hello toolkit based on hello nature of hello project at that location).</span></span>
  * <span data-ttu-id="5c444-175">**JAR:** hello 元件是 Java 封存檔 (JAR)，從指定 hello hello 本機路徑上的 Java 專案匯入**從**屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-175">**JAR:** hello component is a Java archive (JAR) and is imported from a Java project at hello local path specified by hello **From** property.</span></span> <span data-ttu-id="5c444-176">（這是自動偵測 hello hello hello 專案，在該位置的性質為基礎的工具組）。</span><span class="sxs-lookup"><span data-stu-id="5c444-176">(This is detected automatically by hello toolkit based on hello nature of hello project at that location).</span></span>
  * <span data-ttu-id="5c444-177">**none:** tooimport hello 元件會採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="5c444-177">**none:** No action is taken tooimport hello component.</span></span> <span data-ttu-id="5c444-178">這是適用於當 hello 元件被假設 tooalready 會出現在 hello 角色**approot**目錄中，或 hello 元件時只可執行的命令列陳述式，如中所指定的 hello **為**屬性時 hello**部署**方法**exec**。</span><span class="sxs-lookup"><span data-stu-id="5c444-178">This is applicable when hello component is assumed tooalready be present in hello role's **approot** directory, or when hello component is merely an executable command line statement, as specified in hello **As** property when hello **Deploy** method is **exec**.</span></span>
  * <span data-ttu-id="5c444-179">**WAR:** hello 元件是 Java web 應用程式封存檔 (WAR)，並且在 hello hello 所指定的本機路徑動態 Web 專案從匯入**從**屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-179">**WAR:** hello component is a Java web application archive (WAR) and is imported from a Dynamic Web Project at hello local path specified by hello **From** property.</span></span> <span data-ttu-id="5c444-180">（這是自動偵測 hello hello hello 專案，在該位置的性質為基礎的工具組）。</span><span class="sxs-lookup"><span data-stu-id="5c444-180">(This is detected automatically by hello toolkit based on hello nature of hello project at that location).</span></span>
  * <span data-ttu-id="5c444-181">**zip:** hello 元件是 zip 檔案，匯入壓縮 hello 目錄或檔案由 hello**從**屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-181">**zip:** hello component is a zip file and is imported by zipping hello directory or file specified by hello **From** property.</span></span>
* <span data-ttu-id="5c444-182">**從：**上您的本機電腦 toohello 資料夾或代表 hello 的項目 tooimport tooyour 部署檔案的來源路徑。</span><span class="sxs-lookup"><span data-stu-id="5c444-182">**From:** Source path on your local machine toohello folder or file that represents hello item(s) tooimport tooyour deployment.</span></span> <span data-ttu-id="5c444-183">此屬性可以使用 Windows 環境變數。</span><span class="sxs-lookup"><span data-stu-id="5c444-183">Windows environment variables can be used in this property.</span></span> <span data-ttu-id="5c444-184">所有匯入元件都會匯入 hello 角色**approot** hello 專案建立時的目錄。</span><span class="sxs-lookup"><span data-stu-id="5c444-184">All importable components will be imported into hello role's **approot** directory when hello project is built.</span></span>
  
    <span data-ttu-id="5c444-185">請注意，您有 hello 能力 toodeploy 元件從下載部署 toohello 雲端 （而非 hello 計算模擬器） 時。</span><span class="sxs-lookup"><span data-stu-id="5c444-185">Note that you have hello ability toodeploy a component from a download when deploying toohello cloud (not hello compute emulator).</span></span> <span data-ttu-id="5c444-186">請參閱以下有關新增元件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5c444-186">See related information below about adding a component.</span></span>    
* <span data-ttu-id="5c444-187">**做為：**檔案名稱下的 hello 元件將會匯入 hello 角色**approot**目錄，以及最後部署 hello Azure 雲端中。</span><span class="sxs-lookup"><span data-stu-id="5c444-187">**As:** File name under which hello component will be imported into hello role's **approot** directory and ultimately deployed in hello Azure cloud.</span></span> <span data-ttu-id="5c444-188">保留此屬性空白 tookeep hello hello 本機電腦也是一樣，因為它的名稱 hello。</span><span class="sxs-lookup"><span data-stu-id="5c444-188">Leave this property blank tookeep hello name hello same as it is on hello local machine.</span></span> <span data-ttu-id="5c444-189">(可執行檔元件，也就是指**部署**方法設定得**exec**，這可以是任意的 Windows 命令列陳述式。)</span><span class="sxs-lookup"><span data-stu-id="5c444-189">(For executable components, that is, those whose **Deploy** method is set too**exec**, this can be an arbitrary Windows command line statement.)</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="5c444-190">如果您使用此值的空格字元，它們將會以不同方式處理 hello 根據部署方法。</span><span class="sxs-lookup"><span data-stu-id="5c444-190">If you use space characters for this value, they will be handled differently depending on hello deploy method.</span></span> <span data-ttu-id="5c444-191">如果 hello 部署方法**exec**，空格會被解譯為命令列引數分隔符號而非 hello 檔案名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="5c444-191">If hello deploy method is **exec**, spaces will be interpreted as command line argument separators and not as part of hello file name.</span></span> <span data-ttu-id="5c444-192">如需所有其他部署方法，空格會被解譯為 hello 檔案名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="5c444-192">For all other deploy methods, spaces will be interpreted as part of hello file name.</span></span>
  > 
  > 
* <span data-ttu-id="5c444-193">**部署：** hello 部署啟動時，指出 hello 動作方法會套用 toohello 元件。</span><span class="sxs-lookup"><span data-stu-id="5c444-193">**Deploy:** Method that indicates hello action applied toohello component when hello deployment is started.</span></span> <span data-ttu-id="5c444-194">這可以是 hello 的下列值的其中一個：</span><span class="sxs-lookup"><span data-stu-id="5c444-194">This can be one of hello following values:</span></span>
  
  * <span data-ttu-id="5c444-195">**複製：** hello 元件會複製的 toohello hello 所指定的目的地路徑**至**屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-195">**copy:** hello component is copied toohello destination path specified by hello **To** property.</span></span>
  * <span data-ttu-id="5c444-196">**exec:** hello 元件是 hello hello hello 所指定的路徑內容中執行的可執行檔 Windows 命令列陳述式**至**屬性，在 hello hello 部署開始的時間。</span><span class="sxs-lookup"><span data-stu-id="5c444-196">**exec:** hello component is an executable Windows command line statement executed in hello context of hello path specified by hello **To** property, at hello time hello deployment starts.</span></span>
  * <span data-ttu-id="5c444-197">**none:**採取任何動作時，才能套用的 toohello 元件 hello 部署開始。</span><span class="sxs-lookup"><span data-stu-id="5c444-197">**none:** No action is applied toohello component when hello deployment starts.</span></span>
  * <span data-ttu-id="5c444-198">**zip:** hello 元件會解壓縮的 toohello hello 所指定的目的地路徑**至**屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-198">**zip:** hello component is unzipped toohello destination path specified by hello **To** property.</span></span> <span data-ttu-id="5c444-199">這個方法是之後才可使用 hello**匯入**屬性是**zip**。</span><span class="sxs-lookup"><span data-stu-id="5c444-199">This method is available only when hello **Import** property is **zip**.</span></span>
* <span data-ttu-id="5c444-200">**成為：** hello hello 元件將會部署的虛擬機器上的目的地路徑。</span><span class="sxs-lookup"><span data-stu-id="5c444-200">**To:** Destination path on hello virtual machine where hello component will be deployed.</span></span> <span data-ttu-id="5c444-201">Windows 環境變數可以用於這個屬性，且檔案路徑的相對太**approot**。</span><span class="sxs-lookup"><span data-stu-id="5c444-201">Windows environment variables can be used in this property, and file paths are relative too**approot**.</span></span>

<span data-ttu-id="5c444-202">tooadd 新元件，請按一下 hello**新增**按鈕在 hello**元件**屬性頁和**Azure 角色元件**隨即會開啟對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-202">tooadd a new component, click hello **Add** button in hello **Components** property page, and an **Azure Role Component** dialog will be opened.</span></span> <span data-ttu-id="5c444-203">提供為上述 hello 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="5c444-203">Provide values for hello properties which are described above.</span></span> 

<span data-ttu-id="5c444-204">hello 以下顯示新增 WAR 元件的範例。</span><span class="sxs-lookup"><span data-stu-id="5c444-204">hello following shows an example for adding a new WAR component.</span></span>

![][ic719503]

<span data-ttu-id="5c444-205">當部署 toohello 雲端 （而非 hello 計算模擬器），如果您希望 toodeploy hello 元件從下載，請確認**從部署在雲端，而不是在 hello 封裝內包含**已核取。</span><span class="sxs-lookup"><span data-stu-id="5c444-205">When deploying toohello cloud (not hello compute emulator), if you want toodeploy hello component from a download, ensure that **When in cloud, instead of including in hello package, deploy from** is checked.</span></span> <span data-ttu-id="5c444-206">如果您想 toodownload 從您的 Azure 儲存體帳戶時，選取 hello 儲存體帳戶從 hello**儲存體帳戶**下拉式清單 (您可以按一下 hello**帳戶**連結 toomodify 功能的 hello 清單)，這會填入在 hello **URL**欄位，然後填入 hello 剩餘 hello URL 的部分。</span><span class="sxs-lookup"><span data-stu-id="5c444-206">If you want toodownload from your Azure storage account, select hello storage account from hello **Storage account** drop-down list (you can click hello **Accounts** link toomodify what is in hello list), which will partially fill in hello **URL** field, and then fill in hello remaining portion of hello URL.</span></span> <span data-ttu-id="5c444-207">如果您不想 toouse Azure 儲存體，請選取**（無）**從 hello**儲存體帳戶**下拉式清單，然後輸入 hello hello URL tooyour 元件**URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="5c444-207">If you do not want toouse Azure storage, select **(none)** from hello **Storage account** drop-down list, and enter hello URL tooyour component in hello **URL** field.</span></span> <span data-ttu-id="5c444-208">指定其中一個 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="5c444-208">Specify one of hello following methods:</span></span>

* <span data-ttu-id="5c444-209">**複製：** hello 下載元件會複製的 toohello hello 所指定的目的地路徑**tooDirectory**路徑。</span><span class="sxs-lookup"><span data-stu-id="5c444-209">**copy:** hello download component is copied toohello destination path specified by hello **tooDirectory** path.</span></span>
* <span data-ttu-id="5c444-210">**相同：** hello 使用相同的方法**從下載部署**與**從封裝部署**。</span><span class="sxs-lookup"><span data-stu-id="5c444-210">**same:** hello same method used for **Deploy from download** as for **Deploy from package**.</span></span>
* <span data-ttu-id="5c444-211">**zip:** hello 下載元件會解壓縮的 toohello hello 所指定的目的地路徑**tooDirectory**路徑。</span><span class="sxs-lookup"><span data-stu-id="5c444-211">**zip:** hello download component is unzipped toohello destination path specified by hello **tooDirectory** path.</span></span>

<span data-ttu-id="5c444-212">toomodify hello 元件，請選取元件，再按一下 hello**編輯**按鈕在 hello**元件**屬性頁。</span><span class="sxs-lookup"><span data-stu-id="5c444-212">toomodify a component, select hello component and click hello **Edit** button in hello **Components** property page.</span></span> <span data-ttu-id="5c444-213">隨即會開啟對話方塊允許您 toomodify hello 元件屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-213">A dialog will be opened allowing you toomodify hello component properties.</span></span> <span data-ttu-id="5c444-214">按**確定**toosave hello 元件值。</span><span class="sxs-lookup"><span data-stu-id="5c444-214">Press **OK** toosave hello component values.</span></span>

<span data-ttu-id="5c444-215">toodelete hello 元件，請選取元件，再按一下 hello**移除**按鈕在 hello**元件**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="5c444-215">toodelete a component, select hello component and click hello **Remove** button in hello **Components** property page, and then click **Yes** tooconfirm hello deletion.</span></span>

<span data-ttu-id="5c444-216">元件會處理 hello 按所列的順序。</span><span class="sxs-lookup"><span data-stu-id="5c444-216">Components are processed in hello order listed.</span></span> <span data-ttu-id="5c444-217">使用 hello**移**和**下移**按鈕 tooarrange hello 順序。</span><span class="sxs-lookup"><span data-stu-id="5c444-217">Use hello **Move Up** and **Move Down** buttons tooarrange hello order.</span></span>

> [!NOTE]
> <span data-ttu-id="5c444-218">hello 伺服器組態功能必須依賴元件。</span><span class="sxs-lookup"><span data-stu-id="5c444-218">hello server configuration feature relies on components as well.</span></span> <span data-ttu-id="5c444-219">這些元件無法移除或編輯但不會移除 hello 對應伺服器組態。</span><span class="sxs-lookup"><span data-stu-id="5c444-219">Those components cannot be removed or edited without removing hello corresponding server configuration.</span></span> <span data-ttu-id="5c444-220">嘗試 toomake 變更 toosuch 元件時，將會提示您了解。</span><span class="sxs-lookup"><span data-stu-id="5c444-220">You will be prompted about that when attempting toomake changes toosuch components.</span></span>
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a><span data-ttu-id="5c444-221">端點屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-221">Endpoints properties</span></span>
<span data-ttu-id="5c444-222">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="5c444-222">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Endpoints**.</span></span> <span data-ttu-id="5c444-223">在這個對話方塊中，您已擁有 hello 能力 toocreate 端點，以及編輯或移除端點，，hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="5c444-223">Within this dialog, you have hello ability toocreate an endpoint, as well as edit or remove an endpoint, as shown in hello following image.</span></span>

![][ic719505]

<span data-ttu-id="5c444-224">tooadd 的端點，請按一下 hello**新增**hello 按鈕**端點**屬性頁和**加入端點**隨即會開啟對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-224">tooadd an endpoint, click hello **Add** button in hello **Endpoints** property page, and an **Add Endpoint** dialog will be opened.</span></span>

![][ic710897]

<span data-ttu-id="5c444-225">輸入 hello 端點的名稱，選取 hello 類型 (任一**輸入**，**內部**，或**InstanceInput**)，並指定 hello 公用和私用連接埠。</span><span class="sxs-lookup"><span data-stu-id="5c444-225">Enter a name for hello endpoint, select hello type (either **Input**, **Internal**, or **InstanceInput**), and specify hello public and private port.</span></span> <span data-ttu-id="5c444-226">按**確定**toosave hello 新端點值。</span><span class="sxs-lookup"><span data-stu-id="5c444-226">Press **OK** toosave hello new endpoint values.</span></span>

<span data-ttu-id="5c444-227">根據端點 hello 類型，您可以使用連接埠範圍，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5c444-227">Depending on hello type of endpoint, you may use port ranges as follows:</span></span>

* <span data-ttu-id="5c444-228">輸入執行個體端點，hello 公用連接埠可以是連接埠範圍 (例如**2000年-2010年**) hello 私用連接埠是固定的值。</span><span class="sxs-lookup"><span data-stu-id="5c444-228">For an input instance endpoint, hello public port can be a range of ports (for example **2000-2010**) and hello private port is a fixed value.</span></span>
* <span data-ttu-id="5c444-229">內部端點，未使用 hello 公用連接埠，而且 hello 私用連接埠可以是範圍，或保持空白或設定 tooan 星號 tooindicate 由 Azure 自動設定。</span><span class="sxs-lookup"><span data-stu-id="5c444-229">For an internal endpoint, hello public port is not used, and hello private port can be a range, or left blank or set tooan asterisk tooindicate it is automatically set by Azure.</span></span>
* <span data-ttu-id="5c444-230">輸入端點，hello 公用連接埠只能是固定的值，而且 hello 私用連接埠可以是固定的值，或保持空白或設定 tooan 星號 tooindicate 由 Azure 自動設定。</span><span class="sxs-lookup"><span data-stu-id="5c444-230">For input endpoints, hello public port can only be a fixed value, and hello private port can be a fixed value, or left blank or set tooan asterisk tooindicate it is automatically set by Azure.</span></span>

<span data-ttu-id="5c444-231">如果您想 toouse 而非某個範圍的單一通訊埠編號，請將 hello hello 範圍結尾的 hello 文字方塊保留空白。</span><span class="sxs-lookup"><span data-stu-id="5c444-231">If you want toouse a single port number instead of a range, leave hello text box for hello end of hello range blank.</span></span>

<span data-ttu-id="5c444-232">會組 tooautomatic，如果您需要 toodetermine 在執行階段實際使用的通訊埠的通訊埠，您的應用程式可以使用 hello Azure 服務執行階段 API，而其記錄在 hello[封裝 com.microsoft.windowsazure.serviceruntime （英文）摘要][com.microsoft.windowsazure.serviceruntime package summary]。</span><span class="sxs-lookup"><span data-stu-id="5c444-232">For ports that are set tooautomatic, if you need toodetermine which port is actually used during runtime, your application can use hello Azure Service Runtime API, which is documented in hello [com.microsoft.windowsazure.serviceruntime package summary][com.microsoft.windowsazure.serviceruntime package summary].</span></span>

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

<span data-ttu-id="5c444-233">將端點，toomodify 選取 hello 端點，然後按一下 hello**編輯**按鈕在 hello**端點**屬性頁。</span><span class="sxs-lookup"><span data-stu-id="5c444-233">toomodify an endpoint, select hello endpoint and click hello **Edit** button in hello **Endpoints** property page.</span></span> <span data-ttu-id="5c444-234">Toomodify hello 端點名稱、 類型和公用及私用連接埠，可讓您開啟的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-234">A dialog will be opened allowing you toomodify hello endpoint name, type, and public and private ports.</span></span> <span data-ttu-id="5c444-235">按**確定**toosave hello 修改端點值。</span><span class="sxs-lookup"><span data-stu-id="5c444-235">Press **OK** toosave hello modified endpoint values.</span></span>

<span data-ttu-id="5c444-236">將端點，toodelete 選取 hello 端點，然後按一下hello**移除**hello 按鈕**端點**屬性頁，然後按一下**是**tooconfirm hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="5c444-236">toodelete an endpoint, select hello endpoint and click hello **Remove** button in hello **Endpoints** property page, and then click **Yes** tooconfirm hello deletion.</span></span>

<span data-ttu-id="5c444-237">在訂單 tooproperly 設定部分 hello 功能 （例如快取、 工作階段相似性或 SSL 卸載） hello 使用者角色上啟用，hello 工具組可能會自動設定特殊的端點，將會與使用者定義的端點一起列出。</span><span class="sxs-lookup"><span data-stu-id="5c444-237">In order tooproperly configure some of hello features (such as Caching, Session Affinity, or SSL offloading) enabled by hello user on a role, hello toolkit may automatically configure special endpoints that will be listed along with user-defined endpoints.</span></span> <span data-ttu-id="5c444-238">hello toolkit 可防止 hello 使用者編輯或刪除這類自動產生的端點，只要 hello 相關聯的功能啟用。</span><span class="sxs-lookup"><span data-stu-id="5c444-238">hello toolkit prevents hello user from editing or deleting such automatically generated endpoints as long as hello associated feature is enabled.</span></span>

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a><span data-ttu-id="5c444-239">環境變數屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-239">Environment variables properties</span></span>
<span data-ttu-id="5c444-240">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**環境變數**。</span><span class="sxs-lookup"><span data-stu-id="5c444-240">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Environment Variables**.</span></span> <span data-ttu-id="5c444-241">在這個對話方塊中，您已擁有 hello 能力 toocreate 環境變數，以及修改或移除環境變數，，hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="5c444-241">Within this dialog, you have hello ability toocreate an environment variable, as well as modify or remove an environment variable, as shown in hello following image.</span></span>

![][ic719506]

<span data-ttu-id="5c444-242">Hello 角色啟動時，環境變數會是可用 tooyour 啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="5c444-242">Environment variables are available tooyour startup script when hello role starts.</span></span>

> [!NOTE]
> <span data-ttu-id="5c444-243">在指定環境變數時，請記住您的部署將會發行的 tooa Windows 虛擬機器，因此您的環境變數必須是有效的 windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="5c444-243">When specifying environment variables, keep in mind that your deployment will be published tooa Windows virtual machine, so your environment variables must be valid for a Windows-based operating system.</span></span>
> 
> 

<span data-ttu-id="5c444-244">例如 hello 角色啟動時所使用的環境變數中，建立新環境變數，即可 hello**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c444-244">As an example of an environment variable being available when hello role starts, create a new environment variable by clicking hello **Add** button.</span></span> <span data-ttu-id="5c444-245">hello 下列範例示範名為的環境變數**MyRoleVersion**正在建立並指派 hello 值**1.0**。</span><span class="sxs-lookup"><span data-stu-id="5c444-245">hello following shows an environment variable named **MyRoleVersion** being created and assigned hello value **1.0**.</span></span>

![][ic659268]

<span data-ttu-id="5c444-246">在您的 jsp 程式碼，您可以顯示 hello 值使用 hello`System.getenv`方法：</span><span class="sxs-lookup"><span data-stu-id="5c444-246">Within your jsp code, you could display hello value using hello `System.getenv` method:</span></span>

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

<span data-ttu-id="5c444-247">當應用程式執行時會產生以下輸出：</span><span class="sxs-lookup"><span data-stu-id="5c444-247">Resulting in this output when your application runs:</span></span>

![][ic552233]

<span data-ttu-id="5c444-248">toomodify 環境變數，選取 hello 環境變數，然後按一下 hello**編輯**按鈕在 hello**環境變數**屬性頁。</span><span class="sxs-lookup"><span data-stu-id="5c444-248">toomodify an environment variable, select hello environment variable and click hello **Edit** button in hello **Environment Variables** property page.</span></span> <span data-ttu-id="5c444-249">隨即會開啟對話方塊允許您 toomodify hello 環境變數屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-249">A dialog will be opened allowing you toomodify hello environment variable properties.</span></span> <span data-ttu-id="5c444-250">按**確定**toosave hello 環境變數的值。</span><span class="sxs-lookup"><span data-stu-id="5c444-250">Press **OK** toosave hello environment variable values.</span></span>

<span data-ttu-id="5c444-251">toodelete 環境變數，選取 hello 環境變數，然後按一下 hello**移除**按鈕在 hello**環境變數**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="5c444-251">toodelete an environment variable, select hello environment variable and click hello **Remove** button in hello **Environment Variables** property page, and then click **Yes** tooconfirm hello deletion.</span></span>

<span data-ttu-id="5c444-252">順序 tooproperly 中設定的一些 hello 功能 （例如伺服器組態、 遠端偵錯或本機儲存體） hello 使用者角色上啟用，hello 工具組可能會自動設定特殊的環境變數會連同列使用者定義的環境變數。</span><span class="sxs-lookup"><span data-stu-id="5c444-252">In order tooproperly configure some of hello features (such as Server Configuration, Remote Debugging or Local Storage) enabled by hello user on a role, hello toolkit may automatically configure special environment variables that will be listed along with user-defined environment variables.</span></span> <span data-ttu-id="5c444-253">hello toolkit 可防止 hello 使用者編輯或刪除這類自動產生的環境變數，只要 hello 相關聯的功能啟用。</span><span class="sxs-lookup"><span data-stu-id="5c444-253">hello toolkit prevents hello user from editing or deleting such automatically generated environment variables as long as hello associated feature is enabled.</span></span>

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a><span data-ttu-id="5c444-254">負載平衡/工作階段親和性 (也稱為「黏性工作階段」) 屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-254">Load balancing / session affinity (a.k.a "sticky sessions") properties</span></span>
<span data-ttu-id="5c444-255">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**負載平衡**。</span><span class="sxs-lookup"><span data-stu-id="5c444-255">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Load Balancing**.</span></span> <span data-ttu-id="5c444-256">在這個對話方塊中，您 hello 能力 tooenable 或停用工作階段親和性，hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="5c444-256">Within this dialog, you have hello ability tooenable or disable session affinity, as shown in hello following image.</span></span>

![][ic719492]

<span data-ttu-id="5c444-257">如需相關資訊，請參閱[工作階段親和性][Session Affinity]。</span><span class="sxs-lookup"><span data-stu-id="5c444-257">For related information, see [Session Affinity][Session Affinity].</span></span> <span data-ttu-id="5c444-258">另外請注意這項功能的行為在 hello 內容中的 SSL 卸載，依照[SSL 卸載][SSL Offloading]。</span><span class="sxs-lookup"><span data-stu-id="5c444-258">Also, note this feature's behavior in hello context of SSL offloading, as described at [SSL Offloading][SSL Offloading].</span></span>

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a><span data-ttu-id="5c444-259">本機儲存體屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-259">Local storage properties</span></span>
<span data-ttu-id="5c444-260">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**本機儲存體**。</span><span class="sxs-lookup"><span data-stu-id="5c444-260">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="5c444-261">在這個對話方塊中，您已擁有 hello 能力 toocreate、 修改或移除 hello 執行應用程式的虛擬機器的暫存本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="5c444-261">Within this dialog, you have hello ability toocreate, modify or remove temporary local storage for hello virtual machine that is running your application.</span></span> <span data-ttu-id="5c444-262">特定的值可以設定 hello hello 本機儲存體大小，以及是否 hello 內容會保留 hello 角色回收時，hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="5c444-262">Specific values can be set for hello size of hello local storage, as well as whether hello contents are preserved when hello role is recycled, as shown in hello following image.</span></span>

![][ic719508]

<span data-ttu-id="5c444-263">您也可以指定環境變數對應 toohello 本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="5c444-263">You can also optionally specify an environment variable that corresponds toohello local storage.</span></span>

<span data-ttu-id="5c444-264">根據預設，您部署至 Azure 的所有項目是用來放置 （和解壓縮） hello **approot** hello 角色執行個體的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c444-264">By default, everything that you deploy into Azure is placed (and unzipped) in hello **approot** folder of hello role instance.</span></span> <span data-ttu-id="5c444-265">雖然大多數的簡單部署可容納即使解壓縮，配置給 hello hello 空間**approot**目錄可是有限且未妥善定義 （小於 1 GB 是合理的經驗法則）。</span><span class="sxs-lookup"><span data-stu-id="5c444-265">While most simple deployments will fit there even after unzipping, hello space allocated for hello **approot** directory is limited and not well-defined (less than 1 GB is a reasonable rule of thumb).</span></span> <span data-ttu-id="5c444-266">因此，tooensure Azure 配置足夠的磁碟空間較大的部署，可能不適合在 hello **approot**資料夾中，您應該設定本機儲存體資源使用 hello**本機儲存體**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-266">Therefore, tooensure Azure allocates sufficient disk space for larger deployments that might not fit in hello **approot** folder, you should set up a local storage resource using hello **Local Storage** dialog.</span></span> <span data-ttu-id="5c444-267">針對輕鬆 toodo 這個，請參閱[部署大型部署][Deploying Large Deployments]。</span><span class="sxs-lookup"><span data-stu-id="5c444-267">For an easy way toodo this, see [Deploying Large Deployments][Deploying Large Deployments].</span></span>

<span data-ttu-id="5c444-268">您可以從啟動指令碼容易參考 hello 儲存體資源 (例如，您**startup.cmd**) hello中所示，使用自動與hello資源相關聯的helloEclipse工具組的hello環境變數**本機儲存體**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-268">You can easily reference hello storage resource from startup scripts (for example, your **startup.cmd**) using hello environment variable automatically associated by hello Eclipse toolkit with hello resource, as shown in hello **Local Storage** dialog.</span></span> <span data-ttu-id="5c444-269">這個環境變數將包含 hello hello hello 次執行啟動指令碼時已設定您的本機資源的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="5c444-269">That environment variable will contain hello full path of hello local resource you've configured at hello time your startup script is executed.</span></span> 

<span data-ttu-id="5c444-270">toomodify 本機儲存體資源，選取 hello 本機儲存體資源，然後按一下 hello**編輯**按鈕在 hello**本機儲存體**屬性頁。</span><span class="sxs-lookup"><span data-stu-id="5c444-270">toomodify a local storage resource, select hello local storage resource and click hello **Edit** button in hello **Local Storage** property page.</span></span> <span data-ttu-id="5c444-271">隨即會開啟對話方塊允許您 toomodify hello 本機儲存體資源屬性。</span><span class="sxs-lookup"><span data-stu-id="5c444-271">A dialog will be opened allowing you toomodify hello local storage resource properties.</span></span> <span data-ttu-id="5c444-272">按**確定**toosave hello 本機儲存體資源值。</span><span class="sxs-lookup"><span data-stu-id="5c444-272">Press **OK** toosave hello local storage resource values.</span></span>

<span data-ttu-id="5c444-273">toodelete 本機儲存體資源，選取 hello 本機儲存體資源，然後按一下 hello**移除**按鈕在 hello**本機儲存體**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="5c444-273">toodelete a local storage resource, select hello local storage resource and click hello **Remove** button in hello **Local Storage** property page, and then click **Yes** tooconfirm hello deletion.</span></span>

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a><span data-ttu-id="5c444-274">伺服器組態屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-274">Server configuration properties</span></span>
<span data-ttu-id="5c444-275">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**伺服器組態**。</span><span class="sxs-lookup"><span data-stu-id="5c444-275">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Server Configuration**.</span></span> <span data-ttu-id="5c444-276">在這個對話方塊中，您必須 hello 能力 tooadd，移除，並修改 hello JDK 和 Java 應用程式伺服器，供您的部署，以及新增或移除 hello 應用程式 （例如 WAR、 JAR 或 EAR 檔案） 使用您的部署。</span><span class="sxs-lookup"><span data-stu-id="5c444-276">Within this dialog, you have hello ability tooadd, remove, and modify hello JDK and Java application server used by your deployment, as well as add or remove hello applications (such as WAR, JAR or EAR files) used by your deployment.</span></span>

### <a name="jdk-configuration"></a><span data-ttu-id="5c444-277">JDK 組態</span><span class="sxs-lookup"><span data-stu-id="5c444-277">JDK configuration</span></span>
<span data-ttu-id="5c444-278">這個對話方塊可讓您 toospecify hello JDK 封裝 toouse 為您的部署。</span><span class="sxs-lookup"><span data-stu-id="5c444-278">This dialog allows you toospecify hello JDK package toouse for your deployment.</span></span> <span data-ttu-id="5c444-279">如果您在 Windows 上使用 Eclipse，您可以指定 hello JDK 封裝 toouse 在本機執行時在 hello Azure 模擬器，而且您擁有 hello 選項 toodeploy 該本機安裝 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="5c444-279">If you are using Eclipse on Windows, you can specify hello JDK package toouse locally when running in hello Azure emulator and you have hello option toodeploy that local installation tooAzure.</span></span> <span data-ttu-id="5c444-280">在非 Windows 作業系統上 hello 模擬器 JDK 設定不適用，而且您無法部署 hello 在本機安裝的 JDK，因為它不是與 Windows 相容。</span><span class="sxs-lookup"><span data-stu-id="5c444-280">On non-Windows operating systems, hello emulator JDK setting is not applicable and you cannot deploy hello locally installed JDK since it is not compatible with Windows.</span></span> <span data-ttu-id="5c444-281">不過，hello 不論作業系統為何，您使用，您可以隨時在 hello 第 3 個合作對象 JDK 封裝 toodeploy tooAzure，或從其他下載位置指向您自己的 Windows 相容 JDK 封裝。</span><span class="sxs-lookup"><span data-stu-id="5c444-281">However, regardless of hello operating system that you are using, you can always choose among hello 3rd party JDK packages toodeploy tooAzure, or point at your own Windows-compatible JDK package from an alternate download location.</span></span>

<span data-ttu-id="5c444-282">hello 以下是如何在 Windows 上指定 JDK 的範例：</span><span class="sxs-lookup"><span data-stu-id="5c444-282">hello following is an example of how you can specify a JDK on Windows:</span></span>

![][ic780647]

<span data-ttu-id="5c444-283">如果您在 Windows 上使用 Eclipse，您可以指定以 hello JDK toouse 計算模擬器;因此，請確定 toodo**使用 hello JDK 進行本機測試此檔案路徑**簽入 hello**模擬器部署**> 一節。</span><span class="sxs-lookup"><span data-stu-id="5c444-283">If you are using Eclipse on Windows, you can specify a JDK toouse with hello compute emulator; toodo so, ensure **Use hello JDK from this file path for testing locally** is checked in hello **Emulator deployment** section.</span></span> <span data-ttu-id="5c444-284">然後，指定 hello 本機路徑 tooyour JDK;如果 hello 您想 toouse 不會自動選取，您可以瀏覽 toodifferent JDK。</span><span class="sxs-lookup"><span data-stu-id="5c444-284">Then, specify hello local path tooyour JDK; you can browse toodifferent JDK if hello one you want toouse is not selected automatically.</span></span> <span data-ttu-id="5c444-285">您也可以 hello 選項 toodeploy 您 JDK tooyour Azure 雲端服務。toodo 因此，選取 hello**部署我的本機 JDK （自動上傳 toocloud 儲存體）**選項在 hello**雲端部署**> 一節。</span><span class="sxs-lookup"><span data-stu-id="5c444-285">You also have hello option toodeploy your JDK tooyour Azure cloud service; toodo so, select hello **Deploy my local JDK (auto-upload toocloud storage)** option in hello **Cloud deployment** section.</span></span>

<span data-ttu-id="5c444-286">注意： 在非 Windows 作業系統上 hello**模擬器部署**設定和 hello**部署我的本機 JDK**選項則無法使用。</span><span class="sxs-lookup"><span data-stu-id="5c444-286">Note: On non-Windows operating systems, hello **Emulator deployment** settings and hello **Deploy my local JDK** option are not available.</span></span> <span data-ttu-id="5c444-287">hello 下列範例說明如何指定 JDK 的 Mac 上或其他支援的非 Windows 作業系統：</span><span class="sxs-lookup"><span data-stu-id="5c444-287">hello following example illustrates specifying a JDK on a Mac or other supported non-Windows operating system:</span></span>

![][ic789643]

<span data-ttu-id="5c444-288">不論您是在 hello 作業系統，您有下列兩個 hello**雲端部署**hello 來源和類型的 JDK 封裝的選項：</span><span class="sxs-lookup"><span data-stu-id="5c444-288">Regardless of hello operating system you are on, you have hello following two **Cloud deployment** options for hello source and type of your JDK package:</span></span>

* <span data-ttu-id="5c444-289">**部署 Azure 提供的第三方 JDK 封裝**</span><span class="sxs-lookup"><span data-stu-id="5c444-289">**Deploy a 3rd party JDK package available on Azure**</span></span> 
* <span data-ttu-id="5c444-290">**從自訂下載部署**</span><span class="sxs-lookup"><span data-stu-id="5c444-290">**Deploy from a custom download**</span></span> 

<span data-ttu-id="5c444-291">如果您使用 hello**部署第 3 個合作對象 JDK 封裝可從 Azure**選項：</span><span class="sxs-lookup"><span data-stu-id="5c444-291">If you are using hello **Deploy a 3rd party JDK package available from Azure** option:</span></span>

1. <span data-ttu-id="5c444-292">選取名為 hello 核取方塊**部署第 3 個合作對象 JDK 封裝可從 Azure**。</span><span class="sxs-lookup"><span data-stu-id="5c444-292">Check hello checkbox named **Deploy a 3rd party JDK package available from Azure**.</span></span>
2. <span data-ttu-id="5c444-293">從 [hello] 下拉式清單中，選取位於 Azure 的 hello 第 3 個合作對象 JDK 封裝。</span><span class="sxs-lookup"><span data-stu-id="5c444-293">From hello drop-down list, select hello 3rd party JDK package that is available on Azure.</span></span>
3. <span data-ttu-id="5c444-294">您**JDK**  索引標籤看起來類似 toohello 下列視窗：![][ic780648]和它看起來類似 toohello 下列 Mac OS 或其他支援的非 Windows 作業系統：![][ic789643]</span><span class="sxs-lookup"><span data-stu-id="5c444-294">Your **JDK** tab will look similar toohello following on Windows:  ![][ic780648] And it will look similar toohello following on Mac OS or other supported non-Windows operating systems:  ![][ic789643]</span></span>
4. <span data-ttu-id="5c444-295">按一下**確定**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="5c444-295">Click **OK** toosave your changes.</span></span>
5. <span data-ttu-id="5c444-296">當提示的 tooaccept hello hello 第 3 個協力廠商 JDK 封裝提供者授權合約時，請檢閱 hello 授權條款。</span><span class="sxs-lookup"><span data-stu-id="5c444-296">When prompted tooaccept hello license agreement from hello 3rd party JDK package provider, review hello license terms.</span></span> <span data-ttu-id="5c444-297">假設您接受 hello 條款，請按一下**是**tooclose hello**接受授權合約**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-297">Assuming you accept hello terms, click **Yes** tooclose hello **Accept license agreement** dialog.</span></span>
    <span data-ttu-id="5c444-298">請注意該 hello 基礎的邏輯 hello 的 hello 下拉式清單中出現的項目**部署第 3 個合作對象 JDK 封裝可從 Azure**可以自訂選項。</span><span class="sxs-lookup"><span data-stu-id="5c444-298">Note that hello underlying logic for which items appear in hello drop-down list for hello **Deploy a 3rd party JDK package available from Azure** option can be customized.</span></span> <span data-ttu-id="5c444-299">toocustomize hello 中的項目，hello **JDK**  對話方塊中，按一下 hello**自訂**連結。</span><span class="sxs-lookup"><span data-stu-id="5c444-299">toocustomize hello items, in hello **JDK** dialog, click hello **Customize** link.</span></span> <span data-ttu-id="5c444-300">這樣會關閉 hello **JDK**屬性頁，並開啟 hello **componentsets.xml**在 Eclipse，您可以再視需要修改的檔案。</span><span class="sxs-lookup"><span data-stu-id="5c444-300">This will close hello **JDK** property page and open hello **componentsets.xml** file in Eclipse, which you can then modify as needed.</span></span> <span data-ttu-id="5c444-301">文件**componentsets.xml**隨附於 hello **componentsets.xml**檔案本身。</span><span class="sxs-lookup"><span data-stu-id="5c444-301">Documentation for **componentsets.xml** is included in hello **componentsets.xml** file itself.</span></span>

<span data-ttu-id="5c444-302">如果您使用 hello**部署從自訂下載 JDK**選項：</span><span class="sxs-lookup"><span data-stu-id="5c444-302">If you are using hello **Deploy a JDK from a custom download** option:</span></span>

1. <span data-ttu-id="5c444-303">建立 JDK 安裝目錄的 ZIP，請確保該 hello 目錄節點本身是 hello 的子系 hello ZIP 結構和非其內容。</span><span class="sxs-lookup"><span data-stu-id="5c444-303">Create a ZIP of your JDK installation directory, ensuring that hello directory node itself is hello child of hello ZIP structure, and not its contents.</span></span> <span data-ttu-id="5c444-304">請注意 hello hello 目錄名稱，當您將需要更新版本中，並記住此 JDK 安裝將會部署的 tooa Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5c444-304">Take note of hello name of hello directory, as you will need it later, and keep in mind this JDK installation will be deployed tooa Windows virtual machine.</span></span>
2. <span data-ttu-id="5c444-305">上傳到 Azure 儲存體帳戶的 hello ZIP，以 blob 的形式。</span><span class="sxs-lookup"><span data-stu-id="5c444-305">Upload hello ZIP into your Azure storage account as a blob.</span></span> <span data-ttu-id="5c444-306">您可以上傳 blob tooAzure 儲存體使用外部的可用工具。</span><span class="sxs-lookup"><span data-stu-id="5c444-306">You can do this using an externally available tool for uploading blobs tooAzure storage.</span></span> <span data-ttu-id="5c444-307">它會建議 toouse 私用 blob。</span><span class="sxs-lookup"><span data-stu-id="5c444-307">It is recommended toouse a private blob.</span></span> <span data-ttu-id="5c444-308">記下 hello ZIP 內容的 hello blob URL。</span><span class="sxs-lookup"><span data-stu-id="5c444-308">Take note of hello blob URL of hello ZIP contents.</span></span>
3. <span data-ttu-id="5c444-309">選取名為 hello 核取方塊**部署從自訂下載 JDK**。</span><span class="sxs-lookup"><span data-stu-id="5c444-309">Check hello checkbox named **Deploy a JDK from a custom download**.</span></span>
    <span data-ttu-id="5c444-310">如果您想 toodownload 從您的 Azure 儲存體帳戶時，選取 hello 儲存體帳戶從 hello**儲存體帳戶**下拉式清單 (您可以按一下 hello**帳戶**連結 toomodify 功能的 hello 清單)，這會填入在 hello **URL**欄位，然後填入 hello 剩餘 hello URL 的部分。</span><span class="sxs-lookup"><span data-stu-id="5c444-310">If you want toodownload from your Azure storage account, select hello storage account from hello **Storage account** drop-down list (you can click hello **Accounts** link toomodify what is in hello list), which will partially fill in hello **URL** field, and then fill in hello remaining portion of hello URL.</span></span> <span data-ttu-id="5c444-311">如果您不想 toouse Azure 儲存體，請選取**（無）**從 hello**儲存體帳戶**下拉式清單，然後輸入 hello hello URL tooyour JDK 下載**URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="5c444-311">If you do not want toouse Azure storage, select **(none)** from hello **Storage account** drop-down list, and enter hello URL tooyour JDK download in hello **URL** field.</span></span> <span data-ttu-id="5c444-312">如果使用 Azure 儲存體，hello URL 中的 blob 名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="5c444-312">If using Azure storage, blob names in hello URL must be lowercase.</span></span>
4. <span data-ttu-id="5c444-313">請確定該 hello **JAVA_HOME**文字方塊參考 toohello 正確的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="5c444-313">Ensure that hello **JAVA_HOME** textbox refers toohello correct directory name.</span></span> <span data-ttu-id="5c444-314">根據預設，它會參考 hello 做為您選擇在本機使用的 hello 值相同的 JDK 目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="5c444-314">By default, it will reference hello same JDK directory name as hello value you chose for your local use.</span></span> <span data-ttu-id="5c444-315">但是，如果包含在 hello ZIP hello 目錄有不同的名稱 (例如，到期 toousing 不同的版本)，更新 hello 目錄名稱中 hello **JAVA_HOME**文字方塊中，因為這項設定將用於 hello 雲端 （不在 hello 計算模擬器）。</span><span class="sxs-lookup"><span data-stu-id="5c444-315">But if hello directory contained in hello ZIP has a different name (for example, due toousing a different version), update hello directory name in hello **JAVA_HOME** textbox accordingly, since this setting will be used in hello cloud (not in hello compute emulator).</span></span>
5. <span data-ttu-id="5c444-316">按一下**確定**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="5c444-316">Click **OK** toosave your changes.</span></span>

<span data-ttu-id="5c444-317">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="5c444-317">That's it.</span></span> <span data-ttu-id="5c444-318">現在，當您建置 hello 雲端，您會發現 hello 封裝大小會小很多、 hello 建置程序應該會耗費較少的時間和 hello 部署本身發行 toohello 雲端時也應耗費較少的時間。</span><span class="sxs-lookup"><span data-stu-id="5c444-318">Now, when you build for hello cloud, you will notice hello package size will be much smaller, hello build process should typically take less time, and hello deployment itself when you publish toohello cloud should also take less time.</span></span> <span data-ttu-id="5c444-319">請注意該 hello**部署我的本機 JDK （自動上傳 toocloud 儲存體）**或**部署從自訂下載 JDK**選項為作用中只有您的應用程式部署時 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="5c444-319">Note that hello **Deploy my local JDK (auto-upload toocloud storage)** or **Deploy a JDK from a custom download** options are in effect only when your application is deployed in hello cloud.</span></span> <span data-ttu-id="5c444-320">不會影響您的計算模擬器體驗;當您部署 toohello 計算模擬器時，仍然會使用 hello 的 hello 元件的本機版本。</span><span class="sxs-lookup"><span data-stu-id="5c444-320">They have no effect on your compute emulator experience; hello local version of hello components will still be used when you deploy toohello compute emulator.</span></span> 

### <a name="server-configuration"></a><span data-ttu-id="5c444-321">伺服器組態</span><span class="sxs-lookup"><span data-stu-id="5c444-321">Server configuration</span></span>
<span data-ttu-id="5c444-322">hello 的範例如下的方式，您可以指定應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="5c444-322">hello following is an example of how you can specify an application server.</span></span>

![][ic796926]

<span data-ttu-id="5c444-323">請確認該 hello**部署這種伺服器**核取方塊已選取，然後選擇 hello 類型要 toouse 的應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="5c444-323">Verify that hello **Deploy a server of this type** checkbox is selected, and then choose hello type of application server you want toouse.</span></span>

<span data-ttu-id="5c444-324">指定伺服器 toouse 雲端部署，您可以利用 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="5c444-324">For specifying a server toouse for cloud deployment, you can take advantage of hello following options:</span></span>

1. <span data-ttu-id="5c444-325">**部署在 Azure 上可用的第 3 個合作對象伺服器**-這是特別適用於開發/測試案例，其中部署效率和簡化是優先和 hello 伺服器不需要自訂組態。</span><span class="sxs-lookup"><span data-stu-id="5c444-325">**Deploy a 3rd party server available on Azure** - this is especially applicable in dev/test scenarios where deployment efficiency and simplicity is a priority and hello server does not require a custom configuration.</span></span> <span data-ttu-id="5c444-326">或者，要作為起始點的 hello toouse 其中一部伺服器，但您包含適當的伺服器自訂步驟中部署的啟動邏輯。</span><span class="sxs-lookup"><span data-stu-id="5c444-326">Or when you want toouse one of those servers as hello starting point but you include appropriate server customization steps in your deployment's startup logic.</span></span>
2. <span data-ttu-id="5c444-327">**從自訂下載部署**-這是特別適用於生產案例中，當您想 toouse hello 雲端應用特別準備及設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="5c444-327">**Deploy from a custom download** - this is especially applicable in production scenarios when you have a specially prepared and configured server that you want toouse in hello cloud.</span></span>
3. <span data-ttu-id="5c444-328">**部署本機伺服器安裝** - 這個選項特別適用於如果本機伺服器安裝已針對您的用途進行自訂設定。</span><span class="sxs-lookup"><span data-stu-id="5c444-328">**Deploy my local server installation** - this is especially applicable in if your local server installation is already custom-configured for your use.</span></span> <span data-ttu-id="5c444-329">如果您選擇此選項時，您也必須指定本機伺服器的路徑中 hello**本機伺服器路徑**下面文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-329">If you choose this option, you must also specify your local server's path in hello **Local server path** text box below.</span></span>

<span data-ttu-id="5c444-330">如果您使用 hello**部署在 Azure 上可用的第 3 個合作對象伺服器**選項：</span><span class="sxs-lookup"><span data-stu-id="5c444-330">If you are using hello **Deploy a 3rd party server available on Azure** option:</span></span>

1. <span data-ttu-id="5c444-331">選取名為 hello 核取方塊**部署在 Azure 上可用的第 3 個合作對象伺服器**。</span><span class="sxs-lookup"><span data-stu-id="5c444-331">Check hello checkbox named **Deploy a 3rd party server available on Azure**.</span></span>
2. <span data-ttu-id="5c444-332">從 hello 下拉式功能表中，選取與您的部署所需的 hello 伺服器軟體 toouse hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="5c444-332">From hello dropdown menu, select hello desired server software toouse with your deployment in hello cloud.</span></span> <span data-ttu-id="5c444-333">請注意，是否您已經指定一種伺服器 toouse 之前，您將無法限制的 toochoosing 僅雲端中的伺服器 hello 與此伺服器類型相同的系列。</span><span class="sxs-lookup"><span data-stu-id="5c444-333">Note, if you already specified a type of server toouse earlier, you will be limited toochoosing only a cloud server that is in hello same family as that server type.</span></span> <span data-ttu-id="5c444-334">但如果您沒有選擇伺服器類型，您可以選擇任何 Azure 目前可用的 hello 伺服器 hello 伺服器類型將會自動為您選取。</span><span class="sxs-lookup"><span data-stu-id="5c444-334">But if you did not choose a server type, you can choose from any of hello servers that are currently available on Azure and hello server type will be automatically selected for you.</span></span>
3. <span data-ttu-id="5c444-335">按一下**確定**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="5c444-335">Click **OK** toosave your changes.</span></span>

<span data-ttu-id="5c444-336">如果使用 hello**從自訂下載部署**選項：</span><span class="sxs-lookup"><span data-stu-id="5c444-336">If using hello **Deploy from a custom download** option:</span></span>

1. <span data-ttu-id="5c444-337">請確定您已經選取伺服器類型，根據 toohello 先前步驟。</span><span class="sxs-lookup"><span data-stu-id="5c444-337">Make sure that you have already selected a server type according toohello preceding steps.</span></span> <span data-ttu-id="5c444-338">這會告訴 hello 外掛程式如何從自訂下載，因為它的 toodeploy hello 伺服器必須從 hello 與所選取的伺服器類型相同的家族。</span><span class="sxs-lookup"><span data-stu-id="5c444-338">This tells hello plugin how toodeploy hello server from your custom download, as it must be from hello same family as your selected server type.</span></span>
2. <span data-ttu-id="5c444-339">選取名為 hello 核取方塊**從自訂下載部署**。</span><span class="sxs-lookup"><span data-stu-id="5c444-339">Check hello checkbox named **Deploy from a custom download**.</span></span>
    <span data-ttu-id="5c444-340">如果您想 toodownload 從您的 Azure 儲存體帳戶時，選取 hello 儲存體帳戶從 hello**儲存體帳戶**下拉式清單 (您可以按一下 hello**帳戶**連結 toomodify 功能的 hello 清單)，這會填入在 hello **URL**欄位，以及在 hello 剩餘部分 hello URL tooyour 伺服器然後填滿時，下載 ZIP （使用 Azure 儲存體，hello URL 中的 blob 名稱必須是小寫）。</span><span class="sxs-lookup"><span data-stu-id="5c444-340">If you want toodownload from your Azure storage account, select hello storage account from hello **Storage account** drop-down list (you can click hello **Accounts** link toomodify what is in hello list), which will partially fill in hello **URL** field, and then fill in hello remaining portion of hello URL tooyour server download ZIP (when using Azure storage, blob names in hello URL must be lowercase).</span></span> <span data-ttu-id="5c444-341">如果您不想 toouse Azure 儲存體，請選取**（無）**從 hello**儲存體帳戶**下拉式清單，然後輸入 hello hello URL tooyour 伺服器下載 ZIP **URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="5c444-341">If you do not want toouse Azure storage, select **(none)** from hello **Storage account** drop-down list, and enter hello URL tooyour server download ZIP in hello **URL** field.</span></span> <span data-ttu-id="5c444-342">hello ZIP 會包含代表您應用程式伺服器的安裝目錄的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c444-342">hello ZIP would contain a child folder representing your application server installation directory.</span></span> <span data-ttu-id="5c444-343">例如，如果您使用 Apache Tomcat 7.0.35 的 zip，hello 內 zip 會 hello 子資料夾代表 hello 安裝目錄，例如**apache tomcat apache-tomcat-7.0.35**。</span><span class="sxs-lookup"><span data-stu-id="5c444-343">For example, if you are using a zip for Apache Tomcat 7.0.35, within hello zip would be hello child folder representing hello installation directory, such as **apache-tomcat-7.0.35**.</span></span> 
3. <span data-ttu-id="5c444-344">指定 hello hello 主目錄環境變數的值。</span><span class="sxs-lookup"><span data-stu-id="5c444-344">Specify hello value for hello home directory environment variable.</span></span> <span data-ttu-id="5c444-345">它會預設 toohello 值用於您的本機應用程式伺服器，如果有的話，但是如果您的雲端應用程式伺服器是本機應用程式伺服器，您可以指定不同的值。</span><span class="sxs-lookup"><span data-stu-id="5c444-345">It will default toohello value used for your local application server, if any, but you can specify a different value if your cloud application server is different from your local application server.</span></span> <span data-ttu-id="5c444-346">不過，您需要確定您的雲端應用程式伺服器的 hello toomake 相同家族 hello 稍早選取的伺服器類型。</span><span class="sxs-lookup"><span data-stu-id="5c444-346">However, you need toomake sure that your cloud application server is of hello same family as hello server type selected earlier.</span></span>
    <span data-ttu-id="5c444-347">如果您更新在 hello 未來您雲端應用程式伺服器 zip，您可以手動變更 hello 主目錄設定，或 toohave 它再次符合您的本機設定 （如果您變更本機應用程式伺服器）。</span><span class="sxs-lookup"><span data-stu-id="5c444-347">If you update your cloud application server zip in hello future, you can manually change hello home directory setting, or, toohave it again match your local setting (if you changed your local application server too).</span></span>
4. <span data-ttu-id="5c444-348">按一下**確定**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="5c444-348">Click **OK** toosave your changes.</span></span>

<span data-ttu-id="5c444-349">hello 基礎的邏輯，其項目出現在 hello**伺服器** 索引標籤的 hello**伺服器組態**可自訂屬性頁。</span><span class="sxs-lookup"><span data-stu-id="5c444-349">hello underlying logic for which items appear in hello **Server** tab of hello **Server Configuration** property page can be customized.</span></span> <span data-ttu-id="5c444-350">這是一項進階的功能，您可能需要如果您的需求超出 hello 預設值，或如果您想 tooadd 其他伺服器。</span><span class="sxs-lookup"><span data-stu-id="5c444-350">This is an advanced feature that you might need if your needs extend beyond hello default values or if you want tooadd other servers.</span></span> <span data-ttu-id="5c444-351">hello 中的 toocustomize hello 邏輯**伺服器** 對話方塊中，按一下 hello**自訂**連結。</span><span class="sxs-lookup"><span data-stu-id="5c444-351">toocustomize hello logic, in hello **Server** dialog, click hello **Customize** link.</span></span> <span data-ttu-id="5c444-352">這樣會關閉 hello**伺服器組態**屬性頁，並開啟 hello **componentsets.xml** Eclipse，您可以修改為需要的 tooextend hello 伺服器組態範本中的檔案。</span><span class="sxs-lookup"><span data-stu-id="5c444-352">This will close hello **Server Configuration** property page and open hello **componentsets.xml** file in Eclipse, which you can then modify as needed tooextend hello server configuration template.</span></span> <span data-ttu-id="5c444-353">文件**componentsets.xml**隨附於 hello **componentsets.xml**檔案本身。</span><span class="sxs-lookup"><span data-stu-id="5c444-353">Documentation for **componentsets.xml** is included in hello **componentsets.xml** file itself.</span></span>

<span data-ttu-id="5c444-354">如果您使用 hello**部署我的本機伺服器 （自動上傳 toocloud 儲存體）**選項：</span><span class="sxs-lookup"><span data-stu-id="5c444-354">If you are using hello **Deploy my local server (auto-upload toocloud storage)** option:</span></span>

1. <span data-ttu-id="5c444-355">選取名為 hello 核取方塊**部署我的本機伺服器 （自動上傳 toocloud 儲存體）**。</span><span class="sxs-lookup"><span data-stu-id="5c444-355">Check hello checkbox named **Deploy my local server (auto-upload toocloud storage)**.</span></span>
2. <span data-ttu-id="5c444-356">使用 hello**儲存體帳戶**下拉式清單中，選取**（自動）**。</span><span class="sxs-lookup"><span data-stu-id="5c444-356">Using hello **Storage account** drop-down list, select **(auto)**.</span></span> <span data-ttu-id="5c444-357">如果您指定**（自動）** ，hello Eclipse 工具組會使用 hello 相同儲存體帳戶為您的伺服器 hello 其中一個您選取為您的部署中 hello**發行 tooAzure**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5c444-357">If you specify **(auto)** here, hello Eclipse toolkit will use hello same storage account for your server as hello one you select for your deployment in hello **Publish tooAzure** dialog.</span></span>
3. <span data-ttu-id="5c444-358">按一下**確定**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="5c444-358">Click **OK** toosave your changes.</span></span>

<span data-ttu-id="5c444-359">選取您的電腦上的伺服器安裝路徑中 hello**本機伺服器路徑**文字方塊中，如果任何一個 hello 下列條件成立：</span><span class="sxs-lookup"><span data-stu-id="5c444-359">Select a server installation path on your computer in hello **Local server path** text box if any of hello following conditions are true:</span></span>

* <span data-ttu-id="5c444-360">您想 tootest hello 模擬器 （適用於僅 tooWindows） 中的部署。</span><span class="sxs-lookup"><span data-stu-id="5c444-360">You want tootest your deployment in hello emulator (applies tooWindows only).</span></span>
* <span data-ttu-id="5c444-361">您想 toodeploy 您已安裝在本機伺服器的 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="5c444-361">You want toodeploy your locally installed server toohello cloud.</span></span>
* <span data-ttu-id="5c444-362">您想 toouse 中擁有 hello 雲端，在此情況下的自訂伺服器下載，也請確認 hello**部署我的本機伺服器 （自動上傳 toocloud 儲存體）**先前已選取的選項。</span><span class="sxs-lookup"><span data-stu-id="5c444-362">You want toouse a custom server download of your own in hello cloud, in which case, also ensure hello **Deploy my local server (auto-upload toocloud storage)** option is selected above.</span></span>

<span data-ttu-id="5c444-363">如果沒有任何上述選項套用 tooyour 情況下，hello 本機伺服器設定是 hello 的選擇性的。</span><span class="sxs-lookup"><span data-stu-id="5c444-363">If none of hello preceding options apply tooyour situation, hello local server setting is optional.</span></span>

### <a name="applications-configuration"></a><span data-ttu-id="5c444-364">應用程式組態</span><span class="sxs-lookup"><span data-stu-id="5c444-364">Applications configuration</span></span>
<span data-ttu-id="5c444-365">hello 以下是如何指定應用程式的範例。</span><span class="sxs-lookup"><span data-stu-id="5c444-365">hello following is an example of how you can specify an application.</span></span>

![][ic719512]

<span data-ttu-id="5c444-366">按一下**新增**tooadd 另一個應用程式，或**移除**tooremove 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c444-366">Click **Add** tooadd another application, or **Remove** tooremove an application.</span></span> <span data-ttu-id="5c444-367">基於效率考量，如果您想要下載 toouse hello 來源應用程式的部署 toohello 雲端時，使用 hello[元件屬性](#components_properties)toospecify url，儲存體帳戶，依此類推。</span><span class="sxs-lookup"><span data-stu-id="5c444-367">For efficiency purposes, if you want toouse a download for hello source of an application when deploying toohello cloud, use hello [components properties](#components_properties) toospecify a URL, storage account, etc.</span></span> 

<span data-ttu-id="5c444-368">從 hello 2014 年 4 月版開始，您的應用程式會自動上傳到 hello 相同儲存體帳戶 (在 hello **eclipsedeploy**容器) 為 hello 選取為您的部署。</span><span class="sxs-lookup"><span data-stu-id="5c444-368">Beginning with hello April 2014 release, your applications are automatically uploaded into hello same storage account (under hello **eclipsedeploy** container) as hello one selected for your deployment.</span></span> <span data-ttu-id="5c444-369">部署的 hello 啟動邏輯包含第一次下載這些應用程式從該儲存體帳戶的步驟。</span><span class="sxs-lookup"><span data-stu-id="5c444-369">hello startup logic of your deployment contains a step that first downloads those applications from that storage account.</span></span> <span data-ttu-id="5c444-370">這表示您可以升級您的應用程式部署中，而不需要 toorebuild 以及手動上傳較新版 hello 應用程式直接 （例如使用 hello Azure 入口網站） 該儲存體帳戶來重新部署整個封裝 hello，取代 hello WAR 檔案原本那裡上傳 hello 工具組。</span><span class="sxs-lookup"><span data-stu-id="5c444-370">This means that you may upgrade your applications in your deployment without needing toorebuild and redeploy hello entire package, by manually uploading newer versions of hello application directly into that storage account (using hello Azure portal for example), replacing hello WAR files originally uploaded there by hello toolkit.</span></span> <span data-ttu-id="5c444-371">然後，只要起始 hello 回收所有角色執行個體一次，或透過命令列公用程式使用 Azure 的管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="5c444-371">Then, just initiate hello recycling of all those role instances using Azure's management portal again, or via command line utilities.</span></span> <span data-ttu-id="5c444-372">（觸發角色回收直接從內 hello Eclipse 工具組目前不支援。）</span><span class="sxs-lookup"><span data-stu-id="5c444-372">(Triggering role recycling directly from within hello Eclipse toolkit is not currently supported.)</span></span>

### <a name="notes-about-server-configuration"></a><span data-ttu-id="5c444-373">伺服器組態的相關注意事項</span><span class="sxs-lookup"><span data-stu-id="5c444-373">Notes about server configuration</span></span>
<span data-ttu-id="5c444-374">透過 hello 所做的變更**伺服器組態**屬性頁會反映在 hello `<component>` hello package.xml 檔的項目。</span><span class="sxs-lookup"><span data-stu-id="5c444-374">Changes made through hello **Server configuration** property page are reflected in hello `<component>` elements of hello package.xml file.</span></span>

<span data-ttu-id="5c444-375">當您使用 hello**自動上傳...**或**從下載部署...**選項 hello JDK 或應用程式伺服器與您要建立 hello 雲端 （而非 hello 計算模擬器），而且您 toohello 連接的網路，您可能會發現建置訊息，例如 hello 下列在 hello 主控台輸出中，以 hello Ant產生器會驗證 hello 下載的可用性：</span><span class="sxs-lookup"><span data-stu-id="5c444-375">When you use hello **Automatically upload...** or **Deploy from download...** options for either hello JDK or application server, and you are building for hello cloud (not hello compute emulator), and you are connected toohello network, you may notice build messages such as hello following in hello Console output, as hello Ant builder verifies hello download's availability:</span></span>

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

<span data-ttu-id="5c444-376">如果您選取 hello**從下載部署...**選項，可能會顯示下列警告 hello，但仍會繼續建置 hello:</span><span class="sxs-lookup"><span data-stu-id="5c444-376">If you selected hello **Deploy from download...** option, hello following warning may be shown, but hello build will continue:</span></span>

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

<span data-ttu-id="5c444-377">這項警告是 hello 唯一表示 hello 下載的可用性尚未經過驗證。</span><span class="sxs-lookup"><span data-stu-id="5c444-377">This warning is hello only indication that hello download's availability hasn't been verified.</span></span> <span data-ttu-id="5c444-378">因此如果 hello 雲端中的部署是基於某些原因失敗，請查看 toosee 如果您收到這個警告。</span><span class="sxs-lookup"><span data-stu-id="5c444-378">So if a deployment fails in hello cloud for some reason, check toosee if you received this warning.</span></span>

<span data-ttu-id="5c444-379">如果您想 toodisable hello 下載驗證 （例如，如果您認為不必要地放慢 hello 建置），將的 hello`verifydownloads`屬性太`false`在 hello `<windowsazurepackage>` package.xml 的項目：</span><span class="sxs-lookup"><span data-stu-id="5c444-379">If you want toodisable hello download verification (for example, if you feel it unnecessarily slows down hello build), set hello `verifydownloads` attribute too`false` in hello `<windowsazurepackage>` element of package.xml:</span></span> 

`<windowsazurepackage verifydownloads="false" ...>` 

<span data-ttu-id="5c444-380">如果您選取 hello**自動上傳...**選項，則 hello 主控台視窗中您會看到建置訊息的 hello 上傳每 5 秒，只要上傳時必要的報告 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="5c444-380">If you selected hello **Automatically upload...** option, then in hello console window you will see build messages reporting hello progress of hello upload every 5 seconds, whenever an upload is necessary.</span></span>

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a><span data-ttu-id="5c444-381">SSL 卸載屬性</span><span class="sxs-lookup"><span data-stu-id="5c444-381">SSL offloading properties</span></span>
<span data-ttu-id="5c444-382">在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下 **SSL 卸載**。</span><span class="sxs-lookup"><span data-stu-id="5c444-382">Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **SSL Offloading**.</span></span> 

![][ic719481]

<span data-ttu-id="5c444-383">在這個對話方塊中，您可以啟用 SSL 卸載，可讓您 tooeasily 啟用超文字傳輸通訊協定安全性 (HTTPS) 支援在 Azure 上的 Java 部署中，而不需要在您的 Java 應用程式伺服器 tooconfigure SSL。</span><span class="sxs-lookup"><span data-stu-id="5c444-383">Within this dialog, you can enable SSL offloading, allowing you tooeasily enable Hypertext Transfer Protocol Secure (HTTPS) support in your Java deployment on Azure, without requiring you tooconfigure SSL in your Java application server.</span></span> <span data-ttu-id="5c444-384">如需詳細資訊，請參閱[SSL 卸載][ SSL Offloading]和[如何 tooUse SSL 卸載][How tooUse SSL Offloading]。</span><span class="sxs-lookup"><span data-stu-id="5c444-384">For more information, see [SSL Offloading][SSL Offloading] and [How tooUse SSL Offloading][How tooUse SSL Offloading].</span></span>

## <a name="see-also"></a><span data-ttu-id="5c444-385">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5c444-385">See Also</span></span>
<span data-ttu-id="5c444-386">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5c444-386">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="5c444-387">[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5c444-387">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="5c444-388">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5c444-388">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="5c444-389">[Azure 專案屬性][Azure Project Properties]</span><span class="sxs-lookup"><span data-stu-id="5c444-389">[Azure Project Properties][Azure Project Properties]</span></span>

<span data-ttu-id="5c444-390">[Azure 儲存體帳戶清單][Azure Storage Account List]</span><span class="sxs-lookup"><span data-stu-id="5c444-390">[Azure Storage Account List][Azure Storage Account List]</span></span>

<span data-ttu-id="5c444-391">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="5c444-391">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
