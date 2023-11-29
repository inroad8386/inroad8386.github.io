---
title: DispatcherTimer
date: 2023-11-20 00:00:01 
tags: 
description:
image: 
published: true
tags : study
---

## DispatcherTimer
DispatcherTimer는 WPF에서 UI 갱신과 관련된 작업을 수행하는 데 사용되는 타이머입니다.<br> 이 타이머는 특히 UI 업데이트 작업이 필요한 경우에 유용합니다. <br> DispatcherTimer는 UI 스레드에서 실행되며 일반적으로 일정한 간격으로 반복 작업을 수행하거나 특정 시간에 한 번 작업을 수행하는 데 사용됩니다.<br> <br> 


xaml
```cs
        <TextBlock Name="txtblk" 
                   FontFamily="Lucida Console" 
                   FontSize="20"                                    
                   HorizontalAlignment="Center"
                   VerticalAlignment="Center">
        </TextBlock>


```


cs
```cs
        public timer()
        {

            InitializeComponent();
            // DispatcherTimer 인스턴스 생성
            DispatcherTimer timer = new DispatcherTimer();
            timer.Interval = TimeSpan.FromSeconds(1);// 1초마다
            timer.Tick += OnTimerTick;
            // 타이머 시작
            timer.Start();
        }

        private void OnTimerTick(object sender, EventArgs e)
        {
            // 타이머가 간격마다 호출되는 이벤트 핸들러
            // UI 갱신 또는 다른 작업 수행
            txtblk.Text = DateTime.Now.ToString("h:mm:ss tt");
        }

```


<p align="center">
 <img src="/assets/img/20231121.PNG">
</p>



## Dispatcher
Dispatcher는 WPF에서 다른 스레드에서 UI 업데이트를 수행하기 위한 메커니즘을 제공합니다.<br> 
UI 업데이트는 주로 UI 스레드에서 수행되어야 하며, Dispatcher를 사용하여 다른 스레드에서 UI를 업데이트할 때 UI 스레드로 작업을 전달할 수 있습니다.<br> 


## DispatcherTimer
DispatcherTimer는 System.Windows.Threading 네임스페이스에 속한 클래스입니다.<br> 
DispatcherTimer 인스턴스를 생성하고, 간격 (Interval) 및 타이머 이벤트 핸들러를 설정합니다.


## 간격 설정
Interval 속성을 사용하여 타이머 간격을 설정합니다. <br> 
이 간격은 타이머 이벤트 핸들러가 호출되는 주기를 나타냅니다.<br> 

<br> 

## 타이머 이벤트 핸들러 등록
Tick 이벤트 핸들러를 등록하여 타이머가 간격마다 호출될 때 실행될 작업을 정의합니다.
<br> 

## 타이머 시작 및 중지:
Start() 메서드를 호출하여 타이머를 시작하고, Stop() 메서드를 호출하여 타이머를 중지할 수 있습니다.
<br> 

## 주의사항
타이머 이벤트 핸들러 내에서 UI 업데이트를 수행할 때는 Dispatcher.Invoke 또는 Dispatcher.BeginInvoke를 사용하여 UI 스레드로 작업을 전달해야 합니다.


<br><br><br><br><br>
## 참조 
찰스 페졸드의 Programming Windows