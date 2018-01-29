---
title: "適用於 Android 的 Azure Authenticator | Microsoft Docs"
description: "Microsoft Azure Authenticator 應用程式可用來登入以存取工作資源。 Azure Authenticator 應用程式會對您的行動裝置顯示警示，以通知您有一個擱置的雙因素驗證要求。"
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
ms.assetid: b7ceca0d-5c9d-45c4-942c-b3a9b6bad36c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: femila
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 349649e015aae7198d2c40efc3c1865cad087e8a
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="azure-authenticator-for-android"></a>適用於 Android 的 Azure Authenticator
IT 系統管理員可能曾建議您使用 Microsoft Azure Authenticator 進行登入以存取您的工作資源。 此應用程式提供下列兩個登入選項：

* Multi-Factor Authentication 可讓您透過兩個步驟的驗證來保護您的公司或學校帳戶。 使用您知道的某個事物 (例如密碼) 進行登入，並以您擁有的某個事物 (這個應用程式提供的安全性金鑰) 更進一步地保護帳戶。 Azure Authenticator 應用程式會對您的行動裝置顯示警示，以通知您有一個擱置的雙因素驗證要求。 您只需在應用程式中檢視此要求並點選驗證或取消。 或者，系統可能會提示您輸入應用程式中顯示的密碼。
* 工作帳戶可讓您將 Android 手機或平板電腦轉換成受信任的裝置，並提供公司應用程式的單一登入 (SSO)。 IT 系統管理員可能會要求您新增一個工作帳戶，以便存取公司資源。 SSO 可讓您立即登入並自動登入您的公司提供給您的所有應用程式。

## <a name="installing-the-azure-authenticator-app"></a>安裝 Azure Authenticator 應用程式
您可以從 Google Play 商店安裝 Azure Authenticator 應用程式。
從 Samsung Android 裝置與非 Samsung Android 裝置新增工作帳戶的指示稍有不同。 兩者的指示如下所列。

## <a name="adding-the-work-account-from-samsung-android-device"></a>從 Samsung Android 裝置新增工作帳戶
### <a name="adding-the-work-account-through-the-app-home-screen"></a>透過應用程式主畫面新增工作帳戶
下列指示適用於 Samsung GS3 以上的電話或 Note2 以上的平板電腦。

1. 在應用程式的主畫面上，接受使用者授權合約 (EULA)。
2. 在 [啟用帳戶] 畫面上，按一下右邊的內容功能表，然後選取 [工作帳戶] 。
3. 在 [新增帳戶] 畫面上，選取 [公司帳戶]。
4. 在 [啟動裝置管理員] 畫面上，按一下 [啟動] 。
5. 在 [隱私權原則] 畫面上，選取此核取方塊並按一下 [確認] 。
6. 在 [加入工作場所] 畫面上，輸入您的組織所提供的 userID，然後按一下 [加入] 。
7. 若要登入 Azure Authenticator 應用程式，請輸入您的組織帳戶和密碼，然後按一下 [登入] 。
8. 下一個畫面會顯示 Multi-Factor Authentication (MFA) 的相關資訊，這是為了增加安全性的選擇性畫面。 如果您的公司或學校要求次要因素驗證才能建立工作帳戶，您將會看到這個畫面。 它會提供進一步驗證帳戶的指示。
9. [加入工作場所] 畫面會顯示「**正在加入您的工作場所**」訊息。 Azure Authenticator 應用程式會嘗試將您的裝置加入至您的工作場所。
10. 您應該會在下一個畫面上看到「已加入工作場所」訊息。

> [!NOTE]
> 您可以在您的裝置上有單一工作帳戶。
> 
> 

### <a name="adding-the-work-account-from-the-settings-menu"></a>從設定功能表新增工作帳戶
安裝 Azure Authenticator 應用程式之後，您也可以從 Android 帳戶管理員建立工作帳戶。

1. 從 [設定] 功能表瀏覽至 [帳戶]，然後按一下 [新增帳戶]。
2. 請依照「透過應用程式主畫面新增工作帳戶」程序中的步驟 3-10，新增工作帳戶。

