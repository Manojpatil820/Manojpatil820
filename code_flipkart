import pandas as pd
import requests
from bs4 import BeautifulSoup
import streamlit as st

def scrape_flipkart_laptops():
    laptop_names = []
    ratings = []
    reviews_and_ratings = []
    discounted_prices = []
    original_prices = []
    percentage_of_discounts = []
    specifications = []

    for i in range(1, 3):  # Scrape data from two pages
        url = f"https://www.flipkart.com/q/premium-laptops?page={i}"
        response = requests.get(url)
        soup = BeautifulSoup(response.text, 'html.parser')
        page = soup.find("div", class_="_1YokD2 _3Mn1Gg")

        # Extract laptop details
        model_name = page.find_all("div", class_="_4rR01T")
        for name in model_name:
            laptop_names.append(name.text)

        rating_s = page.find_all("div", class_="_3LWZlK")
        for rating in rating_s:
            ratings.append(rating.text)

        reviews_and_rating = page.find_all("span", class_="_2_R_DZ")
        for review in reviews_and_rating:
            reviews_and_ratings.append(review.text)

        laptop_price = page.find_all("div", class_="_30jeq3 _1_WHN1")
        for price in laptop_price:
            discounted_prices.append(price.text)

        without_discount = page.find_all("div", class_="_30jeq3 _1_WHN1")
        for original_price in without_discount:
            original_prices.append(original_price.text)

        dis_per = page.find_all("div", class_="_3Ay6Sb")
        for discount in dis_per:
            percentage_of_discounts.append(discount.text)

        lap_details = page.find_all("ul", class_="_1xgFaf")
        for detail in lap_details:
            specifications.append(detail.text)

    # Create a DataFrame
    data = {
        "Laptop Names": laptop_names,
        "Ratings": ratings,
        "Reviews and Ratings": reviews_and_ratings,
        "Discounted Prices": discounted_prices,
        "Original Prices": original_prices,
        "Percentage of Discount": percentage_of_discounts,
        "Specifications": specifications
    }

    df = pd.DataFrame(data)
    return df

def main():
    st.title("Flipkart Laptop Data Insights")
    
    st.subheader("Scraping Flipkart data for laptops and accessories")
    st.write("This Streamlit app retrieves laptop details and accessories data from Flipkart.")

    # Scrape data
    flipkart_data = scrape_flipkart_laptops()

    st.subheader("Laptop Data from Flipkart")
    st.write(f"Total Laptops Scraped: {len(flipkart_data)}")
    
    # Display the scraped data
    st.dataframe(flipkart_data)

if __name__ == "__main__":
    main()
