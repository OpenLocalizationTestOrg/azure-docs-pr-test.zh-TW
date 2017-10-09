---
title: "aaaHow toouse 您 Office 365 訂用帳戶與 Azure RemoteApp 一起 |Microsoft 文件"
description: "了解如何在 Azure RemoteApp tooshare Office 應用程式中使用 Office 365 訂用帳戶。"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2648868dd28cbcd93e38461ae6dce25eaa5d5e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-your-office-365-subscription-with-azure-remoteapp"></a>如何 toouse 您 Office 365 訂用帳戶與 Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

您知道您可以從 hello 雲端的 Azure RemoteApp tooshare Office 應用程式中使用現有的 Office 365 訂閱嗎？ 閱讀並了解您的 Office 365 + Azure RemoteApp 選項的詳細資訊，包括連結 tooarticles 關於 Office 365，協助您進行最 hello 的訂用帳戶。

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>如何使用適用於 Azure RemoteApp 的 Office 365 帳戶？
簽出 Peter 的新發行項，針對所有 hello 資訊：[如何 toouse Azure RemoteApp 使用 Office 365 使用者帳戶](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-toorun-office-applications-in-azure-remoteapp"></a>可以使用 Office 365 訂用帳戶 toorun Office 應用程式在 Azure RemoteApp 嗎？
可以！ 事實上，使用 Office 365 訂用帳戶是 hello 方式 toobring 只有您的 Office 應用程式 tooAzure RemoteApp。

(注意： 如果您的 Azure RemoteApp 部署由主控合作夥伴傳送，它們可能無法 tooprovide Office 授權您根據[服務提供者授權合約](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

hello Office 365 訂用帳戶最棒的一點是它可讓您使用 hello 許多不同的平台和環境，包括 hello Azure 雲端上的相同使用者授權。 當您使用 Azure RemoteApp 中的 Office 應用程式時您不需要 toopurchase 額外授權或任何特殊方式設定您現有的授權。 您只需要包含 [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx)的 Office 365 訂閱即可。

Office 365 ProPlus 可提供 [共用電腦啟用](https://technet.microsoft.com/library/Dn782860.aspx) - 這項功能可在像是 Azure RemoteApp 的虛擬環境與雲端環境 (以及與遠端桌面服務) 中，為 Office 進行以暫時使用者為單位的啟用。

哪些 Office 365 方案包含 Office 365 ProPlus？ 簽出 hello[服務每個計劃內的可用性](https://technet.microsoft.com/library/office-365-plan-options.aspx)資料表。 請注意，並非所有的計劃包含 Office 365 ProPlus （例如，hello Office 365 商務計劃）。 如果您計劃不存在，請考慮升級 tooa 方案 （例如，Office 365 教育版 E3） 的。

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>那麼，如何搭配 Azure RemoteApp 使用我的 Office 365 ProPlus 授權呢？
針對 Office 365 ProPlus 每個使用者授權可讓單一使用者啟動上 too5 電腦和平板電腦和手機上的 Office 應用程式。 每個啟用向 hello 使用者，直到它們 hello 裝置上停用 Office。 (使用者可以管理其裝置 hello [Office 365 入口網站](https://portal.office365.com/)。)

使用 Azure RemoteApp 單一使用者可能登入數部電腦上 hello 相同不知情就日。 這是因為 hello 服務會自動管理及調整 hello 雲端中的資源，而 hello 使用者只看得到 hello 應用程式與您共用的程式。 針對 Office 365 ProPlus 這種情況下提供共用的電腦的啟動模式-這表示該使用者不需要 toodo 任何授權管理 tooaccess 這些資源和該 hello 個別電腦，不列入 hello 5 的電腦啟用限制。

只要您 (hello admin) 指派 Office 365 ProPlus 授權 tooyour 使用者，他們可以使用 Office 其個人裝置，以及透過您的 Azure RemoteApp 集合。

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>我可以搭配 Office 365 和 Azure RemoteApp 使用哪些 Office 應用程式？
您可以使用您的 Office 365 訂用帳戶 tooactivate 並共用 Azure RemoteApp 部署中的 Office 2013。 我們目前不支援 hello 其他版本的 Office 與 Azure RemoteApp 一起使用。 這包括 Office 2003、Office 2007、Office 2010 和 Office 2016。

## <a name="what-about-visio-pro-or-project-pro"></a>那是否支援 Visio Pro 或 Project Pro ？
hello Office 365 ProPlus 映像包含您的 RemoteApp 訂用帳戶中包括 Visio 專業版和專業版的專案。 但您無法使用 Office 365 ProPlus 的訂用帳戶 tooactivate 這些程式-它們都各自具有自己的授權。 您可以啟動它們在 hello [Office 365 入口網站](https://portal.office365.com/)。 

您不需要 toolicense 這些程式若不想 toouse 它們。 只啟用 hello 程式 toouse-並略過 hello 其他人。 您還是會看到它們在 hello 映像，但您無法使用它們。 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>如何開始使用 Office 365 和 Azure RemoteApp？
您現在知道 hello 的 Office 365 授權的詳細資料，讓我們協助您開始使用 Azure RemoteApp 中-很簡單：

當您建立您的 Azure RemoteApp 集合時，使用 hello **Office 365 ProPlus （所需的訂閱）**映像。

![含 Office 365 ProPlus 的 Azure RemoteApp 映像](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

此映像包含 Windows Server 和 Office 365 ProPlus hello 最新版本。 設定您的集合 (包含發佈應用程式) 後，使用者僅須登入 Azure RemoteApp (透過使用其 RemoteApp 用戶端)，然後提供適用於任何 Office 應用程式的 Office 365 認證即可。 無須進行任何設定或管理，即可自動傳遞授權。

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>可以使用 Office 365 ProPlus 建立自訂映像嗎？
您可以建立集合的自訂映像，其中包含 Office 365 ProPlus。 有 2 種選擇-我們提供的使用 hello Azure 資源庫映像，或者您可以建立您自己的自訂映像和安裝那里 Office 365 ProPlus。

### <a name="use-hello-azure-gallery-image"></a>使用 hello Azure 資源庫映像
最簡單方式 toodeploy hello Office 365 ProPlus tooa 集合太[hello Azure 資源庫映像的其中一種](remoteapp-image-on-azurevm.md)納入您的 Azure RemoteApp 訂用帳戶。 請確認您選擇的 hello **Windows Server 遠端桌面工作階段主機與 Office 365 ProPlus 預先安裝**映像。 然後，該映像，在安裝任何其他您想要的應用程式，您已經準備就緒 toogo。

### <a name="use-a-custom-image"></a>使用自訂映像
您還可以建立自訂映像-您可以建立[Azure VM](remoteapp-image-on-azurevm.md)或[建立 hello 映像在本機](remoteapp-create-custom-image.md)並將它上傳 tooAzure。 在任一情況下，請確定您安裝 Office 365 ProPlus 使用 hello 共用的電腦啟動節點。 使用 hello [Office 部署工具](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx)並遵循 hello[指示](https://technet.microsoft.com/library/Dn782858.aspx)進行安裝。  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>重要：請在自訂映像中停用 Office 365 ProPlus 的自動更新。
自訂映像可供 Azure RemoteApp 做為範本加入額外的資源與 hello 要求，從您的使用者會增加。 tooprevent 延遲和連線問題，停用自動更新 Office hello 映像中。 如果您不這樣做，則每個使用該範本建立的資源將會在啟動時自動更新。 請改用 hello 標準 Azure RemoteApp 程序來更新自訂映像。 如此一來您更新 hello Office 應用程式一次在 hello 範本映像，然後讓負責取得 hello 更新 tooyour 使用者的 Azure RemoteApp。

toodisable 自動更新，新增下列 toohello Office 部署工具的組態檔的 hello:

        <Updates Enabled="FALSE" />

現在您的組態檔應該會包含這幾行：

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>那麼，要如何使用 Office 365 ProPlus 更新映像呢？
在您的集合中有許多原因 tooupdate hello 映像。 以下列出幾個原因：

* 取得 hello 最新的 Windows 更新 
* 取得 hello 最新的 Office 365 ProPlus 應用程式更新
* 更新您的自訂應用程式
* 變更 hello 影像本身的其他組態設定

如 hello 端對端的更新您更新您集合 toouse hello 映像的步驟，請移至[這裡](remoteapp-update.md)。 但如 tooupdate 如何 hello 映像和 Office 365 ProPlus 詳細資訊，請參閱下列資訊的 hello。

您可以選擇下列其中一種方式更新映像：將映像替換為全新的映像，或者手動更新現有的映像。

### <a name="replace-your-image-with-hello-latest-azure-gallery-image--add-customizations"></a>您的映像取代 hello 最新的 Azure 資源庫映像 + 新增自訂項目
使用此選項，您可以讓 Microsoft hello Windows Server 和 Office 365 ProPlus 更新負責。 而不是更新現有的映像，您要建立 hello 最新的資源庫映像為基礎的全新映像。 然後，重複任何步驟，您以前 toocustomize hello 映像-安裝自訂的應用程式，請修改 hello 映像組態等。

hello 圖庫映像會定期更新，所以您可以將很容易，清楚知道您的 Windows Server 和 Office 365 ProPlus 應用程式正在設定 toodate。 當然，hello 代價是，您必須 tooapply 自訂每次收到新的映像。 您可以建立指令碼 tooautomate 設定您的自訂。

### <a name="manually-update-your-existing-image"></a>手動更新您現有的映像
使用此選項，您可以使用標準 Windows 工具 tooapply 更新 toohello 映像。 針對 Office 365 ProPlus 使用 hello Office 部署工具 toodownload 並安裝 hello 最新的更新或版本的 Office 365 ProPlus。

> [!IMPORTANT]
> 請記住，-停用 hello Office 365 ProPlus 自動更新。
> 
> 

需要使用更新的 hello Office 部署工具的詳細資訊？

* [按一下以執行適用於 Office 365 產品使用部署的 hello Office 部署工具](https://technet.microsoft.com/library/JJ219423.aspx)
* [部署和更新 Office 365 ProPlus 使用 hello Office 部署工具](https://channel9.msdn.com/Events/Ignite/2015/BRK3168)（影片）
* [設定 Office 365 ProPlus 的更新設定](https://technet.microsoft.com/library/dn761708.aspx)

