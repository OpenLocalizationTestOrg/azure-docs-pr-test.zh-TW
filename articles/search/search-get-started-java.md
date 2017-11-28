---
title: "開始在 Java 中使用 Azure 搜尋服務 | Microsoft Docs"
description: "如何使用 Java 做為程式設計語言，在 Azure 上建置雲端託管搜尋應用程式。"
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
ms.openlocfilehash: f6ca06a0349def97b38a1bf6d0d8f36236077e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="19981-103">開始在 Java 中使用 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="19981-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19981-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="19981-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="19981-105">.NET</span><span class="sxs-lookup"><span data-stu-id="19981-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="19981-106">瞭解如何建置使用 Azure 搜尋服務提供搜尋體驗的自訂 Java 搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="19981-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="19981-107">本教學課程利用 [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/dn798935.aspx) 來建構在此練習中所使用的物件和作業。</span><span class="sxs-lookup"><span data-stu-id="19981-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="19981-108">若要執行此範例，必須要有 Azure 搜尋服務，您可以在 [Azure 入口網站](https://portal.azure.com)註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="19981-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="19981-109">如需逐步指示，請參閱 [在入口網站中建立 Azure 搜尋服務](search-create-service-portal.md) 。</span><span class="sxs-lookup"><span data-stu-id="19981-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="19981-110">我們使用了以下軟體建置及測試此範例：</span><span class="sxs-lookup"><span data-stu-id="19981-110">We used the following software to build and test this sample:</span></span>

