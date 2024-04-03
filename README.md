# CMake 模板
## Using Guide
1. 源文件目录 src
    - 引入头文件方式 `#include "xxx/xxx.h"`
    - 注意写 `main.c` 之前应该让 `CMake` 生成 `compile_commands.json` 文件（`clangd` 要求，文件默认在 `build` 目录）
2. 头文件目录 inc
    - 格式 `xxx/xxx.h`
3. 库文件目录 lib
    - 已包含示例
4. CMake 注意
    - 构建缓存应在 `build` 目录