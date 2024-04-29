---
title: LogViewer
date: 2024-04-29 00:58:47 
tags: 
description:
image: 
published: true
tags : study
---


# LogViewer 만들기

## 소개 및 목적
로그뷰어 프로그램은 로그 파일을 효과적/효율적으로 분석하기 위한 용도로 개발<br>
사용자가 로그 파일을 읽고 필터링하여 중요한 정보를 추출하고 날짜 사이의 데이터를 추출할 수 있도록 돕는 것이 목표


## 기능 설명
로그파일을 불러와 목록을 나타내고 로그 데이터를 보여주는 기능
사용자 지정 조건에 따라 로그 파일을 검색하고 필터링하는 기능


## 기술적 구현
C# Visual Studio의 WPF를 사용
<br><br><br><br>




## 기능별 코드 해석
### 폴더안의 로그파일목록 불러오기
![](/assets/img/20240429/folder.PNG)<br>
```cs
private void LoadLogFile(object sender, MouseButtonEventArgs e)
{

    FolderBrowserDialog folderBrowserDialog = new FolderBrowserDialog();

    if (folderBrowserDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)
    {
        folderPath = folderBrowserDialog.SelectedPath;

        // 폴더 내의 파일 목록 가져오기
        string[] files = Directory.GetFiles(folderPath);

        // 파일 목록을 ListBox에 출력
        LogFileListBox.Items.Clear(); // 기존 목록 지우기
        LogFileBox.Items.Clear(); // 기존 로그 제거
        foreach (string file in files)
        {
            LogFileListBox.Items.Add(Path.GetFileName(file));
        }
    }
    FolderName.Text = "Seleted Folder : " + Path.GetFileName(folderPath);
}
 ```

FolderBrowserDialog를 사용하여 폴더 선택 대화 상자를 생성<br>
폴더를 선택하고 확인을 클릭하면 선택된 폴더 경로를 folderPath 변수에 저장<br>
선택된 폴더 내의 파일 목록을 가져와서 files 배열에 저장<br>
LogFileListBox의 항목을 모두 지우고, 선택된 폴더 내의 파일 목록을 LogFileListBox에 추가<br>
선택된 폴더의 이름을 텍스트로 표시하는 FolderName 텍스트 블록에 업데이트<br>


<br><br><br><br>




### 불러온 로그파일목록 클릭시 로그데이터 불러오기
![](/assets/img/20240429/log.PNG)<br>
```cs
        /// <summary>
        /// 리스트박스의 log파일 item선택시 로그데이터를 불러옴
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void LogListSelected(object sender, SelectionChangedEventArgs e)
        {
            string selectedFileName = (string)LogFileListBox.SelectedItem; // 선택된 파일명 가져오기
            if (selectedFileName != null && folderPath != null)
            {
                string selectedFilePath = Path.Combine(folderPath, selectedFileName); // 선택된 파일의 전체 경로 생성
                                                                                     // 선택된 파일의 내용을 읽어와서 로그를 표시
                string[] lines = File.ReadAllLines(selectedFilePath); // 파일의 모든 라인을 읽어옴
                LogFileBox.Items.Clear(); // 기존 로그 지우기
                foreach (string line in lines)
                {
                    LogFileBox.Items.Add(line); // 로그 내용을 ListBox에 추가
                }
            }
        }

```
LogFileListBox에서 선택된 파일명을 가져옵니다.<br>
선택된 파일명과 folderPath 변수를 결합하여 선택된 파일의 전체 경로를 생성합니다.<br>
선택된 파일의 내용을 읽어와서 각 줄을 문자열 배열인 lines에 저장합니다.<br>
LogFileBox의 내용을 모두 지운 후, lines 배열에 있는 각 줄을 LogFileBox에 추가하여 로그를 표시합니다.<br>


<br><br><br><br>



