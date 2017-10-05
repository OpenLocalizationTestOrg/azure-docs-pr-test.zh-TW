---
title: "使用 .NET SDK 存取 Azure Mobile Engagement 服務 API"
description: "描述如何使用 Mobile Engagement .NET SDK 存取 Azure Mobile Engagement 服務 API"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a497189268c5a1b7e269cc57904ebc77c1906fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-net-sdk-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="d8a83-103">使用 .NET SDK 存取 Azure Mobile Engagement 服務 API</span><span class="sxs-lookup"><span data-stu-id="d8a83-103">Using .NET SDK to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="d8a83-104">Azure Mobile Engagement 公開一組 API，讓您可以管理裝置、觸達/推送活動等。若要與這些 API 互動，我們也提供您 [Swagger 檔案](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json)，可以與工具搭配使用來針對您慣用的語言產生 SDK。</span><span class="sxs-lookup"><span data-stu-id="d8a83-104">Azure Mobile Engagement exposes a set of APIs for you to manage Devices, Reach/Push campaigns etc. To interact with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="d8a83-105">我們建議使用 [AutoRest](https://github.com/Azure/AutoRest) 工具從我們的 Swagger 檔案產生 SDK。</span><span class="sxs-lookup"><span data-stu-id="d8a83-105">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="d8a83-106">Azure Mobile Engagement 服務將於 2018 年 3 月淘汰，目前僅供現有客戶使用。</span><span class="sxs-lookup"><span data-stu-id="d8a83-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="d8a83-107">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="d8a83-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="d8a83-108">我們已經以類似的方式建立 .NET SDK，可讓您使用 C# 包裝函式與這些 API 互動，且您不需要自行執行驗證權杖交涉和重新整理。</span><span class="sxs-lookup"><span data-stu-id="d8a83-108">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="d8a83-109">這個範例逐步說明使用 .NET SDK 所遵循的一組步驟：</span><span class="sxs-lookup"><span data-stu-id="d8a83-109">This sample goes through the set of steps to follow to use the .NET SDK:</span></span>

1. <span data-ttu-id="d8a83-110">首先，您必須使用 Azure Active Directory 為您的 API 設定驗證，如 [這裡](mobile-engagement-api-authentication.md#authentication)所述。</span><span class="sxs-lookup"><span data-stu-id="d8a83-110">First of all, you need to setup the authentication for your APIs using the Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="d8a83-111">在這些步驟的結尾，您應該會有有效的 **SubscriptionId**、**TenantId**、**ApplicationId** 和 **Secret**。</span><span class="sxs-lookup"><span data-stu-id="d8a83-111">At the end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="d8a83-112">我們將使用簡單的 Windows 主控台應用程式，示範使用 .NET SDK 建立公告行銷活動的案例。</span><span class="sxs-lookup"><span data-stu-id="d8a83-112">We will use a simple Windows Console app to demonstrate working with the .NET SDK with the scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="d8a83-113">開啟 Visual Studio，建立 [主控台應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="d8a83-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="d8a83-114">接下來您必須下載 .NET SDK，它在 Nuget 資源庫 ( **這裡** ) 中以 [Microsoft Azure Engagement Management Library (Microsoft Azure Engagement 管理資源庫)](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/)提供。</span><span class="sxs-lookup"><span data-stu-id="d8a83-114">Next you need to download the .NET SDK which is available as **Microsoft Azure Engagement Management Library** in the Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="d8a83-115">如果您要從 Visual Studio 安裝 Nuget，搜尋套件時必須確定已選取標示 [包括發行前版本]  的選項：</span><span class="sxs-lookup"><span data-stu-id="d8a83-115">If you are installing the Nuget from Visual Studio, you need to ensure that you have check marked the **Include prerelease** option while searching for the package:</span></span>
   
    ![][1]
4. <span data-ttu-id="d8a83-116">在 `Program.cs` 檔案中，加入下列命名空間：</span><span class="sxs-lookup"><span data-stu-id="d8a83-116">In the `Program.cs` file, add the following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="d8a83-117">接著您必須定義以下常數，我們將用來驗證您正在建立公告行銷活動之 Mobile Engagement 應用程式並與其互動：</span><span class="sxs-lookup"><span data-stu-id="d8a83-117">Next you need to define the following constants that we will use for authentication and interacting with the Mobile Engagement App in which you are creating the Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is the Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using the one as specified in the Azure portal (NOT the App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="d8a83-118">定義我們將用來呼叫 Mobile Engagement SDK 方法的 `EngagementManagementClient` 變數：</span><span class="sxs-lookup"><span data-stu-id="d8a83-118">Define the `EngagementManagementClient` variable which we will use to call the Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="d8a83-119">在您的 `Main` 方法加入以下內容：</span><span class="sxs-lookup"><span data-stu-id="d8a83-119">Add the following to your `Main` method:</span></span>
   
        try
            {
                // Initialize the Engagement SDK to call out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="d8a83-120">定義下列處理初始化 `EngagementManagementClient` 的方法，方法是先進行驗證，然後將其本身與您打算建立公告行銷活動的 Mobile Engagement 應用程式關聯：</span><span class="sxs-lookup"><span data-stu-id="d8a83-120">Define the following method which takes care of initializing the `EngagementManagementClient` by first authenticating and then associating itself with the Mobile Engagement App in which you plan to create the Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is the Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create the campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="d8a83-121">請注意，您必須使用 Azure 管理入口網站中針對 AppName 參數定義的 **應用程式資源名稱** 。</span><span class="sxs-lookup"><span data-stu-id="d8a83-121">Note that you need to use the **App Resource Name** as defined in the Azure management portal for the AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="d8a83-122">最後，定義 CreateCampaign 方法，它會負責使用先前初始化的 EngagementClient 來建立含有標題和訊息的簡單**隨時** &  **僅通知**活動：</span><span class="sxs-lookup"><span data-stu-id="d8a83-122">Lastly, define the CreateCampaign method which will take care of using the previously initialized EngagementClient to create a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer to the Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all the non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing the app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer to the Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="d8a83-123">執行主控台應用程式，在成功建立活動後您將會看到以下訊息：</span><span class="sxs-lookup"><span data-stu-id="d8a83-123">Run the console app and you will see the following on successful creation of the campaign:</span></span>
    
    <span data-ttu-id="d8a83-124">**已成功建立活動識別碼 '159'，並且處於「草稿」狀態**</span><span class="sxs-lookup"><span data-stu-id="d8a83-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
