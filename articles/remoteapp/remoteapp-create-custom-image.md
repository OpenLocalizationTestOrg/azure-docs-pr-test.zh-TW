---
title: "aaaHow toocreate 自訂的範本映像的 Azure RemoteApp |Microsoft 文件"
description: "了解 toocreate 自訂範本的 Azure RemoteApp 的映像。 您可以使用此範本與混合式或雲端集合搭配。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a><span data-ttu-id="ca4e3-104">Toocreate 自訂範本的 Azure RemoteApp 的映像</span><span class="sxs-lookup"><span data-stu-id="ca4e3-104">How toocreate a custom template image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ca4e3-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ca4e3-106">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ca4e3-107">Azure RemoteApp 使用 Windows Server 2012 R2 範本映像 toohost 所有 hello 程式，您會想 tooshare 與您的使用者。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-107">Azure RemoteApp uses a Windows Server 2012 R2 template image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="ca4e3-108">toocreate 自訂的 RemoteApp 範本映像，您可以開始使用現有的映像或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-108">toocreate a custom RemoteApp template image, you can start with an existing image or create a new one.</span></span> 

> [!TIP]
> <span data-ttu-id="ca4e3-109">您知道您可以從 Azure VM 建立映像嗎？</span><span class="sxs-lookup"><span data-stu-id="ca4e3-109">Did you know you can create an image from an Azure VM?</span></span> <span data-ttu-id="ca4e3-110">True 的劇本，並減少了 hello 一段時間它採用 tooimport hello 映像。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-110">True story, and it cuts down on hello amount of time it takes tooimport hello image.</span></span> <span data-ttu-id="ca4e3-111">簽出 hello 步驟[這裡](remoteapp-image-on-azurevm.md)。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-111">Check out hello steps [here](remoteapp-image-on-azurevm.md).</span></span>
> 
> 

<span data-ttu-id="ca4e3-112">可以上傳 Azure RemoteApp 搭配使用的 hello 映像的 hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="ca4e3-112">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="ca4e3-113">hello 映像大小應該是 mb/s 的倍數。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-113">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="ca4e3-114">如果您嘗試 tooupload 不精確的多個映像，hello 上傳將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-114">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="ca4e3-115">hello 影像大小必須為 127 GB 或更小。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-115">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="ca4e3-116">必須在 VHD 檔案上 (目前不支援 VHDX 檔案 [Hyper-V 虛擬硬碟])。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-116">It must be on a VHD file (VHDX files [Hyper-V virtual hard drives] are not currently supported).</span></span>
* <span data-ttu-id="ca4e3-117">hello VHD 不能在第 2 代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-117">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="ca4e3-118">hello VHD 可以是固定大小或動態擴充。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-118">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="ca4e3-119">因為它會採用比固定大小的 VHD 檔案的較少時間 tooupload tooAzure，建議您使用動態擴充的 VHD。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-119">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="ca4e3-120">必須使用 hello 主開機記錄 (MBR) 磁碟分割樣式初始化磁碟 hello。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-120">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="ca4e3-121">不支援 hello GUID 磁碟分割表格 (GPT) 磁碟分割樣式。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-121">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="ca4e3-122">hello VHD 必須包含單一 Windows Server 2012 R2 的安裝。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-122">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="ca4e3-123">它可包含多個磁碟區，但只有其中一個包含 Windows 安裝。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-123">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="ca4e3-124">必須安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗功能。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-124">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="ca4e3-125">hello 遠端桌面連線代理人角色必須*不*安裝。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-125">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="ca4e3-126">必須停用 hello 加密檔案系統 (EFS)。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-126">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="ca4e3-127">hello 映像必須使用 hello 參數 SYSPREPed **/oobe /generalize /shutdown** (請勿使用 hello **/mode: vm**參數)。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-127">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="ca4e3-128">不支援從快照鏈結上傳您 VHD。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-128">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="ca4e3-129">**開始之前**</span><span class="sxs-lookup"><span data-stu-id="ca4e3-129">**Before you begin**</span></span>

