---
title: "使用 Azure SDK for Java 在 Azure App Service 中建立 Web 應用程式"
description: "了解如何使用 Azure SDK for Java 在 Azure App Service 中以程式設計方式建立 Web 應用程式。"
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
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="5bf29-103">使用 Azure SDK for Java 在 Azure App Service 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="5bf29-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5bf29-104">Overview</span></span>
<span data-ttu-id="5bf29-105">本逐步解說說明如何建立 Azure SDK for Java 應用程式，以便在 [Azure App Service][Azure App Service] 中建立 Web 應用程式，並將應用程式部署到其上。</span><span class="sxs-lookup"><span data-stu-id="5bf29-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="5bf29-106">其中包括兩個部分：</span><span class="sxs-lookup"><span data-stu-id="5bf29-106">It consists of two parts:</span></span>

* <span data-ttu-id="5bf29-107">第 1 部分示範如何建立 Java 應用程式，以便建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="5bf29-108">第 2 部分示範如何建立簡單 JSP "Hello World" 應用程式，然後使用 FTP 用戶端將程式碼部署至 App Service。</span><span class="sxs-lookup"><span data-stu-id="5bf29-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bf29-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="5bf29-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="5bf29-110">軟體安裝</span><span class="sxs-lookup"><span data-stu-id="5bf29-110">Software Installations</span></span>
<span data-ttu-id="5bf29-111">本文中的 AzureWebDemo 應用程式程式碼是使用 Azure Java SDK 0.7.0 撰寫，您可使用 [Web Platform Installer][Web Platform Installer] (WebPI) 進行安裝。</span><span class="sxs-lookup"><span data-stu-id="5bf29-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="5bf29-112">此外，務必使用最新版的 [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="5bf29-113">安裝 SDK 之後，在 **Maven 儲存機制**中執行**更新索引**以在 Eclipse 專案中更新相依性，然後在 [相依性] 視窗中重新新增各封裝的最新版本。</span><span class="sxs-lookup"><span data-stu-id="5bf29-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="5bf29-114">按一下 [說明] > [安裝詳細資料]，可以驗證 Eclipse 中安裝的軟體版本；您至少要有下列版本：</span><span class="sxs-lookup"><span data-stu-id="5bf29-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="5bf29-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="5bf29-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="5bf29-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="5bf29-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="5bf29-117">在 Azure 中建立和設定雲端資源</span><span class="sxs-lookup"><span data-stu-id="5bf29-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="5bf29-118">開始此程序前，Azure 上必須有使用中 Azure 訂用帳戶並設定預設 Active Directory (AD)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="5bf29-119">在 Azure 中建立 Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="5bf29-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="5bf29-120">如果您的 Azure 訂用帳戶上還沒有 Active Directory (AD)，請使用您的 Microsoft 帳戶登入 [Azure 傳統入口網站][Azure classic portal]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="5bf29-121">如果您有多個訂用帳戶，請按一下 [ **訂用帳戶** ] 並針對您要用於此專案的訂用帳戶選取預設目錄。</span><span class="sxs-lookup"><span data-stu-id="5bf29-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="5bf29-122">接著按一下 [ **套用** ] 切換至該訂用帳戶檢視。</span><span class="sxs-lookup"><span data-stu-id="5bf29-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="5bf29-123">從左側功能表中選取 [ **Active Directory** ]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="5bf29-124">按一下 [新增] > [目錄] > [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="5bf29-125">在 [新增目錄] 中，選取 [建立新目錄]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="5bf29-126">在 [ **名稱**] 中，輸入目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="5bf29-127">在 [網域] 中，輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="5bf29-128">這是您的目錄預設包含的基本網域名稱；其格式為 `<domain_name>.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="5bf29-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="5bf29-129">您可以根據此目錄名稱或您擁有的其他網域名稱予以命名。</span><span class="sxs-lookup"><span data-stu-id="5bf29-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="5bf29-130">之後，您可以新增貴組織已使用的其他網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="5bf29-131">在 [ **國家或地區**] 中，選取您的地區設定。</span><span class="sxs-lookup"><span data-stu-id="5bf29-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="5bf29-132">如需 AD 詳細資訊，請參閱 [什麼是 Azure Active Directory][What is an Azure AD directory]？</span><span class="sxs-lookup"><span data-stu-id="5bf29-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="5bf29-133">建立 Azure 的管理憑證</span><span class="sxs-lookup"><span data-stu-id="5bf29-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="5bf29-134">Azure SDK for Java 使用管理憑證來向 Azure 訂用帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="5bf29-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="5bf29-135">這些是用來驗證下列用戶端應用程式的 X.509 v3 憑證：利用服務管理 API 代表訂用帳戶擁有者管理訂用資源的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="5bf29-136">此程序中的程式碼使用自我簽署的憑證來向 Azure 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="5bf29-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="5bf29-137">在此程序中，您需要事先建立憑證並將其上傳至 [Azure 傳統入口網站][Azure classic portal]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="5bf29-138">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5bf29-138">This involves the following steps:</span></span>

