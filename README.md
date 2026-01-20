<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>kris.co | AI Shopping Agent | Arc Hackathon 2026</title>
    
    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@400;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <style>
        /* ===== CSS VARIABLES ===== */
        :root {
            /* Primary Colors */
            --primary-50: #eef2ff;
            --primary-100: #e0e7ff;
            --primary-500: #6366f1;
            --primary-600: #4f46e5;
            --primary-700: #4338ca;
            
            /* Supporting Colors */
            --emerald-500: #10b981;
            --emerald-600: #059669;
            --amber-500: #f59e0b;
            --rose-500: #f43f5e;
            --slate-800: #1e293b;
            --slate-600: #475569;
            --slate-400: #94a3b8;
            --slate-200: #e2e8f0;
            --slate-100: #f1f5f9;
            --slate-50: #f8fafc;
            
            /* UI Colors */
            --bg-primary: var(--slate-50);
            --bg-card: white;
            --text-primary: var(--slate-800);
            --text-secondary: var(--slate-600);
            --border-color: var(--slate-200);
            
            /* Spacing */
            --spacing-xs: 0.5rem;
            --spacing-sm: 0.75rem;
            --spacing-md: 1rem;
            --spacing-lg: 1.5rem;
            --spacing-xl: 2rem;
            --spacing-2xl: 3rem;
            
            /* Border Radius */
            --radius-sm: 0.5rem;
            --radius-md: 0.75rem;
            --radius-lg: 1rem;
            --radius-xl: 1.5rem;
            
            /* Shadows */
            --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
            --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
            --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
            --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1);
            --shadow-primary: 0 10px 25px rgba(99, 102, 241, 0.2);
            
            /* Transitions */
            --transition-fast: 150ms cubic-bezier(0.4, 0, 0.2, 1);
            --transition-normal: 250ms cubic-bezier(0.4, 0, 0.2, 1);
            --transition-slow: 350ms cubic-bezier(0.4, 0, 0.2, 1);
            
            /* Z-index layers */
            --z-dropdown: 10;
            --z-modal: 50;
            --z-toast: 100;
        }
        
        /* ===== RESET & BASE STYLES ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.6;
            min-height: 100vh;
            padding: var(--spacing-md);
        }
        
        /* ===== TYPOGRAPHY ===== */
        h1, h2, h3, h4, h5, h6 {
            font-weight: 600;
            line-height: 1.2;
            margin-bottom: var(--spacing-md);
        }
        
        .h1 { font-size: 2.5rem; }
        .h2 { font-size: 2rem; }
        .h3 { font-size: 1.5rem; }
        .h4 { font-size: 1.25rem; }
        
        .text-sm { font-size: 0.875rem; }
        .text-xs { font-size: 0.75rem; }
        .text-lg { font-size: 1.125rem; }
        .text-xl { font-size: 1.25rem; }
        
        .font-bold { font-weight: 700; }
        .font-semibold { font-weight: 600; }
        .font-medium { font-weight: 500; }
        .font-normal { font-weight: 400; }
        
        .text-primary { color: var(--primary-600); }
        .text-secondary { color: var(--text-secondary); }
        .text-muted { color: var(--slate-400); }
        .text-success { color: var(--emerald-500); }
        .text-warning { color: var(--amber-500); }
        .text-danger { color: var(--rose-500); }
        
        /* ===== LAYOUT ===== */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: var(--spacing-xl);
        }
        
        .grid-2 { grid-template-columns: repeat(2, 1fr); }
        .grid-3 { grid-template-columns: repeat(3, 1fr); }
        .grid-4 { grid-template-columns: repeat(4, 1fr); }
        
        .gap-xs { gap: var(--spacing-xs); }
        .gap-sm { gap: var(--spacing-sm); }
        .gap-md { gap: var(--spacing-md); }
        .gap-lg { gap: var(--spacing-lg); }
        .gap-xl { gap: var(--spacing-xl); }
        
        .flex { display: flex; }
        .flex-col { flex-direction: column; }
        .items-center { align-items: center; }
        .items-start { align-items: flex-start; }
        .items-end { align-items: flex-end; }
        .justify-between { justify-content: space-between; }
        .justify-center { justify-content: center; }
        .justify-end { justify-content: flex-end; }
        .flex-wrap { flex-wrap: wrap; }
        .flex-1 { flex: 1; }
        .flex-shrink-0 { flex-shrink: 0; }
        
        /* ===== COMPONENTS ===== */
        .card {
            background: var(--bg-card);
            border-radius: var(--radius-lg);
            padding: var(--spacing-xl);
            box-shadow: var(--shadow-md);
            border: 1px solid var(--border-color);
        }
        
        .card-header {
            padding-bottom: var(--spacing-md);
            border-bottom: 2px solid var(--slate-100);
            margin-bottom: var(--spacing-lg);
        }
        
        .card-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: var(--text-primary);
        }
        
        .card-subtitle {
            font-size: 0.875rem;
            color: var(--text-secondary);
        }
        
        /* Buttons */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: var(--spacing-sm);
            padding: var(--spacing-sm) var(--spacing-lg);
            border-radius: var(--radius-md);
            font-weight: 600;
            font-size: 0.875rem;
            cursor: pointer;
            transition: all var(--transition-normal);
            border: 2px solid transparent;
            white-space: nowrap;
            user-select: none;
            text-decoration: none;
        }
        
        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            pointer-events: none;
        }
        
        .btn-primary {
            background: var(--primary-600);
            color: white;
        }
        
        .btn-primary:hover:not(:disabled) {
            background: var(--primary-700);
            transform: translateY(-1px);
            box-shadow: var(--shadow-lg);
        }
        
        .btn-outline {
            background: transparent;
            border-color: var(--slate-300);
            color: var(--text-primary);
        }
        
        .btn-outline:hover:not(:disabled) {
            border-color: var(--primary-500);
            color: var(--primary-600);
        }
        
        .btn-success {
            background: var(--emerald-600);
            color: white;
        }
        
        .btn-success:hover:not(:disabled) {
            background: #0da271;
            transform: translateY(-1px);
            box-shadow: var(--shadow-lg);
        }
        
        .btn-sm {
            padding: 0.375rem 0.75rem;
            font-size: 0.75rem;
        }
        
        .btn-lg {
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
        }
        
        .btn-block {
            width: 100%;
        }
        
        /* Badges */
        .badge {
            display: inline-flex;
            align-items: center;
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        
        .badge-success {
            background-color: #d1fae5;
            color: #065f46;
        }
        
        .badge-warning {
            background-color: #fef3c7;
            color: #92400e;
        }
        
        .badge-info {
            background-color: #dbeafe;
            color: #1e40af;
        }
        
        .badge-primary {
            background-color: #e0e7ff;
            color: #3730a3;
        }
        
        /* Inputs */
        .input {
            width: 100%;
            padding: var(--spacing-sm) var(--spacing-md);
            border: 2px solid var(--border-color);
            border-radius: var(--radius-md);
            font-size: 1rem;
            transition: all var(--transition-fast);
            background: white;
        }
        
        .input:focus {
            outline: none;
            border-color: var(--primary-500);
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
        }
        
        /* ===== HEADER ===== */
        .header {
            grid-column: 1 / -1;
            background: linear-gradient(135deg, var(--primary-500), var(--primary-700));
            color: white;
            padding: var(--spacing-xl);
            border-radius: var(--radius-xl);
            margin-bottom: var(--spacing-xl);
            box-shadow: var(--shadow-primary);
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%234f46e5' fill-opacity='0.05' fill-rule='evenodd'/%3E%3C/svg%3E");
            opacity: 0.1;
        }
        
        .brand {
            display: flex;
            align-items: center;
            gap: var(--spacing-md);
            position: relative;
            z-index: 1;
        }
        
        .brand-logo {
            font-family: 'Baloo 2', cursive;
            font-size: 2rem;
            font-weight: 700;
            letter-spacing: -0.5px;
            animation: pulse 2s infinite;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        @keyframes pulse {
            0%, 100% { 
                transform: scale(1);
                opacity: 1; 
            }
            50% { 
                transform: scale(1.02);
                opacity: 0.9; 
            }
        }
        
        .balance-chip {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            padding: var(--spacing-sm) var(--spacing-lg);
            border-radius: 9999px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
            border: 1px solid rgba(255, 255, 255, 0.2);
            position: relative;
            z-index: 1;
        }
        
        /* ===== CHAT SECTION ===== */
        .chat-container {
            display: flex;
            flex-direction: column;
            height: 600px;
        }
        
        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: var(--spacing-md);
            background: var(--slate-100);
            border-radius: var(--radius-lg);
            margin-bottom: var(--spacing-lg);
            display: flex;
            flex-direction: column;
            gap: var(--spacing-md);
            scroll-behavior: smooth;
        }
        
        .message {
            max-width: 85%;
            padding: var(--spacing-md) var(--spacing-lg);
            border-radius: var(--radius-lg);
            line-height: 1.5;
            animation: slideIn 0.3s ease;
            position: relative;
        }
        
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .message-user {
            align-self: flex-end;
            background: var(--primary-600);
            color: white;
            border-bottom-right-radius: var(--radius-sm);
        }
        
        .message-user::after {
            content: '';
            position: absolute;
            right: -8px;
            top: 20px;
            border-left: 8px solid var(--primary-600);
            border-top: 8px solid transparent;
            border-bottom: 8px solid transparent;
        }
        
        .message-ai {
            align-self: flex-start;
            background: white;
            color: var(--text-primary);
            border: 1px solid var(--border-color);
            border-bottom-left-radius: var(--radius-sm);
            box-shadow: var(--shadow-sm);
        }
        
        .message-ai::before {
            content: '';
            position: absolute;
            left: -8px;
            top: 20px;
            border-right: 8px solid white;
            border-top: 8px solid transparent;
            border-bottom: 8px solid transparent;
        }
        
        .message-ai::after {
            content: '';
            position: absolute;
            left: -9px;
            top: 20px;
            border-right: 8px solid var(--border-color);
            border-top: 8px solid transparent;
            border-bottom: 8px solid transparent;
        }
        
        .message-system {
            align-self: center;
            background: var(--primary-50);
            color: var(--primary-600);
            font-size: 0.875rem;
            max-width: 90%;
            text-align: center;
            border: 1px solid var(--primary-100);
        }
        
        .message-ai .product-mention {
            color: var(--primary-600);
            font-weight: 600;
            background: var(--primary-50);
            padding: 2px 6px;
            border-radius: 4px;
            margin: 0 2px;
        }
        
        .typing-indicator {
            display: flex;
            align-items: center;
            gap: 4px;
            padding: 12px 16px;
            background: white;
            border-radius: var(--radius-lg);
            border: 1px solid var(--border-color);
            align-self: flex-start;
            width: fit-content;
        }
        
        .typing-dot {
            width: 8px;
            height: 8px;
            background: var(--slate-400);
            border-radius: 50%;
            animation: typing 1.4s infinite ease-in-out;
        }
        
        .typing-dot:nth-child(1) { animation-delay: -0.32s; }
        .typing-dot:nth-child(2) { animation-delay: -0.16s; }
        
        @keyframes typing {
            0%, 80%, 100% { transform: scale(0); }
            40% { transform: scale(1); }
        }
        
        /* ===== PRODUCTS GRID ===== */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
            gap: var(--spacing-lg);
            margin-top: var(--spacing-lg);
        }
        
        .product-card {
            background: white;
            border-radius: var(--radius-lg);
            overflow: hidden;
            border: 1px solid var(--border-color);
            transition: all var(--transition-normal);
            cursor: pointer;
            position: relative;
        }
        
        .product-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow-lg);
            border-color: var(--primary-500);
        }
        
        .product-card.selected {
            border-color: var(--primary-500);
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.2);
        }
        
        .product-image {
            height: 160px;
            background: linear-gradient(135deg, var(--primary-50), var(--primary-100));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: var(--primary-600);
            position: relative;
            overflow: hidden;
        }
        
        .product-image::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(to bottom, transparent 50%, rgba(0,0,0,0.05));
        }
        
        .product-info {
            padding: var(--spacing-lg);
        }
        
        .product-price {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-600);
            margin: var(--spacing-sm) 0;
        }
        
        .product-original-price {
            text-decoration: line-through;
            color: var(--slate-400);
            font-size: 0.875rem;
        }
        
        .product-rating {
            display: flex;
            align-items: center;
            gap: 4px;
            color: var(--amber-500);
            font-size: 0.875rem;
            margin-top: var(--spacing-xs);
        }
        
        /* ===== PAYMENT PANEL ===== */
        .payment-summary {
            background: var(--slate-50);
            border-radius: var(--radius-lg);
            padding: var(--spacing-lg);
            margin-bottom: var(--spacing-lg);
            border: 1px solid var(--border-color);
        }
        
        .payment-row {
            display: flex;
            justify-content: space-between;
            padding: var(--spacing-sm) 0;
            border-bottom: 1px solid var(--border-color);
        }
        
        .payment-row:last-child {
            border-bottom: none;
            font-weight: 700;
            font-size: 1.125rem;
            padding-top: var(--spacing-md);
            margin-top: var(--spacing-xs);
            border-top: 2px solid var(--border-color);
        }
        
        /* Payment Options */
        .payment-options {
            margin-top: var(--spacing-lg);
            padding-top: var(--spacing-lg);
            border-top: 1px solid var(--border-color);
        }
        
        .payment-option {
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
            padding: var(--spacing-sm);
            border-radius: var(--radius-md);
            cursor: pointer;
            transition: all var(--transition-fast);
            margin-bottom: var(--spacing-xs);
        }
        
        .payment-option:hover {
            background: var(--slate-50);
        }
        
        .payment-option.selected {
            background: var(--primary-50);
            border: 1px solid var(--primary-100);
        }
        
        .payment-option input[type="radio"] {
            accent-color: var(--primary-600);
        }
        
        /* ===== TRANSACTIONS ===== */
        .transactions-list {
            max-height: 300px;
            overflow-y: auto;
            margin-top: var(--spacing-md);
        }
        
        .transaction-item {
            display: flex;
            align-items: center;
            padding: var(--spacing-md);
            border-bottom: 1px solid var(--border-color);
            gap: var(--spacing-md);
            transition: all var(--transition-fast);
        }
        
        .transaction-item:hover {
            background: var(--slate-50);
        }
        
        .transaction-item:last-child {
            border-bottom: none;
        }
        
        .transaction-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1rem;
            flex-shrink: 0;
        }
        
        /* ===== MODALS ===== */
        .modal-overlay {
            position: fixed;
            inset: 0;
            background: rgba(15, 23, 42, 0.6);
            backdrop-filter: blur(4px);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: var(--z-modal);
            padding: var(--spacing-md);
            animation: fadeIn 0.2s ease;
        }
        
        .modal-overlay.active {
            display: flex;
        }
        
        .modal {
            background: white;
            border-radius: var(--radius-xl);
            width: 100%;
            max-width: 500px;
            padding: var(--spacing-xl);
            box-shadow: var(--shadow-xl);
            animation: slideUp 0.3s ease;
            max-height: 90vh;
            overflow-y: auto;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: var(--spacing-lg);
        }
        
        .modal-close {
            background: none;
            border: none;
            font-size: 1.5rem;
            color: var(--slate-400);
            cursor: pointer;
            padding: var(--spacing-xs);
            border-radius: var(--radius-sm);
            transition: all var(--transition-fast);
        }
        
        .modal-close:hover {
            color: var(--slate-600);
            background: var(--slate-100);
        }
        
        /* ===== TOAST NOTIFICATIONS ===== */
        .toast-container {
            position: fixed;
            top: var(--spacing-xl);
            right: var(--spacing-xl);
            z-index: var(--z-toast);
            display: flex;
            flex-direction: column;
            gap: var(--spacing-sm);
        }
        
        .toast {
            background: white;
            border-radius: var(--radius-md);
            padding: var(--spacing-md) var(--spacing-lg);
            box-shadow: var(--shadow-lg);
            border-left: 4px solid var(--primary-600);
            display: flex;
            align-items: center;
            gap: var(--spacing-md);
            animation: slideInRight 0.3s ease;
            max-width: 350px;
        }
        
        @keyframes slideInRight {
            from {
                opacity: 0;
                transform: translateX(100%);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }
        
        .toast-success {
            border-left-color: var(--emerald-500);
        }
        
        .toast-warning {
            border-left-color: var(--amber-500);
        }
        
        .toast-error {
            border-left-color: var(--rose-500);
        }
        
        .toast-icon {
            font-size: 1.25rem;
        }
        
        /* ===== INVOICE PREVIEW ===== */
        .invoice-preview {
            background: white;
            border: 1px solid var(--border-color);
            border-radius: var(--radius-lg);
            padding: var(--spacing-xl);
            margin-bottom: var(--spacing-lg);
        }
        
        .invoice-header {
            text-align: center;
            margin-bottom: var(--spacing-xl);
            border-bottom: 2px solid var(--primary-100);
            padding-bottom: var(--spacing-lg);
        }
        
        .invoice-details {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: var(--spacing-lg);
            margin-bottom: var(--spacing-xl);
        }
        
        .invoice-table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: var(--spacing-xl);
        }
        
        .invoice-table th {
            text-align: left;
            padding: var(--spacing-sm) var(--spacing-md);
            background: var(--slate-50);
            border-bottom: 2px solid var(--border-color);
        }
        
        .invoice-table td {
            padding: var(--spacing-sm) var(--spacing-md);
            border-bottom: 1px solid var(--border-color);
        }
        
        .invoice-table tr:last-child td {
            border-bottom: none;
        }
        
        .invoice-total {
            text-align: right;
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--primary-600);
            margin-top: var(--spacing-lg);
        }
        
        /* ===== UTILITY CLASSES ===== */
        .w-full { width: 100%; }
        .h-full { height: 100%; }
        .mt-1 { margin-top: 0.25rem; }
        .mt-2 { margin-top: 0.5rem; }
        .mt-4 { margin-top: 1rem; }
        .mt-6 { margin-top: 1.5rem; }
        .mb-1 { margin-bottom: 0.25rem; }
        .mb-2 { margin-bottom: 0.5rem; }
        .mb-4 { margin-bottom: 1rem; }
        .mb-6 { margin-bottom: 1.5rem; }
        .ml-auto { margin-left: auto; }
        .text-center { text-align: center; }
        .hidden { display: none !important; }
        .visible { display: block !important; }
        
        /* ===== RESPONSIVE DESIGN ===== */
        @media (max-width: 1024px) {
            .container {
                grid-template-columns: 1fr;
            }
            
            .products-grid {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            }
            
            .invoice-details {
                grid-template-columns: 1fr;
            }
        }
        
        @media (max-width: 768px) {
            body {
                padding: var(--spacing-sm);
            }
            
            .header {
                flex-direction: column;
                gap: var(--spacing-md);
                text-align: center;
            }
            
            .brand-logo {
                font-size: 1.75rem;
            }
            
            .products-grid {
                grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
            }
            
            .chat-container {
                height: 500px;
            }
            
            .h1 { font-size: 2rem; }
            .h2 { font-size: 1.75rem; }
            .h3 { font-size: 1.25rem; }
            
            .toast-container {
                top: var(--spacing-md);
                right: var(--spacing-md);
                left: var(--spacing-md);
            }
            
            .toast {
                max-width: 100%;
            }
        }
        
        @media (max-width: 480px) {
            .products-grid {
                grid-template-columns: 1fr;
            }
            
            .card {
                padding: var(--spacing-lg);
            }
            
            .modal {
                padding: var(--spacing-lg);
            }
        }
    </style>
