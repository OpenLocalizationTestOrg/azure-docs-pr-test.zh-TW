---
title: "aaaUse Data Lake Analytics Java SDK toodevelop 應用程式 |Microsoft 文件"
description: "使用 Azure Data Lake Analytics Java SDK toodevelop 應用程式"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0d975812fe659ed34ee9befd37ee7c0bf50d3414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="a4a6f-103">透過 Java SDK 開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a4a6f-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="a4a6f-104">了解如何 toouse 會 hello Azure Data Lake Analytics Java SDK toocreate Azure 資料湖帳戶和執行基本作業，例如建立資料夾、 上傳和下載資料檔，刪除您的帳戶，以及使用工作。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-104">Learn how toouse hello Azure Data Lake Analytics Java SDK toocreate an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="a4a6f-105">如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Analytics](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="a4a6f-106">在本教學課程中，您將開發 Java 主控台應用程式，其中包含一般管理作業，以及建立測試資料和提交作業的範例。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="a4a6f-107">透過相同的教學課程使用其他支援的 hello toogo 工具，按一下此區段的最上層顯示 hello hello 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-107">toogo through hello same tutorial using other supported tools, click hello tabs on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4a6f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a4a6f-108">Prerequisites</span></span>
* <span data-ttu-id="a4a6f-109">Java Development Kit (JDK) 8 (使用 Java 1.8 版)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="a4a6f-110">IntelliJ 或其他合適的 Java 開發環境。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="a4a6f-111">此為選用步驟，但建議執行。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-111">This is optional but recommended.</span></span> <span data-ttu-id="a4a6f-112">下列的 hello 指示使用 IntelliJ。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-112">hello instructions below use IntelliJ.</span></span>
* <span data-ttu-id="a4a6f-113">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-113">**An Azure subscription**.</span></span> <span data-ttu-id="a4a6f-114">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a4a6f-115">建立 Azure Active Directory (AAD) 應用程式，並擷取其**用戶端識別碼**、**租用戶識別碼**和**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="a4a6f-116">如需 AAD 應用程式與指示如何 tooget 用戶端識別碼，請參閱[建立 Active Directory 應用程式和服務主體使用入口網站](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-116">For more information about AAD applications and instructions on how tooget a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a4a6f-117">hello Reply URI 與金鑰也會從 hello 入口網站可用一旦建立 hello 應用程式及產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-117">hello Reply URI and Key will also be available from hello portal once you have hello application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="a4a6f-118">如何使用 Azure Active Directory 驗證？</span><span class="sxs-lookup"><span data-stu-id="a4a6f-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="a4a6f-119">hello 下列程式碼片段提供程式碼**非互動式**驗證，其中 hello 應用程式提供它自己的認證。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-119">hello code snippet below provides code for **non-interactive** authentication, where hello application provides its own credentials.</span></span>

<span data-ttu-id="a4a6f-120">您將針對此教學課程 toowork 需要 toogive 應用程式的權限 toocreate 資源在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-120">You will need toogive your application permission toocreate resources in Azure for this tutorial toowork.</span></span> <span data-ttu-id="a4a6f-121">它是**強烈建議**基於此教學課程的 hello 您 Azure 訂用帳戶中只提供此應用程式參與者權限 tooa 新的、 未使用，和空白的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-121">It is **highly recommended** that you only give this application Contributor permissions tooa new, unused, and empty resource group in your Azure subscription for hello purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="a4a6f-122">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="a4a6f-122">Create a Java application</span></span>
1. <span data-ttu-id="a4a6f-123">開啟 IntelliJ 並建立新的 Java 專案使用 hello**命令列應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-123">Open IntelliJ and create a new Java project using hello **Command Line App** template.</span></span>
2. <span data-ttu-id="a4a6f-124">左側 hello 螢幕 hello 專案上按一下滑鼠右鍵，然後按一下**新增架構支援**。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-124">Right-click on hello project on hello left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="a4a6f-125">選擇 [Maven] 並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="a4a6f-126">開啟新建立的 hello **"pom.xml"**檔案，然後加入下列程式碼片段的文字之間 hello hello  **\</version >**標記和 hello  **\< /專案 >**標記：</span><span class="sxs-lookup"><span data-stu-id="a4a6f-126">Open hello newly created **"pom.xml"** file and add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="a4a6f-127">這個步驟是暫時的 hello Azure Data Lake Analytics SDK Maven 中有可用為止。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-127">This step is temporary until hello Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="a4a6f-128">提供 Maven hello SDK 之後，將會更新本文。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-128">This article will be updated once hello SDK is available in Maven.</span></span> <span data-ttu-id="a4a6f-129">所有未來的更新 toothis SDK 將會透過 Maven 了。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-129">All future updates toothis SDK will be availble through Maven.</span></span>
    >

        <repositories>
            <repository>
                <id>adx-snapshots</id>
                <name>Azure ADX Snapshots</name>
                <url>http://adxsnapshots.azurewebsites.net/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>oss-snapshots</id>
                <name>Open Source Snapshots</name>
                <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>always</updatePolicy>
                </snapshots>
            </repository>
        </repositories>
        <dependencies>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-authentication</artifactId>
                <version>1.0.0-20160513.000802-24</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-runtime</artifactId>
                <version>1.0.0-20160513.000812-28</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.rest</groupId>
                <artifactId>client-runtime</artifactId>
                <version>1.0.0-20160513.000825-29</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-store</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-analytics</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
        </dependencies>
4. <span data-ttu-id="a4a6f-130">跳過**檔案**，然後**設定**，然後**建置**，**執行**，**部署**。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-130">Go too**File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="a4a6f-131">選取 [建置工具] > [Maven] > [匯入]。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="a4a6f-132">然後勾選 [自動匯入 Maven 專案] 。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="a4a6f-133">開啟**Main.java**和取代 hello 現有程式碼區塊 hello 與下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-133">Open **Main.java** and replace hello existing code block with hello following code.</span></span> <span data-ttu-id="a4a6f-134">此外，提供參數中所呼叫 hello 程式碼片段，例如 hello 值**localFolderPath**， **_adlaAccountName**， **_adlsAccountName**， **_resourceGroupName**和取代的預留位置**用戶端識別碼**，**用戶端密碼**，**租用戶識別碼**，和**訂用帳戶 ID**。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-134">Also, provide hello values for parameters called out in hello code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="a4a6f-135">此程式碼會透過建立資料湖存放區與資料湖分析帳戶 hello 存放區中，建立檔案的 hello 程序執行作業、 取得作業狀態、 下載作業輸出和最後刪除 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-135">This code goes through hello process of creating Data Lake Store and Data Lake Analytics accounts, creating files in hello store, running a job, getting job status, downloading job output, and finally deleting hello account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a4a6f-136">目前沒有 hello Azure 資料湖服務的已知的問題。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-136">There is currently a known issue with hello Azure Data Lake Service.</span></span>  <span data-ttu-id="a4a6f-137">如果 hello 範例應用程式將會中斷或發生錯誤，您可能需要 toomanually 刪除 hello 資料湖存放區 （& s） Data Lake Analytics 帳戶 hello 指令碼會建立。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-137">If hello sample app is interrupted or encounters an error, you may need toomanually delete hello Data Lake Store & Data Lake Analytics accounts that hello script creates.</span></span>  <span data-ttu-id="a4a6f-138">如果您不熟悉 hello 入口網站，hello[管理 Azure Data Lake Analytics 使用 Azure 入口網站](data-lake-analytics-manage-use-portal.md)指南可協助您開始。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-138">If you're not familiar with hello Portal, hello [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
   >
   >

        package com.company;

        import com.microsoft.azure.CloudException;
        import com.microsoft.azure.credentials.ApplicationTokenCredentials;
        import com.microsoft.azure.management.datalake.store.*;
        import com.microsoft.azure.management.datalake.store.models.*;
        import com.microsoft.azure.management.datalake.analytics.*;
        import com.microsoft.azure.management.datalake.analytics.models.*;
        import com.microsoft.rest.credentials.ServiceClientCredentials;
        import java.io.*;
        import java.nio.charset.Charset;
        import java.nio.file.Files;
        import java.nio.file.Paths;
        import java.util.ArrayList;
        import java.util.UUID;
        import java.util.List;

        public class Main {
            private static String _adlsAccountName;
            private static String _adlaAccountName;
            private static String _resourceGroupName;
            private static String _location;

            private static String _tenantId;
            private static String _subId;
            private static String _clientId;
            private static String _clientSecret;

            private static DataLakeStoreAccountManagementClient _adlsClient;
            private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
            private static DataLakeAnalyticsAccountManagementClient _adlaClient;
            private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
            private static DataLakeAnalyticsCatalogManagementClient _adlaCatalogClient;

            public static void main(String[] args) throws Exception {
                _adlsAccountName = "<DATA-LAKE-STORE-NAME>";
                _adlaAccountName = "<DATA-LAKE-ANALYTICS-NAME>";
                _resourceGroupName = "<RESOURCE-GROUP-NAME>";
                _location = "East US 2";

                _tenantId = "<TENANT-ID>";
                _subId =  "<SUBSCRIPTION-ID>";
                _clientId = "<CLIENT-ID>";

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring hello application client secret, rather than hard-coding it in hello source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this tooany unused, new, empty folder on your local machine.

                // Authenticate
                ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
                SetupClients(creds);

                // Create Data Lake Store and Analytics accounts
                WaitForNewline("Authenticated.", "Creating NEW accounts.");
                CreateAccounts();
                WaitForNewline("Accounts created.", "Displaying accounts.");

                // List Data Lake Store and Analytics accounts that this app can access
                System.out.println(String.format("All ADL Store accounts that this app can access in subscription %s:", _subId));
                List<DataLakeStoreAccount> adlsListResult = _adlsClient.getAccountOperations().list().getBody();
                for (DataLakeStoreAccount acct : adlsListResult) {
                    System.out.println(acct.getName());
                }
                System.out.println(String.format("All ADL Analytics accounts that this app can access in subscription %s:", _subId));
                List<DataLakeAnalyticsAccount> adlaListResult = _adlaClient.getAccountOperations().list().getBody();
                for (DataLakeAnalyticsAccount acct : adlaListResult) {
                    System.out.println(acct.getName());
                }
                WaitForNewline("Accounts displayed.", "Creating files.");

                // Create a file in Data Lake Store: input1.csv
                // TODO: these change order in hello next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job tooData Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input too@\"/output1.csv\" USING Outputters.Csv();", "testJob");
                WaitForNewline("Job submitted.", "Getting job status.");

                // Wait for job completion and output job status
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                System.out.println("Waiting for job completion.");
                WaitForJob(jobId);
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output from Data Lake Store
                DownloadFile("/output1.csv", localFolderPath + "output1.csv");
                WaitForNewline("Job output downloaded.", "Deleting file.");

                // Delete file from Data Lake Store
                DeleteFile("/output1.csv");
                WaitForNewline("File deleted.", "Deleting account.");

                // Delete account
                _adlsClient.getAccountOperations().delete(_resourceGroupName, _adlsAccountName);
                _adlaClient.getAccountOperations().delete(_resourceGroupName, _adlaAccountName);
                WaitForNewline("Account deleted.", "DONE.");
            }

            //Set up clients
            public static void SetupClients(ServiceClientCredentials creds)
            {
                _adlsClient = new DataLakeStoreAccountManagementClientImpl(creds);
                _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClientImpl(creds);
                _adlaClient = new DataLakeAnalyticsAccountManagementClientImpl(creds);
                _adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);
                _adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClientImpl(creds);
                _adlsClient.setSubscriptionId(_subId);
                _adlaClient.setSubscriptionId(_subId);
            }

            // Helper function tooshow status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER toocontinue...");
                try{System.in.read();}
                catch(Exception e){}

                if (!nextAction.isEmpty())
                {
                    System.out.println(nextAction);
                }
            }

            // Create Data Lake Store and Analytics accounts
            public static void CreateAccounts() throws InterruptedException, CloudException, IOException {
                // Create ADLS account
                DataLakeStoreAccount adlsParameters = new DataLakeStoreAccount();
                adlsParameters.setLocation(_location);

                _adlsClient.getAccountOperations().create(_resourceGroupName, _adlsAccountName, adlsParameters);

                // Create ADLA account
                DataLakeStoreAccountInfo adlsInfo = new DataLakeStoreAccountInfo();
                adlsInfo.setName(_adlsAccountName);

                DataLakeStoreAccountInfoProperties adlsInfoProperties = new DataLakeStoreAccountInfoProperties();
                adlsInfo.setProperties(adlsInfoProperties);

                List<DataLakeStoreAccountInfo> adlsInfoList = new ArrayList<DataLakeStoreAccountInfo>();
                adlsInfoList.add(adlsInfo);

                DataLakeAnalyticsAccountProperties adlaProperties = new DataLakeAnalyticsAccountProperties();
                adlaProperties.setDataLakeStoreAccounts(adlsInfoList);
                adlaProperties.setDefaultDataLakeStoreAccount(_adlsAccountName);

                DataLakeAnalyticsAccount adlaParameters = new DataLakeAnalyticsAccount();
                adlaParameters.setLocation(_location);
                adlaParameters.setName(_adlaAccountName);
                adlaParameters.setProperties(adlaProperties);

                    /* If this line generates an error message like "hello deep update for property 'DataLakeStoreAccounts' is not supported", please delete hello ADLS and ADLA accounts via hello portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in hello next version of hello API
            public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException {
                byte[] bytesContents = contents.getBytes();

                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
            }

            public static void DeleteFile(String filePath) throws IOException, CloudException {
                _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
            }

            // Download file
            public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException {
                InputStream stream = _adlsFileSystemClient.getFileSystemOperations().open(srcPath, _adlsAccountName).getBody();

                PrintWriter pWriter = new PrintWriter(destPath, Charset.defaultCharset().name());

                String fileContents = "";
                if (stream != null) {
                    Writer writer = new StringWriter();

                    char[] buffer = new char[1024];
                    try {
                        Reader reader = new BufferedReader(
                                new InputStreamReader(stream, "UTF-8"));
                        int n;
                        while ((n = reader.read(buffer)) != -1) {
                            writer.write(buffer, 0, n);
                        }
                    } finally {
                        stream.close();
                    }
                    fileContents =  writer.toString();
                }

                pWriter.println(fileContents);
                pWriter.close();
            }

            // Submit a U-SQL job by providing script contents.
            // Returns hello job ID
            public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException {
                UUID jobId = java.util.UUID.randomUUID();
                USqlJobProperties properties = new USqlJobProperties();
                properties.setScript(script);
                JobInformation parameters = new JobInformation();
                parameters.setName(jobName);
                parameters.setJobId(jobId);
                parameters.setType(JobType.USQL);
                parameters.setProperties(properties);

                JobInformation jobInfo = _adlaJobClient.getJobOperations().create(_adlaAccountName, jobId, parameters).getBody();

                return jobId;
            }

            // Wait for job completion
            public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                while (jobInfo.getState() != JobState.ENDED)
                {
                    jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
                }
                return jobInfo.getResult();
            }

            // Get job status
            public static String GetJobStatus(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                return jobInfo.getState().toValue();
            }
        }

1. <span data-ttu-id="a4a6f-139">請遵循 hello 提示 toorun 和完整 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-139">Follow hello prompts toorun and complete hello application.</span></span>

## <a name="see-also"></a><span data-ttu-id="a4a6f-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a4a6f-140">See also</span></span>
* <span data-ttu-id="a4a6f-141">toosee hello 相同教學課程中使用其他工具中，按一下在 hello hello 頁面最上方的 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-141">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="a4a6f-142">toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-142">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="a4a6f-143">tooget 開始開發 U-SQL 應用程式，請參閱[使用 Data Lake Tools for Visual Studio 的開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-143">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="a4a6f-144">toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)，和[U SQL 語言參考](http://go.microsoft.com/fwlink/?LinkId=691348)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-144">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="a4a6f-145">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure 資料湖分析](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="a4a6f-146">tooget 的概觀的 Data Lake Analytics，請參閱[Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a4a6f-146">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
