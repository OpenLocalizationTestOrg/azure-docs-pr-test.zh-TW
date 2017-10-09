## <a name="defining-a-backup-policy"></a>定義備份原則
備份原則會定義當拍攝 hello 資料快照集時，與這些快照集的保留時間長度的矩陣。 在定義 VM 的備份原則時，您可以「一天一次」 地觸發備份作業。 當您建立新的原則時，它是套用的 toohello 保存庫。 hello 備份原則介面看起來像這樣：

![備份原則](./media/backup-create-policy-for-vms/backup-policy.png)

toocreate 原則：

1. 輸入的名稱 hello**原則名稱**。
2. 資料快照可依 [每日] 或 [每週] 間隔來擷取。 使用 hello**備份頻率**下拉式功能表 toochoose 是否資料拍攝快照時，每日或每週。
   
   * 如果您選擇每日間隔，用於 hello 快照 hello 反白顯示控制項 tooselect hello hello 一天的時間。 toochange hello 小時的時間，取消選取 hello 小時，然後選取 hello 新小時。
     
     ![每日備份原則](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * 如果您選擇以週為間隔，使用 hello 反白顯示的控制項，請 tooselect hello 天 hello 週和日 tootake hello 快照集的 hello 時間。 在 hello 天功能表中，選取一或多個星期幾。 在 hello 小時功能表上，選取 一小時。 toochange hello 小時的時間，取消選取 hello 選的小時，然後選取 hello 新小時。
     
     ![每週備份原則](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. 根據預設，會選取所有 [保留範圍]  選項。 取消選取任何您不想 toouse 的保留範圍限制。 然後，指定 hello interval(s) toouse。
   
    每月和每年的保留範圍可讓您根據每週或每日增量 toospecify hello 快照集。
   
   > [!NOTE]
   > 在保護 VM 時，備份作業會每天執行一次。 當執行 hello 備份是 hello 相同的每個保留範圍的 hello 時間。
   > 
   > 
4. 設定後 hello 原則的所有選項，請在 hello hello 刀鋒視窗頂端按一下**儲存**。
   
    hello 新原則會立即套用的 toohello 保存庫。

