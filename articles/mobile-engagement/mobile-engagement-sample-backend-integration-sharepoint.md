---
title: "aaaAzure Mobile Engagement-後端整合"
description: "從 SharePoint 的 SharePoint 後端 toocreate 活動與連接 Azure Mobile Engagement"
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
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="f5c39-103">Azure Mobile Engagement - API 整合</span><span class="sxs-lookup"><span data-stu-id="f5c39-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="f5c39-104">在自動化行銷系統中，建立及啟動 hello 行銷活動，也會自動進行。</span><span class="sxs-lookup"><span data-stu-id="f5c39-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="f5c39-105">針對此目的 - Azure Mobile Engagement 也可以使用 API 建立這類自動化行銷活動。</span><span class="sxs-lookup"><span data-stu-id="f5c39-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="f5c39-106">通常客戶使用 hello Mobile Engagement 前端介面 toocreate 公告/輪詢等做為其行銷活動的一部分。</span><span class="sxs-lookup"><span data-stu-id="f5c39-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="f5c39-107">但是為 hello 行銷活動會變成成熟，還是需要 tooleverage hello 資料鎖定 hello （就像任何的 CRM 系統或 CMS 系統，例如 SharePoint） 的後端系統中，因此可以建立完全自動化的管線，可在行動中建立活動Engagement 動態 hello 後端系統從流程中的 hello 資料為基礎。</span><span class="sxs-lookup"><span data-stu-id="f5c39-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="f5c39-108">此教學課程會透過這類案例，SharePoint 清單行銷資料中的 SharePoint 商務使用者填入而且自動化程序會拾取 hello 清單中的項目，並與 hello Mobile Engagement 系統使用連接 hello 使用 REST Apitoocreate 行銷活動與 hello SharePoint 資料。</span><span class="sxs-lookup"><span data-stu-id="f5c39-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f5c39-109">一般情況下，您可以使用這個範例做為起點來了解如何 toocall 如同任何 Mobile Engagement REST API 詳細說明 hello 兩個重要的層面的呼叫 hello Api-正在驗證和傳遞的參數。</span><span class="sxs-lookup"><span data-stu-id="f5c39-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="f5c39-110">SharePoint 整合</span><span class="sxs-lookup"><span data-stu-id="f5c39-110">SharePoint integration</span></span>
1. <span data-ttu-id="f5c39-111">以下是何種 hello 範例 SharePoint 清單如下所示。</span><span class="sxs-lookup"><span data-stu-id="f5c39-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="f5c39-112">**標題**，**類別**， **NotificationTitle**，**訊息**和**URL**用來建立 hello 公告。</span><span class="sxs-lookup"><span data-stu-id="f5c39-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="f5c39-113">有稱為資料行是**IsProcessed** hello 自動化程序範例主控台程式 hello 形式會使用它。</span><span class="sxs-lookup"><span data-stu-id="f5c39-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="f5c39-114">您可以執行這個主控台程式 Azure webjob，讓您可以將它排程，或您可以直接使用 hello SharePoint 工作流程 tooprogram 建立和啟動 hello 公告項目插入至 hello SharePoint 清單時。</span><span class="sxs-lookup"><span data-stu-id="f5c39-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="f5c39-115">在此範例中，我們使用 hello 主控台程式會透過 hello hello SharePoint 中的項目清單，並為每個 Azure Mobile Engagement 建立公告，而且最後標示 hello **IsProcessed**旗標 toobe 則 true成功的通知建立。</span><span class="sxs-lookup"><span data-stu-id="f5c39-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="f5c39-116">我們使用 hello hello 範例中的程式碼*SharePoint Online 使用 hello 用戶端物件模型中的遠端驗證*[這裡](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c)tooauthenticate hello SharePoint 清單。</span><span class="sxs-lookup"><span data-stu-id="f5c39-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="f5c39-117">驗證之後，我們迴圈 hello 清單項目 toofind 出任何新建立的項目 (且其**IsProcessed** = false)。</span><span class="sxs-lookup"><span data-stu-id="f5c39-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="f5c39-118">Mobile Engagement 整合</span><span class="sxs-lookup"><span data-stu-id="f5c39-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="f5c39-119">一旦我們找到需要處理的項目-我們擷取所需的 hello 資訊 toocreate 從 hello 公告清單項目，並呼叫`CreateAzMECampaign`toocreate 它之後再`ActivateAzMECampaign`tooactivate 它。</span><span class="sxs-lookup"><span data-stu-id="f5c39-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="f5c39-120">這些是呼叫 toohello Mobile Engagement 後端基本上 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f5c39-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="f5c39-121">hello Mobile Engagement REST Api 需要**基本驗證配置的 HTTP 授權標頭**這組成 hello`ApplicationId`和 hello `ApiKey` hello Azure 入口網站中取得。</span><span class="sxs-lookup"><span data-stu-id="f5c39-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="f5c39-122">請確定您使用從 hello hello 金鑰**api 金鑰**區段和*不*從 hello **sdk 金鑰**> 一節。</span><span class="sxs-lookup"><span data-stu-id="f5c39-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="f5c39-123">建立的 hello 公告類型的活動，而 toohello[文件](https://msdn.microsoft.com/library/azure/mt683750.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f5c39-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="f5c39-124">您需要確定您要指定 hello 活動 toomake`kind`為*公告*和 hello[裝載](https://msdn.microsoft.com/library/azure/mt683751.aspx)並將它傳遞為 FormUrlEncodedContent。</span><span class="sxs-lookup"><span data-stu-id="f5c39-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
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
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
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
4. <span data-ttu-id="f5c39-125">一旦建立 hello 公告，您會看到類似下列 hello Mobile Engagement 入口網站上的 hello (請注意該 hello 狀態 = 草稿 」 和 「 已啟動 = n/A)</span><span class="sxs-lookup"><span data-stu-id="f5c39-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="f5c39-126">`CreateAzMECampaign`建立公告促銷活動，並傳回其 Id toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="f5c39-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="f5c39-127">`ActivateAzMECampaign`需要此識別碼做為 hello 參數 tooactivate hello 行銷活動。</span><span class="sxs-lookup"><span data-stu-id="f5c39-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
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
   
                // Send hello POST request
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
6. <span data-ttu-id="f5c39-128">一旦啟動 hello 公告，您會看到類似下列 hello hello Mobile Engagement 入口網站上：</span><span class="sxs-lookup"><span data-stu-id="f5c39-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="f5c39-129">一旦取得啟動 hello 行銷活動，同時滿足 hello 準則 hello 活動上的任何裝置就會開始看到通知。</span><span class="sxs-lookup"><span data-stu-id="f5c39-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="f5c39-130">您也會發現該 hello 清單項目標示 IsProcessed = false 已設定 tooTrue 建立 hello 公告活動之後。</span><span class="sxs-lookup"><span data-stu-id="f5c39-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="f5c39-131">這個範例會建立指定大部分 hello 所需內容的簡單宣告活動。</span><span class="sxs-lookup"><span data-stu-id="f5c39-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="f5c39-132">您可以自訂這個就像您可以從 hello 入口網站使用 hello 資訊[這裡](https://msdn.microsoft.com/library/azure/mt683751.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f5c39-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



