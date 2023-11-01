---
title: StoryBoard
date: 2023-10-27 00:58:47 
tags: 
description:
image: 
published: true
tags : study
---

## StoryBoard
WPF에서 Storyboard는 애니메이션 및 시각적 효과를 정의하고 제어하기 위한 중요한 요소 중 하나입니다.<br> Storyboard를 사용하면 XAML 또는 코드를 통해 요소의 속성을 변경하여 애니메이션을 만들고 제어할 수 있습니다.

## Storyboard를 사용하는 주요 단계 및 개념
**애니메이션 요소 정의**<br>
먼저 애니메이션을 적용할 UI 요소를 선택하고 해당 요소의 속성을 정의합니다. 이 속성은 애니메이션 중에 변경될 것입니다. 예를 들어, 버튼의 위치, 크기, 색상 또는 투명도와 같은 속성을 선택할 수 있습니다.

**애니메이션 키 프레임 정의**<br>
Storyboard 내에서 애니메이션의 시작과 끝을 정의하는 키 프레임(KeyFrame)을 생성합니다.<br> 시작과 끝 값 사이의 중간 단계도 추가로 정의할 수 있습니다.<br> 각 키 프레임에는 속성의 값을 변경할 지점 및 시간 간격이 포함됩니다.

**Storyboard 정의**<br> Storyboard 객체를 만들고, 그 안에 애니메이션을 적용할 대상 요소(예: Control 또는 UIElement) 및 해당 요소의 어떤 속성을 애니메이션화할지 설정합니다.

**Trigger 설정**<br> 애니메이션이 시작될 조건을 설정합니다. 이를 트리거(Trigger)로 지정할 수 있으며, 이벤트, 시간 지연, 버튼 클릭과 같은 상황에서 애니메이션을 실행할 수 있습니다.

**애니메이션 재생**<br> Storyboard를 실행하면 정의한 애니메이션이 시작됩니다. <br>애니메이션이 완료되면 요소의 속성은 설정한 값으로 변경됩니다.<br><br>

Storyboard를 사용하면 WPF 애플리케이션에서 다양한 시각적 효과를 만들 수 있습니다. <br>이를 사용하면 사용자 경험을 향상시키고, UI 요소를 부드럽게 움직이게 하거나, 화면 전환 효과를 적용하는 등 다양한 시각적 기능을 구현할 수 있습니다. <br>예를 들어, 버튼 클릭 시 요소가 확대되거나 이동하는 애니메이션을 만들 수 있습니다.
<br><br><br><br>

## 실습

**Storyboard 정의 및 KeyFrames 설정**<br>
먼저 XAML 또는 코드에서 Storyboard를 정의하고 애니메이션 효과를 설정합니다. <br>예를 들어, 버튼을 클릭했을 때 버튼의 위치를 변경하는 간단한 애니메이션을 생성하려면 다음과 같이 설정할 수 있습니다.

```cs

    <Window.Resources>
        <Storyboard x:Key="MoveButton">
            <ThicknessAnimation Storyboard.TargetName="myButton"
                              Storyboard.TargetProperty="Margin"
                              To="50,50,0,0" Duration="0:0:1" />
        </Storyboard>
    </Window.Resources>

    <Grid>
        <Button x:Name="myButton" Content="Click Me" Width="100" Height="30">
            <Button.Triggers>
                <EventTrigger RoutedEvent="Button.Click">
                    <BeginStoryboard Storyboard="{StaticResource MoveButton}"/>
                </EventTrigger>
            </Button.Triggers>
        </Button>
    </Grid>
</Window>

```


버튼에 클릭 이벤트 트리거를 추가하여 Storyboard를 시작하게 합니다.<br>
 이는 버튼 클릭 시 애니메이션을 시작하도록 만들어 줍니다.<br>애플리케이션을 실행하고 "Click Me" 버튼을 클릭하면 버튼이 클릭한 위치로 이동하는 애니메이션이 재생됩니다.
<br><br>

## 실습응용
![](/assets/img/size.PNG)
<br>
<br>
클릭시 버튼의 길이가 증가하는데 다시 한번 클릭시 제자리로 돌아오게 해봅시다.<br>

