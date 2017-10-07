---
title: "Azure Active Directory Connect 常見問題集 - | Microsoft Docs"
description: "此頁面包含有關 Azure AD Connect 的常見問題集。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Azure Active Directory Connect 的常見問題集

## <a name="general-installation"></a>一般安裝
**問： 是否會安裝運作 hello Azure AD 全域管理員是否已啟用的 2FA？**  
從 2016 年 2 月 hello 組建，以支援此功能。

**問： 是否有方法 tooinstall 無人看管的 Azure AD Connect？**  
它是只支援的 tooinstall Azure AD Connect 使用 hello 安裝精靈。 不支援自動和無訊息安裝。

**問：我有一個樹系，但無法連線到其中的網域。如何安裝 Azure AD Connect？**  
從 2016 年 2 月 hello 組建，以支援此功能。

**問： 沒有 hello 在 server core 上的 AD DS 健全狀況代理程式工作嗎？**  
是。 在安裝之後 hello 代理程式，您可以完成 hello 註冊程序使用下列 PowerShell cmdlet 的 hello: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>網路
**問： 我有防火牆、 網路裝置或其他項目，以限制 hello 最大時間連接可以維持開啟我的網路上。使用 Azure AD Connect 時，用戶端逾時閥值時間應該多長？**  
所有的網路軟體、 實體裝置，或其他任何項目 hello 連接可以保持開啟的最長時間應該使用至少 5 分鐘 （300 秒） 的臨界值之間的連線限制 hello hello Azure AD Connect 的用戶端安裝所在的伺服器與 Azure Active Directory。 這也適用於先前發行的 tooall Microsoft 身分識別同步處理工具。

**問：是否支援 SLD (單一標籤網域)？**  
 否，Azure AD Connect 不支援使用 SLD 的內部部署樹系/網域。

**問：是否支援有句點的 NetBios 名稱？**  
否，Azure AD 連接不支援在內部部署樹系/網域 hello NetBios 名稱包含句點的位置 」。 「 hello 名稱中。

## <a name="federation"></a>同盟
**問： 我該怎麼辦如果我收到一封電子郵件，詢問 toorenew 我的 Office 365 憑證**  
使用 hello 指南所述 hello[更新憑證](active-directory-aadconnect-o365-certs.md)上 toorenew hello 憑證的如何主題。

**問：我已經針對 O365 信賴憑證者設定「自動更新信賴憑證者」。我是否必須 tootake 任何動作時我的權杖簽署憑證會自動彙總？**  
使用 hello 文件中所述的 hello 指引[更新憑證](active-directory-aadconnect-o365-certs.md)。

## <a name="environment"></a>Environment
**問： 是否支援 it toorename hello 伺服器在安裝 Azure AD Connect 之後？**  
否。 變更 hello 伺服器名稱將原因 hello 同步處理引擎 toonot 會無法 tooconnect toohello SQL database 和 hello 服務將不能 toostart。

## <a name="identity-data"></a>身分識別資料
**問： hello UPN (userPrincipalName) 屬性，在 Azure AD 中的不符合 hello 由內部部署 UPN-為何？**  
 請參閱以下文章：

* [使用者名稱不符合在 Office 365、 Azure 或 Intune hello 在內部部署 UPN 或替代登入識別碼](https://support.microsoft.com/en-us/kb/2523192)
* [變更未同步處理 hello Azure Active Directory 同步作業工具之後變更 hello 的使用者帳戶 toouse 不同的同盟網域 UPN](https://support.microsoft.com/en-us/kb/2669550)

您也可以如所述設定 Azure AD tooallow hello 同步處理引擎 tooupdate hello userPrincipalName [Azure AD Connect 同步處理服務功能](active-directory-aadconnectsyncservice-features.md)。

**問： 是否支援 it toosoft 比對內部部署 AD 群組/連絡人物件，與現有的 Azure AD 群組/連絡人物件？**  
否，目前不支援。

**問： 是否支援 it toomanually 設定 ImmutableId 屬性上的現有 Azure AD 群組/連絡人物件 toohard 使其符合 tooon 內部部署 AD 群組/連絡人物件嗎？**  
否，目前不支援。



## <a name="custom-configuration"></a>自訂組態
**問： 哪裡適記載的 Azure AD Connect hello PowerShell 指令程式？**  
記載此站台上的 hello cmdlet 的 hello 例外狀況，以供客戶使用不支援在 Azure AD Connect 中找到其他 PowerShell cmdlet。

**問： 是否可以使用 「 伺服器伺服器匯出/匯入 」 中找到*同步處理服務管理員*toomove 伺服器之間的組態？**  
否。 此選項將不會擷取所有組態設定，因此不應使用。 您應該改為使用 hello 精靈 toocreate hello 基底組態 hello 第二部伺服器上並使用 hello 同步處理規則編輯器 toogenerate PowerShell 指令碼 toomove 伺服器之間的任何自訂規則。 請參閱[變換移轉](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)。

**問： 是否可以密碼快取 hello Azure 登入頁面上，且可以這避免因為它包含了密碼 input 的元素與 hello autocomplete ="false"的屬性？**</br>
我們目前不支援修改 hello HTML 屬性的 hello 密碼輸入欄位，包括 hello 自動完成標記。 我們目前使用中的功能，可讓您自訂的 Javascript，這可讓您 tooadd 任何屬性 toohello 密碼欄位。 應可在 2017 年下半年使用這項功能。

**問： 在 hello Azure 登入頁面，會顯示先前登入成功的使用者的使用者名稱。可以關閉此行為嗎？**</br>
我們目前不支援修改 hello HTML 屬性的 hello 登入頁面。 我們目前使用中的功能，可讓您自訂的 Javascript，這可讓您 tooadd 任何屬性 toohello 密碼欄位。 應可在 2017 年下半年使用這項功能。

**問： 是否有方法 tooprevent 並行工作階段？**</br>
否。



## <a name="troubleshooting"></a>疑難排解
**問：如何取得 Azure AD Connect 的說明？**

[搜尋 hello Microsoft 知識庫 (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* 支援 Azure AD Connect 的相關技術解決方案 toocommon 中斷的修復問題的搜尋 hello Microsoft 知識庫 (KB)。

[Microsoft Azure Active Directory 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* 您可以搜尋和瀏覽的技術問題和解答的 hello 社群成員或詢問您自己的問題，依序按一下[這裡](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)。

[Azure AD Connect 客戶支援](https://manage.windowsazure.com/?getsupport=true)

* 使用此連結 tooget 支援透過 hello Azure 入口網站。

