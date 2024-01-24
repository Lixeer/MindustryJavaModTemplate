# Mindustry Java 模组模板
这是一个适用于 Android 和 PC 的 Java Mindustry 模组模板。此模组的 Kotlin 版本可以在 [这里](https://github.com/Anuken/MindustryKotlinModTemplate) 查看。

## 用于桌面测试的构建

1. 安装 JDK **17**。
2. 运行 `gradlew jar` [1]。
3. 你的模组的 jar 文件将位于 `build/libs` 目录中。**只在桌面上进行测试时使用此版本。它不适用于 Android。**
要构建兼容 Android 的版本，你需要 Android SDK。你可以让 Github Actions 处理此操作，或自行设置。请参阅下面的步骤。

## 通过 Github Actions 构建

此存储库已配置了 Github Actions CI，以便在每次提交时自动为您构建模组。这需要一个 Github 存储库，理由显而易见。
要获取适用于每个平台的 jar 文件，请执行以下操作：
1. 创建一个带有你的模组名称的 Github 存储库，并将此存储库的内容上传到其中。进行任何必要的修改，然后提交并推送。
2. 在存储库页面上检查 "Actions" 选项卡。选择列表中的最新提交。如果成功完成，"Artifacts" 部分下将有一个下载链接。
3. 点击下载链接（应该是你的存储库的名称）。这将下载一个**压缩的 jar 文件** - **而不是** jar 文件本身 [2]！解压此文件并在 Mindustry 中导入其中的 jar 文件。此版本应在 Android 和桌面上均可运行。

## 本地构建

在本地构建需要更多的设置时间，但如果你以前进行过 Android 开发，这应该不是问题。
1. 下载 Android SDK，解压缩并将 `ANDROID_HOME` 环境变量设置为其位置。
2. 确保已安装 API 级别 30 以及任何最新版本的构建工具（例如 30.0.1）。
3. 将 build-tools 文件夹添加到你的 PATH 中。例如，如果安装了 `30.0.1`，那么路径就是 `$ANDROID_HOME/build-tools/30.0.1`。
4. 运行 `gradlew deploy`。如果一切设置正确，这将在 `build/libs` 目录中创建一个 jar 文件，可在 Android 和桌面上运行。

## 添加依赖项

请注意，对于 Mindustry、Arc 或其子模块的所有依赖项，**必须在 Gradle 中声明为 compileOnly**。永远不要对核心 Mindustry 或 Arc 依赖项使用 `implementation`。

- `implementation` **将整个依赖项放入 jar 文件中**，在大多数模组依赖项中，这是非常不希望的。你不希望将整个 Mindustry API 包含在你的模组中。
- `compileOnly` 意味着该依赖项仅在编译时存在，不包含在 jar 文件中。

只有在希望将另一个 Java 库与你的模组一起打包，并且该库在 Mindustry 中尚不存在时，才使用 `implementation`。