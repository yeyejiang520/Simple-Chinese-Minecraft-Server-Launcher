```markdown
# Minecraft 服务器管理器
一个基于 Python 开发的 Minecraft 服务器一键启停工具，支持自动同意 EULA 协议、GUI/无GUI启动、进程优雅管理，打包为 EXE 后无需安装 Python 环境即可使用。

## 📋 前置条件
1. **Java 环境**：安装与 Minecraft 版本匹配的 Java（推荐 OpenJDK 21，1.18+ 版本需 Java 17+）
   - 验证：打开 CMD 输入 `java -version`，能显示版本号即配置成功
2. **Minecraft 服务端**：下载对应版本的服务端 JAR 文件（如 `minecraft_server.1.20.1.jar`）

## 🚀 快速使用
### 1. 文件准备
将以下文件放在**同一文件夹**中：
```
MC服务器目录/
├─ mc_server_manager.exe  # 本工具主程序
├─ minecraft_server.1.20.1.jar  # Minecraft服务端JAR文件
```

### 2. 首次配置
1. 双击 `mc_server_manager.exe`，程序会自动生成 `server_config.ini` 配置文件并提示退出
2. 用记事本打开 `server_config.ini`，根据实际情况修改配置：
   ```ini
   [SERVER]
   # 服务端JAR文件名（必须和实际文件名一致）
   server_jar_path = ./minecraft_server.1.20.1.jar
   # Java路径（系统已配置环境变量填java即可，否则填完整路径）
   java_path = java
   # 服务器内存分配（根据电脑配置调整，如4G/8G）
   max_memory = 4G
   min_memory = 2G
   # 服务器工作目录（保持./即可，代表当前文件夹）
   server_dir = ./
   # 是否无GUI启动（False=带图形界面，True=纯命令行）
   nogui = False
   ```

### 3. 启动/停止服务器
1. 重新双击 `mc_server_manager.exe`，出现操作菜单：
   ```
   ===== Minecraft 服务器管理器 =====
   1. 启动服务器
   2. 停止服务器
   3. 退出
   ==================================
   ```
2. 输入数字 `1` 启动服务器：
   - 程序会自动检查并同意 EULA 协议，无需手动修改 `eula.txt`
   - 启动后会实时输出服务器日志，GUI 模式会弹出 Minecraft 服务器图形界面
3. 停止服务器：输入数字 `2`，程序会优雅停止服务器（避免存档损坏）
4. 退出：输入数字 `3`，若服务器仍在运行会提示确认

## ⚙️ 常见配置说明
| 配置项         | 说明                                                                 |
|----------------|----------------------------------------------------------------------|
| `server_jar_path` | 服务端JAR文件路径，仅需填文件名（如`minecraft_server.jar`）           |
| `java_path`      | Java可执行文件路径，示例：`C:\Program Files\Java\jdk-21.0.2\bin\java.exe` |
| `max_memory`     | 服务器最大内存，单位支持G/M（如`8G`/`2048M`）                        |
| `nogui`          | `False`=启动图形界面，`True`=纯命令行（服务器性能占用更低）           |

## ❗ 常见问题解决
### 1. 提示“未找到服务器文件”
- 检查 `server_jar_path` 配置是否和实际JAR文件名完全一致（注意大小写/版本号）
- 确保JAR文件和 `mc_server_manager.exe` 在同一文件夹

### 2. 启动服务器无反应/提示“java不是内部命令”
- 检查 Java 环境变量是否配置成功，或在 `java_path` 中填写完整的Java路径
- 确认 Java 版本与 Minecraft 服务端匹配

### 3. GUI界面无法启动
- 将 `nogui` 改为 `False`
- 确保 Windows 图形界面正常，Java 版本支持该服务端的 GUI 功能

### 4. 中文乱码
- 程序已内置编码适配，若仍乱码：打开 CMD 输入 `chcp 65001`，再重新运行 EXE

## 📌 注意事项
1. 请勿用管理员权限运行（可能导致路径/权限异常）
2. 服务器目录建议不要包含中文/特殊字符（如`我的世界服务器/`）
3. 停止服务器优先使用菜单 `2`，避免直接关闭窗口导致存档损坏
4. 首次启动会生成 `world` 等存档文件夹，请勿随意删除

## 🎨 自定义图标（可选）
若需修改EXE图标，可参考以下步骤：
1. 将 PNG 图片转换为 ICO 格式（推荐尺寸：64×64/128×128）
2. 重新打包脚本：`pyinstaller -F -i 自定义图标.ico mc_server_manager.py`

## 📄 免责声明
本工具仅用于个人学习和非商业用途，使用前请确保已阅读并同意 Minecraft EULA 协议（https://account.mojang.com/documents/minecraft_eula）。
```
