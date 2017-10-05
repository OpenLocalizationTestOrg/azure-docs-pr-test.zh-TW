---
title: "安裝適用於 Eclipse 的 Azure 工具組 | Microsoft Docs"
description: "了解如何安裝 Azure Toolkit for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="d614b-103">安裝 Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="d614b-103">Installing the Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="d614b-104">Azure Toolkit for Eclipse 提供範本和功能，可讓您輕鬆地使用 Eclipse 開發環境來建立、開發、測試及部署 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d614b-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="d614b-105">適用於 Eclipse 的 Azure 工具組是開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="d614b-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="d614b-106">原始程式碼位於 <https://github.com/microsoft/azure-tools-for-java> 的 MIT 授權下方。</span><span class="sxs-lookup"><span data-stu-id="d614b-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="d614b-107">下列步驟示範如何安裝 Azure Toolkit for Eclipse。</span><span class="sxs-lookup"><span data-stu-id="d614b-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="d614b-108">安裝 Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="d614b-108">To install the Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="d614b-109">啟動 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="d614b-109">Start Eclipse.</span></span>
2. <span data-ttu-id="d614b-110">按一下 [說明] 功能表，然後按一下 [安裝新軟體]，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="d614b-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
    ![安裝 Azure Toolkit for Eclipse][01]
3. <span data-ttu-id="d614b-112">在 [可用軟體] 對話方塊的 [使用] 文字方塊中，鍵入 `http://dl.microsoft.com/eclipse`，然後按一下 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="d614b-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by the **Enter** key.</span></span>
4. <span data-ttu-id="d614b-113">在 [名稱] 窗格中，核取 [Azure Toolkit for Eclipse]，然後取消核取 [在安裝期間連絡所有更新網站來尋找必要軟體]。</span><span class="sxs-lookup"><span data-stu-id="d614b-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="d614b-114">您的畫面看起來應該像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="d614b-114">Your screen should appear similar to the following:</span></span>
   
    ![安裝 Azure Toolkit for Eclipse][02]
5. <span data-ttu-id="d614b-116">如果您展開 [Azure Toolkit for Eclipse] ，則會看到下列項目：</span><span class="sxs-lookup"><span data-stu-id="d614b-116">If you expand the **Azure Toolkit for Eclipse**, you will see the following items:</span></span>
   
   * <span data-ttu-id="d614b-117">**Application Insights Plugin for Java**：這個元件可讓您將 Azure 的遙測記錄和分析服務用於應用程式和伺服器執行個體上。</span><span class="sxs-lookup"><span data-stu-id="d614b-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="d614b-118">**Azure Access Control Services Filter**：此元件提供利用 Azure ACS 驗證應用程式使用者、啟用單一登入案例以及從應用程式外部化身分識別邏輯的支援。</span><span class="sxs-lookup"><span data-stu-id="d614b-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="d614b-119">**Azure Common Plugin**：此元件提供其他工具組元件所需的一般功能。</span><span class="sxs-lookup"><span data-stu-id="d614b-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="d614b-120">**Azure Explorer for Eclipse**：此元件提供其他工具組元件所需的一般功能。</span><span class="sxs-lookup"><span data-stu-id="d614b-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="d614b-121">**Azure Plugin for Eclipse with Java**：此元件提供在 Eclipse 中與透過命令列開發可協助建置、測試和部署適用於 Microsoft Azure 雲端的 Java 應用程式之專案的支援。</span><span class="sxs-lookup"><span data-stu-id="d614b-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="d614b-122">**Azure Web Apps Plugin with Java**：此元件提供將 Java Web 應用程式部署到 Microsoft Azure Web 應用程式容器的支援。</span><span class="sxs-lookup"><span data-stu-id="d614b-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="d614b-123">**Microsoft JDBC Driver 4.2 for SQL Server**：這個元件提供適用於 SQL Server 的 JDBC API 以及適用於 Java Platform Enterprise Edition 8 的 Microsoft Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d614b-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="d614b-124">**Package for Apache Qpid Client Libraries for JMS**：此元件提供 Apache Qpid 專案的 JMS 用戶端元件，讓您的應用程式能在 Microsoft Azure 中使用 AMQP 訊息。</span><span class="sxs-lookup"><span data-stu-id="d614b-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="d614b-125">**Package for Microsoft Azure Libraries for Java**：此元件提供用來存取 Microsoft Azure 服務 (例如儲存體、服務匯流排、服務執行階段等) 的 API。</span><span class="sxs-lookup"><span data-stu-id="d614b-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="d614b-126">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d614b-126">Click **Next**.</span></span> <span data-ttu-id="d614b-127">(如果您在安裝此工具組時遇到不尋常的延遲，請確認已取消勾選 [在安裝期間連絡所有更新網站來尋找必要軟體]。)</span><span class="sxs-lookup"><span data-stu-id="d614b-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>
