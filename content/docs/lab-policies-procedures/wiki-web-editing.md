---
title: Lab Website/Wiki Editing
linktitle: Lab Website/Wiki Editing
type: book
date: '2019-05-05T00:00:00+01:00'
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
summary: >
  With the lab website and wiki being hosted through GitHub, resources are compiled below on how to edit some of the more popular pages on the sites, along with general guidelines!
---
The lab website (and wiki) is hosted through Git, under these repositories: <ins>https://github.com/naomibschwartz/naomibschwartz.github.io</ins>, and [insert hyperlink to lab-wiki when published], but the actual website uses a combination of Git and Hugo commands to edit and run it locally or through Git servers. 

Mainly, while using Git and Hugo as a foundation, the visual and frontend is based on WowChemy (or HugoBlox now) templates and their guides. 

Their codes are a mix of HTML, CSS, and markdown languages at the backend – while it may seem daunting, there are MANY resources, and they take in basic commands so it isn’t too difficult to get a grasp. Some incredibly useful resources will be listed throughout this page, and compiled at the end. For any suggestions about the lab website, or questions on editing please reach out to the lab group.

## Editing Lab Content
To edit the website content, you can do this through whatever hosting system you prefer, but mine is using the RStudio desktop application. For the next steps the actions will be specific to this platform, but most commands are done through terminal so it’s unlikely that other platforms would differ in function drastically.

When using RStudio, I like to set it up to have the terminal running within the program, and then you will have the file open that you are looking to edit, and finally the actual folder contents (imaged below).

![](rstudio-setup.png)

Before beginning to edit I would first check what Git branch you are working on, ensuring that you are (a) correctly connected with Git, and (b) you are not working on the main branch if you know other people are working on the page at the same time. 
To do this, simply type ‘ git branch ‘ in your terminal, and the branches that are currently active will be listed. 

The one highlighted in Green is the branch you are on currently, here I am on the main branch, where I have conducted a ‘ git pull ‘ previously to ensure that my content is up to date, and a ‘ git status ‘ to make sure that there are no uncommitted files left – possibly leading to file conflicts down the line.

Once this is done, it’s best to move off of the main branch, onto a new branch where you can push and pull content without interfering with the main branch which holds all the final content that is being published on the website. To create a branch, you type ‘ git branch <branch_name> ‘. To switch over to this branch, you type ‘git checkout <branch_name>’.

Now that you are on your editing branch, it would be a good idea to ‘pull’ content from Git to ensure you are working with the most up to date content. To do this just type ‘git pull origin main’ which will pull the content from the main branch, and make sure the local branch you are working on reflects these changes.

You are now ready to edit content, and hopefully doing so without making conflicting edits with anyone else! Also, by working on a separate branch it adds an extra layer to ensuring that any edited content is acceptable for public viewing. 

To actually edit the website, the two folders you will be working within to edit content are likely to be CONTENT and ASSETS. 

Within content, folders that are tied with each page of the website can be found, and a directory _index.md file which is the landing page for the website. Depending on what you are looking to edit, they have practically the same set-up. I’ll take you through editing the Author, Research, and Publications pages which are likely to be the most edited on the website, and from these you can get a sense of the general editing guidelines.

Beginning with a quick overview of the content folder, we can see the _index.md (which is a file needed at the beginning of any folder so that the website can be read correctly by github pages). Below that there are numerous folders, of which the admin and images folder you can likely ignore, as they don’t hold any content that should be edited.

### Editing Authors
Beginning first with editing Authors, you want to navigate to that folder – you don’t need to change your directory or anything like that, you just want to pull the relevant index.md file out from there to edit. Say I was looking to edit my own page, I can do this by:

1.	Entering the content/authors file, and finding the author (in this case kelsey-mcguire), and opening the _index.md file found there. If you are using R, your desktop should look something like this:

2.	To edit the content, you have to use markdown formatting, but it isn’t too complicated, where you can just swap out the desired information, or say you were looking to add an interest or education, you can do this by following the same format as the previous information listed.
  a.	Here I have added some interests to my author page.
  b.	One edit that may come up a lot surrounding authors are changing them between the groups found on the People’s tab of the website. To do this you want to go down to the user_groups, and change it to the desired group (either Current Lab Members or Alumni) – you can see the difference below on how to distinguish the groups.

3. Once your desired edits are done, you must save the file, and then you can check that it is in the ‘queue’ to be committed by typing ‘ git status’
  a.	It is effective to NOT push after every single edit, instead I would try to do it by major projects - *E.g., Once you have felt like you’ve hit a reasonable break, say you have edited all the pages you needed to, then I would mass commit them at once through one push request so that the system doesn’t get overwhelmed.*

4. Now that you have edited and saved your changes, before pushing them to the Git, it is always a great idea to run a local version of the website on your system. This will visually show you what your changes look like, and then you can go back and forth before they end up as you wished them to be!
  a.	To do this, you simply type ‘ hugo server ‘ – this will build the site and provide a ‘localhost’ link that you can open in your browser.
  b. This should open up our lab website, and you can then navigate to the edited page to see your changes.

You can see that on the actual Git hosted site, the edits don’t appear, but in the local version the edits have been implemented – this will change once you have pushed the edits.

5. When you have confirmed on the local end that all the edits look to be finished and correct you can now add, commit, and push them to the actual git! You will have to first stop the local running of the site (type ‘CTRL + C), and then to see what edits are queued you can type ‘ git status ‘, which will tell you the branch you are on, and what changes are in the works.

Here we can see there is only one edit in the queue, so it would actually be better to		wait until you have more edits in line surrounding a specific task before adding,			committing, and pushing these edits downstream, which will be discussed further down.
ADDING/REMOVING AUTHORS
To add a new member to the group the easiest thing to do would be to copy a pre-existing authors file, and edit it from that template. Two things that you will need to do are:

1. Edit the _index.md with the members information, and triple check that there is no residual information from the .md you copied over. 
2. Place the desired profile photo within the Author’s folder, and rename it to ‘ avatar.jpg ‘ – try to make sure the photos come in JPEG format, but .png sometimes work.

Removing an author is even simpler, all you have to do is delete the folder that refers to them.

### Editing Research Page
With the research page there is actually not as many moving parts as seen with the Authors, instead the entire page is hosted through one markdown file, with some photos being tied in from the assets folders.