* <span data-ttu-id="19981-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)。</span><span class="sxs-lookup"><span data-stu-id="19981-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="19981-112">請務必下載 EE 版本。</span><span class="sxs-lookup"><span data-stu-id="19981-112">Be sure to download the EE version.</span></span> <span data-ttu-id="19981-113">其中一個驗證步驟所需的功能只有在此版本中才能找到。</span><span class="sxs-lookup"><span data-stu-id="19981-113">One of the verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="19981-114">JDK 8u40。</span><span class="sxs-lookup"><span data-stu-id="19981-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="19981-115">Apache Tomcat 8.0。</span><span class="sxs-lookup"><span data-stu-id="19981-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-the-data"></a><span data-ttu-id="19981-116">關於資料</span><span class="sxs-lookup"><span data-stu-id="19981-116">About the data</span></span>
<span data-ttu-id="19981-117">此範例應用程式使用的 [美國地理服務中心 (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)資料已依據羅德島州進行篩選，藉此減少資料集的大小。</span><span class="sxs-lookup"><span data-stu-id="19981-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="19981-118">我們將使用此資料建置可傳回地標建築物 (例如醫院和學校) 及地理特徵 (例如河流、湖泊和山峰) 的搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="19981-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="19981-119">在此應用程式中， **SearchServlet.java** 程式會使用 [索引子](https://msdn.microsoft.com/library/azure/dn798918.aspx) 建構來建置及載入索引，以從公用 Azure SQL Database 擷取篩選過的 USGS 資料集。</span><span class="sxs-lookup"><span data-stu-id="19981-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="19981-120">程式碼中提供線上資料來源的預先定義認證和連接資訊。</span><span class="sxs-lookup"><span data-stu-id="19981-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span></span> <span data-ttu-id="19981-121">關於資料存取，不需要進一步設定。</span><span class="sxs-lookup"><span data-stu-id="19981-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="19981-122">我們在此資料集套用了一個篩選，以維持不超過免費版定價層的 10,000 個文件的數量上限。</span><span class="sxs-lookup"><span data-stu-id="19981-122">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="19981-123">如果使用標準版定價層，則不套用此限制，可以修改此程式碼以使用更大的資料集。</span><span class="sxs-lookup"><span data-stu-id="19981-123">If you use the standard tier, this limit does not apply, and you can modify this code to use a bigger dataset.</span></span> <span data-ttu-id="19981-124">如需各個定價層的容量詳細資料，請參閱 [限制和條件約束](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="19981-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-the-program-files"></a><span data-ttu-id="19981-125">關於程式檔</span><span class="sxs-lookup"><span data-stu-id="19981-125">About the program files</span></span>
<span data-ttu-id="19981-126">以下清單說明與此範例相關的檔案。</span><span class="sxs-lookup"><span data-stu-id="19981-126">The following list describes the files that are relevant to this sample.</span></span>

* <span data-ttu-id="19981-127">Search.jsp：提供使用者介面</span><span class="sxs-lookup"><span data-stu-id="19981-127">Search.jsp: Provides the user interface</span></span>
* <span data-ttu-id="19981-128">SearchServlet.java：提供方法 (類似 MVC 中的控制器)</span><span class="sxs-lookup"><span data-stu-id="19981-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span></span>
* <span data-ttu-id="19981-129">SearchServiceClient.java：處理 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="19981-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="19981-130">SearchServiceHelper.java：提供靜態方法的協助程式類別</span><span class="sxs-lookup"><span data-stu-id="19981-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="19981-131">Document.java：提供資料模型</span><span class="sxs-lookup"><span data-stu-id="19981-131">Document.java: Provides the data model</span></span>
* <span data-ttu-id="19981-132">config.properties：設定搜尋服務 URL 和 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="19981-132">config.properties: Sets the Search service URL and api-key</span></span>
* <span data-ttu-id="19981-133">Pom.xml：Maven 相依性</span><span class="sxs-lookup"><span data-stu-id="19981-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="19981-134">尋找 Azure 搜尋服務的服務名稱和 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="19981-134">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="19981-135">所有對 Azure 搜尋服務的 REST API 呼叫都會要求您提供服務 URL 和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="19981-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span></span> 

1. <span data-ttu-id="19981-136">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="19981-136">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="19981-137">在導向列中，按一下 [搜尋服務]  列出為您的訂用帳戶佈建的所有 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="19981-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="19981-138">選取您要使用的服務。</span><span class="sxs-lookup"><span data-stu-id="19981-138">Select the service you want to use.</span></span>
4. <span data-ttu-id="19981-139">您會在服務儀表板上看到基本資訊磚，以及存取系統管理金鑰的鑰匙圖示。</span><span class="sxs-lookup"><span data-stu-id="19981-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="19981-140">複製服務 URL 和系統管理金鑰，</span><span class="sxs-lookup"><span data-stu-id="19981-140">Copy the service URL and an admin key.</span></span> <span data-ttu-id="19981-141">稍後會需要將它們加到 **config.properties** 檔案中。</span><span class="sxs-lookup"><span data-stu-id="19981-141">You will need them later, when you add them to the **config.properties** file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="19981-142">下載範例檔案</span><span class="sxs-lookup"><span data-stu-id="19981-142">Download the sample files</span></span>
1. <span data-ttu-id="19981-143">前往 GitHub 的 [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo)。</span><span class="sxs-lookup"><span data-stu-id="19981-143">Go to [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="19981-144">按一下 [下載 ZIP] ，將 .zip 檔案儲存至磁碟，然後解壓縮其中所含的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="19981-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span></span> <span data-ttu-id="19981-145">可以考慮將檔案解壓縮到 Java 工作區，以便之後可以輕鬆找到專案。</span><span class="sxs-lookup"><span data-stu-id="19981-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span></span>
3. <span data-ttu-id="19981-146">範例檔案為唯讀。</span><span class="sxs-lookup"><span data-stu-id="19981-146">The sample files are read-only.</span></span> <span data-ttu-id="19981-147">請以滑鼠右鍵按一下資料夾內容，然後清除唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="19981-147">Right-click folder properties and clear the read-only attribute.</span></span>

<span data-ttu-id="19981-148">所有後續的檔案修改及執行陳述式都會用到此資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="19981-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="19981-149">匯入專案</span><span class="sxs-lookup"><span data-stu-id="19981-149">Import project</span></span>
1. <span data-ttu-id="19981-150">在 Eclipse 中，選擇 [檔案] > [匯入] > [一般] > [將現有專案匯入工作區]。</span><span class="sxs-lookup"><span data-stu-id="19981-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="19981-151">在 [Select root directory (選取根目錄)] 中，瀏覽至含有範例檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="19981-151">In **Select root directory**, browse to the folder containing sample files.</span></span> <span data-ttu-id="19981-152">請選取含有 .project 資料夾的資料夾。</span><span class="sxs-lookup"><span data-stu-id="19981-152">Select the folder that contains the .project folder.</span></span> <span data-ttu-id="19981-153">此專案應會在 [Projects (專案)]  清單中顯示為選取的項目。</span><span class="sxs-lookup"><span data-stu-id="19981-153">The project should appear in the **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="19981-154">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="19981-154">Click **Finish**.</span></span>
4. <span data-ttu-id="19981-155">使用 **專案總管** 檢視及編輯檔案。</span><span class="sxs-lookup"><span data-stu-id="19981-155">Use **Project Explorer** to view and edit the files.</span></span> <span data-ttu-id="19981-156">如果還沒開啟，請按一下 [視窗] > [顯示檢視] > [專案總管]，或使用捷徑來開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="19981-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span></span>

## <a name="configure-the-service-url-and-api-key"></a><span data-ttu-id="19981-157">設定服務 URL 和 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="19981-157">Configure the service URL and api-key</span></span>
1. <span data-ttu-id="19981-158">在**專案總管**中按兩下 **config.properties** 以編輯含有伺服器名稱和 API 金鑰的組態設定。</span><span class="sxs-lookup"><span data-stu-id="19981-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span></span>
2. <span data-ttu-id="19981-159">請參閱本文中稍早的步驟，其中提及如何在 [Azure 入口網站](https://portal.azure.com)中找到服務 URL 和 API 金鑰，藉此取得您現在要輸入 **config.properties** 中的值。</span><span class="sxs-lookup"><span data-stu-id="19981-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="19981-160">在 **config.properties**中，以您服務的 API 金鑰取代 "Api Key"。</span><span class="sxs-lookup"><span data-stu-id="19981-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span></span> <span data-ttu-id="19981-161">接著，在同一個檔案中以服務名稱 (URL http://servicename.search.windows.net 的第一個部分) 取代 "service name"。</span><span class="sxs-lookup"><span data-stu-id="19981-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span></span>
   
    ![][5]

## <a name="configure-the-project-build-and-runtime-environments"></a><span data-ttu-id="19981-162">設定專案、組建和執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="19981-162">Configure the project, build and runtime environments</span></span>
1. <span data-ttu-id="19981-163">在 Eclipse 的 [專案總管] 中，以滑鼠右鍵按一下專案 > [屬性] > [專案 Facet]。</span><span class="sxs-lookup"><span data-stu-id="19981-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="19981-164">選取 [Dynamic Web Module (動態網路模組)]、[Java] 及 [JavaScript]。</span><span class="sxs-lookup"><span data-stu-id="19981-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="19981-165">按一下 [套用] 。</span><span class="sxs-lookup"><span data-stu-id="19981-165">Click **Apply**.</span></span>
4. <span data-ttu-id="19981-166">選取 [視窗] > [喜好設定] > [伺服器] > [執行階段環境] > [新增..]。</span><span class="sxs-lookup"><span data-stu-id="19981-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="19981-167">展開 [Apache] 並選取您先前安裝的 Apache Tomcat 伺服器版本。</span><span class="sxs-lookup"><span data-stu-id="19981-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="19981-168">我們的系統安裝了第 8 版。</span><span class="sxs-lookup"><span data-stu-id="19981-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="19981-169">在下一頁指定 Tomcat 的安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="19981-169">On the next page, specify the Tomcat installation directory.</span></span> <span data-ttu-id="19981-170">在 Windows 電腦中，這通常為 C:\Program Files\Apache Software Foundation\Tomcat *版本*。</span><span class="sxs-lookup"><span data-stu-id="19981-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="19981-171">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="19981-171">Click **Finish**.</span></span>
8. <span data-ttu-id="19981-172">選取 [視窗] > [喜好設定] > [Java] > [已安裝的 JRE] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="19981-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="19981-173">在 [Add JRE (新增 JRE)] 中，選取 [Standard VM (標準 VM)]。</span><span class="sxs-lookup"><span data-stu-id="19981-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="19981-174">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="19981-174">Click **Next**.</span></span>
11. <span data-ttu-id="19981-175">在 [JRE Definition (JRE 定義)] 的 [JRE home (JRE 主資料夾)] 中按一下 [Directory (目錄)] 。</span><span class="sxs-lookup"><span data-stu-id="19981-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="19981-176">瀏覽至 [程式檔案] > [Java]，然後選取您先前安裝的 JDK。</span><span class="sxs-lookup"><span data-stu-id="19981-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span></span> <span data-ttu-id="19981-177">請務必選取 JDK 做為 JRE。</span><span class="sxs-lookup"><span data-stu-id="19981-177">It's important to select the JDK as the JRE.</span></span>
13. <span data-ttu-id="19981-178">在 [Installed JREs (安裝的 JRE)] 中選擇 **JDK**。</span><span class="sxs-lookup"><span data-stu-id="19981-178">In Installed JREs, choose the **JDK**.</span></span> <span data-ttu-id="19981-179">您的設定應該類似以下的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="19981-179">Your settings should look similar to the following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="19981-180">您可以選擇性地選取 [視窗] > [網頁瀏覽器] > [Internet Explorer] 以在外部瀏覽器視窗開啟應用程式。</span><span class="sxs-lookup"><span data-stu-id="19981-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span></span> <span data-ttu-id="19981-181">使用外部瀏覽器可給您更好的 Web 應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="19981-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="19981-182">您已經完成設定工作。</span><span class="sxs-lookup"><span data-stu-id="19981-182">You have now completed the configuration tasks.</span></span> <span data-ttu-id="19981-183">接著要建置並執行專案。</span><span class="sxs-lookup"><span data-stu-id="19981-183">Next, you'll build and run the project.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="19981-184">建置專案</span><span class="sxs-lookup"><span data-stu-id="19981-184">Build the project</span></span>
1. <span data-ttu-id="19981-185">在 [專案總管] 中，以滑鼠右鍵按一下專案名稱，然後選擇 [執行身分] > [Maven 組建...] 以設定專案。</span><span class="sxs-lookup"><span data-stu-id="19981-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span></span>
   
    ![][10]
2. <span data-ttu-id="19981-186">在 [Edit Configuration (編輯組態)] 的 [Goals (目標)] 中輸入 "clean install"，然後按一下 [Run (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="19981-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="19981-187">狀態訊息會輸出至主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="19981-187">Status messages are output to the console window.</span></span> <span data-ttu-id="19981-188">您應該會看見 BUILD SUCCESS 訊息，指出專案已建置完成，未發生任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="19981-188">You should see BUILD SUCCESS indicating the project built without errors.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="19981-189">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="19981-189">Run the app</span></span>
<span data-ttu-id="19981-190">在此最後步驟中，您要在本機伺服器執行階段環境中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="19981-190">In this last step, you will run the application in a local server runtime environment.</span></span>

<span data-ttu-id="19981-191">如果您尚未在 Eclipse 中指定伺服器執行階段環境，請務必先行指定。</span><span class="sxs-lookup"><span data-stu-id="19981-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span></span>

1. <span data-ttu-id="19981-192">在 Project Explorer 中，展開 [WebContent] 。</span><span class="sxs-lookup"><span data-stu-id="19981-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="19981-193">以滑鼠右鍵依序按一下 [Search.jsp] > [執行身分] > [在伺服器上執行]。</span><span class="sxs-lookup"><span data-stu-id="19981-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="19981-194">選取 Apache Tomcat 伺服器，然後按一下 [Run (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="19981-194">Select the Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="19981-195">如果您使用非預設工作區來儲存專案，則需要修改 [執行組態]，使其指向專案位置，以避免伺服器啟動錯誤。</span><span class="sxs-lookup"><span data-stu-id="19981-195">If you used a non-default workspace to store your project, you'll need to modify **Run Configuration** to point to the project location to avoid a server start-up error.</span></span> <span data-ttu-id="19981-196">在 [專案總管] 中，以滑鼠右鍵依序按一下 [Search.jsp] > [執行身分] > [執行組態]。</span><span class="sxs-lookup"><span data-stu-id="19981-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="19981-197">選取 Apache Tomcat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="19981-197">Select the Apache Tomcat server.</span></span> <span data-ttu-id="19981-198">按一下 [Arguments (引數)] 。</span><span class="sxs-lookup"><span data-stu-id="19981-198">Click **Arguments**.</span></span> <span data-ttu-id="19981-199">按一下 [Workspace (工作區)] 或 [File System (檔案系統)]，以設定包含專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="19981-199">Click **Workspace** or **File System** to set the folder containing the project.</span></span>
> 
> 

<span data-ttu-id="19981-200">執行應用程式時，您應該會看見瀏覽器視窗，並在其中提供可輸入字詞的搜尋方塊。</span><span class="sxs-lookup"><span data-stu-id="19981-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="19981-201">等待約一分鐘後再按一下 [Search (搜尋)]  ，讓服務有時間建立並載入索引。</span><span class="sxs-lookup"><span data-stu-id="19981-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span></span> <span data-ttu-id="19981-202">如果遇到 HTTP 404 錯誤，只要多等一下，即可再重試一次。</span><span class="sxs-lookup"><span data-stu-id="19981-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="19981-203">搜尋 USGS 資料</span><span class="sxs-lookup"><span data-stu-id="19981-203">Search on USGS data</span></span>
<span data-ttu-id="19981-204">USGS 資料集包含與羅德島州相關的記錄。</span><span class="sxs-lookup"><span data-stu-id="19981-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="19981-205">如果您在空白的搜尋方塊中按一下 [搜尋]  ，預設會出現前 50 個項目。</span><span class="sxs-lookup"><span data-stu-id="19981-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="19981-206">輸入搜尋詞彙，讓搜尋引擎運作一下。</span><span class="sxs-lookup"><span data-stu-id="19981-206">Entering a search term will give the search engine something to go on.</span></span> <span data-ttu-id="19981-207">試著輸入區域名稱。</span><span class="sxs-lookup"><span data-stu-id="19981-207">Try entering a regional name.</span></span> <span data-ttu-id="19981-208">"Roger Williams" 是羅德島州的第一任州長。</span><span class="sxs-lookup"><span data-stu-id="19981-208">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="19981-209">許多公園、建築物和學校都是以他的姓名命名。</span><span class="sxs-lookup"><span data-stu-id="19981-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="19981-210">此外，您也可以試著使用這些字詞：</span><span class="sxs-lookup"><span data-stu-id="19981-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="19981-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="19981-211">Pawtucket</span></span>
* <span data-ttu-id="19981-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="19981-212">Pembroke</span></span>
* <span data-ttu-id="19981-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="19981-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="19981-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19981-214">Next steps</span></span>
<span data-ttu-id="19981-215">這是第一個以 Java 和 USGS 資料集為基礎的 Azure 搜尋服務教學課程。</span><span class="sxs-lookup"><span data-stu-id="19981-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span></span> <span data-ttu-id="19981-216">我們會漸漸擴充本教學課程，以示範其他您可能會想用在自訂方案中的搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="19981-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="19981-217">如果您已有一些 Azure 搜尋服務的背景知識，可以利用此範例做為進一步實驗的跳板，例如擴充[搜尋頁面](search-pagination-page-layout.md)或實作[多面向導覽](search-faceted-navigation.md)。</span><span class="sxs-lookup"><span data-stu-id="19981-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="19981-218">您也可以新增計數和批次處理文件，讓使用者可以逐頁查看結果，藉此改進搜尋結果頁面。</span><span class="sxs-lookup"><span data-stu-id="19981-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="19981-219">不熟悉 Azure 搜尋服務嗎？</span><span class="sxs-lookup"><span data-stu-id="19981-219">New to Azure Search?</span></span> <span data-ttu-id="19981-220">建議您嘗試學習其他教學課程，深入了解您還可以建立哪些東西。</span><span class="sxs-lookup"><span data-stu-id="19981-220">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="19981-221">請瀏覽我們的 [文件頁面](https://azure.microsoft.com/documentation/services/search/) 以尋找更多資源。</span><span class="sxs-lookup"><span data-stu-id="19981-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="19981-222">您也可以查看我們 [影片和教學課程清單](search-video-demo-tutorial-list.md) 中的連結，以存取更多資訊。</span><span class="sxs-lookup"><span data-stu-id="19981-222">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

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
