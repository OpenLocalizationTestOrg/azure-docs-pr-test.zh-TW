---
title: "aaaUsing.NET SDK tooaccess Azure Mobile Engagement 服務 Api"
description: "描述如何 toouse hello Mobile Engagement.NET SDK tooaccess Azure Mobile Engagement 服務 Api"
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
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>使用.NET SDK tooaccess Azure Mobile Engagement 服務 Api
Azure Mobile Engagement 會公開一組的 Api 您 toomanage 裝置，觸達/推送活動等 toointeract 使用這些 Api，我們也提供[Swagger 檔案](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json)您可以使用工具適用於您慣用的 toogenerate Sdk語言。 我們建議您使用 hello [AutoRest](https://github.com/Azure/AutoRest)工具 toogenerate 我們的 Swagger 檔案從您的 SDK。

> [!NOTE]
> hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。 如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。

我們也可以建立類似的方式可讓您 toointeract 使用這些 Api 的 C# 包裝函式的使用.NET SDK，而且不需要 toodo hello 驗證語彙基元交涉並重新整理自己。  

這個範例會透過步驟 toofollow toouse hello.NET SDK hello 組：

1. 首先，您需要 toosetup hello 驗證，使用您 Api 所述，hello Azure Active Directory[這裡](mobile-engagement-api-authentication.md#authentication)。 在這些步驟 hello 結束，您應該會有有效**SubscriptionId**， **TenantId**， **ApplicationId**和**密碼**。 
2. 我們將使用簡單的 Windows 主控台應用程式 toodemonstrate hello.NET SDK 與 hello 案例建立公告促銷活動的使用。 開啟 Visual Studio，建立 [主控台應用程式] 。   
3. 接下來您需要 toodownload hello 可做為.NET SDK **Microsoft Azure Engagement 管理程式庫**hello Nuget gallery 中[這裡](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/)。
   如果您要從 Visual Studio 安裝 hello Nuget，您需要您有核取標記為 hello tooensure**包含發行前版本**搜尋 hello 封裝時的選項：
   
    ![][1]
4. 在 [hello`Program.cs`檔案中加入下列命名空間的 hello:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. 接下來，您必須遵循進行驗證，我們將使用的常數，並與您建立 hello 公告促銷活動的 hello Mobile Engagement 應用程式互動的 toodefine hello:
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. 定義 hello`EngagementManagementClient`我們將會使用變數 toocall hello Mobile Engagement SDK 的方法：
   
        static EngagementManagementClient engagementClient; 
7. 新增下列 tooyour hello`Main`方法：
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. 定義下列方法會負責初始化 hello hello`EngagementManagementClient`第一次驗證，然後將本身關聯的計劃 toocreate hello 公告促銷活動的 hello Mobile Engagement 應用程式：
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > 請注意，您需要 toouse hello**應用程式資源名稱**hello AppName 參數的 hello Azure 管理入口網站中所定義。 
   > 
   > 
9. 最後，需要定義它會負責使用先前初始化 hello EngagementClient toocreate 簡單的 hello CreateCampaign 方法**AnyTime** & **為僅通知的**活動具有標題和訊息： 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. 在成功建立 hello 宣傳活動中，以執行的 hello 主控台應用程式，您會看到 hello 下列：
    
    **已成功建立活動識別碼 '159'，並且處於「草稿」狀態**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
