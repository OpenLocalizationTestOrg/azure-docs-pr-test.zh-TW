---
title: "如何為 Azure RemoteApp 建立自訂範本映像 | Microsoft Docs"
description: "了解如何為 Azure RemoteApp 建立自訂範本映像 您可以使用此範本與混合式或雲端集合搭配。"
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
ms.openlocfilehash: f529a5526f266c7dbac3c719b244d05ab7705941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-custom-template-image-for-azure-remoteapp"></a><span data-ttu-id="39131-104">如何為 Azure RemoteApp 建立自訂範本映像</span><span class="sxs-lookup"><span data-stu-id="39131-104">How to create a custom template image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="39131-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="39131-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="39131-106">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="39131-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="39131-107">Azure RemoteApp 會使用 Windows Server 2012 R2 範本映像來主控您要與使用者共用的所有程式。</span><span class="sxs-lookup"><span data-stu-id="39131-107">Azure RemoteApp uses a Windows Server 2012 R2 template image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="39131-108">若要建立自訂 RemoteApp 範本映像，您可以從現有的映像建立，或是建立新映像。</span><span class="sxs-lookup"><span data-stu-id="39131-108">To create a custom RemoteApp template image, you can start with an existing image or create a new one.</span></span> 

> [!TIP]
> <span data-ttu-id="39131-109">您知道您可以從 Azure VM 建立映像嗎？</span><span class="sxs-lookup"><span data-stu-id="39131-109">Did you know you can create an image from an Azure VM?</span></span> <span data-ttu-id="39131-110">這是真的，而且它可以減少匯入映像所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="39131-110">True story, and it cuts down on the amount of time it takes to import the image.</span></span> <span data-ttu-id="39131-111">請在 [這裡](remoteapp-image-on-azurevm.md)查明步驟。</span><span class="sxs-lookup"><span data-stu-id="39131-111">Check out the steps [here](remoteapp-image-on-azurevm.md).</span></span>
> 
> 

<span data-ttu-id="39131-112">可上傳用於 Azure RemoteApp 的映像有下列需求：</span><span class="sxs-lookup"><span data-stu-id="39131-112">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="39131-113">映像大小應為 MB 的倍數。</span><span class="sxs-lookup"><span data-stu-id="39131-113">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="39131-114">如果您嘗試上傳的映像大小不是正確的倍數，上傳作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="39131-114">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="39131-115">映像大小必須為 127 GB 或更小。</span><span class="sxs-lookup"><span data-stu-id="39131-115">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="39131-116">必須在 VHD 檔案上 (目前不支援 VHDX 檔案 [Hyper-V 虛擬硬碟])。</span><span class="sxs-lookup"><span data-stu-id="39131-116">It must be on a VHD file (VHDX files [Hyper-V virtual hard drives] are not currently supported).</span></span>
* <span data-ttu-id="39131-117">VHD 不能是第 2 代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="39131-117">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="39131-118">VHD 可以固定大小或動態擴充。</span><span class="sxs-lookup"><span data-stu-id="39131-118">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="39131-119">建議採用動態擴充 VHD 的做法，因為這會比固定大小 VHD 檔案更快速地上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="39131-119">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="39131-120">磁碟必須使用主開機記錄 (MBR) 分割樣式進行初始化。</span><span class="sxs-lookup"><span data-stu-id="39131-120">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="39131-121">GUID 磁碟分割資料表 (GPT) 磁碟分割樣式不受支援。</span><span class="sxs-lookup"><span data-stu-id="39131-121">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="39131-122">VHD 必須包含單一 Windows Server 2012 R2 安裝。</span><span class="sxs-lookup"><span data-stu-id="39131-122">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="39131-123">它可包含多個磁碟區，但只有其中一個包含 Windows 安裝。</span><span class="sxs-lookup"><span data-stu-id="39131-123">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="39131-124">必須安裝「遠端桌面工作階段主機 (RDSH)」角色和「桌面體驗」功能。</span><span class="sxs-lookup"><span data-stu-id="39131-124">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="39131-125">*請勿* 安裝「遠端桌面連線代理人」角色。</span><span class="sxs-lookup"><span data-stu-id="39131-125">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="39131-126">必須停用「加密檔案系統 (EFS)」。</span><span class="sxs-lookup"><span data-stu-id="39131-126">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="39131-127">映像必須使用參數 **/oobe /generalize /shutdown** 進行 SYSPREP 處理 (請不要使用 **/mode:vm** 參數)。</span><span class="sxs-lookup"><span data-stu-id="39131-127">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="39131-128">不支援從快照鏈結上傳您 VHD。</span><span class="sxs-lookup"><span data-stu-id="39131-128">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="39131-129">**開始之前**</span><span class="sxs-lookup"><span data-stu-id="39131-129">**Before you begin**</span></span>

