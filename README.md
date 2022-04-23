# Assignment 11: R Dashboards

> #### Install required packages
>
> You will need to install two new packages for this assignment: `flexdashboard` and `crosstalk`
>
> To do so, run the following two lines of code in the RStudio console:
>
>     install.packages("flexdashboard")
>     install.packages("crosstalk")


In this assignment, you will learn how to create dashboards. Dashboards are web pages for interactively visualizing data, and can be created using the RMarkdown files that we are already familiar with.

You will have to create your own RMarkdown file this week, following the instructions in the Exercises. 

**Read the submission instructions carefully**, because they are different for this assignment.

## About the data

The world is in lockdown, but you still gotta catch 'em all. Yes, this week we will be visualizing Pokemon statistics.

This dataset was originally downloaded from Kaggle [here](https://www.kaggle.com/abcsds/pokemon). The table contains the following columns:

| Column | Description |
| ------ | ----------- |
| `#` | ID for each pokemon |
| `Name` | Name of each pokemon |
| `Type 1` | Each pokemon has a type, this determines weakness/resistance to attacks |
| `Type 2` | Some pokemon are dual type and have 2 |
| `Total` | sum of all stats that come after this, a general guide to how strong a pokemon is |
| `HP` | hit points, or health, defines how much damage a pokemon can withstand before fainting |
| `Attack` | the base modifier for normal attacks (eg. Scratch, Punch) |
| `Defense` | the base damage resistance against normal attacks |
| `SP Atk` | special attack, the base modifier for special attacks (e.g. fire blast, bubble beam) |
| `SP Def` | the base damage resistance against special attacks |
| `Speed` | determines which pokemon attacks first each round |


## Exercises

1. Create an RMarkdown file in RStudio by going to the *File* menu, then *New File*, and then *R Markdown*. 

    * If there is a button that says **Create Empty Document**, then click that to create an empty Rmd file. (This button is not always available, depending on your version of RStudio.)
    
    * *Otherwise if that button does not exist*, create the file with the default options, and then **delete all the contents** that are in the file by default.

    Save the new (empty) file in the project folder with the name `assignment11.Rmd`.
    
    In the Git pane in RStudio, you should see this file appear. Commit the `assignment11.Rmd` file, and push it to GitHub.
    
2. Take a look at the contents of the RMarkdown file that you just created.

    RStudio create the file with a default header section as well as some example contents.
    
    The header section should look similar to this:
    
       ---
       title: "R Notebook"
       output: html_document
       ---
        
    Add a line into the header section to add your name as an author, and another line for the date (as you have done in previous assignments). Change the title to *Assignment 11*.
    
    The `output` line indicates what format we want to knit the document into. In previous assignments in the course, we have knitted to PDF files. However, in the example above, we have selected the HTML format, which is a web page. You can try knitting the `assignment11.Rmd` file to an HTML file to see what this looks like. The output will open in a web browser, but the structure should be similar to PDF documents that you are familiar with.
    
    An R dashboard is also an HTML webpage, but it is structured as a dashboard with columns and rows, rather than as a continuous document.
    
    Change the output from `html_document` to `flexdashboard::flex_dashboard`
    
    This tells RStudio to use the flexdashboard library to create our final HTML file when we knit our document. Try knitting the document again. You should find that the document now knits to a flexdashboard, and the default content is no longer formatted into a continuous document.
    
    Once you have finished this exercise, commit your progress so far.
    
3. If you created the file as an empty document, there should be no content below the header section. (If you accidentally created a template file with contents, then delete everything *after* the closing `---` of the header section.
    
    Then, below the header section, create a layout with two columns by entering this content:
    
       Column
       -------------------------------------
        
       ### Component 1
        
       ```{r}
       ```
        
       Column
       -------------------------------------
        
       ### Component 2
        
       ```{r}
       ```

    Try knitting the file again, and see how the dashboard looks now. You should find there are 2 columns, each containing one of the components:
    
    ![](img/2-col-layout.png)
    
    Once you have finished this exercise, commit your progress so far.
    
    > ### `flexdashboard` layouts
    >
    > There are all kinds of flexdashboard layouts that we can create very simply. If you are interested, try copy-and-pasting a few of the examples here: https://rmarkdown.rstudio.com/flexdashboard/layouts.html (make sure you go back to the template above when you are finished).
    >
    > There are a few general principles to understand to format dashboards.
    >
    > * Level 1 headings create new pages. You can create level 1 headings as
    >    
    >       Page 1
    >       ==========
    >
    >    or
    >
    >       # Page 1
    >
    >    (The line of equals signs is an alternative to the `#` symbol.)
    >
    > * Level 2 headings create columns (default) or rows.
    >
    >       Column 1
    >       --------
    >
    >    or
    >
    >       ## Column 2
    >
    >    To create rows instead of columns, you need to set the `orientation` option
    >    in the header:
    >
    >       output: 
    >         flexdashboard::flex_dashboard:
    >           orientation: rows
    >
    > * Level 3 headings create boxes that group content:
    >
    >       ### Content Box 1
    >
    >    (Try adding an extra content box to one of the columns in the template and see what happens.)
    >
    > * We can customize pages, columns/rows, or boxes by puttings options inside 
    >    curly brackets after the name
    >
    >    For example, to convert a column (level 2) into a sidebar:
    >
    >       SidebarName {.sidebar}
    >       ----------------------

4. Using the *`flexdashboard` layouts* guide above, add a sidebar to your dashboard.

    You should also keep the two columns that we created in the previous question, so that your dashboard with sidebar looks like this:
    
    ![](img/2-col-sidebar-layout.png)
    
    Once you have finished this exercise, commit your answers.

5. Now we will start adding some content to the dashboard.

    * Immediately below the header section (but before any of the content), add a new code chunk.
    
      This will be out setup code chunk, so give it the name `setup` and set it so that neither its code not its output appear in the dashboard using the `include = FALSE` option:
      
          ```{r setup, include = FALSE}
          
          ```

    * In the setup chunk,, add code to load the following 3 packages: `tidyverse`, `plotly`, and `crosstalk`. Recall that packages are loaded with the `library` function, e.g.
    
          library(tidyverse)
    
    * Below these, add another line of code to read in the data from the `pokemon.csv` file using the `read_csv` function, and store it as a variable called `pokemon`. You should do this in setup chunk at the top of the Rmd file. (You can leave the columns as their default datatypes.) Make sure you use `read_csv` and not `read.csv` (`read_csv` is a more modern function that is part of the tidyverse).
    
    Once you have finished this exercise, commit your progress so far.


6. 
    * Under the "Component 2" heading in the right-hand column, create a scatter plot showing the `Attack` (y-axis) vs `Defense`. Knit your file to a dashboard and take a look at what it looks like. Color the points by the `Type 1` variable (remember that because `Type 1` contains a space, we have to wrap it in backticks, `, when we use it as a variable).
    
    * There are a couple of problems with our figure.
    
      First, the code may get inserted into our dashboard along with our graph. In a dashboard (unlike a PDF document) we do not typically want to include our code. You can prevent the code from appearing by adding the `echo = FALSE` to the options for the code chunk, like this:
      
          ```{r, echo = FALSE}
    
      > #### `echo` vs `include`
      >
      > `echo = FALSE` prints the output of the chunk but hides the source code
      >
      > `include = FALSE` hides both the source code and the output (but still runs the chunk). We do not want to use this option here, as it will prevent our graph from being visible.
    
    * Finally, the `ggplot` graph is static, and so is not sized to the available area. To fix this, we need to convert our `ggplot` graph into a `plotly` graph. You can do this by first saving the `ggplot` graph as a new variable, and then using the `ggplotly` function on that variable. For example:
    
          p <- pokemon %>%
            ggplot() + ...
          
          ggplotly(p)
    
      Do this to convert your `ggplot` scatter plot into a `plotly` scatter plot. You should see that it is now sized to occupy the entire column.
    
    Once you have finished this exercise, commit your progress so far.
    
7. Under the "Component 1" heading (i.e. the left hand column of the dashboard), create a box plot to show the distribution of the `Total` column for different types of pokemon (i.e. `Total` is on the y-axis, and `Type 1` is on the x-axis). 

    You should also color the box plots by the `Type 1` variables using the `fill` parameter.

    Order the box plots by the median of `Total` for each type of pokemon (as we did in Assignment 9).
    
    Make sure you rename the x-axis label for this graph with the `labs` function. (You do not need to add a title - we will do this in *Exercise 9*).
    
    Convert your `ggplot` graph to a `plotly` graph, as in the previous question, and make sure that we do not see the code of this chunk.
    
    Once you have finished this exercise, commit your progress so far.

8. We have now create two graphs to show our data. However, both graphs are relatively static. One of the advantages of dashboards is that we can create interactive visualizations. Let's do that.

    * First we need to convert our pokemon dataframe to a `SharedData` object. This is part of the `crosstalk` package, and allows one part of the dashboard to alter the dataset and have those alterations reflected in other parts of the dashboard.
    
      Add this line to the bottom of the setup chunk:
      
          shared_pokemon <- SharedData$new(pokemon)
    
    * Next, update the code for both your graphs so that they use the `shared_pokemon` dataset rather than the `pokemon` dataset.
      
      If you knit the Rmd file to a dashboard now, it should look the same as before.
      
    * However, we can now add a control element to our dashboard to select different parts of the data. Under the sidebar section in your Rmd file, add a code chunk with the following line of code:
    
          filter_select("poke_type", "Pokemon Type", shared_pokemon, ~`Type 1`)
    
      If you re-knit your dashboard, you should see that there is now a drop-down menu that you can use to select different types of pokemon. As you do so, the plots should update to show only pokemon of those types!
    
    Once you have finished this exercise, commit your progress so far.

9. Finally, let's add some finishing touches to our dashboard to make it more presentable:

    * Change the names of the components (Component 1 and Component 2) to appropriate titles for each of the graphs by editing these headers in the `Rmd` file.
    
    * Give the x-axis of the box plot a more appropriate label (you can use the `labs` function as we have done before).
    
    * The labels on the box plot's x-axis will overlap by default. You can reduce this by rotating them, by add the following function to your `ggplot` code:
    
          ... + theme(axis.text.x = element_text(angle = 45))
    
    Once you have finished this exercise, commit your progress so far.


## Beyond this Assignment

We have only scratched the surface of what is possible with dashboards. Two ideas for those who want to go further:

* Poke around in the Resources and Further Reading section at the end of these instructions and take a look at some of the example there to see what else you could create. 

* If you want to host your dashboard on the web for anyone to visit, you can do so from GitHub using GitHub Pages - this is left as an exercise for interested readers... 


## How to submit

You must submit two ways:

1. Commit and push both the assignment11.Rmd and the assignment11.html file to GitHub

2. Download the *assignment11.html* file, **zip it** and upload the zip file to the *Assignment 11* posting on Blackboard.

  * To download the *assignment11.html* (after knitting it), find the file in the Files tab of RStudio (bottom right pane), and click the checkbox next to the file name. Then at the top of the Files tab, click the *More* button, and then click *Export* and download the file.
  
  * To make sure that you have downloaded the correct html file, go to the Downloads folder on your computer and find the *assignment11.html* that should now be in there. Double click on the file, and your dashboard should open in a new tab in your web browser.
  
  * Zip the *assignment11.html* file. 
  
    * On Windows, right click on the file, select "Send to" and then select "Compressed (zipped) folder". This will create a file called *assignment11.zip*, which you can upload to Blackboard.
    
    * On a Mac, you can follow these [instructions](https://support.apple.com/guide/mac-help/compress-uncompress-files-folders-mac-mchlp2528/mac)


## Resources and further reading

You may find the following helpful for completeing this assignment:

* The [ggplot cheatsheet](https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)

* Tutorial and documentation on the [flexdashboard package](https://rmarkdown.rstudio.com/flexdashboard/index.html)

* Tutorial and documentation on the [crosstalk package](https://rstudio.github.io/crosstalk/index.html)

* Even more interactive dashboards can be created with the Shiny package which creates not just a web page but also a web server: [tutorial here](https://shiny.rstudio.com/tutorial/)