## <a name="adding-the-work-account-from-a-non-samsung-android-device"></a>從非 Samsung Android 裝置新增工作帳戶
### <a name="adding-the-work-account-through-the-app-home-screen"></a>透過應用程式主畫面新增工作帳戶
1. 在應用程式的主畫面上，接受使用者授權合約 (EULA)。
2. 在 [啟用帳戶] 畫面上，按一下右邊的內容功能表，然後選取 [工作帳戶] 。
3. 在 [帳戶] 畫面上，按一下 [新增帳戶] 。
4. 如果您看到 [帳戶] 畫面，請按一下 [新增帳戶]。 如果先前已建立工作帳戶，您會看到 [同步處理] 畫面顯示現有的工作帳戶。 您只需點選主畫面的上一頁箭頭，即可保留此工作帳戶。 或者，您可以選擇移除此帳戶並重建新的工作帳戶。在 [加入工作場所] 畫面上，輸入您的組織所提供的 userID，然後按一下 [加入]。
5. 若要登入 Azure Authenticator 應用程式，請輸入您的組織帳戶和密碼，然後按一下 [登入] 。
6. 下一個畫面會顯示 Multi-Factor Authentication (MFA) 的相關資訊，這是為了增加安全性的選擇性畫面。 如果您的公司或學校要求次要因素驗證才能建立工作帳戶，您將會看到這個畫面。 它會提供進一步驗證帳戶的指示。
7. 在下一個畫面上按一下 [確定]。 請勿變更憑證名稱。
   「正在加入您的工作場所」訊息。 Azure Authenticator 應用程式會嘗試將您的裝置加入至您的工作場所。
   您應該會在下一個畫面上看到「已加入工作場所」訊息。

> [!NOTE]
> 您可以在您的裝置上有單一工作帳戶。
> 
> 

安裝 Azure Authenticator 應用程式之後，您也可以從 Android 帳戶管理員建立工作帳戶。

1. 從 [設定] 功能表瀏覽至 [帳戶]，然後按一下 [新增帳戶]。
2. 請依照「透過應用程式主畫面新增工作帳戶」程序中的步驟 2-7，新增工作帳戶。

### <a name="how-to-find-out-which-version-is-installed"></a>如何找出所安裝的版本
1. 您可以找出您的裝置上所安裝 Azure Authenticator 應用程式版本和相關聯的服務版本。
2. 從快顯功能表按一下 [關於] 。
3. [關於] 畫面會顯示應用程式的服務和裝置上所安裝的版本。

### <a name="sending-log-files-to-report-issues"></a>傳送記錄檔以回報問題
1. 遵循 Microsoft 支援上的指引，以回報 Azure Authenticator 應用程式相關事件、取得事件號碼，以及針對指定的事件號碼傳送記錄檔，如下所示：
2. 從快顯功能表按一下 [記錄] 。
3. 如果您有未結案的 Microsoft 支援事件，請記下事件號碼 (後面的步驟需要使用它)。 如果您尚未建立支援事件並想要獲得協助，請依照 [Microsoft 支援](https://support.microsoft.com/en-us/contactus)的指引來開啟新的事件。
4. 在 [記錄] 畫面上按一下 [立即傳送] 。
5. 選取您想要使用的電子郵件提供者。
6. 如果您已有未結案的 Microsoft 支援事件，請連絡針對您的問題所指派的支援工程師，以了解如何傳送記錄檔資料並讓它與您的事件產生關聯。 支援工程師會提供給您電子郵件地址和主旨行的資訊。 如果您尚未有支援事件，請依照 Microsoft 支援的指引來開啟新的事件。
7. 以 Microsoft 支援服務提供給您的資訊，編輯 [收件者] 行和 [主旨] 行。
8. Azure Authenticator 應用程式會將記錄檔附加至您要傳送的電子郵件。 描述您所遇到的問題、更新收件者清單 (選擇性)，以及傳送電子郵件。

### <a name="deleting-the-work-account-and-leaving-your-workplace"></a>刪除工作帳戶並離開您的工作場所
您可以隨時移除您所建立的工作帳戶，如下所示：

**從設定功能表刪除工作帳戶**

1. 從 [帳戶管理員] 選取 [工作帳戶] 。
2. 在 [工作帳戶] 畫面的 [一般設定] 中，選取 [帳戶設定 – 離開您的工作場所網路]。
3. 在 [工作場所聯結] 畫面上選取 [離開]。
4. 當「您確定要離開工作場所嗎」訊息顯示時，按一下 [確定]  。
5. 這可確保您已從工作場所中刪除您的工作帳戶。

> [!NOTE]
> 建議您不要使用 [移除帳戶] 選項來刪除工作帳戶，因為此選項在某些舊版的 Android 中可能無法運作。
> 
> 

## <a name="uninstalling-the-app"></a>解除安裝應用程式
在 Samsung Android 裝置上，必須先如下所示移除裝置系統管理員權限，才能解除安裝。 

1. 從 [設定] 的 [系統] 底下，選取 [安全性]。
2. 在 [裝置管理] 中按一下 [裝置系統管理員]。 確定已清除 [Azure Authenticator]  旁邊的核取方塊。

## <a name="troubleshooting"></a>疑難排解
如果您看到 [金鑰存放區錯誤]，這可能是因為您未使用 PIN 設定鎖定畫面。 若要解決這個問題，請將 Azure Authenticator 應用程式解除安裝、設定鎖定螢幕的 PIN，以及重新安裝應用程式。

