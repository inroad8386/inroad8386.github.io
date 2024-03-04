---
title: Event & Delegate
date: 2024-02-28 00:10:01 
tags: 
description:
image: 
published: true
tags : study
---

# Event & Delegate example
저번에 만든 layout에 간단한 기능을 추가하여 이벤트 델리게이트를 연습해본다.


![](/assets/img/20240229/event1.gif)<br>

홈버튼의 기능은 클릭했을 때 mainpage가 나오는 기능이다.<br>
왼쪽 상단은 글자 Home의 기능과 오른쪽의 Home아이콘의 기능을 이벤트 델리게이트를 통해 같은 기능을 하는 간단한 예제를 만들려고 한다.<br>
<br>

## Home 버튼을 눌렀을 때
```cs
        private void MainHome_Click(object sender, RoutedEventArgs e)
        {
            Button button = sender as Button;
            if (button != null)
            {
                string pageName = button.Tag as string;
                if (!string.IsNullOrEmpty(pageName))
                {
                    // 해당 페이지로 Frame을 설정하여 로드
                    switch (pageName)
                    {
                        case "0":
                            frame_change.Content = new MainPage();
                            break;
                        case "1-1":
                            frame_change.Content = new Page1_1();
                            break;
                        case "1-2":
                            frame_change.Content = new Page1_2();
                            break;
                        case "1-3":
                            frame_change.Content = new Page1_3();
                            break;
                        // 다른 페이지도 필요하면 여기에 추가
                        default:
                            // 처리할 페이지가 없는 경우에 대한 예외 처리
                            break;
                    }
                }
            }
        }
```

이 메서드는 WPF 버튼 클릭 이벤트 핸들러입니다. <br>
버튼이 클릭되면 실행되며, 클릭된 버튼의 Tag 속성을 확인하여 해당 페이지를 로드합니다.<br>
클릭된 버튼의 Tag 속성에는 페이지를 식별하는 문자열이 들어있으며, 이를 기반으로 해당하는 페이지를 로드합니다.<br>
예를 들어, 버튼의 Tag 속성이 "0"이면 MainPage를 로드하고, "1-1"이면 Page1_1을 로드합니다.<br>

<br><br>

# 이벤트와 델리게이트

```cs
      // 이벤트를 발생 시키기 위한 이벤트 핸들러 델리게이트 선언
        public delegate void clickevent(object sender, RoutedEventArgs e);
        // 이벤트 선언 ( 값을 전달 하는 쪽 )
        public static event clickevent ClickEvent;
        private void HomeIcon_Click(object sender, RoutedEventArgs e)
        {
            ClickEvent += MainHome_Click;
            ClickEvent?.Invoke(sender, e);
        }
```

**clickevent 델리게이트**<br>
이 델리게이트는 WPF 버튼 클릭 이벤트를 처리하는데 사용됩니다. 버튼 클릭 이벤트가 발생하면 해당 델리게이트가 호출되며, 이벤트 처리를 담당하는 메서드에게 이벤트를 전달합니다.<br>
이 델리게이트는 두 개의 매개변수를 갖습니다. <br>
첫 번째 매개변수는 이벤트를 발생시킨 객체(sender)이고, 두 번째 매개변수는 이벤트에 대한 추가 정보(RoutedEventArgs e)입니다.<br>

**ClickEvent 이벤트**<br>
이벤트를 발생시키기 위한 이벤트 핸들러입니다. <br>
버튼 클릭 이벤트를 처리하는 메서드가 호출될 때 이벤트를 발생시킵니다.<br>
다른 클래스나 메서드에서 이 이벤트를 구독하고, 버튼이 클릭되었을 때 동일한 동작을 실행할 수 있도록 합니다<br>

**HomeIcon_Click 메서드**<br>
이 메서드는 홈아이콘 버튼의 클릭 이벤트 핸들러입니다. <br>
이 메서드에서는 첫 번째 버튼의 클릭 이벤트를 구독하고 해당 이벤트를 발생시킵니다.<br>
따라서 홈아이콘 버튼이 클릭되면 MainHome_Click 메서드가 호출되어 동일한 기능을 수행합니다.<br>

이러한 방식으로 두 개의 버튼이 동일한 기능을 수행할 수 있도록 구현되어 있습니다.<br>
<br><br>

## 개선할 점

**EventHandler의 사용**
```cs
        // 델리게이트를 지우고 이벤트 핸들러만 작성
        public event RoutedEventHandler ClickEvent;
        private void HomeIcon_Click(object sender, RoutedEventArgs e)
        {
            ClickEvent += MainHome_Click;
            ClickEvent?.Invoke(sender, e);
        }
```
clickevent 델리게이트는 이미 .NET 프레임워크에서 제공하는 EventHandler 대리자와 유사한 역할을 하고 있습니다. <br>
따라서 별도의 델리게이트를 선언하지 않고 기존의 EventHandler를 사용하는 것이 더 좋을 수 있습니다.<br>


**이벤트 구독 해제**
```cs
        private void HomeIcon_Click(object sender, RoutedEventArgs e)
        {
            ClickEvent += MainHome_Click;
            ClickEvent?.Invoke(sender, e);

            //사용후 해제
            ClickEvent -= MainHome_Click;
        }

```
HomeIcon_Click 메서드에서 이벤트를 구독한 후 해제하지 않고 있습니다. <br>이는 이벤트 핸들러가 메모리 누수를 발생시킬 수 있으므로, 이벤트를 구독한 후 해당 이벤트를 해제하는 것이 좋습니다.<br>


<br><br><br><br>


## EventHandler 와 RoutedEventHandler

**RoutedEventHandler와** **EventHandler는** .NET Framework의 이벤트 처리를 위한 델리게이터

### 사용하는 프레임워크
**RoutedEventHandler**<br>
 WPF(Windows Presentation Foundation)와 같은 XAML 기반의 프레임워크에서 사용됩니다. <br>
 이벤트 라우팅 기능과 관련된 이벤트 처리에 사용됩니다.
**EventHandler**<br>
 일반적으로 .NET Framework의 다양한 클래스 및 라이브러리에서 사용됩니다. <br>Windows Forms, ASP.NET, WCF 등 다양한 프레임워크에서 이벤트 처리에 사용됩니다.<br>


### 시그니처
**RoutedEventHandler**<br>
 object sender, RoutedEventArgs e와 같은 시그니처를 갖습니다. <br>이것은 WPF에서 이벤트 처리 메서드의 표준적인 형태입니다.<br> sender 매개변수는 이벤트를 발생시킨 요소를 가리키고, RoutedEventArgs는 이벤트에 대한 추가 정보를 제공합니다.<br>
**EventHandler** <br>object sender, EventArgs e와 같은 시그니처를 갖습니다. EventArgs 클래스는 .NET Framework의 대부분의 이벤트에서 사용되는 일반적인 이벤트 인자 클래스입니다.


### 적용 범위
**RoutedEventHandler**<br>
 WPF에서 주로 사용됩니다. <br>WPF의 이벤트 라우팅 메커니즘과 함께 사용하여 이벤트를 라우팅하는 데 유용합니다.<br>
**EventHandler**<br>
일반적인 .NET Framework 어플리케이션에서 사용됩니다. <br>다양한 클래스 및 라이브러리에서 일반적인 이벤트 처리에 사용됩니다.<br>
따라서 프로젝트의 특정 요구 사항에 따라 적절한 델리게이트를 선택해야 합니다. <br><br>WPF 애플리케이션에서는 주로 **RoutedEventHandler를** 사용하고<br> 다른 .NET Framework 프로젝트에서는 **EventHandler를** 사용하는 것이 일반적입니다.