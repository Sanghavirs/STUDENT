<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Management System</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #4361ee;
            --secondary-color: #3a0ca3;
            --accent-color: #f72585;
            --dark-color: #1a1a2e;
            --light-color: #f8f9fa;
            --warning-color: #ff9e00;
            --success-color: #4cc9f0;
            --card-bg: rgba(255, 255, 255, 0.9);
            --glass-bg: rgba(255, 255, 255, 0.15);
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), 
                        url('https://images.unsplash.com/photo-1523050854058-8df90110c9f1?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80') no-repeat center center fixed;
            background-size: cover;
            color: #fff;
            line-height: 1.6;
            min-height: 100vh;
            perspective: 1000px;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 1200px;
            margin: 30px auto;
            padding: 20px;
            position: relative;
        }
        
        h1, h2, h3, h4 {
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        h1 {
            text-align: center;
            font-size: 3rem;
            margin-bottom: 30px;
            background: linear-gradient(90deg, #4361ee, #4cc9f0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            position: relative;
        }
        
        h1::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 150px;
            height: 4px;
            background: linear-gradient(90deg, #4361ee, #4cc9f0);
            border-radius: 2px;
        }
        
        .nav-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 30px;
            position: relative;
            z-index: 10;
        }
        
        .main-content {
            display: flex;
            gap: 20px;
            transform-style: preserve-3d;
        }
        
        .sidebar {
            width: 250px;
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
            border: 1px solid rgba(255, 255, 255, 0.18);
            transform: translateZ(20px);
            height: fit-content;
        }
        
        .content-area {
            flex: 1;
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
            border: 1px solid rgba(255, 255, 255, 0.18);
            transform: translateZ(30px);
        }
        
        .nav-btn {
            padding: 12px 20px;
            background: linear-gradient(135deg, rgba(67, 97, 238, 0.7), rgba(58, 12, 163, 0.7));
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 500;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            min-width: 150px;
            text-align: center;
        }
        
        .nav-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: 0.5s;
        }
        
        .nav-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .nav-btn:hover::before {
            left: 100%;
        }
        
        .nav-btn.active {
            background: linear-gradient(135deg, #4361ee, #3a0ca3);
            box-shadow: 0 5px 15px rgba(67, 97, 238, 0.4);
        }
        
        .section {
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        .section.active {
            display: block;
        }
        
        .section-preview {
            position: absolute;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            padding: 15px;
            width: 300px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            z-index: 100;
            color: #333;
            display: none;
            border: 1px solid rgba(0, 0, 0, 0.1);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
        }
        
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .grid-item {
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            color: #333;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        input[type="text"], 
        input[type="number"], 
        input[type="email"], 
        input[type="tel"],
        input[type="file"], 
        textarea, 
        select {
            width: 100%;
            padding: 12px 15px;
            margin: 8px 0 15px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s;
            background: rgba(255, 255, 255, 0.9);
        }
        
        input:focus, textarea:focus, select:focus {
            border-color: var(--primary-color);
            outline: none;
            box-shadow: 0 0 10px rgba(67, 97, 238, 0.3);
            transform: scale(1.02);
        }
        
        button {
            padding: 12px 25px;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s;
            margin-top: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: 0.5s;
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        button:hover::before {
            left: 100%;
        }
        
        button.secondary {
            background: linear-gradient(135deg, #4cc9f0, #4895ef);
        }
        
        button.warning {
            background: linear-gradient(135deg, #f72585, #b5179e);
        }
        
        img {
            margin-top: 15px;
            width: 150px;
            height: 150px;
            border-radius: 50%;
            border: 5px solid rgba(255, 255, 255, 0.3);
            object-fit: cover;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
        }
        
        img:hover {
            transform: scale(1.05) rotate(5deg);
        }
        
        .result {
            color: var(--success-color);
            font-weight: bold;
        }
        
        .fail {
            color: var(--accent-color);
            font-weight: bold;
        }
        
        .warning {
            color: var(--warning-color);
            font-weight: bold;
        }
        
        .subject {
            background-color: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            border-left: 5px solid var(--primary-color);
            color: #333;
            transition: all 0.3s ease;
        }
        
        .subject:hover {
            transform: translateX(10px);
        }
        
        .feedback {
            padding: 15px;
            background-color: rgba(248, 249, 250, 0.7);
            border-radius: 8px;
            margin-top: 15px;
            font-size: 14px;
            color: #333;
        }
        
        .progress-container {
            background-color: #e0e0e0;
            border-radius: 10px;
            margin: 15px 0;
            height: 20px;
            overflow: hidden;
        }
        
        .progress-bar {
            background: linear-gradient(90deg, #4cc9f0, #4361ee);
            border-radius: 10px;
            height: 100%;
            width: 0%;
            transition: width 1s ease-in-out;
            position: relative;
        }
        
        .progress-bar::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            animation: shine 2s infinite;
        }
        
        @keyframes shine {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }
        
        .notification {
            padding: 15px;
            background: rgba(255, 255, 255, 0.8);
            border-left: 5px solid var(--primary-color);
            margin: 10px 0;
            border-radius: 8px;
            color: #333;
            transition: all 0.3s ease;
        }
        
        .notification:hover {
            transform: translateX(5px);
        }
        
        .activity-card {
            background: rgba(255, 255, 255, 0.8);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            transition: all 0.3s ease;
            color: #333;
        }
        
        .activity-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        .activity-icon {
            font-size: 28px;
            margin-right: 15px;
            color: var(--primary-color);
        }
        
        .teacher-feedback {
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 5px solid var(--primary-color);
            color: #333;
            transition: all 0.3s ease;
        }
        
        .teacher-feedback:hover {
            transform: translateX(5px);
        }
        
        .teacher-name {
            font-weight: bold;
            color: var(--dark-color);
        }
        
        .date {
            font-size: 12px;
            color: #666;
        }
        
        .report-card {
            background: rgba(255, 255, 255, 0.95);
            padding: 30px;
            border-radius: 15px;
            color: #333;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            transform: translateZ(50px);
            display: none;
        }
        
        .report-card h2 {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 30px;
        }
        
        .floating-btn {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            box-shadow: 0 10px 25px rgba(67, 97, 238, 0.5);
            cursor: pointer;
            z-index: 100;
            transition: all 0.3s ease;
        }
        
        .floating-btn:hover {
            transform: translateY(-5px) scale(1.1);
            box-shadow: 0 15px 30px rgba(67, 97, 238, 0.6);
        }
        
        /* 3D Effects */
        .card-3d {
            transform-style: preserve-3d;
            transition: transform 0.5s;
        }
        
        .card-3d:hover {
            transform: rotateY(10deg) rotateX(5deg);
        }
        
        /* Responsive Design */
        @media (max-width: 992px) {
            .main-content {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                margin-bottom: 20px;
            }
            
            .nav-container {
                flex-direction: column;
                align-items: center;
            }
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .grid-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Student Management System</h1>
        
        <div class="nav-container">
            <button class="nav-btn active" data-section="loginSection" 
                    data-preview="Login with student USN to access the system">Login</button>
            <button class="nav-btn" data-section="studentSection" 
                    data-preview="View and manage student personal information">Student Details</button>
            <button class="nav-btn" data-section="contactInfoSection" 
                    data-preview="Manage parent/guardian contact information">Contact Info</button>
            <button class="nav-btn" data-section="behaviorSection" 
                    data-preview="Record and view behavioral feedback">Behavior</button>
            <button class="nav-btn" data-section="goalsSection" 
                    data-preview="Set and track academic goals">Goals</button>
            <button class="nav-btn" data-section="subjectPerformance" 
                    data-preview="View and analyze academic performance">Performance</button>
            <button class="nav-btn" data-section="activitiesSection" 
                    data-preview="Manage extracurricular activities">Activities</button>
            <button class="nav-btn" data-section="remindersSection" 
                    data-preview="Set and view important reminders">Reminders</button>
            <button class="nav-btn" id="generateReportBtn" 
                    data-preview="Generate comprehensive student report">Generate Report</button>
        </div>
        
        <div class="section-preview" id="sectionPreview"></div>
        
        <div class="main-content">
            <div class="content-area card-3d">
                <!-- Login Section -->
                <div id="loginSection" class="section active">
                    <div class="card">
                        <h2>Student Login</h2>
                        <label>Enter USN:</label>
                        <input type="text" id="usnInput" placeholder="e.g. USN001">
                        <button id="loginButton">Login</button>
                        <div id="errorMessage" style="color:var(--accent-color); display:none;"></div>
                    </div>
                </div>
                
                <!-- Student Details Section -->
                <div id="studentSection" class="section">
                    <div class="card">
                        <h2>Student Details</h2>
                        <div class="grid-container">
                            <div class="grid-item">
                                <p><strong>Name:</strong> <span id="studentName"></span></p>
                                <p><strong>USN:</strong> <span id="studentUSN"></span></p>
                                <p><strong>Date of Birth:</strong> <span id="dob"></span></p>
                                <p><strong>Blood Group:</strong> <span id="bloodGroup"></span></p>
                            </div>
                            <div class="grid-item">
                                <p><strong>Father's Name:</strong> <span id="fatherName"></span></p>
                                <p><strong>Mother's Name:</strong> <span id="motherName"></span></p>
                                <p><strong>Class/Grade:</strong> <span id="classGrade"></span></p>
                                <p><strong>Section:</strong> <span id="section"></span></p>
                            </div>
                        </div>
                        <p><strong>Photo:</strong></p>
                        <img id="photoPreview" alt="Student Photo" style="display:none;">
                    </div>
                </div>
                
                <!-- Contact Info Section -->
                <div id="contactInfoSection" class="section">
                    <div class="card">
                        <h2>Parent/Guardian Contact Information</h2>
                        <div class="grid-container">
                            <div class="grid-item">
                                <h3>Father's Contact</h3>
                                <label>Phone Number:</label>
                                <input type="tel" id="fatherPhone" placeholder="+91 XXXXXXXXXX">
                                <label>Email:</label>
                                <input type="email" id="fatherEmail" placeholder="father@example.com">
                            </div>
                            <div class="grid-item">
                                <h3>Mother's Contact</h3>
                                <label>Phone Number:</label>
                                <input type="tel" id="motherPhone" placeholder="+91 XXXXXXXXXX">
                                <label>Email:</label>
                                <input type="email" id="motherEmail" placeholder="mother@example.com">
                            </div>
                            <div class="grid-item">
                                <h3>Guardian's Contact (if applicable)</h3>
                                <label>Name:</label>
                                <input type="text" id="guardianName" placeholder="Guardian's Name">
                                <label>Phone Number:</label>
                                <input type="tel" id="guardianPhone" placeholder="+91 XXXXXXXXXX">
                                <label>Relationship:</label>
                                <input type="text" id="guardianRelation" placeholder="Relationship to student">
                            </div>
                        </div>
                        <button id="saveContactInfo" class="secondary">Save Contact Information</button>
                    </div>
                </div>
                
                <!-- Behavior Section -->
                <div id="behaviorSection" class="section">
                    <div class="card">
                        <h2>Behavioral Feedback</h2>
                        <label>Class Participation:</label>
                        <select id="participationRating">
                            <option value="excellent">Excellent - Always participates</option>
                            <option value="good">Good - Participates often</option>
                            <option value="average">Average - Participates sometimes</option>
                            <option value="poor">Poor - Rarely participates</option>
                        </select>
                        
                        <label>Behavior in Class:</label>
                        <select id="behaviorRating">
                            <option value="excellent">Excellent - Always respectful</option>
                            <option value="good">Good - Usually respectful</option>
                            <option value="average">Average - Occasionally disruptive</option>
                            <option value="poor">Poor - Often disruptive</option>
                        </select>
                        
                        <label>Additional Comments:</label>
                        <textarea id="behaviorComments" rows="4" placeholder="Enter any additional behavioral comments..."></textarea>
                        
                        <button id="saveBehaviorInfo" class="secondary">Save Behavioral Feedback</button>
                    </div>
                </div>
                
                <!-- Goals Section -->
                <div id="goalsSection" class="section">
                    <div class="card">
                        <h2>Goal Setting</h2>
                        <div id="goalsContainer">
                            <div class="goal-item">
                                <label>Goal Title:</label>
                                <input type="text" class="goal-title" placeholder="e.g. Improve Math scores">
                                <label>Goal Description:</label>
                                <textarea class="goal-description" rows="2" placeholder="Describe your goal..."></textarea>
                                <label>Target Date:</label>
                                <input type="date" class="goal-date">
                                <label>Progress:</label>
                                <div class="progress-container">
                                    <div class="progress-bar" style="width: 0%"></div>
                                </div>
                                <input type="range" class="goal-progress" min="0" max="100" value="0">
                                <button class="remove-goal warning">Remove Goal</button>
                            </div>
                        </div>
                        <button id="addGoal" class="secondary">Add Another Goal</button>
                        <button id="saveGoals" class="secondary">Save Goals</button>
                    </div>
                </div>
                
                <!-- Subject Performance Section -->
                <div id="subjectPerformance" class="section">
                    <div class="card">
                        <h2>Subject Performance</h2>
                        
                        <div class="tab-container">
                            <div class="nav-btn tab active" data-tab="current">Current Term</div>
                            <div class="nav-btn tab" data-tab="previous">Previous Terms</div>
                            <div class="nav-btn tab" data-tab="comparison">Progress Comparison</div>
                        </div>
                        
                        <div class="tab-content active" id="current-term">
                            <div class="subject">
                                <h3>Mathematics</h3>
                                <label>Internal Marks (out of 50):</label>
                                <input type="number" class="internalMarks" data-subject="Mathematics">
                                <label>Exam Marks (out of 100):</label>
                                <input type="number" class="examMarks" data-subject="Mathematics">
                                <label>Attendance (%):</label>
                                <input type="number" class="attendance" data-subject="Mathematics">
                                <div class="feedback"></div>
                            </div>
                            <div class="subject">
                                <h3>Chemistry</h3>
                                <label>Internal Marks (out of 50):</label>
                                <input type="number" class="internalMarks" data-subject="Chemistry">
                                <label>Exam Marks (out of 100):</label>
                                <input type="number" class="examMarks" data-subject="Chemistry">
                                <label>Attendance (%):</label>
                                <input type="number" class="attendance" data-subject="Chemistry">
                                <div class="feedback"></div>
                            </div>
                            <div class="subject">
                                <h3>Biology</h3>
                                <label>Internal Marks (out of 50):</label>
                                <input type="number" class="internalMarks" data-subject="Biology">
                                <label>Exam Marks (out of 100):</label>
                                <input type="number" class="examMarks" data-subject="Biology">
                                <label>Attendance (%):</label>
                                <input type="number" class="attendance" data-subject="Biology">
                                <div class="feedback"></div>
                            </div>
                            <div class="subject">
                                <h3>Physics</h3>
                                <label>Internal Marks (out of 50):</label>
                                <input type="number" class="internalMarks" data-subject="Physics">
                                <label>Exam Marks (out of 100):</label>
                                <input type="number" class="examMarks" data-subject="Physics">
                                <label>Attendance (%):</label>
                                <input type="number" class="attendance" data-subject="Physics">
                                <div class="feedback"></div>
                            </div>
                            <div class="subject">
                                <h3>English</h3>
                                <label>Internal Marks (out of 50):</label>
                                <input type="number" class="internalMarks" data-subject="English">
                                <label>Exam Marks (out of 100):</label>
                                <input type="number" class="examMarks" data-subject="English">
                                <label>Attendance (%):</label>
                                <input type="number" class="attendance" data-subject="English">
                                <div class="feedback"></div>
                            </div>
                            <button id="calculatePerformance" class="secondary">Calculate Performance</button>
                        </div>
                        
                        <div class="tab-content" id="previous-terms">
                            <h3>Previous Term Results</h3>
                            <div id="previousResults">
                                <p>No previous term data available yet.</p>
                            </div>
                        </div>
                        
                        <div class="tab-content" id="progress-comparison">
                            <h3>Progress Comparison</h3>
                            <div id="progressChart">
                                <p>Progress comparison chart will appear here after multiple terms of data are available.</p>
                            </div>
                        </div>
                    </div>
                    
                    <div id="overallPerformance" class="card" style="display: none;">
                        <h2>Overall Performance</h2>
                        <div id="results"></div>
                        <div id="overallStatus"></div>
                        
                        <h3>Teacher Feedback</h3>
                        <div id="teacherFeedbackContainer">
                            <div class="teacher-feedback">
                                <div class="teacher-name">Ms. Math Teacher</div>
                                <div class="date">March 15, 2023</div>
                                <p>John has shown great improvement in algebra this term. Needs to work on geometry proofs.</p>
                            </div>
                            <div class="teacher-feedback">
                                <div class="teacher-name">Mr. Science Teacher</div>
                                <div class="date">March 10, 2023</div>
                                <p>Excellent participation in lab experiments. Should focus more on theoretical concepts.</p>
                            </div>
                        </div>
                        
                        <label>Add New Teacher Feedback:</label>
                        <textarea id="newTeacherFeedback" rows="3" placeholder="Enter your feedback..."></textarea>
                        <button id="addTeacherFeedback" class="secondary">Add Feedback</button>
                    </div>
                </div>
                
                <!-- Activities Section -->
                <div id="activitiesSection" class="section">
                    <div class="card">
                        <h2>Extra-Curricular Activities</h2>
                        
                        <h3>Current Activities</h3>
                        <div id="currentActivities">
                            <div class="activity-card">
                                <div class="activity-icon">⚽</div>
                                <div>
                                    <strong>Football Team</strong>
                                    <p>Member of school football team. Practice every Monday and Wednesday.</p>
                                </div>
                            </div>
                            <div class="activity-card">
                                <div class="activity-icon">🎭</div>
                                <div>
                                    <strong>Drama Club</strong>
                                    <p>Participating in school play as lead role. Rehearsals on Fridays.</p>
                                </div>
                            </div>
                        </div>
                        
                        <h3>Add New Activity</h3>
                        <label>Activity Type:</label>
                        <select id="activityType">
                            <option value="sports">Sports</option>
                            <option value="arts">Arts</option>
                            <option value="academic">Academic Club</option>
                            <option value="volunteer">Volunteer Work</option>
                            <option value="other">Other</option>
                        </select>
                        
                        <label>Activity Name:</label>
                        <input type="text" id="activityName" placeholder="e.g. Basketball Team">
                        
                        <label>Description:</label>
                        <textarea id="activityDescription" rows="3" placeholder="Describe the activity..."></textarea>
                        
                        <label>Time Commitment:</label>
                        <input type="text" id="activityTime" placeholder="e.g. 2 hours/week">
                        
                        <button id="addActivity" class="secondary">Add Activity</button>
                        
                        <h3>Scholarship Information</h3>
                        <div id="scholarshipInfo">
                            <p><strong>Merit Scholarship</strong> - Awarded for academic excellence, 2022-2023</p>
                            <p><strong>Sports Scholarship</strong> - Awarded for state-level football performance, 2023</p>
                        </div>
                        
                        <label>Add New Scholarship/Award:</label>
                        <input type="text" id="newScholarshipName" placeholder="Scholarship/Award Name">
                        <textarea id="newScholarshipDetails" rows="2" placeholder="Details about the scholarship/award..."></textarea>
                        <button id="addScholarship" class="secondary">Add Scholarship</button>
                    </div>
                </div>
                
                <!-- Reminders Section -->
                <div id="remindersSection" class="section">
                    <div class="card">
                        <h2>Reminders & Notifications</h2>
                        
                        <h3>Upcoming Events</h3>
                        <div class="notification">
                            <strong>Math Final Exam</strong> - May 15, 2023
                        </div>
                        <div class="notification">
                            <strong>Science Project Deadline</strong> - May 20, 2023
                        </div>
                        <div class="notification">
                            <strong>Parent-Teacher Meeting</strong> - May 25, 2023
                        </div>
                        
                        <h3>Add New Reminder</h3>
                        <label>Reminder Title:</label>
                        <input type="text" id="reminderTitle" placeholder="e.g. Submit English Essay">
                        
                        <label>Date:</label>
                        <input type="date" id="reminderDate">
                        
                        <label>Details:</label>
                        <textarea id="reminderDetails" rows="2" placeholder="Additional details..."></textarea>
                        
                        <button id="addReminder" class="secondary">Add Reminder</button>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Report Card (hidden initially) -->
        <div id="reportCard" class="report-card">
            <h2>Student Report Card</h2>
            <div id="reportCardDetails"></div>
            <button id="printReport" class="secondary">Print Report Card</button>
        </div>
    </div>
    
    <!-- Floating action button -->
    <div class="floating-btn" id="scrollToTop">↑</div>

    <script>
        // Enhanced student data with more fields
        const students = {
            "USN001": { 
                name: "John Doe", 
                usn: "USN001",
                father: "Michael Doe", 
                mother: "Sarah Doe", 
                bloodGroup: "A+", 
                photo: "https://randomuser.me/api/portraits/men/1.jpg",
                dob: "2005-03-15",
                classGrade: "10",
                section: "A",
                fatherPhone: "+919876543210",
                fatherEmail: "michael.doe@example.com",
                motherPhone: "+919876543211",
                motherEmail: "sarah.doe@example.com"
            },
            "USN002": { 
                name: "Jane Smith", 
                usn: "USN002",
                father: "James Smith", 
                mother: "Laura Smith", 
                bloodGroup: "B+", 
                photo: "https://randomuser.me/api/portraits/women/2.jpg",
                dob: "2005-05-20",
                classGrade: "10",
                section: "B",
                fatherPhone: "+919876543212",
                fatherEmail: "james.smith@example.com",
                motherPhone: "+919876543213",
                motherEmail: "laura.smith@example.com"
            },
            "USN003": { 
                name: "Alice Johnson", 
                usn: "USN003",
                father: "Robert Johnson", 
                mother: "Linda Johnson", 
                bloodGroup: "O-", 
                photo: "https://randomuser.me/api/portraits/women/3.jpg",
                dob: "2005-07-10",
                classGrade: "9",
                section: "A",
                fatherPhone: "+919876543214",
                fatherEmail: "robert.johnson@example.com",
                motherPhone: "+919876543215",
                motherEmail: "linda.johnson@example.com"
            }
        };

        // Navigation functionality with hover preview
        document.querySelectorAll('.nav-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                if (this.id === 'generateReportBtn') {
                    generateReport();
                    return;
                }
                
                // Remove active class from all buttons and sections
                document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
                document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
                
                // Add active class to clicked button and corresponding section
                this.classList.add('active');
                const sectionId = this.getAttribute('data-section');
                document.getElementById(sectionId).classList.add('active');
                
                // Scroll to top of the section
                document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
            });

            // Hover preview functionality
            btn.addEventListener('mouseenter', function() {
                const preview = document.getElementById('sectionPreview');
                preview.textContent = this.getAttribute('data-preview');
                preview.style.display = 'block';
                
                const rect = this.getBoundingClientRect();
                preview.style.top = `${rect.bottom + window.scrollY + 5}px`;
                preview.style.left = `${rect.left + window.scrollX}px`;
            });

            btn.addEventListener('mouseleave', function() {
                document.getElementById('sectionPreview').style.display = 'none';
            });
        });

        // Login functionality
        document.getElementById('loginButton').addEventListener('click', function() {
            const usn = document.getElementById('usnInput').value.toUpperCase();
            const student = students[usn];

            if (student) {
                // Basic student info
                document.getElementById('studentName').textContent = student.name;
                document.getElementById('studentUSN').textContent = student.usn;
                document.getElementById('fatherName').textContent = student.father;
                document.getElementById('motherName').textContent = student.mother;
                document.getElementById('bloodGroup').textContent = student.bloodGroup;
                document.getElementById('photoPreview').src = student.photo;
                document.getElementById('photoPreview').style.display = 'block';
                document.getElementById('dob').textContent = student.dob;
                document.getElementById('classGrade').textContent = student.classGrade;
                document.getElementById('section').textContent = student.section;
                
                // Contact info
                document.getElementById('fatherPhone').value = student.fatherPhone || '';
                document.getElementById('fatherEmail').value = student.fatherEmail || '';
                document.getElementById('motherPhone').value = student.motherPhone || '';
                document.getElementById('motherEmail').value = student.motherEmail || '';

                // Navigate to student details section
                document.querySelector('.nav-btn[data-section="studentSection"]').click();
            } else {
                document.getElementById('errorMessage').textContent = "Student not found! Please check your USN.";
                document.getElementById('errorMessage').style.display = 'block';
            }
        });

        // Goal management
        document.getElementById('addGoal').addEventListener('click', function() {
            const goalItem = document.createElement('div');
            goalItem.className = 'goal-item';
            goalItem.innerHTML = `
                <label>Goal Title:</label>
                <input type="text" class="goal-title" placeholder="e.g. Improve Math scores">
                <label>Goal Description:</label>
                <textarea class="goal-description" rows="2" placeholder="Describe your goal..."></textarea>
                <label>Target Date:</label>
                <input type="date" class="goal-date">
                <label>Progress:</label>
                <div class="progress-container">
                    <div class="progress-bar" style="width: 0%"></div>
                </div>
                <input type="range" class="goal-progress" min="0" max="100" value="0">
                <button class="remove-goal warning">Remove Goal</button>
            `;
            document.getElementById('goalsContainer').appendChild(goalItem);
            
            // Add event listener for the progress slider
            goalItem.querySelector('.goal-progress').addEventListener('input', function() {
                const progress = this.value;
                this.previousElementSibling.querySelector('.progress-bar').style.width = progress + '%';
            });
            
            // Add event listener for remove button
            goalItem.querySelector('.remove-goal').addEventListener('click', function() {
                goalItem.remove();
            });
        });

        // Calculate performance
        document.getElementById('calculatePerformance').addEventListener('click', function() {
            const subjects = document.querySelectorAll('.subject');
            let overallResults = '';
            let attendanceWarning = false;
            let failWarning = false;

            subjects.forEach(subject => {
                const subjectName = subject.querySelector('h3').innerText;
                const internalMarks = parseInt(subject.querySelector('.internalMarks').value) || 0;
                const examMarks = parseInt(subject.querySelector('.examMarks').value) || 0;
                const attendance = parseInt(subject.querySelector('.attendance').value) || 0;
                const feedbackDiv = subject.querySelector('.feedback');
                
                // Calculate total marks (internal + exam converted to 50)
                const totalMarks = internalMarks + (examMarks / 2);
                const percentage = (totalMarks / 100) * 100;
                
                // Feedback for Internal Marks
                let feedback = '';
                if (internalMarks < 20) {
                    feedback = 'Internal Marks: <span class="fail">Needs significant improvement</span>';
                } else if (internalMarks < 40) {
                    feedback = 'Internal Marks: <span class="warning">Needs improvement</span>';
                } else {
                    feedback = 'Internal Marks: <span class="result">Excellent</span>';
                }

                // Feedback for Exam Marks
                if (examMarks < 35) {
                    feedback += '<br>Exam Marks: <span class="fail">Failed - Needs remedial classes</span>';
                    failWarning = true;
                } else if (examMarks < 60) {
                    feedback += '<br>Exam Marks: <span class="warning">Passed but needs improvement</span>';
                } else if (examMarks < 90) {
                    feedback += '<br>Exam Marks: <span class="result">Good performance</span>';
                } else {
                    feedback += '<br>Exam Marks: <span class="result">Outstanding performance</span>';
                }

                // Attendance Warning
                if (attendance < 75) {
                    feedback += '<br><span class="warning">Warning: Attendance is below 75%</span>';
                    attendanceWarning = true;
                } else if (attendance < 90) {
                    feedback += '<br><span class="result">Attendance: Satisfactory</span>';
                } else {
                    feedback += '<br><span class="result">Attendance: Excellent</span>';
                }
                
                // Overall subject status
                if (percentage < 40) {
                    feedback += '<br><strong>Overall: <span class="fail">Fail</span></strong>';
                } else if (percentage < 60) {
                    feedback += '<br><strong>Overall: <span class="warning">Pass</span></strong>';
                } else if (percentage < 80) {
                    feedback += '<br><strong>Overall: <span class="result">Good</span></strong>';
                } else {
                    feedback += '<br><strong>Overall: <span class="result">Excellent</span></strong>';
                }

                feedbackDiv.innerHTML = feedback;
                
                overallResults += `
                    <div class="subject">
                        <h3>${subjectName}</h3>
                        <p>Internal: ${internalMarks}/50 | Exam: ${examMarks}/100 | Total: ${totalMarks.toFixed(1)}/100 (${percentage.toFixed(1)}%)</p>
                        <p>Attendance: ${attendance}%</p>
                    </div>
                `;
            });

            document.getElementById('results').innerHTML = overallResults;
            document.getElementById('overallPerformance').style.display = 'block';

            let overallStatus = '';
            if (failWarning) {
                overallStatus = '<div class="fail"><h3>Overall Status: Warning</h3><p>Student has failed in one or more subjects. Remedial action required.</p></div>';
            } else if (attendanceWarning) {
                overallStatus = '<div class="warning"><h3>Overall Status: Satisfactory with Concerns</h3><p>Attendance is below 75% in one or more subjects.</p></div>';
            } else {
                overallStatus = '<div class="result"><h3>Overall Status: Good</h3><p>Student is performing well in all subjects.</p></div>';
            }
            
            document.getElementById('overallStatus').innerHTML = overallStatus;
        });

        // Teacher feedback
        document.getElementById('addTeacherFeedback').addEventListener('click', function() {
            const feedback = document.getElementById('newTeacherFeedback').value;
            if (feedback.trim() === '') return;
            
            const feedbackDiv = document.createElement('div');
            feedbackDiv.className = 'teacher-feedback';
            feedbackDiv.innerHTML = `
                <div class="teacher-name">Teacher</div>
                <div class="date">${new Date().toLocaleDateString()}</div>
                <p>${feedback}</p>
            `;
            
            document.getElementById('teacherFeedbackContainer').prepend(feedbackDiv);
            document.getElementById('newTeacherFeedback').value = '';
        });

        // Activities management
        document.getElementById('addActivity').addEventListener('click', function() {
            const type = document.getElementById('activityType').value;
            const name = document.getElementById('activityName').value;
            const description = document.getElementById('activityDescription').value;
            const time = document.getElementById('activityTime').value;
            
            if (!name.trim()) return;
            
            const icons = {
                'sports': '⚽',
                'arts': '🎨',
                'academic': '📚',
                'volunteer': '🤝',
                'other': '🌟'
            };
            
            const activityCard = document.createElement('div');
            activityCard.className = 'activity-card';
            activityCard.innerHTML = `
                <div class="activity-icon">${icons[type]}</div>
                <div>
                    <strong>${name}</strong>
                    <p>${description || 'No description provided'}</p>
                    ${time ? `<small>Time: ${time}</small>` : ''}
                </div>
            `;
            
            document.getElementById('currentActivities').appendChild(activityCard);
            
            // Clear form
            document.getElementById('activityName').value = '';
            document.getElementById('activityDescription').value = '';
            document.getElementById('activityTime').value = '';
        });

        // Scholarship management
        document.getElementById('addScholarship').addEventListener('click', function() {
            const name = document.getElementById('newScholarshipName').value;
            const details = document.getElementById('newScholarshipDetails').value;
            
            if (!name.trim()) return;
            
            const scholarshipItem = document.createElement('p');
            scholarshipItem.innerHTML = `<strong>${name}</strong> - ${details || 'No details provided'}`;
            document.getElementById('scholarshipInfo').appendChild(scholarshipItem);
            
            // Clear form
            document.getElementById('newScholarshipName').value = '';
            document.getElementById('newScholarshipDetails').value = '';
        });

        // Reminders management
        document.getElementById('addReminder').addEventListener('click', function() {
            const title = document.getElementById('reminderTitle').value;
            const date = document.getElementById('reminderDate').value;
            const details = document.getElementById('reminderDetails').value;
            
            if (!title.trim() || !date) return;
            
            const reminderDiv = document.createElement('div');
            reminderDiv.className = 'notification';
            reminderDiv.innerHTML = `
                <strong>${title}</strong> - ${new Date(date).toLocaleDateString()}
                ${details ? `<p>${details}</p>` : ''}
            `;
            
            document.querySelector('#remindersSection .notification:last-of-type').after(reminderDiv);
            
            // Clear form
            document.getElementById('reminderTitle').value = '';
            document.getElementById('reminderDate').value = '';
            document.getElementById('reminderDetails').value = '';
        });

        // Generate report card
        function generateReport() {
            const reportCardDetails = `
                <div class="grid-container">
                    <div class="grid-item">
                        <h3>Student Information</h3>
                        <p><strong>Name:</strong> ${document.getElementById('studentName').textContent}</p>
                        <p><strong>USN:</strong> ${document.getElementById('studentUSN').textContent}</p>
                        <p><strong>Class:</strong> ${document.getElementById('classGrade').textContent} ${document.getElementById('section').textContent}</p>
                        <p><strong>Blood Group:</strong> ${document.getElementById('bloodGroup').textContent}</p>
                        <img src="${document.getElementById('photoPreview').src}" alt="Student Photo" style="width:120px;height:120px;">
                    </div>
                    <div class="grid-item">
                        <h3>Parent Information</h3>
                        <p><strong>Father:</strong> ${document.getElementById('fatherName').textContent}</p>
                        <p><strong>Phone:</strong> ${document.getElementById('fatherPhone').value || 'N/A'}</p>
                        <p><strong>Mother:</strong> ${document.getElementById('motherName').textContent}</p>
                        <p><strong>Phone:</strong> ${document.getElementById('motherPhone').value || 'N/A'}</p>
                    </div>
                </div>
                
                <h3>Academic Performance</h3>
                ${document.getElementById('results').innerHTML}
                
                <h3>Overall Status</h3>
                ${document.getElementById('overallStatus').innerHTML}
                
                <h3>Teacher Feedback</h3>
                ${document.getElementById('teacherFeedbackContainer').innerHTML}
                
                <h3>Activities & Achievements</h3>
                <div class="grid-container">
                    <div class="grid-item">
                        <h4>Extra-Curricular Activities</h4>
                        ${document.getElementById('currentActivities').innerHTML}
                    </div>
                    <div class="grid-item">
                        <h4>Scholarships & Awards</h4>
                        ${document.getElementById('scholarshipInfo').innerHTML}
                    </div>
                </div>
                
                <h3>Behavioral Feedback</h3>
                <p><strong>Class Participation:</strong> ${document.getElementById('participationRating').options[document.getElementById('participationRating').selectedIndex].text}</p>
                <p><strong>Behavior in Class:</strong> ${document.getElementById('behaviorRating').options[document.getElementById('behaviorRating').selectedIndex].text}</p>
                <p><strong>Additional Comments:</strong> ${document.getElementById('behaviorComments').value || 'None'}</p>
                
                <h3>Goals</h3>
                ${document.getElementById('goalsContainer').innerHTML}
                
                <h3>Upcoming Reminders</h3>
                ${document.querySelector('#remindersSection').querySelectorAll('.notification').length > 0 ? 
                  document.querySelector('#remindersSection').innerHTML : '<p>No upcoming reminders</p>'}
            `;
            
            document.getElementById('reportCardDetails').innerHTML = reportCardDetails;
            document.getElementById('reportCard').style.display = 'block';
            
            // Scroll to report card
            document.getElementById('reportCard').scrollIntoView({ behavior: 'smooth' });
        }

        // Print report card
        document.getElementById('printReport').addEventListener('click', function() {
            const printContents = document.getElementById('reportCard').innerHTML;
            const originalContents = document.body.innerHTML;
            
            document.body.innerHTML = `
                <style>
                    body { font-family: Arial; padding: 20px; }
                    h1, h2, h3 { color: #333; }
                    .result { color: green; }
                    .fail { color: red; }
                    .warning { color: orange; }
                    .grid-container { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
                    img { width: 120px; height: 120px; border-radius: 8px; }
                    .subject, .teacher-feedback, .activity-card { 
                        border: 1px solid #ddd; 
                        padding: 10px; 
                        margin-bottom: 10px; 
                        border-radius: 5px; 
                    }
                    @page { size: auto; margin: 10mm; }
                </style>
                ${printContents}
            `;
            
            window.print();
            document.body.innerHTML = originalContents;
            window.location.reload();
        });

        // Initialize goal progress sliders
        document.querySelectorAll('.goal-progress').forEach(slider => {
            slider.addEventListener('input', function() {
                this.previousElementSibling.querySelector('.progress-bar').style.width = this.value + '%';
            });
        });

        // Initialize tab functionality
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', function() {
                document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                
                this.classList.add('active');
                const tabId = this.getAttribute('data-tab');
                document.getElementById(tabId === 'current' ? 'current-term' : 
                                      tabId === 'previous' ? 'previous-terms' : 'progress-comparison').classList.add('active');
            });
        });

        // Scroll to top button
        document.getElementById('scrollToTop').addEventListener('click', function() {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });

        // Show/hide scroll to top button
        window.addEventListener('scroll', function() {
            const scrollBtn = document.getElementById('scrollToTop');
            if (window.pageYOffset > 300) {
                scrollBtn.style.display = 'flex';
            } else {
                scrollBtn.style.display = 'none';
            }
        });

        // Save contact information
        document.getElementById('saveContactInfo').addEventListener('click', function() {
            alert('Contact information saved successfully!');
        });

        // Save behavior information
        document.getElementById('saveBehaviorInfo').addEventListener('click', function() {
            alert('Behavioral feedback saved successfully!');
        });

        // Save goals
        document.getElementById('saveGoals').addEventListener('click', function() {
            alert('Goals saved successfully!');
        });
    </script>
</body>
</html> in this code add in login page student login and teacher login both and print buttons is not working fix that
