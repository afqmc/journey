# Inital Package

* Open Julia pkg and write

  ```(v1.2) pkg> generate AFQMC```

* Rename the fold to `afqmc.jl`
 
  My github username is `afqmc`. If the folder's name is `AFQMC`, my personal website and gh-pages will have 404 error.
 
* Open `~/.julia/config/startup.jl` and write the command

  ```push!(LOAD_PATH, "/Users/hshi/myproject/AFQMC/afqmc.jl")```
  
# Setup Git

  * `git init`
 
  * Open `.git/info/exclud` and write
 
     ```
     *.swp
     *~
     .*
     docs/build/
     ```
  * Add README.md 

  * `git add .`

  * `git commit -m "init AFQMC project.."`

  * `git remote add github https://github.com/afqmc/afqmc.jl.git`

  * `git push -u github master`
 
# Setup Documentation

  * Follow the instruction on https://juliadocs.github.io/Documenter.jl/stable/man/guide/

  * In AFQMC directory, run `mkdir docs`
 
  * In `docs`, run `mkdir src; touch make.jl`

  * Write the following in to `make.jl`
 
      ```
      using Documenter, AFQMC 
      makedocs(sitename="AFQMC.jl")
      ```
      
  * Write in `src/AFQMC.jl`
 
      ```
      module AFQMC
  
      export greet
      
      """
        greet()

      Print "Hellow World"
      """
      greet() = print("Hello World!")

      end # module
      ```
      
  * Write in `docs/src/index.md`
 
       ````
       #AFQMC.jl Documentation

       ```@docs
       greet()
       ```
       ````
       
   * In docs, run `julia --color=yes make.jl`

   * The documentation is created in `docs/build`

## localhost 
 
  * In `docs/build`

     ```
     python -m SimpleHTTPServer 8000
     ```
     
     or
     
     ```
     python3 -m http.server --bind localhost 8000
     ```
  
  * In web browser

     ```
     http://localhost:8000/
     ```
   
## gh-pages

  * Push the master branch to the cloud 

  * Copy `docs/build` outside

  * Follow the step in https://gist.github.com/ramnathv/2227408

     ```
     cd /path/to/repo-name
     git symbolic-ref HEAD refs/heads/gh-pages
     rm .git/index
     git clean -fdx
     echo "My GitHub Page" > index.html
     git add .
     git commit -a -m "First pages commit"
     git push origin gh-pages
     ```
     
  * Copy the files in `build` to gh-pages and push it the cloud.

  * We can maintain different versions by using `versions.js` file, e.g. using the command below
  
    ```
    var DOC_VERSIONS = [
    "stable",
    "v0.5",
    "v0.1",
    "dev",
   ];
   ```
  
# Test
   
   * Generate`test/runtests.jl` to write tests.
   * Add `Test` package

     ```
     julia>]
     (v1.2) pkg> activate .
     (AFQMC) pkg> activate ./test/
     (test) pkg> add Test
     ```  
   * Test environment will be in `test/Manifest.toml` and `test/Project.toml`
   * Add `deps/build.jl`, the package will run `build.jl` when it is installed.
