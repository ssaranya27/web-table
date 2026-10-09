# web-table

AUTOMATION CODE:

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver=webdriver.Edge()
wait=WebDriverWait(driver, 10)
driver.get("https://assertqa.com/practice/webtables")
table=wait.until(EC.visibility_of_element_located((By.XPATH,"//table/thead/tr")))
print(table.text)
first_row=wait.until(EC.visibility_of_element_located((By.XPATH,"//table/tbody/tr[1]")))
print(first_row.text)
last_row=wait.until(EC.visibility_of_element_located((By.XPATH,"//table/tbody/tr[last()]")))
print(last_row.text)
find_last_name=wait.until(EC.visibility_of_element_located((By.XPATH,"//table//td[contains(text(),'Smith')]")))
assert "Smith" in find_last_name.text
print("Matching cell found:", find_last_name.text)
emails=driver.find_elements(By.XPATH,"//table//td[contains(., '@')]")
for email in emails:
    print(email.text,end=" ")
highest_salary = 0
highest_employee = ""
rows = wait.until(
    EC.visibility_of_all_elements_located(
        (By.XPATH, "//table/tbody/tr")
    )
)

for row in rows:
    cells = row.find_elements(By.TAG_NAME, "td")

    name = cells[1].text + " " + cells[2].text
    salary_text = cells[5].text

    salary = int(
        salary_text.replace("$", "").replace(",", "")
    )

    if salary > highest_salary:
        highest_salary = salary
        highest_employee = name

print()
print("Highest salary:", highest_salary)
print("Employee:", highest_employee)

links = driver.find_elements(
    By.XPATH, "//a[contains(@href, '/practice')]"
)

if len(links) > 0:
    print("Link exists")
else:
    print("Link does not exist")

rows=wait.until(EC.visibility_of_all_elements_located((By.XPATH,"//table/tbody/tr/td")))
print(len(rows))

driver.quit()
```
