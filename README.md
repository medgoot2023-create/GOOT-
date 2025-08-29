<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>برنامج الأستاذ</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
            direction: rtl;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .welcome-screen {
            background: white;
            border-radius: 20px;
            padding: 60px;
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            margin-bottom: 30px;
            /* Background image for the main window */
            background-image: linear-gradient(rgba(255,255,255,0.6), rgba(255,255,255,0.6));
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }

        .welcome-title {
            font-size: 3em;
            color: #667eea;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .welcome-description {
            font-size: 1.2em;
            line-height: 1.8;
            color: #555;
            margin-bottom: 30px;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
        }

        .developer-info {
            font-size: 1.1em;
            color: #764ba2;
            font-weight: bold;
        }

        .main-menu {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .menu-button {
            background: white;
            border: none;
            border-radius: 15px;
            padding: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            text-align: center;
            font-size: 1.1em;
            color: #333;
        }

        .menu-button:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }

        .menu-icon {
            font-size: 2.5em;
            margin-bottom: 15px;
            display: block;
        }

        .section {
            display: none;
            background: white;
            border-radius: 20px;
            padding: 30px;
            margin-top: 20px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
        }

        .section.active {
            display: block;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 2px solid #f0f0f0;
        }

        .section-title {
            font-size: 2em;
            color: #667eea;
        }

        .back-button {
            background: #764ba2;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.3s ease;
        }

        .back-button:hover {
            background: #5a3a7a;
            transform: scale(1.05);
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            border-color: #667eea;
            outline: none;
        }

        .tabs {
            display: flex;
            border-bottom: 2px solid #f0f0f0;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .tab-button {
            background: none;
            border: none;
            padding: 15px 25px;
            cursor: pointer;
            font-size: 1em;
            color: #666;
            border-bottom: 3px solid transparent;
            transition: all 0.3s ease;
            margin-bottom: -2px;
        }

        .tab-button.active {
            color: #667eea;
            border-bottom-color: #667eea;
            background: #f8f9ff;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .schedule-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        .schedule-table th,
        .schedule-table td {
            border: 2px solid #ddd;
            padding: 10px;
            text-align: center;
            min-width: 120px;
        }

        .schedule-table th {
            background: #667eea;
            color: white;
        }

        .schedule-table input {
            width: 100%;
            border: none;
            padding: 8px;
            text-align: center;
            background: transparent;
        }

        .student-list {
            max-height: 400px;
            overflow-y: auto;
            border: 1px solid #ddd;
            border-radius: 8px;
        }

        .student-item {
            padding: 15px;
            border-bottom: 1px solid #f0f0f0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .student-item:last-child {
            border-bottom: none;
        }

        .add-button {
            background: #28a745;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px 5px;
        }

        .remove-button {
            background: #dc3545;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
        }

        .grades-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        .grades-table th,
        .grades-table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }

        .grades-table th {
            background: #667eea;
            color: white;
        }

        .grades-table input {
            width: 60px;
            padding: 4px;
            text-align: center;
            border: 1px solid #ccc;
        }

        /* Excel-like table for Daily Record */
        .excel-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
            border-spacing: 0;
        }

        .excel-table th, .excel-table td {
            border: 1px solid #000;
            padding: 0;
            text-align: center;
            vertical-align: top;
        }
        .excel-table th {
            background: #eef2ff;
            color: #333;
            position: sticky;
            top: 0;
            z-index: 1;
        }

        .excel-table input, .excel-table select, .excel-table textarea {
            width: 100%;
            box-sizing: border-box;
            padding: 8px;
            border: 1px solid transparent; /* Keep layout but hide border */
            background-color: transparent;
        }


        /* Vertical text for the Time column (2nd child) */
        #dailyRecordTable tbody td:nth-child(2) {
            height: 150px; /* Set a fixed height for the cell */
            display: flex;
            align-items: center;
            justify-content: center;
        }

        #dailyRecordTable tbody td:nth-child(2) input {
            transform: rotate(-90deg);
            width: 130px; /* This becomes the visual height, must be < cell height */
            flex-shrink: 0; /* Prevent the item from shrinking */
        }

        /* Restore appearance for inputs with suggestions to show the arrow */
        .excel-table input[list] {
            border: 1px solid #ccc;
        }
        .excel-table textarea { min-height: 110px; resize: vertical; }
        /* Make the 8th column (سير النشاط) specifically wider/taller and with larger font */
        .excel-table td:nth-child(8) textarea { 
            min-height: 130px; 
            font-size: 1.1em; /* Larger font */
            font-family: Arial, sans-serif; /* Change font to Arial */
        }

        .file-upload {
            border: 2px dashed #667eea;
            padding: 40px;
            text-align: center;
            border-radius: 10px;
            margin: 20px 0;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .file-upload:hover {
            background: #f8f9ff;
        }

        .lesson-item {
            background: #f8f9ff;
            padding: 20px;
            border-radius: 10px;
            margin: 10px 0;
            border-left: 5px solid #667eea;
        }

        .settings-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .settings-section {
            background: #f8f9ff;
            padding: 25px;
            border-radius: 15px;
            border: 2px solid #e0e6ff;
        }

        .settings-section h3 {
            color: #667eea;
            margin-bottom: 20px;
            font-size: 1.3em;
        }

        /* Smaller buttons for daily record controls */
        #dailyRecord .import-section .add-button,
        #dailyRecord .import-section .remove-button {
            padding: 6px 12px;
            font-size: 0.9em;
            margin: 5px 3px;
        }

        /* Daily Record Excel-like Layout */
        .daily-record-form {
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            gap: 10px;
            margin-bottom: 20px;
            background: #f8f9ff;
            padding: 20px;
            border-radius: 10px;
            border: 2px solid #e0e6ff;
        }

        .daily-record-form .form-group {
            margin-bottom: 0;
        }

        .daily-record-form label {
            font-size: 0.9em;
            margin-bottom: 5px;
        }

        .daily-record-form input,
        .daily-record-form select,
        .daily-record-form textarea {
            padding: 8px;
            font-size: 0.9em;
        }

        .lesson-flow-notes {
            grid-column: span 8;
        }

        .lesson-flow-notes textarea {
            min-height: 120px;
            resize: vertical;
        }

        .import-section {
            background: #e8f4fd;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            border: 2px solid #b3d9ff;
        }

        .lessons-container {
            margin-top: 20px;
            padding: 20px;
            border: 2px dashed #ddd;
            border-radius: 10px;
            background: #f9f9f9;
            min-height: 200px;
        }

        .lesson-item {
            background: white;
            padding: 15px;
            margin: 10px 0;
            border-radius: 8px;
            border: 1px solid #e0e0e0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .lesson-item .lesson-info {
            flex: 1;
        }

        .lesson-item .lesson-actions {
            display: flex;
            gap: 10px;
        }

        .parent-message {
            background: white;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
            border: 1px solid #e0e0e0;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .parent-message .message-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #f0f0f0;
        }

        .parent-message .message-content {
            line-height: 1.6;
            color: #333;
        }

        .import-section h3 {
            color: #0056b3;
            margin-bottom: 15px;
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .welcome-screen {
                padding: 30px;
            }
            
            .welcome-title {
                font-size: 2em;
            }
            
            .main-menu {
                grid-template-columns: 1fr;
            }
            
            .tabs {
                flex-direction: column;
            }
            
            .schedule-table {
                font-size: 0.8em;
            }

            .daily-record-form {
                grid-template-columns: 1fr;
            }

            .lesson-flow-notes {
                grid-column: span 1;
            }
        }


        /* Notification Styles */
        #notification-container {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1000;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }

        .notification {
            padding: 15px 25px;
            border-radius: 8px;
            color: white;
            font-size: 1.1em;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            opacity: 0;
            transform: translateY(-20px);
            transition: all 0.5s ease;
            min-width: 300px;
            text-align: center;
        }

        .notification.show {
            opacity: 1;
            transform: translateY(0);
        }

        .notification.success {
            background: linear-gradient(135deg, #28a745, #218838);
        }

        .notification.error {
            background: linear-gradient(135deg, #dc3545, #c82333);
        }

        .notification.info {
            background: linear-gradient(135deg, #17a2b8, #138496);
        }

        /* CSS Framework for New Features */
        :root {
            --success-color: #28A745;
            --danger-color: #DC3545;
            --warning-color: #FFC107;
            --info-color: #17A2B8;
            --primary-color: #007BFF;
            --secondary-color: #6C757D;
            --calendar-color: #4A90E2;
            --lesson-color: #2D5A27;
            --parent-color: #FD7E14;
            --assignment-color: #8B5CF6;
            --analytics-color: #1E3A8A;
            --quiz-color: #B91C1C;
        }

        /* Calendar Styles */
        .calendar-button {
            background: linear-gradient(135deg, var(--calendar-color), #357ABD) !important;
            color: white !important;
        }

        /* START: Calendar styles */
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 6px;
            border: 1px solid #ddd;
            padding: 6px;
            background: #fafafa;
        }
        .calendar-day {
            min-height: 90px;
            border: 1px solid #eee;
            padding: 6px;
            background: white;
            display:flex;
            flex-direction:column;
        }
        .calendar-day .date-label {
            font-weight: bold;
            font-size: 0.9em;
            margin-bottom: 6px;
        }
        .calendar-event {
            display:inline-block;
            color: white;
            padding: 4px 6px;
            border-radius: 4px;
            font-size: 0.75em;
            margin-bottom: 4px;
            cursor: pointer;
            word-break: break-word;
        }
        /* event colors */
        .event-lesson { background: #51CF66; }
        .event-exam   { background: #FF6B6B; }
        .event-meeting{ background: #FFD93D; color:#333; }
        .event-note   { background: #4A90E2; }

        /* small month nav */
        #currentMonthLabel { font-size:1.1em; }

        .calendar-empty {
            color:#999;
            font-size:0.9em;
        }

        /* Modal override for calendar modal (if needed) */
        #calendarModal .modal-content { max-width:480px; }
        /* END: Calendar styles */

        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .calendar-nav {
            display: flex;
            gap: 10px;
        }

        /* KPI Cards */
        .kpi-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .kpi-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            text-align: center;
            border-left: 5px solid var(--primary-color);
        }

        .kpi-card.success {
            border-left-color: var(--success-color);
        }

        .kpi-card.attendance {
            border-left-color: var(--info-color);
        }

        .kpi-card.average {
            border-left-color: var(--warning-color);
        }

        .kpi-value {
            font-size: 2.5em;
            font-weight: bold;
            color: #333;
            margin: 10px 0;
        }

        .kpi-trend {
            font-size: 0.9em;
            padding: 5px 10px;
            border-radius: 15px;
            display: inline-block;
        }

        .kpi-trend.up {
            background: #d4edda;
            color: var(--success-color);
        }

        .kpi-trend.down {
            background: #f8d7da;
            color: var(--danger-color);
        }

        .kpi-trend.stable {
            background: #e2e3e5;
            color: var(--secondary-color);
        }

        /* Charts Container */
        .charts-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 30px;
            margin-top: 30px;
        }

        .chart-section {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .chart-section h3 {
            color: #333;
            margin-bottom: 20px;
            text-align: center;
        }

        /* Action Buttons */
        .action-btn {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            margin: 5px;
        }

        .action-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .action-btn.primary {
            background: var(--primary-color);
            color: white;
        }

        .action-btn.success {
            background: var(--success-color);
            color: white;
        }

        .action-btn.danger {
            background: var(--danger-color);
            color: white;
        }

        .action-btn.warning {
            background: var(--warning-color);
            color: white;
        }

        /* Assignment Cards */
        .assignment-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            margin: 15px 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            border-left: 5px solid var(--assignment-color);
        }

        .progress-bar {
            width: 100%;
            height: 20px;
            background: #e9ecef;
            border-radius: 10px;
            overflow: hidden;
            margin: 10px 0;
        }

.progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--success-color), #20c997);
    transition: width 0.3s ease;
}

        .student-behavior-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .points-display {
            display: flex;
            justify-content: space-around;
            margin: 15px 0;
        }

        .positive-points {
            color: var(--success-color);
            font-weight: bold;
            font-size: 1.2em;
        }

        .negative-points {
            color: var(--danger-color);
            font-weight: bold;
            font-size: 1.2em;
        }

        .total-points {
            color: var(--primary-color);
            font-weight: bold;
            font-size: 1.2em;
        }

        .behavior-item {
            padding: 8px 12px;
            margin: 5px 0;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
        }

        .behavior-item.positive {
            background: #d4edda;
            border-left: 3px solid var(--success-color);
        }

        .behavior-item.negative {
            background: #f8d7da;
            border-left: 3px solid var(--danger-color);
        }

        /* Connection Status */
        .connection-status {
            position: fixed;
            top: 10px;
            right: 20px;
            background: white;
            padding: 10px 15px;
            border-radius: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            z-index: 1000;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .status-icon.online {
            color: var(--success-color);
        }

        .status-icon.offline {
            color: var(--danger-color);
        }

        /* At-risk Students */
        .at-risk-students {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }

        .student-alert-card {
            background: white;
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
            border-left: 4px solid var(--warning-color);
        }

        .student-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .risk-level {
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.8em;
            font-weight: bold;
        }

        .risk-level.high {
            background: var(--danger-color);
            color: white;
        }

        .risk-factors {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 10px;
        }

        .factor {
            background: #e9ecef;
            padding: 4px 8px;
            border-radius: 12px;
            font-size: 0.8em;
        }

        /* Quiz Builder */
        .quiz-builder-container {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 30px;
            margin-bottom: 30px;
        }
        
        .quiz-form {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            border: 1px solid #dee2e6;
        }
        
        .questions-section {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            border: 1px solid #dee2e6;
        }
        
        .quiz-actions {
            grid-column: 1 / -1;
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
        }
        
        .saved-quizzes {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            border: 1px solid #dee2e6;
        }
        
        .question-item {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin: 15px 0;
            border: 1px solid #dee2e6;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .options-container {
            margin: 10px 0;
        }

        .option {
            display: block;
            width: 100%;
            margin: 5px 0;
            padding: 8px 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        /* Resource Library */
        .resources-library {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .search-bar {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .search-bar input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        .resource-filters {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .filter-btn {
            padding: 8px 16px;
            border: 1px solid #ddd;
            background: white;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .filter-btn.active {
            background: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
        }

        /* Modal Styles */
        .modal-backdrop {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.6);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1050;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            width: 90%;
            max-width: 600px;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-content h3 {
            margin-bottom: 20px;
            color: #667eea;
        }

        .modal-actions {
            margin-top: 20px;
            text-align: left;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .kpi-grid {
                grid-template-columns: 1fr;
            }
            
            .charts-container {
                grid-template-columns: 1fr;
            }
            
            .calendar-grid {
                font-size: 0.8em;
            }
            
            .calendar-day {
                min-height: 60px;
            }
        }

        /* Ensure calendar modal is hidden by default */
        #calendarModal {
            display: none !important;
        }
        
        #calendarModal.show {
            display: flex !important;
        }
        
        /* Homework Tracking Modal specific styles */
        #homeworkTrackingModal .modal-content {
            position: absolute !important;
            top: 5% !important;
            left: 5% !important;
            transform: none !important;
            width: 90% !important;
            max-width: 1200px !important;
            max-height: 85vh !important;
            overflow-y: auto;
        }
        
        /* Modal backdrop styles */
        .modal-backdrop {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.6);
            z-index: 9999;
            display: none;
        }
        
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            width: 90%;
            max-width: 600px;
            max-height: 80vh;
            overflow-y: auto;
            position: relative;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        /* Tab system styles */
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .tab-button.active {
            color: #667eea;
            border-bottom-color: #667eea;
            background: #f8f9ff;
        }
        
        /* Student item styles */
        .student-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            margin: 10px 0;
            background: #f8f9ff;
            border-radius: 8px;
            border: 1px solid #e0e6ff;
        }
        
        .student-info {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
        
        .student-name {
            font-weight: bold;
            color: #333;
        }
        
        .student-class {
            color: #666;
            font-size: 0.9em;
        }
        
        .student-birth {
            color: #888;
            font-size: 0.8em;
        }
        
        .student-actions {
            display: flex;
            gap: 10px;
        }
        
        .attendance-controls, .rewards-controls {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        
        .attendance-controls label, .rewards-controls label {
            display: flex;
            align-items: center;
            gap: 5px;
            cursor: pointer;
        }
        
        /* Import section styles */
        .import-section {
            background: #f8f9ff;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .import-section h3 {
            margin-bottom: 10px;
            color: #667eea;
        }
        
        .import-section p {
            margin-bottom: 15px;
            color: #666;
        }
        
        /* Excel table styles */
        .excel-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .excel-table th,
        .excel-table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }
        
        .excel-table th {
            background-color: #f2f2f2;
            font-weight: bold;
        }
        
        .excel-table input,
        .excel-table textarea {
            width: 100%;
            border: none;
            padding: 4px;
            background: transparent;
        }
        
        .excel-table textarea {
            resize: vertical;
            min-height: 40px;
        }
        
        /* Analytics styles */
        .analytics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .analytics-card {
            background: #f8f9ff;
            padding: 20px;
            border-radius: 10px;
            border: 1px solid #e0e6ff;
        }
        
        .analytics-card h4 {
            color: #667eea;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .analytics-card p {
            margin: 8px 0;
            padding: 8px;
            background: white;
            border-radius: 5px;
            border-left: 3px solid #667eea;
        }
        
        /* Grades table styles */
        .grades-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .grades-table th,
        .grades-table td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: center;
        }
        
        .grades-table th {
            background-color: #667eea;
            color: white;
            font-weight: bold;
        }
        
        .grades-table input {
            width: 80px;
            padding: 5px;
            border: 1px solid #ddd;
            border-radius: 3px;
            text-align: center;
        }
        
        .grades-table input[type="text"] {
            width: 150px;
        }
        
        /* Assignments section styles */
        #assignments .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }
        
        #assignments .form-group {
            margin-bottom: 15px;
        }
        
        #assignments select,
        #assignments input,
        #assignments textarea {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s ease;
        }
        
        #assignments select:focus,
        #assignments input:focus,
        #assignments textarea:focus {
            border-color: #667eea;
            outline: none;
        }
        
        #assignments textarea {
            resize: vertical;
            min-height: 100px;
        }
        
        #assignments .add-button {
            background: #667eea;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 8px;
            font-size: 1.1em;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        
        #assignments .add-button:hover {
            background: #5a6fd8;
        }
        
        /* Assignment list styles */
        .lesson-item {
            background: #f8f9ff;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
            border: 1px solid #e0e6ff;
        }
        
        .lesson-item h4 {
            color: #667eea;
            margin-bottom: 10px;
        }
        
        .progress-bar {
            background: #f1f1f1;
            height: 12px;
            border-radius: 6px;
            overflow: hidden;
            margin: 10px 0;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #28a745, #218838);
            transition: width 0.3s ease;
        }
        
        .action-btn {
            background: #6c757d;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            margin-right: 10px;
            font-size: 0.9em;
        }
        
        .action-btn:hover {
            background: #5a6268;
        }
        
        /* Homework Tracking Table Styles */
        .homework-tracking-section {
            margin: 30px 0;
            background: #f8f9ff;
            padding: 20px;
            border-radius: 10px;
            border: 1px solid #e0e6ff;
        }
        
        .homework-tracking-section h4 {
            color: #667eea;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .table-container {
            overflow-x: auto;
            max-width: 100%;
        }
        
        #homeworkTrackingTable {
            width: 100%;
            border-collapse: collapse;
            background: white;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        
        #homeworkTrackingTable th {
            background: #667eea;
            color: white;
            padding: 12px 8px;
            text-align: center;
            font-weight: bold;
            border: 1px solid #ddd;
            white-space: nowrap;
        }
        
        #homeworkTrackingTable td {
            padding: 10px 8px;
            border: 1px solid #ddd;
            text-align: center;
            vertical-align: middle;
        }
        
        #homeworkTrackingTable tr:nth-child(even) {
            background-color: #f8f9ff;
        }
        
        #homeworkTrackingTable tr:hover {
            background-color: #e3f2fd;
        }
        
        .homework-actions {
            display: flex;
            gap: 5px;
            justify-content: center;
            flex-wrap: wrap;
        }
        
        .homework-actions button {
            padding: 6px 12px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.85em;
            white-space: nowrap;
        }
        
        .track-btn {
            background: #17a2b8;
            color: white;
        }
        
        .track-btn:hover {
            background: #138496;
        }
        
        .export-btn {
            background: #28a745;
            color: white;
        }
        
        .export-btn:hover {
            background: #218838;
        }
    </style>
    
    <!-- XLSX Library for Excel import/export -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    
    <script>
      // Individual button functions to avoid null element errors
      function hideWelcome() {
        const welcome = document.getElementById('welcomeScreen');
        if (welcome) welcome.style.setProperty('display', 'none', 'important');
        document.querySelectorAll('.section').forEach(function(s){ 
            s.style.setProperty('display', 'none', 'important'); 
        });
      }
      
      function showTeacherInfo() {
        if (typeof showSection === 'function') return showSection('teacherInfo');
        hideWelcome();
        const section = document.getElementById('teacherInfo');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showSchedule() {
        if (typeof showSection === 'function') return showSection('schedule');
        hideWelcome();
        const section = document.getElementById('schedule');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showStudents() {
        if (typeof showSection === 'function') return showSection('students');
        hideWelcome();
        const section = document.getElementById('students');
        if (section) section.style.setProperty('display', 'block', 'important');
        setTimeout(() => { if (typeof updateAllLists === 'function') updateAllLists(); }, 100);
      }
      
      function showDailyRecord() {
        // Delegate to centralized navigation to ensure consistent hiding/init
        if (typeof showSection === 'function') {
          showSection('dailyRecord');
        } else {
          // Fallback
          hideWelcome();
          const section = document.getElementById('dailyRecord');
          if (section) section.style.setProperty('display', 'block', 'important');
        }
      }
      
      function showLessons() {
        if (typeof showSection === 'function') return showSection('lessons');
        hideWelcome();
        const section = document.getElementById('lessons');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showPresentations() {
        if (typeof showSection === 'function') return showSection('presentations');
        hideWelcome();
        const section = document.getElementById('presentations');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showSettings() {
        if (typeof showSection === 'function') return showSection('settings');
        hideWelcome();
        const section = document.getElementById('settings');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showCalendar() {
        if (typeof showSection === 'function') return showSection('calendar');
        hideWelcome();
        const section = document.getElementById('calendar');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showLessonPlanner() {
        if (typeof showSection === 'function') return showSection('lessonPlanner');
        hideWelcome();
        const section = document.getElementById('lessonPlanner');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showParents() {
        if (typeof showSection === 'function') return showSection('parents');
        hideWelcome();
        const section = document.getElementById('parents');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function showAssignments() {
        if (typeof showSection === 'function') return showSection('assignments');
        hideWelcome();
        const studentsSection = document.getElementById('students');
        if (studentsSection) {
          studentsSection.style.setProperty('display', 'block', 'important');
          setTimeout(() => {
            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            const assignmentsTab = document.querySelector('button[onclick*="assignments"]');
            const assignmentsContent = document.getElementById('assignments');
            if (assignmentsTab) assignmentsTab.classList.add('active');
            if (assignmentsContent) assignmentsContent.classList.add('active');
            if (typeof updateAssignmentClassSelects === 'function') updateAssignmentClassSelects();
            if (typeof renderAssignments === 'function') renderAssignments();
          }, 100);
        }
      }
      
      function showQuizBuilder() {
        if (typeof showSection === 'function') return showSection('quizBuilder');
        hideWelcome();
        const section = document.getElementById('quizBuilder');
        if (section) section.style.setProperty('display', 'block', 'important');
      }
      
      function goBack() {
        // Hide all sections
        document.querySelectorAll('.section').forEach(function(s) {
            s.style.display = 'none';
        });
        
        // Show the welcome screen
        const welcome = document.getElementById('welcomeScreen');
        if (welcome) {
            welcome.style.display = 'block';
        }
      }
    </script>
</head>
<body>
    <div id="notification-container"></div>

    <!-- Confirmation Modal -->
    <div id="confirmationModal" class="modal-backdrop" style="display:none;">
        <div class="modal-content">
            <h3 data-translate-key="confirmTitle">تأكيد الإجراء</h3>
            <p id="confirmationMessage" data-translate-key="confirmMessage">هل أنت متأكد من أنك تريد المتابعة؟</p>
            <div class="modal-actions">
                <button id="confirmYesBtn" class="add-button" data-translate-key="yesBtn">نعم</button>
                <button class="remove-button" onclick="closeModal('confirmationModal')" data-translate-key="noBtn">لا</button>
            </div>
        </div>
    </div>
    <div class="container">
        <!-- Welcome Screen -->
        <div id="welcomeScreen" class="welcome-screen">
            <h1 class="welcome-title" data-translate-key="welcomeTitle">📚 مرحباً بكم في برنامج الأستاذ</h1>
            <p class="welcome-description" data-translate-key="welcomeDescription">
                يسهل عليك هذا البرنامج العديد من المهام كالدفتر اليومي ومراقبة نتائج التلاميذ وغياباتهم، كتابة التوقيت، تنظيم الدروس وغيرها الكثير من الميزات المفيدة للمعلم
            </p>
            <p class="developer-info" data-translate-key="developerInfo">من إعداد الأستاذ حميدات مصطفى</p>
            
            <div class="main-menu">
                <button class="menu-button" onclick="showSection('teacherInfo')" data-translate-key="teacherInfo">
                    <span class="menu-icon">👨‍🏫</span>
                    معلومات الأستاذ
                </button>
                <button class="menu-button" onclick="showSection('schedule')" data-translate-key="weeklySchedule">
                    <span class="menu-icon">📅</span>
                    التوقيت الأسبوعي
                </button>
                <button class="menu-button" onclick="showSection('students')" data-translate-key="students">
                    <span class="menu-icon">👥</span>
                    التلاميذ
                </button>
                <button class="menu-button" onclick="showSection('dailyRecord')" data-translate-key="dailyRecord">
                    <span class="menu-icon">📖</span>
                    الدفتر اليومي
                </button>
                <button class="menu-button" onclick="showSection('lessons')" data-translate-key="lessons">
                    <span class="menu-icon">📚</span>
                    الدروس
                </button>
                <button class="menu-button" onclick="showSection('presentations')" data-translate-key="presentations">
                    <span class="menu-icon">🎥</span>
                    العروض والتجارب
                </button>
                <button class="menu-button" onclick="showSection('settings')" data-translate-key="settings">
                    <span class="menu-icon">⚙️</span>
                    الإعدادات
                </button>
                <!-- START: Calendar Button -->
                <button class="menu-button calendar-button" onclick="showSection('calendar')">
                    <span class="menu-icon">📅</span>
                    التقويم الشهري
                </button>
                <!-- START: Lesson Planner Button (put inside .main-menu) -->
                <button class="menu-button" onclick="showSection('lessonPlanner')">
                    <span class="menu-icon">📝</span>
                    تخطيط الدروس
                </button>
                <!-- END -->
                
                <!-- START: Parents Button -->
                <button class="menu-button" onclick="showSection('parents')">
                    <span class="menu-icon">👥</span>
                    التواصل مع الأولياء
                </button>
                <!-- END -->
                
                <!-- Assignments Button -->
        <button class="menu-button" onclick="showSection('assignments')">
            <span class="menu-icon">📋</span>
            إدارة الواجبات
        </button>
        
        <!-- Quiz Builder Button -->
        <button class="menu-button" onclick="showSection('quizBuilder')">
            <span class="menu-icon">❓</span>
            منشئ الاختبارات
        </button>
                <!-- END -->
                
                <!-- Test Button for Debugging -->
                <button class="menu-button" onclick="testNavigation()" style="background: #dc3545; margin-top: 20px;">
                    <span class="menu-icon">🧪</span>
                    اختبار التنقل
                </button>
                
            </div>
        </div>

        <!-- Teacher Info Section -->
        <div id="teacherInfo" class="section">
            <div class="section-header">
                <h2 class="section-title">👨‍🏫 معلومات الأستاذ</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            <div class="form-grid">
                <div class="form-group">
                    <label>الاسم:</label>
                    <input type="text" id="firstName" placeholder="أدخل الاسم">
                </div>
                <div class="form-group">
                    <label>اللقب:</label>
                    <input type="text" id="lastName" placeholder="أدخل اللقب">
                </div>
                <div class="form-group">
                    <label>العنوان:</label>
                    <input type="text" id="address" placeholder="أدخل العنوان">
                </div>
                <div class="form-group">
                    <label>تاريخ الميلاد:</label>
                    <input type="date" id="birthDate">
                </div>
                <div class="form-group">
                    <label>رقم الهاتف:</label>
                    <input type="tel" id="phone" placeholder="أدخل رقم الهاتف">
                </div>
                <div class="form-group">
                    <label>الإيميل:</label>
                    <input type="email" id="email" placeholder="أدخل الإيميل">
                </div>
                <div class="form-group">
                    <label>الإطار:</label>
                    <input type="text" id="framework" placeholder="أدخل الإطار">
                </div>
                <div class="form-group">
                    <label>مادة التدريس:</label>
                    <input type="text" id="subject" placeholder="أدخل مادة التدريس">
                </div>
                <div class="form-group">
                    <label>الشهادة:</label>
                    <input type="text" id="certificate" placeholder="أدخل الشهادة">
                </div>
                <div class="form-group">
                    <label>تاريخ أول تعيين:</label>
                    <input type="date" id="firstAppointment">
                </div>
                <div class="form-group">
                    <label>الصفة:</label>
                    <input type="text" id="position" placeholder="أدخل الصفة">
                </div>
                <div class="form-group">
                    <label>تاريخ الترسيم:</label>
                    <input type="date" id="confirmationDate">
                </div>
                <div class="form-group">
                    <label>الدرجة:</label>
                    <input type="text" id="grade" placeholder="أدخل الدرجة">
                </div>
                <div class="form-group">
                    <label>المؤسسة الحالية:</label>
                    <input type="text" id="currentInstitution" placeholder="أدخل المؤسسة الحالية">
                </div>
                <div class="form-group">
                    <label>السنة الدراسية:</label>
                    <input type="text" id="academicYear" placeholder="أدخل السنة الدراسية">
                </div>
            </div>
        </div>

        <!-- Schedule Section -->
        <div id="schedule" class="section">
            <div class="section-header">
                <h2 class="section-title">📅 التوقيت الأسبوعي</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            <div class="form-grid">
                <div class="form-group">
                    <label>الأستاذ:</label>
                    <input type="text" id="scheduleTeacher" placeholder="اسم الأستاذ">
                </div>
                <div class="form-group">
                    <label>السنة الدراسية:</label>
                    <input type="text" id="scheduleYear" placeholder="السنة الدراسية">
                </div>
                <div class="form-group">
                    <label>الأقسام المسندة:</label>
                    <input type="text" id="assignedClasses" placeholder="الأقسام المسندة">
                </div>
                <div class="form-group">
                    <label>عدد ساعات العمل:</label>
                    <input type="number" id="workHours" placeholder="عدد الساعات">
                </div>
            </div>
            
            <table class="schedule-table">
                <thead>
                    <tr>
                        <th>اليوم</th>
                        <th>08:00 - 09:00</th>
                        <th>09:00 - 10:00</th>
                        <th>10:00 - 11:00</th>
                        <th>11:00 - 12:00</th>
                        <th>14:00 - 15:00</th>
                        <th>15:00 - 16:00</th>
                        <th>16:00 - 17:00</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td>الأحد</td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td></tr>
                    <tr><td>الاثنين</td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td></tr>
                    <tr><td>الثلاثاء</td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td></tr>
                    <tr><td>الأربعاء</td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td></tr>
                    <tr><td>الخميس</td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td><td><input type="text"></td></tr>
                </tbody>
            </table>
        </div>

        <!-- Students Section -->
        <div id="students" class="section">
            <div class="section-header">
                <h2 class="section-title">👥 التلاميذ</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            
            <div class="import-section">
                <h3>📊 استيراد قائمة التلاميذ</h3>
                <p>يمكنك استيراد ملف Excel يحتوي على: الاسم، اللقب، تاريخ الميلاد</p>
                <input type="file" id="studentsExcelFile" accept=".xlsx,.xls" style="display: none;" onchange="handleExcelImport(this)">
                <button class="add-button" onclick="document.getElementById('studentsExcelFile').click()">
                    📂 اختر ملف Excel
                </button>
            </div>
            
            <div class="tabs">
                <button class="tab-button active" onclick="showTab('studentsList', event)">📋 قائمة التلاميذ</button>
                <button class="tab-button" onclick="showTab('grades', event)">📊 المعدلات</button>
                <button class="tab-button" onclick="showTab('attendance', event)">📌 الغياب</button>
                <button class="tab-button" onclick="showTab('rewards', event)">🏆 النقاط والجوائز</button>
                <button class="tab-button" onclick="showTab('behavior', event)">⭐ السلوك والتقدير</button>
                <button class="tab-button" onclick="showTab('analyticsTab', event)">📊 التحليلات والإحصائيات</button>
                <button class="tab-button" onclick="showTab('assignments', event)">📝 ادارة الواجبات</button>
            </div>

            <!-- Students List Tab -->
            <div id="studentsList" class="tab-content active">
                <div class="form-group">
                    <label>القسم:</label>
                    <select id="classSelect" onchange="updateStudentsList()">
                        <option value="1AM1">1AM1</option>
                        <option value="1AM2">1AM2</option>
                        <option value="1AM3">1AM3</option>
                        <option value="1AM4">1AM4</option>
                        <option value="2AM1">2AM1</option>
                        <option value="2AM2">2AM2</option>
                        <option value="2AM3">2AM3</option>
                        <option value="3AM1">3AM1</option>
                        <option value="3AM2">3AM2</option>
                        <option value="3AM3">3AM3</option>
                        <option value="4AM1">4AM1</option>
                        <option value="4AM2">4AM2</option>
                    </select>
                </div>
                
                <button class="add-button" onclick="addStudent()">➕ إضافة تلميذ يدوياً</button>
                
                <div id="studentsListContainer" class="student-list">
                    <!-- Students will be added here dynamically -->
                </div>
            </div>

            <!-- Grades Tab -->
            <div id="grades" class="tab-content">
                <div class="form-group">
                    <label>القسم:</label>
                    <select id="gradesClassSelect" onchange="updateGradesTable()">
                        <option value="1AM1">1AM1</option>
                        <option value="1AM2">1AM2</option>
                        <option value="1AM3">1AM3</option>
                        <option value="1AM4">1AM4</option>
                        <option value="2AM1">2AM1</option>
                        <option value="2AM2">2AM2</option>
                        <option value="2AM3">2AM3</option>
                        <option value="3AM1">3AM1</option>
                        <option value="3AM2">3AM2</option>
                        <option value="3AM3">3AM3</option>
                        <option value="4AM1">4AM1</option>
                        <option value="4AM2">4AM2</option>
                    </select>
                </div>
                <div class="import-section">
                    <button class="add-button" onclick="saveGrades()">💾 حفظ المعدلات</button>
                    <button class="add-button" onclick="exportGradesToExcel()">📤 تصدير المعدلات إلى Excel</button>
                </div>
                
                <table id="gradesTable" class="grades-table">
                    <thead>
                        <tr>
                            <th>التلميذ</th>
                            <th>التقويم</th>
                            <th>الفرض</th>
                            <th>الاختبار</th>
                            <th>المعدل</th>
                            <th>الملاحظة</th>
                        </tr>
                    </thead>
                    <tbody id="gradesTableBody">
                        <!-- Grades will be added here dynamically -->
                    </tbody>
                </table>
            </div>

            <!-- Attendance Tab -->
            <div id="attendance" class="tab-content">
                <div class="form-group">
                    <label>القسم:</label>
                    <select id="attendanceClassSelect" onchange="updateAttendanceList()">
                        <option value="1AM1">1AM1</option>
                        <option value="1AM2">1AM2</option>
                        <option value="1AM3">1AM3</option>
                        <option value="1AM4">1AM4</option>
                        <option value="2AM1">2AM1</option>
                        <option value="2AM2">2AM2</option>
                        <option value="2AM3">2AM3</option>
                        <option value="3AM1">3AM1</option>
                        <option value="3AM2">3AM2</option>
                        <option value="3AM3">3AM3</option>
                        <option value="4AM1">4AM1</option>
                        <option value="4AM2">4AM2</option>
                    </select>
                </div>
                
                <div id="attendanceList" class="student-list">
                    <!-- Attendance list will be updated here -->
                </div>
            </div>

            <!-- Rewards Tab -->
            <div id="rewards" class="tab-content">
                <div class="form-group">
                    <label>القسم:</label>
                    <select id="rewardsClassSelect" onchange="updateRewardsList()">
                        <option value="1AM1">1AM1</option>
                        <option value="1AM2">1AM2</option>
                        <option value="1AM3">1AM3</option>
                        <option value="1AM4">1AM4</option>
                        <option value="2AM1">2AM1</option>
                        <option value="2AM2">2AM2</option>
                        <option value="2AM3">2AM3</option>
                        <option value="3AM1">3AM1</option>
                        <option value="3AM2">3AM2</option>
                        <option value="3AM3">3AM3</option>
                        <option value="4AM1">4AM1</option>
                        <option value="4AM2">4AM2</option>
                    </select>
                    
                    <button class="add-button" onclick="testAddPoints()" style="margin-left: 10px; background: #17a2b8;">
                        🧪 اختبار النقاط
                    </button>
                    
                    <button class="add-button" onclick="refreshRewardsData()" style="margin-left: 10px; background: #28a745;">
                        🔄 تحديث البيانات
                    </button>
                </div>
                
                <div id="rewardsList" class="student-list">
                    <!-- Rewards list will be updated here -->
                </div>
            </div>
            
            <!-- Behavior Tab -->
            <div id="behavior" class="tab-content">
                <div class="form-group">
                    <label>القسم:</label>
                    <select id="behaviorClassSelect" onchange="updateBehaviorList()">
                        <option value="1AM1">1AM1</option>
                        <option value="1AM2">1AM2</option>
                        <option value="1AM3">1AM3</option>
                        <option value="1AM4">1AM4</option>
                        <option value="2AM1">2AM1</option>
                        <option value="2AM2">2AM2</option>
                        <option value="2AM3">2AM3</option>
                        <option value="3AM1">3AM1</option>
                        <option value="3AM2">3AM2</option>
                        <option value="3AM3">3AM3</option>
                        <option value="4AM1">4AM1</option>
                        <option value="4AM2">4AM2</option>
                    </select>
                </div>
                
                <div id="behaviorList" class="student-list">
                    <!-- Behavior list will be updated here -->
                </div>
            </div>
            
            <!-- Analytics Tab -->
            <div id="analyticsTab" class="tab-content">
                <div class="form-group">
                    <label>القسم:</label>
                    <select id="analyticsClassSelect" onchange="updateAnalytics()">
                        <option value="1AM1">1AM1</option>
                        <option value="1AM2">1AM2</option>
                        <option value="1AM3">1AM3</option>
                        <option value="1AM4">1AM4</option>
                        <option value="2AM1">2AM1</option>
                        <option value="2AM2">2AM2</option>
                        <option value="2AM3">2AM3</option>
                        <option value="3AM1">3AM1</option>
                        <option value="3AM2">3AM2</option>
                        <option value="3AM3">3AM3</option>
                        <option value="4AM1">4AM1</option>
                        <option value="4AM2">4AM2</option>
                    </select>
                </div>
                
                <div id="analyticsContent">
                    <div class="analytics-grid">
                        <div class="analytics-card">
                            <h4>إحصائيات عامة</h4>
                            <div id="generalStats"></div>
                        </div>
                        <div class="analytics-card">
                            <h4>أفضل التلاميذ</h4>
                            <div id="topStudents"></div>
                        </div>
                        <div class="analytics-card">
                            <h4>التلاميذ المحتاجون للدعم</h4>
                            <div id="needsSupport"></div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Assignments Tab -->
            <div id="assignments" class="tab-content">
                <h3>📝 إدارة الواجبات</h3>
                
                <form id="assignmentForm">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>عنوان الواجب:</label>
                            <input type="text" id="assignmentTitle" required>
                        </div>
                        <div class="form-group">
                            <label>القسم:</label>
                            <select id="assignmentClass" required list="assignmentClassSuggestions">
                                <option value="">اختر القسم</option>
                                <option value="1AM1">1AM1</option>
                                <option value="1AM2">1AM2</option>
                                <option value="1AM3">1AM3</option>
                                <option value="1AM4">1AM4</option>
                                <option value="2AM1">2AM1</option>
                                <option value="2AM2">2AM2</option>
                                <option value="2AM3">2AM3</option>
                                <option value="3AM1">3AM1</option>
                                <option value="3AM2">3AM2</option>
                                <option value="3AM3">3AM3</option>
                                <option value="4AM1">4AM1</option>
                                <option value="4AM2">4AM2</option>
                            </select>
                            <datalist id="assignmentClassSuggestions">
                                <option value="1AM1">1AM1</option>
                                <option value="1AM2">1AM2</option>
                                <option value="1AM3">1AM3</option>
                                <option value="1AM4">1AM4</option>
                                <option value="2AM1">2AM1</option>
                                <option value="2AM2">2AM2</option>
                                <option value="2AM3">2AM3</option>
                                <option value="3AM1">3AM1</option>
                                <option value="3AM2">3AM2</option>
                                <option value="3AM3">3AM3</option>
                                <option value="4AM1">4AM1</option>
                                <option value="4AM2">4AM2</option>
                            </datalist>
                        </div>
                        <div class="form-group">
                            <label>نوع الواجب:</label>
                            <select id="assignmentType" required>
                                <option value="homework">واجب منزلي</option>
                                <option value="project">مشروع</option>
                                <option value="research">بحث</option>
                                <option value="presentation">عرض</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>تاريخ الاستحقاق:</label>
                            <input type="date" id="dueDate" required>
                        </div>
                        <div class="form-group">
                            <label>الدرجة القصوى:</label>
                            <input type="number" id="maxPoints" min="1" max="100" value="10" required>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>وصف الواجب:</label>
                        <textarea id="assignmentDescription" rows="4" placeholder="وصف مفصل للواجب..."></textarea>
                    </div>
                    
                    <button type="button" class="add-button" onclick="createAssignment()">📝 إنشاء الواجب</button>
                <button type="button" class="add-button" onclick="refreshAssignments()" style="background: #17a2b8; margin-left: 10px;">
                    🔄 تحديث القائمة
                </button>
                </form>
                
                <h3 style="margin-top: 30px;">الواجبات المنشأة</h3>
                
                <!-- Excel-like Homework Tracking Table -->
                <div class="homework-tracking-section">
                    <h4>📊 تتبع الواجبات - جدول Excel</h4>
                    <div class="table-container">
                        <table id="homeworkTrackingTable" class="excel-table">
                            <thead>
                                <tr>
                                    <th>#</th>
                                    <th>عنوان الواجب</th>
                                    <th>القسم</th>
                                    <th>نوع الواجب</th>
                                    <th>تاريخ الاستحقاق</th>
                                    <th>الدرجة القصوى</th>
                                    <th>الوصف</th>
                                    <th>عدد التلاميذ</th>
                                    <th>عدد التسليم</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="homeworkTrackingTableBody">
                                <!-- Homework rows will be added here -->
                            </tbody>
                        </table>
                    </div>
                </div>
                
                <div id="assignmentsList">
                    <!-- Assignments will be displayed here -->
                </div>
            
            <!-- Add Student Modal -->
            <div id="addStudentModal" class="modal" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); z-index: 9999;">
                <div class="modal-content" style="background: white; padding: 30px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.2); width: 90%; max-width: 500px; max-height: 80vh; overflow-y: auto; position: relative; top: 50%; left: 50%; transform: translate(-50%, -50%);">
                    <h3>إضافة تلميذ جديد</h3>
                    <form onsubmit="event.preventDefault(); saveNewStudent();">
                        <div class="form-group">
                            <label>الاسم:</label>
                            <input type="text" id="newStudentFirstName" required placeholder="أدخل الاسم">
                        </div>
                        <div class="form-group">
                            <label>اللقب:</label>
                            <input type="text" id="newStudentLastName" required placeholder="أدخل اللقب">
                        </div>
                        <div class="form-group">
                            <label>القسم:</label>
                            <select id="newStudentClass" required>
                                <option value="1AM1">1AM1</option>
                                <option value="1AM2">1AM2</option>
                                <option value="1AM3">1AM3</option>
                                <option value="1AM4">1AM4</option>
                                <option value="2AM1">2AM1</option>
                                <option value="2AM2">2AM2</option>
                                <option value="2AM3">2AM3</option>
                                <option value="3AM1">3AM1</option>
                                <option value="3AM2">3AM2</option>
                                <option value="3AM3">3AM3</option>
                                <option value="4AM1">4AM1</option>
                                <option value="4AM2">4AM2</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>تاريخ الميلاد:</label>
                            <input type="date" id="newStudentBirthDate">
                        </div>
                        <div style="display: flex; gap: 10px; justify-content: flex-end;">
                            <button type="submit" class="add-button">حفظ</button>
                            <button type="button" class="remove-button" onclick="closeModal('addStudentModal')">إلغاء</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>

        <!-- Daily Record Section -->
        <div id="dailyRecord" class="section">
            <div class="section-header">
                <div>
                    <button class="add-button" onclick="addDailyRow()" style="margin-left: 10px;">➕ إضافة صف</button>
                    <button class="add-button" onclick="exportDailyToExcel()">📤 تصدير إلى Excel</button>
                </div>
                <h2 class="section-title">📖 الدفتر اليومي</h2>
                <button class="back-button" onclick="goBack()" data-translate-key="backToMain">العودة للقائمة الرئيسية</button>
            </div>

            <div style="overflow:auto; max-height: 75vh; border:1px solid #e0e6ff; border-radius:10px;">
                <table id="dailyRecordTable" class="excel-table">
                    <colgroup>
                        <col style="width: 10%">
                        <col style="width: 10%">
                        <col style="width: 9%">
                        <col style="width: 9%">
                        <col style="width: 9%">
                        <col style="width: 9%">
                        <col style="width: 10%">
                        <col style="width: 25%"> 
                        <col style="width: 9%">
                    </colgroup>
                    <thead>
                        <tr>
                            <th>📅 التاريخ</th>
                            <th>⏰ التوقيت</th>
                            <th>🏫 القسم</th>
                            <th>📘 الميدان</th>
                            <th>📗 المقطع</th>
                            <th>📚 المورد</th>
                            <th>📌 النشاط</th>
                            <th>✏ سير النشاط</th>
                            <th>📝 ملاحظات</th>
                        </tr>
                    </thead>
                    <tbody id="dailyRecordTableBody">
                        <!-- Sample data will be loaded here -->
                    </tbody>
                </table>
            </div>

            <!-- Suggestions lists for inputs -->
            <datalist id="timeSuggestions">
                <option value="08:00 – 09:00">
                <option value="09:00 – 10:00">
                <option value="10:00 – 11:00">
                <option value="11:00 – 12:00">
                <option value="08:00 – 10:00">
                <option value="10:00 – 12:00">
                <option value="14:00 – 15:00">
                <option value="15:00 – 16:00">
                <option value="16:00 – 17:00">
                <option value="14:00 – 16:00">
            </datalist>
            <datalist id="weekSuggestions">
                <option value="الأسبوع 1"></option>
                <option value="الأسبوع 2"></option>
                <option value="الأسبوع 3"></option>
                <option value="الأسبوع 4"></option>
                <option value="الأسبوع 5"></option>
                <option value="الأسبوع 6"></option>
                <option value="الأسبوع 7"></option>
                <option value="الأسبوع 8"></option>
                <option value="الأسبوع 9"></option>
                <option value="الأسبوع 10"></option>
                <option value="الأسبوع 11"></option>
                <option value="الأسبوع 12"></option>
                <option value="الأسبوع 13"></option>
                <option value="الأسبوع 14"></option>
                <option value="الأسبوع 15"></option>
                <option value="الأسبوع 16"></option>
                <option value="الأسبوع 17"></option>
                <option value="الأسبوع 18"></option>
                <option value="الأسبوع 19"></option>
                <option value="الأسبوع 20"></option>
                <option value="الأسبوع 21"></option>
                <option value="الأسبوع 22"></option>
                <option value="الأسبوع 23"></option>
                <option value="الأسبوع 24"></option>
                <option value="الأسبوع 25"></option>
                <option value="الأسبوع 26"></option>
                <option value="الأسبوع 27"></option>
                <option value="الأسبوع 28"></option>
                <option value="الأسبوع 29"></option>
                <option value="الأسبوع 30"></option>
                <option value="الأسبوع 31"></option>
                <option value="الأسبوع 32"></option>
                <option value="الأسبوع 33"></option>
                <option value="الأسبوع 34"></option>
                <option value="الأسبوع 35"></option>
                <option value="الأسبوع 36"></option>
                <option value="الأسبوع 37"></option>
                <option value="الأسبوع 38"></option>
                <option value="الأسبوع 39"></option>
                <option value="الأسبوع 40"></option>
            </datalist>
            <datalist id="activitySuggestions">
                <option value="1"></option>
                <option value="2"></option>
                <option value="3"></option>
                <option value="4"></option>
                <option value="5"></option>
                <option value="6"></option>
            </datalist>
            <datalist id="classSuggestions">
                <option value="1AM1"></option>
                <option value="1AM2"></option>
                <option value="1AM3"></option>
                <option value="1AM4"></option>
                <option value="2AM1"></option>
                <option value="2AM2"></option>
                <option value="2AM3"></option>
                <option value="3AM1"></option>
                <option value="3AM2"></option>
                <option value="3AM3"></option>
                <option value="4AM1"></option>
                <option value="4AM2"></option>
            </datalist>
            <datalist id="fieldSuggestions">
                <option value="الميدان الأول"></option>
                <option value="الميدان الثاني"></option>
                <option value="الميدان الثالث"></option>
                <option value="الميدان الرابع"></option>
            </datalist>
            <datalist id="sectionSuggestions">
                <option value="المقطع الأول"></option>
                <option value="المقطع الثاني"></option>
                <option value="المقطع الثالث"></option>
                <option value="المقطع الرابع"></option>
            </datalist>
            <datalist id="resourceSuggestions">
                <option value="المورد الأول"></option>
                <option value="المورد الثاني"></option>
                <option value="المورد الثالث"></option>
                <option value="المورد الرابع"></option>
                <option value="المورد الخامس"></option>
                <option value="المورد السادس"></option>
            </datalist>
        </div>

        <!-- Lessons Section -->
        <div id="lessons" class="section">
            <div class="section-header">
                <h2 class="section-title">📚 الدروس</h2>
                <button class="back-button" onclick="goBack()" data-translate-key="backToMain">العودة للقائمة الرئيسية</button>
            </div>
            
            <div class="tabs">
                <button class="tab-button active" onclick="showTab('firstYear', event)">السنة الأولى متوسط</button>
                <button class="tab-button" onclick="showTab('secondYear', event)">السنة الثانية متوسط</button>
                <button class="tab-button" onclick="showTab('thirdYear', event)">السنة الثالثة متوسط</button>
                <button class="tab-button" onclick="showTab('fourthYear', event)">السنة الرابعة متوسط</button>
            </div>

            <div id="firstYear" class="tab-content active">
                <h3>دروس السنة الأولى متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('lesson1Upload').click()">
                    <p>📁 اضغط هنا لإضافة درس جديد</p>
                    <input type="file" id="lesson1Upload" accept=".pdf" style="display: none;" onchange="handleLessonUpload(this, 'firstYear')">
                </div>
                <div id="firstYearLessons" class="lessons-container">
                    <!-- Lessons will be added here -->
                </div>
            </div>

            <div id="secondYear" class="tab-content">
                <h3>دروس السنة الثانية متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('lesson2Upload').click()">
                    <p>📁 اضغط هنا لإضافة درس جديد</p>
                    <input type="file" id="lesson2Upload" accept=".pdf" style="display: none;" onchange="handleLessonUpload(this, 'secondYear')">
                </div>
                <div id="secondYearLessons" class="lessons-container">
                    <!-- Lessons will be added here -->
                </div>
            </div>

            <div id="thirdYear" class="tab-content">
                <h3>دروس السنة الثالثة متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('lesson3Upload').click()">
                    <p>📁 اضغط هنا لإضافة درس جديد</p>
                    <input type="file" id="lesson3Upload" accept=".pdf" style="display: none;" onchange="handleLessonUpload(this, 'thirdYear')">
                </div>
                <div id="thirdYearLessons" class="lessons-container">
                    <!-- Lessons will be added here -->
                </div>
            </div>

            <div id="fourthYear" class="tab-content">
                <h3>دروس السنة الرابعة متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('lesson4Upload').click()">
                    <p>📁 اضغط هنا لإضافة درس جديد</p>
                    <input type="file" id="lesson4Upload" accept=".pdf" style="display: none;" onchange="handleLessonUpload(this, 'fourthYear')">
                </div>
                <div id="fourthYearLessons" class="lessons-container">
                    <!-- Lessons will be added here -->
                </div>
            </div>
        </div>

        <!-- Presentations Section -->
        <div id="presentations" class="section">
            <div class="section-header">
                <h2 class="section-title">🎥 العروض والتجارب</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            
            <div class="tabs">
                <button class="tab-button active" onclick="showTab('presentations1', event)">السنة الأولى متوسط</button>
                <button class="tab-button" onclick="showTab('presentations2', event)">السنة الثانية متوسط</button>
                <button class="tab-button" onclick="showTab('presentations3', event)">السنة الثالثة متوسط</button>
                <button class="tab-button" onclick="showTab('presentations4', event)">السنة الرابعة متوسط</button>
            </div>

            <div id="presentations1" class="tab-content active">
                <h3>عروض السنة الأولى متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('pres1Upload').click()">
                    <p>🎬 اضغط هنا لإضافة عرض جديد (PowerPoint, Video)</p>
                    <input type="file" id="pres1Upload" accept=".ppt,.pptx,.mp4,.avi,.mov" style="display: none;" onchange="handlePresentationUpload(this, 'presentations1')">
                </div>
                <div id="presentations1Container" class="lessons-container">
                    <!-- Presentations will be added here -->
                </div>
            </div>

            <div id="presentations2" class="tab-content">
                <h3>عروض السنة الثانية متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('pres2Upload').click()">
                    <p>🎬 اضغط هنا لإضافة عرض جديد (PowerPoint, Video)</p>
                    <input type="file" id="pres2Upload" accept=".ppt,.pptx,.mp4,.avi,.mov" style="display: none;" onchange="handlePresentationUpload(this, 'presentations2')">
                </div>
                <div id="presentations2Container" class="lessons-container">
                    <!-- Presentations will be added here -->
                </div>
            </div>

            <div id="presentations3" class="tab-content">
                <h3>عروض السنة الثالثة متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('pres3Upload').click()">
                    <p>🎬 اضغط هنا لإضافة عرض جديد (PowerPoint, Video)</p>
                    <input type="file" id="pres3Upload" accept=".ppt,.pptx,.mp4,.avi,.mov" style="display: none;" onchange="handlePresentationUpload(this, 'presentations3')">
                </div>
                <div id="presentations3Container" class="lessons-container">
                    <!-- Presentations will be added here -->
                </div>
            </div>

            <div id="presentations4" class="tab-content">
                <h3>عروض السنة الرابعة متوسط</h3>
                <div class="file-upload" onclick="document.getElementById('pres4Upload').click()">
                    <p>🎬 اضغط هنا لإضافة عرض جديد (PowerPoint, Video)</p>
                    <input type="file" id="pres4Upload" accept=".ppt,.pptx,.mp4,.avi,.mov" style="display: none;" onchange="handlePresentationUpload(this, 'presentations4')">
                </div>
                <div id="presentations4Container" class="lessons-container">
                    <!-- Presentations will be added here -->
                </div>
            </div>
        </div>

        <!-- Settings Section -->
        <div id="settings" class="section">
            <div class="section-header">
                <h2 class="section-title">⚙️ الإعدادات</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            
            <div class="settings-grid">
                <div class="settings-section">
                    <h3>🌍 إعدادات اللغة</h3>
                    <div class="form-group">
                        <label>اللغة:</label>
                        <select id="languageSelect" onchange="setLanguage(this.value)">
                            <option value="ar">العربية</option>
                            <option value="fr">Français</option>
                            <option value="en">English</option>
                        </select>
                    </div>
                </div>

                <div class="settings-section">
                    <h3>🎨 إعدادات المظهر</h3>
                    <div class="form-group">
                        <label>المظهر:</label>
                        <select id="themeSelect" onchange="changeTheme()">
                            <option value="light">الوضع الفاتح</option>
                            <option value="dark">الوضع الداكن</option>
                            <option value="blue">الوضع الأزرق</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>حجم الخط:</label>
                        <select id="fontSizeSelect" onchange="changeFontSize()">
                            <option value="small">صغير</option>
                            <option value="medium" selected>متوسط</option>
                            <option value="large">كبير</option>
                        </select>
                    </div>
                </div>

                <div class="settings-section">
                    <h3>💾 إعدادات البيانات</h3>
                    <button class="add-button" onclick="exportData()">📤 تصدير البيانات</button>
                    <button class="add-button" onclick="importData()">📥 استيراد البيانات</button>
                    <button class="add-button" onclick="clearAllData()" style="background: #dc3545;">🗑️ حذف جميع البيانات</button>
                </div>

                <div class="settings-section">
                    <h3>🔔 إعدادات التنبيهات</h3>
                    <div class="form-group">
                        <label>
                            <input type="checkbox" id="enableNotifications" onchange="toggleNotifications()"> 
                            تفعيل التنبيهات
                        </label>
                    </div>
                    <div class="form-group">
                        <label>
                            <input type="checkbox" id="autoSave" onchange="toggleAutoSave()"> 
                            الحفظ التلقائي
                        </label>
                    </div>
                </div>
            </div>
        </div>

        <!-- Calendar Section -->
        <div id="calendar" class="section">
            <div class="section-header">
                <h2 class="section-title">📅 التقويم الشهري</h2>
                <div class="calendar-header-controls">
                    <button class="action-btn" onclick="prevMonth()">🗺️ عرض الشهر السابق</button>
                    <button class="action-btn" onclick="nextMonth()">🗺️ عرض الشهر التالي</button>
                    <button class="action-btn" onclick="exportCalendarICS()">📤 تصدير التقويم</button>
                    <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
                </div>
            </div>

            <div id="calendarControls" style="margin-bottom:12px; display:flex; justify-content:space-between; align-items:center;">
                <div id="currentMonthLabel" style="font-weight:bold;"></div>
                <div>
                    <select id="calendarClassSelect" onchange="renderCalendar(currentYear, currentMonth)"></select>
                </div>
            </div>

            <div id="calendarGrid" class="calendar-grid" aria-live="polite"></div>
        </div>

        <!-- Calendar Modal -->
        <div id="calendarModal" class="modal-backdrop" role="dialog" aria-hidden="true">
            <div class="modal-content">
                <h3 id="modalTitle">إضافة حدث</h3>
                <form id="calendarEventForm" onsubmit="event.preventDefault(); saveCalendarEvent();">
                    <div class="form-group">
                        <label>نوع الحدث:</label>
                        <select id="eventType" required>
                            <option value="lesson">درس</option>
                            <option value="exam">امتحان</option>
                            <option value="meeting">اجتماع</option>
                            <option value="note">ملاحظة</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>التاريخ:</label>
                        <input type="date" id="eventDate" required>
                    </div>
                    <div class="form-group">
                        <label>الوقت:</label>
                        <input type="time" id="eventTime">
                    </div>
                    <div class="form-group">
                        <label>القسم المعني:</label>
                        <select id="eventClassSelect"></select>
                    </div>
                    <div class="form-group">
                        <label>الوصف:</label>
                        <textarea id="eventDescription" rows="3"></textarea>
                    </div>
                    <div style="display:flex; gap:10px; justify-content:flex-end;">
                        <button type="submit" class="add-button">حفظ</button>
                        <button type="button" class="remove-button" onclick="closeCalendarModal()">إلغاء</button>
                    </div>
                </form>
            </div>
        </div>

        <!-- Lesson Planner Section -->
        <div id="lessonPlanner" class="section">
            <div class="section-header">
                <h2 class="section-title">📝 تخطيط الدروس</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            
            <form id="lessonPlanForm" onsubmit="event.preventDefault(); saveLessonPlan();">
                <div class="form-grid">
                    <div class="form-group">
                        <label>عنوان الدرس:</label>
                        <input type="text" id="lessonTitle" required>
                    </div>
                    <div class="form-group">
                        <label>المادة:</label>
                        <input type="text" id="lessonSubject" required>
                    </div>
                    <div class="form-group">
                        <label>المدة (دقيقة):</label>
                        <input type="number" id="lessonDuration" min="15" max="120" required>
                    </div>
                </div>
                
                <div class="form-group">
                    <label>الأهداف:</label>
                    <textarea id="lessonObjectives" rows="3" placeholder="اكتب أهداف الدرس..."></textarea>
                </div>
                
                <div class="form-group">
                    <label>الأنشطة:</label>
                    <div id="activitiesList">
                        <!-- Activities will be added here -->
                    </div>
                    <button type="button" class="add-button" onclick="addActivityItem()">➕ إضافة نشاط</button>
                </div>
                
                <button type="submit" class="add-button">💾 حفظ خطة الدرس</button>
            </form>
            
            <h3 style="margin-top: 30px;">خطط الدروس المحفوظة</h3>
            <div id="lessonPlansList">
                <!-- Lesson plans will be displayed here -->
            </div>
        </div>

        <!-- Parents Section -->
        <div id="parents" class="section">
            <div class="section-header">
                <h2 class="section-title">👥 التواصل مع الأولياء</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            
            <div class="tabs">
                <button class="tab-button active" onclick="showTab('parentMessages', event)">📧 الرسائل</button>
                <button class="tab-button" onclick="showTab('parentWork', event)">📚 أعمال التلاميذ</button>
            </div>
            
            <!-- Parent Messages Tab -->
            <div id="parentMessages" class="tab-content active">
                <form id="parentMessageForm" onsubmit="event.preventDefault(); sendParentMessage();">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>المستلمون:</label>
                            <select id="messageRecipients" multiple required>
                                <!-- Students will be populated here -->
                            </select>
                        </div>
                        <div class="form-group">
                            <label>الموضوع:</label>
                            <input type="text" id="messageSubject" placeholder="موضوع الرسالة">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>نص الرسالة:</label>
                        <textarea id="messageContent" rows="5" placeholder="اكتب رسالتك هنا..." required></textarea>
                    </div>
                    
                    <button type="submit" class="add-button">📤 إرسال الرسالة</button>
                </form>
                
                <h3 style="margin-top: 30px;">الرسائل المرسلة</h3>
                <div id="parentMessagesList">
                    <!-- Messages will be displayed here -->
                </div>
            </div>
            
            <!-- Parent Work Tab -->
            <div id="parentWork" class="tab-content">
                <div class="form-group">
                    <label>القسم:</label>
                    <select id="parentWorkClass" onchange="updateParentWorkStudents()">
                        <!-- Classes will be populated here -->
                    </select>
                </div>
                
                <div class="form-group">
                    <label>التلميذ:</label>
                    <select id="parentWorkStudent">
                        <!-- Students will be populated here -->
                    </select>
                </div>
                
                <div class="file-upload" onclick="document.getElementById('parentWorkUpload').click()">
                    <p>📁 اضغط هنا لإضافة أعمال التلميذ</p>
                    <input type="file" id="parentWorkUpload" accept="image/*,.pdf,.doc,.docx" style="display: none;" onchange="handleWorkUpload(this)">
                </div>
                
                <div id="workGallery" style="display: flex; flex-wrap: wrap; gap: 10px; margin-top: 20px;">
                    <!-- Work images will be displayed here -->
                </div>
            </div>
        </div>

        <!-- Assignments Section moved to التلاميذ tab -->
            
            <!-- Homework Tracking Modal -->
            <div id="homeworkTrackingModal" class="modal" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); z-index: 9999;">
                <div class="modal-content" style="background: white; padding: 30px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.2); width: 90%; max-width: 1200px; max-height: 85vh; overflow-y: auto; position: absolute; top: 5%; left: 5%; transform: none;">
                    <h3 id="trackingModalTitle">تتبع الواجب</h3>
                    
                    <div class="homework-info" style="background: #f8f9ff; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
                        <div id="homeworkInfoContent"></div>
                    </div>
                    

                    
                    <div class="table-container">
                        <table class="excel-table">
                            <thead>
                                <tr>
                                    <th>#</th>
                                    <th>اسم التلميذ</th>
                                    <th>القسم</th>
                                    <th>حالة التسليم</th>
                                    <th>تاريخ التسليم</th>
                                    <th>النقاط</th>
                                    <th>حفظ</th>
                                    <th>الحالة</th>
                                </tr>
                            </thead>
                            <tbody id="homeworkTrackingStudentsBody">
                                <!-- Students will be listed here -->
                            </tbody>
                        </table>
                    </div>
                    
                    <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px;">
                        <button class="add-button" onclick="saveHomeworkTracking()">💾 حفظ التتبع</button>
                        <button class="remove-button" onclick="resetHomeworkPoints()" style="background: #6c757d;">🔄 إعادة تعيين النقاط</button>
                        <button class="add-button" onclick="debugHomeworkTracking()" style="background: #ffc107; color: #000;">🐛 تصحيح</button>
                        <button class="remove-button" onclick="closeHomeworkTrackingModal()">إغلاق</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Quiz Builder Section -->
        <div id="quizBuilder" class="section">
            <div class="section-header">
                <h2 class="section-title">❓ منشئ الاختبارات</h2>
                <button class="back-button" onclick="goBack()">العودة للقائمة الرئيسية</button>
            </div>
            
            <div class="quiz-builder-container">
                <div class="quiz-form">
                    <h3>📝 إنشاء اختبار جديد</h3>
                    <form id="quizForm" onsubmit="event.preventDefault(); saveQuiz();">
                        <div class="form-group">
                            <label>عنوان الاختبار:</label>
                            <input type="text" id="quizTitle" required placeholder="أدخل عنوان الاختبار">
                        </div>
                        
                        <div class="form-group">
                            <label>القسم:</label>
                            <select id="quizClass" required>
                                <option value="">اختر القسم</option>
                                <option value="1AM1">1AM1</option>
                                <option value="1AM2">1AM2</option>
                                <option value="1AM3">1AM3</option>
                                <option value="2AM1">2AM1</option>
                                <option value="2AM2">2AM2</option>
                                <option value="2AM3">2AM3</option>
                                <option value="3AM1">3AM1</option>
                                <option value="3AM2">3AM2</option>
                                <option value="3AM3">3AM3</option>
                                <option value="4AM1">4AM1</option>
                                <option value="4AM2">4AM2</option>
                            </select>
                        </div>
                        
                        <div class="form-group">
                            <label>مدة الاختبار (دقيقة):</label>
                            <input type="number" id="quizDuration" min="15" max="120" value="45" required>
                        </div>
                        
                        <div class="form-group">
                            <label>الدرجة القصوى:</label>
                            <input type="number" id="quizMaxScore" min="10" max="100" value="20" required>
                        </div>
                    </form>
                </div>
                
                <div class="questions-section">
                    <h3>❓ الأسئلة</h3>
                    <div id="questionsContainer">
                        <!-- Questions will be added here -->
                    </div>
                    <button type="button" class="add-button" onclick="addQuestion()">➕ إضافة سؤال</button>
                </div>
                
                <div class="quiz-actions">
                    <button type="button" class="add-button" onclick="previewQuiz()">👁️ معاينة الاختبار</button>
                    <button type="button" class="add-button" onclick="saveQuiz()">💾 حفظ الاختبار</button>
                    <button type="button" class="add-button" onclick="exportQuizJSON()">📤 تصدير JSON</button>
                </div>
            </div>
            
            <div class="saved-quizzes">
                <h3>📚 الاختبارات المحفوظة</h3>
                <div id="quizzesList">
                    <!-- Saved quizzes will be displayed here -->
                </div>
            </div>
        </div>
    </div>

        <script>
        // Global variables declaration
        let studentsData = {};
        let gradesData = {};
        let attendanceData = {};
        let rewardsData = {};
        let calendarEvents = {};
        let lessonPlans = [];
        let parentMessages = [];
        let assignmentsData = [];
        let behaviorData = {};
        let quizzes = [];
        let lessonsData = {};
        let presentationsData = {};
        let dailyRecords = [];

        // Constants for localStorage keys
        const CAL_KEY = 'calendarEvents_v1';
        const LESSONS_KEY = 'lessonPlans_v1';
        const PARENTS_KEY = 'parentMessages_v1';
        const ASSIGN_KEY = 'assignments_v1';
        const BEHAV_KEY = 'behaviorData_v1';
        const QUIZ_KEY = 'quizzes_v1';

        // Quiz Builder System
        quizzes = JSON.parse(localStorage.getItem(QUIZ_KEY) || '[]');

    function addQuestion(data = {}) {
        const container = document.getElementById('questionsContainer');
        const qid = Date.now();
        const div = document.createElement('div'); 
        div.className = 'question-item';
        div.dataset.id = qid;
        div.innerHTML = `
            <input type="text" placeholder="نص السؤال" class="question-text" value="${data.text||''}">
            <select class="question-type" onchange="updateQuestionOptions(this)">
                <option value="multiple"${data.type === 'multiple' ? ' selected' : ''}>اختيار من متعدد</option>
                <option value="true-false"${data.type === 'true-false' ? ' selected' : ''}>صح/خطأ</option>
                <option value="short"${data.type === 'short' ? ' selected' : ''}>إجابة قصيرة</option>
            </select>
            <div class="options-container"></div>
            <select class="correct-answer"><option>اختر الإجابة الصحيحة</option></select>
            <button class="remove-button" type="button" onclick="this.parentElement.remove()">حذف السؤال</button>
        `;
        container.appendChild(div);
        
        // Initialize options based on question type
        updateQuestionOptions(div.querySelector('.question-type'));
        
        // If data has options, populate them
        if (data.options && data.options.length > 0) {
            const optionsContainer = div.querySelector('.options-container');
            const inputs = optionsContainer.querySelectorAll('.option');
            data.options.forEach((opt, i) => {
                if (inputs[i]) inputs[i].value = opt;
            });
        }
    }

    function updateQuestionOptions(selectElement) {
        const questionItem = selectElement.closest('.question-item');
        const optionsContainer = questionItem.querySelector('.options-container');
        const correctSelect = questionItem.querySelector('.correct-answer');
        const questionType = selectElement.value;
        
        optionsContainer.innerHTML = '';
        correctSelect.innerHTML = '<option>اختر الإجابة الصحيحة</option>';
        
        if (questionType === 'multiple') {
            // Add 4 option inputs
            for (let i = 0; i < 4; i++) {
                const input = document.createElement('input');
                input.className = 'option';
                input.placeholder = `الخيار ${i + 1}`;
                input.addEventListener('input', () => updateCorrectAnswers(questionItem));
                optionsContainer.appendChild(input);
            }
            
            // Add button to add more options
            const addOptBtn = document.createElement('button');
            addOptBtn.type = 'button';
            addOptBtn.className = 'action-btn';
            addOptBtn.textContent = '➕ خيار إضافي';
            addOptBtn.onclick = () => {
                const input = document.createElement('input');
                input.className = 'option';
                input.placeholder = 'خيار جديد';
                input.addEventListener('input', () => updateCorrectAnswers(questionItem));
                optionsContainer.insertBefore(input, addOptBtn);
                updateCorrectAnswers(questionItem);
            };
            optionsContainer.appendChild(addOptBtn);
            
        } else if (questionType === 'true-false') {
            // Add true/false options
            const trueInput = document.createElement('input');
            trueInput.className = 'option';
            trueInput.value = 'صح';
            trueInput.readOnly = true;
            optionsContainer.appendChild(trueInput);
            
            const falseInput = document.createElement('input');
            falseInput.className = 'option';
            falseInput.value = 'خطأ';
            falseInput.readOnly = true;
            optionsContainer.appendChild(falseInput);
            
            correctSelect.innerHTML = '<option>اختر الإجابة الصحيحة</option><option value="صح">صح</option><option value="خطأ">خطأ</option>';
        }
        // For 'short' type, no options needed
    }

    function updateCorrectAnswers(questionItem) {
        const correctSelect = questionItem.querySelector('.correct-answer');
        const options = Array.from(questionItem.querySelectorAll('.option')).map(input => input.value.trim()).filter(val => val);
        
        correctSelect.innerHTML = '<option>اختر الإجابة الصحيحة</option>';
        options.forEach(option => {
            const optionElement = document.createElement('option');
            optionElement.value = option;
            optionElement.textContent = option;
            correctSelect.appendChild(optionElement);
        });
    }

    function saveQuiz() {
        const title = document.getElementById('quizTitle').value.trim();
        if (!title) { 
            showNotification('أدخل عنوان الاختبار', 'error'); 
            return; 
        }
        
        const questions = [];
        const questionItems = document.querySelectorAll('#questionsContainer .question-item');
        
        if (questionItems.length === 0) {
            showNotification('أضف سؤال واحد على الأقل', 'error');
            return;
        }
        
        let hasError = false;
        questionItems.forEach(qi => {
            const text = qi.querySelector('.question-text').value.trim();
            const type = qi.querySelector('.question-type').value;
            const options = Array.from(qi.querySelectorAll('.option')).map(i => i.value.trim()).filter(val => val);
            const correct = qi.querySelector('.correct-answer').value;
            
            if (!text) {
                showNotification('أدخل نص السؤال', 'error');
                hasError = true;
                return;
            }
            
            if ((type === 'multiple' || type === 'true-false') && !correct) {
                showNotification('اختر الإجابة الصحيحة', 'error');
                hasError = true;
                return;
            }
            
            questions.push({ text, type, options, correct });
        });
        
        if (hasError) return;
        
        const quiz = {
            id: Date.now(),
            title,
            instructions: document.getElementById('quizInstructions').value,
            duration: document.getElementById('quizDuration').value || 30,
            questions,
            createdAt: new Date().toISOString()
        };
        
        quizzes.unshift(quiz);
        localStorage.setItem(QUIZ_KEY, JSON.stringify(quizzes));
        renderQuizzes();
        showNotification('تم حفظ الاختبار بنجاح', 'success');
        
        // Reset form
        document.getElementById('quizForm').reset();
        document.getElementById('questionsContainer').innerHTML = '';
    }

    function renderQuizzes() {
        const container = document.getElementById('quizzesList');
        if (!container) {
            console.log('Quiz container not found, skipping render');
            return;
        }
        
        container.innerHTML = '';
        
        if (quizzes.length === 0) {
            container.innerHTML = '<p>لا توجد اختبارات محفوظة</p>';
            return;
        }
        
        quizzes.forEach(quiz => {
            const div = document.createElement('div');
            div.className = 'lesson-item';
            div.innerHTML = `
                <div class="quiz-info">
                    <strong>${quiz.title}</strong>
                    <p>${quiz.questions.length} سؤال - ${quiz.duration} دقيقة</p>
                    <small>تاريخ الإنشاء: ${new Date(quiz.createdAt).toLocaleDateString('ar-EG')}</small>
                </div>
                <div class="quiz-actions">
                    <button class="add-button" onclick="exportQuizJSON(${quiz.id})">📤 تصدير JSON</button>
                    <button class="add-button" onclick="previewQuiz(${quiz.id})">👁️ معاينة</button>
                    <button class="remove-button" onclick="deleteQuiz(${quiz.id})">🗑️ حذف</button>
                </div>
            `;
            container.appendChild(div);
        });
    }

    function exportQuizJSON(id) {
        const quiz = quizzes.find(q => q.id === id);
        if (!quiz) return;
        
        const blob = new Blob([JSON.stringify(quiz, null, 2)], { type: 'application/json' });
        downloadBlob(blob, `quiz_${quiz.title.replace(/[^a-zA-Z0-9]/g, '_')}.json`);
        showNotification('تم تصدير الاختبار', 'success');
    }

    function previewQuiz(id) {
        const quiz = quizzes.find(q => q.id === id);
        if (!quiz) return;
        
        let previewHTML = `
            <h2>${quiz.title}</h2>
            <p><strong>التعليمات:</strong> ${quiz.instructions || 'لا توجد تعليمات'}</p>
            <p><strong>المدة:</strong> ${quiz.duration} دقيقة</p>
            <hr>
        `;
        
        quiz.questions.forEach((q, index) => {
            previewHTML += `
                <div class="question-preview">
                    <h4>السؤال ${index + 1}: ${q.text}</h4>
                    <p><strong>النوع:</strong> ${getQuestionTypeName(q.type)}</p>
            `;
            
            if (q.options && q.options.length > 0) {
                previewHTML += '<p><strong>الخيارات:</strong></p><ul>';
                q.options.forEach(option => {
                    const isCorrect = option === q.correct ? ' ✓' : '';
                    previewHTML += `<li>${option}${isCorrect}</li>`;
                });
                previewHTML += '</ul>';
            }
            
            if (q.correct) {
                previewHTML += `<p><strong>الإجابة الصحيحة:</strong> ${q.correct}</p>`;
            }
            
            previewHTML += '</div><hr>';
        });
        
        openModal(`معاينة الاختبار - ${quiz.title}`, previewHTML, 'large');
    }

    function getQuestionTypeName(type) {
        const types = {
            'multiple': 'اختيار من متعدد',
            'true-false': 'صح/خطأ',
            'short': 'إجابة قصيرة'
        };
        return types[type] || type;
    }

    function deleteQuiz(id) {
        if (confirm('هل أنت متأكد من حذف هذا الاختبار؟')) {
            quizzes = quizzes.filter(q => q.id !== id);
            localStorage.setItem(QUIZ_KEY, JSON.stringify(quizzes));
            renderQuizzes();
            showNotification('تم حذف الاختبار', 'success');
        }
    }

    function initQuizBuilder() {
        quizzes = JSON.parse(localStorage.getItem(QUIZ_KEY) || '[]');
        renderQuizzes();
    }

    // Backup & Restore System with Encryption
    const BACKUP_KEY = 'backupSettings_v1';
        calendarEvents = JSON.parse(localStorage.getItem(CAL_KEY) || '{}');
        let currentDate = new Date();
        let currentYear = currentDate.getFullYear();
        let currentMonth = currentDate.getMonth();

        function initCalendar() {
            const grid = document.getElementById('calendarGrid');
            const label = document.getElementById('currentMonthLabel');
            
            // Only initialize if calendar elements exist
            if (grid && label) {
                updateCalendarClassSelects();
                renderCalendar(currentYear, currentMonth);
            }
        }

        function updateCalendarClassSelects() {
            const sel = document.getElementById('calendarClassSelect');
            const evSel = document.getElementById('eventClassSelect');
            if (!sel || !evSel) return;
            sel.innerHTML = '';
            evSel.innerHTML = '';
            const classes = Object.keys(studentsData).sort();
            classes.forEach(cl => {
                const o = document.createElement('option'); o.value = cl; o.textContent = cl; sel.appendChild(o);
                const o2 = o.cloneNode(true); evSel.appendChild(o2);
            });
        }

        function renderCalendar(year, month) {
            const grid = document.getElementById('calendarGrid');
            const label = document.getElementById('currentMonthLabel');
            
            // Check if elements exist before proceeding
            if (!grid || !label) {
                console.log('Calendar elements not found, skipping render');
                return;
            }
            
            currentYear = year; currentMonth = month;
            const first = new Date(year, month, 1);
            const startDay = first.getDay(); // 0 (Sun) .. 6
            const daysInMonth = new Date(year, month + 1, 0).getDate();

            // For RTL week starting Monday for Arabic schools, adjust if needed.
            // We'll display Sun..Sat to match grid semantics; you can change.
            label.textContent = `${year} - ${month+1}`;

            // build 7x6 matrix
            grid.innerHTML = '';
            const totalCells = 42;
            let dayCounter = 1 - startDay; // so that first cell corresponds
            for (let i=0;i<totalCells;i++, dayCounter++) {
                const cell = document.createElement('div');
                cell.className = 'calendar-day';
                if (dayCounter < 1 || dayCounter > daysInMonth) {
                    cell.innerHTML = `<div class="date-label calendar-empty"></div>`;
                    grid.appendChild(cell);
                    continue;
                }
                const dateKey = `${year}-${String(month+1).padStart(2,'0')}-${String(dayCounter).padStart(2,'0')}`;
                const dateLabel = document.createElement('div');
                dateLabel.className = 'date-label';
                dateLabel.textContent = dayCounter;
                cell.appendChild(dateLabel);

                // events for this date
                const events = calendarEvents[dateKey] || [];
                events.forEach((ev, idx) => {
                    const evEl = document.createElement('div');
                    evEl.className = 'calendar-event ' + ('event-' + (ev.type || 'note'));
                    evEl.textContent = (ev.type ? {'lesson':'درس','exam':'امتحان','meeting':'اجتماع','note':'ملاحظة'}[ev.type] + ': ' : '') + (ev.description || ev.title || '');
                    evEl.onclick = () => { openEditEventModal(dateKey, idx); };
                    cell.appendChild(evEl);
                });

                // click on cell to add event
                cell.onclick = (e) => {
                    // avoid triggering when clicking an existing event (those have onclick)
                    if (e.target !== cell && e.target.classList.contains('calendar-event')) return;
                    openAddEventModal(dateKey);
                };

                grid.appendChild(cell);
            }
        }

        function prevMonth() {
            if (currentMonth === 0) { currentMonth = 11; currentYear--; } else currentMonth--;
            renderCalendar(currentYear, currentMonth);
        }
        function nextMonth() {
            if (currentMonth === 11) { currentMonth = 0; currentYear++; } else currentMonth++;
            renderCalendar(currentYear, currentMonth);
        }

        function openAddEventModal(dateKey = null) {
            const modal = document.getElementById('calendarModal');
            if (modal) {
                modal.classList.add('show');
                document.getElementById('modalTitle').textContent = 'إضافة حدث';
                document.getElementById('eventDate').value = dateKey ? dateKey : (new Date()).toISOString().split('T')[0];
                document.getElementById('eventDescription').value = '';
                document.getElementById('eventTime').value = '';
                document.getElementById('eventType').value = 'lesson';
                document.getElementById('calendarEventForm').dataset.editing = '';
            }
        }

        function openEditEventModal(dateKey, index) {
            const events = calendarEvents[dateKey] || [];
            const ev = events[index];
            if (!ev) return;
            
            const modal = document.getElementById('calendarModal');
            if (modal) {
                modal.classList.add('show');
                document.getElementById('modalTitle').textContent = 'تعديل حدث';
                document.getElementById('eventDate').value = dateKey;
                document.getElementById('eventTime').value = ev.time || '';
                document.getElementById('eventType').value = ev.type || 'note';
                document.getElementById('eventDescription').value = ev.description || ev.title || '';
                document.getElementById('calendarEventForm').dataset.editing = `${dateKey}::${index}`;
            }
        }

        function closeCalendarModal() {
            const modal = document.getElementById('calendarModal');
            if (modal) {
                modal.classList.remove('show');
            }
        }

        function saveCalendarEvent() {
            const date = document.getElementById('eventDate').value;
            const time = document.getElementById('eventTime').value;
            const type = document.getElementById('eventType').value;
            const description = document.getElementById('eventDescription').value;
            const cls = document.getElementById('eventClassSelect').value || '';

            if (!date) { showNotification('يرجى اختيار تاريخ الحدث', 'error'); return; }

            if (!calendarEvents[date]) calendarEvents[date] = [];
            const editing = document.getElementById('calendarEventForm').dataset.editing;
            if (editing) {
                const [d, idx] = editing.split('::');
                calendarEvents[d][idx] = { type, time, description, class: cls };
            } else {
                calendarEvents[date].push({ type, time, description, class: cls });
            }
            localStorage.setItem(CAL_KEY, JSON.stringify(calendarEvents));
            closeCalendarModal();
            renderCalendar(currentYear, currentMonth);
            showNotification('تم حفظ الحدث', 'success');
        }

        function exportCalendarICS() {
            // convert all events to ICS text
            let ics = 'BEGIN:VCALENDAR\nVERSION:2.0\nPRODID:-//TeacherApp//EN\n';
            for (const date in calendarEvents) {
                (calendarEvents[date] || []).forEach((ev, idx) => {
                    const uid = `ev-${date}-${idx}@teacherapp`;
                    const dt = (ev.time ? date + 'T' + ev.time.replace(':','') + '00' : date.replace(/-/g,'' ) + 'T000000');
                    ics += 'BEGIN:VEVENT\n';
                    ics += `UID:${uid}\n`;
                    ics += `DTSTAMP:${formatDateTimeISOStringUTC(new Date())}\n`;
                    ics += `DTSTART:${dt}\n`;
                    ics += `SUMMARY:${(ev.type||'حدث')}: ${escapeICS(ev.description||'')}\n`;
                    ics += `DESCRIPTION:${escapeICS(ev.description||'')}\n`;
                    ics += 'END:VEVENT\n';
                });
            }
            ics += 'END:VCALENDAR';
            const blob = new Blob([ics], { type: 'text/calendar' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url; a.download = 'calendar.ics';
            document.body.appendChild(a); a.click(); a.remove();
            URL.revokeObjectURL(url);
        }

        function escapeICS(text) {
            return String(text).replace(/\n/g,'\\n').replace(/,/g,'\\,');
        }
        function formatDateTimeISOStringUTC(d) {
            // returns YYYYMMDDTHHMMSSZ
            const Y = d.getUTCFullYear();
            const M = String(d.getUTCMonth()+1).padStart(2,'0');
            const D = String(d.getUTCDate()).padStart(2,'0');
            const h = String(d.getUTCHours()).padStart(2,'0');
            const m = String(d.getUTCMinutes()).padStart(2,'0');
            const s = String(d.getUTCSeconds()).padStart(2,'0');
            return `${Y}${M}${D}T${h}${m}${s}Z`;
        }
        /* END: Calendar JS */

        /* START: Lesson Planner JS */
        lessonPlans = JSON.parse(localStorage.getItem(LESSONS_KEY) || '[]');

        function addActivityItem(data = {}) {
            const container = document.getElementById('activitiesList');
            const div = document.createElement('div'); div.className = 'activity-item';
            div.innerHTML = `<input type="text" class="activity-desc" placeholder="وصف النشاط" value="${data.desc||''}">
                             <input type="number" class="activity-duration" placeholder="المدة (دقيقة)" min="1" max="120" value="${data.duration||10}">
                             <button class="remove-button" type="button" onclick="this.parentElement.remove()">حذف</button>`;
            container.appendChild(div);
        }

        function saveLessonPlan() {
            const title = document.getElementById('lessonTitle').value.trim();
            if (!title) { showNotification('أدخل عنوان الدرس', 'error'); return; }
            const plan = {
                id: Date.now(),
                title,
                subject: document.getElementById('lessonSubject').value,
                duration: document.getElementById('lessonDuration').value,
                objectives: document.getElementById('lessonObjectives').value,
                activities: Array.from(document.querySelectorAll('#activitiesList .activity-item')).map(it => ({
                    desc: it.querySelector('.activity-desc').value,
                    duration: it.querySelector('.activity-duration').value
                }))
            };
            lessonPlans.unshift(plan);
            localStorage.setItem(LESSONS_KEY, JSON.stringify(lessonPlans));
            showNotification('تم حفظ خطة الدرس', 'success');
            renderLessonPlans();
            document.getElementById('lessonPlanForm').reset();
            document.getElementById('activitiesList').innerHTML = '';
            addActivityItem();
        }

        function renderLessonPlans() {
            const container = document.getElementById('lessonPlansList');
            container.innerHTML = '';
            lessonPlans.forEach(p => {
                const div = document.createElement('div');
                div.className = 'lesson-item';
                div.innerHTML = `<h4>${p.title} — ${p.subject}</h4>
                                 <p>المدة: ${p.duration} دقيقة</p>
                                 <p>الأهداف: ${p.objectives}</p>
                                 <button class="add-button" onclick='openLessonPreview(${p.id})'>عرض</button>
                                 <button class="remove-button" onclick='removeLessonPlan(${p.id})'>حذف</button>`;
                container.appendChild(div);
            });
        }

        function openLessonPreview(id) {
            const p = lessonPlans.find(x => x.id === id);
            if (!p) return;
            let html = `<h3>${p.title}</h3><p>المادة: ${p.subject}</p><p>المدة: ${p.duration}</p><p>الأهداف:<br>${p.objectives}</p><h4>الأنشطة:</h4><ul>`;
            p.activities.forEach(a => html += `<li>${a.desc} — ${a.duration} دقيقة</li>`);
            html += '</ul>';
            // simple modal: use notification container or alert
            const win = window.open('', '_blank', 'width=600,height=600');
            win.document.write(`<html><head><title>${p.title}</title></head><body>${html}</body></html>`);
        }

        function removeLessonPlan(id) {
            lessonPlans = lessonPlans.filter(x => x.id !== id);
            localStorage.setItem(LESSONS_KEY, JSON.stringify(lessonPlans));
            renderLessonPlans();
        }

        function exportLessonPlanPDF() {
            const title = document.getElementById('lessonTitle').value || 'lesson';
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            doc.text(`خطة درس: ${title}`, 20, 30);
            doc.save(`lesson_${title}.pdf`);
        }

        function initLessonPlanner() {
            lessonPlans = JSON.parse(localStorage.getItem(LESSONS_KEY) || '[]');
            renderLessonPlans();
            addActivityItem();
        }

        // Alias for compatibility
        function updateLessonPlansList() {
            renderLessonPlans();
        }
        /* END: Lesson Planning JS */

        /* START: Parents Communication JS */
        parentMessages = JSON.parse(localStorage.getItem(PARENTS_KEY) || '[]');

        function sendParentMessage() {
            const recipients = Array.from(document.getElementById('messageRecipients').selectedOptions).map(o => o.value);
            const subject = document.getElementById('messageSubject').value.trim();
            const content = document.getElementById('messageContent').value.trim();
            if (!recipients.length || !content) { showNotification('اختر المستلمين واكتب نص الرسالة', 'error'); return; }
            const msg = { id: Date.now(), recipients, subject, content, date: new Date().toISOString() };
            parentMessages.unshift(msg);
            localStorage.setItem(PARENTS_KEY, JSON.stringify(parentMessages));
            showNotification('تم إرسال الرسالة (محلياً)', 'success');
            document.getElementById('messageSubject').value = ''; document.getElementById('messageContent').value = '';
            updateParentMessagesList();
        }

        function updateParentWorkStudents() {
            const className = document.getElementById('parentWorkClass').value;
            const studentSelect = document.getElementById('parentWorkStudent');
            
            if (!className || !studentsData[className]) {
                studentSelect.innerHTML = '<option>اختر القسم أولاً</option>';
                return;
            }
            
            studentSelect.innerHTML = '<option value="">اختر التلميذ</option>';
            studentsData[className].forEach(student => {
                const option = document.createElement('option');
                option.value = student.id;
                option.textContent = student.name;
                studentSelect.appendChild(option);
            });
        }

        function updateParentMessagesList() {
            const container = document.getElementById('parentMessagesList');
            if (!parentMessages || parentMessages.length === 0) {
                container.innerHTML = '<p>لا توجد رسائل مرسلة</p>';
                return;
            }
            
            container.innerHTML = parentMessages.map(msg => `
                <div class="parent-message">
                    <div class="message-header">
                        <strong>إلى: ${msg.recipients.join(', ')}</strong>
                        <small>${new Date(msg.date).toLocaleDateString('ar-EG')}</small>
                    </div>
                    <div class="message-content">
                        <p><strong>الموضوع:</strong> ${msg.subject || 'بدون موضوع'}</p>
                        <p>${msg.content}</p>
                    </div>
                </div>
            `).join('');
        }

        function handleWorkUpload(input) {
            const file = input.files[0];
            if (file) {
                const studentId = document.getElementById('parentWorkStudent').value;
                if (!studentId) {
                    showNotification('يرجى اختيار التلميذ أولاً', 'error');
                    return;
                }
                showNotification(`تم رفع أعمال التلميذ: ${file.name}`, 'success');
            }
        }

        function handleWorkUpload(input) {
            const files = Array.from(input.files || []);
            const gallery = document.getElementById('workGallery');
            files.forEach(file => {
                const reader = new FileReader();
                reader.onload = (e) => {
                    const img = document.createElement('img');
                    img.src = e.target.result; img.style.width = '120px'; img.style.height = '80px'; img.style.objectFit='cover'; img.style.borderRadius='6px';
                    gallery.appendChild(img);
                };
                reader.readAsDataURL(file);
            });
        }
        /* END: Parents Communication JS */

        /* START: Assignments JS */
        assignmentsData = JSON.parse(localStorage.getItem(ASSIGN_KEY) || '[]');

        function updateAssignmentClassSelects() {
            const sel = document.getElementById('assignmentClass');
            if (!sel) return;
            
            // Keep the default options if no students exist yet
            if (Object.keys(studentsData).length === 0) {
                return; // Keep the default options we added in HTML
            }
            
            // Update with actual student classes
            sel.innerHTML = '<option value="">اختر القسم</option>';
            Object.keys(studentsData).sort().forEach(cl => {
                const o = document.createElement('option'); 
                o.value = cl; 
                o.textContent = cl; 
                sel.appendChild(o);
            });
        }

        function createAssignment() {
            alert('تم استدعاء الدالة!'); // Test alert
            console.log('=== CREATE ASSIGNMENT FUNCTION STARTED ===');
            
            // Get form values
            const title = document.getElementById('assignmentTitle').value.trim();
            const cls = document.getElementById('assignmentClass').value;
            const description = document.getElementById('assignmentDescription').value;
            const dueDate = document.getElementById('dueDate').value;
            const type = document.getElementById('assignmentType').value;
            const maxPoints = document.getElementById('maxPoints').value;
            
            console.log('Form values:', { title, cls, description, dueDate, type, maxPoints });
            
            // Simple validation
            if (!title) {
                alert('يرجى إدخال عنوان الواجب');
                return;
            }
            
            if (!cls) {
                alert('يرجى اختيار القسم');
                return;
            }
            
            if (!dueDate) {
                alert('يرجى اختيار تاريخ الاستحقاق');
                return;
            }
            
            // Create assignment object
            const assignment = {
                id: Date.now(),
                title: title,
                description: description,
                class: cls,
                dueDate: dueDate,
                type: type,
                maxPoints: parseInt(maxPoints) || 10,
                submissions: {}
            };
            
            console.log('Assignment object created:', assignment);
            
            // Initialize assignmentsData if it doesn't exist
            if (!assignmentsData) {
                assignmentsData = [];
            }
            
            // Add to assignments array
            assignmentsData.unshift(assignment);
            console.log('Added to assignmentsData:', assignmentsData);
            
            // Save to localStorage
            localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
            console.log('Saved to localStorage:', localStorage.getItem(ASSIGN_KEY));
            
            // Show success message
            alert('تم إنشاء الواجب بنجاح!\n\nالعنوان: ' + title + '\nالقسم: ' + cls + '\nالنوع: ' + type + '\nالتاريخ: ' + dueDate);
            
            // Clear form
            document.getElementById('assignmentForm').reset();
            
            // Update display
            renderAssignments();
            
            console.log('=== CREATE ASSIGNMENT FUNCTION COMPLETED ===');
        }

        function renderAssignments() {
            const container = document.getElementById('assignmentsList');
            const tableBody = document.getElementById('homeworkTrackingTableBody');
            
            if (!container) return;
            
            container.innerHTML = '';
            
            if (!assignmentsData || assignmentsData.length === 0) {
                container.innerHTML = '<p style="text-align: center; padding: 20px; color: #666;">لا توجد واجبات منشأة بعد. قم بإنشاء واجب جديد!</p>';
                if (tableBody) tableBody.innerHTML = '';
                return;
            }
            
            // Render Excel-like table
            if (tableBody) {
                tableBody.innerHTML = '';
                assignmentsData.forEach((a, index) => {
                    const totalStudents = (studentsData[a.class] || []).length;
                    const submittedCount = Object.values(a.submissions || {}).filter(s => s.submitted).length;
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${index + 1}</td>
                        <td><strong>${a.title}</strong></td>
                        <td>${a.class}</td>
                        <td>${getAssignmentTypeName(a.type)}</td>
                        <td>${a.dueDate}</td>
                        <td>${a.maxPoints}</td>
                        <td>${a.description || '-'}</td>
                        <td>${totalStudents}</td>
                        <td>${submittedCount}</td>
                        <td>
                            <div class="homework-actions">
                                <button class="track-btn" onclick="openHomeworkTracking(${a.id})">📊 تتبع التلاميذ</button>
                                <button class="export-btn" onclick="exportHomeworkToExcel(${a.id})">📤 تصدير Excel</button>
                            </div>
                        </td>
                    `;
                    tableBody.appendChild(row);
                });
            }
            
            // Render detailed cards
            assignmentsData.forEach(a => {
                const totalStudents = (studentsData[a.class] || []).length;
                const submittedCount = Object.values(a.submissions || {}).filter(s => s.submitted).length;
                const pct = totalStudents ? Math.round((submittedCount/totalStudents)*100) : 0;
                const div = document.createElement('div');
                div.className = 'lesson-item';
                div.innerHTML = `
                    <h4>📋 ${a.title}</h4>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin: 15px 0;">
                        <div><strong>🏫 القسم:</strong> ${a.class}</div>
                        <div><strong>📝 النوع:</strong> ${getAssignmentTypeName(a.type)}</div>
                        <div><strong>📅 تاريخ الاستحقاق:</strong> ${a.dueDate}</div>
                        <div><strong>⭐ الدرجة القصوى:</strong> ${a.maxPoints}</div>
                    </div>
                    ${a.description ? `<p><strong>📖 الوصف:</strong> ${a.description}</p>` : ''}
                    <div class="progress-bar" style="background:#f1f1f1; height:12px; border-radius:6px; overflow:hidden; margin: 15px 0;">
                        <div class="progress-fill" style="width:${pct}%; height:100%; background:linear-gradient(90deg,#28a745,#218838);"></div>
                    </div>
                    <p style="margin: 10px 0;"><strong>📊 التقدم:</strong> ${submittedCount} من أصل ${totalStudents} تلميذ سلم الواجب</p>
                    <div style="display: flex; gap: 10px; flex-wrap: wrap; margin-top: 15px;">
                        <button class="action-btn" onclick="remindLate(${a.id})">🔔 تذكير المتأخرين</button>
                        <button class="add-button" onclick="openGradeAssignment(${a.id})">📝 تصحيح الواجبات</button>
                        <button class="remove-button" onclick="deleteAssignment(${a.id})">🗑️ حذف الواجب</button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function remindLate(assignmentId) {
            // simulated reminder: mark or notify
            showNotification('تم إرسال تذكير (محلي) للتلاميذ المتأخرين', 'info');
        }

        function openGradeAssignment(assignmentId) {
            // open simple window to grade or mark submissions
            const a = assignmentsData.find(x => x.id === assignmentId);
            if (!a) return;
            const students = studentsData[a.class] || [];
            let html = `<h3>${a.title} — ${a.class}</h3>`;
            students.forEach(s => {
                const sub = a.submissions[s.id] || { submitted:false, date:'', points:0 };
                html += `<div style="padding:6px;border-bottom:1px solid #eee;">
                            <strong>${s.name}</strong>
                            <button onclick="markSubmitted(${assignmentId}, ${s.id})">+ تسليم</button>
                            <button onclick="markUnsubmitted(${assignmentId}, ${s.id})">إلغاء</button>
                            <input placeholder="نقطة" value="${sub.points}" onchange="setSubmissionPoints(${assignmentId}, ${s.id}, this.value)">
                         </div>`;
            });
            const win = window.open('', '_blank', 'width=600,height=700');
            win.document.write(`<html><body>${html}</body></html>`);
        }

        function markSubmitted(assignId, studentId) {
            const a = assignmentsData.find(x => x.id === assignId);
            if (!a) return;
            a.submissions[studentId] = { submitted:true, date: new Date().toISOString(), points: a.submissions[studentId]?.points || 0 };
            localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
            renderAssignments();
        }
        function markUnsubmitted(assignId, studentId) {
            const a = assignmentsData.find(x => x.id === assignId);
            if (!a) return;
            a.submissions[studentId] = { submitted:false, date: '', points: 0 };
            localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
            renderAssignments();
        }
        function setSubmissionPoints(assignId, studentId, points) {
            const a = assignmentsData.find(x => x.id === assignId);
            if (!a) return;
            if (!a.submissions[studentId]) a.submissions[studentId] = { submitted:false, date:'', points:0 };
            a.submissions[studentId].points = +points;
            localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
        }

        /* END: Assignments JS */

        /* START: Analytics Dashboard JS */
        function initAnalyticsDashboard() {
            computeAndRenderKPIs();
            renderGradesDistributionChart();
            renderMonthlyPerformanceChart();
            renderAtRiskStudents();
        }

        function computeAndRenderKPIs() {
            // simple aggregate across all classes
            const classes = Object.keys(studentsData);
            let totStudents = 0, totPassed = 0, totAvg = 0, countAvg = 0;
            classes.forEach(cl => {
                (studentsData[cl] || []).forEach(s => {
                    totStudents++;
                    const g = gradesData[cl]?.[s.id] || { average: 0 };
                    if ((g.average || 0) >= 10) totPassed++;
                    totAvg += (g.average || 0);
                    countAvg++;
                });
            });
            document.getElementById('dashSuccess').textContent = totStudents ? Math.round((totPassed/totStudents)*100) + '%' : '0%';
            document.getElementById('dashAverage').textContent = countAvg ? (totAvg/countAvg).toFixed(2) : '-';
            // attendance: cannot compute exact without total classes; show placeholder
            document.getElementById('dashAttendance').textContent = '--';
        }

        function renderGradesDistributionChart() {
            const ctx = document.getElementById('gradesDistributionChart').getContext('2d');
            // collect averages
            const values = [];
            Object.keys(studentsData).forEach(cl => (studentsData[cl]||[]).forEach(s => {
                const g = gradesData[cl]?.[s.id] || { average:0 };
                values.push(g.average || 0);
            }));
            // bucket distribution 0-20 into 5 ranges
            const buckets = [0,0,0,0,0];
            values.forEach(v => {
                if (v < 4) buckets[0]++; else if (v < 8) buckets[1]++; else if (v < 12) buckets[2]++; else if (v < 16) buckets[3]++; else buckets[4]++;
            });
            if (window.gradesDistChart) window.gradesDistChart.destroy();
            window.gradesDistChart = new Chart(ctx, {
                type:'bar',
                data:{ labels: ['0-4','4-8','8-12','12-16','16-20'], datasets:[{label:'عدد التلاميذ', data: buckets}]},
                options:{ responsive:true, maintainAspectRatio:false }
            });
        }

        function renderMonthlyPerformanceChart() {
            const ctx = document.getElementById('monthlyPerformanceChart').getContext('2d');
            // placeholder monthly data: compute average of averages per month from dailyRecords if available
            const months = ['يناير','فبراير','مارس','ابريل','ماي','يونيو','يوليو','اوت','سبتمبر','اكتوبر','نوفمبر','ديسمبر'];
            const data = Array(12).fill(0);
            const counts = Array(12).fill(0);
            // we don't have dated grade entries; use random placeholder or static calculation
            for (let i=0;i<12;i++){ data[i]=Math.round(Math.random()*4)+10; } // placeholder
            if (window.monthPerfChart) window.monthPerfChart.destroy();
            window.monthPerfChart = new Chart(ctx, {
                type:'line',
                data:{ labels: months, datasets:[{label:'المعدل الشهري (تقريبي)', data}]},
                options:{ responsive:true, maintainAspectRatio:false }
            });
        }

        function renderAtRiskStudents() {
            const out = document.getElementById('atRiskList');
            out.innerHTML = '';
            // criteria: average < 8 or absences > 5
            Object.keys(studentsData).forEach(cl => (studentsData[cl]||[]).forEach(s => {
                const g = gradesData[cl]?.[s.id] || { average:0 };
                const a = attendanceData[cl]?.[s.id] || { absences:0 };
                if ((g.average || 0) < 8 || (a.absences || 0) > 5) {
                    const card = document.createElement('div');
                    card.className = 'student-alert-card';
                    card.innerHTML = `<div class="student-info"><span class="student-name">${s.name}</span>
                                      <span class="risk-level high">${ (g.average||0) < 8 ? 'خطر عالي' : 'خطر متوسط'}</span></div>
                                      <div class="risk-factors"><span class="factor">غيابات: ${a.absences||0}</span>
                                      <span class="factor">معدل: ${(g.average||0).toFixed(2)}</span></div>
                                      <button class="action-btn" onclick="interveneStudent('${cl}', ${s.id})">📞 تدخل فوري</button>`;
                    out.appendChild(card);
                }
            }));
        }

        function interveneStudent(className, studentId) {
            showNotification('تدخل مسجل (محلي) — اتخذ إجراء مع ولي الأمر', 'info');
        }

        // Alias for compatibility
        function updateAnalyticsDashboard() {
            initAnalyticsDashboard();
        }
        /* END: Analytics Dashboard JS */

        // Initialize behavior tracking when class changes (guard if element not present yet)
        const _classSelectEl = document.getElementById('classSelect');
        if (_classSelectEl) {
            _classSelectEl.addEventListener('change', function() {
                updateBehaviorStudentSelect();
                renderBehaviorCards();
            });
        }
        
        // Offline sync helpers
        function enqueuePendingSync(item) {
            const key = 'pendingSyncQueue_v1';
            const q = JSON.parse(localStorage.getItem(key) || '[]');
            q.push(item);
            localStorage.setItem(key, JSON.stringify(q));
            const pendingElement = document.getElementById('pendingSync');
            if (pendingElement) pendingElement.style.display = 'block';
        }

        async function syncPendingData() {
            const key = 'pendingSyncQueue_v1';
            const q = JSON.parse(localStorage.getItem(key) || '[]');
            if (q.length === 0) { 
                const pendingElement = document.getElementById('pendingSync');
                if (pendingElement) pendingElement.style.display = 'none';
                return; 
            }
            
            // Try to POST each item to remote endpoint
            let successCount = 0;
            for (const item of q) {
                try {
                    // Attempt sync - requires server endpoint /sync
                    const res = await fetch('/sync', { 
                        method: 'POST', 
                        headers: { 'Content-Type': 'application/json' }, 
                        body: JSON.stringify(item) 
                    });
                    if (res.ok) successCount++;
                } catch (e) {
                    console.log('Sync attempt failed:', e);
                    // Fail silently, will retry later
                }
            }
            
            if (successCount === q.length) {
                localStorage.setItem(key, JSON.stringify([]));
                const pendingElement = document.getElementById('pendingSync');
                if (pendingElement) pendingElement.style.display = 'none';
                showNotification('تمت المزامنة بنجاح', 'success');
            } else {
                showNotification('يوجد بيانات لم تُزامن — سيتم المحاولة لاحقاً', 'info');
                const pendingElement = document.getElementById('pendingSync');
                if (pendingElement) pendingElement.style.display = 'block';
            }
        }

        // Navigation functions
        function showSection(sectionId) {
            console.log(`=== SHOWING SECTION: ${sectionId} ===`);
            
            // Hide welcome screen
            const welcome = document.getElementById('welcomeScreen');
            if (welcome) {
                welcome.style.display = 'none';
                console.log('✅ Hidden welcome screen');
            } else {
                console.log('❌ Welcome screen not found');
            }
            
            // Hide all sections
            const allSections = document.querySelectorAll('.section');
            console.log(`Found ${allSections.length} sections to hide`);
            allSections.forEach(s => {
                s.style.display = 'none';
                console.log(`Hidden section: ${s.id}`);
            });
            
            // Debug: List all sections found
            console.log('All sections found:', Array.from(allSections).map(s => s.id));
            
            // Hide any open modals
            hideModals();
            
            // Show the requested section
            const section = document.getElementById(sectionId);
            console.log(`Looking for section with ID: ${sectionId}`);
            console.log(`Section found:`, section);
            if (section) {
                section.style.setProperty('display', 'block', 'important');
                console.log(`✅ Showing section: ${sectionId}`);
                
                // Special handling for specific sections
                if (sectionId === 'students') {
                    // Refresh all lists when students section is shown
                    setTimeout(() => {
                        if (typeof updateAllLists === 'function') {
                            updateAllLists();
                        }
                    }, 100);
                } else if (sectionId === 'assignments') {
                    // Show students section and activate assignments tab
                    const studentsSection = document.getElementById('students');
                    if (studentsSection) {
                        studentsSection.style.setProperty('display', 'block', 'important');
                        
                        // Switch to assignments tab
                        setTimeout(() => {
                            // Remove active class from all tabs
                            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));
                            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
                            
                            // Activate assignments tab
                            const assignmentsTab = document.querySelector('button[onclick*="assignments"]');
                            const assignmentsContent = document.getElementById('assignments');
                            
                            if (assignmentsTab) assignmentsTab.classList.add('active');
                            if (assignmentsContent) assignmentsContent.classList.add('active');
                            
                            // Update assignments
                            updateAssignmentClassSelects();
                            renderAssignments();
                        }, 100);
                    }
                } else if (sectionId === 'dailyRecord') {
                    // Initialize daily record when shown
                    setTimeout(() => {
                        if (typeof loadDailyRecord === 'function') {
                            console.log('Loading daily record...');
                            loadDailyRecord();
                        } else {
                            console.log('❌ loadDailyRecord function not found');
                        }
                    }, 100);
                } else if (sectionId === 'lessons') {
                    // Initialize lessons when shown
                    setTimeout(() => {
                        if (typeof initLessonPlanner === 'function') {
                            console.log('Initializing lessons...');
                            initLessonPlanner();
                        } else {
                            console.log('❌ initLessonPlanner function not found');
                        }
                    }, 100);
                } else if (sectionId === 'presentations') {
                    // Initialize presentations when shown
                    setTimeout(() => {
                        if (typeof initLessonPlanner === 'function') {
                            console.log('Initializing presentations...');
                            initLessonPlanner();
                        } else {
                            console.log('❌ initLessonPlanner function not found');
                        }
                    }, 100);
                } else if (sectionId === 'calendar') {
                    // Initialize calendar when shown
                    setTimeout(() => {
                        if (typeof initCalendar === 'function') {
                            console.log('Initializing calendar...');
                            initCalendar();
                        } else {
                            console.log('❌ initCalendar function not found');
                        }
                    }, 100);
                } else if (sectionId === 'lessonPlanner') {
                    // Initialize lesson planner when shown
                    setTimeout(() => {
                        if (typeof initLessonPlanner === 'function') {
                            console.log('Initializing lesson planner...');
                            initLessonPlanner();
                        } else {
                            console.log('❌ initLessonPlanner function not found');
                        }
                    }, 100);
                } else if (sectionId === 'parents') {
                    // Initialize parents section when shown
                    setTimeout(() => {
                        if (typeof updateParentWorkStudents === 'function') {
                            console.log('Initializing parents section...');
                            updateParentWorkStudents();
                        } else {
                            console.log('❌ updateParentWorkStudents function not found');
                        }
                    }, 100);
                } else if (sectionId === 'quizBuilder') {
                    // Initialize quiz builder when shown
                    setTimeout(() => {
                        if (typeof initQuizBuilder === 'function') {
                            console.log('Initializing quiz builder...');
                            initQuizBuilder();
                        } else {
                            console.log('❌ initQuizBuilder function not found');
                        }
                    }, 100);
                }
            } else {
                console.log(`❌ Section not found: ${sectionId}`);
            }
            
            console.log(`=== SECTION SHOW COMPLETED ===`);
        }

        function goBack() {
            // Hide all sections
            document.querySelectorAll('.section').forEach(function(s) {
                s.style.setProperty('display', 'none', 'important');
            });
            
            // Show the welcome screen
            const welcome = document.getElementById('welcomeScreen');
            if (welcome) {
                welcome.style.setProperty('display', 'block', 'important');
            }
        }

        // Notification system
        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            notification.textContent = message;
            notification.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                padding: 12px 20px;
                border-radius: 4px;
                color: white;
                font-weight: bold;
                z-index: 10000;
                max-width: 300px;
                word-wrap: break-word;
            `;
            
            // Set background color based on type
            switch(type) {
                case 'success': notification.style.backgroundColor = '#4CAF50'; break;
                case 'error': notification.style.backgroundColor = '#f44336'; break;
                case 'warning': notification.style.backgroundColor = '#ff9800'; break;
                default: notification.style.backgroundColor = '#2196F3';
            }
            
            document.body.appendChild(notification);
            
            // Auto remove after 3 seconds
            setTimeout(() => {
                notification.style.opacity = '0';
                notification.style.transition = 'opacity 0.3s';
                setTimeout(() => notification.remove(), 300);
            }, 3000);
        }

        // Modal system
        function openModal(title, content, size = 'medium') {
            const modal = document.createElement('div');
            modal.className = 'modal-overlay';
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0,0,0,0.5);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 9999;
            `;
            
            const modalContent = document.createElement('div');
            modalContent.className = 'modal-content';
            modalContent.style.cssText = `
                background: white;
                padding: 20px;
                border-radius: 8px;
                max-height: 80vh;
                overflow-y: auto;
                position: relative;
                ${size === 'large' ? 'width: 80%; max-width: 800px;' : 'width: 60%; max-width: 500px;'}
            `;
            
            modalContent.innerHTML = `
                <button onclick="this.closest('.modal-overlay').remove()" style="
                    position: absolute;
                    top: 10px;
                    right: 15px;
                    background: none;
                    border: none;
                    font-size: 20px;
                    cursor: pointer;
                    color: #999;
                ">&times;</button>
                <h3>${title}</h3>
                <div>${content}</div>
            `;
            
            modal.appendChild(modalContent);
            document.body.appendChild(modal);
            
            // Close on overlay click
            modal.addEventListener('click', (e) => {
                if (e.target === modal) modal.remove();
            });
        }

        // Data persistence functions
        function saveData() {
            // Save all application data to localStorage
            localStorage.setItem('studentsData', JSON.stringify(studentsData));
            localStorage.setItem('gradesData', JSON.stringify(gradesData));
            localStorage.setItem('attendanceData', JSON.stringify(attendanceData));
            localStorage.setItem('rewardsData', JSON.stringify(rewardsData));
            localStorage.setItem('calendarEvents_v1', JSON.stringify(calendarEvents));
            localStorage.setItem('lessonPlans_v1', JSON.stringify(lessonPlans));
            localStorage.setItem('parentMessages_v1', JSON.stringify(parentMessages));
            localStorage.setItem('assignments_v1', JSON.stringify(assignmentsData));
            localStorage.setItem('behaviorData_v1', JSON.stringify(behaviorData));
            localStorage.setItem('quizzes_v1', JSON.stringify(quizzes));
        }

        function loadSavedData() {
            // Load all application data from localStorage
            studentsData = JSON.parse(localStorage.getItem('studentsData') || '{}');
            gradesData = JSON.parse(localStorage.getItem('gradesData') || '{}');
            attendanceData = JSON.parse(localStorage.getItem('attendanceData') || '{}');
            rewardsData = JSON.parse(localStorage.getItem('rewardsData') || '{}');
            calendarEvents = JSON.parse(localStorage.getItem('calendarEvents_v1') || '{}');
            lessonPlans = JSON.parse(localStorage.getItem('lessonPlans_v1') || '[]');
            parentMessages = JSON.parse(localStorage.getItem('parentMessages_v1') || '[]');
            assignmentsData = JSON.parse(localStorage.getItem('assignments_v1') || '[]');
            behaviorData = JSON.parse(localStorage.getItem('behaviorData_v1') || '{}');
            quizzes = JSON.parse(localStorage.getItem('quizzes_v1') || '[]');
        }

        // (removed) Duplicate DOMContentLoaded initializer to avoid double init
        
        // Auto-sync when online
        document.addEventListener('online', syncPendingData);
        
        // Auto-save functionality
        setInterval(saveData, 30000); // Auto-save every 30 seconds

        // Note: All required functions are defined below in their proper sections

        // --- File Handling (Lessons & Presentations) ---
        function handleLessonUpload(input, yearLevel) {
            const file = input.files[0];
            if (file) {
                const lessonTitle = prompt('أدخل عنوان الدرس:');
                if (lessonTitle) {
                    if (!lessonsData[yearLevel]) lessonsData[yearLevel] = [];
                    const lesson = { id: Date.now(), title: lessonTitle, fileName: file.name, file: file };
                    lessonsData[yearLevel].push(lesson);
                    displayLessons(yearLevel);
                }
            }
        }

        function displayLessons(yearLevel) {
            const container = document.getElementById(yearLevel + 'Lessons');
            if (!lessonsData[yearLevel]) return;
            container.innerHTML = lessonsData[yearLevel].map(lesson => `
                <div class="lesson-item">
                    <h4>${lesson.title}</h4>
                    <p>📄 ${lesson.fileName}</p>
                    <button class="add-button" onclick="openFile(${lesson.id}, '${yearLevel}', 'lessons')">فتح</button>
                    <button class="remove-button" onclick="removeFile(${lesson.id}, '${yearLevel}', 'lessons')">حذف</button>
                </div>
            `).join('');
        }

        function handlePresentationUpload(input, yearLevel) {
            const file = input.files[0];
            if (file) {
                const title = prompt('أدخل عنوان العرض:');
                if (title) {
                    if (!presentationsData[yearLevel]) presentationsData[yearLevel] = [];
                    const pres = { id: Date.now(), title: title, fileName: file.name, file: file };
                    presentationsData[yearLevel].push(pres);
                    displayPresentations(yearLevel);
                }
            }
        }

        function displayPresentations(yearLevel) {
            const container = document.getElementById(yearLevel + 'Container');
            if (!presentationsData[yearLevel]) return;
            container.innerHTML = presentationsData[yearLevel].map(p => `
                <div class="lesson-item">
                    <h4>${p.title}</h4>
                    <p>🎬 ${p.fileName}</p>
                    <button class="add-button" onclick="openFile(${p.id}, '${yearLevel}', 'presentations')">فتح</button>
                    <button class="remove-button" onclick="removeFile(${p.id}, '${yearLevel}', 'presentations')">حذف</button>
                </div>
            `).join('');
        }

        function openFile(id, yearLevel, type) {
            const data = (type === 'lessons' ? lessonsData : presentationsData)[yearLevel];
            const item = data.find(i => i.id === id);
            if (item && item.file) {
                window.open(URL.createObjectURL(item.file), '_blank');
            }
        }

        function removeFile(id, yearLevel, type) {
            if (confirm('هل أنت متأكد من الحذف؟')) {
                if (type === 'lessons') {
                    lessonsData[yearLevel] = lessonsData[yearLevel].filter(i => i.id !== id);
                    displayLessons(yearLevel);
                } else {
                    presentationsData[yearLevel] = presentationsData[yearLevel].filter(i => i.id !== id);
                    displayPresentations(yearLevel);
                }
                saveData();
            }
        }

        function changeFontSize() {
            const size = document.getElementById('fontSizeSelect').value;
            document.body.style.fontSize = size === 'small' ? '14px' : size === 'large' ? '18px' : '16px';
        }

        function changeTheme() {
            const theme = document.getElementById('themeSelect').value;
            document.body.className = theme;
            localStorage.setItem('selectedTheme', theme);
            showNotification(`تم تغيير المظهر إلى ${theme === 'light' ? 'الوضع الفاتح' : theme === 'dark' ? 'الوضع الداكن' : 'الوضع الأزرق'}`, 'success');
        }

        function exportData() {
            saveData(); // Ensure current state is saved
            const allData = {};
            for (let i = 0; i < localStorage.length; i++) {
                const key = localStorage.key(i);
                try {
                    allData[key] = JSON.parse(localStorage.getItem(key));
                } catch (e) {
                    allData[key] = localStorage.getItem(key);
                }
            }
            const dataStr = JSON.stringify(allData, null, 2);
            const dataBlob = new Blob([dataStr], {type: 'application/json'});
            const url = URL.createObjectURL(dataBlob);
            const link = document.createElement('a');
            link.href = url;
            link.download = 'teacher_data_backup.json';
            link.click();
            showNotification('تم تصدير البيانات بنجاح!', 'success');
        }

        function importData() {
            const input = document.createElement('input');
            input.type = 'file';
            input.accept = '.json';
            input.onchange = e => {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = e => {
                        try {
                            const data = JSON.parse(e.target.result);
                            for(const key in data) {
                                localStorage.setItem(key, JSON.stringify(data[key]));
                            }
                            showNotification('تم استيراد البيانات بنجاح! سيتم إعادة تحميل التطبيق.', 'success');
                            location.reload();
                        } catch (error) {
                            showNotification('خطأ في قراءة الملف!', 'error');
                        }
                    };
                    reader.readAsText(file);
                }
            };
            input.click();
        }

        function clearAllData() {
            if (confirm('هل أنت متأكد من حذف جميع البيانات؟ هذا الإجراء غير قابل للتراجع!')) {
                localStorage.clear();
                showNotification('تم حذف جميع البيانات. سيتم إعادة تحميل التطبيق.', 'success');
                setTimeout(() => window.location.reload(), 2000);
            }
        }

        function toggleNotifications() {
            const enabled = document.getElementById('enableNotifications').checked;
            localStorage.setItem('notificationsEnabled', enabled);
            showNotification(`التنبيهات ${enabled ? 'مفعلة' : 'معطلة'}`, 'info');
        }

        function toggleAutoSave() {
            const enabled = document.getElementById('autoSave').checked;
            localStorage.setItem('autoSaveEnabled', enabled);
            showNotification(`الحفظ التلقائي ${enabled ? 'مفعل' : 'معطل'}`, 'info');
        }

        // --- Language Translation ---
        const translations = {};
        async function setLanguage(lang) {
            // For now, just set the language without translations
            localStorage.setItem('preferredLanguage', lang);
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            if (document.getElementById('languageSelect')) {
                document.getElementById('languageSelect').value = lang;
            }
            showNotification(`تم تغيير اللغة إلى ${lang === 'ar' ? 'العربية' : lang === 'fr' ? 'Français' : 'English'}`, 'success');
        }

        function loadLanguagePreference() {
            const preferredLanguage = localStorage.getItem('preferredLanguage') || 'ar';
            setLanguage(preferredLanguage);
        }

        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
        }

        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            notification.textContent = message;
            notification.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                padding: 12px 20px;
                border-radius: 4px;
                color: white;
                font-weight: bold;
                z-index: 10000;
                max-width: 300px;
                word-wrap: break-word;
                background-color: ${type === 'success' ? '#4CAF50' : type === 'error' ? '#f44336' : type === 'warning' ? '#ff9800' : '#2196F3'};
            `;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.style.opacity = '0';
                notification.style.transition = 'opacity 0.3s';
                setTimeout(() => notification.remove(), 300);
            }, 3000);
        }

        // Initialize application (single canonical initializer)
        document.addEventListener('DOMContentLoaded', function() {
            // Load and prepare data
            loadSavedData();
            initializeDefaultData();
            updateAllLists();
            loadDailyRecord();
            
            // Initialize modules if their root elements and init functions exist
            if (document.getElementById('calendarGrid') && typeof initCalendar === 'function') {
                initCalendar();
            }
            if (document.getElementById('lessonPlanner') && typeof initLessonPlanner === 'function') {
                initLessonPlanner();
            }
            if (document.getElementById('quizBuilder') && typeof initQuizBuilder === 'function') {
                initQuizBuilder();
            }
            if (document.getElementById('assignments')) {
                updateAssignmentClassSelects();
                renderAssignments();
            }
            
            // Start at welcome: hide all sections then show welcome screen
            document.querySelectorAll('.section').forEach(s => s.style.display = 'none');
            const welcome = document.getElementById('welcomeScreen');
            if (welcome) welcome.style.display = 'block';
        });

        function updateAllLists() {
            if (typeof updateClassSelects === 'function') updateClassSelects();
            if (typeof updateStudentsList === 'function') updateStudentsList();
            if (typeof updateGradesTable === 'function') updateGradesTable();
            if (typeof updateAttendanceList === 'function') updateAttendanceList();
            if (typeof updateRewardsList === 'function') updateRewardsList();
            if (typeof updateBehaviorStudentSelect === 'function') updateBehaviorStudentSelect();
            if (typeof updateBehaviorList === 'function') updateBehaviorList();
            if (typeof updateBehaviorPoints === 'function') updateBehaviorPoints();
            if (typeof updateAnalytics === 'function') updateAnalytics();
        }

        function initializeDefaultData() {
            const classes = ['1AM1', '1AM2', '1AM3', '1AM4', '2AM1', '2AM2', '2AM3', '3AM1', '3AM2', '3AM3', '4AM1', '4AM2'];
            classes.forEach(className => {
                if (!studentsData[className]) studentsData[className] = [];
                if (!gradesData[className]) gradesData[className] = {};
                if (!attendanceData[className]) attendanceData[className] = {};
                if (!rewardsData[className]) rewardsData[className] = {};
            });
        }

        // Function to hide calendar modal when switching sections
        function hideCalendarModal() {
            const modal = document.getElementById('calendarModal');
            if (modal) {
                modal.classList.remove('show');
            }
        }

        // Enhanced goBack function that also hides modals
        function goBack() {
            // Hide all sections
            document.querySelectorAll('.section').forEach(function(s) {
                s.style.display = 'none';
            });
            
            // Hide any open modals
            hideCalendarModal();
            
            // Show the welcome screen
            const welcome = document.getElementById('welcomeScreen');
            if (welcome) {
                welcome.style.display = 'block';
            }
        }

        // Hide any open modals
        function hideModals() {
            hideCalendarModal();
        }

        // Students Management Functions
        
        // --- Excel Import ---
        function handleExcelImport(input) {
            console.log('=== EXCEL IMPORT STARTED ===');
            const file = input.files[0];
            if (!file) {
                console.log('No file selected');
                return;
            }
            console.log('File selected:', file.name, 'Size:', file.size);
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    console.log('File read successfully, processing...');
                    const data = new Uint8Array(e.target.result);
                    console.log('Data length:', data.length);
                    
                    if (typeof XLSX === 'undefined') {
                        showNotification('خطأ: مكتبة Excel غير محملة', 'error');
                        console.error('XLSX library not loaded');
                        return;
                    }
                    
                    const workbook = XLSX.read(data, {type: 'array'});
                    console.log('Workbook sheets:', workbook.SheetNames);
                    
                    const firstSheetName = workbook.SheetNames[0];
                    const worksheet = workbook.Sheets[firstSheetName];
                    const jsonData = XLSX.utils.sheet_to_json(worksheet);
                    console.log('Parsed data:', jsonData);
                    
                    const className = prompt('أدخل اسم القسم (مثل: 1AM1):');
                    if (className) {
                        console.log('Class name entered:', className);
                        processImportedStudents(jsonData, className);
                    } else {
                        console.log('No class name entered');
                    }
                } catch (error) {
                    console.error('Excel processing error:', error);
                    showNotification('خطأ في قراءة ملف Excel: ' + error.message, 'error');
                }
            };
            
            reader.onerror = function(error) {
                console.error('File reading error:', error);
                showNotification('خطأ في قراءة الملف', 'error');
            };
            
            reader.readAsArrayBuffer(file);
            console.log('=== EXCEL IMPORT FUNCTION COMPLETED ===');
        }

        function processImportedStudents(data, className) {
            console.log('=== PROCESSING IMPORTED STUDENTS ===');
            console.log('Data received:', data);
            console.log('Class name:', className);
            
            if (!studentsData[className]) {
                studentsData[className] = [];
                console.log('Created new class array for:', className);
            }
            
            let importedCount = 0;
            data.forEach((row, index) => {
                console.log(`Processing row ${index}:`, row);
                
                const firstName = row['الاسم'] || row['Name'] || '';
                const lastName = row['اللقب'] || row['LastName'] || '';
                const birthDate = row['تاريخ الميلاد'] || row['BirthDate'] || '';
                
                console.log('Extracted data:', { firstName, lastName, birthDate });
                
                if (firstName.trim() || lastName.trim()) {
                    const student = { 
                        id: Date.now() + importedCount, 
                        name: `${firstName} ${lastName}`.trim(), 
                        birthDate 
                    };
                    
                    console.log('Created student object:', student);
                    studentsData[className].push(student);
                    
                    // Initialize grades data
                    if (!gradesData[className]) gradesData[className] = {};
                    gradesData[className][student.id] = { evaluation: 0, homework: 0, exam: 0, average: 0, note: '' };
                    
                    // Initialize attendance data
                    if (!attendanceData[className]) attendanceData[className] = {};
                    attendanceData[className][student.id] = { absences: 0 };
                    
                    // Initialize rewards data
                    if (!rewardsData[className]) rewardsData[className] = {};
                    rewardsData[className][student.id] = { points: 0 };
                    
                    importedCount++;
                    console.log(`Student ${importedCount} added successfully`);
                } else {
                    console.log(`Row ${index} skipped - no valid name data`);
                }
            });
            
            console.log(`Total students imported: ${importedCount}`);
            console.log('Final studentsData:', studentsData);
            
            showNotification(`تم استيراد ${importedCount} تلميذ بنجاح للقسم ${className}`, 'success');
            updateAllLists();
            saveData();
            console.log('=== PROCESSING COMPLETED ===');
        }

        // --- Students Management ---
        function initializeDefaultData() {
            const classes = ['1AM1', '1AM2', '1AM3', '1AM4', '2AM1', '2AM2', '2AM3', '3AM1', '3AM2', '3AM3', '4AM1', '4AM2'];
            classes.forEach(className => {
                if (!studentsData[className]) studentsData[className] = [];
                if (!gradesData[className]) gradesData[className] = {};
                if (!attendanceData[className]) attendanceData[className] = {};
                if (!rewardsData[className]) rewardsData[className] = {};
            });
        }

        function updateClassSelects() {
            const selects = ['classSelect', 'gradesClassSelect', 'attendanceClassSelect', 'rewardsClassSelect'];
            const classes = Object.keys(studentsData).sort();
            selects.forEach(selectId => {
                const select = document.getElementById(selectId);
                if (select) {
                    const currentValue = select.value;
                    if (classes.length > 0) {
                        select.innerHTML = '';
                        classes.forEach(className => {
                            const option = document.createElement('option');
                            option.value = className;
                            option.textContent = className;
                            select.appendChild(option);
                        });
                        select.value = classes.includes(currentValue) ? currentValue : classes[0];
                    } else {
                        select.innerHTML = '<option>لا توجد أقسام</option>';
                    }
                }
            });
        }

        function addStudent() {
            document.getElementById('newStudentFirstName').value = '';
            document.getElementById('newStudentLastName').value = '';
            document.getElementById('newStudentBirthDate').value = '';
            document.getElementById('addStudentModal').style.display = 'flex';
        }

        function saveNewStudent() {
            const className = document.getElementById('classSelect').value;
            const firstName = document.getElementById('newStudentFirstName').value.trim();
            const lastName = document.getElementById('newStudentLastName').value.trim();
            const birthDate = document.getElementById('newStudentBirthDate').value;

            if (!firstName || !lastName || !birthDate) {
                showNotification('يرجى ملء جميع الحقول', 'error');
                return;
            }

            if (!studentsData[className]) studentsData[className] = [];
            if (!gradesData[className]) gradesData[className] = {};
            if (!attendanceData[className]) attendanceData[className] = {};
            if (!rewardsData[className]) rewardsData[className] = {};

            const student = { 
                id: Date.now(), 
                name: `${firstName} ${lastName}`,
                firstName, 
                lastName, 
                birthDate 
            };

            studentsData[className].push(student);
            gradesData[className][student.id] = { evaluation: 0, homework: 0, exam: 0, average: 0, note: '' };
            attendanceData[className][student.id] = { absences: 0 };
            rewardsData[className][student.id] = { points: 0 };
            
            updateAllLists();
            saveData();
            closeModal('addStudentModal');
            showNotification('تمت إضافة التلميذ بنجاح', 'success');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
        }

        function removeStudent(studentId) {
            const className = document.getElementById('classSelect').value;
            if (confirm('هل أنت متأكد من حذف هذا التلميذ؟')) {
                studentsData[className] = studentsData[className].filter(s => s.id !== studentId);
                delete gradesData[className][studentId];
                delete attendanceData[className][studentId];
                delete rewardsData[className][studentId];
                updateAllLists();
                saveData();
                showNotification('تم حذف التلميذ بنجاح', 'success');
            }
        }

        function updateStudentsList() {
            const className = document.getElementById('classSelect').value;
            const container = document.getElementById('studentsListContainer');
            if (!className || !studentsData[className] || studentsData[className].length === 0) {
                container.innerHTML = '<p style="text-align: center; padding: 20px; color: #666;">لا يوجد تلاميذ في هذا القسم</p>';
                return;
            }
            container.innerHTML = studentsData[className].map(student => `
                <div class="student-item">
                    <span>${student.name}${student.birthDate ? ` - ${student.birthDate}` : ''}</span>
                    <button class="remove-button" onclick="removeStudent(${student.id})">حذف</button>
                </div>
            `).join('');
        }

        // --- Grades Management ---
        function updateGradesTable() {
            const className = document.getElementById('gradesClassSelect').value;
            const tbody = document.getElementById('gradesTableBody');
            if (!className || !studentsData[className] || studentsData[className].length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center; padding: 20px; color: #666;">لا يوجد تلاميذ في هذا القسم</td></tr>';
                return;
            }
            tbody.innerHTML = studentsData[className].map(student => {
                const grades = gradesData[className]?.[student.id] || { evaluation: 0, homework: 0, exam: 0, average: 0, note: '' };
                return `
                    <tr>
                        <td>${student.name}</td>
                        <td><input type="number" min="0" max="20" value="${grades.evaluation}" onchange="updateGrade(${student.id}, 'evaluation', this.value)"></td>
                        <td><input type="number" min="0" max="20" value="${grades.homework}" onchange="updateGrade(${student.id}, 'homework', this.value)"></td>
                        <td><input type="number" min="0" max="20" value="${grades.exam}" onchange="updateGrade(${student.id}, 'exam', this.value)"></td>
                        <td><strong>${grades.average.toFixed(2)}</strong></td>
                        <td><input type="text" value="${grades.note}" onchange="updateGrade(${student.id}, 'note', this.value)"></td>
                    </tr>
                `;
            }).join('');
        }

        function updateGrade(studentId, gradeType, value) {
            const className = document.getElementById('gradesClassSelect').value;
            const grades = gradesData[className][studentId];
            if (gradeType === 'note') {
                grades.note = value;
            } else {
                grades[gradeType] = parseFloat(value) || 0;
                grades.average = (((grades.evaluation + grades.homework) / 2) + (grades.exam * 2)) / 3;
            }
            updateGradesTable();
        }

        function saveGrades() {
            saveData();
            showNotification('تم حفظ المعدلات بنجاح', 'success');
        }

        function exportGradesToExcel() {
            const className = document.getElementById('gradesClassSelect').value;
            if (!studentsData[className] || studentsData[className].length === 0) {
                showNotification('لا توجد بيانات لتصديرها.', 'info');
                return;
            }
            const data = studentsData[className].map(student => {
                const g = gradesData[className][student.id] || {};
                return {
                    'التلميذ': student.name,
                    'التقويم': g.evaluation || 0,
                    'الفرض': g.homework || 0,
                    'الاختبار': g.exam || 0,
                    'المعدل': (g.average || 0).toFixed(2),
                    'الملاحظة': g.note || ''
                };
            });
            const ws = XLSX.utils.json_to_sheet(data);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, 'المعدلات');
            XLSX.writeFile(wb, `معدلات قسم ${className}.xlsx`);
        }

        // --- Attendance & Rewards ---
        function updateAttendanceList() {
            const className = document.getElementById('attendanceClassSelect').value;
            const container = document.getElementById('attendanceList');
            if (!className || !studentsData[className] || studentsData[className].length === 0) {
                container.innerHTML = '<p style="text-align: center; padding: 20px; color: #666;">لا يوجد تلاميذ في هذا القسم</p>';
                return;
            }
            container.innerHTML = studentsData[className].map(student => {
                const attendance = attendanceData[className]?.[student.id] || { absences: 0 };
                return `
                    <div class="student-item">
                        <span>${student.name} - الغيابات: ${attendance.absences}</span>
                        <div>
                            <button class="add-button" onclick="addAbsence(${student.id})">+ غياب</button>
                            <button class="remove-button" onclick="removeAbsence(${student.id})">- غياب</button>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function addAbsence(studentId) {
            const className = document.getElementById('attendanceClassSelect').value;
            attendanceData[className][studentId].absences++;
            updateAttendanceList();
        }

        function removeAbsence(studentId) {
            const className = document.getElementById('attendanceClassSelect').value;
            if (attendanceData[className][studentId].absences > 0) {
                attendanceData[className][studentId].absences--;
                updateAttendanceList();
            }
        }

        function updateRewardsList() {
            const className = document.getElementById('rewardsClassSelect').value;
            const container = document.getElementById('rewardsList');
            if (!className || !studentsData[className] || studentsData[className].length === 0) {
                container.innerHTML = '<p style="text-align: center; padding: 20px; color: #666;">لا يوجد تلاميذ في هذا القسم</p>';
                return;
            }
            container.innerHTML = studentsData[className].map(student => {
                const rewards = rewardsData[className]?.[student.id] || { points: 0 };
                return `
                    <div class="student-item">
                        <div class="student-info">
                            <span class="student-name">${student.name}</span>
                            <span class="student-points">⭐ النقاط: <strong id="displayPoints_${student.id}">${rewards.points}</strong></span>
                        </div>
                        <div class="rewards-controls">
                            <input type="number" placeholder="النقاط" min="1" max="10" style="width: 80px;" id="points_${student.id}" value="${rewards.points}">
                            <button class="add-button" onclick="addRewardPoint(${student.id})">+ نقطة</button>
                            <button class="remove-button" onclick="removeRewardPoint(${student.id})">- نقطة</button>
                            <button class="add-button" onclick="addCustomPoints(${student.id})" style="background: #17a2b8;">إضافة نقاط مخصصة</button>
                            <button class="add-button" onclick="setExactPoints(${student.id})" style="background: #28a745;">تعيين النقاط</button>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function addRewardPoint(studentId) {
            const className = document.getElementById('rewardsClassSelect').value;
            if (!rewardsData[className]) {
                rewardsData[className] = {};
            }
            if (!rewardsData[className][studentId]) {
                rewardsData[className][studentId] = { points: 0 };
            }
            
            rewardsData[className][studentId].points++;
            localStorage.setItem('rewardsData', JSON.stringify(rewardsData));
            updateRewardsList();
        }

        function removeRewardPoint(studentId) {
            const className = document.getElementById('rewardsClassSelect').value;
            if (!rewardsData[className] || !rewardsData[className][studentId]) return;
            
            if (rewardsData[className][studentId].points > 0) {
                rewardsData[className][studentId].points--;
                localStorage.setItem('rewardsData', JSON.stringify(rewardsData));
                updateRewardsList();
            }
        }
        
        function addCustomPoints(studentId) {
            const className = document.getElementById('rewardsClassSelect').value;
            const pointsInput = document.getElementById(`points_${studentId}`);
            const points = parseInt(pointsInput.value) || 0;
            
            if (points <= 0) {
                alert('يرجى إدخال عدد نقاط صحيح');
                return;
            }
            
            if (!rewardsData[className]) {
                rewardsData[className] = {};
            }
            
            if (!rewardsData[className][studentId]) {
                rewardsData[className][studentId] = { points: 0 };
            }
            
            rewardsData[className][studentId].points += points;
            localStorage.setItem('rewardsData', JSON.stringify(rewardsData));
            
            // Clear input
            pointsInput.value = '';
            
            // Update display
            updateRewardsList();
            
            alert(`تم إضافة ${points} نقاط للتلميذ بنجاح!`);
        }
        
        function setExactPoints(studentId) {
            const className = document.getElementById('rewardsClassSelect').value;
            const pointsInput = document.getElementById(`points_${studentId}`);
            const points = parseInt(pointsInput.value) || 0;
            
            if (points < 0) {
                alert('يرجى إدخال عدد نقاط صحيح');
                return;
            }
            
            if (!rewardsData[className]) {
                rewardsData[className] = {};
            }
            
            if (!rewardsData[className][studentId]) {
                rewardsData[className][studentId] = { points: 0 };
            }
            
            // Set exact points (not add)
            rewardsData[className][studentId].points = points;
            localStorage.setItem('rewardsData', JSON.stringify(rewardsData));
            
            // Update display
            updateRewardsList();
            
            alert(`تم تعيين النقاط إلى ${points} للتلميذ بنجاح!`);
        }

        // --- Daily Record ---
        function gatherDailyRows() {
            const rows = document.querySelectorAll('#dailyRecordTableBody tr');
            return Array.from(rows).map(row => {
                if (!row || row.cells.length < 9) return null;
                const getVal = (idx) => {
                    const cell = row.cells[idx];
                    if (!cell) return '';
                    const el = cell.querySelector('input, textarea');
                    return el && typeof el.value !== 'undefined' ? el.value : '';
                };
                return {
                    date: getVal(0),
                    time: getVal(1),
                    class: getVal(2),
                    domain: getVal(3),
                    section: getVal(4),
                    resource: getVal(5),
                    activity: getVal(6),
                    flow: getVal(7),
                    notes: getVal(8),
                };
            }).filter(Boolean);
        }

        function exportDailyToExcel() {
            const headerCells = document.querySelectorAll('#dailyRecordTable thead th');
            const headers = Array.from(headerCells).map(th => th.innerText.trim());

            const data = gatherDailyRows().map((r, idx) => {
                let rowData = {'#': idx + 1};
                headers.forEach((header, index) => {
                    const fieldKey = ['date', 'time', 'class', 'domain', 'section', 'resource', 'activity', 'flow', 'notes'][index];
                    rowData[header] = r[fieldKey];
                });
                return rowData;
            });
            const ws = XLSX.utils.json_to_sheet(data);
            ws['!cols'] = [{wch:4},{wch:12},{wch:12},{wch:10},{wch:12},{wch:10},{wch:12},{wch:10},{wch:40},{wch:25}];
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, 'الدفتر اليومي');
            XLSX.writeFile(wb, 'daily_record.xlsx');
        }

        function addDailyRow(data = {}) {
            const tbody = document.getElementById('dailyRecordTableBody');
            const row = tbody.insertRow();
            const fields = ['date', 'time', 'class', 'domain', 'section', 'resource', 'activity', 'flow', 'notes'];
            fields.forEach(field => {
                const cell = row.insertCell();
                const el = ['flow', 'notes'].includes(field) ? document.createElement('textarea') : document.createElement('input');
                el.value = data[field] || '';
                if (field === 'date') {
                    el.type = 'date';
                    if (!el.value) {
                        const tomorrow = new Date();
                        tomorrow.setDate(tomorrow.getDate() + 1);
                        el.value = tomorrow.toISOString().split('T')[0];
                    }
                } else if (field !== 'flow' && field !== 'notes') {
                    el.type = 'text';
                    if (field === 'class') el.setAttribute('list', 'classSuggestions');
                    if (field === 'time') el.setAttribute('list', 'timeSuggestions');
                }
                cell.appendChild(el);
            });
        }

        function loadDailyRecord() {
            const data = JSON.parse(localStorage.getItem('dailyRecordData')) || [];
            const tbody = document.getElementById('dailyRecordTableBody');
            tbody.innerHTML = ''; // Clear existing rows
            if (data.length === 0) {
                addDailyRow();
            } else {
                data.forEach(addDailyRow);
            }
            tbody.addEventListener('input', saveData); // Auto-save on any input change
        }

        // --- Data Persistence ---
        function saveData() {
            const teacherInfo = {
                firstName: document.getElementById('firstName')?.value || '',
                lastName: document.getElementById('lastName')?.value || '',
                address: document.getElementById('address')?.value || '',
                birthDate: document.getElementById('birthDate')?.value || '',
                phone: document.getElementById('phone')?.value || '',
                email: document.getElementById('email')?.value || '',
                framework: document.getElementById('framework')?.value || '',
                subject: document.getElementById('subject')?.value || '',
                certificate: document.getElementById('certificate')?.value || '',
                firstAppointment: document.getElementById('firstAppointment')?.value || '',
                position: document.getElementById('position')?.value || '',
                confirmationDate: document.getElementById('confirmationDate')?.value || '',
                grade: document.getElementById('grade')?.value || '',
                currentInstitution: document.getElementById('currentInstitution')?.value || '',
                academicYear: document.getElementById('academicYear')?.value || '',
            };
            localStorage.setItem('teacherInfo', JSON.stringify(teacherInfo));

            const scheduleInfo = {
                teacher: document.getElementById('scheduleTeacher')?.value || '',
                year: document.getElementById('scheduleYear')?.value || '',
                classes: document.getElementById('assignedClasses')?.value || '',
                hours: document.getElementById('workHours')?.value || '',
                table: Array.from(document.querySelectorAll('.schedule-table tbody tr')).map(tr => 
                    Array.from(tr.querySelectorAll('input')).map(input => input.value)
                )
            };
            localStorage.setItem('scheduleInfo', JSON.stringify(scheduleInfo));

            localStorage.setItem('studentsData', JSON.stringify(studentsData));
            localStorage.setItem('gradesData', JSON.stringify(gradesData));
            localStorage.setItem('attendanceData', JSON.stringify(attendanceData));
            localStorage.setItem('rewardsData', JSON.stringify(rewardsData));
            localStorage.setItem('dailyRecordData', JSON.stringify(gatherDailyRows()));
        }

        function loadSavedData() {
            const teacherInfo = JSON.parse(localStorage.getItem('teacherInfo'));
            if (teacherInfo) {
                Object.keys(teacherInfo).forEach(key => {
                    const el = document.getElementById(key);
                    if (el) el.value = teacherInfo[key];
                });
            }

            const scheduleInfo = JSON.parse(localStorage.getItem('scheduleInfo'));
            if (scheduleInfo) {
                const scheduleTeacher = document.getElementById('scheduleTeacher');
                const scheduleYear = document.getElementById('scheduleYear');
                const assignedClasses = document.getElementById('assignedClasses');
                const workHours = document.getElementById('workHours');
                
                if (scheduleTeacher) scheduleTeacher.value = scheduleInfo.teacher || '';
                if (scheduleYear) scheduleYear.value = scheduleInfo.year || '';
                if (assignedClasses) assignedClasses.value = scheduleInfo.classes || '';
                if (workHours) workHours.value = scheduleInfo.hours || '';
                
                if (scheduleInfo.table) {
                    const rows = document.querySelectorAll('.schedule-table tbody tr');
                    rows.forEach((tr, rowIndex) => {
                        tr.querySelectorAll('input').forEach((input, colIndex) => {
                            input.value = scheduleInfo.table[rowIndex]?.[colIndex] || '';
                        });
                    });
                }
            }

            studentsData = JSON.parse(localStorage.getItem('studentsData')) || {};
            gradesData = JSON.parse(localStorage.getItem('gradesData')) || {};
            attendanceData = JSON.parse(localStorage.getItem('attendanceData')) || {};
            rewardsData = JSON.parse(localStorage.getItem('rewardsData')) || {};
            dailyRecords = JSON.parse(localStorage.getItem('dailyRecordData')) || [];
        }

        // Tab Management
        function showTab(tabId, event) {
            // Hide all tab contents
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Remove active class from all tab buttons
            document.querySelectorAll('.tab-button').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected tab content
            const selectedTab = document.getElementById(tabId);
            if (selectedTab) {
                selectedTab.classList.add('active');
            }
            
            // Add active class to clicked button
            if (event && event.target) {
                event.target.classList.add('active');
            }
            
            // Special handling for specific tabs
            if (tabId === 'assignments') {
                // Load and render assignments when assignments tab is shown
                console.log('Assignments tab opened, rendering assignments...');
                updateAssignmentClassSelects();
                renderAssignments();
            } else if (tabId === 'rewards') {
                // Update rewards list when rewards tab is shown
                updateRewardsList();
            } else if (tabId === 'grades') {
                // Update grades table when grades tab is shown
                updateGradesTable();
            } else if (tabId === 'attendance') {
                // Update attendance list when attendance tab is shown
                updateAttendanceList();
            } else if (tabId === 'behavior') {
                // Update behavior list when behavior tab is shown
                updateBehaviorList();
            } else if (tabId === 'analyticsTab') {
                // Update analytics when analytics tab is shown
                updateAnalytics();
            }
        }
        
        // (removed) Duplicate DOMContentLoaded initializer to avoid double init

        function removeRewardPoint(studentId) {
            const className = document.getElementById('rewardsClassSelect').value;
            if (rewardsData[className]?.[studentId]?.points > 0) {
                rewardsData[className][studentId].points--;
                updateRewardsList();
            }
        }
        
        // --- Behavior Management ---
        function updateBehaviorList() {
            const className = document.getElementById('behaviorClassSelect').value;
            const container = document.getElementById('behaviorList');
            if (!className || !studentsData[className] || studentsData[className].length === 0) {
                container.innerHTML = '<p style="text-align: center; padding: 20px; color: #666;">لا يوجد تلاميذ في هذا القسم</p>';
                return;
            }
            container.innerHTML = studentsData[className].map(student => {
                const behavior = rewardsData[className]?.[student.id] || { points: 0 };
                const behaviorLevel = behavior.points >= 80 ? 'ممتاز' : behavior.points >= 60 ? 'جيد' : behavior.points >= 40 ? 'مقبول' : 'ضعيف';
                return `
                    <div class="student-item">
                        <span>${student.name} - التقدير: ${behaviorLevel}</span>
                        <div>
                            <button class="add-button" onclick="addBehaviorPoint(${student.id})">+ نقطة سلوك</button>
                            <button class="remove-button" onclick="removeBehaviorPoint(${student.id})">- نقطة سلوك</button>
                        </div>
                    </div>
                `;
            }).join('');
        }
        
        function addBehaviorPoint(studentId) {
            const className = document.getElementById('behaviorClassSelect').value;
            if (!rewardsData[className]) rewardsData[className] = {};
            if (!rewardsData[className][studentId]) rewardsData[className][studentId] = { points: 0 };
            rewardsData[className][studentId].points++;
            updateBehaviorList();
            updateRewardsList();
        }
        
        function removeBehaviorPoint(studentId) {
            const className = document.getElementById('behaviorClassSelect').value;
            if (rewardsData[className]?.[studentId]?.points > 0) {
                rewardsData[className][studentId].points--;
                updateBehaviorList();
                updateRewardsList();
            }
        }
        
        // --- Analytics ---
        function updateAnalytics() {
            const className = document.getElementById('analyticsClassSelect').value;
            if (!className || !studentsData[className]) {
                document.getElementById('analyticsContent').innerHTML = '<p style="text-align: center; padding: 20px; color: #666;">لا توجد بيانات للتحليل</p>';
                return;
            }
            
            const students = studentsData[className];
            const generalStats = document.getElementById('generalStats');
            const topStudents = document.getElementById('topStudents');
            const needsSupport = document.getElementById('needsSupport');
            
            // General Statistics
            const totalStudents = students.length;
            const avgGrade = students.reduce((sum, student) => {
                const grades = gradesData[className]?.[student.id] || { average: 0 };
                return sum + (grades.average || 0);
            }, 0) / totalStudents;
            
            const avgAttendance = students.reduce((sum, student) => {
                const attendance = attendanceData[className]?.[student.id] || { absences: 0 };
                return sum + (20 - (attendance.absences || 0));
            }, 0) / totalStudents;
            
            generalStats.innerHTML = `
                <p>إجمالي التلاميذ: ${totalStudents}</p>
                <p>متوسط المعدل: ${avgGrade.toFixed(2)}/20</p>
                <p>متوسط الحضور: ${avgAttendance.toFixed(1)}/20</p>
            `;
            
            // Top Students
            const topStudentsList = students
                .map(student => {
                    const grades = gradesData[className]?.[student.id] || { average: 0 };
                    return { ...student, average: grades.average || 0 };
                })
                .sort((a, b) => b.average - a.average)
                .slice(0, 5);
            
            topStudents.innerHTML = topStudentsList.map(student => 
                `<p>${student.name}: ${student.average.toFixed(2)}/20</p>`
            ).join('');
            
            // Students needing support
            const needsSupportList = students
                .map(student => {
                    const grades = gradesData[className]?.[student.id] || { average: 0 };
                    const attendance = attendanceData[className]?.[student.id] || { absences: 0 };
                    return { ...student, average: grades.average || 0, absences: attendance.absences || 0 };
                })
                .filter(student => student.average < 10 || student.absences > 5)
                .slice(0, 5);
            
            needsSupport.innerHTML = needsSupportList.length > 0 ? 
                needsSupportList.map(student => 
                    `<p>${student.name}: معدل ${student.average.toFixed(2)}، غيابات ${student.absences}</p>`
                ).join('') : 
                '<p>لا يوجد تلاميذ يحتاجون للدعم</p>';
        }

        // Helper function to get assignment type name in Arabic
        function getAssignmentTypeName(type) {
            const typeNames = {
                'homework': 'واجب منزلي',
                'project': 'مشروع',
                'research': 'بحث',
                'presentation': 'عرض'
            };
            return typeNames[type] || type;
        }
        
        // Function to delete an assignment
        function deleteAssignment(assignmentId) {
            if (confirm('هل أنت متأكد من حذف هذا الواجب؟')) {
                assignmentsData = assignmentsData.filter(x => x.id !== assignmentId);
                localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
                showNotification('تم حذف الواجب بنجاح', 'success');
                renderAssignments();
            }
        }
        
        // Test function to check if assignments system is working
        function testAssignmentFunction() {
            try {
                console.log('=== TESTING ASSIGNMENTS SYSTEM ===');
                
                // Check if elements exist
                const titleInput = document.getElementById('assignmentTitle');
                const classSelect = document.getElementById('assignmentClass');
                const form = document.getElementById('assignmentForm');
                const list = document.getElementById('assignmentsList');
                
                console.log('Elements found:', {
                    titleInput: !!titleInput,
                    classSelect: !!classSelect,
                    form: !!form,
                    list: !!list
                });
                
                // Check if assignmentsData exists
                console.log('assignmentsData:', assignmentsData);
                console.log('ASSIGN_KEY:', ASSIGN_KEY);
                
                // Check localStorage
                const saved = localStorage.getItem(ASSIGN_KEY);
                console.log('localStorage saved:', saved);
                
                // Test creating a simple assignment
                const testAssignment = {
                    id: Date.now(),
                    title: 'واجب اختبار',
                    description: 'هذا واجب اختبار',
                    class: '1AM1',
                    dueDate: '2024-12-31',
                    type: 'homework',
                    maxPoints: 10,
                    submissions: {}
                };
                
                console.log('Test assignment:', testAssignment);
                
                // Add to array
                if (!assignmentsData) {
                    assignmentsData = [];
                }
                assignmentsData.push(testAssignment);
                
                // Save to localStorage
                localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
                
                // Try to render
                renderAssignments();
                
                alert('تم اختبار النظام! تحقق من وحدة التحكم (F12) لرؤية النتائج.');
                
            } catch (error) {
                console.error('Test function error:', error);
                alert('خطأ في اختبار النظام: ' + error.message);
            }
        }

        // Homework Tracking Functions
        let currentTrackingAssignment = null;
        
        function openHomeworkTracking(assignmentId) {
            const assignment = assignmentsData.find(a => a.id === assignmentId);
            if (!assignment) {
                alert('لم يتم العثور على الواجب');
                return;
            }
            
            currentTrackingAssignment = assignment;
            
            // Initialize submissions object if it doesn't exist
            if (!currentTrackingAssignment.submissions) {
                currentTrackingAssignment.submissions = {};
            }
            
            console.log('=== OPENING HOMEWORK TRACKING ===');
            console.log('Assignment:', assignment);
            console.log('Submissions object:', currentTrackingAssignment.submissions);
            
            // Update modal title and info
            document.getElementById('trackingModalTitle').textContent = `تتبع الواجب: ${assignment.title}`;
            
            const infoContent = document.getElementById('homeworkInfoContent');
            infoContent.innerHTML = `
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                    <div><strong>🏫 القسم:</strong> ${assignment.class}</div>
                    <div><strong>📝 النوع:</strong> ${getAssignmentTypeName(assignment.type)}</div>
                    <div><strong>📅 تاريخ الاستحقاق:</strong> ${assignment.dueDate}</div>
                    <div><strong>⭐ الدرجة القصوى:</strong> ${assignment.maxPoints}</div>
                    <div style="grid-column: 1 / -1; text-align: center; padding: 10px; border-radius: 8px; background: ${assignment.pointsApplied ? '#d4edda' : '#fff3cd'}; color: ${assignment.pointsApplied ? '#155724' : '#856404'}; border: 1px solid ${assignment.pointsApplied ? '#c3e6cb' : '#ffeaa7'};">
                        <strong>${assignment.pointsApplied ? '✅ تم تطبيق النقاط مسبقاً' : '⚠️ لم يتم تطبيق النقاط بعد'}</strong>
                    </div>
                </div>
            `;
            
            // Load students for this class
            loadStudentsForTracking(assignment.class);
            
            // Show modal
            document.getElementById('homeworkTrackingModal').style.display = 'block';
        }
        
        function loadStudentsForTracking(className) {
            const students = studentsData[className] || [];
            const tbody = document.getElementById('homeworkTrackingStudentsBody');
            
            if (!tbody) return;
            
            tbody.innerHTML = '';
            
            if (students.length === 0) {
                tbody.innerHTML = '<tr><td colspan="8" style="text-align: center; padding: 20px; color: #666;">لا يوجد تلاميذ في هذا القسم</td></tr>';
                return;
            }
            
            students.forEach((student, index) => {
                // Ensure submission object exists in the actual data
                if (!currentTrackingAssignment.submissions[student.id]) {
                    currentTrackingAssignment.submissions[student.id] = { submitted: false, date: '', points: 0 };
                }
                
                const submission = currentTrackingAssignment.submissions[student.id];
                const row = document.createElement('tr');
                
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td><strong>${student.name}</strong></td>
                    <td>${className}</td>
                    <td>
                        <select class="submission-status" data-student-id="${student.id}" onchange="updateSubmissionStatus(${student.id}, this.value)">
                            <option value="false" ${!submission.submitted ? 'selected' : ''}>لم يسلم</option>
                            <option value="true" ${submission.submitted ? 'selected' : ''}>سلم</option>
                        </select>
                    </td>
                    <td>
                        <input type="date" class="submission-date" data-student-id="${student.id}" 
                               value="${submission.date || ''}" 
                               ${!submission.submitted ? 'disabled' : ''}
                               onchange="updateSubmissionDate(${student.id}, this.value)">
                    </td>
                    <td>
                        ${submission.submitted ? 
                            `<div style="display: flex; gap: 5px; align-items: center;">
                                <input type="number" class="submission-points" data-student-id="${student.id}" 
                                       value="${submission.points || 0}" min="1" max="10" style="width: 60px;"
                                       onchange="updateSubmissionPoints(${student.id}, this.value)">
                                <span style="color: #28a745; font-size: 0.8em;">إضافة نقاط</span>
                            </div>` :
                            `<div style="display: flex; gap: 5px; align-items: center;">
                                <input type="number" class="submission-points" data-student-id="${student.id}" 
                                       value="${submission.points || 0}" min="1" max="5" style="width: 60px;"
                                       onchange="updateSubmissionPoints(${student.id}, this.value)">
                                <span style="color: #dc3545; font-size: 0.8em;">خصم نقاط</span>
                            </div>`
                        }
                    </td>
                    <td>
                        <button class="add-button" onclick="saveIndividualStudent(${student.id})" style="font-size: 0.8em; padding: 5px 10px;">
                            💾 حفظ
                        </button>
                    </td>
                    <td>
                        <span style="color: #666; font-size: 0.8em;">
                            ${submission.submitted ? '✅ تم التسليم' : '❌ لم يسلم'}
                        </span>
                    </td>
                `;
                
                tbody.appendChild(row);
            });
        }
        
        function updateSubmissionStatus(studentId, status) {
            if (!currentTrackingAssignment) return;
            
            const isSubmitted = status === 'true';
            
            if (!currentTrackingAssignment.submissions[studentId]) {
                currentTrackingAssignment.submissions[studentId] = { submitted: false, date: '', points: 0 };
            }
            
            currentTrackingAssignment.submissions[studentId].submitted = isSubmitted;
            
            // Auto-set current date when marked as submitted
            if (isSubmitted) {
                currentTrackingAssignment.submissions[studentId].date = new Date().toISOString().split('T')[0];
            }
            
            // Enable/disable date input only
            const dateInput = document.querySelector(`.submission-date[data-student-id="${studentId}"]`);
            
            if (dateInput) dateInput.disabled = !isSubmitted;
            
            // Refresh the table to show the correct points column (add/subtract)
            loadStudentsForTracking(currentTrackingAssignment.class);
        }
        
        function updateSubmissionDate(studentId, date) {
            if (!currentTrackingAssignment) return;
            
            if (!currentTrackingAssignment.submissions[studentId]) {
                currentTrackingAssignment.submissions[studentId] = { submitted: false, date: '', points: 0 };
            }
            
            currentTrackingAssignment.submissions[studentId].date = date;
        }
        
        function updateSubmissionPoints(studentId, points) {
            if (!currentTrackingAssignment) return;
            
            console.log(`=== UPDATING SUBMISSION POINTS ===`);
            console.log(`Student ID: ${studentId}, Points: ${points}`);
            
            if (!currentTrackingAssignment.submissions[studentId]) {
                currentTrackingAssignment.submissions[studentId] = { submitted: false, date: '', points: 0 };
                console.log(`Created new submission for student ${studentId}`);
            }
            
            const currentPoints = parseInt(points) || 0;
            currentTrackingAssignment.submissions[studentId].points = currentPoints;
            
            console.log(`Updated submission points:`, currentTrackingAssignment.submissions[studentId]);
            
            // Save the updated assignment data immediately
            const assignmentIndex = assignmentsData.findIndex(a => a.id === currentTrackingAssignment.id);
            if (assignmentIndex !== -1) {
                assignmentsData[assignmentIndex] = currentTrackingAssignment;
                localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
                console.log(`Saved updated assignment data to localStorage`);
            }
            
            // DON'T update rewards here - only save the points value
            // Points will be applied when saving the tracking
        }
        
        // markHomeworkComplete function removed - status is controlled manually through dropdown
        
        function updateStudentRewards(studentId, className, points) {
            console.log(`=== UPDATE STUDENT REWARDS ===`);
            console.log(`Student ID: ${studentId}, Class: ${className}, Points: ${points}`);
            
            // Initialize rewards data if it doesn't exist
            if (!rewardsData[className]) {
                rewardsData[className] = {};
                console.log(`Created new rewards data for class ${className}`);
            }
            
            if (!rewardsData[className][studentId]) {
                rewardsData[className][studentId] = { points: 0 };
                console.log(`Created new rewards data for student ${studentId}`);
            }
            
            const oldPoints = rewardsData[className][studentId].points;
            
            // Add points to student
            rewardsData[className][studentId].points += points;
            
            console.log(`Points updated: ${oldPoints} + ${points} = ${rewardsData[className][studentId].points}`);
            
            // Save to localStorage
            localStorage.setItem('rewardsData', JSON.stringify(rewardsData));
            console.log(`Saved to localStorage:`, localStorage.getItem('rewardsData'));
            
            // Update the rewards display in التلاميذ section
            try {
                updateRewardsList();
                console.log(`Rewards list updated successfully`);
            } catch (error) {
                console.error(`Error updating rewards list:`, error);
            }
            
            console.log(`Final rewards data:`, rewardsData);
            console.log(`=== UPDATE COMPLETED ===`);
        }
        
        // Test function to manually add points
        function testAddPoints() {
            const className = document.getElementById('rewardsClassSelect')?.value || '1AM1';
            const testStudentId = Object.keys(studentsData[className] || {})[0];
            
            if (testStudentId) {
                console.log(`Testing points addition for student ${testStudentId} in class ${className}`);
                updateStudentRewards(testStudentId, className, 5);
                alert(`تم إضافة 5 نقاط للتلميذ الأول في القسم ${className}. تحقق من النقاط والجوائز!`);
            } else {
                alert('لا يوجد تلاميذ في هذا القسم للاختبار');
            }
        }
        
        // Function to refresh rewards data from localStorage
        function refreshRewardsData() {
            console.log('=== REFRESHING REWARDS DATA ===');
            
            // Reload rewards data from localStorage
            const savedRewards = localStorage.getItem('rewardsData');
            console.log('Saved rewards from localStorage:', savedRewards);
            
            if (savedRewards) {
                try {
                    rewardsData = JSON.parse(savedRewards);
                    console.log('Parsed rewards data:', rewardsData);
                } catch (error) {
                    console.error('Error parsing rewards data:', error);
                    rewardsData = {};
                }
            } else {
                console.log('No saved rewards data found');
                rewardsData = {};
            }
            
            // Update the display
            updateRewardsList();
            
            alert('تم تحديث بيانات النقاط من التخزين المحلي!');
        }
        
        function saveHomeworkTracking() {
            if (!currentTrackingAssignment) return;
            
            console.log('=== SAVING HOMEWORK TRACKING ===');
            console.log('Current assignment:', currentTrackingAssignment);
            console.log('Current submissions:', currentTrackingAssignment.submissions);
            
            // Check if points were already applied (prevent double counting)
            if (currentTrackingAssignment.pointsApplied) {
                alert('تم تطبيق النقاط مسبقاً لهذا الواجب!');
                return;
            }
            
            // Process all points before saving
            const students = studentsData[currentTrackingAssignment.class] || [];
            console.log(`Processing ${students.length} students for class ${currentTrackingAssignment.class}`);
            
            let totalPointsApplied = 0;
            
            students.forEach(student => {
                const submission = currentTrackingAssignment.submissions[student.id];
                console.log(`\n--- Processing Student: ${student.name} ---`);
                console.log(`Submission data:`, submission);
                
                if (submission) {
                    console.log(`Submission exists for ${student.name}`);
                    console.log(`Points: ${submission.points}, Submitted: ${submission.submitted}`);
                    
                    // Check if points exist and are greater than 0
                    if (submission.points && submission.points > 0) {
                        if (submission.submitted) {
                            // Add points for submitted homework
                            console.log(`✅ Adding ${submission.points} points to student ${student.name}`);
                            updateStudentRewards(student.id, currentTrackingAssignment.class, submission.points);
                            totalPointsApplied += submission.points;
                        } else {
                            // Subtract points for not submitted homework
                            console.log(`❌ Subtracting ${submission.points} points from student ${student.name}`);
                            updateStudentRewards(student.id, currentTrackingAssignment.class, -submission.points);
                            totalPointsApplied += submission.points;
                        }
                    } else {
                        console.log(`⚠️ No points to apply for ${student.name} (points: ${submission.points})`);
                    }
                } else {
                    console.log(`⚠️ No submission data for ${student.name}`);
                }
            });
            
            console.log(`\n=== SUMMARY ===`);
            console.log(`Total points processed: ${totalPointsApplied}`);
            console.log(`Final rewards data:`, rewardsData);
            
            // Mark points as applied to prevent double counting
            currentTrackingAssignment.pointsApplied = true;
            
            // Update the assignment in the main assignmentsData array
            const assignmentIndex = assignmentsData.findIndex(a => a.id === currentTrackingAssignment.id);
            if (assignmentIndex !== -1) {
                assignmentsData[assignmentIndex] = currentTrackingAssignment;
                console.log('Updated assignment in main data array');
            }
            
            // Save assignments data
            localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
            
            // Update the display
            renderAssignments();
            
            alert(`تم حفظ تتبع الواجب والنقاط بنجاح!\n\nتم معالجة ${totalPointsApplied} نقاط.`);
            closeHomeworkTrackingModal();
        }
        
        function debugHomeworkTracking() {
            if (!currentTrackingAssignment) {
                alert('لا يوجد واجب مفتوح للتصحيح');
                return;
            }
            
            console.log('=== DEBUG HOMEWORK TRACKING ===');
            console.log('Current tracking assignment:', currentTrackingAssignment);
            console.log('All assignments data:', assignmentsData);
            console.log('Current rewards data:', rewardsData);
            
            // Check submissions
            if (currentTrackingAssignment.submissions) {
                console.log('Submissions data:');
                Object.keys(currentTrackingAssignment.submissions).forEach(studentId => {
                    const submission = currentTrackingAssignment.submissions[studentId];
                    const student = studentsData[currentTrackingAssignment.class]?.find(s => s.id == studentId);
                    console.log(`Student ${student?.name || studentId}:`, submission);
                });
            }
            
            // Check localStorage
            const savedAssignments = localStorage.getItem(ASSIGN_KEY);
            const savedRewards = localStorage.getItem('rewardsData');
            console.log('Saved assignments from localStorage:', savedAssignments);
            console.log('Saved rewards from localStorage:', savedRewards);
            
            alert('تم إرسال معلومات التصحيح إلى وحدة التحكم (Console). اضغط F12 لرؤية التفاصيل.');
        }
        
        function saveIndividualStudent(studentId) {
            if (!currentTrackingAssignment) return;
            
            const submission = currentTrackingAssignment.submissions[studentId];
            if (!submission) return;
            
            console.log(`=== SAVING INDIVIDUAL STUDENT ===`);
            console.log(`Student ID: ${studentId}`);
            console.log(`Submission data:`, submission);
            
            // Apply points to rewards system immediately
            if (submission.points > 0) {
                if (submission.submitted) {
                    // Add points for submitted homework
                    console.log(`✅ Adding ${submission.points} points to student ${studentId}`);
                    updateStudentRewards(studentId, currentTrackingAssignment.class, submission.points);
                } else {
                    // Subtract points for not submitted homework
                    console.log(`❌ Subtracting ${submission.points} points from student ${studentId}`);
                    updateStudentRewards(studentId, currentTrackingAssignment.class, -submission.points);
                }
            }
            
            // Update the assignment in the main assignmentsData array
            const assignmentIndex = assignmentsData.findIndex(a => a.id === currentTrackingAssignment.id);
            if (assignmentIndex !== -1) {
                assignmentsData[assignmentIndex] = currentTrackingAssignment;
                console.log('Updated assignment in main data array');
            }
            
            // Save to localStorage
            localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
            
            // Show success message
            const student = studentsData[currentTrackingAssignment.class]?.find(s => s.id == studentId);
            const studentName = student ? student.name : `Student ${studentId}`;
            const action = submission.submitted ? 'إضافة' : 'خصم';
            const points = submission.points;
            
            alert(`تم حفظ بيانات ${studentName} بنجاح!\n\n${action} ${points} نقاط`);
            
            console.log(`=== INDIVIDUAL SAVE COMPLETED ===`);
        }
        
        function refreshAssignments() {
            console.log('=== REFRESHING ASSIGNMENTS ===');
            
            // Reload assignments data from localStorage
            const savedAssignments = localStorage.getItem(ASSIGN_KEY);
            console.log('Saved assignments from localStorage:', savedAssignments);
            
            if (savedAssignments) {
                try {
                    assignmentsData = JSON.parse(savedAssignments);
                    console.log('Parsed assignments data:', assignmentsData);
                } catch (error) {
                    console.error('Error parsing assignments data:', error);
                    assignmentsData = [];
                }
            } else {
                console.log('No saved assignments data found');
                assignmentsData = [];
            }
            
            // Update the display
            renderAssignments();
            
            alert('تم تحديث قائمة الواجبات من التخزين المحلي!');
        }
        
        function testNavigation() {
            console.log('=== TESTING NAVIGATION ===');
            
            // Test if sections exist
            const sections = ['teacherInfo', 'schedule', 'students', 'dailyRecord', 'lessons', 'presentations', 'settings', 'calendar', 'lessonPlanner', 'parents', 'quizBuilder'];
            
            sections.forEach(sectionId => {
                const section = document.getElementById(sectionId);
                if (section) {
                    console.log(`✅ Section ${sectionId} exists`);
                    console.log(`   - Display style: ${section.style.display}`);
                    console.log(`   - Computed display: ${window.getComputedStyle(section).display}`);
                } else {
                    console.log(`❌ Section ${sectionId} NOT found`);
                }
            });
            
            // Test showSection function
            console.log('Testing showSection function...');
            showSection('dailyRecord');
            
            alert('تم اختبار التنقل! راجع وحدة التحكم للحصول على التفاصيل.');
        }
        
        function resetHomeworkPoints() {
            if (!currentTrackingAssignment) return;
            
            if (confirm('هل أنت متأكد من إعادة تعيين النقاط لهذا الواجب؟')) {
                // Reset the points applied flag
                currentTrackingAssignment.pointsApplied = false;
                
                // Clear all submission points
                if (currentTrackingAssignment.submissions) {
                    Object.keys(currentTrackingAssignment.submissions).forEach(studentId => {
                        if (currentTrackingAssignment.submissions[studentId]) {
                            currentTrackingAssignment.submissions[studentId].points = 0;
                        }
                    });
                }
                
                // Save the reset data
                localStorage.setItem(ASSIGN_KEY, JSON.stringify(assignmentsData));
                
                // Refresh the display
                loadStudentsForTracking(currentTrackingAssignment.class);
                
                alert('تم إعادة تعيين النقاط بنجاح! يمكنك الآن إدخال النقاط مرة أخرى.');
            }
        }
        
        function closeHomeworkTrackingModal() {
            document.getElementById('homeworkTrackingModal').style.display = 'none';
            currentTrackingAssignment = null;
        }
        
        function exportHomeworkToExcel(assignmentId) {
            const assignment = assignmentsData.find(a => a.id === assignmentId);
            if (!assignment) {
                alert('لم يتم العثور على الواجب');
                return;
            }
            
            const students = studentsData[assignment.class] || [];
            const data = students.map((student, index) => {
                const submission = assignment.submissions[student.id] || { submitted: false, date: '', points: 0 };
                return {
                    '#': index + 1,
                    'اسم التلميذ': student.name,
                    'القسم': assignment.class,
                    'عنوان الواجب': assignment.title,
                    'نوع الواجب': getAssignmentTypeName(assignment.type),
                    'تاريخ الاستحقاق': assignment.dueDate,
                    'الدرجة القصوى': assignment.maxPoints,
                    'حالة التسليم': submission.submitted ? 'سلم' : 'لم يسلم',
                    'تاريخ التسليم': submission.date || '-',
                    'النقاط الممنوحة': submission.points || 0
                };
            });
            
            const ws = XLSX.utils.json_to_sheet(data);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, `واجب_${assignment.title}`);
            XLSX.writeFile(wb, `واجب_${assignment.title}_${assignment.class}.xlsx`);
            
            alert('تم تصدير الواجب إلى Excel بنجاح!');
        }
    </script>
</body>
</html>
