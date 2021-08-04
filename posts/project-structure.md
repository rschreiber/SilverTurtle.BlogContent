Title: Project Structure
Lead: A look at how I've structured the project and repos
Published: 2/Aug/2021
Tags:
  - Sites
  - Github
  - Repos
---
It's been quite a while since I put the first post out, and a lot of head scratching on my part as how to best put this project together so that future maintenance is made a bit easier.

Something I'll tackle in a future post, but worth briefly mention here now is that there are 3 major components to having this static blog site.
- The site generator
- The site template, or theme
- The site content

I wanted to keep these all separate so that there's a clear boundary when I'm working on these in the future, however, they all need to come together with a specific folder structure when the generator runs.

What I've settled on, after trying out 5 different combinations prior to now, is to have these three components stored in separate repos inside GitHub, and making use of git sub-modules to bring the two projects together. What we need (and now have) is a file/folder/project/repo structure on disk that looks like this:
- Generator
  - Content
  - Theme
  
  
The GitHub action that does the build and deploy of the site is in the Generator repo, and I've set up an action on both the content and theme repos that cause the generator repo to kick off.

Additional steps in in the Generator build action include fetching the Content and Themes repos as submodules and ensuring they're in the correct sub-folders before the Generator application runs. I'll dive into this in my next post.


