<template>
    <main class="form-signin w-100 m-auto">
        <form @submit.stop.prevent="submit">
          <h1 class="h3 mb-3 fw-normal">Please sign in</h1>
      
          <div class="form-floating">
            <input 
            v-model="email"
            type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
            <label for="floatingInput">Email address</label>
          </div>
          <div class="form-floating">
            <input 
            v-model="password"
            type="password" class="form-control" id="floatingPassword" placeholder="Password">
            <label for="floatingPassword">Password</label>
          </div>
      
          <button class="btn btn-primary w-100 py-2" type="submit">Sign in</button>
        </form>
      </main>
  </template>
  
  <script>
  import Cookie from 'js-cookie';

  export default {
    name: 'LoginView',

    data(){
        return {
            email: '',
            password: '',
        };
    },

    created(){
        Cookie.remove('_todolist_token');
    },

    methods: {
        submit(){
            const payload = {
                email: this.email,
                password: this.password, 
            };

            fetch(`http://127.0.0.1:8000/api/login`, {
                method: 'POST', 
                headers: { 
                    'Content-Type' : 'application/json',
                    'Access' : 'application/json',
                 },
                body: JSON.stringify(payload)
            })
            .then(response => response.json())
            .then(res => {
                Cookie.set('_todolist_token', res.acess_token);
                console.log(res.access_token);
            })
        },
    },
  };

  </script>

<style>
.form-signin {
    max-width: 330px;
    padding: 1rem;
  }
  
  .form-signin .form-floating:focus-within {
    z-index: 2;
  }
  
  .form-signin input[type="email"] {
    margin-bottom: -1px;
    border-bottom-right-radius: 0;
    border-bottom-left-radius: 0;
  }
  
  .form-signin input[type="password"] {
    margin-bottom: 10px;
    border-top-left-radius: 0;
    border-top-right-radius: 0;
  } 
</style>
  