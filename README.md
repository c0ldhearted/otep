<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Joseph Academy - Login/Register</title>
    <link rel="stylesheet" href="c:\Users\josep\OneDrive\Desktop\New folder (2)\cssdesign.css"> <!-- Link to an external CSS file for styles -->
</head>
<body>

<!-- Background Image -->
<div class="background-image" style="background-image: url('https://nacwl.com/wp-content/uploads/2022/04/fareham-academy-006.jpg');">
    <div class="overlay">
        <h1>Welcome to Joseph Academy</h1>
    </div>
</div>

<!-- Login/Register Section -->
<div class="auth-container">
    <div class="auth-forms">
        <!-- Register Form -->
        <form id="registerForm" class="form">
            <h2>Register an Account</h2>
            <input type="text" name="name" placeholder="Full Name" required>
            <input type="text" name="studentId" placeholder="Student ID" required>
            <input type="email" name="email" placeholder="Email" required>
            <input type="password" name="password" placeholder="Password" required>
            <input type="password" name="confirmPassword" placeholder="Confirm Password" required>
            <button type="submit">Register</button>
        </form>

        <!-- Registration Success Message -->
        <p id="registrationSuccess" style="display: none; color: green; text-align: center;">
            Registered successfully! Please log in.
        </p>

        <!-- Login Form -->
        <form id="loginForm" class="form" style="display: none;">
            <h2>Login</h2>
            <input type="email" name="email" placeholder="Email" required>
            <input type="password" name="password" placeholder="Password" required>
            <button type="submit">Login</button>
            <p><a href="#" onclick="forgotPassword()">Forgot Password?</a></p>
            <p id="loginError" class="error-message" style="display: none;">Incorrect details, please try again.</p>
        </form>
    </div>
</div>

<!-- Login Success Message -->
<div id="loginSuccess" style="display: none; text-align: center; color: green; margin-top: 10px;">
    Successfully logged in! Redirecting to your dashboard...
</div>

<script>
    // Registration Form Submission
    document.getElementById('registerForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const name = event.target.name.value;
        const studentId = event.target.studentId.value;
        const email = event.target.email.value;
        const password = event.target.password.value;

        // Store user data in localStorage
        localStorage.setItem('registeredName', name);
        localStorage.setItem('registeredStudentId', studentId);
        localStorage.setItem('registeredEmail', email);
        localStorage.setItem('registeredPassword', password);

        document.getElementById('registrationSuccess').style.display = 'block';
        setTimeout(function() {
            document.getElementById('registrationSuccess').style.display = 'none';
            document.getElementById('registerForm').style.display = 'none';
            document.getElementById('loginForm').style.display = 'block';
        }, 2000); // Show success message for 2 seconds before showing the login form
    });

    // Login Form Submission
    document.getElementById('loginForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const email = event.target.email.value;
        const password = event.target.password.value;

        // Retrieve stored data
        const storedEmail = localStorage.getItem('registeredEmail');
        const storedPassword = localStorage.getItem('registeredPassword');

        // Validate email and password
        if (email === storedEmail && password === storedPassword) {
            document.getElementById('loginError').style.display = 'none';
            // Show login success message
            const successMessage = document.getElementById('loginSuccess');
            successMessage.style.display = 'block';

            // Redirect to the dashboard after 2 seconds
            setTimeout(function() {
                successMessage.style.display = 'none';
                window.location.href = 'otepdashboard.html'; // Redirect to the dashboard page
            }, 2000);
        } else {
            document.getElementById('loginError').style.display = 'block';
        }
    });

    // Forgot Password Placeholder Function
    function forgotPassword() {
        alert('Password reset instructions sent to your email.');
    }
</script>

</body>
</html>
