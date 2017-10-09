因為持續的開發，安裝在 Android Studio 中的 hello Android SDK 版本可能不符合 hello 程式碼中的 hello 版本。 hello 本教學課程中所參考的 Android SDK 位於版本 23，hello 最新寫入 hello 時。 hello 版本號碼可能會增加為新發行的 hello SDK 出現，並建議使用 hello 可用的最新版本。

版本不符合的兩個徵兆為：

- 當您建立或重建 hello 專案時，您可能會收到 Gradle 之類的錯誤訊息 「**失敗 toofind 目標 Google Inc.:Google APIs:n**"。
- 錯誤訊息可能是程式碼中必須根據 `import` 陳述式解析的標準 Android 物件所產生。

如果任一種出現，hello Android SDK 安裝在 Android Studio 中的 hello 版本可能不符合 hello SDK 目標的 hello 下載專案。 tooverify hello 版本中，進行下列變更 hello:

1. 在 Android Studio 中，依序按一下 [工具]  >  [Android]  >  [SDK 管理員]。 如果您尚未安裝 hello hello SDK 平台最新版本，然後按一下 tooinstall 它。 記下 hello 版本號碼。
2. 在 hello**專案總管**索引標籤，在**Gradle 指令碼**，開啟 hello 檔案**build.gradle (modeule： 應用程式)**。 請確定該 hello **compileSdkVersion**和**buildToolsVersion**設定 toohello 安裝最新 SDK 版本。 hello 標記看起來可能像這樣：

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. 在 hello Android Studio 專案總管 中，以滑鼠右鍵按一下 hello 專案節點，選擇 **屬性**，hello 左側資料行中選擇  **Android**。 請確定該 hello**專案建置目標**設定 toohello hello 與相同的 SDK 版本**targetSdkVersion**。

在 Android Studio 中，hello 資訊清單檔案已不再使用的 toospecify hello 目標 SDK 和最低 SDK 版本，不同於使用 Eclipse 的 hello 案例。
