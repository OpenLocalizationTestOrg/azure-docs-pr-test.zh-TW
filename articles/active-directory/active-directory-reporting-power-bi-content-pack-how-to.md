---
title: "aaaHow toouse hello Azure Active Directory Power BI 內容套件 |Microsoft 文件"
description: "了解如何 toouse hello Azure Active Directory Power BI 內容套件"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>如何 toouse hello Azure Active Directory Power BI 內容套件

身為 IT 管理員，了解您的使用者如何採用及使用 Azure Active Directory 功能相當重要。它可讓您 tooplan IT 基礎結構和通訊 tooincrease 使用量和 tooget hello 最 AAD 功能。 Power BI 內容套件提供 hello 能力 toofurther 分析您的資料 toounderstand 方式，您可以使用此資料 toogather 更豐富深入了解與 hello 其 Azure Active Directory 的 Azure Active Directory 的各種功能您有很大依賴。  與 hello 整合 Azure Active Directory 應用程式開發介面放入 Power BI，您可以輕鬆地下載 hello 預先建立的內容套件，並在您使用 Power BI 提供豐富的視覺效果經驗的 Azure Active Directory 中獲得見解 tooall hello 活動。 您可以建立自己的儀表板，並輕鬆地與組織中所有人共用。 

本主題提供您 tooinstall 並用 hello 內容的逐步指示與組件，您的環境中。

## <a name="installation"></a>安裝  

**tooinstall hello Power BI 內容套件：**

1. 登入[Power BI](https://app.powerbi.com/groups/me/getdata/services)與您的 Power BI 帳戶 (這是 hello 做為您的 O365 或 Azure AD 帳戶的相同帳戶)。

2. 在 hello hello 左側瀏覽窗格底部，選取**取得資料**。

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. 在 hello**服務**方塊中，按一下**取得**。
   
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  搜尋 **Azure Active Directory**。

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  出現提示時，輸入您的 Azure AD 租用戶識別碼，然後按 [下一步]。

    > [!TIP] 
    > 您的 Office 365 / Azure AD 租用戶快速 tooget hello 租用戶識別碼是 toologin toohello Azure AD 入口網站、 向下鑽研 toohello 目錄並複製 hello 識別碼，從下列 URL 的 hello: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  按一下 [登入]。 
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  輸入您的使用者名稱和密碼，然後按一下登入。
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  在 hello 應用程式的同意對話方塊中，按一下 **接受**。
 
9.  建立好 Azure Active Directory 活動記錄儀表板後，按一下該儀表板。
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>此內容套件有何功用？

我們進到您可以執行與此內容套件之前，此處的預覽 hello hello 內容中的各種報表組件。 報表資料會回到 toohello**過去 30 天內**。

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>此版 Azure Active Directory 記錄內容套件中包含的報表

**應用程式使用量和趨勢報表**： 取得深入了解 hello 的應用程式中使用您的組織，以及正在使用哪些最 hello 與時機。 您可以使用此報表 toogather 深入了解如何使用您最近推出您組織中的應用程式，或找出哪些應用程式上相當普遍。 這樣，如果您看到 是否未使用 hello 應用程式，來改善使用方式。

**依位置和使用者的登入**： 取得深入了解所有 hello 登入使用 Azure 身分識別與可提供深入了解 hello hello 使用者身分執行。 透過此項目，您可以更深入地了解個人登入狀況並回答下列問題：

- 此使用者從何處登入？
- 哪些使用者擁有 hello 大部分的登入和其中執行他們登入從嗎？ 
- 成功 hello 登入？  
 
您可以按一下特定日期或位置，以深入探詢詳細資料。

**每個應用程式的唯一使用者**：檢視使用指定應用程式的所有唯一使用者。 此項目僅包括「*成功*」登入應用程式的使用者。

**裝置登入**: hello 的 OS 類型檢視和瀏覽器正在使用的 hello 使用者包括的詳細資訊與您組織中的使用者：

- 使用者名稱
- IP 位址
- 位置 
- 登入狀態 

使用這份報表，您可以了解在組織內使用各種裝置設定檔，並判斷根據用途的裝置原則的 hello

**SSPR 漏斗圖**：了解在組織中如何完成密碼重設。 查看進入多少密碼重設嘗試透過 hello SSPR 工具，以及多少個成功。 更深入發掘 hello 使用 hello SSPR 漏斗圖的密碼重設失敗，並了解特定失敗的發生原因。 此報表會提供更深入的了解如何 hello SSPR 工具使用的組織內進行 hello 正確的決策。

## <a name="customizing-azure-ad-activity-content-pack"></a>自訂 Azure AD 的活動內容套件

**變更視覺效果**： 您可以按一下來變更報表視覺效果**編輯報表**和選取您想要的 hello 視覺效果。
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**包含其他欄位**： 您可以加入欄位 toohello 報表或選取您希望 tooadd/移除 hello 欄位 hello visual toowhich 移除它。 在 hello 下列範例中，我加入 「 登入狀態 」 欄位 toohello 資料表檢視表。 
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**釘選視覺效果 tooyour 儀表板**： 您可以自訂儀表板和包含您自己的視覺效果 toohello 報表並將其釘選 toohello 儀表板。 在 hello 面範例中，我要加入新的篩選器，稱為 「 登入狀態 」，並包含 hello 報表中。 我也從橫條圖 tooa 折線圖變更 hello 視覺效果，並可以將這個新的視覺 toohello 儀表板釘選。

![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**共用儀表板**： 當您建立您想要的 hello 內容之後時，您可以在組織中與 hello 使用者共用 hello 儀表板。 請記住一旦共用 hello 報表時，他們可以看到您所選取 hello 報表中的 hello 欄位。
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>排定每日重新整理 Power BI 報表

tooschedule 每日重新整理 Power BI 報表中，跳過**資料集 > 設定 > 排程重新整理**並將其設定，如下所示。
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>更新 toonewer 版本內容套件

如果您想 tooupdate 內容 pack tooget 較新版本：

- 下載 hello 新內容套件，並設定根據本文所列的指示。

- 在您設定它，請移過**資料來源 > 設定 > 資料來源認證**，然後重新輸入您的認證，如下所示

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Hello hello 內容套件的新版本可以運作，因為您可以在必要時刪除 hello 基礎報表和與該內容套件相關聯的資料集移除 hello 舊版本。

## <a name="still-having-issues"></a>仍然有問題嗎？ 

請參閱我們的[疑難排解指南](active-directory-reporting-troubleshoot-content-pack.md)。 如需使用 Power BI 的一般說明，請參閱這些[說明文章](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/)。
 

## <a name="next-steps"></a>後續步驟

如需報告的概觀，請參閱 hello [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。
