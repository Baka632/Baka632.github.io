---
layout: post
title: UWP的标题栏
description: >
 关于UWP的标题栏
categories: [uwp]
---

# UWP的标题栏
UWP的标题栏一般情况下有**五个**元素，分别是：
* "返回"按钮(当无法返回时"返回"按钮会隐藏)
* 标题
* "最小化"按钮
* "最大化"按钮
* 关闭按钮

如图所示
![dc6366cd-faa6-4c6e-a5cf-463e79c70d64.png](https://storage.live.com/items/9EADE23CF2DB11C4!115?authkey=AFS7TPnPU9OPxsk)
这是一般的标题栏，但是，这种标题栏看起来不是很美观，所以我们要改变它！

# 标题栏简单的颜色自定义
如果只想改变颜色，那么这是非常简单的！只需要一些代码就可以搞定。
下面是一个例子：
>此代码可放在应用的 OnLaunched 方法 (App.xaml.cs) 中、对 Window.Activate 的调用的后面，或应用的第一页中。

	// using Windows.UI.ViewManagement;
    
	var titleBar = ApplicationView.GetForCurrentView().TitleBar;
    
	// 设置活动窗口的标题栏颜色
	titleBar.ForegroundColor = Windows.UI.Colors.White; //前景色
	titleBar.BackgroundColor = Windows.UI.Colors.Green; //背景色
	titleBar.ButtonForegroundColor = Windows.UI.Colors.White; //按钮前景色
	titleBar.ButtonBackgroundColor = Windows.UI.Colors.SeaGreen; //按钮背景色

	// 设置非活动窗口的标题栏颜色
	titleBar.InactiveForegroundColor = Windows.UI.Colors.Gray; //前景色
	titleBar.InactiveBackgroundColor = Windows.UI.Colors.SeaGreen; //背景色
	titleBar.ButtonInactiveForegroundColor = Windows.UI.Colors.Gray; //按钮前景色
	titleBar.ButtonInactiveBackgroundColor = Windows.UI.Colors.SeaGreen; //按钮背景色

设置标题栏颜色时需要注意以下几点：
* 按钮背景颜色不会应用于关闭按钮的悬停和按下状态。 关闭按钮始终对这些状态使用系统定义的颜色。
* 使用系统后退按钮时，按钮颜色属性会应用于该按钮。
* 将颜色属性设置为 null 会将其重置为默认的系统颜色。
* 你无法设置透明色。 颜色的 alpha 通道会被忽略。

另外，Windows 为用户提供了将选定的主题色应用于标题栏的选项。 如果要设置任何标题栏颜色，建议显式设置所有颜色。 这可以确保不存在因用户定义的颜色设置而出现意外的颜色组合。

### 将亚克力扩展到标题栏
若要创建无缝的应用窗口外观，可以将 Acrylic 应用到标题栏区域。 此示例中将 Acrylic 扩展到标题栏的方式是将默认标题栏隐藏，然后将 ApplicationViewTitleBar 对象的 ButtonBackgroundColor 和 ButtonInactiveBackgroundColor 属性设置为 Colors.Transparent。

应用的客户端区域会进行扩展以覆盖整个窗口，包括标题栏区域。 你将负责对整个窗口（在应用画布顶部重叠的标题按钮除外）进行绘制和输入处理。

以下示例介绍如何将亚克力扩展到标题栏
>此代码也可放在应用的 OnLaunched 方法 (App.xaml.cs) 中、对 Window.Activate 的调用的后面，或应用的第一页中。

	// using Windows.ApplicationModel.Core;

	// 隐藏默认的标题栏
	CoreApplication.GetCurrentView().TitleBar.ExtendViewIntoTitleBar = true;
    ApplicationViewTitleBar titleBar = ApplicationView.GetForCurrentView().TitleBar;
    titleBar.ButtonBackgroundColor = Colors.Transparent;
    titleBar.ButtonInactiveBackgroundColor = Colors.Transparent;

这个操作不会影响到系统的默认按钮，但是应用标题会受到影响，因此需要使用 CaptionTextBlockStyle 为应用程序标题绘制标题栏的TextBlock。


	<TextBlock Text="应用标题" 
               Style="{StaticResource CaptionTextBlockStyle}" 
               x:Name="TitleText"
         />

关于更多自定义操作，请访问微软官方文档[标题栏自定义](https://docs.microsoft.com/zh-cn/windows/uwp/design/shell/title-bar)
