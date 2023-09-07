<script>
    import Login from './Login.svelte';
    // import Input  from './Input.svelte'
	/* export let name; */
	
	// [ADMIN LOGIN] Function for handling admin login
async function handleAdminLogin() {
  try {
    const { data, error } = await supabase
      .from('users') // Replace 'user_table' with your actual table name
      .select('*')
      .eq('username', providedUsername); // Replace 'username' with your column name

    if (error) {
      console.error('Database error:', error.message);
      return; // Return early if there's an error
    }

    if (data && data.length > 0) {
      const user = data[0];
      const storedPassword = user.password; // Retrieve the hashed and salted password
      const passwordMatches = await comparePasswords(providedPassword, storedPassword);

      if (passwordMatches && user.role === 'Admin') {
        // Password matches, user is an admin
        // Proceed with admin authentication logic
      } else {
        console.error('Admin credentials are not valid.');
      }
    } else {
      console.error('Admin not found.');
    }
  } catch (error) {
    console.error('Error:', error.message);
  }
}


// [USER LOGIN] Function for handling user login
async function handleUserLogin() {
  try {
    const { data, error } = await supabase
      .from('users') // Replace 'user_table' with your actual table name
      .select('*')
      .eq('username', providedUsername); // Replace 'username' with your column name

    if (error) {
      console.error('Database error:', error.message);
      return; // Return early if there's an error
    }

    if (data && data.length > 0) {
      const user = data[0];
      const storedPassword = user.password; // Retrieve the hashed and salted password
      const passwordMatches = await comparePasswords(providedPassword, storedPassword);

      if (passwordMatches && user.role === 'User') {
        // Password matches, user is authenticated
        const userRole = user.role; // Retrieve the user's role
        // Proceed with user authentication logic based on the role
      } else {
        console.error('Password does not match or user is not a User.');
      }
    } else {
      console.error('User not found.');
    }
  } catch (error) {
    console.error('Error:', error.message);
  }
}


	// Function to determine which login logic to execute based on user type
	async function handleLogin() {
		// Determine the user type (e.g., 'Admin' or 'User') based on your logic
		const userType = 'Admin'; // Replace with your logic to determine the user type

		if (userType === 'Admin') {
		await handleAdminLogin();
		} else if (userType === 'User') {
		await handleUserLogin();
		} else {
		console.error('Invalid user type.');
		}
	}

	// Call the handleLogin function when a login action occurs (e.g., button click)
	async function handleLoginButtonClick() {
		await handleLogin();
	}
	</script>

	<!-- Your HTML content here -->

	<button on:click={handleLoginButtonClick}>Log In</button>



<main>
	<h1>Kangan Quiz</h1>
    <Login />
	
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>