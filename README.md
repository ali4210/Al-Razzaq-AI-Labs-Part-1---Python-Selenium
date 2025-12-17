# Al Nafi International College - Selenium Automation Portfolio

## => Project Overview
This repository hosts a complete collection of **20 Automation Labs** completed during the **Selenium & Web Automation** certification at **Al Nafi International College**.

The project demonstrates comprehensive proficiency in **Web UI Automation**, covering the entire testing lifecycle from basic element interaction to advanced handling of iFrames, Windows, and End-to-End (E2E) workflows using **Python** and **Selenium WebDriver**. All scripts have been updated to the modern **Selenium 4** standard.

**Tech Stack:** Python 3.x, Selenium 4, WebDriver Manager, PyTest.

---

## => Repository Structure

The labs are organized into **5 modules** mirroring the automation engineer's workflow:

```text
/Al-Nafi-Selenium-Automation
│
├── 01_Browser_Basics/         # Setup, Navigation, Headless Mode
├── 02_Locators_Interactions/  # CSS/XPath, Forms, Buttons
├── 03_UI_Components/          # Dropdowns, Alerts, iFrames
├── 04_Advanced_Controls/      # Waits (Sync), Scrolling, Screenshots
└── 05_End_to_End_Project/     # Full E2E Web Application Test

```

---

## => Module Details

### 1. Browser Basics (Labs 1, 2, 8, 19)

*Focus: Environment configuration and driver management.*

**Setup:** Installing Selenium via pip and verifying installation.



**Navigation:** Launching Chrome/Firefox and validating URLs.


**Headless Testing:** Configuring `ChromeOptions` to run tests without a UI for CI/CD efficiency.



### 2. Locators & Interactions (Labs 3-7, 11)

*Focus: Identifying and manipulating DOM elements.*

* 
**Strategy:** Using `By.ID`, `By.NAME`, `CSS Selectors`, and `XPATH` to find robust locators.


* 
**Actions:** Simulating user behavior: Clicking buttons, typing into inputs (`send_keys`), and submitting forms.


* 
**Bulk Handling:** Locating and iterating through multiple elements (e.g., extracting all links).



### 3. UI Components (Labs 12-16)

*Focus: Handling complex HTML structures.*

* 
**Dropdowns:** Using the `Select` class to choose options by index, value, or text.


* 
**Context Switching:** Handling Javascript **Alerts** (`switch_to.alert`) and **iFrames** (`switch_to.frame`).


* 
**Multi-Window:** Managing multiple browser tabs and window handles.



### 4. Advanced Controls (Labs 9, 10, 17, 18)

*Focus: Stability and Debugging.*

* 
**Synchronization:** Implementing **Explicit Waits** (`WebDriverWait`) to handle dynamic loading (vs. Implicit Waits).


* 
**Evidence:** Capturing **Screenshots** automatically with timestamps.


* 
**JavaScript Execution:** Using `execute_script` for scrolling and handling hidden elements.


* 
**File Uploads:** Automating file inputs without GUI interaction.



### 5. Capstone Project (Lab 20)

**End-to-End Automation:** A complete script testing a simulated workflow.

* 
**Flow:** Login -> Search Product -> Form Interaction -> Validation -> Teardown.



---

## => Comprehensive Guidelines: The "Universal Automation Logic"

**How to Rebuild These Scripts**

Every automation script in this repository follows the **POM-lite (Page Object Model inspired)** structure. You can use this template for any test.

### Phase 1: The Setup Pattern (Universal)

**Concept:** Start the browser and define wait strategies.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# 1. Initialize Driver
options = webdriver.ChromeOptions()
# options.add_argument("--headless") # Optional for servers
driver = webdriver.Chrome(options=options)

# 2. Universal Timeout (Explicit Wait)
# Crucial for stability in modern web apps
wait = WebDriverWait(driver, 10) # Wait up to 10 seconds

# 3. Navigate
driver.get("[https://example.com](https://example.com)")

```

### Phase 2: The Interaction Pattern

**Concept:** Find -> Wait -> Act. *Never act without waiting.*

```python
# Universal Interaction Logic
try:
    # 1. Locate (with wait)
    # Using modern Selenium 4 'By' strategy
    element = wait.until(EC.element_to_be_clickable((By.ID, "submit_btn")))
    
    # 2. Act
    element.click()
    
    # 3. Input
    input_field = driver.find_element(By.NAME, "username")
    input_field.clear() # Always clear before typing
    input_field.send_keys("MyUser")
    
except Exception as e:
    print(f"Test Failed: {e}")
    driver.save_screenshot("error_evidence.png")

```

### Phase 3: The Validation Pattern

**Concept:** Trust but verify (Assertions).

```python
# Universal Assertion Logic
actual_title = driver.title
expected_title = "Dashboard"

# Use Python's built-in assert for verification
assert expected_title in actual_title, f"Expected {expected_title}, but got {actual_title}"
print("Validation Passed ✅")

```

### Phase 4: The Teardown Pattern

**Concept:** Clean up resources to prevent memory leaks.

```python
# Always close the browser session
driver.quit()

```

---

## => Installation & Usage

1. **Clone the repository:**
```bash
git clone [https://github.com/SaleemAli/Al-Nafi-Selenium-Automation.git](https://github.com/SaleemAli/Al-Nafi-Selenium-Automation.git)

```


2. **Install dependencies:**
```bash
pip install selenium webdriver-manager

```


3. **Run a specific lab:**
```bash
cd 05_End_to_End_Project
python e2e_ecommerce_test.py

```



---

## => Connect

**Saleem Ali** *QA Automation Engineer*

[LinkedIn Profile](https://www.google.com/search?q=https://www.linkedin.com/in/saleem-ali) | [GitHub Repositories](https://www.google.com/search?q=https://github.com/SaleemAli%3Ftab%3Drepositories)

---

**Status:** Completed

**Institution:** [Al Nafi International College - Our Courses](https://alnafi.com/courses)

```

```


