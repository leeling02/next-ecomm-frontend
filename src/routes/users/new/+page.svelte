<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    // import { authenticateUser } from './../../../utils/auth.js';
    let formErrors = {};
    
  
    function postSignUp() {
      goto('/');
    }
  
    async function createUser(evt) {
      evt.preventDefault()
  
    //   if (evt.target['password'].value != evt.target['password-confirmation'].value) {
    //     formErrors['password'] = { message: 'Password confirmation does not match' };
    //     return;
    //   }
    
  
      const userData = {
        name: evt.target['username'].value,
        email: evt.target['email'].value,
        password: evt.target['password'].value,
        // passwordConfirm: evt.target['password-confirmation'].value
      };




      const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/users', {
      method: 'POST',
      mode: 'cors',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(userData)
    });

    if (resp.status == 200) {
        const res = await resp.json()
        // console.log(res)
    
        postSignUp();

    } else if (resp.status == 400) {
        const res = await resp.json();
        console.log(res)
        console.log(res.error)
        formErrors = res.error; 
    
    } else if (resp.status == 500) {
        
      const res = await resp.json();
      //   ignore this: formErrors['email'] = { message: 'this email is already taken, please try with another email.' };
      formErrors = res.error; //form error message of 'email already taken'
      
    
    } else {

}
    }
  

</script>

<h1 class="text-center text-xl">Create an Account to Post a Job</h1>
<div class="text-center">
    <a class="link-hover italic text-xs" href="/login">Already have an account? Click here to login instead.</a>
</div>
<div class="flex justify-center items-center mt-8">
    <form on:submit={createUser} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="username">
                <span class="label-text">Username</span>
            </label>
            <input type="text" name="username" placeholder="johndoe" class="input input-bordered w-full" />
            {#if 'username' in formErrors}
            <label class="label" for="username">
                <span class="label-text-alt text-red-500">{formErrors['username']}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="email">
                <span class="label-text">Email</span>
            </label>
            <input type="email" name="email" placeholder="john@example.com" class="input input-bordered w-full" required />
            {#if 'email' in formErrors}
            <label class="label" for="email">
                <span class="label-text-alt text-red-500">{formErrors['email']}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="password">
                <span class="label-text">Password</span>
            </label>
            <input type="password" name="password" placeholder="" class="input input-bordered w-full" required />
            {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password']}</span>
            </label>
            {/if}
        </div>
    
        <div class="form-control w-full">
            <label class="label" for="password">
                <span class="label-text">Confirm Password</span>
            </label>
            <input type="password" name="password-confirmation" placeholder="" class="input input-bordered w-full" required />
            {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password']}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Create an Account</button>
        </div>
    </form>
</div>