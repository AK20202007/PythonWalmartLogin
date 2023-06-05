# PythonWalmartLogin
import pandas as pd

from selenium import webdriver

from selenium.webdriver.common.keys import Keys

login_url = "https://www.walmart.com/account/login"


item = input("Enter an item: ")


driver = webdriver.Chrome()

driver.get(login_url)

driver.implicitly_wait(10)


username = driver.find_element_by_id("email")
password = driver.find_element_by_id("password")

username.send_keys("your_username")
password.send_keys("your_password")


password.send_keys(Keys.RETURN)


driver.implicitly_wait(10)


search_box = driver.find_element_by_id("global-search-input")

search_box.send_keys(item)

search_box.send_keys(Keys.RETURN)

driver.implicitly_wait(10)


results = driver.find_elements_by_class_name("search-result-product-title")


df = pd.DataFrame(columns=["Item Name"])


for result in results:
    item_name = result.text
    df = df.append({"Item Name": item_name}, ignore_index=True)


print(df)


driver.quit()
