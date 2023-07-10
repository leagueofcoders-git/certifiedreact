**Module 04**

```
  setupMiddlewares: (middlewares, devServer) => {
    if (!devServer) {
        throw new Error('webpack-dev-server is not defined')
    }

    if (fs.existsSync(paths.proxySetup)) {
        require(paths.proxySetup)(devServer.app)
    }
    middlewares.push(
        evalSourceMapMiddleware(devServer),
        redirectServedPath(paths.publicUrlOrPath),
        noopServiceWorkerMiddleware(paths.publicUrlOrPath)
    )
    return middlewares;
},  
```

**Module 12 - Registration Form**

```
import React from "react";
import { useForm } from "react-hook-form";

const RegistrationForm = () => {

  const { register,getValues, handleSubmit, formState: { errors } } = useForm();
  const onMySubmit = (data) => {
    //save data to local storage
    localStorage.setItem("userdata",JSON.stringify({ 
      name: data.name, email: data.email, password: data.password 
  }));
    alert(localStorage.getItem("userdata"));
  };

  return (
    <div className='container mt-5 ml-5'>
      <h1>Registration Form</h1>

      <form onSubmit={handleSubmit(onMySubmit)}>
        <div class="mb-3">
          <input type="text" className='form-control' placeholder="Your name" {...register("name")} />
        </div>
        <div class="mb-3">
          <input type="text" className='form-control' placeholder="Your email" {...register("email", {
          required: "Please Enter Your Email!",
          pattern: {
              value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i, 
              message: "Please Enter A Valid Email!"}
          })} />
          {errors.email && <span style={{ color: "red" }}>
            *Email* is mandatory </span>}
        </div>
        <div class="mb-3">
          <input type="password" className='form-control' placeholder="Your password" {...register("password", {
            required:"Please enter a password",
            minLength: {
              value: 8,
              message: "Password must be at least 8 characters long!"
              }
          })} />
           <span style={{ color: "red" }}>{errors.password?.message}</span>
        </div>
        <div class="mb-3">
          <input type="password" className='form-control' placeholder="Confirm password" {...register("confirmPassword", 
          {validate: (match) => {
            const pwd = getValues("password")
            return match === pwd || "Password does not match!"
          }}) 
         }/>
          <span style={{ color: "red" }}>{errors.confirmPassword?.message}</span>
        </div>
        <div class="mb-3">
          <input type={"submit"} className='btn btn-primary' />
        </div>
      </form>

    </div>
  )
}

export default RegistrationForm
```

**Module 12 - Login Form**

```
import React, {useState} from "react";
import { useForm } from "react-hook-form";

function Login() {

    const[loginInfo, setLoginInfo] = useState('')
    const[alert, setAlert] = useState('')
    const {register,handleSubmit,formState: { errors }} = useForm();
    const onSubmit = (userdata) => {
        const userData = JSON.parse(localStorage.getItem("userdata"));
        if (userData.email === userdata.email) {
            if (userData.password === userdata.password) {
                setLoginInfo(userData.name + " You Are Successfully Logged In");
                setAlert("alert alert-success")
                sessionStorage.setItem("userName",JSON.stringify({name: userData.name}
                ));
            } else {
                setLoginInfo("Email or Password is not matching with our record");
                setAlert("alert alert-danger")
            }
        } else {
            setLoginInfo("Email or Password is not matching with our record") ;
            setAlert("alert alert-danger")
        }
    };

    return (
        <div className='container mt-5 ml-5'>
            <h1>Login Form</h1>
            <form onSubmit={handleSubmit(onSubmit)}>
                <div className="mb-3">
                    <input type="email" className='form-control' {...register("email", { required: true })} />
                    {errors.email && <span style={{ color: "red" }}>
                    *Email* is required </span>}
                </div>
                <div className="mb-3">
                    <input type="password"  className='form-control'{...register("password")} />
                </div>
                <div className="mb-3">
                    <input type="submit" className="btn btn-primary mb-3" value="Login" />
                </div>
                <div className="mb-3">
                    <p className={alert}>{loginInfo}</p>
                </div>
            </form>
        </div>
    );
}
export default Login;
```
**Module 13 - Movies.js**

```
<div className="container">
            <div className="row row-cols-1 row-cols-md-3 g-4">           
                {movies.map((movielist) => {
                    return (
                        <div className="col" key={movielist.id}>
                        <div className="card h-100">
                            <img src={'https://image.tmdb.org/t/p/w500/' + movielist.backdrop_path} className="card-img-top" alt="..." />
                            <div className="card-body">
                                <h5 className="card-title">{movielist.original_title}</h5>
                                <p className="card-text">{movielist.overview}</p>
                            </div>
                            <div className="card-footer">
                                <small className="text-muted">Release Date: {movielist.release_date}</small>
                            </div>
                        </div>
                        </div>
                    )
                })}
            </div>    
</div>
```
