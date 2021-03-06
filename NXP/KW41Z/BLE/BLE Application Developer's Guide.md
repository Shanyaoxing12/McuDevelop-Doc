# **Bluetooth® Low Energy Application Developer’s Guide** <!-- omit in toc -->

- [1. 前言](#1-前言)
- [2. 先决条件](#2-先决条件)
    - [2.1 RTOS任务队列和事件](#21-rtos任务队列和事件)
    - [2.2 GATT数据库](#22-gatt数据库)
    - [2.3 非易失性内存(NVM)访问](#23-非易失性内存nvm访问)
- [3. 主机栈初始化和API](#3-主机栈初始化和api)
    - [3.1 主机任务初始化](#31-主机任务初始化)
    - [3.2 初始化主机的主要函数](#32-初始化主机的主要函数)
    - [3.3 HCI出入点](#33-hci出入点)
    - [3.4 主机栈库和API可用性](#34-主机栈库和api可用性)
    - [3.5 同步和异步函数](#35-同步和异步函数)
    - [3.6 无线发射功率级别](#36-无线发射功率级别)
- [4. 通用访问配置文件(GAP)层](#4-通用访问配置文件gap层)
    - [4.1 中央设置](#41-中央设置)
        - [4.1.1 扫描](#411-扫描)
        - [4.1.2 发起和关闭连接](#412-发起和关闭连接)
        - [4.1.3 配对和绑定](#413-配对和绑定)
    - [4.2 外设](#42-外设)
        - [4.2.1 广告](#421-广告)
        - [4.2.2 配对和绑定](#422-配对和绑定)
    - [4.3 LE数据包长度扩展](#43-le数据包长度扩展)
    - [4.4 增强型隐私特性](#44-增强型隐私特性)
        - [4.4.1 简介](#441-简介)
            - [4.4.1.1 可解析私有地址](#4411-可解析私有地址)
            - [4.4.1.2 非可解析私有地址](#4412-非可解析私有地址)
            - [4.4.1.3 多重身份解析密钥](#4413-多重身份解析密钥)
        - [4.4.2 主机隐私](#442-主机隐私)
        - [4.4.3 控制器隐私](#443-控制器隐私)
            - [4.4.3.1 扫描和启动](#4431-扫描和启动)
            - [4.4.3.2 广告](#4432-广告)
            - [4.4.3.3 连接](#4433-连接)
- [5. 通用属性配置文件(GATT)层](#5-通用属性配置文件gatt层)
    - [5.1 客户端API](#51-客户端api)
        - [5.1.1 安装客户端回调](#511-安装客户端回调)
            - [5.1.1.1 客户端程序回调](#5111-客户端程序回调)
            - [5.1.1.2 通知和指示回调](#5112-通知和指示回调)
        - [5.1.2 MTU交换](#512-mtu交换)
        - [5.1.3 服务和特征发现](#513-服务和特征发现)
            - [5.1.3.1 发现所有主要服务](#5131-发现所有主要服务)
            - [5.1.3.2 发现主要服务(通过UUID)](#5132-发现主要服务通过uuid)
            - [5.1.3.3 发现包含的服务](#5133-发现包含的服务)
            - [5.1.3.4 发现服务的所有特征](#5134-发现服务的所有特征)
            - [5.1.3.5 发现特征(通过UUID)](#5135-发现特征通过uuid)
            - [5.1.3.6 发现特征描述符](#5136-发现特征描述符)
        - [5.1.4 读取和写入特征](#514-读取和写入特征)
            - [5.1.4.1 特征值读取程序](#5141-特征值读取程序)
            - [5.1.4.2 特征读取(通过UUID)程序](#5142-特征读取通过uuid程序)
            - [5.1.4.3 特征读取(多个)程序](#5143-特征读取多个程序)
            - [5.1.4.4 特征写入程序](#5144-特征写入程序)
        - [5.1.5 读取和写入特征描述符](#515-读取和写入特征描述符)
        - [5.1.6 重置程序](#516-重置程序)
    - [5.2 服务器API](#52-服务器api)
        - [5.2.1 服务器回调](#521-服务器回调)
        - [5.2.2 发送通知和指示](#522-发送通知和指示)
        - [5.2.3 属性写入通知](#523-属性写入通知)
- [6. GATT数据库应用程序接口](#6-gatt数据库应用程序接口)
    - [6.1 写入和读取属性](#61-写入和读取属性)
    - [6.2 查找属性句柄](#62-查找属性句柄)
- [7. 创建GATT数据库](#7-创建gatt数据库)
    - [7.1 静态创建GATT数据库](#71-静态创建gatt数据库)
        - [7.1.1 声明自定义128位UUID](#711-声明自定义128位uuid)
        - [7.1.2 声明服务](#712-声明服务)
            - [7.1.2.1 服务声明宏](#7121-服务声明宏)
            - [7.1.2.2 包含声明宏](#7122-包含声明宏)
        - [7.1.3 声明特征](#713-声明特征)
            - [7.1.3.1 特征声明宏](#7131-特征声明宏)
            - [7.1.3.2 声明特征值](#7132-声明特征值)
            - [7.1.3.3 声明特征描述符](#7133-声明特征描述符)
        - [7.1.4 静态GATT数据库定义示例](#714-静态gatt数据库定义示例)
    - [7.2 动态创建GATT数据库](#72-动态创建gatt数据库)
        - [7.2.1 初始化和发布](#721-初始化和发布)
        - [7.2.2 添加服务](#722-添加服务)
        - [7.2.3 添加特征和描述符](#723-添加特征和描述符)
        - [7.2.4 删除服务和特征](#724-删除服务和特征)
- [8. 创建自定义配置文件](#8-创建自定义配置文件)
    - [8.1 定义自定义UUID](#81-定义自定义uuid)
    - [8.2 创建服务功能](#82-创建服务功能)
    - [8.3 GATT客户端交互](#83-gatt客户端交互)
- [9. 应用程序结构](#9-应用程序结构)
    - [9.1 文件夹结构](#91-文件夹结构)
    - [9.2 应用程序主要框架](#92-应用程序主要框架)
        - [9.2.1 主要任务](#921-主要任务)
        - [9.2.2 应用程序消息](#922-应用程序消息)
        - [9.2.3 空闲任务](#923-空闲任务)
    - [9.3 BLE连接管理器](#93-ble连接管理器)
        - [9.3.1 GAP通用事件](#931-gap通用事件)
        - [9.3.2 GAP配置](#932-gap配置)
        - [9.3.3 GAP连接事件](#933-gap连接事件)
    - [9.4 GATT数据库](#94-gatt数据库)
    - [9.5 RTOS特定](#95-rtos特定)
        - [9.5.1 操作系统选择](#951-操作系统选择)
        - [9.5.2 BLE任务配置](#952-ble任务配置)
    - [9.6 板配置](#96-板配置)
    - [9.7 BLE初始化](#97-ble初始化)
    - [9.8 BLE主机栈配置](#98-ble主机栈配置)
    - [9.9 配置文件配置](#99-配置文件配置)
    - [9.10 应用程序代码](#910-应用程序代码)
- [10. 低功耗管理](#10-低功耗管理)
    - [10.1 系统考虑因素](#101-系统考虑因素)
    - [10.2 何时/如何 进入低功耗状态](#102-何时如何-进入低功耗状态)
    - [10.3 深度睡眠模式](#103-深度睡眠模式)
        - [10.3.1 深度睡眠模式1](#1031-深度睡眠模式1)
        - [10.3.2 深度睡眠模式2](#1032-深度睡眠模式2)
        - [10.3.3 深度睡眠模式3](#1033-深度睡眠模式3)
        - [10.3.4 深度睡眠模式4](#1034-深度睡眠模式4)
        - [10.3.5 深度睡眠模式5](#1035-深度睡眠模式5)
        - [10.3.6 深度睡眠模式6](#1036-深度睡眠模式6)
    - [10.4 低功耗使用示例](#104-低功耗使用示例)
        - [10.4.1 BLE栈空闲时使用低功耗](#1041-ble栈空闲时使用低功耗)
        - [10.4.2 广告时使用低功耗](#1042-广告时使用低功耗)
        - [10.4.3 扫描时使用低功耗](#1043-扫描时使用低功耗)
        - [10.4.4 在连接中使用低功耗](#1044-在连接中使用低功耗)


# 1. 前言

本文档介绍了如何在BLE应用程序中集成Bluetooth®LowEnergy（BLE）主机栈，并提供了最常用的API和代码示例的详细说明。

该文档还列出了BLE主机栈的先决条件和初始化，然后按照层和应用程序角色分组表示API，如下所述。

首先，通用访问配置文件（GAP）层根据设备的GAP角色分为两个部分：中央和外设。

通过代码示例解释了这两种设备的基本设置，例如如何准备设备以进行连接、如何将它们连接在一起以及配对和绑定过程。

接下来，通用属性配置文件（GATT）层介绍了两个连接设备之间数据传输所需的API。同样，根据设备的GATT角色，章节分为两个部分：客户端和服务器。

该文档进一步描述了应用程序中GATT数据库API的使用，以操纵GATT服务器数据库中的数据。

然后，文档展示了一种用户友好的静态构建GATT数据库的方法。该方法包括使用一组预定义的宏，应用程序可以使用这些宏在应用程序编译时构建数据库。

下一节包含关于如何构建自定义概要文件的说明。接下来的部分将专门介绍典型应用程序的结构。

此外，本文档还有一章专门介绍低功耗管理以及应用程序如何使用软硬件的低功耗模式。

下一节将介绍主机栈通过专用服务/配置文件提供的空中编程（OTAP）功能以及如何在应用程序中使用它们。本节还详细介绍了OTAP过程和引导装载程序应用程序中涉及的框架组件，引导程序应用程序在设备上进行映像的实际升级。

最后，文档有一个部分，描述了当主机栈在单独的处理器上运行时如何构建BLE应用程序。

------------------------------------------------------------------------------------------------------------------------

# 2. 先决条件

BLE主机栈库包含许多外部引用，应用程序必须定义这些引用以提供主机的全部功能。

如果不这样做，将在尝试构建应用程序二进制文件时导致链接错误。

## 2.1 RTOS任务队列和事件

这些任务队列在 **ble_host_tasks.h** 中声明，如下：

```c
/*! App to Host message queue for the Host Task */
extern msgQueue_t gApp2Host_TaskQueue;
/*! HCI to Host message queue for the Host Task */
extern msgQueue_t gHci2Host_TaskQueue; 
/*! Event for the Host Task Queue */
extern osaEventId_t gHost_TaskEvent;
```

有关主机所需的RTOS任务的详细信息，请参阅[主机任务初始化](#31-主机任务初始化)。

## 2.2 GATT数据库

由于内存效率的原因，主机栈不为GATT数据库分配内存。

相反，应用程序必须根据其需求和约束分配内存、定义和填充数据库。可以静态地、在应用程序编译时或动态地这样做。

无论应用程序如何创建GATT数据库，都必须定义 **gatt_database.h** 中的以下两个外部引用：

```c
/*! The number of attributes in the GATT Database. */
extern uint16_t gGattDbAttributeCount_c;
 
/*! Reference to the GATT database */
extern gattDbAttribute_t gattDatabase[];
```

属性模板（gattDbAttribute_t）定义如下：

```c
typedefstruct gattDbAttribute_tag {
    uint16_t handle ; 
/*!< Attribute handle - cannot be 0x0000; attribute handles need not be consecutive, but must be strictly increasing. */
    uint16_t permissions ; 
/*!< Attribute permissions as defined by ATT. */
    uint32_t uuid ; 
/*!< The UUID should be read according to the gattDbAttribute_t.uuidType member: for 2-byte and 4-byte UUIDs, this contains the value of the UUID; for 16-byte UUIDs, this is a pointer to the allocated 16-byte array containing the UUID. */
    uint8_t * pValue ; 
/*!< Pointer to allocated value array. */
    uint16_t valueLength ; 
/*!< Size of the value array. */
    uint16_t uuidType : 2; 
/*!< Identifies the length of the UUID; the 2-bit values are interpreted according to the bleUuidType_t enumeration. */
    uint16_t maxVariableValueLength : 10; 
/*!< Maximum length of the attribute value array; if this is set to 0, then the attribute's length (valueLength) is fixed and cannot be changed. */
} gattDbAttribute_t ;
```

## 2.3 非易失性内存(NVM)访问

主机栈包含一个内部设备信息管理，它依赖于访问非易失性内存来存储和加载绑定的设备数据。

应用程序开发者通过定义三个函数和一个变量来确定NVM访问机制。函数必须首先对信息进行预处理，然后执行标准的NVM操作（擦除、写入、读取）。声明如下：

```c
extern void App_NvmErase
(
    uint8_t mEntryIdx
);
extern void App_NvmWrite
(
    uint8_t mEntryIdx,
    void*   pBondHeader 
    void*   pBondDataDynamic,
    void*   pBondDataStatic,
    void*   pBondDataDeviceInfo,    
    void*   pBondDataDescriptor,
   uint8_t mDescriptorIndex
);
extern void App_NvmRead
(
    uint8_t mEntryIdx,
    void*   pBondHeader 
    void*   pBondDataDynamic,
    void*   pBondDataStatic,
    void*   pBondDataDeviceInfo,     
    void*   pBondDataDescriptor,
   uint8_t mDescriptorIndex
);
```

设备信息被划分成几个部件，以确保软件磨损均衡机制也能得到最优的使用。部件大小是固定的（在 **ble_constant.h** 中定义），并且具有以下含义：

| API pointer to bond component                                        | Component size (ble_constants.h) | Description                                                                  |
| :------------------------------------------------------------------- | :------------------------------- | :--------------------------------------------------------------------------- |
| pBondHeader: points to a bleBondIdentityHeaderBlob_t element         | gBleBondIdentityHeaderSize_c     | Bonding information which is sufficient to identify a bonded device          |
| pBondDataDynamic: points to a bleBondDataDynamicBlob_t element       | gBleBondDataDynamicSize_c        | Bonding information that might change frequently                             |
| pBondDataStatic: points to a bleBondDataStaticBlob_t element         | gBleBondDataStaticSize_c         | Bonding information that is unlikely to change frequently                    |
| pBondDataDeviceInfo: points to a bleBondDataDeviceInfoBlob_t element | gBleBondDataDeviceInfoSize_c     | Additional bonding information that can be accessed using the host stack API |
| pBondDataDescriptor: points to a bleBondDataDescriptorBlob_t element | gBleBondDataDescriptorSize_c     | Bonding information used to store one CCCD                                   |

应用程序开发者不需要关心绑定信息的格式，因为这是由主机栈处理的。每个绑定数据槽必须包含一个绑定头blob、一个动态数据blob、一个静态数据blob、一个设备信息blob和一个等于 gcGapMaximumSavedCccds_c（ **ble_constant.h** ）的描述符blob数组。一个槽由 mEntryIdx 参数唯一标识。一个描述符由 mEntryIdx - mDescriptorIndex 对唯一标识。

> PS：CCCD - Client Characteristic Configuration Descriptor

如果作为参数传递的一个或多个指针为空，则必须忽略从绑定槽的对应blob的读写操作。擦除函数必须清除条目索引指定的整个绑定数据槽。

上述函数的当前实现使用框架NVM模块或RAM缓冲区。有关NVM配置和功能的其他详细信息可以在 **Connectivity Framework Reference Manual** 中找到。

要启用NVM机制，请确保：
* 将 gAppUseNvm_d（ **app_preinclude.h** ）设置为 1
* 工具链链接器选项中的 gUseNVMLink_d = 1

如果 gAppUseNvm_d 设置为0，则所有绑定数据将存储在RAM中，并且可以访问，直到复位或重新上电。

> NOTE：如果 gAppUseNvm_d 设置为1，则默认的NVM模块配置将应用于 **app_preinclude.h** 文件中。

------------------------------------------------------------------------------------------------------------------------

# 3. 主机栈初始化和API

## 3.1 主机任务初始化

应用程序开发者需要将主机任务配置为主机栈需求的一部分。任务是运行所有主机层的环境（GAP、GATT、ATT、L2CAP、SM、GATTDB）

任务函数的原型在 **ble_host_tasks.h** 文件中：

```c
void Host_TaskHandler(void * args);
```

应该在应用程序的任务代码中以NULL作为参数调用它。

应用程序开发者需要定义任务事件和队列，如[RTOS任务队列和事件](#21-rtos任务队列和事件)中所述。

主机任务的优先级始终高于控制器任务。优先级值通过 gHost_TaskPriority_c（ **ble_host_task_config.h** ）和 gControllerTaskPriority_c（ **ble_controller_task_config.h** ）来配置。注意，改变这些值会对BLE栈产生重大的影响。

优先级别是根据OS抽象（OSA）优先级定义的，其中0是最高优先级，15是最低优先级。有关更多信息，请参阅 **Connectivity Framework Reference Manual**。注意，RTOS特定的优先级可能因操作系统而异。

## 3.2 初始化主机的主要函数

在平台设置完成并启动所有RTOS任务之后，必须初始化主机栈。

需要调用的函数位于 **ble_general.h** 文件中，并具有以下原型：

```c
bleResult_t Ble_HostInitialize
(
    gapGenericCallback_t genericCallback,
    hciHostToControllerInterface_t hostToControllerInterface
);
```

genericCallback 是应用程序已装入的主要回调。它接收来自GAP层的大多数事件，这些事件称为通用事件。通用事件具有一个类型（请参阅 gapGenericEventType_t）和根据事件类型（联合体）的数据。

hostToControllerInterface 是主机栈的HCI出口点。这是主机每次尝试向LE控制器发送HCI消息时调用的函数。

通过 gInitializationComplete_c 通用事件在 genericCallback 中发出主机栈初始化的完成信号。

在接收到该事件之后，可以启动主应用程序逻辑。

![Figure 1. BLE Host Stack overview](../Pic/BLE%20Application%20Developer's%20Guide-Figure1.jpg)

## 3.3 HCI出入点

主机栈的HCI入口点位于 **ble_general.h** 文件中的第二个函数：

```c
void Ble_HciRecv
(
    hciPacketType_t packetType,
    void* pPacket,
    uint16_t packetSize
);
```

这是应用程序必须调用以将HCI消息插入到主机中的函数。

因此，Ble_Initialize 函数中的 Ble_HciRecv 函数和 hostToControllerInterface 参数直接（如果控制器软件和主机运行在同一芯片上）表示需要连接到LE控制器的两个点（参见[初始化主机的主要函数](#32-初始化主机的主要函数)）或通过一个物理接口（例如UART）。

## 3.4 主机栈库和API可用性

本文档中引用的所有API均可在中央和外设库中获得。例如，**ble_host_lib.a** 是一个功能齐全的库，完整地支持GAP级别的中央和外设API，以及GATT级别的客户端和服务器API。

但是，某些应用程序可能针对内存受限的设备，并不需要完整的支持。为了减少代码大小和RAM利用率，还提供了另外两个库：
* **ble_host_peripheral_lib.a**
    * 只支持用于GAP外设和GAP广播者角色的API
    * 只支持用于GATT服务器角色的API
* **ble_host_peripheral_lib.a**
    * 只支持用于GAP中央和GAP观察者角色的API
    * 只支持用于GATT客户端角色的API

若果尝试使用其不支持的API（例如，使用 **ble_host_peripheral_lib.a** 调用 Gap_Connect），API会返回 gBleFeatureNotSupported_c 错误代码。

> NOTE：有关API支持的明确信息，请参阅 **Bluetooth Low Energy Host StackAPI Reference Manual**。每个函数文档都在备注部分包含此信息。

## 3.5 同步和异步函数

绝大多数GAP和GATT的API都是异步执行的。调用这些函数会生成RTOS消息，并且位于主机任务消息队列中。

因此，这些API的实际结果将在由应用程序安装的特定回调触发的事件中发出信号。有关每个API触发的事件的特定信息，请参阅 **Bluetooth Low Energy Host StackAPI Reference Manual**。

但是，有一些API会立即执行（同步）。在 **Bluetooth Low Energy Host StackAPI Reference Manual** 的每个函数文档中明确提到了这一点。

如果没有提到任何内容，则该API是异步的。

## 3.6 无线发射功率级别

控制器接口包含一个API，可用于将无线发射功率设置为不同的级别。

对于广告和连接通道，可以使用以下宏设置不同的功率级别：

```c
#define Controller_SetAdvertisingTxPowerLevel(level) \
Controller_SetTxPowerLevel(level,gAdvTxChannel_c)
```

和

```c
#define Controller_SetConnectionTxPowerLevel(level) \
Controller_SetTxPowerLevel(level,gConnTxChannel_c)
```

数字功率级别均匀分布在最小和最大输出功率值之间（以dBm表示）。更多信息请参考 **silicon datasheet**。

------------------------------------------------------------------------------------------------------------------------

# 4. 通用访问配置文件(GAP)层

GAP层管理连接，安全性和绑定设备。

GAP层API构建在主机控制器接口（HCI）、安全管理器协议（SMP）和设备数据库之上。

GAP定义了BLE设备在BLE系统中可能具有的四种角色（见 4.1.3 节的 Table 1. GAP Security Modes and Levels）：
* 中央
    * 扫描广告者（外设和广播者）
    * 发起与外设的连接；在链路层（LL）级别为Master
    * 通常充当GATT客户端，但其本身也可以包含GATT数据库
* 外设
    * 广告和接受来自中央的连接请求；在链路层（LL）级别为Slave
    * 通常包含GATT数据库并充当GATT服务器，但也可能是客户端
* 观察者
    * 扫描广告者，但不发起连接；传输是可选的
* 广播者
    * 广告，但不接受来自中央的连接请求；接收是可选的

![Figure 2. GAP Topology](../Pic/BLE%20Application%20Developer's%20Guide-Figure2.jpg)

## 4.1 中央设置

通常，中央必须开始扫描以查找外设。当中央扫描了它想要连接的外设时，它会停止扫描并发起与该外设的连接。建立连接后，如果外设需要，它可以进行配对，或者如果两个设备在过去已经绑定，则可以直接加密链路。

### 4.1.1 扫描

中央设备的最基本设置从扫描开始，由 **gap_interface.h** 中的以下函数执行：

```c
bleResult_t Gap_StartScanning
(
    gapScanningParameters_t * pScanningParameters,
    gapScanningCallback_t scanningCallback
);
```

如果 pScanningParameters 指针为NULL，则使用当前设置的参数。如果在设备上电后未设置任何参数，则使用标准默认值：

```c
#define gGapDefaultScanningParameters_d \
{ \
    /* type */              gGapScanTypePassive_c, \
    /* interval */          gGapScanIntervalDefault_d, \
    /* window */            gGapScanWindowDefault_d, \
    /* ownAddressType */    gBleAddrTypePublic_c, \
    /* filterPolicy */      gScanAll_c \
}
```

定义非默认扫描参数的最简单方法是使用上述默认值初始化 gapScanningParameters_t 结构，并只更改所需的字段。

例如，要执行主动扫描并仅扫描白名单中的设备，可以使用以下代码：

```c
gapScanningParameters_t scanningParameters = gGapDefaultScanningParameters_d;
scanningParameters.type = gGapScanTypeActive_c;
scanningParameters.filterPolicy = gScanWhiteListOnly_c;
Gap_StartScanning(&scanningParameters, scanningCallback);
```

scanningCallback 通过GAP层与扫描有关的信号事件触发。

最重要的事件是 gDeviceScanned_c 事件，每次扫描到广告设备时都会触发该事件。此事件的数据包含有关广告者的信息：

```c
typedefstruct gapScannedDevice_tag {
    bleAddressType_t                 addressType;
    bleDeviceAddress_t               aAddress;
    int8_t                           rssi;
    uint8_t                          dataLength;
    uint8_t *                        data;
    bleAdvertisingReportEventType_t  advEventType;
} gapScannedDevice_t;
```

如果此信息表示为中央想要连接的已知外设，则后者必须停止扫描和连接到该外设。

要停止扫描，请调用此函数：

```c
bleResult_t Gap_StopScanning (void);
```

默认情况下，GAP层配置为使用 gDeviceScanned_c 事件类型将所有已扫描到的设备报告给应用程序。但是，某些用例可能需要执行特定的GAP发现程序，其中广告报告必须通过广告数据中的 Flags AD 值进行过滤。其他用例要求主机栈在扫描特定设备时自动发起连接。

要启用基于 Flags AD 值的过滤或设置自动连接的设备地址，必须在扫描开始之前调用以下函数：

```c
bleResult_tGap_SetScanMode
(
    gapScanMode_t scanMode,
    gapAutoConnectParams_t* pAutoConnectParams
);
```

扫描模式的默认值为 gNoDiscovery_c，它会报告所有数据包，而不管其内容如何，​​并且不执行任何自动连接。

要启用有限发现，必须使用 gLimitedDiscovery_c 值，而 gGeneralDiscovery_c 值激活通用发现。

要在扫描特定设备时启用自动连接，必须设置 gAutoConnect_c 值，在这种情况下，pAutoConnectParams 参数必须指向保存目标设备地址的结构以及主机用于这些设备的连接参数。

### 4.1.2 发起和关闭连接

要连接到已扫描的外设，请从 gDeviceScanned_c 事件数据中提取其地址和地址类型，停止扫描并调用以下函数：

```c
bleResult_t Gap_Connect
(
    gapConnectionRequestParameters_t * pParameters,
    gapConnectionCallback_t connCallback
);
```

创建连接参数结构的简单方法是使用默认值初始化它，然后仅更改需要的字段。默认结构定义如下：

```c
#define gGapDefaultConnectionRequestParameters_d \
{ \
    /* scanInterval */          gGapScanIntervalDefault_d, \
    /* scanWindow */            gGapScanWindowDefault_d, \
    /* filterPolicy */          gUseDeviceAddress_c, \
    /* ownAddressType */        gBleAddrTypePublic_c, \
    /* peerAddressType */       gBleAddrTypePublic_c, \
    /* peerAddress */           { 0, 0, 0, 0, 0, 0 }, \
    /* connIntervalMin */       gGapDefaultMinConnectionInterval_d, \
    /* connIntervalMax */       gGapDefaultMaxConnectionInterval_d, \
    /* connLatency */           gGapDefaultConnectionLatency_d, \
    /* supervisionTimeout */    gGapDefaultSupervisionTimeout_d, \
    /* connEventLengthMin */    gGapConnEventLengthMin_d, \
    /* connEventLengthMax */    gGapConnEventLengthMax_d \
}
```

在以下示例中，中央扫描一个具有已知地址的特定心率传感器。当它找到它时，它立即连接到它。

```c
static bleDeviceAddress_t heartRateSensorAddress = { 0xa1, 0xb2, 0xc3, 0xd4, 0xe5, 0xf6 };
static bleAddressType_t hrsAddressType = gBleAddrTypePublic_c;
static bleAddressType_t ownAddressType = gBleAddrTypePublic_c;
voidgapScanningCallback( gapScanningEvent_t * pScanningEvent)
{
    switch (pScanningEvent-> eventType )
    {
        /* ... */
        casegDeviceScanned_c:
        {
            if (hrsAddressType == pScanningEvent -> eventData.scannedDevice.addressType && 
                Ble_DeviceAddressesMatch(heartRateSensorAddress, pScanningEvent-> eventData.scannedDevice.aAddress ))
            {
                gapConnectionRequestParameters_t connReqParams = gGapDefaultConnectionRequestParameters_d; 
                connReqParams.peerAddressType = hrsAddressType;
                Ble_CopyDeviceAddress(connReqParams.peerAddress , heartRateSensorAddress); 
                connReqParams.ownAddressType = ownAddressType;
                bleResult_t result = Gap_StopScanning();
                if (gBleSuccess_c != result)
                {
                    /* Handle error */
                }
                else
                {
                    /* There is no need to wait for the gScanStateChanged_c event because
                     * the commands are queued in the host task
                     * and executed consecutively. */
                    result = Gap_Connect(&connReqParams, connectionCallback);
                    if (gBleSuccess_c != result)
                    {
                        /* Handle error */
                    }
                }
            }
            break;
        }
        /* ... */
    }
}
```

connCallback 由GAP触发，以发送与活动连接相关的所有事件。它有以下原型：

```c
typedef void (* gapConnectionCallback_t )
(
    deviceId_t deviceId,
    gapConnectionEvent_t * pConnectionEvent
);
```

在这个回调中应该监听的第一个事件是 gConnEvtConnected_c 事件。如果应用程序决定在产生此事件之前删除连接建立，它应该调用以下宏：

```c
#define Gap_CancelInitiatingConnection()\
    Gap_Disconnect(gCancelOngoingInitiatingConnection_d)
```

这是非常有用的，例如，当应用程序选择对连接请求使用限时计时器时。

在接收到 gConnEvtConnected_c 事件时，应用程序可以继续从事件数据（pConnectionEvent->event.connectedEvent）中提取必要的参数。要保存的最重要的参数是 deviceId。

deviceId 是一个唯一的8位无符号整数，用于识别后续GAP和GATT的API调用的活动连接。与某个连接相关的所有功能都需要deviceId 参数。例如，要断开连接，请调用此函数：

```c
bleResult_t Gap_Disconnect
(
    deviceId_t deviceId
);
```

### 4.1.3 配对和绑定

用户连接到外设后，使用以下功能检查此设备过去是否已绑定：

```c
bleResult_t Gap_CheckIfBonded
(
    deviceId_t deviceId,
    bool_t * pOutIsBonded
);
```

如果有，可以通过以下方式请求链路加密：

```c
bleResult_t Gap_EncryptLink
(
    deviceId_t deviceId,
);
```

如果链路加密成功，则会触发 gConnEvtEncryptionChanged_c 连接事件。否则，将收到 gConnEvtAuthenticationRejected_c 事件，并将 rejectReason 事件数据参数设置为 gLinkEncryptionFailed_c。

另一方面，如果这是一个新设备（未绑定），可以启动配对，如下所示：

```c
bleResult_t Gap_Pair
(
    deviceId_t deviceId,
    gapPairingParameters_t * pPairingParameters
);
```

配对参数如下所示：

```c
typedef struct gapPairingParameters_tag {
    bool_t                       withBonding;
    gapSecurityModeAndLevel_t    securityModeAndLevel;
    uint8_t                      maxEncryptionKeySize;
    gapIoCapabilities_t          localIoCapabilities;
    bool_t                       oobAvailable;
    gapSmpKeyFlags_t             centralKeys;
    gapSmpKeyFlags_t             peripheralKeys;
    bool_t                       leSecureConnectionSupported;
    bool_t                       useKeypressNotifications;
} gapPairingParameters_t;
```

参数的名称是自解释的。如果中央想要绑定，那么 withBonding 标志应设置为TRUE。

对于安全模式和级别，GAP层将其定义如下：（M代表安全模式，L代表级别）
* M1L1 代表无安全要求
* 除了 M1L1，其他 M1 需要加密，而 M2 需要数据签名
* M1L2 和 M2L1 不需要身份验证（它们允许仅工作配对，没有MITM保护），而 M1L3 和 M2L2 需要身份验证（必须使用PIN或OOB数据配对，以提供MITM保护）
* 从蓝牙规范4.2开始，OOB配对仅在某些条件下提供MITM保护。如果OOB数据交换功能通过专用API提供MITM保护，则应用程序必须通知栈
* M1L4 保留给使用LE安全连接配对方法进行身份验证的配对（带有MITM保护）
* 如果使用LE安全连接配对方法但它不提供MITM保护，则配对将以 M1L2 完成。

> PS：仅工作 - 仅工作（Just Works）方式主要针对没有输入方式的设备。

> PS：MITM - 在密码学和计算机安全领域中，中间人攻击（英语：Man-in-the-middle attack，缩写：MITM）是指攻击者与通讯的两端分别创建独立的联系，并交换其所收到的数据，使通讯的两端认为他们正在通过一个私密的连接与对方直接对话，但事实上整个会话都被攻击者完全控制。在中间人攻击中，攻击者可以拦截通讯双方的通话并插入新的内容。

> PS：OOB数据 - 在计算机网络中，带外数据（out-of-band data）是通过独立于主带内数据流的流传输的数据。带外数据机制提供概念上独立的信道，允许通过该机制发送的任何数据与带内数据分开。应该提供带外数据机制作为数据信道和传输协议的固有特性，而不是要求建立单独的信道和端点。

![Table 1. GAP Security Modes and Levels](../Pic/BLE%20Application%20Developer's%20Guide-Table1.jpg)

centralKeys 应该为应用程序中可用的所有密钥设置标志。如果中央使用私有解析地址，则IRK是强制性的，而如果中央想要使用数据签名，则必须使用CSRK。LTK是由外设提供的，只有当中央打算在未来的重新连接（GAP角色更改）中成为外设时才应包括LTK。

peripheralKeys 应遵循相同的准则。如果要执行加密，LTK是强制性的，而如果外设使用私有解析地址，则应该请求对端的IRK。

有关密钥分发的详细指南，请参阅  4.1.3 节的 Table 2. Key Distribution guidelines。

前三行是配对参数（centralKeys 和 peripheralKeys）和使用 Gap_SendSmpKeys 分发密钥的指南。

如果执行LE安全连接配对（BLE 4.2），则LTK在内部生成，因此设备将忽略配对参数的密钥分发字段中的相应位。

如果IRK也是分发的（其标志已在配对参数中设置），则应分发身份地址。因此，只能通过询问IRK（它在 gapSmpKeyFlags_t 结构中没有单独的标志）来“询问”它，因此是N/A。

分发密钥的协商如下：
* 在SMP配对请求（由 Gap_Pair 启动）中，中央为要分发（centralKeys）和接收（peripheralKeys）的密钥设置标志  
 ![Table 2. Key Distribution guidelines](../Pic/BLE%20Application%20Developer's%20Guide-Table2.jpg)
* 外设检查这两个分发，并且在执行它认为必要的任何更改后必须发送SMP配对响应（由 Gap_AcceptPairingRequest 启动）。外设只允许将一些中央设置为1的标志设置为0，但不允许相反。例如，它不能 请求/分发 中央没有 提供/要求 的密钥。如果外设与中央的分发相反，它可以通过使用 Gap_RejectPairing 函数拒绝配对
* 中央检查配对响应中的更新的分发。如果它与外设所做的更改相反，它可以拒绝配对（Gap_RejectPairing）。否则，配对继续，并且在密钥分发阶段（gConnEvtKeyExchangeRequest_c 事件），只有最终协商的密钥包含在与 Gap_SendSmpKeys 一起发送的密钥结构中
* 对于LE安全连接（两个设备都在配对请求和配对响应数据包的 AuthReq 字段中设置 SC 位），LTK不会被分发，它将被生成，并且配对响应包的 Inittiator Key Distribution 和 Responder Key Distribution 字段中的相应位应设置为0。

如果使用LE安全连接配对（BLE 4.2），并且需要交换OOB数据，则应用程序必须通过调用 Gap_LeScGetLocalOobData 函数从主机栈中获取本地LE SC OOB数据。数据包含在通用的 gLeScLocalOobData_c 事件中。

在以下情况下刷新本地LE SC OOB数据：
* Gap_LeScRegeneratePublicKey 函数被调用（gLeScPublicKeyRegenerated_c 通用事件也作为这个API的结果而产生）
* 设备被重置(这也会导致公钥重新生成)

如果配对继续，可能会发生以下连接事件：
* 请求事件
    * gConnEvtPasskeyRequest_c：配对需要PIN；应用程序必须使用 Gap_EnterPasskey(deviceId, passkey) 进行响应
    * gConnEvtOobRequest_c：如果配对开始时双方都将 oobAvailable 设置为TRUE；应用程序必须使用 Gap_ProvideOob(deviceId, oob) 进行响应
    * gConnEvtKeyExchangeRequest_c：配对已达到密钥交换阶段；应用程序必须使用 Gap_SendSmpKeys(deviceId, smpKeys) 进行响应
    * gConnEvtLeScOobDataRequest_c：栈请求从对端（r，Cr 和 Addr）接收的LE SC OOB数据；应用程序必须使用 Gap_LeScSetPeerOobData(deviceId, leScOobData) 进行响应
    * gConnEvtLeScDisplayNumericValue_c：栈请求显示和确认LE SC数值比较值；应用程序必须使用 Gap_LeScValidateNumericValue(deviceId, ncvValidated) 进行响应
* 信息事件
    * gConnEvtKeysReceived_c：密钥交换阶段完成；密钥自动保存在内部设备数据库中，并提供给应用程序进行即时检查；应用程序不必将密钥保存在NVM存储中，因为如果双方都将 withBonding 设置为TRUE，则会在内部完成
    * gConnEvtAuthenticationRejected_c：对端设备拒绝配对；事件数据的 rejectReason 参数指示外设与配对参数不一致的原因（它不能是 gLinkEncryptionFailed_c，因为该原因是为链路加密失败保留的）
    * gConnEvtPairingComplete_c：配对过程已成功完成，或者在SMP数据包交换期间可能发生错误；请注意，这与 gConnEvtKeyExchangeRequest_c 事件不同；后者表示配对被对端拒绝，而前者则用于因SMP数据包交换而导致的失败
    * gConnEvtLeScKeypressNotification_c：栈通知应用程序在 Passkey Entry Pairing Method 期间已收到远程 SMP Keypress Notification

链路加密或配对成功完成后，中央可以立即开始使用GATT API交换数据。

![Figure 3. Central pairing flow – APIs and eventsGap_RejectPairing may be called on any pairing event](../Pic/BLE%20Application%20Developer's%20Guide-Figure3.jpg)

## 4.2 外设

外设开启广告，等待其他中央的扫描和连接请求。

### 4.2.1 广告

在开始广告之前，应配置广告参数。否则，使用以下默认值：

```c
#define gGapDefaultAdvertisingParameters_d \
{ \
    /* minInterval */            gGapAdvertisingIntervalDefault_c, \
    /* maxInterval */            gGapAdvertisingIntervalDefault_c, \
    /* advertisingType */        gConnectableUndirectedAdv_c, \
    /* addressType */            gBleAddrTypePublic_c, \
    /* directedAddressType */    gBleAddrTypePublic_c, \
    /* directedAddress */        {0, 0, 0, 0, 0, 0}, \
    /* channelMap */             (gapAdvertisingChannelMapFlags_t) (gGapAdvChanMapFlag37_c | gGapAdvChanMapFlag38_c | gGapAdvChanMapFlag39_c), \
    /* filterPolicy */           gProcessAll_c \
}
```

要设置不同的广告参数，应分配 gapAdvertisingParameters_t 结构并使用默认值进行初始化。然后，可以修改必要的字段。

之后，应调用以下函数：

```c
bleResult_t Gap_SetAdvertisingParameters
(
    gapAdvertisingParameters_t * pAdvertisingParameters
);
```

应用程序应该监听 gAdvertisingParametersSetupComplete_c 通用事件。

接下来，应该配置广告数据，并且如果广告类型支持主动扫描，则还应该配置扫描响应数据。如果未配置其中任何一个，则默认为空数据。

用于配置广告 和/或 扫描响应数据的函数如下所示：

```c
bleResult_t Gap_SetAdvertisingData
(
    gapAdvertisingData_t * pAdvertisingData,
    gapScanResponseData_t * pScanResponseData
);
```

这两个指针中的任何一个都可以是NULL，在这种情况下它们将被忽略（相应的数据保留为先前配置的，如果从未设置过，则为空），但不能同时忽略这两个指针。

应用程序应该监听 gAdvertisingDataSetupComplete_c 通用事件。

完成所有必要的设置后，可以使用此函数启动广告：

```c
bleResult_t Gap_StartAdvertising
(
    gapAdvertisingCallback_t advertisingCallback,
    gapConnectionCallback_t connectionCallback
);
```

advertisingCallback 用于接收广告事件（广告状态更改或广告命令失败），而 connectionCallback 仅在广告期间已建立连接时使用。

该连接回调与中央调用 Gap_Connect 函数时使用的回调相同 。

如果中央发起与此外设的连接，则会触发 gConnEvtConnected_c 连接事件。

要在外设尚未收到任何连接请求时停止广告，请使用此函数：

```c
bleResult_t Gap_StopAdvertising (void);
```

在外设进入连接后不应调用此函数。

### 4.2.2 配对和绑定

在与中央建立连接后，外设在安全方面的作用是被动的。中央负责启动配对过程，或者如果设备过去已经绑定，则使用共享LTK加密链路。

如果中央试图在不进行身份验证的情况下访问敏感数据，外设会使用适当的错误代码（身份验证不足，加密不足，授权不足等）发送错误响应（在ATT级别），从而向中央指示它需要执行安全程序。

所有安全检查都由GAP模块内部执行，并自动发送安全错误响应。应用程序开发者需要做的就是注册安全需求。

首先，在构建GATT数据库时（请参阅[创建GATT数据库](#7-创建gatt数据库)），敏感属性应该在其访问权限中内置安全性（例如，只读/带有身份验证读取/带有身份验证写入/具有授权写入，等等）。

其次，如果GATT数据库除了在属性权限中已经指定的安全性之外还需要额外的安全性（例如，某些服务在某些情况下需要更高的安全性），则必须调用以下函数：

```c
bleResult_t Gap_RegisterDeviceSecurityRequirements
(
    gapDeviceSecurityRequirements_t * pSecurity
);
```

该参数是一个指向结构的指针，该结构包含设备主要安全设置和服务特定的安全设置。所有这些安全性要求都是指向 gapSecurityRequirements_t 结构的指针。要忽略的指针应设置为NULL。

虽然外设不会启动任何类型的安全程序，但它可以向中央通报其安全要求。这通常在连接之后立即执行，以避免为请求而交换无用的数据包（因安全性不足可能被拒绝）。

通知在SMP级别通过从设备安全请求包被执行。要使用它，请提供以下GAP API：

```c
bleResult_t Gap_SendSlaveSecurityRequest
(
    deviceId_t deviceId,
    bool_t bondAfterPairing,
    gapSecurityModeAndLevel_t securityModeLevel
);
```

bondAfterPairing 参数向中央指示此外设是否可以绑定，securityModeLevel 通知中央对其进行配对时所需的安全模式和级别。有关安全模式和级别的说明，请参阅第 4.1.3 节，其由GAP模块定义。

此请求不需要中央的答复，也不需要中央立即采取任何行动。中央可以简单地选择忽略从设备安全请求。

如果两个设备已经绑定过，则外设应该期望接收 gConnEvtLongTermKeyRequest_c 连接事件（除非执行LE安全连接配对，如BLE 4.2中所指定的），这意味着中央也识别为绑定，而不是配对，它直接使用先前共享的LTK加密链路。此时，本地LE控制器请求主机提供在配对期间交换的相同的LTK。

当设备先前已配对过时，除了外设的LTK，还会发送EDIV（2字节）和RAND（8字节）值（它们由SMP定义）。因此，在向控制器提供密钥之前，应用程序应检查这两个值是否与 gConnEvtLongTermKeyRequest_c 事件中接收的值匹配。如果他们这样做，应用程序应回复：

```c
bleResult_t Gap_ProvideLongTermKey
(
    deviceId_t deviceId,
    uint8_t * aLtk,
    uint8_t ltkSize
);
```

LTK的大小不能超过最大值：16。

如果EDIV和RAND值不匹配，或者外设无法识别绑定，则可以拒绝加密请求：

```c
bleResult_t Gap_DenyLongTermKey
(
    deviceId_t deviceId
);
```

如果使用LE SC配对，则LTK由主机栈内部生成，并且在绑定后链路加密期间不会从应用程序请求它。在此方案中，仅通过 gConnEvtEncryptionChanged_c 连接事件通知应用程序链路加密 。

如果设备未绑定，则外设应该期望接收 gConnEvtPairingRequest_c，这指示中央已启动了配对。

如果应用程序接受配对参数（请参阅[配对和绑定](#413-配对和绑定)以获取详细说明），它可以回复：

```c
bleResult_t Gap_AcceptPairingRequest
(
    deviceId_t deviceId,
    gapPairingParameters_t * pPairingParameters
);
```

这时，外设发送自己的配对参数，如SMP所定义。

发送此响应后，应用程序应该期望接收与中央相同的配对事件（请参阅[配对和绑定](#413-配对和绑定)），但有一个例外：如果应用程序在连接之前通过调用如下API设置了配对的密钥（PIN），则 gConnEvtPasskeyRequest_c 事件不会被调用：

```c
bleResult_t Gap_SetLocalPasskey
(
    uint32_t passkey
);
```

这样做的原因通常是外设具有一个静态密钥PIN，它仅分发给信任的设备。如果由于任何原因，外设必须动态更改PIN，它可以在配对开始之前调用上述函数（例如，在使用 Gap_AcceptPairingRequest 发送配对响应之前）。

如果外设应用程序从不调用 Gap_SetLocalPasskey，则 gConnEvtPasskeyRequest_c 事件将照常发送到应用程序。

外设可以使用以下API来拒绝配对过程：

```c
bleResult_t Gap_RejectPairing
(
    deviceId_t                       deviceId,
    gapAuthenticationRejectReason_t  reason
);
```

reason 应说明拒绝配对的原因。gLinkEncryptionFailed_c 值保留用于 gConnEvtAuthenticationRejected_c 连接事件，以指示链路加密失败而不是配对失败。因此，它并不能作为配对拒绝的原因。

Gap_RejectPairing 函数不仅可以在接收到配对请求后被调用，还可以在配对过程中被调用（在处理配对事件时或异步，如果因某种原因外设决定中断配对）。这也适用于中央。

![Figure 4. Peripheral pairing flow – APIs and eventsGap_RejectPairing may be called on any pairing event](../Pic/BLE%20Application%20Developer's%20Guide-Figure4.jpg)

对于中央和外设，绑定是在内部执行的，不是应用程序的关注点。应用程序通过 gConnEvtPairingComplete_c 事件参数被告知是否发生了绑定。

## 4.3 LE数据包长度扩展

该新特性将最大数据通道有效负载长度从27个字节扩展到251个字节（8-bit）。

建立连接后，链路层会立即自动完成长度管理。栈传递默认值，用于表示最大传输的有效负载字节数和最大包传输时间，应用程序在编译时在 **ble_globals.c** 中配置该默认值：

```c
#ifndef gBleDefaultTxOctets_c
#define gBleDefaultTxOctets_c 0x00FB
#endif

#ifndef gBleDefaultTxTime_c
#define gBleDefaultTxTime_c 0x0848
#endif
```

设备可以在连接时随时更新数据长度。触发此机制的函数如下：

```c
bleResult_t Gap_UpdateLeDataLength
(
    deviceId_t deviceId,
    uint16_t   txOctets,
    uint16_t   txTime
);
```

在执行该过程之后，将触发 gConnEvtLeDataLengthChanged_c 连接事件，其事件数据中包含最大传输的有效负载字节数和最大包传输时间。如果远程设备启动该过程，则该事件是发送事件。该过程详述如下：

![Figure 5. Data Length Update Procedure](../Pic/BLE%20Application%20Developer's%20Guide-Figure5.jpg)

## 4.4 增强型隐私特性

### 4.4.1 简介

蓝牙4.2主机栈引入了对增强型隐私特性的支持。

可以在主机或控制器中启用隐私：
* 主机隐私内容包括：
    * 定期在主机内重新生成随机地址（可解析或非可解析私有地址）并将其应用到控制器中
    * 保持主机中的对端IRK列表并尝试解决任何传入的RPA
* 控制器隐私（蓝牙4.2引入的），包括在控制器中写入本地IRK，以及所有已知的对端IRK，并让控制器执行硬件、全自动IRK生成和解析

> PS：RPA - 可解析私有地址（Resolvable Private Address）

可以随时启用主机隐私或控制器隐私。当在在另一个隐私正在进行时试图启用一个隐私会生成 gBleInvalidState_c 错误。当尝试两次启用相同的隐私类型时，或者在未启用隐私时尝试禁用隐私，都会会返回相同的错误。

#### 4.4.1.1 可解析私有地址

可解析私有地址（RPA）是一个使用身份解析密钥（IRK）生成的随机地址。该地址对外部观察者来说是完全随机的，因此设备可以周期性地重新生成其RPA以维护隐私，因为使用相同IRK生成的任何两个不同RPA之间没有相关性。

另一方面，IRK也可用于解析RPA，即可以检查是否使用了此IRK生成此RPA。这个过程称为“解析设备的身份”。拥有设备IRK的人总是可以尝试针对RPA解析其身份。

例如，假设设备A经常使用IRKA更改其RPA。在某些时候，A与B绑定。当A具有不同的地址时，A必须给B一种在后续连接中识别它的方法。为实现此目的，A在配对过程的密钥分发阶段分发IRKA。B将从A哪里收到的IRKA存储下来。

之后，B使用RPAX连接到的设备X。此地址看起来完全随机，但B可以尝试使用IRKA解析RPAX。如果解析操作成功，则意味着IRKA用于生成RPAX。由于IRKA属于设备A，这意味着X是A。所以B能够识别设备X的身份，但没有其他人可以做到这一点因为他们没有IRKA。

#### 4.4.1.2 非可解析私有地址

非可解析私有地址（NRPA）是一个完全随机的地址，没有生成模式，因此不能由对端解析。

无法跟踪使用经常更改的NRPA的设备，因为每个新的地址看起来都属于新的设备。

#### 4.4.1.3 多重身份解析密钥

如果一个设备与多个对端绑定，所有对端都使用RPA，则需要存储每个对端的IRK，以便以后能够识别它们（参见之前的章节）。

这意味着每当设备连接到使用未知RPA的对端设备时，它都需要尝试使用每个已存储的IRK来解析RPA。如果IRK的数量很大，那么这会引入大量的计算。

在主机中执行所有这些解析操作可能成本很高。利用硬件加速并启用控制器隐私效率会更高。

### 4.4.2 主机隐私

要启用或禁用主机隐私，可以使用以下API：

```c
bleResult_t Gap_EnableHostPrivacy
(
    bool_t       enable,
    uint8_t *    aIrk
);
```

当 enable 设置为TRUE时，aIrk 参数定义要生成的私有地址类型。如果 aIrk 为NULL，则定期生成新的NRPA并将其写入控制器。否则，IRK将从 aIrk 地址内部复制 ，并且它用于定期生成新的RPA。

私有地址（NRPA或RPA）的生命周期是 gGapHostPrivacyTimeout 外部常量所包含的秒数，该常量在 **ble_config.c** 源文件中定义。默认值为900（15分钟）。

### 4.4.3 控制器隐私

要启用或禁用控制器隐私，可以使用以下API：

```c
bleResult_t Gap_EnableControllerPrivacy
(
    bool_t                       enable,
    uint8_t *                    aOwnIrk,
    uint8_t                      peerIdCount,
    gapIdentityInformation_t*    aPeerIdentities
);
```

当 enable 设置为TRUE时，aOwnIrk 参数不应为NULL，peerIdCount 不应为0或大于 gcGapControllerResolvingListSize_c，且 aPeerIdentities 不应为NULL。

控制器使用 aOwnIrk 定义的IRK定期生成新的RPA。RPA的生命周期是 gGapControllerPrivacyTimeout 外部常量所包含的秒数，该常量在 **ble_config.c** 源文件中定义。默认值为900（15分钟）。

aPeerIdentities 是每个绑定设备的身份信息的数组。身份信息包含设备的身份地址（公共或随机静态地址）和设备的IRK。此数组可以通过 Gap_GetBondedDevicesIdentityInformation 从主机获取 。

启用控制器隐私涉及到控制器的一个快速的命令序列。序列完成后，将触发 gControllerPrivacyStateChanged_c 通用事件。

#### 4.4.3.1 扫描和启动

当中央设备正在扫描时（控制器隐私已启用），控制器会主动尝试解析广告包的广告地址字段中包含的任何PRA。如果找到针对​​对端IRK列表的任何匹配，则已扫描设备结构的 advertisingAddressResolved 参数等于TRUE。

在这种情况下，addressType 和 aAddress 字段不再包含通过OTA看到的实际广告地址，而是包含IRK能够解析广告地址的设备的身份地址。为了连接到该设备，这些字段应用于完成连接请求参数结构的 peerAddressType 和 peerAddress 字段，并且 usePeerIdentityAddress 字段应设置为TRUE。

如果 advertisingAddressResolved 等于FALSE，则广告者使用的是公共或随机静态地址，一个NRPA或一个无法解析的PRA。因此，通过将 usePeerIdentityAddress 设置为FALSE ，启动与此设备的连接，就像未启用控制器隐私一样。

> PS：蓝牙地址分为公共（public）地址和随机（random）地址。其中公共地址是固定的，由厂商设定；随机地址分为静态（static）地址和私有（private）地址，静态地址在蓝牙设备在每次上电后初始化，私有地址分为[可解析私有地址](#4411-可解析私有地址)和[非可解析私有地址](#4412-非可解析私有地址)。

#### 4.4.3.2 广告

当外设启动广告时（控制器隐私已启用），广告参数结构的 ownAddressType 字段未使用。相反，控制器总是生成一个RPA并将其作为广告地址进行广告。

#### 4.4.3.3 连接

当设备连接时（控制器隐私已启用），gConnEvtConnected_c 连接事件参数结构包含的相关字段比没有控制器隐私的要多。

如果对端使用RPA是可以通过使用从列表中IRK进行解析的，那么 peerRpaResolved 字段等于TRUE。在这种情况下， peerAddressType 和 peerAddress 字段包含已解析设备的身份地址，peerRpa 字段包含用于创建连接的实际RPA（中央在启动连接时使用的RPA，或外设广告使用的RPA）。

如果本地控制器已自动生成一个RPA（当连接已创建时），那么 localRpaUsed 字段等于TRUE，并且 localRpa 字段包含实际RPA。

------------------------------------------------------------------------------------------------------------------------

# 5. 通用属性配置文件(GATT)层

GATT层包含用于发现服务和特征以及在设备之间传输数据的API。

GATT层建立在属性协议（ATT）之上，该协议在专用的L2CAP信道（信道ID：0x04）上进行BLE设备间数据传输。

一旦在设备之间建立连接，就可以随时使用GATT API。其无需初始化，因为其会自动创建L2CAP通道。

为了识别GATT对端实例，使用GAP层的相同 deviceId 值（在 gConnEvtConnected_c 连接事件中获得）。

有两个GATT角色定义在通过ATT交换数据的两个设备上：
* GATT服务器 - 包含GATT数据库的设备，GATT数据库是一个暴露有意义数据的服务和特征的集合。通常，服务器会响应客户端发送的请求和命令，但可以将其配置为通过通知和指示自行发送数据。
* GATT客户端 - 通常向服务器发送请求和命令以发现服务器数据库上的服务和特征并交换数据的“活动”设备。

没有固定的规则来决定哪个设备是客户端，哪个设备是服务器。任何设备都可以随时发起请求，从而临时充当客户端，对端设备可以响应该请求，前提是它具有支持充当服务器和具有GATT数据库。

通常，GAP 中央充当GATT客户端，以发现服务和特征，并从GAP外设（通常具有GATT数据库）中获取数据。许多标准BLE配置文件都假设外设具有数据库并且必须充当服务器。但是，这绝不是通用的规则。

## 5.1 客户端API

客户端可以配置ATT MTU，发现服务和特征，并启动数据交换。

所有函数都具有相同的第一个参数：deviceId，用于标识GATT服务器在GATT过程中作为目标的连接设备。这是必要的，因为客户端可能同时连接到多个服务器。

但是，首先，应用程序必须安装必要的回调。

> PS：MTU - 最大传输单元（Maximum Transmission Unit）是指一种通信协议的某一层上面所能通过的最大数据包大小（以字节为单位）

### 5.1.1 安装客户端回调

客户端应用程序必须安装三个回调。

#### 5.1.1.1 客户端程序回调

客户端启动的所有程序都是异步的。他们依靠OTA交换ATT数据包。

要获知程序完成的情况，应用程序必须安装带有以下信号的回调：

```c
typedef void (* gattClientProcedureCallback_t )
(
    deviceId_t               deviceId,
    gattProcedureType_t      procedureType,
    gattProcedureResult_t    procedureResult,
    bleResult_t              error
);
```

要安装此回调，必须调用以下函数：

```c
bleResult_t GattClient_RegisterProcedureCallback
(
    gattClientProcedureCallback_t callback
);
```

procedureType 参数可以用来识别已经开始和已经完成的程序。在给定时刻只能有一个程序处于活动状态。尝试在一个程序正在进行时启动另一个程序会返回错误 gGattAnotherProcedureInProgress_c。

procedureResult 参数指示程序是否成功地完成或者发生了错误。在后一种情况下，error 参数包含错误代码。

```c
void gattClientProcedureCallback
(
    deviceId_t               deviceId,
    gattProcedureType_t      procedureType,
    gattProcedureResult_t    procedureResult,
    bleResult_t              error
)
{
    switch (procedureType)
    {
        /* ... */
    }
}

GattClient_RegisterProcedureCallback(gattClientProcedureCallback);
```

#### 5.1.1.2 通知和指示回调

当客户端从服务器接收到通知时，它会触发一个以下原型的回调：

```c
typedef void (* gattClientNotificationCallback_t )
(
    deviceId_t    deviceId,
    uint16_t      characteristicValueHandle,
    uint8_t *     aValue,
    uint16_t      valueLength
);
```

deviceId 用以识别服务器连接（同时多个连接）。characteristicValueHandle 是GATT数据库中特征值声明的属性手柄。客户端必须先发现它才能识别它。

必须安装回调：

```c
bleResult_t GattClient_RegisterNotificationCallback
(
    gattClientNotificationCallback_t callback
);
```

指示的定义与之相似。

当收到通知或指示时，客户端使用 characteristicValueHandle 来确认那些特征被通知。客户端必须知道可能在任何时候被 通知/指示 的特征值句柄，因为它先前已通过编写CCCD来激活它们（请参阅[读取和写入特征描述符](#515-读取和写入特征描述符)）。

### 5.1.2 MTU交换

通过BLE发送的无线数据包最多包含27个字节的L2CAP层数据。由于L2CAP报头长度为4个字节（包括信道ID），所以在L2CAP层上的所有层（包括ATT和GATT）可能只在无线数据包中发送23个字节的数据（根据低功耗蓝牙4.1规范）。

> NOTE：此数字是固定的，在BLE 4.1中不能增加。

为了维持无线数据包和ATT数据包之间的逻辑映射，标准已将ATT数据包的默认长度（也叫ATT_MTU）设置为23。因此，任何ATT请求都适合单个无线数据包。如果ATT上面的层希望发送超过23个字节的数据，则需要将数据包分割小包并发出多个ATT请求。

然而，ATT协议允许设备增加ATT_MTU（前提是两个设备都支持）。增加ATT_MTU只有一个作用：应用程序不必对长数据进行分段，即它发送的单个事务可以超过23个字节。分片被移到L2CAP层。然而，在空中仍然会发送多个无线包。

如果GATT客户端支持大于默认的MTU，它应该在连接到任何服务器后立即启动MTU交换。在MTU交换期间，两个设备都将其最大MTU发送到另一个，并且选择两者中的最小值为新的MTU。

例如，如果客户端支持的最大ATT_MTU为250，并且服务器支持最大值120，则在交换后，两个设备都将新的ATT_MTU值设置为120。

要启动MTU交换，请从 **gatt_client_interface.h** 调用以下函数 ：

```c
bleResult_t result = GattClient_ExchangeMtu(deviceId);

if (gBleSuccess_c != result)
{
    /* Treat error */
}
```

本地设备支持的最大ATT_MTU的值不必包含在请求中，因为它是静态的。它在 **ble_constants.h** 文件中以名称 gAttMaxMtu_c 定义。在GATT内部实现，ATT交换MTU请求（和服务器的响应）使用该值。

交换完成后，客户端回调通过 gGattProcExchangeMtu_c 程序类型触发。

```c
void gattClientProcedureCallback
(
    deviceId_t deviceId,
    gattProcedureType_t procedureType,
    gattProcedureResult_t procedureResult,
    bleResult_t error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcExchangeMtu_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* To obtain the new MTU */
                uint16_t newMtu;
                bleResult_t result = Gatt_GetMtu(deviceId, &newMtu);
                if (gBleSuccess_c == result)
                {
                    /* Use the value of the new MTU */
                    (void) newMtu;
                }
            }
            else
            {
                /* Handle error */
            }
            break;
        
        /* ... */
    }
}
```

### 5.1.3 服务和特征发现

有多个可用于发现的API，应用程序可以根据需求使用它们。

#### 5.1.3.1 发现所有主要服务

以下API可用于发现服务器数据库中的所有主要服务：

```c
bleResult_t GattClient_DiscoverAllPrimaryServices
(
    deviceId_t        deviceId,
    gattService_t *   aOutPrimaryServices,
    uint8_t           maxServiceCount,
    uint8_t *         pOutDiscoveredCount
);
```

aOutPrimaryServices 参数必须指向一个已分配的服务数组。数组的大小必须等于 maxServiceCount 参数的值，该参数将被传递以确保GATT模块在发现的服务超出预期时不会尝试写入数组的末尾。

pOutDiscoveredCount 参数必须指向一个静态变量，因为GATT模块使用它来写入在程序结束时已发现服务的数量。此数量小于或等于 maxServiceCount。

如果数量相等，则服务数量可能多于 maxServiceCount 个，但由于数组大小限制而无法发现它们。应用程序开发者负责根据服务器数据库的预期内容分配足够大的数字。

在以下示例中，应用程序希望在服务器上找到不超过10个服务。

```c
#define mcMaxPrimaryServices_c 10
static gattService_t primaryServices[mcMaxPrimaryServices_c];
uint8_t mcPrimaryServices;

bleResult_t result = GattClient_DiscoverAllPrimaryServices
(
    deviceId,
    primaryServices,
    mcMaxPrimaryServices_c,
    &mcPrimaryServices
);

if (gBleSuccess_c != result)
{
    /* Treat error */
}
```

完成后，该操作将触发客户端程序回调。应用程序可以读取已发现服务的数量以及每个服务的句柄范围和UUID。

```c
void gattClientProcedureCallback
(
    deviceId_t deviceId,
    gattProcedureType_t procedureType,
    gattProcedureResult_t procedureResult,
    bleResult_t error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcDiscoverAllPrimaryServices_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Read number of discovered services */
                PRINT( mcPrimaryServices );
                /* Read each service's handle range and UUID */
                for (int j = 0; j < mcPrimaryServices; j++)
                {
                    PRINT( primaryServices[j].startHandle );
                    PRINT( primaryServices[j].endHandle );
                    PRINT( primaryServices[j].uuidType );
                    PRINT( primaryServices[j].uuid );
                }
            }
            else
            {
                /* Handle error */
                PRINT( error );
            }
            break;
        /* ... */
    }
}
```

#### 5.1.3.2 发现主要服务(通过UUID)

要仅发现已知类型（服务UUID）的主要服务，可以使用以下API：

```c
bleResult_t GattClient_DiscoverPrimaryServicesByUuid
(
    deviceId_t        deviceId,
    bleUuidType_t     uuidType,
    bleUuid_t *       pUuid,
    gattService_t *   aOutPrimaryServices,
    uint8_t           maxServiceCount,
    uint8_t *         pOutDiscoveredCount
);
```

该程序与[发现所有主要服务](#5131-发现所有主要服务)中描述的程序非常相似。唯一的区别是这次我们根据两个额外参数描述的服务UUID来过滤搜索：pUuid 和 uuidType。

该程序在客户端只对特定类型的服务感兴趣时非常有用。通常，它在已知包含某些服务（某些配置文件特定的）的服务器上执行。因此，大多数情况下，搜索期望找到给定类型的单个服务。结果通常只分配一个结构。

例如，当两个设备实例心率（HR）配置文件时，HR收集器连接到HR传感器，并且可能仅对心率服务（HRS）和其特征感兴趣。以下代码示例演示如何实现此目的。服务和特征UUID的标准值（由Bluetooth SIG定义）位于 **ble_sig_defines.h** 文件中。

```c
static gattService_t heartRateService;
static uint8_t mcHrs;
bleResult_t result = GattClient_DiscoverPrimaryServicesByUuid
(
    deviceId,
    gBleUuidType16_c,            /* Service UUID type */
    gBleSig_HeartRateService_d,  /* Service UUID */
    &heartRateService,           /* Only one HRS is expected to be found */
    1,
    &mcHrs                      /* Will be equal to 1 at the end of the procedure if the HRS is found, 0 otherwise */
);

if (gBleSuccess_c != result)
{
    /* Treat error */
}
```

在客户端程序回调中，应用程序应检查是否找到具有给定UUID的任何服务并读取其句柄范围（也可以在该服务范围内继续进行特征发现）。

```c
void gattClientProcedureCallback
(
    deviceId_t deviceId,
    gattProcedureType_t procedureType,
    gattProcedureResult_t procedureResult,
    bleResult_t error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcDiscoverPrimaryServicesByUuid_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                if (1 == mcHrs)
                {
                    /* HRS found, read the handle range */
                    PRINT( heartRateService.startHandle );
                    PRINT( heartRateService.endHandle );
                }
                else
                {
                    /* HRS not found! */
                }
            }
            else
            {
                /* Handle error */
                PRINT( error );
            }
            break;
        /* ... */
    }
}
```

#### 5.1.3.3 发现包含的服务

[发现所有主要服务](#5131-发现所有主要服务)显示如何发现主要服务。但是，服务器也可能包含次要服务，这些次要服务不应单独使用，通常包含在主服务中。包含意味着所有次要服务的特征都需要主服务的配置文件才可以使用。

因此，在发现主服务后，可以使用以下程序来发现其中包含的服务（通常是次要服务）：

```c
bleResult_t GattClient_FindIncludedServices
(
    deviceId_t         deviceId,
    gattService_t *    pIoService,
    uint8_t            maxServiceCount
);
```

pIoService 指向的服务结构必须具有链接到已分配的服务数组的 aIncludedServices 字段，其大小为 maxServiceCount，根据要找到的包含的服务的预期数量进行选择。这是应用程序的选择，通常遵循配置文件规范。

此外，必须设置服务的范围（startHandle 和 endHandle 字段），这可能已由先前的服务发现程序完成（如[发现所有主要服务](#5131-发现所有主要服务)和[发现主要服务(通过UUID)](#5132-发现主要服务通过uuid)中所述）。

发现包含的服务的数量由GATT模块在 pIoService 结构的 cNumIncludedServices 字段中写入。显然，最多有 maxServiceCount 个包含的服务被发现。

以下示例假定心率服务是使用[发现主要服务(通过UUID)](#5132-发现主要服务通过uuid)中的程序发现的。

```c
/* Finding services included in the Heart Rate Primary Service */
gattService_t * pPrimaryService = &heartRateService;

#define mxMaxIncludedServices_c 3
static gattService_t includedServices[mxMaxIncludedServices_c];

/* Linking the array */
pPrimaryService-> aIncludedServices = includedServices;

bleResult_t result = GattClient_FindIncludedServices
(
    deviceId,
    pPrimaryService,
    mxMaxIncludedServices_c
);

if (gBleSuccess_c != result)
{
    /* Treat error */
}
```

当客户端程序回调被触发时，如果找到任何包含的服务，则应用程序可以读取其句柄范围及其UUID。

```c
void gattClientProcedureCallback
(
    deviceId_t deviceId,
    gattProcedureType_t procedureType,
    gattProcedureResult_t procedureResult,
    bleResult_t error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcFindIncludedServices_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Read included services data */
                PRINT( pPrimaryService-> cNumIncludedServices );
                for (int j = 0; j < pPrimaryService-> cNumIncludedServices ; j++)
                {
                    PRINT( pPrimaryService-> aIncludedServices[j].startHandle );
                    PRINT( pPrimaryService-> aIncludedServices[j].endHandle );
                    PRINT( pPrimaryService-> aIncludedServices[j].uuidType );
                    PRINT( pPrimaryService-> aIncludedServices[j].uuid );
                }
            }
            else
            {
                /* Handle error */
                PRINT( error );
            }
            break;
        /* ... */
    }
}
```

#### 5.1.3.4 发现服务的所有特征

特征发现的主要API有以下原型：

```c
bleResult_tGattClient_DiscoverAllCharacteristicsOfService
(
    deviceId_t         deviceId,
    gattService_t *    pIoService,
    uint8_t            maxCharacteristicCount
);
```

所有必需的信息都包含在 pIoService 指向的服务结构中，最重要的是服务范围（startHandle 和 endHandle），其通常已由服务发现程序填写。如果没有，则需要手动写入。

此外，服务结构的 aCharacteristics 字段必须链接到已分配的特征数组。

以下示例发现[发现主要服务(通过UUID)](#5132-发现主要服务通过uuid)部分中发现的心率服务中包含的所有特征。

```c
gattService_t* pService = &heartRateService

#define mcMaxCharacteristics_c 10
static gattCharacteristic_t hrsCharacteristics[mcMaxCharacteristics_c];

pService->aCharacteristics = hrsCharacteristics;

bleResult_t result = GattClient_DiscoverAllCharacteristicsOfService
(
    deviceId,
    pService,
    mcMaxCharacteristics_c
);
```

当程序完成时，触发客户端程序回调。

```c
void gattClientProcedureCallback
(
    deviceId_t               deviceId,
    gattProcedureType_t      procedureType,
    gattProcedureResult_t    procedureResult,
    bleResult_t              error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcDiscoverAllCharacteristics_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Read number of discovered Characteristics */
                PRINT(pService-> cNumCharacteristics );
                /* Read discovered Characteristics data */
                for ( uint8_t j = 0; j < pService-> cNumCharacteristics ; j++)
                {
                    /* Characteristic UUID is found inside the value field
                     * to avoid duplication */
                    PRINT(pService-> aCharacteristics[j].value.uuidType );
                    PRINT(pService-> aCharacteristics[j].value.uuid );
    
                /* Characteristic Properties indicating the supported operations:
                 * - Read
                 * - Write
                 * - Write Without Response
                 * - Notify
                 * - Indicate
                 */
                PRINT(pService-> aCharacteristics[j].properties );

                /* Characteristic Value Handle - used to identify
                 * the Characteristic in future operations */
                PRINT(pService-> aCharacteristics[j].value.handle );
                }
            }
            else
            {
                /* Handle error */
                PRINT( error );
            }
            break;
        /* ... */
    }
}
```

#### 5.1.3.5 发现特征(通过UUID)

此程序在客户端打算在特定服务中发现特定特征时非常有用。API允许发现同一类型的多个特征，但通常是在预期找到给定类型的单个特征时使用。

继续[发现主要服务(通过UUID)](#5132-发现主要服务通过uuid)的示例，让我们假设客户端想要发现心率服务内的心率控制点特征，如下面的代码所示。

```c
gattService_t * pService = &heartRateService;

static gattCharacteristic_t hrcpCharacteristic;
static uint8_t mcHrcpChar;

bleResult_t result = GattClient_DiscoverCharacteristicOfServiceByUuid
(
    deviceId,
    gBleUuidType16_c,
    gBleSig_HrControlPoint_d,
    pService,
    &hrcpCharacteristic,
    1,
    &mcHrcpChar
);
```

此API可以像前面的示例一样使用，换言之，可以按照服务发现程序使用。但是，用户可能希望在整个数据库上使用UUID执行特征搜索，完全跳过服务发现。为此，必须定义伪服务结构，并且必须将其范围设置为最大值，如以下示例所示：

```c
gattService_t dummyService;
dummyService.startHandle = 0x0001;
dummyService.endHandle = 0xFFFF;
static gattCharacteristic_t hrcpCharacteristic;
static uint8_t mcHrcpChar;

bleResult_t result = GattClient_DiscoverCharacteristicOfServiceByUuid
(
    deviceId,
    gBleUuidType16_c,
    gBleSig_HrControlPoint_d,
    &dummyService,
    &hrcpCharacteristic,
    1,
    &mcHrcpChar
);
```

在任何情况下，都应该在程序回调中检查 mcHrcpChar 变量的值。

```c
void gattClientProcedureCallback
(
    deviceId_t               deviceId,
    gattProcedureType_t      procedureType,
    gattProcedureResult_t    procedureResult,
    bleResult_t              error
)
{
    switch (procedureType)
    {
    /* ... */
    case gGattProcDiscoverCharacteristicByUuid_c:
        if (gGattProcSuccess_c == procedureResult)
        {
            if (1 == mcHrcpChar)
            {
                /* HRCP found, read discovered data */
                PRINT(hrcpCharacteristic.properties );
                PRINT(hrcpCharacteristic.value.handle );
            }
            else
            {
                /* HRCP not found! */
            }
        }
        else
        {
            /* Handle error */
            PRINT(error);
        }
        break;
    /* ... */
    }
}
```

#### 5.1.3.6 发现特征描述符

为了发现一个特征的所有描述符，提供了以下API

```c
bleResult_t GattClient_DiscoverAllCharacteristicDescriptors
(
    deviceId_t                deviceId,
    gattCharacteristic_t *    pIoCharacteristic,
    uint16_t                  endingHandle,
    uint8_t                   maxDescriptorCount
);
```

pIoCharacteristic 指针必须指向与一个具有 value.handle 字段集（通过发现操作或应用程序）的特征结构和 aDescriptors 字段指向一个已分配的描述符结构数组。

endingHandle 应该设置为数据库中下一个特征或服务声明的句柄，以指示何时必须停止对描述符的搜索。GATT客户端模块使用ATT查找信息请求来发现描述符，直到发现一个特征或服务声明，或者到达 endingHandle 为止。因此，通过提供正确的结束句柄，可以优化对描述符的搜索，从而避免了不必要的额外的空中包。

但是，如果应用程序不知道下一个声明所在的位置并且无法提供此优化提示，则 endsHandle 应设置为 0xFFFF。

继续[发现特征(通过UUID)](#5135-发现特征通过uuid)的示例，以下代码假定心率控制点特征具有不超过5个描述符并执行描述符发现。

```c
#define mcMaxDescriptors_c 5
static gattAttribute_t aDescriptors[mcMaxDescriptors_c];
hrcpCharacteristic.aDescriptors = aDescriptors;

bleResult_t result = GattClient_DiscoverAllCharacteristicDescriptors
(
    deviceId,
    &hrcpCharacteristic,
    0xFFFF, /* We don’t know where the next Characterstic/Service begins */
    mcMaxDescriptors_c
);

if (gBleSuccess_c != result)
{
    /* Handle error */
}
```

在该程序结束时，会触发客户端程序回调。

```c
void gattClientProcedureCallback
(
    deviceId_t               deviceId,
    gattProcedureType_t      procedureType,
    gattProcedureResult_t    procedureResult,
    bleResult_t              error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcDiscoverAllCharacteristicDescriptors_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Read number of discovered descriptors */
                PRINT(hrcpCharacteristic.cNumDescriptors );
                /* Read descriptor data */
                for ( uint8_t j = 0; j < hrcpCharacteristic.cNumDescriptors ; j++)
                {
                    PRINT(hrcpCharacteristic.aDescriptors[j].handle );
                    PRINT(hrcpCharacteristic.aDescriptors[j].uuidType );
                    PRINT(hrcpCharacteristic.aDescriptors[j].uuid );
                }
            }
            else
            {
                /* Handle error */
                PRINT(error);
            }
            break;
        /* ... */
    }
}
```

### 5.1.4 读取和写入特征

#### 5.1.4.1 特征值读取程序

读取特征值的主要API如下所示：

```c
bleResult_t GattClient_ReadCharacteristicValue
(
    deviceId_t                deviceId,
    gattCharacteristic_t *    pIoCharacteristic,
    uint16_t                  maxReadBytes
);
```

这个程序假设应用程序知道特征值句柄，通常来自先前的特征发现程序。因此，必须完成 pIoCharacteristic 指向的结构的  value.handle 字段。

此外，应用程序必须分配足够大的字节数组，以便写入接收到的值（来自ATT数据包交换）。maxReadBytes 参数设置为这个已分配数组的大小。

GATT客户端模块通过在需要时发出重复的ATT读取Blob请求来透明地处理长特征，其长度大于单个ATT包的长度。

以下示例假定应用程序知道特征值句柄，并且值长度是可变的，但限制为50个字节。

```c
gattCharacteristic_t myCharacteristic;
myCharacteristic.value.handle = 0x10AB;

#define mcMaxValueLength_c 50
static uint8_t aValue[mcMaxValueLength_c];

myCharacteristic.value.paValue = aValue;

bleResult_t result = GattClient_ReadCharacteristicValue
(
    deviceId,
    &myCharacteristic,
    mcMaxValueLength_c
);

if (gBleSuccess_c != result)
{
    /* Handle error */
}
```

无论值的长度如何，读取完成时都会触发客户端程序回调。接收的值长度也填充在 value 结构中。

```c
void gattClientProcedureCallback
(
    deviceId_t              deviceId,
    gattProcedureType_t     procedureType,
    gattProcedureResult_t   procedureResult,
    bleResult_t             error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcReadCharacteristicValue_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Read value length */
                PRINT(myCharacteristic.value.valueLength );
                /* Read data */
                for ( uint16_t j = 0; j < myCharacteristic.value.valueLength ; j++)
                {
                    PRINT(myCharacteristic.value.paValue[j]);
                }
            }
            else
            {
                /* Handle error */
                PRINT(error);
            }
            break;
        /* ... */
    }
}
```

#### 5.1.4.2 特征读取(通过UUID)程序

此程序的API如下所示：

```c
bleResult_t GattClient_ReadUsingCharacteristicUuid
(
    deviceId_t      deviceId,
    bleUuidType_t   uuidType,
    bleUuid_t *     pUuid,
    uint8_t *       aOutBuffer,
    uint16_t        maxReadBytes,
    uint16_t *      pOutActualReadBytes
);
```

这为重要的优化提供了支持，这涉及在不执行任何服务或特征发现的情况下读取特征值。

例如，以下是编写连接到任何服务器并希望读取设备名称的应用程序的过程。

设备名称包含在GAP服务的设备名称特征中。因此，必要的步骤包括发现所有主要服务，通过其UUID识别GAP服务，发现GAP服务的所有特征并识别设备名称特征（或者，通过GAP服务中的UUID发现特征），最后，使用特征读取程序读取设备名称。

相反，特征读取(通过UUID)程序允许读取一个具有指定UUID的特征，假设服务器上存在一个特征，而不知道特征值句柄。

所描述的示例实现如下：

```c
#define mcMaxValueLength_c 20
static uint8_t aValue[2 + mcMaxValueLength_c]; //First 2 bytes are the handle
static uint16_t deviceNameLength;

bleUuid_t uuid = {
    .uuid16 = gBleSig_GapDeviceName_d
};

bleResult_t result = GattClient_ReadUsingCharacteristicUuid
(
    deviceId,
    gBleUuidType16_c,
    &uuid,
    aValue,
    mcMaxValueLength_c,
    &deviceNameLength
);

if (gBleSuccess_c != result)
{
    /* Handle error */
}
```

读取完成后将触发客户端程序回调。因为在此程序中只交换了一个空中包，因此只能用作长度不大于 ATT_MTU - 1 的特征值的快速读取。

```c
void gattClientProcedureCallback
(
    deviceId_t               deviceId,
    gattProcedureType_t      procedureType,
    gattProcedureResult_t    procedureResult,
    bleResult_t              error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcReadUsingCharacteristicUuid_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Read characteristic value handle */
                PRINT(aValue[0] | (aValue[1] << 8));
                deviceNameLength -= 2;
                
                /* Read value length */
                PRINT(deviceNameLength);
                
                /* Read data */
                for ( uint8_t j = 0; j < deviceNameLength; j++)
                {
                    PRINT(aValue[2 + j]);
                }
            }
            else
            {
                /* Handle error */
                PRINT(error);
            }
            break;
        /* ... */
    }
}
```

#### 5.1.4.3 特征读取(多个)程序

本程序的API如下：

```c
bleResult_t GattClient_ReadMultipleCharacteristicValues
(
    deviceId_t                deviceId,
    uint8_t                   cNumCharacteristics,
    gattCharacteristic_t *    aIoCharacteristics
);
```

此程序还允许针对特定情况进行优化，当多个特征（其值为已知的，固定长度）可以在单个ATT事务（通常是单个空中包）中读取时就会发生优化。

应用程序必须知道每个特征的值句柄和值长度。它还必须分别使用上述值写入到 value.handle 和 value.maxValueLength，然后将 value.paValue 字段与大小为 maxValueLength 的已分配数组相链接。

以下示例涉及在单个数据包中读取三个特征。

```c
#define mcNumCharacteristics_c 3

#define mcChar1Length_c 4
#define mcChar2Length_c 5
#define mcChar3Length_c 6

static uint8_t aValue1[mcChar1Length_c];
static uint8_t aValue2[mcChar2Length_c];
static uint8_t aValue3[mcChar3Length_c];

static gattCharacteristic_t myChars[mcNumCharacteristics_c];

myChars[0].value.handle = 0x0015;
myChars[1].value.handle = 0x0025;
myChars[2].value.handle = 0x0035;

myChars[0].value.maxValueLength = mcChar1Length_c;
myChars[1].value.maxValueLength = mcChar2Length_c;
myChars[2].value.maxValueLength = mcChar3Length_c;

myChars[0].value.paValue = aValue1;
myChars[1].value.paValue = aValue2;
myChars[2].value.paValue = aValue3;

bleResult_t result = GattClient_ReadMultipleCharacteristicValues
(
    deviceId,
    mcNumCharacteristics_c,
    myChars
);

if (gBleSuccess_c != result)
{
    /* Handle error */
}
```

当触发客户端程序回调时，如果没有发生错误，每个特征值的长度应该等于请求的长度。

```c
void gattClientProcedureCallback
(
    deviceId_t              deviceId,
    gattProcedureType_t     procedureType,
    gattProcedureResult_t   procedureResult,
    bleResult_t             error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcReadMultipleCharacteristicValues_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                for ( uint8_t i = 0; i < mcNumCharacteristics_c; i++)
                {
                    /* Read value length */
                    PRINT(myChars[i].value.valueLength );
                    /* Read data */
                    for ( uint8_t j = 0; j < myChars[i].value.valueLength ; j++)
                    {
                        PRINT(myChars[i].value.paValue[j]);
                    }
                }
            }
            else
            {
                /* Handle error */
                PRINT(error);
            }
            break;

        /* ... */
    }
}
```

#### 5.1.4.4 特征写入程序

有一个通用的API可用于写入特征值：

```c
bleResult_t GattClient_WriteCharacteristicValue
(
    deviceId_t                deviceId,
    gattCharacteristic_t *    pCharacteristic,
    uint16_t                  valueLength,
    uint8_t *                 aValue,
    bool_t                    withoutResponse,
    bool_t                    signedWrite,
    bool_t                    doReliableLongCharWrites,
    uint8_t *                 aCsrk
);
```

它有许多参数来支持不同组合的特征写入程序。

pCharacteristic 指向的结构仅用于表示特征值句柄的 value.handle 字段。要写入的值包含在大小为 valueLength 的 aValue 数组中。

如果应用程序希望执行无响应写入程序，则可以将 withoutResponse 参数设置为TRUE，该程序转换为ATT写入命令。如果选择此值，则 signedWrite 参数指示是否应对数据进行签名（通过ATT签名写入命令签名写入程序），在这种情况下，aCsrk 参数不能为NULL并包含用于对数据进行签名的 CSRK。否则，将忽略 signedWrite 和 aCsrk。

最后，如果应用程序正在写一个长特征值（由于ATT_MTU限制而需要多个空气包 ）并且希望服务器确认通过空中发送的属性的每个部分，则应将 doReliableLongCharWrites 设置为TRUE。

为简化应用程序代码，定义了以下宏：

```c
#define GattClient_SimpleCharacteristicWrite(deviceId, pChar, valueLength, aValue) \
        GattClient_WriteCharacteristicValue \
        (deviceId, pChar, valueLength, aValue, FALSE, FALSE, FALSE, NULL)
```

这是写入特征的最简单用法。如果值长度不超过空中数据包的最大值（ATT_MTU - 3），它将发送ATT写请求。否则，它发送带有部分属性的ATT准备写请求，而不检查ATT准备写响应数据的一致性，最后一个ATT会执行写请求。

```c
#define GattClient_CharacteristicWriteWithoutResponse(deviceId, pChar, valueLength, aValue) \
        GattClient_WriteCharacteristicValue \
        (deviceId, pChar, valueLength, aValue, TRUE, FALSE, FALSE, NULL)
```

此用法发送ATT写命令。此处不允许使用长特征值并触发 gBleInvalidParameter_c 错误。

```c
#define GattClient_CharacteristicSignedWrite(deviceId, pChar, valueLength, aValue, aCsrk) \
        GattClient_WriteCharacteristicValue \
        (deviceId, pChar, valueLength, aValue, TRUE, TRUE, FALSE, aCsrk)
```

此用法发送ATT签名写命令。必须提供用于签名数据的CSRK。

这是写一个3字节长特征值的简短示例。

```c
gattCharacteristic_t myChar;
myChar. value . handle = 0x00A0; /* Or maybe it was previously discovered? */

#define mcValueLength_c 3
uint8_t aValue[mcValueLength_c] = { 0x01, 0x02, 0x03 };

bleResult_t result = GattClient_SimpleCharacteristicWrite
(
    deviceId,
    &myChar,
    mcValueLength_c,
    aValue
);

if (gBleSuccess_c != result)
{
    /* Handle error */
}
```

写入完成后会触发客户端程序回调。

```c
void gattClientProcedureCallback
(
    deviceId_t              deviceId,
    gattProcedureType_t     procedureType,
    gattProcedureResult_t   procedureResult,
    bleResult_t             error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcWriteCharacteristicValue_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Continue */
            }
            else
            {
               /* Handle error */
                PRINT(error);
            }  
            break;
        
        /* ... */
    }
}
```

### 5.1.5 读取和写入特征描述符

为这些程序提供了两个API，它们与特征读写非常相似。

唯一的区别是要 读/写 的属性的句柄是通过指向 gattAttribute_t 结构的指针（与 gattCharacteristic_t.value 字段相同的类型）提供的。

```c
bleResult_t GattClient_ReadCharacteristicDescriptor
(
    deviceId_t           deviceId,
    gattAttribute_t *    pIoDescriptor,
    uint16_t             maxReadBytes
);
```

pIoDescriptor->handle 是必须的（它可能是由 gattclient_discoverallcharacterticdescriptors 发现的）。GATT模块填充在字段 pIoDescriptor->aValue（必须链接到一个已分配的数组）和 pIoDescriptor->valueLength（数组的大小）中读取的值。

使用此函数也可以类似地执行写入一个描述符：

```c
bleResult_t GattClient_WriteCharacteristicDescriptor
(
    deviceId_t           deviceId,
    gattAttribute_t *    pDescriptor,
    uint16_t             valueLength,
    uint8_t *            aValue
);
```

在调用函数前，只有 pDescriptor->handle 是必须被填充的。

最常写的描述符之一是客户端特征配置描述符（CCCD）。它具有明确定义的UUID（gBleSig_CCCD_d）和一个2字节长的值，可以写入以 启用/禁用 通知 和/或 指示。

在以下示例中，将发现特征的描述符并编写其CCCD以激活通知。

```c
static gattCharacteristic_t myChar;
myChar. value . handle = 0x00A0; /* Or maybe it was previously discovered? */

#define mcMaxDescriptors_c 5
static gattAttribute_t aDescriptors[mcMaxDescriptors_c];
myChar. aDescriptors = aDescriptors;

/* ... */

{
    bleResult_t result = GattClient_DiscoverAllCharacteristicDescriptors
    (
        deviceId,
        &myChar,
        0xFFFF,
        mcMaxDescriptors_c
    );

    if (gBleSuccess_c != result)
    {
        /* Handle error */
    }
}

/* ... */

void gattClientProcedureCallback
(
    deviceId_t               deviceId,
    gattProcedureType_t      procedureType,
    gattProcedureResult_t    procedureResult,
    bleResult_t              error
)
{
    switch (procedureType)
    {
        /* ... */
        case gGattProcDiscoverAllCharacteristicDescriptors_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Find CCCD */
                for ( uint8_t j = 0; j < myChar. cNumDescriptors ; j++)
                {
                    if (gBleUuidType16_c == myChar.aDescriptors[j].uuidType
                        && gBleSig_CCCD_d == myChar.aDescriptors[j].uuid.uuid16 )
                    {
                        uint8_t cccdValue[2];
                        packTwoByteValue(gCccdNotification_c, cccdValue);
                        bleResult_t result = GattClient_WriteCharacteristicDescriptor
                        (
                            deviceId,
                            &myChar.aDescriptors[j],
                            2,
                            cccdValue
                        );

                        if (gBleSuccess_c != result)
                        {
                            /* Handle error */
                        }
                        break;
                    }
                }
            }
            else
            {
                /* Handle error */
                PRINT(error);
            }
            break;

        case gGattProcWriteCharacteristicDescriptor_c:
            if (gGattProcSuccess_c == procedureResult)
            {
                /* Notification successfully activated */
            }
            else
            {
                /* Handle error */
                PRINT(error);
            }

        /* ... */
    }
}
```

### 5.1.6 重置程序

要取消正在进行的客户端程序，可以调用以下API：

```c
bleResult_t GattClient_ResetProcedure (void);
```

它重置GATT客户端的内部状态，并且可以随时启动新程序。

## 5.2 服务器API

一旦创建了GATT数据库并且已使用 Gap_RegisterDeviceSecurityRequirements 注册了所需的安全设置，所有ATT请求、命令和属性访问安全性检查都由GATT服务器模块内部处理。

除了这种自动功能外，应用程序还可以使用GATT服务器API来发送通知和指示，并且可以选择性地拦截客户端某些尝试写入的属性。

### 5.2.1 服务器回调

第一个GATT服务器调用是服务器回调的安装，它有以下原型

```c
typedef void (* gattServerCallback_t )
(
    deviceId_t              deviceId,     /*!< Device ID identifying the active connection. */
    gattServerEvent_t *     pServerEvent  /*!< Server event. */
);
```

可以使用以下API安装回调：

```c
bleResult_t GattServer_RegisterCallback
(
    gattServerCallback_t callback
);
```

gattServerEvent_t 结构的第一个成员是 eventType，它是一个具有以下可能值的枚举类型：
* gEvtMtuChanged_c：表示客户端启动的MTU交换程序已成功完成且ATT_MTU已增加。事件数据包含ATT_MTU的新值。应用程序流是否可能依赖于ATT_MTU的值，例如，可能存在针对不同ATT_MTU范围的特定优化。如果在此程序中未更改ATT_MTU，则不会触发此事件
* gEvtHandleValueConfirmation_c：在服务器发送指示后，从客户端收到的确认
* gEvtAttributeWritten_c，gEvtAttributeWrittenWithoutResponse_c：请参阅[属性写入通知](#523-属性写入通知)
* gEvtCharacteristicCccdWritten_c：客户端写入了一个CCCD。应用程序应使用 Gap_SaveCccd 保存绑定设备的CCCD值
* gEvtError_c：服务器启动程期间发生错误

### 5.2.2 发送通知和指示

为这些服务器启动操作提供的API非常相似：

```c
bleResult_t GattServer_SendNotification
(
    deviceId_t deviceId,
    uint16_t handle
);
bleResult_t GattServer_SendIndication
(
    deviceId_t deviceId,
    uint16_t q handle
);
```

只需要为这些函数提供属性句柄。属性值会自动从GATT数据库中检索到。

请注意，应用程序开发者的责任是通过写入相应的CCCD值来检查 deviceId 指定的客户端是否先前已激活 通知/指示。为此，应使用以下GAP API：

```c
bleResult_t Gap_CheckNotificationStatus
(
    deviceId_t   deviceId,
    uint16_t     handle,
    bool_t *     pOutIsActive
);
bleResult_t Gap_CheckIndicationStatus
(
    deviceId_t   deviceId,
    uint16_t     handle,
    bool_t *     pOutIsActive
);
```

> NOTE：必须将这两个函数与 Gap_SaveCccd 一起仅用于绑定设备，因为数据保存在NVM中并在重新连接时重新加载。对于不绑定的设备，应用程序也可以使用自己的簿记机制。

发送通知和指示之间有一个重要的区别：后者一次只能发送一个，并且应用程序必须在发送新指示之前等待客户端确认（由 gEvtHandleValueConfirmation_c 服务器事件或由带有 gGattClientConfirmationTimeout_c 错误代码的 gEvtError_c 事件发出的信号）。否则，将触发带有 gGattIndicationAlreadyInProgress_c 错误代码的 gEvtError_c 事件 。通知可以连续发送。

### 5.2.3 属性写入通知

当GATT客户端 从/向 服务器的GATT数据库读取和写入值时，它使用ATT请求。

GATT服务器模块实现管理这些请求，并根据数据库安全设置和客户端的安全状态（已验证身份，已授权等）自动发送ATT响应，而不通知应用程序。

然而，在某些情况下需要通知应用程序ATT数据包交换。例如，许多标准配置文件为某些服务定义了一些所谓的控制点特征。这些特征的价值仅对应用程序具有直接意义。写入这些特征通常会触发特定的动作。

例如，考虑一个虚构的智能灯。它在外设角色中具有BLE连通性，它包含一个具有灯服务（以及其他服务）的小型GATT数据库。灯服务包含两个特征：灯状态特征（LSC）和灯动作特征（LAC）。

LSC是具有读写属性的“普通”特征。它的值为0，灯灭，或1，灯亮。写入该值可将灯设置为所需状态。读取它提供了当前状态，这仅在远程传递信息时有用。

LAC只有一个属性，Write Without Response。用户可以使用不带响应写入程序仅写入值0x01（所有其他值都无效）。每当用户在LAC中写入0x01时，灯将切换其状态。

由于以下原因，LAC是控制点特征的一个很好的例子：
* 写入某个值（在这种情况下为0x01）会触发灯泡上的操作
* 用户写入的值仅具有直接意义（“0x01切换灯”），并且该值以后不会再次使用。因此，它不需要存储在数据库中

显然，无论何时写入控制点特征，都必须通知应用程序以触发某些应用程序特定的动作。

GATT服务器允许应用程序将一个属性句柄集合注册为“write-notifiable”，换句话说，每当对端客户端写入这些属性中的任何一个时，应用程序都希望接收到事件。

GATT数据库中的所有控制点特征都必须注册其值句柄。实际上，应用程序可以使用以下API为其自身目的注册任何其他句柄以进行写入通知：

```c
bleResult_t GattServer_RegisterHandlesForWriteNotifications
(
    uint8_t      handleCount,
    uint16_t *   aAttributeHandles
);
```

handleCount 是 aAttributeHandles 数组的大小并且它不能超过 gcGattMaxHandleCountForWriteNotifications_c。

使用此函数注册属性句柄后，每当客户端尝试写入其值时，将使用以下事件类型之一触发GATT服务器回调：
* gEvtAttributeWritten_c：当使用写入程序（ATT写入请求）写入属性时触发。在这种情况下，应用程序必须确定写入的值是否有效和是否必须在数据库中写入，如果是，应用程序必须使用 GattDb_WriteAttribute 写入值，请参阅第6章。此时，GATT服务器模块不会通过OTA自动发送ATT写响应。相反，它等待应用程序调用此函数：
    ```c
    bleResult_t GattServer_SendAttributeWrittenStatus
    (
        deviceId_t   deviceId,
        uint16_t     attributeHandle,
        uint8_t      status
    );
    ```
    status 参数的值被解释为ATT错误代码。如果值有效且应用程序成功处理，则它必须等于 gAttErrCodeNoError_c（0x00）。否则，它必须等于配置文件特定的错误代码（在区间0xE0-0xFF中）或应用程序特定的错误代码（在区间0x80-0x9F中）
* gEvtAttributeWrittenWithoutResponse_c：当使用不带响应写入程序（ATT写入命令）写入属性时触发。由于此程序不需要响应，因此应用程序可以处理它，并在必要时将其写入数据库。无论该值是否有效，都不需要应用程序的响应
* gEvtLongCharacteristicWritten_c：当客户端已完成写入长特征值时触发。事件数据包括特征值属性的句柄和指向数据库中其值的指针

------------------------------------------------------------------------------------------------------------------------

# 6. GATT数据库应用程序接口

对于客户端和服务器之间的OTA数据包交换，GATT服务器模块自动从GATT数据库中检索数据，并响应来自对端客户端的所有ATT请求（前提是它通过了安全检查）。这可确保服务器应用程序不必对数据库执行任何类型的搜索。

但是，应用程序必须能够访问数据库，以将有意义的数据写入到其特征中。例如，温度传感器必须定期将温度（由外部温度计测量）写入到温度特征。

对于这些情况，**gatt_db_app_interface.h** 文件中提供了一些API。

> NOTE：此接口提供的所有函数都是同步执行的。操作的结果保存在返回值中，并且不会生成任何事件。

## 6.1 写入和读取属性

这些是从应用程序执行基本属性操作的两个函数：

```c
bleResult_t GattDb_WriteAttribute
(
    uint16_t    handle,
    uint16_t    valueLength,
    uint8_t *   aValue
);
```

值长度必须是有效的，正如创建数据库时定义的那样。否则，将返回 gGattInvalidValueLength_c 错误。

此外，如果数据库是静态创建的，如[创建GATT数据库](#7-创建gatt数据库)中所述，句柄可以通过枚举成员（在 **gatt_db.h** 中定义了一个友好的名称）引用。

```c
bleResult_t GattDb_ReadAttribute
(
    uint16_t    handle,
    uint16_t    maxBytes,
    uint8_t *   aOutValue,
    uint16_t *  pOutValueLength
);
```

aOutValue 数组必须以 maxBytes 大小进行分配。

## 6.2 查找属性句柄

尽管应用程序应该完全了解GATT数据库的内容，但在某些情况下，对某些属性句柄执行某些动态搜索可能会很有用。

要在已知其声明句柄的服务中查找特定的特征值句柄，提供了以下API：

```c
bleResult_t GattDb_FindCharValueHandleInService
(
    uint16_t        serviceHandle,
    bleUuidType_t   characteristicUuidType,
    bleUuid_t *     pCharacteristicUuid,
    uint16_t *      pOutCharValueHandle
);
```

如果返回值是 gBleSuccess_c，则句柄在 pOutCharValueHandle 中写入。如果 serviceHandle 是无效的或不是一个有效的服务声明，将返回 gBleGattDbInvalidHandle_c。否则，从 serviceHandle + 1 开始执行搜索。如果未找到给定UUID的特征，则该函数返回 gBleGattDbCharacteristicNotFound_c 值。

要在特征中查找给定类型的特征描述符，当特征值句柄已知时，提供了以下API：

```c
bleResult_t GattDb_FindDescriptorHandleForCharValueHandle
(
    uint16_t        charValueHandle,
    bleUuidType_t   descriptorUuidType,
    bleUuid_t *     pDescriptorUuid,
    uint16_t *      pOutDescriptorHandle
);
```

同样，函数返回 gBleGattDbInvalidHandle_c 表示句柄无效。否则，它从 charValueHandle + 1 开始搜索。然后，如果未找到指定类型的描述符，则返回 gBleGattDbDescriptorNotFound_c。否则，它的属性句柄在 pOutDescriptorHandle 中写入，并且函数返回 gBleSuccess_c。

最常用的特征描述符之一是客户端配置特征描述符（CCCD），其UUID等于 gBleSig_CCCD_d。对于此特定类型，将使用特殊API作为快捷方式：

```c
bleResult_t GattDb_FindCccdHandleForCharValueHandle
(
    uint16_t    charValueHandle,
    uint16_t *  pOutCccdHandle
);
```

------------------------------------------------------------------------------------------------------------------------

# 7. 创建GATT数据库

GATT数据库包含几个GATT服务，其中每个服务必须包含至少一个GATT特征。

属性数据库包含一组属性。每个属性都有四个字段：
* 属性手柄 - 一个2字节的数据库索引，从0x0001开始，随着每个新属性的增加而增加，不一定是连续的；最大值为0xFFFF
* 属性类型或UUID - 一个2字节、4字节或16字节的UUID
* 属性权限 - 1字节，包含访问标志；这定义了是否可以读取或写入属性的值以及每种操作类型的安全性要求
* 属性值 - 一个的最大为512个字节的数组

ATT不解释数据库中包含的UUID和值。它只处理基于属性句柄的数据传输。

GATT根据属性的UUID为属性赋予意义，并将它们分组为特征和服务。

有两种可能的方法来定义GATT数据库：在编译时（静态）或在运行时（动态）。

## 7.1 静态创建GATT数据库

为了在编译时定义GATT数据库，GATT_DB API提供了几个宏。这些宏在编译时以许多不同的方式扩展，生成相应的属性数据库，属性协议(ATT)可以在该数据库上运行。

这是定义数据库的默认方式。

GATT数据库定义写在两个文件中，其需要与所有宏扩展文件一起添加到应用程序项目中：
* **gatt_db.h** - 包含服务和特征的实际声明
* **gat_uuid128.h** - 包含自定义UUID的声明（16字节宽）；这些UUID被赋予一个用户友好的名称，其用于 **gatt_db.h** 文件以替换全部16字节序列

### 7.1.1 声明自定义128位UUID

所有的自定义128位UUID都在必需的文件 **gatt_uuid128.h** 中声明。

这个文件中的每一行都包含一个UUID声明。声明使用以下宏：
* UUID128 (name, byte1, byte2, …, byte16)

name 参数是用户友好的句柄，其在 **gatt_db.h** 文件中引用这个UUID。

16个字节以LSB优先顺序写入，每个使用0xZZ格式。

> NOTE：在某些情况下，它期望重用 **gatt_uuid128.h** 中声明的128位UUID。16字节数组可通过其友好名称获得，并可通过在应用程序中包含 **gatt_db_handles.h** 来访问。强烈建议仅在只读操作中使用它。例如：

```c
(gatt_uuid128.h)
UID128(uuid_service_wireless_uart, 0xE0, 0x1C, 0x4B, 0x5E, 0x1E, 0xEB, 0xA1, 0x5C, 0xEE, 0xF4,
0x5E, 0xBA, 0x00, 0x01, 0xFF, 0x01)

(app.c)
#include "gatt_db_handles.h"
........
/* Start Service Discovery*/
BleServDisc_FindService(peerDeviceId, gBleUuidType128_c, (bleUuid_t*)
&uuid_service_wireless_uart);
```

### 7.1.2 声明服务

有两种类型的服务：
* 主要服务
* 次要服务 - 这些服务只包括在其他主要或次要服务中

服务声明属性有一个UUID，其由Bluetooth SIG定义：
* 0x2800 a.k.a. <Primary Service> - 用于主要服务声明
* 0x2801 a.k.a. <Secondary Service> - 用于次要服务声明

服务声明属性权限是只读的，不需要身份验证。服务声明属性值包含服务UUID。服务范围从服务声明开始到下一个服务声明结束。在服务范围内声明的所有特征都被视为属于该服务。

#### 7.1.2.1 服务声明宏

以下宏将用于声明服务：
* PRIMARY_SERVICE (name, uuid16)
    * 最常用的
    * name 参数对所有宏都是通用的；它是生成的属性的通用用户友好的标识符
    * uuid16 是一个2字节的SIG定义的UUID，以0xZZZZ格式写入
* PRIMARY_SERVICE_UUID32 (name, uuid32)
    * 该宏是一个4字节的SIG定义的UUID，以0xZZZZZZZZ格式写入
* PRIMARY_SERVICE_UUID128 (name, uuid128)
    * uuid128 是在 **gatt_uuid128.h** 文件中自定义UUID的友好名称
* SECONDARY_SERVICE (name, uuid16)
* SECONDARY_SERVICE_UUID32 (name, uuid32)
* SECONDARY_SERVICE_UUID128 (name, uuid128)
    * 这三个都与主要服务声明类似

#### 7.1.2.2 包含声明宏

次要服务由其他服务（通常是主要服务）包括在内。主要服务也可能包含其他主要服务。包含是使用包含声明宏完成的：
* INCLUDE (service_name)
    * service_name 参数是用于声明次要服务的友好名称
    * 此宏仅用于具有SIG定义的2字节服务UUID的辅助服务
* INCLUDE_CUSTOM (service_name)
    * 此宏用于具有4字节UUID或16字节UUID的辅助服务

服务包含的效果是包含服务被认为包含所包含服务的所有特征。

### 7.1.3 声明特征

必须仅在服务内声明特征。特征属于最近声明的服务，因此GATT数据库必须始终以服务声明开始。

特征声明属性具有以下UUID，由Bluetooth SIG定义：
* 0x2803 a.k.a. <Characteristic>

特征声明属性的权限是：只读，不需要身份验证。

特征声明属性值包含：
* 特征UUID
* 特征值的声明句柄
* 特征特性 - 读、写、通知，等等（1个字节的标志）
  
特征范围从特征声明开始直到下一个新特征或服务声明结束。

如下这些在特征声明后：
* 特征值声明（强制性的；在特征声明之后）
* 零或多个特征描述符声明

#### 7.1.3.1 特征声明宏

以下宏用于声明特征：
* CHARACTERISTIC (name, uuid16, properties)
* CHARACTERISTIC_UUID32 (name, uuid32, properties)
* CHARACTERISTIC_UUID128 (name, uuid128,properties)
    * 有关uuidXXX参数说明，请参阅服务声明

properties 参数是位掩码。标志在 gattcharactertiesbitfields_t 中定义。

#### 7.1.3.2 声明特征值

特征值声明紧跟在特征声明之后，并使用以下宏之一：
* VALUE(name, uuid16, permissions, valueLength, valueByte1, valueByte2, …)
* VALUE_UUID32(name, uuid32, permissions, valueLength, valueByte1, valueByte2, …)
* VALUE_UUID128(name, uuid128, permissions, valueLength, valueByte1, valueByte2, …)
    * 有关uuidXXX参数说明，请参阅服务声明
    * permissions 参数是位掩码；标志在 gattAttributePermissionsBitFields_t 中定义
        * valueLength 是特征值要分配的字节数。在此参数之后，应有相同字节数的字节数组以0xZZ格式来表示此特征的初始值

这些宏用于声明固定长度的特征值。

某些特征具有可变长度值。对于那些特征，使用以下宏：
* VALUE_VARLEN (name, uuid16, permissions, maximumValueLength, initialValueLength, valueByte1, valueByte2, …)
* VALUE_UUID32_VARLEN (name, uuid32, permissions, maximumValueLength, initialValueLength, valueByte1, valueByte2, …)
* VALUE_UUID128_VARLEN (name, uuid128, permissions, maximumValueLength, initialValueLength, valueByte1, valueByte2, …)
    * 为此特征值分配的字节数为 maximumValueLength
    * valueByteXXX 参数的数量应等于 initialValueLength

显然，initialValueLength 最多等于 maximumValueLength。

#### 7.1.3.3 声明特征描述符

特征的描述符在特征值声明之后和下一个特征声明之前声明。

用于声明特征描述符的宏与用于声明固定长度特征值的宏非常相似：
* DESCRIPTOR (name, uuid16, permissions, descriptorValueLength, descriptorValueByte1, descriptorValueByte2, …)
* DESCRIPTOR_UUID32 (name, uuid32, permissions, descriptorValueLength, descriptorValueByte1, descriptorValueByte2, …)
* DESCRIPTOR_UUID128(name, uuid128, permissions, descriptorValueLength, descriptorValueByte1, descriptorValueByte2, …)

经常使用的特殊特征描述符是客户端特征配置描述符（CCCD）。这是客户端写入一些位以激活服务器通知 和/或 指示的描述符。它有一个保留的2字节的SIG定义的UUID（0x2902），其属性值仅包含1个字节（其中2个位用于配置，其余6个位保留）。

由于CCCD经常出现在标准BLE配置文件的特征定义中，因此使用特殊的宏来进行CCCD声明：
* CCCD (name)

这个简单的宏基本上等同于以下描述符声明：

```c
DESCRIPTOR (name, 0x2902, (gGattAttPermAccessReadable_c | gGattAttPermAccessWritable_c), 2, 0x00, 0x00)
```

### 7.1.4 静态GATT数据库定义示例

GAP服务必须出现在任何GATT数据库中。它的服务UUID等于0x1800 <GAP Service>，并且它包含三个只读特征，无需认证：设备名称，外观和外设首选连接参数。这些在SIG文档中也有明确定义的UUID。

此服务的定义如下所示：

```c
PRIMARY_SERVICE(service_gap, 0x1800)

    CHARACTERISTIC(char_device_name, 0x2A00, (gGattCharPropRead_c) )
        VALUE(value_device_name, 0x2A00, (gGattAttPermAccessReadable_c), 6, “Sensor”)

    CHARACTERISTIC(char_appearance, 0x2A01, (gGattCharPropRead_c) )
        VALUE(value_appearance, 0x2A01, (gGattAttPermAccessReadable_c), 2, 0xC2, 0x03)

    CHARACTERISTIC(char_ppcp, 0x2A04, (gGattCharPropRead_c) )
        VALUE(value_ppcp, 0x2A04, (gGattAttPermAccessReadable_c), 8, 0x0A, 0x00, 0x10, 0x00, 0x64, 0x00, 0xE2, 0x04)
```

另一个经常遇到的服务是扫描参数服务：

```c
PRIMARY_SERVICE(service_scan_parameters, 0x1813)

    CHARACTERISTIC(char_scan_interval_window, 0x2A4F, (gGattCharPropWriteWithoutRsp_c) )
        VALUE(value_scan_interval_window, 0x2A4F, (gGattAttPermAccessWritable), 4, 0x00, 0x00, 0x00, 0x00)

    CHARACTERISTIC(char_scan_refresh, 0x2A31, (gGattCharPropRead_c | gGattCharPropNotify_c) )
        VALUE(value_scan_refresh, 0x2A31, (gGattAttPermAccessReadable_c), 1, 0x00)
        CCCD(cccd_scan_refresh)
```

> NOTE：声明中给出的所有“用户友好”名称都静态定义为枚举成员，在数值上等于声明的属性句柄。这意味着如果 **gatt_db_handles.h** 包含在应用程序源文件中，那么在需要属性句柄的任何地方都可以使用其中一个名称作为函数的参数。例如，要从应用程序级代码中写入“扫描刷新特征”的值，请使用以下指令：

```c
#include "gatt_db_handles.h"
...
uint8_t scan_refresh_value = 0x12;
GattDb_WriteAttribute( char_scan_refresh, &scan_refresh_value, 1);
```

## 7.2 动态创建GATT数据库

要在运行时定义GATT数据库，必须在 **app_preinclude.h** 中定义 **gGattDbDynamic_d** 宏，其值等于1。

然后，应用程序必须使用 **gatt_db_dynamic.h** 接口提供的API来根据需要添加和删除服务和特征。

有关服务和特征参数的详细说明，请参见第7.1节。

### 7.2.1 初始化和发布

在将任何内容添加到数据库之前，必须使用一个空属性集合对其进行初始化。

GattDbDynamic_Init() API的自动调用由 **gatt_database.c** 源文件中的 GattDb_Init() 提供实现。应用程序特定的代码（例如，**app.c** 中的代码）不需要再次调用此API，除非在某些时候它使用 GattDb_ReleaseDatabase() 破坏了数据库。

### 7.2.2 添加服务

可用于添加服务的API是自解释的：
* GattDbDynamic_AddPrimaryServiceDeclaration
    * 服务UUID被指定为参数
* GattDbDynamic_AddSecondaryServiceDeclaration
    * 服务UUID被指定为参数
* GattDbDynamic_AddIncludeDeclaration
    * 服务UUID和句柄范围被指定为参数

这些函数有一个可选的输出参数 pOutHandle。如果其值不为NULL，则执行会在指向添加的声明的属性句柄的指向位置写入一个16位值。

应用程序可以将此句柄用作某些 GattDbApp API或服务删除函数中的参数。

在任何特征之前至少需要添加一个服务。

### 7.2.3 添加特征和描述符

用于添加特征和描述符的API列举如下：
* GattDbDynamic_AddCharacteristicDeclarationAndValue
    * 特征UUID，特性，访问权限和初始值被指定为参数
* GattDbDynamic_AddCharacteristicDeclarationWithUniqueValue
    * 对此API的多个调用分配了一个唯一的512字节值缓冲区作为应用程序的优化（该应用程序处理不总是需要单独存储的大值缓冲区）
* GattDbDynamic_AddCharacteristicDescriptor
    * 描述符UUID，访问权限和初始值被指定为参数
* GattDbDynamic_AddCccd
    * CCCD的快捷方式

### 7.2.4 删除服务和特征

要删除服务或特性，可以使用以下API，这两个API都只需要声明句柄作为参数：
* GattDbDynamic_RemoveService
* GattDbDynamic_RemoveCharacteristic

------------------------------------------------------------------------------------------------------------------------

# 8. 创建自定义配置文件

本章介绍用户如何通过定义配置文件和服务在BLE主机栈上创建可自定义的功能。以温度传感器和收集器应用程序（在BLE SDK中找到）使用的温度配置文件作为参考，以解释构建自定义功能的步骤。

## 8.1 定义自定义UUID

定义配置文件中包含的新服务的第一步是为服务和包含的特征定义自定义的128位UUID。这些值在 **gatt_uuid128.h** 中定义，该文件位于应用程序文件夹中。例如，温度配置文件对服务使用以下UUID：

```c
/* Temperature */
UUID128(uuid_service_temperature, 0xfb ,0x34 ,0x9b ,0x5f ,0x80 ,0x00 ,0x00 ,0x80 ,0x00 ,0x10 , 0x00 , 0x02 ,0x00 ,0xfe ,0x00 ,0x00)
```

服务和特征的定义在 **gattdb.h** 中进行，如[创建GATT数据库](#7-创建gatt数据库)中所述。有关如何构建数据库的更多详细信息，请参阅[应用程序结构](#9-应用程序结构)。

## 8.2 创建服务功能

SDK中的所有已定义服务都有一个通用模板，其帮助应用程序作出相应的行为。

服务本地存储已连接客户端的设备标识。该值在订阅和非订阅事件中被更改。

```c
/*! Temperature Service - Subscribed Client*/
static deviceId_t mTms_SubscribedClientId;
```

应用程序通过服务配置结构初始化和更改服务。它通常包含服务句柄，服务的初始值（例如，温度服务的初始温度）以及在某些情况下可以存储已保存测量值的用户特定结构（例如，血压服务）。以下是自定义温度服务的示例：

```c
/*! Temperature Service - Configuration */
typedef struct tmsConfig_tag
{
    uint16_t serviceHandle ;
    int16_t  initialTemperature ;
} tmsConfig_t ;
```

通过调用启动程序来初始化服务。该函数需要一个指向服务配置结构的指针作为输入。通常在初始化应用程序时调用此函数。它重置订阅客户端的静态设备标识，并初始化动态和静态特征值。温度服务（TMS）的示例如下所示：

```c
bleResult_t Tms_Start ( tmsConfig_t *pServiceConfig)
{
    mTms_SubscribedClientId = gInvalidDeviceId_c;
    
    return Tms_RecordTemperatureMeasurement (pServiceConfig-> serviceHandle , 
                                             pServiceConfig->initialTemperature );
}
```

设备连接到服务器时会触发服务订阅。它需要将对端设备标识作为输入参数来更新本地变量。断开连接时，将调用取消订阅函数以重置设备标识。对于温度服务：

```c
bleResult_t Tms_Subscribe (deviceId_t deviceId)
{
    mTms_SubscribedClientId = deviceId;
    return gBleSuccess_c;
}

bleResult_t Tms_Unsubscribe (void)
{
    mTms_SubscribedClientId = gInvalidDeviceId_c;
    return gBleSuccess_c;
}
```

根据服务的复杂性，API实现了额外的函数。对于温度服务，只有一个可以通过服务器通知的温度特性。API实现了记录测量函数，该函数将新测量值保存在GATT数据库中，并在可能的情况下将通知发送到客户端设备。该函数需要服务句柄和新的温度值作为输入参数：

```c
bleResult_t Tms_RecordTemperatureMeasurement (uint16_t serviceHandle, int16_t temperature)
{
    uint16_t handle;
    bleResult_t result;
    bleUuid_t uuid = Uuid16(gBleSig_Temperature_d);

    /* Get handle of Temperature characteristic */
    result = GattDb_FindCharValueHandleInService(serviceHandle, gBleUuidType16_c, &uuid, &handle);

    if (result != gBleSuccess_c)
        return result;

    /* Update characteristic value */
    result = GattDb_WriteAttribute(handle, sizeof( uint16_t ), ( uint8_t *)&temperature);
    
    if (result != gBleSuccess_c)
        return result;
    
    Hts_SendTemperatureMeasurementNotification(handle);
    
    return gBleSuccess_c;
}
```

为了适应重置服务的一些用例，调用停止函数。重置还意味着服务取消订阅。以下是温度服务的示例：

```c
bleResult_t Tms_Stop ( tmsConfig_t *pServiceConfig)
{
    return Tms_Unsubscribe();
}
```

## 8.3 GATT客户端交互

服务的客户端（包括服务发现，通知配置，属性读取等）由应用程序处理。应用程序调用GATT客户端API并做出相应的反应。此规则的唯一例外是服务接口声明了客户端配置结构。此结构通常包含服务句柄以及发现的所有特征值和描述符的句柄。此外，它还可以包含客户端可用于与服务器交互的值。对于温度服务客户端，结构如下：

```c
/*! Temperature Client - Configuration */
typedef struct tmcConfig_tag
{
    uint16_t                hService;
    uint16_t                hTemperature;
    uint16_t                hTempCccd;
    uint16_t                hTempDesc;
    gattDbCharPresFormat_t  tempFormat;
} tmcConfig_t;
```

------------------------------------------------------------------------------------------------------------------------

# 9. 应用程序结构

本章介绍了可在SDK中找到的蓝牙低功耗演示应用程序的组织。通过熟悉应用程序结构，用户可以快速地将其设计适应的现有演示或创建新的应用程序。

温度传感器应用程序用作展示架构的参考。

## 9.1 文件夹结构

下图展示了应用程序的文件夹结构：

![Figure 6. Application Folder structure in workspace](../Pic/BLE%20Application%20Developer's%20Guide-Figure6.jpg)

app 文件夹遵循一个特定的结构，该结构推荐用于任何使用BLE主机栈开发的应用程序：
* common 组包含所有配置文件和演示应用程序共享的应用程序框架：
    * 应用程序主要框架
    * BLE连接管理器
    * BLE栈以及任务初始化和配置
    * GATT数据库
* temperature_sensor 组包含特定于HRS应用程序的代码

bluetooth 文件夹/组 包含：
* controller/interface 和 host/interface - 控制器和主机的公共接口；功能包含在库（**ble_kw4xz_controller_lib.a** 和 **ble_4-x_host_lib_[armarch].a** ）中，库位于子文件夹 controller/lib 和 host/lib 中，其没有显示在IAR项目结构中，而是添加到库类别下的工具链链接器设置中
* hci_transport 包含HCI传输的头文件和源，当应用程序使用串行接口与外部控制器通信时。在示例演示中，主机和控制器都位于同一芯片上
* profiles 包含配置文件特定的代码；标准配置文件的每个演示应用程序都使用它

framework 文件夹/组 包含示例应用程序使用的框架部件。更多详情，请参阅 **Connectivity Framework Reference Manual**。

KSDK 文件夹/组 包含板特定的配置文件。

RTOS 文件夹包含所支持的操作系统的源代码或裸机的配置。

## 9.2 应用程序主要框架

应用程序主要模块包含所有程序使用的通用代码，如：
* 主要任务
* 主机栈任务和应用程序任务之间的消息传递框架
* 在低功耗应用程序中使用的空闲任务

### 9.2.1 主要任务

主要任务（main_task）是操作系统创建的第一个任务，也是初始化系统其余部分的任务。它初始化框架组件（内存管理器，计时器管理器等）和蓝牙主机栈（Ble_Initialize）。它还从 **app.c** 调用 BleApp_Init，该函数用于初始化已实现的应用程序特定的外设驱动程序。

该函数调用代表应用程序任务的 App_Thread。此任务重用为主要任务分配的堆栈，并被调用以处理主机栈发送的所有事件和消息。

主要任务的堆栈大小和优先级在 **fsl_os_abstraction_config.h** 中定义：

```c
#ifndef gMainThreadStackSize_c
#define gMainThreadStackSize_c 1024
#endif
#ifndef gMainThreadPriority_c
#define gMainThreadPriority_c 7
#endif
```

### 9.2.2 应用程序消息

该模块包含一个包装器，用于为主机任务上下文中的主机栈生成的事件创建消息，并将这些消息发送给应用程序，以在应用程序任务的上下文中处理。

例如，主机生成的连接事件由 App_ConnectionCallback 接收。该函数创建一条消息，将其置于应用程序队列的主机中，并使用 gAppEvtMsgFromHostStack_c 向应用程序发出信号。应用程序任务将消息出列并调用 App_HandleHostMessageInput，它调用实现应用程序特定代码（**app.c**）的相应回调，在此示例中为：BleApp_ConnectionCallback。

强烈建议应用程序开发者使用 **app.c** 模块在此类回调上添加自定义代码。

### 9.2.3 空闲任务

空闲任务是在应用程序启用框架低功耗模块时创建的。它包含在节点进入之前和退出睡眠模式之后执行的代码。更多低功耗功能的信息。请阅读[低功耗管理]()。

当运行FreeRTOS作为操作系统时，应用程序将通过链接 vApplicationIdleHook 来挂钩FreeRTOS库中实现的空闲任务。

应用程序开发者应将此函数用作应用程序特定代码的容器：

```c
static void App_Idle(void);
```

堆栈大小在 **ApplMain.h** 中定义：

```c
#ifndef gAppIdleTaskStackSize_c
#define gAppIdleTaskStackSize_c (400)
#endif
```

## 9.3 BLE连接管理器

连接管理器是一个助手模块，其包含通用的应用程序配置和与蓝牙主机栈的交互。它实现了以下事件和方法：
* 主机栈GAP通用事件
* GAP外设和GAP中央配置上的主机栈连接事件
* GAP外设或GAP中央的主机栈配置

### 9.3.1 GAP通用事件

GAP通用事件由主机栈触发，并通过通用回调发送到应用程序。在进行任何应用程序特定的交互之前，将调用连接管理器回调来处理通用的应用程序事件，例如设备地址存储。

```c
void BleApp_GenericCallback ( gapGenericEvent_t * pGenericEvent)
{
    /* Call BLE Conn Manager */
    BleConnManager_GenericEvent(pGenericEvent);

    switch (pGenericEvent-> eventType )
    {
        ...
    }
}
```

### 9.3.2 GAP配置

GAP中央或外设配置用于创建通用的配置（例如设置公共地址，注册安全需求，在白名单中添加绑定），之后应用程序可以自定义这些配置。在任何应用程序特定的配置GAP连接事件之前，在 BleApp_Config 函数中调用它：

```c
static void BleApp_Config()
{
    /* Configure as GAP peripheral */
    BleConnManager_GapPeripheralConfig();
    ...
}
```

### 9.3.3 GAP连接事件

GAP连接事件由主机栈触发，并通过连接回调发送。在进行任何应用程序特定的交互之前，都会调用连接管理器回调来处理通用的应用程序事件，例如设备连接，断开连接或配对相关请求。它在已注册的连接中调用，如下所示：

```c
static void BleApp_ConnectionCallback ( deviceId_t peerDeviceId, gapConnectionEvent_t *pConnectionEvent)
{
    /* Connection Manager to handle Host Stack interactions */
    BleConnManager_GapPeripheralEvent(peerDeviceId, pConnectionEvent);
    
    switch (pConnectionEvent-> eventType )
    {
        ...
    }
}
```

强烈建议应用程序开发者使用 **app.c** 模块添加自定义代码。

## 9.4 GATT数据库

gatt_db 包含了一个头文件集合分组（在 macros 子文件夹中）。这些宏用于通过不同方式扩展 **gatt_db.h** 文件的内容来为GATT数据库生成静态代码。[创建GATT数据库](#7-创建gatt数据库)解释了如何使用用户友好的宏来编写 **gatt_db.h** 文件，这些宏定义了GATT数据库。

在应用程序编译时，gatt_database.c文件中填充了用于分配和正确填充GATT数据库的枚举，结构和初始化代码。通过这种方式，可以创建并正确初始化 gattDatabase 数组和 gGattDbAttributeCount_c 变量（请参阅[GATT数据库](#22-gatt数据库)）。

> NOTE：请勿修改 gatt_db 文件夹及其子文件夹中包含的任何文件。

为了完成GATT数据库的初始化，此演示应用程序在其特定应用程序文件夹中包含了所需的 **gatt_db.h** 和 **gatt_uuid128.h** 文件，以及其他配置文件特定的配置和代码文件。

## 9.5 RTOS特定

### 9.5.1 操作系统选择

SDK为每个支持的操作系统（FreeRTOS OS）和裸机配置提供不同的项目。要在系统之间切换，用户需要切换工作区。

RTOS源代码位于KSDK包中，并链接到RTOS虚拟文件夹的工作区中，如下所示：

![Figure 7. Location of FreeRTOS souce code in workspace](../Pic/BLE%20Application%20Developer's%20Guide-Figure7.jpg)

### 9.5.2 BLE任务配置

为应用程序开发者提供了四个用于RTOS任务初始化的文件：
* **ble_controller_task_config.h** 和 **ble_controller_task.c**，用于控制器
* **ble_host_task_config.h** 和 **ble_host_tasks.c**，用于主机

建议重用这些文件，因为它们执行所有与RTOS相关的必要工作。当任务需要更大的堆栈大小或不同的优先级设置时，应用程序开发者应该只修改 **\*_config.h** 文件中的宏。应在 **app_preinclude.h** 文件中覆盖新值。

## 9.6 板配置

可以在 ConnSw/boards 文件夹中找到支持的板配置文件。这些文件包含驱动程序使用的时钟和引脚配置。用户可以根据设计修改引脚和时钟源的配置来自定义板文件。

![Figure 8. Board configuration files](../Pic/BLE%20Application%20Developer's%20Guide-Figure8.jpg)

## 9.7 BLE初始化

**ble_init.h** 和 **ble_init.c** 文件包含以下函数的声明和实现：

```c
bleResult_t Ble_Initialize
(
    gapGenericCallback_t gapGenericCallback
)
{
#if (gUseHciTransportDownward_d == 1)

    /* Configure HCI Transport */
    hcitConfigStruct_t hcitConfigStruct =
    {
        .interfaceType = gHcitInterfaceType_d,
        .interfaceChannel = gHcitInterfaceNumber_d,
        .interfaceBaudrate = gHcitInterfaceSpeed_d,
        .transportInterface = Ble_HciRecv
    };

    /* HCI Transport Init */
    if (gHciSuccess_c != Hcit_Init(&hcitConfigStruct))
    {
        return gHciTransportError_c;
    }

    /* BLE Host Tasks Init */
    if (osaStatus_Success != Ble_HostTaskInit())
    {
        return gBleOsError_c;
    }

    /* BLE Host Stack Init */
    return Ble_HostInitialize(gapGenericCallback, (hciHostToControllerInterface_t) Hcit_SendPacket);

#elif (gUseHciTransportUpward_d == 1)

    if (osaStatus_Success != Controller_TaskInit())
    {
        return gBleOsError_c;
    }

    /* BLE Controller Init */
    if (osaStatus_Success != Controller_Init((gHostRecvCallback_t)Hcit_SendPacket))
    {
        return gBleOsError_c;
    }

    /* Configure HCI Transport */
    hcitConfigStruct_t hcitConfigStruct =
    {
        .interfaceType = gHcitInterfaceType_d,
        .interfaceChannel = gHcitInterfaceNumber_d,
        .interfaceBaudrate = gHcitInterfaceSpeed_d,
        .transportInterface = Controller_RecvPacket
    };

    return Hcit_Init(&hcitConfigStruct);

#else

    /* BLE Controller Task Init */
    if (osaStatus_Success != Controller_TaskInit())
    {
        return gBleOsError_c;
    }

    /* BLE Controller Init */
    if (osaStatus_Success != Controller_Init(Ble_HciRecv))
    {
        return gBleOsError_c;
    }

    /* BLE Host Tasks Init */
    if (osaStatus_Success != Ble_HostTaskInit())
    {
        return gBleOsError_c;
    }

    /* BLE Host Stack Init */
    return Ble_HostInitialize(gapGenericCallback, ( hciHostToControllerInterface_t ) Controller_RecvPacket);

#endif
}
```

> NOTE：应用程序应该使用此函数，因为它正确执行了所有必需的BLE初始化。

下面提供了逐步分析：
* 首先，调用 **ble_host_task_config.h** 中的 Ble_HostTaskInit 函数。这将创建BLE主机栈所需的两个任务
* 接下来，基于 gUseHciTransportDownward_d 编译开关将初始化分成两个路径
    * 如果它被激活（等于1），则主机栈通过HCI接口与外部控制器通信。在此示例中，使用串行管理器（USB）初始化HCI接口。然后，Ble_HostInitialize 函数使用作为 hciHostToControllerInterface_t 参数的传输包传输函数以初始化主机
    * 如果它未激活（等于0），（这是演示程序的默认设置），则控制器库可用并且控制器任务通过 Controller_TaskInit 初始化。然后，用 Controller_Init 和 Ble_HostInitialize 初始化的两个堆栈将控制器的HCI接口与主机连接起来

## 9.8 BLE主机栈配置

BLE主机栈预先配置为四个可用库：
* 外设主机栈库
* 中央主机栈库
* 中央和外设主机栈库
* FSCI 中央和外设主机栈库

这些库位于 ConnSw/bluetooth/libs 文件夹中。用户应将其用例的最佳匹配库添加到其项目的链接器选项中。例如，温度传感器使用外设主机栈库，如下所示：

![Figure 9. Linker configuration for Temperature Sensor](../Pic/BLE%20Application%20Developer's%20Guide-Figure9.jpg)

## 9.9 配置文件配置

实现的配置文件和服务位于 ConnSw/bluetooth/profiles 文件夹中。应用程序链接实现配置文件所需的每个服务源文件和接口。例如，对于温度传感器，目录树如下所示：

![Figure 10. Linker configuration for Temperature Sensor](../Pic/BLE%20Application%20Developer's%20Guide-Figure10.jpg)

温度配置文件实现自定义温度服务，电池和设备信息服务。

## 9.10 应用程序代码

应用程序文件夹（ConnSw/app）包含common文件夹和应用程序文件夹。应用程序文件夹包含以下模块：
* **app.c** 和 **app.h**。此模块存储应用程序特定的功能（API用于特定触发器，外设的处理，栈的回调，低功耗的处理等）。

在初始化BLE主机栈之前，主要任务调用 BleApp_Init。此函数可以存储独立于主机栈工作的初始化模块。例如，温度传感器应用程序初始化温度传感器驱动：

```c
void BleApp_Init(void)
{
    TempSensor_Init();
}
```

初始化栈后，应用程序的通用回调调用 BleApp_Config。该函数包含初始化后对主机栈所做的配置。这包括注册回调，设置服务安全性，启动服务，分配定时器，将设备添加到白名单等。例如，温度传感器配置以下内容：

```c
static void BleApp_Config()
{
    /* Configure as GAP peripheral */
    BleConnManager_GapPeripheralConfig();

    /* Register for callbacks */
    App_RegisterGattServerCallback(BleApp_GattServerCallback);

    mAdvState. advOn = FALSE;

    /* Start services */
    tmsServiceConfig. initialTemperature = 100 * BOARD_GetTemperature();
    Tms_Start(&tmsServiceConfig);
    basServiceConfig. batteryLevel = BOARD_GetBatteryLevel();
    Bas_Start(&basServiceConfig);
    Dis_Start(&disServiceConfig);

    /* Allocate aplication timer */
    appTimerId = TMR_AllocateTimer();

#if (cPWR_UsePowerDownMode)
    PWR_ChangeDeepSleepMode(3);
    PWR_AllowDeviceToSleep();
#endif
}
```

为了启动应用程序功能，需要调用 BleApp_Start。该函数通常包含开始为传感器节点做广告或扫描中央设备的代码。在温度传感器的示例中，函数如下：

```c
void BleApp_Start(void)
{
    Led1On();

    if (mPeerDeviceId == gInvalidDeviceId_c)
    {
        /* Device is not connected and not advertising*/
        if (!mAdvState. advOn )
        {
            BleApp_Advertise();
        }
    }
    else
    {
        BleApp_SendTemperature();
    }
}
```

* **app_config.c**。此文件包含用于配置栈的数据结构。这包括广告数据，扫描数据，连接参数，广告参数，SMP密钥，安全需求等。
* **app_preinclude.h**。此头文件包含用于覆盖应用程序中任何模块的默认配置的宏。它作为预包含文件添加到IAR的预处理器命令行中：  
![Figure 11. Preinclude file](../Pic/BLE%20Application%20Developer's%20Guide-Figure11.jpg)
* **gatt_db.h** 和 **gatt_uuid128.h**。这两个头文件包含GATT数据库的定义和应用程序使用的自定义UUID。有关更多信息，请参阅[创建GATT数据库](#7-创建gatt数据库)。

------------------------------------------------------------------------------------------------------------------------

# 10. 低功耗管理

## 10.1 系统考虑因素

ARM®Cortex®-M0+ CPU和BLE链路层硬件具有自己的电源模式。因此，KW4x SoC的低功耗模式是BLE链路层电源模式和MCU低功耗模式之间的组合。

对于MCU，定义了两种类型的低功耗模式：睡眠模式（基于ARM架构睡眠模式）和深度睡眠模式（基于ARM架构深度睡眠模式）。本文档仅对深度睡眠模式感兴趣，此元件使用的MCU深度睡眠模式为LLS3和VLLS0/1。

BLE链路层也具有睡眠和深度睡眠模式，但此元件仅使用深度睡眠模式。要运行该模式，BLE链路层需要来自RF参考振荡器的时钟，并通过名为BLE系统时钟请求信号请求它。该信号由RSIM模块监控，并且当它被置为高电平时，RSIM产生中断请求。可以在LLWU中配置此中断以唤醒系统。进入深度睡眠状态后，BLE链路层取消激活BLE系统时钟请求，因为深度睡眠时不需要RF时钟。在BLE参考时钟寄存器在深度睡眠期间达到BLE唤醒实例寄存器中的值之前，可编程超时，BLE链路层再次激活BLE系统时钟请求。如果RSIM模块能够在此事件上产生中断，并且该中断在LLWU模块中配置为唤醒芯片，BLE链接层在退出DSM（深度睡眠模式）之前唤醒整个SoC。

## 10.2 何时/如何 进入低功耗状态

当整个系统空闲且所有软件层都同意时，系统应进入低功耗状态。对于此用例，定义了必须在系统中具有最低优先级的空闲任务，其用于进入和退出低功耗状态。因此，系统在空闲任务中进入低功耗状态，该任务仅在其他任务没有事件时运行。

在该任务中，低功耗示例调用静态函数 AppIdle。为此示例执行以下步骤：
* 检查设备是否可以进入睡眠状态（所有调用了 PWR_DisallowDeviceToSleep 的软件层都已调回 PWR_AllowDeviceToSleep）
* 设备通过调用 PWR_EnterLowPower 进入低功耗状态
* 从睡眠状态返回时，应用程序会检查唤醒原因。如果设备需要在唤醒时作出反应，则调用 PWR_DisallowDeviceToSleep 并调用特定函数。在此示例中，节点处理由键盘按下导致的唤醒
    ```c
    staticvoidApp_Idle(void)
    {
        PWRLib_WakeupReason_t wakeupReason;
        
        if ( PWR_CheckIfDeviceCanGoToSleep() )
        {
            /* Enter Low-Power */
            wakeupReason = PWR_EnterLowPower();

    #if gFSCI_IncludeLpmCommands_c
        /* Send Wake Up indication to FSCI */
        FSCI_SendWakeUpIndication();
    #endif

    #if gKBD_KeysCount_c > 0
        /* Woke up on Keyboard Press */
        if (wakeupReason.Bits.FromKeyBoard)
        {
            KBD_SwitchPressedOnWakeUp();
            PWR_DisallowDeviceToSleep();
        }
    #endif
        }
    }
    ```
* 只有在 PWR_AllowDeviceToSleep 被调回且空闲任务再次运行后，节点才会重新进入睡眠状态

系统上运行的每个 软件层/实体 都可以通过调用 PWR_DisallowDeviceToSleep 来阻止它进入低功耗状态。系统会保持唤醒状态，直到调用 PWR_DisallowDeviceToSleep 的所有软件层都调回 PWR_AllowDeviceToSleep 并且系统运行到空闲任务。MCU根据启动的定时器类型进入睡眠或深度睡眠。低功耗定时器是唯一不会阻止系统进入深度睡眠状态的定时器。如果启动任何其他定时器，则MCU进入睡眠而不是深度睡眠。用户应该停止除低功耗定时器之外的所有定时器。注意，启动定时器的函数，如 LED_StartFlash，会阻止系统进入深度睡眠状态。

## 10.3 深度睡眠模式

该元件实现了四种低功耗模式。用户可以使用 PWR_ChangeDeepSleepMode 函数在运行时切换模式。默认的低功耗模式由头文件 **PWR_Configuration.h** 中定义的值 cPWR_DeepSleepMode 来选择。

### 10.3.1 深度睡眠模式1

这种低功耗模式设计用于BLE栈处于活动状态时。广告中的节点示例如下所示：

![Figure 12. Deep Sleep Mode 1 usage example](../Pic/BLE%20Application%20Developer's%20Guide-Figure12.jpg)

在此模式下，MCU进入LLS3，并且BLE链路层进入深度睡眠状态。SoC可以通过（使用LLWU模块）在 BOARD_LLWU_PIN_ENABLE_BITMAP 中配置为唤醒源的GPIO、LPTMR超时，或BLE链路层唤醒中断（BLE_LL 参考时钟到达唤醒即使寄存器）从该模式唤醒。LPTMR定时器用于测量MCU在深度睡眠中花费的时间，以便在唤醒时同步低功耗定时器。有两种方法可以使用此模式：
* BLE栈决定它可以进入低功耗并调用 PWR_AllowDeviceToSleep。如果没有其他软件实体阻止系统进入深度睡眠（所有调用了 PWR_DisallowDeviceToSleep 的软件层都调回了 PWR_AllowDeviceToSleep）并且系统运行到空闲任务，则进入函数 PWR_EnterLowPower 并且系统准备进入低功耗模式1。BLE链路层状态会被检查，发现它不处于深度睡眠状态。BLE栈的一个函数会被调用以获得BLE链路层需要再次运行的最近时刻，并且使用该值对BLE链路层中的唤醒实例寄存器进行编程。然后将BLE链路层置于深度睡眠状态，MCU进入LLS3
* BLE栈决定它可以进入低功耗并调用 PWR_BLE_EnterDSM， 然后调用 PWR_AllowDeviceToSleep。通过这种方式，BLE链路层立即进入深度睡眠状态，剩下MCU在空闲任务中进入LLS3。如果没有其他软件实体阻止系统进入深度睡眠并且系统运行到空闲任务，则进入函数 PWR_EnterLowPower 并且系统准备完成进入低功耗模式1。BLE链路层状态会被检查并发现它处于深度睡眠状态，因此MCU将自身置于LLS3并最终达到深度睡眠模式1

在BLE链路层参考时钟寄存器达到唤醒寄存器中的值之前，超时为 cPWR_BLE_LL_OscStartupDelay + cPWR_BLE_LL_OffsetToWakeupInstant，BLE链路层唤醒整个SoC，系统恢复其活动。检查 **PWR_Configuration.h** 头文件中的两个定义。

### 10.3.2 深度睡眠模式2

这种低功耗模式设计用于BLE栈空闲时。在此模式下，MCU进入LLS3，并且BLE链路层进入深度睡眠状态。SoC通过（使用LLWU模块）在 BOARD_LLWU_PIN_ENABLE_BITMAP 中配置为唤醒源的GPIO或BLE链路层唤醒中断（BLE_LL 参考时钟寄存器到达唤醒实例寄存器）从此模式唤醒。LPTMR定时器用于测量MCU在深度睡眠中花费的时间，以便在唤醒时同步低功耗定时器。可以在编译时使用 **PWR_Configuration.h** 头文件中定义的 cPWR_DeepSleepDurationMs 或在运行时调用 PWR_SetDeepSleepTimeInMs 函数来配置深度睡眠的持续时间。

最大深度睡眠持续时间限制为 40959ms。

### 10.3.3 深度睡眠模式3

这种低功耗模式设计用于BLE栈空闲时。在此模式下，MCU进入LLS3，并且BLE链路层保持空闲。SoC通过（使用LLWU模块）在 BOARD_LLWU_PIN_ENABLE_BITMAP 中配置为唤醒源的GPIO或BLE链路层唤醒中断从此模式唤醒。LPTMR定时器用于测量MCU在深度睡眠中花费的时间，以便在唤醒时同步低功耗定时器。可以在编译时使用 **PWR_Configuration.h** 头文件中定义的 cPWR_DeepSleepDurationMs 或在运行时调用 PWR_SetDeepSleepTimeInMs 函数来配置深度睡眠的持续时间。

此模式下的最大可配置深度睡眠持续时间为 65535000ms（18.2小时）。

定期扫描的节点示例如下所示：

![Figure 13. Deep Sleep Mode 3 usage example](../Pic/BLE%20Application%20Developer's%20Guide-Figure13.jpg)

### 10.3.4 深度睡眠模式4

这是所有模式中的最低功耗模式。这种低功耗模式设计用于BLE栈空闲时。在此模式下，MCU进入 VLLS0/VLLS1，并且BLE链路层保持空闲。SoC通过（使用LLWU模块）在 BOARD_LLWU_PIN_ENABLE_BITMAP 中配置为唤醒源的GPIO从此模式唤醒。由于通过重置序列退出该深度睡眠模式，因此不对低功耗定时器进行同步。配置此模式有两个定义：
* cPWR_DCDC_InBypass 配置使用的VLLS模式。如果此定义为TRUE，则MCU进入VLLS0，否则MCU进入VLLS1，因为在DCDC降压或升压模式下不允许VLLS0
* cPWR_POR_DisabledInVLLS0。此定义仅在 cPWR_DCDC_InBypass 为TRUE时才有意义，因此MCU进入VLLS0模式。如果为TRUE，则此定义禁用VLLS0中的POR电路，从而使深度睡眠模式成为最低功耗模式

### 10.3.5 深度睡眠模式5

这种低功耗模式设计用于BLE栈空闲时。在此模式下，MCU进入VLLS2，并且BLE链路层保持空闲。SoC通过（使用LLWU模块）在 BOARD_LLWU_PIN_ENABLE_BITMAP 中配置为唤醒源的GPIO从此模式唤醒。

此模式具有部分SRAM保留。保留4KB的RAM（从0x20000000到0x20000FFF）。

### 10.3.6 深度睡眠模式6

这种低功耗模式设计用于BLE栈空闲时。在此模式下，MCU进入STOP。SoC通过以下方式从此模式唤醒：
* 通过使用LLWU模块在 BOARD_LLWU_PIN_ENABLE_BITMAP 中配置为唤醒源的GPIO 
* 使用LLWU模块的LPTMR超时。LPTMR定时器用于测量MCU在深度睡眠中花费的时间，以便在唤醒时同步低功耗定时器。可以在编译时使用 **PWR_Configuration.h** 头文件中定义的 cPWR_DeepSleepDurationMs 或在运行时调用 PWR_SetDeepSleepTimeInMs 函数来配置深度睡眠的持续时间。此模式下的最大可配置深度睡眠持续时间为 65535000ms（18.2小时）
* UART中断
* 来自BLE链路层的无线电中断

可在下表中找到可用电源模式的摘要：

![Table 3. Available power modes](../Pic/BLE%20Application%20Developer's%20Guide-Table3.jpg)

## 10.4 低功耗使用示例

### 10.4.1 BLE栈空闲时使用低功耗

在这种情况下使用的最有效的低功耗模式是深度睡眠模式3，同时也保留SRAM。应用程序还必须将 cPWR_DeepSleepDurationMs 配置为允许正在运行的低功耗定时器在到期之前更新的值。例如，如果应用程序想要每30秒唤醒以扫描一次，则宏的值不得超过30000。

要允许设备进入睡眠状态，请在栈初始化或断开连接后调用 PWR_ChangeDeepSleepMode 和 PWR_AllowDeviceToSleep。

```c
PWR_ChangeDeepSleepMode(3);
PWR_SetDeepSleepTimeInMs(cPWR_DeepSleepDurationMs);
PWR_AllowDeviceToSleep();
```

### 10.4.2 广告时使用低功耗

广告要求BLE链路层发送广告包并在配置的间隔上侦听连接请求，而不需要更高层的介入。因此，深度睡眠模式1是此用例的最佳候选者。

要允许设备进入深度睡眠模式1，请调用 PWR_ChangeDeepSleepMode 和 PWR_AllowDeviceToSleep，在调用函数后立即开始广告。应用程序还必须将 cPWR_DeepSleepDurationMs 配置为一个值，该值允许正在运行的低功耗定时器在到期之前进行更新。

```c
BleApp_Advertise();
PWR_ChangeDeepSleepMode(1);
PWR_SetDeepSleepTimeInMs(cPWR_DeepSleepDurationMs);
PWR_AllowDeviceToSleep();
```

MCU进入睡眠状态并在接收到连接请求或在链路层唤醒超时时唤醒。BLE在广告事件间进入DSM。

当接收到连接请求时，节点不允许睡眠以为服务发现等其他程序做好准备。

```c
PWR_DisallowDeviceToSleep();
```

### 10.4.3 扫描时使用低功耗

扫描要求BLE链路层在整个程序中处于运行模式。扫描完成后设备可以进入睡眠状态，或者保持活动状态（找到合适的设备）。这种情况下，深度睡眠模式2和3是最佳候选者。选择哪个模式取决于两次连续扫描之间的间隔，因为深度睡眠模式2的最大超时时间为 40959ms。

要允许设备进入深度睡眠模式2，请调用 PWR_ChangeDeepSleepMode 和 PWR_AllowDeviceToSleep。应用程序还必须将 cPWR_DeepSleepDurationMs 配置为一个值，该值允许正在运行的低功耗定时器在到期之前进行更新。

```c
PWR_ChangeDeepSleepMode(2);
PWR_SetDeepSleepTimeInMs(cPWR_DeepSleepDurationMs);
PWR_AllowDeviceToSleep();
```

当控制器关闭扫描时，可以在 gScanStateChanged_c 事件上完成此操作。当再次扫描时，设备可以被低功耗定时器超时时唤醒。

### 10.4.4 在连接中使用低功耗

连接期间的低功耗需要考虑连接间隔、从设备延迟和监视超时。BLE链路层必须定期发送空PDU以维持连接，因此它必须在DSM中。因此，深度睡眠模式1是此用例的最佳候选者。

应该在 gConnEvtConnected_c 事件上调用该函数。

```c
case gConnEvtConnected_c:
{
    PWR_ChangeDeepSleepMode(1);
    PWR_SetDeepSleepTimeInMs(cPWR_DeepSleepDurationMs);
    PWR_AllowDeviceToSleep();
}
```

------------------------------------------------------------------------------------------------------------------------