<span data-ttu-id="ca4e3-130">您需要建立 hello 服務之前 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ca4e3-130">You need toodo hello following before creating hello service:</span></span>

* <span data-ttu-id="ca4e3-131">[註冊](https://azure.microsoft.com/services/remoteapp/) RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-131">[Sign up](https://azure.microsoft.com/services/remoteapp/) for RemoteApp.</span></span>
* <span data-ttu-id="ca4e3-132">建立使用者帳戶在 Active Directory toouse，為 hello RemoteApp 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-132">Create a user account in Active Directory toouse as hello RemoteApp service account.</span></span> <span data-ttu-id="ca4e3-133">限制此帳戶的 「 hello 」 權限，讓它只會將機器 toohello 網域。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-133">Restrict hello permissions for this account so that it can only join machines toohello domain.</span></span> <span data-ttu-id="ca4e3-134">如需詳細資訊，請參閱 [設定 RemoteApp 的 Azure Active Directory](remoteapp-ad.md) 。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-134">See [Configure Azure Active Directory for RemoteApp](remoteapp-ad.md) for more information.</span></span>
* <span data-ttu-id="ca4e3-135">收集內部部署網路的相關資訊：IP 位址資訊和 VPN 裝置詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-135">Gather information about your on-premises network: IP address information and VPN device details.</span></span>
* <span data-ttu-id="ca4e3-136">安裝 hello [Azure PowerShell](/powershell/azure/overview)模組。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-136">Install hello [Azure PowerShell](/powershell/azure/overview) module.</span></span>
* <span data-ttu-id="ca4e3-137">收集您想要 toogrant 存取的 hello 使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-137">Gather information about hello users that you want toogrant access to.</span></span> <span data-ttu-id="ca4e3-138">這可以是使用者 Microsoft 帳戶資訊或 Active Directory 工作帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-138">This can be either Microsoft account information or Active Directory work account information for users.</span></span>

## <a name="create-a-template-image"></a><span data-ttu-id="ca4e3-139">建立範本映像</span><span class="sxs-lookup"><span data-stu-id="ca4e3-139">Create a template image</span></span>
<span data-ttu-id="ca4e3-140">這些是 hello 高階步驟 toocreate 從頭新的範本映像：</span><span class="sxs-lookup"><span data-stu-id="ca4e3-140">These are hello high level steps toocreate a new template image from scratch:</span></span>

1. <span data-ttu-id="ca4e3-141">找出 Windows Server 2012 R2 Update DVD 或 ISO 映像。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-141">Locate a Windows Server 2012 R2 Update DVD or ISO image.</span></span>
2. <span data-ttu-id="ca4e3-142">建立 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-142">Create a VHD file.</span></span>
3. <span data-ttu-id="ca4e3-143">安裝 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-143">Install Windows Server 2012 R2.</span></span>
4. <span data-ttu-id="ca4e3-144">安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗 」 功能。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-144">Install hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature.</span></span>
5. <span data-ttu-id="ca4e3-145">安裝您的應用程式所需的其他功能。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-145">Install additional features required by your applications.</span></span>
6. <span data-ttu-id="ca4e3-146">安裝及設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-146">Install and configure your applications.</span></span> <span data-ttu-id="ca4e3-147">toomake 共用應用程式更容易，新增的任何應用程式或您想 tooshare toohello 程式**啟動**hello 映像，特別是在 **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 的功能表。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-147">toomake sharing apps easier, add any apps or programs that you want tooshare toohello **Start** menu of hello image, specifically in **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.</span></span>
7. <span data-ttu-id="ca4e3-148">執行您的應用程式所需的任何其他 Windows 設定。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-148">Perform any additional Windows configurations required by your applications.</span></span>
8. <span data-ttu-id="ca4e3-149">停用 hello 加密檔案系統 (EFS)。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-149">Disable hello Encrypting File System (EFS).</span></span>
9. <span data-ttu-id="ca4e3-150">**REQUIRED:** tooWindows Update 去安裝所有重要更新。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-150">**REQUIRED:** Go tooWindows Update and install all important updates.</span></span>
10. <span data-ttu-id="ca4e3-151">SYSPREP hello 映像。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-151">SYSPREP hello image.</span></span>

<span data-ttu-id="ca4e3-152">hello 建立新的映像的詳細的步驟如下：</span><span class="sxs-lookup"><span data-stu-id="ca4e3-152">hello detailed steps for creating a new image are:</span></span>

1. <span data-ttu-id="ca4e3-153">找出 Windows Server 2012 R2 Update DVD 或 ISO 映像。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-153">Locate a Windows Server 2012 R2 Update DVD or ISO image.</span></span>
2. <span data-ttu-id="ca4e3-154">使用「磁碟管理」建立 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-154">Create a VHD file by using Disk Management.</span></span>
   
   1. <span data-ttu-id="ca4e3-155">啟動「磁碟管理」(diskmgmt.msc)。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-155">Launch Disk Management (diskmgmt.msc).</span></span>
   2. <span data-ttu-id="ca4e3-156">建立會動態擴充、大小 40 GB 或更大的 VHD。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-156">Create a dynamically expanding VHD of 40 GB or more in size.</span></span> <span data-ttu-id="ca4e3-157">（評估 hello 工作量用於 Windows、 應用程式，以及自訂所需的空間。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-157">(Estimate hello amount of space needed for Windows, your applications, and customizations.</span></span> <span data-ttu-id="ca4e3-158">Windows Server 與 hello RDSH 角色和已安裝桌面體驗功能將需要大約 10 GB 的空間）。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-158">Windows Server with hello RDSH role and Desktop Experience feature installed will require about 10 GB of space).</span></span>
      
      1. <span data-ttu-id="ca4e3-159">按一下 [動作 > 建立 VHD]。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-159">Click **Action > Create VHD**.</span></span>
      2. <span data-ttu-id="ca4e3-160">指定 hello 位置、 大小和 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-160">Specify hello location, size, and VHD format.</span></span> <span data-ttu-id="ca4e3-161">選取 動態擴充，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-161">Select **Dynamically expanding**, and then click **OK**.</span></span>
      
      <span data-ttu-id="ca4e3-162">此作業會執行數秒。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-162">This will run for several seconds.</span></span> <span data-ttu-id="ca4e3-163">Hello VHD 建立完成時，您應該會看到新的磁碟不含任何磁碟機代號，並在 hello 磁碟管理 主控台中，「 未初始化 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-163">When hello VHD creation is complete, you should see a new disk without any drive letter and in “Not initialized" state in hello Disk Management console.</span></span>
      
      * <span data-ttu-id="ca4e3-164">Hello 磁碟 （不 hello 未配置的空間） 上按一下滑鼠右鍵，然後按一下**初始化磁碟**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-164">Right-click hello disk (not hello unallocated space), and then click **Initialize Disk**.</span></span> <span data-ttu-id="ca4e3-165">選取**MBR** （主開機記錄） 作為 hello 磁碟分割樣式，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-165">Select **MBR** (Master Boot Record) as hello partition style, and then click **OK**.</span></span>
      * <span data-ttu-id="ca4e3-166">建立新的磁碟區： hello 未配置空間，以滑鼠右鍵按一下，然後按一下**新增簡單磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-166">Create a new volume: right-click hello unallocated space, and then click **New Simple Volume**.</span></span> <span data-ttu-id="ca4e3-167">您可以接受 hello hello 精靈中的預設值，但請確定當您上傳 hello 範本映像時，指派磁碟機代號 tooavoid 潛在問題。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-167">You can accept hello defaults in hello wizard, but make sure you assign a drive letter tooavoid potential problems when you upload hello template image.</span></span>
      * <span data-ttu-id="ca4e3-168">Hello 磁碟上按一下滑鼠右鍵，然後按一下**中斷連結 VHD**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-168">Right-click hello disk, and then click **Detach VHD**.</span></span>
3. <span data-ttu-id="ca4e3-169">安裝 Windows Server 2012 R2：</span><span class="sxs-lookup"><span data-stu-id="ca4e3-169">Install Windows Server 2012 R2:</span></span>
   
   1. <span data-ttu-id="ca4e3-170">建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-170">Create a new virtual machine.</span></span> <span data-ttu-id="ca4e3-171">使用新的虛擬機器精靈，在 HYPER-V 管理員] 或 [用戶端 HYPER-V hello。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-171">Use hello New Virtual Machine Wizard in Hyper-V Manager or Client Hyper-V.</span></span>
      1. <span data-ttu-id="ca4e3-172">在 hello 指定世代 頁面上，選擇 **第 1 代**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-172">On hello Specify Generation page, choose  **Generation 1**.</span></span>
      2. <span data-ttu-id="ca4e3-173">在 hello 連接虛擬硬碟 頁面上，選取 **使用現有的虛擬硬碟**，並瀏覽 toohello hello 先前步驟中所建立的 VHD。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-173">On hello Connect Virtual Hard Disk page, select **Use an existing virtual hard disk**, and browse toohello VHD you created in hello previous step.</span></span>
      3. <span data-ttu-id="ca4e3-174">在 hello 安裝選項 頁面上，選取 **安裝作業系統從開機 CD/DVD_ROM**，然後選取 Windows Server 2012 R2 安裝媒體的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-174">On hello Installation Options page, select **Install an operating system from a boot CD/DVD_ROM**, and then select hello location of your Windows Server 2012 R2 installation media.</span></span>
      4. <span data-ttu-id="ca4e3-175">選擇 hello 精靈需要 tooinstall Windows 中的其他選項和您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-175">Choose other options in hello wizard necessary tooinstall Windows and your applications.</span></span> <span data-ttu-id="ca4e3-176">完成 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-176">Finish hello wizard.</span></span>
   2. <span data-ttu-id="ca4e3-177">Hello 精靈完成後，編輯 hello hello 虛擬機器設定，並變更任何其他必要 tooinstall Windows 與程式，例如 hello 虛擬處理器數目，，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-177">After hello wizard finishes, edit hello settings of hello virtual machine and make any other changes necessary tooinstall Windows and your programs, such as hello number of virtual processors, and then click **OK**.</span></span>
   3. <span data-ttu-id="ca4e3-178">Toohello 虛擬機器連線，並安裝 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-178">Connect toohello virtual machine and install Windows Server 2012 R2.</span></span>
4. <span data-ttu-id="ca4e3-179">安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗功能：</span><span class="sxs-lookup"><span data-stu-id="ca4e3-179">Install hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature:</span></span>
   1. <span data-ttu-id="ca4e3-180">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-180">Launch Server Manager.</span></span>
   2. <span data-ttu-id="ca4e3-181">按一下**新增角色及功能**hello 歡迎畫面上，或從 hello**管理**功能表。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-181">Click **Add Roles and features** on hello Welcome screen or from hello **Manage** menu.</span></span>
   3. <span data-ttu-id="ca4e3-182">按一下**下一步**hello 在您開始前 頁面上。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-182">Click **Next** on hello Before You Begin page.</span></span>
   4. <span data-ttu-id="ca4e3-183">選取 角色型或功能型安裝，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-183">Select **Role-based or feature-based installation**, and then click **Next**.</span></span>
   5. <span data-ttu-id="ca4e3-184">從 [hello] 清單中，選取 hello 本機電腦，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-184">Select hello local machine from hello list, and then click **Next**.</span></span>
   6. <span data-ttu-id="ca4e3-185">選取 [遠端桌面服務]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-185">Select **Remote Desktop Services**, and then click **Next**.</span></span>
   7. <span data-ttu-id="ca4e3-186">展開 [使用者介面與基礎結構]，然後選取 [桌面體驗]。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-186">Expand **User Interfaces and Infrastructure** and select **Desktop Experience**.</span></span>
   8. <span data-ttu-id="ca4e3-187">按一下 [新增功能]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-187">Click **Add Features**, and then click **Next**.</span></span>
   9. <span data-ttu-id="ca4e3-188">在 hello 遠端桌面服務 頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-188">On hello Remote Desktop Services page, click **Next**.</span></span>
   10. <span data-ttu-id="ca4e3-189">按一下 [遠端桌面工作階段主機] 。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-189">Click **Remote Desktop Session Host**.</span></span>
   11. <span data-ttu-id="ca4e3-190">按一下 [新增功能]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-190">Click **Add Features**, and then click **Next**.</span></span>
   12. <span data-ttu-id="ca4e3-191">Hello 確認安裝選項 頁面上，選取**必要時自動重新啟動 hello 目的地伺服器**，然後按一下**是**hello 上重新啟動的警告。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-191">On hello Confirm installation selections page, select **Restart hello destination server automatically if required**, and then click **Yes** on hello restart warning.</span></span>
   13. <span data-ttu-id="ca4e3-192">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-192">Click **Install**.</span></span> <span data-ttu-id="ca4e3-193">hello 電腦將重新啟動。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-193">hello computer will restart.</span></span>
5. <span data-ttu-id="ca4e3-194">安裝您的應用程式，例如 hello.NET Framework 3.5 所需的其他功能。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-194">Install additional features required by your applications, such as hello .NET Framework 3.5.</span></span> <span data-ttu-id="ca4e3-195">tooinstall hello 功能，執行 hello 新增角色及功能精靈。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-195">tooinstall hello features, run hello Add Roles and Features Wizard.</span></span>
6. <span data-ttu-id="ca4e3-196">安裝和設定 hello 程式以及您想要透過 RemoteApp toopublish 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-196">Install and configure hello programs and applications you want toopublish through RemoteApp.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca4e3-197">安裝 hello RDSH 角色之前安裝的應用程式 tooensure hello 映像之前，會發現任何問題的應用程式相容性上傳 tooRemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-197">Install hello RDSH role before installing applications tooensure that any issues with application compatibility are discovered before hello image is uploaded tooRemoteApp.</span></span>
> 
> <span data-ttu-id="ca4e3-198">請確定快顯 tooyour 應用程式 (**.lnk**檔案) 會出現在 hello**啟動**(%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs) 的所有使用者的功能表。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-198">Make sure a shortcut tooyour application (**.lnk** file) appears in hello **Start** menu for all users (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs).</span></span> <span data-ttu-id="ca4e3-199">此外也請確認您在 hello 中看到該 hello 圖示**啟動**功能表是您想要使用者 toosee。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-199">Also ensure that hello icon you see in hello **Start** menu is what you want users toosee.</span></span> <span data-ttu-id="ca4e3-200">如果不是，請變更圖示。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-200">If not, change it.</span></span> <span data-ttu-id="ca4e3-201">(不這麼做*有*tooadd hello 應用程式 toohello 開始功能表上，但它讓它更容易 toopublish hello 應用程式中的 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-201">(You do not *have* tooadd hello application toohello Start menu, but it makes it much easier toopublish hello application in RemoteApp.</span></span> <span data-ttu-id="ca4e3-202">否則，您必須 tooprovide hello 安裝路徑 hello 應用程式發行 hello 應用程式時。）</span><span class="sxs-lookup"><span data-stu-id="ca4e3-202">Otherwise, you have tooprovide hello installation path for hello application when you publish hello app.)</span></span>
> 
> 

1. <span data-ttu-id="ca4e3-203">執行您的應用程式所需的任何其他 Windows 設定。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-203">Perform any additional Windows configurations required by your applications.</span></span>
2. <span data-ttu-id="ca4e3-204">停用 hello 加密檔案系統 (EFS)。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-204">Disable hello Encrypting File System (EFS).</span></span> <span data-ttu-id="ca4e3-205">執行下列命令，在提升權限的命令視窗中的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca4e3-205">Run hello following command at an elevated command window:</span></span>
   
     <span data-ttu-id="ca4e3-206">Fsutil 行為集 disableencryption 1</span><span class="sxs-lookup"><span data-stu-id="ca4e3-206">Fsutil behavior set disableencryption 1</span></span>
   
   <span data-ttu-id="ca4e3-207">或者，您可以設定，或新增下列 DWORD 值 hello 登錄中的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca4e3-207">Alternatively, you can set or add hello following DWORD value in hello registry:</span></span>
   
     <span data-ttu-id="ca4e3-208">HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1</span><span class="sxs-lookup"><span data-stu-id="ca4e3-208">HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1</span></span>
3. <span data-ttu-id="ca4e3-209">如果您要建置您的映像，在 Azure 虛擬機器內，重新命名 hello  **\%windir%\Panther\Unattend.xml**檔案，這樣將會封鎖 hello 上傳用指令碼，稍後無法運作。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-209">If you are building your image inside an Azure virtual machine, rename hello **\%windir%\Panther\Unattend.xml** file, as this will block hello upload script used later from working.</span></span> <span data-ttu-id="ca4e3-210">變更這個檔案 tooUnattend.old hello 名稱，使您仍會有 hello 檔案，以防您需要 toorevert 您的部署。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-210">Change hello name of this file tooUnattend.old so that you will still have hello file in case you need toorevert your deployment.</span></span>
4. <span data-ttu-id="ca4e3-211">TooWindows Update 去安裝所有重要更新。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-211">Go tooWindows Update and install all important updates.</span></span> <span data-ttu-id="ca4e3-212">您可能需要 toorun Windows Update 多次 tooget 所有更新。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-212">You might need toorun Windows Update multiple times tooget all updates.</span></span> <span data-ttu-id="ca4e3-213">(有時候您安裝更新，而該更新本身又需要另外的更新。)</span><span class="sxs-lookup"><span data-stu-id="ca4e3-213">(Sometimes you install an update, and that update itself requires an update.)</span></span>
5. <span data-ttu-id="ca4e3-214">SYSPREP hello 映像。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-214">SYSPREP hello image.</span></span> <span data-ttu-id="ca4e3-215">在提升權限的命令提示字元執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca4e3-215">At an elevated command prompt, run hello following command:</span></span>
   
   <span data-ttu-id="ca4e3-216">**C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**</span><span class="sxs-lookup"><span data-stu-id="ca4e3-216">**C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**</span></span>
   
   <span data-ttu-id="ca4e3-217">**注意：**不使用 hello **/mode: vm** hello SYSPREP 命令，即使這是虛擬機器的參數。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-217">**Note:** Do not use hello **/mode:vm** switch of hello SYSPREP command even though this is a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca4e3-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca4e3-218">Next steps</span></span>
<span data-ttu-id="ca4e3-219">既然您已自訂的範本映像，您需要 tooupload 該映像 tooyour RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="ca4e3-219">Now that you have your custom template image, you need tooupload that image tooyour RemoteApp collection.</span></span> <span data-ttu-id="ca4e3-220">請使用您的集合在下列文章 toocreate hello hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="ca4e3-220">Use hello information in hello following articles toocreate your collection:</span></span>

* [<span data-ttu-id="ca4e3-221">如何 toocreate RemoteApp 的混合式集合</span><span class="sxs-lookup"><span data-stu-id="ca4e3-221">How toocreate a hybrid collection of RemoteApp</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="ca4e3-222">如何 toocreate 的 RemoteApp 雲端集合</span><span class="sxs-lookup"><span data-stu-id="ca4e3-222">How toocreate a cloud collection of RemoteApp</span></span>](remoteapp-create-cloud-deployment.md)

