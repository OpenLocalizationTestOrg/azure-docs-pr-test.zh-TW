---
title: "組件 aaaHPC 叢集與 Azure Active Directory |Microsoft 文件"
description: "了解 toointegrate HPC Pack 2016 Azure 與 Azure Active Directory 中的叢集化"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="2ef24-103">使用 Azure Active Directory 管理 Azure 中的 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="2ef24-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="2ef24-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) 支援與 [Azure Active Directory](../../active-directory/index.md) (Azure AD) 整合，以便系統管理員在 Azure 中部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="2ef24-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="2ef24-105">請遵循下列高的層級工作的 hello 本文章中的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2ef24-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="2ef24-106">手動整合 HPC Pack 叢集與 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="2ef24-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="2ef24-107">在 Azure 中管理和排程 HPC Pack 叢集中的工作</span><span class="sxs-lookup"><span data-stu-id="2ef24-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="2ef24-108">HPC Pack 叢集解決方案整合與 Azure AD 會遵循標準步驟 toointegrate 其他應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="2ef24-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="2ef24-109">本文假設您已熟悉 Azure AD 中的基本使用者管理。</span><span class="sxs-lookup"><span data-stu-id="2ef24-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="2ef24-110">如需詳細資訊及背景，請參閱 hello [Azure Active Directory 文件](../../active-directory/index.md)hello 遵循 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2ef24-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="2ef24-111">整合的優點</span><span class="sxs-lookup"><span data-stu-id="2ef24-111">Benefits of integration</span></span>


<span data-ttu-id="2ef24-112">Azure Active Directory (Azure AD) 是多租用戶雲端式目錄和身分識別管理服務，提供單一登入 (SSO) 存取 toocloud 解決方案。</span><span class="sxs-lookup"><span data-stu-id="2ef24-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="2ef24-113">HPC Pack 叢集與 Azure AD 的整合可協助您達成下列目標 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="2ef24-114">移除 hello HPC Pack 叢集 hello 傳統 Active Directory 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="2ef24-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="2ef24-115">這有助於減少維護 hello 叢集，如果這不是您的商務和加速 hello 部署程序所需的 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="2ef24-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="2ef24-116">下列由 Azure AD 的優點運用 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="2ef24-117">單一登入</span><span class="sxs-lookup"><span data-stu-id="2ef24-117">Single sign-on</span></span> 
    *   <span data-ttu-id="2ef24-118">在 Azure 中的 hello HPC Pack 叢集使用的本機 AD 身分識別</span><span class="sxs-lookup"><span data-stu-id="2ef24-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory 環境](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="2ef24-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="2ef24-120">Prerequisites</span></span>
