---
title: "使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫伺服器 | Microsoft Docs"
description: "本文說明如何使用 Azure 入口網站，快速建立新的「適用於 MySQL 的 Azure 資料庫」伺服器和管理伺服器。"
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="d880d-103">使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="d880d-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="d880d-104">本文說明如何使用 Azure 入口網站，快速建立新的「適用於 MySQL 的 Azure 資料庫」伺服器和管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="d880d-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.</span></span> <span data-ttu-id="d880d-105">伺服器管理包括檢視伺服器詳細資料和資料庫、重設密碼及刪除伺服器。</span><span class="sxs-lookup"><span data-stu-id="d880d-105">Server management includes viewing server details & databases, resetting password and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="d880d-106">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d880d-106">Log in to the Azure portal</span></span>
<span data-ttu-id="d880d-107">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d880d-107">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="d880d-108">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="d880d-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="d880d-109">請遵循下列步驟建立名為 "mysqlserver4demo" 的「適用於 MySQL 的 Azure 資料庫」伺服器</span><span class="sxs-lookup"><span data-stu-id="d880d-109">Follow these steps to create an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="d880d-110">1- 按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d880d-110">1- Click **New** button found on the upper left-hand corner of the Azure portal.</span></span>

<span data-ttu-id="d880d-111">2- 從 [新增] 頁面中選取 [資料庫]，然後從 [資料庫] 頁面中選取 [適用於 MySQL 的 Azure 資料庫]。</span><span class="sxs-lookup"><span data-stu-id="d880d-111">2- Select **Databases** from the New page, and select **Azure Database for MySQL** from the Databases page.</span></span>

