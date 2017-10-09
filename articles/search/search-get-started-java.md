---
title: "使用 Azure 搜尋在 Java 中啟動 aaaGet |Microsoft 文件"
description: "如何 toobuild 託管雲端搜尋上為您的程式語言中使用 Java 的 Azure 應用程式。"
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="a3be6-103">開始在 Java 中使用 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="a3be6-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3be6-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="a3be6-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="a3be6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a3be6-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="a3be6-106">了解如何自訂 Java toobuild 搜尋應用程式，使用 Azure 搜尋的搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="a3be6-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="a3be6-107">本教學課程使用 hello [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 物件和作業在此練習中使用。</span><span class="sxs-lookup"><span data-stu-id="a3be6-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="a3be6-108">toorun 此範例中，您必須擁有 Azure 搜尋服務，您可以申請中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a3be6-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="a3be6-109">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a3be6-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="a3be6-110">我們使用下列軟體 toobuild hello，並測試這個範例：</span><span class="sxs-lookup"><span data-stu-id="a3be6-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="a3be6-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)。</span><span class="sxs-lookup"><span data-stu-id="a3be6-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="a3be6-112">是確定 toodownload hello EE 版本。</span><span class="sxs-lookup"><span data-stu-id="a3be6-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="a3be6-113">其中一個 hello 驗證步驟需要只在這個版本中找到的功能。</span><span class="sxs-lookup"><span data-stu-id="a3be6-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="a3be6-114">JDK 8u40。</span><span class="sxs-lookup"><span data-stu-id="a3be6-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="a3be6-115">Apache Tomcat 8.0。</span><span class="sxs-lookup"><span data-stu-id="a3be6-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="a3be6-116">關於 hello 資料</span><span class="sxs-lookup"><span data-stu-id="a3be6-116">About hello data</span></span>
<span data-ttu-id="a3be6-117">此範例應用程式會使用資料 hello[美國地理服務 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)、 篩選上 hello 羅德島狀態 tooreduce hello 資料集的大小。</span><span class="sxs-lookup"><span data-stu-id="a3be6-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="a3be6-118">我們將使用此資料 toobuild 傳回例如醫院和學校，以及地理功能，例如資料流、 湖泊、 和 summits 地標建築物的搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3be6-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="a3be6-119">在此應用程式，hello **SearchServlet.java**建置程式，並載入 hello 索引使用[索引子](https://msdn.microsoft.com/library/azure/dn798918.aspx)建構，擷取 hello 篩選 USG 從公開的 Azure SQL Database 的資料集。</span><span class="sxs-lookup"><span data-stu-id="a3be6-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="a3be6-120">Hello 程式碼中提供預先定義的認證和連接資訊 toohello 線上資料來源。</span><span class="sxs-lookup"><span data-stu-id="a3be6-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="a3be6-121">關於資料存取，不需要進一步設定。</span><span class="sxs-lookup"><span data-stu-id="a3be6-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="a3be6-122">我們在 hello 免費定價層的 hello 10000 文件限制此資料集 toostay 套用篩選。</span><span class="sxs-lookup"><span data-stu-id="a3be6-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="a3be6-123">如果您使用 hello 標準層，不會套用此限制，以及您可以修改這個程式碼 toouse 更大的資料集。</span><span class="sxs-lookup"><span data-stu-id="a3be6-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="a3be6-124">如需各個定價層的容量詳細資料，請參閱 [限制和條件約束](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="a3be6-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="a3be6-125">關於 hello 程式檔案</span><span class="sxs-lookup"><span data-stu-id="a3be6-125">About hello program files</span></span>
<span data-ttu-id="a3be6-126">hello 下列清單說明相關 toothis 範例的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a3be6-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="a3be6-127">Search.jsp： 提供 hello 使用者介面</span><span class="sxs-lookup"><span data-stu-id="a3be6-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="a3be6-128">SearchServlet.java： 提供的方法 （類似 tooa 控制站在 MVC 中）</span><span class="sxs-lookup"><span data-stu-id="a3be6-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="a3be6-129">SearchServiceClient.java：處理 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a3be6-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="a3be6-130">SearchServiceHelper.java：提供靜態方法的協助程式類別</span><span class="sxs-lookup"><span data-stu-id="a3be6-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="a3be6-131">Document.java： 提供 hello 資料模型</span><span class="sxs-lookup"><span data-stu-id="a3be6-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="a3be6-132">config.properties： 設定 hello 搜尋服務 URL 和 api 金鑰</span><span class="sxs-lookup"><span data-stu-id="a3be6-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="a3be6-133">Pom.xml：Maven 相依性</span><span class="sxs-lookup"><span data-stu-id="a3be6-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="a3be6-134">尋找 hello 服務名稱和您的 Azure 搜尋服務的 api 金鑰</span><span class="sxs-lookup"><span data-stu-id="a3be6-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="a3be6-135">所有對 Azure 搜尋 REST API 呼叫會要求您提供 hello 服務 URL 和 api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a3be6-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="a3be6-136">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a3be6-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a3be6-137">Hello 跳躍列中，按一下**搜尋服務**toolist hello Azure 搜尋服務的所有訂用帳戶佈建。</span><span class="sxs-lookup"><span data-stu-id="a3be6-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="a3be6-138">選取您想要 toouse hello 服務。</span><span class="sxs-lookup"><span data-stu-id="a3be6-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="a3be6-139">Hello 服務儀表板上，您會看到磚，以便於基本資訊以及 hello 索引鍵圖示來存取 hello 系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="a3be6-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="a3be6-140">複製 hello 服務 URL 和管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="a3be6-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="a3be6-141">您需要這些更新版本中，當新增 toohello **config.properties**檔案。</span><span class="sxs-lookup"><span data-stu-id="a3be6-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="a3be6-142">下載檔案的 hello 範例</span><span class="sxs-lookup"><span data-stu-id="a3be6-142">Download hello sample files</span></span>
1. <span data-ttu-id="a3be6-143">跳過[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="a3be6-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="a3be6-144">按一下**Download ZIP**儲存 hello.zip 檔案 toodisk，，然後將它包含的所有 hello 檔案都解壓縮。</span><span class="sxs-lookup"><span data-stu-id="a3be6-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="a3be6-145">請考慮擷取 hello 檔案至您的 Java 工作區 toomake 它更容易 toofind hello 專案更新版本。</span><span class="sxs-lookup"><span data-stu-id="a3be6-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="a3be6-146">hello 範例檔案是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="a3be6-146">hello sample files are read-only.</span></span> <span data-ttu-id="a3be6-147">以滑鼠右鍵按一下資料夾內容和清除 hello 唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="a3be6-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="a3be6-148">所有後續的檔案修改及執行陳述式都會用到此資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a3be6-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="a3be6-149">匯入專案</span><span class="sxs-lookup"><span data-stu-id="a3be6-149">Import project</span></span>
1. <span data-ttu-id="a3be6-150">在 Eclipse 中，選擇 [檔案] > [匯入] > [一般] > [將現有專案匯入工作區]。</span><span class="sxs-lookup"><span data-stu-id="a3be6-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="a3be6-151">在**選取根目錄**，瀏覽 toohello 包含範例檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a3be6-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="a3be6-152">選取包含 hello.project 資料夾 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a3be6-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="a3be6-153">hello 專案應該會出現在 hello**專案**為選定項目清單。</span><span class="sxs-lookup"><span data-stu-id="a3be6-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="a3be6-154">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-154">Click **Finish**.</span></span>
4. <span data-ttu-id="a3be6-155">使用**Project Explorer** tooview 和編輯 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a3be6-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="a3be6-156">如果它尚未開啟，請按一下**視窗** > **顯示檢視** > **Project Explorer**或使用 hello 捷徑 tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="a3be6-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="a3be6-157">設定 hello 服務 URL 和 api 金鑰</span><span class="sxs-lookup"><span data-stu-id="a3be6-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="a3be6-158">在**Project Explorer**，連按兩下**config.properties** tooedit hello 組態設定包含 hello 伺服器名稱和 api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a3be6-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="a3be6-159">Toohello 稍早在本文中，其中 hello 中找到 hello 服務 URL 和 api 金鑰中的步驟，請參閱[Azure 入口網站](https://portal.azure.com)，現在您將在輸入 tooget hello 值**config.properties**。</span><span class="sxs-lookup"><span data-stu-id="a3be6-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="a3be6-160">在**config.properties**，「 Api 金鑰 」 取代為您的服務的 hello api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a3be6-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="a3be6-161">接下來，服務名稱 （使用的 hello URL http://servicename.search.windows.net hello 第一個元件） 會取代 「 服務名稱 」 hello 中相同的檔案。</span><span class="sxs-lookup"><span data-stu-id="a3be6-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="a3be6-162">設定專案，建置和執行階段環境的 hello</span><span class="sxs-lookup"><span data-stu-id="a3be6-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="a3be6-163">在 Eclipse 中，在 [專案總管] 中，以滑鼠右鍵按一下 hello 專案 >**屬性** > **專案 Facet**。</span><span class="sxs-lookup"><span data-stu-id="a3be6-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="a3be6-164">選取 [Dynamic Web Module (動態網路模組)]、[Java] 及 [JavaScript]。</span><span class="sxs-lookup"><span data-stu-id="a3be6-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="a3be6-165">按一下 [套用] 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-165">Click **Apply**.</span></span>
4. <span data-ttu-id="a3be6-166">選取 [視窗] > [喜好設定] > [伺服器] > [執行階段環境] > [新增..]。</span><span class="sxs-lookup"><span data-stu-id="a3be6-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="a3be6-167">展開 Apache 並選取您先前安裝的 hello Apache Tomcat 伺服器 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="a3be6-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="a3be6-168">我們的系統安裝了第 8 版。</span><span class="sxs-lookup"><span data-stu-id="a3be6-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="a3be6-169">在 hello 下一個頁面上，指定 hello Tomcat 安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="a3be6-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="a3be6-170">在 Windows 電腦中，這通常為 C:\Program Files\Apache Software Foundation\Tomcat *版本*。</span><span class="sxs-lookup"><span data-stu-id="a3be6-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="a3be6-171">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-171">Click **Finish**.</span></span>
8. <span data-ttu-id="a3be6-172">選取 [視窗] > [喜好設定] > [Java] > [已安裝的 JRE] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="a3be6-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="a3be6-173">在 [Add JRE (新增 JRE)] 中，選取 [Standard VM (標準 VM)]。</span><span class="sxs-lookup"><span data-stu-id="a3be6-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="a3be6-174">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-174">Click **Next**.</span></span>
11. <span data-ttu-id="a3be6-175">在 [JRE Definition (JRE 定義)] 的 [JRE home (JRE 主資料夾)] 中按一下 [Directory (目錄)] 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="a3be6-176">瀏覽過**Program Files** > **Java**並選取您先前安裝的 JDK hello。</span><span class="sxs-lookup"><span data-stu-id="a3be6-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="a3be6-177">它是 hello JRE 重要 tooselect hello JDK。</span><span class="sxs-lookup"><span data-stu-id="a3be6-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="a3be6-178">在安裝 JREs，選擇 hello **JDK**。</span><span class="sxs-lookup"><span data-stu-id="a3be6-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="a3be6-179">您的設定應該看起來類似 toohello 下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="a3be6-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="a3be6-180">（選擇性） 選取**視窗** > **網頁瀏覽器** > **Internet Explorer** tooopen hello 應用程式，在外部瀏覽器視窗中的。</span><span class="sxs-lookup"><span data-stu-id="a3be6-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="a3be6-181">使用外部瀏覽器可給您更好的 Web 應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="a3be6-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="a3be6-182">您現在已完成 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a3be6-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="a3be6-183">接下來，您會建置並執行 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a3be6-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="a3be6-184">建置 hello 專案</span><span class="sxs-lookup"><span data-stu-id="a3be6-184">Build hello project</span></span>
1. <span data-ttu-id="a3be6-185">在 專案總管 hello 專案名稱上按一下滑鼠右鍵，然後選擇 **執行身分** > **Maven 建置...** tooconfigure hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a3be6-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="a3be6-186">在 Edit Configuration (編輯組態) 的 Goals (目標) 中輸入 "clean install"，然後按一下Run (執行) 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="a3be6-187">狀態訊息會輸出 toohello 主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="a3be6-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="a3be6-188">您應該會看到建置成功指示 hello 建立專案時不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3be6-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="a3be6-189">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="a3be6-189">Run hello app</span></span>
<span data-ttu-id="a3be6-190">在最後一個步驟中，您將在本機伺服器執行階段環境中執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3be6-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="a3be6-191">如果尚未您尚未在 Eclipse 中指定的伺服器執行階段環境，您將先需要 toodo。</span><span class="sxs-lookup"><span data-stu-id="a3be6-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="a3be6-192">在 Project Explorer 中，展開 [WebContent] 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="a3be6-193">以滑鼠右鍵依序按一下 [Search.jsp] > [執行身分] > [在伺服器上執行]。</span><span class="sxs-lookup"><span data-stu-id="a3be6-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="a3be6-194">選取 hello Apache Tomcat 伺服器，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="a3be6-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="a3be6-195">如果您使用非預設工作區 toostore 您的專案，您將需要 toomodify**執行設定**toopoint toohello 專案位置 tooavoid 伺服器啟動時的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3be6-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="a3be6-196">在 [專案總管] 中，以滑鼠右鍵依序按一下 [Search.jsp] > [執行身分] > [執行組態]。</span><span class="sxs-lookup"><span data-stu-id="a3be6-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="a3be6-197">選取 hello Apache Tomcat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a3be6-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="a3be6-198">按一下 [Arguments (引數)] 。</span><span class="sxs-lookup"><span data-stu-id="a3be6-198">Click **Arguments**.</span></span> <span data-ttu-id="a3be6-199">按一下**工作區**或**檔案系統**包含 hello 專案 tooset hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a3be6-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="a3be6-200">當您執行 hello 應用程式時，您應該會看到瀏覽器視窗中，輸入條款提供搜尋方塊。</span><span class="sxs-lookup"><span data-stu-id="a3be6-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="a3be6-201">等候約 1 分鐘後，再按一下**搜尋**toogive hello 服務時間 toocreate 和負載 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="a3be6-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="a3be6-202">如果您收到 HTTP 404 錯誤，您只需要 toowait 稍微較長的時間後再重試。</span><span class="sxs-lookup"><span data-stu-id="a3be6-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="a3be6-203">搜尋 USGS 資料</span><span class="sxs-lookup"><span data-stu-id="a3be6-203">Search on USGS data</span></span>
<span data-ttu-id="a3be6-204">hello USG 資料集包含相關 toohello 狀態的羅德島的記錄。</span><span class="sxs-lookup"><span data-stu-id="a3be6-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="a3be6-205">如果您按一下**搜尋**上是空的搜尋 方塊中，您會取得 hello 排行前 50 名項目，hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="a3be6-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="a3be6-206">輸入的搜尋詞彙，將 hello 搜尋引擎一些 toogo 上。</span><span class="sxs-lookup"><span data-stu-id="a3be6-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="a3be6-207">試著輸入區域名稱。</span><span class="sxs-lookup"><span data-stu-id="a3be6-207">Try entering a regional name.</span></span> <span data-ttu-id="a3be6-208">「 Roger Williams 」 已羅德島 hello 第一個管理員。</span><span class="sxs-lookup"><span data-stu-id="a3be6-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="a3be6-209">許多公園、建築物和學校都是以他的姓名命名。</span><span class="sxs-lookup"><span data-stu-id="a3be6-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="a3be6-210">此外，您也可以試著使用這些字詞：</span><span class="sxs-lookup"><span data-stu-id="a3be6-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="a3be6-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="a3be6-211">Pawtucket</span></span>
* <span data-ttu-id="a3be6-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="a3be6-212">Pembroke</span></span>
* <span data-ttu-id="a3be6-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="a3be6-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3be6-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3be6-214">Next steps</span></span>
<span data-ttu-id="a3be6-215">這是根據 Java 和 hello USG 資料集 hello 第一個 Azure 搜尋教學課程。</span><span class="sxs-lookup"><span data-stu-id="a3be6-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="a3be6-216">經過一段時間，我們將會延長此教學課程 toodemonstrate 您可能會想 toouse 自訂方案中的其他搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="a3be6-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="a3be6-217">如果您已經有一些背景，在 Azure 搜尋中，可用於此範例為 springboard 進一步的實驗，或許加強 hello[搜尋頁面](search-pagination-page-layout.md)，或實作[多面向導覽](search-faceted-navigation.md)。</span><span class="sxs-lookup"><span data-stu-id="a3be6-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="a3be6-218">您也可以藉由加入計數和批次的文件，以便使用者可以透過 hello 結果頁改善 hello 搜尋結果頁面時。</span><span class="sxs-lookup"><span data-stu-id="a3be6-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="a3be6-219">新 tooAzure 搜尋嗎？</span><span class="sxs-lookup"><span data-stu-id="a3be6-219">New tooAzure Search?</span></span> <span data-ttu-id="a3be6-220">我們建議您嘗試其他教學課程 toodevelop 了解您可以建立。</span><span class="sxs-lookup"><span data-stu-id="a3be6-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="a3be6-221">請瀏覽我們[文件頁面](https://azure.microsoft.com/documentation/services/search/)toofind 更多資源。</span><span class="sxs-lookup"><span data-stu-id="a3be6-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="a3be6-222">您也可以檢視中的 hello 連結我們[影片和教學課程清單](search-video-demo-tutorial-list.md)tooaccess 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a3be6-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
