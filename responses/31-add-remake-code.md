So, what does this do for you? Well, if you had this `remake.yml` file in your current working directory, and the `download_data()`, `process_data()`, and `myplot()` functions were in `code.R` (which you don't), it would look like this when you run `scmake` from the `scipiper` package

![scmake run image](https://user-images.githubusercontent.com/2349007/81699123-8c355a00-942c-11ea-8919-4ff4bccfb1e8.png)

---
Now - adding on to this PR by pushing up additional commits - add and modify code, folders, and this remake file so you can build _your_ `figure_1.png` with `scipiper::scmake()` (BTW, if you haven't run into this syntax, {package_name}::{function_name} allows you to run a function without `library({package_name})`). Build on your existing folders, functions, and code from the previous sections. Comment in the pull request with a screenshot of the build message, like we have in the message above :point_up:. Assign Alison or Jordan to review your PR, and we may ask for a few changes before merging. 


