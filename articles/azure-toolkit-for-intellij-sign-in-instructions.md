---
title: "aaaSign 中的指示 hello Azure Toolkit for IntelliJ |Microsoft 文件"
description: "了解如何 toosign 中使用 tooMicrosoft Azure hello Azure Toolkit IntelliJ。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="a8c11-103">登入的指示 hello Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a8c11-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="a8c11-104">hello Azure Toolkit for IntelliJ 提供兩種方法在 tooyour Azure 帳戶登入：</span><span class="sxs-lookup"><span data-stu-id="a8c11-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="a8c11-105">**互動式**： 您在 tooyour Azure 帳戶中輸入您的 Azure 認證每次您登入。</span><span class="sxs-lookup"><span data-stu-id="a8c11-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="a8c11-106">**自動化**： 您建立的認證檔案，您可以使用 tooautomatically 登 tooyour Azure 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a8c11-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="a8c11-107">hello 下列各節說明如何 toouse 每一種方法。</span><span class="sxs-lookup"><span data-stu-id="a8c11-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="a8c11-108">以互動方式登入 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="a8c11-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="a8c11-109">在手動輸入您的 Azure 認證 tooAzure toosign hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="a8c11-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="a8c11-110">使用 IntelliJ IDEA 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="a8c11-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="a8c11-111">按一下**工具**，點太**Azure**，然後按一下 **Azure 登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![hello IntelliJ Azure 登入 命令][I01]

3. <span data-ttu-id="a8c11-113">在 hello **Azure 登入**視窗中，選取**互動式**，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![hello Azure 登入與選取的 Interactive 視窗][I02]

4. <span data-ttu-id="a8c11-115">在 hello **Azure 登入**出現對話方塊，請輸入您的 Azure 認證，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![hello Azure 登入 對話方塊視窗][I03]

