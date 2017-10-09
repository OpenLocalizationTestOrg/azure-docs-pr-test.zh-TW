---
title: "與 AD DS 的 Azure AD Connect Health aaaUsing |Microsoft 文件"
description: "這是 hello Azure AD Connect Health 頁面，將討論如何 toomonitor AD DS。"
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>在 AD DS 使用 Azure AD Connect Health
下列文件的 hello 是特定 toomonitoring Active Directory 網域服務與 Azure AD Connect Health。 AD DS 的 hello 支援版本： Windows Server 2008 R2、 Windows Server 2012、 Windows Server 2012 R2 和 Windows Server 2016。

如需使用 Azure AD Connect Health 來監視 AD FS 的詳細資訊，請參閱[在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)。 此外，如需使用 Azure AD Connect Health 來監視 Azure AD Connect (同步處理) 的詳細資訊，請參閱 [使用適用於同步處理的 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)。

![適用於 AD DS 的 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>適用於 AD DS 的 Azure AD Connect Health 警示
AD DS 的 hello Azure AD Connect Health 警示一節，提供您的使用中和未解決的警示，相關的 tooyour 網域控制站清單。 選取 使用中或已解決的警示開啟新的刀鋒視窗的其他資訊，以及解決步驟，並連結 toosupporting 文件。 每種警示類型可以有一或多個對應 tooeach hello 受該特定的警示影響的網域控制站的執行個體。 Hello hello 警示刀鋒視窗底部，您可以按兩下受影響的網域控制站 tooopen 有關該警示的執行個體的更多詳細資料與其他刀鋒視窗。

在這個刀鋒視窗中，您可以啟用警示的電子郵件通知，並檢視中變更 hello 時間範圍。 展開 hello 時間範圍可讓您 toosee 先前已解決的警示。

![Azure AD Connect 同步處理錯誤](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>網域控制站儀表板
此儀表板提供環境的拓撲檢視，以及關鍵作業計量和每個受監視網域控制站的健康狀態。 hello 呈現的衡量標準協助識別 tooquickly，任何網域控制站，可能需要進一步調查。 根據預設，會顯示 hello 資料行的子集。 不過，您可以找到 hello 整組可用的資料行中，按兩下 hello 資料行命令。 選取您最關心，開啟此儀表板在單一、 輕鬆地將 tooview hello 健全狀況的 AD DS 環境的 hello 資料行。

![網域控制站](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

網域控制站可以依其個別網域或站台，可協助您了解 hello 環境拓撲。 最後，如果您按兩下 hello 刀鋒視窗中的標頭，hello 儀表板最大化 tooutilize hello 可用的螢幕大小。 顯示多個資料行時，此較大的檢視很有幫助。

## <a name="replication-status-dashboard"></a>複寫狀態儀表板
此儀表板提供 hello 複寫狀態以及複寫拓撲的受監視的網域控制站的檢視。 列出 hello 最近的複寫嘗試 hello 狀態，以及任何找到的錯誤很有幫助文件。 您可以按兩下網域控制站並顯示錯誤，tooopen 資訊的新刀鋒視窗，例如： hello 錯誤，並建議解決方法步驟的相關詳細資料，以及連結 tootroubleshooting 文件。

![複寫狀態](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>監視
這項功能提供不同的效能計數器，會持續收集從每個 hello 監視網域控制站的圖形化的趨勢。 網域控制站的效能可以輕鬆地和樹系中所有其他受監視的網域控制站進行比較。 此外，您可以看到各種效能計數器並排，在環境中針對問題進行疑難排解時這很有用。

![監視](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

根據預設，我們已預先選取四個效能計數器。不過，您可以藉由按一下 hello 篩選命令和選取或取消選取任何所需的效能計數器包含其他項目。 此外，您可以按兩下效能計數器圖形 tooopen hello 監視網域控制站的每個包含資料點的新刀鋒視窗。

## <a name="related-links"></a>相關連結
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 代理程式安裝](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 操作](active-directory-aadconnect-health-operations.md)
* [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
* [使用 Azure AD Connect Health 進行同步處理](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health 常見問題集](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 版本歷程記錄](active-directory-aadconnect-health-version-history.md)

