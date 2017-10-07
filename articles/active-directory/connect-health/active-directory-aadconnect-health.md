---
title: "雲端 aaaMonitor hello 使內部部署識別基礎結構。"
description: "這是 hello Azure AD Connect Health 頁面說明它是什麼，並使用它的原因。"
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>監視您內部部署識別基礎結構和同步處理服務 hello 雲端中
Azure Active Directory (Azure AD) Connect Health 可協助您監視，並深入了解您的內部部署身分識別基礎結構和 hello 同步處理服務。 它可讓您 toomaintain 可靠的連線 tooOffice 365 和 Microsoft Online Services 所提供適用於您的索引鍵識別元件，例如 Active Directory Federation Services (AD FS) 伺服器，Azure AD Connect 的伺服器 （也就是監視功能做為同步處理引擎），Active Directory 網域控制站，依此類推。您也可以 hello 關鍵資料點，這些元件的相關輕鬆地存取，讓您可取得使用方式和其他重要 insights toomake 旁徵博引的決定。

hello 資訊顯示在 hello [Azure AD Connect Health 入口網站](https://aka.ms/aadconnecthealth)。 您可以在 hello Azure AD Connect Health 入口網站來檢視警示、 效能監視、 流量分析和其他資訊。 Azure AD Connect Health 可讓您在一個位置的索引鍵識別元件的健全狀況的 hello 單一的方式。

![Azure AD Connect Health 是什麼](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

在 Azure AD Connect Health hello 功能會增加，hello 入口網站會提供透過 hello 透鏡身分識別的單一儀表板。 您可獲得更健全、 狀況良好，且整合的環境使用者 tooincrease 完成其能力 tooget 工作。

## <a name="why-use-azure-ad-connect-health"></a>為何使用 Azure AD Connect Health？
當您整合內部部署目錄與 Azure AD 時，您的使用者會更有效率，因為沒有通用識別身分 tooaccess 雲端和內部部署資源。 不過，這項整合會確保此環境狀況良好，以便使用者能夠可靠地從任何裝置存取內部部署和 hello 中雲端的資源的 hello 挑戰。 Azure AD Connect Health 可協助您監視，並深入了解您的內部部署識別基礎結構使用的 tooaccess Office 365 或其他 Azure AD 應用程式。 使用方式相當簡單，您只需將代理程式安裝在各個內部部署身分識別伺服器中即可。

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[適用於 AD FS 的 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
在 Windows Server 2008 R2、Windows Server 2012 和 Windows Server 2012 R2 上，適用於 AD FS 的 Azure AD Connect Health 支援 AD FS 2.0。 它也支援監視 hello AD FS proxy，或提供驗證的 web 應用程式 proxy 伺服器支援外部網路存取權。 與簡單且便宜的 hello 健康情況代理程式安裝，Azure AD Connect Health 的 AD FS 提供 hello 遵循組的索引鍵的功能：

* AD FS 與 AD FS proxy 伺服器沒有狀況良好時，使用警示 tooknow 監視
* 重大警示的電子郵件通知
* 效能資料的趨勢，適合用於 AD FS 的容量規劃
* AD FS 登入與樞紐分析表 （應用程式、 使用者、 網路位置等等），也就是有用的 toounderstand 如何取得利用 AD FS 的使用情況分析
* AD FS 報告，例如嘗試使用錯誤使用者名稱/密碼的前 50 名使用者及其最後一個 IP 位址

hello 下列影片概述 Azure AD Connect Health 的 AD fs。

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[適用於同步處理的 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health 進行同步監視，並提供您在內部部署 Active Directory 與 Azure AD 之間發生的 hello 同步處理的相關資訊。 Azure AD Connect Health 進行同步提供 hello 遵循組的索引鍵的功能：

* 監視與警示 tooknow Azure AD Connect 的伺服器時，也稱為 hello 同步處理引擎狀況不良
* 重大警示的電子郵件通知
* 同步處理操作情資，包括同步處理作業的延遲圖表以及不同作業 (如新增、更新、刪除) 的趨勢
* 快速概覽資訊同步處理內容的相關和最後一個成功匯出 tooAzure AD
* 物件層級同步處理錯誤的相關報告\(不需要 Azure AD Premium\)

hello 下列影片提供 Azure AD Connect Health 的概觀來同步處理。

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[適用於 AD DS 的 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
適用於 Active Directory Domain Services (AD DS) 的 Azure AD Connect Health 可以監視安裝在 Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 及 Windows Server 2016 上的網域控制站。 hello 健全狀況代理程式安裝可讓您 toomonitor 內部從 hello 雲端的 AD DS 環境。 Azure AD Connect Health 的 AD DS 提供下列的索引鍵的功能集的 hello:

* 監視警示 toodetect，當網域控制站的狀況不良和電子郵件通知為重要警示
* hello 網域控制站儀表板，可提供 hello 健全狀況的快速檢視與您的網域控制站的操作狀態
* hello 複寫狀態儀表板具有 hello 最新的複寫資訊，並偵測到錯誤時，連結 tootroubleshooting 輔助線
* 從任何地方快速存取常用的效能計數器，所需的疑難排解和監視的目的 tooperformance 資料圖形

hello 下列影片概述 Azure AD Connect Health 的 AD ds。

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>開始使用 Azure AD Connect Health
tooget 開始使用 Azure AD Connect Health，使用 hello 下列步驟：

1. [取得 Azure AD Premium](../active-directory-get-started-premium.md) 或[開始試用](https://azure.microsoft.com/trial/get-started-active-directory/)。
2. 在身分識別伺服器上[下載和安裝 Azure AD Connect Health 代理程式](#download-and-install-azure-ad-connect-health-agent)。
3. 檢視 hello Azure AD Connect Health 儀表板在[https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth)。

> [!NOTE]
> 請記住，您看到您的 Azure AD Connect Health 儀表板中的資料之前，您需要 tooinstall hello Azure AD Connect Health 代理程式在您的目標伺服器上。
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>下載和安裝 Azure AD Connect Health 代理程式
* 請確定您[滿足 hello 需求](active-directory-aadconnect-health-agent-install.md#requirements)有關 Azure AD Connect Health。
* 開始使用適用於 AD FS 的 Azure AD Connect Health
    * [下載適用於 AD FS 的 Azure AD Connect Health 代理程式](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [請參閱 hello 安裝指示](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs)。
* 開始使用適用於同步處理的 Azure AD Connect Health
    * [下載並安裝新版的 Azure AD Connect hello](http://go.microsoft.com/fwlink/?linkid=615771)。 hello 健康情況代理程式同步處理將會安裝為 hello Azure AD Connect 的安裝的一部分 (1.0.9125.0 版本或更高版本)。
* 開始使用適用於 AD DS 的 Azure AD Connect Health
    * [下載適用於 AD DS 的 Azure AD Connect Health 代理程式](http://go.microsoft.com/fwlink/?LinkID=820540)。
    * [請參閱 hello 安裝指示](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds)。

## <a name="azure-ad-connect-health-portal"></a>Azure AD Connect Health 入口網站
hello Azure AD Connect Health 入口網站會顯示警示、 監視、 效能和使用情況分析的檢視。 hello https://aka.ms/aadconnecthealth URL 會帶您 Azure AD Connect Health toohello 主要刀鋒視窗。 您可以將刀鋒視窗視為視窗。 在 hello 主要刀鋒視窗中，您會看到**快速入門**，Azure AD Connect Health 和其他設定選項中的服務。 請參閱 hello 下列螢幕擷取畫面和遵循 hello 螢幕擷取畫面的簡短說明。 在您部署的 hello 代理程式之後，hello 健全狀況服務會自動識別 Azure AD Connect Health 正在監視的 hello 服務。

> [!NOTE]
> 如需授權資訊，請參閱 hello [Azure AD 連接常見問題集](active-directory-aadconnect-health-faq.md)或 hello [Azure AD 定價頁面](https://aka.ms/aadpricing)。
    
![Azure AD Connect Health 入口網站](./media/active-directory-aadconnect-health/portal4.png)

* **快速入門**： 當您選取此選項時，hello**快速入門**刀鋒視窗隨即開啟。 您可以下載 hello Azure AD Connect Health 代理程式選取**取得工具**。 您也可以存取文件，並提供意見反應。
* **Active Directory Federation Services**： 此選項會顯示所有 hello AD FS 服務，Azure AD Connect Health 目前監視。 當您選取執行個體時，hello 刀鋒視窗中開啟顯示該服務執行個體的相關資訊。 這項資訊包括概觀、屬性、警示、監視和使用情況分析。 深入了解在 hello 功能[使用 Azure AD Connect Health 使用 AD FS](active-directory-aadconnect-health-adfs.md)。
* **Azure Active Directory Connect (同步處理)**：此選項會顯示 Azure AD Connect Health 目前正在監視的 Azure AD Connect 伺服器。 當您選取 hello 項目時，開啟 hello 刀鋒視窗就會顯示您 Azure AD Connect 的伺服器相關資訊。 深入了解在 hello 功能[使用 Azure AD Connect Health 進行同步](active-directory-aadconnect-health-sync.md)。
* **Active Directory 網域服務**： 此選項會顯示所有 hello AD DS 樹系，Azure AD Connect Health 目前監視。 當您選取的樹系時，hello 刀鋒視窗中開啟顯示該樹系的相關資訊。 這項資訊包含基本資訊、 hello 網域控制站儀表板、 hello 複寫狀態儀表板、 警示與監視的概觀。 深入了解在 hello 功能[使用 Azure AD Connect Health 與 AD DS](active-directory-aadconnect-health-adds.md)。
* **設定**： 這個區段包含選項 tooturn hello 下列開啟或關閉：

  - 自動更新 tooautomatically update hello Azure AD Connect Health 代理程式 toohello 最新版本： 當它們變成可用時，將會自動更新的 toohello hello Azure AD Connect Health 代理程式最新版本。 此選項預設為啟用狀態。
  - 允許 Microsoft 存取 tooyour Azure AD 目錄的健全狀況資料的疑難排解之用： 如果啟用此選項，可以看到 Microsoft hello，您會看到相同資料。 這項資訊可能有助於進行問題的疑難排解和協助。 此選項預設為停用狀態。

## <a name="related-links"></a>相關連結
* [Azure AD Connect Health 代理程式安裝](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 操作](active-directory-aadconnect-health-operations.md)
* [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
* [使用 Azure AD Connect Health 進行同步處理](active-directory-aadconnect-health-sync.md)
* [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health 常見問題集](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 版本歷程記錄](active-directory-aadconnect-health-version-history.md)
