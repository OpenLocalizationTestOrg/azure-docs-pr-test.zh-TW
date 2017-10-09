---
title: "aaaEnabling 在 Eclipse 的 Azure 部署的遠端存取權"
description: "了解 tooenable 遠端存取使用 hello Azure Toolkit for Eclipse 的 Azure 部署的方式。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="bf6a7-103">在 Eclipse 中啟用 Azure 部署的遠端存取</span><span class="sxs-lookup"><span data-stu-id="bf6a7-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="bf6a7-104">toohelp 疑難排解您的部署，您可能會啟用並使用裝載您部署遠端存取 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="bf6a7-105">hello 遠端存取 」 功能會依賴 hello 遠端桌面通訊協定 (RDP)。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="bf6a7-106">您已發行它 tooAzure，或如果您使用 Eclipse 與 Windows 作業系統，您就可以設定遠端存取，然後再發行 tooAzure 之後，您可以設定遠端存取您的部署。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="bf6a7-107">請注意，您將需要遠端桌面用戶端與您在 Azure 中的順序 tooconnect tooyour 部署的虛擬機器的作業系統相容。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="bf6a7-108">如何才能 tooenable 遠端存取部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bf6a7-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="bf6a7-109">tooenable 遠端存取部署應用程式 tooAzure 之前，您需要在 Windows 上執行 Eclipse toobe。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="bf6a7-110">hello 下列影像顯示 hello**遠端存取**使用 tooenable 遠端存取內容對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="bf6a7-111">有兩種方式 toodisplay hello**遠端存取**屬性 對話方塊：</span><span class="sxs-lookup"><span data-stu-id="bf6a7-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="bf6a7-112">按一下 hello**進階**hello 中的連結**遠端存取**區段 hello**發行 tooAzure**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="bf6a7-113">開啟 hello**屬性**的 Azure 專案 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="bf6a7-114">當您建立新的 Azure 部署專案時，hello 專案不會預設啟用遠端存取。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="bf6a7-115">不過，您可以輕鬆地啟用遠端存取指定 hello 使用者名稱和密碼在 hello**發行 tooAzure**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="bf6a7-116">使用 X.509 憑證加密 hello 遠端存取密碼。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="bf6a7-117">如果您未使用提供您自己的憑證，hello 加密依賴隨附 hello Azure Plugin for Eclipse 的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="bf6a7-118">此自我簽署的憑證是在 hello **cert**您的 Azure 專案的資料夾會儲存兩種形式的公開憑證檔案 (SampleRemoteAccessPublic.cer) 和做為個人資訊交換 (PFX) 憑證檔案 （SampleRemoteAccessPrivate.pfx)。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="bf6a7-119">hello 後者包含 hello hello 憑證私密金鑰，而且有預設密碼**Password1**。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="bf6a7-120">不過，由於此密碼是公用的知識，hello 預設憑證應只用於學習目的，不適用於生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="bf6a7-121">因此以外的學習的目的，當您想 tooenabled 遠端工作階段為您的部署，您應該按一下 hello**進階**hello 中的連結**發行 tooAzure**對話方塊 toospecify 自己憑證。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="bf6a7-122">請注意，您必須 tooupload hello PFX 版本 hello 憑證 tooyour 託管服務內 hello Azure 管理入口網站，讓 Azure 可以解密 hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="bf6a7-123">hello hello 教學課程的其餘部分會顯示 tooenable 遠端存取的 Azure 部署專案，開始建立停用遠端存取的方式。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="bf6a7-124">基於本教學課程的目的，我們將建立一個新的自我簽署憑證，而其 .pfx 檔案將包含您選擇的密碼。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="bf6a7-125">您也可以使用憑證授權單位所核發的憑證的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="bf6a7-126">如何 tooenable 遠端存取之後，您已部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bf6a7-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="bf6a7-127">tooenable 遠端存取部署 tooAzure，下列步驟使用 hello 之後：</span><span class="sxs-lookup"><span data-stu-id="bf6a7-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="bf6a7-128">登入使用您的 Azure 帳戶的 hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="bf6a7-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="bf6a7-129">在 [雲端服務] 清單中，選取您部署的雲端服務</span><span class="sxs-lookup"><span data-stu-id="bf6a7-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="bf6a7-130">在 hello 雲端服務網頁上，按一下 hello**設定**連結</span><span class="sxs-lookup"><span data-stu-id="bf6a7-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="bf6a7-131">在 hello hello 組態 頁面底部，按一下 hello**遠端**連結</span><span class="sxs-lookup"><span data-stu-id="bf6a7-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="bf6a7-132">Hello 快顯對話方塊出現時：</span><span class="sxs-lookup"><span data-stu-id="bf6a7-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="bf6a7-133">指定角色 hello 您想 tooenable 遠端存取</span><span class="sxs-lookup"><span data-stu-id="bf6a7-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="bf6a7-134">按一下 tooselect hello**啟用遠端桌面**核取方塊</span><span class="sxs-lookup"><span data-stu-id="bf6a7-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="bf6a7-135">指定使用者名稱和密碼，您想要遠端存取 toouse</span><span class="sxs-lookup"><span data-stu-id="bf6a7-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="bf6a7-136">選取 hello 憑證 toouse</span><span class="sxs-lookup"><span data-stu-id="bf6a7-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="bf6a7-137">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="bf6a7-137">Click **OK**</span></span> 

