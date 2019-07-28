# Welcome to Kaopiz Library!
This Markdown is the guidance for using  Z-Order library. 

# Table of Contents
 * [Requirement](#Requirement)
 * [Provided functions](#Provided-functions)
	* [Open application by path ](#Open-application-by-path )
	 * [Open application by name](#Open-application-by-name)
	 * [Bring current process to front](#Bring-current-process-to-front)
	 * [Bring a process to front by name app](#Bring-a-process-to-front-by-name-app)
 * [An Example](#An-Example)
# Requirement
- Target Framework: .NET Framework 4.6.1
- Language: CSharp


## Open application by path 
parameter is location path, such as `C:\Program Files\abc.exe`
```csharp
public static bool OpenApplicationByPath(string filePath)
```

## Open application by name
```csharp
public static bool OpenApplication(string nameApp)
```

## Bring current process to front
```csharp
public static void BringCurrentProcToFront()
```

## Bring a process to front by app's name
```csharp
public static void BringWindowToFront(string your_window_title)
```

## An Example
```csharp
using System;
using System.Threading;
using System.Windows.Forms;
using Kaopiz;

namespace KaopizExample
{
    public class BenderExample
    {
        private OpenFileDialog browser = new OpenFileDialog();
		
		//Diaglog open file browser only in Winform application
        public string OpenDiaglog()
        {
            browser.InitialDirectory = "c:\\";
            browser.Filter = "exe files (*.exe)|*.exe|All files (*.*)|*.*";
            browser.FilterIndex = 0;
            browser.RestoreDirectory = true;
            if (browser.ShowDialog() == DialogResult.OK)
            {
                return browser.FileName;
            }
            return null;
        }

        public void StartApp(string textBox, int timeDelay)
        {
            if (textBox == null || textBox == "")
            {
                MessageBox.Show("Please fill the path!");
            }
            try
            {
                ZOrder.OpenApplicationByPath(textBox);
            }
            catch (Exception)
            {
                MessageBox.Show("Can not open App!");
            }
            if (timeDelay == 0)
            {
                return;
            }
        }
		
		//Bring current app to front
        public Thread BringAppToFront(int time)
        {
            var t = new Thread(() => SetDelayTime(time));
            t.Start();
            return t;
        }

        private void SetDelayTime(int time)
        {
            Thread.Sleep(time * 1000);
            ZOrder.BringCurrentProcToFront();
        }
    }   
}
```
