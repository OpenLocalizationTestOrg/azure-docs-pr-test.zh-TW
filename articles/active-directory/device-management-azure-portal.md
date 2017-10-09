---
title: "使用 aaaManaging 裝置 hello Azure 入口網站-預覽 |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 toomanage 裝置。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="63e91-103">管理使用的裝置 hello Azure 入口網站-預覽</span><span class="sxs-lookup"><span data-stu-id="63e91-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="63e91-104">這項功能目前為公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="63e91-104">This capability currently is in public preview.</span></span> <span data-ttu-id="63e91-105">準備 toorevert 或移除任何變更。</span><span class="sxs-lookup"><span data-stu-id="63e91-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="63e91-106">公開預覽期間的任何 Azure Active Directory (Azure AD) 訂用帳戶中使用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="63e91-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="63e91-107">不過，hello 功能正式推出時，某些層面 hello 功能可能需要 Azure Active Directory premium 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="63e91-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="63e91-108">使用 Azure Active Directory (Azure AD) 中的裝置管理，您可以確保使用者會從符合安全性與合規性之標準的裝置來存取您的資源。</span><span class="sxs-lookup"><span data-stu-id="63e91-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="63e91-109">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="63e91-109">This topic:</span></span>

- <span data-ttu-id="63e91-110">假設您熟悉 hello[簡介 toodevice 管理 Azure Active Directory 中](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="63e91-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="63e91-111">提供您管理您的裝置使用的相關資訊與 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="63e91-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="63e91-112">toomanage 裝置 hello Azure 入口網站中的，您需要 tooclick**裝置**在 hello**管理**區段 hello hello **Azure Active Directory**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63e91-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![管理 Intune 裝置](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="63e91-114">設定裝置設定</span><span class="sxs-lookup"><span data-stu-id="63e91-114">Configure device settings</span></span>

<span data-ttu-id="63e91-115">您的裝置使用 hello Azure 入口網站，他們需要 toobe toomanage 註冊或聯結 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="63e91-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="63e91-116">身為管理員，您可以微調 hello 註冊，並將裝置設定 hello 裝置設定程序。</span><span class="sxs-lookup"><span data-stu-id="63e91-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![管理 Intune 裝置](./media/device-management-azure-portal/22.png)


<span data-ttu-id="63e91-118">hello 裝置設定 刀鋒視窗，可讓您 tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="63e91-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="63e91-119">**使用者可以將裝置 tooAzure AD** -這個設定可讓您可以加入裝置 tooAzure AD tooselect hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="63e91-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="63e91-120">hello 預設值是**所有**。</span><span class="sxs-lookup"><span data-stu-id="63e91-120">hello default is **All**.</span></span>

- <span data-ttu-id="63e91-121">**Azure AD 的其他本機系統管理員已加入裝置**-您可以選取在裝置上的本機系統管理員權限授與 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="63e91-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="63e91-122">如果在此處加入使用者加入 toohello*裝置系統管理員*在 Azure AD 中的角色。</span><span class="sxs-lookup"><span data-stu-id="63e91-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="63e91-123">Azure AD 中的全域管理員和裝置擁有者預設會授與本機系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="63e91-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="63e91-124">此選項是 premium edition 的功能可透過 Azure AD Premium 或 Enterprise Mobility Suite (EMS) hello 等產品。</span><span class="sxs-lookup"><span data-stu-id="63e91-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="63e91-125">**使用者可以向 Azure AD 註冊其裝置**-您需要向 Azure AD 中註冊此設定 tooallow 裝置 toobe tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="63e91-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="63e91-126">如果您選取**無**，不允許 tooregister 未加入的 Azure AD 或 Azure AD 加入的混合式裝置。</span><span class="sxs-lookup"><span data-stu-id="63e91-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="63e91-127">需要先註冊 (registration)，才可註冊 (enrollment) Microsoft Intune 或適用於 Office 365 的行動裝置管理 (MDM)。</span><span class="sxs-lookup"><span data-stu-id="63e91-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="63e91-128">如果您已設定任一服務，則會選取 [全部] 且無法使用 [無]。</span><span class="sxs-lookup"><span data-stu-id="63e91-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="63e91-129">**需要 Multi-factor Auth toojoin 裝置**-您可以選擇使用者是否需要的 tooprovide 第二個驗證因素 toojoin 其裝置 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="63e91-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="63e91-130">hello 預設值是**否**。</span><span class="sxs-lookup"><span data-stu-id="63e91-130">hello default is **No**.</span></span> <span data-ttu-id="63e91-131">建議在註冊裝置時要求 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="63e91-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="63e91-132">啟用此服務的多重要素驗證之前，您必須確定 hello 使用者註冊其裝置的設定多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="63e91-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="63e91-133">如需不同 Azure Multi-Factor Authentication 服務的詳細資訊，請參閱[開始使用 Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="63e91-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="63e91-134">**裝置數目上限**-此設定可讓您的使用者可以在 Azure AD 中擁有的裝置 tooselect hello 最大數目。</span><span class="sxs-lookup"><span data-stu-id="63e91-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="63e91-135">如果使用者達到此配額時，直到其中一個會無法可以 tooadd 其他裝置或多 hello 現有裝置的移除。</span><span class="sxs-lookup"><span data-stu-id="63e91-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="63e91-136">針對所有的裝置加入 Azure AD 或 Azure AD 註冊今天計算 hello 裝置引號。</span><span class="sxs-lookup"><span data-stu-id="63e91-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="63e91-137">hello 預設值是**20**。</span><span class="sxs-lookup"><span data-stu-id="63e91-137">hello default value is **20**.</span></span>

- <span data-ttu-id="63e91-138">**使用者可以跨裝置同步設定及應用程式資料**-根據預設，此設定為太**NONE**。</span><span class="sxs-lookup"><span data-stu-id="63e91-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="63e91-139">選取特定的使用者或群組，或全部允許 hello 使用者的設定和應用程式資料 toosync 跨他們的 Windows 10 裝置。</span><span class="sxs-lookup"><span data-stu-id="63e91-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="63e91-140">深入了解同步在 Windows 10 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="63e91-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="63e91-141">這個選項是可透過 Azure AD Premium 或 Enterprise Mobility Suite (EMS) hello 等產品的高階功能。</span><span class="sxs-lookup"><span data-stu-id="63e91-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![管理 Intune 裝置](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="63e91-143">尋找裝置</span><span class="sxs-lookup"><span data-stu-id="63e91-143">Locate devices</span></span>

<span data-ttu-id="63e91-144">身為管理員，在 hello Azure 入口網站，您有兩個選項 toolocate 已註冊，並加入裝置：</span><span class="sxs-lookup"><span data-stu-id="63e91-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="63e91-145">**所有裝置**在 hello**管理**區段 hello**裝置**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="63e91-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![所有裝置](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="63e91-147">**裝置**在 hello**管理**區段**使用者**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="63e91-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![所有裝置](./media/device-management-azure-portal/43.png)



<span data-ttu-id="63e91-149">兩個選項，您可以使用取得 tooa 檢視的：</span><span class="sxs-lookup"><span data-stu-id="63e91-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="63e91-150">可讓您 toosearch 裝置做為篩選條件使用 hello 顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="63e91-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="63e91-151">為您提供已註冊和已加入裝置的詳細概觀</span><span class="sxs-lookup"><span data-stu-id="63e91-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="63e91-152">可讓您 tooperform 一般裝置管理工作</span><span class="sxs-lookup"><span data-stu-id="63e91-152">Enables you tooperform common device management tasks</span></span>
   

![所有裝置](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="63e91-154">裝置管理工作</span><span class="sxs-lookup"><span data-stu-id="63e91-154">Device management tasks</span></span>

<span data-ttu-id="63e91-155">身為管理員，您可以管理 hello 註冊或已加入的裝置。</span><span class="sxs-lookup"><span data-stu-id="63e91-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="63e91-156">本節為您提供一般裝置管理工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="63e91-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="63e91-157">**管理 Intune 裝置** - 如果您是 Intune 系統管理員，您可以管理標示為 **Microsoft Intune** 的裝置。</span><span class="sxs-lookup"><span data-stu-id="63e91-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="63e91-158">系統管理員可能會看到其他裝置</span><span class="sxs-lookup"><span data-stu-id="63e91-158">An administrator can see additional device</span></span> 

![管理 Intune 裝置](./media/device-management-azure-portal/31.png)


<span data-ttu-id="63e91-160">**啟用/停用 Azure AD 裝置**</span><span class="sxs-lookup"><span data-stu-id="63e91-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="63e91-161">tooenable 或停用裝置，您會需要在 Azure AD 中 toobe 全域管理員。</span><span class="sxs-lookup"><span data-stu-id="63e91-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="63e91-162">停用裝置可防止裝置存取您的 Azure AD 資源。</span><span class="sxs-lookup"><span data-stu-id="63e91-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="63e91-163">toodisable hello 裝置，您可以按一下*...*</span><span class="sxs-lookup"><span data-stu-id="63e91-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="63e91-164">按一下 hello 裝置以取得其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="63e91-164">click hello device for additional details.</span></span>

 
![管理 Intune 裝置](./media/device-management-azure-portal/33.png)

<span data-ttu-id="63e91-166">停用裝置 hello 會將狀態變更在 hello**啟用**資料行太**否**。</span><span class="sxs-lookup"><span data-stu-id="63e91-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![停用裝置](./media/device-management-azure-portal/32.png)


<span data-ttu-id="63e91-168">**刪除 Azure AD 裝置**-toodelete 裝置，您需要在 Azure AD 中的 toobe 全域管理員。</span><span class="sxs-lookup"><span data-stu-id="63e91-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="63e91-169">刪除裝置：</span><span class="sxs-lookup"><span data-stu-id="63e91-169">Deleting a device:</span></span>
 
- <span data-ttu-id="63e91-170">防止裝置存取您的 Azure AD 資源</span><span class="sxs-lookup"><span data-stu-id="63e91-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="63e91-171">移除所有詳細資料會附加的 toohello 裝置，例如，適用於 Windows 裝置的 BitLocker 金鑰</span><span class="sxs-lookup"><span data-stu-id="63e91-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="63e91-172">代表無法復原的活動，除非必要，否則不建議使用</span><span class="sxs-lookup"><span data-stu-id="63e91-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="63e91-173">如果裝置已由另一個管理授權單位 (例如 Microsoft Intune) 管理，請確定已抹除 / 淘汰之前刪除 Azure AD 中的 hello 裝置 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="63e91-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="63e91-174">您可選取 […]</span><span class="sxs-lookup"><span data-stu-id="63e91-174">You can either select “…”</span></span> <span data-ttu-id="63e91-175">toodelete hello 裝置，或按一下 其他詳細資料的 hello 裝置上</span><span class="sxs-lookup"><span data-stu-id="63e91-175">toodelete hello device or click on hello device for additional details</span></span>
 
![刪除裝置](./media/device-management-azure-portal/34.png)


<span data-ttu-id="63e91-177">**檢視或複製裝置識別碼**-您可以在 hello 裝置或使用 PowerShell 在疑難排解期間使用裝置識別碼 tooverify hello 裝置識別碼詳細資料。</span><span class="sxs-lookup"><span data-stu-id="63e91-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="63e91-178">tooaccess hello 複製選項，請按一下 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="63e91-178">tooaccess hello copy option, click hello device.</span></span>

![檢視裝置識別碼](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="63e91-180">**檢視或複製 BitLocker 金鑰**-如果您是系統管理員，您可以檢視和複製 hello BitLocker 金鑰 toohelp 使用者 toorecover 加密的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="63e91-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="63e91-181">這些金鑰只適用於已加密並將其金鑰儲存在 Azure AD 中的 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="63e91-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="63e91-182">存取 hello 裝置的詳細資料時，您可以複製這些機碼。</span><span class="sxs-lookup"><span data-stu-id="63e91-182">You can copy these keys when accessing details of hello device.</span></span>
 
![檢視 BitLocker 金鑰](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="63e91-184">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="63e91-184">Audit logs</span></span>


<span data-ttu-id="63e91-185">hello 裝置活動皆可透過 hello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="63e91-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="63e91-186">這包括觸發 hello 裝置註冊服務或由 hello 使用者的活動：</span><span class="sxs-lookup"><span data-stu-id="63e91-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="63e91-187">建立裝置和 hello 裝置上加入擁有者/使用者</span><span class="sxs-lookup"><span data-stu-id="63e91-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="63e91-188">變更 toodevice 設定</span><span class="sxs-lookup"><span data-stu-id="63e91-188">Changes toodevice settings</span></span>

- <span data-ttu-id="63e91-189">刪除或更新裝置等裝置作業</span><span class="sxs-lookup"><span data-stu-id="63e91-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="63e91-190">是您稽核資料的項目點 toohello**稽核記錄檔**在 hello**活動**hello 區段 **裝置*刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63e91-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![稽核記錄檔](./media/device-management-azure-portal/61.png)


<span data-ttu-id="63e91-192">稽核記錄的預設清單檢視顯示︰</span><span class="sxs-lookup"><span data-stu-id="63e91-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="63e91-193">hello 日期和時間 hello 出現項目</span><span class="sxs-lookup"><span data-stu-id="63e91-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="63e91-194">hello 目標</span><span class="sxs-lookup"><span data-stu-id="63e91-194">hello targets</span></span>

- <span data-ttu-id="63e91-195">hello 啟動器 / 動作項目 （使用者） 的活動</span><span class="sxs-lookup"><span data-stu-id="63e91-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="63e91-196">hello 活動 （目標）</span><span class="sxs-lookup"><span data-stu-id="63e91-196">hello activity (what)</span></span>

![稽核記錄檔](./media/device-management-azure-portal/63.png)

<span data-ttu-id="63e91-198">您可以自訂 hello 清單檢視中，依序按一下**資料行**hello 工具列中。</span><span class="sxs-lookup"><span data-stu-id="63e91-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![稽核記錄檔](./media/device-management-azure-portal/64.png)


<span data-ttu-id="63e91-200">向下 hello toonarrow 報告資料 tooa 層級，適用於您，您可以篩選 hello 稽核資料，使用下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="63e91-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="63e91-201">分類</span><span class="sxs-lookup"><span data-stu-id="63e91-201">Catergory</span></span>
- <span data-ttu-id="63e91-202">活動資源類型</span><span class="sxs-lookup"><span data-stu-id="63e91-202">Activity resource type</span></span>
- <span data-ttu-id="63e91-203">活動</span><span class="sxs-lookup"><span data-stu-id="63e91-203">Activity</span></span>
- <span data-ttu-id="63e91-204">日期範圍</span><span class="sxs-lookup"><span data-stu-id="63e91-204">Date range</span></span>
- <span data-ttu-id="63e91-205">目標</span><span class="sxs-lookup"><span data-stu-id="63e91-205">Target</span></span>
- <span data-ttu-id="63e91-206">啟動者 (執行者)</span><span class="sxs-lookup"><span data-stu-id="63e91-206">Initiated By (Actor)</span></span>

<span data-ttu-id="63e91-207">此外 toohello 篩選，您可以搜尋特定的項目。</span><span class="sxs-lookup"><span data-stu-id="63e91-207">In addition toohello filters, you can search for specific entries.</span></span>

![稽核記錄檔](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="63e91-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63e91-209">Next steps</span></span>

* [<span data-ttu-id="63e91-210">Azure Active Directory 中的簡介 toodevice 管理</span><span class="sxs-lookup"><span data-stu-id="63e91-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



