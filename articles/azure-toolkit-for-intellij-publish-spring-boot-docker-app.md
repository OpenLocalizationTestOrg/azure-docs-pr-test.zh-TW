---
title: "aaaPublish Spring 開機應用程式以使用 Docker 容器 hello Azure Toolkit for IntelliJ |Microsoft 文件"
description: "深入了解如何為 Docker 容器使用的 Azure web 應用程式 tooMicrosoft toopublish hello Azure Toolkit IntelliJ。"
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="36fb6-103">Docker 容器發行 Spring 開機應用程式使用 hello Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="36fb6-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="36fb6-104">hello [Spring 架構]是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。</span><span class="sxs-lookup"><span data-stu-id="36fb6-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="36fb6-105">其中一個 hello 更常用建置的專案是在該平台是[Spring 開機]，可提供簡單的方法建立獨立的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="36fb6-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="36fb6-106">[Docker]是開放原始碼解決方案，可協助開發人員自動化 hello 部署、 調整及管理其容器中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="36fb6-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="36fb6-107">本教學課程中引導您完成 hello 步驟 toodeploy Spring 開機應用程式，Azure Docker 容器 tooMicrosoft 為使用 hello Azure Toolkit for IntelliJ。</span><span class="sxs-lookup"><span data-stu-id="36fb6-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="36fb6-108">複製 hello 預設 Spring 開機 Docker 儲存機制</span><span class="sxs-lookup"><span data-stu-id="36fb6-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="36fb6-109">hello 下列步驟引導您完成使用 IntelliJ 複製 hello Spring 開機 Docker 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="36fb6-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="36fb6-110">如果您想 toouse 命令列，請參閱[部署 Spring 開機應用程式在 Azure 容器服務中的 Linux 上][Deploy Spring Boot on Linux in ACS]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="36fb6-111">開啟 IntelliJ。</span><span class="sxs-lookup"><span data-stu-id="36fb6-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="36fb6-112">在 hello 歡迎畫面上，選取 hello **GitHub**選項在 hello**版本控制中簽出**清單。</span><span class="sxs-lookup"><span data-stu-id="36fb6-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![版本控制的 GitHub 選項][CL01]

1. <span data-ttu-id="36fb6-114">如果您是提示的 toolog 中，輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="36fb6-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="36fb6-115">如果您使用使用者名稱/密碼 toolog tooGitHub 中：</span><span class="sxs-lookup"><span data-stu-id="36fb6-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![用於輸入 GitHub 使用者名稱和密碼的對話方塊][CL02a]

   * <span data-ttu-id="36fb6-117">如果您正在使用語彙基元 toolog tooGitHub 中：</span><span class="sxs-lookup"><span data-stu-id="36fb6-117">If you are using a token toolog in tooGitHub:</span></span>

      ![用於輸入 GitHub 權杖的對話方塊][CL02b]

1. <span data-ttu-id="36fb6-119">輸入**https://github.com/spring-guides/gs-spring-boot-docker.git** hello 儲存機制 URL，請指定您的本機路徑和資料夾資訊，然後按一下**複製**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![[複製存放庫] 對話方塊][CL03]

1. <span data-ttu-id="36fb6-121">當系統提示您輸入 toocreate IntelliJ 專案選取**否**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![拒絕 toocreate IntelliJ 專案][CL04]

1. <span data-ttu-id="36fb6-123">在 hello  褖畫惎 頁面上，按一下 **匯入專案**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-123">On hello welcome page, click **Import Project**.</span></span>

   ![選擇 [匯入專案]][CL05]

1. <span data-ttu-id="36fb6-125">找出您再製 hello Spring 開機儲存機制的 hello 路徑中，選取 hello**完成**下 hello 根目錄，然後按一下資料夾**確定**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![選取要匯入的資料夾][CL06]

1. <span data-ttu-id="36fb6-127">當系統提示您時，選取 [從現有來源建立專案]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![選項 toocreate 從現有來源的專案][CL07]

1. <span data-ttu-id="36fb6-129">指定您的專案名稱或接受預設值 hello、 確認 hello 正確的路徑 toohello**完成**資料夾，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![指定 hello 的專案名稱][CL08]

1. <span data-ttu-id="36fb6-131">自訂任何要匯入的目錄，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![選擇目錄][CL09]

1. <span data-ttu-id="36fb6-133">檢閱 hello 文件庫 tooimport，，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![檢閱專案程式庫][CL10]

1. <span data-ttu-id="36fb6-135">檢閱 hello 模組結構，並按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-135">Review hello module structure, and then click **Next**.</span></span>

   ![檢閱模組結構][CL11]

1. <span data-ttu-id="36fb6-137">指定您的 JDK，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-137">Specify your JDK, and then click **Next**.</span></span>

   ![指定 JDK][CL12]

1. <span data-ttu-id="36fb6-139">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="36fb6-139">Click **Finish**.</span></span>

   ![[完成] 按鈕][CL13]