WPF에서는 XAML만을 사용하여 버튼의 애니메이션을 제어하는 방법이 가능합니다. <br>이를 위해 다음과 같이 ToggleButton을 사용하여 버튼의 상태를 토글하고 애니메이션을 적용할 수 있습니다.<br> 

```cs

   <Window.Resources>
        <Storyboard x:Key="MoveButton">
            <DoubleAnimation Storyboard.TargetProperty="Width"
             To="400" Duration="0:0:0.5"/>
        </Storyboard>
        <Storyboard x:Key="MoveBackButton">
            <DoubleAnimation Storyboard.TargetProperty="Width"
             To="100" Duration="0:0:0.5"/>
        </Storyboard>
        <Style TargetType="ToggleButton">
            <Style.Triggers>
                <Trigger Property="IsChecked" Value="True">
                    <Trigger.EnterActions>
                        <BeginStoryboard Storyboard="{StaticResource MoveButton}"/>
                    </Trigger.EnterActions>
                    <Trigger.ExitActions>
                        <BeginStoryboard Storyboard="{StaticResource MoveBackButton}"/>
                    </Trigger.ExitActions>
                </Trigger>
            </Style.Triggers>
        </Style>
    </Window.Resources>

    <Grid>
        <ToggleButton Content="Toggle" Width="100" Height="50" HorizontalAlignment="Center" VerticalAlignment="Center"/>
    </Grid>

```
이 코드에서 ToggleButton을 사용하여 클릭할 때 버튼의 상태가 토글되도록 만들었습니다. <br>Style에서 IsChecked 속성 값에 따라 버튼의 Width 설정하여 애니메이션을 달성합니다.<br> 


## ToggleButton

WPF 애플리케이션에서 사용되는 컨트롤 중 하나로, 사용자가 토글 동작을 수행할 수 있는 버튼 형태의 UI 요소입니다. <br>이 컨트롤은 두 가지 상태를 갖고 있으며, 버튼을 클릭하면 상태가 전환됩니다. <br>대표적으로 "On"과 "Off" 상태가 있으며 사용자가 버튼을 클릭하면 "On"에서 "Off"로 또는 그 반대로 상태가 변경됩니다.

ToggleButton은 사용자가 이진 선택을 할 때 유용하며, 대표적인 예로 "체크 박스"와 "라디오 버튼"이 있습니다.<br> 이러한 컨트롤들은 ToggleButton을 기반으로 만들어지며, 상태가 변경될 때 이벤트를 트리거할 수 있습니다.<br>

## ToggleButton 주요 속성
**IsChecked** <br> 
현재 토글 상태를 나타내는 속성입니다. <br> 이 속성을 통해 "On" 또는 "Off" 상태를 확인하고 설정할 수 있습니다.<br><br>
**Content**<br>  버튼 내에 표시할 텍스트나 다른 UI 요소를 설정하는 속성입니다.<br><br>
**Click**<br>  버튼이 클릭될 때 실행할 이벤트 핸들러를 연결하는 이벤트입니다.<br><br>
<br> 
ToggleButton은 사용자 인터페이스에서 특정 작업을 트리거하는 데 매우 유용하며, 사용자가 선택 옵션을 쉽게 변경할 수 있게 해줍니다.
<br><br>


<br><br>

## ThicknessAnimation와 DoubleAnimation
**ThicknessAnimation**<br>
Thickness 유형의 속성에 애니메이션을 적용하는 데 사용됩니다. <br>Thickness는 여러 값을 나타내는데 사용되는 유형으로, 주로 여백 또는 여러 개의 값을 갖는 속성에 적용됩니다.<br> 예를 들어, Margin 속성은 Thickness 형식이므로 ThicknessAnimation을 사용하여 여백을 애니메이션화할 수 있습니다.<br><br>

**DoubleAnimation**<br>
double 유형의 숫자 속성에 애니메이션을 적용하는 데 사용됩니다. <br>이것은 주로 숫자 값이 변경되는 속성, 예를 들면 너비, 높이, 투명도 등과 같은 숫자 값을 가지는 속성에 적용됩니다.
<br>


<br><br>
## 참조 
https://learn.microsoft.com/ko-kr/dotnet/desktop/wpf/graphics-multimedia/storyboards-overview?view=netframeworkdesktop-4.8