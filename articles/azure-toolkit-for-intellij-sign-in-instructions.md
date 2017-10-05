---
title: "適用於 IntelliJ 的 Azure 工具組登入指示 | Microsoft Docs"
description: "了解如何使用適用於 IntelliJ 的 Azure 工具組登入 Microsoft Azure。"
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
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="4cb15-103">Azure Toolkit for IntelliJ 的登入指示</span><span class="sxs-lookup"><span data-stu-id="4cb15-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="4cb15-104">適用於 IntelliJ 的 Azure 工具組提供兩種登入您 Azure 帳戶的方法︰</span><span class="sxs-lookup"><span data-stu-id="4cb15-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="4cb15-105">**互動式**︰在每次登入 Azure 帳戶時要輸入 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="4cb15-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="4cb15-106">**自動化**︰建立認證檔案，用以自動登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4cb15-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="4cb15-107">下列各節會說明如何使用每個方法。</span><span class="sxs-lookup"><span data-stu-id="4cb15-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="4cb15-108">以互動方式登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="4cb15-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="4cb15-109">若要以手動方式輸入您的 Azure 認證來登入 Azure，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="4cb15-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="4cb15-110">使用 IntelliJ IDEA 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="4cb15-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="4cb15-111">按一下 [工具]，指向 [Azure]，然後按一下 [Azure 登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ 的 [Azure 登入] 命令][I01]

3. <span data-ttu-id="4cb15-113">在 [Azure 登入] 視窗中，選取 [互動式]，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![選取了 [互動式] 的 [Azure 登入] 視窗][I02]

4. <span data-ttu-id="4cb15-115">在 [Azure 登入] 對話方塊出現時，輸入您的 Azure 認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![[Azure 登入] 對話方塊視窗][I03]