The way that this markdown is set up is through Blocks (extensive documentation can be found here: https://docs.hugoblox.com/getting-started/page-builder/), where each one represents a different research project within the lab.

### Add New Project
To add a new project, you can simply copy and paste the format from another project, or you can write it from scratch using the template below – ensure that your new block begins with a dash and the block depicting what template you are using (typically you will just use a markdown format, but Hugo provides some pre-set templates which you can explore as well)

```
- block: markdown
   id: active-project-x
   content:
      title: Section 1
      subtitle: A subtitle
      text: Add any **markdown** formatted content here - text, images, videos, galleries - and even HTML code!
```

Each project should have an id, which can just follow the same format as active-project-x or you can make it more descriptive if you’d like. The actual text uses markdown formatting, where some basic syntax can be found here: <ins>https://www.markdownguide.org/cheat-sheet/</ins>.

Some features you may want to add within the Markdown block, could include:
-	*Adding a Relevant Publication*
  - If the publication is featured within the Publication page on the website, it is actually fairly simple to add one – all you have to do is set up a hyperlink using markdown syntax using this format:

```
pub code here 
```
  - You can see an example of this within the code under active-projects-3 (Impacts of Rainfall Seasonality on Tropical Forest Composition, Function, and Drought Response)

- *Adding a Photo Album*
  - If you have a collection of images from a project that you would like to feature underneath the relevant research, you can create a photo album which can be set up as a gallery. 
  - To get this to work you will have to leave the content page and enter the assets one, where you navigate to the media/albums folder. 
  - Within this album you should create a new folder pertaining to the research and insert the images you want preferably in .JPEG format
  - Within the Research index.md file, you can then type ```gallery code``` to have the gallery featured on the page.

### Moving Projects to Past Projects
The past projects is set up a little differently than the current projects. Instead of having a separate section for each project, old projects are featured as drop-down menus, where you can move a project to this section by simply adding the text below to the past-projects markdown block:

```
{{< spoiler text="PROJECT-TITLE/DESCRIPTION" >}}

        TEXT DESCRIBING PROJECT

        {{< /spoiler >}}
```

### Editing Publications
The publications page is likely the most intensive coding wise to update, where there are ways to auto-import publications, but since that has already been initialized when the website was first set-up, it may be easier to import publications manually. There are a few guides on the different packages that help set up the publications that I will list below, but a general guide will be given below as well:
-	<ins>https://docs.hugoblox.com/tutorial/resume/step-3/</ins> (auto-importing publications)
-	<ins>https://docs.hugoblox.com/reference/content-types/#publications</ins> (manually importing publications using Pipx)
-	<ins>https://github.com/GetRD/academic-file-converter</ins> (Git repo detailing steps on manually importing publications

To add a publication to the pre-existing publications page you will need to:

1. Use Pipx or Pip to install the academic package, which will convert .bib files to usable files.	

```
pipx install academic OR pip3 install -U academic
```

2. Navigate to the main repository folder (e.g., ~/naomibschwartz.github.io)
3. Download the reference in a .bib (Bibtex) format, which you will then import into this folder by typing

```
academic import [publication].bib content/publication/ --compact
```

	**The --compact represents an argument used to layout the content from the Bibtex, to		  learn more see the guides provided above.*

4.	Once this action has been performed, you should see a new folder created in relation to the article you are importing
5.	Within this new publication, you will see two files a cite.bib, which contains the original Bibtex citation, along with a index.md file which has converted this information into a readable markdown file for the website.
  - You should not need to edit the .bib file, but if you want to make alterations, like assigning an info bar to an author, or changing which type of publication it is (e.g., conference paper, article, etc.) you can do so in the index.md file
   
The main commands that you will likely use to modify the publication would be adding author notes, and changing the publication type. Below you can see how this formatting works, where the author notes are in a dashed list and the note is written for the corresponding author. Publication type is a numerical system, where you simply type the number relating to the type of publication, and it will automatically be sorted.

If you encounter issues, you can look through the other publications to see what is different, one issue is sometimes within the abstract there could be an apostrophe or quotation that results in an error, so if you see an error pop-up for a publication, it may be a good idea to skim the abstract for any of these syntax-related errors.

## Adding, Committing, and Pushing Edits
### Adding Edits
First use ```git status``` to see what edits are queued for a push – edits will show in red if they have yet to be committed.

The easiest way to add the edits are to type ```git add .``` the '.' means that all changes (noted in red) will be added to the push – the edits should be in green if we type the ```git status```

### Committing Edits
When committing its beneficial to tie a message to your edits so that the Git Manager can see what edits have been done when accepting the merge between your edits to the main branch, and when trying to find where conflicts are emerging from. 

So once you have added your edits, you simply type ```git commit -m [MESSAGE]``` the '-m' means you want to tie a message. Try to make it concise, so that the manager is able to see quickly what was done, because other than that the code will speak for itself!

### Pushing Edits
Now that your edits have been added, and committed, you can now push them upstream to the Git Repository. To do this type ```git push origin [branch-name]```. This will create a copy of your branch in the Git Repo that the manager can then merge with the main branch if all looks to be correct.
 
For larger commits, it may take a bit longer to push, so no worries if it doesn’t immediately happen – we can then check on the main Git Repo to see if our edits have made it there. 

We can see they have with the creation of the pull request! This will be where the manager can compare and merge the branches if there are no conflicts, and your edits can now be implemented into the website. 
  - It will take a couple moments for the website to merge and publish the edits, so don’t worry if it doesn’t appear right away – if there is an issue you will see a little alert at the top of the Repository
