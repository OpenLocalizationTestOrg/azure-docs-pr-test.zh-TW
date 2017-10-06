---
title: "Azure AD 使用者帳戶 aaaCreate |Microsoft 文件"
description: "本文說明 toocreate Azure AD 使用者帳戶的 runbook 在 Azure 自動化 tooauthenticate Azure 和傳統 Azure 中的認證。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "azure active directory 使用者, azure 服務管理, azure ad 使用者帳戶"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>使用 Azure 傳統部署和 Resource Manager 驗證 Runbook
本文將告訴您必須執行 tooconfigure Azure AD 使用者帳戶的 Azure 傳統部署模型或 Azure 資源管理員資源上執行的 Azure 自動化 runbook 的 hello 步驟。  Toobe 然後繼續進行時支援的驗證身分識別您 Azure 資源管理員的基礎 runbook、 hello 建議的方法使用 Azure 執行身分帳戶。       

## <a name="create-a-new-azure-active-directory-user"></a>建立新的 Azure Active Directory 使用者
1. Hello 想 toomanage 的 Azure 訂用帳戶的服務系統管理員身分登入 toohello Azure 傳統入口網站。
2. 選取**Active Directory**，然後選取您的組織目錄中的 hello 名稱。
3. 選取 hello**使用者**索引標籤，然後在 hello 命令區域中，選取**新增使用者**。
4. 在 hello**告訴我們這位使用者**頁面的 **使用者類型**，選取**您組織中的新使用者**。
5. 輸入使用者稱。  
6. 選取您在 hello Active Directory 頁面上的 Azure 訂用帳戶相關聯的 hello 目錄名稱。
7. 在 hello**使用者設定檔**頁面上，提供第一個和最後一個名稱、 使用者易記的名稱，與使用者從 hello**角色**清單。  請勿 [啟用 Multi-Factor Authentication] 。
8. 請注意 hello 使用者的完整名稱和暫時密碼。
9. 選取 [設定] > [系統管理員] > [新增]。
10. 輸入您所建立的 hello 使用者 hello 完整使用者名稱。
11. 選取您想 hello 使用者 toomanage hello 訂用帳戶。
12. 登出 Azure，然後重新登入您剛建立的 hello 帳戶。 您將會提示的 toochange hello 使用者的密碼。

## <a name="create-an-automation-account-in-azure-classic-portal"></a>在 Azure 傳統入口網站中建立自動化帳戶
在本節中，您可以執行 hello 遵循步驟 toocreate hello 使用 Azure 入口網站中的 Azure 自動化帳戶與您管理在 Azure 傳統部署資源的 runbook。  

> [!NOTE]
> 以 hello Azure 傳統入口網站建立的自動化帳戶可以管理由 Azure 傳統 hello 和 Azure 入口網站和其中的 cmdlet。 一旦建立 hello 帳戶，並沒有差別如何建立及管理 hello 帳戶內的資源。 如果您打算 toocontinue toouse hello Azure 傳統入口網站，則您應該使用，而不是 hello Azure 入口網站 toocreate 任何自動化帳戶。
> 
> 

1. Hello 想 toomanage 的 Azure 訂用帳戶的服務系統管理員身分登入 toohello Azure 傳統入口網站。
2. 選取 [自動化] 。
3. 在 hello**自動化**頁面上，選取**建立自動化帳戶**。
4. 在 hello**建立自動化帳戶**，輸入新的自動化帳戶的名稱，然後選取**區域**hello 下拉式清單中。  
5. 按一下**確定**tooaccept 您的設定，並建立 hello 帳戶。
6. 建立之後，它就會列在 hello**自動化**頁面。
7. 按一下 hello 帳戶，它會使您 toohello 儀表板頁面。  
8. 在 hello 自動化儀表板 頁面上，選取 **資產**。
9. 在 hello**資產**頁面上，選取**加入設定**位於 hello hello 頁面的底部。
10. 在 hello**加入設定**頁面上，選取**Add Credential**。
11. 在 hello**定義認證**頁面上，選取**Windows PowerShell 認證**從 hello**認證類型**下拉式清單，並提供 hello 認證的名稱。
12. 在 hello 下列**定義認證** 頁面中輸入的 hello 密碼 hello AD 使用者帳戶在 hello 稍早建立的**使用者名**hello 中的欄位和 hello 密碼**密碼**和**確認密碼**欄位。 按一下**確定**toosave 您的變更。

## <a name="create-an-automation-account-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立自動化帳戶
本節中，執行下列步驟 toocreate hello 使用 Azure 入口網站中的 Azure 自動化帳戶與您管理 Azure Resource Manager 模式中的資源的 runbook 的 hello。  

1. 以登入 toohello Azure 入口網站 hello 想 toomanage 的 Azure 訂用帳戶的服務系統管理員。
2. 選取 [自動化帳戶] 。
3. 在 hello 自動化帳戶刀鋒視窗中，按一下 **新增**。<br><br>![加入自動化帳戶](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. 在 hello**加入自動化帳戶**刀鋒視窗中的，在 hello**名稱**方塊中，輸入新的自動化帳戶的名稱。
5. 如果您有多個訂閱，指定 hello 新帳戶，以及新的其中一個 hello 或現有的**資源群組**和 Azure 資料中心**位置**。
6. 選取 hello 值**是**hello**建立 Azure 執行身分帳戶**選項，然後按一下 hello**建立** 按鈕。  
   
    > [!NOTE]
    > 如果您選擇 toonot hello 執行身分帳戶選取 hello 選項建立**否**，您會看到一則警告訊息中 hello 與**加入自動化帳戶**刀鋒視窗。  雖然 hello 帳戶建立並指派 toohello**參與者**角色在 hello 訂用帳戶，不會有對應的驗證識別身分，在您的訂用帳戶目錄服務，因此，沒有存取權您的訂用帳戶中的資源。  這會防止任何從正在 tooauthenticate 可以參考此帳戶的 runbook，並執行對 Azure 資源管理員資源的工作。
    > 
    >

    <br>![加入自動化帳戶警告](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. 而 Azure 會建立 hello 自動化帳戶，您可以追蹤在 hello 進度**通知**hello 功能表。

Hello hello 認證建立完成後，您會需要的 toocreate 稍早建立認證資產 tooassociate hello 自動化帳戶以 hello AD 使用者帳戶。  請記住，我們只建立 hello 自動化帳戶並不是與驗證身分識別相關聯。  Hello 中所述步驟 hello[認證 Azure 自動化文件中的資產](automation-credentials.md#creating-a-new-credential-asset)，然後輸入 hello 值**username** hello 格式**網域 \ 使用者**。

## <a name="use-hello-credential-in-a-runbook"></a>在 runbook 中使用 hello 認證
您可以擷取使用 hello runbook 中的 hello 認證[Get-automationpscredential](http://msdn.microsoft.com/library/dn940015.aspx)活動，然後使用它與[Add-azureaccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour Azure 訂用帳戶。 如果 hello 認證是系統管理員的多個 Azure 訂用帳戶，則您也應該使用[Select-azuresubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello 正確。 這通常會出現在大多數 Azure 自動化 runbook 的 hello 頂端的 hello 範例下列 Windows PowerShell 中顯示。

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

您應該在您的 Runbook 中的任何 [檢查點](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) 後重複這幾行。 如果 hello runbook 已暫停，然後繼續在另一個背景工作上，它將需要再次 tooperform hello 驗證。

## <a name="next-steps"></a>後續步驟
* 檢閱 hello 不同的 runbook 類型和建立您自己的 runbook 從步驟 hello 下列文章[Azure 自動化 runbook 類型](automation-runbook-types.md)