5. <span data-ttu-id="4cb15-117">在 [選取訂用帳戶] 對話方塊中，選取您要使用的訂用帳戶，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![[選取訂用帳戶] 對話方塊][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="4cb15-119">在以互動方式登入後，登出您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="4cb15-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="4cb15-120">在使用前面的步驟設定好帳戶後，每次您重新啟動 IntelliJ IDEA 時，系統都會自動將您登出 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4cb15-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="4cb15-121">不過，如果您想要登出 Azure 帳戶而不重新啟動 IntelliJ IDEA，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4cb15-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="4cb15-122">在 IntelliJ IDEA 的 [工具] 功能表上，指向 [Azure]，然後按一下 [Azure 登出]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![IntelliJ 的 [Azure 登出] 命令][L01]

2. <span data-ttu-id="4cb15-124">在 [Azure 登出] 確認視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![[Azure 登出] 確認視窗][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="4cb15-126">自動登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="4cb15-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="4cb15-127">本節會逐步引導您建立認證檔案，並在檔案中包含您的服務主體資料。</span><span class="sxs-lookup"><span data-stu-id="4cb15-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="4cb15-128">在完成此程序後，Eclipse 會使用認證檔案，讓您在每次開啟專案時自動登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="4cb15-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="4cb15-129">使用 IntelliJ IDEA 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="4cb15-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="4cb15-130">在 [工具] 功能表上，指向 [Azure]，然後按一下 [Azure 登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ 的 [Azure 登入] 命令][A01]

3. <span data-ttu-id="4cb15-132">在 [Azure 登入] 視窗中選取 [自動化]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![選取了 [自動化] 的 [Azure 登入] 視窗][A02]

4. <span data-ttu-id="4cb15-134">在 [Azure 登入對話方塊] 視窗中，輸入您的 Azure 認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![[Azure 登入] 對話方塊視窗][A03]

5. <span data-ttu-id="4cb15-136">在 [建立驗證檔案] 視窗中，選取您想要使用的訂用帳戶，選擇您的目的地目錄，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![[建立驗證檔案] 視窗][A04]

6. <span data-ttu-id="4cb15-138">在 [服務主體建立狀態] 對話方塊中，於系統成功建立檔案之後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![[服務主體建立狀態] 對話方塊][A05]

7. <span data-ttu-id="4cb15-140">在 [Azure 登入] 視窗中，按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![[Azure 登入] 對話方塊][A06]

8. <span data-ttu-id="4cb15-142">在 [選取訂用帳戶] 對話方塊中，選取您要使用的訂用帳戶，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![[選取訂用帳戶] 對話方塊][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="4cb15-144">在自動登入後登出您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="4cb15-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="4cb15-145">在使用前面的步驟設定好帳戶後，每次您重新啟動 IntelliJ IDEA 時，Azure 工具組都會將您自動登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4cb15-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="4cb15-146">不過，若要登出您的 Azure 帳戶，並防止 Azure 工具組自動將您登入，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="4cb15-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="4cb15-147">在 IntelliJ IDEA 的 [工具] 功能表上，指向 [Azure]，然後按一下 [Azure 登出]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![IntelliJ 的 [Azure 登出] 命令][L01]

2. <span data-ttu-id="4cb15-149">在 [Azure 登出] 確認視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![[Azure 登出] 確認視窗][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="4cb15-151">使用現有的認證檔案自動登入 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="4cb15-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="4cb15-152">如果您在使用 IntelliJ IDEA 時登出了 Azure 帳戶，您必須使用現有的認證檔案來自動重新登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="4cb15-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="4cb15-153">若要將適用於 Eclipse 的 Azure 工具組設定為使用現有認證檔案，請執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="4cb15-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="4cb15-154">使用 IntelliJ IDEA 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="4cb15-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="4cb15-155">在 [工具] 功能表上，指向 [Azure]，然後按一下 [Azure 登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ 的 [Azure 登入] 命令][A01]

3. <span data-ttu-id="4cb15-157">在 [Azure 登入] 視窗中選取 [自動化]，然後按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![選取了 [自動化] 的 [Azure 登入] 視窗][A02]

4. <span data-ttu-id="4cb15-159">在 [選取驗證檔案] 對話方塊中，選取先前建立的認證檔案，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![[選取驗證檔案] 對話方塊][A08]

5. <span data-ttu-id="4cb15-161">在 [Azure 登入] 視窗中，按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![選取了 [自動化] 的 [Azure 登入] 視窗][A06]

6. <span data-ttu-id="4cb15-163">在 [選取訂用帳戶] 對話方塊中，選取您要使用的訂用帳戶，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![[選取訂用帳戶] 對話方塊][A07]

## <a name="next-steps"></a><span data-ttu-id="4cb15-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4cb15-165">Next steps</span></span>
<span data-ttu-id="4cb15-166">如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="4cb15-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="4cb15-167">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="4cb15-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb15-168">[Azure Toolkit for Eclipse 的新功能]</span><span class="sxs-lookup"><span data-stu-id="4cb15-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb15-169">[安裝 Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4cb15-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb15-170">[Azure Toolkit for Eclipse 的登入指示]</span><span class="sxs-lookup"><span data-stu-id="4cb15-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb15-171">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="4cb15-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="4cb15-172">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4cb15-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4cb15-173">[適用於 IntelliJ 的 Azure 工具組新增功能]</span><span class="sxs-lookup"><span data-stu-id="4cb15-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4cb15-174">[安裝 Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4cb15-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4cb15-175">*適用於 IntelliJ 的 Azure 工具組登入指示* (本文)</span><span class="sxs-lookup"><span data-stu-id="4cb15-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="4cb15-176">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="4cb15-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="4cb15-177">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="4cb15-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="4cb15-178">[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="4cb15-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="4cb15-180">[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="4cb15-181">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="4cb15-182">[安裝 Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="4cb15-183">[安裝 Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="4cb15-184">[Azure Toolkit for Eclipse 的登入指示]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="4cb15-185">[Azure Toolkit for Eclipse 的新功能]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="4cb15-186">[適用於 IntelliJ 的 Azure 工具組新增功能]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="4cb15-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="4cb15-187">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="4cb15-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="4cb15-188">[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="4cb15-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

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
