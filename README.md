### R cookbook

#### Management commands

```
.libPaths() # get library location
library()   # see all packages installed
search()    # see packages currently loaded
sessionInfo() # Get and report session information including R version and loaded libraries
# Find all available methods for a given library
library(NAME)
utils::methods(class = 'NAME')
```

#### R package management and custom package installation from source

```
R CMD INSTALL [options] [-l lib] pkgs
```

[rdocumentation](https://www.rdocumentation.org/packages/utils/versions/3.6.2/topics/INSTALL)  
Standard library installation method from console within R: `install.packages('pkg')`, `BiocManager::install('pkd')`, `devtools::install_github('pkg')`, `remotes::install('pkg')` (check remotes command), etc.

If there are compiler related issues in regards to installation of a library then the following command can be executed from the downloaded original library source package: `R CMD INSTALL <pkg_path>`. The following commands maybe helpful during installation:

```
# Get help on available options and tools:
R CMD --help

# Get information about Make config variables:
R CMD config --all
```

Note that if a compilation fails due to missing required C++ library dependencies, and `homebrew` is used to install the required libraries, `Makeconf` file which is located in `R_HOME/Resources/etc` or `/Library/Frameworks/R.framework/Resources/etc/` can be adjusted for `FLIBS` path for instance to choose the correct compiler and library path (`LIBRARY_PATH`). Otherwise, at least in UNIX operating systems environmental variables are not accessed by R during installation. This leads to confusion about compiler use even if the desired compiler is available from the first directory within the `PATH` variable.

In additional often in `src` directory of a given library package `Makevars` file specify any library defined variables during installation.

#### Miscellaneous topics

```
# Access to values in a named list  
list$name

# Assignment of names for list elements in a 'for' loop is accomplished through list[[name]] syntax for example:
some_list <- c("name_1"=1, "name_2"=2, "name_3"=3)
other_list <- list()
for (name in names(some_list)) {
    other_list[[name]] <- 0
} 
```