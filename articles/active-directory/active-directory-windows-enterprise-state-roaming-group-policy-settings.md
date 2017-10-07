---
title: "aaaGroup 原則和 MDM 設定 |Microsoft 文件"
description: "提供應該在公司所擁有的裝置上使用的群組原則和行動裝置管理 (MDM) 設定的相關資訊。 這些原則會套用的 toohello 使用者整個裝置。"
services: active-directory
keywords: "什麼是企業狀態漫遊的群組原則和 MDM 設定, 企業狀態漫遊, windows 雲端"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>群組原則和 MDM 設定
只有在公司擁有的裝置上使用這些群組原則和行動裝置管理 (MDM) 設定，因為這些原則會套用的 toohello 使用者整個裝置。 套用個人 MDM 原則 toodisable 設定同步處理，使用者所擁有的裝置將會產生負面影響 hello 使用該裝置。 此外，hello 裝置上的其他使用者帳戶也將 hello 原則所影響。

想要 toomanage 漫遊個人 (unmanaged) 的裝置可以使用的企業 hello Azure 入口網站 tooenable 或停用漫遊，而不是使用群組原則或 mdm。
hello 下表描述可用的 hello 原則設定。

## <a name="mdm-settings"></a>MDM 設定
hello MDM 原則設定會套用 tooboth Windows 10 和 Windows 10 行動裝置。  Windows 10 行動裝置版支援僅適用於以 Microsoft 帳戶為基礎且透過使用者的 OneDrive 帳戶進行的漫遊。  請參閱 「 裝置和端點 > 一節以取得詳細資料，在 Azure ad 支援哪些裝置太基礎同步處理。

| 名稱 | 說明 |
| --- | --- |
| 允許 Microsoft 帳戶連接 |可讓使用者 tooauthenticate hello 裝置上使用 Microsoft 帳戶 |
| 允許同步處理我的設定 |可讓使用者 tooroam Windows 設定和應用程式資料。同步處理，以及行動裝置上的備份時將停用此原則將會停用 |

## <a name="group-policy-settings"></a>群組原則設定
hello 群組原則設定適用於聯結的 tooan Active Directory 網域的 tooWindows 10 裝置。 hello 資料表也包含舊設定，會出現 toomanage 同步處理設定，但不適用於企業狀態漫遊適用於 Windows 10，其會利用 '請勿使用' hello 描述中註明。

| 名稱 | 說明 |
| --- | --- |
| 帳戶：封鎖 Microsoft 帳戶 |此原則設定會防止使用者在這部電腦上新增新的 Microsoft 帳戶 |
| 不要同步處理 |防止使用者 tooroam Windows 設定和應用程式資料 |
| 不要同步處理個人化 |停用同步 hello 佈景主題的群組 |
| 不要同步處理瀏覽器設定 |停用同步 hello Internet Explorer 的群組 |
| 不要同步處理密碼 |停用密碼群組的同步處理 |
| 不要同步處理其他 Windows 設定 |停用其他 Windows 設定群組的同步處理 |
| 不要同步處理桌面個人化 |不要使用；沒有作用 |
| 不要同步處理已計量連接 |停用已計量連接的漫遊，例如行動電話 3G |
| 不要同步處理應用程式 |不要使用；沒有作用 |
| 不要同步處理應用程式設定 |停用應用程式資料的漫遊 |
| 不要同步處理啟動設定 |不要使用；沒有作用 |

## <a name="related-topics"></a>相關主題
* [企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)
* [在 Azure Active Directory 中啟用企業狀態漫遊](active-directory-windows-enterprise-state-roaming-enable.md)
* [設定和資料漫遊常見問題集](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Windows 10 漫遊設定參考](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [疑難排解](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

