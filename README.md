<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Laptop Inventory System</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f8f9fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(135deg, #4b6cb7 0%, #182848 100%);
            color: white;
            padding: 20px 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .logo i {
            font-size: 2rem;
        }
        
        .logo h1 {
            font-size: 1.8rem;
            font-weight: 600;
        }
        
        .search-bar {
            display: flex;
            gap: 8px;
            background: rgba(255,255,255,0.2);
            padding: 8px 12px;
            border-radius: 25px;
        }
        
        .search-bar input {
            background: transparent;
            border: none;
            color: white;
            font-size: 1rem;
            width: 200px;
            outline: none;
        }
        
        .search-bar input::placeholder {
            color: rgba(255,255,255,0.8);
        }
        
        .search-bar button {
            background: transparent;
            border: none;
            color: white;
            cursor: pointer;
            font-size: 1rem;
        }
        
        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 25px 0;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .filter-section {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        
        .filter-section label {
            font-weight: 500;
            color: #555;
            font-size: 0.9rem;
        }
        
        .filter-section select {
            padding: 10px 12px;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            background: white;
            font-size: 0.9rem;
            cursor: pointer;
        }
        
        .add-btn {
            background: linear-gradient(135deg, #4b6cb7 0%, #182848 100%);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-size: 0.9rem;
            font-weight: 500;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .inventory-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .laptop-card {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        
        .laptop-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.12);
        }
        
        .card-header {
            background: linear-gradient(135deg, #4b6cb7 0%, #182848 100%);
            color: white;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .laptop-info h3 {
            font-size: 1.2rem;
            margin-bottom: 3px;
        }
        
        .laptop-info p {
            opacity: 0.9;
            font-size: 0.85rem;
        }
        
        .status {
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.75rem;
            font-weight: 500;
        }
        
        .status.available {
            background: #d4edda;
            color: #155724;
        }
        
        .status.in-use {
            background: #cce5ff;
            color: #004085;
        }
        
        .status.maintenance {
            background: #fff3cd;
            color: #856404;
        }
        
        .card-body {
            padding: 20px;
        }
        
        .specs {
            margin-bottom: 20px;
        }
        
        .spec-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
            font-size: 0.9rem;
        }
        
        .spec-item:last-child {
            border-bottom: none;
        }
        
        .spec-label {
            color: #666;
        }
        
        .spec-value {
            font-weight: 500;
            color: #333;
        }
        
        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            background: #f8f9fa;
            border-top: 1px solid #eee;
        }
        
        .price {
            font-size: 1.3rem;
            font-weight: 700;
            color: #333;
        }
        
        .actions {
            display: flex;
            gap: 8px;
        }
        
        .action-btn {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 0.9rem;
        }
        
        .edit-btn {
            background: #e3f2fd;
            color: #1976d2;
        }
        
        .delete-btn {
            background: #ffebee;
            color: #d32f2f;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .modal.active {
            display: flex;
        }
        
        .modal-content {
            background: white;
            border-radius: 12px;
            width: 95%;
            max-width: 500px;
            max-height: 95vh;
            overflow-y: auto;
        }
        
        .modal-header {
            background: linear-gradient(135deg, #4b6cb7 0%, #182848 100%);
            color: white;
            padding: 15px;
            border-radius: 12px 12px 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .modal-header h2 {
            font-size: 1.3rem;
        }
        
        .close-btn {
            background: none;
            border: none;
            color: white;
            font-size: 1.3rem;
            cursor: pointer;
        }
        
        .modal-body {
            padding: 20px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 6px;
            font-weight: 500;
            color: #555;
            font-size: 0.9rem;
        }
        
        .form-group input,
        .form-group select {
            width: 100%;
            padding: 10px 12px;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            font-size: 0.9rem;
        }
        
        .modal-footer {
            padding: 15px 20px;
            border-top: 1px solid #eee;
            display: flex;
            gap: 10px;
        }
        
        .btn {
            padding: 10px 15px;
            border-radius: 8px;
            font-size: 0.9rem;
            font-weight: 500;
            cursor: pointer;
            border: none;
            flex: 1;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #4b6cb7 0%, #182848 100%);
            color: white;
        }
        
        .btn-secondary {
            background: #e9ecef;
            color: #666;
        }
        
        .no-results {
            text-align: center;
            padding: 40px 20px;
            grid-column: 1 / -1;
        }
        
        .no-results i {
            font-size: 3rem;
            color: #ddd;
            margin-bottom: 15px;
        }
        
        .no-results h3 {
            font-size: 1.4rem;
            color: #666;
            margin-bottom: 10px;
        }
        
        .no-results p {
            color: #999;
            font-size: 1rem;
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                text-align: center;
                gap: 15px;
            }
            
            .search-bar {
                width: 100%;
                max-width: 300px;
            }
            
            .search-bar input {
                width: 100%;
            }
            
            .controls {
                flex-direction: column;
                align-items: stretch;
            }
            
            .filter-section {
                justify-content: center;
            }
            
            .add-btn {
                width: 100%;
                justify-content: center;
            }
            
            .inventory-grid {
                grid-template-columns: 1fr;
            }
            
            .logo h1 {
                font-size: 1.5rem;
            }
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 15px;
            }
            
            .card-header {
                padding: 12px;
            }
            
            .laptop-info h3 {
                font-size: 1.1rem;
            }
            
            .spec-item {
                font-size: 0.85rem;
            }
            
            .price {
                font-size: 1.1rem;
            }
            
            .action-btn {
                width: 30px;
                height: 30px;
                font-size: 0.8rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-laptop"></i>
                    <h1>Laptop Inventory</h1>
                </div>
                <div class="search-bar">
                    <input type="text" id="searchInput" placeholder="Search laptops...">
                    <button><i class="fas fa-search"></i></button>
                </div>
            </div>
        </div>
    </header>

    <div class="container">
        <div class="controls">
            <div class="filter-section">
                <label for="statusFilter">Filter:</label>
                <select id="statusFilter">
                    <option value="all">All Status</option>
                    <option value="available">Available</option>
                    <option value="in-use">In Use</option>
                    <option value="maintenance">Maintenance</option>
                </select>
            </div>
            <button class="add-btn" id="addLaptopBtn">
                <i class="fas fa-plus"></i>
                Add Laptop
            </button>
        </div>

        <div class="inventory-grid" id="inventoryGrid">
            <!-- Laptop cards will be dynamically inserted here -->
        </div>
    </div>

    <div class="modal" id="laptopModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="modalTitle">Add New Laptop</h2>
                <button class="close-btn">&times;</button>
            </div>
            <div class="modal-body">
                <form id="laptopForm">
                    <input type="hidden" id="laptopId">
                    <div class="form-group">
                        <label for="brand">Brand</label>
                        <input type="text" id="brand" required>
                    </div>
                    <div class="form-group">
                        <label for="model">Model</label>
                        <input type="text" id="model" required>
                    </div>
                    <div class="form-group">
                        <label for="serialNumber">Serial Number</label>
                        <input type="text" id="serialNumber" required>
                    </div>
                    <div class="form-group">
                        <label for="processor">Processor</label>
                        <input type="text" id="processor" required>
                    </div>
                    <div class="form-group">
                        <label for="ram">RAM</label>
                        <input type="text" id="ram" required>
                    </div>
                    <div class="form-group">
                        <label for="storage">Storage</label>
                        <input type="text" id="storage" required>
                    </div>
                    <div class="form-group">
                        <label for="screenSize">Screen Size</label>
                        <input type="text" id="screenSize" required>
                    </div>
                    <div class="form-group">
                        <label for="price">Price ($)
