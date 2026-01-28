# 入门

本文主要关于如何设置你的 Mod 开发环境, 以及如何运行与测试你的 Mod.

## 前置条件

- 熟悉 Java 编程语言, 以及面向对象, 多态, 泛型, and functional features.
- 安装 Java 21 开发套件 (JDK) 和 64-bit Java 虚拟机 (JVM). NeoForge 推荐且官方支持 [Microsoft builds of OpenJDK][jdk], 但是任何其他 JDK 也能够正常工作.

:::caution
确保你正在使用 64 位的 JVM. 一种检查方式是在终端中输入 `java -version`. Minecraft 不支持 32 位的 JVM.
:::

- 熟悉一个集成开发环境 (IDE).
      - NeoForge 官方支持 [IntelliJ IDEA][intellij] 和 [Eclipse][eclipse], 两者都有 Gradle 集成. 不过其他 IDE 也可以使用, 例如 Netbeans, Visual Studio Code, Vim, Emacs 等.
- 熟悉 [Git][git] 和 [GitHub][github]. 这不是技术需要, 但是会让你的生活更美好.

## 设置开发环境

- 前往 [Mod Generator](https://neoforged.net/mod-generator/) 页面, 输入你的 Mod 名字, mod id(可选), Java 包名, Minecraft 版本, 和 Gradle plugin ([ModDevGradle][mdg] 或 [NeoGradle][ng]), 点击 "Download Mod Project", 提取下载好的 ZIP 文件.
- 打开你的 IDE 并导入该 Gradle 项目. Eclipse 和 IntelliJ IDEA 可以自动导入. 如果你的 IDE 不能自动导入, 你可以在终端执行 `gradlew` 命令.
      - 如果是第一次, Gradle 将自动下载 NeoForge 的所有依赖, 包括 Minecraft 本身, 并且会反编译它. 这会花费较多的时间 (可能高达一个小时, 这取决于你的硬件和网络条件).
      - 无论何时你改变 Gradle 文件, Gradle 改变都需要被重新加载, 可以通过 IDE 的 "Reload Gradle" 按钮, 或者再次执行 `gradlew` 命令.

## 自定义 Mod 信息

Mod 的许多基本属性都可以在 `gradle.properties` 文件中修改, 如 Mod 名称, Mod ID 等. 关于更多信息, 看 `gradle.properties` 的注释, 或者看 [the documentation of the `gradle.properties` file][properties].

If you want to modify the build process beyond that, 你可以编辑 `build.gradle` 和 `settings.gradle` 文件. NeoForge 提供的 Gradle 插件, [ModDevGradle][mdg] 或 [NeoGradle][ng], 提供了许多设置选项, a few of which are explained within the buildscript as comments.

:::caution
仅仅在你知道你在做什么的时候编辑 `build.gradle` 和 `settings.gradle`. Mod 的所有基本属性都可以在 `gradle.properties` 设置.
:::

## 构建和测试

要构建你的 Mod, 运行 `gradlew build`. 这会在 `build/libs` 下输出一个名为 `<archivesBaseName>-<version>.jar` 的文件. `<archivesBaseName>` 和 `<version>` 都是 `build.gradle` 中设置的属性, 默认是 `gradle.properties` 中的 `mod_id` 和 `mod_version`; 如果你愿意可以在 `build.gradle` 中修改. 产生的 jar 文件可以放在 `mods` 文件夹中, 或发布到 Mod 平台.

要在测试环境中运行你的 Mod, 可以使用生成的 run configurations 或使用相关的 Tasks (e.g. `gradlew runClient`). 这会从对应的 run 目录启动 Minecraft (e.g. `runs/client` or `runs/server`), along with any source sets specified. The default MDK includes the `main` source set, so any code written in `src/main/java` will be applied.

### 服务器测试

如果你想运行服务器, 通过 Gradle configuration 或者执行 `gradlew runServer`, 但是服务器会马上关闭. 你必须编辑运行目录下的 `eula.txt` 文件来接受 Minecraft EULA.

接受 EULA 后, 服务器在 `localhost` (或 `127.0.0.1`) 下可用. 不过, 你仍然不能加入, 因为服务器默认是在线模式, 要求正版验证 (开发环境下你没有验证). 要解决这个问题，关闭服务器后在 `server.properties` 中修改 `online-mode` 属性为 `false`. 现在, 启动服务器, 你应该可以正常连接.

:::tip
你总是应该在服务器上测试你的 Mod. 这包括 [仅客户端 Mod][client], as these should not do anything when loaded on the server.
:::

[client]: ../concepts/sides.md
[eclipse]: https://www.eclipse.org/downloads/
[git]: https://www.git-scm.com/
[github]: https://github.com/
[intellij]: https://www.jetbrains.com/idea/
[jdk]: https://learn.microsoft.com/en-us/java/openjdk/download#openjdk-21
[mdg]: https://github.com/neoforged/ModDevGradle
[modgen]: https://neoforged.net/mod-generator/
[ng]: https://github.com/neoforged/NeoGradle
[properties]: modfiles.md#gradleproperties
