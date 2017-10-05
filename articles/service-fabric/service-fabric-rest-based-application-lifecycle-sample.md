---
title: "REST 應用程式生命週期範例 | Microsoft Docs"
description: "Microsoft Azure Service Fabric 範例，其中示範使用 Service Fabric REST 介面顯示應用程式生命週期。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 0a374e53-ff23-4ee8-8cc6-259d41e118e7
ms.service: service-fabric
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/2/2016
ms.author: ryanwi
redirect_url: /rest/api/servicefabric/
ms.openlocfilehash: e0c744c4784deb2ce21abcb9b7e012a38b6d16a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="rest-based-application-lifecycle-sample"></a><span data-ttu-id="edabf-103">REST 架構應用程式生命週期範例</span><span class="sxs-lookup"><span data-stu-id="edabf-103">REST-based application lifecycle sample</span></span>
<span data-ttu-id="edabf-104">這個範例會透過 REST API 呼叫示範 Service Fabric 應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="edabf-104">This sample demonstrates the Service Fabric application lifecycle through REST API calls.</span></span> <span data-ttu-id="edabf-105">如需 Service Fabric 應用程式生命週期的詳細資訊，請參閱 [Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="edabf-105">For more information on the Service Fabric application lifecycle, see [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

<span data-ttu-id="edabf-106">這個範例會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="edabf-106">This sample performs the following:</span></span>

* <span data-ttu-id="edabf-107">佈建映像存放區中之 WordCount 應用程式封裝的 **WordCount 1.0.0** 範例。</span><span class="sxs-lookup"><span data-stu-id="edabf-107">Provisions the **WordCount 1.0.0** sample from the WordCount application package in the image store.</span></span>
* <span data-ttu-id="edabf-108">顯示包含 WordCount 1.0.0 的應用程式類型清單。</span><span class="sxs-lookup"><span data-stu-id="edabf-108">Displays the list of application types, which includes WordCount 1.0.0.</span></span>
* <span data-ttu-id="edabf-109">將 WordCount 應用程式建立為 **fabric:/WordCount**。</span><span class="sxs-lookup"><span data-stu-id="edabf-109">Creates the WordCount application as **fabric:/WordCount**.</span></span>
* <span data-ttu-id="edabf-110">顯示包含 fabric:/WordCount 1.0.0 版的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="edabf-110">Displays the list of applications, which includes fabric:/WordCount version 1.0.0.</span></span>
* <span data-ttu-id="edabf-111">佈建映像存放區中之 **WordCountUpgrade** 應用程式封裝的 1.1.0 版 WordCount 範例。</span><span class="sxs-lookup"><span data-stu-id="edabf-111">Provisions the 1.1.0 version of the WordCount sample from the **WordCountUpgrade** application package in the image store.</span></span>
* <span data-ttu-id="edabf-112">顯示包含 WordCount 1.0.0 與 **WordCount 1.1.0**的應用程式類型清單。</span><span class="sxs-lookup"><span data-stu-id="edabf-112">Displays the list of application types, which includes both WordCount 1.0.0 and **WordCount 1.1.0**.</span></span>
* <span data-ttu-id="edabf-113">將 WordCount 應用程式升級為 1.1.0 版。</span><span class="sxs-lookup"><span data-stu-id="edabf-113">Upgrades the WordCount application to version 1.1.0.</span></span>
* <span data-ttu-id="edabf-114">顯示包含 WordCount 1.1.0 版，但不再包含 WordCount 1.0.0 版的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="edabf-114">Displays the list of applications, which includes WordCount version 1.1.0, but no longer includes WordCount version 1.0.0.</span></span>
* <span data-ttu-id="edabf-115">刪除 WordCount 應用程式。</span><span class="sxs-lookup"><span data-stu-id="edabf-115">Deletes the WordCount application.</span></span>
* <span data-ttu-id="edabf-116">顯示不再包含 fabric:/WordCount 的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="edabf-116">Displays the list of applications, which no longer includes fabric:/WordCount.</span></span>
* <span data-ttu-id="edabf-117">解除佈建 WordCount 1.1.0 版範例。</span><span class="sxs-lookup"><span data-stu-id="edabf-117">Unprovisions the 1.1.0 version of the WordCount sample.</span></span>
* <span data-ttu-id="edabf-118">顯示包含 WordCount 1.0.0，但不再包含 WordCount 1.1.0 的應用程式類型清單。</span><span class="sxs-lookup"><span data-stu-id="edabf-118">Displays the list of application types, which includes WordCount 1.0.0, but no longer includes WordCount 1.1.0.</span></span>
* <span data-ttu-id="edabf-119">解除佈建 WordCount 1.0.0 版範例。</span><span class="sxs-lookup"><span data-stu-id="edabf-119">Unprovisions the 1.0.0 version of the WordCount sample.</span></span>
* <span data-ttu-id="edabf-120">顯示不再包含 WordCount 的應用程式類型清單。</span><span class="sxs-lookup"><span data-stu-id="edabf-120">Displays the list of application types, which no longer includes WordCount.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edabf-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="edabf-121">Prerequisites</span></span>
<span data-ttu-id="edabf-122">此範例使用 [WordCount 範本](http://aka.ms/servicefabricsamples) (可在 **入門** 範本中找到)。</span><span class="sxs-lookup"><span data-stu-id="edabf-122">This sample uses the [WordCount sample](http://aka.ms/servicefabricsamples) (found in the **Getting Started** samples).</span></span> <span data-ttu-id="edabf-123">必須先建置 WordCount 範例，再兩個應用程式封裝複製到映像存放區。</span><span class="sxs-lookup"><span data-stu-id="edabf-123">The WordCount sample must be built first, and then two application packages must be copied to the image store.</span></span>

| <span data-ttu-id="edabf-124">資料夾</span><span class="sxs-lookup"><span data-stu-id="edabf-124">Folder</span></span> | <span data-ttu-id="edabf-125">說明</span><span class="sxs-lookup"><span data-stu-id="edabf-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="edabf-126">WordCount</span><span class="sxs-lookup"><span data-stu-id="edabf-126">WordCount</span></span> |<span data-ttu-id="edabf-127">WordCount 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="edabf-127">The WordCount sample application.</span></span> <span data-ttu-id="edabf-128">**ApplicationManifest.xml** 檔案中有 **ApplicationTypeVersion ="1.0.0"**。</span><span class="sxs-lookup"><span data-stu-id="edabf-128">The **ApplicationManifest.xml** file contains **ApplicationTypeVersion="1.0.0"**.</span></span> |
| <span data-ttu-id="edabf-129">WordCountUpgrade</span><span class="sxs-lookup"><span data-stu-id="edabf-129">WordCountUpgrade</span></span> |<span data-ttu-id="edabf-130">WordCount 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="edabf-130">The WordCount sample application.</span></span> <span data-ttu-id="edabf-131">ApplicationManifest.xml 檔案必須變更為 **ApplicationTypeVersion ="1.1.0"** ，應用程式才能升級。</span><span class="sxs-lookup"><span data-stu-id="edabf-131">The ApplicationManifest.xml file must be changed to **ApplicationTypeVersion="1.1.0"** to allow the application upgrade to occur.</span></span> |

<span data-ttu-id="edabf-132">若要建立應用程式封裝，並將其複製到映像存放區，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="edabf-132">To create the application packages and copy them to the image store, take the following steps:</span></span>

1. <span data-ttu-id="edabf-133">將 **C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug** 複製到 **C:\Temp\WordCount**。</span><span class="sxs-lookup"><span data-stu-id="edabf-133">Copy **C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug** to **C:\Temp\WordCount**.</span></span> <span data-ttu-id="edabf-134">即會建立 WordCount 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="edabf-134">This creates the WordCount application package.</span></span>
2. <span data-ttu-id="edabf-135">將 C:\Temp\WordCount 複製到 **C:\Temp\WordCountUpgrade**。</span><span class="sxs-lookup"><span data-stu-id="edabf-135">Copy C:\Temp\WordCount to **C:\Temp\WordCountUpgrade**.</span></span> <span data-ttu-id="edabf-136">這會建立 **WordCountUpgrade** 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="edabf-136">This creates the **WordCountUpgrade application** package.</span></span>
3. <span data-ttu-id="edabf-137">在文字編輯器中，開啟 **C:\Temp\WordCountUpgrade\ApplicationManifest.xml**。</span><span class="sxs-lookup"><span data-stu-id="edabf-137">Open **C:\Temp\WordCountUpgrade\ApplicationManifest.xml** in a text editor.</span></span>
4. <span data-ttu-id="edabf-138">在 **ApplicationManifest** 項目中，將 **ApplicationTypeVersion** 屬性變更為 **"1.1.0"**。</span><span class="sxs-lookup"><span data-stu-id="edabf-138">In the **ApplicationManifest** element, change the **ApplicationTypeVersion** attribute to **"1.1.0"**.</span></span>  <span data-ttu-id="edabf-139">即會更新應用程式的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="edabf-139">This updates the version number of the application.</span></span>
5. <span data-ttu-id="edabf-140">儲存已變更的 ApplicationManifest.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="edabf-140">Save the changed ApplicationManifest.xml file.</span></span>
6. <span data-ttu-id="edabf-141">以系統管理員身分執行下列 PowerShell 指令碼，將應用程式複製到映像存放區：</span><span class="sxs-lookup"><span data-stu-id="edabf-141">Run the following PowerShell script as an administrator to copy the applications to the image store:</span></span>

```powershell
# Deploy the WordCount and upgrade applications
$applicationPathWordCount = "C:\Temp\WordCount"
$applicationPathUpgrade = "C:\Temp\WordCountUpgrade"

# LOCAL:
$imageStoreConnection = "file:C:\SfDevCluster\Data\ImageStoreShare"
$cluster = 'localhost:19000'

Connect-ServiceFabricCluster $cluster

Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $applicationPathWordCount -ImageStoreConnectionString $imageStoreConnection
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $applicationPathUpgrade -ImageStoreConnectionString $imageStoreConnection
```

<span data-ttu-id="edabf-142">當 PowerShell 指令碼完成時，應用程式也已就緒，可以開始執行的。</span><span class="sxs-lookup"><span data-stu-id="edabf-142">When the PowerShell script finishes, this application is ready to run.</span></span>

## <a name="example"></a><span data-ttu-id="edabf-143">範例</span><span class="sxs-lookup"><span data-stu-id="edabf-143">Example</span></span>
<span data-ttu-id="edabf-144">下列範例示範 Service Fabric 應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="edabf-144">The following example demonstrates the Service Fabric application lifecycle.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Fabric.Health;
using System.Fabric.Query;
using System.IO;
using System.Net;
using System.Text;
using System.Web.Script.Serialization;

namespace ServiceFabricRestCaller
{
    class Program
    {
        static void Main(string[] args)
        {
            Uri clusterUri = new Uri("http://localhost:19080");
            string buildPathApplication = "WordCount";
            string applicationVersionNumber = "1.0.0";
            string buildPathUpgrade = "WordCountUpgrade";
            string updateVersionNumber = "1.1.0";

            Console.WriteLine("\nProvision the 1.0.0 WordCount application for the first time.");
            ProvisionAnApplication(clusterUri, buildPathApplication);
            Console.WriteLine("\nPress Enter to get the list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet the list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter to create the fabric:/WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nCreate the fabric:/WordCount application.");
            CreateApplication(clusterUri);
            Console.WriteLine("\nPress Enter to get the list of applications: ");
            Console.ReadLine();


            Console.WriteLine("\nGet the list of applications.");
            GetApplicationList(clusterUri);
            Console.WriteLine("\nPress Enter to provision the 1.1.0 upgrade to the WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nProvision the 1.1.0 upgrade to the WordCount application.");
            ProvisionAnApplication(clusterUri, buildPathUpgrade);
            Console.WriteLine("\nPress Enter to get the list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet the list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter to upgrade the fabric:/WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nUpgrade the fabric:/WordCount application.");
            UpgradeApplicationByApplicationType(clusterUri);
            Console.WriteLine("\nPress Enter to get the list of applications: ");
            Console.ReadLine();


            Console.WriteLine("\nGet the list of applications.");
            GetApplicationList(clusterUri);
            Console.WriteLine("\nPress Enter to delete the fabric:/WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nDelete the fabric:/WordCount application.");
            DeleteApplication(clusterUri);
            Console.WriteLine("\nPress Enter to get the list of applications: ");
            Console.ReadLine();


            Console.WriteLine("\nGet the list of applications.");
            GetApplicationList(clusterUri);
            Console.WriteLine("\nPress Enter to unprovision the WordCount 1.1.0 application: ");
            Console.ReadLine();


            Console.WriteLine("\nUnprovision the WordCount 1.1.0 application.");
            UnprovisionAnApplication(clusterUri, updateVersionNumber);
            Console.WriteLine("\nPress Enter to get the list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet the list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter to unprovision the WordCount 1.0.0 application: ");
            Console.ReadLine();


            Console.WriteLine("\nUnprovision the WordCount 1.0.0 application.");
            UnprovisionAnApplication(clusterUri, applicationVersionNumber);
            Console.WriteLine("\nPress Enter to get the final list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet the final list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter to end this program: ");
            Console.ReadLine();
        }

        #region Classes

        /// <summary>
        /// Class similar to ApplicationType. Designed for use with JavaScriptSerializer.
        /// </summary>
        public class AppType
        {
            public string Name { get; set; }
            public string Version { get; set; }
            public List<ApplicationParameter> DefaultParameterList { get; set; }
        }

        /// <summary>
        /// Class designed for use with JavaScriptSerializer.
        /// </summary>
        public class ApplicationInfo
        {
            public string Id { get; set; }
            public string Name { get; set; }
            public string TypeName { get; set; }
            public string TypeVersion { get; set; }
            public ApplicationStatus Status { get; set; }
            public List<Parameter> Parameters { get; set; }
            public HealthState HealthState { get; set; }
        }

        /// <summary>
        /// Class similar to Parameter. Designed for use with JavaScriptSerializer.
        /// </summary>
        public class Parameter
        {
            public string Name { get; set; }
            public string Value { get; set; }
        }

        #endregion


        #region Get List of Application Types (REST API)

        /// <summary>
        /// Gets the list of application types.
        /// </summary>
        /// <param name="clusterUri">The URI to access the cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool GetListOfApplicationTypes(Uri clusterUri)
        {
            // String to capture the response stream.
            string responseString = string.Empty;

            // Create the request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/ApplicationTypes?api-version={0}",
            "1.0"));    // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "GET";

            // Execute the request and obtain the response.
            try
            {
                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    using (StreamReader streamReader = new StreamReader(response.GetResponseStream(), true))
                    {
                        // Capture the response string.
                        responseString = streamReader.ReadToEnd();
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display the error message.
                Console.WriteLine("Error getting the list of application types:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            // Deserialize the response string.
            JavaScriptSerializer jss = new JavaScriptSerializer();
            List<AppType> applicationTypes = jss.Deserialize<List<AppType>>(responseString);

            // Display application type information for each application type.
            Console.WriteLine("Application types:");
            foreach (AppType applicationType in applicationTypes)
            {
                Console.WriteLine("  Application Type:");
                Console.WriteLine("    Name: " + applicationType.Name);
                Console.WriteLine("    Version: " + applicationType.Version);
                Console.WriteLine("    Default Parameter List:");

                foreach (var parameter in applicationType.DefaultParameterList)
                {
                    Console.WriteLine("      Name: " + parameter.Name);
                    Console.WriteLine("      Value: " + parameter.Value);
                }
            }

            return true;
        }

        #endregion


        #region Provision an Application (REST API)

        /// <summary>
        /// Provisions an application to the image store.
        /// </summary>
        /// <param name="clusterUri">The URI to access the cluster.</param>
        /// <param name="applicationTypeBuildPath">The application type build path ("WordCount" or "WordCountUpgrade").</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool ProvisionAnApplication(Uri clusterUri, string applicationTypeBuildPath)
        {
            // Create the request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/ApplicationTypes/$/Provision?api-version={0}",
                "1.0"));    // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "POST";
            request.ContentType = "application/json; charset=utf-8";

            // Create the byte array that will become the request body.
            string requestBody = "{\"ApplicationTypeBuildPath\":\"" + applicationTypeBuildPath + "\"}";
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Stores the response status code.
            HttpStatusCode statusCode;

            // Create the request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute the request and obtain the response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display the error message.
                Console.WriteLine("Error provisioning the application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Provision an Application response status = " + statusCode.ToString());
            return true;
        }

        #endregion

        #region Unprovision an Application (REST API)

        /// <summary>
        /// Unprovisions an application.
        /// </summary>
        /// <param name="clusterUri">The URI to access the cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool UnprovisionAnApplication(Uri clusterUri, string versionToUnprovision)
        {
            // Create the request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/ApplicationTypes/{0}/$/Unprovision?api-version={1}",
                "WordCount",     // Application Type Name
                "1.0"));            // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "POST";
            request.ContentType = "application/json; charset=utf-8";

            // Stores the response status code.
            HttpStatusCode statusCode;

            // Create the byte array that will become the request body.
            string requestBody = "{\"ApplicationTypeVersion\":\"" + versionToUnprovision + "\"}";
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Create the request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute the request and obtain the response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display the error message.
                Console.WriteLine("Error unprovisioning the application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Unprovision an Application response status = " + statusCode.ToString());
            return true;
        }

        #endregion

        #region Get Application List (REST API)

        /// <summary>
        /// Gets the list of applications.
        /// </summary>
        /// <param name="clusterUri">The URI to access the cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool GetApplicationList(Uri clusterUri)
        {
            // String to capture the response stream.
            string responseString = string.Empty;

            // Create the request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/Applications?api-version={0}",
                "1.0")); // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "GET";

            // Execute the request and obtain the response.
            try
            {
                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    using (StreamReader streamReader = new StreamReader(response.GetResponseStream(), true))
                    {
                        // Capture the response string.
                        responseString = streamReader.ReadToEnd();
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display the error message.
                Console.WriteLine("Error getting the application list:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }


            // Deserialize the response string.
            JavaScriptSerializer jss = new JavaScriptSerializer();
            List<ApplicationInfo> applicationInfos = jss.Deserialize<List<ApplicationInfo>>(responseString);

            // Display some application information for each application.
            Console.WriteLine("Application List:");
            foreach (ApplicationInfo applicationInfo in applicationInfos)
            {
                Console.WriteLine("  Application:");
                Console.WriteLine("    Id: " + applicationInfo.Id);
                Console.WriteLine("    Name: " + applicationInfo.Name);
                Console.WriteLine("    TypeName: " + applicationInfo.TypeName);
                Console.WriteLine("    TypeVersion: " + applicationInfo.TypeVersion);
                Console.WriteLine("    Status: " + applicationInfo.Status);
                Console.WriteLine("    HealthState: " + applicationInfo.HealthState);

                Console.WriteLine("    Parameters:");

                foreach (Parameter parameter in applicationInfo.Parameters)
                {
                    Console.WriteLine("      Parameter:");
                    Console.WriteLine("        Name: " + parameter.Name);
                    Console.WriteLine("        Value: " + parameter.Value);
                }
            }

            return true;
        }

        #endregion

        #region Create Application (REST API)

        /// <summary>
        /// Creates an application.
        /// </summary>
        /// <param name="clusterUri">The URI to access the cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool CreateApplication(Uri clusterUri)
        {
            // String to capture the response stream.
            string responseString = string.Empty;

            // Stores the response status code.
            HttpStatusCode statusCode;

            // Create the request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/Applications/$/Create?api-version={0}",
                "1.0"));    // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.ContentType = "text/json";
            request.Method = "POST";

            // Create the byte array that will become the request body.
            string requestBody = "{\"Name\":\"fabric:/WordCount\"," +
                                    "\"TypeName\":\"WordCount\"," +
                                    "\"TypeVersion\":\"1.0.0\"," +
                                    "\"ParameterList\":[]}";
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Create the request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute the request and obtain the response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display the error message.
                Console.WriteLine("Error creating application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Create Application response status = " + statusCode.ToString());

            return true;
        }

        #endregion


        #region Delete Application (REST API)

        /// <summary>
        /// Deletes an application.
        /// </summary>
        /// <param name="clusterUri">The URI to access the cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool DeleteApplication(Uri clusterUri)
        {
            // Create the request and add URL parameters.
            Uri requestUri = new Uri(clusterUri,
                string.Format("/Applications/{0}/$/Delete?api-version={1}",
                "WordCount",    // Application Name
                "1.0"));        // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "POST";
            request.ContentLength = 0;

            // Stores the response status code.
            HttpStatusCode statusCode;

            // Execute the request and obtain the response.
            try
            {
                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    statusCode = response.StatusCode;
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display the error message.
                Console.WriteLine("Error deleting application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Delete Application response status = " + statusCode.ToString());

            return true;
        }

        #endregion

        #region Upgrade Application by Application Type (REST API)

        /// <summary>
        /// Upgrades an application by application type.
        /// </summary>
        /// <param name="clusterUri">The URI to access the cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool UpgradeApplicationByApplicationType(Uri clusterUri)
        {
            // String to capture the response stream.
            string responseString = string.Empty;

            // Stores the response status code.
            HttpStatusCode statusCode;

            // Create the request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/Applications/{0}/$/Upgrade?api-version={1}",
                "WordCount",     // Application Name
                "1.0"));                // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.ContentType = "text/json";
            request.Method = "POST";


            // Create the Health Policy.
            string requestBody = "{\"Name\":\"fabric:/WordCount\"," +
                                    "\"TargetApplicationTypeVersion\":\"1.1.0\"," +
                                    "\"Parameters\":[]," +
                                    "\"UpgradeKind\":1," +
                                    "\"RollingUpgradeMode\":1," +
                                    "\"UpgradeReplicaSetCheckTimeoutInSeconds\":5," +
                                    "\"ForceRestart\":true," +
                                    "\"MonitoringPolicy\":" +
                                    "{\"FailureAction\":1," +
                                    "\"HealthCheckWaitDurationInMilliseconds\":\"5000\"," +
                                    "\"HealthCheckStableDurationInMilliseconds\":\"10000\"," +
                                    "\"HealthCheckRetryTimeoutInMilliseconds\":\"20000\"," +
                                    "\"UpgradeTimeoutInMilliseconds\":\"60000\"," +
                                    "\"UpgradeDomainTimeoutInMilliseconds\":\"30000\"}}";

            // Create the byte array that will become the request body.
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Create the request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute the request and obtain the response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display the error message.
                Console.WriteLine("Error upgrading application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Update Application response status = " + statusCode.ToString());

            return true;
        }

        #endregion
    }
}
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="edabf-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="edabf-145">Next steps</span></span>
[<span data-ttu-id="edabf-146">Service Fabric 應用程式生命週期</span><span class="sxs-lookup"><span data-stu-id="edabf-146">Service Fabric application lifecycle</span></span>](service-fabric-application-lifecycle.md)

