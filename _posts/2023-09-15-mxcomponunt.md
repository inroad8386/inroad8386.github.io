---
title: MX Component - PLC 통신
date: 2023-09-14 09:58:47 
tags: 
description:
image: 
published: true
tags : study
---

## MX component
프로토콜을 의식하지 않고도 PC에서 PLC나 모션 컨트롤러로의 통신을 <br>간단히 처리할 수 있는 Active X® 컨트롤, .NET 컨트롤 라이브러리
<br>
<br>
번거롭고 복잡했던 시리얼 통신이나 Ethernet 통신을 실행하는<br> 애플리케이션의 개발이 MX Component를 사용함으로써 매우 간단해짐
<br>

## GX Works 2 / Gx Works 3 차이
대응 하는 PLC 가 다름<br>
Works2 : QCPU, LCPU, FXCPU 등 이하 CPU <br>
Works3 : 최신 RCPU, FX5CPU, NCCPU 등 <br>

## Word (워드)
워드 데이터는 16개의 bit, 2개의 byte 수치 데이터를 말함<br>
표기 방법은 10진수와 16진수로 할 수 있음<br>
65,536가지 수를 표현할 수 있으며 10진수로 표현 시 0~65,535까지 가능<br>



## 설치 프로그램

1)  Communication Setup utility<br>
2)  GX Works 2 <br>
3)  PLC Monitor Utility<br>

⚠️ 설치 후 실행시 관리자 권한 으로 실행할 것 <br>



## Step1 

1.   Communication Setup Utility 관리자 권한으로 실행<br>
2.   Wizard 클릭<br>
3.   Logical Station number 0 입력<br>
4.   Comment 이름설정<br>

## Step2
1.  GX Works 2 관리자 권한으로 실행<br>
2.  Ladder 작성 후 시뮬레이션 실행<br><br>
![test](https://github.com/inroad8386/inroad8386.github.io/blob/main/assets/img/PLC.PNG?raw=true)
<br><br> New Project 설정 후 다음과 같은 그림의 래더를 작성 후 Debug - Stat/Stop 클릭 <br>

 \*설정<br>
Project Type : Simple Project<br>
PLC Series : QCPU (Q mode)<br>
PLC Type : Q02/Q02H<br>
Language : Ladder<br>

 \*단축키<br>
Shift + Insert : 줄 추가<br>
Shift + Delete : 줄 삭제<br>
접점 단축키 : F5<br>

 \*작성법<br>
Shift +insert 로 줄 추가<br>
F5 누르고 접점에 M0 입력<br>
F7 누르고 RND D0 입력<br>
F4 눌러서 출력<br>

## Step 3
1. PLC Monitor Utility 관리자 권한으로 실행
2. Device D0 입력 후 Start monitor 클릭

## Step 4
1. Visual Studio 실행
2. 다음의 코드 실행

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using ActUtlType64Lib;

namespace PlcRemote
{
    /// <summary>
    /// MainWindow.xaml에 대한 상호 작용 논리
    /// </summary>
    public partial class MainWindow : Window
    {
        bool bPlcConnection = false;
        System.Timers.Timer _Timer;
        ActUtlTypeLib.ActUtlType _ActUtlType;


        public MainWindow()
        {
            InitializeComponent();
        }


        //Timer 간격이 경과되면 발생될 내용
        void _Timer_Elapsed(object sender, System.Timers.ElapsedEventArgs e)
        {
            if (bPlcConnection.Equals(true))
            {
                String szDevice = "D0"; //읽어올 PLC Device
                int lSize = 1; //읽어올 PLC Device의 Word 수
                int[] lplData = new int[lSize]; //읽어온 PLC Device Word 값을 저장할 변수


                //_ActUtlType.ReadDeviceBlock 함수의 리턴 값
                int nResult = _ActUtlType.ReadDeviceBlock(szDevice, lSize, out lplData[0]);
                if (nResult.Equals(0)) //정상적으로 리턴받으면 0을 받는다.
                {
                    this.Dispatcher.Invoke(new D_Set_Value(_Set_Value), lplData[0]);
                }
            }
        }


        // PLC로 부터 읽은 데이터를 입력하기 위한 대리자
        private delegate void D_Set_Value(int nValue);
        private void _Set_Value(int nValue)
        {
            vConnectedText.Text = String.Format("Connected : {0}", nValue);
        }

        //PLC 연결 버튼
        private void Button_Click_2(object sender, RoutedEventArgs e)
        {
            _Timer = new System.Timers.Timer();
            _Timer.Interval = 100;
            _Timer.Elapsed += _Timer_Elapsed;
            _ActUtlType = new ActUtlTypeLib.ActUtlType();


            //Logical Station number를 입력할 TextBox가 String.Empty이거나, Null이 아니면 진행되도록.
            if (String.IsNullOrEmpty(vPortNumber.Text).Equals(false))
            {
                _ActUtlType.ActLogicalStationNumber = Convert.ToInt32(vPortNumber.Text);
                if (_ActUtlType.Open().Equals(0))
                {
                    bPlcConnection = true;


                    //PLC의 M0를 접점시키는 코드
                    if (_ActUtlType.WriteDeviceBlock("M0", 1, 1).Equals(0))
                    {
                        _Timer.Start();
                    }
                }
            }
        }
        //PLC 연결 해제 버튼
        private void Button_Click_3(object sender, RoutedEventArgs e)
        {
            if (bPlcConnection.Equals(true))
            {
                //PLC의 M0를 접점을 해제시키는 코드
                if (_ActUtlType.WriteDeviceBlock("M0", 1, 0).Equals(0))
                {
                    _Timer.Stop();
                    _Timer.Dispose();
                    _ActUtlType.Close();
                }
            }
        }
    }
}

```
<br><br>
<br>
![test](https://github.com/inroad8386/inroad8386.github.io/blob/main/assets/img/good3.PNG?raw=true)<br>
<br>
데이터 값이 계속 변화하는지 확인하기
<br><br><br><br><br>

[참조]<br>
https://orangetazo.tistory.com/19 <br>
https://mech19.tistory.com/45 <br>
