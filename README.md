<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Grocery List & Billing System</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f0f4f8 0%, #d9e2ec 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 15px;
        }
        
        .container {
            width: 100%;
            max-width: 1200px;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.15);
            overflow: hidden;
            margin: 20px;
        }
        
        header {
            background: linear-gradient(90deg, #4b6cb7 0%, #182848 100%);
            color: white;
            padding: 25px 20px;
            text-align: center;
            position: relative;
        }
        
        header h1 {
            font-size: 2rem;
            margin-bottom: 8px;
        }
        
        header p {
            opacity: 0.9;
            font-size: 1rem;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .app-container {
            display: flex;
            flex-wrap: wrap;
        }
        
        .list-section {
            flex: 1;
            min-width: 300px;
            padding: 25px 20px;
            border-right: 1px solid #eee;
        }
        
        .billing-section {
            flex: 1;
            min-width: 300px;
            padding: 25px 20px;
            background: #f9fbfd;
        }
        
        .section-title {
            font-size: 1.4rem;
            color: #2c3e50;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #4b6cb7;
            display: flex;
            align-items: center;
        }
        
        .section-title i {
            margin-right: 10px;
            color: #4b6cb7;
        }
        
        .input-group {
            display: flex;
            flex-wrap: wrap;
            margin-bottom: 20px;
            gap: 10px;
        }
        
        .input-group input, 
        .input-group select {
            flex: 1;
            min-width: 120px;
            padding: 12px 15px;
            border: 2px solid #e1e5ee;
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
            transition: border 0.3s;
        }
        
        .input-group input:focus,
        .input-group select:focus {
            border-color: #4b6cb7;
        }
        
        .input-group button {
            background: #4b6cb7;
            color: white;
            border: none;
            padding: 0 25px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            min-width: 50px;
        }
        
        .input-group button i {
            font-size: 1.2rem;
            margin-right: 8px;
        }
        
        .input-group button:hover {
            background: #3a5999;
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(74, 108, 183, 0.3);
        }
        
        .grocery-list {
            list-style: none;
            margin-top: 20px;
        }
        
        .grocery-item {
            display: flex;
            align-items: center;
            padding: 15px;
            background: white;
            border-radius: 10px;
            margin-bottom: 12px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.06);
            transition: all 0.3s ease;
            border-left: 4px solid #4b6cb7;
        }
        
        .grocery-item.checked {
            background-color: #f0f7ff;
            border-left-color: #4CAF50;
        }
        
        .grocery-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .grocery-item input[type="checkbox"] {
            width: 22px;
            height: 22px;
            margin-right: 15px;
            cursor: pointer;
            accent-color: #4CAF50;
        }
        
        .item-details {
            flex: 1;
            min-width: 0;
        }
        
        .item-name {
            font-weight: 600;
            font-size: 1.1rem;
            margin-bottom: 5px;
            color: #2c3e50;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .item-meta {
            display: flex;
            gap: 15px;
            font-size: 0.95rem;
        }
        
        .item-price {
            color: #4b6cb7;
            font-weight: 600;
        }
        
        .item-category {
            color: #7f8c8d;
            font-style: italic;
        }
        
        .quantity-controls {
            display: flex;
            align-items: center;
            margin: 0 15px;
            background: #f5f7fa;
            border-radius: 50px;
            overflow: hidden;
        }
        
        .quantity-btn {
            width: 32px;
            height: 32px;
            background: #e1e5ee;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 1.1rem;
            transition: all 0.2s;
        }
        
        .quantity-btn:hover {
            background: #4b6cb7;
            color: white;
        }
        
        .quantity-display {
            width: 40px;
            text-align: center;
            font-weight: 600;
        }
        
        .item-total {
            font-weight: 700;
            min-width: 70px;
            text-align: right;
            color: #2c3e50;
        }
        
        .action-buttons {
            display: flex;
            margin-left: 10px;
        }
        
        .action-btn {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s;
            margin-left: 8px;
        }
        
        .edit-btn {
            background: #4b6cb7;
            color: white;
        }
        
        .edit-btn:hover {
            background: #3a5999;
            transform: scale(1.1);
        }
        
        .delete-btn {
            background: #ff6b6b;
            color: white;
        }
        
        .delete-btn:hover {
            background: #ff5252;
            transform: scale(1.1);
        }
        
        .bill-details {
            background: white;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
        }
        
        .bill-row {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px dashed #e1e5ee;
        }
        
        .bill-row:last-child {
            border-bottom: none;
        }
        
        .bill-label {
            color: #7f8c8d;
        }
        
        .bill-value {
            font-weight: 600;
            color: #2c3e50;
        }
        
        .total-row {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 2px solid #e1e5ee;
            font-size: 1.3rem;
            color: #2c3e50;
        }
        
        .total-amount {
            color: #4b6cb7;
            font-weight: 700;
            font-size: 1.5rem;
        }
        
        .bill-items {
            max-height: 250px;
            overflow-y: auto;
            margin-top: 20px;
            padding-right: 10px;
        }
        
        .bill-item {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #f1f1f1;
            animation: fadeIn 0.3s ease;
        }
        
        .bill-item-name {
            flex: 1;
        }
        
        .bill-item-meta {
            display: flex;
            gap: 10px;
            color: #7f8c8d;
            font-size: 0.9rem;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateX(-10px); }
            to { opacity: 1; transform: translateX(0); }
        }
        
        .empty-state {
            text-align: center;
            padding: 30px;
            color: #7f8c8d;
        }
        
        .empty-state i {
            font-size: 3rem;
            margin-bottom: 15px;
            color: #bdc3c7;
        }
        
        .action-buttons-section {
            display: flex;
            gap: 12px;
            margin-top: 25px;
            flex-wrap: wrap;
        }
        
        .btn {
            flex: 1;
            padding: 14px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s;
            min-width: 140px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .btn-primary {
            background: #4b6cb7;
            color: white;
        }
        
        .btn-primary:hover {
            background: #3a5999;
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(74, 108, 183, 0.3);
        }
        
        .btn-outline {
            background: transparent;
            border: 2px solid #4b6cb7;
            color: #4b6cb7;
        }
        
        .btn-outline:hover {
            background: #f5f7fa;
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
        }
        
        .btn-warning {
            background: #ff9800;
            color: white;
        }
        
        .btn-warning:hover {
            background: #e68a00;
            transform: translateY(-2px);
        }
        
        .instructions {
            background: #e3f2fd;
            border-radius: 10px;
            padding: 15px;
            margin-top: 20px;
            font-size: 0.9rem;
            color: #2c3e50;
        }
        
        .instructions ul {
            padding-left: 20px;
            margin-top: 10px;
        }
        
        .instructions li {
            margin-bottom: 8px;
            line-height: 1.5;
        }
        
        .mobile-warning {
            display: none;
            background: #fff8e1;
            border-left: 4px solid #ffc107;
            padding: 10px 15px;
            margin-top: 15px;
            border-radius: 0 8px 8px 0;
            font-size: 0.9rem;
        }
        
        .stats-bar {
            display: flex;
            justify-content: space-between;
            background: #e3f2fd;
            padding: 12px 20px;
            border-radius: 10px;
            margin-top: 15px;
        }
        
        .stat-item {
            text-align: center;
        }
        
        .stat-value {
            font-weight: 700;
            font-size: 1.2rem;
            color: #4b6cb7;
        }
        
        .stat-label {
            font-size: 0.85rem;
            color: #7f8c8d;
        }
        
        /* Mobile responsiveness */
        @media (max-width: 768px) {
            .container {
                margin: 10px;
                border-radius: 15px;
            }
            
            header {
                padding: 20px 15px;
            }
            
            header h1 {
                font-size: 1.6rem;
            }
            
            .app-container {
                flex-direction: column;
            }
            
            .list-section, .billing-section {
                padding: 20px 15px;
            }
            
            .list-section {
                border-right: none;
                border-bottom: 1px solid #eee;
            }
            
            .section-title {
                font-size: 1.3rem;
            }
            
            .input-group {
                flex-direction: column;
                gap: 10px;
            }
            
            .input-group input, 
            .input-group select,
            .input-group button {
                width: 100%;
                padding: 14px;
            }
            
            .grocery-item {
                padding: 12px;
                flex-wrap: wrap;
            }
            
            .item-details {
                min-width: 100%;
                margin-bottom: 10px;
            }
            
            .quantity-controls {
                margin: 0 0 0 auto;
            }
            
            .item-total {
                min-width: auto;
                margin-left: 15px;
            }
            
            .bill-details {
                padding: 15px;
            }
            
            .mobile-warning {
                display: block;
            }
            
            .bill-item {
                flex-direction: column;
                gap: 5px;
            }
        }
        
        @media (max-width: 480px) {
            .btn {
                min-width: 100%;
            }
            
            .action-buttons-section {
                flex-direction: column;
            }
            
            .bill-row, .total-row {
                font-size: 1.1rem;
            }
            
            .total-amount {
                font-size: 1.3rem;
            }
            
            .stats-bar {
                flex-direction: column;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-shopping-basket"></i> Smart Grocery List</h1>
            <p>Complete grocery management with quantity control and auto-billing system</p>
        </header>
        
        <div class="app-container">
            <section class="list-section">
                <h2 class="section-title"><i class="fas fa-list"></i> Your Grocery List</h2>
                
                <div class="input-group">
                    <input type="text" id="item-name" placeholder="Item name">
                    <input type="number" id="item-price" placeholder="Price (₹)" step="0.01" min="0">
                    <select id="item-category">
                        <option value="">Select Category</option>
                        <option value="fruits">Fruits & Vegetables</option>
                        <option value="dairy">Dairy & Eggs</option>
                        <option value="meat">Meat & Seafood</option>
                        <option value="bakery">Bakery</option>
                        <option value="beverages">Beverages</option>
                        <option value="snacks">Snacks</option>
                        <option value="frozen">Frozen Foods</option>
                        <option value="household">Household</option>
                    </select>
                    <button id="add-item">
                        <i class="fas fa-plus"></i> Add Item
                    </button>
                </div>
                
                <div class="mobile-warning">
                    <i class="fas fa-info-circle"></i> Check items to add to your bill
                </div>
                
                <div class="stats-bar">
                    <div class="stat-item">
                        <div class="stat-value" id="total-items">0</div>
                        <div class="stat-label">Total Items</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="pending-items">0</div>
                        <div class="stat-label">Pending</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="estimated-total">₹0.00</div>
                        <div class="stat-label">Est. Total</div>
                    </div>
                </div>
                
                <ul class="grocery-list" id="grocery-list">
                    <!-- Grocery items will be added here dynamically -->
                </ul>
                
                <div class="instructions">
                    <p><strong>How to use:</strong></p>
                    <ul>
                        <li>Add items with name, price, and category</li>
                        <li>Adjust quantity with + and - buttons</li>
                        <li>Check items to add to bill (quantity matters)</li>
                        <li>Edit or delete items as needed</li>
                        <li>All changes update bill automatically</li>
                    </ul>
                </div>
            </section>
            
            <section class="billing-section">
                <h2 class="section-title"><i class="fas fa-receipt"></i> Your Bill</h2>
                
                <div class="bill-details">
                    <div class="bill-row">
                        <span class="bill-label">Subtotal:</span>
                        <span class="bill-value" id="subtotal">₹0.00</span>
                    </div>
                    <div class="bill-row">
                        <span class="bill-label">Tax (5%):</span>
                        <span class="bill-value" id="tax">₹0.00</span>
                    </div>
                    <div class="bill-row">
                        <span class="bill-label">Discount (10%):</span>
                        <span class="bill-value" id="discount">₹0.00</span>
                    </div>
                    <div class="bill-row total-row">
                        <span class="bill-label">Total:</span>
                        <span class="bill-value total-amount" id="total">₹0.00</span>
                    </div>
                </div>
                
                <div class="bill-items" id="bill-items">
                    <div class="empty-state" id="empty-bill">
                        <i class="fas fa-receipt"></i>
                        <p>Your bill is empty</p>
                        <p>Check items from your grocery list to add them here</p>
                    </div>
                </div>
                
                <div class="action-buttons-section">
                    <button class="btn btn-outline" id="clear-list">
                        <i class="fas fa-trash-alt"></i> Clear List
                    </button>
                    <button class="btn btn-warning" id="save-list">
                        <i class="fas fa-save"></i> Save List
                    </button>
                    <button class="btn btn-primary" id="checkout">
                        <i class="fas fa-credit-card"></i> Checkout
                    </button>
                </div>
            </section>
        </div>
    </div>

    <script>
        // Grocery categories with icons
        const categories = {
            'fruits': {name: 'Fruits & Vegetables', icon: 'fa-apple-alt'},
            'dairy': {name: 'Dairy & Eggs', icon: 'fa-egg'},
            'meat': {name: 'Meat & Seafood', icon: 'fa-drumstick-bite'},
            'bakery': {name: 'Bakery', icon: 'fa-bread-slice'},
            'beverages': {name: 'Beverages', icon: 'fa-coffee'},
            'snacks': {name: 'Snacks', icon: 'fa-cookie'},
            'frozen': {name: 'Frozen Foods', icon: 'fa-icicles'},
            'househ