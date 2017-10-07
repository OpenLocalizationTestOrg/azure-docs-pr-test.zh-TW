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
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement - API 整合
在自動化行銷系統中，建立及啟動 hello 行銷活動，也會自動進行。 針對此目的 - Azure Mobile Engagement 也可以使用 API 建立這類自動化行銷活動。 

通常客戶使用 hello Mobile Engagement 前端介面 toocreate 公告/輪詢等做為其行銷活動的一部分。 但是為 hello 行銷活動會變成成熟，還是需要 tooleverage hello 資料鎖定 hello （就像任何的 CRM 系統或 CMS 系統，例如 SharePoint） 的後端系統中，因此可以建立完全自動化的管線，可在行動中建立活動Engagement 動態 hello 後端系統從流程中的 hello 資料為基礎。 

![][5]

此教學課程會透過這類案例，SharePoint 清單行銷資料中的 SharePoint 商務使用者填入而且自動化程序會拾取 hello 清單中的項目，並與 hello Mobile Engagement 系統使用連接 hello 使用 REST Apitoocreate 行銷活動與 hello SharePoint 資料。 

> [!IMPORTANT]
> 一般情況下，您可以使用這個範例做為起點來了解如何 toocall 如同任何 Mobile Engagement REST API 詳細說明 hello 兩個重要的層面的呼叫 hello Api-正在驗證和傳遞的參數。 
> 
> 

## <a name="sharepoint-integration"></a>SharePoint 整合
1. 以下是何種 hello 範例 SharePoint 清單如下所示。 **標題**，**類別**， **NotificationTitle**，**訊息**和**URL**用來建立 hello 公告。 有稱為資料行是**IsProcessed** hello 自動化程序範例主控台程式 hello 形式會使用它。 您可以執行這個主控台程式 Azure webjob，讓您可以將它排程，或您可以直接使用 hello SharePoint 工作流程 tooprogram 建立和啟動 hello 公告項目插入至 hello SharePoint 清單時。 在此範例中，我們使用 hello 主控台程式會透過 hello hello SharePoint 中的項目清單，並為每個 Azure Mobile Engagement 建立公告，而且最後標示 hello **IsProcessed**旗標 toobe 則 true成功的通知建立。
   
    ![][1]
2. 我們使用 hello hello 範例中的程式碼*SharePoint Online 使用 hello 用戶端物件模型中的遠端驗證*[這裡](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c)tooauthenticate hello SharePoint 清單。
3. 驗證之後，我們迴圈 hello 清單項目 toofind 出任何新建立的項目 (且其**IsProcessed** = false)。 
   
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

## <a name="mobile-engagement-integration"></a>Mobile Engagement 整合
1. 一旦我們找到需要處理的項目-我們擷取所需的 hello 資訊 toocreate 從 hello 公告清單項目，並呼叫`CreateAzMECampaign`toocreate 它之後再`ActivateAzMECampaign`tooactivate 它。 這些是呼叫 toohello Mobile Engagement 後端基本上 REST API 呼叫。 
2. hello Mobile Engagement REST Api 需要**基本驗證配置的 HTTP 授權標頭**這組成 hello`ApplicationId`和 hello `ApiKey` hello Azure 入口網站中取得。 請確定您使用從 hello hello 金鑰**api 金鑰**區段和*不*從 hello **sdk 金鑰**> 一節。 
   
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
3. 建立的 hello 公告類型的活動，而 toohello[文件](https://msdn.microsoft.com/library/azure/mt683750.aspx)。 您需要確定您要指定 hello 活動 toomake`kind`為*公告*和 hello[裝載](https://msdn.microsoft.com/library/azure/mt683751.aspx)並將它傳遞為 FormUrlEncodedContent。 
   
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
4. 一旦建立 hello 公告，您會看到類似下列 hello Mobile Engagement 入口網站上的 hello (請注意該 hello 狀態 = 草稿 」 和 「 已啟動 = n/A)
   
    ![][3]
5. `CreateAzMECampaign`建立公告促銷活動，並傳回其 Id toohello 呼叫端。 `ActivateAzMECampaign`需要此識別碼做為 hello 參數 tooactivate hello 行銷活動。 
   
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
6. 一旦啟動 hello 公告，您會看到類似下列 hello hello Mobile Engagement 入口網站上：
   
    ![][4]
7. 一旦取得啟動 hello 行銷活動，同時滿足 hello 準則 hello 活動上的任何裝置就會開始看到通知。 
8. 您也會發現該 hello 清單項目標示 IsProcessed = false 已設定 tooTrue 建立 hello 公告活動之後。  

這個範例會建立指定大部分 hello 所需內容的簡單宣告活動。 您可以自訂這個就像您可以從 hello 入口網站使用 hello 資訊[這裡](https://msdn.microsoft.com/library/azure/mt683751.aspx)。 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