* <span data-ttu-id="5bf29-139">產生代表您的用戶端憑證的 PFX 檔案，並將其儲存於本機。</span><span class="sxs-lookup"><span data-stu-id="5bf29-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="5bf29-140">從 PFX 檔案產生管理憑證 (CER 檔案)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="5bf29-141">將 CER 檔案上傳至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf29-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="5bf29-142">將 PFX 檔案轉換為 JKS，因為 Java 使用該格式來驗證憑證的使用。</span><span class="sxs-lookup"><span data-stu-id="5bf29-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="5bf29-143">撰寫應用程式的驗證碼，以便參照本機 JKS 檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf29-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="5bf29-144">當您完成這個程序時，CER 憑證會位於 Azure 訂用帳戶，而 JKS 憑證會位於本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="5bf29-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="5bf29-145">如需管理憑證的詳細資訊，請參閱 [建立和上傳 Azure 的管理憑證][Create and Upload a Management Certificate for Azure]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="5bf29-146">建立憑證</span><span class="sxs-lookup"><span data-stu-id="5bf29-146">Create a certificate</span></span>
<span data-ttu-id="5bf29-147">若要建立自己的自我簽署憑證，請開啟作業系統上的命令主控台並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="5bf29-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="5bf29-148">**注意：** 您用來執行此命令的電腦必須已安裝 JDK。</span><span class="sxs-lookup"><span data-stu-id="5bf29-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="5bf29-149">此外，keytool 的路徑取決於您安裝 JDK 的位置。</span><span class="sxs-lookup"><span data-stu-id="5bf29-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="5bf29-150">如需詳細資訊，請參閱 Java 線上文件中的 [金鑰和憑證管理工具 (keytool)][Key and Certificate Management Tool (keytool)]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="5bf29-151">若要建立 .pfx 檔案：</span><span class="sxs-lookup"><span data-stu-id="5bf29-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="5bf29-152">若要建立 .cer 檔案：</span><span class="sxs-lookup"><span data-stu-id="5bf29-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="5bf29-153">其中：</span><span class="sxs-lookup"><span data-stu-id="5bf29-153">where:</span></span>

