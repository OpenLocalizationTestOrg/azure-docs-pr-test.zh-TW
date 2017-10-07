---
title: "使用 Azure Active Directory cmdlet aaaConfigure 群組設定 |Microsoft 文件"
description: "如何管理 hello 設定為使用 Azure Active Directory cmdlets 適用的群組"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>設定群組設定的 Azure Active Directory Cmdlet

> [!IMPORTANT]
> 此內容適用於 tooOffice 365 群組。 如需有關如何 tooallow 使用者 toocreate 安全性群組、 設定`Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True`中所述[Set-msolcompanysettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)。 

Office 365 群組設定是使用 Settings 物件和 SettingsTemplate 物件所設定。 一開始，您看設定的任何物件在目錄中，因為您的目錄已設定 hello 預設設定。 toochange hello 預設設定，您必須建立新的設定物件，使用設定的範本。 設定範本是由 Microsoft 所定義。 有數個不同的設定範本。 tooconfigure Office 365 群組設定為您的目錄，您會使用名為"Group.Unified"hello 範本。 tooconfigure Office 365 群組設定在單一群組中，使用名為"Group.Unified.Guest"hello 範本。 此範本是使用的 toomanage 來賓存取 tooan Office 365 群組。 

hello cmdlet 是 hello Azure Active Directory PowerShell V2 模組的一部分。 如需相關指示如何 toodownload 和安裝 hello 模組，您在電腦上，請參閱 hello 文章[Azure Active Directory PowerShell 版本 2](https://docs.microsoft.com/powershell/azuread/)。 您可以安裝 hello 2 版的 hello 模組從[hello PowerShell 資源庫](https://www.powershellgallery.com/packages/AzureAD/)。

## <a name="retrieve-a-specific-settings-value"></a>擷取一個特定設定值
如果您知道 hello 名稱 hello 設定您想 tooretrieve，您可以使用以下 cmdlet tooretrieve hello 目前的設定值的 hello。 我們在此範例中，擷取 hello 值設定名為"UsageGuidelinesUrl。 」 您可以在本文中深入了解目錄設定及其名稱。

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>建立 hello 目錄層級的設定
這些步驟會建立設定目錄層級套用 hello 目錄中的 tooall Office 365 群組 （統一群組）。

1. 在 hello DirectorySettings cmdlet，您必須指定 hello SettingsTemplate 想 toouse hello 識別碼。 如果您不知道此識別碼，此 cmdlet 會傳回所有的設定範本 hello 清單：
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  這個 Cmdlet 呼叫會傳回所有可用的範本︰
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. tooadd 使用方式方針 URL，首先您需要 tooget hello SettingsTemplate 物件，定義 hello 使用方式方針 URL 值。也就是說，hello Group.Unified 範本：
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. 接下來，根據該範本建立新的設定物件：
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. 然後更新 hello 使用方式方針值：
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. 最後，套用 hello 設定：
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

成功完成時，hello cmdlet 會傳回 hello hello 新的設定物件識別碼：
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
以下是 hello hello Group.Unified SettingsTemplate 中定義的設定。

| **設定** | **說明** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>類型：布林值<li>預設值︰True |指出是否允許建立統一群組 hello 目錄中的 hello 旗標。 |
|  <ul><li>GroupCreationAllowedGroupId<li>類型：字串<li>預設值：“” |Hello 安全性群組的 hello 允許 toocreate 統一群組的 GUID，即使 EnableGroupCreation = = false。 |
|  <ul><li>UsageGuidelinesUrl<li>類型：字串<li>預設值：“” |連結 toohello 群組使用的指導方針。 |
|  <ul><li>ClassificationDescriptions<li>類型：字串<li>預設值：“” | 分類說明的以逗號分隔清單。 |
|  <ul><li>DefaultClassification<li>類型：字串<li>預設值：“” | hello 是 toobe 作為 hello 預設分類群組但是沒有指定的分類。|
|  <ul><li>PrefixSuffixNamingRequirement<li>類型：字串<li>預設值：“” |尚未實作
|  <ul><li>AllowGuestsToBeGroupOwner<li>類型︰布林值<li>預設值︰False | 布林值，表示來賓使用者是否可以是群組的擁有者。 |
|  <ul><li>AllowGuestsToAccessGroups<li>類型︰布林值<li>預設值︰True | 布林值，指出有 guest 使用者可以存取 tooUnified 群組的內容。 |
|  <ul><li>GuestUsageGuidelinesUrl<li>類型：字串<li>預設值：“” | hello url 連結 toohello 客體使用指導方針。 |
|  <ul><li>AllowToAddGuests<li>類型︰布林值<li>預設值︰True | 布林值，指出允許的 tooadd 遊客 toothis 目錄。|
|  <ul><li>ClassificationList<li>類型：字串<li>預設值：“” |可以是套用的 tooUnified 群組的有效的分類值的逗號分隔清單。 |
|  <ul><li>EnableGroupCreation<li>類型：布林值<li>預設值︰True | 布林值，表示非系統管理使用者是否可以建立新的整合群組。 |


## <a name="read-settings-at-hello-directory-level"></a>讀取 hello 目錄層級設定
這些步驟讀取目錄層級，套用 tooall hello 目錄中的 Office 群組的設定。

1. 讀取所有現有的目錄設定：
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  此 Cmdlet 會傳回所有目錄設定的清單：
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. 讀取特定群組的所有設定：
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. 使用設定識別碼 GUID，讀取特定目錄設定物件的所有目錄設定值︰
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  此 cmdlet 會傳回在這個設定物件，此特定群組中的 hello 名稱和值：
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a>更新特定群組的設定

1. 搜尋名為"Groups.Unified.Guest"hello 設定範本
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. 擷取 hello hello Groups.Unified.Guest 範本的範本物件：
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. 從 hello 範本建立新的設定物件：
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. 設定 hello 設定 toohello 必要值：
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. 在 hello 目錄中建立新的設定 hello hello 需要群組：
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Hello 目錄層級的更新設定

下列步驟更新目錄層級，套用 tooall 統一群組 hello 目錄中的設定。 這些範例假設您的目錄中已經有 Settings 物件。

1. 找不到 hello 現有的設定物件：
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. 更新 hello 值：
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. 更新 hello 設定：
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>移除 hello 目錄層級設定
此步驟移除目錄層級，套用 tooall hello 目錄中的 Office 群組的設定。
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Cmdlet 語法參考
您可以在 [Azure Active Directory Cmdlet](/powershell/azure/install-adv2?view=azureadps-2.0)中找到更多 Azure Active Directory PowerShell 文件。

## <a name="additional-reading"></a>其他閱讀資料

* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
