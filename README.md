# Minecraft Mod Template

從 [SophisticatedTravelersBackpack](https://github.com/vomiter-scp-zh/SophisticatedTravelersBackpack) 抽出的兩分支專案骨架。

| Branch | Minecraft | Loader | Java |
| --- | --- | --- | --- |
| `master` | 1.20.1 | Forge 47.4.22 | 17 |
| `2101` | 1.21.1 | NeoForge 21.1.238 | 21 |

本分支來源：`master`，commit `3833dde504451115e94ce6bc0b96bc7319f0177f`。

## 使用

ZIP 內包含完整 `.git`；解壓縮後直接在此資料夾執行 `git switch master` 或 `git switch 2101`。
預設 checkout 為 `master`。這是新建立的 template Git 歷史，不含原模組歷史，也未設定 remote。
Windows：`gradlew.bat build`；Linux/macOS：`./gradlew build`。

先修改 `gradle.properties` 的 `mod_id`、`mod_name`、`mod_version`、`mod_group_id`、作者與描述。
接著同步修改 `ExampleMod.java` 的 package、MODID、class 名稱與路徑，以及 Mixin JSON 檔名與 package。
Forge 分支的 refmap 名稱、NeoForge metadata 的 `[[mixins]]` config 也必須同步修改。
如改專案資料夾名稱，可一併修改 `settings.gradle` 的 `rootProject.name`。

原專案的自訂 Gradle plugins 保留：Forge 使用 0.1.0，NeoForge 使用 0.2.0。
GitHub Packages 認證仍從 `gpr.user` / `gpr.key` 讀取；請放在使用者的
`~/.gradle/gradle.properties`，不要提交認證資料。

保留 Gradle Wrapper 8.8、mappings、client/server/gameTestServer/data run 設定、
本機 Maven 發布設定、metadata、resource pack 與空 Mixin 設定。
NeoForge 分支不套用 Forge 專用的 MixinGradle 與 ForgeGradle scripts。
背包程式碼、模型、材質、配方，以及 Sophisticated/Traveler/JEI/Jade 專用依賴已移除。
`runData` 沒有註冊任何 data provider；GameTestServer 也沒有測試內容。
metadata 的 MIT License 值沿用來源，可依新專案需求調整。

## 驗證狀態

已檢查兩個分支的 Git 完整性、乾淨工作目錄、metadata/Mixin/pack 格式、
Gradle script 引用、版本與入口 MODID 一致性，以及 ZIP 解壓縮後切換分支。
執行 `./gradlew help --no-daemon` 時，環境無法連線下載 Gradle 8.8
（Network is unreachable），因此未完成 Gradle 設定評估或 Java 編譯驗證。
