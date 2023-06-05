# PythonWalmartLogin
import pandas as pd
from selenium import webdriver
from selenium.webdriver.common.keys import Keys

# Walmart login URL
login_url = "https://www.walmart.com/account/login"

# User input for item
item = input("Enter an item: ")

# Launch web browser
driver = webdriver.Chrome()

# Open Walmart login page
driver.get(login_url)

# Wait for the page to load
driver.implicitly_wait(10)

# Fill in login credentials
username = driver.find_element_by_id("email")
password = driver.find_element_by_id("password")

# Enter your Walmart login credentials here
username.send_keys("your_username")
password.send_keys("your_password")

# Submit login form
password.send_keys(Keys.RETURN)

# Wait for the page to load
driver.implicitly_wait(10)

# Search for the item on Walmart
search_box = driver.find_element_by_id("global-search-input")
search_box.send_keys(item)
search_box.send_keys(Keys.RETURN)

# Wait for the search results to load
driver.implicitly_wait(10)

# Extract the search results
results = driver.find_elements_by_class_name("search-result-product-title")

# Create a pandas DataFrame to store the search results
df = pd.DataFrame(columns=["Item Name"])

# Add each search result to the DataFrame
for result in results:
    item_name = result.text
    df = df.append({"Item Name": item_name}, ignore_index=True)

# Print the shopping list
print(df)

# Close the web browser
driver.quit()