</head>
<body>
    <!-- Toast Notifications Container -->
    <div class="toast-container" id="toastContainer"></div>

    <div class="container">
        <!-- Header -->
        <header class="header flex items-center justify-between">
            <div class="brand">
                <div class="brand-logo">kris.co</div>
                <span class="text-sm font-medium opacity-90">AI Shopping Agent • Arc Hackathon 2026</span>
            </div>
            
            <div class="flex items-center gap-lg">
                <div class="balance-chip">
                    <i class="fas fa-wallet"></i>
                    <span id="usdcBalance">1,250.00 USDC</span>
                </div>
                
                <div class="flex gap-sm">
                    <button class="btn btn-outline" onclick="Demo.reset()" title="Reset demo">
                        <i class="fas fa-redo"></i> Reset
                    </button>
                    <button class="btn btn-primary" onclick="Demo.toggleMode()" title="Toggle developer mode">
                        <i class="fas fa-code"></i> <span id="modeText">Dev Mode</span>
                    </button>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="card">
            <div class="card-header">
                <h2 class="card-title flex items-center gap-sm">
                    <i class="fas fa-robot text-primary"></i>
                    AI Shopping Assistant
                </h2>
                <p class="card-subtitle">Powered by Google Gemini & Arc • Real-time USDC payments</p>
            </div>
            
            <div class="chat-container">
                <div class="chat-messages" id="chatMessages">
                    <!-- Messages will be added by JavaScript -->
                </div>
                
                <div class="flex gap-sm">
                    <input type="text" 
                           class="input flex-1" 
                           id="chatInput"
                           placeholder="Ask me to find products, negotiate prices, or make purchases... (Try: 'Find wireless headphones under $100')"
                           onkeydown="if(event.key === 'Enter') Chat.sendMessage()">
                    <button class="btn btn-primary" onclick="Chat.sendMessage()" title="Send message">
                        <i class="fas fa-paper-plane"></i>
                    </button>
                </div>
            </div>
        </main>

        <!-- Sidebar -->
        <aside class="flex flex-col gap-xl">
            <!-- Payment Panel -->
            <div class="card">
                <div class="card-header">
                    <h3 class="card-title flex items-center gap-sm">
                        <i class="fas fa-bolt text-success"></i>
                        Arc Payment
                    </h3>
                </div>
                
                <div class="payment-summary">
                    <div class="payment-row">
                        <span class="text-secondary">Product:</span>
                        <span id="paymentProduct" class="font-medium">None selected</span>
                    </div>
                    <div class="payment-row">
                        <span class="text-secondary">Price:</span>
                        <span id="paymentPrice" class="font-medium">0.00 USDC</span>
                    </div>
                    <div class="payment-row">
                        <span class="text-secondary">Arc Fee (0.3%):</span>
                        <span id="paymentFee" class="font-medium">0.00 USDC</span>
                    </div>
                    <div class="payment-row">
                        <span class="font-semibold">Total:</span>
                        <span id="paymentTotal" class="font-bold text-primary">0.00 USDC</span>
                    </div>
                </div>
                
                <div class="payment-options">
                    <div class="text-sm font-medium text-secondary mb-2">Payment Method:</div>
                    <label class="payment-option" id="optionArc">
                        <input type="radio" name="paymentMethod" value="arc" checked>
                        <i class="fas fa-bolt text-success"></i>
                        <span class="flex-1">USDC via Arc</span>
                        <span class="text-xs badge badge-success">Recommended</span>
                    </label>
                    <label class="payment-option">
                        <input type="radio" name="paymentMethod" value="card">
                        <i class="fas fa-credit-card text-primary"></i>
                        <span class="flex-1">Credit/Debit Card</span>
                    </label>
                    <label class="payment-option">
                        <input type="radio" name="paymentMethod" value="crypto">
                        <i class="fas fa-wallet text-warning"></i>
                        <span class="flex-1">Crypto Wallet</span>
                    </label>
                </div>
                
                <div class="flex flex-col gap-sm mt-4">
                    <button class="btn btn-success btn-lg btn-block" 
                            id="payButton" 
                            disabled 
                            onclick="Payment.process()"
                            title="Proceed to payment">
                        <i class="fas fa-lock"></i> Pay Now
                    </button>
                    
                    <div class="text-center text-xs text-muted">
                        <i class="fas fa-bolt"></i> Sub-second settlement • 0.3% fee
                    </div>
                </div>
            </div>

            <!-- Budget Panel -->
            <div class="card">
                <div class="card-header">
                    <h3 class="card-title flex items-center gap-sm">
                        <i class="fas fa-chart-pie"></i>
                        Budget Overview
                    </h3>
                </div>
                
                <div class="flex justify-center mb-4">
                    <canvas id="budgetChart" width="250" height="250"></canvas>
                </div>
                
                <div class="grid grid-3 gap-sm">
                    <div class="text-center">
                        <div class="text-xl font-bold text-primary" id="budgetUsed">$245.50</div>
                        <div class="text-xs text-muted">Spent</div>
                    </div>
                    <div class="text-center">
                        <div class="text-xl font-bold text-primary" id="budgetRemaining">$1,004.50</div>
                        <div class="text-xs text-muted">Remaining</div>
                    </div>
                    <div class="text-center">
                        <div class="text-xl font-bold text-success" id="budgetSaved">$58.75</div>
                        <div class="text-xs text-muted">Saved</div>
                    </div>
                </div>
                
                <div class="mt-4 pt-4 border-t border-border-color">
                    <button class="btn btn-outline btn-sm w-full" onclick="Invoice.downloadAll()" title="Download all invoices">
                        <i class="fas fa-file-download"></i> Download All Invoices
                    </button>
                </div>
            </div>

            <!-- Transaction History -->
            <div class="card flex-1">
                <div class="card-header">
                    <h3 class="card-title flex items-center gap-sm">
                        <i class="fas fa-history"></i>
                        Recent Transactions
                    </h3>
                    <button class="btn btn-outline btn-sm ml-auto" onclick="Invoice.viewAll()" title="View all invoices">
                        <i class="fas fa-receipt"></i> Invoices
                    </button>
                </div>
                
                <div class="transactions-list" id="transactionsList">
                    <!-- Transactions will be added by JavaScript -->
                </div>
            </div>
        </aside>

        <!-- Products Section -->
        <section class="card" style="grid-column: 1 / -1; margin-top: var(--spacing-xl);">
            <div class="card-header flex items-center justify-between">
                <h2 class="card-title flex items-center gap-sm">
                    <i class="fas fa-shopping-bag"></i>
                    Recommended Products
                </h2>
                <span class="badge badge-primary">
                    <span id="productCount">6</span> products
                </span>
            </div>
            
            <div class="products-grid" id="productsGrid">
                <!-- Products will be added by JavaScript -->
            </div>
        </section>

        <!-- Footer -->
        <footer class="text-center text-muted text-sm" style="grid-column: 1 / -1; margin-top: var(--spacing-xl); padding-top: var(--spacing-xl); border-top: 1px solid var(--border-color);">
            <p>kris.co AI Shopping Agent Demo • Arc Hackathon 2026 • Powered by Google Gemini & Arc with USDC settlement</p>
            <p class="mt-2">This is a frontend simulation demonstrating AI agent commerce with real-time Arc payments</p>
            <div class="mt-4 flex justify-center gap-4">
                <button class="btn btn-outline btn-sm" onclick="Demo.showHelp()">
                    <i class="fas fa-question-circle"></i> Help Guide
                </button>
                <button class="btn btn-outline btn-sm" onclick="Demo.exportData()">
                    <i class="fas fa-download"></i> Export Data
                </button>
                <button class="btn btn-outline btn-sm" onclick="Demo.viewStatistics()">
                    <i class="fas fa-chart-bar"></i> Statistics
                </button>
            </div>
        </footer>
    </div>

    <!-- Modals -->
    <div class="modal-overlay" id="negotiationModal">
        <div class="modal">
            <div class="modal-header">
                <h3 class="h3">Negotiate Price</h3>
                <button class="modal-close" onclick="Modal.close('negotiation')">&times;</button>
            </div>
            
            <div class="mb-6">
                <div class="text-sm text-muted mb-2">Select negotiation strategy for:</div>
                <div class="font-semibold text-lg text-primary" id="negotiationProductName"></div>
                <div class="text-sm text-muted mt-1">Seller: <span id="negotiationSeller"></span></div>
            </div>
            
            <div class="flex flex-col gap-sm mb-6">
                <label class="payment-option selected">
                    <input type="radio" name="negotiationStrategy" value="auto" checked class="text-primary">
                    <i class="fas fa-robot text-primary"></i>
                    <span class="flex-1">
                        <div class="font-medium">Auto Negotiation</div>
                        <div class="text-xs text-muted">Let AI decide best approach</div>
                    </span>
                </label>
                <label class="payment-option">
                    <input type="radio" name="negotiationStrategy" value="5" class="text-primary">
                    <i class="fas fa-percentage text-primary"></i>
                    <span class="flex-1">
                        <div class="font-medium">5% Discount</div>
                        <div class="text-xs text-muted">Request 5% off the price</div>
                    </span>
                </label>
                <label class="payment-option">
                    <input type="radio" name="negotiationStrategy" value="10" class="text-primary">
                    <i class="fas fa-percentage text-primary"></i>
                    <span class="flex-1">
                        <div class="font-medium">10% Discount</div>
                        <div class="text-xs text-muted">Request 10% off the price</div>
                    </span>
                </label>
                <label class="payment-option">
                    <input type="radio" name="negotiationStrategy" value="best" class="text-primary">
                    <i class="fas fa-trophy text-warning"></i>
                    <span class="flex-1">
                        <div class="font-medium">Best Possible Offer</div>
                        <div class="text-xs text-muted">Get the highest possible discount</div>
                    </span>
                </label>
            </div>
            
            <div class="flex gap-sm justify-end">
                <button class="btn btn-outline" onclick="Modal.close('negotiation')">Cancel</button>
                <button class="btn btn-primary" onclick="ProductsController.startNegotiation()">
                    <i class="fas fa-comments-dollar"></i> Start Negotiation
                </button>
            </div>
        </div>
    </div>

    <div class="modal-overlay" id="paymentModal">
        <div class="modal">
            <div class="modal-header">
                <h3 class="h3">Confirm Payment</h3>
                <button class="modal-close" onclick="Modal.close('payment')">&times;</button>
            </div>
            
            <div class="mb-6">
                <div class="text-center mb-4">
                    <div class="text-lg font-semibold text-primary" id="confirmProduct"></div>
                    <div class="text-sm text-muted mt-1">Transaction ID: <span id="confirmTransactionId"></span></div>
                </div>
                
                <div class="invoice-preview">
                    <div class="flex justify-between mb-3">
                        <span class="text-muted">Product Amount:</span>
                        <span id="confirmAmount" class="font-medium"></span>
                    </div>
                    <div class="flex justify-between mb-3">
                        <span class="text-muted">Arc Fee (0.3%):</span>
                        <span id="confirmFee" class="font-medium"></span>
                    </div>
                    <div class="flex justify-between mb-3">
                        <span class="text-muted">Network Fee:</span>
                        <span class="font-medium">0.50 USDC</span>
                    </div>
                    <div class="flex justify-between pt-3 border-t">
                        <span class="font-semibold">Total Amount:</span>
                        <span id="confirmTotal" class="font-bold text-lg text-primary"></span>
                    </div>
                </div>
                
                <div class="flex items-center gap-sm mt-4 p-3 bg-slate-50 rounded-lg">
                    <i class="fas fa-info-circle text-primary"></i>
                    <div class="text-sm text-muted">
                        <div class="font-medium">Payment Method:</div>
                        <div id="confirmMethod">USDC via Arc</div>
                    </div>
                </div>
            </div>
            
            <div class="text-xs text-muted mb-6">
                <i class="fas fa-shield-alt mr-1"></i>
                Payment will be processed via Arc with sub-second settlement
            </div>
            
            <div class="flex gap-sm justify-end">
                <button class="btn btn-outline" onclick="Modal.close('payment')">Cancel</button>
                <button class="btn btn-success" onclick="Payment.confirm()">
                    <i class="fas fa-check"></i> Confirm & Pay
                </button>
            </div>
        </div>
    </div>

    <div class="modal-overlay" id="invoiceModal">
        <div class="modal" style="max-width: 800px;">
            <div class="modal-header">
                <h3 class="h3">Invoice Details</h3>
                <button class="modal-close" onclick="Modal.close('invoice')">&times;</button>
            </div>
            
            <div class="invoice-preview" id="invoicePreview">
                <!-- Invoice content will be inserted here -->
            </div>
            
            <div class="flex gap-sm justify-end mt-6">
                <button class="btn btn-outline" onclick="Modal.close('invoice')">Close</button>
                <button class="btn btn-primary" onclick="Invoice.downloadCurrent()">
                    <i class="fas fa-download"></i> Download Invoice
                </button>
                <button class="btn btn-success" onclick="Invoice.print()">
                    <i class="fas fa-print"></i> Print Invoice
                </button>
            </div>
        </div>
    </div>

    <div class="modal-overlay" id="invoicesModal">
        <div class="modal" style="max-width: 800px;">
            <div class="modal-header">
                <h3 class="h3">All Invoices</h3>
                <button class="modal-close" onclick="Modal.close('invoices')">&times;</button>
            </div>
            
            <div class="mb-6">
                <div class="flex items-center justify-between mb-4">
                    <div class="text-lg font-semibold">
                        <span id="invoiceCount">0</span> Invoices Generated
                    </div>
                    <button class="btn btn-primary btn-sm" onclick="Invoice.downloadAll()">
                        <i class="fas fa-download"></i> Download All
                    </button>
                </div>
                
                <div class="transactions-list" id="invoicesList" style="max-height: 400px;">
                    <!-- Invoices list will be inserted here -->
                </div>
            </div>
            
            <div class="flex gap-sm justify-end">
                <button class="btn btn-outline" onclick="Modal.close('invoices')">Close</button>
            </div>
        </div>
    </div>

    <div class="modal-overlay" id="helpModal">
        <div class="modal" style="max-width: 700px;">
            <div class="modal-header">
                <h3 class="h3">Help Guide - How to Use kris.co</h3>
                <button class="modal-close" onclick="Modal.close('help')">&times;</button>
            </div>
            
            <div class="space-y-4">
                <div class="p-4 bg-slate-50 rounded-lg">
                    <h4 class="font-semibold text-primary mb-2"><i class="fas fa-shopping-cart mr-2"></i>1. Browse Products</h4>
                    <p class="text-sm text-muted">Click on any product card to select it for purchase. Each product shows the current price, original price, and discount percentage.</p>
                </div>
                
                <div class="p-4 bg-slate-50 rounded-lg">
                    <h4 class="font-semibold text-primary mb-2"><i class="fas fa-comments-dollar mr-2"></i>2. Negotiate Prices</h4>
                    <p class="text-sm text-muted">Click the "Negotiate" button on any product to try to get a better price. Choose from different negotiation strategies to maximize your savings.</p>
                </div>
                
                <div class="p-4 bg-slate-50 rounded-lg">
                    <h4 class="font-semibold text-primary mb-2"><i class="fas fa-bolt mr-2"></i>3. Make Payments</h4>
                    <p class="text-sm text-muted">After selecting a product, choose your payment method (USDC via Arc recommended) and click "Pay Now". Confirm the payment in the modal.</p>
                </div>
                
                <div class="p-4 bg-slate-50 rounded-lg">
                    <h4 class="font-semibold text-primary mb-2"><i class="fas fa-file-invoice mr-2"></i>4. Download Invoices</h4>
                    <p class="text-sm text-muted">After each purchase, download the invoice as a PDF. You can also view and download all invoices from the "Invoices" button.</p>
                </div>
                
                <div class="p-4 bg-slate-50 rounded-lg">
                    <h4 class="font-semibold text-primary mb-2"><i class="fas fa-robot mr-2"></i>5. Chat with AI Assistant</h4>
                    <p class="text-sm text-muted">Use the chat interface to ask for product recommendations, check your budget, or get help with payments.</p>
                </div>
            </div>
            
            <div class="flex gap-sm justify-end mt-6">
                <button class="btn btn-primary" onclick="Modal.close('help')">
                    <i class="fas fa-check"></i> Got it!
                </button>
            </div>
        </div>
    </div>

    <script>
        // ===== APPLICATION STATE =====
        const State = {
            usdcBalance: 1250.00,
            budgetTotal: 1250.00,
            spent: 245.50,
            saved: 58.75,
            selectedProduct: null,
            devMode: false,
            isNegotiating: false,
            negotiationProductId: null,
            budgetChart: null,
            invoices: [],
            currentInvoice: null
        };

        // ===== DATA MODELS =====
        const Products = [
            {
                id: 1,
                name: "Wireless Mechanical Keyboard",
                price: 89.99,
                originalPrice: 99.99,
                category: "Electronics",
                emoji: "⌨️",
                seller: "TechGadgets Inc.",
                rating: 4.5,
                description: "Mechanical keyboard with wireless connectivity and RGB lighting"
            },
            {
                id: 2,
                name: "Noise Cancelling Headphones",
                price: 149.99,
                originalPrice: 199.99,
                category: "Electronics",
                emoji: "🎧",
                seller: "AudioPro",
                rating: 4.8,
                description: "Premium noise cancelling headphones with 30-hour battery"
            },
            {
                id: 3,
                name: "Smart Fitness Watch",
                price: 199.99,
                originalPrice: 249.99,
                category: "Wearables",
                emoji: "⌚",
                seller: "FitTech",
                rating: 4.3,
                description: "Advanced fitness tracker with heart rate monitoring"
            },
            {
                id: 4,
                name: "Portable SSD 1TB",
                price: 79.99,
                originalPrice: 89.99,
                category: "Computer",
                emoji: "💾",
                seller: "StorageMasters",
                rating: 4.7,
                description: "High-speed portable SSD with 1TB storage"
            },
            {
                id: 5,
                name: "Ergonomic Office Chair",
                price: 249.99,
                originalPrice: 299.99,
                category: "Furniture",
                emoji: "💺",
                seller: "HomeOffice Co.",
                rating: 4.6,
                description: "Premium ergonomic chair with lumbar support"
            },
            {
                id: 6,
                name: "USB-C Hub (7-in-1)",
                price: 34.99,
                originalPrice: 39.99,
                category: "Accessories",
                emoji: "🔌",
                seller: "ConnectTech",
                rating: 4.4,
                description: "7-port USB-C hub with HDMI, USB, and card readers"
            }
        ];

        // Load transactions from localStorage or use default
        const loadTransactions = () => {
            const saved = localStorage.getItem('krisco_transactions');
            if (saved) {
                return JSON.parse(saved);
            }
            return [
                { 
                    id: 1, 
                    title: "Wireless Earbuds", 
                    amount: 79.99, 
                    time: "10 min ago", 
                    status: "success", 
                    type: "purchase",
                    invoiceId: "INV-2024-001"
                },
                { 
                    id: 2, 
                    title: "Price Negotiation", 
                    amount: 15.50, 
                    time: "45 min ago", 
                    status: "success", 
                    type: "savings" 
                },
                { 
                    id: 3, 
                    title: "Laptop Stand", 
                    amount: 39.99, 
                    time: "2 hours ago", 
                    status: "success", 
                    type: "purchase",
                    invoiceId: "INV-2024-002"
                },
                { 
                    id: 4, 
                    title: "Webcam 1080p", 
                    amount: 59.99, 
                    time: "1 day ago", 
                    status: "success", 
                    type: "purchase",
                    invoiceId: "INV-2024-003"
                },
                { 
                    id: 5, 
                    title: "Price Negotiation", 
                    amount: 22.25, 
                    time: "2 days ago", 
                    status: "success", 
                    type: "savings" 
                }
            ];
        };

        let Transactions = loadTransactions();

        // Load invoices from localStorage or use default
        const loadInvoices = () => {
            const saved = localStorage.getItem('krisco_invoices');
            if (saved) {
                return JSON.parse(saved);
            }
            return [];
        };

        State.invoices = loadInvoices();

        // ===== UTILITY FUNCTIONS =====
        const Utils = {
            formatCurrency(amount) {
                return `$${amount.toFixed(2)}`;
            },
            
            formatUSDC(amount) {
                return `${amount.toFixed(2)} USDC`;
            },
            
            randomDelay(min = 500, max = 1500) {
                return Math.floor(Math.random() * (max - min + 1)) + min;
            },
            
            generateTransactionId() {
                const timestamp = Date.now();
                const random = Math.floor(Math.random() * 10000);
                return `TXN-${timestamp}-${random.toString().padStart(4, '0')}`;
            },
            
            generateInvoiceId() {
                const count = State.invoices.length + 1;
                return `INV-2024-${count.toString().padStart(3, '0')}`;
            },
            
            generateHash(length = 16) {
                return Array.from({length}, () => 
                    Math.floor(Math.random() * 16).toString(16)
                ).join('');
            },
            
            formatDate(date = new Date()) {
                return date.toLocaleDateString('en-US', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric',
                    hour: '2-digit',
                    minute: '2-digit'
                });
            },
            
            saveToStorage() {
                localStorage.setItem('krisco_transactions', JSON.stringify(Transactions));
                localStorage.setItem('krisco_invoices', JSON.stringify(State.invoices));
            }
        };

        // ===== TOAST NOTIFICATIONS =====
        const Toast = {
            show(message, type = 'info', duration = 3000) {
                const container = document.getElementById('toastContainer');
                const toast = document.createElement('div');
                toast.className = `toast toast-${type}`;
                
                const icons = {
                    info: 'fa-info-circle',
                    success: 'fa-check-circle',
                    warning: 'fa-exclamation-triangle',
                    error: 'fa-times-circle'
                };
                
                toast.innerHTML = `
                    <i class="fas ${icons[type]} toast-icon text-${type === 'info' ? 'primary' : type}"></i>
                    <div class="flex-1">${message}</div>
                    <button class="modal-close btn-sm" onclick="this.parentElement.remove()">&times;</button>
                `;
                
                container.appendChild(toast);
                
                // Auto remove after duration
                setTimeout(() => {
                    if (toast.parentElement) {
                        toast.remove();
                    }
                }, duration);
                
                return toast;
            },
            
            info(message, duration = 3000) {
                return this.show(message, 'info', duration);
            },
            
            success(message, duration = 3000) {
                return this.show(message, 'success', duration);
            },
            
            warning(message, duration = 3000) {
                return this.show(message, 'warning', duration);
            },
            
            error(message, duration = 3000) {
                return this.show(message, 'error', duration);
            }
        };

        // ===== MODAL CONTROLLER =====
        const Modal = {
            open(modalId) {
                const modal = document.getElementById(`${modalId}Modal`);
                if (modal) {
                    modal.classList.add('active');
                    document.body.style.overflow = 'hidden';
                }
            },
            
            close(modalId) {
                const modal = document.getElementById(`${modalId}Modal`);
                if (modal) {
                    modal.classList.remove('active');
                    document.body.style.overflow = '';
                }
            },
            
            closeAll() {
                document.querySelectorAll('.modal-overlay.active').forEach(modal => {
                    modal.classList.remove('active');
                });
                document.body.style.overflow = '';
            }
        };

        // Close modals when clicking outside
        document.addEventListener('click', (e) => {
            if (e.target.classList.contains('modal-overlay')) {
                Modal.closeAll();
            }
        });

        // ===== CHAT CONTROLLER =====
        const Chat = {
            sendMessage() {
                const input = document.getElementById('chatInput');
                const message = input.value.trim();
                
                if (!message) return;
                
                this.addMessage('user', message);
                input.value = '';
                
                // Show typing indicator
                this.showTyping();
                
                // Simulate AI response
                setTimeout(() => {
                    this.hideTyping();
                    this.generateAIResponse(message);
                }, Utils.randomDelay(800, 2000));
            },
            
            addMessage(type, content) {
                const messagesDiv = document.getElementById('chatMessages');
                const messageDiv = document.createElement('div');
                
                messageDiv.className = `message message-${type}`;
                messageDiv.innerHTML = content;
                
                messagesDiv.appendChild(messageDiv);
                messagesDiv.scrollTop = messagesDiv.scrollHeight;
            },
            
            showTyping() {
                const messagesDiv = document.getElementById('chatMessages');
                const typingDiv = document.createElement('div');
                typingDiv.className = 'typing-indicator';
                typingDiv.id = 'typingIndicator';
                typingDiv.innerHTML = `
                    <div class="typing-dot"></div>
                    <div class="typing-dot"></div>
                    <div class="typing-dot"></div>
                    <span class="text-xs text-muted ml-2">AI is thinking...</span>
                `;
                
                messagesDiv.appendChild(typingDiv);
                messagesDiv.scrollTop = messagesDiv.scrollHeight;
            },
            
            hideTyping() {
                const typingDiv = document.getElementById('typingIndicator');
                if (typingDiv) {
                    typingDiv.remove();
                }
            },
            
            generateAIResponse(userMessage) {
                const responses = {
                    'keyboard': `I found the perfect wireless mechanical keyboard! Check out the <span class="product-mention">Wireless Mechanical Keyboard</span> for ${Utils.formatUSDC(89.99)} (10% off). Would you like me to negotiate a better price?`,
                    'headphone': `For noise-cancelling headphones, I recommend the <span class="product-mention">Noise Cancelling Headphones</span> at ${Utils.formatUSDC(149.99)} (25% off). Great deal!`,
                    'budget': `You have ${Utils.formatUSDC(State.usdcBalance)} available. You've spent ${Utils.formatCurrency(State.spent)} and saved ${Utils.formatCurrency(State.saved)} through negotiations.`,
                    'arc': `Arc enables instant USDC payments with predictable 0.3% fees and sub-second settlement. Perfect for AI agent commerce!`,
                    'invoice': `You can download invoices for all your purchases. Click the "Invoices" button in the transaction history panel to view and download them.`,
                    'help': `Here's what I can help you with:<br>
                    1. <strong>Find products</strong> - Ask me to search for specific items<br>
                    2. <strong>Negotiate prices</strong> - Click the negotiate button on any product<br>
                    3. <strong>Make payments</strong> - Select a product and choose your payment method<br>
                    4. <strong>Download invoices</strong> - Get PDF invoices for all purchases`,
                    'default': `I can help you find products, negotiate prices, and process payments via Arc. Try asking about specific products or check the recommendations below!`
                };
                
                const lowerMessage = userMessage.toLowerCase();
                let response = responses.default;
                
                if (lowerMessage.includes('keyboard') || lowerMessage.includes('wireless')) {
                    response = responses.keyboard;
                } else if (lowerMessage.includes('headphone') || lowerMessage.includes('audio')) {
                    response = responses.headphone;
                } else if (lowerMessage.includes('budget') || lowerMessage.includes('balance')) {
                    response = responses.budget;
                } else if (lowerMessage.includes('arc') || lowerMessage.includes('payment')) {
                    response = responses.arc;
                } else if (lowerMessage.includes('invoice') || lowerMessage.includes('receipt')) {
                    response = responses.invoice;
                } else if (lowerMessage.includes('help') || lowerMessage.includes('how to')) {
                    response = responses.help;
                } else if (lowerMessage.includes('hi') || lowerMessage.includes('hello')) {
                    response = `Hello! I'm your AI Shopping Assistant from <strong>kris.co</strong>. How can I help you today?`;
                }
                
                this.addMessage('ai', response);
            },
            
            addSystemMessage(content) {
                this.addMessage('system', `<i class="fas fa-info-circle mr-1"></i> ${content}`);
            }
        };

        // ===== PRODUCTS CONTROLLER =====
        const ProductsController = {
            render() {
                const grid = document.getElementById('productsGrid');
                grid.innerHTML = '';
                
                Products.forEach(product => {
                    const discount = Math.round(((product.originalPrice - product.price) / product.originalPrice) * 100);
                    const discountAmount = product.originalPrice - product.price;
                    
                    const card = document.createElement('div');
                    card.className = `product-card ${State.selectedProduct?.id === product.id ? 'selected' : ''}`;
                    card.setAttribute('data-id', product.id);
                    card.innerHTML = `
                        <div class="product-image">
                            <span>${product.emoji}</span>
                            <div class="absolute top-2 right-2">
                                <span class="badge ${discount >= 20 ? 'badge-success' : 'badge-warning'}">
                                    ${discount}% OFF
                                </span>
                            </div>
                        </div>
                        <div class="product-info">
                            <div class="font-semibold text-sm text-muted mb-1">${product.category}</div>
                            <div class="font-semibold text-lg mb-2 line-clamp-2" title="${product.name}">${product.name}</div>
                            <div class="flex items-center gap-sm mb-2">
                                <div class="product-price">${Utils.formatUSDC(product.price)}</div>
                                <div class="product-original-price">${Utils.formatUSDC(product.originalPrice)}</div>
                            </div>
                            <div class="product-rating">
                                ${'★'.repeat(Math.floor(product.rating))}${'☆'.repeat(5 - Math.floor(product.rating))}
                                <span class="text-muted ml-1">${product.rating}</span>
                            </div>
                            <div class="flex items-center justify-between mb-4 mt-2">
                                <span class="text-xs text-muted">Save ${Utils.formatUSDC(discountAmount)}</span>
                                <span class="text-xs text-muted">${product.seller}</span>
                            </div>
                            <div class="flex gap-sm">
                                <button class="btn btn-outline btn-sm flex-1" onclick="ProductsController.openNegotiation(${product.id})" title="Negotiate price">
                                    <i class="fas fa-comments-dollar"></i> Negotiate
                                </button>
                                <button class="btn btn-primary btn-sm flex-1" onclick="ProductsController.select(${product.id})" title="Buy this product">
                                    <i class="fas fa-shopping-cart"></i> Buy
                                </button>
                            </div>
                        </div>
                    `;
                    
                    grid.appendChild(card);
                });
                
                document.getElementById('productCount').textContent = Products.length;
            },
            
            select(productId) {
                const product = Products.find(p => p.id === productId);
                if (!product) return;
                
                State.selectedProduct = product;
                this.updatePaymentPanel();
                this.render();
                
                Chat.addSystemMessage(`Selected <strong>${product.name}</strong> for ${Utils.formatUSDC(product.price)}. Ready for payment!`);
                
                const payButton = document.getElementById('payButton');
                payButton.disabled = false;
                payButton.innerHTML = `<i class="fas fa-lock"></i> Pay ${Utils.formatUSDC(product.price)}`;
                
                Toast.success(`Selected "${product.name}" for purchase`);
            },
            
            openNegotiation(productId) {
                const product = Products.find(p => p.id === productId);
                if (!product) return;
                
                if (State.isNegotiating) {
                    Toast.warning('Please wait, another negotiation is in progress');
                    return;
                }
                
                State.negotiationProductId = productId;
                document.getElementById('negotiationProductName').textContent = product.name;
                document.getElementById('negotiationSeller').textContent = product.seller;
                Modal.open('negotiation');
            },
            
            startNegotiation() {
                if (State.isNegotiating) return;
                
                const productId = State.negotiationProductId;
                const product = Products.find(p => p.id === productId);
                if (!product) return;
                
                const strategy = document.querySelector('input[name="negotiationStrategy"]:checked').value;
                State.isNegotiating = true;
                
                Modal.close('negotiation');
                Chat.addSystemMessage(`🤖 Negotiating with ${product.seller} for ${product.name}...`);
                
                // Show toast notification
                Toast.info(`Negotiating with ${product.seller}...`);
                
                setTimeout(() => {
                    const successRate = Math.random();
                    let discount = 0;
                    let message = '';
                    
                    // Determine discount based on strategy
                    if (strategy === 'auto') {
                        discount = successRate > 0.7 ? 0.15 : successRate > 0.4 ? 0.08 : 0;
                        message = successRate > 0.7 ? 'Excellent deal!' : successRate > 0.4 ? 'Good negotiation!' : 'Best offer available';
                    } else if (strategy === '5') {
                        discount = successRate > 0.3 ? 0.05 : 0;
                        message = successRate > 0.3 ? '5% discount secured!' : 'Could not secure 5% discount';
                    } else if (strategy === '10') {
                        discount = successRate > 0.5 ? 0.1 : successRate > 0.2 ? 0.05 : 0;
                        message = successRate > 0.5 ? '10% discount secured!' : successRate > 0.2 ? 'Got 5% instead' : 'Could not secure discount';
                    } else if (strategy === 'best') {
                        discount = successRate > 0.8 ? 0.2 : successRate > 0.6 ? 0.15 : successRate > 0.3 ? 0.08 : 0;
                        message = successRate > 0.8 ? 'Best possible deal!' : successRate > 0.6 ? 'Great discount!' : successRate > 0.3 ? 'Moderate discount' : 'Best offer available';
                    }
                    
                    if (discount > 0) {
                        const discountAmount = product.price * discount;
                        const oldPrice = product.price;
                        product.price = parseFloat((product.price - discountAmount).toFixed(2));
                        State.saved += discountAmount;
                        
                        Chat.addSystemMessage(`✅ Success! Got ${(discount * 100).toFixed(0)}% off. New price: ${Utils.formatUSDC(product.price)} (was ${Utils.formatUSDC(oldPrice)})`);
                        Toast.success(`${message} Saved ${Utils.formatUSDC(discountAmount)}!`);
                        
                        UI.updateBudget();
                        
                        // If this product is selected, update payment panel
                        if (State.selectedProduct?.id === productId) {
                            this.updatePaymentPanel();
                        }
                    } else {
                        Chat.addSystemMessage(`❌ ${product.seller} declined the offer. Price remains ${Utils.formatUSDC(product.price)}`);
                        Toast.warning('Could not secure a discount this time');
                    }
                    
                    this.render();
                    State.isNegotiating = false;
                    State.negotiationProductId = null;
                }, 2000);
            },
            
            updatePaymentPanel() {
                if (!State.selectedProduct) {
                    document.getElementById('paymentProduct').textContent = 'None selected';
                    document.getElementById('paymentPrice').textContent = '0.00 USDC';
                    document.getElementById('paymentFee').textContent = '0.00 USDC';
                    document.getElementById('paymentTotal').textContent = '0.00 USDC';
                    return;
                }
                
                const product = State.selectedProduct;
                const arcFee = product.price * 0.003;
                const total = product.price + arcFee;
                
                document.getElementById('paymentProduct').textContent = product.name;
                document.getElementById('paymentPrice').textContent = Utils.formatUSDC(product.price);
                document.getElementById('paymentFee').textContent = Utils.formatUSDC(arcFee);
                document.getElementById('paymentTotal').textContent = Utils.formatUSDC(total);
            }
        };

        // ===== PAYMENT CONTROLLER =====
        const Payment = {
            process() {
                if (!State.selectedProduct) {
                    Toast.error('Please select a product first');
                    return;
                }
                
                const product = State.selectedProduct;
                const arcFee = product.price * 0.003;
                const total = product.price + arcFee;
                const transactionId = Utils.generateTransactionId();
                
                // Get selected payment method
                const paymentMethod = document.querySelector('input[name="paymentMethod"]:checked').value;
                const methodNames = {
                    arc: 'USDC via Arc',
                    card: 'Credit/Debit Card',
                    crypto: 'Crypto Wallet'
                };
                
                // Update confirmation modal
                document.getElementById('confirmProduct').textContent = product.name;
                document.getElementById('confirmAmount').textContent = Utils.formatUSDC(product.price);
                document.getElementById('confirmFee').textContent = Utils.formatUSDC(arcFee);
                document.getElementById('confirmTotal').textContent = Utils.formatUSDC(total);
                document.getElementById('confirmTransactionId').textContent = transactionId;
                document.getElementById('confirmMethod').textContent = methodNames[paymentMethod];
                
                Modal.open('payment');
            },
            
            confirm() {
                if (!State.selectedProduct) return;
                
                const product = State.selectedProduct;
                const arcFee = product.price * 0.003;
                const total = product.price + arcFee;
                const transactionId = Utils.generateTransactionId();
                
                Modal.close('payment');
                
                // Disable pay button during processing
                const payButton = document.getElementById('payButton');
                payButton.disabled = true;
                payButton.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Processing...';
                
                Chat.addSystemMessage(`🔄 Processing ${Utils.formatUSDC(total)} payment via Arc...`);
                Toast.info('Processing payment...');
                
                setTimeout(() => {
                    // Update state
                    State.usdcBalance -= total;
                    State.spent += product.price;
                    
                    // Generate invoice
                    const invoice = this.generateInvoice(product, total, transactionId);
                    State.currentInvoice = invoice;
                    State.invoices.push(invoice);
                    
                    // Add transaction
                    const transaction = {
                        id: Transactions.length + 1,
                        title: product.name,
                        amount: product.price,
                        time: 'Just now',
                        status: 'success',
                        type: 'purchase',
                        invoiceId: invoice.id,
                        transactionId: transactionId
                    };
                    
                    Transactions.unshift(transaction);
                    
                    // Update UI
                    UI.updateBalance();
                    UI.updateBudget();
                    UI.renderTransactions();
                    
                    // Show success messages
                    const txHash = '0x' + Utils.generateHash(64);
                    Chat.addSystemMessage(`✅ Payment settled via Arc in <strong>0.47s</strong>! Transaction: ${txHash.substring(0, 16)}...`);
                    Chat.addSystemMessage(`📦 Order confirmed! ${product.name} will ship within 24 hours.`);
                    
                    // Show invoice download option
                    setTimeout(() => {
                        Toast.success('Payment successful! Download your invoice below.', 5000);
                        this.showInvoiceDownload(invoice);
                    }, 500);
                    
                    // Reset
                    State.selectedProduct = null;
                    ProductsController.render();
                    ProductsController.updatePaymentPanel();
                    
                    // Reset pay button
                    setTimeout(() => {
                        payButton.innerHTML = '<i class="fas fa-lock"></i> Pay Now';
                        payButton.disabled = true;
                    }, 500);
                    
                    // Save to localStorage
                    Utils.saveToStorage();
                    
                }, 1500);
            },
            
            generateInvoice(product, total, transactionId) {
                const invoiceId = Utils.generateInvoiceId();
                const date = new Date();
                const arcFee = product.price * 0.003;
                const networkFee = 0.50;
                
                return {
                    id: invoiceId,
                    transactionId: transactionId,
                    date: date.toISOString(),
                    customer: {
                        name: "Demo User",
                        email: "demo@kris.co",
                        address: "123 Demo Street, San Francisco, CA 94107"
                    },
                    merchant: {
                        name: "kris.co AI Shopping",
                        address: "456 Innovation Blvd, San Francisco, CA 94107",
                        email: "support@kris.co"
                    },
                    items: [{
                        description: product.name,
                        quantity: 1,
                        price: product.price,
                        total: product.price
                    }],
                    fees: {
                        arcFee: arcFee,
                        networkFee: networkFee,
                        totalFees: arcFee + networkFee
                    },
                    subtotal: product.price,
                    total: total + networkFee,
                    paymentMethod: document.querySelector('input[name="paymentMethod"]:checked').value,
                    status: 'paid'
                };
            },
            
            showInvoiceDownload(invoice) {
                Chat.addSystemMessage(`📄 Invoice ${invoice.id} generated. <button class="btn btn-sm btn-primary" onclick="Invoice.view('${invoice.id}')">Download Invoice</button>`);
            }
        };

        // ===== INVOICE CONTROLLER =====
        const Invoice = {
            view(invoiceId) {
                const invoice = State.invoices.find(inv => inv.id === invoiceId);
                if (!invoice) {
                    Toast.error('Invoice not found');
                    return;
                }
                
                State.currentInvoice = invoice;
                this.renderPreview(invoice);
                Modal.open('invoice');
            },
            
            viewAll() {
                this.renderInvoicesList();
                Modal.open('invoices');
            },
            
            renderPreview(invoice) {
                const container = document.getElementById('invoicePreview');
                const date = new Date(invoice.date);
                const formattedDate = date.toLocaleDateString('en-US', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric'
                });
                
                container.innerHTML = `
                    <div class="invoice-header">
                        <h2 class="h2 text-primary">INVOICE</h2>
                        <div class="text-lg font-semibold">${invoice.id}</div>
                        <div class="text-muted">Date: ${formattedDate}</div>
                        <div class="badge badge-success mt-2">${invoice.status.toUpperCase()}</div>
                    </div>
                    
                    <div class="invoice-details">
                        <div>
                            <h4 class="font-semibold mb-2">Bill From:</h4>
                            <div class="text-sm">
                                <div>${invoice.merchant.name}</div>
                                <div>${invoice.merchant.address}</div>
                                <div>${invoice.merchant.email}</div>
                            </div>
                        </div>
                        
                        <div>
                            <h4 class="font-semibold mb-2">Bill To:</h4>
                            <div class="text-sm">
                                <div>${invoice.customer.name}</div>
                                <div>${invoice.customer.email}</div>
                                <div>${invoice.customer.address}</div>
                            </div>
                        </div>
                    </div>
                    
                    <table class="invoice-table">
                        <thead>
                            <tr>
                                <th>Description</th>
                                <th>Quantity</th>
                                <th>Price</th>
                                <th>Total</th>
                            </tr>
                        </thead>
                        <tbody>
                            ${invoice.items.map(item => `
                                <tr>
                                    <td>${item.description}</td>
                                    <td>${item.quantity}</td>
                                    <td>${Utils.formatUSDC(item.price)}</td>
                                    <td>${Utils.formatUSDC(item.total)}</td>
                                </tr>
                            `).join('')}
                        </tbody>
                    </table>
                    
                    <div class="text-right">
                        <div class="flex justify-between mb-2">
                            <span class="text-muted">Subtotal:</span>
                            <span>${Utils.formatUSDC(invoice.subtotal)}</span>
                        </div>
                        <div class="flex justify-between mb-2">
                            <span class="text-muted">Arc Fee (0.3%):</span>
                            <span>${Utils.formatUSDC(invoice.fees.arcFee)}</span>
                        </div>
                        <div class="flex justify-between mb-2">
                            <span class="text-muted">Network Fee:</span>
                            <span>${Utils.formatUSDC(invoice.fees.networkFee)}</span>
                        </div>
                        <div class="flex justify-between pt-4 border-t text-lg font-bold">
                            <span>TOTAL:</span>
                            <span class="text-primary">${Utils.formatUSDC(invoice.total)}</span>
                        </div>
                    </div>
                    
                    <div class="mt-6 pt-6 border-t text-sm text-muted">
                        <div class="grid grid-2 gap-4">
                            <div>
                                <div class="font-medium mb-1">Payment Method:</div>
                                <div>${invoice.paymentMethod === 'arc' ? 'USDC via Arc' : invoice.paymentMethod === 'card' ? 'Credit/Debit Card' : 'Crypto Wallet'}</div>
                            </div>
                            <div>
                                <div class="font-medium mb-1">Transaction ID:</div>
                                <div>${invoice.transactionId}</div>
                            </div>
                        </div>
                        <div class="mt-4 italic">
                            Thank you for your business! All payments are processed securely via Arc.
                        </div>
                    </div>
                `;
            },
            
            renderInvoicesList() {
                const container = document.getElementById('invoicesList');
                const countElement = document.getElementById('invoiceCount');
                
                if (State.invoices.length === 0) {
                    container.innerHTML = `
                        <div class="text-center py-8 text-muted">
                            <i class="fas fa-file-invoice text-4xl mb-4"></i>
                            <div class="font-medium">No invoices yet</div>
                            <div class="text-sm mt-2">Make a purchase to generate your first invoice</div>
                        </div>
                    `;
                    countElement.textContent = '0';
                    return;
                }
                
                container.innerHTML = State.invoices.map(invoice => {
                    const date = new Date(invoice.date);
                    const formattedDate = date.toLocaleDateString('en-US', {
                        month: 'short',
                        day: 'numeric',
                        year: 'numeric'
                    });
                    
                    return `
                        <div class="transaction-item">
                            <div class="transaction-icon bg-primary-100 text-primary">
                                <i class="fas fa-file-invoice"></i>
                            </div>
                            <div class="flex-1">
                                <div class="font-semibold">${invoice.id}</div>
                                <div class="text-xs text-muted">${formattedDate} • ${invoice.items[0].description}</div>
                            </div>
                            <div class="flex flex-col items-end gap-1">
                                <div class="font-bold text-primary">${Utils.formatUSDC(invoice.total)}</div>
                                <div class="flex gap-1">
                                    <button class="btn btn-outline btn-xs" onclick="Invoice.view('${invoice.id}')" title="View invoice">
                                        <i class="fas fa-eye"></i>
                                    </button>
                                    <button class="btn btn-primary btn-xs" onclick="Invoice.downloadSingle('${invoice.id}')" title="Download invoice">
                                        <i class="fas fa-download"></i>
                                    </button>
                                </div>
                            </div>
                        </div>
                    `;
                }).join('');
                
                countElement.textContent = State.invoices.length.toString();
            },
            
            downloadSingle(invoiceId) {
                const invoice = State.invoices.find(inv => inv.id === invoiceId);
                if (!invoice) {
                    Toast.error('Invoice not found');
                    return;
                }
                
                this.downloadInvoice(invoice);
            },
            
            downloadCurrent() {
                if (!State.currentInvoice) {
                    Toast.error('No invoice selected');
                    return;
                }
                
                this.downloadInvoice(State.currentInvoice);
            },
            
            downloadAll() {
                if (State.invoices.length === 0) {
                    Toast.error('No invoices available');
                    return;
                }
                
                // Create a ZIP of all invoices
                const invoiceTexts = State.invoices.map(inv => this.generateInvoiceText(inv)).join('\n\n---\n\n');
                const filename = `krisco-invoices-${new Date().toISOString().split('T')[0]}.txt`;
                
                this.downloadFile(filename, invoiceTexts);
                Toast.success(`Downloaded ${State.invoices.length} invoices`);
            },
            
            downloadInvoice(invoice) {
                const invoiceText = this.generateInvoiceText(invoice);
                const filename = `${invoice.id}.txt`;
                
                this.downloadFile(filename, invoiceText);
                Toast.success(`Invoice ${invoice.id} downloaded`);
            },
            
            generateInvoiceText(invoice) {
                const date = new Date(invoice.date);
                const formattedDate = date.toLocaleDateString('en-US', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric',
                    hour: '2-digit',
                    minute: '2-digit'
                });
                
                return `
========================================
            kris.co INVOICE
========================================

Invoice ID: ${invoice.id}
Date: ${formattedDate}
Status: ${invoice.status.toUpperCase()}
Transaction ID: ${invoice.transactionId}

----------------------------------------
BILL FROM:
${invoice.merchant.name}
${invoice.merchant.address}
${invoice.merchant.email}

BILL TO:
${invoice.customer.name}
${invoice.customer.email}
${invoice.customer.address}

----------------------------------------
ITEM DETAILS:
${invoice.items.map(item => `
• ${item.description}
  Quantity: ${item.quantity}
  Price: ${Utils.formatUSDC(item.price)}
  Total: ${Utils.formatUSDC(item.total)}
