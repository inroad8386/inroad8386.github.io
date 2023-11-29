---
title: Inheritance
date: 2023-11-29 00:00:01 
tags: 
description:
image: 
published: true
tags : study
---

## Inheritance

**기본 개념** <br>
상속은 부모 클래스(기본 클래스)와 자식 클래스(파생 클래스) 간의 관계를 말합니다.<br>
부모 클래스는 자신의 특성(멤버 변수 및 메서드)을 하나 이상의 자식 클래스에게 물려줍니다.<br>
<br>

**재사용성**<br>
부모 클래스에 정의된 멤버(변수, 메서드)들을 자식 클래스에서 다시 작성하지 않고도 사용할 수 있습니다.<br>
코드 중복을 피하며 유지보수성을 향상시킵니다.<br>
<br>

**폴리모피즘(Polymorphism)**<br>
상속은 다형성의 기반이 됩니다. 자식 클래스는 부모 클래스의 메서드를 오버라이딩(재정의)하거나, 새로운 메서드를 추가할 수 있습니다.<br>
다형성을 통해 동일한 인터페이스를 사용하면서 다양한 구현을 할 수 있습니다.<br>
<br>

**계층 구조**<br>
클래스 간의 계층 구조를 형성하여 객체들을 논리적으로 구성할 수 있습니다. <br>예를 들어, "동물"이라는 부모 클래스에서 "포유류"와 "조류"라는 자식 클래스를 파생시킬 수 있습니다.<br><br>


**접근 제어 및 보안**<br>
상속을 통해 부모 클래스에서 선언된 멤버를 자식 클래스에서 활용할 수 있습니다.<br>
 그러나 부모 클래스에서 private으로 선언된 멤버는 자식 클래스에서 직접 접근할 수 없습니다.<br>

 <br><br>



## 예제

**Computer.cs**
```cs

    public class Computer
    {
        protected bool powerOn;
        public void Boot() { }
        public void Shutdown() { }
        public void Reset() { }
    }

```
외부에 접근을 차단하면서 자식에게는 허용하는 접근제한자 protected 사용

<br><br>

**Program.cs**
```cs

    public class Notebook : Computer
    {
        bool fingerScan;
        public bool HasFingerScanDevice() { return fingerScan; }


        public void CloseLid()
        {
            if(powerOn == true)// protected
            Shutdown(); // 부모 메서드 호출
        }

    }
    class Program
    {
        static void Main(string[] args)
        {
            Notebook notebook = new Notebook();
            notebook.Boot(); 
            // Notebook 인스턴스에 대해 부모의 메서드 호출
        }
    }


```

위의 컴퓨터 클래스에서 protected bool powerOn 을 사용하였기 때문에 Program.cs에서도 사용이 가능합니다




C# 의 상속에 대해서는 단일 상속만 지원합니다
단일 상속은 한 클래스가 하나의 직접적인 부모 클래스만 상속할 수 있음을 의미합니다. 

C#은 계층 상속은 가능하지만 동시에 둘 이상의 부모 클래스로 부터 다중 상속을 받는 것은 허용하지 않습니다.

<br><br><br><br><br>
## 참조 
C# 9.0 Programming