<script>
//ADMIN LOGIN
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

  if (passwordMatches && user.role === 'Admin') {
    // Password matches, user is an admin
    // Proceed with admin authentication logic
  } else {
    console.error('Admin credentials are not valid.');
  }
} else {
  console.error('Admin not found.');
}

</script>