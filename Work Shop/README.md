# Chrome WebDriver Path Setup Guide

This guide focuses on setting up Selenium WebDriver with explicit path configuration to avoid common installation and path-related errors.

## Project Setup

### 1. Required Dependencies
Install the necessary packages:
```bash
pip install selenium
pip install webdriver-manager
```

### 2. Chrome WebDriver Installation

1. Download ChromeDriver:
   - Visit the official ChromeDriver download page: https://googlechromodriver.github.io/ChromeDriver/
   - Download the version that matches your Chrome browser version
   - Extract the downloaded file

2. Create a dedicated folder for ChromeDriver:
   ```
   C:\Program Files (x86)\chromedriver-win64\
   ```

3. Move the `chromedriver.exe` to this folder

### 3. Code Implementation

Create your Python script (`app.py`) with the following code:

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
import os
import logging

# Set up logging
logging.basicConfig(level=logging.INFO)

try:
    # Specify the exact path to chromedriver.exe
    chrome_driver_path = r"C:\Program Files (x86)\chromedriver-win64\chromedriver.exe"
    
    # Verify the driver exists
    if not os.path.exists(chrome_driver_path):
        raise FileNotFoundError(f"ChromeDriver not found at: {chrome_driver_path}")
    
    # Set up the service
    service = Service(executable_path=chrome_driver_path)
    
    # Configure Chrome options
    options = Options()
    options.add_experimental_option('excludeSwitches', ['enable-logging'])
    
    # Initialize the driver
    driver = webdriver.Chrome(service=service, options=options)
    
    # Test the connection
    driver.get("https://example.com")
    print(f"Page title: {driver.title}")

except Exception as e:
    print(f"An error occurred: {str(e)}")
    logging.error(f"Error details: {str(e)}", exc_info=True)

finally:
    # Close the browser window if it was opened
    if 'driver' in locals():
        driver.quit()
```

### 4. Environment Variables Setup

1. Open System Properties:
   - Press `Win + R`
   - Type `sysdm.cpl` and press Enter
   - Go to "Advanced" tab
   - Click "Environment Variables"

2. Add ChromeDriver to System PATH:
   - Under "System variables", find and select "Path"
   - Click "Edit"
   - Click "New"
   - Add `C:\Program Files (x86)\chromedriver-win64`
   - Click "OK" on all windows

3. Verify PATH setup:
   - Open a new Command Prompt
   - Run: `echo %PATH%`
   - Ensure the ChromeDriver path is listed

## Common Issues and Solutions

### 1. WinError 193 (%1 is not a valid Win32 application)
This error usually occurs when:
- Wrong architecture version of ChromeDriver is installed
- PATH is pointing to incorrect location
- ChromeDriver file is corrupted

Solution:
```python
# Verify the driver path and architecture
import os
import platform

def verify_driver():
    chrome_driver_path = r"C:\Program Files (x86)\chromedriver-win64\chromedriver.exe"
    
    # Check if file exists
    if not os.path.exists(chrome_driver_path):
        print("ChromeDriver not found!")
        return False
        
    # Check system architecture
    system_arch = platform.architecture()[0]
    print(f"System Architecture: {system_arch}")
    
    return True

# Run verification before starting Selenium
if not verify_driver():
    raise Exception("Driver verification failed!")
```

### 2. Driver Not Found
If you get a "Driver not found" error:
1. Double-check the path
2. Ensure proper permissions
3. Try running as administrator

```python
# Add permission check
import os

def check_permissions():
    chrome_driver_path = r"C:\Program Files (x86)\chromedriver-win64\chromedriver.exe"
    try:
        # Try to read the file
        with open(chrome_driver_path, 'rb') as f:
            pass
        return True
    except PermissionError:
        print("Permission denied! Try running as administrator")
        return False
    except Exception as e:
        print(f"Error: {str(e)}")
        return False
```

## Version Compatibility

Keep track of versions to ensure compatibility:

```python
def print_versions():
    from selenium import webdriver
    import chromedriver_autoinstaller
    import platform
    
    print(f"Python Version: {platform.python_version()}")
    print(f"Selenium Version: {webdriver.__version__}")
    print(f"OS Version: {platform.platform()}")
    
    # Get Chrome version
    try:
        import winreg
        key = winreg.OpenKey(winreg.HKEY_CURRENT_USER, r"Software\Google\Chrome\BLBeacon")
        version = winreg.QueryValueEx(key, "version")[0]
        print(f"Chrome Version: {version}")
    except:
        print("Could not detect Chrome version")
```

## Testing the Setup

Create a test script to verify everything works:

```python
def test_setup():
    try:
        # Print versions
        print_versions()
        
        # Check permissions
        if not check_permissions():
            return False
            
        # Initialize driver
        chrome_driver_path = r"C:\Program Files (x86)\chromedriver-win64\chromedriver.exe"
        service = Service(executable_path=chrome_driver_path)
        driver = webdriver.Chrome(service=service)
        
        # Test connection
        driver.get("https://www.google.com")
        print("Setup successful!")
        driver.quit()
        return True
        
    except Exception as e:
        print(f"Setup failed: {str(e)}")
        return False

if __name__ == "__main__":
    test_setup()
```

## Maintenance

Regular maintenance tasks:
1. Update Chrome browser when prompted
2. Download matching ChromeDriver version
3. Replace the existing chromedriver.exe with the new version
4. Clear browser cache and cookies if necessary
5. Keep Selenium updated: `pip install --upgrade selenium`

Remember to always maintain version compatibility between:
- Chrome Browser
- ChromeDriver
- Selenium
- Python
