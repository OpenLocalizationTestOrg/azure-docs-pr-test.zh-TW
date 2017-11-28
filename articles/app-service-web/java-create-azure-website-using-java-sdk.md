---
title: "aaaCreate 使用 hello Azure SDK for Java 的 Azure App Service 中的 Web 應用程式"
description: "了解如何 toocreate Web 應用程式以程式設計方式使用的 Azure App Service 上 hello Azure SDK for Java。"
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="52c33-103">使用 hello Azure SDK for Java 的 Azure App Service 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="52c33-104">概觀</span><span class="sxs-lookup"><span data-stu-id="52c33-104">Overview</span></span>
<span data-ttu-id="52c33-105">本逐步解說示範如何建立 Web 應用程式中的 Java 應用程式的 Azure SDK toocreate [Azure App Service][Azure App Service]，然後部署應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="52c33-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="52c33-106">其中包括兩個部分：</span><span class="sxs-lookup"><span data-stu-id="52c33-106">It consists of two parts:</span></span>

* <span data-ttu-id="52c33-107">第 1 部分會示範如何 toobuild Java 應用程式，會建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="52c33-108">第 2 部分會示範如何 toocreate 簡單 JSP"Hello World"應用程式，然後使用 FTP 用戶端 toodeploy 程式碼 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="52c33-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52c33-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="52c33-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="52c33-110">軟體安裝</span><span class="sxs-lookup"><span data-stu-id="52c33-110">Software Installations</span></span>
<span data-ttu-id="52c33-111">hello AzureWebDemo 本文中的應用程式程式碼撰寫使用 Azure Java SDK 0.7.0，您可以安裝使用 hello [Web Platform Installer] [ Web Platform Installer] (WebPI)。</span><span class="sxs-lookup"><span data-stu-id="52c33-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="52c33-112">此外，請確定 toouse hello 最新版本的 hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="52c33-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="52c33-113">安裝 hello SDK 之後，更新您的 Eclipse 專案中的 hello 相依性執行**更新索引**中**Maven 儲存機制**，再重新加入 hello 最新版本，每個封裝中 hello **相依性**視窗。</span><span class="sxs-lookup"><span data-stu-id="52c33-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="52c33-114">您可以按一下來確認您已安裝的軟體在 Eclipse 中的 hello 版本**協助 > 安裝詳細資料**; 您應該有至少 hello 下列版本：</span><span class="sxs-lookup"><span data-stu-id="52c33-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="52c33-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="52c33-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="52c33-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="52c33-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="52c33-117">在 Azure 中建立和設定雲端資源</span><span class="sxs-lookup"><span data-stu-id="52c33-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="52c33-118">在開始此程序之前，您會需要 toohave 作用中的 Azure 訂用帳戶，並設定預設的 Active Directory (AD) 在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="52c33-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="52c33-119">在 Azure 中建立 Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="52c33-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="52c33-120">如果您沒有 Azure 訂用帳戶已經有 Active Directory (AD)，登入 hello [Azure 傳統入口網站][ Azure classic portal]與您的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="52c33-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="52c33-121">如果您有多個訂閱，按一下**訂閱**和選取 hello 預設目錄 hello 訂閱您想要 toouse 為這個專案。</span><span class="sxs-lookup"><span data-stu-id="52c33-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="52c33-122">然後按一下 **套用**tooswitch toothat 訂閱檢視。</span><span class="sxs-lookup"><span data-stu-id="52c33-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="52c33-123">選取**Active Directory**從左邊的 hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="52c33-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="52c33-124">按一下 [新增] > [目錄] > [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="52c33-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="52c33-125">在 [新增目錄] 中，選取 [建立新目錄]。</span><span class="sxs-lookup"><span data-stu-id="52c33-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="52c33-126">在 [ **名稱**] 中，輸入目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="52c33-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="52c33-127">在 [網域] 中，輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="52c33-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="52c33-128">這是與您的目錄; 預設隨附的基本網域名稱它有 hello 表單`<domain_name>.onmicrosoft.com`。</span><span class="sxs-lookup"><span data-stu-id="52c33-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="52c33-129">您可以命名會根據 hello 目錄名稱或另一個您所擁有的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="52c33-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="52c33-130">之後，您可以新增貴組織已使用的其他網域名稱。</span><span class="sxs-lookup"><span data-stu-id="52c33-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="52c33-131">在 [ **國家或地區**] 中，選取您的地區設定。</span><span class="sxs-lookup"><span data-stu-id="52c33-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="52c33-132">如需 AD 詳細資訊，請參閱 [什麼是 Azure Active Directory][What is an Azure AD directory]？</span><span class="sxs-lookup"><span data-stu-id="52c33-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="52c33-133">建立 Azure 的管理憑證</span><span class="sxs-lookup"><span data-stu-id="52c33-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="52c33-134">hello Azure SDK for Java 使用管理憑證 tooauthenticate 與 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="52c33-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="52c33-135">這些是您使用 tooauthenticate 使用 hello 服務管理 API tooact 代表 hello 訂用帳戶擁有者 toomanage 訂用帳戶資源的用戶端應用程式的 X.509 v3 憑證。</span><span class="sxs-lookup"><span data-stu-id="52c33-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="52c33-136">此程序中的 hello 程式碼會使用自我簽署的憑證 tooauthenticate 與 Azure。</span><span class="sxs-lookup"><span data-stu-id="52c33-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="52c33-137">在此程序需要 toocreate 憑證，並將它上傳 toohello [Azure 傳統入口網站][ Azure classic portal]事先。</span><span class="sxs-lookup"><span data-stu-id="52c33-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="52c33-138">這牽涉到 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="52c33-138">This involves hello following steps:</span></span>

