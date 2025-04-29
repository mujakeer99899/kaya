<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kaya Restaurant - Menu</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Roboto:wght@300;400&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f9f5f0;
        }
        .hero {
            background-image: url('https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            height: 70vh;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            text-align: center;
            text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.8);
        }
        .nav-bar {
            background-color: rgba(34, 34, 34, 0.95);
            position: sticky;
            top: 0;
            z-index: 1000;
            padding: 1rem 0;
        }
        .search-bar {
            max-width: 600px;
            margin: 2rem auto;
            position: relative;
        }
        .search-bar input {
            width: 100%;
            padding: 0.75rem 1rem;
            border-radius: 25px;
            border: 1px solid #ccc;
            font-size: 1rem;
            outline: none;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .menu-section {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }
        .category {
            margin-bottom: 3rem;
        }
        .category h2 {
            font-family: 'Playfair Display', serif;
            font-size: 2.5rem;
            color: #2d2d2d;
            border-bottom: 3px solid #d4a373;
            padding-bottom: 0.5rem;
            margin-bottom: 1.5rem;
        }
        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
        }
        .menu-item {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            overflow: hidden;
            text-align: center;
            padding: 1rem;
            cursor: pointer;
        }
        .menu-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
        }
        .menu-item img {
            width: 100%;
            height: 150px;
            object-fit: cover;
            border-radius: 8px;
            margin-bottom: 0.5rem;
        }
        .menu-item span.name {
            font-size: 1.2rem;
            font-weight: 600;
            color: #2d2d2d;
            display: block;
        }
        .menu-item span.price {
            font-size: 1rem;
            color: #d4a373;
            margin: 0.5rem 0;
            display: block;
        }
        .order-btn {
            background-color: #d4a373;
            color: white;
            padding: 0.5rem 1.5rem;
            border-radius: 5px;
            text-transform: uppercase;
            font-weight: 600;
            transition: background-color 0.3s ease;
            border: none;
            cursor: pointer;
        }
        .order-btn:hover {
            background-color: #b38b59;
        }
        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 2000;
            align-items: center;
            justify-content: center;
        }
        .modal-content {
            background-color: white;
            border-radius: 10px;
            max-width: 500px;
            width: 90%;
            padding: 2rem;
            text-align: center;
            position: relative;
        }
        .modal-content img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 8px;
            margin-bottom: 1rem;
        }
        .modal-content h3 {
            font-family: 'Playfair Display', serif;
            font-size: 1.8rem;
            color: #2d2d2d;
            margin-bottom: 0.5rem;
        }
        .modal-content p.price {
            font-size: 1.2rem;
            color: #d4a373;
            margin-bottom: 1rem;
        }
        .modal-content p.description {
            font-size: 1rem;
            color: #4a4a4a;
            margin-bottom: 1.5rem;
        }
        .close-btn {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 1.5rem;
            cursor: pointer;
            color: #2d2d2d;
        }
        footer {
            background-color: #2d2d2d;
            color: white;
            text-align: center;
            padding: 2rem;
            font-size: 0.9rem;
        }
        @media (max-width: 768px) {
            .hero {
                height: 50vh;
            }
            .menu-grid {
                grid-template-columns: 1fr;
            }
            .nav-bar .flex {
                flex-wrap: wrap;
                justify-content: center;
            }
            .modal-content {
                width: 95%;
                padding: 1.5rem;
            }
            .modal-content img {
                height: 150px;
            }
        }
    </style>
