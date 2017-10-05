---
title: "適用於 Eclipse 的 Azure 工具組登入指示 | Microsoft Docs"
description: "了解如何使用適用於 Eclipse 的 Azure 工具組登入 Microsoft Azure。"
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
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="e1d22-103">適用於 Eclipse 的 Azure 工具組的 Azure 登入指示</span><span class="sxs-lookup"><span data-stu-id="e1d22-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="e1d22-104">適用於 Eclipse 的 Azure 工具組提供兩種登入您 Azure 帳戶的方法︰</span><span class="sxs-lookup"><span data-stu-id="e1d22-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="e1d22-105">**互動式** - 當您使用這個方法時，每次登入 Azure 帳戶都要輸入 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="e1d22-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="e1d22-106">**自動化** - 當您使用這個方法時，您所建立的認證檔案會包含您的服務主體資料，此後您可以使用認證檔案自動登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1d22-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="e1d22-107">下列各節中的步驟將說明如何使用每個方法。</span><span class="sxs-lookup"><span data-stu-id="e1d22-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="e1d22-108">以互動方式登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e1d22-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="e1d22-109">下列步驟將說明如何以手動方式輸入您的 Azure 認證來登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="e1d22-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="e1d22-110">使用 Eclipse 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="e1d22-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="e1d22-111">依序按一下 [工具]、[Azure] 以及 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 登入的 Eclipse 功能表][I01]

1. <span data-ttu-id="e1d22-113">當 [Azure 登入] 對話方塊出現時，請選取 [互動式]，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![[登入] 對話方塊][I02]

1. <span data-ttu-id="e1d22-115">當 [Azure 登入] 對話方塊出現時，請輸入您的 Azure 認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![[Azure 登入] 對話方塊][I03]

1. <span data-ttu-id="e1d22-117">當 [選取訂用帳戶]對話方塊出現時，請選取您要使用的訂用帳戶，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![[選取訂用帳戶] 對話方塊][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="e1d22-119">當您以互動方式登入時，登出您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e1d22-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="e1d22-120">在上一節中設定步驟之後，每次您重新啟動 Eclipse 時，都會自動將您登出 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1d22-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="e1d22-121">不過，如果您想要登出您的 Azure 帳戶而不重新啟動 Eclipse，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e1d22-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="e1d22-122">在 Eclipse 中，依序按一下 [工具]、[Azure] 以及 [登出]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 登出的 Eclipse 功能表][L01]

1. <span data-ttu-id="e1d22-124">當 [Azure 登出] 對話方塊出現時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![[登出] 對話方塊][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="e1d22-126">自動登入 Azure 帳戶，並建立要在未來使用的認證檔案</span><span class="sxs-lookup"><span data-stu-id="e1d22-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="e1d22-127">下列步驟將逐步引導您建立的認證檔案會包含您的服務主體資料。</span><span class="sxs-lookup"><span data-stu-id="e1d22-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="e1d22-128">一旦完成這些步驟後，Eclipse 會自動使用認證檔案，讓您每次開啟專案時都會自動登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="e1d22-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="e1d22-129">使用 Eclipse 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="e1d22-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="e1d22-130">依序按一下 [工具]、[Azure] 以及 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 登入的 Eclipse 功能表][A01]

1. <span data-ttu-id="e1d22-132">當 [Azure 登入] 對話方塊出現時，請選取 [自動化]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![[登入] 對話方塊][A02]

1. <span data-ttu-id="e1d22-134">當 [Azure 登入] 對話方塊出現時，請輸入您的 Azure 認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![[Azure 登入] 對話方塊][A03]

1. <span data-ttu-id="e1d22-136">當 [建立驗證檔案] 對話方塊出現時，請選取您想要使用的訂用帳戶，選擇您的目的地目錄，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![[Azure 登入] 對話方塊][A04]

1. <span data-ttu-id="e1d22-138">[服務主體建立狀態]對話方塊隨即顯示，並在您的檔案成功建立之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![[服務主體建立狀態] 對話方塊][A05]

