<script>
    import { authenticateUser } from "../../../utils/auth";
    import { goto } from '$app/navigation'; 

  
    function postLogin() {
    goto('/about');
      }
    
      //Sections below are as --Login Function--
      async function Login(evt) {
        const userData = {
          email: evt.target['username'].value,        
          password: evt.target['password'].value,
        };
  
        
        const resp = await authenticateUser(userData.email, userData.password)
      
        if (resp.success) {
          postLogin();
      
        } else {
          throw 'Please check your username/password';
        
        }
  
      }
  
  </script>
  
  
  <div>
  
  <form on:submit={Login}>
    <label style="display:flex; flex-direction:column; align-items:center; justify-content: center">
      Username:
      <input type="text" name="username" required>
    </label >
    <label style="display:flex; flex-direction:column; align-items:center; justify-content: center">
      Password:
      <input type="password" name="password" required>
    </label>
    <button id="loginButton" style="position:absolute; right: 700px">Log In</button>
</form>
<!-- on:click={createLoginStore} -->

  
  </div>
    
  
      
  
      