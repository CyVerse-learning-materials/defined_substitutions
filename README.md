# 2.0 Release css/js/config files

In this repo are some configuration files needed to bring existing repos to
the Learning Center 2.0 spec.  


## 2.0 Upgraded Files

|file|Notes|Location to place in the target repo (relative to top level directory)|
|----|-----|------------------------------------|
|`triage-for-2-0-release.md`|This is a github template for issues. When the repo is ready to be evaluted for 2.0, an issue should be created using this emplate.|`./github/ISSUE_TEMPLATE/triage-for-2-0-release.md`|
|`cyverse.css`|Repo css|`misc/static/cyverse.css` |
|`cyverse.js`|Repo js|`misc/static/cyverse.js`|
|`detail-expand.css` |Repo css|`misc/static/detail-expand.css`|
|`intercom-script-for-learning.js`|Intercom js|`misc/static/intercom-script-for-learning.js`|
|`question-answer.js`|Q&A js|`misc/static/question-answer.js`|
|`jquery.tablesorter.min.js`|Repo css|`misc/static/jquery.tablesorter.min.js`|
|`cyverse_spinx_conf.py`\*|sphinx config file|`misc/cyverse_spinx_conf.py`|
|`conf.py`\*|sphinx config|`conf.py`|
|`cyverse_rst_defined_substitutions.txt`\*|list of URLS|`cyverse_rst_defined_substitutions.txt`|
|`custom_urls.txt`\*|repo-specific of URLS|`custom_urls.txt`|
|`README.md`\*|Project Readme|`README.md`|

\* - These files may have some project-specific features so you should not
automatically copy over existing files.

### Organizing repos

