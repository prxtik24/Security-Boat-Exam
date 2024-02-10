# Security-Boat-Exam
Task 1: Authentication System

from flask import Flask, request, jsonify
import jwt
import datetime
from functools import wraps

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your_secret_key'


def generate_token(user_id):
    token = jwt.encode({'user_id': user_id, 'exp': datetime.datetime.utcnow() + datetime.timedelta(hours=1)}, app.config['SECRET_KEY'])
    return token


def login_required(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        token = request.headers.get('Authorization')
        if not token:
            return jsonify({'message': 'Token is missing!'}), 403
        try:
            data = jwt.decode(token, app.config['SECRET_KEY'])
        except:
            return jsonify({'message': 'Token is invalid!'}), 403
        return f(*args, **kwargs)
    return decorated_function


@app.route('/signup', methods=['POST'])
def signup():
    # Add logic to register a new user
    return jsonify({'message': 'Signup successful!'})


@app.route('/login', methods=['POST'])
def login():
    # Add logic to authenticate user and generate JWT token
    # Return token on successful login
    return jsonify({'token': generate_token(user_id)})


@app.route('/logout', methods=['GET'])
@login_required
def logout():
    # Add logic to logout user
    return jsonify({'message': 'Logout successful!'})

if __name__ == '__main__':
    app.run(debug=True)


Task 2: List of Products by Category


@app.route('/products/<category>', methods=['GET'])
def get_products_by_category(category):
    # Add logic to retrieve products based on category
    return jsonify({'products': products_in_category})


Task 3: Add Specific Product


@app.route('/products/add', methods=['POST'])
@login_required
def add_product():
    # Add logic to add a new product
    return jsonify({'message': 'Product added successfully!'})


Task 4: Buy Product


@app.route('/products/buy/<product_id>', methods=['POST'])
@login_required
def buy_product(product_id):
    # Add logic to purchase a product
    return jsonify({'message': 'Product purchased successfully!'})


Task 5: Status of Product


@app.route('/products/status/<product_id>', methods=['GET'])
@login_required
def check_product_status(product_id):
    # Add logic to check status of a product
    return jsonify({'status': product_status})