* <span data-ttu-id="52c33-139">產生代表您的用戶端憑證的 PFX 檔案，並將其儲存於本機。</span><span class="sxs-lookup"><span data-stu-id="52c33-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="52c33-140">從 hello PFX 檔案產生管理憑證 （CER 檔案）。</span><span class="sxs-lookup"><span data-stu-id="52c33-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="52c33-141">上傳 hello CER 檔案 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="52c33-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="52c33-142">因為 Java 使用該使用憑證的格式 tooauthenticate 轉換 JKS，hello PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="52c33-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="52c33-143">撰寫 hello 應用程式的驗證程式碼，它會參考 toohello 本機 JKS 檔案。</span><span class="sxs-lookup"><span data-stu-id="52c33-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="52c33-144">當您完成此程序時，hello CER 憑證都位於您的 Azure 訂閱和 hello JKS 憑證都位於本機磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="52c33-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="52c33-145">如需管理憑證的詳細資訊，請參閱 [建立和上傳 Azure 的管理憑證][Create and Upload a Management Certificate for Azure]。</span><span class="sxs-lookup"><span data-stu-id="52c33-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="52c33-146">建立憑證</span><span class="sxs-lookup"><span data-stu-id="52c33-146">Create a certificate</span></span>
<span data-ttu-id="52c33-147">toocreate 您自己的自我簽署的憑證，開啟命令主控台，在您的作業系統上，然後執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="52c33-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="52c33-148">**注意：** hello 電腦執行這個命令必須有 hello 安裝的 JDK。</span><span class="sxs-lookup"><span data-stu-id="52c33-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="52c33-149">此外，hello 路徑 toohello keytool hello hello JDK 安裝的位置而定。</span><span class="sxs-lookup"><span data-stu-id="52c33-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="52c33-150">如需詳細資訊，請參閱[金鑰和憑證管理工具 (keytool)] [ Key and Certificate Management Tool (keytool)] hello Java 線上文件中。</span><span class="sxs-lookup"><span data-stu-id="52c33-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="52c33-151">toocreate hello.pfx 檔案：</span><span class="sxs-lookup"><span data-stu-id="52c33-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="52c33-152">toocreate hello.cer 檔案：</span><span class="sxs-lookup"><span data-stu-id="52c33-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="52c33-153">其中：</span><span class="sxs-lookup"><span data-stu-id="52c33-153">where:</span></span>

