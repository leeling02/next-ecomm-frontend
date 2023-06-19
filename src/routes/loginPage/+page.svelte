<script>
    import { authenticateUser, createLoginStore } from "../../utils/auth";
    import { goto } from '$app/navigation'; 

  
    function postLogin() {
    goto('/about');
      }
    
      //Sections below are as --Login Function--
      async function Login(evt) {
        const userData = {
          username: evt.target['username'].value,        
          password: evt.target['password'].value,
        };
  
        // console.log("123")
        const res = await authenticateUser(userData.username, userData.password)
      
      //to track whether he/she is authenticated user, using authenticated function
  
        if (res.success) {
          postLogin();
      //Unhappy path 
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
    <button on:click={createLoginStore} id="loginButton" style="position:absolute; right: 700px">Log In</button>
  
</form>
    

  
  </div>
    
  
      
  
      