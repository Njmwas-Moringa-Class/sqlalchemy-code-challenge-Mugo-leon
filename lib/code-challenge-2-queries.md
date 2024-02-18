QUERY 1 - RETURNS RATINGS CUSTOMERS HAVE GIVEN A RESTAURANT
customer_id = 1  # Replace this with other customer IDs to check for other customers

# Retrieve the customer
customer = session.query(Customer).filter_by(id=customer_id).first()

# Check if the customer exists
if customer:
    for review in customer.get_reviews():
        print(review)
else:
    print(f"Customer with ID {customer_id} not found.")
    
    
QUERY 2 - RETURNS ALL RATINGS OF A RESTAURANT
restaurant_id = 1  # Replace this with other restaurant IDs to check for other restaurants

# Retrieve the restaurant
restaurant = session.query(Restaurant).filter_by(id=restaurant_id).first()

# Check if the restaurant exists
if restaurant:
    # Print all reviews for the restaurant
    for review in restaurant.get_reviews():
        print(review)
else:
    print(f"Restaurant with ID {restaurant_id} not found.")

QUERY 3 - RETURNS ALL RESTAURANTS A CUSTOMER HAS REVIEWED
customer_id = 1  # Replace this with other customer IDs to check for other customers

# Retrieve the customer
customer = session.query(Customer).filter_by(id=customer_id).first()

# Check if the customer exists
if customer:
    # Print the names of all restaurants the customer has reviewed
    for review in customer.get_reviews():
        print(review.get_restaurant().name)
else:
    print(f"Customer with ID {customer_id} not found.")

QUERY 4 - Returns the full name of the customer, with the first name and the last name concatenated, Western style.
customer_id = 1  # Replace this with other customer IDs to check for other customers

# Retrieve the customer
customer = session.query(Customer).filter_by(id=customer_id).first()

# Check if the customer exists
if customer:
    # Concatenate first name and last name
    full_name = f"{customer.first_name} {customer.last_name}"
    print(full_name)
else:
    print(f"Customer with ID {customer_id} not found.")
    
QUERY 5 - Returns highest rated restaurant
from sqlalchemy import desc, func

# Query the Restaurant table to get the restaurant with the highest star rating
highest_rated_restaurant = session.query(Restaurant).\
    join(Review).\
    group_by(Restaurant.id).\
    order_by(desc(func.avg(Review.star_rating))).\
    first()

# Check if any restaurant was found
if highest_rated_restaurant:
    print(f"Highest Rated Restaurant: {highest_rated_restaurant.name}")
    print(f"Average Star Rating: {highest_rated_restaurant.get_reviews().average('star_rating')}")
else:
    print("No restaurants found.")



