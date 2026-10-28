PRACTICAL 6
VERSION CONTROL AND COLLABORATIVE DEVELOPMENT
USING GIT AND GITHUB
1. Aim
To practice distributed version control by creating a repository, using branches, resolving merge conflicts, and submitting changes through GitHub Pull Requests.
2. Objectives
●	Install Git and configure the local username and email.
●	Create a GitHub repository and clone it locally.
●	Create feature branches and record changes using commits.
●	Push branches to GitHub and open Pull Requests.
●	Reproduce and resolve a merge conflict.
●	Inspect the commit graph and document the practical with screenshots.
3. Resources / Tools Required
●	Git: https://git-scm.com/
●	GitHub account: https://github.com/
●	GitHub documentation: https://docs.github.com/en/get-started
●	Git cheat sheet: https://education.github.com/git-cheat-sheet-education.pdf
●	PowerShell or another terminal and a text editor.
4. Theory
Git is a distributed version control system that records changes to files and allows multiple developers to work concurrently. A repository stores project files and their history. A commit records a snapshot of staged changes, while a branch provides an independent line of development.
GitHub hosts Git repositories online and provides collaboration features such as Pull Requests. A Pull Request proposes changes from one branch into another so that the changes can be reviewed before merging.
A merge conflict occurs when Git cannot automatically combine changes, such as when two branches edit the same lines differently. The developer must inspect the conflict, select or combine the required content, remove conflict markers, test the result, and commit the resolution.
Project continuity: The practical uses the University Document Sharing Platform from earlier practicals. A small login-page skeleton is used to demonstrate the Git workflow without building the complete platform.
5. Repository and Branch Plan
Item	Purpose
Repository	university-document-sharing-platform-practical6 (suggested name)
main	Stable branch containing accepted changes.
feature/login-page	First developer's login-page skeleton change.
feature/login-validation	Second developer's competing edit to the same lines.
Pull Request 1	Proposes the first branch into main.
Pull Request 2	Proposes the second branch; conflict is resolved before integration.

These are suggested names. Record the actual names used in your repository. The GitHub repository, branches, Pull Requests, and screenshots must be created during the practical; this report generator does not create them.
6. Step-by-Step Procedure
Step 1: Install and Configure Git
Install Git from the official website. Open PowerShell and verify the installation. Configure your own commit username and email.
git --version
git config --global user.name "Nitya Parmar"
git config --global user.email "nityaparmar1707@gmail.com"
git config --global --list

Actual terminal capture supplied by the student: Git installation and configured identity.
 
Figure 1: Git installation and configuration (example view).
Step 2: Create and Clone the Repository
Create a repository on GitHub. A suggested name is university-document-sharing-platform-practical6. Initialize it with a README, copy its HTTPS clone URL, and run the following commands from the folder where you want the project.
git clone https://github.com/YOUR-USERNAME/university-document-sharing-platform-practical6.git
cd university-document-sharing-platform-practical6
git status
git branch

Replace YOUR-USERNAME and the repository name with your actual GitHub details.
Step 3: Create the First Feature Branch
git checkout -b feature/login-page
git branch

The checkout -b command creates a new branch and switches to it. The login-page changes will be developed on this branch instead of directly on main.
 
Actual GitHub repository page supplied by the student. 
Figure 2: GitHub repository and branch plan (example view).
Step 4: Create and Commit the Login Page
Create a file named login.html in the repository folder and add the following basic HTML login-form skeleton. It is a demonstration only and does not implement real authentication.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>University Document Sharing Platform - Login</title>
</head>
<body>
    <main>
        <h1>University Document Sharing Platform</h1>
        <form id="login-form">
            <label for="email">University Email</label>
            <input id="email" name="email" type="email" required>
 
            <label for="password">Password</label>
            <input id="password" name="password" type="password" required>
 
            <button type="submit">Sign in</button>
        </form>
    </main>
</body>
</html>

Save the file and commit it:
git add login.html
git status
git commit -m "Add login page skeleton"
git log -1 --oneline

git add stages the file, git status displays the working-tree state, and git commit records the staged changes.
Step 5: Push the First Branch and Open Pull Request 1
git push -u origin feature/login-page

Open the repository on GitHub. Select Pull requests, then New pull request. Set the base branch to main and the compare branch to feature/login-page. Give the PR a clear title and description, create it, review it, and merge it into main. Record its real number and URL.
 
Figure 3: First Pull Request review (example view).
Evidence 1: First Pull Request
Paste an actual screenshot of Pull Request 1. Record its number, URL, and status.
 
Caption: See the image above; record the actual repository/PR URL and status where applicable.
Step 6: Create the Second Branch with a Conflicting Edit
The lab manual asks a partner to clone the repository and edit the same file and lines. To guarantee a conflict, create this second branch from the original main before Pull Request 1 is merged. On the partner’s computer, clone the repository and create the second branch from that original state. If you are working alone, use a second local clone to simulate the partner only if your instructor permits it.
git clone https://github.com/YOUR-USERNAME/university-document-sharing-platform-practical6.git
cd university-document-sharing-platform-practical6
git checkout main
git pull origin main
git checkout -b feature/login-validation

In login.html, change the heading line to a different version, for example: University Student Portal — Secure Login. Make sure the second branch changes the same original heading line that was present on the first branch.
git add login.html
git commit -m "Update login page heading"
git push -u origin feature/login-validation

