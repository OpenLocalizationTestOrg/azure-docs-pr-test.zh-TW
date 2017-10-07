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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="07467-103">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="07467-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07467-104">此內容適用於 tooOffice 365 群組。</span><span class="sxs-lookup"><span data-stu-id="07467-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="07467-105">如需有關如何 tooallow 使用者 toocreate 安全性群組、 設定`Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True`中所述[Set-msolcompanysettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)。</span><span class="sxs-lookup"><span data-stu-id="07467-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="07467-106">Office 365 群組設定是使用 Settings 物件和 SettingsTemplate 物件所設定。</span><span class="sxs-lookup"><span data-stu-id="07467-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="07467-107">一開始，您看設定的任何物件在目錄中，因為您的目錄已設定 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="07467-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="07467-108">toochange hello 預設設定，您必須建立新的設定物件，使用設定的範本。</span><span class="sxs-lookup"><span data-stu-id="07467-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="07467-109">設定範本是由 Microsoft 所定義。</span><span class="sxs-lookup"><span data-stu-id="07467-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="07467-110">有數個不同的設定範本。</span><span class="sxs-lookup"><span data-stu-id="07467-110">There are several different settings templates.</span></span> <span data-ttu-id="07467-111">tooconfigure Office 365 群組設定為您的目錄，您會使用名為"Group.Unified"hello 範本。</span><span class="sxs-lookup"><span data-stu-id="07467-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="07467-112">tooconfigure Office 365 群組設定在單一群組中，使用名為"Group.Unified.Guest"hello 範本。</span><span class="sxs-lookup"><span data-stu-id="07467-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="07467-113">此範本是使用的 toomanage 來賓存取 tooan Office 365 群組。</span><span class="sxs-lookup"><span data-stu-id="07467-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="07467-114">hello cmdlet 是 hello Azure Active Directory PowerShell V2 模組的一部分。</span><span class="sxs-lookup"><span data-stu-id="07467-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="07467-115">如需相關指示如何 toodownload 和安裝 hello 模組，您在電腦上，請參閱 hello 文章[Azure Active Directory PowerShell 版本 2](https://docs.microsoft.com/powershell/azuread/)。</span><span class="sxs-lookup"><span data-stu-id="07467-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="07467-116">您可以安裝 hello 2 版的 hello 模組從[hello PowerShell 資源庫](https://www.powershellgallery.com/packages/AzureAD/)。</span><span class="sxs-lookup"><span data-stu-id="07467-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="07467-117">擷取一個特定設定值</span><span class="sxs-lookup"><span data-stu-id="07467-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="07467-118">如果您知道 hello 名稱 hello 設定您想 tooretrieve，您可以使用以下 cmdlet tooretrieve hello 目前的設定值的 hello。</span><span class="sxs-lookup"><span data-stu-id="07467-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="07467-119">我們在此範例中，擷取 hello 值設定名為"UsageGuidelinesUrl。 」</span><span class="sxs-lookup"><span data-stu-id="07467-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="07467-120">您可以在本文中深入了解目錄設定及其名稱。</span><span class="sxs-lookup"><span data-stu-id="07467-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="07467-121">建立 hello 目錄層級的設定</span><span class="sxs-lookup"><span data-stu-id="07467-121">Create settings at hello directory level</span></span>
<span data-ttu-id="07467-122">這些步驟會建立設定目錄層級套用 hello 目錄中的 tooall Office 365 群組 （統一群組）。</span><span class="sxs-lookup"><span data-stu-id="07467-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="07467-123">在 hello DirectorySettings cmdlet，您必須指定 hello SettingsTemplate 想 toouse hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="07467-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="07467-124">如果您不知道此識別碼，此 cmdlet 會傳回所有的設定範本 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="07467-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="07467-125">這個 Cmdlet 呼叫會傳回所有可用的範本︰</span><span class="sxs-lookup"><span data-stu-id="07467-125">This cmdlet call returns all templates that are available:</span></span>
  
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
2. <span data-ttu-id="07467-126">tooadd 使用方式方針 URL，首先您需要 tooget hello SettingsTemplate 物件，定義 hello 使用方式方針 URL 值。也就是說，hello Group.Unified 範本：</span><span class="sxs-lookup"><span data-stu-id="07467-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="07467-127">接下來，根據該範本建立新的設定物件：</span><span class="sxs-lookup"><span data-stu-id="07467-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="07467-128">然後更新 hello 使用方式方針值：</span><span class="sxs-lookup"><span data-stu-id="07467-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="07467-129">最後，套用 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="07467-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="07467-130">成功完成時，hello cmdlet 會傳回 hello hello 新的設定物件識別碼：</span><span class="sxs-lookup"><span data-stu-id="07467-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="07467-131">以下是 hello hello Group.Unified SettingsTemplate 中定義的設定。</span><span class="sxs-lookup"><span data-stu-id="07467-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="07467-132">**設定**</span><span class="sxs-lookup"><span data-stu-id="07467-132">**Setting**</span></span> | <span data-ttu-id="07467-133">**說明**</span><span class="sxs-lookup"><span data-stu-id="07467-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="07467-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="07467-134">EnableGroupCreation</span></span><li><span data-ttu-id="07467-135">類型：布林值</span><span class="sxs-lookup"><span data-stu-id="07467-135">Type: Boolean</span></span><li><span data-ttu-id="07467-136">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="07467-136">Default: True</span></span> |<span data-ttu-id="07467-137">指出是否允許建立統一群組 hello 目錄中的 hello 旗標。</span><span class="sxs-lookup"><span data-stu-id="07467-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="07467-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="07467-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="07467-139">類型：字串</span><span class="sxs-lookup"><span data-stu-id="07467-139">Type: String</span></span><li><span data-ttu-id="07467-140">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="07467-140">Default: “”</span></span> |<span data-ttu-id="07467-141">Hello 安全性群組的 hello 允許 toocreate 統一群組的 GUID，即使 EnableGroupCreation = = false。</span><span class="sxs-lookup"><span data-stu-id="07467-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="07467-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="07467-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="07467-143">類型：字串</span><span class="sxs-lookup"><span data-stu-id="07467-143">Type: String</span></span><li><span data-ttu-id="07467-144">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="07467-144">Default: “”</span></span> |<span data-ttu-id="07467-145">連結 toohello 群組使用的指導方針。</span><span class="sxs-lookup"><span data-stu-id="07467-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="07467-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="07467-146">ClassificationDescriptions</span></span><li><span data-ttu-id="07467-147">類型：字串</span><span class="sxs-lookup"><span data-stu-id="07467-147">Type: String</span></span><li><span data-ttu-id="07467-148">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="07467-148">Default: “”</span></span> | <span data-ttu-id="07467-149">分類說明的以逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="07467-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="07467-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="07467-150">DefaultClassification</span></span><li><span data-ttu-id="07467-151">類型：字串</span><span class="sxs-lookup"><span data-stu-id="07467-151">Type: String</span></span><li><span data-ttu-id="07467-152">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="07467-152">Default: “”</span></span> | <span data-ttu-id="07467-153">hello 是 toobe 作為 hello 預設分類群組但是沒有指定的分類。</span><span class="sxs-lookup"><span data-stu-id="07467-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="07467-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="07467-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="07467-155">類型：字串</span><span class="sxs-lookup"><span data-stu-id="07467-155">Type: String</span></span><li><span data-ttu-id="07467-156">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="07467-156">Default: “”</span></span> |<span data-ttu-id="07467-157">尚未實作</span><span class="sxs-lookup"><span data-stu-id="07467-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="07467-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="07467-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="07467-159">類型︰布林值</span><span class="sxs-lookup"><span data-stu-id="07467-159">Type: Boolean</span></span><li><span data-ttu-id="07467-160">預設值︰False</span><span class="sxs-lookup"><span data-stu-id="07467-160">Default: False</span></span> | <span data-ttu-id="07467-161">布林值，表示來賓使用者是否可以是群組的擁有者。</span><span class="sxs-lookup"><span data-stu-id="07467-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="07467-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="07467-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="07467-163">類型︰布林值</span><span class="sxs-lookup"><span data-stu-id="07467-163">Type: Boolean</span></span><li><span data-ttu-id="07467-164">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="07467-164">Default: True</span></span> | <span data-ttu-id="07467-165">布林值，指出有 guest 使用者可以存取 tooUnified 群組的內容。</span><span class="sxs-lookup"><span data-stu-id="07467-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="07467-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="07467-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="07467-167">類型：字串</span><span class="sxs-lookup"><span data-stu-id="07467-167">Type: String</span></span><li><span data-ttu-id="07467-168">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="07467-168">Default: “”</span></span> | <span data-ttu-id="07467-169">hello url 連結 toohello 客體使用指導方針。</span><span class="sxs-lookup"><span data-stu-id="07467-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="07467-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="07467-170">AllowToAddGuests</span></span><li><span data-ttu-id="07467-171">類型︰布林值</span><span class="sxs-lookup"><span data-stu-id="07467-171">Type: Boolean</span></span><li><span data-ttu-id="07467-172">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="07467-172">Default: True</span></span> | <span data-ttu-id="07467-173">布林值，指出允許的 tooadd 遊客 toothis 目錄。</span><span class="sxs-lookup"><span data-stu-id="07467-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="07467-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="07467-174">ClassificationList</span></span><li><span data-ttu-id="07467-175">類型：字串</span><span class="sxs-lookup"><span data-stu-id="07467-175">Type: String</span></span><li><span data-ttu-id="07467-176">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="07467-176">Default: “”</span></span> |<span data-ttu-id="07467-177">可以是套用的 tooUnified 群組的有效的分類值的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="07467-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="07467-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="07467-178">EnableGroupCreation</span></span><li><span data-ttu-id="07467-179">類型：布林值</span><span class="sxs-lookup"><span data-stu-id="07467-179">Type: Boolean</span></span><li><span data-ttu-id="07467-180">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="07467-180">Default: True</span></span> | <span data-ttu-id="07467-181">布林值，表示非系統管理使用者是否可以建立新的整合群組。</span><span class="sxs-lookup"><span data-stu-id="07467-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="07467-182">讀取 hello 目錄層級設定</span><span class="sxs-lookup"><span data-stu-id="07467-182">Read settings at hello directory level</span></span>
<span data-ttu-id="07467-183">這些步驟讀取目錄層級，套用 tooall hello 目錄中的 Office 群組的設定。</span><span class="sxs-lookup"><span data-stu-id="07467-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="07467-184">讀取所有現有的目錄設定：</span><span class="sxs-lookup"><span data-stu-id="07467-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="07467-185">此 Cmdlet 會傳回所有目錄設定的清單：</span><span class="sxs-lookup"><span data-stu-id="07467-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="07467-186">讀取特定群組的所有設定：</span><span class="sxs-lookup"><span data-stu-id="07467-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="07467-187">使用設定識別碼 GUID，讀取特定目錄設定物件的所有目錄設定值︰</span><span class="sxs-lookup"><span data-stu-id="07467-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="07467-188">此 cmdlet 會傳回在這個設定物件，此特定群組中的 hello 名稱和值：</span><span class="sxs-lookup"><span data-stu-id="07467-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="07467-189">更新特定群組的設定</span><span class="sxs-lookup"><span data-stu-id="07467-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="07467-190">搜尋名為"Groups.Unified.Guest"hello 設定範本</span><span class="sxs-lookup"><span data-stu-id="07467-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="07467-191">擷取 hello hello Groups.Unified.Guest 範本的範本物件：</span><span class="sxs-lookup"><span data-stu-id="07467-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="07467-192">從 hello 範本建立新的設定物件：</span><span class="sxs-lookup"><span data-stu-id="07467-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="07467-193">設定 hello 設定 toohello 必要值：</span><span class="sxs-lookup"><span data-stu-id="07467-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="07467-194">在 hello 目錄中建立新的設定 hello hello 需要群組：</span><span class="sxs-lookup"><span data-stu-id="07467-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="07467-195">Hello 目錄層級的更新設定</span><span class="sxs-lookup"><span data-stu-id="07467-195">Update settings at hello directory level</span></span>

<span data-ttu-id="07467-196">下列步驟更新目錄層級，套用 tooall 統一群組 hello 目錄中的設定。</span><span class="sxs-lookup"><span data-stu-id="07467-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="07467-197">這些範例假設您的目錄中已經有 Settings 物件。</span><span class="sxs-lookup"><span data-stu-id="07467-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="07467-198">找不到 hello 現有的設定物件：</span><span class="sxs-lookup"><span data-stu-id="07467-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="07467-199">更新 hello 值：</span><span class="sxs-lookup"><span data-stu-id="07467-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="07467-200">更新 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="07467-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="07467-201">移除 hello 目錄層級設定</span><span class="sxs-lookup"><span data-stu-id="07467-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="07467-202">此步驟移除目錄層級，套用 tooall hello 目錄中的 Office 群組的設定。</span><span class="sxs-lookup"><span data-stu-id="07467-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="07467-203">Cmdlet 語法參考</span><span class="sxs-lookup"><span data-stu-id="07467-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="07467-204">您可以在 [Azure Active Directory Cmdlet](/powershell/azure/install-adv2?view=azureadps-2.0)中找到更多 Azure Active Directory PowerShell 文件。</span><span class="sxs-lookup"><span data-stu-id="07467-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="07467-205">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="07467-205">Additional reading</span></span>

* [<span data-ttu-id="07467-206">使用 Azure Active Directory 群組來管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="07467-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="07467-207">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07467-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
