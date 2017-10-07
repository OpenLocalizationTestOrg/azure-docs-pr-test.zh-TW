---
title: "Azure AD Connect：預覽版功能 | Microsoft Docs"
description: "本主題詳細描述 Azure AD Connect 中位於預覽的功能。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>有關預覽中之功能的其他詳細資料
本主題描述如何 toouse 功能目前在預覽中。

## <a name="group-writeback"></a>群組回寫
hello 選項用於群組回寫中的選擇性功能可讓您 toowriteback **Office 365 群組**tooa 樹系安裝 exchange。 這是永遠 hello 雲端中受控制的群組。 如果您有 Exchange 內部部署，然後您可以撰寫回這些群組 tooon 單位以便與在內部部署 Exchange 信箱的使用者可以傳送和接收電子郵件從這些群組。

Office 365 群組和如何 toouse 它們可以找到詳細資訊[這裡](http://aka.ms/O365g)。

Office 365 群組將會在內部部署 AD DS 中顯示為通訊群組。 在內部部署 Exchange 伺服器必須在 Exchange 2013 累積更新 8 （2015 年 3 月發行） 或 Exchange 2016 toorecognize 這個新的群組類型。

**Hello 預覽期間的附註**

* 目前不在 hello 預覽中才會填入 hello 地址通訊錄屬性。 沒有這個屬性，hello 群組不是顯示在 hello GAL。 hello 最簡單的方式 toopopulate 這個屬性是 toouse hello Exchange PowerShell cmdlet `update-recipient`。
* 只有 hello Exchange 結構描述的樹系是有效的目標群組。 如果不偵測到任何 Exchange，然後群組回寫是不可能 tooenable。
* 目前只支援單一樹系 Exchange 組織部署。 如果您有一個以上的 Exchange 組織內部，然後您需要在內部部署 GALSync 解決方案的這些群組 tooappear 其他樹系中。
* 安全性群組或通訊群組，並不會處理 hello 群組回寫功能。

> [!NOTE]
> 用於群組回寫需要訂用帳戶 tooAzure AD Premium。
> 
>

## <a name="user-writeback"></a>使用者回寫
> [!IMPORTANT]
> hello 使用者回寫預覽功能已移除 hello 2015 年 8 月更新 tooAzure AD Connect。 如果已啟用它，則您應該停用這個功能。
>
>

## <a name="next-steps"></a>後續步驟
繼續[自訂 Azure AD Connect 安裝](active-directory-aadconnect-get-started-custom.md)。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
