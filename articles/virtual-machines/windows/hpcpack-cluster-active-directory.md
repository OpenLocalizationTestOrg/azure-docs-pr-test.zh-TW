---
title: "HPC Pack 叢集與 Azure Active Directory |Microsoft Docs"
description: "了解如何整合 Azure 中的 HPC Pack 2016 叢集與 Azure Active Directory"
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
ms.openlocfilehash: c5a06a9c810349b1bcce01c7f73563941a5af0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="18dc9-103">使用 Azure Active Directory 管理 Azure 中的 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="18dc9-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="18dc9-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) 支援與 [Azure Active Directory](../../active-directory/index.md) (Azure AD) 整合，以便系統管理員在 Azure 中部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="18dc9-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="18dc9-105">依照本文中的步驟執行高階工作︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-105">Follow the steps in this article for the following high level tasks:</span></span> 
* <span data-ttu-id="18dc9-106">手動整合 HPC Pack 叢集與 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="18dc9-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="18dc9-107">在 Azure 中管理和排程 HPC Pack 叢集中的工作</span><span class="sxs-lookup"><span data-stu-id="18dc9-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="18dc9-108">整合 HPC Pack 叢集解決方案與 Azure AD 時，請依循標準步驟來整合其他應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="18dc9-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span></span> <span data-ttu-id="18dc9-109">本文假設您已熟悉 Azure AD 中的基本使用者管理。</span><span class="sxs-lookup"><span data-stu-id="18dc9-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="18dc9-110">如需詳細資訊及背景，請參閱 [Azure Active Directory 文件](../../active-directory/index.md)和下一節。</span><span class="sxs-lookup"><span data-stu-id="18dc9-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="18dc9-111">整合的優點</span><span class="sxs-lookup"><span data-stu-id="18dc9-111">Benefits of integration</span></span>


<span data-ttu-id="18dc9-112">Azure Active Directory (Azure AD) 是多租用戶雲端型目錄和身分識別管理服務，可提供雲端解決方案的單一登入 (SSO) 存取權。</span><span class="sxs-lookup"><span data-stu-id="18dc9-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span></span>

<span data-ttu-id="18dc9-113">HPC Pack 叢集與 Azure AD 的整合可協助您達成下列目標︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span></span>

