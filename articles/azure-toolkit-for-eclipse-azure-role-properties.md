---
title: "Azure 角色屬性"
description: "了解如何使用適用於 Eclipse 的 Azure 工具組以進行 Azure 角色設定。"
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
ms.openlocfilehash: cd734c64ba6d1394cb261bace92dee9dd579dd08
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-properties"></a><span data-ttu-id="f3e63-103">Azure 角色屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-103">Azure Role Properties</span></span>
<span data-ttu-id="f3e63-104">您可以在適用於 Eclipse 的 Azure 工具組內設定 Azure 角色的各種組態設定。</span><span class="sxs-lookup"><span data-stu-id="f3e63-104">Various configuration settings for your Azure role can be set within the Azure Toolkit for Eclipse.</span></span>

## <a name="configuring-azure-role-properties"></a><span data-ttu-id="f3e63-105">設定 Azure 角色屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-105">Configuring Azure Role Properties</span></span>
<span data-ttu-id="f3e63-106">透過背景工作角色的各個屬性對話方塊，即可完成 Azure 角色屬性的設定工作。</span><span class="sxs-lookup"><span data-stu-id="f3e63-106">Configuring your Azure Role Properties is accomplished through the property dialogs for your worker role.</span></span> <span data-ttu-id="f3e63-107">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，然後選取 [Azure] 子功能表。</span><span class="sxs-lookup"><span data-stu-id="f3e63-107">Open the context menu for the role in Eclipse's Project Explorer pane and select the **Azure** sub-menu.</span></span> <span data-ttu-id="f3e63-108">(如果在 Eclipse 的 [專案總管] 中看不到角色，請在 [專案總管] 中展開 Azure 專案)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-108">(If you don't see the role in the Eclipse Project Explorer, expand your Azure project in Project Explorer.)</span></span>

![][ic789599]

<span data-ttu-id="f3e63-109">本主題說明可以從 [屬性]  對話方塊設定的各種屬性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-109">The various properties that can be set from the **Properties** dialogs are described in this topic.</span></span> <span data-ttu-id="f3e63-110">要注意的是，在您建立新的 Azure 部署專案時，系統會自動填入其中的許多屬性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-110">Note that many properties are filled in automatically when you create a new Azure deployment project.</span></span>

<span data-ttu-id="f3e63-111">以下是可供 Azure 角色使用的屬性頁。</span><span class="sxs-lookup"><span data-stu-id="f3e63-111">The following property pages are available for Azure roles.</span></span>