* <span data-ttu-id="52c33-154">`<java-install-dir>`是您已安裝 Java hello 路徑 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="52c33-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="52c33-155">`<keystore-id>`hello 金鑰存放區項目識別項 (例如， `AzureRemoteAccess`)。</span><span class="sxs-lookup"><span data-stu-id="52c33-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="52c33-156">`<cert-store-dir>`是您想在其中 toostore 憑證 hello 路徑 toohello 目錄 (例如`C:/Certificates`)。</span><span class="sxs-lookup"><span data-stu-id="52c33-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="52c33-157">`<cert-file-name>`這是 hello hello 憑證檔案名稱 (例如`AzureWebDemoCert`)。</span><span class="sxs-lookup"><span data-stu-id="52c33-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="52c33-158">`<password>`這是您選擇 tooprotect hello 憑證; hello 密碼它必須是至少 6 個字元。</span><span class="sxs-lookup"><span data-stu-id="52c33-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="52c33-159">您可以不輸入密碼，但不建議這麼做。</span><span class="sxs-lookup"><span data-stu-id="52c33-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="52c33-160">`<dname>`hello X.500 辨別名稱 toobe 相關聯的別名，並當做 hello 簽發者和 hello 自我簽署憑證中的 [主旨] 欄位。</span><span class="sxs-lookup"><span data-stu-id="52c33-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="52c33-161">如需詳細資訊，請參閱 [建立和上傳 Azure 的管理憑證][Create and Upload a Management Certificate for Azure]。</span><span class="sxs-lookup"><span data-stu-id="52c33-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="52c33-162">上傳 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="52c33-162">Upload hello certificate</span></span>
<span data-ttu-id="52c33-163">tooupload 自我簽署的憑證 tooAzure，移 toohello**設定**hello 傳統入口網站，在頁面上，然後按一下 [hello**管理憑證**] 索引標籤。按一下**上傳**底部 hello hello 頁面上，瀏覽 toohello 建立 hello CER 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="52c33-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="52c33-164">Hello PFX 檔轉換成 JKS</span><span class="sxs-lookup"><span data-stu-id="52c33-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="52c33-165">在 hello （以系統管理員身分執行） 的 Windows 命令提示字元，cd toohello 目錄包含 hello 憑證並執行下列命令，hello 其中`<java-install-dir>`是您安裝 Java 在電腦的 hello 目錄：</span><span class="sxs-lookup"><span data-stu-id="52c33-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="52c33-166">出現提示時，輸入 hello 目的地 keystore 的密碼;這會是 hello hello JKS 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="52c33-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="52c33-167">出現提示時，輸入 hello 來源 keystore 的密碼。這是您指定 hello PFX 檔案的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="52c33-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="52c33-168">hello 兩個密碼並沒有 toobe hello 相同。</span><span class="sxs-lookup"><span data-stu-id="52c33-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="52c33-169">您可以不輸入密碼，但不建議這麼做。</span><span class="sxs-lookup"><span data-stu-id="52c33-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="52c33-170">建置 Web 應用程式建立應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="52c33-171">建立 hello Eclipse 工作區和 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="52c33-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="52c33-172">在本節中建立工作區和 Maven hello web 應用程式建立應用程式的專案，名為 AzureWebDemo。</span><span class="sxs-lookup"><span data-stu-id="52c33-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="52c33-173">建立新的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="52c33-173">Create a new Maven project.</span></span> <span data-ttu-id="52c33-174">按一下 [檔案] > [新增] > [Maven 專案]。</span><span class="sxs-lookup"><span data-stu-id="52c33-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="52c33-175">在 [新增 Maven 專案] 中，選取 [建立簡單專案] 和 [使用預設工作區位置]。</span><span class="sxs-lookup"><span data-stu-id="52c33-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="52c33-176">Hello 第二頁上**新 Maven 專案**，指定下列 hello:</span><span class="sxs-lookup"><span data-stu-id="52c33-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="52c33-177">群組識別碼： `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="52c33-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="52c33-178">成品識別碼：AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="52c33-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="52c33-179">版本：0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="52c33-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="52c33-180">封裝：jar</span><span class="sxs-lookup"><span data-stu-id="52c33-180">Packaging: jar</span></span>
   * <span data-ttu-id="52c33-181">名稱：AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="52c33-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="52c33-182">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-182">Click **Finish**.</span></span>
3. <span data-ttu-id="52c33-183">Hello 新專案的 pom.xml 檔案總管中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="52c33-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="52c33-184">選取 hello**相依性** 索引標籤。由於這是新專案，所以尚未列出任何封裝。</span><span class="sxs-lookup"><span data-stu-id="52c33-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="52c33-185">檢視開啟 hello Maven 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="52c33-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="52c33-186">按一下 [視窗] > [顯示檢視] > [其他] > [Maven] > [Maven 儲存機制]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="52c33-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="52c33-187">hello **Maven 儲存機制**檢視將會出現在 hello hello IDE 底部。</span><span class="sxs-lookup"><span data-stu-id="52c33-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="52c33-188">開啟**通用儲存機制**，以滑鼠右鍵按一下 hello**中央**儲存機制，並選取**重建索引**。</span><span class="sxs-lookup"><span data-stu-id="52c33-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="52c33-189">此步驟可能需要幾分鐘的時間視您的連線 hello 速度而定。</span><span class="sxs-lookup"><span data-stu-id="52c33-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="52c33-190">當 hello 索引重建作業時，您應該會看到 hello Microsoft Azure 套件 hello 中的**中央**Maven 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="52c33-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="52c33-191">在 [相依性] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="52c33-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="52c33-192">在 [輸入群組識別碼...] 中輸入 `azure-management`。</span><span class="sxs-lookup"><span data-stu-id="52c33-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="52c33-193">選取的基本管理和應用程式服務 Web 應用程式管理的 hello 封裝：</span><span class="sxs-lookup"><span data-stu-id="52c33-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="52c33-194">**注意：**新版本發行之後，您要更新 hello 相依性，如果您需要 toore-這份清單中加入每個 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="52c33-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="52c33-195">按一下 之後**新增**並選取每個相依性，它會使用 hello 新版本號碼 hello**相依性**清單。</span><span class="sxs-lookup"><span data-stu-id="52c33-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="52c33-196">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-196">Click **OK**.</span></span> <span data-ttu-id="52c33-197">hello Azure 的封裝，則會出現在 hello**相依性**清單。</span><span class="sxs-lookup"><span data-stu-id="52c33-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="52c33-198">呼叫 hello Azure SDK 撰寫 Java 程式碼 tooCreate Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="52c33-199">接下來，撰寫 Java toocreate hello App Service web 應用程式會呼叫應用程式開發介面 hello Azure SDK 中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="52c33-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="52c33-200">建立 Java 類別 toocontain hello 主要進入點的程式碼。</span><span class="sxs-lookup"><span data-stu-id="52c33-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="52c33-201">在 專案總管 hello 專案節點上按一下滑鼠右鍵，然後選取**新增 > 類別**。</span><span class="sxs-lookup"><span data-stu-id="52c33-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="52c33-202">在**新 Java 類別**，hello 類別命名`WebCreator`並檢查 hello**公用靜態 void main**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="52c33-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="52c33-203">hello 選取項目應該會出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="52c33-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="52c33-204">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-204">Click **Finish**.</span></span> <span data-ttu-id="52c33-205">hello WebCreator.java 檔案會出現在 [專案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="52c33-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="52c33-206">呼叫 hello Azure API tooCreate App Service Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="52c33-207">新增必要匯入</span><span class="sxs-lookup"><span data-stu-id="52c33-207">Add necessary imports</span></span>
<span data-ttu-id="52c33-208">在 WebCreator.java，加入下列匯入; hello這些匯入提供使用 Azure 應用程式開發介面存取 tooclasses hello 中的管理程式庫：</span><span class="sxs-lookup"><span data-stu-id="52c33-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="52c33-209">定義 hello 主要進入點類別</span><span class="sxs-lookup"><span data-stu-id="52c33-209">Define hello main entry point class</span></span>
<span data-ttu-id="52c33-210">Hello 目的 hello AzureWebDemo 應用程式是 toocreate App Service Web 應用程式，因為此應用程式的名稱 hello 主要類別`WebAppCreator`。</span><span class="sxs-lookup"><span data-stu-id="52c33-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="52c33-211">這個類別會提供 hello 主要進入點呼叫的程式碼 hello Azure 服務管理 API toocreate hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="52c33-212">新增下列 hello web 應用程式和網路空間的參數定義的 hello。</span><span class="sxs-lookup"><span data-stu-id="52c33-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="52c33-213">您將需要 tooprovide 您自己的 Azure 訂用帳戶 ID 和憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="52c33-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="52c33-214">其中：</span><span class="sxs-lookup"><span data-stu-id="52c33-214">where:</span></span>

* <span data-ttu-id="52c33-215">`<subscription-id>`這是您想在其中 toocreate hello 資源 hello Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="52c33-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="52c33-216">`<certificate-store-path>`是您的本機憑證存放區目錄中的 hello 路徑和檔名 toohello JKS 檔案。</span><span class="sxs-lookup"><span data-stu-id="52c33-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="52c33-217">例如，`C:/Certificates/CertificateName.jks` 適用於 Linux，而 `C:\Certificates\CertificateName.jks` 適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="52c33-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="52c33-218">`<certificate-password>`這是您在建立 JKS 憑證時指定的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="52c33-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="52c33-219">`webAppName`可以是您選擇; 任何名稱此程序會使用 hello 名稱`WebDemoWebApp`。</span><span class="sxs-lookup"><span data-stu-id="52c33-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="52c33-220">hello 的完整網域名稱為 hello`webAppName`以 hello`domainName`附加，因此在此案例 hello 完整的網域是`webdemowebapp.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="52c33-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="52c33-221">`domainName` 應如上所述加以指定。</span><span class="sxs-lookup"><span data-stu-id="52c33-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="52c33-222">`webSpaceName`應該有一個 hello 中定義的值 hello [WebSpaceNames] [ WebSpaceNames]類別。</span><span class="sxs-lookup"><span data-stu-id="52c33-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="52c33-223">`appServicePlanName` 應如上所述加以指定。</span><span class="sxs-lookup"><span data-stu-id="52c33-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="52c33-224">**注意：**每次執行此應用程式時，您需要 toochange hello 值`webAppName`和`appServicePlanName`（或刪除 hello hello Azure 入口網站上的 web 應用程式） 再執行一次 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="52c33-225">否則，執行也會失敗，因為 hello 相同的資源已存在於 Azure。</span><span class="sxs-lookup"><span data-stu-id="52c33-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="52c33-226">定義 hello web 建立方法</span><span class="sxs-lookup"><span data-stu-id="52c33-226">Define hello web creation method</span></span>
<span data-ttu-id="52c33-227">接下來，定義方法 toocreate hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="52c33-228">這個方法， `createWebApp`，指定 hello web 應用程式與 hello 網路空間 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="52c33-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="52c33-229">它也會建立並設定 hello App Service Web 應用程式管理用戶端，定義 hello [WebSiteManagementClient] [ WebSiteManagementClient]物件。</span><span class="sxs-lookup"><span data-stu-id="52c33-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="52c33-230">hello 管理用戶端就是索引鍵 toocreating Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="52c33-231">它提供可讓應用程式 toomanage 藉由呼叫 hello 服務管理 API 的 web 應用程式 （如建立、 更新和刪除，請執行作業） 的 RESTful web 服務。</span><span class="sxs-lookup"><span data-stu-id="52c33-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="52c33-232">hello 程式碼將輸出指出成功或失敗，hello 回應 hello HTTP 狀態，而且如果成功的話，會輸出 hello hello 建立 web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="52c33-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="52c33-233">定義 hello main （） 方法</span><span class="sxs-lookup"><span data-stu-id="52c33-233">Define hello main() method</span></span>
<span data-ttu-id="52c33-234">提供 hello main （） 方法的程式碼的呼叫 createWebApp() toocreate hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="52c33-235">最後，從 `main` 呼叫 `createWebApp`：</span><span class="sxs-lookup"><span data-stu-id="52c33-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="52c33-236">執行 hello 應用程式，並確認 web 應用程式建立</span><span class="sxs-lookup"><span data-stu-id="52c33-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="52c33-237">tooverify 執行應用程式，按一下**執行 > 執行**。</span><span class="sxs-lookup"><span data-stu-id="52c33-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="52c33-238">Hello 應用程式完成時執行，您應該會看到下列輸出 hello Eclipse 主控台中的 hello:</span><span class="sxs-lookup"><span data-stu-id="52c33-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="52c33-239">登入 hello Azure 傳統入口網站並按一下**Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="52c33-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="52c33-240">hello 新 web 應用程式應該會在幾分鐘內出現 hello Web 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="52c33-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="52c33-241">部署應用程式 toohello Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="52c33-242">您已執行 AzureWebDemo 並建立 hello 新 web 應用程式，登入 hello 傳統入口網站，按一下之後**Web 應用程式**，然後選取**WebDemoWebApp**在 hello **Web 應用程式**清單。</span><span class="sxs-lookup"><span data-stu-id="52c33-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="52c33-243">在 hello web 應用程式的儀表板 頁面上，按一下 **瀏覽**(或按一下 hello URL `webdemowebapp.azurewebsites.net`) toonavigate tooit。</span><span class="sxs-lookup"><span data-stu-id="52c33-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="52c33-244">您會看到空白預留位置 頁面上，因為沒有內容尚未被 toohello 已發行的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="52c33-245">接下來您將建立"Hello World"應用程式，並將它部署 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="52c33-246">建立 JSP Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="52c33-247">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-247">Create hello application</span></span>
<span data-ttu-id="52c33-248">順序 toodemonstrate toodeploy 應用程式 toohello web hello 如何在下列程序為您示範如何 toocreate 簡單"Hello World"Java 應用程式，並將它上傳 toohello App Service Web 應用程式建立您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="52c33-249">按一下 [檔案] > [新增] > [動態 Web 專案]。</span><span class="sxs-lookup"><span data-stu-id="52c33-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="52c33-250">將它命名為 `JSPHello`</span><span class="sxs-lookup"><span data-stu-id="52c33-250">Name it `JSPHello`.</span></span> <span data-ttu-id="52c33-251">您不需要 toochange 在這個對話方塊中的任何其他設定。</span><span class="sxs-lookup"><span data-stu-id="52c33-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="52c33-252">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="52c33-253">在 專案總管 中，展開 hello **JSPHello**專案中，以滑鼠右鍵按一下**WebContent**，然後按一下**新增 > JSP 檔案**。</span><span class="sxs-lookup"><span data-stu-id="52c33-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="52c33-254">在 [hello] 新增 JSP 檔案對話方塊 hello 新檔案名稱中`index.jsp`。</span><span class="sxs-lookup"><span data-stu-id="52c33-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="52c33-255">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-255">Click **Next**.</span></span>
3. <span data-ttu-id="52c33-256">在 hello**選取 JSP 範本**對話方塊中，選取**新增 JSP 檔案 (html)**按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="52c33-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="52c33-257">在 index.jsp 中，加入下列程式碼中 hello hello`<head>`和`<body>`標記區段：</span><span class="sxs-lookup"><span data-stu-id="52c33-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="52c33-258">在本機執行 hello Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="52c33-259">執行此應用程式之前，您需要 tooconfigure 一些屬性。</span><span class="sxs-lookup"><span data-stu-id="52c33-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="52c33-260">以滑鼠右鍵按一下 hello **JSPHello**專案，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="52c33-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="52c33-261">在 hello**屬性**對話方塊： 選取**Java 組建路徑**，選取 hello**順序和匯出**索引標籤上，核取**JRE 系統程式庫**，然後按一下**向上**toomove 它 toohello hello 清單的頂端。</span><span class="sxs-lookup"><span data-stu-id="52c33-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="52c33-262">此外在 hello**屬性**對話方塊： 選取**目標執行階段**按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="52c33-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="52c33-263">在 hello**新的伺服器執行階段環境**對話方塊中，例如伺服器選取**Apache Tomcat v7.0**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="52c33-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="52c33-264">在 hello **Tomcat 伺服器**對話方塊中，設定**名稱**太`Apache Tomcat v7.0`，並設定**Tomcat 安裝目錄**toohello 目錄，您已經安裝 hello 版本您想要 toouse tomcat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="52c33-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="52c33-265">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-265">Click **Finish**.</span></span>
5. <span data-ttu-id="52c33-266">接著您回復 toohello**目標執行階段**頁面 hello**屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="52c33-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="52c33-267">選取 [Apache Tomcat v7.0]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="52c33-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="52c33-268">在 hello Eclipse**執行**功能表上，按一下 **執行**。</span><span class="sxs-lookup"><span data-stu-id="52c33-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="52c33-269">在 hello**執行身分**對話方塊中，選取**在伺服器上執行**。</span><span class="sxs-lookup"><span data-stu-id="52c33-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="52c33-270">在 hello**在伺服器上執行**對話方塊中，選取**Tomcat 伺服器 v7.0**:</span><span class="sxs-lookup"><span data-stu-id="52c33-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="52c33-271">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-271">Click **Finish**.</span></span>
7. <span data-ttu-id="52c33-272">當 hello 應用程式執行，您應該會看見 hello **JSPHello**頁面出現在 Eclipse 中的 localhost 視窗 (`http://localhost:8080/JSPHello/`)、 顯示 hello 下列訊息：</span><span class="sxs-lookup"><span data-stu-id="52c33-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="52c33-273">匯出 WAR hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-273">Export hello application as a WAR</span></span>
<span data-ttu-id="52c33-274">可讓您可以將它部署 toohello web 應用程式，請為網頁封存檔 (WAR) 檔案匯出 hello web 專案檔。</span><span class="sxs-lookup"><span data-stu-id="52c33-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="52c33-275">hello 下列 web 專案檔位於 hello WebContent 資料夾中：</span><span class="sxs-lookup"><span data-stu-id="52c33-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="52c33-276">Hello WebContent 資料夾上按一下滑鼠右鍵，然後選取**匯出**。</span><span class="sxs-lookup"><span data-stu-id="52c33-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="52c33-277">在 hello**匯出選取** 對話方塊中，按一下**Web > WAR**檔案，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="52c33-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="52c33-278">在 [hello**匯出 WAR** ] 對話方塊中，在 hello 目前專案中，選取 hello src 目錄，並納入 hello hello 結尾的 hello WAR 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="52c33-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="52c33-279">例如：</span><span class="sxs-lookup"><span data-stu-id="52c33-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="52c33-280">如需有關部署的 WAR 檔案的詳細資訊，請參閱[新增 App Service Web 應用程式的 Java 應用程式 tooAzure](web-sites-java-add-app.md)。</span><span class="sxs-lookup"><span data-stu-id="52c33-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="52c33-281">部署的 hello Hello World 應用程式使用 FTP</span><span class="sxs-lookup"><span data-stu-id="52c33-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="52c33-282">選取第三方 FTP 用戶端 toopublish hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="52c33-283">此程序描述兩個選項： hello Kudu 主控台內建在 Azure。和 FileZilla，方便、 圖形化使用者介面的常用工具。</span><span class="sxs-lookup"><span data-stu-id="52c33-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="52c33-284">**注意：** hello Azure Toolkit for Eclipse 支援部署 toostorage 帳戶和雲端服務，但目前不支援部署 tooweb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="52c33-285">您可以部署 toostorage 帳戶和雲端服務中所述，使用 Azure 部署專案[在 Eclipse 中建立 Azure Hello World 應用程式](http://msdn.microsoft.com/library/azure/hh690944.aspx)，但不適用於 tooweb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="52c33-286">使用其他方法，例如 FTP 或 GitHub tootransfer 檔案 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="52c33-287">**注意：**我們不建議使用 FTP，從 hello Windows 命令提示字元 （hello 命令列 FTP.EXE 公用程式隨附於 Windows）。</span><span class="sxs-lookup"><span data-stu-id="52c33-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="52c33-288">使用作用中的 FTP，例如 FTP.EXE，FTP 用戶端通常會將 toowork 容錯移轉的防火牆。</span><span class="sxs-lookup"><span data-stu-id="52c33-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="52c33-289">作用中 FTP 指定以 LAN 為基礎的內部位址，toowhich FTP 伺服器可能會失敗 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="52c33-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="52c33-290">如需有關部署 tooan App Service web 應用程式使用 FTP 的詳細資訊，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="52c33-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="52c33-291">使用 FTP 公用程式部署</span><span class="sxs-lookup"><span data-stu-id="52c33-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="52c33-292">[設定部署認證] 來設定</span><span class="sxs-lookup"><span data-stu-id="52c33-292">Set up deployment credentials</span></span>
<span data-ttu-id="52c33-293">請確定您已執行 hello **AzureWebDemo**應用程式 toocreate web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="52c33-294">傳輸檔案 toothis 位置。</span><span class="sxs-lookup"><span data-stu-id="52c33-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="52c33-295">登入 hello 傳統入口網站並按一下**Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="52c33-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="52c33-296">請確定**WebDemoWebApp**會出現在 hello web 應用程式清單，並確定它正在執行。</span><span class="sxs-lookup"><span data-stu-id="52c33-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="52c33-297">按一下**WebDemoWebApp** tooopen 其**儀表板**頁面。</span><span class="sxs-lookup"><span data-stu-id="52c33-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="52c33-298">在 hello**儀表板**頁面的 **快速概覽**，按一下 **設定部署認證**(如果您已經有部署認證，這樣會讀取**重設部署認證**)。</span><span class="sxs-lookup"><span data-stu-id="52c33-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="52c33-299">部署認證與 Microsoft 帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="52c33-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="52c33-300">您需要 toospecify 使用者名稱和密碼，您可以使用 toodeploy 使用 Git 和 FTP。</span><span class="sxs-lookup"><span data-stu-id="52c33-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="52c33-301">您可以使用這些認證 toodeploy tooany web 應用程式中所有的 Azure 訂用帳戶與您的 Microsoft 帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="52c33-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="52c33-302">提供 Git 和 FTP 的部署認證 hello 對話方塊中，以及記錄 hello 使用者名稱和密碼，供日後使用。</span><span class="sxs-lookup"><span data-stu-id="52c33-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="52c33-303">取得 FTP 連線資訊</span><span class="sxs-lookup"><span data-stu-id="52c33-303">Get FTP connection information</span></span>
<span data-ttu-id="52c33-304">toouse FTP toodeploy 應用程式檔案 toohello 新建立的 web 應用程式，您需要 tooobtain 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="52c33-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="52c33-305">有兩種方式 tooobtain 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="52c33-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="52c33-306">一種方式是 toovisit hello web 應用程式的**儀表板**頁面; hello 另一種方式是 toodownload hello web 應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="52c33-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="52c33-307">hello 發行設定檔是 XML 檔案，提供您的 web 應用程式在 Azure App Service 中的資訊，例如 FTP 主機名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="52c33-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="52c33-308">您可以使用此使用者名稱和密碼 toodeploy tooany web 應用程式不是只有此一個 hello Azure 帳戶相關聯的所有訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="52c33-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="52c33-309">tooobtain FTP 連線資訊從 hello web 應用程式的刀鋒視窗中 hello [Azure 入口網站][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="52c33-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="52c33-310">在下**Essentials**，尋找並複製 hello **FTP 主機名稱**。</span><span class="sxs-lookup"><span data-stu-id="52c33-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="52c33-311">這是相似的 URI 太`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="52c33-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="52c33-312">在 [基本功能] 之下，尋找並複製 [FTP/部署使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="52c33-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="52c33-313">這將會有 hello 形式*webappname\deployment-username*; 例如`WebDemoWebApp\deployer77`。</span><span class="sxs-lookup"><span data-stu-id="52c33-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="52c33-314">從 hello tooobtain FTP 連線資訊發行設定檔：</span><span class="sxs-lookup"><span data-stu-id="52c33-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="52c33-315">在 hello web 應用程式的刀鋒視窗中，按一下 **取得發行設定檔**。</span><span class="sxs-lookup"><span data-stu-id="52c33-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="52c33-316">這會下載.publishsettings 檔案 tooyour 本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="52c33-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="52c33-317">在 XML 編輯器或文字編輯器中開啟 hello.publishsettings 檔案，並尋找 hello`<publishProfile>`項目包含`publishMethod="FTP"`。</span><span class="sxs-lookup"><span data-stu-id="52c33-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="52c33-318">它看起來應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="52c33-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="52c33-319">請注意該 hello web 應用程式的`publishProfile`設定對應 toohello FileZilla 網站管理員設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="52c33-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="52c33-320">`publishUrl`hello 與相同**FTP 主機名稱**，hello 您的設定值**主機**。</span><span class="sxs-lookup"><span data-stu-id="52c33-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="52c33-321">`publishMethod="FTP"`表示您設定**通訊協定**太**FTP-檔案傳輸通訊協定**，和**加密**太**使用一般 FTP**。</span><span class="sxs-lookup"><span data-stu-id="52c33-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="52c33-322">`userName`和`userPWD`是索引鍵的 hello 實際您指定當您重設 hello 的部署認證的使用者名稱和密碼值。</span><span class="sxs-lookup"><span data-stu-id="52c33-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="52c33-323">`userName`hello 與相同**部署 / FTP 使用者**。</span><span class="sxs-lookup"><span data-stu-id="52c33-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="52c33-324">它們會太對應**使用者**和**密碼**FileZilla 中。</span><span class="sxs-lookup"><span data-stu-id="52c33-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="52c33-325">`ftpPassiveMode="True"`表示該 hello FTP 站台使用被動 FTP 傳送;選取**被動**上 hello**傳輸設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52c33-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="52c33-326">設定 hello Web 應用程式 toohost Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="52c33-327">發佈 hello 應用程式之前，您需要 toochange 一些組態設定，讓 hello web 應用程式可以裝載 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="52c33-328">在 hello 傳統入口網站移 toohello web 應用程式的**儀表板**頁面上，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="52c33-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="52c33-329">在 hello**設定**頁面上，指定下列設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="52c33-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="52c33-330">在**Java 版本**hello 預設值是**關閉**; 選取 hello Java 版本應用程式的目標，例如 1.7.0_51。</span><span class="sxs-lookup"><span data-stu-id="52c33-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="52c33-331">執行這項操作之後，也請確定**網頁容器**設定 tooa Tomcat 伺服器版本。</span><span class="sxs-lookup"><span data-stu-id="52c33-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="52c33-332">在**預設文件**、 新增 index.jsp 和 toohello hello 清單頂端上移。</span><span class="sxs-lookup"><span data-stu-id="52c33-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="52c33-333">（hello 預設 web 應用程式的檔案是 hostingstart.html）。</span><span class="sxs-lookup"><span data-stu-id="52c33-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="52c33-334">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="52c33-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="52c33-335">使用 Kudu 發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-335">Publish your application using Kudu</span></span>
<span data-ttu-id="52c33-336">其中一種方式 toopublish hello 應用程式是 toouse hello Kudu 偵錯主控台內建在 Azure。</span><span class="sxs-lookup"><span data-stu-id="52c33-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="52c33-337">Kudu 為已知 toobe 穩定且一致的應用程式服務 Web 應用程式和 Tomcat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="52c33-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="52c33-338">您可以存取 hello web 應用程式的 hello 主控台瀏覽下列表單的 hello tooa URL:</span><span class="sxs-lookup"><span data-stu-id="52c33-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="52c33-339">在此程序 hello Kudu 主控台位於下列 URL; hello瀏覽 toothis 位置：</span><span class="sxs-lookup"><span data-stu-id="52c33-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="52c33-340">從 hello 上方功能表中，選取**偵錯主控台 > CMD**。</span><span class="sxs-lookup"><span data-stu-id="52c33-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="52c33-341">在 hello 主控台命令列中，瀏覽過`/site/wwwroot`(或按一下`site`，然後`wwwroot`hello 頁面頂端的 hello hello 目錄檢視中):</span><span class="sxs-lookup"><span data-stu-id="52c33-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="52c33-342">在您指定 [ **Java 版本**] 後，Tomcat 伺服器應建立 webapps 目錄。</span><span class="sxs-lookup"><span data-stu-id="52c33-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="52c33-343">在 hello 主控台命令列瀏覽 toohello webapps 目錄：</span><span class="sxs-lookup"><span data-stu-id="52c33-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="52c33-344">拖曳從 JSPHello.war`<project-path>/JSPHello/src/`拖放到 hello Kudu 目錄檢視下`/site/wwwroot/webapps`。</span><span class="sxs-lookup"><span data-stu-id="52c33-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="52c33-345">請勿拖曳 toohello 」 將拖曳到此處 tooupload 和 zip 」 區域中，因為 Tomcat 會將它解壓縮。</span><span class="sxs-lookup"><span data-stu-id="52c33-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="52c33-346">在第一個 JSPHello.war 會出現在 hello 目錄區域本身：</span><span class="sxs-lookup"><span data-stu-id="52c33-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="52c33-347">短時間 （可能少於 5 分鐘） 內 Tomcat 伺服器會將 hello WAR 檔案解壓縮至打開包裝後的 JSPHello 目錄。</span><span class="sxs-lookup"><span data-stu-id="52c33-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="52c33-348">是否已將工具解壓縮並複製那里 index.jsp，按一下 hello 根目錄 toosee。</span><span class="sxs-lookup"><span data-stu-id="52c33-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="52c33-349">如果是這樣，瀏覽後 toohello webapps 目錄 toosee 是否 hello 解壓縮的 JSPHello 在建立目錄。</span><span class="sxs-lookup"><span data-stu-id="52c33-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="52c33-350">如果您未看見這些項目，請稍後並重複。</span><span class="sxs-lookup"><span data-stu-id="52c33-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="52c33-351">使用 FileZilla 發佈您的應用程式 (選用)</span><span class="sxs-lookup"><span data-stu-id="52c33-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="52c33-352">您可以使用 toopublish hello 應用程式的另一個工具是 FileZilla、 受歡迎的第三方 FTP 用戶端，以方便、 圖形化使用者介面。</span><span class="sxs-lookup"><span data-stu-id="52c33-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="52c33-353">如果您還沒有 FileZilla，可以從 [http://filezilla-project.org/](http://filezilla-project.org/) 下載並安裝此工具。</span><span class="sxs-lookup"><span data-stu-id="52c33-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="52c33-354">如需有關使用 hello 用戶端的詳細資訊，請參閱 hello [FileZilla 文件](https://wiki.filezilla-project.org/Documentation)和此部落格文章[FTP 用戶端-第 4 部分： FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx)。</span><span class="sxs-lookup"><span data-stu-id="52c33-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="52c33-355">在 FileZilla 中，按一下 [檔案] > [網站管理員]。</span><span class="sxs-lookup"><span data-stu-id="52c33-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="52c33-356">在 hello**網站管理員** 對話方塊中，按一下 **新站台**。</span><span class="sxs-lookup"><span data-stu-id="52c33-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="52c33-357">新的空白 FTP 站台會出現在**選取項目**提示您 tooprovide 名稱。</span><span class="sxs-lookup"><span data-stu-id="52c33-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="52c33-358">在此程序中，將它命名為 `AzureWebDemo-FTP`</span><span class="sxs-lookup"><span data-stu-id="52c33-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="52c33-359">在 hello**一般**索引標籤上，指定下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="52c33-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="52c33-360">**主機：** Enter hello **FTP 主機名稱**您複製從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="52c33-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="52c33-361">**連接埠：** （保持空白，這是被動傳輸以及 hello 伺服器將會決定 hello 連接埠 toouse。）</span><span class="sxs-lookup"><span data-stu-id="52c33-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="52c33-362">**通訊協定：** (FTP 檔案傳輸通訊協定)</span><span class="sxs-lookup"><span data-stu-id="52c33-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="52c33-363">**加密：** 使用一般 FTP</span><span class="sxs-lookup"><span data-stu-id="52c33-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="52c33-364">**登入類型：** 正常</span><span class="sxs-lookup"><span data-stu-id="52c33-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="52c33-365">**使用者：** Enter hello 部署 / FTP 使用者，您所複製的 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="52c33-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="52c33-366">這是 hello 完整 FTP 使用者名稱，其具有 hello 表單*webappname\username*。</span><span class="sxs-lookup"><span data-stu-id="52c33-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="52c33-367">**密碼：**輸入 hello 密碼，您會指定當您將 hello 的部署認證。</span><span class="sxs-lookup"><span data-stu-id="52c33-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="52c33-368">在 hello**傳輸設定**索引標籤上，選取**被動**。</span><span class="sxs-lookup"><span data-stu-id="52c33-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="52c33-369">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="52c33-369">Click **Connect**.</span></span> <span data-ttu-id="52c33-370">如果成功，FileZilla 的主控台將顯示`Status: Connected`訊息和問題`LIST`命令 toolist hello 目錄內容。</span><span class="sxs-lookup"><span data-stu-id="52c33-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="52c33-371">在 [hello**本機**站台] 面板中，選取 hello 來源目錄中的 hello JSPHello.war 檔案位於; hello 路徑會是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="52c33-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="52c33-372">在 [hello**遠端**站台] 面板中，選取 hello 目的地資料夾。</span><span class="sxs-lookup"><span data-stu-id="52c33-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="52c33-373">您將部署 hello WAR 檔案 toohello `webapps` hello web 應用程式的根目錄下的目錄。</span><span class="sxs-lookup"><span data-stu-id="52c33-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="52c33-374">瀏覽過`/site/wwwroot`，以滑鼠右鍵按一下`wwwroot`，然後選取**建立目錄**。</span><span class="sxs-lookup"><span data-stu-id="52c33-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="52c33-375">名稱 hello 目錄`webapps`並輸入該目錄。</span><span class="sxs-lookup"><span data-stu-id="52c33-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="52c33-376">太傳輸 JSPHello.war`/site/wwwroot/webapps`。</span><span class="sxs-lookup"><span data-stu-id="52c33-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="52c33-377">選取在 hello JSPHello.war**本機**檔案清單，以滑鼠右鍵按一下它，然後選取**上傳**。</span><span class="sxs-lookup"><span data-stu-id="52c33-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="52c33-378">您應看見該檔案出現在 `/site/wwwroot/webapps`中。</span><span class="sxs-lookup"><span data-stu-id="52c33-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="52c33-379">Tomcat 伺服器複製 JSPHello.war toohello webapps 目錄之後，將會自動解除封裝 （解壓縮） hello hello WAR 檔案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="52c33-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="52c33-380">雖然 Tomcat 伺服器一開始會解壓縮幾乎會立即，它可能需要很長時間 hello FTP 用戶端中的 hello 檔案 tooappear （可能是小時）。</span><span class="sxs-lookup"><span data-stu-id="52c33-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="52c33-381">在 hello Web 應用程式上執行 hello Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="52c33-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="52c33-382">您已經上傳 hello WAR 檔案，並確認已建立解壓縮 Tomcat 伺服器之後`JSPHello`目錄中，瀏覽過`http://webdemowebapp.azurewebsites.net/JSPHello`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="52c33-383">**注意：**如果您按一下**瀏覽**從 hello 傳統入口網站，您可能會收到 hello 預設網頁，指出 「 此基礎的 Java web 應用程式已成功建立。 」</span><span class="sxs-lookup"><span data-stu-id="52c33-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="52c33-384">順序 tooview hello 而不是 hello 預設網頁的應用程式輸出中，您可能有 toorefresh hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="52c33-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="52c33-385">Hello 應用程式執行時，您應該會看到網頁以 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="52c33-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="52c33-386">清除 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="52c33-386">Clean up Azure resources</span></span>
<span data-ttu-id="52c33-387">此程序會建立 App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52c33-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="52c33-388">您還是必須支付 hello 資源存在於。</span><span class="sxs-lookup"><span data-stu-id="52c33-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="52c33-389">除非您計劃 toocontinue 使用 hello web 應用程式執行測試或開發，您應該考慮停止或刪除它。</span><span class="sxs-lookup"><span data-stu-id="52c33-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="52c33-390">已停止的 Web 應用程式仍將帶來少許費用，但您可以隨時予以重新啟動。</span><span class="sxs-lookup"><span data-stu-id="52c33-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="52c33-391">刪除 web 應用程式會清除您已上傳 tooit 的所有資料。</span><span class="sxs-lookup"><span data-stu-id="52c33-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
