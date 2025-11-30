<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KL University Peer Collaboration Portal - Unified Access</title>
    
    <style>
        /* A. Global Reset & Layout */
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 0; background-color: #f7f7f7; color: #333; display: flex; justify-content: center; align-items: center; min-height: 100vh; }
        .container { background: white; padding: 40px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); width: 400px; text-align: center; }
        
        /* B. Red/White Theming */
        :root { --primary-red: #cc0000; --light-red: #fffafa; --dark-red: #990000; }
        h1, h2, h3 { color: var(--primary-red); }
        .header { background-color: var(--primary-red); color: white; padding: 15px 30px; display: flex; justify-content: space-between; align-items: center; width: 100%; position: fixed; top: 0; left: 0; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); z-index: 1000; }
        
        .btn-primary { background-color: var(--primary-red); color: white; padding: 12px 20px; border: none; border-radius: 4px; cursor: pointer; width: 90%; margin-top: 15px; transition: background-color 0.3s; }
        .btn-primary:hover { background-color: var(--dark-red); }

        /* C. Inputs and Elements */
        input[type="text"], input[type="password"], select { width: 90%; padding: 12px; margin: 10px 0; border: 1px solid #ddd; border-left: 5px solid var(--primary-red); border-radius: 4px; box-sizing: border-box; }
        .dashboard { max-width: 1000px; width: 100%; margin: 80px auto 20px auto; padding: 20px; background-color: white; border-radius: 8px; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05); text-align: left; }
        
        .feature-list a { display: block; padding: 10px; margin-bottom: 5px; background: var(--light-red); border-left: 3px solid var(--primary-red); text-decoration: none; color: #333; border-radius: 4px; }
        .feature-list a:hover { background: #ffe0e0; }
        
        .chat-box { border: 1px solid #ddd; padding: 15px; background: #fff; max-height: 150px; overflow-y: scroll; margin-top: 10px; border-radius: 4px; }
        .chat-box p { margin: 5px 0; }

        table { width: 100%; border-collapse: collapse; margin-top: 15px; }`
        th, td { border: 1px solid #eee; padding: 10px; text-align: left; }
        th { background-color: var(--light-red); color: var(--primary-red); }
        .status-submitted { color: green; font-weight: bold; }
        .status-pending { color: orange; font-weight: bold; }
    </style>
</head>
<body>

    <div id="login-view" class="container">
        <h1>🔒 KL Collaboration Portal Login</h1>
        
        <input type="text" id="user-id" placeholder="Registration ID: 2400032139">
        <input type="password" id="password" placeholder="Password: 123">
        
        <select id="role-select">
            <option value="student">Student</option>
            <option value="teacher">Faculty/Teacher</option>
        </select>
        
        <button class="btn-primary" onclick="handleLogin()">Log In</button>
        <p id="error-message" style="color: var(--primary-red); margin-top: 10px;"></p>
        
        <div style="margin-top: 15px; font-size: 0.85em; color: #666;">
            <p>Demo: Both roles use ID: **2400032139** | Pass: **123**</p>
        </div>
    </div>

    <header class="header" id="app-header" style="display: none;">
        <h1 style="color: white; margin: 0;">KL Collab Portal</h1>
        <button onclick="handleLogout()" style="background: none; border: 1px solid white; color: white; padding: 5px 10px; border-radius: 4px; cursor: pointer;">Logout</button>
    </header>

    <div id="teacher-dashboard" class="dashboard" style="display: none;">
        <h1>👨‍🏫 Faculty Dashboard</h1>
        <h2>Welcome, <span id="teacher-name">Faculty!</span></h2>
        <p>Manage your courses, assignments, and collaboration groups.</p>
        
        <div class="feature-list" style="margin-top: 20px;">
            <a href="javascript:void(0)">📝 Create New Collaboration Project</a>
            <a href="javascript:void(0)">📚 Grade Submissions</a>
            <a href="javascript:void(0)">👥 View Student Profiles</a>
            <a href="javascript:void(0)">🗓️ Update Course Schedule</a>
        </div>

        <h3 style="margin-top: 30px;">Pending Review</h3>
        <ul id="pending-review-list" style="list-style: none; padding: 0;">
            <li style="padding: 10px; border-bottom: 1px solid #ddd;">CSE 301 Project - Team Alpha</li>
            <li style="padding: 10px; border-bottom: 1px solid #ddd;">ENG 102 Technical Report Draft</li>
        </ul>
    </div>

    <div id="student-portal" class="dashboard" style="display: none;">
        
        <h1>🧑‍🎓 Student Academic Portal - KL University</h1>
        <h2>Hello, <span id="student-name">Student!</span></h2>
        
        <h3 style="margin-top: 20px;">Active Projects & Collaboration</h3>
        <div style="border: 1px solid #cc0000; padding: 15px; border-radius: 6px; background-color: var(--light-red);">
            <h4>CSE 301: Advanced Data Structures Project</h4>
            <p style="margin: 5px 0;">**Group:** Team Phoenix | **Due:** Nov 30, 2025</p>
            <a href="javascript:void(0)" style="color: var(--primary-red); font-weight: bold;">View Project Details →</a>
            
            <h4 style="margin-top: 15px;">Group Chat (Simulated)</h4>
            <div class="chat-box">
                <p><strong>Alice:</strong> Did everyone finish the hash table implementation?</p>
                <p style="color: orange;"><strong>Bob:</strong> Almost, I'm stuck on collision resolution. Need help!</p>
            </div>
            <textarea id="chat-input" placeholder="Type your message..." style="width: 90%; height: 40px; margin-top: 10px;"></textarea>
            <button class="btn-primary" style="width: 90%; margin-top: 5px;">Send</button>
        </div>

        <h3 style="margin-top: 30px;">Assignment Status Tracker</h3>
        <table>
            <thead>
                <tr>
                    <th>Course Code</th>
                    <th>Assignment Title</th>
                    <th>Due Date</th>
                    <th>Status</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>CSE 205</td>
                    <td>Mid-Term Case Study</td>
                    <td>Oct 20, 2025</td>
                    <td class="status-submitted">Submitted</td>
                </tr>
                <tr>
                    <td>ENG 102</td>
                    <td>Technical Report Draft</td>
                    <td>Nov 15, 2025</td>
                    <td class="status-pending">Pending</td>
                </tr>
            </tbody>
        </table>

        <h3 style="margin-top: 30px;">Quick Actions & Resources</h3>
        <div style="display: flex; gap: 20px; flex-wrap: wrap;">
             <a href="javascript:void(0)" style="color: var(--primary-red);">⚙️ Update Profile Information</a>
             <a href="javascript:void(0)" style="color: var(--primary-red);">📧 Contact Course Coordinator</a>
             <a href="javascript:void(0)" style="color: var(--primary-red);">📚 Syllabus: Advanced Algorithms</a>
             <a href="javascript:void(0)" style="color: var(--primary-red);">📄 Lecture Notes: Week 10 (OS)</a>
        </div>
    </div>


    <script>
        // --- Simulated Database (The JavaScript "Back-End") ---
        const USERS = {
            // Updated to use the same ID for both, internally differentiated by role suffix
            '2400033240-teacher': { id: 1, name: 'Faculty Admin', role: 'teacher', pass: '240' },
            '2400032139-student': { id: 2, name: 'Student Collab', role: 'student', pass: '123' },
            '2400031118-student': { id: 2, name: 'Student Collab', role: 'student', pass: '118' },
        };

        let currentUser = null;

        function handleLogin() {
            const userId = document.getElementById('user-id').value.trim();
            const password = document.getElementById('password').value.trim();
            const selectedRole = document.getElementById('role-select').value;
            const errorMessage = document.getElementById('error-message');
            
            // Construct the unique key based on the selected role
            const userKey = `${userId}-${selectedRole}`;
            const user = USERS[userKey];

            // --- CORE BACK-END VALIDATION LOGIC ---
            if (!user) {
                errorMessage.textContent = '❌ Invalid credentials or incorrect role selected.';
                return;
            }

            if (user.pass !== password) {
                errorMessage.textContent = '❌ Invalid credentials: Password incorrect.';
                return;
            }
            // (Role check is already built into the userKey, so it's guaranteed to match the selected role)
            // ------------------------------------

            // Authentication successful
            currentUser = user;
            errorMessage.textContent = '';
            
            // 1. Hide Login and Show Header
            document.getElementById('login-view').style.display = 'none';
            document.getElementById('app-header').style.display = 'flex';
            
            // 2. Display the correct dashboard based on role
            if (currentUser.role === 'teacher') {
                document.getElementById('teacher-dashboard').style.display = 'block';
                document.getElementById('student-portal').style.display = 'none';
                document.getElementById('teacher-name').textContent = currentUser.name;
            } else {
                document.getElementById('teacher-dashboard').style.display = 'none';
                document.getElementById('student-portal').style.display = 'block';
                document.getElementById('student-name').textContent = currentUser.name;
            }
            
            // Adjust body layout for the dashboard view
            document.body.style.justifyContent = 'flex-start';
            document.body.style.alignItems = 'flex-start';
        }

        function handleLogout() {
            currentUser = null;
            
            // Reset to login view
            document.getElementById('app-header').style.display = 'none';
            document.getElementById('teacher-dashboard').style.display = 'none';
            document.getElementById('student-portal').style.display = 'none';
            document.getElementById('login-view').style.display = 'block';

            // Reset input fields
            document.getElementById('user-id').value = '';
            document.getElementById('password').value = '';

            // Adjust body layout for centering
            document.body.style.justifyContent = 'center';
            document.body.style.alignItems = 'center';
        }

    </script>
</body>
</html>