</head>
<body>
    <div class="hero">
        <div>
            <h1 class="text-5xl md:text-6xl font-bold font-playfair">Kaya Restaurant</h1>
            <p class="text-xl md:text-2xl mt-4">Savor the Art of Flavor</p>
        </div>
    </div>
    <nav class="nav-bar">
        <div class="max-w-5xl mx-auto flex flex-wrap justify-center space-x-2 md:space-x-4">
            <button onclick="showCategory('all')" class="text-white px-4 py-2 rounded hover:bg-gray-700">All</button>
            <button onclick="showCategory('appetizers')" class="text-white px-4 py-2 rounded hover:bg-gray-700">Appetizers</button>
            <button onclick="showCategory('veg')" class="text-white px-4 py-2 rounded hover:bg-gray-700">Vegetarian</button>
            <button onclick="showCategory('non-veg')" class="text-white px-4 py-2 rounded hover:bg-gray-700">Non-Vegetarian</button>
            <button onclick="showCategory('desserts')" class="text-white px-4 py-2 rounded hover:bg-gray-700">Desserts</button>
            <button onclick="showCategory('beverages')" class="text-white px-4 py-2 rounded hover:bg-gray-700">Beverages</button>
            <button onclick="showCategory('specials')" class="text-white px-4 py-2 rounded hover:bg-gray-700">Specials</button>
        </div>
    </nav>
    <div class="search-bar">
        <input type="text" id="searchInput" placeholder="Search menu items..." oninput="searchMenu()">
    </div>
    <div class="menu-section" id="menuContainer">
        <div class="category" id="appetizers">
            <h2>Appetizers</h2>
            <div class="menu-grid"></div>
        </div>
        <div class="category" id="veg">
            <h2>Vegetarian</h2>
            <div class="menu-grid"></div>
        </div>
        <div class="category" id="non-veg">
            <h2>Non-Vegetarian</h2>
            <div class="menu-grid"></div>
        </div>
        <div class="category" id="desserts">
            <h2>Desserts</h2>
            <div class="menu-grid"></div>
        </div>
        <div class="category" id="beverages">
            <h2>Beverages</h2>
            <div class="menu-grid"></div>
        </div>
        <div class="category" id="specials">
            <h2>Chef's Specials</h2>
            <div class="menu-grid"></div>
        </div>
    </div>
    <!-- Modal for Dish Details -->
    <div id="dishModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">×</span>
            <img id="modalImage" src="" alt="Dish">
            <h3 id="modalName"></h3>
            <p id="modalPrice" class="price"></p>
            <p id="modalDescription" class="description"></p>
            <button id="modalOrderBtn" class="order-btn">Order Now</button>
        </div>
    </div>
    <footer>
        <p class="text-lg">Contact Us: +91 9949427470 | info@kayarestaurant.com</p>
        <p>123 Gourmet Avenue, Food City, FC 12345</p>
        <p>© 2025 Kaya Restaurant. All Rights Reserved.</p>
    </footer>

    <script>
        // Menu items data with images, prices in INR, and descriptions
        const menuItems = [
            // Appetizers
            { name: "Spring Rolls", price: 5.99, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Crispy rolls filled with fresh vegetables, served with sweet chili sauce." },
            { name: "Garlic Bread", price: 4.49, category: "appetizers", image: "https://images.unsplash.com/photo-1622735672604-b1f5f0e127ae?auto=format&fit=crop&w=300&q=80", description: "Toasted bread with a rich garlic butter spread." },
            { name: "Bruschetta", price: 6.29, category: "app échapper:izers", image: "https://images.unsplash.com/photo-1599819170777-1c3e1c8e7775?auto=format&fit=crop&w=300&q=80", description: "Grilled bread topped with fresh tomatoes, basil, and olive oil." },
            { name: "Stuffed Mushrooms", price: 7.49, category: "appetizers", image: "https://images.unsplash.com/photo-1595878655060-2b1e3c3e8f22?auto=format&fit=crop&w=300&q=80", description: "Mushrooms filled with a savory cheese and herb stuffing." },
            { name: "Mozzarella Sticks", price: 6.99, category: "appetizers", image: "https://images.unsplash.com/photo-1595878655060-2b1e3c3e8f22?auto=format&fit=crop&w=300&q=80", description: "Golden-fried mozzarella sticks with marinara dip." },
            { name: "Chicken Wings", price: 8.49, category: "appetizers", image: "https://images.unsplash.com/photo-1569058242253-92d5d0d27b1b?auto=format&fit=crop&w=300&q=80", description: "Spicy buffalo wings served with a cooling ranch dip." },
            { name: "Nachos Supreme", price: 7.99, category: "appetizers", image: "https://images.unsplash.com/photo-1598312916848-3e8e9f9d8d8d?auto=format&fit=crop&w=300&q=80", description: "Crispy nachos topped with cheese, jalapeños, and salsa." },
            { name: "Samosa", price: 5.49, category: "appetizers", image: "https://images.unsplash.com/photo-1590283601920-b8e0d0b0c1ef?auto=format&fit=crop&w=300&q=80", description: "Crispy pastry filled with spiced potatoes and peas." },
            { name: "Onion Rings", price: 4.99, category: "appetizers", image: "https://images.unsplash.com/photo-1586871506839-6483e9a7e869?auto=format&fit=crop&w=300&q=80", description: "Golden-fried onion rings with a tangy dip." },
            { name: "Calamari Fritti", price: 8.99, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Crispy fried calamari rings with marinara sauce." },
            { name: "Potato Skins", price: 6.49, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Baked potato skins topped with cheese and bacon bits." },
            { name: "Prawn Cocktail", price: 9.29, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Chilled prawns in a tangy cocktail sauce." },
            { name: "Caprese Salad", price: 7.49, category: "appetizers", image: "https://images.unsplash.com/photo-1599819170777-1c3e1c8e7775?auto=format&fit=crop&w=300&q=80", description: "Fresh tomatoes, mozzarella, and basil drizzled with balsamic glaze." },
            { name: "Hummus Platter", price: 6.99, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Creamy hummus served with pita bread and veggies." },
            { name: "Tandoori Paneer", price: 8.49, category: "appetizers", image: "https://images.unsplash.com/photo-1604477632857-5e6b6b4b3f98?auto=format&fit=crop&w=300&q=80", description: "Marinated paneer grilled to perfection." },
            { name: "Mini Quiches", price: 6.29, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Bite-sized quiches with assorted fillings." },
            { name: "Crab Cakes", price: 9.99, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Golden crab cakes served with a zesty remoulade." },
            { name: "Veg Pakora", price: 5.99, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Crispy vegetable fritters with a tangy chutney." },
            { name: "Chicken Satay", price: 8.29, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Grilled chicken skewers with peanut sauce." },
            { name: "Cheese Platter", price: 10.49, category: "appetizers", image: "https://images.unsplash.com/photo-1608030805234-14b476a8b06c?auto=format&fit=crop&w=300&q=80", description: "Assorted cheeses with crackers and grapes." },
            // Vegetarian
            { name: "Paneer Tikka", price: 8.99, category: "veg", image: "https://images.unsplash.com/photo-1604477632857-5e6b6b4b3f98?auto=format&fit=crop&w=300&q=80", description: "Marinated paneer cubes grilled with spices." },
            { name: "Vegetable Biryani", price: 7.49, category: "veg", image: "https://images.unsplash.com/photo-1589301760014-d929f3979dbc?auto=format&fit=crop&w=300&q=80", description: "Fragrant rice with mixed vegetables and spices." },
            { name: "Dal Makhani", price: 6.99, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Creamy black lentils cooked with butter and spices." },
            { name: "Aloo Gobi", price: 7.99, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Potatoes and cauliflower in a spiced curry." },
            { name: "Chana Masala", price: 6.49, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Spicy chickpea curry with fresh herbs." },
            { name: "Palak Paneer", price: 8.29, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Paneer cubes in a creamy spinach gravy." },
            { name: "Veg Korma", price: 7.99, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Mixed vegetables in a rich, creamy sauce." },
            { name: "Mushroom Masala", price: 7.49, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Spiced mushrooms in a flavorful gravy." },
            { name: "Baingan Bharta", price: 7.29, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Smoky roasted eggplant mashed with spices." },
            { name: "Veg Manchurian", price: 6.99, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Vegetable dumplings in a tangy Indo-Chinese sauce." },
            { name: "Malai Kofta", price: 8.49, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Soft paneer balls in a creamy tomato sauce." },
            { name: "Bhindi Masala", price: 7.19, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Stir-fried okra with onions and spices." },
            { name: "Paneer Butter Masala", price: 8.99, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Paneer in a rich buttery tomato sauce." },
            { name: "Veg Fried Rice", price: 6.79, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Stir-fried rice with mixed vegetables." },
            { name: "Tofu Stir Fry", price: 7.49, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Crispy tofu with vegetables in a savory sauce." },
            { name: "Veg Noodles", price: 6.99, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Stir-fried noodles with vegetables." },
            { name: "Rajma Curry", price: 6.89, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Kidney beans in a spiced tomato gravy." },
            { name: "Veg Pulao", price: 7.29, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Fragrant rice with vegetables and spices." },
            { name: "Paneer Bhurji", price: 8.19, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Scrambled paneer with spices and herbs." },
            { name: "Mixed Veg Curry", price: 7.39, category: "veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Assorted vegetables in a spiced curry." },
            // Non-Vegetarian
            { name: "Chicken Tikka Masala", price: 10.99, category: "non-veg", image: "https://images.unsplash.com/photo-1599487488170-d71c1088b435?auto=format&fit=crop&w=300&q=80", description: "Grilled chicken in a creamy tomato sauce." },
            { name: "Butter Chicken", price: 9.99, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Tender chicken in a rich buttery sauce." },
            { name: "Fish Curry", price: 11.49, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Fresh fish cooked in a spicy coconut curry." },
            { name: "Mutton Rogan Josh", price: 12.99, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Aromatic mutton curry with Kashmiri spices." },
            { name: "Chicken Biryani", price: 10.49, category: "non-veg", image: "https://images.unsplash.com/photo-1589301760014-d929f3979dbc?auto=format&fit=crop&w=300&q=80", description: "Fragrant rice with spiced chicken." },
            { name: "Prawn Masala", price: 12.29, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Prawns cooked in a spicy masala sauce." },
            { name: "Lamb Korma", price: 11.99, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Tender lamb in a creamy nut-based sauce." },
            { name: "Chicken Vindaloo", price: 10.79, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Spicy chicken curry with vinegar and potatoes." },
            { name: "Tandoori Chicken", price: 11.49, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Marinated chicken grilled in a tandoor." },
            { name: "Fish Fry", price: 10.99, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Crispy fried fish with spices." },
            { name: "Mutton Biryani", price: 12.49, category: "non-veg", image: "https://images.unsplash.com/photo-1589301760014-d929f3979dbc?auto=format&fit=crop&w=300&q=80", description: "Fragrant rice with spiced mutton." },
            { name: "Chicken Keema", price: 10.29, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Minced chicken cooked with spices." },
            { name: "Prawn Fried Rice", price: 11.79, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Stir-fried rice with succulent prawns." },
            { name: "Chicken Manchurian", price: 10.69, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Chicken in a tangy Indo-Chinese sauce." },
            { name: "Lamb Saag", price: 11.89, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Lamb cooked with creamy spinach." },
            { name: "Chicken Noodles", price: 10.39, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Stir-fried noodles with chicken." },
            { name: "Fish Tikka", price: 11.59, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Marinated fish grilled to perfection." },
            { name: "Mutton Keema", price: 12.19, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Minced mutton cooked with spices." },
            { name: "Chicken Curry", price: 10.49, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Classic chicken curry with rich spices." },
            { name: "Prawn Korma", price: 12.69, category: "non-veg", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Prawns in a creamy nut-based sauce." },
            // Desserts
            { name: "Gulab Jamun", price: 4.99, category: "desserts", image: "https://images.unsplash.com/photo-1603565816030-8f16b1e4e0a1?auto=format&fit=crop&w=300&q=80", description: "Soft dough balls soaked in sugar syrup." },
            { name: "Rasmalai", price: 5.49, category: "desserts", image: "https://images.unsplash.com/photo-1603565816030-8f16b1e4e0a1?auto=format&fit=crop&w=300&q=80", description: "Spongy paneer balls in sweetened milk." },
            { name: "Chocolate Lava Cake", price: 6.29, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Warm cake with a gooey chocolate center." },
            { name: "Cheesecake", price: 5.99, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Creamy cheesecake with a graham cracker crust." },
            { name: "Kulfi", price: 4.79, category: "desserts", image: "https://images.unsplash.com/photo-1603565816030-8f16b1e4e0a1?auto=format&fit=crop&w=300&q=80", description: "Traditional Indian ice cream with nuts." },
            { name: "Tiramisu", price: 6.49, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Coffee-flavored layered dessert with mascarpone." },
            { name: "Mango Mousse", price: 5.69, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Light and creamy mango-flavored mousse." },
            { name: "Ice Cream Sundae", price: 5.29, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Vanilla ice cream with toppings and whipped cream." },
            { name: "Kheer", price: 4.89, category: "desserts", image: "https://images.unsplash.com/photo-1603565816030-8f16b1e4e0a1?auto=format&fit=crop&w=300&q=80", description: "Creamy rice pudding with cardamom and nuts." },
            { name: "Carrot Cake", price: 5.79, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Moist cake with cream cheese frosting." },
            { name: "Panna Cotta", price: 6.19, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Silky vanilla custard with berry compote." },
            { name: "Fruit Tart", price: 5.99, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Crispy tart filled with custard and fresh fruits." },
            { name: "Baklava", price: 5.49, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Layered pastry with nuts and honey syrup." },
            { name: "Jalebi", price: 4.69, category: "desserts", image: "https://images.unsplash.com/photo-1603565816030-8f16b1e4e0a1?auto=format&fit=crop&w=300&q=80", description: "Crispy fried spirals soaked in sugar syrup." },
            { name: "Brownie", price: 5.39, category: "desserts", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Fudgy chocolate brownie with a crispy top." },
            // Beverages
            { name: "Mango Lassi", price: 3.99, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Refreshing yogurt-based mango drink." },
            { name: "Masala Chai", price: 2.99, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Spiced Indian tea with milk." },
            { name: "Fresh Lemonade", price: 3.49, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Cool and tangy lemon drink." },
            { name: "Iced Coffee", price: 4.29, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Chilled coffee with a touch of sweetness." },
            { name: "Virgin Mojito", price: 4.49, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Minty lime mocktail with soda." },
            { name: "Coca Cola", price: 2.49, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Classic carbonated soft drink." },
            { name: "Green Tea", price: 3.29, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Light and refreshing green tea." },
            { name: "Orange Juice", price: 3.79, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Freshly squeezed orange juice." },
            { name: "Pineapple Smoothie", price: 4.69, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Creamy pineapple blended with yogurt." },
            { name: "Hot Chocolate", price: 3.99, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Rich and warm chocolate drink." },
            { name: "Sparkling Water", price: 2.99, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Crisp carbonated water." },
            { name: "Strawberry Shake", price: 4.79, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Creamy strawberry milkshake." },
            { name: "Espresso", price: 3.49, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Strong and bold coffee shot." },
            { name: "Butter Milk", price: 3.19, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Cool and spiced buttermilk." },
            { name: "Cucumber Cooler", price: 4.29, category: "beverages", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Refreshing cucumber and mint drink." },
            // Specials
            { name: "Truffle Pasta", price: 14.99, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Creamy pasta with truffle oil and mushrooms." },
            { name: "Lobster Thermidor", price: 19.99, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Lobster in a rich cheese and cream sauce." },
            { name: "Saffron Risotto", price: 13.49, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Creamy risotto infused with saffron." },
            { name: "Grilled Salmon", price: 16.99, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Perfectly grilled salmon with lemon herb sauce." },
            { name: "Veg Stuffed Bell Peppers", price: 12.99, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Bell peppers stuffed with spiced vegetables." },
            { name: "Lamb Shank", price: 18.49, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Slow-cooked lamb shank with rosemary." },
            { name: "Seafood Platter", price: 21.99, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Assorted seafood with dipping sauces." },
            { name: "Mushroom Ravioli", price: 13.99, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Homemade ravioli with mushroom filling." },
            { name: "Chicken Cordon Bleu", price: 15.49, category: "specials", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=300&q=80", description: "Breaded chicken stuffed with ham and cheese." },
            { name: "Trio Dessert Plate", price: 11.99, category: "specials", image: "https://images.unsplash.com/photo-1603565816030-8f16b1e4e0a1?auto=format&fit=crop&w=300&q=80", description: "A trio of mini desserts for sharing." }
        ];

        // Conversion rate: 1 USD = 83 INR
        const USD_TO_INR = 83;

        // Populate menu items
        function populateMenu() {
            const categories = ['appetizers', 'veg', 'non-veg', 'desserts', 'beverages', 'specials'];
            categories.forEach(category => {
                const categoryDiv = document.getElementById(category);
                const gridDiv = categoryDiv.querySelector('.menu-grid');
                const items = menuItems.filter(item => item.category === category);
                gridDiv.innerHTML = ''; // Clear existing items
                items.forEach(item => {
                    const itemDiv = document.createElement('div');
                    itemDiv.className = 'menu-item';
                    itemDiv.setAttribute('data-name', item.name.toLowerCase());
                    const priceInINR = (item.price * USD_TO_INR).toFixed(2);
                    itemDiv.innerHTML = `
                        <img src="${item.image}" alt="${item.name}" loading="lazy">
                        <span class="name">${item.name}</span>
                        <span class="price">₹${priceInINR}</span>
                    `;
                    itemDiv.addEventListener('click', () => showModal(item.name, priceInINR, item.image, item.description));
                    gridDiv.appendChild(itemDiv);
                });
            });
        }

        // Show/hide categories
        function showCategory(category) {
            const categories = ['appetizers', 'veg', 'non-veg', 'desserts', 'beverages', 'specials'];
            categories.forEach(cat => {
                const section = document.getElementById(cat);
                section.style.display = category === 'all' || category === cat ? 'block' : 'none';
            });
            document.getElementById('searchInput').value = ''; // Clear search
            searchMenu(); // Reset search results
        }

        // Search functionality
        function searchMenu() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const items = document.querySelectorAll('.menu-item');
            items.forEach(item => {
                const name = item.getAttribute('data-name');
                item.style.display = name.includes(query) ? 'block' : 'none';
            });
            // Show/hide categories based on visible items
            const categories = ['appetizers', 'veg', 'non-veg', 'desserts', 'beverages', 'specials'];
            categories.forEach(cat => {
                const categoryDiv = document.getElementById(cat);
                const visibleItems = categoryDiv.querySelectorAll('.menu-item[style="display: block;"]');
                categoryDiv.style.display = visibleItems.length > 0 ? 'block' : 'none';
            });
        }

        // Show modal with dish details
        function showModal(name, price, image, description) {
            const modal = document.getElementById('dishModal');
            document.getElementById('modalImage').src = image;
            document.getElementById('modalImage').alt = name;
            document.getElementById('modalName').textContent = name;
            document.getElementById('modalPrice').textContent = `₹${price}`;
            document.getElementById('modalDescription').textContent = description;
            document.getElementById('modalOrderBtn').onclick = () => placeOrder(name, price);
            modal.style.display = 'flex';
        }

        // Close modal
        function closeModal() {
            document.getElementById('dishModal').style.display = 'none';
        }

        // Place order via WhatsApp
        function placeOrder(item, price) {
            const message = `Hello, I would like to order ${item} (₹${price}) from Kaya Restaurant.`;
            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://wa.me/919949427470?text=${encodedMessage}`;
            window.open(whatsappUrl, '_blank');
        }

        // Initialize menu
        window.onload = () => {
            populateMenu();
            // Close modal when clicking outside
            document.getElementById('dishModal').addEventListener('click', (e) => {
                if (e.target === document.getElementById('dishModal')) {
                    closeModal();
                }
            });
        };
    </script>
</body>
</html>
