##API
###获取 App Delegate
- delegate

###获取 App Windows
- keyWindow
 - 最近发送makeKeyAndVisible消息的window
- Windows
 - 当前与app相关联的window，不包括系统创建和管理的，例如显示status bar的window
 - The windows in the array are ordered from back to front by window level; thus, the last window in the array is on top of all other app windows.

###控制和处理 Events

###打开 URL 资源
- \- openURL:（iOS 2.0–10.0）
- \- canOpenURL:

###管理 App Appearance
- statusBarFrame
- networkActivityIndicatorVisible
- applicationIconBadgeNumber
- userInterfaceLayoutDirection

