---
title: "權杖驗證 aaaSecuring Azure CDN 資產 |Microsoft 文件"
description: "使用權杖驗證 toosecure 存取 tooyour Azure CDN 資產。"
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>使用權杖驗證保護 Azure CDN 資產

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>概觀

語彙基元的驗證是一套機制，可讓您從服務資產 toounauthorized 用戶端的 tooprevent Azure CDN。  這通常是內容的 tooprevent"hotlinking"，不同的網站，通常訊息面板，其中會使用您的資產沒有權限。  這會對您的內容傳遞成本產生影響。 藉由啟用這項功能在 CDN 上的，要求將由 CDN 邊緣快顯傳遞 hello 內容之前進行驗證。 

## <a name="how-it-works"></a>運作方式

權杖驗證會驗證產生要求的要求 toocontain 語彙基元值，其中包含編碼的資訊 hello 要求者的信任的網站要求。 將只提供內容 toorequester hello 編碼資訊符合 hello 需求，否則會拒絕要求。 您可以使用以下一或多個參數的 hello 需求設定。

- 國家/地區︰允許或拒絕來自指定國家/地區的要求。  [有效的國碼/地區碼清單。](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL： 只允許指定的資產或路徑 toorequest。  
- 主機： 允許或拒絕要求 hello 要求標頭中使用指定的主機。
- 查閱者： 允許或拒絕指定的查閱者 toorequest。
- IP 位址︰只允許來自特定 IP 位址或 IP 子網路的要求。
- 通訊協定： 允許，或使用 toorequest hello 內容 hello 通訊協定為基礎的區塊要求。
- 到期時間： 指派日期和時間週期 tooensure，連結只會維持有效一段有限的時間。

請參閱每個參數的詳細組態範例。

## <a name="reference-architecture"></a>參考架構

請參閱下列參考架構上 CDN toowork 與 Web 應用程式的權杖驗證所設定。

![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>CDN 端點上的權杖驗證邏輯
    
此圖說明若權杖驗證設定於 CDN 端點上，Azure CDN 如何驗證用戶端要求。

![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>設定權杖驗證

1. 從 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour CDN 設定檔，然後按一下hello**管理**按鈕 toolaunch hello 補充入口網站。

    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-rules-engine/cdn-manage-btn.png)

2. 將滑鼠停留在**HTTP 大型**，然後按一下**語彙基元 Auth** hello 彈出式視窗中。 您將在此索引標籤中設定加密金鑰和加密參數。

    1. 針對**主要金鑰**輸入唯一的加密金鑰。  針對**備份金鑰**輸入另一個加密金鑰

        ![CDN 權杖驗證安裝識別碼](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. 使用加密工具設定加密參數 (根據到期時間、國家/地區、訪客來源、通訊協定、用戶端 IP 來允許或拒絕要求。 您可以使用任何組合。)

        ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - ec-expire︰指定權杖在指定時間週期之後到期的時間。 提交之後 hello 到期時間將會遭到拒絕的要求。 這個參數會使用 Unix 時間戳記 (以自從 1/1/1970 00:00:00 GMT 的標準 epoch 以來的秒數為根據。 您可以使用標準時間與 Unix 時間之間的線上工具 tooprovide 轉換）。例如，如果您想 tooset hello 語彙基元 toobe 過期在 2016 年 12 月 31 12:00:00 GMT 使用 hello Unix 時間： 1483185600，如下所示：
    
        ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - url 允許 ec： 可讓您 tootailor 語彙基元 tooa 特定資產或路徑。 它會限制存取 toorequests 其 URL 以特定的相對路徑開頭。 您可以輸入多個路徑，並以逗號分隔每個路徑。 URL 會區分大小寫。 根據 hello 需求，您可以設定不同的值 tooprovide 不同的存取層級。 下面是數個案例：
        
            如果您有一個 URL：http://www.mydomain.com/pictures/city/strasbourg.png。 據以查看輸入值 "" 及其存取層級

            1. 輸入值 "/"：將允許所有的要求
            2. 輸入值"/ 圖片 」: 將允許所有 hello 下列要求
            
                - http://www.mydomain.com/pictures.png
                - http://www.mydomain.com/pictures/city/strasbourg.png
                - http://www.mydomain.com/picturesnew/city/strasbourgh.png
            3. 輸入值 "/pictures/"：只允許 /pictures/ 的要求
            4. 輸入值 "/ pictures/city/strasbourg.png"：只允許此資產的要求
    
        ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - ec-country-allow︰只允許來自一或多個指定國家/地區的要求。 來自其他所有國家/地區的要求將會遭到拒絕。 使用國家/地區碼 tooset hello 參數，並以逗號分隔每個國家/地區碼。 例如，如果您想 tooallow 皒玿璅法國的存取權，輸入我們 FR 在 hello 資料行做為下面。  
        
        ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - ec-country-deny︰拒絕來自一或多個指定國家/地區的要求。 將允許來自其他所有國家/地區的要求。 使用國家/地區碼 tooset hello 參數，並以逗號分隔每個國家/地區碼。 比方說，如果您想 toodeny 皒玿璅法國的存取權，請輸入我們 FR hello 資料行中。
    
        - ec-ref-allow︰只允許來自指定訪客來源的要求。 查閱者識別 hello hello 網頁連結所要求的 toohello 資源 URL。 hello 查閱者參數值不應包含 hello 通訊協定。 您可以輸入主機名稱和 (或) 該主機名稱上的特定路徑。 您也可以在單一參數內加入多個訪客來源，以逗號區隔每個訪客來源。 如果您指定的查閱者數值，但 hello 查閱者資訊不會傳送 hello 要求，因為 toosome 瀏覽器設定中，預設將會拒絕這些要求。 您可以指派 「 遺漏 」 或空白值在 hello 參數 tooallow 這些要求使用遺漏的查閱者資訊。 您也可以使用"*。 consoto.com"tooallow consoto.com 的所有子網域。例如，如果您想 tooallow 存取要求來自 www.consoto.com、 consoto2.com 和具有空白或遺漏 reffers erquests 底下的所有子網域，輸入下列值：
        
        ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - ec-ref-deny︰拒絕來自指定訪客來源的要求。 請參閱 toodetails 和 「 ec-ref-允許 」 參數中的範例。
         
        - ec-proto-allow︰只允許來自指定通訊協定的要求。 例如，http 或 https。
        
        ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - ec-proto-deny︰拒絕來自指定通訊協定的要求。 例如，http 或 https。
    
        - ec clientip： 限制存取 toospecified 要求者 IP 位址。 支援 IPV4 和 IPV6。 您可以指定單一要求 IP 位址或 IP 子網路。
            
        ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. 您可以測試您的權杖與 hello 描述工具。

    4. 您也可以自訂時，會傳回 toouser 會拒絕要求的回應 hello 類型。 根據預設，我們會使用 403。

3. 現在按一下 [HTTP 大型] 下方的 [規則引擎] 索引標籤。 您將使用此索引標籤 toodefine 路徑 tooapply hello 功能、 啟用 hello 權杖驗證功能，並啟用相關功能的其他權杖驗證。

    - 使用"IF"資料行 toodefine 資產或您想要 tooapply 權杖驗證路徑。 
    - 按一下 從 hello 功能下拉式 tooenable 權杖驗證 tooadd"語彙基元 Auth"。
        
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. 在 hello**規則引擎**索引標籤上，有幾個額外的功能，您可以啟用。
    
    - 語彙基元 auth 拒絕程式碼： hello 的型別決定時，會傳回 toouser 要求遭到拒絕的回應。 設定此規則會覆寫 hello 語彙基元 auth 索引標籤中的 hello 拒絕程式碼設定。
    - 語彙基元 auth 忽略： 決定使用的 URL toovalidate 語彙基元是否會區分大小寫。
    - 權杖驗證參數： 重新命名 hello 權杖驗證查詢字串參數顯示 hello 中要求的 URL。 
        
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-token-auth/cdn-rules-engine2.png)

5. 您可以自訂權杖，這是可針對權杖型驗證功能產生權杖的應用程式。 原始程式碼可以在 [GitHub (英文)](https://github.com/VerizonDigital/ectoken) 上存取。
可用的語言包括：
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Azure CDN 功能和提供者定價

請參閱 hello [CDN 概觀](cdn-overview.md)主題。