7. <span data-ttu-id="d614b-128">在 [安裝詳細資料] 對話方塊中，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d614b-128">In the **Install Details** dialog, click **Next**.</span></span>
   
    ![檢閱安裝詳細資料][03]
8. <span data-ttu-id="d614b-130">在 [檢閱授權] 對話方塊中，檢閱授權合約的條款。</span><span class="sxs-lookup"><span data-stu-id="d614b-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="d614b-131">如果您接受授權合約的條款，請按一下 [我接受授權合約的條款]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d614b-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="d614b-132">(其餘的步驟假設您接受授權合約的條款。</span><span class="sxs-lookup"><span data-stu-id="d614b-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="d614b-133">如果您不接受授權合約的條款，請結束安裝程序。)</span><span class="sxs-lookup"><span data-stu-id="d614b-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
    ![檢閱授權][04]
   
    <span data-ttu-id="d614b-135">Eclipse 會下載並安裝必要的封裝。</span><span class="sxs-lookup"><span data-stu-id="d614b-135">Eclipse will download and install the requisite packages.</span></span>
   
    ![安裝進度][05]
9. <span data-ttu-id="d614b-137">如果系統提示您重新啟動 Eclipse 以完成安裝，請按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="d614b-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
    ![重新啟動提示][06]

## <a name="see-also"></a><span data-ttu-id="d614b-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d614b-139">See Also</span></span>
<span data-ttu-id="d614b-140">如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="d614b-140">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="d614b-141">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="d614b-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d614b-142">[適用於 Eclipse 的 Azure 工具組的新功能]</span><span class="sxs-lookup"><span data-stu-id="d614b-142">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <bpt id="p1">*</bpt>Installing the Azure Toolkit for Eclipse (This Article)<ept id="p1">*</ept>
  * <span data-ttu-id="d614b-144">[適用於 Eclipse 的 Azure 工具組登入指示]</span><span class="sxs-lookup"><span data-stu-id="d614b-144">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d614b-145">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]</span><span class="sxs-lookup"><span data-stu-id="d614b-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="d614b-146">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d614b-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d614b-147">[適用於 IntelliJ 的 Azure 工具組新增功能]</span><span class="sxs-lookup"><span data-stu-id="d614b-147">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d614b-148">[安裝 Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d614b-148">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d614b-149">[適用於 IntelliJ 的 Azure 工具組登入指示]</span><span class="sxs-lookup"><span data-stu-id="d614b-149">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d614b-150">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="d614b-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="d614b-151">如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="d614b-151">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="d614b-152">[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="d614b-152">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="d614b-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="d614b-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="d614b-154">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="d614b-154">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="d614b-155">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="d614b-155">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
<span data-ttu-id="d614b-156">[安裝 Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="d614b-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="d614b-157">[適用於 Eclipse 的 Azure 工具組登入指示]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="d614b-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="d614b-158">[適用於 IntelliJ 的 Azure 工具組登入指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="d614b-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="d614b-159">[適用於 Eclipse 的 Azure 工具組的新功能]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="d614b-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="d614b-160">[適用於 IntelliJ 的 Azure 工具組新增功能]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="d614b-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="d614b-161">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="d614b-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
