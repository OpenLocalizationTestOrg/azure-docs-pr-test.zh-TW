---
title: "aaaAuthenticate 與 Mobile Engagement REST Api 手動安裝"
description: "描述如何 toomanually 安裝 Mobile Engagement REST Api 的驗證"
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
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>使用 Mobile Engagement REST API 進行驗證 - 手動設定
這是附錄文件太[與 Mobile Engagement REST Api 的驗證](mobile-engagement-api-authentication.md)。 請確定讀取第一個 tooget hello 內容。 此描述您的驗證設定的替代方式 toodo hello 一次性安裝 hello Mobile Engagement REST Api 使用 hello Azure 入口網站。 

> [!NOTE]
> 下列的 hello 指示根據這個[Active Directory 指南](../azure-resource-manager/resource-group-create-service-principal-portal.md)和自訂的所需的 Mobile Engagement 應用程式開發介面的驗證內容。 因此如果您想 toounderstand hello 執行下列步驟在詳細資料，請參閱 tooit。 
> 
> 

1. 登入 tooyour Azure 帳戶透過 hello[傳統入口網站](https://manage.windowsazure.com/)。
2. 選取**Active Directory** hello 左窗格中。
   
     ![選取 Active Directory][1]
3. 選擇 hello**預設的 Active Directory**在 Azure 入口網站。 
   
     ![選擇目錄][2]
   
   > [!IMPORTANT]
   > 這個方法僅適用於您要使用 hello 預設 Active Directory，您的帳戶，而且將無法運作，如果您已建立您的帳戶在 Active Directory 中進行。 
   > 
   > 
4. tooview hello 應用程式在目錄中，按一下 **應用程式**。
   
     ![檢視應用程式][3]
5. 按一下 [加入] 。 
   
     ![新增應用程式][4]
6. 按一下 [加入] 
   
     ![新的應用程式][5]
7. 填入 hello 應用程式和應用程式做為選取的 hello 類型名稱**WEB 應用程式和/或 WEB API**按一下 hello 下一步 按鈕。
   
     ![名稱應用程式][6]
8. 您可以針對 [登入 URL] 和 [應用程式識別碼 URI] 提供任何 dummy URL。 不會使用我們的案例並不會驗證其本身的 hello Url。  
   
     ![應用程式屬性][7]
9. 在這個 hello 結束時，您會有 AAD 應用程式，但您先前提供類似 hello 下列 hello 名稱。 這是您的 **AD\_APP\_NAME**，請記下它。  
   
     ![應用程式名稱][8]
10. 按一下 hello 應用程式名稱，然後按一下 **設定**。
    
      ![設定應用程式][9]
11. 請記下將使用做為用戶端識別碼 hello**用戶端\_識別碼**對於您的 API 呼叫。 
    
     ![設定應用程式][10]
12. 捲動 toohello**金鑰**區段並加入最好 2 年 （過期） 持續時間的索引鍵，然後按一下**儲存**。 
    
     ![設定應用程式][11]
13. 立即複製 hello 值顯示為 hello 金鑰現在只顯示並不會儲存，因此不會再顯示。 如果遺失則您將有 toogenerate 新的金鑰。 這會是 hello **CLIENT_SECRET**對於您的 API 呼叫。 
    
     ![設定應用程式][12]
    
    > [!IMPORTANT]
    > 此金鑰會過期結尾 hello hello 持續時間，您所指定，請確定 toorenew hello 時間否則一 API 驗證不會再。 如果您認為此金鑰遭到盜用，您也可以將它刪除並重新建立。
    > 
    > 
14. 按一下**檢視端點**按鈕現在這會開啟 hello**應用程式端點** 對話方塊。 
    
    ![][13]
15. 從 hello 應用程式端點對話方塊中，複製 hello **OAUTH 2.0 權杖端點**。 
    
    ![][14]
16. 此端點將處於下列其中 hello hello URL 中的 GUID 是表單的 hello 您**TENANT_ID**所以請記下它： 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. 現在我們將繼續在此應用程式上的 tooconfigure hello 權限。 這就 tooopen 向上 hello [Azure 入口網站](https://portal.azure.com)。 
18. 按一下**資源群組**並尋找 hello **Mobile Engagement**資源群組。  
    
    ![][15]
19. 按一下 hello **Mobile Engagement**資源群組，並瀏覽 toohello**設定**這裡刀鋒視窗。 
    
    ![][16]
20. 按一下**使用者**在 hello 設定 刀鋒視窗，然後按一下**新增**tooadd 使用者。 
    
    ![][17]
21. 按一下 [選取角色] 
    
    ![][18]
22. 按一下 [擁有者] 
    
    ![][19]
23. 應用程式的 hello 名稱搜尋**AD\_應用程式\_名稱**hello [搜尋] 方塊中。 依預設，您不會在這裡看到它。 一旦您找到它，請選取它，然後按一下 **選取**在 hello hello 刀鋒視窗的底部。 
    
    ![][20]
24. 在 hello**加入存取**刀鋒視窗中，它會顯示為**1 個使用者、 群組 0**。 按一下**確定**此刀鋒視窗 tooconfirm hello 變更。 
    
    ![][21]

您現在已完成所需的 hello AAD 設定，而且所有設定 toocall hello 應用程式開發介面。 

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



