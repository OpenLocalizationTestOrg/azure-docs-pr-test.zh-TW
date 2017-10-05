---
title: "Azure Mobile Engagement - 後端整合"
description: "連接 Azure Mobile Engagement 與 SharePoint 後端以從 SharePoint 建立行銷活動"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="d5655-103">Azure Mobile Engagement - API 整合</span><span class="sxs-lookup"><span data-stu-id="d5655-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="d5655-104">在自動化行銷系統中，建立及啟動行銷活動也會自動發生。</span><span class="sxs-lookup"><span data-stu-id="d5655-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="d5655-105">針對此目的 - Azure Mobile Engagement 也可以使用 API 建立這類自動化行銷活動。</span><span class="sxs-lookup"><span data-stu-id="d5655-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="d5655-106">通常客戶使用 Mobile Engagement 前端介面建立公告/投票等等做為其行銷活動的一部分。</span><span class="sxs-lookup"><span data-stu-id="d5655-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="d5655-107">不過隨著行銷活動成熟，就需要運用後端系統 (例如任何 CRM 系統或 CMS 系統，例如 SharePoint) 中鎖定的資料，以便建立完全自動化的管線，根據從後端系統傳送的資料，在 Mobile Engagement 中動態建立行銷活動。</span><span class="sxs-lookup"><span data-stu-id="d5655-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="d5655-108">本教學課程會逐步解說此類案例，其中 SharePoint 商務使用者會以行銷資料填入 SharePoint 清單，自動化程序會從清單挑選項目，並且使用可用的 REST API 與 Mobile Engagement 系統連線，以從 SharePoint 資料建立行銷活動。</span><span class="sxs-lookup"><span data-stu-id="d5655-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d5655-109">一般而言，您可以使用這個範例做為起點，了解如何呼叫任何 Mobile Engagement REST API，因為它詳細說明呼叫 API 的兩個重要層面 - 驗證和傳遞參數。</span><span class="sxs-lookup"><span data-stu-id="d5655-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="d5655-110">SharePoint 整合</span><span class="sxs-lookup"><span data-stu-id="d5655-110">SharePoint integration</span></span>
1. <span data-ttu-id="d5655-111">以下是範例 SharePoint 清單的類似外觀。</span><span class="sxs-lookup"><span data-stu-id="d5655-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="d5655-112">**標題**、**類別**、**NotificationTitle**、**訊息** 和 **URL** 是用來建立公告。</span><span class="sxs-lookup"><span data-stu-id="d5655-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="d5655-113">有稱為 **IsProcessed** 的資料行，由主控台程式形式的範例自動化程序使用。</span><span class="sxs-lookup"><span data-stu-id="d5655-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="d5655-114">您可以執行這個主控台程式做為 Azure WebJob，讓您可以排程至程式或直接使用 SharePoint 工作流程，在項目插入至 SharePoint 清單時建立和啟動公告。</span><span class="sxs-lookup"><span data-stu-id="d5655-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="d5655-115">在此範例中，我們使用主控台程式，會逐一進行 SharePoint 清單中的項目，並為每個項目在 Azure Mobile Engagement 中建立公告，最後於成功建立公告時將 **IsProcessed** 旗標標示為 true。</span><span class="sxs-lookup"><span data-stu-id="d5655-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="d5655-116">我們是從 *這裡* [使用用戶端物件模型在 SharePoint Online 中遠端驗證](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) 的程式碼，以使用 SharePoint 清單進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d5655-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="d5655-117">驗證之後，我們會重複執行清單項目，以找出任何新建立的項目 (其 **IsProcessed** = false)。</span><span class="sxs-lookup"><span data-stu-id="d5655-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="d5655-118">Mobile Engagement 整合</span><span class="sxs-lookup"><span data-stu-id="d5655-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="d5655-119">一旦我們找到需要處理的項目 - 我們會擷取必要的資訊以從清單項目建立公告，並且呼叫 `CreateAzMECampaign` 來建立它，然後呼叫 `ActivateAzMECampaign` 來啟動它。</span><span class="sxs-lookup"><span data-stu-id="d5655-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="d5655-120">這些基本上是 REST API 呼叫，呼叫至 Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="d5655-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="d5655-121">Mobile Engagement REST API **需要基本驗證配置授權 HTTP 標頭**，由 `ApplicationId` 和 `ApiKey` 組成，您可以從 Azure 入口網站取得。</span><span class="sxs-lookup"><span data-stu-id="d5655-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="d5655-122">請確定您使用的金鑰是來自 **api 金鑰** 區段，而不是來自 **sdk 金鑰** 區段。</span><span class="sxs-lookup"><span data-stu-id="d5655-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="d5655-123">度於建立公告類型行銷活動 - 參考 [文件](https://msdn.microsoft.com/library/azure/mt683750.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5655-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="d5655-124">您必須確定您指定行銷活動 `kind` 做為 *公告* 和 [裝載](https://msdn.microsoft.com/library/azure/mt683751.aspx) ，並將它傳遞為 FormUrlEncodedContent。</span><span class="sxs-lookup"><span data-stu-id="d5655-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="d5655-125">建立公告之後，您會在 Mobile Engagement 入口網站上看到如下的訊息 (請注意，State=Draft 和 Activated = N/A)</span><span class="sxs-lookup"><span data-stu-id="d5655-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="d5655-126">`CreateAzMECampaign` 會建立公告行銷活動，並將其識別碼傳回給呼叫端。</span><span class="sxs-lookup"><span data-stu-id="d5655-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="d5655-127">`ActivateAzMECampaign` 需要此識別碼做為參數來啟動行銷活動。</span><span class="sxs-lookup"><span data-stu-id="d5655-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="d5655-128">啟動公告之後，您會在 Mobile Engagement 入口網站上看到如下的訊息：</span><span class="sxs-lookup"><span data-stu-id="d5655-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="d5655-129">啟動行銷活動之後，滿足行銷活動準則的任何裝置上就能開始看到通知。</span><span class="sxs-lookup"><span data-stu-id="d5655-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="d5655-130">您也會發現標示為 IsProcessed = false 的清單項目在建立公告行銷活動之後已設定為 True。</span><span class="sxs-lookup"><span data-stu-id="d5655-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="d5655-131">此範例會建立簡單的公告行銷活動，指定大部分必要的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5655-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="d5655-132">您可以使用 [這裡](https://msdn.microsoft.com/library/azure/mt683751.aspx)的資訊，從入口網站視需要對此進行自訂。</span><span class="sxs-lookup"><span data-stu-id="d5655-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



