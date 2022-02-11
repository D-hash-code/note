
## Thoughts on How Python can be Leveraged for Reporting

### Directory structures

**How should we really be naming files, and where should we place them?**

Some important don'ts to get out of the way first. Don't make the file names too long. Don't use different casings and conventions for files in the same codebase.

Some less strict don'ts. Don't nest file a layer deeper than it needs to be.

There is a question of the responsibilities of each python file. Picture this, we want to create some reporting functionality. Taking a data file and processing it through to an exported pdf with some specific data required by the end user. There is a spectrum of how we can structure this project. On one end of the spectrum we have
- everything from loading the csv to exporting the pdf sits in one python file

on the other end of the spectrum
- all of the subfunctions are split up and placed in utility folders/spaces and called by a container python file to achieve the same as the other approach

The advantage of the second approach is that downstream as we add more functions we can reuse stuff that we have already created. A single load_csv function can be used to convert our input csv to a dataframe for all of our reporting initiatives. This follows the DRY (don't repeat yourself) principle.

The advantage of the first approach is that when we create some reporting functionality in it's own space we are sure it won't break downstream. If a function is being used in various reporting initiatives, people will tend to want to make changes to it (even though we know we shouldn't!). And so a modular chunk of code is unstable. Another advantage of this "one project's code in one place" approach is that when we create something for a specific use case we don't need to think too deeply about how it can be used in other cases. Making something reusable is requires more thinking and work.

After all that I think I land somewhere in the middle about this. For the specific case of going from raw data to a report, the ideal approach is;
1. start assuming that all code for this reporting initiative will sit inside a single function
2. seperate responsibilities of the code by creating lots of small specific functions
3. for each function ask
   1. how often do I suspect I will need to use the specific behaviour that this function provides?
   2. suppose I provide differing inputs to the function, can I still leverage the functions behaviour easily? (i.e. if the function provides groupby + filtering functionality and my input dataframes have different column names then could I still use the same function?) 
4. If unsure leave the function as is for now, we can always export it to a global location later.