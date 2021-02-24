# Common Conventions 
1. Directory names and Python Module names to be in lower case with '_'

# Repositry structure for Python Algorithms

Master branch of UI and Algorithms would have code common(lib, util)
	    
    ~/Desktop/DEMO/DEMO_ALGO_BASE (master)
	$ dir
	algo  README_ALGO.md

	~/Desktop/DEMO/DEMO_ALGO_BASE (master)
	$ cd algo/

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ dir
	lib  README.md
	
Create a new branch for each algorithm, by cutting from a master branch which has common code (lib, util), and place algorithm in a folder.

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ git checkout -b word2vec
	Switched to a new branch 'word2vec'

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ dir
	lib  README.md

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ mkdir word2vec

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ git status
	On branch word2vec
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

			word2vec/

	nothing added to commit but untracked files present (use "git add" to track)

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ git add help.py

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ git status
	On branch word2vec
	Changes to be committed:
	  (use "git reset HEAD <file>..." to unstage)

			new file:   word2vec/help.py


	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ git commit -a -m "initializing word2vec framework"
	[word2vec 2720e81] initializing word2vec framework
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 algo/word2vec/help.py

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ git status
	On branch word2vec
	nothing to commit, working tree clean

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ git push origin word2vec
	Counting objects: 4, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (4/4), 454 bytes | 0 bytes/s, done.
	Total 4 (delta 0), reused 0 (delta 0)
	To https://github.com/Scry-Analytics/DEMO_ALGO_BASE.git
	 * [new branch]      word2vec -> word2vec

Merge changes of algorithm to master branch (Optional)

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (word2vec)
	$ git checkout master
	Switched to branch 'master'
	Your branch is up-to-date with 'origin/master'.

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ gitk --all &
	[2] 39236
	[1]   Done                    gitk

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ git branch
	* master
	  word2vec

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ git merge word2vec
	Merge made by the 'recursive' strategy.
	 algo/word2vec/help.py | 0
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 algo/word2vec/help.py

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ git status
	On branch master
	Your branch is ahead of 'origin/master' by 3 commits.
	  (use "git push" to publish your local commits)
	nothing to commit, working tree clean

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ git push origin master
	Counting objects: 3, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (3/3), 368 bytes | 0 bytes/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/Scry-Analytics/DEMO_ALGO_BASE.git
	   5bffc14..de731c3  master -> master

	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ git branch
	* master
	  word2vec
	  
	~/Desktop/DEMO/DEMO_ALGO_BASE/algo (master)
	$ ls
	lib  README.md  word2vec
	
# Create a git repositry for each solution

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git remote -v
	origin  https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git (fetch)
	origin  https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git (push)

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git branch --all
	* master
	  remotes/origin/HEAD -> origin/master
	  remotes/origin/master

	/DEMO/DEMO_SOLUTION_1 (master)
	$

# Fetch and Merge code for UI

Configure a remote origin to fetch code from remote repositry
	
	/DEMO/DEMO_SOLUTION_1 (master)
	$ git remote add demo_ui_base https://github.com/Scry-Analytics/DEMO_UI_BASE.git

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git remote -v
	demo_ui_base    https://github.com/Scry-Analytics/DEMO_UI_BASE.git (fetch)
	demo_ui_base    https://github.com/Scry-Analytics/DEMO_UI_BASE.git (push)
	origin  https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git (fetch)
	origin  https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git (push)

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git branch --all
	* master
	  remotes/origin/HEAD -> origin/master
	  remotes/origin/master

Fetch branch information of remote repositry 

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git fetch --all
	Fetching origin
	Fetching demo_ui_base
	warning: no common commits
	remote: Counting objects: 19, done.
	remote: Compressing objects: 100% (10/10), done.
	remote: Total 19 (delta 1), reused 15 (delta 0), pack-reused 0
	Unpacking objects: 100% (19/19), done.
	From https://github.com/Scry-Analytics/DEMO_UI_BASE
	 * [new branch]      master     -> demo_ui_base/master
	 * [new branch]      rolebased  -> demo_ui_base/rolebased

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git branch --all
	* master
	  remotes/demo_ui_base/master
	  remotes/demo_ui_base/rolebased
	  remotes/origin/HEAD -> origin/master
	  remotes/origin/master

	/DEMO/DEMO_SOLUTION_1 (master)
	$

Create a reference branch pointing to remote branch

Convention : Reference Branch to be used to pull latest code from remote repositry <br>
Convention : Reference Branch Name : ref_<remote_repo_name>_<remote_branch>
				
	
	/DEMO/DEMO_SOLUTION_1 (master)
	$ git branch
	* master

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git checkout -b ref_demo_ui_base_rolebased -t demo_ui_base/rolebased
	Branch ref_demo_ui_base_rolebased set up to track remote branch rolebased from demo_ui_
	base.
	Switched to a new branch 'ref_demo_ui_base_rolebased'

	/DEMO/DEMO_SOLUTION_1 (ref_demo_ui_base_rolebased)

	$ git branch
	  master
	* ref_demo_ui_base_rolebased

	/DEMO/DEMO_SOLUTION_1 (ref_demo_ui_base_rolebased)

	$ ls
	README_UI.md  ui

	/DEMO/DEMO_SOLUTION_1 (ref_demo_ui_base_rolebased)

	$ ls ui/
	auth  readme.txt  role

