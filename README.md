# campus-xerox-queue-management
Queue management system for Campus Xerox and Printing Shop
index.html:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Campus Xerox & Printing Shop - Queue Management System</title>
    <link rel="stylesheet" href="css/style.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
</head>
<body>

    <!-- Top Navigation Bar -->
    <header class="navbar">
        <div class="nav-container">
            <div class="brand">
                <div class="brand-logo">🖨️</div>
                <div class="brand-text">
                    <h1>Campus PrintQ</h1>
                    <p class="brand-sub">Xerox & Printing Shop Queue System</p>
                </div>
            </div>
            
            <nav class="nav-tabs">
                <button class="nav-btn active" data-tab="student-tab">
                    <span class="tab-icon">📝</span> Student Portal
                </button>
                <button class="nav-btn" data-tab="live-queue-tab">
                    <span class="tab-icon">⏱️</span> Live Queue Board
                </button>
                <button class="nav-btn" data-tab="operator-tab">
                    <span class="tab-icon">⚙️</span> Operator Dashboard
                </button>
            </nav>

            <div class="server-status-badge">
                <span class="status-dot online"></span>
                <span id="backend-status-text">Backend: Connected</span>
            </div>
        </div>
    </header>

    <!-- Main Application Container -->
    <main class="main-container">

        <!-- Banner / Quick Value Metric -->
        <section class="hero-strip">
            <div class="hero-content">
                <h2>Skip the 45-Minute Print Shop Rush!</h2>
                <p>Submit documents online, get a real-time queue token, track your printing progress from anywhere on campus, and walk in only when it's ready for pickup.</p>
            </div>
            <div class="hero-pills">
                <div class="pill">⚡ Instant FIFO Token</div>
                <div class="pill">💰 Live Dynamic Pricing</div>
                <div class="pill">🛡️ Zero Pen-Drive Viruses</div>
            </div>
        </section>

        <!-- Toast Notification Container -->
        <div id="toast-container" class="toast-container"></div>

        <!-- ===================================================================
             TAB 1: STUDENT PORTAL (Submit Request & Live Tracking)
             =================================================================== -->
        <section id="student-tab" class="tab-pane active">
            <div class="portal-grid">
                
                <!-- Left Column: Print Request Submission Form -->
                <div class="card form-card">
                    <div class="card-header">
                        <div class="card-title">
                            <span class="header-icon">📄</span>
                            <div>
                                <h3>Submit Printing Request</h3>
                                <p>Fill in your document details and print specifications</p>
                            </div>
                        </div>
                    </div>

                    <form id="print-order-form" novalidate>
                        <!-- Section 1: Student Information -->
                        <div class="form-section-title">1. Student Details</div>
                        <div class="form-row two-col">
                            <div class="form-group">
                                <label for="fullName">Full Name <span class="req">*</span></label>
                                <input type="text" id="fullName" name="fullName" placeholder="e.g. Kavitha Raman" required>
                                <span class="error-text" id="err-fullName"></span>
                            </div>
                            <div class="form-group">
                                <label for="registerNumber">Register / Roll No <span class="req">*</span></label>
                                <input type="text" id="registerNumber" name="registerNumber" placeholder="e.g. 710123CSBS042" required>
                                <span class="error-text" id="err-registerNumber"></span>
                            </div>
                        </div>

                        <div class="form-row two-col">
                            <div class="form-group">
                                <label for="email">Campus Email <span class="req">*</span></label>
                                <input type="email" id="email" name="email" placeholder="student@campus.edu" required>
                                <span class="error-text" id="err-email"></span>
                            </div>
                            <div class="form-group">
                                <label for="phoneNumber">Mobile Number <span class="req">*</span></label>
                                <input type="tel" id="phoneNumber" name="phoneNumber" placeholder="e.g. 9876543210" required>
                                <span class="error-text" id="err-phoneNumber"></span>
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="department">Department <span class="req">*</span></label>
                            <select id="department" name="department" required>
                                <option value="">-- Select Department --</option>
                                <option value="Computer Science & Business Systems">Computer Science & Business Systems (CSBS)</option>
                                <option value="Computer Science & Engineering">Computer Science & Engineering (CSE)</option>
                                <option value="Information Technology">Information Technology (IT)</option>
                                <option value="Artificial Intelligence & Data Science">Artificial Intelligence & Data Science (AI & DS)</option>
                                <option value="Electronics & Communication">Electronics & Communication (ECE)</option>
                                <option value="Electrical & Electronics">Electrical & Electronics (EEE)</option>
                                <option value="Mechanical Engineering">Mechanical Engineering (MECH)</option>
                                <option value="Civil Engineering">Civil Engineering (CIVIL)</option>
                                <option value="MBA / Management">MBA / Management</option>
                            </select>
                            <span class="error-text" id="err-department"></span>
                        </div>

                        <!-- Section 2: Document & Print Specs -->
                        <div class="form-section-title">2. Document Specifications</div>
                        <div class="form-row two-col">
                            <div class="form-group">
                                <label for="documentTitle">Document Name / Title <span class="req">*</span></label>
                                <input type="text" id="documentTitle" name="documentTitle" placeholder="e.g. OS_Lab_Manual_Final.pdf" required>
                                <span class="error-text" id="err-documentTitle"></span>
                            </div>
                            <div class="form-group">
                                <label for="documentType">Document Type</label>
                                <select id="documentType" name="documentType">
                                    <option value="PDF">PDF Document (.pdf)</option>
                                    <option value="DOCX">Word Document (.docx)</option>
                                    <option value="PPTX">Presentation Slides (.pptx)</option>
                                    <option value="IMAGE">Image / Poster (.png, .jpg)</option>
                                </select>
                            </div>
                        </div>

                        <div class="form-row two-col">
                            <div class="form-group">
                                <label for="pageCount">Total Pages <span class="req">*</span></label>
                                <input type="number" id="pageCount" name="pageCount" min="1" value="1" required>
                                <span class="error-text" id="err-pageCount"></span>
                            </div>
                            <div class="form-group">
                                <label for="copies">Number of Copies <span class="req">*</span></label>
                                <input type="number" id="copies" name="copies" min="1" value="1" required>
                                <span class="error-text" id="err-copies"></span>
                            </div>
                        </div>

                        <!-- Options: Color Mode -->
                        <div class="form-group">
                            <label>Print Color Mode <span class="req">*</span></label>
                            <div class="radio-card-group">
                                <label class="radio-card">
                                    <input type="radio" name="printColor" value="BLACK_AND_WHITE" checked>
                                    <div class="radio-card-content">
                                        <span class="radio-title">Black & White</span>
                                        <span class="radio-price" id="rate-bw">₹1.00 / page</span>
                                    </div>
                                </label>
                                <label class="radio-card">
                                    <input type="radio" name="printColor" value="COLOR">
                                    <div class="radio-card-content">
                                        <span class="radio-title">Full Color</span>
                                        <span class="radio-price" id="rate-color">₹5.00 / page</span>
                                    </div>
                                </label>
                            </div>
                        </div>

                        <!-- Options: Page Layout (Duplex) -->
                        <div class="form-group">
                            <label>Page Side Layout <span class="req">*</span></label>
                            <div class="radio-card-group">
                                <label class="radio-card">
                                    <input type="radio" name="pageSide" value="SINGLE_SIDED" checked>
                                    <div class="radio-card-content">
                                        <span class="radio-title">Single Sided</span>
                                        <span class="radio-desc">Standard standard sheet</span>
                                    </div>
                                </label>
                                <label class="radio-card">
                                    <input type="radio" name="pageSide" value="DOUBLE_SIDED">
                                    <div class="radio-card-content">
                                        <span class="radio-title">Double Sided (Duplex)</span>
                                        <span class="radio-desc">Paper saving (25% off per side)</span>
                                    </div>
                                </label>
                            </div>
                        </div>

                        <!-- Options: Binding -->
                        <div class="form-group">
                            <label>Binding Option</label>
                            <div class="radio-card-group binding-group">
                                <label class="radio-card">
                                    <input type="radio" name="bindingType" value="NONE" checked>
                                    <div class="radio-card-content">
                                        <span class="radio-title">No Binding</span>
                                        <span class="radio-price">₹0</span>
                                    </div>
                                </label>
                                <label class="radio-card">
                                    <input type="radio" name="bindingType" value="STAPLE">
                                    <div class="radio-card-content">
                                        <span class="radio-title">Staple Corner</span>
                                        <span class="radio-price">+ ₹2</span>
                                    </div>
                                </label>
                                <label class="radio-card">
                                    <input type="radio" name="bindingType" value="SPIRAL">
                                    <div class="radio-card-content">
                                        <span class="radio-title">Spiral Bound</span>
                                        <span class="radio-price">+ ₹25</span>
                                    </div>
                                </label>
                                <label class="radio-card">
                                    <input type="radio" name="bindingType" value="HARD_BOUND">
                                    <div class="radio-card-content">
                                        <span class="radio-title">Hard Bound Project</span>
                                        <span class="radio-price">+ ₹100</span>
                                    </div>
                                </label>
                            </div>
                        </div>

                        <!-- Dynamic Live Cost Preview Banner -->
                        <div class="cost-preview-box">
                            <div class="cost-header">
                                <span>Estimated Printing Cost</span>
                                <span class="cost-currency">INR (₹)</span>
                            </div>
                            <div class="cost-amount-row">
                                <span class="cost-symbol">₹</span>
                                <span class="cost-value" id="preview-cost-total">1.00</span>
                            </div>
                            <div class="cost-breakdown" id="preview-breakdown">
                                1 page × 1 copy @ ₹1.00/pg + ₹0 binding
                            </div>
                        </div>

                        <!-- Submit Button -->
                        <button type="submit" id="btn-submit-order" class="btn btn-primary btn-block">
                            <span class="btn-text">🚀 Submit & Get Queue Token</span>
                            <span class="btn-spinner" style="display: none;">⏳ Queuing...</span>
                        </button>
                    </form>
                </div>

                <!-- Right Column: Instant Token Confirmation & Tracking Search -->
                <div class="portal-sidebar">
                    
                    <!-- Token Result Card (Populated upon submission) -->
                    <div id="new-token-card" class="card token-result-card" style="display: none;">
                        <div class="token-header">
                            <span class="token-badge-icon">🎟️</span>
                            <h4>Your Queue Token Issued!</h4>
                        </div>
                        <div class="token-display">
                            <span class="token-number" id="res-token-number">TK-101</span>
                            <span class="token-status-pill status-pending" id="res-status-pill">PENDING</span>
                        </div>
                        <div class="token-metrics">
                            <div class="metric-box">
                                <span class="metric-label">Queue Position</span>
                                <span class="metric-val" id="res-queue-pos">#1</span>
                            </div>
                            <div class="metric-box">
                                <span class="metric-label">Estimated Wait</span>
                                <span class="metric-val" id="res-wait-time">~3 mins</span>
                            </div>
                            <div class="metric-box">
                                <span class="metric-label">Total Cost</span>
                                <span class="metric-val" id="res-total-cost">₹1.00</span>
                            </div>
                        </div>
                        <div class="token-instructions">
                            <p>📌 Please take a screenshot or note down your token: <strong id="res-token-copy">TK-101</strong>.</p>
                            <p>You will pay cash or UPI at the counter when collecting your document.</p>
                        </div>
                    </div>

                    <!-- Live Queue Tracking Tool -->
                    <div class="card track-card">
                        <div class="card-header">
                            <div class="card-title">
                                <span class="header-icon">🔍</span>
                                <div>
                                    <h3>Track Existing Request</h3>
                                    <p>Enter your token number to check live status</p>
                                </div>
                            </div>
                        </div>

                        <div class="track-input-group">
                            <input type="text" id="track-token-input" placeholder="e.g. TK-101" uppercase>
                            <button id="btn-track-order" class="btn btn-secondary">Check Status</button>
                        </div>

                        <!-- Tracking Result Pane -->
                        <div id="track-result-pane" style="display: none;" class="track-result">
                            <hr class="divider">
                            <div class="track-status-header">
                                <div>
                                    <span class="track-token" id="track-res-token">TK-101</span>
                                    <div class="track-doc" id="track-res-doc">Cloud_Computing_Lab_Record.pdf</div>
                                </div>
                                <span class="token-status-pill" id="track-res-status">PROCESSING</span>
                            </div>

                            <!-- Visual Queue Step Progress -->
                            <div class="status-stepper">
                                <div class="step-item" id="step-pending">
                                    <div class="step-circle">1</div>
                                    <div class="step-label">Pending</div>
                                </div>
                                <div class="step-line" id="line-1"></div>
                                <div class="step-item" id="step-processing">
                                    <div class="step-circle">2</div>
                                    <div class="step-label">Printing</div>
                                </div>
                                <div class="step-line" id="line-2"></div>
                                <div class="step-item" id="step-ready">
                                    <div class="step-circle">3</div>
                                    <div class="step-label">Ready</div>
                                </div>
                                <div class="step-line" id="line-3"></div>
                                <div class="step-item" id="step-completed">
                