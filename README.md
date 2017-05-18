# hw08: Economic Dynamics (2017Q1)

Publish: 2017-05-18 15:00:00  
Due: 2017-05-28 18:00:00

## Purpose

Project start-up

## Assignment Overview

In this assignment and the next, you will make an R package **lrem**, abbreviation for Linear Rational Expectations Model,  **under your own account** (if you have a repository of the same name already, you can use any other name but let the lecturer know the name you chose). The final project of this course (a package that solves and simulates a class of LRE models) will be submitted (pushed) to this repository as an update. 

For assessment of this assignment and the final project, the TA and I will do the following:

* Read README.md of your package repository and install it on our computers.
* Use the installed package following instructions in the vignette. 
* Use the installed package to solve and simulate (secret) models. 

This assignment is a preparatory exercise, in which you will 

* Make a repository;
* Make a package skeleton;
* Move contents of the solution to hw07;
* Add a functionality to `lre_auto()` function;
* Write a vignette about the use case of `lre_auto()` function and simulation.

The main problems that require hard work are collected under [Problems](#problems) section.

## Instructions

### Set up a repository

* Create a public repository `lrem` here https://github.com/new
    * Don't check "Initialize this repository with a README"
* You are redirected to the how-to page. Clone the repository by clicking 
  "Set up in Desktop" button.   
  You will have a folder named `lrem` somewhere on your computer. 
* Open RStudio and set this `lrem` folder as the current working directory.
    * See [here](https://support.rstudio.com/hc/en-us/articles/200711843-Working-Directories-and-Workspaces) if you don't know how to do it.

### Make a package with `devtools`

Make sure that `getwd()` points to the empty `lrem` folder.

#### `devtools::create(".")`

Create a package by
```
devtools::create(".")
```
As you already know, this command sets up the package skeleton in the `lrem` folder. 
Now the time to do the first commit. (And push if you want to.)

`.` is the UNIX way to represent current directory.

#### `DESCRIPTION` file

Then do the following to `DESCRIPTION` file.
* Write "Title" section.
* Fill out your name in `Authors@R` section.
* Write "Description" section.
* Rewrite License section to whatever license you want it to be licensed under.
  You can use `devtools::use_mit_license()` for MIT License. In that case, 
  don't forget to rewrite `LICENSE` file's Copyright holder section.
* Run `devtools::use_package("QZ")` to specify the dependency.

#### `README.md` file

Create `README.Rmd` with 
```
devtools::use_readme_rmd()
```
Write something and knit to create README.md. This file is the first webpage 
that someone who access http://github.com/your-account/lrem will see. 
Write a nice and short instruction how to install and use your package. 

#### vignette 

Create a vignette with 
```
devtools::use_vignette("lrem-intro")
```
A vignette is a short paper that accompanies a package. Package creators 
write extended notes, for example, about the goals the package accomplish 
and how to use the package. You will write a vignette in this and next assignments.
The above command creates `vignette/lrem-intro.Rmd`. You can write in now familiar 
Rmd format. Start writing what model is going be solved by your package.

Build the vignette with 
```
devtools::build_vignettes()
```
You will have nice HTML vignette under `inst/doc` folder.

## Problems

### Update hw07's contents and allow for $E \neq I$

The contents of your hw07 solution are sufficient to solve autonomous, 
deterministic LRE model with $E = I$. Move everything under `R` directory of the new package. 

Then, add a new functionality so that `lre_auto()` function can solve $Ex_{t+1} = Ax_t$ as well. I'd suggest the following structure:

```r
lre_auto_bk <- function(A, x0) {
  # The contents of hw07's lre_auto
}

lre_auto_klein <- function(A, E, x0) {
  # Solution here using QZ decomposition!
}

lre_auto <- function(A, E = NULL, x0) {
   if (is.null(E)) {
     lre_auto_bk(A, x0)
   } else {
     lre_auto_klein(A, E, x0)
   }
}
```

**Don't forget to write Roxygen comments for `lre_auto` and export it to the namespace.**



### Update the vignette

Now you have something you can write about the package. 
Users may want to know

* how to use the package (after installation);
* what kind of models can be solved by it; and
* one or two examples.

Write extended documentation about `lre_auto()` in a vignette in either `lrem-intro.Rmd` or a new file.

If you have no idea what to write in a vignette, have a look at a vignette for **ggplot2** for example by running

```
vignette("extending-ggplot2")
```

`vignette()` lists all available vignettes. 

### tests (optional)

Add tests if you really want to make a good package. Read Hadley's chapter
http://r-pkgs.had.co.nz/tests.html on testing.

### Build viggnets, check, commit, and push

Do the following.

* `devtools::build_vignettes()`
* `devtools::check()`


Then, go to the Git pane. 

* Check every check box.
* Click Commit button and fill our the commit message.
* Click Commit again.
* Then push.

That's it. You don't need to make a Pull Request. 

## Remarks

### Collaboration

Because the repositories you make are public, everybody else can see your work. 
I don't deny you to learn from other students' works but keep in mind that their works 
are copyright protected unless otherwise explicitly stated.

Be a sensible user not a pirate. 

### Need help?

If you have questions about this assignment, ask on Slack giving us the repository name, hw08. Alternatively, you can open an issue for the [base repository](https://github.com/rokko-ed17q1/hw08/issues). 
