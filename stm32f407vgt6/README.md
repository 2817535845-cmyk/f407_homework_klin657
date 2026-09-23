# STM32F407VGT6 implementations

该目录保存两个可以独立配置、生成和编译的 STM32CubeMX 工程：

- `polling/`：轮询版本，是原有工程迁移后的内容。
- `interrupt/`：中断版本，目前是轮询版本的副本，供后续修改。

两个工程分别拥有自己的 `board.ioc`、`Core/`、`Drivers/` 和 CMake 配置，修改或重新生成其中一个工程不会覆盖另一个工程。

## Build

轮询版本：

```bash
cd stm32f407vgt6/polling
cmake --preset Debug --fresh
cmake --build --preset Debug
```

中断版本：

```bash
cd stm32f407vgt6/interrupt
cmake --preset Debug --fresh
cmake --build --preset Debug
```

`build/` 是本地构建产物，不应提交到 Git。