On GitHub, open Pull Request 2 from feature/login-validation into main. Do not merge it yet. If GitHub reports no conflict, continue with the local conflict procedure in Step 7.
 
Figure 4: Second branch and Pull Request (example view).
Evidence 2: Second Branch and Pull Request
Paste actual screenshots of the second branch and Pull Request 2. Record the branch name, PR number, and URL.
 
Caption: See the image above; record the actual repository/PR URL and status where applicable.
Step 7: Reproduce and Resolve the Merge Conflict
After Pull Request 1 has been merged into main, update the second branch by merging the latest remote main into it. Because feature/login-validation was created from the earlier main and changed the same heading differently, Git should report a conflict.
git checkout feature/login-validation
git fetch origin
git merge origin/main

Open login.html. A conflict may look similar to the example below. The exact text depends on the changes in your repository.
 
Figure 5: Merge conflict in login.html (example view).
<<<<<<< HEAD
<h1>University Student Portal — Secure Login</h1>
=======
<h1>University Document Sharing Platform</h1>
>>>>>>> origin/main

The HEAD section represents the current branch version. The section after ======= represents the incoming version from origin/main. Edit the file and keep or combine the required content. For example, the two headings can be combined into one.
<h1>University Document Sharing Platform — Secure Login</h1>

Delete every conflict marker (<<<<<<<, =======, and >>>>>>>). Save the file and verify that it contains valid HTML and no conflict markers.
 
Figure 6: Resolved login.html without conflict markers (example view).
git status
git diff
git add login.html
git commit -m "Resolve login page merge conflict"
git push origin feature/login-validation




If Git says a merge is still in progress, complete the merge commit as prompted. Do not abort the merge if you intend to keep the resolution. Return to Pull Request 2, confirm that the branch is updated and the conflict is resolved, review the changes, and merge the PR into main.
Evidence 3: Conflict Before Resolution
Paste an actual screenshot of the Git conflict message and/or conflict markers.
 
Caption: See the image above; record the actual repository/PR URL and status where applicable.
Evidence 4: Resolved File and Successful Merge
Paste actual screenshots showing the resolved file without conflict markers and the successful merge of Pull Request 2.
 
Caption: See the image above; record the actual repository/PR URL and status where applicable.



Step 8: Inspect the Commit Graph
After the Pull Requests have been integrated, inspect the final repository history using the following commands.
git checkout main
git pull origin main
git log --graph --oneline --all
git branch -a
git status

The log graph displays commits across branches and references. Run the command in your own repository and capture the actual output. Do not replace the real graph with an invented example.
 
Figure 7: Git commit graph (example view).
Actual terminal evidence supplied: current main branch, remote tracking branch, initial commit, and clean/mostly clean working tree status (this is not yet the final multi-branch graph). 
Evidence 5: Final Commit Graph
Paste an actual screenshot of git log --graph --oneline --all from your repository.
 
Caption: See the image above; record the actual repository/PR URL and status where applicable.




7. Git Commands Used and Their Purpose

Command	Purpose
git --version	Checks whether Git is installed.
git config --global user.name / user.email	Configures the author identity for commits.
git clone <url>	Copies a remote repository locally.
git checkout -b <branch>	Creates and switches to a new branch.
git status	Displays the current branch and file states.
git add <file>	Stages changes for a commit.
git commit -m "message"	Records staged changes.
git push -u origin <branch>	Pushes a branch and sets its upstream.
git fetch origin	Downloads remote references without merging them.
git merge origin/main	Merges the fetched main branch into the current branch.
git diff	Displays differences between file versions or states.
git log --graph --oneline --all	Shows a compact graph of the repository's commit history.

8. Results and Observations
Complete the table after performing the practical. Record actual repository information and outcomes.
Verification Item	Actual Result / Evidence
Git installed and configured	[PASS/FAIL + evidence]
Repository created and cloned	[Actual repository URL]
At least two branches created	[Actual branch names]
First Pull Request merged	[PR number, URL, status]
Second Pull Request opened	[PR number, URL, status]
Conflict reproduced and resolved	[Describe the conflicting lines and resolution]
Second Pull Request merged	[PR status and URL]
Commit graph captured	[Screenshot filename or location]

Evidence integrity note: Screenshots of the repository, Pull Request 1, Git configuration, and current history were supplied by the student. Conflict/resolution/graph illustrations are local demonstration examples and must be replaced with screenshots from the student’s own terminal after running those steps. Pull Request 2 has not been supplied yet.
9. Evidence Checklist
●	☐ Repository URL is entered and opens correctly.
●	☐ Git installation and configuration evidence is included.
●	☐ First branch and Pull Request evidence is included.
●	☐ Second branch and Pull Request evidence is included.
●	☐ Actual conflict message or conflict markers are shown.
●	☐ Resolved file contains no conflict markers.
●	☐ Both PR statuses and merge results are recorded accurately.
●	☐ Actual commit graph screenshot is included.
●	☐ Screenshots are readable and have captions.
10. Conclusion
This practical demonstrates the collaborative Git and GitHub workflow, including repository creation, branching, commits, pushing changes, Pull Requests, and merge-conflict resolution. After the practical is performed, the repository history and screenshots provide evidence of the changes and their integration. All placeholders must be replaced with actual repository details and results before submission.
11. References
Git official website: https://git-scm.com/
GitHub documentation: https://docs.github.com/en/get-started
Git cheat sheet: https://education.github.com/git-cheat-sheet-education.pdf
