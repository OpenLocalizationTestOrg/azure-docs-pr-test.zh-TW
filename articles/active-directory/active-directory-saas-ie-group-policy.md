---
title: "aaaDeploy Azure 存取面板延伸模組使用 GPO 的 ie |Microsoft 文件"
description: "如何 toouse 群組原則 toodeploy hello Internet Explorer 附加元件 hello 我的應用程式入口網站。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="71e42-103">如何 tooDeploy hello Internet explorer 使用群組原則的存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="71e42-103">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="71e42-104">本教學課程會示範如何 toouse 群組原則 tooremotely hello 存取面板延伸模組 Internet Explorer 的電腦上安裝您的使用者。</span><span class="sxs-lookup"><span data-stu-id="71e42-104">This tutorial shows how toouse group policy tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="71e42-105">這項擴充功能都需要 Internet Explorer，使用者需要 toosign 到應用程式使用的設定[密碼型單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="71e42-105">This extension is required for Internet Explorer users who need toosign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="71e42-106">建議系統管理員自動化 hello 部署這項擴充功能。</span><span class="sxs-lookup"><span data-stu-id="71e42-106">It is recommended that admins automate hello deployment of this extension.</span></span> <span data-ttu-id="71e42-107">否則，使用者有 toodownload 和 hello 延伸自行安裝，是很容易出錯的 toouser 錯誤，需要系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="71e42-107">Otherwise, users have toodownload and install hello extension themselves, which is prone toouser error and requires administrator permissions.</span></span> <span data-ttu-id="71e42-108">本教學課程涵蓋使用群組原則自動化軟體部署的一種方法。</span><span class="sxs-lookup"><span data-stu-id="71e42-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="71e42-109">深入了解群組原則。</span><span class="sxs-lookup"><span data-stu-id="71e42-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="71e42-110">hello 存取面板延伸模組也會提供如[Chrome](https://go.microsoft.com/fwLink/?LinkID=311859)和[Firefox](https://go.microsoft.com/fwLink/?LinkID=626998)，這兩者需要系統管理員權限 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="71e42-110">hello Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions tooinstall.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71e42-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="71e42-111">Prerequisites</span></span>
* <span data-ttu-id="71e42-112">您已設定[Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，及您已加入您的使用者機器 tooyour 網域。</span><span class="sxs-lookup"><span data-stu-id="71e42-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>
* <span data-ttu-id="71e42-113">您必須擁有 hello [編輯設定] 的權限 tooedit hello 群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="71e42-113">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="71e42-114">根據預設，hello 下列安全性群組的成員擁有此權限： 網域系統管理員、 企業系統管理員和 Group Policy Creator Owners。</span><span class="sxs-lookup"><span data-stu-id="71e42-114">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="71e42-115">深入了解。</span><span class="sxs-lookup"><span data-stu-id="71e42-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a><span data-ttu-id="71e42-116">步驟 1： 建立 hello 的發佈點</span><span class="sxs-lookup"><span data-stu-id="71e42-116">Step 1: Create hello Distribution Point</span></span>
<span data-ttu-id="71e42-117">首先，您必須在網路位置上 hello 機器可存取您想 tooremotely 安裝 hello 擴充功能上放置 hello 安裝程式套件。</span><span class="sxs-lookup"><span data-stu-id="71e42-117">First, you must place hello installer package on a network location that can be accessed by hello machines that you wish tooremotely install hello extension on.</span></span> <span data-ttu-id="71e42-118">toodo，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="71e42-118">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="71e42-119">系統管理員身分登入 toohello 伺服器</span><span class="sxs-lookup"><span data-stu-id="71e42-119">Log on toohello server as an administrator</span></span>
2. <span data-ttu-id="71e42-120">在 hello**伺服器管理員**視窗中，跳過**檔案和存放服務**。</span><span class="sxs-lookup"><span data-stu-id="71e42-120">In hello **Server Manager** window, go too**Files and Storage Services**.</span></span>
   
    ![開啟檔案和存放服務](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="71e42-122">移 toohello**共用** 索引標籤。然後按一下工作 > 新增共用...</span><span class="sxs-lookup"><span data-stu-id="71e42-122">Go toohello **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![開啟檔案和存放服務](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="71e42-124">完整的 hello**新增共用精靈**和設定權限 tooensure，可以存取從使用者的機器。</span><span class="sxs-lookup"><span data-stu-id="71e42-124">Complete hello **New Share Wizard** and set permissions tooensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="71e42-125">深入了解共用。</span><span class="sxs-lookup"><span data-stu-id="71e42-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="71e42-126">下載下列 Microsoft Windows Installer 套件 （.msi 檔案） 的 hello:[存取面板 Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="71e42-126">Download hello following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="71e42-127">複製 hello installer 封裝 tooa 所需的 hello 共用上的位置。</span><span class="sxs-lookup"><span data-stu-id="71e42-127">Copy hello installer package tooa desired location on hello share.</span></span>
   
    ![複製 hello.msi 檔案 toohello 共用。](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="71e42-129">請確認用戶端電腦會從 hello 共用可以 tooaccess hello 安裝程式套件。</span><span class="sxs-lookup"><span data-stu-id="71e42-129">Verify that your client machines are able tooaccess hello installer package from hello share.</span></span> 

## <a name="step-2-create-hello-group-policy-object"></a><span data-ttu-id="71e42-130">步驟 2： 建立 hello 群組原則物件</span><span class="sxs-lookup"><span data-stu-id="71e42-130">Step 2: Create hello Group Policy Object</span></span>
1. <span data-ttu-id="71e42-131">裝載 Active Directory 網域服務 (AD DS) 安裝 toohello 伺服器上的記錄。</span><span class="sxs-lookup"><span data-stu-id="71e42-131">Log on toohello server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="71e42-132">在 hello 伺服器管理員中，移過**工具** > **群組原則管理**。</span><span class="sxs-lookup"><span data-stu-id="71e42-132">In hello Server Manager, go too**Tools** > **Group Policy Management**.</span></span>
   
    ![移 tooTools > 群組原則管理](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="71e42-134">Hello hello 左窗格中**群組原則管理**視窗中，檢視您的組織單位 (OU) 階層，並判斷在哪些範圍中，您想要 tooapply hello 群組原則。</span><span class="sxs-lookup"><span data-stu-id="71e42-134">In hello left pane of hello **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like tooapply hello group policy.</span></span> <span data-ttu-id="71e42-135">比方說，您可能會決定 toopick 小型的 OU toodeploy tooa 少數使用者來進行測試，或您可能會選取最上層 OU toodeploy tooyour 整個組織。</span><span class="sxs-lookup"><span data-stu-id="71e42-135">For instance, you may decide toopick a small OU toodeploy tooa few users for testing, or you may pick a top-level OU toodeploy tooyour entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="71e42-136">如果您想要 toocreate 或編輯您的組織單位 (Ou)，切換後 toohello 伺服器管理員，並跳過**工具** > **Active Directory 使用者和電腦**。</span><span class="sxs-lookup"><span data-stu-id="71e42-136">If you would like toocreate or edit your Organization Units (OUs), switch back toohello Server Manager and go too**Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="71e42-137">一旦您選取 OU，以滑鼠右鍵按一下它然後選取 [在這個網域中建立 GPO 並連結到...]</span><span class="sxs-lookup"><span data-stu-id="71e42-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![建立新的 GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="71e42-139">在 hello**新的 GPO**提示字元中，輸入名稱的 hello 新群組原則物件。</span><span class="sxs-lookup"><span data-stu-id="71e42-139">In hello **New GPO** prompt, type in a name for hello new Group Policy Object.</span></span>
   
    ![名稱 hello 新的 GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="71e42-141">以滑鼠右鍵按一下 hello 建立，並選取 群組原則物件**編輯**。</span><span class="sxs-lookup"><span data-stu-id="71e42-141">Right-click hello Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![編輯 hello 新的 GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a><span data-ttu-id="71e42-143">步驟 3： 指派 hello 安裝套件</span><span class="sxs-lookup"><span data-stu-id="71e42-143">Step 3: Assign hello Installation Package</span></span>
1. <span data-ttu-id="71e42-144">判斷您是否想要根據 toodeploy hello 延伸模組**電腦設定**或**使用者設定**。</span><span class="sxs-lookup"><span data-stu-id="71e42-144">Determine whether you would like toodeploy hello extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="71e42-145">當使用[電腦設定](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx)，無論哪個使用者登入 tooit hello 電腦上安裝 hello 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="71e42-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello extension is installed on hello computer regardless of which users log on tooit.</span></span> <span data-ttu-id="71e42-146">與[使用者設定](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx)，使用者擁有 hello 擴充功能安裝，無論哪一台電腦登入。</span><span class="sxs-lookup"><span data-stu-id="71e42-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have hello extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="71e42-147">Hello hello 左窗格中**群組原則管理編輯器** 視窗中，移 tooeither 的 hello 下列的組態類型視您所選擇的資料夾路徑：</span><span class="sxs-lookup"><span data-stu-id="71e42-147">In hello left pane of hello **Group Policy Management Editor** window, go tooeither of hello following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="71e42-148">以滑鼠右鍵按一下 [軟體安裝]，然後選取 [新增] > [套件...]</span><span class="sxs-lookup"><span data-stu-id="71e42-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![建立新的軟體安裝套件](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="71e42-150">包含從 hello 安裝程式套件移 toohello 共用的資料夾[步驟 1： 建立 hello 的發佈點](#step-1-create-the-distribution-point)，選取 hello.msi 檔案，然後按一下**開啟**。</span><span class="sxs-lookup"><span data-stu-id="71e42-150">Go toohello shared folder that contains hello installer package from [Step 1: Create hello Distribution Point](#step-1-create-the-distribution-point), select hello .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="71e42-151">如果 hello 共用位於相同的伺服器上，確認您要執行 hello 網路檔案的路徑，而不是 hello 本機檔案路徑存取 hello.msi。</span><span class="sxs-lookup"><span data-stu-id="71e42-151">If hello share is located on this same server, verify that you are accessing hello .msi through hello network file path, rather than hello local file path.</span></span>
   > 
   > 
   
    ![選取 hello 安裝套件 hello 共用資料夾中。](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="71e42-153">在 hello**部署軟體**提示，請選取**指派**部署方法。</span><span class="sxs-lookup"><span data-stu-id="71e42-153">In hello **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="71e42-154">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="71e42-154">Then click **OK**.</span></span>
   
    ![選取 [已指派]，然後按一下 [確定]。](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="71e42-156">hello 延伸模組現在是已部署的 toohello 您選取的 OU。</span><span class="sxs-lookup"><span data-stu-id="71e42-156">hello extension is now deployed toohello OU that you selected.</span></span> [<span data-ttu-id="71e42-157">深入了解群組原則軟體安裝。</span><span class="sxs-lookup"><span data-stu-id="71e42-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a><span data-ttu-id="71e42-158">步驟 4： 自動啟用 hello Internet Explorer 擴充功能</span><span class="sxs-lookup"><span data-stu-id="71e42-158">Step 4: Auto-Enable hello Extension for Internet Explorer</span></span>
<span data-ttu-id="71e42-159">此外 toorunning hello 安裝程式，Internet Explorer 的每一個延伸模組必須明確啟用才能使用。</span><span class="sxs-lookup"><span data-stu-id="71e42-159">In addition toorunning hello installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="71e42-160">遵循以下 tooenable 的 hello 步驟 hello 使用群組原則的存取面板延伸模組：</span><span class="sxs-lookup"><span data-stu-id="71e42-160">Follow hello steps below tooenable hello Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="71e42-161">在 [hello**群組原則管理編輯器**] 視窗中，移 tooeither 的下列的路徑，您在中的組態類型視選擇的 hello[步驟 3： 指派 hello 安裝套件](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="71e42-161">In hello **Group Policy Management Editor** window, go tooeither of hello following paths, depending on which type of configuration you chose in [Step 3: Assign hello Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="71e42-162">以滑鼠右鍵按一下 [附加元件清單]，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="71e42-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="71e42-163">![編輯附加元件清單。](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="71e42-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="71e42-164">在 hello**附加元件清單**視窗中，選取**啟用**。</span><span class="sxs-lookup"><span data-stu-id="71e42-164">In hello **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="71e42-165">然後，在 hello**選項**區段中，按一下**顯示...**.</span><span class="sxs-lookup"><span data-stu-id="71e42-165">Then, under hello **Options** section, click **Show...**.</span></span>
   
    ![按一下 [啟用]，然後按一下 [顯示...]](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="71e42-167">在 hello**顯示內容**視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="71e42-167">In hello **Show Contents** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="71e42-168">Hello 第一個資料行 (hello**值名稱**欄位)、 複製及貼上下列類別識別碼 hello:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="71e42-168">For hello first column (hello **Value Name** field), copy and paste hello following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="71e42-169">Hello 第二個資料行 (hello**值**欄位)，輸入下列值的 hello:`1`</span><span class="sxs-lookup"><span data-stu-id="71e42-169">For hello second column (hello **Value** field), type in hello following value: `1`</span></span>
   3. <span data-ttu-id="71e42-170">按一下**確定**tooclose hello**顯示內容**視窗。</span><span class="sxs-lookup"><span data-stu-id="71e42-170">Click **OK** tooclose hello **Show Contents** window.</span></span>
      
      ![填寫 hello 和上述所指定的值。](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="71e42-172">按一下**確定**tooapply 變更並關閉 hello**附加元件清單**視窗。</span><span class="sxs-lookup"><span data-stu-id="71e42-172">Click **OK** tooapply your changes and close hello **Add-on List** window.</span></span>

<span data-ttu-id="71e42-173">hello 擴充功能應該已啟用的 hello 機器 hello 選取 OU。</span><span class="sxs-lookup"><span data-stu-id="71e42-173">hello extension should now be enabled for hello machines in hello selected OU.</span></span> [<span data-ttu-id="71e42-174">進一步瞭解使用群組原則 tooenable 或停用 Internet Explorer 附加元件。</span><span class="sxs-lookup"><span data-stu-id="71e42-174">Learn more about using group policy tooenable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="71e42-175">步驟 5 (選用)：停用 [記住密碼] 提示</span><span class="sxs-lookup"><span data-stu-id="71e42-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="71e42-176">當使用者登入 toowebsites 使用 hello 存取面板延伸模組，Internet Explorer 可能會顯示 hello 下列提示詢問 「 您希望？ toostore 密碼 」</span><span class="sxs-lookup"><span data-stu-id="71e42-176">When users sign-in toowebsites using hello Access Panel Extension, Internet Explorer may show hello following prompt asking "Would you like toostore your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="71e42-177">如果您想 tooprevent 看到此提示使用者，然後依照 tooprevent 自動完成下列步驟來 hello 與記住的密碼：</span><span class="sxs-lookup"><span data-stu-id="71e42-177">If you wish tooprevent your users from seeing this prompt, then follow hello steps below tooprevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="71e42-178">在 hello**群組原則管理編輯器**視窗中，移 toohello 下面所列的路徑。</span><span class="sxs-lookup"><span data-stu-id="71e42-178">In hello **Group Policy Management Editor** window, go toohello path listed below.</span></span> <span data-ttu-id="71e42-179">這項組態設定僅提供於 [使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="71e42-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="71e42-180">找出 hello 設定名為**開啟表單上的使用者名稱和密碼的 hello 自動完成功能**。</span><span class="sxs-lookup"><span data-stu-id="71e42-180">Find hello setting named **Turn on hello auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="71e42-181">舊版的 Active Directory 可能會列出這項設定使用 hello 名稱**不允許自動完成 toosave 密碼**。</span><span class="sxs-lookup"><span data-stu-id="71e42-181">Previous versions of Active Directory may list this setting with hello name **Do not allow auto-complete toosave passwords**.</span></span> <span data-ttu-id="71e42-182">hello 組態，該設定不同於 hello 設定本教學課程中所述。</span><span class="sxs-lookup"><span data-stu-id="71e42-182">hello configuration for that setting differs from hello setting described in this tutorial.</span></span>
   > 
   > 
   
    ![請記住這個 toolook 在使用者設定。](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="71e42-184">以滑鼠右鍵按一下 hello 上方設定，然後選取**編輯**。</span><span class="sxs-lookup"><span data-stu-id="71e42-184">Right click hello above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="71e42-185">在標題為 hello 視窗**開啟表單上的使用者名稱和密碼的 hello 自動完成功能**，選取**已停用**。</span><span class="sxs-lookup"><span data-stu-id="71e42-185">In hello window titled **Turn on hello auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![選取 [停用]](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="71e42-187">按一下**確定**tooapply 這些變更並關閉 hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="71e42-187">Click **OK** tooapply these changes and close hello window.</span></span>

<span data-ttu-id="71e42-188">使用者將不再是無法 toostore 其認證，或使用自動完成 tooaccess 預存認證。</span><span class="sxs-lookup"><span data-stu-id="71e42-188">Users will no longer be able toostore their credentials or use auto-complete tooaccess previously stored credentials.</span></span> <span data-ttu-id="71e42-189">不過，此原則允許使用者 toocontinue toouse 對於其他類型的表單欄位，例如搜尋欄位自動完成。</span><span class="sxs-lookup"><span data-stu-id="71e42-189">However, this policy does allow users toocontinue toouse auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="71e42-190">如果使用者已選擇 toostore 某些認證之後，會啟用此原則，此原則將*不*清除已儲存的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="71e42-190">If this policy is enabled after users have chosen toostore some credentials, this policy will *not* clear hello credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-hello-deployment"></a><span data-ttu-id="71e42-191">步驟 6： 測試部署的 hello</span><span class="sxs-lookup"><span data-stu-id="71e42-191">Step 6: Testing hello Deployment</span></span>
<span data-ttu-id="71e42-192">如果 hello 擴充部署成功，請遵循下方 tooverify hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="71e42-192">Follow hello steps below tooverify if hello extension deployment was successful:</span></span>

1. <span data-ttu-id="71e42-193">如果您使用部署**電腦設定**，登入用戶端電腦屬於您在選取的 OU toohello[步驟 2： 建立群組原則物件 hello](#step-2-create-the-group-policy-object)。</span><span class="sxs-lookup"><span data-stu-id="71e42-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs toohello OU that you selected in [Step 2: Create hello Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="71e42-194">如果您使用部署**使用者設定**，請確定 toosign 中的所屬 toothat OU 使用者的身分。</span><span class="sxs-lookup"><span data-stu-id="71e42-194">If you deployed using **User Configuration**, make sure toosign in as a user who belongs toothat OU.</span></span>
2. <span data-ttu-id="71e42-195">可能需要一些符號集 hello 群組原則的變更與此機器 toofully 更新。</span><span class="sxs-lookup"><span data-stu-id="71e42-195">It may take a couple sign ins for hello group policy changes toofully update with this machine.</span></span> <span data-ttu-id="71e42-196">tooforce hello 更新中，開啟**命令提示字元**視窗並執行下列命令的 hello:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="71e42-196">tooforce hello update, open a **Command Prompt** window and run hello following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="71e42-197">您必須重新啟動 hello 機器 hello 安裝 tootake 地方。</span><span class="sxs-lookup"><span data-stu-id="71e42-197">You must restart hello machine for hello installation tootake place.</span></span> <span data-ttu-id="71e42-198">開機可能需要相當多的時間比平常 hello 延伸模組時安裝。</span><span class="sxs-lookup"><span data-stu-id="71e42-198">Bootup may take significantly more time than usual while hello extension installs.</span></span>
4. <span data-ttu-id="71e42-199">重新開機之後，開啟 **Internet Explorer**。</span><span class="sxs-lookup"><span data-stu-id="71e42-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="71e42-200">Hello hello 視窗的右上角，按一下**工具**（hello 齒輪圖示），然後選取**管理附加元件**。</span><span class="sxs-lookup"><span data-stu-id="71e42-200">On hello upper-right corner of hello window, click **Tools** (hello gear icon), and then select **Manage add-ons**.</span></span>
   
    ![移 tooTools > 管理附加元件](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="71e42-202">在 hello**管理附加元件**視窗中，確認該 hello**存取面板延伸模組**已安裝且其**狀態**已經過設定**已啟用**.</span><span class="sxs-lookup"><span data-stu-id="71e42-202">In hello **Manage Add-ons** window, verify that hello **Access Panel Extension** has been installed and that its **Status** has been set too**Enabled**.</span></span>
   
    ![確認 存取面板延伸模組已安裝並啟用該 hello。](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="71e42-204">相關文章</span><span class="sxs-lookup"><span data-stu-id="71e42-204">Related Articles</span></span>
* [<span data-ttu-id="71e42-205">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="71e42-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="71e42-206">搭配 Azure Active Directory 的應用程式存取和單一登入</span><span class="sxs-lookup"><span data-stu-id="71e42-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="71e42-207">疑難排解 hello Internet explorer 的 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="71e42-207">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

