---
lab:
  task: Prepare your environment for administration
  exercise: Exercise 0 - Prepare your environment for administration
---

## WWL 租户 - 使用条款

如果在讲师引导式培训过程中向你提供租户，请注意，提供租户旨在支持讲师引导式培训中的动手实验室。

租户不应共享或用于动手实验室以外的用途。 本课程使用的租户为试用租户，课程结束后无法使用或访问，不符合扩展条件。

租户不得转换为付费订阅。 在本课程中获得的租户仍然是 Microsoft Corporation 的财产，我们保留随时获取访问权限和收回的权利。

# 实验室设置：为管理准备环境

在此实验室中，你将为管理任务配置和准备环境。 你将激活必要的功能、设置管理权限，以及确保正确配置关键元素。

**任务**：

- 在 Microsoft Purview 门户中启用审核
- 分配合规性角色
- 浏览 Microsoft Purview 门户

## 任务 – 在 Microsoft Purview 门户中启用审核

在此任务中，你将在 Microsoft Purview 门户中启用“审核”以监视门户活动。

1. 使用管理员**** 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 打开 Microsoft Edge。

1. 在 Microsoft Edge**** 中，导航到`https://purview.microsoft.com`，并以 MOD 管理员****`admin@WWLxZZZZZZ.onmicrosoft.com` 的身份（其中 ZZZZZZ 是实验室托管提供商提供的唯一租户前缀）登录。 管理员的密码应由实验室托管提供程序提供。

1. 在 Microsoft Edge 中，导航到 Microsoft Purview 门户，`https://purview.microsoft.com`，然后登录。

1. 有关新的 Microsoft Purview 门户的消息将显示在屏幕上。 选择“**开始使用**”以访问新门户。

    ![显示“欢迎使用新的 Microsoft Purview 门户屏幕”的屏幕截图。](../Media/welcome-purview-portal.png)

1. 从左侧边栏中选择“**解决方案**”，然后选择“**审核**”。

1. 在“**搜索**”页面，选择“**开始录制用户和管理活动**”栏以启用审核日志记录。

    ![显示“开始录制用户和管理员活动”按钮的屏幕截图。](../Media/enable-audit-button.png)

1. 选择此选项后，蓝色栏应从此页面消失。

    >[!Note] **注意:前提是“审核”按钮不启用日志记录**
    >
    >在一些租户中，选择“开始记录用户和管理员活动”**** 可能不会激活审核。  
    >
    >如果出现这种情况，你可以改为通过 PowerShell 启用审核：
    >
    >1. 通过右键单击 Windows 按钮打开提升的终端窗口，然后选择“终端 (管理员)”****。  
    >
    >1. 安装最新的 Exchange Online PowerShell**** 模块：
    >
    >     ```powershell
    >     Install-Module ExchangeOnlineManagement
    >     ```
    >
    >     键入“Y”**** 表示“是”并按“Enter”**** 来确认任何提示。
    >
    >1. 输入以下命令，更改执行策略：
    >
    >     ```powershell
    >     Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    >     ```
    >
    >1. 关闭提升的终端窗口并打开一个常规 PowerShell 会话。
    >
    >1. 连接到 Exchange Online：
    >
    >     ```powershell
    >     Connect-ExchangeOnline
    >     ```
    >
    >    以`admin@WWLxZZZZZZ.onmicrosoft.com` 身份登录（其中 ZZZZZZ 是实验室托管提供商的唯一租户前缀）。 管理员的密码应由实验室托管提供程序提供。
    >
    >1. 检查是否已启用审核：
    >
    >     ```powershell
    >     Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    >     ```
    >
    >    如果返回 False**__**，请启用审核功能：
    >
    >     ```powershell
    >     Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    >     ```
    >
    >1. 验证现在已启用它：
    >
    >     ```powershell
    >     Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    >     ```
    >
    >    审核功能处于活动状态后，该命令应返回 True**__**。

已在 Microsoft 365 中成功启用审核。

## 任务 – 分配合规性角色

在此任务中，你会将**合规性管理员**角色分配给这些实验室练习中涉及到的用户。

1. 在**Microsoft Edge** 中，导航到 Microsoft 365 管理中心。`https://admin.microsoft.com` 你需要以具有**全局管理员**权限的用户身份登录。

1. 在左侧边栏中，展开“**用户**”，然后选择“**活动用户**”。

1. 选择或创建用户以继续完成这些实验室练习。

   如果选择使用现有用户，请选择具有最低权限的用户以获得最低访问权限。

   1. 如果创建新用户，请为用户分配适合这些实验室练习的许可证。 用户必须具有 Microsoft 365 E5 许可证或适用于这些练习的兼容加载项。 在新用户设置的可选设置中为用户分配**合规性管理员**角色，然后完成新用户创建。

   1. 如果修改现有用户的访问权限，请选择该用户，然后选择“**管理角色**”。 向用户分配**合规性管理员**角色并保存所做的更改。

1. 选择右上角的用户图标，然后选择“**退出登录**”，使具有“全局管理员”访问权限的帐户退出登录。

   示例：

   ![显示退出登录 MOD 管理员帐户的导航路径的屏幕截图。](../Media/sign-out.png)

你已成功向用户分配**合规性管理员**角色，需要先完成此操作才能执行本实验室的其他练习。

## 任务 – 浏览 Microsoft Purview 门户

在此任务中，你将以之前授予**合规性管理员**角色的用户身份登录，以浏览 Microsoft Purview 门户。 在后续实验室和练习中，此角色将称为**合规性管理员**。

1. 在“Microsoft Edge”中，导航到`https://purview.microsoft.com`。

1. 显示“选择帐户”窗口时，请选择“使用其他帐户” 。

1. 显示“**登录**”窗口时，以你之前选作**合规性管理员**的用户身份登录。

1. 熟悉新的 Microsoft Purview 门户。 完成后，让浏览器窗口保持打开状态。

你已成功切换到**合规性管理员**的帐户，现在可以开始使用实验室。
