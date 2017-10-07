---
title: "Azure AD Connect︰同步服務執行個體 | Microsoft Docs"
description: "本頁記載 Azure AD 執行個體的特殊考量。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect：執行個體的特殊考量
Azure AD Connect 最常搭配 hello 全球執行個體的 Azure AD 和 Office 365。 但還有其他執行個體，而它們有不同的 URL 需求和其他特殊考量。

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Germany
hello [Microsoft 雲端德國](http://www.microsoft.de/cloud-deutschland)是統領雲端由德文的資料信任項。

| 在 [proxy 伺服器的 Url tooopen |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| +憑證撤銷清單 |

當您登入 tooyour Azure AD 租用戶時，您必須在 hello onmicrosoft.de 網域中使用的帳戶。

目前不存在於 hello Microsoft 雲端德國的功能：

* 無法使用 **Azure AD Connect Health**。
* 無法使用「自動更新」。
* **密碼回寫**適用於 Azure AD Connect 1.1.570.0 預覽版本和更新的版本。
* 無法使用其他 Azure AD Premium 服務。

## <a name="microsoft-azure-government-cloud"></a>Microsoft Azure Government 雲端
hello [Microsoft Azure 政府雲端](https://azure.microsoft.com/features/gov/)是美國政府的雲端。

此雲端是以舊版的 DirSync 提供支援。 從 Azure AD connect 組建 1.1.180 hello 新一代 hello 雲端的支援。 這個層代使用僅限美國根據的端點，且有不同的 Url tooopen 清單中您的 proxy 伺服器。

| 在 [proxy 伺服器的 Url tooopen |
| --- |
| \*.microsoftonline.com |
| \*.microsoftonline.us |
| \*.gov.us.microsoftonline.com |
| +憑證撤銷清單 |

Azure AD Connect 不能 tooautomatically 偵測 Azure AD 租用戶位於 hello 政府雲端。 相反地，您需要下列動作，當您安裝 Azure AD Connect tootake hello。

1. 啟動 hello Azure AD Connect 的安裝。
2. 當您看見 hello 應該 tooaccept hello 使用者授權合約的第一頁時，不會繼續，但保留 hello 安裝精靈執行。
3. 啟動 regedit 並變更登錄機碼 hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello 值`2`。
4. 請返回 toohello Azure AD Connect 的安裝精靈、 接受 hello 使用者授權合約，並繼續。 在安裝期間，請確定 toouse hello**自訂組態**安裝路徑 （以及不快速安裝）。 然後，繼續如往常般 hello 安裝。

目前不存在於 hello Microsoft Azure 政府雲端的功能：

* 無法使用 **Azure AD Connect Health**。
* 無法使用「自動更新」。
* **密碼回寫**適用於 Azure AD Connect 1.1.570.0 預覽版本和更新的版本。
* 無法使用其他 Azure AD Premium 服務。

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
