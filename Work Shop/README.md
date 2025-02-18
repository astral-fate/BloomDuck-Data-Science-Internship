# Web Scraping with Selenium Setup Guide

This repository contains a web scraping project using Selenium WebDriver with Python. Follow this guide to set up your environment and get started.

## Prerequisites

Before you begin, ensure you have the following installed:
- Python 3.x (preferably Python 3.8 or higher)
- Google Chrome browser
- Git (for cloning the repository)

## Installation Steps

1. **Clone the Repository**
   ```bash
   git clone <your-repository-url>
   cd <repository-name>
   ```


2. **Install Required Packages**
   ```bash
   pip install selenium
   pip install webdriver-manager
   ```

4. **Environment Setup**

   ### Windows Setup
   1. Add Chrome WebDriver to System PATH:
      - Open System Properties (Win + Pause/Break)
      - Click on "Advanced system settings"
      - Click on "Environment Variables"
      - Under "System Variables", find and select "Path"
      - Click "Edit"
      - Click "New"
      - Add the following paths:
        ```
        C:\Program Files\NVIDIA Corporation\NVIDIA NvDLISR
        C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common
        C:\Program Files (x86)\chromedriver-win64\chromedriver.exe
        C:\Users\[YourUsername]\AppData\Local\Programs\Python\Python3x\
        ```
      - Click "OK" to save

   2. Verify Chrome WebDriver Installation:
      ```bash
      where chromedriver
      ```

   ### MacOS/Linux Setup
   1. Add Chrome WebDriver to PATH:
      ```bash
      echo 'export PATH=$PATH:/path/to/chromedriver' >> ~/.bash_profile
      source ~/.bash_profile
      ```

### Troupleshooting 

1. **ChromeDriver Version Mismatch**
   - Ensure your Chrome browser version matches the ChromeDriver version
   - Check Chrome version: Open Chrome → ⋮ (menu) → Help → About Google Chrome
   - Update ChromeDriver if necessary

2. **Path Issues**
   - Verify system PATH includes ChromeDriver location
   - Try running Python and Chrome as administrator
   - Check for any antivirus software blocking ChromeDriver execution

3. **Common Errors**
   - `WinError 193`: Usually indicates architecture mismatch or incorrect PATH
   - `ChromeDriver not found`: Check if ChromeDriver is properly installed
   - `Session not created`: Version mismatch between Chrome and ChromeDriver



