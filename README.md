# CMake 模板
## Using Guide
1. 源文件目录 `src`
    - 引入头文件方式 `#include "xxx/xxx.h"`
    - 注意写 `main.c/.cpp` 之前应该让 `CMake` 生成 `compile_commands.json` 文件（`clangd` 要求，文件默认在 `build` 目录）
2. 头文件目录 `inc`
    - 格式 `foo/foo.h`
    - 与 `lib` 中 `库文件` 名称对应
3. 库文件目录 `lib`
    - 格式 `foo/foo.c`
    - 与 `inc` 中 `头文件` 名称对应
    - 对于某个 `lib` 并不使用 `ALL_INCS` 变量，使用与之对应的头文件接口如 `foo_interface` ，因为 `lib` 和 `inc` 对应，除非包含多个头文件，同样使用手动添加
4. CMake 注意
    - 构建缓存应在 `build` 目录
# Version
## v1
1. 需要手动添加目录和修改对应的 `CMakeLists.txt` 文件
## v2 (Current)
1. 不需要手动更新对应的 `CMakeLists.txt` 文件
2. 只需要正确添加目录和文件即可（方式如上所述）