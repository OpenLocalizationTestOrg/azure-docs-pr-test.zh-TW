---
title: "使用 Azure Active Directory Cmdlet 設定群組設定 | Microsoft Docs"
description: "如何使用 Azure Active Directory Cmdlet 管理群組的設定"
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
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="681e6-103">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="681e6-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="681e6-104">本內容僅適用於 Office 365 群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="681e6-105">如需有關如何允許使用者建立安全性群組的詳細資訊，請如 [Set-msolcompanysettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) 中所述設定 `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True`。</span><span class="sxs-lookup"><span data-stu-id="681e6-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="681e6-106">Office 365 群組設定是使用 Settings 物件和 SettingsTemplate 物件所設定。</span><span class="sxs-lookup"><span data-stu-id="681e6-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="681e6-107">一開始，您在目錄中不會看到任何設定物件，因為已使用預設設定來設定您的目錄。</span><span class="sxs-lookup"><span data-stu-id="681e6-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="681e6-108">若要變更預設設定，您必須使用設定範本來建立新的設定物件。</span><span class="sxs-lookup"><span data-stu-id="681e6-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="681e6-109">設定範本是由 Microsoft 所定義。</span><span class="sxs-lookup"><span data-stu-id="681e6-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="681e6-110">有數個不同的設定範本。</span><span class="sxs-lookup"><span data-stu-id="681e6-110">There are several different settings templates.</span></span> <span data-ttu-id="681e6-111">若要設定目錄的 Office 365 群組設定，您要使用名為 "Group.Unified" 的範本。</span><span class="sxs-lookup"><span data-stu-id="681e6-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="681e6-112">若要在單一群組上設定 Office 365 群組設定，請使用名為 "Group.Unified.Guest" 的範本。</span><span class="sxs-lookup"><span data-stu-id="681e6-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="681e6-113">此範本是用來管理 Office 365 群組的來賓存取權。</span><span class="sxs-lookup"><span data-stu-id="681e6-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="681e6-114">Cmdlet 是 Azure Active Directory PowerShell V2 模組的一部分。</span><span class="sxs-lookup"><span data-stu-id="681e6-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="681e6-115">如需有關如何在電腦上下載及安裝模組的指示，請參閱 [Azure Active Directory PowerShell 第 2 版](https://docs.microsoft.com/powershell/azuread/)文章。</span><span class="sxs-lookup"><span data-stu-id="681e6-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="681e6-116">您可以從 [PowerShell 資源庫](https://www.powershellgallery.com/packages/AzureAD/)安裝第 2 版的模組。</span><span class="sxs-lookup"><span data-stu-id="681e6-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="681e6-117">擷取一個特定設定值</span><span class="sxs-lookup"><span data-stu-id="681e6-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="681e6-118">如果您知道需要擷取的設定名稱，可以使用以下 Cmdlet 來擷取目前的設定值。</span><span class="sxs-lookup"><span data-stu-id="681e6-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="681e6-119">在此範例中，我們會擷取名為 "UsageGuidelinesUrl" 的設定值。</span><span class="sxs-lookup"><span data-stu-id="681e6-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="681e6-120">您可以在本文中深入了解目錄設定及其名稱。</span><span class="sxs-lookup"><span data-stu-id="681e6-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="681e6-121">建立目錄層級的設定</span><span class="sxs-lookup"><span data-stu-id="681e6-121">Create settings at the directory level</span></span>
<span data-ttu-id="681e6-122">這些步驟會建立目錄層級的設定，其會套用至目錄中的所有 Office 365 群組整合群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="681e6-123">在 DirectorySettings Cmdlet 中，您必須指定需要使用的 SettingsTemplate 識別碼。</span><span class="sxs-lookup"><span data-stu-id="681e6-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="681e6-124">如果您不知道此識別碼，這個 Cmdlet 會傳回所有設定範本的清單：</span><span class="sxs-lookup"><span data-stu-id="681e6-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="681e6-125">這個 Cmdlet 呼叫會傳回所有可用的範本︰</span><span class="sxs-lookup"><span data-stu-id="681e6-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="681e6-126">若要新增使用方針 URL，首先您需要取得 SettingsTemplate 物件，此物件會定義使用方針 URL 值；也就是 Group.Unified 範本：</span><span class="sxs-lookup"><span data-stu-id="681e6-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="681e6-127">接下來，根據該範本建立新的設定物件：</span><span class="sxs-lookup"><span data-stu-id="681e6-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="681e6-128">然後更新使用方針值：</span><span class="sxs-lookup"><span data-stu-id="681e6-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="681e6-129">最後，套用設定：</span><span class="sxs-lookup"><span data-stu-id="681e6-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="681e6-130">成功完成時，此 Cmdlet 會傳回新設定物件的識別碼︰</span><span class="sxs-lookup"><span data-stu-id="681e6-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="681e6-131">以下是 Group.Unified SettingsTemplate 中定義的設定。</span><span class="sxs-lookup"><span data-stu-id="681e6-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="681e6-132">**設定**</span><span class="sxs-lookup"><span data-stu-id="681e6-132">**Setting**</span></span> | <span data-ttu-id="681e6-133">**說明**</span><span class="sxs-lookup"><span data-stu-id="681e6-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="681e6-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="681e6-134">EnableGroupCreation</span></span><li><span data-ttu-id="681e6-135">類型：布林值</span><span class="sxs-lookup"><span data-stu-id="681e6-135">Type: Boolean</span></span><li><span data-ttu-id="681e6-136">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="681e6-136">Default: True</span></span> |<span data-ttu-id="681e6-137">此旗標指出是否允許在目錄中建立整合的群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="681e6-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="681e6-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="681e6-139">類型：字串</span><span class="sxs-lookup"><span data-stu-id="681e6-139">Type: String</span></span><li><span data-ttu-id="681e6-140">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="681e6-140">Default: “”</span></span> |<span data-ttu-id="681e6-141">安全性群組的 GUID，即使 EnableGroupCreation == false，還是允許成員建立整合群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="681e6-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="681e6-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="681e6-143">類型：字串</span><span class="sxs-lookup"><span data-stu-id="681e6-143">Type: String</span></span><li><span data-ttu-id="681e6-144">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="681e6-144">Default: “”</span></span> |<span data-ttu-id="681e6-145">群組使用方針的連結。</span><span class="sxs-lookup"><span data-stu-id="681e6-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="681e6-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="681e6-146">ClassificationDescriptions</span></span><li><span data-ttu-id="681e6-147">類型：字串</span><span class="sxs-lookup"><span data-stu-id="681e6-147">Type: String</span></span><li><span data-ttu-id="681e6-148">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="681e6-148">Default: “”</span></span> | <span data-ttu-id="681e6-149">分類說明的以逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="681e6-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="681e6-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="681e6-150">DefaultClassification</span></span><li><span data-ttu-id="681e6-151">類型：字串</span><span class="sxs-lookup"><span data-stu-id="681e6-151">Type: String</span></span><li><span data-ttu-id="681e6-152">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="681e6-152">Default: “”</span></span> | <span data-ttu-id="681e6-153">如果尚未指定，則是做為群組預設分類的分類。</span><span class="sxs-lookup"><span data-stu-id="681e6-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="681e6-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="681e6-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="681e6-155">類型：字串</span><span class="sxs-lookup"><span data-stu-id="681e6-155">Type: String</span></span><li><span data-ttu-id="681e6-156">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="681e6-156">Default: “”</span></span> |<span data-ttu-id="681e6-157">尚未實作</span><span class="sxs-lookup"><span data-stu-id="681e6-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="681e6-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="681e6-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="681e6-159">類型︰布林值</span><span class="sxs-lookup"><span data-stu-id="681e6-159">Type: Boolean</span></span><li><span data-ttu-id="681e6-160">預設值︰False</span><span class="sxs-lookup"><span data-stu-id="681e6-160">Default: False</span></span> | <span data-ttu-id="681e6-161">布林值，表示來賓使用者是否可以是群組的擁有者。</span><span class="sxs-lookup"><span data-stu-id="681e6-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="681e6-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="681e6-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="681e6-163">類型︰布林值</span><span class="sxs-lookup"><span data-stu-id="681e6-163">Type: Boolean</span></span><li><span data-ttu-id="681e6-164">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="681e6-164">Default: True</span></span> | <span data-ttu-id="681e6-165">布林值，表示來賓使用者是否可以具有整合群組內容的存取權。</span><span class="sxs-lookup"><span data-stu-id="681e6-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="681e6-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="681e6-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="681e6-167">類型：字串</span><span class="sxs-lookup"><span data-stu-id="681e6-167">Type: String</span></span><li><span data-ttu-id="681e6-168">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="681e6-168">Default: “”</span></span> | <span data-ttu-id="681e6-169">來賓使用指導方針的連結 url。</span><span class="sxs-lookup"><span data-stu-id="681e6-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="681e6-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="681e6-170">AllowToAddGuests</span></span><li><span data-ttu-id="681e6-171">類型︰布林值</span><span class="sxs-lookup"><span data-stu-id="681e6-171">Type: Boolean</span></span><li><span data-ttu-id="681e6-172">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="681e6-172">Default: True</span></span> | <span data-ttu-id="681e6-173">布林值表示是否允許將來賓新增至此目錄。</span><span class="sxs-lookup"><span data-stu-id="681e6-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="681e6-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="681e6-174">ClassificationList</span></span><li><span data-ttu-id="681e6-175">類型：字串</span><span class="sxs-lookup"><span data-stu-id="681e6-175">Type: String</span></span><li><span data-ttu-id="681e6-176">預設值：“”</span><span class="sxs-lookup"><span data-stu-id="681e6-176">Default: “”</span></span> |<span data-ttu-id="681e6-177">以逗號分隔的有效分類值清單，這些值可以套用到整合的群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="681e6-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="681e6-178">EnableGroupCreation</span></span><li><span data-ttu-id="681e6-179">類型：布林值</span><span class="sxs-lookup"><span data-stu-id="681e6-179">Type: Boolean</span></span><li><span data-ttu-id="681e6-180">預設值︰True</span><span class="sxs-lookup"><span data-stu-id="681e6-180">Default: True</span></span> | <span data-ttu-id="681e6-181">布林值，表示非系統管理使用者是否可以建立新的整合群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="681e6-182">讀取目錄層級的設定</span><span class="sxs-lookup"><span data-stu-id="681e6-182">Read settings at the directory level</span></span>
<span data-ttu-id="681e6-183">這些步驟會讀取目錄層級的設定，其會套用至目錄中的所有 Office 群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="681e6-184">讀取所有現有的目錄設定：</span><span class="sxs-lookup"><span data-stu-id="681e6-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="681e6-185">此 Cmdlet 會傳回所有目錄設定的清單：</span><span class="sxs-lookup"><span data-stu-id="681e6-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="681e6-186">讀取特定群組的所有設定：</span><span class="sxs-lookup"><span data-stu-id="681e6-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="681e6-187">使用設定識別碼 GUID，讀取特定目錄設定物件的所有目錄設定值︰</span><span class="sxs-lookup"><span data-stu-id="681e6-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="681e6-188">此 Cmdlet 會傳回針對此特定群組的這個設定物件中的名稱和值：</span><span class="sxs-lookup"><span data-stu-id="681e6-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="681e6-189">更新特定群組的設定</span><span class="sxs-lookup"><span data-stu-id="681e6-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="681e6-190">搜尋名為「Groups.Unified.Guest」的設定範本</span><span class="sxs-lookup"><span data-stu-id="681e6-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="681e6-191">擷取 Groups.Unified.Guest 範本的範本物件：</span><span class="sxs-lookup"><span data-stu-id="681e6-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="681e6-192">從範本建立新的設定物件︰</span><span class="sxs-lookup"><span data-stu-id="681e6-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="681e6-193">將設定設為必要值︰</span><span class="sxs-lookup"><span data-stu-id="681e6-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="681e6-194">在目錄中建立必要群組的新設定︰</span><span class="sxs-lookup"><span data-stu-id="681e6-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="681e6-195">更新目錄層級的設定</span><span class="sxs-lookup"><span data-stu-id="681e6-195">Update settings at the directory level</span></span>

<span data-ttu-id="681e6-196">這些步驟會更新目錄層級的設定，其會套用至目錄中的所有整合群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="681e6-197">這些範例假設您的目錄中已經有 Settings 物件。</span><span class="sxs-lookup"><span data-stu-id="681e6-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="681e6-198">尋找現有的 Settings 物件：</span><span class="sxs-lookup"><span data-stu-id="681e6-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="681e6-199">更新值：</span><span class="sxs-lookup"><span data-stu-id="681e6-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="681e6-200">更新設定：</span><span class="sxs-lookup"><span data-stu-id="681e6-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="681e6-201">移除目錄層級的設定</span><span class="sxs-lookup"><span data-stu-id="681e6-201">Remove settings at the directory level</span></span>
<span data-ttu-id="681e6-202">這個步驟會移除目錄層級的設定，其會套用至目錄中的所有 Office 群組。</span><span class="sxs-lookup"><span data-stu-id="681e6-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="681e6-203">Cmdlet 語法參考</span><span class="sxs-lookup"><span data-stu-id="681e6-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="681e6-204">您可以在 [Azure Active Directory Cmdlet](/powershell/azure/install-adv2?view=azureadps-2.0)中找到更多 Azure Active Directory PowerShell 文件。</span><span class="sxs-lookup"><span data-stu-id="681e6-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="681e6-205">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="681e6-205">Additional reading</span></span>

* [<span data-ttu-id="681e6-206">使用 Azure Active Directory 群組來管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="681e6-206">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="681e6-207">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="681e6-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