<span data-ttu-id="bf6a7-138">您會看到一個訊息，指出您的組態變更正在進行，這可能需要幾分鐘的時間 toocomplete 中。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="bf6a7-139">Hello 組態變更完成之後，請依照 hello 中的 hello 步驟**toolog 中的從遠端**本文中稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="bf6a7-140">如何在封裝中的 tooenable 遠端存取</span><span class="sxs-lookup"><span data-stu-id="bf6a7-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="bf6a7-141">在 Eclipse 的專案總管窗格中，於您的 Azure 專案上按一下滑鼠右鍵，並按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="bf6a7-142">在 hello**屬性** 對話方塊中，展開  **Azure**在 hello 左側窗格中按一下**遠端存取**。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="bf6a7-143">在 [hello**遠端存取**] 對話方塊中，確定**啟用所有角色 tooaccept 遠端桌面連線使用這些登入認證**已核取。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="bf6a7-144">指定 hello 遠端桌面連線的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="bf6a7-145">指定並確認 hello hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="bf6a7-146">當您進行 「 遠端桌面 」 連線時，將使用 hello 的使用者名稱和密碼值在此對話方塊中設定。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="bf6a7-147">(請注意，這個密碼不同於您的 PFX 密碼)。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="bf6a7-148">指定 hello hello 使用者帳戶到期日。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="bf6a7-149">按一下**新增**toocreate 新的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="bf6a7-150">(或者，您可以選取憑證，從您的工作區或檔案系統，透過 hello**工作區**或**FileSystem**分別，但基於本教學課程中我們將建立新的按鈕憑證。）</span><span class="sxs-lookup"><span data-stu-id="bf6a7-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="bf6a7-151">在 [hello**新憑證**] 對話方塊中，指定並確認您會使用 PFX 檔案的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="bf6a7-152">接受提供的 hello 值**名稱 (CN)**，或使用自訂名稱。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="bf6a7-153">指定要在其中儲存 hello 新的憑證，.cer 格式的 hello 路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="bf6a7-154">此步驟和 hello 下一個步驟中，您可以使用 hello **cert**的 Azure 專案，但您的資料夾是免費 toochoose 另一個位置。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="bf6a7-155">基於本教學課程的目的，我們將使用 **c:\mycert\mycert.cer**。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="bf6a7-156">(建立 hello **c:\mycert**先前 tooproceeding 資料夾或使用現有的資料夾，視。)</span><span class="sxs-lookup"><span data-stu-id="bf6a7-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="bf6a7-157">指定要儲存 hello 新憑證和私密金鑰，.pfx 格式的 hello 路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="bf6a7-158">基於本教學課程的目的，我們將使用 **c:\mycert\mycert.pfx**。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="bf6a7-159">您**新憑證**對話方塊看起來類似 toohello 下列 (更新 hello 資料夾路徑，如果您未使用**c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="bf6a7-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="bf6a7-160">按一下**確定**tooclose hello**新憑證**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="bf6a7-161">您**遠端存取**對話方塊看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="bf6a7-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="bf6a7-162">按一下**確定**tooclose hello**遠端存取**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="bf6a7-163">重建您的應用程式，以 hello 建置部署 toocloud 的集合。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="bf6a7-164">在 toolog 遠端</span><span class="sxs-lookup"><span data-stu-id="bf6a7-164">toolog in remotely</span></span>
<span data-ttu-id="bf6a7-165">角色執行個體準備就緒之後，您可以從遠端登入 toohello 則裝載應用程式的虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="bf6a7-166">如果在 Windows 和您選取的 hello 上使用 Eclipse**上的啟動遠端桌面部署**選項在您部署 tooAzure，您會看到的遠端桌面連線登入畫面啟動您的部署時。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="bf6a7-167">當系統提示您輸入 hello 使用者名稱和密碼時，輸入您為 hello 遠端使用者指定的 hello 值，且將無法 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="bf6a7-168">中的另一個方式 toolog 遠端是透過 hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure 管理入口網站</a>:</span><span class="sxs-lookup"><span data-stu-id="bf6a7-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="bf6a7-169">Hello 內**雲端服務**檢視 hello Azure 管理入口網站中，按一下您的雲端服務中，按一下**執行個體**，按一下 [特定的執行個體，然後按一下hello**連接**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="bf6a7-170">hello**連接**按鈕會顯示為 hello 命令列中的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="bf6a7-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="bf6a7-171">按一下 hello 之後**連接** 按鈕，您將會提示的 tooopen RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="bf6a7-172">開啟 hello 檔案，並依照 hello 提示。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="bf6a7-173">(您可能也儲存此檔案 tooyour 本機電腦，然後執行 hello 檔案按兩下 tooremote 記錄 tooyour 中虛擬機器，而不需要 toofirst 移 hello 管理入口網站。)</span><span class="sxs-lookup"><span data-stu-id="bf6a7-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="bf6a7-174">當系統提示您輸入 hello 使用者名稱和密碼時，輸入您為 hello 遠端使用者指定的 hello 值，且將無法 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="bf6a7-175">如果您是在非 Windows 作業系統上，您需要 toouse 遠端桌面用戶端與作業系統相容，並遵循 hello 步驟 tooconfigure 與 hello 您下載的 RDP 檔案中的 hello 設定該用戶端。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="bf6a7-176">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bf6a7-176">See Also</span></span>
<span data-ttu-id="bf6a7-177">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bf6a7-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="bf6a7-178">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bf6a7-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="bf6a7-179">[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bf6a7-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="bf6a7-180">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="bf6a7-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