> <span data-ttu-id="d880d-112">建立的「適用於 MySQL 的 Azure 資料庫」伺服器會有一組已定義的[計算和儲存體](./concepts-compute-unit-and-storage.md)資源。</span><span class="sxs-lookup"><span data-stu-id="d880d-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="d880d-113">建立的資料庫位於 Azure 資源群組和「適用於 MySQL 的 Azure 資料庫」伺服器中。</span><span class="sxs-lookup"><span data-stu-id="d880d-113">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![建立新的伺服器](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="d880d-115">3- 在「適用於 MySQL 的 Azure 資料庫」表單中填寫下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="d880d-115">3- Fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="d880d-116">**表單欄位**</span><span class="sxs-lookup"><span data-stu-id="d880d-116">**Form Field**</span></span> | <span data-ttu-id="d880d-117">**欄位描述**</span><span class="sxs-lookup"><span data-stu-id="d880d-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="d880d-118">*伺服器名稱*</span><span class="sxs-lookup"><span data-stu-id="d880d-118">*Server name*</span></span> | <span data-ttu-id="d880d-119">azure-mysql (伺服器名稱是全域唯一的)</span><span class="sxs-lookup"><span data-stu-id="d880d-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="d880d-120">*訂用帳戶*</span><span class="sxs-lookup"><span data-stu-id="d880d-120">*Subscription*</span></span> | <span data-ttu-id="d880d-121">MySQLaaS (從下拉式清單選取)</span><span class="sxs-lookup"><span data-stu-id="d880d-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="d880d-122">*資源群組*</span><span class="sxs-lookup"><span data-stu-id="d880d-122">*Resource group*</span></span> | <span data-ttu-id="d880d-123">myresource (建立新的資源群組，或使用現有的資源群組)</span><span class="sxs-lookup"><span data-stu-id="d880d-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="d880d-124">伺服器管理員登入</span><span class="sxs-lookup"><span data-stu-id="d880d-124">*Server admin login*</span></span> | <span data-ttu-id="d880d-125">myadmin (設定管理帳戶名稱)</span><span class="sxs-lookup"><span data-stu-id="d880d-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="d880d-126">*密碼*</span><span class="sxs-lookup"><span data-stu-id="d880d-126">*Password*</span></span> | <span data-ttu-id="d880d-127">設定管理帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="d880d-127">setup admin account password</span></span> |
| <span data-ttu-id="d880d-128">*確認密碼*</span><span class="sxs-lookup"><span data-stu-id="d880d-128">*Confirm password*</span></span> | <span data-ttu-id="d880d-129">確認管理帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="d880d-129">confirm admin account password</span></span> |
| <span data-ttu-id="d880d-130">*位置*</span><span class="sxs-lookup"><span data-stu-id="d880d-130">*Location*</span></span> | <span data-ttu-id="d880d-131">北歐 (選取北歐或美國西部)</span><span class="sxs-lookup"><span data-stu-id="d880d-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="d880d-132">*版本*</span><span class="sxs-lookup"><span data-stu-id="d880d-132">*Version*</span></span> | <span data-ttu-id="d880d-133">5.6 (選擇適用於 MySQL 的 Azure 資料庫伺服器版本)</span><span class="sxs-lookup"><span data-stu-id="d880d-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="d880d-134">4- 按一下 [定價層] 指定新資料庫的服務層和效能等級。</span><span class="sxs-lookup"><span data-stu-id="d880d-134">4- Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="d880d-135">在基本層，計算單位可以設定在 50 到 100 之間，而在標準層，則可以設定在 100 到 200 之間，還可根據加入的數量來新增儲存體。</span><span class="sxs-lookup"><span data-stu-id="d880d-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="d880d-136">在本作法指南中，我們選擇 50 計算單位和 50GB。</span><span class="sxs-lookup"><span data-stu-id="d880d-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="d880d-137">按一下 [確定]  以儲存您的選取項目。</span><span class="sxs-lookup"><span data-stu-id="d880d-137">Click **OK** to save your selection.</span></span>
<span data-ttu-id="d880d-138">![建立伺服器定價層](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="d880d-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="d880d-139">5- 按一下 [建立] 佈建伺服器。</span><span class="sxs-lookup"><span data-stu-id="d880d-139">5- Click **Create** to provision the server.</span></span> <span data-ttu-id="d880d-140">佈建需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d880d-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="d880d-141">勾選 [釘選到儀表板] 選項以輕鬆追蹤部署。</span><span class="sxs-lookup"><span data-stu-id="d880d-141">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="d880d-142">雖然基本層支援的儲存體最多為 1000GB，而標準層最多為 10000GB，但在公開預覽中，最大儲存體仍暫時限於 1000GB。</span><span class="sxs-lookup"><span data-stu-id="d880d-142">Although up to 1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, the maximum storage is still limited to 1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="d880d-143">更新適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="d880d-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="d880d-144">佈建新的伺服器之後，使用者有 2 個選項可編輯現有的伺服器︰重設系統管理員密碼，或變更計算單位來相應增加/減少伺服器。</span><span class="sxs-lookup"><span data-stu-id="d880d-144">After new server is provisioned, user has 2 options to edit an existing server: reset administrator password or scale up/down the server by changing the compute-units.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="d880d-145">變更系統管理員使用者密碼</span><span class="sxs-lookup"><span data-stu-id="d880d-145">Change the administrator user password</span></span>
<span data-ttu-id="d880d-146">1- 在伺服器 [概觀] 刀鋒視窗中，按一下 [重設密碼] 填入密碼輸入和確認視窗。</span><span class="sxs-lookup"><span data-stu-id="d880d-146">1- On the server **Overview** blade, click **Reset password** to populate a password input and confirmation window.</span></span>

<span data-ttu-id="d880d-147">2- 在視窗中輸入新密碼並確認密碼，如下所示︰![重設密碼](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="d880d-147">2- Enter new password and confirm the password in the window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="d880d-148">3- 按一下 [確定] 儲存新密碼。</span><span class="sxs-lookup"><span data-stu-id="d880d-148">3- Click **OK** to save the new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="d880d-149">變更計算單位以相應增加/減少</span><span class="sxs-lookup"><span data-stu-id="d880d-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="d880d-150">1- 在 [伺服器] 刀鋒視窗的 [設定] 下，按一下 [定價層]，開啟「適用於 MySQL 的 Azure 資料庫」伺服器的 [定價層] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d880d-150">1- On the server blade, under **Settings**, click **Pricing tier** to open the Pricing tier blade for the Azure Database for MySQL server.</span></span>

<span data-ttu-id="d880d-151">2- 依照**建立適用於 MySQL 的 Azure 資料庫伺服器**中的步驟 4，在相同的定價層變更計算單位。</span><span class="sxs-lookup"><span data-stu-id="d880d-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** to change Compute Units in the same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="d880d-152">刪除適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="d880d-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="d880d-153">1- 在伺服器 [概觀] 刀鋒視窗上，按一下 [刪除] 命令按鈕，開啟 [刪除確認] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d880d-153">1- On the server **Overview** blade, click **Delete** command button to open the Deleting confirmation blade.</span></span>

<span data-ttu-id="d880d-154">2- 在刀鋒視窗的輸入方塊中，輸入正確的伺服器名稱以再次確認。</span><span class="sxs-lookup"><span data-stu-id="d880d-154">2- Type the correct server name in input box of the blade for double confirmation.</span></span>

<span data-ttu-id="d880d-155">3- 再按一次 [刪除] 按鈕，確認刪除動作，並等候通知列上出現「刪除成功」快顯訊息。</span><span class="sxs-lookup"><span data-stu-id="d880d-155">3- Click **Delete** button again to confirm deleting action and wait for “Deleting success” popup on the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="d880d-156">列出「適用於 MySQL 的 Azure 資料庫」資料庫</span><span class="sxs-lookup"><span data-stu-id="d880d-156">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="d880d-157">在伺服器 [概觀] 刀鋒視窗上，向下捲動直到在底部看到資料庫圖格。</span><span class="sxs-lookup"><span data-stu-id="d880d-157">On the server **Overview** blade, scroll down until you see the database tile on the bottom.</span></span> <span data-ttu-id="d880d-158">資料表中會列出所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="d880d-158">All the databases will be listed in the table.</span></span> <span data-ttu-id="d880d-159">按一下 [刪除] 命令按鈕，開啟 [刪除確認] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d880d-159">click **Delete** command button to open the Deleting confirmation blade.</span></span>

![顯示資料庫](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="d880d-161">顯示「適用於 MySQL 的 Azure 資料庫」伺服器的詳細資料</span><span class="sxs-lookup"><span data-stu-id="d880d-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="d880d-162">在伺服器刀鋒視窗的 [設定] 下，按一下 [屬性]，將會開啟 [屬性] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d880d-162">Click **Properties** under **Settings** on the server blade will open the **Properties** blade.</span></span> <span data-ttu-id="d880d-163">然後，您就可以檢視伺服器的所有詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d880d-163">Then you can view all detailed information about the server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d880d-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d880d-164">Next steps</span></span>

[<span data-ttu-id="d880d-165">快速入門：使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="d880d-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
