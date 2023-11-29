---
title: Reflection
date: 2023-11-08 00:00:01 
tags: 
description:
image: 
published: true
tags : study
---

 프로그램이 실행 중에 자신의 구조와 정보를 검사, 조사, 분석하는 프로세스를 의미합니다. <br>
리플렉션을 통해 코드가 실행 중에 타입(Type) 정보, 어셈블리(Assembly) 정보, 메서드(Method) 정보, 필드(Field) 정보, 속성(Property) 정보 등을 동적으로 검색하고 조작할 수 있습니다.


## 기능 <br>

**타입 정보 얻기**<br>
 리플렉션을 사용하여 어셈블리에서 특정 타입의 정보를 가져올 수 있습니다.<br> 이 정보에는 클래스의 메서드, 필드, 속성 및 인터페이스 등이 포함됩니다.

**인스턴스 생성**<br>
 리플렉션을 사용하여 타입 정보를 기반으로 객체(인스턴스)를 동적으로 생성할 수 있습니다.<br>
  이것은 특히 플러그인 시스템 또는 동적 로딩과 같은 상황에서 유용합니다.

**메서드 호출**<br>
 리플렉션을 통해 객체의 메서드를 호출하고 메서드의 매개변수를 동적으로 전달할 수 있습니다.

**속성 및 필드 조작**<br>
 리플렉션을 사용하여 객체의 속성과 필드 값을 가져오거나 설정할 수 있습니다.

**어셈블리 및 모듈 정보**<br>리플렉션을 통해 어셈블리와 모듈의 정보를 얻을 수 있으며, 이는 다양한 어셈블리 관리 작업에 유용합니다.

리플렉션은 고급 프로그래밍 시나리오, 동적 코드 생성, 플러그인 시스템, 직렬화, 의존성 주입과 같은 기술에서 사용됩니다.
<br> 그러나 리플렉션은 실행 시간에 추가 오버헤드와 보안 문제를 발생시킬 수 있으므로 신중하게 사용해야 합니다.

<br><br>

## 예제

```cs

using System;
using System.Reflection;

public class MyClass
{
    public int MyProperty { get; set; }
    
    public void MyMethod()
    {
        Console.WriteLine("Hello from MyMethod!");
    }
}

class Program
{
    static void Main()
    {
        // 타입 정보 얻기
        Type myType = typeof(MyClass);
        
        // 객체 생성
        object myObject = Activator.CreateInstance(myType);
        
        // 속성 값 설정
        PropertyInfo propertyInfo = myType.GetProperty("MyProperty");
        propertyInfo.SetValue(myObject, 42);
        
        // 메서드 호출
        MethodInfo methodInfo = myType.GetMethod("MyMethod");
        methodInfo.Invoke(myObject, null);
        
        // 속성 값 가져오기
        int propertyValue = (int)propertyInfo.GetValue(myObject);
        Console.WriteLine("MyProperty value: " + propertyValue);
    }
}


```

**MyClass**라는 클래스를 정의하고, **C#**의 **리플렉션**을 사용하여 다음 작업을 수행합니다<br>
**MyClass** 타입 정보를 얻기 위해 **typeof** 연산자를 사용합니다.<br>
**myType**을 기반으로 **MyClass**의 인스턴스를 동적으로 생성합니다.<br>
리플렉션을 통해 **MyProperty** 속성 값을 설정하고, **MyMethod** 메서드를 호출합니다.<br>
마지막으로 **MyProperty** 속성 값을 다시 가져와서 출력합니다.<br>
이러한 동적 작업을 통해 **리플렉션**은 실행 중에 코드를 조사하고 조작하는 데 사용됩니다.<br>

<br><br><br><br>

## 윈도우 런타임 라이브러리


## ColorItem.xaml
```cs

  <Grid>
        <StackPanel Orientation="Horizontal">
            <Rectangle Name="rectangle"
                       Width="72"
                       Height="72"
                       Margin="6"/>

            <StackPanel VerticalAlignment="Center">
                <TextBlock Name="txtblkName"
                           FontSize="24"/>
                <TextBlock Name="txtblkRgb"
                           FontSize="18"/>
            </StackPanel>
        </StackPanel>
    </Grid>

```
네임이 rectangle인 사각형 도형과 
네임이 txtblkName인 텍스트블록과 
네임이 txtblkRgb인 블록을 stackpanel안에 생성한다.

## ColorItem.xaml.cs
```cs

    public partial class ColorItem : UserControl
    {
        public ColorItem(string name, Color clr)
        {
            InitializeComponent();

            rectangle.Fill = new SolidColorBrush(clr);
            txtblkName.Text = name;
            txtblkRgb.Text = string.Format("{0:X2}-{1:X2}-{2:X2}-{3:X2}", clr.A, clr.R, clr.G, clr.B);
        }
    }
```
 사각형(또는 직사각형) 요소의 채우기 속성(Fill)을 설정합니다.<br>
