<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login and Register</title>
</head>
<body>
    <h2>Login</h2>
    <form action="process.php" method="post">
        <input type="hidden" name="action" value="login">
        
        <label for="login_username">Username:</label>
        <input type="text" id="login_username" name="username" required><br><br>

        <label for="login_password">Password:</label>
        <input type="password" id="login_password" name="password" required><br><br>

        <label for="license_key">License Key:</label>
        <input type="text" id="license_key" name="license_key" required><br><br>

        <input type="submit" value="Login">
    </form>

    <h2>Register</h2>
    <form action="process.php" method="post">
        <input type="hidden" name="action" value="register">

        <label for="reg_username">Username:</label>
        <input type="text" id="reg_username" name="username" required><br><br>

        <label for="reg_password">Password:</label>
        <input type="password" id="reg_password" name="password" required><br><br>

        <input type="submit" value="Register">
    </form>
</body>
</html>
