---
title: Resource Dictionary
date: 2023-09-21 00:58:47 
tags: 
description:
image: 
published: true
tags : study
---

## Resource Dictionary
XAML을 사용하여 앱의 UI 또는 리소스를 정의
<br>
리소스는 일반적으로 두 번 이상 사용할 것으로 예상하는 일부 개체의 정의
<br>
향후 XAML 리소스 참조용으로 해당 이름처럼 작동하는 리소스 키를 지정
<br>
<br><br>


## XAML 리소소 사전 추가
![](/assets/img/dictionary.PNG)
<br>
<br>
Ctrl + Shift + A (새 항목 추가) -  리소스 사전 클릭 
<br><br><br>

## ButtonStyle.xaml
```cs

    <Style x:Key="BtnStyle" TargetType="Button"> // key = BtnStyle
        <Setter Property="FontSize" Value="20"/> // 폰트 사이즈
        <Setter Property="Foreground" Value="Navy" /> // 글자색
        <Setter Property="Background" Value="White"/> // 배경색
        <Setter Property="BorderBrush" Value="Navy"/> // 테두리색
        <Setter Property="BorderThickness" Value="3"/> // 테두리 굵기
    </Style>

```
<br> 
리소스 사전으로 생성한 파일이며 특성을 담을 스타일을 설정<br>
다음과 같은 스타일을 저장할 키 값을 Style x:Key="BtnStyle" 로 정의
<br><br><br>

## MainWindow.xaml
![](/assets/img/main.PNG)
```cs

    <Window.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="/ButtonStyle.xaml"/>
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Window.Resources>

      <Grid>
        <Button Style="{StaticResource BtnStyle}" // key = BtnStyle
        Content="MainWindow"
        HorizontalAlignment="Left" 
        Margin="255,150,0,0" 
        VerticalAlignment="Top" 
        Width="235"
        Height="100"/>

    </Grid>

```
<br>
Resource Dictionary 추가를 위해 MergedDictionaries 안의  Source 값을 지정<br>
처음에 생성했던 Dictionary 파일의 ButtonStyle.xaml의 경로를 Source의 값에 설정<br>
<br><br>
<br>
## StaticResource 

```cs

    <Button Style="{StaticResource BtnStyle}" // key = BtnStyle

```

XAML 리소스 사전에 정의된 XAML 특성 값을 가져오기 위한 기술<br>

ButtonStyle.xaml 에서 정의한  Style x:Key="BtnStyle" 에 의해 <br>
MainWindow.xaml 에서 Button Style="{StaticResource BtnStyle}" 하여  특성의 값을 가져옴
<br>
<br>
<br>



## SubWindow.xaml 미완
![](/assets/img/sub_1.PNG)

```cs

<Window x:Class="ResourceDictionary.SubWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:ResourceDictionary"
        mc:Ignorable="d"
        Title="SubWindow" Height="450" Width="800">
    <Grid>
        <Button Style="{StaticResource BtnStyle}"  // key = BtnStyle
        Content="SubWindow"
        HorizontalAlignment="Left"
        Margin="285,170,0,0"
        VerticalAlignment="Top"
        Width="210"
        Height="70"/>
    </Grid>

</Window>

```
<br>
MainWindow.xaml 에서는 <ResourceDictionary Source="/ButtonStyle.xaml"/> 를 추가하여 버튼의 스타일을 특성을 불러왔다
<br>
하지만 리소스에 대한 참조소스가 없으므로 특성이 적용 되지 않는다
<br>
<br>
SubWindow.xaml 에서도 같은 특성을 이용하고 싶은데  리소스를 또 작성해야 하는가?
<br>
그렇지 않다 추가적인 윈도우에서도 적용 하고싶으면 App.xaml에 리소스를 작성하면 모든 윈도우에서 사용이 가능하기 때문에 똑같은 작업을 반복 하지 않아도 된다
<br>
<br>
<br>
<br>

## App.xaml
![](/assets/img/sub.PNG)


```cs

<Application x:Class="ResourceDictionary.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:ResourceDictionary"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="/ButtonStyle.xaml"/>
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
         
    </Application.Resources>
</Application>

```
App.xaml에 리소스를 작성한 후 subwindow의 화면이다 <br> 리소스 딕셔너리의 스타일 특성을 잘 불러와진 모습이다 <br><br>
추가적으로 Mainwindow에 작성한 리소스를 제거 해주어도 <br>이미 App.xaml에 작성하였기 때문에 특성은 유지 된다

<br><br>
## 이글을 마치며
Resource Dictionary는 자주 사용하는 자원들을 데이터로 저장하여 
<br>객체를 재사용 하고 접근함으로 유용해보인다





