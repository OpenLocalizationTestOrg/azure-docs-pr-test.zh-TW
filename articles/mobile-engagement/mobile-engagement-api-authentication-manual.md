---
title: "使用 Mobile Engagement REST API 進行驗證 - 手動設定"
description: "描述如何手動設定 Mobile Engagement REST API 的驗證"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>使用 Mobile Engagement REST API 進行驗證 - 手動設定
這是 [使用 Mobile Engagement REST API 進行驗證](mobile-engagement-api-authentication.md)的附錄說明文件。 請務必先閱讀它，以取得內容。 這會說明如何使用 Azure 入口網站設定 Mobile Engagement REST API 驗證的一次性設定的替代方式。 

> [!NOTE]
> 下列指示是根據這份 [Active Directory 指南](../azure-resource-manager/resource-group-create-service-principal-portal.md) ，並且針對 Mobile Engagement API 驗證所需進行自訂。 如果您想要了解以下的詳細步驟，請參閱它。 
> 
> 

1. 透過 [傳統入口網站](https://manage.windowsazure.com/)登入 Azure 帳戶。
2. 從左窗格中，選取 [ **Active Directory** ]。
   
     ![選取 Active Directory][1]
3. 在 Azure 入口網站中選擇 [預設 Active Directory]  。 
   
     ![選擇目錄][2]
   
   > [!IMPORTANT]
   > 這個方法只適用於您在帳戶的預設 Active Directory 中工作時，如果您在帳戶中建立的 Active Directory 中進行則無效。 
   > 
   > 
4. 若要檢視目錄中的應用程式，請按一下 [ **應用程式**]。
   
     ![檢視應用程式][3]
5. 按一下 [加入] 。 
   
     ![新增應用程式][4]
6. 按一下 [加入] 
   
     ![新的應用程式][5]
7. 填入應用程式的名稱，然後選取 [WEB 應用程式和/或 WEB API]  作為應用程式的類型，再按一下 [下一步] 按鈕。
   
     ![名稱應用程式][6]
8. 您可以針對 [登入 URL] 和 [應用程式識別碼 URI] 提供任何 dummy URL。 我們的案例不會使用它們，且不會驗證 URL 本身。  
   
     ![應用程式屬性][7]
9. 在這結束時，您將會有 AAD 應用程式，且具有您先前提供如下的名稱。 這是您的 **AD\_APP\_NAME**，請記下它。  
   
     ![應用程式名稱][8]
10. 按一下應用程式名稱，然後按一下 [設定] 。
    
      ![設定應用程式][9]
11. 記下將作為 API 呼叫之 **CLIENT\_ID** 的用戶端識別碼。 
    
     ![設定應用程式][10]
12. 向下捲動至 [金鑰] 區段，並加入持續時間最好為 2 年 (到期) 的金鑰，然後按一下 [儲存]。 
    
     ![設定應用程式][11]
13. 立即複製為金鑰顯示的值，因為它只會現在顯示，且不會儲存，因此不會再顯示。 如果您遺失它，則必須產生新的金鑰。 這會是您 API 呼叫的 **CLIENT_SECRET**。 
    
     ![設定應用程式][12]
    
    > [!IMPORTANT]
    > 此金鑰將在您指定的持續時間結束時到期，因此到時候請務必更新，否則您的 API 驗證將無法再使用。 如果您認為此金鑰遭到盜用，您也可以將它刪除並重新建立。
    > 
    > 
14. 按一下 [檢視端點] 按鈕，現在它將會開啟 [應用程式端點] 對話方塊。 
    
    ![][13]
15. 從 [應用程式端點] 對話方塊中，複製 [OAUTH 2.0 權杖端點] 。 
    
    ![][14]
16. 此端點將為下列形式，其中 URL 中的 GUID 是您的 **TENANT_ID**，因此請記下它︰ 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. 現在我們將繼續設定此應用程式上的權限。 這將需要開啟 [Azure 入口網站](https://portal.azure.com)。 
18. 按一下 [資源群組] 並尋找 [Mobile Engagement] 資源群組。  
    
    ![][15]
19. 按一下 [Mobile Engagement] 資源群組，並瀏覽至此處的 [設定] 刀鋒視窗。 
    
    ![][16]
20. 在 [設定] 刀鋒視窗中按一下 [使用者]，然後按一下 [新增] 來新增使用者。 
    
    ![][17]
21. 按一下 [選取角色] 
    
    ![][18]
22. 按一下 [擁有者] 
    
    ![][19]
23. 在 [搜尋] 方塊中搜尋應用程式的名稱 **AD\_APP\_NAME**。 依預設，您不會在這裡看到它。 找到之後請選取它，然後按一下刀鋒視窗底部的 [選取]  。 
    
    ![][20]
24. 在 [新增存取] 刀鋒視窗中，它會顯示為 [1 個使用者、0 個群組]。 按一下此刀鋒視窗中的 [確定]  ，確認變更。 
    
    ![][21]

您現在已完成所需的 AAD 組態，可以呼叫 API。 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



