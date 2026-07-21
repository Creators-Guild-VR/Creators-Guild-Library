For this we will be using the [VRChat Creator Companion](https://vrchat.com/home/download) and [Github Desktop](https://desktop.github.com/download/).

Github desktop allows you to save iterative versions of your project, as well as share the project source files with other users. It acts as an extremely effective backup as well as collaboration tool.

Even if you are not working with other people on your project, please back it up, your files are worth it.

Please set these two software up ahead of following the steps. Github will require account creation.



1. Create a project in the VRChat Creator Companion.
	1. Select new project in the top right, then fill out the options.
	2. Once you click create project, you're all done here.
	3. Unity will open automatically and your project will be registered on the list in the VRChat Creator Companion.

![[Pasted image 20260721184705.png]]

3. Create a GitHub repo in git hub desktop.**![[Pasted image 20260721184051.png]]

4. Set the file path 1 level above your VRChat Unity project, and the name should match it exactly. 

![[Pasted image 20260721184920.png]]

5. **Add .gitignore to the project.**
	1. When using github desktop you will be prompted upon repo creation to pick a .gitignore. Pick "Unity".
	2. You can see the git ignore is selected to Unity in the above image.
	3. The git ignore tells git which files not to save and share.
	4. This is useful because engines generate a lot of files that are not important

6. Push it
	1. Click publish repository. This is basically the upload button for your project.
	2. You will be prompted to name the project and set if it is public or private (I suggest private, public will allow anyone to access your unity project source files online)
![[Pasted image 20260721185018.png|430]]
![[Pasted image 20260721185155.png|456]]

7. Add Git LFS
	1. Sometimes, you will be prompted to install Git LFS. If this happens, install it.
	2. LFS stands for Large File Storage. Most git projects only use code, so no storage of large files is required. However in our case we need to store textures, 3d models, audio files and more large files.
	3. We need to install Git LFS, and tell it which files to upload to LFS instead of the regular git servers. (Regular git servers do not tolerate big files).
	4. Go to the repository menu, and open in git bash (if git bash is not there, use CMD, git or whatever option is offered)
![[Pasted image 20260721185418.png]]

Now bear with me, it gets a little bit busy here but it's not difficult.

When the console opens, input:

`git lfs install`

![[Pasted image 20260721185543.png|380]]

and press enter. You can now close the console.

After you have done this, please navigate to your projects folder and locate .gitattributes on the top level.

![[Pasted image 20260721185743.png]]

Open it with your text editor of choice.

Replace the contents of that text file with the this one from inside the zip, or just replace the file completely:

![[GitIgnore.zip]]

After that, back in Github Desktop, we're going to see a change in our change log. All your work since your last commit (save) will be shown here.

Let's write a commit name and press commit 1 file to main.

![[Pasted image 20260721190436.png]]

Then, press push to upload.
![[Pasted image 20260721190452.png]]

This is the same process you should follow after a work day, to save your work on github. (Commit then push)

## You are now ready to get to work on your project, safe from file loss, have fun!

(Fun fact, this entire wiki is also hosted on git, 