* <span data-ttu-id="2ef24-121">**Azure 虛擬機器中部署的 HPC Pack 2016 叢集** - 如需相關步驟，請參閱[在 Azure 中部署 HPC Pack 2016 叢集](hpcpack-2016-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="2ef24-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="2ef24-122">您需要 hello 的 hello 前端節點的 DNS 名稱 」 和 「 叢集管理員來完成這篇文章中的 hello 步驟 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="2ef24-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2ef24-123">HPC Pack 2016 之前的 HPC Pack 版本不支援 Azure Active Directory 整合。</span><span class="sxs-lookup"><span data-stu-id="2ef24-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="2ef24-124">**用戶端電腦**-您需要 Windows 或 Windows Server 用戶端電腦太執行 HPC Pack 用戶端公用程式。</span><span class="sxs-lookup"><span data-stu-id="2ef24-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="2ef24-125">如果您只想 toouse hello HPC Pack web 入口網站或 REST API toosubmit 作業，您可以使用您選擇的任何用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="2ef24-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="2ef24-126">**HPC Pack 用戶端公用程式**-使用 hello 可用的安裝套件可從 Microsoft 下載中心 hello 的 hello 用戶端電腦上安裝 hello HPC Pack 用戶端公用程式。</span><span class="sxs-lookup"><span data-stu-id="2ef24-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="2ef24-127">步驟 1： 註冊 hello HPC 叢集中的伺服器與 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="2ef24-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="2ef24-128">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="2ef24-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2ef24-129">按一下**Active Directory**在 hello 左的窗格中，，然後按一下hello 您訂用帳戶中所需的目錄。</span><span class="sxs-lookup"><span data-stu-id="2ef24-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="2ef24-130">您必須擁有的權限 tooaccess 資源 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="2ef24-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="2ef24-131">按一下 [使用者]，並確定已經建立或設定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ef24-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="2ef24-132">按一下 應用程式 > 新增，然後按一下新增我的組織正在開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ef24-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="2ef24-133">輸入下列資訊在 hello 精靈中的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="2ef24-134">**名稱** - HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="2ef24-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="2ef24-135">**類型** - 選取 [Web 應用程式和/或 Web API]</span><span class="sxs-lookup"><span data-stu-id="2ef24-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="2ef24-136">**登入 URL**-hello hello 範例中，預設為基底 URL`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="2ef24-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="2ef24-137">**應用程式識別碼 URI** - `https://<Directory_name>/<application_name>`。</span><span class="sxs-lookup"><span data-stu-id="2ef24-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="2ef24-138">取代`<Directory_name`> 以您的 Azure AD 租用戶，例如，完整名稱的 hello `hpclocal.onmicrosoft.com`，並取代`<application_name>`hello 您先前選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ef24-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="2ef24-139">已加入 hello 應用程式之後，請按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="2ef24-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="2ef24-140">設定下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="2ef24-141">針對 [應用程式為多租用戶]，選取 [是]</span><span class="sxs-lookup"><span data-stu-id="2ef24-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="2ef24-142">選取**是**如**使用者指派必要的 tooaccess 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2ef24-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="2ef24-143">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2ef24-143">Click **Save**.</span></span> <span data-ttu-id="2ef24-144">儲存完成後，按一下 [管理資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="2ef24-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="2ef24-145">此動作會下載您應用程式的資訊清單 JavaScript 物件標記法 (JSON) 檔案。</span><span class="sxs-lookup"><span data-stu-id="2ef24-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="2ef24-146">編輯 hello 下載資訊清單，找出 hello`appRoles`設定並新增下列應用程式角色的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="2ef24-147">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="2ef24-147">Save hello file.</span></span> <span data-ttu-id="2ef24-148">然後在 hello 入口網站中，按一下**管理資訊清單** > **上傳資訊清單**。</span><span class="sxs-lookup"><span data-stu-id="2ef24-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="2ef24-149">然後，您可以上傳 hello 編輯資訊清單。</span><span class="sxs-lookup"><span data-stu-id="2ef24-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="2ef24-150">按一下 使用者、選取使用者，然後按一下指派。</span><span class="sxs-lookup"><span data-stu-id="2ef24-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="2ef24-151">指派其中一個 hello 可用的角色 （HpcUsers 或 HpcAdminMirror） toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2ef24-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="2ef24-152">與 hello 目錄中的其他使用者重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="2ef24-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="2ef24-153">如需叢集使用者的背景資訊，請參閱[管理叢集使用者](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2ef24-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="2ef24-154">toomanage 使用者，我們建議您使用 hello Azure Active Directory 預覽刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2ef24-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="2ef24-155">步驟 2: Hello HPC 叢集的用戶端向 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="2ef24-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="2ef24-156">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="2ef24-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2ef24-157">按一下**Active Directory**在 hello 左的窗格中，，然後按一下hello 您訂用帳戶中所需的目錄。</span><span class="sxs-lookup"><span data-stu-id="2ef24-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="2ef24-158">您必須擁有的權限 tooaccess 資源 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="2ef24-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="2ef24-159">按一下 應用程式 > 新增，然後按一下新增我的組織正在開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ef24-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="2ef24-160">輸入下列資訊在 hello 精靈中的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="2ef24-161">**名稱** - HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="2ef24-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="2ef24-162">**類型** - 選取 [原生用戶端應用程式]</span><span class="sxs-lookup"><span data-stu-id="2ef24-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="2ef24-163">**重新導向 URI** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="2ef24-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="2ef24-164">已加入 hello 應用程式之後，請按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="2ef24-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="2ef24-165">複製 hello**用戶端識別碼**值，並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="2ef24-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="2ef24-166">您稍後在設定應用程式時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="2ef24-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="2ef24-167">在**權限 tooother 應用程式**，按一下 **新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2ef24-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="2ef24-168">搜尋並新增 hello HpcPackClusterServer 應用程式 （在步驟 1 中建立）。</span><span class="sxs-lookup"><span data-stu-id="2ef24-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="2ef24-169">在 hello**委派的權限**下拉式清單中，選取**存取 HpcClusterServer**。</span><span class="sxs-lookup"><span data-stu-id="2ef24-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="2ef24-170">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2ef24-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="2ef24-171">步驟 3： 設定 hello HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="2ef24-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="2ef24-172">連接 Azure toohello HPC Pack 2016 前端節點。</span><span class="sxs-lookup"><span data-stu-id="2ef24-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="2ef24-173">啟動 HPC PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2ef24-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="2ef24-174">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="2ef24-175">其中</span><span class="sxs-lookup"><span data-stu-id="2ef24-175">where</span></span>

    * <span data-ttu-id="2ef24-176">`AADTenant`指定 hello Azure AD 租用戶名稱例如`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="2ef24-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="2ef24-177">`AADClientAppId`指定 hello hello 步驟 2 中建立的應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ef24-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="2ef24-178">重新啟動 hello HpcSchedulerStateful 服務。</span><span class="sxs-lookup"><span data-stu-id="2ef24-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="2ef24-179">中包含多個前端節點的叢集，您可以執行下列 PowerShell 命令 hello 前端節點 tooswitch hello 主要複本上 hello HpcSchedulerStateful 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="2ef24-180">步驟 4： 管理和提交從 hello 用戶端的工作</span><span class="sxs-lookup"><span data-stu-id="2ef24-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="2ef24-181">tooinstall hello HPC Pack 用戶端公用程式在您的電腦上從 hello Microsoft Download Center 下載 HPC Pack 2016 安裝程式檔案 （完整安裝）。</span><span class="sxs-lookup"><span data-stu-id="2ef24-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="2ef24-182">當您開始 hello 安裝時，請選擇 hello hello 安裝選項**HPC Pack 用戶端公用程式**。</span><span class="sxs-lookup"><span data-stu-id="2ef24-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="2ef24-183">tooprepare hello 用戶端電腦，安裝期間使用的 hello 憑證[HPC 叢集設定](hpcpack-2016-cluster.md)hello 用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="2ef24-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="2ef24-184">使用標準 Windows 憑證管理程序 tooinstall hello 公開憑證 toohello**憑證 – 目前使用者** > **受信任的根憑證授權單位**儲存。</span><span class="sxs-lookup"><span data-stu-id="2ef24-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="2ef24-185">您可以現在執行 hello HPC Pack 命令或使用 HPC Pack 作業管理員 GUI hello toosubmit 及管理叢集工作使用 hello Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ef24-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="2ef24-186">工作提交的選項，請參閱[提交 HPC 作業 tooan HPC Pack 叢集在 Azure 中](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster)。</span><span class="sxs-lookup"><span data-stu-id="2ef24-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="2ef24-187">當您第一次嘗試 tooconnect toohello HPC Pack 叢集在 Azure 中的 hello 時，會出現快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="2ef24-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="2ef24-188">輸入在您 Azure AD 認證 toolog。</span><span class="sxs-lookup"><span data-stu-id="2ef24-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="2ef24-189">hello 權杖後來會快取。</span><span class="sxs-lookup"><span data-stu-id="2ef24-189">hello token is then cached.</span></span> <span data-ttu-id="2ef24-190">更新版本中使用 Azure hello 的連線 toohello 叢集快取權杖，除非驗證變更或 hello 快取清除。</span><span class="sxs-lookup"><span data-stu-id="2ef24-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="2ef24-191">例如，完成 hello 上一個步驟之後，您可以查詢從內部部署用戶端的工作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ef24-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="2ef24-192">透過 Azure AD 整合提交作業的實用 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="2ef24-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="2ef24-193">管理 hello 本機權杖快取</span><span class="sxs-lookup"><span data-stu-id="2ef24-193">Manage hello local token cache</span></span>

<span data-ttu-id="2ef24-194">HPC Pack 2016 提供兩個新的 HPC PowerShell cmdlet toomanage hello 本機權杖快取。</span><span class="sxs-lookup"><span data-stu-id="2ef24-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="2ef24-195">這些 Cmdlet 可用於非互動方式提交作業。</span><span class="sxs-lookup"><span data-stu-id="2ef24-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="2ef24-196">請參閱下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="2ef24-197">設定 hello 送出工作使用 hello Azure AD 帳戶的認證</span><span class="sxs-lookup"><span data-stu-id="2ef24-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="2ef24-198">某些情況下，您可能想在 hello HPC 叢集使用者下的 toorun hello 作業 （針對加入網域的 HPC 叢集，以一個網域使用者身分執行; 對於未加入網域的 HPC 叢集，hello 前端節點上一個本機使用者身分執行）。</span><span class="sxs-lookup"><span data-stu-id="2ef24-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="2ef24-199">使用下列命令 tooset hello 認證 hello:</span><span class="sxs-lookup"><span data-stu-id="2ef24-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="2ef24-200">然後提交 hello 工作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2ef24-200">Then submit hello job as follows.</span></span> <span data-ttu-id="2ef24-201">hello 作業/工作會執行下 $localUser hello 計算節點上。</span><span class="sxs-lookup"><span data-stu-id="2ef24-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="2ef24-202">如果`–Credential`中未指定`Submit-HpcJob`，hello 工作或任務下執行本機對應的使用者為 hello Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ef24-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="2ef24-203">（hello HPC 叢集會建立本機使用者以相同的名稱，為 Azure AD 帳戶 toorun hello 工作 hello hello）。</span><span class="sxs-lookup"><span data-stu-id="2ef24-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="2ef24-204">設定 hello Azure AD 帳戶的擴充的資料。</span><span class="sxs-lookup"><span data-stu-id="2ef24-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="2ef24-205">使用 hello Azure AD 帳戶的 Linux 節點上執行 MPI 工作時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="2ef24-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="2ef24-206">設定 hello Azure AD 帳戶本身的擴充的資料</span><span class="sxs-lookup"><span data-stu-id="2ef24-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="2ef24-207">設定擴充資料並且以 HPC 叢集使用者身分執行</span><span class="sxs-lookup"><span data-stu-id="2ef24-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