1. <span data-ttu-id="e1d22-140">當 [Azure 登入]對話方塊出現時，按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![[Azure 登入] 對話方塊][A06]

1. <span data-ttu-id="e1d22-142">當 [選取訂用帳戶]對話方塊出現時，請選取您要使用的訂用帳戶，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![[選取訂用帳戶] 對話方塊][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="e1d22-144">當您以自動化方式登入時，登出您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e1d22-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="e1d22-145">在上一節中設定步驟之後，每次您重新啟動 Eclipse 時，Azure 工具組都會自動將您登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1d22-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="e1d22-146">不過，若要登出您的 Azure 帳戶，並防止 Azure 工具組自動將您登入，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e1d22-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="e1d22-147">在 Eclipse 中，依序按一下 [工具]、[Azure] 以及 [登出]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 登出的 Eclipse 功能表][L01]

1. <span data-ttu-id="e1d22-149">當 [Azure 登出] 對話方塊出現時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![[登出] 對話方塊][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="e1d22-151">使用已建立的認證檔案來自動登入 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e1d22-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="e1d22-152">如果您在使用 Eclipse 時登出 Azure，必須重新設定適用於 Eclipse 的 Azure 工具組來使用已建立的認證檔案之後，才可以自動登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1d22-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="e1d22-153">下列步驟將引導您將 Azure 工具組設定為使用現有的認證檔案。</span><span class="sxs-lookup"><span data-stu-id="e1d22-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="e1d22-154">使用 Eclipse 開啟您的專案。</span><span class="sxs-lookup"><span data-stu-id="e1d22-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="e1d22-155">依序按一下 [工具]、[Azure] 以及 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 登入的 Eclipse 功能表][A01]

1. <span data-ttu-id="e1d22-157">當 [Azure 登入] 對話方塊出現時，請選取 [自動化]，然後按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![[登入] 對話方塊][A02]

1. <span data-ttu-id="e1d22-159">當 [選取驗證檔案] 對話方塊出現時，請選取您稍早建立的認證檔案，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![[登入] 對話方塊][A08]

1. <span data-ttu-id="e1d22-161">當 [Azure 登入]對話方塊出現時，按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![[Azure 登入] 對話方塊][A06]

1. <span data-ttu-id="e1d22-163">當 [選取訂用帳戶]對話方塊出現時，請選取您要使用的訂用帳戶，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![[選取訂用帳戶] 對話方塊][A07]

## <a name="see-also"></a><span data-ttu-id="e1d22-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e1d22-165">See Also</span></span>
<span data-ttu-id="e1d22-166">如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="e1d22-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="e1d22-167">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="e1d22-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e1d22-168">[適用於 Eclipse 的 Azure 工具組的新功能]</span><span class="sxs-lookup"><span data-stu-id="e1d22-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e1d22-169">[安裝 Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e1d22-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e1d22-170">適用於 Eclipse 的 Azure 工具組登入指示 (本文)</span><span class="sxs-lookup"><span data-stu-id="e1d22-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="e1d22-171">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]</span><span class="sxs-lookup"><span data-stu-id="e1d22-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="e1d22-172">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e1d22-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e1d22-173">[適用於 IntelliJ 的 Azure 工具組新增功能]</span><span class="sxs-lookup"><span data-stu-id="e1d22-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e1d22-174">[安裝 Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e1d22-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e1d22-175">[適用於 IntelliJ 的 Azure 工具組登入指示]</span><span class="sxs-lookup"><span data-stu-id="e1d22-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e1d22-176">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="e1d22-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="e1d22-177">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="e1d22-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="e1d22-178">[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="e1d22-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="e1d22-180">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="e1d22-181">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="e1d22-182">[安裝 Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="e1d22-183">[安裝 Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="e1d22-184">[適用於 IntelliJ 的 Azure 工具組登入指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="e1d22-185">[適用於 Eclipse 的 Azure 工具組的新功能]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="e1d22-186">[適用於 IntelliJ 的 Azure 工具組新增功能]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="e1d22-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="e1d22-187">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="e1d22-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="e1d22-188">[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="e1d22-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