### 해당 날짜 사이의 기간에만 생성된 로그만 추출하기
![](/assets/img/20240429/date.PNG)<br>
```cs

private void SearchDateLog(object sender, RoutedEventArgs e)
{
    DateTime startDate = startDatePicker.SelectedDate ?? DateTime.MinValue;
    DateTime endDate = endDatePicker.SelectedDate ?? DateTime.MaxValue;

    // 폴더 내의 파일 목록 가져오기
    if (folderPath != null)
    {
        string[] files = Directory.GetFiles(folderPath);

        // ListBox 초기화
        LogFileListBox.Items.Clear();
        LogFileBox.Items.Clear();

        // 파일을 순회하면서 날짜 형식으로 시작하는 파일을 찾고 ListBox에 추가
        foreach (string file in files)
        {
            string fileName = Path.GetFileName(file);
            // 파일 이름이 "yyyyMMdd" 형식으로 시작하는지 확인
            if (fileName.Length >= 8 && fileName.Substring(0, 8).All(char.IsDigit))
            {
                DateTime fileDate;

                // 파일 이름에서 날짜를 추출하여 DateTime으로 변환
                if (DateTime.TryParseExact(fileName.Substring(0, 8), "yyyyMMdd", CultureInfo.InvariantCulture, DateTimeStyles.None, out fileDate))
                {
                    // 시작 날짜와 끝 날짜 사이의 파일만 ListBox에 추가
                    if (fileDate >= startDate && fileDate <= endDate)
                    {
                        LogFileListBox.Items.Add(fileName);
                    }
                }
            }
        }
    }
}

```

SearchDateLog 메서드는 날짜를 기준으로 로그 파일을 검색하는 역할을 합니다.<br> 시작 날짜와 끝 날짜 사이의 파일만 ListBox에 추가합니다.<br>

시작 날짜와 끝 날짜를 설정하며, 선택된 날짜가 없을 경우 기본값으로 최솟값 또는 최댓값을 설정합니다.<br>
선택된 폴더 내의 파일 목록을 가져와서 files 배열에 저장합니다.<br>
ListBox(LogFileListBox)와 로그 표시 창(LogFileBox)의 내용을 모두 지웁니다.<br>
파일을 순회하면서 파일 이름이 "yyyyMMdd" 형식으로 시작하는지 확인하고, 해당 형식에 맞는 파일명만 ListBox에 추가합니다.<br>
<br><br><br><br>


### 로그안에 적힌 단어 검색하기
![](/assets/img/20240429/search.PNG)<br>
```cs
private void LogWordSearch(object sender, RoutedEventArgs e)
{
    string searchText = LogWord_Textbox.Text; //찾을 wordbox의 text

    if (!string.IsNullOrEmpty(searchText))
    {
        string selectedFileName = (string)LogFileListBox.SelectedItem; // 선택된 파일명 가져오기
        if (selectedFileName != null && folderPath != null)
        {
            string selectedFilePath = Path.Combine(folderPath, selectedFileName); // 선택된 파일의 전체 경로 생성
                                                                                      // 선택된 파일의 내용을 읽어와서 로그를 표시
            string[] lines = File.ReadAllLines(selectedFilePath); // 파일의 모든 라인을 읽어옴
            LogFileBox.Items.Clear(); // 기존 로그 지우기
            foreach (string line in lines)
            {
                if (line.Contains(searchText)) // textbox에 입력된 word를 포함하는 파일의 라인을 찾기
                {
                    LogFileBox.Items.Add(line); // 로그 내용을 ListBox에 추가
                }
            }
        }
    }
}
```
LogWordSearch 메서드는 특정 단어를 검색하여 해당 단어가 포함된 로그를 표시하는 역할을 합니다.<br>