<span data-ttu-id="36fb6-141">IntelliJ 匯入做為專案的 hello Spring 開機應用程式，並顯示 hello 結構 hello 匯入完成時。</span><span class="sxs-lookup"><span data-stu-id="36fb6-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![IntelliJ 中的 Spring Boot 應用程式][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="36fb6-143">建置 Spring Boot 應用程式</span><span class="sxs-lookup"><span data-stu-id="36fb6-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="36fb6-144">使用 hello Maven POM 建置 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="36fb6-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="36fb6-145">如果尚未開啟，請開啟 hello Maven 工具視窗。</span><span class="sxs-lookup"><span data-stu-id="36fb6-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="36fb6-146">按一下 [檢視] > [工具視窗] > [Maven 專案]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![[工具視窗] 和 [Maven 專案] 命令][BU01]

1. <span data-ttu-id="36fb6-148">在 hello Maven 工具視窗中，以滑鼠右鍵按一下**封裝**選取**執行 Maven 建置**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="36fb6-149">(如果 Maven 專案並不會自動顯示，按一下 hello**重新匯入**hello Maven 工具列上的圖示。)</span><span class="sxs-lookup"><span data-stu-id="36fb6-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![[執行 Maven 建置] 命令][BU02]

1. <span data-ttu-id="36fb6-151">Spring Boot 應用程式成功建立時，IntelliJ 應該會顯示「建置成功」訊息。</span><span class="sxs-lookup"><span data-stu-id="36fb6-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![「建置成功」訊息][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="36fb6-153">建立已可供部署的構件</span><span class="sxs-lookup"><span data-stu-id="36fb6-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="36fb6-154">toopublish Spring 開機應用程式，您需要 toocreate 可供部署的成品。</span><span class="sxs-lookup"><span data-stu-id="36fb6-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="36fb6-155">使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="36fb6-155">Use hello following steps:</span></span>

1. <span data-ttu-id="36fb6-156">在 IntelliJ 中開啟 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="36fb6-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="36fb6-157">依序按一下 [檔案] 及 [專案結構]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-157">Click **File**, and then click **Project Structure**.</span></span>

   ![[專案結構] 命令][ART01]

1. <span data-ttu-id="36fb6-159">按一下綠色加號 hello (**+**) 符號 tooadd 成品時，按一下  **JAR**，然後按一下**空**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![新增構件][ART02]

1. <span data-ttu-id="36fb6-161">命名您的成品，同時確保不 tooadd hello 「 d 」 延伸模組，然後指定 hello hello Maven 輸出的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="36fb6-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![指定構件屬性][ART03]

1. <span data-ttu-id="36fb6-163">建立構件的資訊清單 (選用)：</span><span class="sxs-lookup"><span data-stu-id="36fb6-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="36fb6-164">a.</span><span class="sxs-lookup"><span data-stu-id="36fb6-164">a.</span></span> <span data-ttu-id="36fb6-165">按一下 [建立資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-165">Click **Create Manifest**.</span></span>

      ![按一下 hello 建立資訊清單的按鈕][ART04a]

   <span data-ttu-id="36fb6-167">b.</span><span class="sxs-lookup"><span data-stu-id="36fb6-167">b.</span></span> <span data-ttu-id="36fb6-168">選擇 hello hello 成品的預設路徑，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![指定構件路徑][ART04b]

   <span data-ttu-id="36fb6-170">c.</span><span class="sxs-lookup"><span data-stu-id="36fb6-170">c.</span></span> <span data-ttu-id="36fb6-171">按一下 hello 省略符號 (**...**) toolocate hello 主要類別。</span><span class="sxs-lookup"><span data-stu-id="36fb6-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![找出主要類別][ART04c]

   <span data-ttu-id="36fb6-173">d.</span><span class="sxs-lookup"><span data-stu-id="36fb6-173">d.</span></span> <span data-ttu-id="36fb6-174">選擇您的主要類別，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="36fb6-174">Choose your main class, and then click **OK**.</span></span>

      ![指定主要類別][ART04d]

1. <span data-ttu-id="36fb6-176">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="36fb6-176">Click **OK**.</span></span>

   ![關閉 hello 專案結構對話方塊][ART05]

> [!NOTE]
> <span data-ttu-id="36fb6-178">如需在 IntelliJ 中建立成品的詳細資訊，請參閱[設定成品]hello JetBrains 網站上。</span><span class="sxs-lookup"><span data-stu-id="36fb6-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="36fb6-179">建置部署的 hello 成品</span><span class="sxs-lookup"><span data-stu-id="36fb6-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="36fb6-180">按一下 建置，然後按一下構件。</span><span class="sxs-lookup"><span data-stu-id="36fb6-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![[建置構件] 命令][BU04]

1. <span data-ttu-id="36fb6-182">當 hello**組建成品**出現內容功能表，按一下**建置**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![[建置構件] 操作功能表][BU05]