Switch to master branch and merge the reference branch

	$ git checkout master
	Switched to branch 'master'
	Your branch is up-to-date with 'origin/master'.

	/DEMO/DEMO_SOLUTION_1 (master)
	$ ls
	README.md

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git branch
	* master
	  ref_demo_ui_base_rolebased

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git merge ref_demo_ui_base_rolebased --allow-unrelated-histories
	Merge made by the 'recursive' strategy.
	 README_UI.md    | 1 +
	 ui/auth/auth.py | 1 +
	 ui/readme.txt   | 0
	 ui/role/auth.py | 1 +
	 4 files changed, 3 insertions(+)
	 create mode 100644 README_UI.md
	 create mode 100644 ui/auth/auth.py
	 create mode 100644 ui/readme.txt
	 create mode 100644 ui/role/auth.py

	/DEMO/DEMO_SOLUTION_1 (master)
	$ ls
	README.md  README_UI.md  ui

	/DEMO/DEMO_SOLUTION_1 (master)
	$

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git push origin master
	Counting objects: 21, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (12/12), done.
	Writing objects: 100% (21/21), 1.79 KiB | 0 bytes/s, done.
	Total 21 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), done.
	To https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git
	   7904c53..dee7a28  master -> master

	/DEMO/DEMO_SOLUTION_1 (master)
	$

# Fetch and Merge code for Algorithms

Configure a remote origin to fetch code from remote repositry

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git remote add demo_algo_base https://github.com/Scry-Analytics/DEMO_ALGO_BASE.git

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git remote -v
	demo_algo_base  https://github.com/Scry-Analytics/DEMO_ALGO_BASE.git (fetch)
	demo_algo_base  https://github.com/Scry-Analytics/DEMO_ALGO_BASE.git (push)
	demo_ui_base    https://github.com/Scry-Analytics/DEMO_UI_BASE.git (fetch)
	demo_ui_base    https://github.com/Scry-Analytics/DEMO_UI_BASE.git (push)
	origin  https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git (fetch)
	origin  https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git (push)

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git branch --all
	* master
	  ref_demo_ui_base_rolebased
	  remotes/demo_ui_base/master
	  remotes/demo_ui_base/rolebased
	  remotes/origin/HEAD -> origin/master
	  remotes/origin/master

Fetch branch information of remote repositry 

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git fetch --all
	Fetching origin
	Fetching demo_ui_base
	Fetching demo_algo_base
	warning: no common commits
	remote: Counting objects: 22, done.
	remote: Compressing objects: 100% (17/17), done.
	remote: Total 22 (delta 6), reused 18 (delta 2), pack-reused 0
	Unpacking objects: 100% (22/22), done.
	From https://github.com/Scry-Analytics/DEMO_ALGO_BASE
	 * [new branch]      doc2vec    -> demo_algo_base/doc2vec
	 * [new branch]      master     -> demo_algo_base/master
	 * [new branch]      tfidf      -> demo_algo_base/tfidf
	 * [new branch]      word2vec   -> demo_algo_base/word2vec

Create a reference branch pointing to remote branch
	Convention : Reference Branch to be used to pull latest code from remote repositry
	Convention : Reference Branch Name : ref_<remote_repo_name>_<remote_branch>
	
	/DEMO/DEMO_SOLUTION_1 (master)
	$ git checkout -b ref_demo_algo_base_word2vec -t demo_algo_base/word2vec
	Branch ref_demo_algo_base_word2vec set up to track remote branch word2vec from demo_algo_base.
	Switched to a new branch 'ref_demo_algo_base_word2vec'

	/DEMO/DEMO_SOLUTION_1 (ref_demo_algo_base_word2vec
	)
	$ ls
	algo  README_ALGO.md

	/DEMO/DEMO_SOLUTION_1 (ref_demo_algo_base_word2vec
	)
	$ ls algo/
	lib  README.md  word2vec

	/DEMO/DEMO_SOLUTION_1 (ref_demo_algo_base_word2vec
	)
	$ git branch
	  master
	* ref_demo_algo_base_word2vec
	  ref_demo_ui_base_rolebased


Switch to master branch and merge the reference branch
	$ git checkout master
	Switched to branch 'master'
	Your branch is up-to-date with 'origin/master'.

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git merge ref_demo_algo_base_word2vec --allow-unrelated-histories
	Merge made by the 'recursive' strategy.
	 README_ALGO.md         | 0
	 algo/README.md         | 2 ++
	 algo/lib/common_lib.py | 0
	 algo/word2vec/help.py  | 0
	 4 files changed, 2 insertions(+)
	 create mode 100644 README_ALGO.md
	 create mode 100644 algo/README.md
	 create mode 100644 algo/lib/common_lib.py
	 create mode 100644 algo/word2vec/help.py

	/DEMO/DEMO_SOLUTION_1 (master)
	$ git push origin master
	Counting objects: 11, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (9/9), done.
	Writing objects: 100% (11/11), 1.20 KiB | 0 bytes/s, done.
	Total 11 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), done.
	To https://github.com/Scry-Analytics/DEMO_SOLUTION_1.git
	   dee7a28..06e42b5  master -> master

	/DEMO/DEMO_SOLUTION_1 (master)
	$ ls
	algo  README.md  README_ALGO.md  README_UI.md  ui

	/DEMO/DEMO_SOLUTION_1 (master)
	$