LogWord_Textbox에서 사용자가 입력한 텍스트를 가져와서 searchText 변수에 저장합니다.<br>
만약 searchText가 비어 있지 않다면 실행됩니다.<br>
LogFileListBox에서 선택된 파일명을 가져옵니다.<br>
선택된 파일명과 folderPath 변수를 결합하여 선택된 파일의 전체 경로를 생성합니다.<br>
선택된 파일의 내용을 읽어와서 각 줄을 문자열 배열인 lines에 저장합니다.<br>
lines 배열을 순회하면서 각 줄이 searchText를 포함하는지 확인하고, 포함하는 경우 해당 줄을 LogFileBox에 추가하여 로그를 표시합니다.<br>
<br><br><br>


**로그를 텍스트 파일로 저장하기**<br>
![](/assets/img/20240429/save.PNG)<br>
```cs
private void SaveLogFile(object sender, MouseButtonEventArgs e)
{
    SaveFileDialog saveFileDialog = new SaveFileDialog();
    saveFileDialog.Filter = "Text Files (*.txt)|*.txt";
    if (saveFileDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)
    {
        string filePath = saveFileDialog.FileName;

        // 파일에 아이템들을 저장
        using (StreamWriter writer = new StreamWriter(filePath))
        {
            foreach (var item in LogFileBox.Items)
            {
                writer.WriteLine(item.ToString());
            }
        }
        System.Windows.MessageBox.Show("파일이 저장되었습니다.");
    }
}
```

SaveFileDialog를 생성하여 파일 저장 대화 상자를 표시합니다. <br>
사용자는 텍스트 파일로 저장할 수 있도록 필터를 설정합니다.<br>
사용자가 확인을 클릭하여 파일 저장 대화 상자를 닫으면 실행됩니다.<br>
사용자가 선택한 파일의 경로를 가져와서 filePath 변수에 저장합니다.<br>
LogFileBox에 있는 각 항목을 텍스트 파일에 저장합니다.<br> StreamWriter를 사용하여 파일에 텍스트를 씁니다.<br>
파일 저장이 완료되면 사용자에게 메시지를 표시합니다.<br>

<br><br><br>


<br>


