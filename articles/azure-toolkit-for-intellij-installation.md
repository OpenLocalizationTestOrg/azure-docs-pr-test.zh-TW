---
title: "安裝適用於 IntelliJ 的 Azure 工具組 | Microsoft Docs"
description: "了解如何安裝 Azure Toolkit for the IntelliJ IDEA。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bf11a8580500f78c4a96a02953f221501eeffe6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="a7404-103">安裝 Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a7404-103">Installing the Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="a7404-104">Azure Toolkit for IntelliJ 提供範本和功能，可讓您輕鬆地使用 IntelliJ IDEA 開發環境來建立、開發、測試及部署 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7404-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the IntelliJ IDEA development environment.</span></span> <span data-ttu-id="a7404-105">Azure Toolkit for IntelliJ 是開放原始碼專案，其來源程式碼可從 GitHub 上該專案網站的 MIT License 下取得，URL 如下：</span><span class="sxs-lookup"><span data-stu-id="a7404-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span>

<span data-ttu-id="a7404-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="a7404-106"><https://github.com/microsoft/azure-tools-for-java></span></span>

<span data-ttu-id="a7404-107">安裝 Azure Toolkit for IntelliJ 的方法有兩種，一種是從 [設定] 對話方塊，另一種是從啟動畫面上的 [設定] 功能表；下列步驟中將會示範這兩種安裝方法。</span><span class="sxs-lookup"><span data-stu-id="a7404-107">There are two methods of installing the Azure Toolkit for IntelliJ, from the Settings dialog box and from the Configure menu on the start screen; both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="a7404-108">從 [設定] 對話方塊安裝 Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a7404-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>
1. <span data-ttu-id="a7404-109">啟動 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="a7404-109">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="a7404-110">IntelliJ IDEA 開啟時，按一下 [檔案]，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="a7404-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
    ![開啟 IntelliJ IDEA 的 [設定] 對話方塊][01a]
3. <span data-ttu-id="a7404-112">在 [設定] 對話方塊中，按一下 [外掛程式]，然後按一下 [瀏覽儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="a7404-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
    ![IntelliJ IDEA [設定] 對話方塊][02a]
4. <span data-ttu-id="a7404-114">在 [瀏覽儲存機制] 對話方塊中，於 [搜尋] 方塊中輸入 "Azure"。</span><span class="sxs-lookup"><span data-stu-id="a7404-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="a7404-115">反白顯示 [適用於 IntelliJ 的 Azure 工具組]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="a7404-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![搜尋 Azure Toolkit for IntelliJ][03]
   
    <span data-ttu-id="a7404-117">IntelliJ IDEA 會在對話方塊中顯示安裝進度。</span><span class="sxs-lookup"><span data-stu-id="a7404-117">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![安裝進度][04]
5. <span data-ttu-id="a7404-119">安裝完成後，按一下 [重新啟動 IntelliJ IDEA] 。</span><span class="sxs-lookup"><span data-stu-id="a7404-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![重新啟動 IntelliJ IDEA][05]
6. <span data-ttu-id="a7404-121">按一下 [確定]  以關閉 [設定] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a7404-121">Click **OK** to close the Settings dialog box.</span></span>
   
    ![關閉 IntelliJ IDEA [設定] 對話方塊][06]
7. <span data-ttu-id="a7404-123">當系統提示您重新啟動 IntelliJ IDEA 或延後，請按一下 [重新啟動] 。</span><span class="sxs-lookup"><span data-stu-id="a7404-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![重新啟動 IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="a7404-125">從啟動畫面安裝 Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a7404-125">To install the Azure Toolkit for IntelliJ from the start screen</span></span>
1. <span data-ttu-id="a7404-126">啟動 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="a7404-126">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="a7404-127">IntelliJ IDEA 啟動畫面出現時，按一下 [設定]，然後按一下 [外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="a7404-127">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
    ![安裝 IntelliJ IDEA 外掛程式][01b]
3. <span data-ttu-id="a7404-129">在 [外掛程式] 對話方塊中，按一下 [瀏覽儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="a7404-129">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
    ![瀏覽 IntelliJ IDEA 外掛程式儲存機制][02b]
4. <span data-ttu-id="a7404-131">在 [瀏覽儲存機制] 對話方塊中，於 [搜尋] 方塊中輸入 "Azure"。</span><span class="sxs-lookup"><span data-stu-id="a7404-131">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="a7404-132">反白顯示 [適用於 IntelliJ 的 Azure 工具組]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="a7404-132">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![搜尋 Azure Toolkit for IntelliJ][03]
   
    <span data-ttu-id="a7404-134">IntelliJ IDEA 會在對話方塊中顯示安裝進度。</span><span class="sxs-lookup"><span data-stu-id="a7404-134">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![安裝進度][04]
5. <span data-ttu-id="a7404-136">安裝完成後，按一下 [重新啟動 IntelliJ IDEA] 。</span><span class="sxs-lookup"><span data-stu-id="a7404-136">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![重新啟動 IntelliJ IDEA][05]
6. <span data-ttu-id="a7404-138">當系統提示您重新啟動 IntelliJ IDEA 或延後，請按一下 [重新啟動] 。</span><span class="sxs-lookup"><span data-stu-id="a7404-138">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![重新啟動 IntelliJ IDEA][07]

## <a name="see-also"></a><span data-ttu-id="a7404-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a7404-140">See Also</span></span>
<span data-ttu-id="a7404-141">如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="a7404-141">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="a7404-142">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="a7404-142">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a7404-143">[適用於 Eclipse 的 Azure 工具組的新功能]</span><span class="sxs-lookup"><span data-stu-id="a7404-143">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a7404-144">[安裝 Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a7404-144">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a7404-145">[適用於 Eclipse 的 Azure 工具組登入指示]</span><span class="sxs-lookup"><span data-stu-id="a7404-145">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a7404-146">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]</span><span class="sxs-lookup"><span data-stu-id="a7404-146">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="a7404-147">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a7404-147">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a7404-148">[適用於 IntelliJ 的 Azure 工具組新增功能]</span><span class="sxs-lookup"><span data-stu-id="a7404-148">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <bpt id="p1">*</bpt>Installing the Azure Toolkit for IntelliJ (This Article)<ept id="p1">*</ept>
  * <span data-ttu-id="a7404-150">[適用於 IntelliJ 的 Azure 工具組登入指示]</span><span class="sxs-lookup"><span data-stu-id="a7404-150">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a7404-151">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="a7404-151">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="a7404-152">如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="a7404-152">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="a7404-153">[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="a7404-153">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="a7404-154">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="a7404-154">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="a7404-155">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="a7404-155">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="a7404-156">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="a7404-156">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="a7404-157">[安裝 Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="a7404-157">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
<span data-ttu-id="a7404-158">[適用於 Eclipse 的 Azure 工具組登入指示]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="a7404-158">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="a7404-159">[適用於 IntelliJ 的 Azure 工具組登入指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="a7404-159">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="a7404-160">[適用於 Eclipse 的 Azure 工具組的新功能]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="a7404-160">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="a7404-161">[適用於 IntelliJ 的 Azure 工具組新增功能]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="a7404-161">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="a7404-162">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="a7404-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01a]: ./media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: ./media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: ./media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: ./media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: ./media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: ./media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: ./media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: ./media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: ./media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
