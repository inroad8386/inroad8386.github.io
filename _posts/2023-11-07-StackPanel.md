---
title: StackPanel
date: 2023-11-08 00:00:01 
tags: 
description:
image: 
published: true
tags : study
---

## StackPanel
다른 요소를 수평 또는 수직으로 정렬하는 데 사용되는 레이아웃 컨테이너입니다. <br>
StackPanel은 자식 요소들을 순서대로 나란히 또는 쌓아서 배치할 수 있으며, 각 요소는 다른 요소와 겹치지 않고 다음 요소와 이웃합니다.



```cs

 <StackPanel  Orientation="Horizontal"
                    VerticalAlignment="Center"
                    HorizontalAlignment="Center">
            <TextBlock Text="Rectangle:"
                       VerticalAlignment="Center"/>

            <Rectangle Stroke="Blue"
                       Fill="Red"
                       Width="72"
                       Height="72"
                       Margin="12 0"
                       VerticalAlignment="Center"/>

            <TextBlock Text="Ellipse:"
                       VerticalAlignment="Center"/>

            <Ellipse Stroke="red"
                       Fill="blue"
                       Width="72"
                       Height="72"
                       Margin="12 0"
                       VerticalAlignment="Center"/>

            <TextBlock Text="Petzold:"
                       VerticalAlignment="Center"/>
            
            <Image Source="http://www.charlespetzold.com/pw6/PetzoldJersey.jpg"
                   Stretch="Uniform"
                   Width="72"
                   Margin="12 0"
                   VerticalAlignment="Center"></Image>

        </StackPanel>
    </Grid>

```



<p align="center">

 <img src="/assets/img/stackpanel.PNG">

</p>

**StackPanel**의 중요한 속성은 **Orientation**입니다. 이 속성을 사용하여 **StackPanel**의 배치 방향을 설정할 수 있습니다. <br>**Orientation**을 **"Horizontal"**으로 설정하면 자식 요소들이 **수평**으로 나란히 배치되며, **"Vertical"**로 설정하면 **수직**으로 쌓아 올릴 수 있습니다.


<br>
<br>

## Ellipse
타원 모양을 나타내는 시각적 요소입니다.<br> Ellipse는 원 또는 타원을 그릴 때 사용됩니다.<br>  주로 다음과 같은 속성을 가지고 있으며 이를 통해 원 또는 타원의 모양과 모양을 변경할 수 있습니다<br> <br> 
**Width와 Height (너비와 높이)**<br>
 Ellipse의 너비와 높이를 설정하여 원 또는 타원의 크기를 결정합니다.

**Fill (채우기)**<br>
 Ellipse 내부를 어떻게 채울 것인지를 정의하는 속성입니다. <br>
 이 속성을 사용하여 색상, 그라데이션, 이미지 또는 브러시를 지정할 수 있습니다.

**Stroke (테두리)** <br>
Ellipse의 테두리 선의 스타일을 설정합니다. <br>
이 속성을 사용하여 테두리의 색상, 굵기 및 스타일을 지정할 수 있습니다.

**StrokeThickness (테두리 두께)**<br>
Ellipse의 테두리 두께를 설정합니다. <br>
두께를 조절하여 테두리의 굵기를 변경할 수 있습니다.

WPF의 Ellipse 요소에 Stretch 속성을 **"Uniform"**으로 설정하면 Ellipse이 부모 컨테이너에 맞추어 일정한 비율로 확대 또는 축소됩니다.<br>
 이는 원래의 가로 세로 비율을 유지하면서 크기를 조정하는 것을 의미합니다.<br><br>

```cs

<Ellipse Width="100" Height="50" Fill="Blue" Stretch="Uniform" />

```
Ellipse은 가로와 세로 크기를 Uniform으로 설정하므로 가로와 세로 크기의 비율은 항상 유지되며, 확대 또는 축소할 때에도 비율이 일정하게 유지
<br><br>



## WhatSize - Width,Height 값 자동으로 변경
```cs

   <Grid>
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Center" VerticalAlignment="Top">
            <TextBlock Text="&#x21A4;" />
            <TextBlock Text="{Binding ElementName=page, Path=ActualWidth}" />
            <TextBlock Text="pixels &#x21A6;"/>
        </StackPanel>


        <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
            <TextBlock Text="&#x21A5;" TextAlignment="Center" />
                
        <StackPanel Orientation="Horizontal" 
                    HorizontalAlignment="Center">
            <TextBlock Text="{Binding ElementName=page, Path=ActualHeight}" />
            <TextBlock Text="Pixels" />
        </StackPanel>
        <TextBlock Text="&#x21A7;" TextAlignment="Center" />
        </StackPanel>
    </Grid>

```
<p align="center">
 <img src="/assets/img/act.gif">
</p>

**ActualWidth**와 **ActualHeight**는 **FrameworkElement** 클래스의 속성 중 하나로, 요소의 현재 실제 너비를 나타냅니다.<br> 이것은 요소가 화면에서 차지하는 실제 너비를 나타내며, 동적으로 변경됩니다.<br> 
이 바인딩은 **ActualWidth**와 **ActualHeight** 속성을 사용하여 요소의 실제 너비와 높이를 읽고 해당 값을 표시하는 데 사용됩니다.<br> 
변경된 요소의 너비와 높이에 따라 텍스트 또는 레이아웃이 자동으로 조정됩니다.
<br> <br> 


## ScroolViewer
애플리케이션에서 스크롤 가능한 영역을 만들기 위해 사용되는 컨트롤입니다.<br>
 ScrollViewer는 내부의 컨텐츠가 화면에 맞지 않는 경우 사용자가 스크롤하여 컨텐츠를 볼 수 있도록 해줍니다.<br>

## 사용법

 ```cs
     <Grid>
        <ScrollViewer>
            <StackPanel Name="stackPanel"></StackPanel>
        </ScrollViewer>
    </Grid>

 ```

## 특징

**스크롤 바**<br>
 내부 컨텐츠의 크기가 스크린보다 큰 경우 수직 및 수평 스크롤 바를 제공하여 사용자가 컨텐츠를 스크롤할 수 있게 합니다.
<br>

**자동 크기 조정** <br>
ScrollViewer는 내부 컨텐츠의 크기에 따라 자동으로 크기를 조정할 수 있습니다. <br>
이것은 내부 컨텐츠의 크기가 변경될 때 ScrollViewer가 올바르게 동작하게 만듭니다.<br>


**컨텐츠 배치**<br>
 ScrollViewer 내부에는 하나의 컨텐츠만 포함될 수 있으며 이 컨텐츠는 ScrollViewer의 가로 또는 세로 방향 스크롤 가능한 영역 내에 배치됩니다.<br>

**스타일링 및 템플릿**<br>
 ScrollViewer는 WPF 스타일 및 템플릿을 사용하여 외관을 사용자 지정할 수 있습니다.<br>
  따라서 스크롤 바 및 배경과 같은 요소들을 사용자 정의할 수 있습니다.<br>



<br><br><br><br><br>
## 참조 
찰스 페졸드의 Programming Windows