The script `organize_repos.sh` is designed to take a list of repo git urls
(e.g. https://github.com/CyVerse-learning-materials/trimmomatic_quickstart.git),
clone those repositories, create a branch for the new release, and commit that
branch back to GitHub

**FOR THE 2.0 RELEASE ALL WORK SHOULD BE DONE ON THE BRANCH `learning_center_2_0_release_candidate`**
Once the repo passes triage (from the 2.0 release template issue) the work
can be merged to master. Then a 2.0 release can be created.

### Upgrading a Repo to 2.0

In many cases you can automatically upgrade an existing repo to the 2.0 spec.
Here are the steps.

1. Clone this repo to a location on your computer

       $ git clone https://github.com/CyVerse-learning-materials/learning-center-2.0-release.git

2. Make a directory to contain the repo(s) you wish to upgrade

       $ mkdir repos_to_upgrade

3. In the directory you have created, clone the repo(s) you wish to upgrade

       $ cd repos_to_upgrade
       $ git clone repo_1_url.git
       $ git clone repo_2_url.git
       $ git clone repo_3_url.git

3. You should now have a directory which contains your git repository (you
   may or may not have `tree` command but as long as you have this setup you
   are fine).

       $ tree -L 1 repos_to_upgrade/

         repos_to_upgrade/
         ├── repo_1
         ├── repo_2
         └── repo_3

4. Change back into this `learning-center-2.0-release` directory

       $ cd ../learning-center-2.0-release

5. Run the upgrade script using the `-d` option to specify the directory with
   your repo(s)

        $ bash upgrade.sh -d ../repos_to_upgrade

6. This script will copy new files/versions into the repo and attempt to replace
   some of the logos and texts in existing files. **This may break the repo to
   be upgraded**. An HTML file with a preview build will be created (e.g.
   `my_repo/_build`). Please preview every page in the repo and ensure things
   look good.

7. Once you have made changes, push the needed repo back to github. Then create
   an issue (there should now be a template issue `Triage for Release`). Create
   the issue (**Please make sure the repo name is in the issue title**). Do your
   best to complete the checklist and then notify Tutorials@cyverse.org your
   repo is ready for the 2.0 release.


**FOR THE 2.0 RELEASE ALL WORK SHOULD BE DONE ON THE BRANCH `learning_center_2_0_release_candidate`**
Once the repo passes triage (from the 2.0 release template issue) the work
can be merged to master. Then a 2.0 release can be created on GitHub.  


## How to maintain links in CyVerse learning materials

CyVerse uses
[RestructuredText](https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html)
(RST) to build documentation. To add links within your documentation, RST allows
you a few ways, but the preferred way is to use a
[substitution](https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#substitution-definitions)
. Combined with the
[include](https://docutils.sourceforge.io/docs/ref/rst/directives.html#including-an-external-document-fragment) directive we can have a single page with all the URLs for links in the
documentation. If a link changes, this means you can update a single page and
fix the link everywhere it appears.

There are two places we recommend you place links

 - `cyverse_rst_defined_substitutions.txt` - This is a list of common
    CyVerse-related links (like our homepage or commonly cites URLS like
    learning center articles).
 - `custom_urls` - You can place all of the URLS particular to your repo in
    in this one file, making them easier to manage.

Not all repos will meet this standard and that's OK, although the upgrade is a
change to move towards better compliance.

### Link formatting

1. CyVerse
   [documentation templates](https://github.com/CyVerse-learning-materials)
   contain the directive (if you don't have this line add it)

       .. include:: cyverse_rst_defined_substitutions.txt

2. Your documentation template should also contain the file
   `cyverse_rst_defined_substitutions.txt`

3. As you create your documentation, add your URLs to the
       `cyverse_rst_defined_substitutions.txt` file in this format

     ````
       .. |LINK TITLE| raw:: html

        <a href="https://link.url/" target="_blank">LINK TITLE</a>

     ````

4. When you are writing your documentation, enter links by using the link title
   you have specified surrounded with the `|` character, i.e.

       |LINK TITLE|


### Tips and adding to this master file


1. Unfortunately all repos cannot automatically copy from this master file. If
   the `cyverse_rst_defined_substitutions.txt` file in this repo is newer than
   the one in your template, you will need to manually copy it. We will update
   the templates on a regular basis.

2. When adding to the `cyverse_rst_defined_substitutions.txt` file in this repo
   try to keep this alphabetical.


## Building Documentation from Scratch

**You will need the following accounts**

1. GitHub account - makes it possible to collaborate on the documentation:
    - https://github.com/

### Obtaining the template

1. Choose one of the template repositories at https://github.com/CyVerse-learning-materials/
   (these are pinned at the top of this page). Click the **Use this template**
   button. Name your repo for the name of your documentation e.g.
   *'name_tutorial'*. You may choose public or private. There is no need to
   include all branches (leave unchecked).

2. Once you have a new repo made from the template, clone this new repo
   to your local machine for editing.

        $git clone MY-TUTORIAL

### Authoring tools (local install)

In order to build our documentation you can install the authoring tools or
skip this section and use the Docker container we have built.

**You will need the following software**

1. Python (3.7 or later) - This is required for the Sphinx package that will
   build our documentation:
    - https://www.python.org/downloads/
2. If needed, install pip:
    - https://packaging.python.org/installing/#install-pip-setuptools-and-wheel
3. Sphinx - This will build our tutorials into HTML and other formats (this uses
   the Python package installer 'pip' so Python must be installed first); we
   will also install the theme we need for our documentation

   **Note** You can use the [`minimal_requirements.txt`](https://raw.githubusercontent.com/CyVerse-learning-materials/learning-center-2.0-release/master/readthedocstools/minimal_requirements.txt) in /readthedocstools to
   install these requirements. If you run into problems try this with
   the whole [`requirements.txt`](https://raw.githubusercontent.com/CyVerse-learning-materials/learning-center-2.0-release/master/readthedocstools/requirements.txt) - both of which are in the
   [learning-center-2.0-release](https://github.com/CyVerse-learning-materials/learning-center-2.0-release)
   repo (see `/readthedocstools` in that repo).

        $ pip3 install -r /readthedocstools/minimal_requirements.txt

4. git - We use git to version control our documentation and manage with GitHub
    - https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

#### Editing the template

1. Edit the **index.rst** and other files as needed. Save images or other files
   in the appropriate directories. **See the recommended style guide in the template.**

2. Since tutorials will likely span multiple pages, you can copy internal pages
   page as many times as needed. Update the table of contents at the top of the
   'index.rst' accordingly. We will have **only documentation piece per repo.**

3. Save your work such as:
    - individual pages (e.g. `index.rst`, `step2.rst`)
    - images (as `.png` files in the  the `/img` folder)
    - changes or additions to `cyverse_rst_defined_substitutions.txt` and
      `custom_urls.txt`

4. Edit the `conf.py` and `/misc/cyverse_sphinx_conf.py` files to set the
   project and author information

5. Build the tutorial:

     ````
        $ make html
     ````
    Alternatively you can make an automatically building previewing using this
    command

      ````
         $ sphinx-autobuild -b html --host 0.0.0.0 --port 8000 --poll . _build_html
      ````

6. Your HTML site will be in the `_build_html` or `_build` directory that has
   been created (you can preview this in your web browser at this time).

7. Commit your changes and push the tutorial back to GitHub.


### Authoring tools (Docker)

For your convenience, all of the documentation software has been packed in
a Docker container.

1. If needed, install Docker (See [Get Docker](https://docs.docker.com/get-docker/))
   then pull the Docker image:

     ````
        $ docker pull jasonjwilliamsny/cyverse-learning-materials-tools:1.0
     ````

2. Run the container interactively (`-it`). Map port 8000 inside the container to
   port 8000 outside (`-p 8000:8000`) and use the volume command (`-v`) to
   mount the container to a directory of your choice. This directory should be
   the place where you cloned your repo in step 1 of this section.  You will
   need to be able to open files using a web browser and use a text editor to
   edit files.

     ````
        $ docker run -it -p 8000:8000 -v LOCALDIRECTORY:/DOCKERDOCUMENTATION jasonjwilliamsny/cyverse-learning-materials-tools:1.0
     ````
4. From inside the Docker container bash terminal, navigate to the
   mounted directory (e.g. `DOCKERDOCUMENTATION`). You should see your cloned
   repository there. You can now follow the steps in the
   `Obtaining the template` section with the following modifications:

   - To preview your documentation, from **inside the docker container** use the
     following command to view build and preview your documentation. **NOTE**
     this command will only work if you are in the same directory as your
     documentation repository and you are **inside the docker container shell**.

     ````
         $ sphinx-autobuild -b html --host 0.0.0.0 --port 8000 --poll . _build_html
     ````

      You documentation should be served at http://0.0.0.0:8000. Open a web
      browser on your computer to see the preview. As you make changes
      to the documentation, the browser should automatically update within
      a few seconds of making the change.

5. Follow the directions in the "Editing the template" section above.

## Wrapping up and hosting documentation in the Learning Center

Once you have built your documentation, notify
[Tutorials@CyVerse.org](mailto:Tutorials@CyVerse.org) that your tutorial is
ready for inclusion in the main CyVerse documentation repo. We will review and
verify the contribution, and add you as a maintainer repo in the CyVerse
collection. Alternatively, you can host your tutorial independently on
ReadTheDocs following their
[instructions for importing documentation](https://docs.readthedocs.io/en/latest/getting_started.html#import-your-docs). We will also follow up about ensuring test data associated with the
documentation are available and open.

### Documentation Style Guide

*General Principles*

- Write instructions in short numbered steps
- Where possible limit step to one action; small final actions such as
  'press submit' should be separated by a semicolon
- Limit the use of screenshots; where they are needed, use ReStructured text
  directives for [substitution of images](http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#substitution-definitions)
- Use the *'raw ::html'* directive to enter hyperlinks so that they will open
  in a new tab. See each repo for an example of the code
- Example data associated with documentation should be anonymously available on
  CyVerse Data Commons (Tutorials@cyverse.org can help you with this)
- Discovery Environment applications should be directly linked to documentation
  (clicking the 'info' button on any application will give you the 'App URL')
- Atmosphere images should be directly linked to documentation
  (e.g. "atmo.cyverse.org/application/images/####"

*Specific examples*

|Instruction|Example|
|-----------|-------|
|Steps generally begin with a verb or preposition|<ul><li>Click on the button<li>Under the "Result" menu</ul>|
|Locations of files are given in absolute paths|<ul><li>/dir1/dir2/file.extension</ul>|
|Top-level menus in Discovery Environment Apps in double quotes|<ul><li>Under "Input" select...</ul>|
|Subheadings/steps in Discovery Environment Apps in single quotes|<ul><li>For 'sensitivity' enter...</ul>|
|Buttons and keywords in bold|<ul><li>Click on **Apps**<li>Select **Arabidopsis**<li>Set 'sensitivity' to **Medium**</ul>|


## Sample and test data for Learning Center materials

**ALL** materials with sample or test data on the Learning Center should be  
available with anonymous/public read access at /iplant/home/shared/cyverse_training

````
/iplant/home/shared/cyverse_training:
  C- /iplant/home/shared/cyverse_training/classrooms
  C- /iplant/home/shared/cyverse_training/cyverse_austria_training
  C- /iplant/home/shared/cyverse_training/datasets
  C- /iplant/home/shared/cyverse_training/example
  C- /iplant/home/shared/cyverse_training/manuals
  C- /iplant/home/shared/cyverse_training/platform_guides
  C- /iplant/home/shared/cyverse_training/quickstarts
  C- /iplant/home/shared/cyverse_training/tutorials
  C- /iplant/home/shared/cyverse_training/workshop_materials
````

In general, data should be in the appropriate `manuals`,`platform_guides`,
`quickstarts`, `tutorials`, or `workshop_materials` folders.
