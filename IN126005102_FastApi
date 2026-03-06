from fastapi import FastAPI

app = FastAPI()

# Temporary product database
products = [
    {"id": 1, "name": "Wireless Mouse", "price": 499, "category": "Electronics", "in_stock": True},
    {"id": 2, "name": "Notebook", "price": 99, "category": "Stationery", "in_stock": True},
    {"id": 3, "name": "Pen Set", "price": 49, "category": "Stationery", "in_stock": True},
    {"id": 4, "name": "USB Cable", "price": 199, "category": "Electronics", "in_stock": False},

    # Q1 – New products
    {"id": 5, "name": "Laptop Stand", "price": 1199, "category": "Electronics", "in_stock": True},
    {"id": 6, "name": "Mechanical Keyboard", "price": 2599, "category": "Electronics", "in_stock": True},
    {"id": 7, "name": "Webcam", "price": 1799, "category": "Electronics", "in_stock": False},
]

# Home endpoint
@app.get("/")
def home():
    return {"status": "FastAPI Store API Running"}

# Q1 – Get all products
@app.get("/products")
def fetch_products():
    product_count = len(products)

    return {
        "products": products,
        "total": product_count
    }

# Q2 – Filter products by category
@app.get("/products/category/{category_name}")
def filter_category(category_name: str):

    filtered_products = []

    for item in products:
        if item["category"].lower() == category_name.lower():
            filtered_products.append(item)

    if len(filtered_products) == 0:
        return {"error": "No products found in this category"}

    return {
        "category": category_name,
        "products": filtered_products,
        "total": len(filtered_products)
    }

# Q3 – Only available products
@app.get("/products/instock")
def available_products():

    stock_list = []

    for item in products:
        if item["in_stock"] == True:
            stock_list.append(item)

    return {
        "in_stock_products": stock_list,
        "count": len(stock_list)
    }

# Q4 – Store overview
@app.get("/store/summary")
def store_overview():

    total_products = len(products)

    in_stock_items = [p for p in products if p["in_stock"]]
    in_stock_count = len(in_stock_items)

    out_stock_count = total_products - in_stock_count

    category_set = set()
    for item in products:
        category_set.add(item["category"])

    return {
        "store_name": "My E-commerce Store",
        "total_products": total_products,
        "in_stock": in_stock_count,
        "out_of_stock": out_stock_count,
        "categories": list(category_set)
    }

# Q5 – Product search
@app.get("/products/search/{keyword}")
def search_product(keyword: str):

    matches = []

    for item in products:
        if keyword.lower() in item["name"].lower():
            matches.append(item)

    if not matches:
        return {"message": "No products matched your search"}

    return {
        "keyword": keyword,
        "products": matches,
        "count": len(matches)
    }

# BONUS – Best deal and premium product
@app.get("/products/deals")
def product_deals():

    lowest_price_product = min(products, key=lambda x: x["price"])
    highest_price_product = max(products, key=lambda x: x["price"])

    return {
        "best_deal": lowest_price_product,
        "premium_pick": highest_price_product
    }
