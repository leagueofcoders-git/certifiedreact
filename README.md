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

**Module 11**

```
import React from "react";
import { useForm } from "react-hook-form";

const RegistrationForm = () => {

  const { register,getValues, handleSubmit, formState: { errors } } = useForm();
  const onMySubmit = (data) => {
    //save data to database
    alert(JSON.stringify(data));
  };

  return (
    <div className='container mt-5 ml-5'>
      <h1>Registration Form</h1>

      <form onSubmit={handleSubmit(onMySubmit)}>
        <div class="mb-3">
          <input type="text" className='form-control' placeholder="Your name" {...register("name")} />
        </div>
        <div class="mb-3">
          <input type="email" className='form-control' placeholder="Your email" {...register("email", {
             required: true })} />
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

