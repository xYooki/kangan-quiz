<!-- GitHubSignIn.svelte -->

<script>
    async function signInWithGitHub() {
      // Use Supabase's authentication to initiate GitHub OAuth sign-in
      const { user, error } = await supabase.auth.signIn({ provider: 'github' });
  
      if (error) {
        console.error('GitHub sign-in error:', error.message);
      }
    }
  </script>
  
  <button on:click={signInWithGitHub}>Sign in with GitHub</button>
  

  
