---
title: "aaaCreate 和管理適用於使用 Azure 入口網站的 MySQL 伺服器的 Azure 資料庫 |Microsoft 文件"
description: "本文說明如何快速建立新的 Azure 資料庫的 MySQL server 和管理使用 hello Azure 入口網站的 hello 伺服器。"
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="ff654-103">使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ff654-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="ff654-104">本文說明如何快速建立新的 Azure 資料庫的 MySQL server 和管理使用 hello Azure 入口網站的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff654-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="ff654-105">伺服器管理包括檢視伺服器詳細資料 （& s） 資料庫、 重設密碼和刪除 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff654-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="ff654-106">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ff654-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="ff654-107">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ff654-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="ff654-108">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ff654-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="ff654-109">請遵循這些步驟 toocreate 名為"mysqlserver4demo"MySQL 伺服器的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="ff654-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="ff654-110">1-按一下**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff654-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="ff654-111">2-選取**資料庫**hello 新頁面上，然後選取從**Azure 資料庫的 MySQL**從 hello 資料庫頁面。</span><span class="sxs-lookup"><span data-stu-id="ff654-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="ff654-112">建立的「適用於 MySQL 的 Azure 資料庫」伺服器會有一組已定義的[計算和儲存體](./concepts-compute-unit-and-storage.md)資源。</span><span class="sxs-lookup"><span data-stu-id="ff654-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="ff654-113">hello 資料庫會建立在 Azure 資源群組和 Azure 資料庫的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff654-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![建立新的伺服器](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="ff654-115">3-填寫 hello Azure 資料庫的 MySQL 表單以 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="ff654-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="ff654-116">**表單欄位**</span><span class="sxs-lookup"><span data-stu-id="ff654-116">**Form Field**</span></span> | <span data-ttu-id="ff654-117">**欄位描述**</span><span class="sxs-lookup"><span data-stu-id="ff654-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="ff654-118">*伺服器名稱*</span><span class="sxs-lookup"><span data-stu-id="ff654-118">*Server name*</span></span> | <span data-ttu-id="ff654-119">azure-mysql (伺服器名稱是全域唯一的)</span><span class="sxs-lookup"><span data-stu-id="ff654-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="ff654-120">*訂用帳戶*</span><span class="sxs-lookup"><span data-stu-id="ff654-120">*Subscription*</span></span> | <span data-ttu-id="ff654-121">MySQLaaS (從下拉式清單選取)</span><span class="sxs-lookup"><span data-stu-id="ff654-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="ff654-122">*資源群組*</span><span class="sxs-lookup"><span data-stu-id="ff654-122">*Resource group*</span></span> | <span data-ttu-id="ff654-123">myresource (建立新的資源群組，或使用現有的資源群組)</span><span class="sxs-lookup"><span data-stu-id="ff654-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="ff654-124">伺服器管理員登入</span><span class="sxs-lookup"><span data-stu-id="ff654-124">*Server admin login*</span></span> | <span data-ttu-id="ff654-125">myadmin (設定管理帳戶名稱)</span><span class="sxs-lookup"><span data-stu-id="ff654-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="ff654-126">*密碼*</span><span class="sxs-lookup"><span data-stu-id="ff654-126">*Password*</span></span> | <span data-ttu-id="ff654-127">設定管理帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="ff654-127">setup admin account password</span></span> |
| <span data-ttu-id="ff654-128">*確認密碼*</span><span class="sxs-lookup"><span data-stu-id="ff654-128">*Confirm password*</span></span> | <span data-ttu-id="ff654-129">確認管理帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="ff654-129">confirm admin account password</span></span> |
| <span data-ttu-id="ff654-130">*位置*</span><span class="sxs-lookup"><span data-stu-id="ff654-130">*Location*</span></span> | <span data-ttu-id="ff654-131">北歐 (選取北歐或美國西部)</span><span class="sxs-lookup"><span data-stu-id="ff654-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="ff654-132">*版本*</span><span class="sxs-lookup"><span data-stu-id="ff654-132">*Version*</span></span> | <span data-ttu-id="ff654-133">5.6 (選擇適用於 MySQL 的 Azure 資料庫伺服器版本)</span><span class="sxs-lookup"><span data-stu-id="ff654-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="ff654-134">4 按一下**定價層**toospecify hello 服務層和效能層級為您新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff654-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="ff654-135">在基本層，計算單位可以設定在 50 到 100 之間，而在標準層，則可以設定在 100 到 200 之間，還可根據加入的數量來新增儲存體。</span><span class="sxs-lookup"><span data-stu-id="ff654-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="ff654-136">在本作法指南中，我們選擇 50 計算單位和 50GB。</span><span class="sxs-lookup"><span data-stu-id="ff654-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="ff654-137">按一下**確定**toosave 選取項目。</span><span class="sxs-lookup"><span data-stu-id="ff654-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="ff654-138">![建立伺服器定價層](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="ff654-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="ff654-139">5 按一下**建立**tooprovision hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff654-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="ff654-140">佈建需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ff654-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="ff654-141">檢查 hello **Pin toodashboard**選項 tooallow 輕鬆追蹤您的部署。</span><span class="sxs-lookup"><span data-stu-id="ff654-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="ff654-142">雖然在基本層 too1000GB 和 10000 GB 標準層將會支援存放裝置，對於公開預覽，hello 最大儲存體是暫時仍會限制的 too1000GB。</span><span class="sxs-lookup"><span data-stu-id="ff654-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="ff654-143">更新適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ff654-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="ff654-144">新的伺服器已佈建之後，使用者會有 2 選項 tooedit 現有的伺服器： 重設管理員密碼或小數位數向上/向下 hello 伺服器變更 hello 計算單位。</span><span class="sxs-lookup"><span data-stu-id="ff654-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="ff654-145">變更 hello 系統管理員使用者密碼</span><span class="sxs-lookup"><span data-stu-id="ff654-145">Change hello administrator user password</span></span>
<span data-ttu-id="ff654-146">1-hello 伺服器上**概觀**刀鋒視窗中，按一下 **重設密碼**toopopulate 密碼輸入和確認視窗。</span><span class="sxs-lookup"><span data-stu-id="ff654-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="ff654-147">2-輸入新密碼並確認 hello 密碼在 hello 視窗中，如下所示：![重設密碼](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="ff654-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="ff654-148">3-按一下**確定**toosave hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="ff654-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="ff654-149">變更計算單位以相應增加/減少</span><span class="sxs-lookup"><span data-stu-id="ff654-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="ff654-150">1-在 hello 伺服器刀鋒視窗中，在**設定**，按一下 **定價層**tooopen hello 定價層刀鋒視窗中的 hello Azure 資料庫的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff654-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="ff654-151">2 後續步驟 4 中的**建立 MySQL 伺服器的 Azure 資料庫**toochange 計算單位 hello 相同定價層。</span><span class="sxs-lookup"><span data-stu-id="ff654-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="ff654-152">刪除適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ff654-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="ff654-153">1-hello 伺服器上**概觀**刀鋒視窗中，按一下 **刪除**命令按鈕 tooopen hello 刪除確認刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ff654-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="ff654-154">Double 確認 hello 刀鋒視窗的輸入方塊中的 2 類型 hello 正確的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ff654-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="ff654-155">3-按一下**刪除**按鈕再次 tooconfirm 刪除動作，然後等候 hello 通知列的 「 刪除成功 」 的快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="ff654-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="ff654-156">清單 hello Azure 資料庫的 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="ff654-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="ff654-157">Hello 伺服器上**概觀**刀鋒視窗中，向下捲動直到您看到 hello 資料庫並排顯示 hello 下方。</span><span class="sxs-lookup"><span data-stu-id="ff654-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="ff654-158">所有的 hello 資料庫將列在 hello 資料表中。</span><span class="sxs-lookup"><span data-stu-id="ff654-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="ff654-159">按一下**刪除**命令按鈕 tooopen hello 刪除確認刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ff654-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![顯示資料庫](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="ff654-161">顯示「適用於 MySQL 的 Azure 資料庫」伺服器的詳細資料</span><span class="sxs-lookup"><span data-stu-id="ff654-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="ff654-162">按一下**屬性**下**設定**hello 伺服器刀鋒視窗會開啟 hello**屬性**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ff654-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="ff654-163">然後您可以檢視有關 hello 伺服器的所有詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="ff654-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff654-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff654-164">Next steps</span></span>

[<span data-ttu-id="ff654-165">快速入門：使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ff654-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
