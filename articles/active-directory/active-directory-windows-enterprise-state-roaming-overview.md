---
title: "aaaEnterprise 狀態漫遊概觀 |Microsoft 文件"
description: "提供 Windows 裝置中企業狀態漫遊設定的相關資訊。 企業狀態漫遊使用者提供一致的方式透過他們的 Windows 裝置，並減少 hello 設定新裝置所需的時間。"
services: active-directory
keywords: "什麼是企業狀態漫遊, 企業同步處理, windows 雲端"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>企業狀態漫遊概觀
與 Windows 10 [Azure Active Directory (Azure AD)](active-directory-whatis.md)使用者提升 hello 能力 toosecurely 同步處理其使用者設定和應用程式設定資料 toohello 雲端。 企業狀態漫遊使用者提供一致的方式透過他們的 Windows 裝置，並減少 hello 設定新裝置所需的時間。 企業狀態漫遊的運作類似 toohello 標準[取用者設定同步處理](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs)，最初在 Windows 8 中導入。 此外，企業狀態漫遊提供：

* **分隔公司和取用者資料** – 組織可以控制他們的資料，取用者雲端帳戶中不會混合公司資料，企業雲端帳戶中也不會混合取用者資料。
* **增強式安全性**– 資料會自動加密使用 Azure Rights Management (Azure RMS) 離開 hello 使用者的 Windows 10 裝置之前，資料將會存留在 hello 雲端中的靜止時加密。 所有內容都維持在 hello 雲端，除了 hello 命名空間，例如設定名稱和 Windows 應用程式名稱中的靜止時加密。  
* **較佳的管理和監視**– 提供控制項與可見性者同步處理您組織中以及透過 hello Azure AD 入口網站整合哪些裝置上的設定。 

企業狀態漫遊也可以在多個 Azure 區域中使用。 您可以找到 hello 更新清單的區域上 hello[依照地區的 Azure 服務](https://azure.microsoft.com/regions/#services)下 Azure Active Directory 頁面。

| 文章 | 說明 |
| --- | --- |
| [在 Azure Active Directory 中啟用企業狀態漫遊](active-directory-windows-enterprise-state-roaming-enable.md) |企業狀態漫遊是可用 tooany 組織與 Premium Azure Active Directory (Azure AD) 的訂用帳戶。 如需有關如何 tooget Azure AD 訂用帳戶，請參閱 hello [Azure AD 產品](https://azure.microsoft.com/services/active-directory)頁面。 |
| [設定和資料漫遊常見問題集](active-directory-windows-enterprise-state-roaming-faqs.md) |本主題將回答 IT 系統管理員可能會遇到的設定和應用程式資料同步處理的一些問題。 |
| [設定同步處理的群組原則和 MDM 設定](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 提供群組原則和行動裝置管理 (MDM) 原則設定 toolimit 設定同步處理。 |
| [Windows 10 漫遊設定參考](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |hello 以下是所有將進行漫遊及/或備份在 Windows 10 中的 hello 設定的完整清單。 |
| [疑難排解](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |本主題會執行一些疑難排解基本步驟，並且包含一份已知問題清單。 |