new SolidColorBrush(clr) 이 부분은 브러시를 생성하여 사각형의 Fill 속성에 할당합니다. <br>clr은 미리 정의된 색상을 나타내며, 새로운 SolidColorBrush 객체를 생성하여 이 색상으로 설정합니다.<br> 따라서 rectangle의 내부는 지정된 색상으로 채워집니다.<br>
<br>
코드에서 전달된 매개변수로, 텍스트 블록에 표시할 텍스트 내용을 포함하고 있습니다.<br> 이 코드는 txtblkName의 Text 속성에 name 변수의 값을 할당하여 해당 텍스트 블록에 name 변수의 내용을 표시합니다.<br>
부분은 문자열을 형식화하는 역할을 합니다. {0:X2}는 숫자를 16진수로 표시하고, X2는 2자리 16진수로 표시하라는 의미입니다. 이 부분은 RGBA 값을 16진수 형식으로 변환합니다. clr.A, clr.R, clr.G, clr.B는 각각 알파, 빨강, 녹색 및 파랑 채널의 값을 나타냅니다.

## MainWindow.xaml
```cs

     <Grid>
            <ScrollViewer>
            <StackPanel>
           
                    <StackPanel Name="stackPanel" HorizontalAlignment="Center"></StackPanel>
               
            </StackPanel>
            </ScrollViewer>
        </Grid>

```

네임이 stackPanel 인 StackPanel 생성 






## MainWindow.xaml.cs
```cs
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();


            IEnumerable<PropertyInfo> properties = typeof(Colors).GetTypeInfo().DeclaredProperties;

            foreach(PropertyInfo property in properties)
            {
                Color clr = (Color)property.GetValue(null);
                ColorItem clrItem = new ColorItem(property.Name, clr);
                stackPanel.Children.Add(clrItem);
            }
         
        }
    }
```


 **IEnumerable\<PropertyInfo>** 는 C#에서 사용되는 데이터 형식으로, **PropertyInfo** 객체의 컬렉션을 나타냅니다. <br>
**PropertyInfo**는 **System.Reflection** 네임스페이스에 있는 클래스 입니다.<br>

**IEnumerable\<PropertyInfo>**은 **Colors** 클래스의 속성을 나타내는 **PropertyInfo** 객체의 컬렉션이 됩니다.<br>
 이 컬렉션을 사용하여 **Colors** 클래스의 각 속성에 대한 정보, 이름, 데이터 형식 및 속성과 관련된 정보에 접근할 수 있습니다.<br>
 **IEnumerable\<PropertyInfo>**은 여러 개의 PropertyInfo 객체를 담을 수 있는 컬렉션 형식입니다.<br>
 이 컬렉션은 여러 **PropertyInfo** 객체를 열거할 수 있는 방법을 제공합니다. <br>
  다시 말해, **IEnumerable\<PropertyInfo>**은 여러 속성 정보를 담고 있으며, 코드를 통해 이 컬렉션을 반복하면 **Colors** 클래스의 각 속성에 대한 정보를 순회할 수 있습니다.<br>

 **DeclaredProperties**는 **Type** 클래스의 메서드 중 하나로, 해당 형식이 선언한 속성을 나타내는 **PropertyInfo** 객체의 컬렉션을 반환합니다. <br>
 **Type**클래스는 **.NET**에서 형식에 대한 정보를 제공하는 클래스이며, **PropertyInfo**는 속성에 대한 정보를 제공하는 클래스입니다.<br>
 따라서 **DeclaredProperties** 를 호출하면 형식이 선언한 속성에 대한 정보를 담은** **IEnumerable\<PropertyInfo>**가 반환됩니다. <br>
 이것은 **리플렉션(Reflection)**을 사용하여 런타임에 형식 정보를 동적으로 가져오는 데에 사용됩니다
 <br>

**IEnumerable\<PropertyInfo>**을 사용하여 **Colors** 클래스의 각 속성을 반복하고, 각 속성의 값을 가져와서 **ColorItem** 객체를 생성한 후 **stackPanel**에 추가하는 작업을 수행합니다.<br>


**foreach** 루프를 사용하여 **properties**의 각 **PropertyInfo** 객체를 반복합니다.<br>
**property.GetValue(null)**를 사용하여 현재 속성의 값을 가져옵니다. <br>
**null**을 전달한 이유는 **Colors** 클래스의 속성은 정적 속성(static properties)이므로 인스턴스가 필요하지 않기 때문입니다.<br>
**Color** 값(clr)을 가져온 후, 해당 값과 속성의 이름을 사용하여 **ColorItem** 객체(**clrItem**)를 생성합니다.<br>
**stackPanel.Children.Add(clrItem)**을 사용하여 **stackPanel**에 **ColorItem**을 추가합니다. <br>
이로써 각 속성에 해당하는 **ColorItem**이 **UI**에 추가됩니다.<br>




<br><br><br><br><br>
## 참조 
찰스 페졸드의 Programming Windows