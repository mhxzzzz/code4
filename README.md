# code_4

![MATLAB](https://img.shields.io/badge/MATLAB-2022a-orange)
![Platform](https://img.shields.io/badge/platform-Windows%2010-lightgrey)
![License](https://img.shields.io/badge/license-TBD-yellow)

A computational tool for analyzing non-covalent weak interactions in solid materials based on charge density from first-principles calculations. (Currently a very preliminary test version, with calculation results already compared with literature )

---

## ✨ Supported Methods

- **NCI** (Non-Covalent Interactions Index)
- **DORI** (Density Overlap Regions Indicator)
- **IRI** (Interaction Region Indicator)

---

## 📂 Supported Charge Density Formats

| Format | Source Software | Description |
|:---:|:---|:---|
| CHGCAR | VASP | Directly read VASP output charge density files |
| XSF | Quantum ESPRESSO, ABINIT | Support xsf format output from QE and ABINIT |
| CUBE | Gaussian | Support cube format output from Gaussian |

---

## 📚 Physical Principles and Citation

### Physical Principles
*To be improved*

### Citation
When using corresponding methods for structure analysis, authors are recommended to cite the original literature where the methods were published:

- **NCI**: E. R. Johnson, S. Keinan, P. Mori-Sánchez, J. Contreras-García, A. J. Cohen, W. Yang, *J. Am. Chem. Soc.* 2010, **132**, 6498-6506. DOI: [10.1021/ja100936w](https://doi.org/10.1021/ja100936w)

- **DORI**: P. de Silva, C. Corminboeuf, *J. Chem. Theory Comput.* 2014, **10**, 3745. DOI: [10.1021/ct500490b](https://doi.org/10.1021/ct500490b)

- **IRI**: T. Lu, Q. Chen, *Chemistry-Methods* 2021, **1**, 231. DOI: [10.1002/cmtd.202100007](https://doi.org/10.1002/cmtd.202100007)

---

## 🔧 Installation

### Requirements
The program is developed based on **MATLAB 2022a**. It is distributed as compiled executable files. Users **do not need to install the complete MATLAB environment**, only the free MATLAB Runtime toolkit is required.

### Download Versions
Two versions of executable files are provided:

| Version | Description | Applicable Scenario |
|:---|:---|:---|
| `for_redistribution` | Installer that includes both the exe file and MATLAB Runtime | For computers without MATLAB Runtime configured, internet connection required during installation |
| `for_redistribution_files_only` | Packaged standalone executable file | For computers with MATLAB Runtime already configured |

### Supported Platforms
Currently supports **all platforms that can install the MATLAB Runtime toolkit**. The author has only tested on **Windows 10** so far.

---

## 🚀 Usage Example (Using Windows 10 System)

### Step 1: Prepare Input Files
The following files need to be prepared before running:
- Program `code_4.exe`
- Input file `input` (text format containing calculation parameters)
- Charge density file

### Step 2: Run the Program
Double-click `code_4.exe` to run. The program will display calculation progress in the command window.

### Step 3: View Results
Calculation results are saved in the automatically generated `Results_Output` folder.

---

## ⚙️ Input Parameters Description

### Required Parameters

#### `FilePath`
- **Type**: String
- **Description**: Path to the charge density file, supports absolute or relative paths. The program will automatically identify the format based on the file extension (e.g., CHGCAR, XSF, CUBE).
- **Example**: `FilePath = E:\Matlab\CHGCAR_KDP`

### Optional Parameters

The following parameters are optional settings. The program provides reasonable default values, which users can adjust according to calculation requirements.

#### `CalcType`
- **Type**: String
- **Description**: Type of method to calculate. Multiple methods can be calculated simultaneously, separated by commas or spaces. Supported values include:
  - `RDG` - Reduced Density Gradient function (for NCI analysis)
  - `IRI` - Interaction Region Indicator function
  - `DORI` - Density Overlap Regions Indicator
- **Example**: `CalcType = RDG, IRI, DORI`

#### `AlgoType`
- **Type**: Integer
- **Description**: Choose the core algorithm for gradient calculation.
  - `1` - Direct method: Calculate on the original grid. Fast and maintains original precision.
  - `2` - Interpolation method: Interpolate to uniform grid first, then calculate. Higher precision but slower.
- **Default**: `1`
- **Example**: `AlgoType = 1`

#### `OutputRoot`
- **Type**: String
- **Description**: Root directory path for output results. The program will automatically create subfolders named according to "calculation type_algorithm_file type_material name" in this directory to store all output files.
- **Default**: `Results_Output`
- **Example**: `OutputRoot = Results_Output`

---

## 📊 Output File Description

### Output Folder Naming Convention

All results are saved in automatically generated folders under the root directory specified by `OutputRoot`. The folder naming convention is:
{CalcType}{AlgoStr}{FileType}_{MatName}

Where:
- `CalcType`: Calculation types connected with underscores (e.g., `RDG_IRI`)
- `AlgoStr`: `Direct` or `Interp` (corresponding to AlgoType)
- `FileType`: Input file type (e.g., `VASP`, `XSF`, `CUBE`)
- `MatName`: Material name extracted from the input filename (removing common prefixes such as `CHGCAR_`)

> **Note**: If the folder already exists, suffixes like `_1`, `_2` will be automatically added.

### Typical Output File Structure

Taking calculation of `RDG` with input file `CHGCAR_KDP` as an example:

Results_Output/

└── RDG_Direct_VASP_KDP/

    ├── CHGCAR_KDP_RDG.vasp # RDG data (corresponding to input format)

    ├── CHGCAR_KDP_RDG_sign_lambda2_rho.vasp # sign(λ₂)·ρ field data (for coloring)

    ├── CHGCAR_KDP_RDG_SignRho.txt # Scatter plot x-axis data [sign(λ₂)ρ]

    ├── CHGCAR_KDP_RDG_Value.txt # Scatter plot y-axis data [RDG values]
 
    ├── CHGCAR_KDP_RDG_SignRho_Value.txt # Two-column merged file (x, y)

    └── RDG_Scatter.png # RDG scatter plot


### Output File Details

| File | Description | Purpose |
|:---|:---|:---|
| `*_RDG.vasp` | RDG isosurface data | Visualize RDG isosurfaces (VMD, VESTA, etc.) |
| `*_RDG_sign_lambda2_rho.vasp` | sign(λ₂)·ρ coloring field | Map onto RDG isosurfaces to distinguish interaction types |
| `*_SignRho.txt` | Scatter plot x-axis data | sign(λ₂)ρ values |
| `*_Value.txt` | Scatter plot y-axis data | RDG values |
| `*_SignRho_Value.txt` | Two-column merged data | Can be directly used for third-party plotting software |
| `RDG_Scatter.png` | Generated scatter plot | Quickly view low-gradient peak distribution |


# 中文版本说明书
# code_4

![MATLAB](https://img.shields.io/badge/MATLAB-2022a-orange)
![平台](https://img.shields.io/badge/platform-Windows%2010-lightgrey)
![许可证](https://img.shields.io/badge/license-待定-yellow)

基于第一性原理计算得到的电荷密度分析固体材料中非共价弱相互作用的计算工具。（目前只是一个很初步的测试版本，计算结果和文献及主流软件进行过对比）

---

## ✨ 支持的方法

- **NCI** (Non-Covalent Interactions Index) - 非共价相互作用指数
- **DORI** (Density Overlap Regions Indicator) - 密度重叠区域指标
- **IRI** (Interaction Region Indicator) - 相互作用区域指示器

---

## 📂 支持的电荷密度格式

| 格式 | 来源软件 | 说明 |
| :---: | :---: | :--- |
| CHGCAR | VASP | 直接读取VASP输出的电荷密度文件 |
| XSF | Quantum ESPRESSO, ABINIT | 支持QE和ABINIT输出的xsf格式 |
| CUBE | Gaussian | 支持Gaussian输出的cube格式 |

---

## 📚 物理原理与引用

### 物理原理

待完善

### 引用说明

作者使用相应的方法去分析结构，建议引用发表该方法的文献：

- **NCI**: E. R. Johnson, S. Keinan, P. Mori-Sánchez, J. Contreras-García, A. J. Cohen, W. Yang, *J. Am. Chem. Soc.* 2010, **132**, 6498-6506. DOI: [10.1021/ja100936w](https://doi.org/10.1021/ja100936w)

- **DORI**: P. de Silva, C. Corminboeuf, *J. Chem. Theory Comput.* 2014, **10**, 3745. DOI: [10.1021/ct500490b](https://doi.org/10.1021/ct500490b)

- **IRI**: T. Lu, Q. Chen, *Chemistry-Methods* 2021, **1**, 231. DOI: [10.1002/cmtd.202100007](https://doi.org/10.1002/cmtd.202100007)

---

## 🔧 安装

### 环境要求

程序的开发基于 **MATLAB 2022a**。本程序以编译后的可执行文件形式分发，用户**无需安装MATLAB完整环境**，仅需安装免费的MATLAB Runtime工具包。

### 下载版本

提供两个版本的可执行文件：

| 版本 | 说明 | 适用场景 |
| :--- | :--- | :--- |
| `for_redistribution` | 安装包会一并安装exe文件和MATLAB Runtime | 未配置MATLAB Runtime的电脑，安装过程需要联网 |
| `for_redistribution_files_only` | 打包好的独立可执行文件 | 已安装MATLAB Runtime的电脑 |

### 支持平台

目前支持**所有可以安装MATLAB Runtime工具包的平台**。作者目前仅在**Windows 10**系统上进行过完整测试。

---

## 🚀 使用实例（以Windows 10系统为例）

### 步骤1：安装程序。

### 步骤2：准备输入文件

运行前需要准备以下文件：

- 程序 `code_4.exe`
- 输入文件 `input`（文本格式，包含计算参数）
- 电荷密度文件

（注意input中FilePath = 电荷密度储存的文件夹\CHGCAR_KDP）

### 步骤3：运行程序

双击 `code_4.exe` 运行。

### 步骤4：查看结果

计算结果保存在 `Results_Output` 文件夹中。

---

## ⚙️ 输入参数说明

### 必须设置参数

#### `FilePath`

- **类型**：字符串
- **说明**：电荷密度文件的路径，支持绝对路径或相对路径。程序将根据文件扩展名自动识别格式（CHGCAR、XSF、CUBE）。
- **示例**：`FilePath = E:\Matlab\CHGCAR_KDP`

### 可选参数

以下参数为可选设置，程序已提供合理的默认值，用户可根据计算需求进行调整。

#### `CalcType`

- **类型**：字符串
- **说明**：需要计算的方法类型。可同时计算多个方法，用逗号或空格分隔。支持的值包括：
  - `RDG` - 约化密度梯度函数（用于NCI分析）
  - `IRI` - 相互作用区域指示函数
  - `DORI` - 密度重叠区域指数
- **示例**：`CalcType = RDG, IRI, DORI`

#### `AlgoType`

- **类型**：整数
- **说明**：选择梯度计算的核心算法。
  - `1` - 直接法：在原始网格上直接计算。速度快且保持原始精度。
  - `2` - 插值法：先插值到均匀网格再计算。精度较高但运行速度较慢。
- **默认值**：`1`
- **示例**：`AlgoType = 1`

#### `OutputRoot`

- **类型**：字符串
- **说明**：输出结果的根目录路径。程序将在该目录下自动创建以“计算类型_算法_文件类型_材料名”命名的子文件夹，用于存放所有输出文件。
- **默认值**：`Results_Output`
- **示例**：`OutputRoot = Results_Output`

---

## 📊 输出文件说明

### 输出文件夹命名规则

所有结果保存在由 `OutputRoot` 指定的根目录下的自动生成的文件夹中。文件夹命名规则为：{CalcType}{AlgoStr}{FileType}_{MatName}
其中：

- `CalcType`：用下划线连接的计算类型（如 `RDG_IRI`）
- `AlgoStr`：`Direct` 或 `Interp`（对应AlgoType）
- `FileType`：输入文件类型（如 `VASP`、`XSF`、`CUBE`）
- `MatName`：从输入文件名中提取的材料名（去除常见前缀如 `CHGCAR_`）

> **注**：若文件夹已存在，则自动添加 `_1`、`_2` 等后缀。

### 典型输出文件结构

以计算 `RDG` 且输入文件为 `CHGCAR_KDP` 为例：

Results_Output/

└── RDG_Direct_VASP_KDP/

    ├── CHGCAR_KDP_RDG.vasp # RDG数据（与输入格式对应）

    ├── CHGCAR_KDP_RDG_sign_lambda2_rho.vasp # sign(λ₂)·ρ 场数据（用于着色）

    ├── CHGCAR_KDP_RDG_SignRho.txt # 散点图 x 轴数据 [sign(λ₂)ρ]

    ├── CHGCAR_KDP_RDG_Value.txt # 散点图 y 轴数据 [RDG值]

    ├── CHGCAR_KDP_RDG_SignRho_Value.txt # 两列合并文件（x, y）

    └── RDG_Scatter.png # RDG 散点图

### 输出文件详解

| 文件 | 说明 | 用途 |
| :--- | :--- | :--- |
| `*_RDG.vasp` | RDG等值面数据 | 可视化RDG等值面（VMD、VESTA等） |
| `*_RDG_sign_lambda2_rho.vasp` | sign(λ₂)·ρ着色场 | 映射到RDG等值面上，区分相互作用类型 |
| `*_SignRho.txt` | 散点图x轴数据 | sign(λ₂)ρ值 |
| `*_Value.txt` | 散点图y轴数据 | RDG值 |
| `*_SignRho_Value.txt` | 两列合并数据 | 可直接用于第三方绘图软件 |
| `RDG_Scatter.png` | 生成的散点图 | 快速查看低梯度峰分布 |
