> [!IMPORTANT]
> tooreceive 從 Mobile Engagement 的推播通知，您需要 tooenable`Silent Remote Notifications`應用程式中。 您需要 tooadd hello 遠端通知值 toohello UIBackgroundModes 陣列 Info.plist 檔案中。
> 
> 

1. 開啟`info.plist`hello 專案中的檔案
2. 以滑鼠右鍵按一下 hello hello 清單中的最上層項目 (`Information Property List`) 並加入新的資料列
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. 在 hello 輸入新的資料列`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. 按一下 hello 向左箭號 tooexpand hello 資料列
5. 新增下列值 toohello 項目 0 的 hello`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. 一旦您進行變更的 hello，XML 應該包含下列 hello hello info.plist 索引鍵和值：
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. 如果您使用 **Xcode 7 +** 和 **iOS 9 +**：
   
   * 在 [目標] > [目標名稱] > [功能]，啟用 [推播通知]。