* <span data-ttu-id="5bf29-154">`<java-install-dir>` 是您安裝 Java 的目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="5bf29-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="5bf29-155">`<keystore-id>` 是keystore 項目識別碼 (例如 `AzureRemoteAccess`)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="5bf29-156">`<cert-store-dir>` 是您儲存憑證的目錄路徑 (例如 `C:/Certificates`)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="5bf29-157">`<cert-file-name>` 是憑證檔案的名稱 (例如 `AzureWebDemoCert`)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="5bf29-158">`<password>` 是您選擇用來保護憑證的密碼；長度必須至少 6 個字元。</span><span class="sxs-lookup"><span data-stu-id="5bf29-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="5bf29-159">您可以不輸入密碼，但不建議這麼做。</span><span class="sxs-lookup"><span data-stu-id="5bf29-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="5bf29-160">`<dname>` 是要與別名相關聯的 X.500 辨別名稱，並作為自我簽署憑證中的簽發者和主旨欄位。</span><span class="sxs-lookup"><span data-stu-id="5bf29-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="5bf29-161">如需詳細資訊，請參閱 [建立和上傳 Azure 的管理憑證][Create and Upload a Management Certificate for Azure]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="5bf29-162">上傳憑證</span><span class="sxs-lookup"><span data-stu-id="5bf29-162">Upload the certificate</span></span>
<span data-ttu-id="5bf29-163">若要將自我簽署憑證上傳至 Azure，請移至傳統入口網站中的 [設定] 頁面，然後按一下 [管理憑證] 索引標籤。按一下頁面底部的 [ **上傳** ] 並導覽至您建立之 CER 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="5bf29-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="5bf29-164">將 PFX 檔案轉換為 JKS</span><span class="sxs-lookup"><span data-stu-id="5bf29-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="5bf29-165">在 Windows 命令提示字元 (以系統管理員身分執行) 中，將目錄變更至包含憑證的目錄並執行下列命令，其中 `<java-install-dir>` 是電腦上安裝 Java 的目錄：</span><span class="sxs-lookup"><span data-stu-id="5bf29-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="5bf29-166">出現提示後，請輸入目的地 keystore 密碼；這會是 JKS 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="5bf29-167">出現提示後，請輸入來源 keystore 密碼；這是您為 PFX 檔案指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="5bf29-168">兩組密碼不必相同。</span><span class="sxs-lookup"><span data-stu-id="5bf29-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="5bf29-169">您可以不輸入密碼，但不建議這麼做。</span><span class="sxs-lookup"><span data-stu-id="5bf29-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="5bf29-170">建置 Web 應用程式建立應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="5bf29-171">建立 Eclipse 工作區和 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="5bf29-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="5bf29-172">在這一節中，您可為 Web 應用程式建立應用程式 (名稱為 AzureWebDemo) 建立工作區和 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="5bf29-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="5bf29-173">建立新的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="5bf29-173">Create a new Maven project.</span></span> <span data-ttu-id="5bf29-174">按一下 [檔案] > [新增] > [Maven 專案]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="5bf29-175">在 [新增 Maven 專案] 中，選取 [建立簡單專案] 和 [使用預設工作區位置]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="5bf29-176">在 [ **新增 Maven 專案**] 的第二頁上，指定下列各項：</span><span class="sxs-lookup"><span data-stu-id="5bf29-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="5bf29-177">群組識別碼： `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="5bf29-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="5bf29-178">成品識別碼：AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="5bf29-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="5bf29-179">版本：0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="5bf29-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="5bf29-180">封裝：jar</span><span class="sxs-lookup"><span data-stu-id="5bf29-180">Packaging: jar</span></span>
   * <span data-ttu-id="5bf29-181">名稱：AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="5bf29-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="5bf29-182">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-182">Click **Finish**.</span></span>
3. <span data-ttu-id="5bf29-183">在 [專案總管] 中開啟新專案的 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf29-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="5bf29-184">選取 [ **相依性** ] 索引標籤。由於這是新專案，所以尚未列出任何封裝。</span><span class="sxs-lookup"><span data-stu-id="5bf29-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="5bf29-185">開啟 [Maven 儲存機制] 檢視。</span><span class="sxs-lookup"><span data-stu-id="5bf29-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="5bf29-186">按一下 [視窗] > [顯示檢視] > [其他] > [Maven] > [Maven 儲存機制]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="5bf29-187">[ **Maven 儲存機制** ] 檢視將顯示在 IDE 底部。</span><span class="sxs-lookup"><span data-stu-id="5bf29-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="5bf29-188">開啟 [全域儲存機制]，以滑鼠右鍵按一下 **central** 儲存機制，然後選取 [重建索引]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="5bf29-189">視您的連線速度而定，此步驟可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="5bf29-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="5bf29-190">重建索引時，您應可在 **central** Maven 儲存機制中看見 Microsoft Azure 封裝。</span><span class="sxs-lookup"><span data-stu-id="5bf29-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="5bf29-191">在 [相依性] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="5bf29-192">在 [輸入群組識別碼...] 中輸入 `azure-management`。</span><span class="sxs-lookup"><span data-stu-id="5bf29-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="5bf29-193">選取用於基礎管理和 App Service Web Apps 管理的封裝：</span><span class="sxs-lookup"><span data-stu-id="5bf29-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="5bf29-194">**注意：** 如果在新版本發行後更新相依性，則需在這份清單中重新新增每個相依性。</span><span class="sxs-lookup"><span data-stu-id="5bf29-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="5bf29-195">按一下 [新增] 並選取每個相依性後，每個相依性會在 [相依性] 清單中顯示新的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="5bf29-196">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-196">Click **OK**.</span></span> <span data-ttu-id="5bf29-197">Azure 封裝會接著顯示在 [相依性] 清單中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="5bf29-198">呼叫 Azure SDK 以便撰寫 Java 程式碼來建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="5bf29-199">接著，撰寫可在 Azure SDK for Java 中呼叫 API 的程式碼，以便建立 App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="5bf29-200">建立 Java 類別以包含主要進入點程式碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="5bf29-201">在 [專案總管] 中，以滑鼠右鍵按一下專案節點並選取 [新增] > [類別]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="5bf29-202">在 [新增 Java 類別] 中，將類別命名為 `WebCreator` 並勾選 [public static void main] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5bf29-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="5bf29-203">選取項目應如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bf29-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="5bf29-204">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-204">Click **Finish**.</span></span> <span data-ttu-id="5bf29-205">WebCreator.java 檔案會顯示在 [專案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="5bf29-206">呼叫 Azure API 以建立 App Service Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="5bf29-207">新增必要匯入</span><span class="sxs-lookup"><span data-stu-id="5bf29-207">Add necessary imports</span></span>
<span data-ttu-id="5bf29-208">在 WebCreator.java 中，新增下列匯入；這些匯入可供存取類別管理資料館中的類別，以便使用 Azure API：</span><span class="sxs-lookup"><span data-stu-id="5bf29-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="5bf29-209">定義主要進入點類別</span><span class="sxs-lookup"><span data-stu-id="5bf29-209">Define the main entry point class</span></span>
<span data-ttu-id="5bf29-210">因為 AzureWebDemo 應用程式的目的是要建立 App Service Web 應用程式，所以請將此應用程式的主要類別命名為 `WebAppCreator`</span><span class="sxs-lookup"><span data-stu-id="5bf29-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="5bf29-211">此類別提供主要進入點程式碼，以便呼叫 Azure 服務管理 API 來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="5bf29-212">新增 Web 應用程式和網路空間的下列參數定義。</span><span class="sxs-lookup"><span data-stu-id="5bf29-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="5bf29-213">您需要提供自己的 Azure 訂用帳戶識別碼和憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="5bf29-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="5bf29-214">其中：</span><span class="sxs-lookup"><span data-stu-id="5bf29-214">where:</span></span>

* <span data-ttu-id="5bf29-215">`<subscription-id>` 是您要建立資源的 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="5bf29-216">`<certificate-store-path>` 是本機憑證存放區目錄中 JKS 檔案的路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="5bf29-217">例如，`C:/Certificates/CertificateName.jks` 適用於 Linux，而 `C:\Certificates\CertificateName.jks` 適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="5bf29-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="5bf29-218">`<certificate-password>` 是在建立 JKS 憑證時指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="5bf29-219">`webAppName` 可以您選擇的任何名稱；此程序使用 `WebDemoWebApp` 這個名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="5bf29-220">完整網域名稱為附加 `domainName` 的 `webAppName`，所以此例中的完整網域為 `webdemowebapp.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="5bf29-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="5bf29-221">`domainName` 應如上所述加以指定。</span><span class="sxs-lookup"><span data-stu-id="5bf29-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="5bf29-222">`webSpaceName` 應是在 [WebSpaceNames][WebSpaceNames] 類別中指定的其中一個值。</span><span class="sxs-lookup"><span data-stu-id="5bf29-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="5bf29-223">`appServicePlanName` 應如上所述加以指定。</span><span class="sxs-lookup"><span data-stu-id="5bf29-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="5bf29-224">**注意：**每次執行此應用程式時，您必須先變更 `webAppName` 和 `appServicePlanName` 的值 (或在 Azure 入口網站上刪除 Web 應用程式)，才能再次執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="5bf29-225">否則，執行作業會因為 Azure 上已存在相同資源而失敗。</span><span class="sxs-lookup"><span data-stu-id="5bf29-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="5bf29-226">定義 Web 建立方法</span><span class="sxs-lookup"><span data-stu-id="5bf29-226">Define the web creation method</span></span>
<span data-ttu-id="5bf29-227">接著，定義用以建立 Web 應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="5bf29-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="5bf29-228">此方法 ( `createWebApp`) 會指定 Web 應用程式和網路空間的參數。</span><span class="sxs-lookup"><span data-stu-id="5bf29-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="5bf29-229">也會建立及設定 App Service Web Apps 管理用戶端，而該管理用戶端是由 [WebSiteManagementClient][WebSiteManagementClient] 物件定義。</span><span class="sxs-lookup"><span data-stu-id="5bf29-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="5bf29-230">此管理用戶端是建立 Web Apps 的關鍵。</span><span class="sxs-lookup"><span data-stu-id="5bf29-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="5bf29-231">它可提供符合 REST 限制的 Web 服務，以便應用程式藉由呼叫服務管理 API 來管理 Web 應用程式 (執行作業，例如建立、更新和刪除)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
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
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="5bf29-232">此程式碼將會輸出回應的 HTTP 狀態 (表示成功或失敗)，如果成功，將會輸出所建立 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="5bf29-233">定義 main() 方法</span><span class="sxs-lookup"><span data-stu-id="5bf29-233">Define the main() method</span></span>
<span data-ttu-id="5bf29-234">提供 main() 方法程式碼，以便呼叫 createWebApp() 來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="5bf29-235">最後，從 `main` 呼叫 `createWebApp`：</span><span class="sxs-lookup"><span data-stu-id="5bf29-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="5bf29-236">執行應用程式並驗證 Web 應用程式建立</span><span class="sxs-lookup"><span data-stu-id="5bf29-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="5bf29-237">若要確認您的應用程式可執行，請按一下 [執行] > [執行]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="5bf29-238">當應用程式完成執行時，您應在 Eclipse 主控台中看見下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5bf29-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="5bf29-239">登入 Azure 傳統入口網站並按一下 [ **Web Apps**]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="5bf29-240">幾分鐘內，新的 Web 應用程式應顯示在 Web Apps 清單中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="5bf29-241">將應用程式部署至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="5bf29-242">執行 AzureWebDemo 並建立新的 Web 應用程式之後，登入傳統入口網站，按一下 **Web Apps**，然後選取 [ **WebDemoWebApp** in the **Web Apps** ] 清單中顯示新的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="5bf29-243">在 Web 應用程式的儀表板頁面中，按一下 [瀏覽] \(或按一下 URL：`webdemowebapp.azurewebsites.net`) 以導覽至該 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="5bf29-244">您將會看見空白預留位置頁面，因為尚未將任何內容發佈至此 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="5bf29-245">接下來，您會建立 "Hello World" 應用程式並將其部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="5bf29-246">建立 JSP Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="5bf29-247">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-247">Create the application</span></span>
<span data-ttu-id="5bf29-248">為了示範如何將應用程式部署到 Web，下列程序顯示如何建立簡單的 "Hello World" Java 應用程式並將它更新至您的應用程式所建立的 App Service Web App。</span><span class="sxs-lookup"><span data-stu-id="5bf29-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="5bf29-249">按一下 [檔案] > [新增] > [動態 Web 專案]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="5bf29-250">將它命名為 `JSPHello`</span><span class="sxs-lookup"><span data-stu-id="5bf29-250">Name it `JSPHello`.</span></span> <span data-ttu-id="5bf29-251">您不需要變更此對話方塊中的任何其他設定。</span><span class="sxs-lookup"><span data-stu-id="5bf29-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="5bf29-252">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="5bf29-253">在 [專案總管] 中，展開 **JSPHello** 專案，以滑鼠右鍵按一下 **WebContent**，然後按一下 [新增] > [JSP 檔案]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="5bf29-254">在 [新增 JSP 檔案] 對話方塊中，將新檔案命名為 `index.jsp`。</span><span class="sxs-lookup"><span data-stu-id="5bf29-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="5bf29-255">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-255">Click **Next**.</span></span>
3. <span data-ttu-id="5bf29-256">在 [Select JSP Template] 對話方塊中，選取 [New JSP File (html)]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="5bf29-257">在 index.jsp 的 `<head>` 和 `<body>` 標記區段中新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf29-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="5bf29-258">在 localhost 中執行 Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="5bf29-259">執行此應用程式前，您需設定一些屬性。</span><span class="sxs-lookup"><span data-stu-id="5bf29-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="5bf29-260">在 **JSPHello** 專案上按一下滑鼠右鍵，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="5bf29-261">在 [屬性] 對話方塊中：選取 [Java 組建路徑]、選取 [順序和匯出] 索引標籤、核取 [JRE 系統程式庫]，然後按一下 [向上] 將它移至清單最上方。</span><span class="sxs-lookup"><span data-stu-id="5bf29-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="5bf29-262">此外，在 [屬性] 對話方塊中：選取 [目標執行階段] 並按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="5bf29-263">在 [新增伺服器執行階段環境] 對話方塊中，選取伺服器 (例如 **Apache Tomcat v7.0**) 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="5bf29-264">在 [Tomcat 伺服器] 對話方塊中，將 [名稱] 設定為 `Apache Tomcat v7.0`，然後將 [Tomcat 安裝目錄] 設定為您安裝 Tomcat 伺服器的目錄。</span><span class="sxs-lookup"><span data-stu-id="5bf29-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="5bf29-265">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-265">Click **Finish**.</span></span>
5. <span data-ttu-id="5bf29-266">然後，返回 [屬性] 對話方塊的 [目標執行階段] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5bf29-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="5bf29-267">選取 [Apache Tomcat v7.0]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="5bf29-268">在 Eclipse 的 [執行] 功能表中，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="5bf29-269">在 [執行身分] 對話方塊中，選取 [在伺服器上執行]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="5bf29-270">在 [在伺服器上執行] 對話方塊中，選取 [Tomcat v7.0 Server]：</span><span class="sxs-lookup"><span data-stu-id="5bf29-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="5bf29-271">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-271">Click **Finish**.</span></span>
7. <span data-ttu-id="5bf29-272">當應用程式執行時，您應看見 [JSPHello] 頁面顯示於 Eclipse 的 localhost 視窗 (`http://localhost:8080/JSPHello/`)，顯示下列訊息：</span><span class="sxs-lookup"><span data-stu-id="5bf29-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="5bf29-273">將應用程式匯出為 WAR</span><span class="sxs-lookup"><span data-stu-id="5bf29-273">Export the application as a WAR</span></span>
<span data-ttu-id="5bf29-274">將 Web 專案檔案匯出為網頁封存 (WAR) 檔案，以便將它部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="5bf29-275">下列 Web 專案檔案位於 WebContent 資料夾中：</span><span class="sxs-lookup"><span data-stu-id="5bf29-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="5bf29-276">以滑鼠右鍵按一下 WebContent 資料夾並選取 [ **匯出**]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="5bf29-277">在 [匯出選取] 對話方塊中，按一下 [Web] > [WAR] 檔案，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="5bf29-278">在 [ **WAR 匯出** ] 對話方塊中，選取目前專案中的 src 目錄，然後在結尾包含 WAR 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="5bf29-279">例如：</span><span class="sxs-lookup"><span data-stu-id="5bf29-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="5bf29-280">如需部署 WAR 檔案的詳細資訊，請參閱 [將 Java 應用程式新增至 Azure App Service Web Apps](web-sites-java-add-app.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="5bf29-281">使用 FTP 部署 Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="5bf29-282">選取協力廠商 FTP 用戶端，以發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="5bf29-283">此程序說明兩個選項：Azure 內建的 Kudu 主控台；以及 FileZilla (具有便利圖形 UI 的熱門工具)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="5bf29-284">**注意：** Azure Toolkit for Eclipse 支援部署至儲存體帳戶和雲端服務，但目前不支援部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="5bf29-285">如 [在 Eclipse 中建立 Azure 的 Hello World 應用程式](http://msdn.microsoft.com/library/azure/hh690944.aspx)所述，您可以使用 Azure 部署專案部署至儲存體帳戶和雲端服務，但不能部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="5bf29-286">使用 FTP 或 GitHub 等方法將檔案移轉至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="5bf29-287">**注意：** 不建議從 Windows 命令提示字元 (Windows 隨附的命令列 FTP.EXE 公用程式) 使用 FTP。</span><span class="sxs-lookup"><span data-stu-id="5bf29-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="5bf29-288">採用使用中 FTP (例如 FTP.EXE) 的 FTP 用戶端通常無法透過防火牆作業。</span><span class="sxs-lookup"><span data-stu-id="5bf29-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="5bf29-289">使用中 FTP 可指定 FTP 伺服器將可能無法連線的內部 LAN 位址。</span><span class="sxs-lookup"><span data-stu-id="5bf29-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="5bf29-290">如需使用 FTP 部署至 App Service Web 應用程式的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="5bf29-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="5bf29-291">使用 FTP 公用程式部署</span><span class="sxs-lookup"><span data-stu-id="5bf29-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="5bf29-292">[設定部署認證] 來設定</span><span class="sxs-lookup"><span data-stu-id="5bf29-292">Set up deployment credentials</span></span>
<span data-ttu-id="5bf29-293">確定您已執行 **AzureWebDemo** 應用程式來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="5bf29-294">您會將檔案移轉到此位置。</span><span class="sxs-lookup"><span data-stu-id="5bf29-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="5bf29-295">登入傳統入口網站並按一下 [ **Web Apps**]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="5bf29-296">確定 **WebDemoWebApp** 顯示在 Web 應用程式清單中，並確定它正在執行中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="5bf29-297">按一下 **WebDemoWebApp** 以開啟其 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5bf29-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="5bf29-298">在 [儀表板] 頁面的 [快速瀏覽] 下，按一下 [設定您的部署認證] \(如果您已有部署認證，則為 [重設您的部署認證])。</span><span class="sxs-lookup"><span data-stu-id="5bf29-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="5bf29-299">部署認證與 Microsoft 帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="5bf29-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="5bf29-300">您需要指定使用者名稱和密碼，以便利用 Git 和 FTP 進行部署。</span><span class="sxs-lookup"><span data-stu-id="5bf29-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="5bf29-301">您可以使用這些認證來部署至與您的 Microsoft 帳戶相關聯的所有 Azure 訂用帳戶中的任何 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="5bf29-302">在對話方塊中提供 Git 和 FTP 部署，並記錄使用者名稱和密碼以供未來使用。</span><span class="sxs-lookup"><span data-stu-id="5bf29-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="5bf29-303">取得 FTP 連線資訊</span><span class="sxs-lookup"><span data-stu-id="5bf29-303">Get FTP connection information</span></span>
<span data-ttu-id="5bf29-304">若要使用 FTP 將應用程式檔案部署至新建立的 Web 應用程式，您需要取得連線資訊。</span><span class="sxs-lookup"><span data-stu-id="5bf29-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="5bf29-305">取得連線資訊的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="5bf29-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="5bf29-306">造訪 Web 應用程式的 [ **儀表板** ] 頁面是一種方法；另一種方法則是下載 Web 應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="5bf29-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="5bf29-307">發行設定檔是可提供下列資訊的 XML 檔案：Azure App Service 中 Web 應用程式的 FTP 主機名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="5bf29-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="5bf29-308">您可以使用此使用者名稱和密碼來部署至與 Azure 帳戶相關聯的所有訂用帳戶中的任何 Web 應用程式 (不限於這一個)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="5bf29-309">若要從 [Azure 入口網站][Azure Portal]中的 Web 應用程式刀鋒視窗中獲得 FTP 連線資訊：</span><span class="sxs-lookup"><span data-stu-id="5bf29-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="5bf29-310">在 [基本功能] 之下，尋找並複製 [FTP 主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="5bf29-311">這是類似於 `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`的 URI。</span><span class="sxs-lookup"><span data-stu-id="5bf29-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="5bf29-312">在 [基本功能] 之下，尋找並複製 [FTP/部署使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="5bf29-313">其格式為 *webappname\deployment-username*；例如 `WebDemoWebApp\deployer77`。</span><span class="sxs-lookup"><span data-stu-id="5bf29-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="5bf29-314">若要從發行設定檔取得 FTP 連線資訊：</span><span class="sxs-lookup"><span data-stu-id="5bf29-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="5bf29-315">在 Web 應用程式的刀鋒視窗中，按一下 [ **取得發行設定檔**]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="5bf29-316">這會將 .publishsettings 檔案下載到本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="5bf29-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="5bf29-317">在 XML 編輯器或文字編輯器中開啟 .publishsettings 檔案，然後尋找包含 `publishMethod="FTP"` 的 `<publishProfile>` 元素。</span><span class="sxs-lookup"><span data-stu-id="5bf29-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="5bf29-318">該元素如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bf29-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="5bf29-319">請注意，Web 應用程式的 `publishProfile` 設定會對應至 FileZilla Site Manager 設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bf29-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="5bf29-320">`publishUrl` 與 [FTP 主機名稱] 相同 (您在 [主機] 中設定的值)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="5bf29-321">`publishMethod="FTP"` 表示您將 [通訊協定] 設定為 [FTP - 檔案傳輸通訊協定]，而將 [加密] 設定為 [使用一般 FTP]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="5bf29-322">`userName` 和 `userPWD` 是您重設部署認證時指定之實際使用者名稱和密碼值的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5bf29-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="5bf29-323">`userName` 與 [ **部署 / FTP 使用者**] 相同。</span><span class="sxs-lookup"><span data-stu-id="5bf29-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="5bf29-324">這些對應至 FileZilla 中的 [使用者] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="5bf29-325">`ftpPassiveMode="True"`表示 FTP 站台使用被動 FTP 傳輸；選取 [ **被動** on the **被動** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5bf29-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="5bf29-326">設定 Web 應用程式以裝載 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="5bf29-327">在發佈應用程式前，您需要變更一些組態設定，以便 Web 應用程式裝載 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="5bf29-328">在傳統入口網站中，移至 Web 應用程式的 [儀表板] 頁面並按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="5bf29-329">在 [ **設定** ] 頁面上，指定下列設定。</span><span class="sxs-lookup"><span data-stu-id="5bf29-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="5bf29-330">[Java 版本] 的預設值為 [關閉]；選取應用程式鎖定的 Java 版本；例如 1.7.0_51。</span><span class="sxs-lookup"><span data-stu-id="5bf29-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="5bf29-331">這麼做之後，還要確定 [ **Web 容器** ] 設定已設定為 Tomcat Server 的版本。</span><span class="sxs-lookup"><span data-stu-id="5bf29-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="5bf29-332">在 [預設文件] 中，新增 index.jsp 並向上移至清單最上方。</span><span class="sxs-lookup"><span data-stu-id="5bf29-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="5bf29-333">(Web 應用程式的預設檔案為 hostingstart.html。)</span><span class="sxs-lookup"><span data-stu-id="5bf29-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="5bf29-334">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5bf29-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="5bf29-335">使用 Kudu 發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-335">Publish your application using Kudu</span></span>
<span data-ttu-id="5bf29-336">使用 Azure 內建的 Kudu 偵錯主控台是發佈應用程式的一種方法。</span><span class="sxs-lookup"><span data-stu-id="5bf29-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="5bf29-337">Kudu 已知可穩定而一致地使用於 App Service Web Apps 和 Tomcat Server。</span><span class="sxs-lookup"><span data-stu-id="5bf29-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="5bf29-338">瀏覽至下列格式的 URL，以存取 Web 應用程式的主控台：</span><span class="sxs-lookup"><span data-stu-id="5bf29-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="5bf29-339">在此程序中，Kudu 主控台位於下列 URL；請瀏覽至此位置：</span><span class="sxs-lookup"><span data-stu-id="5bf29-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="5bf29-340">從頂端功能表，選取 [偵錯主控台] > [CMD]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="5bf29-341">在主控台命令列中，導覽至 `/site/wwwroot` (或按一下 `site`，然後按一下頁面頂端的目錄檢視中的 `wwwroot`)：</span><span class="sxs-lookup"><span data-stu-id="5bf29-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="5bf29-342">在您指定 [ **Java 版本**] 後，Tomcat 伺服器應建立 webapps 目錄。</span><span class="sxs-lookup"><span data-stu-id="5bf29-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="5bf29-343">在主控台命令列中，導覽至 webapps 目錄：</span><span class="sxs-lookup"><span data-stu-id="5bf29-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="5bf29-344">從 `<project-path>/JSPHello/src/` 拖曳 JSPHello.war 並放在 `/site/wwwroot/webapps` 之下的 Kudu 目錄檢視中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="5bf29-345">請勿將它拖曳至 [拖曳至此以便上傳和壓縮] 區域，因為 Tomcat 會將它解壓縮。</span><span class="sxs-lookup"><span data-stu-id="5bf29-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="5bf29-346">JSPHello.war 一開始會自行出現在目錄區域中：</span><span class="sxs-lookup"><span data-stu-id="5bf29-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="5bf29-347">Tomcat Server 會在短時間 (或許少於 5 分鐘) 內將 WAR 檔案解壓縮到已解壓縮的 JSPHello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="5bf29-348">按一下 ROOT 目錄，查看 index.jsp 是否已解壓縮並複製到此處。</span><span class="sxs-lookup"><span data-stu-id="5bf29-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="5bf29-349">若是如此，請導覽回到 webapps 目錄，查看是否已建立已解壓縮的 JSPHello 目錄。</span><span class="sxs-lookup"><span data-stu-id="5bf29-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="5bf29-350">如果您未看見這些項目，請稍後並重複。</span><span class="sxs-lookup"><span data-stu-id="5bf29-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="5bf29-351">使用 FileZilla 發佈您的應用程式 (選用)</span><span class="sxs-lookup"><span data-stu-id="5bf29-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="5bf29-352">FileZilla 是另一項可用來發佈應用程式的工具 ，這是具有便利圖形 UI 的熱門協力廠商 FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5bf29-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="5bf29-353">如果您還沒有 FileZilla，可以從 [http://filezilla-project.org/](http://filezilla-project.org/) 下載並安裝此工具。</span><span class="sxs-lookup"><span data-stu-id="5bf29-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="5bf29-354">如需使用用戶端的詳細資訊，請參閱 [FileZilla 文件](https://wiki.filezilla-project.org/Documentation)和 [FTP 用戶端 - 第 4 部分：FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx) 上的這篇部落格。</span><span class="sxs-lookup"><span data-stu-id="5bf29-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="5bf29-355">在 FileZilla 中，按一下 [檔案] > [網站管理員]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="5bf29-356">在 [網站管理員] 對話方塊中，按一下 [新增網站]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="5bf29-357">[ **選取項目** ] 中將會出現新的空白 FTP 網站，提示您提供名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf29-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="5bf29-358">在此程序中，將它命名為 `AzureWebDemo-FTP`</span><span class="sxs-lookup"><span data-stu-id="5bf29-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="5bf29-359">在 [一般]  索引標籤上，指定下列設定：</span><span class="sxs-lookup"><span data-stu-id="5bf29-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="5bf29-360">**主機：**輸入您從儀表板複製的 [FTP 主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="5bf29-361">**連接埠：**(留白，因為這是被動式傳輸，伺服器將會決定要使用的連接埠。)</span><span class="sxs-lookup"><span data-stu-id="5bf29-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="5bf29-362">**通訊協定：** (FTP 檔案傳輸通訊協定)</span><span class="sxs-lookup"><span data-stu-id="5bf29-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="5bf29-363">**加密：** 使用一般 FTP</span><span class="sxs-lookup"><span data-stu-id="5bf29-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="5bf29-364">**登入類型：** 正常</span><span class="sxs-lookup"><span data-stu-id="5bf29-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="5bf29-365">**使用者：** 輸入您從儀表板複製的部署/FTP 使用者。</span><span class="sxs-lookup"><span data-stu-id="5bf29-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="5bf29-366">這是完整 FTP 使用者名稱，格式為 *webappname\username*。</span><span class="sxs-lookup"><span data-stu-id="5bf29-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="5bf29-367">**密碼：** 輸入您設定部署認證時指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="5bf29-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="5bf29-368">在 [傳輸設定] 索引標籤上，選取 [被動]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="5bf29-369">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-369">Click **Connect**.</span></span> <span data-ttu-id="5bf29-370">如果成功，FileZilla 的主控台將顯示 `Status: Connected` 訊息並發出 `LIST` 命令以列出目錄內容。</span><span class="sxs-lookup"><span data-stu-id="5bf29-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="5bf29-371">在 [ **本機** ] 網站面板中，選取 JSPHello.war 檔案所在的來源目錄；路徑將類似下列路徑：</span><span class="sxs-lookup"><span data-stu-id="5bf29-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="5bf29-372">在 [ **遠端** ] 網站面板中，選取目的地資料夾。</span><span class="sxs-lookup"><span data-stu-id="5bf29-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="5bf29-373">您會將 WAR 檔案部署至 Web 應用程式的根目錄下的 `webapps` 目錄。</span><span class="sxs-lookup"><span data-stu-id="5bf29-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="5bf29-374">導覽至 `/site/wwwroot`，以滑鼠右鍵按一下 `wwwroot`，然後選取 [建立目錄]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="5bf29-375">將目錄命名為 `webapps` 並輸入該目錄。</span><span class="sxs-lookup"><span data-stu-id="5bf29-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="5bf29-376">將 JSPHello.war 傳輸至 `/site/wwwroot/webapps`</span><span class="sxs-lookup"><span data-stu-id="5bf29-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="5bf29-377">選取 [本機] 檔案清單中的 JSPHello.war，在其上按一下滑鼠右鍵並選取 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="5bf29-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="5bf29-378">您應看見該檔案出現在 `/site/wwwroot/webapps`中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="5bf29-379">將 JSPHello.war 複製到 webapps 目錄之後，Tomcat Server 會自動將 WAR 檔案中的檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="5bf29-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="5bf29-380">雖然 Tomcat Server 幾乎立即開始進行解壓縮，但檔案可能需要很長的一段時間 (可能數小時) 才會出現在 FTP 用戶端中。</span><span class="sxs-lookup"><span data-stu-id="5bf29-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="5bf29-381">在 Web 應用程式上執行 Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf29-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="5bf29-382">上傳 WAR 檔案並確認 Tomcat Server 已建立解壓縮的 `JSPHello` 目錄後，請瀏覽至 `http://webdemowebapp.azurewebsites.net/JSPHello` 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="5bf29-383">**注意：**如果從傳統入口網站按一下 [瀏覽]，可能會出現預設網頁，表示「此 Java Web 應用程式建立成功」。</span><span class="sxs-lookup"><span data-stu-id="5bf29-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="5bf29-384">您可能必須重新整理網頁，才能檢視應用程式輸出 (而非預設網頁)。</span><span class="sxs-lookup"><span data-stu-id="5bf29-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="5bf29-385">當應用程式執行時，您應看見有下列輸出的網頁：</span><span class="sxs-lookup"><span data-stu-id="5bf29-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="5bf29-386">清除 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="5bf29-386">Clean up Azure resources</span></span>
<span data-ttu-id="5bf29-387">此程序會建立 App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf29-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="5bf29-388">只要資源存在，您就需支付費用。</span><span class="sxs-lookup"><span data-stu-id="5bf29-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="5bf29-389">除非打算繼續使用 Web 應用程式進行測試或開發，否則您應考慮予以停止或刪除。</span><span class="sxs-lookup"><span data-stu-id="5bf29-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="5bf29-390">已停止的 Web 應用程式仍將帶來少許費用，但您可以隨時予以重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5bf29-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="5bf29-391">刪除 Web 應用程式會清除您已上傳至其上的所有資料。</span><span class="sxs-lookup"><span data-stu-id="5bf29-391">Deleting a web app erases all data you have uploaded to it.</span></span>

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