* <span data-ttu-id="18dc9-114">移除 HPC Pack 叢集中的傳統 Active Directory 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="18dc9-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span></span> <span data-ttu-id="18dc9-115">這可以協助降低維護叢集 (如果您的企業不需這麼做) 的成本，以及加快部署程序。</span><span class="sxs-lookup"><span data-stu-id="18dc9-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span></span>
* <span data-ttu-id="18dc9-116">運用 Azure AD 所提供的下列優點︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-116">Leverage the following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="18dc9-117">單一登入</span><span class="sxs-lookup"><span data-stu-id="18dc9-117">Single sign-on</span></span> 
    *   <span data-ttu-id="18dc9-118">在 Azure 中使用 HPC Pack 叢集的本機 AD 身分識別</span><span class="sxs-lookup"><span data-stu-id="18dc9-118">Using a local AD identity for the HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory 環境](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="18dc9-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="18dc9-120">Prerequisites</span></span>
* <span data-ttu-id="18dc9-121">**Azure 虛擬機器中部署的 HPC Pack 2016 叢集** - 如需相關步驟，請參閱[在 Azure 中部署 HPC Pack 2016 叢集](hpcpack-2016-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="18dc9-122">您必須要有前端節點的 DNS 名稱和叢集系統管理員的認證，才能完成本文中的步驟。</span><span class="sxs-lookup"><span data-stu-id="18dc9-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="18dc9-123">HPC Pack 2016 之前的 HPC Pack 版本不支援 Azure Active Directory 整合。</span><span class="sxs-lookup"><span data-stu-id="18dc9-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="18dc9-124">**用戶端電腦** - 您需要有可執行 HPC Pack 用戶端公用程式的 Windows 或 Windows Server 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="18dc9-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span></span> <span data-ttu-id="18dc9-125">如果您只想要使用 HPC Pack Web 入口網站或 REST API 來提交工作，您可以使用自行選擇的任何用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="18dc9-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="18dc9-126">**HPC Pack 用戶端公用程式** - 使用從 Microsoft 下載中心取得的免費安裝套件，在用戶端電腦上安裝 HPC Pack 用戶端公用程式。</span><span class="sxs-lookup"><span data-stu-id="18dc9-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span></span>


## <a name="step-1-register-the-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="18dc9-127">步驟 1︰向 Azure AD 租用戶註冊 HPC 叢集伺服器</span><span class="sxs-lookup"><span data-stu-id="18dc9-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="18dc9-128">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="18dc9-129">按一下左側功能表中的 **Active Directory**，然後按一下您訂用帳戶想要的目錄。</span><span class="sxs-lookup"><span data-stu-id="18dc9-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="18dc9-130">您必須具備存取目錄中資源的權限。</span><span class="sxs-lookup"><span data-stu-id="18dc9-130">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="18dc9-131">按一下 [使用者]，並確定已經建立或設定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="18dc9-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="18dc9-132">按一下 [應用程式] > [新增]，然後按一下 [新增我的組織正在開發的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="18dc9-133">在精靈中輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-133">Enter the following information in the wizard:</span></span>
    * <span data-ttu-id="18dc9-134">**名稱** - HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="18dc9-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="18dc9-135">**類型** - 選取 [Web 應用程式和/或 Web API]</span><span class="sxs-lookup"><span data-stu-id="18dc9-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="18dc9-136">**單入 URL**- 範例的基礎 URL，預設為 `https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="18dc9-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="18dc9-137">**應用程式識別碼 URI** - `https://<Directory_name>/<application_name>`。</span><span class="sxs-lookup"><span data-stu-id="18dc9-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="18dc9-138">以 Azure AD 租用戶的完整名稱 (例如 `hpclocal.onmicrosoft.com`) 取代 `<Directory_name`> ，並以您先前選擇的名稱取代 `<application_name>`。</span><span class="sxs-lookup"><span data-stu-id="18dc9-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span></span>

5. <span data-ttu-id="18dc9-139">新增應用程式之後，請按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-139">After the app is added, click **Configure**.</span></span> <span data-ttu-id="18dc9-140">設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="18dc9-140">Configure the following properties:</span></span>
    * <span data-ttu-id="18dc9-141">針對 [應用程式為多租用戶]，選取 [是]</span><span class="sxs-lookup"><span data-stu-id="18dc9-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="18dc9-142">針對 [存取應用程式需要使用者指派]，選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-142">Select **Yes** for **User assignment required to access app**.</span></span>

6. <span data-ttu-id="18dc9-143">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="18dc9-143">Click **Save**.</span></span> <span data-ttu-id="18dc9-144">儲存完成後，按一下 [管理資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="18dc9-145">此動作會下載您應用程式的資訊清單 JavaScript 物件標記法 (JSON) 檔案。</span><span class="sxs-lookup"><span data-stu-id="18dc9-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="18dc9-146">找出 `appRoles` 設定並新增下列應用程式角色，以編輯下載的資訊清單︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span></span>
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
7. <span data-ttu-id="18dc9-147">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="18dc9-147">Save the file.</span></span> <span data-ttu-id="18dc9-148">然後在入口網站中，按一下 [管理資訊清單]  >  [上傳資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="18dc9-149">然後，您可以上傳編輯後的資訊清單。</span><span class="sxs-lookup"><span data-stu-id="18dc9-149">You can then upload the edited manifest.</span></span>
8. <span data-ttu-id="18dc9-150">按一下 [使用者]、選取使用者，然後按一下 [指派]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="18dc9-151">將其中一個可用的角色 (HpcUsers 或 HpcAdminMirror) 指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="18dc9-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span></span> <span data-ttu-id="18dc9-152">對目錄中的其他使用者重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="18dc9-152">Repeat this step with additional users in the directory.</span></span> <span data-ttu-id="18dc9-153">如需叢集使用者的背景資訊，請參閱[管理叢集使用者](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="18dc9-154">若要管理使用者，我們建議使用 [Azure 入口網站](https://portal.azure.com)中的 Azure Active Directory 預覽刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="18dc9-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-the-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="18dc9-155">步驟 2︰向 Azure AD 租用戶註冊 HPC 叢集用戶端</span><span class="sxs-lookup"><span data-stu-id="18dc9-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="18dc9-156">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="18dc9-157">按一下左側功能表中的 **Active Directory**，然後按一下您訂用帳戶想要的目錄。</span><span class="sxs-lookup"><span data-stu-id="18dc9-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="18dc9-158">您必須具備存取目錄中資源的權限。</span><span class="sxs-lookup"><span data-stu-id="18dc9-158">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="18dc9-159">按一下 [應用程式] > [新增]，然後按一下 [新增我的組織正在開發的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="18dc9-160">在精靈中輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-160">Enter the following information in the wizard:</span></span>

    * <span data-ttu-id="18dc9-161">**名稱** - HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="18dc9-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="18dc9-162">**類型** - 選取 [原生用戶端應用程式]</span><span class="sxs-lookup"><span data-stu-id="18dc9-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="18dc9-163">**重新導向 URI** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="18dc9-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="18dc9-164">新增應用程式之後，請按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-164">After the app is added, click **Configure**.</span></span> <span data-ttu-id="18dc9-165">複製 [用戶端識別碼]  值並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="18dc9-165">Copy the **Client ID** value and save it.</span></span> <span data-ttu-id="18dc9-166">您稍後在設定應用程式時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="18dc9-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="18dc9-167">在 [其他應用程式的權限] 中，按一下 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-167">In **Permissions to other applications**, click **Add Application**.</span></span> <span data-ttu-id="18dc9-168">搜尋並將新增 HpcPackClusterServer 應用程式 (在步驟 1 中建立)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="18dc9-169">在 [委派的權限] 下拉式清單中，選取 [存取 HpcClusterServer]。</span><span class="sxs-lookup"><span data-stu-id="18dc9-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="18dc9-170">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="18dc9-170">Then click **Save**.</span></span>


## <a name="step-3-configure-the-hpc-cluster"></a><span data-ttu-id="18dc9-171">步驟 3︰設定 HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="18dc9-171">Step 3: Configure the HPC cluster</span></span>

1. <span data-ttu-id="18dc9-172">連接到 Azure 中的 HPC Pack 2016 前端節點。</span><span class="sxs-lookup"><span data-stu-id="18dc9-172">Connect to the HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="18dc9-173">啟動 HPC PowerShell。</span><span class="sxs-lookup"><span data-stu-id="18dc9-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="18dc9-174">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="18dc9-174">Run the following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="18dc9-175">其中</span><span class="sxs-lookup"><span data-stu-id="18dc9-175">where</span></span>

    * <span data-ttu-id="18dc9-176">`AADTenant` 指定 Azure AD 租用戶名稱，例如 `hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="18dc9-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="18dc9-177">`AADClientAppId` 為在步驟 2 中建立的應用程式指定用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="18dc9-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span></span>

4. <span data-ttu-id="18dc9-178">重新啟動 HpcSchedulerStateful 服務。</span><span class="sxs-lookup"><span data-stu-id="18dc9-178">Restart the HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="18dc9-179">在具有多個前端節點的叢集中，您可以在前端節點上執行下列 PowerShell 命令，以切換 HpcSchedulerStateful 服務的主要複本︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-the-client"></a><span data-ttu-id="18dc9-180">步驟 4︰從用戶端管理和提交工作</span><span class="sxs-lookup"><span data-stu-id="18dc9-180">Step 4: Manage and submit jobs from the client</span></span>

<span data-ttu-id="18dc9-181">若要在電腦上安裝 HPC Pack 用戶端公用程式，請從 Microsoft 下載中心下載 HPC Pack 2016 安裝程式檔案 (完整安裝)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span></span> <span data-ttu-id="18dc9-182">當您開始安裝時，請選擇安裝 **HPC Pack 用戶端公用程式**。</span><span class="sxs-lookup"><span data-stu-id="18dc9-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="18dc9-183">若要準備用戶端電腦，請在用戶端電腦上安裝 [HPC 叢集設定](hpcpack-2016-cluster.md)期間所使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="18dc9-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span></span> <span data-ttu-id="18dc9-184">使用標準 Windows 憑證管理程序，將公開憑證安裝至 [憑證 - 目前使用者] > [受信任的根憑證授權單位] 存放區。</span><span class="sxs-lookup"><span data-stu-id="18dc9-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="18dc9-185">您現在可以執行 HPC Pack 命令或使用 HPC Pack 工作管理員 GUI，以便利用 Azure AD 帳戶提交和管理叢集工作。</span><span class="sxs-lookup"><span data-stu-id="18dc9-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span></span> <span data-ttu-id="18dc9-186">如需工作提交選項，請參閱[在 Azure 中將 HPC 作業提交至 HPC Pack 叢集](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="18dc9-187">當您第一次嘗試在 Azure 中連接 HPC Pack 叢集時，就會出現快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="18dc9-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span></span> <span data-ttu-id="18dc9-188">輸入您的 Azure AD 認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="18dc9-188">Enter your Azure AD credentials to log in.</span></span> <span data-ttu-id="18dc9-189">隨即會快取權杖。</span><span class="sxs-lookup"><span data-stu-id="18dc9-189">The token is then cached.</span></span> <span data-ttu-id="18dc9-190">除非驗證變更或已清除快取的權杖，否則連往 Azure 中叢集的後續連線會使用快取的權杖。</span><span class="sxs-lookup"><span data-stu-id="18dc9-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span></span>
>
  
<span data-ttu-id="18dc9-191">例如，完成先前的步驟之後，您可以從內部部署用戶端查詢作業，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="18dc9-192">透過 Azure AD 整合提交作業的實用 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="18dc9-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-the-local-token-cache"></a><span data-ttu-id="18dc9-193">管理本機權杖快取</span><span class="sxs-lookup"><span data-stu-id="18dc9-193">Manage the local token cache</span></span>

<span data-ttu-id="18dc9-194">HPC Pack 2016 提供兩個新的 HPC PowerShell Cmdlet 來管理本機權杖快取。</span><span class="sxs-lookup"><span data-stu-id="18dc9-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span></span> <span data-ttu-id="18dc9-195">這些 Cmdlet 可用於非互動方式提交作業。</span><span class="sxs-lookup"><span data-stu-id="18dc9-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="18dc9-196">請參閱下列範例：</span><span class="sxs-lookup"><span data-stu-id="18dc9-196">See the following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-the-credentials-for-submitting-jobs-using-the-azure-ad-account"></a><span data-ttu-id="18dc9-197">設定認證以便利用 Azure AD 帳戶提交作業</span><span class="sxs-lookup"><span data-stu-id="18dc9-197">Set the credentials for submitting jobs using the Azure AD account</span></span> 

<span data-ttu-id="18dc9-198">有時候，您可能想要在 HPC 叢集使用者底下執行作業 (針對已加入網域的 HPC 叢集、以一個網域使用者身分執行；針對未加入網域的 HPC 叢集，以一個前端節點上的本機使用者身分執行)。</span><span class="sxs-lookup"><span data-stu-id="18dc9-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span></span>

1. <span data-ttu-id="18dc9-199">使用下列命令來設定認證︰</span><span class="sxs-lookup"><span data-stu-id="18dc9-199">Use the following commands to set the credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="18dc9-200">然後如下所示提交作業。</span><span class="sxs-lookup"><span data-stu-id="18dc9-200">Then submit the job as follows.</span></span> <span data-ttu-id="18dc9-201">作業/工作會在計算節點上以 $localUser 身分執行。</span><span class="sxs-lookup"><span data-stu-id="18dc9-201">The job/task runs under $localUser on the compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="18dc9-202">如果未使用 `Submit-HpcJob` 指定 `–Credential`，則會以 Azure AD 帳戶的本機對應使用者身分執行作業或工作。</span><span class="sxs-lookup"><span data-stu-id="18dc9-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span></span> <span data-ttu-id="18dc9-203">(HPC 叢集會使用與 Azure AD 帳戶相同的名稱建立本機使用者以執行工作。)</span><span class="sxs-lookup"><span data-stu-id="18dc9-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span></span>
    
3. <span data-ttu-id="18dc9-204">設定 Azure AD 帳戶的擴充資料。</span><span class="sxs-lookup"><span data-stu-id="18dc9-204">Set extended data for the Azure AD account.</span></span> <span data-ttu-id="18dc9-205">使用 Azure AD 帳戶在 Linux 節點上執行 MPI 作業時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="18dc9-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span></span>

   * <span data-ttu-id="18dc9-206">設定 Azure AD 帳戶本身的擴充資料</span><span class="sxs-lookup"><span data-stu-id="18dc9-206">Set extended data for the Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="18dc9-207">設定擴充資料並且以 HPC 叢集使用者身分執行</span><span class="sxs-lookup"><span data-stu-id="18dc9-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

