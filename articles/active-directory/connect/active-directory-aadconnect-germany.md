---
title: "aaaAzure AD 連線 Microsoft 雲端德國"
description: "Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您與 Azure AD 整合 Office 365、 Azure 和 SaaS 應用程式的通用識別身分的 tooprovide。"
keywords: "簡介 tooAzure AD Connect，Azure AD Connect 的概觀，什麼是 Azure AD Connect，安裝 active directory，德國，黑色樹系"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Microsoft Cloud Germany 中的 Azure AD Connect - 公開預覽
## <a name="introduction"></a>簡介
Azure AD Connect 可進行內部部署 Active Directory 與 Azure Active Directory 之間的同步處理。
目前，有許多 hello 案例[Microsoft 雲端德國](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx)必須由 hello 運算子。 使用 Microsoft 雲端德國時，您必須知道的 hello 下列：

* 下列 Url，必須先在 proxy 伺服器進行同步處理 toooccur 成功 hello:
  
  * *.microsoftonline.de
  * *.windows.net
  * * 憑證撤銷清單
* 當您登入時 tooyour Azure AD 目錄中時，您必須使用的帳戶 hello onmicrosoft.de 網域中。
* 下列功能的 hello 便無法使用：
  * Azure AD Connect Health
  * 自動更新
 
## <a name="download"></a>下載
您可以下載 Azure AD Connect 從 hello 入口網站中的 hello Azure AD Connect 刀鋒視窗。  使用 hello toolocate hello Azure AD Connect 刀鋒視窗下方的指示。

### <a name="hello-azure-ad-connect-blade"></a>hello Azure AD Connect 刀鋒伺服器
一旦您已登入 toohello Azure 入口網站，請勿 hello 遵循：

1. 移 tooBrowse
2. 選取 Azure Active Directory
3. 然後選取 Azure AD Connect

您應該會看到下列 hello:

![Azure AD Connect 刀鋒視窗](media/active-directory-aadconnect-germany/germany1.png)

hello 下表描述顯示在 [hello] 刀鋒視窗中的 hello 功能。

| Title | 說明 |
| --- | --- |
| 同步處理狀態 |讓您知道已啟用或停用同步處理。 |
| 上次同步處理 |hello 上次成功同步處理完成。 |
| 同盟網域 |顯示目前設定的同盟網域的 hello 數目。 |

## <a name="installation"></a>安裝
tooinstall Azure AD Connect，您可以使用 hello 文件[這裡](active-directory-aadconnect.md#install-azure-ad-connect)。

## <a name="advanced-features-and-additional-information"></a>進階功能和其他資訊
如需自訂設定或進階組態的其他資訊和指引，請從 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)著手。  此頁面會提供資訊和連結 tooadditional 指引。

