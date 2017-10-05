---
title: "在 Eclipse 中啟用 Azure 部署的遠端存取"
description: "了解如何使用適用於 Eclipse 的 Azure 工具組來啟用 Azure 部署的遠端存取。"
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="80d7b-103">在 Eclipse 中啟用 Azure 部署的遠端存取</span><span class="sxs-lookup"><span data-stu-id="80d7b-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="80d7b-104">為協助疑難排解您的部署，您可以啟用並使用「遠端存取」以連線到裝載您的部署的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="80d7b-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="80d7b-105">遠端存取功能需要遠端桌面通訊協定 (RDP)。</span><span class="sxs-lookup"><span data-stu-id="80d7b-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="80d7b-106">您可以先將您的部署發行到 Azure 之後再設定遠端存取，或如果您使用 Eclipse 與 Windows 作業系統，則可先設定遠端存取，再將它發行到 Azure。</span><span class="sxs-lookup"><span data-stu-id="80d7b-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="80d7b-107">請注意，要連線到您在 Azure 的部署的虛擬機器，您需要相容於您的作業系統的遠端桌面用戶端。</span><span class="sxs-lookup"><span data-stu-id="80d7b-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="80d7b-108">如何在部署到 Azure 之前先啟用遠端存取</span><span class="sxs-lookup"><span data-stu-id="80d7b-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="80d7b-109">若要在將您的應用程式部署到 Azure 之前先啟用遠端存取，您需要在 Windows 上執行 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="80d7b-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="80d7b-110">下列影像顯示用來啟用遠端存取的 [遠端存取]  內容對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80d7b-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="80d7b-111">有兩種方式來顯示 [遠端存取]  內容對話方塊：</span><span class="sxs-lookup"><span data-stu-id="80d7b-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="80d7b-112">按一下 [發佈到 Azure] 對話方塊的 [遠端存取] 區段中的 [進階] 連結。</span><span class="sxs-lookup"><span data-stu-id="80d7b-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="80d7b-113">開啟您的 Azure 專案的 [內容]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80d7b-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="80d7b-114">當您建立新的 Azure 部署專案時，專案預設不會啟用遠端存取。</span><span class="sxs-lookup"><span data-stu-id="80d7b-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="80d7b-115">不過，您可以在 [發佈到 Azure] 對話方塊指定使用者名稱和密碼，就能輕鬆地啟用遠端存取。</span><span class="sxs-lookup"><span data-stu-id="80d7b-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="80d7b-116">遠端存取密碼使用 X.509 憑證加密。</span><span class="sxs-lookup"><span data-stu-id="80d7b-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="80d7b-117">如果您未使用它來提供您自己的憑證，加密是依賴隨附於 Azure Plugin for Eclipse 的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="80d7b-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="80d7b-118">這個自我簽署的憑證在您的 Azure 專案的 **cert** 資料夾中，而且儲存為公開憑證檔案 (SampleRemoteAccessPublic.cer) 和個人資訊交換 (PFX) 憑證檔案 (SampleRemoteAccessPrivate.pfx)。</span><span class="sxs-lookup"><span data-stu-id="80d7b-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="80d7b-119">後者包含憑證的私密金鑰，而且具有預設密碼 **Password1**。</span><span class="sxs-lookup"><span data-stu-id="80d7b-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="80d7b-120">不過，由於此密碼是公開資訊，預設的憑證應僅供教學使用，不適用於實際執行部署。</span><span class="sxs-lookup"><span data-stu-id="80d7b-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="80d7b-121">因此，除教學的用途外，當您想為您的部署啟用遠端工作階段時，您應該按一下 [發佈到 Azure] 對話方塊中的 [進階] 連結來指定您自己的憑證。</span><span class="sxs-lookup"><span data-stu-id="80d7b-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="80d7b-122">請注意，您必須將憑證的 PFX 版本上傳至 Azure 管理入口網站中您裝載的服務，這樣 Azure 才可以解密使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="80d7b-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="80d7b-123">其餘的教學課程示範如何為一開始建立時停用遠端存取的 Azure 部署專案啟用遠端存取。</span><span class="sxs-lookup"><span data-stu-id="80d7b-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="80d7b-124">基於本教學課程的目的，我們將建立一個新的自我簽署憑證，而其 .pfx 檔案將包含您選擇的密碼。</span><span class="sxs-lookup"><span data-stu-id="80d7b-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="80d7b-125">您也可以選擇使用憑證授權單位所核發的憑證。</span><span class="sxs-lookup"><span data-stu-id="80d7b-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="80d7b-126">如何在部署到 Azure 之後啟用遠端存取</span><span class="sxs-lookup"><span data-stu-id="80d7b-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="80d7b-127">若要在部署到 Azure 之後啟用遠端存取，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="80d7b-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="80d7b-128">使用您的 Azure 帳戶登入 Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="80d7b-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="80d7b-129">在 [雲端服務] 清單中，選取您部署的雲端服務</span><span class="sxs-lookup"><span data-stu-id="80d7b-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="80d7b-130">在雲端服務 Web 頁面上，按一下 [設定]  連結</span><span class="sxs-lookup"><span data-stu-id="80d7b-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="80d7b-131">在 [組態] 頁面底部，按一下 [遠端]  連結</span><span class="sxs-lookup"><span data-stu-id="80d7b-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="80d7b-132">當快顯對話方塊出現時：</span><span class="sxs-lookup"><span data-stu-id="80d7b-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="80d7b-133">指定您想要為其啟用遠端存取的角色</span><span class="sxs-lookup"><span data-stu-id="80d7b-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="80d7b-134">按一下以選取 [啟用遠端桌面]  核取方塊</span><span class="sxs-lookup"><span data-stu-id="80d7b-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="80d7b-135">指定您想要用於遠端存取的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="80d7b-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="80d7b-136">選取要使用的憑證</span><span class="sxs-lookup"><span data-stu-id="80d7b-136">Select the certificate to use</span></span>

