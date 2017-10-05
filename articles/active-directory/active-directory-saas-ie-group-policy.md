---
title: "使用 GPO 部署適用於 IE 的 Azure 存取面板延伸模組 | Microsoft Docs"
description: "如何使用群組原則針對我的 app 入口網站部署 Internet Explorer 附加元件。"
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
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="166c9-103">如何使用群組原則部署 Internet Explorer 的存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="166c9-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="166c9-104">本教學課程示範如何使用群組原則，在您的使用者電腦上遠端安裝 Internet Explorer 的存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="166c9-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="166c9-105">需要登入使用 [密碼單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)設定的應用程式的 Internet Explorer 使用者，都需要此延伸模組。</span><span class="sxs-lookup"><span data-stu-id="166c9-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="166c9-106">我們建議系統管理員自動化部署這個延伸模組。</span><span class="sxs-lookup"><span data-stu-id="166c9-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="166c9-107">否則，使用者必須自行下載並安裝延伸模組，這樣很容易發生使用者錯誤，而且需要系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="166c9-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="166c9-108">本教學課程涵蓋使用群組原則自動化軟體部署的一種方法。</span><span class="sxs-lookup"><span data-stu-id="166c9-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="166c9-109">深入了解群組原則。</span><span class="sxs-lookup"><span data-stu-id="166c9-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="166c9-110">存取面板延伸模組也可供 [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) 和 [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998) 使用，兩者都不需要系統管理員權限即可安裝。</span><span class="sxs-lookup"><span data-stu-id="166c9-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="166c9-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="166c9-111">Prerequisites</span></span>
* <span data-ttu-id="166c9-112">您已設定了 [Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，並且已將使用者的電腦加入網域。</span><span class="sxs-lookup"><span data-stu-id="166c9-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="166c9-113">您必須擁有「編輯設定」權限，才能編輯群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="166c9-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="166c9-114">根據預設，下列安全性群組的成員擁有此權限：網域系統管理員、企業系統管理員及群組原則建立者擁有者。</span><span class="sxs-lookup"><span data-stu-id="166c9-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="166c9-115">深入了解。</span><span class="sxs-lookup"><span data-stu-id="166c9-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="166c9-116">步驟 1：建立發佈點</span><span class="sxs-lookup"><span data-stu-id="166c9-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="166c9-117">首先，您必須將安裝程式套件放在網路位置上，該位置可供您要在上面遠端安裝延伸模組的電腦進行存取。</span><span class="sxs-lookup"><span data-stu-id="166c9-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="166c9-118">若要這樣做，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="166c9-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="166c9-119">以系統管理員身分登入伺服器</span><span class="sxs-lookup"><span data-stu-id="166c9-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="166c9-120">在 [伺服器管理員] 視窗中，移至 [檔案和存放服務]。</span><span class="sxs-lookup"><span data-stu-id="166c9-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![開啟檔案和存放服務](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="166c9-122">移至 [共用]  索引標籤。然後按一下 [工作] > [新增共用...]</span><span class="sxs-lookup"><span data-stu-id="166c9-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![開啟檔案和存放服務](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="166c9-124">完成 [新增共用精靈]  並設定權限以確保可以從您的使用者電腦存取該精靈。</span><span class="sxs-lookup"><span data-stu-id="166c9-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="166c9-125">深入了解共用。</span><span class="sxs-lookup"><span data-stu-id="166c9-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="166c9-126">下載下列 Microsoft Windows 安裝程式套件 (.msi file)：[Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="166c9-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="166c9-127">將安裝程式套件複製到共用上想要的位置。</span><span class="sxs-lookup"><span data-stu-id="166c9-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![將 .msi 檔案複製到共用。](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="166c9-129">確認用戶端電腦能夠從共用存取安裝程式套件。</span><span class="sxs-lookup"><span data-stu-id="166c9-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="166c9-130">步驟 2：建立群組原則物件</span><span class="sxs-lookup"><span data-stu-id="166c9-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="166c9-131">登入裝載 Active Directory 網域服務 (AD DS) 安裝的伺服器。</span><span class="sxs-lookup"><span data-stu-id="166c9-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="166c9-132">在 [伺服器管理員] 中，移至 [工具]  >  [群組原則管理]。</span><span class="sxs-lookup"><span data-stu-id="166c9-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![移至工具 > 群組原則管理](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="166c9-134">在 [群組原則管理]  視窗的左窗格中，檢視您的組織單位 (OU) 階層並決定您想要套用群組原則的範圍。</span><span class="sxs-lookup"><span data-stu-id="166c9-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="166c9-135">例如，您可能決定針對測試挑選小型 OU 以部署到少數使用者，或者您可能會挑選最上層 OU 以部署到整個組織。</span><span class="sxs-lookup"><span data-stu-id="166c9-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="166c9-136">如果您想要建立或編輯您的組織單位 (OU)，切換回 [伺服器管理員]，然後移至 [工具]  >  [Active Directory 使用者和電腦]。</span><span class="sxs-lookup"><span data-stu-id="166c9-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="166c9-137">一旦您選取 OU，以滑鼠右鍵按一下它然後選取 [在這個網域中建立 GPO 並連結到...]</span><span class="sxs-lookup"><span data-stu-id="166c9-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![建立新的 GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="166c9-139">在 [新增 GPO]  提示中，輸入新的群組原則物件的名稱。</span><span class="sxs-lookup"><span data-stu-id="166c9-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![命名新的 GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="166c9-141">以滑鼠右鍵按一下您建立的群組原則物件，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="166c9-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![編輯新的 GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="166c9-143">步驟 3：指派安裝套件</span><span class="sxs-lookup"><span data-stu-id="166c9-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="166c9-144">決定您想要根據 [電腦設定] 或 [使用者設定] 部署延伸模組。</span><span class="sxs-lookup"><span data-stu-id="166c9-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="166c9-145">當使用[電腦設定](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx)時，不論哪一個使用者登入電腦，都會在電腦上安裝延伸模組。</span><span class="sxs-lookup"><span data-stu-id="166c9-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="166c9-146">使用[使用者設定](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx)時，無論使用者登入哪一台電腦，都會在該電腦上安裝延伸模組。</span><span class="sxs-lookup"><span data-stu-id="166c9-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="166c9-147">在 [群組原則管理編輯器]  視窗的左窗格中，移至下列其中一個資料夾路徑，根據您選擇的設定類型而定：</span><span class="sxs-lookup"><span data-stu-id="166c9-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="166c9-148">以滑鼠右鍵按一下 [軟體安裝]，然後選取 [新增] > [套件...]</span><span class="sxs-lookup"><span data-stu-id="166c9-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![建立新的軟體安裝套件](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="166c9-150">移至共用資料夾，該資料夾包含[步驟 1：建立發佈點](#step-1-create-the-distribution-point)的安裝程式套件，選取 .msi 檔案，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="166c9-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="166c9-151">如果共用位於相同的伺服器上，確認您是透過網路檔案路徑存取此 .msi，，而不是本機檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="166c9-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![從共用資料夾中選取安裝套件。](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="166c9-153">在 [部署軟體] 提示中，針對您的部署方法選取 [已指派]。</span><span class="sxs-lookup"><span data-stu-id="166c9-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="166c9-154">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="166c9-154">Then click **OK**.</span></span>
   
    ![選取 [已指派]，然後按一下 [確定]。](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="166c9-156">延伸模組現在已部署至您所選取的 OU。</span><span class="sxs-lookup"><span data-stu-id="166c9-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="166c9-157">深入了解群組原則軟體安裝。</span><span class="sxs-lookup"><span data-stu-id="166c9-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="166c9-158">步驟 4：自動啟用 Internet Explorer 的延伸模組</span><span class="sxs-lookup"><span data-stu-id="166c9-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="166c9-159">除了執行安裝程式之外，Internet Explorer 的每個延伸模組必須明確啟用才能使用。</span><span class="sxs-lookup"><span data-stu-id="166c9-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="166c9-160">遵循下列步驟以使用群組原則啟用存取面板延伸模組：</span><span class="sxs-lookup"><span data-stu-id="166c9-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="166c9-161">在 [群組原則管理編輯器]  視窗中，移至下列其中一個路徑，根據您在 [步驟 3：指派安裝套件](#step-3-assign-the-installation-package)中選擇的設定類型而定：</span><span class="sxs-lookup"><span data-stu-id="166c9-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="166c9-162">以滑鼠右鍵按一下 [附加元件清單]，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="166c9-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="166c9-163">![編輯附加元件清單。](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="166c9-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="166c9-164">在 [附加元件清單] 視窗中，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="166c9-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="166c9-165">然後，在 [選項] 區段中，按一下 [顯示...]。</span><span class="sxs-lookup"><span data-stu-id="166c9-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![按一下 [啟用]，然後按一下 [顯示...]](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="166c9-167">在 [顯示內容]  視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="166c9-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="166c9-168">對於第一個資料行 ([值名稱] 欄位)，複製和貼上以下類別識別碼：`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="166c9-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="166c9-169">對於第二個資料行 ([值] 欄位)，輸入下列值：`1`</span><span class="sxs-lookup"><span data-stu-id="166c9-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="166c9-170">按一下 [確定] 關閉 [顯示內容] 視窗。</span><span class="sxs-lookup"><span data-stu-id="166c9-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![填寫值，如上述步驟所指定。](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="166c9-172">按一下 [確定] 以套用變更並關閉 [附加元件清單] 視窗。</span><span class="sxs-lookup"><span data-stu-id="166c9-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="166c9-173">延伸模組現在應該已在所選 OU 中的機器啟用。</span><span class="sxs-lookup"><span data-stu-id="166c9-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="166c9-174">深入了解使用群組原則啟用或停用 Internet Explorer 附加元件。</span><span class="sxs-lookup"><span data-stu-id="166c9-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="166c9-175">步驟 5 (選用)：停用 [記住密碼] 提示</span><span class="sxs-lookup"><span data-stu-id="166c9-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="166c9-176">當使用者登入使用存取面板擴充功能的網站時，Internet Explorer 可能會顯示下列提示詢問「是否要儲存密碼？」</span><span class="sxs-lookup"><span data-stu-id="166c9-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="166c9-177">如果不想使用者看到此提示，請依照下列步驟防止自動完成記住密碼：</span><span class="sxs-lookup"><span data-stu-id="166c9-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="166c9-178">在 [群組原則管理編輯器]  視窗中，移至下文列出的路徑。</span><span class="sxs-lookup"><span data-stu-id="166c9-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="166c9-179">這項組態設定僅提供於 [使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="166c9-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="166c9-180">尋找名為 [開啟表單上使用者名稱和密碼的自動完成功能] 的設定。</span><span class="sxs-lookup"><span data-stu-id="166c9-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="166c9-181">舊版的 Active Directory 可能會列出這項設定，但名為 [不允許以自動完成儲存密碼]。</span><span class="sxs-lookup"><span data-stu-id="166c9-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="166c9-182">該設定的組態不同於本教學課程中所描述的設定。</span><span class="sxs-lookup"><span data-stu-id="166c9-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![記得要在 [使用者設定] 下尋找此項目。](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="166c9-184">以滑鼠右鍵按一下上述設定，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="166c9-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="166c9-185">在標題為 [開啟表單上使用者名稱和密碼的自動完成功能] 的視窗中選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="166c9-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![選取 [停用]](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="166c9-187">按一下 [確定]  套用這些變更並關閉視窗。</span><span class="sxs-lookup"><span data-stu-id="166c9-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="166c9-188">使用者不能再繼續儲存其認證，或使用自動完成來存取之前儲存的認證。</span><span class="sxs-lookup"><span data-stu-id="166c9-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="166c9-189">不過，這項原則允許使用者對其他類型的表單欄位可繼續使用自動完成，例如搜尋欄位。</span><span class="sxs-lookup"><span data-stu-id="166c9-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="166c9-190">如果在使用者選擇儲存某些認證之後才啟用這項原則，此原則 *不* 會清除已儲存的認證。</span><span class="sxs-lookup"><span data-stu-id="166c9-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="166c9-191">步驟 6：測試部署</span><span class="sxs-lookup"><span data-stu-id="166c9-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="166c9-192">請遵循下列步驟以確認延伸模組是否成功部署：</span><span class="sxs-lookup"><span data-stu-id="166c9-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="166c9-193">如果您使用 [電腦組態] 進行部署，請登入屬於您在 [步驟 2：建立群組原則物件](#step-2-create-the-group-policy-object)中選取之 OU 的用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="166c9-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="166c9-194">如果您使用 [使用者組態] 進行部署，請務必以屬於該 OU 的使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="166c9-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="166c9-195">可能要登入好幾次才能讓群組原則變更完全更新至此電腦。</span><span class="sxs-lookup"><span data-stu-id="166c9-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="166c9-196">若要強制更新，開啟 [命令提示字元] 視窗，然後執行下列命令：`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="166c9-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="166c9-197">您必須重新啟動電腦才能進行安裝。</span><span class="sxs-lookup"><span data-stu-id="166c9-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="166c9-198">安裝延伸模組時，開機可能需要比平常更多的時間。</span><span class="sxs-lookup"><span data-stu-id="166c9-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="166c9-199">重新開機之後，開啟 **Internet Explorer**。</span><span class="sxs-lookup"><span data-stu-id="166c9-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="166c9-200">在視窗的右上角按一下 [工具] 的齒輪圖示，然後選取 [管理附加元件]。</span><span class="sxs-lookup"><span data-stu-id="166c9-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![移至工具 > 管理附加元件](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="166c9-202">在 [管理附加元件] 視窗中，確認 [存取面板擴充功能] 已安裝且其 [狀態] 已設為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="166c9-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![確認存取面板延伸模組已安裝並啟用。](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="166c9-204">相關文章</span><span class="sxs-lookup"><span data-stu-id="166c9-204">Related Articles</span></span>
* [<span data-ttu-id="166c9-205">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="166c9-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="166c9-206">搭配 Azure Active Directory 的應用程式存取和單一登入</span><span class="sxs-lookup"><span data-stu-id="166c9-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="166c9-207">疑難排解 Internet explorer 的存取面板擴充功能</span><span class="sxs-lookup"><span data-stu-id="166c9-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

