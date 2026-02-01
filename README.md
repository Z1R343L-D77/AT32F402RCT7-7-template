# AT32F402RCT7-7 开发模板

AT32F402RCT7-7项目模板 - 为雅特力(ArteryTek)AT32F402RCT7-7微控制器提供的完整开发基础框架。包含系统配置、外设驱动、工程模板和示例代码，帮助开发者快速启动基于Cortex-M4F内核的嵌入式项目。

## 📋 芯片特性

- **内核**: ARM Cortex-M4F with FPU
- **主频**: 最高216MHz
- **Flash**: 256KB
- **SRAM**: 102KB (96KB + 6KB)
- **封装**: LQFP64
- **工作电压**: 2.6V - 3.6V

## 🗂️ 项目结构

```
AT32F402RCT7-7-template/
├── bsp/                          # 板级支持包
│   ├── at32f402_405_board.c     # 板级初始化代码
│   └── at32f402_405_board.h
├── cmsis/                        # CMSIS标准接口
│   ├── at32f402_405.h           # 芯片寄存器定义
│   ├── at32f402_405_conf.h      # 外设配置头文件
│   ├── system_at32f402_405.c    # 系统初始化
│   └── startup_at32f402_405.s   # 启动文件
├── libraries/                    # 标准外设库
│   ├── cmsis/                   # CMSIS库文件
│   │   ├── cm4/core_support/    # Cortex-M4核心支持
│   │   └── dsp/                 # DSP库
│   └── drivers/                 # 外设驱动库
│       ├── inc/                 # 驱动头文件
│       └── src/                 # 驱动源文件
├── user/                         # 用户应用代码
│   ├── inc/                     # 用户头文件
│   │   ├── at32f402_405_clock.h # 时钟配置
│   │   ├── at32f402_405_conf.h  # 外设配置
│   │   └── at32f402_405_int.h   # 中断处理
│   └── src/                     # 用户源文件
│       ├── at32f402_405_clock.c
│       ├── at32f402_405_int.c
│       └── main.c               # 主程序入口
├── mdkv5/                       # Keil编译输出目录
│   ├── Objects/                 # 目标文件
│   └── Listings/                # 列表文件
├── readme/                      # 文档资料
├── at32f402rct7_demo.uvprojx   # Keil MDK项目文件
├── at32f402rct7_demo.uvoptx    # Keil项目配置
└── README.md                    # 本文件
```

## 🚀 快速开始

### 环境要求

- **IDE**: Keil MDK-ARM V5.36 或更高版本
- **编译器**: ARM Compiler 6 (ARMCLANG)
- **Pack**: ArteryTek.AT32F402_405_DFP.2.1.3 或更高版本

### 安装步骤

1. **安装Keil MDK**
   - 从[Keil官网](https://www.keil.com/)下载并安装MDK-ARM

2. **安装芯片支持包**
   - 在Keil Pack Installer中搜索并安装 `ArteryTek.AT32F402_405_DFP`
   - 或从[雅特力官网](https://www.arterytek.com/)下载并手动安装

3. **克隆项目**
   ```bash
   git clone https://github.com/Z1R343L-D77/AT32F402RCT7-7-template.git
   cd AT32F402RCT7-7-template
   ```

4. **打开项目**
   - 双击 `at32f402rct7_demo.uvprojx` 在Keil中打开项目

5. **编译与下载**
   - 点击编译按钮 (F7) 编译项目
   - 连接调试器后点击下载按钮 (F8) 下载到芯片

## 📦 包含的外设驱动

项目包含完整的AT32F402外设驱动库：

- ✅ **ACC** - 自动时钟校准
- ✅ **ADC** - 模数转换器
- ✅ **CAN** - 控制器局域网
- ✅ **CRC** - 循环冗余校验
- ✅ **CRM** - 时钟和复位管理
- ✅ **DMA** - 直接内存访问
- ✅ **ERTC** - 增强型实时时钟
- ✅ **EXINT** - 外部中断
- ✅ **FLASH** - 闪存控制
- ✅ **GPIO** - 通用输入输出
- ✅ **I2C** - I2C通信接口
- ✅ **MISC** - 其他功能
- ✅ **PWC** - 电源控制
- ✅ **SPI** - 串行外设接口
- ✅ **TMR** - 定时器
- ✅ **USART** - 通用同步异步收发器
- ✅ **USB** - USB设备接口
- ✅ **WDT** - 看门狗定时器
- ✅ **WWDT** - 窗口看门狗

## 💡 使用说明

### 修改系统时钟

在 `user/src/at32f402_405_clock.c` 中配置系统时钟：

```c
void system_clock_config(void)
{
    // 配置系统时钟为216MHz
    // 可根据需求修改
}
```

### 添加外设初始化

在 `user/src/main.c` 的 `main()` 函数中添加外设初始化代码：

```c
int main(void)
{
    system_clock_config();

    // 在此处添加外设初始化
    // 例如: GPIO, UART, Timer等

    while(1)
    {
        // 主循环
    }
}
```

### 配置中断

在 `user/src/at32f402_405_int.c` 中添加中断服务函数：

```c
void USART1_IRQHandler(void)
{
    // USART1中断处理代码
}
```

## 🔧 配置说明

### 外设配置

在 `cmsis/at32f402_405_conf.h` 中启用/禁用需要的外设：

```c
#define AT32F402Cx_HD           // 高密度芯片
// #define AT32F402Cx_MD        // 中密度芯片

// 根据需要启用外设
#define AT32_PERIPH_GPIO
#define AT32_PERIPH_USART
// ...
```

### 调试器配置

支持以下调试器：
- CMSIS-DAP
- J-Link
- ST-Link

在Keil的 `Options for Target -> Debug` 中选择对应的调试器。

## 📝 开发建议

1. **代码组织**: 将应用代码放在 `user/` 目录下，保持库文件不被修改
2. **版本控制**: `.gitignore` 已配置忽略编译输出和临时文件
3. **外设使用**: 参考 `libraries/drivers/` 中的驱动代码学习外设使用方法
4. **时钟配置**: 根据实际需求调整系统时钟，注意外设时钟限制
5. **中断优先级**: 合理配置中断优先级，避免冲突

## 📚 参考资料

- [AT32F402/405系列数据手册](https://www.arterytek.com/cn/product/AT32F402.jsp)
- [AT32F402/405参考手册](https://www.arterytek.com/cn/product/AT32F402.jsp)
- [雅特力官方论坛](https://www.arterytek.com/cn/index.jsp)
- [Keil MDK使用指南](https://www.keil.com/support/man/docs/uv4/)

## 🤝 贡献

欢迎提交问题和拉取请求来改进这个模板！

## 📄 许可证

本项目使用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## ⚡ 更新日志

### v1.0.0 (2026-02-01)
- 初始版本发布
- 包含完整的AT32F402外设驱动库
- 添加Keil MDK项目模板
- 配置VS Code开发环境支持

---

**作者**: Z1R343L-D77
**项目主页**: https://github.com/Z1R343L-D77/AT32F402RCT7-7-template
