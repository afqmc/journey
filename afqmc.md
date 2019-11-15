# Creating Package

* Open Julia pkg and write

  ```(v1.2) pkg> generate AFQMC```
 
* Open `~/.julia/config/startup.jl` and write the command

  ```push!(LOAD_PATH, "/Users/hshi/myproject/AFQMC/AFQMC")```
  
* Setup git environment

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

  * `git remote add github https://github.com/afqmc/AFQMC.git`

  * `git push -u github master`

* Setup documentation environment

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

* Use localhost to check the documentation
 
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
   
* Setup gh-pages branch

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

  