* [<span data-ttu-id="f3e63-112">虛擬機器屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-112">Virtual machine properties</span></span>](#virtual_machine_properties)
* [<span data-ttu-id="f3e63-113">快取屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-113">Caching properties</span></span>](#caching_properties)
* [<span data-ttu-id="f3e63-114">憑證屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-114">Certificates properties</span></span>](#certificates_properties)
* [<span data-ttu-id="f3e63-115">元件屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-115">Components properties</span></span>](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [<span data-ttu-id="f3e63-116">端點屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-116">Endpoints properties</span></span>](#endpoints_properties)
* [<span data-ttu-id="f3e63-117">環境變數屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-117">Environment variables properties</span></span>](#environment_variables_properties)
* [<span data-ttu-id="f3e63-118">負載平衡/工作階段親和性 (也稱為「黏性工作階段」) 屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-118">Load balancing / session affinity (a.k.a "sticky sessions") properties</span></span>](#session_affinity_properties)
* [<span data-ttu-id="f3e63-119">本機儲存體屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-119">Local storage properties</span></span>](#local_storage_properties)
* [<span data-ttu-id="f3e63-120">伺服器組態屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-120">Server configuration properties</span></span>](#server_configuration_properties)
* [<span data-ttu-id="f3e63-121">SSL 卸載屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-121">SSL offloading properties</span></span>](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a><span data-ttu-id="f3e63-122">虛擬機器屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-122">Virtual machine properties</span></span>
<span data-ttu-id="f3e63-123">在 Eclipse 的 [專案總管] 窗格中開啟角色的操作功能表，按一下 [Azure]，然後按一下 [屬性]，您就能夠變更虛擬機器的大小，而且也可以變更執行個體數目，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f3e63-123">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Properties**, and you will have the ability to change the virtual machine size, and also change the number of instances, as shown in the following image.</span></span>

![][ic719499]

> [!NOTE]
> <span data-ttu-id="f3e63-124">僅限 Windows：若您將執行個體數目設為大於 1 的值，並同時設定了應用程式伺服器，則不論此設定為何，工具組將只會允許在模擬器中執行 1 個角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="f3e63-124">Windows only: when you set the number of instances to a value greater than 1 and you also configure an application server, the toolkit will allow only 1 role instance to run in the emulator, regardless of this setting.</span></span> <span data-ttu-id="f3e63-125">這是為了避免不同的伺服器執行個體在同一部電腦上執行時，彼此之間發生連接埠繫結衝突 (例如，全都嘗試繫結至連接埠 8080) 。</span><span class="sxs-lookup"><span data-stu-id="f3e63-125">This is to avoid port binding conflicts between the different server instances (for example, all trying to bind to port 8080) when they run on the same computer.</span></span> <span data-ttu-id="f3e63-126">您想要的執行個體計數設定會保留下來，但此設定只會在您部署至雲端時生效。</span><span class="sxs-lookup"><span data-stu-id="f3e63-126">Your desired instance count setting is preserved, but it goes into effect only when you deploy to the cloud.</span></span>
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a><span data-ttu-id="f3e63-127">快取屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-127">Caching properties</span></span>
<span data-ttu-id="f3e63-128">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [快取]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-128">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Caching**.</span></span> <span data-ttu-id="f3e63-129">在這個對話方塊中，您可以啟用已具名且共置的 memcache 相容快取，以協助 Web 應用程式加快速度。</span><span class="sxs-lookup"><span data-stu-id="f3e63-129">Within this dialog, you can enable named co-located memcache-compatible caches, allowing you to help speed up your web applications.</span></span>

![][ic719483]

<span data-ttu-id="f3e63-130">在 [快取]  屬性頁內，您可以指定下列項目的全域設定：</span><span class="sxs-lookup"><span data-stu-id="f3e63-130">Within the **Caching** property page, you can specify global settings for the following:</span></span>

* <span data-ttu-id="f3e63-131">是否啟用共置快取。</span><span class="sxs-lookup"><span data-stu-id="f3e63-131">whether co-located caching is enabled.</span></span>
* <span data-ttu-id="f3e63-132">快取大小佔記憶體的百分比。</span><span class="sxs-lookup"><span data-stu-id="f3e63-132">the cache size as a percent of memory.</span></span>
* <span data-ttu-id="f3e63-133">當應用程式以雲端服務的形式執行時，用來儲存快取狀態的儲存體帳戶名稱，若不想儲存快取狀態，則為無 </span><span class="sxs-lookup"><span data-stu-id="f3e63-133">the storage account name for saving the cache state when your application runs as a cloud service, or none if you do not want to save the cache state.</span></span> <span data-ttu-id="f3e63-134">(在計算模擬器中執行應用程式時，不會使用儲存體帳戶名稱)。如果您將儲存體帳戶名稱設定為 [(自動)] \(此為預設值)，您的快取設定會自動使用您在 [發佈至 Azure] 對話方塊中所選取的同一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3e63-134">(The storage account name is not used when you run your application in the compute emulator.) If you set the storage account name to **(auto)** (which is the default), your caching configuration will automatically use the same storage account as the one you select in the **Publish to Azure** dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e63-135">只有在使用 Eclipse 工具組的發佈精靈發佈部署時，[(自動)] 設定才會有所要的效果。</span><span class="sxs-lookup"><span data-stu-id="f3e63-135">The **(auto)** setting will have the desired effect only if you publish your deployment using the Eclipse toolkit's publish wizard.</span></span> <span data-ttu-id="f3e63-136">如果您改為使用外部機制 (例如 [Azure 管理入口網站][Azure Management Portal]) 手動發佈 .cspkg 檔案，部署作業將無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="f3e63-136">If instead you publish the .cspkg file manually using an external mechanism, such as the [Azure Management Portal][Azure Management Portal], the deployment will not function properly.</span></span>
> 
> 

<span data-ttu-id="f3e63-137">下列對話方塊顯示快取的各項屬性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-137">The following dialog shows the properties for a cache.</span></span>

![][ic719501]

* <span data-ttu-id="f3e63-138">**名稱：** 共置快取的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3e63-138">**Name:** The name of the co-located cache.</span></span>
* <span data-ttu-id="f3e63-139">**連接埠號碼：** 用於快取的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="f3e63-139">**Port number:** The port number to use for the cache.</span></span>
* <span data-ttu-id="f3e63-140">**到期原則：** 可為下列其中一個值，用以指定快取中的金鑰何時到期。</span><span class="sxs-lookup"><span data-stu-id="f3e63-140">**Expiration policy:** One of the following values that specifies when a key in the cache expires.</span></span>
  * <span data-ttu-id="f3e63-141">**絕對：**到達 [存留分鐘數] 所指定的時間時，金鑰就會到期。</span><span class="sxs-lookup"><span data-stu-id="f3e63-141">**Absolute:** The key expires when the time specified by **Minutes to live** is reached.</span></span>
  * <span data-ttu-id="f3e63-142">**永久有效：** 金鑰沒有到期時間。</span><span class="sxs-lookup"><span data-stu-id="f3e63-142">**NeverExpires:** The key does not have an expiration time.</span></span>
  * <span data-ttu-id="f3e63-143">**滑動視窗：**金鑰未遭到存取的時間達到 [存留分鐘數] 所指定的時間長度時，金鑰就會到期。金鑰一經存取，便會重設到期時鐘。</span><span class="sxs-lookup"><span data-stu-id="f3e63-143">**SlidingWindow:** The key expires if it has not been accessed for the amount of time specified by **Minutes to live**; each time it is accessed, the expiration clock is reset.</span></span>
* <span data-ttu-id="f3e63-144">**存留分鐘數：** 依據到期原則所決定的 Memcached 金鑰存留分鐘數上限。</span><span class="sxs-lookup"><span data-stu-id="f3e63-144">**Minutes to live:** Maximum number of minutes for a memcached key to live, subject to the expiration policy.</span></span>
* <span data-ttu-id="f3e63-145">**在不同角色執行個體上複寫備份以提供高可用性：** 啟用時，有助於利用在不同角色執行個體上複寫備份以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-145">**High availability with replicated backups on different role instances:** If enabled, helps provide high availability utilizing replicated backups on different role instances.</span></span> <span data-ttu-id="f3e63-146">但請注意，若要讓此功能運作，您的部署中至少要有兩個作用中的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="f3e63-146">Note that at least two role instances must be in effect for your deployment for this feature to work.</span></span>

<span data-ttu-id="f3e63-147">若要新增快取，請按一下 [快取] 屬性頁中的 [新增] 按鈕，隨即就會開啟 [設定具名快取] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-147">To add a new cache, click the **Add** button in the **Caching** property page, and a **Configure Named Cache** dialog will be opened.</span></span> <span data-ttu-id="f3e63-148">提供上述屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-148">Provide values for the properties which are described above.</span></span>

<span data-ttu-id="f3e63-149">若要修改具名快取，請選取快取，然後按一下 [快取] 屬性頁中的 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3e63-149">To modify a named cache, select the cache and click the **Edit** button in the **Caching** property page.</span></span> <span data-ttu-id="f3e63-150">隨即會開啟對話方塊供您修改快取屬性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-150">A dialog will be opened allowing you to modify the cache properties.</span></span> <span data-ttu-id="f3e63-151">按 [確定]  以儲存快取值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-151">Press **OK** to save the cache values.</span></span>

<span data-ttu-id="f3e63-152">若要刪除快取，請選取快取，按一下 [快取] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。</span><span class="sxs-lookup"><span data-stu-id="f3e63-152">To delete a cache, select the cache and click the **Remove** button in the **Caching** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="f3e63-153">如需有關如何使用快取的詳細資訊，請參閱[如何使用共置快取][How to Use Co-located Caching]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-153">For more information on how to use caching, see [How to Use Co-located Caching][How to Use Co-located Caching].</span></span>

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a><span data-ttu-id="f3e63-154">憑證屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-154">Certificates properties</span></span>
<span data-ttu-id="f3e63-155">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-155">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Certificates**.</span></span>

![][ic710964]

<span data-ttu-id="f3e63-156">在這個對話方塊中，您可以新增或移除 Eclipse 專案所參考的憑證。</span><span class="sxs-lookup"><span data-stu-id="f3e63-156">Within this dialog, you can add or remove certificates referenced by your Eclipse project.</span></span> <span data-ttu-id="f3e63-157">請注意，此處所列的憑證不會自動儲存在任何 Java 金鑰存放區內，因此無法自動在 Java 應用程式內提供使用。</span><span class="sxs-lookup"><span data-stu-id="f3e63-157">Note that the certificates listed here are not automatically stored inside any Java keystore, and therefore are not automatically available for any use from within a Java application.</span></span> <span data-ttu-id="f3e63-158">這些憑證只會向 Azure 進行註冊，以便可以預先載入到執行部署之虛擬機器上的 Windows 憑證存放區，並於隨後供其他 Windows 軟體使用。</span><span class="sxs-lookup"><span data-stu-id="f3e63-158">They are only registered with Azure so that they can be preloaded into the Windows certificate store on the virtual machines running your deployment and subsequently used by other Windows software.</span></span> <span data-ttu-id="f3e63-159">目前來說，工具組中只有一個功能會使用 [憑證] 對話方塊中以此方式所參考的憑證，那就是 [SSL 卸載][SSL Offloading]，因為此功能需依賴 Internet Information Services (IIS) 和應用程式要求路由 (ARR)，而這兩者要求適當的憑證必須以這種方式提供。</span><span class="sxs-lookup"><span data-stu-id="f3e63-159">Currently, the only feature of the toolkit that uses the certificates referenced this way in the **Certificates** dialog is [SSL Offloading][SSL Offloading], due to its reliance on Internet Information Services (IIS) and Application Request Routing (ARR), which require the proper certificate to be made available in this manner.</span></span>

<span data-ttu-id="f3e63-160">當您使用發佈精靈將專案部署至 Azure 時，系統會提示您指向這些憑證所對應的個人資訊交換 (PFX) 檔案以及憑證的密碼，以便自動將憑證上傳至 Azure 服務，但前提是這些憑證先前並未上傳至該處。</span><span class="sxs-lookup"><span data-stu-id="f3e63-160">When you deploy your project to Azure using the Publish wizard, you will be prompted to point at the Personal Information Exchange (PFX) files corresponding to these certificates, along with their passwords, in order to automatically upload them to the Azure service, but only if they have not been uploaded there previously.</span></span>

<a name="components_properties"></a> 

### <a name="components-properties"></a><span data-ttu-id="f3e63-161">元件屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-161">Components properties</span></span>
<span data-ttu-id="f3e63-162">在 Eclipse 的 [專案總管] 窗格中開啟角色的操作功能表，按一下 [Azure]，然後按一下 [元件]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-162">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Components**.</span></span> <span data-ttu-id="f3e63-163">在這個對話方塊中，您可以新增、修改或移除角色的元件，以及變更它們的處理順序。</span><span class="sxs-lookup"><span data-stu-id="f3e63-163">Within this dialog, you have the ability to add, modify, or remove the components of your role, as well as change the order in which they are processed.</span></span>

![][ic719502]

<span data-ttu-id="f3e63-164">元件功能可讓您對 Azure 部署專案新增相依項目，例如 Java 應用程式專案、特殊檔案，以及部署所需的可執行命令列陳述式。</span><span class="sxs-lookup"><span data-stu-id="f3e63-164">The components feature enables you to add dependencies to your Azure deployment project, such as Java application projects, special files, and executable command line statements that are needed by your deployment.</span></span>

<span data-ttu-id="f3e63-165">針對每個元件，您可以指定：</span><span class="sxs-lookup"><span data-stu-id="f3e63-165">For each component, you can specify:</span></span>

* <span data-ttu-id="f3e63-166">在建置 Azure 部署專案時，將元件匯入到其中時所要採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="f3e63-166">The step to be taken when importing the component into your Azure deployment project when it is built.</span></span>
* <span data-ttu-id="f3e63-167">在 Azure 雲端部署該元件時所要採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="f3e63-167">The step to be taken when deploying that component in the Azure cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e63-168">在指定元件檔案或命令列時請記住，您的部署將會發佈至 Windows 虛擬機器，因此您自訂的步驟必須適用於 Windows 架構的作業系統。</span><span class="sxs-lookup"><span data-stu-id="f3e63-168">When specifying component files or command lines, keep in mind that your deployment will be published to a Windows virtual machine, so your custom steps must be valid for a Windows-based operating system.</span></span> 
> 
> 

<span data-ttu-id="f3e63-169">元件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="f3e63-169">Components have the following properties:</span></span>

* <span data-ttu-id="f3e63-170">**匯入：** 指出在建置專案時用來將元件匯入到其中的方法。</span><span class="sxs-lookup"><span data-stu-id="f3e63-170">**Import:** Method that indicates how the component will be imported into the project when the project is built.</span></span> <span data-ttu-id="f3e63-171">此屬性可為下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="f3e63-171">This can be one of the following values:</span></span>
  * <span data-ttu-id="f3e63-172">**複製：**將元件從 [來源] 屬性所指定的本機路徑複製到角色的 **approot** 目錄。</span><span class="sxs-lookup"><span data-stu-id="f3e63-172">**copy:** The component is copied from the local path specified by the **From** property into the role's **approot** directory.</span></span>
  * <span data-ttu-id="f3e63-173">**EAR：**元件是 Java 企業封存檔 (EAR)，從 [來源] 屬性所指定之本機路徑上的企業應用程式專案所匯入。</span><span class="sxs-lookup"><span data-stu-id="f3e63-173">**EAR:** The component is a Java enterprise archive (EAR) imported from an Enterprise Application Project at the local path specified by the **From** property.</span></span> <span data-ttu-id="f3e63-174">(工具組會根據該位置之專案的性質自動偵測此元件)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-174">(This is detected automatically by the toolkit based on the nature of the project at that location).</span></span>
  * <span data-ttu-id="f3e63-175">**JAR：**元件是 Java 封存檔 (JAR)，從 [來源] 屬性所指定之本機路徑上的 Java 專案所匯入。</span><span class="sxs-lookup"><span data-stu-id="f3e63-175">**JAR:** The component is a Java archive (JAR) and is imported from a Java project at the local path specified by the **From** property.</span></span> <span data-ttu-id="f3e63-176">(工具組會根據該位置之專案的性質自動偵測此元件)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-176">(This is detected automatically by the toolkit based on the nature of the project at that location).</span></span>
  * <span data-ttu-id="f3e63-177">**無：** 不採取任何動作來匯入元件。</span><span class="sxs-lookup"><span data-stu-id="f3e63-177">**none:** No action is taken to import the component.</span></span> <span data-ttu-id="f3e63-178">此值適用於假設元件已出現在角色的 **approot** 目錄中時，或當元件只是如 [為] 屬性所指定的可執行命令列陳述式時 (當 [部署] 方法是 [可執行檔] 時)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-178">This is applicable when the component is assumed to already be present in the role's **approot** directory, or when the component is merely an executable command line statement, as specified in the **As** property when the **Deploy** method is **exec**.</span></span>
  * <span data-ttu-id="f3e63-179">**WAR：**元件是 Java Web 應用程式封存檔 (WAR)，從 [來源] 屬性所指定之本機路徑上的動態 Web 專案所匯入。</span><span class="sxs-lookup"><span data-stu-id="f3e63-179">**WAR:** The component is a Java web application archive (WAR) and is imported from a Dynamic Web Project at the local path specified by the **From** property.</span></span> <span data-ttu-id="f3e63-180">(工具組會根據該位置之專案的性質自動偵測此元件)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-180">(This is detected automatically by the toolkit based on the nature of the project at that location).</span></span>
  * <span data-ttu-id="f3e63-181">**Zip 檔：**元件是 Zip 檔案，透過壓縮 [來源] 屬性所指定的目錄或檔案所匯入。</span><span class="sxs-lookup"><span data-stu-id="f3e63-181">**zip:** The component is a zip file and is imported by zipping the directory or file specified by the **From** property.</span></span>
* <span data-ttu-id="f3e63-182">**來源：** 代表要匯入部署中之項目的資料夾或檔案在本機電腦上的來源路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-182">**From:** Source path on your local machine to the folder or file that represents the item(s) to import to your deployment.</span></span> <span data-ttu-id="f3e63-183">此屬性可以使用 Windows 環境變數。</span><span class="sxs-lookup"><span data-stu-id="f3e63-183">Windows environment variables can be used in this property.</span></span> <span data-ttu-id="f3e63-184">在建置專案時，所有可匯入的元件都會匯入到角色的 **approot** 目錄。</span><span class="sxs-lookup"><span data-stu-id="f3e63-184">All importable components will be imported into the role's **approot** directory when the project is built.</span></span>
  
    <span data-ttu-id="f3e63-185">請注意，在部署到雲端 (而非計算模擬器) 時，可以透過下載來部署元件。</span><span class="sxs-lookup"><span data-stu-id="f3e63-185">Note that you have the ability to deploy a component from a download when deploying to the cloud (not the compute emulator).</span></span> <span data-ttu-id="f3e63-186">請參閱以下有關新增元件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-186">See related information below about adding a component.</span></span>    
* <span data-ttu-id="f3e63-187">**為：**元件要匯入到角色的 **approot** 目錄下的檔案名稱，而且此元件最終會部署在 Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="f3e63-187">**As:** File name under which the component will be imported into the role's **approot** directory and ultimately deployed in the Azure cloud.</span></span> <span data-ttu-id="f3e63-188">將此屬性空白，可讓名稱保持與位於本機電腦上時相同 </span><span class="sxs-lookup"><span data-stu-id="f3e63-188">Leave this property blank to keep the name the same as it is on the local machine.</span></span> <span data-ttu-id="f3e63-189">(若為可執行檔元件，亦即 [部署] 方法設為 [可執行檔] 的元件，此屬性可以是任意的 Windows 命令列陳述式。)</span><span class="sxs-lookup"><span data-stu-id="f3e63-189">(For executable components, that is, those whose **Deploy** method is set to **exec**, this can be an arbitrary Windows command line statement.)</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="f3e63-190">如果您對這個值使用空格字元，則會根據部署方法進行不同的處理。</span><span class="sxs-lookup"><span data-stu-id="f3e63-190">If you use space characters for this value, they will be handled differently depending on the deploy method.</span></span> <span data-ttu-id="f3e63-191">如果部署方法是 [可執行檔] ，系統會將空格解譯為命令列引數分隔符號，而非檔案名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="f3e63-191">If the deploy method is **exec**, spaces will be interpreted as command line argument separators and not as part of the file name.</span></span> <span data-ttu-id="f3e63-192">若為其他所有部署方法，系統會將空格解譯為檔案名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="f3e63-192">For all other deploy methods, spaces will be interpreted as part of the file name.</span></span>
  > 
  > 
* <span data-ttu-id="f3e63-193">**部署：** 指出開始部署時套用至元件之動作的方法。</span><span class="sxs-lookup"><span data-stu-id="f3e63-193">**Deploy:** Method that indicates the action applied to the component when the deployment is started.</span></span> <span data-ttu-id="f3e63-194">此屬性可為下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="f3e63-194">This can be one of the following values:</span></span>
  
  * <span data-ttu-id="f3e63-195">**複製：**元件會複製到 [目的地] 屬性所指定的目的地路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-195">**copy:** The component is copied to the destination path specified by the **To** property.</span></span>
  * <span data-ttu-id="f3e63-196">**可執行檔：**元件是可執行的 Windows 命令列陳述式，會在開始部署於 [目的地] 屬性所指定之路徑的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="f3e63-196">**exec:** The component is an executable Windows command line statement executed in the context of the path specified by the **To** property, at the time the deployment starts.</span></span>
  * <span data-ttu-id="f3e63-197">**無：** 開始部署時，不會對元件套用任何動作。</span><span class="sxs-lookup"><span data-stu-id="f3e63-197">**none:** No action is applied to the component when the deployment starts.</span></span>
  * <span data-ttu-id="f3e63-198">**Zip 檔：**元件會解壓縮到 [目的地] 屬性所指定的目的地路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-198">**zip:** The component is unzipped to the destination path specified by the **To** property.</span></span> <span data-ttu-id="f3e63-199">這個方法只適用於 [匯入] 屬性是 [Zip 檔] 時。</span><span class="sxs-lookup"><span data-stu-id="f3e63-199">This method is available only when the **Import** property is **zip**.</span></span>
* <span data-ttu-id="f3e63-200">**目的地：** 元件將要部署在虛擬機器上的目的地路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-200">**To:** Destination path on the virtual machine where the component will be deployed.</span></span> <span data-ttu-id="f3e63-201">此屬性可以使用 Windows 環境變數，而且檔案路徑是相對於 **approot**。</span><span class="sxs-lookup"><span data-stu-id="f3e63-201">Windows environment variables can be used in this property, and file paths are relative to **approot**.</span></span>

<span data-ttu-id="f3e63-202">若要新增元件，請按一下 [元件] 屬性頁中的 [新增] 按鈕，隨即就會開啟 [Azure 角色元件] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-202">To add a new component, click the **Add** button in the **Components** property page, and an **Azure Role Component** dialog will be opened.</span></span> <span data-ttu-id="f3e63-203">提供上述屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-203">Provide values for the properties which are described above.</span></span> 

<span data-ttu-id="f3e63-204">下圖顯示新增 WAR 元件的範例。</span><span class="sxs-lookup"><span data-stu-id="f3e63-204">The following shows an example for adding a new WAR component.</span></span>

![][ic719503]

<span data-ttu-id="f3e63-205">在部署到雲端 (而非計算模擬器) 時，如果您想要透過下載來部署元件，請確定您已核取 [在雲端中而非納入封裝時，透過下列方式部署]  。</span><span class="sxs-lookup"><span data-stu-id="f3e63-205">When deploying to the cloud (not the compute emulator), if you want to deploy the component from a download, ensure that **When in cloud, instead of including in the package, deploy from** is checked.</span></span> <span data-ttu-id="f3e63-206">如果您想要從 Azure 儲存體帳戶進行下載，請從 [儲存體帳戶] 下拉式清單選取儲存體帳戶 (您可以按一下 [帳戶] 連結以修改清單內容)，所選結果會部分填入 [URL] 欄位，請您自行填入 URL 的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="f3e63-206">If you want to download from your Azure storage account, select the storage account from the **Storage account** drop-down list (you can click the **Accounts** link to modify what is in the list), which will partially fill in the **URL** field, and then fill in the remaining portion of the URL.</span></span> <span data-ttu-id="f3e63-207">如果您不想使用 Azure 儲存體，請從 [儲存體帳戶] 下拉式清單選取 [(無)]，然後在 [URL] 欄位中輸入元件的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3e63-207">If you do not want to use Azure storage, select **(none)** from the **Storage account** drop-down list, and enter the URL to your component in the **URL** field.</span></span> <span data-ttu-id="f3e63-208">指定下列其中一個方法：</span><span class="sxs-lookup"><span data-stu-id="f3e63-208">Specify one of the following methods:</span></span>

* <span data-ttu-id="f3e63-209">**複製：**下載元件會複製到 [目的地目錄] 路徑所指定的目的地路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-209">**copy:** The download component is copied to the destination path specified by the **To Directory** path.</span></span>
* <span data-ttu-id="f3e63-210">**相同：**用於 [從下載部署] 和用於 [從封裝部署] 的方法相同。</span><span class="sxs-lookup"><span data-stu-id="f3e63-210">**same:** The same method used for **Deploy from download** as for **Deploy from package**.</span></span>
* <span data-ttu-id="f3e63-211">**Zip 檔：**下載元件會解壓縮到 [目的地目錄] 路徑所指定的目的地路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-211">**zip:** The download component is unzipped to the destination path specified by the **To Directory** path.</span></span>

<span data-ttu-id="f3e63-212">若要修改元件，請選取元件，然後按一下 [元件] 屬性頁中的 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3e63-212">To modify a component, select the component and click the **Edit** button in the **Components** property page.</span></span> <span data-ttu-id="f3e63-213">隨即會開啟對話方塊供您修改元件屬性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-213">A dialog will be opened allowing you to modify the component properties.</span></span> <span data-ttu-id="f3e63-214">按 [確定]  以儲存元件值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-214">Press **OK** to save the component values.</span></span>

<span data-ttu-id="f3e63-215">若要刪除元件，請選取元件，按一下 [元件] 屬性頁中的 [移除] 按鈕，然後按一下 [是]以確認刪除。</span><span class="sxs-lookup"><span data-stu-id="f3e63-215">To delete a component, select the component and click the **Remove** button in the **Components** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="f3e63-216">元件會依照所列順序進行處理。</span><span class="sxs-lookup"><span data-stu-id="f3e63-216">Components are processed in the order listed.</span></span> <span data-ttu-id="f3e63-217">使用 [上移] 和 [下移] 按鈕來排列順序。</span><span class="sxs-lookup"><span data-stu-id="f3e63-217">Use the **Move Up** and **Move Down** buttons to arrange the order.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e63-218">伺服器組態功能也需依賴元件。</span><span class="sxs-lookup"><span data-stu-id="f3e63-218">The server configuration feature relies on components as well.</span></span> <span data-ttu-id="f3e63-219">不移除對應的伺服器組態，就無法移除或編輯這些元件。</span><span class="sxs-lookup"><span data-stu-id="f3e63-219">Those components cannot be removed or edited without removing the corresponding server configuration.</span></span> <span data-ttu-id="f3e63-220">當您嘗試對這類元件進行變更時，將會提示您相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-220">You will be prompted about that when attempting to make changes to such components.</span></span>
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have the ability to enable or disable remote debugging, as well as create debug configurations, as shown in the following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a><span data-ttu-id="f3e63-221">端點屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-221">Endpoints properties</span></span>
<span data-ttu-id="f3e63-222">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-222">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Endpoints**.</span></span> <span data-ttu-id="f3e63-223">在這個對話方塊中，您可以建立端點以及編輯或移除端點，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f3e63-223">Within this dialog, you have the ability to create an endpoint, as well as edit or remove an endpoint, as shown in the following image.</span></span>

![][ic719505]

<span data-ttu-id="f3e63-224">若要新增端點，請按一下 [端點] 屬性頁中的 [新增] 按鈕，隨即就會開啟 [新增端點] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-224">To add an endpoint, click the **Add** button in the **Endpoints** property page, and an **Add Endpoint** dialog will be opened.</span></span>

![][ic710897]

<span data-ttu-id="f3e63-225">輸入端點名稱，選取類型 ([輸入]、[內部] 或 [執行個體輸入])，並指定公用和私人連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3e63-225">Enter a name for the endpoint, select the type (either **Input**, **Internal**, or **InstanceInput**), and specify the public and private port.</span></span> <span data-ttu-id="f3e63-226">按 [確定]  以儲存新的端點值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-226">Press **OK** to save the new endpoint values.</span></span>

<span data-ttu-id="f3e63-227">根據端點的類型，您可以使用的連接埠範圍如下：</span><span class="sxs-lookup"><span data-stu-id="f3e63-227">Depending on the type of endpoint, you may use port ranges as follows:</span></span>

* <span data-ttu-id="f3e63-228">若為輸入執行個體端點，公用連接埠可以是連接埠範圍 (例如 **2000-2010**)，但私人連接埠是固定值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-228">For an input instance endpoint, the public port can be a range of ports (for example **2000-2010**) and the private port is a fixed value.</span></span>
* <span data-ttu-id="f3e63-229">若為內部端點，則不會使用公用連接埠，而且私用連接埠可以是範圍、保留空白，或設為星號以表示它會由 Azure 自動設定。</span><span class="sxs-lookup"><span data-stu-id="f3e63-229">For an internal endpoint, the public port is not used, and the private port can be a range, or left blank or set to an asterisk to indicate it is automatically set by Azure.</span></span>
* <span data-ttu-id="f3e63-230">若為輸入端點，則公用連接埠只能是固定值，但私用連接埠可以是固定值、保留空白，或設為星號以表示它會由 Azure 自動設定。</span><span class="sxs-lookup"><span data-stu-id="f3e63-230">For input endpoints, the public port can only be a fixed value, and the private port can be a fixed value, or left blank or set to an asterisk to indicate it is automatically set by Azure.</span></span>

<span data-ttu-id="f3e63-231">如果您想要使用單一連接埠號碼而非某個範圍，請將代表範圍結尾的文字方塊保留空白。</span><span class="sxs-lookup"><span data-stu-id="f3e63-231">If you want to use a single port number instead of a range, leave the text box for the end of the range blank.</span></span>

<span data-ttu-id="f3e63-232">針對設為自動設定的連接埠，如果您需要確定在執行階段實際使用的連接埠，則應用程式可以使用 [com.microsoft.windowsazure.serviceruntime 封裝摘要][com.microsoft.windowsazure.serviceruntime package summary]中所記載的「Azure 服務執行階段 API」。</span><span class="sxs-lookup"><span data-stu-id="f3e63-232">For ports that are set to automatic, if you need to determine which port is actually used during runtime, your application can use the Azure Service Runtime API, which is documented in the [com.microsoft.windowsazure.serviceruntime package summary][com.microsoft.windowsazure.serviceruntime package summary].</span></span>

<!-- To see how instance input endpoints can be used to help with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

<span data-ttu-id="f3e63-233">若要修改端點，請選取端點，然後按一下 [端點] 屬性頁中的 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3e63-233">To modify an endpoint, select the endpoint and click the **Edit** button in the **Endpoints** property page.</span></span> <span data-ttu-id="f3e63-234">隨即會開啟對話方塊供您修改端點名稱、類型和公用與私人連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3e63-234">A dialog will be opened allowing you to modify the endpoint name, type, and public and private ports.</span></span> <span data-ttu-id="f3e63-235">按 [確定]  以儲存修改過的端點值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-235">Press **OK** to save the modified endpoint values.</span></span>

<span data-ttu-id="f3e63-236">若要刪除端點，請選取端點，按一下 [端點] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。</span><span class="sxs-lookup"><span data-stu-id="f3e63-236">To delete an endpoint, select the endpoint and click the **Remove** button in the **Endpoints** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="f3e63-237">為了正確設定使用者對某個角色所啟用的某些功能 (例如快取、工作階段親和性或 SSL 卸載)，工具組可能會自動設定隨使用者定義的端點一起列出的特殊端點。</span><span class="sxs-lookup"><span data-stu-id="f3e63-237">In order to properly configure some of the features (such as Caching, Session Affinity, or SSL offloading) enabled by the user on a role, the toolkit may automatically configure special endpoints that will be listed along with user-defined endpoints.</span></span> <span data-ttu-id="f3e63-238">只要啟用關聯的功能，工具組就會防止使用者編輯或刪除這類自動產生的端點。</span><span class="sxs-lookup"><span data-stu-id="f3e63-238">The toolkit prevents the user from editing or deleting such automatically generated endpoints as long as the associated feature is enabled.</span></span>

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a><span data-ttu-id="f3e63-239">環境變數屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-239">Environment variables properties</span></span>
<span data-ttu-id="f3e63-240">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [環境變數]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-240">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Environment Variables**.</span></span> <span data-ttu-id="f3e63-241">在這個對話方塊中，您可以建立環境變數以及修改或移除環境變數，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f3e63-241">Within this dialog, you have the ability to create an environment variable, as well as modify or remove an environment variable, as shown in the following image.</span></span>

![][ic719506]

<span data-ttu-id="f3e63-242">當角色啟動時，啟動指令碼就能夠使用環境變數。</span><span class="sxs-lookup"><span data-stu-id="f3e63-242">Environment variables are available to your startup script when the role starts.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e63-243">在指定環境變數時請記住，您的部署將會發佈至 Windows 虛擬機器，因此您的環境變數必須適用於 Windows 架構的作業系統。</span><span class="sxs-lookup"><span data-stu-id="f3e63-243">When specifying environment variables, keep in mind that your deployment will be published to a Windows virtual machine, so your environment variables must be valid for a Windows-based operating system.</span></span>
> 
> 

<span data-ttu-id="f3e63-244">為了舉例說明角色啟動時可供使用的環境變數，請按一下 [新增] 按鈕以建立新的環境變數。</span><span class="sxs-lookup"><span data-stu-id="f3e63-244">As an example of an environment variable being available when the role starts, create a new environment variable by clicking the **Add** button.</span></span> <span data-ttu-id="f3e63-245">下圖顯示我們將會建立名為 **MyRoleVersion** 的環境變數，並對其指派 **1.0** 的值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-245">The following shows an environment variable named **MyRoleVersion** being created and assigned the value **1.0**.</span></span>

![][ic659268]

<span data-ttu-id="f3e63-246">在 jsp 程式碼中，您可以使用 `System.getenv` 方法來顯示值：</span><span class="sxs-lookup"><span data-stu-id="f3e63-246">Within your jsp code, you could display the value using the `System.getenv` method:</span></span>

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

<span data-ttu-id="f3e63-247">當應用程式執行時會產生以下輸出：</span><span class="sxs-lookup"><span data-stu-id="f3e63-247">Resulting in this output when your application runs:</span></span>

![][ic552233]

<span data-ttu-id="f3e63-248">若要修改環境變數，請選取環境變數，然後按一下 [環境變數] 屬性頁中的 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3e63-248">To modify an environment variable, select the environment variable and click the **Edit** button in the **Environment Variables** property page.</span></span> <span data-ttu-id="f3e63-249">隨即會開啟對話方塊供您修改環境變數屬性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-249">A dialog will be opened allowing you to modify the environment variable properties.</span></span> <span data-ttu-id="f3e63-250">按 [確定]  以儲存環境變數值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-250">Press **OK** to save the environment variable values.</span></span>

<span data-ttu-id="f3e63-251">若要刪除環境變數，請選取環境變數，按一下 [環境變數] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。</span><span class="sxs-lookup"><span data-stu-id="f3e63-251">To delete an environment variable, select the environment variable and click the **Remove** button in the **Environment Variables** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="f3e63-252">為了正確設定使用者對某個角色所啟用的某些功能 (例如伺服器組態、遠端偵錯或本機儲存體)，工具組可能會自動設定隨使用者定義的環境變數一起列出的特殊環境變數。</span><span class="sxs-lookup"><span data-stu-id="f3e63-252">In order to properly configure some of the features (such as Server Configuration, Remote Debugging or Local Storage) enabled by the user on a role, the toolkit may automatically configure special environment variables that will be listed along with user-defined environment variables.</span></span> <span data-ttu-id="f3e63-253">只要啟用關聯的功能，工具組就會防止使用者編輯或刪除這類自動產生的環境變數。</span><span class="sxs-lookup"><span data-stu-id="f3e63-253">The toolkit prevents the user from editing or deleting such automatically generated environment variables as long as the associated feature is enabled.</span></span>

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a><span data-ttu-id="f3e63-254">負載平衡/工作階段親和性 (也稱為「黏性工作階段」) 屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-254">Load balancing / session affinity (a.k.a "sticky sessions") properties</span></span>
<span data-ttu-id="f3e63-255">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [負載平衡]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-255">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Load Balancing**.</span></span> <span data-ttu-id="f3e63-256">在這個對話方塊中，您可以啟用或停用工作階段親和性，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f3e63-256">Within this dialog, you have the ability to enable or disable session affinity, as shown in the following image.</span></span>

![][ic719492]

<span data-ttu-id="f3e63-257">如需相關資訊，請參閱[工作階段親和性][Session Affinity]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-257">For related information, see [Session Affinity][Session Affinity].</span></span> <span data-ttu-id="f3e63-258">另外，請注意這項功能在 SSL 卸載情況下的行為，如 [SSL 卸載][SSL Offloading]所述。</span><span class="sxs-lookup"><span data-stu-id="f3e63-258">Also, note this feature's behavior in the context of SSL offloading, as described at [SSL Offloading][SSL Offloading].</span></span>

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a><span data-ttu-id="f3e63-259">本機儲存體屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-259">Local storage properties</span></span>
<span data-ttu-id="f3e63-260">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [本機儲存體]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-260">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="f3e63-261">在這個對話方塊中，您可以建立、修改或移除正在執行應用程式之虛擬機器的暫存本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="f3e63-261">Within this dialog, you have the ability to create, modify or remove temporary local storage for the virtual machine that is running your application.</span></span> <span data-ttu-id="f3e63-262">您可以針對本機儲存體大小，以及回收角色時是否保留其內容設定特定值，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f3e63-262">Specific values can be set for the size of the local storage, as well as whether the contents are preserved when the role is recycled, as shown in the following image.</span></span>

![][ic719508]

<span data-ttu-id="f3e63-263">您也可以選擇性地指定對應至本機儲存體的環境變數。</span><span class="sxs-lookup"><span data-stu-id="f3e63-263">You can also optionally specify an environment variable that corresponds to the local storage.</span></span>

<span data-ttu-id="f3e63-264">根據預設，所有部署至 Azure 的項目皆會放置 (和解壓縮) 在角色執行個體的 **approot** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3e63-264">By default, everything that you deploy into Azure is placed (and unzipped) in the **approot** folder of the role instance.</span></span> <span data-ttu-id="f3e63-265">雖然該資料夾可容納大多數的簡單部署 (即使在解壓縮之後)，但配置給 **approot** 目錄的空間實際上有限且未明確定義 (根據經驗合理推估是小於 1 GB)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-265">While most simple deployments will fit there even after unzipping, the space allocated for the **approot** directory is limited and not well-defined (less than 1 GB is a reasonable rule of thumb).</span></span> <span data-ttu-id="f3e63-266">因此，為確保 Azure 配置足夠的磁碟空間來容納 **approot** 資料夾可能放不下的較大部署，您應該使用 [本機儲存體] 對話方塊設定本機儲存資源。</span><span class="sxs-lookup"><span data-stu-id="f3e63-266">Therefore, to ensure Azure allocates sufficient disk space for larger deployments that might not fit in the **approot** folder, you should set up a local storage resource using the **Local Storage** dialog.</span></span> <span data-ttu-id="f3e63-267">若要了解這項設定的簡單做法，請參閱[部署大型部署][Deploying Large Deployments]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-267">For an easy way to do this, see [Deploying Large Deployments][Deploying Large Deployments].</span></span>

<span data-ttu-id="f3e63-268">您可以使用由 Eclipse 工具組自動關聯至資源的環境變數，從啟動指令碼 (例如 **startup.cmd**) 輕鬆參考儲存體資源，如 [本機儲存體] 對話方塊所示。</span><span class="sxs-lookup"><span data-stu-id="f3e63-268">You can easily reference the storage resource from startup scripts (for example, your **startup.cmd**) using the environment variable automatically associated by the Eclipse toolkit with the resource, as shown in the **Local Storage** dialog.</span></span> <span data-ttu-id="f3e63-269">該環境變數會包含您已在執行啟動指令碼時設定之本機資源的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-269">That environment variable will contain the full path of the local resource you've configured at the time your startup script is executed.</span></span> 

<span data-ttu-id="f3e63-270">若要修改本機儲存資源，請選取本機儲存資源，然後按一下 [本機儲存體] 屬性頁中的 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3e63-270">To modify a local storage resource, select the local storage resource and click the **Edit** button in the **Local Storage** property page.</span></span> <span data-ttu-id="f3e63-271">隨即會開啟對話方塊供您修改本機儲存資源屬性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-271">A dialog will be opened allowing you to modify the local storage resource properties.</span></span> <span data-ttu-id="f3e63-272">按 [確定]  以儲存本機儲存資源的值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-272">Press **OK** to save the local storage resource values.</span></span>

<span data-ttu-id="f3e63-273">若要刪除本機儲存資源，請選取本機儲存資源，按一下 [本機儲存] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。</span><span class="sxs-lookup"><span data-stu-id="f3e63-273">To delete a local storage resource, select the local storage resource and click the **Remove** button in the **Local Storage** property page, and then click **Yes** to confirm the deletion.</span></span>

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a><span data-ttu-id="f3e63-274">伺服器組態屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-274">Server configuration properties</span></span>
<span data-ttu-id="f3e63-275">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [伺服器組態]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-275">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Server Configuration**.</span></span> <span data-ttu-id="f3e63-276">在這個對話方塊中，您可以新增、移除和修改部署所使用的 JDK 和 Java 應用程式伺服器，以及新增或移除部署所使用的應用程式 (例如 WAR、JAR 或 EAR 檔案)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-276">Within this dialog, you have the ability to add, remove, and modify the JDK and Java application server used by your deployment, as well as add or remove the applications (such as WAR, JAR or EAR files) used by your deployment.</span></span>

### <a name="jdk-configuration"></a><span data-ttu-id="f3e63-277">JDK 組態</span><span class="sxs-lookup"><span data-stu-id="f3e63-277">JDK configuration</span></span>
<span data-ttu-id="f3e63-278">這個對話方塊可讓您指定要用於部署的 JDK 封裝。</span><span class="sxs-lookup"><span data-stu-id="f3e63-278">This dialog allows you to specify the JDK package to use for your deployment.</span></span> <span data-ttu-id="f3e63-279">如果您在 Windows 上使用 Eclipse，您可以指定當 JDK 封裝是在 Azure 模擬器中執行時，讓此封裝在本機上使用，而且您可以選擇將該本機安裝部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f3e63-279">If you are using Eclipse on Windows, you can specify the JDK package to use locally when running in the Azure emulator and you have the option to deploy that local installation to Azure.</span></span> <span data-ttu-id="f3e63-280">在非 Windows 作業系統上則不適用模擬器 JDK 設定，而且您無法部署本機安裝的 JDK，因為它與 Windows 不相容。</span><span class="sxs-lookup"><span data-stu-id="f3e63-280">On non-Windows operating systems, the emulator JDK setting is not applicable and you cannot deploy the locally installed JDK since it is not compatible with Windows.</span></span> <span data-ttu-id="f3e63-281">不過，無論您使用什麼作業系統，一律都可以選擇使用第三方 JDK 封裝來部署至 Azure，或從其他下載位置指向您自己的 Windows 相容 JDK 封裝。</span><span class="sxs-lookup"><span data-stu-id="f3e63-281">However, regardless of the operating system that you are using, you can always choose among the 3rd party JDK packages to deploy to Azure, or point at your own Windows-compatible JDK package from an alternate download location.</span></span>

<span data-ttu-id="f3e63-282">以下範例說明如何在 Windows 上指定 JDK：</span><span class="sxs-lookup"><span data-stu-id="f3e63-282">The following is an example of how you can specify a JDK on Windows:</span></span>

![][ic780647]

<span data-ttu-id="f3e63-283">如果您在 Windows 上使用 Eclipse，您可以指定用於計算模擬器的 JDK，若要進行指定，請確定已勾選 [模擬器部署] 區段中的 [使用此檔案路徑中的 JDK 以進行本機測試]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-283">If you are using Eclipse on Windows, you can specify a JDK to use with the compute emulator; to do so, ensure **Use the JDK from this file path for testing locally** is checked in the **Emulator deployment** section.</span></span> <span data-ttu-id="f3e63-284">然後，指定 JDK 的本機路徑，如果系統未自動選取您想使用的 JDK，您可以瀏覽至不同的 JDK。</span><span class="sxs-lookup"><span data-stu-id="f3e63-284">Then, specify the local path to your JDK; you can browse to different JDK if the one you want to use is not selected automatically.</span></span> <span data-ttu-id="f3e63-285">您也可以選擇將 JDK 部署至 Azure 雲端服務，若要這樣做，請選取 [雲端部署] 區段中的 [部署本機 JDK (自動上傳至雲端儲存體)] 選項。</span><span class="sxs-lookup"><span data-stu-id="f3e63-285">You also have the option to deploy your JDK to your Azure cloud service; to do so, select the **Deploy my local JDK (auto-upload to cloud storage)** option in the **Cloud deployment** section.</span></span>

<span data-ttu-id="f3e63-286">附註：在非 Windows 作業系統中，無法使用 [模擬器部署] 設定和 [部署本機 JDK] 選項。</span><span class="sxs-lookup"><span data-stu-id="f3e63-286">Note: On non-Windows operating systems, the **Emulator deployment** settings and the **Deploy my local JDK** option are not available.</span></span> <span data-ttu-id="f3e63-287">下列範例說明如何在 Mac 或其他支援的非 Windows 作業系統上指定 JDK：</span><span class="sxs-lookup"><span data-stu-id="f3e63-287">The following example illustrates specifying a JDK on a Mac or other supported non-Windows operating system:</span></span>

![][ic789643]

<span data-ttu-id="f3e63-288">不論您所在的作業系統為何，JDK 封裝的來源和類型都有下列兩個 [雲端部署]  選項：</span><span class="sxs-lookup"><span data-stu-id="f3e63-288">Regardless of the operating system you are on, you have the following two **Cloud deployment** options for the source and type of your JDK package:</span></span>

* <span data-ttu-id="f3e63-289">**部署 Azure 提供的第三方 JDK 封裝**</span><span class="sxs-lookup"><span data-stu-id="f3e63-289">**Deploy a 3rd party JDK package available on Azure**</span></span> 
* <span data-ttu-id="f3e63-290">**從自訂下載部署**</span><span class="sxs-lookup"><span data-stu-id="f3e63-290">**Deploy from a custom download**</span></span> 

<span data-ttu-id="f3e63-291">如果您使用 [部署可從 Azure 取得的第三方 JDK 封裝]  選項：</span><span class="sxs-lookup"><span data-stu-id="f3e63-291">If you are using the **Deploy a 3rd party JDK package available from Azure** option:</span></span>

1. <span data-ttu-id="f3e63-292">核取名為 [部署可從 Azure 取得的第三方 JDK 封裝] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-292">Check the checkbox named **Deploy a 3rd party JDK package available from Azure**.</span></span>
2. <span data-ttu-id="f3e63-293">從下拉式清單中，選取 Azure 提供的第三方 JDK 封裝。</span><span class="sxs-lookup"><span data-stu-id="f3e63-293">From the drop-down list, select the 3rd party JDK package that is available on Azure.</span></span>
3. <span data-ttu-id="f3e63-294">您**JDK**  索引標籤看起來類似下列的 Windows:![][ic780648]和看起來會類似下列的 Mac OS 或其他支援的非 Windows 作業系統：![][ic789643]</span><span class="sxs-lookup"><span data-stu-id="f3e63-294">Your **JDK** tab will look similar to the following on Windows:  ![][ic780648] And it will look similar to the following on Mac OS or other supported non-Windows operating systems:  ![][ic789643]</span></span>
4. <span data-ttu-id="f3e63-295">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f3e63-295">Click **OK** to save your changes.</span></span>
5. <span data-ttu-id="f3e63-296">當系統提示您接受第三方 JDK 封裝提供者所提出的授權合約時，請檢閱授權條款。</span><span class="sxs-lookup"><span data-stu-id="f3e63-296">When prompted to accept the license agreement from the 3rd party JDK package provider, review the license terms.</span></span> <span data-ttu-id="f3e63-297">假設您接受這些條款，請按一下 [是] 以關閉 [接受授權合約] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-297">Assuming you accept the terms, click **Yes** to close the **Accept license agreement** dialog.</span></span>
    <span data-ttu-id="f3e63-298">請注意，您可以自訂 [部署可從 Azure 取得的第三方 JDK 封裝] 選項的下拉式清單中要出現哪些項目的基礎邏輯。</span><span class="sxs-lookup"><span data-stu-id="f3e63-298">Note that the underlying logic for which items appear in the drop-down list for the **Deploy a 3rd party JDK package available from Azure** option can be customized.</span></span> <span data-ttu-id="f3e63-299">若要自訂出現的項目，請在 [JDK] 對話方塊中按一下 [自訂] 連結。</span><span class="sxs-lookup"><span data-stu-id="f3e63-299">To customize the items, in the **JDK** dialog, click the **Customize** link.</span></span> <span data-ttu-id="f3e63-300">此動作將會關閉 [JDK] 屬性頁，並在 Eclipse 中開啟 **componentsets.xml** 檔案，然後您就可以視需要進行修改。</span><span class="sxs-lookup"><span data-stu-id="f3e63-300">This will close the **JDK** property page and open the **componentsets.xml** file in Eclipse, which you can then modify as needed.</span></span> <span data-ttu-id="f3e63-301">**componentsets.xml** 的說明文件隨附於 **componentsets.xml** 檔案本身。</span><span class="sxs-lookup"><span data-stu-id="f3e63-301">Documentation for **componentsets.xml** is included in the **componentsets.xml** file itself.</span></span>

<span data-ttu-id="f3e63-302">如果您使用 [從自訂下載部署 JDK]  選項：</span><span class="sxs-lookup"><span data-stu-id="f3e63-302">If you are using the **Deploy a JDK from a custom download** option:</span></span>

1. <span data-ttu-id="f3e63-303">建立 JDK 安裝目錄的 ZIP 檔，確保目錄節點本身是 ZIP 結構的子系，而非其內容的子系。</span><span class="sxs-lookup"><span data-stu-id="f3e63-303">Create a ZIP of your JDK installation directory, ensuring that the directory node itself is the child of the ZIP structure, and not its contents.</span></span> <span data-ttu-id="f3e63-304">記下目錄名稱，因為您稍後會需要它，並請記住此 JDK 安裝將會部署到 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3e63-304">Take note of the name of the directory, as you will need it later, and keep in mind this JDK installation will be deployed to a Windows virtual machine.</span></span>
2. <span data-ttu-id="f3e63-305">以 blob 的形式將 ZIP 檔上傳到 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3e63-305">Upload the ZIP into your Azure storage account as a blob.</span></span> <span data-ttu-id="f3e63-306">若要這麼做，您可以使用外部取得的工具來將 blob 上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="f3e63-306">You can do this using an externally available tool for uploading blobs to Azure storage.</span></span> <span data-ttu-id="f3e63-307">建議您使用私人 blob。</span><span class="sxs-lookup"><span data-stu-id="f3e63-307">It is recommended to use a private blob.</span></span> <span data-ttu-id="f3e63-308">記下 ZIP 內容的 blob URL。</span><span class="sxs-lookup"><span data-stu-id="f3e63-308">Take note of the blob URL of the ZIP contents.</span></span>
3. <span data-ttu-id="f3e63-309">核取名為 [從自訂下載部署 JDK] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-309">Check the checkbox named **Deploy a JDK from a custom download**.</span></span>
    <span data-ttu-id="f3e63-310">如果您想要從 Azure 儲存體帳戶進行下載，請從 [儲存體帳戶] 下拉式清單選取儲存體帳戶 (您可以按一下 [帳戶] 連結以修改清單內容)，所選結果會部分填入 [URL] 欄位，請您自行填入 URL 的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="f3e63-310">If you want to download from your Azure storage account, select the storage account from the **Storage account** drop-down list (you can click the **Accounts** link to modify what is in the list), which will partially fill in the **URL** field, and then fill in the remaining portion of the URL.</span></span> <span data-ttu-id="f3e63-311">如果您不想使用 Azure 儲存體，請從 [儲存體帳戶] 下拉式清單選取 [(無)]，然後在 [URL] 欄位中輸入 JDK 下載的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3e63-311">If you do not want to use Azure storage, select **(none)** from the **Storage account** drop-down list, and enter the URL to your JDK download in the **URL** field.</span></span> <span data-ttu-id="f3e63-312">如果使用 Azure 儲存體，則 URL 中的 blob 名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="f3e63-312">If using Azure storage, blob names in the URL must be lowercase.</span></span>
4. <span data-ttu-id="f3e63-313">確定 [JAVA_HOME] 文字方塊有參考正確的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="f3e63-313">Ensure that the **JAVA_HOME** textbox refers to the correct directory name.</span></span> <span data-ttu-id="f3e63-314">根據預設，它會參考與您為本機使用所選擇之值相同的 JDK 目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="f3e63-314">By default, it will reference the same JDK directory name as the value you chose for your local use.</span></span> <span data-ttu-id="f3e63-315">但如果 ZIP 檔中包含的目錄有不同名稱 (例如由於使用不同版本)，請相應地更新 [JAVA_HOME] 文字方塊中的目錄名稱，因為此設定會用於雲端 (而非計算模擬器)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-315">But if the directory contained in the ZIP has a different name (for example, due to using a different version), update the directory name in the **JAVA_HOME** textbox accordingly, since this setting will be used in the cloud (not in the compute emulator).</span></span>
5. <span data-ttu-id="f3e63-316">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f3e63-316">Click **OK** to save your changes.</span></span>

<span data-ttu-id="f3e63-317">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="f3e63-317">That's it.</span></span> <span data-ttu-id="f3e63-318">現在，當您針對雲端進行建置時，您會發現封裝大小變小很多，建置程序所需的時間通常較少，而且部署本身在發佈至雲端時所需的時間也應該會變少。</span><span class="sxs-lookup"><span data-stu-id="f3e63-318">Now, when you build for the cloud, you will notice the package size will be much smaller, the build process should typically take less time, and the deployment itself when you publish to the cloud should also take less time.</span></span> <span data-ttu-id="f3e63-319">請注意，只有當應用程式部署在雲端時，[部署本機 JDK (自動上傳至雲端儲存體)] 或 [從自訂下載部署 JDK] 選項才有作用。</span><span class="sxs-lookup"><span data-stu-id="f3e63-319">Note that the **Deploy my local JDK (auto-upload to cloud storage)** or **Deploy a JDK from a custom download** options are in effect only when your application is deployed in the cloud.</span></span> <span data-ttu-id="f3e63-320">在使用計算模擬器時，這兩個選項不會有任何作用，當您部署至計算模擬器時，仍然會使用本機版本的元件。</span><span class="sxs-lookup"><span data-stu-id="f3e63-320">They have no effect on your compute emulator experience; the local version of the components will still be used when you deploy to the compute emulator.</span></span> 

### <a name="server-configuration"></a><span data-ttu-id="f3e63-321">伺服器組態</span><span class="sxs-lookup"><span data-stu-id="f3e63-321">Server configuration</span></span>
<span data-ttu-id="f3e63-322">以下範例說明如何指定應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3e63-322">The following is an example of how you can specify an application server.</span></span>

![][ic796926]

<span data-ttu-id="f3e63-323">確認已選取 [部署此類型的伺服器]  核取方塊，然後選擇您想要使用的應用程式伺服器類型。</span><span class="sxs-lookup"><span data-stu-id="f3e63-323">Verify that the **Deploy a server of this type** checkbox is selected, and then choose the type of application server you want to use.</span></span>

<span data-ttu-id="f3e63-324">若要指定要用於雲端部署的伺服器，您可以利用下列選項：</span><span class="sxs-lookup"><span data-stu-id="f3e63-324">For specifying a server to use for cloud deployment, you can take advantage of the following options:</span></span>

1. <span data-ttu-id="f3e63-325">**部署 Azure 提供的第三方伺服器** - 這個選項特別適用於開發/測試案例，因為這種案例的優先考量是部署效率和簡易性，因此伺服器不需要自訂組態。</span><span class="sxs-lookup"><span data-stu-id="f3e63-325">**Deploy a 3rd party server available on Azure** - this is especially applicable in dev/test scenarios where deployment efficiency and simplicity is a priority and the server does not require a custom configuration.</span></span> <span data-ttu-id="f3e63-326">或者，當您想要使用其中一部伺服器做為起點，但您在部署的啟動邏輯中加入了適當的伺服器自訂步驟。</span><span class="sxs-lookup"><span data-stu-id="f3e63-326">Or when you want to use one of those servers as the starting point but you include appropriate server customization steps in your deployment's startup logic.</span></span>
2. <span data-ttu-id="f3e63-327">**從自訂下載部署** - 這個選項特別適用於生產案例，前提示您有為了在雲端中使用而特別準備及設定的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3e63-327">**Deploy from a custom download** - this is especially applicable in production scenarios when you have a specially prepared and configured server that you want to use in the cloud.</span></span>
3. <span data-ttu-id="f3e63-328">**部署本機伺服器安裝** - 這個選項特別適用於如果本機伺服器安裝已針對您的用途進行自訂設定。</span><span class="sxs-lookup"><span data-stu-id="f3e63-328">**Deploy my local server installation** - this is especially applicable in if your local server installation is already custom-configured for your use.</span></span> <span data-ttu-id="f3e63-329">如果您選擇此選項，則必須同時在下方的 [本機伺服器路徑]  文字方塊中指定本機伺服器的路徑。</span><span class="sxs-lookup"><span data-stu-id="f3e63-329">If you choose this option, you must also specify your local server's path in the **Local server path** text box below.</span></span>

<span data-ttu-id="f3e63-330">如果您使用 [部署 Azure 提供的第三方伺服器]  選項：</span><span class="sxs-lookup"><span data-stu-id="f3e63-330">If you are using the **Deploy a 3rd party server available on Azure** option:</span></span>

1. <span data-ttu-id="f3e63-331">核取名為 [部署 Azure 提供的第三方伺服器] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-331">Check the checkbox named **Deploy a 3rd party server available on Azure**.</span></span>
2. <span data-ttu-id="f3e63-332">從下拉式功能表中，選取想要在雲端中搭配部署使用的伺服器軟體。</span><span class="sxs-lookup"><span data-stu-id="f3e63-332">From the dropdown menu, select the desired server software to use with your deployment in the cloud.</span></span> <span data-ttu-id="f3e63-333">請注意，如果您先前已指定要使用的伺服器類型，您會遭到限制而只能選擇與該伺服器類型位於相同系列中的雲端伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3e63-333">Note, if you already specified a type of server to use earlier, you will be limited to choosing only a cloud server that is in the same family as that server type.</span></span> <span data-ttu-id="f3e63-334">但如果您沒有選擇伺服器類型，則可以選擇 Azure 上目前提供的任何伺服器，而且系統會自動為您選取伺服器類型。</span><span class="sxs-lookup"><span data-stu-id="f3e63-334">But if you did not choose a server type, you can choose from any of the servers that are currently available on Azure and the server type will be automatically selected for you.</span></span>
3. <span data-ttu-id="f3e63-335">按一下 [確定]  以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f3e63-335">Click **OK** to save your changes.</span></span>

<span data-ttu-id="f3e63-336">如果使用 [從自訂下載部署]  選項：</span><span class="sxs-lookup"><span data-stu-id="f3e63-336">If using the **Deploy from a custom download** option:</span></span>

1. <span data-ttu-id="f3e63-337">確定您已根據上述步驟選取伺服器類型。</span><span class="sxs-lookup"><span data-stu-id="f3e63-337">Make sure that you have already selected a server type according to the preceding steps.</span></span> <span data-ttu-id="f3e63-338">這會告訴外掛程式如何從自訂下載部署伺服器，因為伺服器必須來自與所選伺服器類型相同的系列。</span><span class="sxs-lookup"><span data-stu-id="f3e63-338">This tells the plugin how to deploy the server from your custom download, as it must be from the same family as your selected server type.</span></span>
2. <span data-ttu-id="f3e63-339">核取名為 [部署可從 Azure 取得的第三方 JDK 封裝] **從自訂下載部署**。</span><span class="sxs-lookup"><span data-stu-id="f3e63-339">Check the checkbox named **Deploy from a custom download**.</span></span>
    <span data-ttu-id="f3e63-340">如果您想要從 Azure 儲存體帳戶進行下載，請從 [儲存體帳戶] 下拉式清單選取儲存體帳戶 (您可以按一下 [帳戶] 連結以修改清單內容)，所選結果會部分填入 [URL] 欄位，請您自行填入伺服器下載 ZIP 檔之 URL 的其餘部分 (在使用 Azure 儲存體時，URL 中的 blob 名稱必須是小寫)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-340">If you want to download from your Azure storage account, select the storage account from the **Storage account** drop-down list (you can click the **Accounts** link to modify what is in the list), which will partially fill in the **URL** field, and then fill in the remaining portion of the URL to your server download ZIP (when using Azure storage, blob names in the URL must be lowercase).</span></span> <span data-ttu-id="f3e63-341">如果您不想使用 Azure 儲存體，請從 [儲存體帳戶] 下拉式清單選取 [(無)]，然後在 [URL] 欄位中輸入伺服器下載 ZIP 檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3e63-341">If you do not want to use Azure storage, select **(none)** from the **Storage account** drop-down list, and enter the URL to your server download ZIP in the **URL** field.</span></span> <span data-ttu-id="f3e63-342">ZIP 檔會包含代表應用程式伺服器安裝目錄的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3e63-342">The ZIP would contain a child folder representing your application server installation directory.</span></span> <span data-ttu-id="f3e63-343">例如，如果您使用 Apache Tomcat 7.0.35 的 ZIP 檔，ZIP 檔內會有代表安裝目錄的子資料夾，例如 **apache-tomcat-7.0.35**。</span><span class="sxs-lookup"><span data-stu-id="f3e63-343">For example, if you are using a zip for Apache Tomcat 7.0.35, within the zip would be the child folder representing the installation directory, such as **apache-tomcat-7.0.35**.</span></span> 
3. <span data-ttu-id="f3e63-344">指定主目錄環境變數的值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-344">Specify the value for the home directory environment variable.</span></span> <span data-ttu-id="f3e63-345">它會預設為用於本機應用程式伺服器的值 (如果有的話)，但如果您的雲端應用程式伺服器與本機應用程式伺服器不同，則可以指定不同的值。</span><span class="sxs-lookup"><span data-stu-id="f3e63-345">It will default to the value used for your local application server, if any, but you can specify a different value if your cloud application server is different from your local application server.</span></span> <span data-ttu-id="f3e63-346">不過，您必須確定雲端應用程式伺服器屬於與先前所選伺服器類型相同的系列。</span><span class="sxs-lookup"><span data-stu-id="f3e63-346">However, you need to make sure that your cloud application server is of the same family as the server type selected earlier.</span></span>
    <span data-ttu-id="f3e63-347">如果您日後更新雲端應用程式伺服器 ZIP 檔，您可以手動變更主目錄設定，或讓它再次符合本機設定 (如果您也變更了本機應用程式伺服器)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-347">If you update your cloud application server zip in the future, you can manually change the home directory setting, or, to have it again match your local setting (if you changed your local application server too).</span></span>
4. <span data-ttu-id="f3e63-348">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f3e63-348">Click **OK** to save your changes.</span></span>

<span data-ttu-id="f3e63-349">您可以自訂 [伺服器組態] 屬性頁的 [伺服器] 索引標籤中要出現哪些項目的基礎邏輯。</span><span class="sxs-lookup"><span data-stu-id="f3e63-349">The underlying logic for which items appear in the **Server** tab of the **Server Configuration** property page can be customized.</span></span> <span data-ttu-id="f3e63-350">如果您需要的不是預設值，或如果您想要新增其他伺服器，就可能需要這項進階功能。</span><span class="sxs-lookup"><span data-stu-id="f3e63-350">This is an advanced feature that you might need if your needs extend beyond the default values or if you want to add other servers.</span></span> <span data-ttu-id="f3e63-351">若要自訂此邏輯，請在 [伺服器] 對話方塊中按一下 [自訂] 連結。</span><span class="sxs-lookup"><span data-stu-id="f3e63-351">To customize the logic, in the **Server** dialog, click the **Customize** link.</span></span> <span data-ttu-id="f3e63-352">此動作將會關閉 [伺服器組態] 屬性頁，並在 Eclipse 中開啟 **componentsets.xml** 檔案，然後您就可以視需要進行修改，以擴充伺服器組態範本。</span><span class="sxs-lookup"><span data-stu-id="f3e63-352">This will close the **Server Configuration** property page and open the **componentsets.xml** file in Eclipse, which you can then modify as needed to extend the server configuration template.</span></span> <span data-ttu-id="f3e63-353">**componentsets.xml** 的說明文件隨附於 **componentsets.xml** 檔案本身。</span><span class="sxs-lookup"><span data-stu-id="f3e63-353">Documentation for **componentsets.xml** is included in the **componentsets.xml** file itself.</span></span>

<span data-ttu-id="f3e63-354">如果您使用 [部署本機伺服器 (自動上傳至雲端儲存體)]  選項：</span><span class="sxs-lookup"><span data-stu-id="f3e63-354">If you are using the **Deploy my local server (auto-upload to cloud storage)** option:</span></span>

1. <span data-ttu-id="f3e63-355">核取名為 [部署本機伺服器 (自動上傳至雲端儲存體)] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f3e63-355">Check the checkbox named **Deploy my local server (auto-upload to cloud storage)**.</span></span>
2. <span data-ttu-id="f3e63-356">使用 [儲存體帳戶] 下拉式清單，選取 [(自動)]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-356">Using the **Storage account** drop-down list, select **(auto)**.</span></span> <span data-ttu-id="f3e63-357">如果您在此指定 [(自動)]，Eclipse 工具組會為您的伺服器使用與您在 [發佈至 Azure] 對話方塊中為部署所選帳戶相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3e63-357">If you specify **(auto)** here, the Eclipse toolkit will use the same storage account for your server as the one you select for your deployment in the **Publish to Azure** dialog.</span></span>
3. <span data-ttu-id="f3e63-358">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f3e63-358">Click **OK** to save your changes.</span></span>

<span data-ttu-id="f3e63-359">如果下列任一條件成立，請在 [本機伺服器路徑]  文字方塊中選取電腦上的伺服器安裝路徑：</span><span class="sxs-lookup"><span data-stu-id="f3e63-359">Select a server installation path on your computer in the **Local server path** text box if any of the following conditions are true:</span></span>

* <span data-ttu-id="f3e63-360">您想要在模擬器中測試部署 (僅適用於 Windows)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-360">You want to test your deployment in the emulator (applies to Windows only).</span></span>
* <span data-ttu-id="f3e63-361">您想要將本機安裝的伺服器部署到雲端。</span><span class="sxs-lookup"><span data-stu-id="f3e63-361">You want to deploy your locally installed server to the cloud.</span></span>
* <span data-ttu-id="f3e63-362">您想要使用雲端中的自有自訂伺服器下載，若是這種情況，也請確定您已選取上面的 [部署本機伺服器 (自動上傳至雲端儲存體)]  選項。</span><span class="sxs-lookup"><span data-stu-id="f3e63-362">You want to use a custom server download of your own in the cloud, in which case, also ensure the **Deploy my local server (auto-upload to cloud storage)** option is selected above.</span></span>

<span data-ttu-id="f3e63-363">如果您的情況不適用上述任何選項，則可以選擇使用本機伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="f3e63-363">If none of the preceding options apply to your situation, the local server setting is optional.</span></span>

### <a name="applications-configuration"></a><span data-ttu-id="f3e63-364">應用程式組態</span><span class="sxs-lookup"><span data-stu-id="f3e63-364">Applications configuration</span></span>
<span data-ttu-id="f3e63-365">以下範例說明如何指定應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3e63-365">The following is an example of how you can specify an application.</span></span>

![][ic719512]

<span data-ttu-id="f3e63-366">按一下 [新增] 以新增其他應用程式，或按一下 [移除] 以移除應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3e63-366">Click **Add** to add another application, or **Remove** to remove an application.</span></span> <span data-ttu-id="f3e63-367">為求效率，如果您想要在部署到雲端時使用下載做為應用程式的來源，請使用 [元件屬性](#components_properties) 以指定 URL、儲存體帳戶等項目。</span><span class="sxs-lookup"><span data-stu-id="f3e63-367">For efficiency purposes, if you want to use a download for the source of an application when deploying to the cloud, use the [components properties](#components_properties) to specify a URL, storage account, etc.</span></span> 

<span data-ttu-id="f3e63-368">從 2014 年 4 月版本開始，您的應用程式會自動上傳至與您為部署所選帳戶相同的儲存體帳戶 (在 **eclipsedeploy** 容器之下)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-368">Beginning with the April 2014 release, your applications are automatically uploaded into the same storage account (under the **eclipsedeploy** container) as the one selected for your deployment.</span></span> <span data-ttu-id="f3e63-369">部署的啟動邏輯包含先從該儲存體帳戶下載這些應用程式的步驟。</span><span class="sxs-lookup"><span data-stu-id="f3e63-369">The startup logic of your deployment contains a step that first downloads those applications from that storage account.</span></span> <span data-ttu-id="f3e63-370">這表示您不需要重新建置並重新部署整個封裝就可以升級部署中的應用程式，方法是直接將較新版的應用程式手動上傳至該儲存體帳戶 (例如使用 Azure 入口網站)，來取代工具組原本上傳至該處的 WAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="f3e63-370">This means that you may upgrade your applications in your deployment without needing to rebuild and redeploy the entire package, by manually uploading newer versions of the application directly into that storage account (using the Azure portal for example), replacing the WAR files originally uploaded there by the toolkit.</span></span> <span data-ttu-id="f3e63-371">然後，就只要再次使用 Azure 的管理入口網站或透過命令列公用程式開始回收所有角色執行個體 </span><span class="sxs-lookup"><span data-stu-id="f3e63-371">Then, just initiate the recycling of all those role instances using Azure's management portal again, or via command line utilities.</span></span> <span data-ttu-id="f3e63-372">(目前不支援直接從 Eclipse 工具組內觸發角色回收程序)。</span><span class="sxs-lookup"><span data-stu-id="f3e63-372">(Triggering role recycling directly from within the Eclipse toolkit is not currently supported.)</span></span>

### <a name="notes-about-server-configuration"></a><span data-ttu-id="f3e63-373">伺服器組態的相關注意事項</span><span class="sxs-lookup"><span data-stu-id="f3e63-373">Notes about server configuration</span></span>
<span data-ttu-id="f3e63-374">透過 [伺服器組態] 屬性頁所做的變更會反映在 package.xml 檔的 `<component>` 元素中。</span><span class="sxs-lookup"><span data-stu-id="f3e63-374">Changes made through the **Server configuration** property page are reflected in the `<component>` elements of the package.xml file.</span></span>

<span data-ttu-id="f3e63-375">當您針對 JDK 或應用程式伺服器使用 [自動上傳...] 或 [從下載部署...] 選項，而且您正在針對雲端 (而非計算模擬器) 進行建置，並且已連線到網路時，您可能會發現建置訊息 (例如主控台輸出中的下列內容)，因為 Ant 產生器會驗證下載的可用性：</span><span class="sxs-lookup"><span data-stu-id="f3e63-375">When you use the **Automatically upload...** or **Deploy from download...** options for either the JDK or application server, and you are building for the cloud (not the compute emulator), and you are connected to the network, you may notice build messages such as the following in the Console output, as the Ant builder verifies the download's availability:</span></span>

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

<span data-ttu-id="f3e63-376">如果您選取 [從下載部署...]  選項，可能會顯示下列警告，但建置作業會繼續：</span><span class="sxs-lookup"><span data-stu-id="f3e63-376">If you selected the **Deploy from download...** option, the following warning may be shown, but the build will continue:</span></span>

`[windowsazurepackage] warning: Failed to confirm blob availability! Make sure the URL and/or the access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

<span data-ttu-id="f3e63-377">只有這個警告會指出尚未驗證下載的可用性。</span><span class="sxs-lookup"><span data-stu-id="f3e63-377">This warning is the only indication that the download's availability hasn't been verified.</span></span> <span data-ttu-id="f3e63-378">因此如果雲端中的部署因為某些原因失敗，請檢查是否有收到這個警告。</span><span class="sxs-lookup"><span data-stu-id="f3e63-378">So if a deployment fails in the cloud for some reason, check to see if you received this warning.</span></span>

<span data-ttu-id="f3e63-379">如果您想要停用下載驗證 (例如，如果您認為進行驗證只會拖慢建置速度)，請在 package.xml 的 `<windowsazurepackage>` 項目中，將 `verifydownloads` 屬性設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="f3e63-379">If you want to disable the download verification (for example, if you feel it unnecessarily slows down the build), set the `verifydownloads` attribute to `false` in the `<windowsazurepackage>` element of package.xml:</span></span> 

`<windowsazurepackage verifydownloads="false" ...>` 

<span data-ttu-id="f3e63-380">如果您已選取 [自動上傳...]  選項，則每當需要上傳時，您就會在主控台視窗中看到每隔 5 秒報告一次上傳進度的建置訊息。</span><span class="sxs-lookup"><span data-stu-id="f3e63-380">If you selected the **Automatically upload...** option, then in the console window you will see build messages reporting the progress of the upload every 5 seconds, whenever an upload is necessary.</span></span>

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a><span data-ttu-id="f3e63-381">SSL 卸載屬性</span><span class="sxs-lookup"><span data-stu-id="f3e63-381">SSL offloading properties</span></span>
<span data-ttu-id="f3e63-382">在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [SSL 卸載]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-382">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **SSL Offloading**.</span></span> 

![][ic719481]

<span data-ttu-id="f3e63-383">在這個對話方塊中，您可以啟用 SSL 卸載，以便在 Azure 上的 Java 部署中輕鬆啟用超文字安全傳輸通訊協定 (HTTPS) 支援，而不必在 Java 應用程式伺服器中設定 SSL。</span><span class="sxs-lookup"><span data-stu-id="f3e63-383">Within this dialog, you can enable SSL offloading, allowing you to easily enable Hypertext Transfer Protocol Secure (HTTPS) support in your Java deployment on Azure, without requiring you to configure SSL in your Java application server.</span></span> <span data-ttu-id="f3e63-384">如需詳細資訊，請參閱 [SSL 卸載][SSL Offloading]和[如何使用 SSL 卸載][How to Use SSL Offloading]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-384">For more information, see [SSL Offloading][SSL Offloading] and [How to Use SSL Offloading][How to Use SSL Offloading].</span></span>

## <a name="see-also"></a><span data-ttu-id="f3e63-385">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f3e63-385">See Also</span></span>
<span data-ttu-id="f3e63-386">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f3e63-386">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="f3e63-387">[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f3e63-387">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="f3e63-388">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f3e63-388">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="f3e63-389">[Azure 專案屬性][Azure Project Properties]</span><span class="sxs-lookup"><span data-stu-id="f3e63-389">[Azure Project Properties][Azure Project Properties]</span></span>

<span data-ttu-id="f3e63-390">[Azure 儲存體帳戶清單][Azure Storage Account List]</span><span class="sxs-lookup"><span data-stu-id="f3e63-390">[Azure Storage Account List][Azure Storage Account List]</span></span>

<span data-ttu-id="f3e63-391">如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="f3e63-391">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

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
[How to Use Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How to Use SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
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