6. <span data-ttu-id="80d7b-137">按一下 [確定] </span><span class="sxs-lookup"><span data-stu-id="80d7b-137">Click **OK**</span></span> 

<span data-ttu-id="80d7b-138">您會看到訊息指出您的組態變更正在進行，可能需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="80d7b-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="80d7b-139">完成組態變更之後，請依照本文稍後的＜從遠端登入＞  一節中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="80d7b-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="80d7b-140">如何在您的封裝中啟用遠端存取</span><span class="sxs-lookup"><span data-stu-id="80d7b-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="80d7b-141">在 Eclipse 的專案總管窗格中，於您的 Azure 專案上按一下滑鼠右鍵，並按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="80d7b-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="80d7b-142">在 [內容] 對話方塊中，展開左窗格中的 [Azure]，按一下 [遠端存取]。</span><span class="sxs-lookup"><span data-stu-id="80d7b-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="80d7b-143">在 [遠端存取] 對話方塊中，確定已勾選 [讓所有角色接受使用這些登入認證的遠端桌面連線]。</span><span class="sxs-lookup"><span data-stu-id="80d7b-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="80d7b-144">指定遠端桌面連線的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="80d7b-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="80d7b-145">指定並確認使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="80d7b-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="80d7b-146">當您建立遠端桌面連線時，將使用在此對話方塊中設定的使用者名稱和密碼值。</span><span class="sxs-lookup"><span data-stu-id="80d7b-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="80d7b-147">(請注意，這個密碼不同於您的 PFX 密碼)。</span><span class="sxs-lookup"><span data-stu-id="80d7b-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="80d7b-148">指定使用者帳戶的到期日。</span><span class="sxs-lookup"><span data-stu-id="80d7b-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="80d7b-149">按一下 [新增] 來建立新的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="80d7b-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="80d7b-150">(或者，您可以透過 [工作區] 或 [檔案系統] 按鈕，分別從您的工作區或檔案系統選取憑證，但基於本教學課程目的，我們將建立新的憑證。)</span><span class="sxs-lookup"><span data-stu-id="80d7b-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="80d7b-151">在 [新憑證]  對話方塊中，指定並確認將使用於 PFX 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="80d7b-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="80d7b-152">接受為 [名稱 (CN)] 提供的值，或使用自訂的名稱。</span><span class="sxs-lookup"><span data-stu-id="80d7b-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="80d7b-153">指定儲存新憑證的路徑和檔案名稱 (.cer 格式)。</span><span class="sxs-lookup"><span data-stu-id="80d7b-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="80d7b-154">針對這一步和下一步，您可以使用您的 Azure 專案的 **cert** 資料夾，但您也可以選擇其他位置。</span><span class="sxs-lookup"><span data-stu-id="80d7b-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="80d7b-155">基於本教學課程的目的，我們將使用 **c:\mycert\mycert.cer**。</span><span class="sxs-lookup"><span data-stu-id="80d7b-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="80d7b-156">(請先建立 **c:\mycert** 資料夾後再繼續，或視需要使用現有的資料夾。)</span><span class="sxs-lookup"><span data-stu-id="80d7b-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="80d7b-157">指定儲存新憑證和其私密金鑰的路徑和檔案名稱 (私密金鑰為 .pfx 格式)。</span><span class="sxs-lookup"><span data-stu-id="80d7b-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="80d7b-158">基於本教學課程的目的，我們將使用 **c:\mycert\mycert.pfx**。</span><span class="sxs-lookup"><span data-stu-id="80d7b-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="80d7b-159">您的 [新憑證] 對話方塊看起來應該和下面類似 (如果您不是使用 **c:\mycert**，請更新資料夾路徑)：</span><span class="sxs-lookup"><span data-stu-id="80d7b-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="80d7b-160">按一下 [確定] 關閉 [新憑證] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80d7b-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="80d7b-161">您的 [遠端存取] 對話方塊看起來應該和下面類似：</span><span class="sxs-lookup"><span data-stu-id="80d7b-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="80d7b-162">按一下 [確定] 關閉 [遠端存取] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80d7b-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="80d7b-163">使用為部署到雲端所設定的組建，重新建立您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="80d7b-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="80d7b-164">從遠端登入</span><span class="sxs-lookup"><span data-stu-id="80d7b-164">To log in remotely</span></span>
<span data-ttu-id="80d7b-165">您的角色執行個體準備就緒後，您可以從遠端登入裝載您的應用程式的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="80d7b-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="80d7b-166">如果使用 Eclipse 和 Windows，而且您在部署到 Azure 的期間選取 [部署時啟動遠端桌面]  選項，當您的部署開始時會提供一個 [遠端桌面連線] 登入畫面。</span><span class="sxs-lookup"><span data-stu-id="80d7b-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="80d7b-167">當系統提示您輸入使用者名稱和密碼時，輸入您為遠端使用者指定的值就能登入。</span><span class="sxs-lookup"><span data-stu-id="80d7b-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="80d7b-168">從遠端登入的另一種方式是透過 <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure 管理入口網站</a>：</span><span class="sxs-lookup"><span data-stu-id="80d7b-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="80d7b-169">在 Azure 管理入口網站的 [雲端服務] 檢視中，按一下 [執行個體]，按一下特定的執行個體，再按一下 [連接] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="80d7b-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="80d7b-170">命令列中會顯示如下的 [連線]  按鈕：</span><span class="sxs-lookup"><span data-stu-id="80d7b-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="80d7b-171">按一下 [連接] 按鈕後，將會提示您開啟 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="80d7b-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="80d7b-172">開啟檔案，並依照提示執行。</span><span class="sxs-lookup"><span data-stu-id="80d7b-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="80d7b-173">(您可以也將此檔案儲存到您的本機電腦，然後按兩下執行該檔案以遠端登入您的虛擬機器，而不需要先前往管理入口網站。)</span><span class="sxs-lookup"><span data-stu-id="80d7b-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="80d7b-174">當系統提示您輸入使用者名稱和密碼時，輸入您為遠端使用者指定的值就能登入。</span><span class="sxs-lookup"><span data-stu-id="80d7b-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="80d7b-175">如果您是在非 Windows 作業系統上，則必須使用與作業系統相容的遠端桌面用戶端，並使用您下載的 RDP 檔案中的設定，依照步驟來設定該用戶端。</span><span class="sxs-lookup"><span data-stu-id="80d7b-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="80d7b-176">另請參閱</span><span class="sxs-lookup"><span data-stu-id="80d7b-176">See Also</span></span>
<span data-ttu-id="80d7b-177">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="80d7b-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="80d7b-178">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="80d7b-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="80d7b-179">[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="80d7b-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="80d7b-180">如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="80d7b-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
