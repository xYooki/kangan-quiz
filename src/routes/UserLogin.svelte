<script> 
//USER LOGIN
const { data, error } = await supabase
  .from('users') // Replace 'user_table' with your actual table name
  .select('*')
  .eq('username', providedUsername); // Replace 'username' with your column name

if (error) {
  console.error('Database error:', error.message);
} else if (data && data.length > 0) {
  const user = data[0];
  const storedPassword = user.password; // Retrieve the hashed and salted password
  const passwordMatches = await comparePasswords(providedPassword, storedPassword);

  if (passwordMatches && user.role === 'User') {
    // Password matches, user is authenticated
    const userRole = user.role; // Retrieve the user's role
    // Proceed with user authentication logic based on the role
  } else {
    console.error('Password does not match.');
  }
} else {
  console.error('User not found.');
}
</script>
 