5. <span data-ttu-id="a8c11-117">在 hello**選取的訂用帳戶**對話方塊中，選取 hello 訂閱您想 toouse，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![hello 選取多個訂閱對話方塊][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="a8c11-119">在以互動方式登入後，登出您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="a8c11-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="a8c11-120">您已使用 hello 先前步驟來設定您的帳戶之後，您將會自動登出您的 Azure 帳戶，每次您重新啟動 IntelliJ 概念。</span><span class="sxs-lookup"><span data-stu-id="a8c11-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="a8c11-121">不過，如果想要從您的 Azure 帳戶的 toosign*沒有*IntelliJ 概念，重新啟動之後執行 hello。</span><span class="sxs-lookup"><span data-stu-id="a8c11-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="a8c11-122">在 IntelliJ 概念，在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登出**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![hello IntelliJ Azure 登出命令][L01]

2. <span data-ttu-id="a8c11-124">在 hello **Azure 登出**確認視窗中，按一下 **是**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![hello Azure 登出確認視窗][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="a8c11-126">自動登入 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="a8c11-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="a8c11-127">本節會逐步引導您建立認證檔案，並在檔案中包含您的服務主體資料。</span><span class="sxs-lookup"><span data-stu-id="a8c11-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="a8c11-128">您已完成此程序之後，Eclipse 使用 hello 認證檔案 tooautomatically 登中 tooAzure 每次開啟專案。</span><span class="sxs-lookup"><span data-stu-id="a8c11-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="a8c11-129">使用 IntelliJ IDEA 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="a8c11-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="a8c11-130">在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![hello IntelliJ Azure 登入 命令][A01]

3. <span data-ttu-id="a8c11-132">在 hello **Azure 登入**視窗中，選取**自動化**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![hello Azure 登入與自動選取視窗][A02]

4. <span data-ttu-id="a8c11-134">在 hello **Azure 登入對話方塊**視窗中，輸入您的 Azure 認證，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![hello Azure 登入 對話方塊視窗][A03]

5. <span data-ttu-id="a8c11-136">在 hello**建立驗證檔案**視窗中，選取 hello 訂閱您想 toouse，選擇您的目的地目錄，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![hello 驗證檔建立視窗][A04]

6. <span data-ttu-id="a8c11-138">在 hello**服務主體建立狀態**對話方塊中，已成功建立您的檔案之後，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![hello 服務主體建立狀態 對話方塊][A05]

7. <span data-ttu-id="a8c11-140">在 hello **Azure 登入**視窗中，按一下 **登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![[Azure 登入] 對話方塊][A06]

8. <span data-ttu-id="a8c11-142">在 hello**選取的訂用帳戶**對話方塊中，選取 hello 訂閱您想 toouse，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![hello 選取多個訂閱對話方塊][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="a8c11-144">在自動登入後登出您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="a8c11-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="a8c11-145">您已使用 hello 先前步驟來設定您的帳戶之後，hello Azure Toolkit 會自動將您登入 tooyour 每次您重新啟動 IntelliJ 概念的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a8c11-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="a8c11-146">不過，toosign 您的 Azure 帳戶的資料，並防止 hello Azure Toolkit 從您自動登入，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="a8c11-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="a8c11-147">在 IntelliJ 概念，在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登出**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![hello IntelliJ Azure 登出命令][L01]

2. <span data-ttu-id="a8c11-149">在 hello **Azure 登出**確認視窗中，按一下 **是**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![hello Azure 登出確認視窗][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="a8c11-151">自動登入 tooyour Azure 帳戶使用現有的認證檔案</span><span class="sxs-lookup"><span data-stu-id="a8c11-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="a8c11-152">如果您會登出您的 Azure 帳戶，當您使用 IntelliJ 概念時，您必須使用現有的認證檔案 tooautomatically 登入 toohello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a8c11-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="a8c11-153">tooconfigure hello Azure Toolkit for Eclipse toouse 現有的認證檔案，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="a8c11-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="a8c11-154">使用 IntelliJ IDEA 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="a8c11-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="a8c11-155">在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![hello IntelliJ Azure 登入 命令][A01]

3. <span data-ttu-id="a8c11-157">在 hello **Azure 登入**視窗中，選取**自動化**，然後按一下**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![hello Azure 登入與自動選取視窗][A02]

4. <span data-ttu-id="a8c11-159">在 hello**選取驗證檔案**對話方塊中，選取先前建立的認證檔案，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![hello 選取驗證檔案對話方塊][A08]

5. <span data-ttu-id="a8c11-161">在 hello **Azure 登入**視窗中，按一下 **登入**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![hello Azure 登入與自動選取視窗][A06]

6. <span data-ttu-id="a8c11-163">在 hello**選取的訂用帳戶**對話方塊中，選取 hello 訂閱您想 toouse，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a8c11-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![hello 選取多個訂閱對話方塊][A07]

## <a name="next-steps"></a><span data-ttu-id="a8c11-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8c11-165">Next steps</span></span>
<span data-ttu-id="a8c11-166">針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="a8c11-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="a8c11-167">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="a8c11-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8c11-168">[在 hello Azure Toolkit for Eclipse 中最新消息]</span><span class="sxs-lookup"><span data-stu-id="a8c11-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8c11-169">[安裝 Azure Toolkit for Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="a8c11-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8c11-170">[登入指示 hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8c11-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8c11-171">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="a8c11-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="a8c11-172">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a8c11-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a8c11-173">[在 hello Azure Toolkit for IntelliJ 最新消息]</span><span class="sxs-lookup"><span data-stu-id="a8c11-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a8c11-174">[安裝 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a8c11-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a8c11-175">*登入的指示 hello Azure Toolkit for IntelliJ* （即本文）</span><span class="sxs-lookup"><span data-stu-id="a8c11-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="a8c11-176">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="a8c11-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="a8c11-177">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。</span><span class="sxs-lookup"><span data-stu-id="a8c11-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[登入指示 hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[在 hello Azure Toolkit for Eclipse 中最新消息]: ./azure-toolkit-for-eclipse-whats-new.md
[在 hello Azure Toolkit for IntelliJ 最新消息]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