<span data-ttu-id="36fb6-184">IntelliJ 應該 hello 專案的工具視窗中會顯示 hello 完成 Spring 開機應用程式的成品。</span><span class="sxs-lookup"><span data-stu-id="36fb6-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![建立的構件][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="36fb6-186">使用 Docker 容器發行您的 web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="36fb6-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="36fb6-187">如果您不具有登入 tooyour Azure 帳戶，請依照下列中的 hello 步驟[登入的指示 hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="36fb6-188">在 hello [專案總管] 工具視窗中，hello 專案上按一下滑鼠右鍵，然後選取**Azure** > **發佈為 Docker 容器**。</span><span class="sxs-lookup"><span data-stu-id="36fb6-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![[發佈為 Docker 容器] 命令][PU01]

1. <span data-ttu-id="36fb6-190">當 hello**在 Azure 上部署 Docker 容器** 對話方塊隨即出現，則會顯示任何現有的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="36fb6-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="36fb6-191">如果您選擇 toodeploy tooan 現有主機，您可以略過 toostep 4。</span><span class="sxs-lookup"><span data-stu-id="36fb6-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="36fb6-192">否則，請使用下列步驟 toocreate 主機 hello:</span><span class="sxs-lookup"><span data-stu-id="36fb6-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="36fb6-193">a.</span><span class="sxs-lookup"><span data-stu-id="36fb6-193">a.</span></span> <span data-ttu-id="36fb6-194">按一下綠色加號 hello (**+**) 符號。</span><span class="sxs-lookup"><span data-stu-id="36fb6-194">Click hello green plus (**+**) symbol.</span></span>

      ![新增 Docker 主機][PU02]

   <span data-ttu-id="36fb6-196">b.</span><span class="sxs-lookup"><span data-stu-id="36fb6-196">b.</span></span> <span data-ttu-id="36fb6-197">當 hello**建立 Docker 主機** 對話方塊隨即出現，您可以選擇 tooaccept hello 預設值，或者您可以指定新的 Docker 主機的任何自訂設定。</span><span class="sxs-lookup"><span data-stu-id="36fb6-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="36fb6-198">(如需詳細說明 hello 的各種設定，請參閱[為 Docker 容器發行 web 應用程式，使用 IntelliJ hello Azure Toolkit][Publish Container with Azure Toolkit]。)按一下**下一步**當您指定哪些設定 toouse。</span><span class="sxs-lookup"><span data-stu-id="36fb6-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![指定 Docker 主機選項][PU03a]

   <span data-ttu-id="36fb6-200">c.</span><span class="sxs-lookup"><span data-stu-id="36fb6-200">c.</span></span> <span data-ttu-id="36fb6-201">您可以從 Azure 金鑰保存庫選擇 toouse 現有登入認證，或者您可以選擇 tooenter 新 Docker 登入認證。</span><span class="sxs-lookup"><span data-stu-id="36fb6-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="36fb6-202">當您已指定選項時，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-202">Click **Finish** when you have specified your options.</span></span>

      ![指定 Docker 主機認證][PU03b]

1. <span data-ttu-id="36fb6-204">選取您的 Docker 主機，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="36fb6-204">Select your Docker host, and then click **Next**.</span></span>

   ![選取 hello Docker 主機 toouse][PU04]

1. <span data-ttu-id="36fb6-206">Hello hello 最後一頁上**在 Azure 上部署 Docker 容器**對話方塊方塊中，指定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="36fb6-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="36fb6-207">a.</span><span class="sxs-lookup"><span data-stu-id="36fb6-207">a.</span></span> <span data-ttu-id="36fb6-208">您可以選擇 toospecify hello 容器，將會裝載您的 Docker 容器的自訂名稱，或者您可以接受 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="36fb6-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="36fb6-209">b.</span><span class="sxs-lookup"><span data-stu-id="36fb6-209">b.</span></span> <span data-ttu-id="36fb6-210">使用下列語法的 hello docker 主機輸入 hello TCP 連接埠： *[外部連接埠]*:*[內部連接埠]*。</span><span class="sxs-lookup"><span data-stu-id="36fb6-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="36fb6-211">例如， **80:8080**指定外部連接埠 80 與 hello 預設 Spring 開機的內部連接埠 8080。</span><span class="sxs-lookup"><span data-stu-id="36fb6-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="36fb6-212">如果您已自訂您的內部連接埠 （例如，藉由編輯 hello application.yml 檔案），您需要 toospecify hello 連接埠號碼 hello 正確路由的 toooccur 在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="36fb6-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="36fb6-213">c.</span><span class="sxs-lookup"><span data-stu-id="36fb6-213">c.</span></span> <span data-ttu-id="36fb6-214">設定這些選項之後，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="36fb6-214">After you have configured these options, click **Finish**.</span></span>

   ![在 Azure 上部署 Docker 容器][PU05]

1. <span data-ttu-id="36fb6-216">當 hello Azure Toolkit 完成發行時，hello Azure 活動記錄檔顯示**發佈**hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="36fb6-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![已成功部署 Docker 主機][PU06]

## <a name="next-steps"></a><span data-ttu-id="36fb6-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36fb6-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="36fb6-219">toolearn 需額外的方法，以建立 Spring 開機應用程式使用 IntelliJ，請參閱[建立 Spring 開機專案](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html)hello JetBrains 網站上。</span><span class="sxs-lookup"><span data-stu-id="36fb6-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[設定成品]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring 開機]: http://projects.spring.io/spring-boot/
[Spring 架構]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
