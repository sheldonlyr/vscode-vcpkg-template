如何在vscode中使用cmake presets和vcpkg

- 添加环境变量 `VCPKG_ROOT`
- 执行 `vcpkg new --application` 来生成vcpkg.json和vcpkg-configuration.json
- 执行 `vcpkg add port [pkg-name]` 来添加依赖
- 执行 `vcpkg x-update-baseline --add-initial-baseline` 来生成和自动填充 `builtin-baseline` 字段
- 执行 `cmake --preset debug` 来配置项目
- 执行 `cmake --build --preset debug` 来生成项目
