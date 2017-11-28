---
title: "aaaConfigure 保護 Azure Service Fabric 叢集連線 |Microsoft 文件"
description: "了解如何 toouse Visual Studio tooconfigure 保護 hello Azure Service Fabric 叢集所支援的連線。"
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a><span data-ttu-id="8e706-103">設定從 Visual Studio 的安全連線 tooa Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="8e706-103">Configure secure connections tooa Service Fabric cluster from Visual Studio</span></span>
<span data-ttu-id="8e706-104">了解如何 toouse Visual Studio toosecurely 存取 Azure Service Fabric 叢集的存取控制原則設定。</span><span class="sxs-lookup"><span data-stu-id="8e706-104">Learn how toouse Visual Studio toosecurely access an Azure Service Fabric cluster with access control policies configured.</span></span>

## <a name="cluster-connection-types"></a><span data-ttu-id="8e706-105">叢集連線類型</span><span class="sxs-lookup"><span data-stu-id="8e706-105">Cluster connection types</span></span>
<span data-ttu-id="8e706-106">Hello Azure Service Fabric 叢集所支援兩種連線類型：**不安全**連線和**x509 憑證為基礎**保護連線。</span><span class="sxs-lookup"><span data-stu-id="8e706-106">Two types of connections are supported by hello Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections.</span></span> <span data-ttu-id="8e706-107">(如果是裝載在內部部署環境的 Service Fabric 叢集，則也支援 **Windows** 和 **dSTS** 驗證。)正在建立 hello 叢集時，您會有 tooconfigure hello 叢集連線類型。</span><span class="sxs-lookup"><span data-stu-id="8e706-107">(For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have tooconfigure hello cluster connection type when hello cluster is being created.</span></span> <span data-ttu-id="8e706-108">一旦建立之後，就無法變更 hello 連接類型。</span><span class="sxs-lookup"><span data-stu-id="8e706-108">Once it's created, hello connection type can’t be changed.</span></span>

<span data-ttu-id="8e706-109">hello Visual Studio Service Fabric 工具支援所有的驗證類型進行發佈的連線 tooa 叢集。</span><span class="sxs-lookup"><span data-stu-id="8e706-109">hello Visual Studio Service Fabric tools support all authentication types for connecting tooa cluster for publishing.</span></span> <span data-ttu-id="8e706-110">請參閱[從 hello Azure 入口網站設定 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)如需有關指示 tooset 安全的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="8e706-110">See [Setting up a Service Fabric cluster from hello Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how tooset up a secure Service Fabric cluster.</span></span>

## <a name="configure-cluster-connections-in-publish-profiles"></a><span data-ttu-id="8e706-111">在發行設定檔中設定叢集連接</span><span class="sxs-lookup"><span data-stu-id="8e706-111">Configure cluster connections in publish profiles</span></span>
<span data-ttu-id="8e706-112">如果您發行 Service Fabric 專案從 Visual Studio 時，使用 hello**發行 Service Fabric 應用程式**對話方塊方塊 toochoose Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="8e706-112">If you publish a Service Fabric project from Visual Studio, use hello **Publish Service Fabric Application** dialog box toochoose an Azure Service Fabric cluster.</span></span> <span data-ttu-id="8e706-113">在 [連線端點] 之下，選取您訂用帳戶下的現有叢集。</span><span class="sxs-lookup"><span data-stu-id="8e706-113">Under **Connection endpoint**, select an existing cluster under your subscription.</span></span>

![hello * * 發行 Service Fabric 應用程式 * * 對話方塊會使用的 tooconfigure Service Fabric 連線。][publishdialog]

<span data-ttu-id="8e706-115">hello**發行 Service Fabric 應用程式**對話方塊會自動驗證 hello 叢集連線。</span><span class="sxs-lookup"><span data-stu-id="8e706-115">hello **Publish Service Fabric Application** dialog box automatically validates hello cluster connection.</span></span> <span data-ttu-id="8e706-116">如果出現提示，請登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e706-116">If prompted, sign in tooyour Azure account.</span></span> <span data-ttu-id="8e706-117">如果驗證成功，則表示您的系統已正確安裝憑證，tooconnect toohello 叢集安全地儲存，或您的叢集已不安全的 hello。</span><span class="sxs-lookup"><span data-stu-id="8e706-117">If validation passes, it means that your system has hello correct certificates installed tooconnect toohello cluster securely, or your cluster is non-secure.</span></span> <span data-ttu-id="8e706-118">網路問題，或沒有正確地設定系統 tooconnect tooa 安全叢集，可能被造成驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="8e706-118">Validation failures can be caused by network issues or by not having your system correctly configured tooconnect tooa secure cluster.</span></span>

![hello * * 發行 Service Fabric 應用程式 * * 對話方塊會驗證現有的正確設定 Service Fabric 叢集連線。][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a><span data-ttu-id="8e706-120">tooconnect tooa 安全叢集</span><span class="sxs-lookup"><span data-stu-id="8e706-120">tooconnect tooa secure cluster</span></span>
1. <span data-ttu-id="8e706-121">請確定您可以存取其中一個 hello hello 目的地叢集信任的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="8e706-121">Make sure you can access one of hello client certificates that hello destination cluster trusts.</span></span> <span data-ttu-id="8e706-122">hello 憑證通常會為個人資訊交換 (.pfx) 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="8e706-122">hello certificate is usually shared as a Personal Information Exchange (.pfx) file.</span></span> <span data-ttu-id="8e706-123">請參閱[從 hello Azure 入口網站設定 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)如 tooconfigure hello 伺服器 toogrant 存取 tooa 用戶端的方式。</span><span class="sxs-lookup"><span data-stu-id="8e706-123">See [Setting up a Service Fabric cluster from hello Azure portal](service-fabric-cluster-creation-via-portal.md) for how tooconfigure hello server toogrant access tooa client.</span></span>
2. <span data-ttu-id="8e706-124">安裝 hello 受信任的憑證。</span><span class="sxs-lookup"><span data-stu-id="8e706-124">Install hello trusted certificate.</span></span> <span data-ttu-id="8e706-125">toodo，按兩下 hello.pfx 檔案，或使用 hello PowerShell 指令碼 Import-pfxcertificate tooimport hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="8e706-125">toodo this, double-click hello .pfx file, or use hello PowerShell script Import-PfxCertificate tooimport hello certificates.</span></span> <span data-ttu-id="8e706-126">安裝 hello 憑證太**Cert: \LocalMachine\My**。</span><span class="sxs-lookup"><span data-stu-id="8e706-126">Install hello certificate too**Cert:\LocalMachine\My**.</span></span> <span data-ttu-id="8e706-127">它是確定 tooaccept 匯入 hello 憑證時的所有預設設定。</span><span class="sxs-lookup"><span data-stu-id="8e706-127">It's OK tooaccept all default settings while importing hello certificate.</span></span>
3. <span data-ttu-id="8e706-128">選擇 hello**發行...** hello 專案 tooopen hello hello 快顯功能表上的命令**發行 Azure 應用程式**對話方塊，然後選取 hello 目標叢集。</span><span class="sxs-lookup"><span data-stu-id="8e706-128">Choose hello **Publish...** command on hello shortcut menu of hello project tooopen hello **Publish Azure Application** dialog box and then select hello target cluster.</span></span> <span data-ttu-id="8e706-129">hello 工具會自動解析 hello 連線，並儲存在 hello 參數將發行的 hello 安全連線設定檔。</span><span class="sxs-lookup"><span data-stu-id="8e706-129">hello tool automatically resolves hello connection and saves hello secure connection parameters in hello publish profile.</span></span>
4. <span data-ttu-id="8e706-130">選用： 您可以編輯 hello 發行設定檔 toospecify 安全叢集連線。</span><span class="sxs-lookup"><span data-stu-id="8e706-130">Optional: You can edit hello publish profile toospecify a secure cluster connection.</span></span>
   
   <span data-ttu-id="8e706-131">因為您手動編輯 hello 發行設定檔 XML 檔 toospecify hello 憑證資訊，請確定 toonote hello 憑證存放區名稱，儲存位置和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="8e706-131">Since you're manually editing hello Publish Profile XML file toospecify hello certificate information, be sure toonote hello certificate store name, store location, and certificate thumbprint.</span></span> <span data-ttu-id="8e706-132">您將需要的 tooprovide hello 憑證存放區的這些值的名稱和儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="8e706-132">You'll need tooprovide these values for hello certificate's store name and store location.</span></span> <span data-ttu-id="8e706-133">請參閱[How to： 擷取 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8e706-133">See [How to: Retrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.</span></span>
   
   <span data-ttu-id="8e706-134">您可以使用 hello *ClusterConnectionParameters*參數 toospecify hello PowerShell 參數 toouse 連接 toohello Service Fabric 叢集時。</span><span class="sxs-lookup"><span data-stu-id="8e706-134">You can use hello *ClusterConnectionParameters* parameters toospecify hello PowerShell parameters toouse when connecting toohello Service Fabric cluster.</span></span> <span data-ttu-id="8e706-135">有效的參數是可接受的 hello Connect-servicefabriccluster cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8e706-135">Valid parameters are any that are accepted by hello Connect-ServiceFabricCluster cmdlet.</span></span> <span data-ttu-id="8e706-136">如需可用參數的清單，請參閱 [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8e706-136">See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.</span></span>
   
   <span data-ttu-id="8e706-137">如果您要發行 tooa 遠端叢集，您會需要針對該特定群集 toospecify hello 適當的參數。</span><span class="sxs-lookup"><span data-stu-id="8e706-137">If you’re publishing tooa remote cluster, you need toospecify hello appropriate parameters for that specific cluster.</span></span> <span data-ttu-id="8e706-138">hello 以下是連接 tooa 不安全叢集的範例：</span><span class="sxs-lookup"><span data-stu-id="8e706-138">hello following is an example of connecting tooa non-secure cluster:</span></span>
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   <span data-ttu-id="8e706-139">連接 tooan x509 憑證為基礎安全叢集的範例如下：</span><span class="sxs-lookup"><span data-stu-id="8e706-139">Here’s an example for connecting tooan x509 certificate-based secure cluster:</span></span>
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. <span data-ttu-id="8e706-140">編輯任何其他必要的設定，例如升級參數和應用程式參數檔案的位置，然後應用程式並發行從 hello**發行 Service Fabric 應用程式**Visual Studio 中的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8e706-140">Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from hello **Publish Service Fabric Application** dialog box in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e706-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e706-141">Next steps</span></span>
<span data-ttu-id="8e706-142">如需有關存取 Service Fabric 叢集的詳細資訊，請參閱 [使用 Service Fabric 總管視覺化叢集](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="8e706-142">For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
