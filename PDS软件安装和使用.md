### 一、软件下载
1. **注册账户**：访问 [紫光同创官网](https://www.pangomicro.com/index.html) 注册，需使用企业/教育邮箱（如学校邮箱），职位填“学生”，公司填学校名称。
2. **下载安装包**：登录后，在官网“软件下载”页面，选择与电脑系统（仅支持Windows 7/10/11及CentOS - x64）匹配的最新版本（如当前最新版PDS_2022.2 - SP6.7 - ads - win64）。若参赛，可联系赛事官方获取安装包，避免官网注册审核流程。

### 二、软件安装
1. **关闭杀毒软件**：防止拦截组件导致安装失败。
2. **运行安装程序**：双击下载的`Setup.exe`，点击“Next”，阅读并接受许可协议。
3. **选择安装路径**：默认路径为`C:\pango\PDS_2022.1`，建议保持默认；若自定义路径，确保无中文和特殊字符。
4. **完成安装**：点击“Install”开始安装，完成后点击“Finish”。
5. **安装依赖**：
    - 提示安装运行库`vcredist_VS2017.exe`时，点击“是”（若未安装过）。
    - 提示安装`USB Cable Driver`（下载器驱动）和`ParallelPortDriver`（并口驱动）时，均点击“是”，按提示完成安装。

### 三、环境配置
1. **License申请**：
    - 联系微信客服（17665247134，工作日联系）或通过官网“申请License”入口提交。紫光同创根据电脑MAC地址发放NODE - LOCKED类型许可证。
    - 获License文件后，在PDS安装目录（如`C:\pango\PDS_2022.1`）新建“license”文件夹存放。
2. **设置环境变量**：按`Win + R`打开运行窗口，输入`sysdm.cpl`回车，在“系统属性”→“高级”→“环境变量”中，将License文件路径（如`D:\pango\license\pds_node - locked.lic`）添加到系统变量。
3. **安装tap - windows（通用License时）**：用于生成虚拟网卡，安装路径保持默认，完成后在设备管理器中确认“TAP - Windows Adapter V9”正常。

### 四、基本操作
1. **新建工程**：打开PDS，点击“File”→“New Project”，设置工程名称、路径，选择FPGA器件型号（如赛事推荐板卡对应的型号）。
2. **添加文件**：在工程中右键点击“Source”→“Add Source”，添加Verilog/VHDL代码文件。
3. **综合与实现**：点击工具栏“Start Synthesis”进行综合，“Start Implementation”进行布局布线。
4. **生成比特流**：综合实现无误后，点击“Generate Programming File”生成可下载到FPGA的比特流文件。
5. **下载到硬件**：通过JTAG等接口连接开发板，点击“Program Device”选择生成的比特流文件，下载至FPGA验证功能。
6. **仿真调试**：若需仿真，可联合Modelsim等工具（参考《PDS与modelsim联合仿真.pdf》），编译库后运行仿真脚本。
 