`).join('')}

----------------------------------------
PAYMENT SUMMARY:
Subtotal: ${Utils.formatUSDC(invoice.subtotal)}
Arc Fee (0.3%): ${Utils.formatUSDC(invoice.fees.arcFee)}
Network Fee: ${Utils.formatUSDC(invoice.fees.networkFee)}
----------------------------------------
TOTAL: ${Utils.formatUSDC(invoice.total)}

Payment Method: ${invoice.paymentMethod === 'arc' ? 'USDC via Arc' : invoice.paymentMethod === 'card' ? 'Credit/Debit Card' : 'Crypto Wallet'}

----------------------------------------
Thank you for shopping with kris.co!
All payments processed securely via Arc.
========================================
`;
            },
            
            downloadFile(filename, text) {
                const element = document.createElement('a');
                element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
                element.setAttribute('download', filename);
                element.style.display = 'none';
                document.body.appendChild(element);
                element.click();
                document.body.removeChild(element);
            },
            
            print() {
                window.print();
            }
        };

        // ===== UI CONTROLLER =====
        const UI = {
            init() {
                this.updateBalance();
                this.updateBudget();
                this.initBudgetChart();
                this.renderTransactions();
                ProductsController.render();
                
                // Set up payment options
                this.setupPaymentOptions();
                
                // Add welcome message
                setTimeout(() => {
                    Chat.addMessage('ai', `Hello! I'm your AI Shopping Assistant from <strong>kris.co</strong>. I can help you find products, negotiate prices, and make instant payments using USDC via Arc.<br><br>Try asking for a product or click on items below!`);
                    Toast.info('Welcome to kris.co AI Shopping Agent!', 5000);
                }, 500);
            },
            
            updateBalance() {
                document.getElementById('usdcBalance').textContent = Utils.formatUSDC(State.usdcBalance);
            },
            
            updateBudget() {
                document.getElementById('budgetUsed').textContent = Utils.formatCurrency(State.spent);
                document.getElementById('budgetRemaining').textContent = Utils.formatCurrency(State.budgetTotal - State.spent);
                document.getElementById('budgetSaved').textContent = Utils.formatCurrency(State.saved);
                this.updateBudgetChart();
            },
            
            initBudgetChart() {
                const ctx = document.getElementById('budgetChart').getContext('2d');
                if (State.budgetChart) {
                    State.budgetChart.destroy();
                }
                
                State.budgetChart = new Chart(ctx, {
                    type: 'doughnut',
                    data: {
                        labels: ['Spent', 'Remaining'],
                        datasets: [{
                            data: [State.spent, State.budgetTotal - State.spent],
                            backgroundColor: ['#6366f1', '#e2e8f0'],
                            borderWidth: 0,
                            borderRadius: 4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { display: false },
                            tooltip: {
                                callbacks: {
                                    label: (context) => `${context.label}: ${Utils.formatCurrency(context.raw)}`
                                }
                            }
                        },
                        cutout: '70%'
                    }
                });
            },
            
            updateBudgetChart() {
                if (State.budgetChart) {
                    State.budgetChart.data.datasets[0].data = [State.spent, State.budgetTotal - State.spent];
                    State.budgetChart.update();
                }
            },
            
            renderTransactions() {
                const list = document.getElementById('transactionsList');
                list.innerHTML = '';
                
                Transactions.slice(0, 5).forEach(transaction => {
                    const item = document.createElement('div');
                    item.className = 'transaction-item';
                    item.onclick = transaction.invoiceId ? () => Invoice.view(transaction.invoiceId) : null;
                    item.style.cursor = transaction.invoiceId ? 'pointer' : 'default';
                    
                    item.innerHTML = `
                        <div class="transaction-icon ${transaction.status === 'success' ? 'bg-emerald-100 text-emerald-600' : 'bg-amber-100 text-amber-600'}">
                            <i class="fas ${transaction.type === 'savings' ? 'fa-comments-dollar' : 'fa-shopping-cart'}"></i>
                        </div>
                        <div class="flex-1">
                            <div class="font-semibold">${transaction.title}</div>
                            <div class="text-xs text-muted">${transaction.time} ${transaction.invoiceId ? '• Click to view invoice' : ''}</div>
                        </div>
                        <div class="font-bold ${transaction.type === 'savings' ? 'text-emerald-600' : 'text-primary'}">
                            ${transaction.type === 'savings' ? '-' : ''}${Utils.formatUSDC(transaction.amount)}
                        </div>
                    `;
                    
                    list.appendChild(item);
                });
            },
            
            setupPaymentOptions() {
                const options = document.querySelectorAll('.payment-option');
                options.forEach(option => {
                    const input = option.querySelector('input[type="radio"]');
                    option.addEventListener('click', () => {
                        input.checked = true;
                        options.forEach(opt => opt.classList.remove('selected'));
                        option.classList.add('selected');
                    });
                });
                
                // Highlight Arc option by default
                document.getElementById('optionArc').classList.add('selected');
            }
        };

        // ===== DEMO CONTROLLER =====
        const Demo = {
            reset() {
                if (!confirm('Are you sure you want to reset the demo? All transactions and invoices will be cleared.')) {
                    return;
                }
                
                State.usdcBalance = 1250.00;
                State.spent = 245.50;
                State.saved = 58.75;
                State.selectedProduct = null;
                State.invoices = [];
                Transactions = [
                    { 
                        id: 1, 
                        title: "Wireless Earbuds", 
                        amount: 79.99, 
                        time: "10 min ago", 
                        status: "success", 
                        type: "purchase",
                        invoiceId: "INV-2024-001"
                    },
                    { 
                        id: 2, 
                        title: "Price Negotiation", 
                        amount: 15.50, 
                        time: "45 min ago", 
                        status: "success", 
                        type: "savings" 
                    },
                    { 
                        id: 3, 
                        title: "Laptop Stand", 
                        amount: 39.99, 
                        time: "2 hours ago", 
                        status: "success", 
                        type: "purchase",
                        invoiceId: "INV-2024-002"
                    },
                    { 
                        id: 4, 
                        title: "Webcam 1080p", 
                        amount: 59.99, 
                        time: "1 day ago", 
                        status: "success", 
                        type: "purchase",
                        invoiceId: "INV-2024-003"
                    },
                    { 
                        id: 5, 
                        title: "Price Negotiation", 
                        amount: 22.25, 
                        time: "2 days ago", 
                        status: "success", 
                        type: "savings" 
                    }
                ];
                
                // Reset product prices
                Products.forEach(p => {
                    if (p.id === 1) p.price = 89.99;
                    if (p.id === 2) p.price = 149.99;
                    if (p.id === 3) p.price = 199.99;
                    if (p.id === 4) p.price = 79.99;
                    if (p.id === 5) p.price = 249.99;
                    if (p.id === 6) p.price = 34.99;
                });
                
                // Clear chat
                document.getElementById('chatMessages').innerHTML = '';
                
                // Clear localStorage
                localStorage.removeItem('krisco_transactions');
                localStorage.removeItem('krisco_invoices');
                
                // Update UI
                UI.updateBalance();
                UI.updateBudget();
                ProductsController.render();
                ProductsController.updatePaymentPanel();
                UI.renderTransactions();
                
                document.getElementById('payButton').disabled = true;
                document.getElementById('payButton').innerHTML = '<i class="fas fa-lock"></i> Pay Now';
                
                // Add welcome message
                Chat.addMessage('ai', 'Demo reset! Ready to help you shop with AI and Arc payments.');
                Toast.success('Demo has been reset to initial state');
            },
            
            toggleMode() {
                State.devMode = !State.devMode;
                const modeText = document.getElementById('modeText');
                const button = document.querySelector('.btn-primary');
                
                if (State.devMode) {
                    modeText.textContent = 'Demo Mode';
                    button.innerHTML = '<i class="fas fa-eye"></i> Demo Mode';
                    Chat.addSystemMessage('🛠 Developer mode activated - showing technical details');
                    Toast.info('Developer mode activated');
                } else {
                    modeText.textContent = 'Dev Mode';
                    button.innerHTML = '<i class="fas fa-code"></i> Dev Mode';
                    Chat.addSystemMessage('🎯 Switched to demo mode');
                    Toast.info('Demo mode activated');
                }
            },
            
            showHelp() {
                Modal.open('help');
            },
            
            exportData() {
                const data = {
                    transactions: Transactions,
                    invoices: State.invoices,
                    budget: {
                        balance: State.usdcBalance,
                        spent: State.spent,
                        saved: State.saved
                    },
                    exportDate: new Date().toISOString()
                };
                
                const filename = `krisco-export-${new Date().toISOString().split('T')[0]}.json`;
                const jsonString = JSON.stringify(data, null, 2);
                
                Invoice.downloadFile(filename, jsonString);
                Toast.success('Data exported successfully');
            },
            
            viewStatistics() {
                const totalPurchases = Transactions.filter(t => t.type === 'purchase').length;
                const totalSpent = Transactions.filter(t => t.type === 'purchase').reduce((sum, t) => sum + t.amount, 0);
                const totalSaved = Transactions.filter(t => t.type === 'savings').reduce((sum, t) => sum + t.amount, 0);
                
                Chat.addMessage('ai', `
                    <strong>📊 Your Shopping Statistics:</strong><br>
                    • Total Purchases: ${totalPurchases}<br>
                    • Total Spent: ${Utils.formatUSDC(totalSpent)}<br>
                    • Total Saved: ${Utils.formatUSDC(totalSaved)}<br>
                    • Average Savings per Purchase: ${Utils.formatUSDC(totalSaved / Math.max(totalPurchases, 1))}<br>
                    • Invoices Generated: ${State.invoices.length}
                `);
                
                Toast.info('Statistics displayed in chat');
            }
        };

        // ===== INITIALIZATION =====
        document.addEventListener('DOMContentLoaded', () => {
            UI.init();
            
            // Initialize chat input
            const chatInput = document.getElementById('chatInput');
            chatInput.addEventListener('keydown', (e) => {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    Chat.sendMessage();
                }
            });
            
            // Focus chat input on load
            setTimeout(() => chatInput.focus(), 1000);
            
            // Add keyboard shortcuts
            document.addEventListener('keydown', (e) => {
                // Ctrl + / for help
                if (e.ctrlKey && e.key === '/') {
                    e.preventDefault();
                    Demo.showHelp();
                }
                
                // Ctrl + R to reset
                if (e.ctrlKey && e.key === 'r') {
                    e.preventDefault();
                    Demo.reset();
                }
                
                // Escape to close modals
                if (e.key === 'Escape') {
                    Modal.closeAll();
                }
            });
            
            // Make all buttons work properly
            document.querySelectorAll('button').forEach(button => {
                button.addEventListener('click', function(e) {
                    // Add click feedback
                    this.style.transform = 'scale(0.98)';
                    setTimeout(() => {
                        this.style.transform = '';
                    }, 150);
                });
            });
        });
    </script>
</body>
</html>
