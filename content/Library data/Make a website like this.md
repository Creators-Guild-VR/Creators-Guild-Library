## Overview

### Resulting workflow
- Edit the page locally on Obsidian as a simple markdown text editor
- Push changes directly from Obsidian without ever touching git
- Share the website link to the guides you create with anyone
- Add collaborators to the repository to collaborate instead of sharing files and whatnot

### General steps
- Set up a repository using the Quartz template
- Get Quartz initialized and configured
- Open the repository as an Obsidian vault and set up the git plugin
- Upload and let Quartz do the magic for you


## Prerequisites
- A [GitHub](https://github.com/) account
- [nodejs](https://nodejs.org/en)
- [git](https://git-scm.com/)
- [Github Desktop](https://desktop.github.com/download/) (simplest local git login cause fuck the new buggy console login)
- [Obsidian](https://obsidian.md/)

## Steps
1. Go to the [Quartz repository](https://github.com/jackyzha0/quartz) on GitHub and click on "Create a Template" at the top right corner![[Pasted image 20260614101526.png]]![[Pasted image 20260614101227.png]]
2. Rename branch v5 to "main" to follow git best practices, otherwise your main branch will be called v5 for absolutely no reason
	1. Go to the repository's settings 
		- ![[Pasted image 20260614103148.png]]
	2. Click on the pencil icon
		- ![[Pasted image 20260614103342.png]]
	3. Rename to main and click Rename 
		- ![[Pasted image 20260614103410.png]]
3. Delete all pull requests (they'll otherwise become clutter, it's just annoying)
	- ![[Pasted image 20260614103037.png]]
4. Got back to Settings and set up Pages
	1. Scroll through the list on the left until you find Pages
		- ![[Pasted image 20260614105357.png]]
	2. Set it to GitHub Actions and don't do anything else there 
		- ![[Pasted image 20260614105647.png]]
5. Open Github Desktop
	1. Click on the repository selection dropdown
		- ![[Pasted image 20260614101850.png]]
	2. Select Clone repository, it should display all repositories you have access to 
		- ![[Pasted image 20260614101808.png]]
6. Set up Quartz on your project
	1. Open up a nodejs terminal by pressing the Windows key and looking up "node", should pop right up
		- ![[Pasted image 20260614150958.png]]
	2. Install dependencies
		1. Navigate to your downloaded repository 
			- ![[Pasted image 20260614110240.png]]
			- `cd "REPOSITORY_PATH"`
				- if the repository is on a different drive, do `F:`, replace F with the drive's letter
			- `npm i`
	3. Run the Quartz setup by using `npx quartz create`
		1. "Obsidian" on the first option 
			- ![[Pasted image 20260614110526.png]]
		2. Empty Quartz 
			- ![[Pasted image 20260614110714.png]]
		3. Set up the URL of GitHub Pages 
			- ![[Pasted image 20260614113605.png]]
			- The naming scheme is `USERNAME.github.io/REPOSITORY_NAME/`
			- For this you need your GitHub username and your repository name
			1. Get USERNAME
				1. Got your GitHub profile
					- ![[Pasted image 20260614113704.png]]
				2. On the URL bar copy everything after the ".com/" ![[Pasted image 20260614114958.png]]
			2. Get REPOSITORY_NAME
				1. Go to your repository's GitHub page 
					- ![[Pasted image 20260614114814.png]]
				2. On the URL bar copy everything after your username ![[Pasted image 20260614114908.png]]
		- Here's the message you'll get once the setup is completed 
			![[Pasted image 20260614121928.png]]
	4. Install the necessary plugins using `npx quartz plugin install --from-config`
		- ![[Pasted image 20260614125007.png]]
	5. Run `npx quartz sync --no-push` for the first time set up (you won't need this again)
	6. Test if it's working by using `npx quartz build --serve` to build a local preview
		- Go into any browser and access localhost:8080 to see the preview
7. Set up github deployment actions to match the main branch name, on your repository's root, go to .github>workflows
	1. Add [[deploy.yml]] to .github>workflows
	2. Open `docker-build-push.yaml` and replace "v5" for "main" on line 5 and 8
	3. Open `deploy-v5.yaml` and replace "v5" for "main" on line 6
	- (yes, this is because we renamed branch v5 to main on Step 2, you can rename branch main to v5 to avoid doing this but you'll find that it's cleaner this way)
8. Open the repository as an Obsidian vault
	1. Select the second option 
		- ![[Pasted image 20260614104009.png]]
9. Set up git from Obsidian using the community plugin
	1. At the bottom of the screen click, the cog 
		- ![[Pasted image 20260614104311.png]]
	2. Go to Community plugins 
		- ![[Pasted image 20260614104341.png]]
	3. Turn on community plugins 
		- ![[Pasted image 20260614104402.png]]
	4. Browse community plugins 
		- ![[Pasted image 20260614104419.png]]
	5. Search for "git" 
		- ![[Pasted image 20260614104439.png]]
	6. Click on install 
		- ![[Pasted image 20260614104508.png]]
	7. Make sure to also click enable (the install button turns into enable) 
		- ![[Pasted image 20260614104544.png]]
		1. If you didn't click enable, you can go back to the Community Plugins menu inside setup (shown on step 9.2) and do it from there 
			- ![[Pasted image 20260614104700.png]]
	8. Use Ctrl + P and choose Git Commit and Git Push to update the data on the page, refer to [[Save updates to the library]] to handle using Git on Obsidian
		- Once you've successfully pushed the changes for the first time, you can see confirmation that the page was uploaded by going 
## Extra Data
- Every time you git push it will publish the site on your URL
- Check [[Edit this library]] for data on sharing
- You can check the URL it's posting to by checking back on the menu on step 4.2
- Everything inside the "content" folder will show up on Github pages, everything outside will not
	- ![[Pasted image 20260614104843.png]]
- For more info on how to personalize the page, check [Quartz documentation: configuration](https://quartz.jzhao.xyz/configuration)

## Sources
- [Quartz documentation: installation](https://quartz.jzhao.xyz/getting-started/installation)
- [Quartz documentation: hosting (GitHub section)](https://quartz.jzhao.xyz/hosting)
- [Quartz documentation: configuration](https://quartz.jzhao.xyz/configuration)