## 전체코드
![](/assets/img/20240429/main.PNG)<br>
```cs
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Forms;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using Path = System.IO.Path;

namespace LogViewer
{
    /// <summary>
    /// MainWindow.xaml에 대한 상호 작용 논리
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

       public string folderPath; // 선택된 폴더 경로를 저장할 변수
       public string selectedFilePath; // 선택된 파일 경로를 저장할 변수
       

        /// <summary>
        /// 로그파일 불러오기
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void LoadLogFile(object sender, MouseButtonEventArgs e)
        {

            FolderBrowserDialog folderBrowserDialog = new FolderBrowserDialog();

            if (folderBrowserDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)
            {
                folderPath = folderBrowserDialog.SelectedPath;

                // 폴더 내의 파일 목록 가져오기
                string[] files = Directory.GetFiles(folderPath);

                // 파일 목록을 ListBox에 출력
                LogFileListBox.Items.Clear(); // 기존 목록 지우기
                LogFileBox.Items.Clear(); // 기존 로그 제거
                foreach (string file in files)
                {
                    LogFileListBox.Items.Add(Path.GetFileName(file));
                }
            }
            FolderName.Text = "Seleted Folder : " + Path.GetFileName(folderPath);

            // 바로 로그만 찾는거
            //Microsoft.Win32.OpenFileDialog openFileDialog = new Microsoft.Win32.OpenFileDialog();
            //openFileDialog.Filter = "All Files|*.*";


            //if (openFileDialog.ShowDialog() == true)
            //{
            //    // 선택된 파일 경로 가져오기
            //    string filePath = openFileDialog.FileName;

            //    // 파일 내용을 읽어와서 ListBox에 추가
            //    string[] lines = File.ReadAllLines(filePath);
            //    LogFileBox.Items.Clear(); // 기존 로그 제거
            //    foreach (string line in lines)
            //    {
            //        LogFileBox.Items.Add(line);
            //    }
            //}
        }

        /// <summary>
        /// 리스트박스의 log파일 item선택시 로그데이터를 불러옴
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void LogListSelected(object sender, SelectionChangedEventArgs e)
        {
            string selectedFileName = (string)LogFileListBox.SelectedItem; // 선택된 파일명 가져오기
            if (selectedFileName != null && folderPath != null)
            {
                string selectedFilePath = Path.Combine(folderPath, selectedFileName); // 선택된 파일의 전체 경로 생성
                                                                                     // 선택된 파일의 내용을 읽어와서 로그를 표시
                string[] lines = File.ReadAllLines(selectedFilePath); // 파일의 모든 라인을 읽어옴
                LogFileBox.Items.Clear(); // 기존 로그 지우기
                foreach (string line in lines)
                {
                    LogFileBox.Items.Add(line); // 로그 내용을 ListBox에 추가
                }
            }
        }

        private void SearchDateLog(object sender, RoutedEventArgs e)
        {
            DateTime startDate = startDatePicker.SelectedDate ?? DateTime.MinValue;
            DateTime endDate = endDatePicker.SelectedDate ?? DateTime.MaxValue;

            // 폴더 내의 파일 목록 가져오기
            if (folderPath != null)
            {
                string[] files = Directory.GetFiles(folderPath);

                // ListBox 초기화
                LogFileListBox.Items.Clear();
                LogFileBox.Items.Clear();

                // 파일을 순회하면서 날짜 형식으로 시작하는 파일을 찾고 ListBox에 추가
                foreach (string file in files)
                {
                    string fileName = Path.GetFileName(file);
                    // 파일 이름이 "yyyyMMdd" 형식으로 시작하는지 확인
                    if (fileName.Length >= 8 && fileName.Substring(0, 8).All(char.IsDigit))
                    {
                        DateTime fileDate;

                        // 파일 이름에서 날짜를 추출하여 DateTime으로 변환
                        if (DateTime.TryParseExact(fileName.Substring(0, 8), "yyyyMMdd", CultureInfo.InvariantCulture, DateTimeStyles.None, out fileDate))
                        {
                            // 시작 날짜와 끝 날짜 사이의 파일만 ListBox에 추가
                            if (fileDate >= startDate && fileDate <= endDate)
                            {
                                LogFileListBox.Items.Add(fileName);
                            }
                        }
                    }
                }
            }
        }
        private void LogWordSearch(object sender, RoutedEventArgs e)
        {
            string searchText = LogWord_Textbox.Text; //찾을 wordbox의 text

            if (!string.IsNullOrEmpty(searchText))
            {
                string selectedFileName = (string)LogFileListBox.SelectedItem; // 선택된 파일명 가져오기
                if (selectedFileName != null && folderPath != null)
                {
                    string selectedFilePath = Path.Combine(folderPath, selectedFileName); // 선택된 파일의 전체 경로 생성
                                                                                          // 선택된 파일의 내용을 읽어와서 로그를 표시
                    string[] lines = File.ReadAllLines(selectedFilePath); // 파일의 모든 라인을 읽어옴
                    LogFileBox.Items.Clear(); // 기존 로그 지우기
                    foreach (string line in lines)
                    {
                        if (line.Contains(searchText)) // textbox에 입력된 word를 포함하는 파일의 라인을 찾기
                        {
                            LogFileBox.Items.Add(line); // 로그 내용을 ListBox에 추가
                        }
                    }
                }
            }
        }

        private void SaveLogFile(object sender, MouseButtonEventArgs e)
        {
            SaveFileDialog saveFileDialog = new SaveFileDialog();
            saveFileDialog.Filter = "Text Files (*.txt)|*.txt";
            if (saveFileDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)
            {
                string filePath = saveFileDialog.FileName;

                // 파일에 아이템들을 저장
                using (StreamWriter writer = new StreamWriter(filePath))
                {
                    foreach (var item in LogFileBox.Items)
                    {
                        writer.WriteLine(item.ToString());
                    }
                }
                System.Windows.MessageBox.Show("파일이 저장되었습니다.");
            }
        }
    }
}

```