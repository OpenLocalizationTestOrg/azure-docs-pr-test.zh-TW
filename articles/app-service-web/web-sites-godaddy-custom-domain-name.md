---
title: "aaaConfigure Azure App Service (GoDaddy) 中的自訂網域名稱"
description: "了解 toouse 網域從 GoDaddy 使用 Azure Web 應用程式的名稱"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>在 Azure App Service 中設定自訂網域名稱 (直接向 GoDaddy 購買)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

如果您已購買通過 Azure App Service Web 應用程式網域，則 toohello 最後一個步驟，請參閱[購買 Web 應用程式網域](custom-dns-web-site-buydomains-web-app.md)。

本文提供搭配使用直接從 [GoDaddy](https://godaddy.com) 購買的自訂網域名稱與 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) 的相關指示。

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>了解 DNS 記錄
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>新增自訂網域的 DNS 記錄
tooassociate App Service 中的 web 應用程式與您的自訂網域，您必須新增新的項目 hello DNS 資料表中的自訂網域使用 GoDaddy 所提供的工具。 使用 hello GoDaddy.com 依照步驟 toolocate hello DNS 工具

1. 登入帳戶 tooyour GoDaddy.com，並選取**我的帳戶**然後**管理我的網域**。 您想 toouse Azure web 應用程式，並選取 hello 網域名稱的選取 hello 下拉式選單**管理 DNS**。
   
    ![custom domain page for GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. 從 hello**網域詳細資料**頁面上，捲動 toohello **DNS 區域檔案** 索引標籤。這是 hello 區段用於加入及修改您的網域名稱的 DNS 記錄。
   
    ![DNS Zone File tab](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    選取**新增記錄**tooadd 現有的記錄。
   
    太**編輯**現有記錄、 選取 hello 畫筆及紙張圖示旁邊 hello 記錄。
   
   > [!NOTE]
   > 新增記錄之前，請注意，GoDaddy 已為熱門子網域 (在編輯器中稱為**主機**) 建立 DNS 記錄，例如**電子郵件**、**檔案**、**郵件**及其他。 如果您已經想 toouse hello 名稱存在，而不是建立一個新的 hello 現有記錄的修改。
   > 
   > 
3. 當加入資料錄，您必須先選取 hello 記錄類型。
   
    ![選取記錄類型](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    接下來，您必須提供 hello**主機**(hello 自訂的網域或子網域) 和決定其**指向**。
   
    ![新增區域記錄](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * 加入時**（主機） 記錄**-您必須設定 hello**主機**欄位 tooeither  **@**  (這代表根網域名稱，例如**contoso.com**，) * （萬用字元比對多的子網域） 或您想 toouse hello 子網域 (例如， **www**。)您必須設定 hello**指向**欄位 toohello Azure web 應用程式的 IP 位址。
   * 加入時**CNAME （別名） 記錄**-您必須設定 hello**主機**apps toouse 欄位 toohello 子網域。 例如 **www**。 您必須設定 hello**指向**欄位 toohello **。 名稱是.azurewebsites.net** Azure web 應用程式的網域名稱。 例如，**contoso.azurewebsites.net**。
4. 按一下 [加入另一個] 。
5. 選取**TXT**和 hello 記錄類型，然後指定**主機**值 **@** 和**指向**值**&lt;yourwebappname&gt;。 名稱是.azurewebsites.net**。
   
   > [!NOTE]
   > Azure toovalidate 您擁有 hello 網域 hello 所記錄或 hello 第一個 TXT 記錄描述會使用這個 TXT 記錄。 一旦 hello 網域已對應的 toohello hello Azure 入口網站中的 web 應用程式，就可以移除此 TXT 記錄項目。
   > 
   > 
6. 當您完成新增或修改的記錄，按一下**完成**toosave 變更。

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>啟用 web 應用程式上的 hello 網域名稱
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