<span data-ttu-id="39131-130">在建立服務之前，您必須執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="39131-130">You need to do the following before creating the service:</span></span>

* <span data-ttu-id="39131-131">[註冊](https://azure.microsoft.com/services/remoteapp/) RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="39131-131">[Sign up](https://azure.microsoft.com/services/remoteapp/) for RemoteApp.</span></span>
* <span data-ttu-id="39131-132">在 Active Directory 中建立使用者帳戶，以做為 RemoteApp 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="39131-132">Create a user account in Active Directory to use as the RemoteApp service account.</span></span> <span data-ttu-id="39131-133">限制此帳戶的權限，使其只能將機器加入網域中。</span><span class="sxs-lookup"><span data-stu-id="39131-133">Restrict the permissions for this account so that it can only join machines to the domain.</span></span> <span data-ttu-id="39131-134">如需詳細資訊，請參閱 [設定 RemoteApp 的 Azure Active Directory](remoteapp-ad.md) 。</span><span class="sxs-lookup"><span data-stu-id="39131-134">See [Configure Azure Active Directory for RemoteApp](remoteapp-ad.md) for more information.</span></span>
* <span data-ttu-id="39131-135">收集內部部署網路的相關資訊：IP 位址資訊和 VPN 裝置詳細資料。</span><span class="sxs-lookup"><span data-stu-id="39131-135">Gather information about your on-premises network: IP address information and VPN device details.</span></span>
* <span data-ttu-id="39131-136">安裝 [Azure PowerShell](/powershell/azure/overview) 模組。</span><span class="sxs-lookup"><span data-stu-id="39131-136">Install the [Azure PowerShell](/powershell/azure/overview) module.</span></span>
* <span data-ttu-id="39131-137">收集您想授與存取權之使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="39131-137">Gather information about the users that you want to grant access to.</span></span> <span data-ttu-id="39131-138">這可以是使用者 Microsoft 帳戶資訊或 Active Directory 工作帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="39131-138">This can be either Microsoft account information or Active Directory work account information for users.</span></span>

## <a name="create-a-template-image"></a><span data-ttu-id="39131-139">建立範本映像</span><span class="sxs-lookup"><span data-stu-id="39131-139">Create a template image</span></span>
<span data-ttu-id="39131-140">以下是從頭建立新範本映像的高階步驟：</span><span class="sxs-lookup"><span data-stu-id="39131-140">These are the high level steps to create a new template image from scratch:</span></span>

1. <span data-ttu-id="39131-141">找出 Windows Server 2012 R2 Update DVD 或 ISO 映像。</span><span class="sxs-lookup"><span data-stu-id="39131-141">Locate a Windows Server 2012 R2 Update DVD or ISO image.</span></span>
2. <span data-ttu-id="39131-142">建立 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="39131-142">Create a VHD file.</span></span>
3. <span data-ttu-id="39131-143">安裝 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="39131-143">Install Windows Server 2012 R2.</span></span>
4. <span data-ttu-id="39131-144">安裝「遠端桌面工作階段主機 (RDSH)」角色和「桌面體驗」功能。</span><span class="sxs-lookup"><span data-stu-id="39131-144">Install the Remote Desktop Session Host (RDSH) role and the Desktop Experience feature.</span></span>
5. <span data-ttu-id="39131-145">安裝您的應用程式所需的其他功能。</span><span class="sxs-lookup"><span data-stu-id="39131-145">Install additional features required by your applications.</span></span>
6. <span data-ttu-id="39131-146">安裝及設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="39131-146">Install and configure your applications.</span></span> <span data-ttu-id="39131-147">若要讓共用應用程式更加容易，請將任何您要共用的 App 或程式加入此映像的 [開始] 功能表，特別是在 **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 中。</span><span class="sxs-lookup"><span data-stu-id="39131-147">To make sharing apps easier, add any apps or programs that you want to share to the **Start** menu of the image, specifically in **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.</span></span>
7. <span data-ttu-id="39131-148">執行您的應用程式所需的任何其他 Windows 設定。</span><span class="sxs-lookup"><span data-stu-id="39131-148">Perform any additional Windows configurations required by your applications.</span></span>
8. <span data-ttu-id="39131-149">停用「加密檔案系統 (EFS)」。</span><span class="sxs-lookup"><span data-stu-id="39131-149">Disable the Encrypting File System (EFS).</span></span>
9. <span data-ttu-id="39131-150">**必要：** 前往 Windows Update 並安裝所有重要的更新。</span><span class="sxs-lookup"><span data-stu-id="39131-150">**REQUIRED:** Go to Windows Update and install all important updates.</span></span>
10. <span data-ttu-id="39131-151">進行映像的 SYSPREP 處理。</span><span class="sxs-lookup"><span data-stu-id="39131-151">SYSPREP the image.</span></span>

<span data-ttu-id="39131-152">建立新映像的詳細步驟為：</span><span class="sxs-lookup"><span data-stu-id="39131-152">The detailed steps for creating a new image are:</span></span>

1. <span data-ttu-id="39131-153">找出 Windows Server 2012 R2 Update DVD 或 ISO 映像。</span><span class="sxs-lookup"><span data-stu-id="39131-153">Locate a Windows Server 2012 R2 Update DVD or ISO image.</span></span>
2. <span data-ttu-id="39131-154">使用「磁碟管理」建立 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="39131-154">Create a VHD file by using Disk Management.</span></span>
   
   1. <span data-ttu-id="39131-155">啟動「磁碟管理」(diskmgmt.msc)。</span><span class="sxs-lookup"><span data-stu-id="39131-155">Launch Disk Management (diskmgmt.msc).</span></span>
   2. <span data-ttu-id="39131-156">建立會動態擴充、大小 40 GB 或更大的 VHD。</span><span class="sxs-lookup"><span data-stu-id="39131-156">Create a dynamically expanding VHD of 40 GB or more in size.</span></span> <span data-ttu-id="39131-157">(請估計 Windows、您的應用程式和自訂所需的空間量。</span><span class="sxs-lookup"><span data-stu-id="39131-157">(Estimate the amount of space needed for Windows, your applications, and customizations.</span></span> <span data-ttu-id="39131-158">已安裝 RDSH 角色和「桌面體驗」功能的 Windows Server 將需要約 10 GB 的空間)。</span><span class="sxs-lookup"><span data-stu-id="39131-158">Windows Server with the RDSH role and Desktop Experience feature installed will require about 10 GB of space).</span></span>
      
      1. <span data-ttu-id="39131-159">按一下 [動作 > 建立 VHD]。</span><span class="sxs-lookup"><span data-stu-id="39131-159">Click **Action > Create VHD**.</span></span>
      2. <span data-ttu-id="39131-160">指定位置、大小和 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="39131-160">Specify the location, size, and VHD format.</span></span> <span data-ttu-id="39131-161">選取 [動態擴充]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="39131-161">Select **Dynamically expanding**, and then click **OK**.</span></span>
      
      <span data-ttu-id="39131-162">此作業會執行數秒。</span><span class="sxs-lookup"><span data-stu-id="39131-162">This will run for several seconds.</span></span> <span data-ttu-id="39131-163">VHD 建立完成後，您會在 [磁碟管理] 主控台中看見不具任何磁碟機代號、狀態為「未初始化」的新磁碟。</span><span class="sxs-lookup"><span data-stu-id="39131-163">When the VHD creation is complete, you should see a new disk without any drive letter and in “Not initialized" state in the Disk Management console.</span></span>
      
      * <span data-ttu-id="39131-164">以滑鼠右鍵按一下磁碟 (不是未配置的空間)，然後按一下 [初始化磁碟] 。</span><span class="sxs-lookup"><span data-stu-id="39131-164">Right-click the disk (not the unallocated space), and then click **Initialize Disk**.</span></span> <span data-ttu-id="39131-165">選取 [MBR] \(主開機記錄) 做為磁碟分割樣式，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="39131-165">Select **MBR** (Master Boot Record) as the partition style, and then click **OK**.</span></span>
      * <span data-ttu-id="39131-166">建立新的磁碟區： 以滑鼠右鍵按一下未配置的空間，然後按一下 [新增簡單磁碟區] 。</span><span class="sxs-lookup"><span data-stu-id="39131-166">Create a new volume: right-click the unallocated space, and then click **New Simple Volume**.</span></span> <span data-ttu-id="39131-167">您可以接受精靈中的預設值，但請務必指派磁碟機代號，以避免在上傳範本映像時發生問題。</span><span class="sxs-lookup"><span data-stu-id="39131-167">You can accept the defaults in the wizard, but make sure you assign a drive letter to avoid potential problems when you upload the template image.</span></span>
      * <span data-ttu-id="39131-168">以滑鼠右鍵按一下磁碟，然後按一下 [Detach VHD] 。</span><span class="sxs-lookup"><span data-stu-id="39131-168">Right-click the disk, and then click **Detach VHD**.</span></span>
3. <span data-ttu-id="39131-169">安裝 Windows Server 2012 R2：</span><span class="sxs-lookup"><span data-stu-id="39131-169">Install Windows Server 2012 R2:</span></span>
   
   1. <span data-ttu-id="39131-170">建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="39131-170">Create a new virtual machine.</span></span> <span data-ttu-id="39131-171">在 [Hyper-V 管理員] 或 [用戶端 Hyper-V] 中使用 [新增虛擬機器精靈]。</span><span class="sxs-lookup"><span data-stu-id="39131-171">Use the New Virtual Machine Wizard in Hyper-V Manager or Client Hyper-V.</span></span>
      1. <span data-ttu-id="39131-172">在 [Specify Generation] 頁面上，選擇 [Generation 1]。</span><span class="sxs-lookup"><span data-stu-id="39131-172">On the Specify Generation page, choose  **Generation 1**.</span></span>
      2. <span data-ttu-id="39131-173">在 [連接虛擬硬碟] 頁面上選取 [使用現有的虛擬硬碟] ，然後瀏覽至您在上一個步驟中建立的 VHD。</span><span class="sxs-lookup"><span data-stu-id="39131-173">On the Connect Virtual Hard Disk page, select **Use an existing virtual hard disk**, and browse to the VHD you created in the previous step.</span></span>
      3. <span data-ttu-id="39131-174">在 [安裝選項] 頁面上，選取 [從開機 CD/DVD_ROM 安裝作業系統]，然後選取您的 Windows Server 2012 R2 安裝媒體的位置。</span><span class="sxs-lookup"><span data-stu-id="39131-174">On the Installation Options page, select **Install an operating system from a boot CD/DVD_ROM**, and then select the location of your Windows Server 2012 R2 installation media.</span></span>
      4. <span data-ttu-id="39131-175">在精靈中選擇其他安裝 Windows 和應用程式所需的選項。</span><span class="sxs-lookup"><span data-stu-id="39131-175">Choose other options in the wizard necessary to install Windows and your applications.</span></span> <span data-ttu-id="39131-176">完成精靈。</span><span class="sxs-lookup"><span data-stu-id="39131-176">Finish the wizard.</span></span>
   2. <span data-ttu-id="39131-177">精靈完成後，請編輯虛擬機器設定並進行安裝 Windows 和程式所需的任何其他變更 (例如虛擬處理器數目)，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="39131-177">After the wizard finishes, edit the settings of the virtual machine and make any other changes necessary to install Windows and your programs, such as the number of virtual processors, and then click **OK**.</span></span>
   3. <span data-ttu-id="39131-178">連接到虛擬機器，並安裝 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="39131-178">Connect to the virtual machine and install Windows Server 2012 R2.</span></span>
4. <span data-ttu-id="39131-179">安裝「遠端桌面工作階段主機 (RDSH)」角色和「桌面體驗」功能：</span><span class="sxs-lookup"><span data-stu-id="39131-179">Install the Remote Desktop Session Host (RDSH) role and the Desktop Experience feature:</span></span>
   1. <span data-ttu-id="39131-180">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="39131-180">Launch Server Manager.</span></span>
   2. <span data-ttu-id="39131-181">在 [歡迎使用] 畫面或 [管理] 功能表上，按一下 [新增角色和功能]。</span><span class="sxs-lookup"><span data-stu-id="39131-181">Click **Add Roles and features** on the Welcome screen or from the **Manage** menu.</span></span>
   3. <span data-ttu-id="39131-182">在 [開始之前] 頁面上，按 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="39131-182">Click **Next** on the Before You Begin page.</span></span>
   4. <span data-ttu-id="39131-183">選取 [角色型或功能型安裝]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="39131-183">Select **Role-based or feature-based installation**, and then click **Next**.</span></span>
   5. <span data-ttu-id="39131-184">從清單中選取本機機器，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="39131-184">Select the local machine from the list, and then click **Next**.</span></span>
   6. <span data-ttu-id="39131-185">選取 [遠端桌面服務]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="39131-185">Select **Remote Desktop Services**, and then click **Next**.</span></span>
   7. <span data-ttu-id="39131-186">展開 [使用者介面與基礎結構]，然後選取 [桌面體驗]。</span><span class="sxs-lookup"><span data-stu-id="39131-186">Expand **User Interfaces and Infrastructure** and select **Desktop Experience**.</span></span>
   8. <span data-ttu-id="39131-187">按一下 [新增功能]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="39131-187">Click **Add Features**, and then click **Next**.</span></span>
   9. <span data-ttu-id="39131-188">在 [遠端桌面服務] 頁面上，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="39131-188">On the Remote Desktop Services page, click **Next**.</span></span>
   10. <span data-ttu-id="39131-189">按一下 [遠端桌面工作階段主機] 。</span><span class="sxs-lookup"><span data-stu-id="39131-189">Click **Remote Desktop Session Host**.</span></span>
   11. <span data-ttu-id="39131-190">按一下 [新增功能]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="39131-190">Click **Add Features**, and then click **Next**.</span></span>
   12. <span data-ttu-id="39131-191">在 [確認安裝選項] 頁面上，選取 [必要時自動重新啟動目的地伺服器]，然後在出現重新啟動警告時按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="39131-191">On the Confirm installation selections page, select **Restart the destination server automatically if required**, and then click **Yes** on the restart warning.</span></span>
   13. <span data-ttu-id="39131-192">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="39131-192">Click **Install**.</span></span> <span data-ttu-id="39131-193">電腦會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="39131-193">The computer will restart.</span></span>
5. <span data-ttu-id="39131-194">安裝您的應用程式所需的其他功能，例如 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="39131-194">Install additional features required by your applications, such as the .NET Framework 3.5.</span></span> <span data-ttu-id="39131-195">若要安裝這些功能，請執行 [新增角色和功能] 精靈。</span><span class="sxs-lookup"><span data-stu-id="39131-195">To install the features, run the Add Roles and Features Wizard.</span></span>
6. <span data-ttu-id="39131-196">安裝並設定您要透過 RemoteApp 發佈的程式和應用程式。</span><span class="sxs-lookup"><span data-stu-id="39131-196">Install and configure the programs and applications you want to publish through RemoteApp.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39131-197">請在安裝應用程式之前先安裝 RDSH 角色，以確保可在映像上傳至 RemoteApp 之前發現任何關於應用程式相容性的問題。</span><span class="sxs-lookup"><span data-stu-id="39131-197">Install the RDSH role before installing applications to ensure that any issues with application compatibility are discovered before the image is uploaded to RemoteApp.</span></span>
> 
> <span data-ttu-id="39131-198">請確定應用程式的捷徑 (**.lnk** 檔案) 出現在所有使用者的 [開始] 功能表 (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs)。</span><span class="sxs-lookup"><span data-stu-id="39131-198">Make sure a shortcut to your application (**.lnk** file) appears in the **Start** menu for all users (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs).</span></span> <span data-ttu-id="39131-199">也請確定您在 [開始] 功能表中看到的圖示是您想讓使用者看到的。</span><span class="sxs-lookup"><span data-stu-id="39131-199">Also ensure that the icon you see in the **Start** menu is what you want users to see.</span></span> <span data-ttu-id="39131-200">如果不是，請變更圖示。</span><span class="sxs-lookup"><span data-stu-id="39131-200">If not, change it.</span></span> <span data-ttu-id="39131-201">(您不一定要將應用程式新增至 [開始] 功能表，但這樣做的話在 RemoteApp 中發佈應用程式會更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="39131-201">(You do not *have* to add the application to the Start menu, but it makes it much easier to publish the application in RemoteApp.</span></span> <span data-ttu-id="39131-202">否則，當您發佈應用程式時，您必須提供應用程式的安裝路徑。)</span><span class="sxs-lookup"><span data-stu-id="39131-202">Otherwise, you have to provide the installation path for the application when you publish the app.)</span></span>
> 
> 

1. <span data-ttu-id="39131-203">執行您的應用程式所需的任何其他 Windows 設定。</span><span class="sxs-lookup"><span data-stu-id="39131-203">Perform any additional Windows configurations required by your applications.</span></span>
2. <span data-ttu-id="39131-204">停用「加密檔案系統 (EFS)」。</span><span class="sxs-lookup"><span data-stu-id="39131-204">Disable the Encrypting File System (EFS).</span></span> <span data-ttu-id="39131-205">在提高權限的命令視窗上執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="39131-205">Run the following command at an elevated command window:</span></span>
   
     <span data-ttu-id="39131-206">Fsutil 行為集 disableencryption 1</span><span class="sxs-lookup"><span data-stu-id="39131-206">Fsutil behavior set disableencryption 1</span></span>
   
   <span data-ttu-id="39131-207">或者，您可以在登錄中設定或新增下列 DWORD 值：</span><span class="sxs-lookup"><span data-stu-id="39131-207">Alternatively, you can set or add the following DWORD value in the registry:</span></span>
   
     <span data-ttu-id="39131-208">HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1</span><span class="sxs-lookup"><span data-stu-id="39131-208">HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1</span></span>
3. <span data-ttu-id="39131-209">如果您是在 Azure 虛擬機器內建立映像，請重新命名 **\%windir%\Panther\Unattend.xml** 檔案，以免上傳指令碼稍後無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="39131-209">If you are building your image inside an Azure virtual machine, rename the **\%windir%\Panther\Unattend.xml** file, as this will block the upload script used later from working.</span></span> <span data-ttu-id="39131-210">將此檔案名稱變更為 Unattend.old，以便當您需要回復部署時，仍舊保有這個檔案可用。</span><span class="sxs-lookup"><span data-stu-id="39131-210">Change the name of this file to Unattend.old so that you will still have the file in case you need to revert your deployment.</span></span>
4. <span data-ttu-id="39131-211">前往 Windows Update 並安裝所有重要的更新。</span><span class="sxs-lookup"><span data-stu-id="39131-211">Go to Windows Update and install all important updates.</span></span> <span data-ttu-id="39131-212">您可能必須執行 Windows Update 很多次才能取得所有更新。</span><span class="sxs-lookup"><span data-stu-id="39131-212">You might need to run Windows Update multiple times to get all updates.</span></span> <span data-ttu-id="39131-213">(有時候您安裝更新，而該更新本身又需要另外的更新。)</span><span class="sxs-lookup"><span data-stu-id="39131-213">(Sometimes you install an update, and that update itself requires an update.)</span></span>
5. <span data-ttu-id="39131-214">進行映像的 SYSPREP 處理。</span><span class="sxs-lookup"><span data-stu-id="39131-214">SYSPREP the image.</span></span> <span data-ttu-id="39131-215">在提高權限的命令提示字元上執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="39131-215">At an elevated command prompt, run the following command:</span></span>
   
   <span data-ttu-id="39131-216">**C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**</span><span class="sxs-lookup"><span data-stu-id="39131-216">**C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**</span></span>
   
   <span data-ttu-id="39131-217">**注意：**請不要使用 SYSPREP 命令的 **/mode:vm** 參數，即使這是虛擬機器亦然。</span><span class="sxs-lookup"><span data-stu-id="39131-217">**Note:** Do not use the **/mode:vm** switch of the SYSPREP command even though this is a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39131-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39131-218">Next steps</span></span>
<span data-ttu-id="39131-219">現在您的自訂範本映像已經就緒，您需要將該映像上傳至您的 RemoteApp 收藏。</span><span class="sxs-lookup"><span data-stu-id="39131-219">Now that you have your custom template image, you need to upload that image to your RemoteApp collection.</span></span> <span data-ttu-id="39131-220">使用下列文章中的資訊建立您的收藏：</span><span class="sxs-lookup"><span data-stu-id="39131-220">Use the information in the following articles to create your collection:</span></span>

* [<span data-ttu-id="39131-221">如何建立 RemoteApp 的混合式收藏</span><span class="sxs-lookup"><span data-stu-id="39131-221">How to create a hybrid collection of RemoteApp</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="39131-222">如何建立 RemoteApp 的雲端收藏</span><span class="sxs-lookup"><span data-stu-id="39131-222">How to create a cloud collection of RemoteApp</span></span>](remoteapp-create-cloud-deployment.md)

