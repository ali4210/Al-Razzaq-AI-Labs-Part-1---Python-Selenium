# 🤖 The Universal Selenium Mastery Guide
**Author:** Saleem Ali
**Curriculum:** Al Nafi Selenium (Labs 1–20)
**Purpose:** Personal Code Reference & Execution Manual

**Note:** I have updated all code to **Selenium 4** standards (e.g., `driver.find_element(By.ID, ...)` instead of `find_element_by_id`), as the old methods are deprecated.

---

## 📋 Lab Index
| Labs | Topic | Module |
| :--- | :--- | :--- |
| **1–2** | Install, Setup, Navigation | [Module 1: Basics](#-module-1-browser-basics) |
| **3–4** | Locators (ID, Name, CSS, XPath) | [Module 2: Interactions](#-module-2-locators--interactions) |
| **5–7** | Clicking, Typing, Forms | [Module 2: Interactions](#-module-2-locators--interactions) |
| **8, 11** | Verify Title, Multiple Elements | [Module 2: Interactions](#-module-2-locators--interactions) |
| **9–10** | Waits, Screenshots | [Module 4: Advanced](#-module-4-advanced-controls) |
| **12–16** | Dropdowns, Radios, Alerts, Frames | [Module 3: UI Components](#-module-3-ui-components) |
| **17–18** | Scrolling, File Upload | [Module 4: Advanced](#-module-4-advanced-controls) |
| **19** | Headless Mode | [Module 1: Basics](#-module-1-browser-basics) |
| **20** | End-to-End Project | [Module 5: Capstone](#-module-5-end-to-end-project) |

---

## 🟢 Module 1: Browser Basics

### Lab 1: Installation & Setup
* **Goal:** Verify Environment.
* **Script:** `01_setup.py`
```python
import selenium
from selenium import webdriver
print(f"Selenium Version: {selenium.__version__}")
# Use WebDriver Manager to avoid path issues
driver = webdriver.Chrome()
print("Browser Launched Successfully!")
driver.quit()

```

### Lab 2: Launch & Navigate

* **Goal:** Open URL and check.
* **Script:** `02_launch.py`

```python
from selenium import webdriver
driver = webdriver.Chrome()
driver.get("[https://www.google.com](https://www.google.com)")
print(f"Current URL: {driver.current_url}")
driver.quit()

```

### Lab 8: Verify Title

* **Goal:** Assertions.
* **Script:** `08_title_check.py`

```python
driver.get("[https://www.python.org](https://www.python.org)")
assert "Python" in driver.title, "Title mismatch!"
print("Title Verified.")

```

### Lab 19: Headless Mode

* **Goal:** Run without UI (Fast/Server).
* **Script:** `19_headless.py`

```python
from selenium.webdriver.chrome.options import Options
options = Options()
options.add_argument("--headless")
driver = webdriver.Chrome(options=options)
driver.get("[https://www.example.com](https://www.example.com)")
print(f"Headless Title: {driver.title}")

```

---

## 🔵 Module 2: Locators & Interactions

### Lab 3: Locating by ID & Name

* **Goal:** Basic Finding.
* **Script:** `03_locators_basic.py`

```python
from selenium.webdriver.common.by import By
# driver.get("file:///test_page.html")
# Old: driver.find_element_by_id("user") -> DEPRECATED
# New:
user = driver.find_element(By.ID, "username")
pw = driver.find_element(By.NAME, "password")
print(user.get_attribute("outerHTML"))

```

### Lab 4: CSS & XPath

* **Goal:** Advanced Finding.
* **Script:** `04_css_xpath.py`

```python
# CSS: Faster, simpler
elem_css = driver.find_element(By.CSS_SELECTOR, ".classname #id")
# XPath: Powerful, traverses up/down
elem_xpath = driver.find_element(By.XPATH, "//input[@type='text']")

```

### Lab 11: Locating Multiple Elements

* **Goal:** Get all links.
* **Script:** `11_multiple_elements.py`

```python
links = driver.find_elements(By.TAG_NAME, "a") # Note the 's' in elements
print(f"Found {len(links)} links")
for link in links:
    print(link.get_attribute("href"))

```

### Lab 5: Clicking Buttons

* **Goal:** Interaction.
* **Script:** `05_click.py`

```python
btn = driver.find_element(By.ID, "submit_btn")
btn.click()

```

### Lab 6: Typing (send_keys)

* **Goal:** Input data.
* **Script:** `06_typing.py`

```python
search = driver.find_element(By.NAME, "q")
search.clear() # Good practice to clear first
search.send_keys("Selenium Python")

```

### Lab 7: Form Submission

* **Goal:** Submit forms.
* **Script:** `07_submit.py`

```python
# You can click the button OR just use .submit() on the form element
form = driver.find_element(By.ID, "login_form")
form.submit()

```

---

## 🟠 Module 3: UI Components

### Lab 12: Dropdowns

* **Goal:** Handling `<select>`.
* **Script:** `12_dropdown.py`

```python
from selenium.webdriver.support.ui import Select
dropdown = Select(driver.find_element(By.ID, "colors"))
dropdown.select_by_visible_text("Blue")
# dropdown.select_by_value("blue_val")
# dropdown.select_by_index(1)

```

### Lab 13: Radio & Checkboxes

* **Goal:** Toggling.
* **Script:** `13_radio_check.py`

```python
# Click to select/deselect
checkbox = driver.find_element(By.ID, "subscribe")
if not checkbox.is_selected():
    checkbox.click()

```

### Lab 14: Alerts

* **Goal:** Javascript Popups.
* **Script:** `14_alerts.py`

```python
driver.find_element(By.ID, "alert_btn").click()
alert = driver.switch_to.alert
print(alert.text)
alert.accept() # Or alert.dismiss()

```

### Lab 15: Windows & Tabs

* **Goal:** Multi-tasking.
* **Script:** `15_windows.py`

```python
original_window = driver.current_window_handle
# (Trigger new window)
for window_handle in driver.window_handles:
    if window_handle != original_window:
        driver.switch_to.window(window_handle)
        break
# Switch back
driver.switch_to.window(original_window)

```

### Lab 16: iFrames

* **Goal:** embedded HTML.
* **Script:** `16_iframes.py`

```python
driver.switch_to.frame("frame_name_or_index")
# Do work inside frame
driver.switch_to.default_content() # Go back to main page

```

---

## 🟣 Module 4: Advanced Controls

### Lab 9: Waits (Crucial!)

* **Goal:** Sync speed.
* **Script:** `09_waits.py`

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Explicit Wait (The Best Way)
wait = WebDriverWait(driver, 10)
element = wait.until(EC.element_to_be_clickable((By.ID, "dynamic_btn")))
element.click()

```

### Lab 10: Screenshots

* **Goal:** Evidence.
* **Script:** `10_screenshot.py`

```python
import time
timestamp = time.strftime("%Y%m%d-%H%M%S")
driver.save_screenshot(f"evidence_{timestamp}.png")

```

### Lab 17: Scrolling

* **Goal:** JavaScript execution.
* **Script:** `17_scroll.py`

```python
# Scroll to bottom
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
# Scroll to element
element = driver.find_element(By.ID, "footer")
driver.execute_script("arguments[0].scrollIntoView();", element)

```

### Lab 18: File Upload

* **Goal:** Sending paths.
* **Script:** `18_upload.py`

```python
import os
# Don't click the 'Upload' button! Send keys to the <input type='file'>
file_input = driver.find_element(By.ID, "upload_input")
file_path = os.path.abspath("test_file.txt")
file_input.send_keys(file_path)

```

---

## ⚫ Module 5: End-to-End Project

### Lab 20: The Capstone

* **Goal:** Full Workflow.
* **Script:** `20_e2e_project.py`

```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By

# 1. Setup
driver = webdriver.Chrome()
driver.get("[http://automationpractice.com/index.php](http://automationpractice.com/index.php)")

# 2. Action: Search
driver.find_element(By.NAME, "search_query").send_keys("Dress")
driver.find_element(By.NAME, "submit_search").click()

# 3. Validation
assert "Search" in driver.title
results = driver.find_elements(By.CSS_SELECTOR, ".product-container")
assert len(results) > 0

print("E2E Test Passed!")
driver.quit()

```
