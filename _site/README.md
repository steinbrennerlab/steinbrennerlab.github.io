# [http://steinbrennerlab.org](http://steinbrennerlab.org)
The Steinbrenner lab webpage uses So Simple, a Jekyll theme https://github.com/mmistakes/so-simple-theme/tree/master/docs.  It is hosted by Github pages.  Minor site-wide customizations are included in `/assets/css/main.scss` and in `/_includes`

Content is added to the "News" or "People" pages by creating .md files within the posts and people subfolders then rebuilding the webpage in jekyll 
```bundle exec jekyll b```
and pushing edits to github.  

# Lab members
All timeline files live in `lab_timeline/`.
- Edit lab_timeline/lab_members.txt. Members with column "keep" = 1 are shown in lab_members.png. As of 2025 I set this to zero only for undergraduates and rotation students who have left the lab.
- Run the code in lab_timeline/process_lab_members_txt.ipynb (update the hard-coded `date` first)
- Output files (written to lab_timeline/) are lab_members.png, previous_UG_rotations.png, and previous_UG_rotations.csv

# Adding news
Create an .md file modeled after one in the "_posts" subfolder.  It will be added to _posts

# Adding yourself
Send a thumbnail (aim for 400 px wide, 200 px tall), a larger image, and any information (minimum: one-sentence summary of interests)

