<h1 align="center" id="top">IE Practice 1</h1>

Table of contents:
- <a href="#part-1">Part 1</a>
- <a href="#part-2">Part 2</a>
- <a href="#part-3">Part 3</a>
- <a href="#part-4">Part 4</a>

## Part 1

First I created a file `Part1.txt` and it was full of misatakes and had and extra line which was going to be removed. In the second commit I fixed mistakes and commited. Still I didn't remove extra line. After that I removed the line and commited by the following command so that the changes be applied in the last commit.

```
$ git commit --amend
```

After that i realized the file name was supposed to be `FileA.txt` not `Part1.txt`. So I repeated the above scenario with `FileA.txt`.

<div align="right">
<a href="#top">back to top</a>
</div>

## Part 2

In this part we were going to create a `.env` file, commit and finally remove it file from history. I've created the file and commited it by this message `.env file is created`. Then I modified it and commited it again. Also, I created a file named `garbage` so that the commits won't be removed after removing `.env` file. The following line was used to remove the `.env` file.

```
$ git filter-repo --invert-paths --path Part2.env
```

before this command, we need to install the `filter-repo` like [this link](https://github.com/newren/git-filter-repo/blob/main/INSTALL.md).

### Alternative

Also, we could remove the 2 commits instead of removing just file by the following command:

```
$ git reset HEAD~2
$ git reset HEAD — hard
```

<div align="right">
<a href="#top">back to top</a>
</div>

## Part 3

In this case, we are going to somehow share repository modifications without commiting and pushing. We can use the following command to find modifications and export it as a patch file:

```
$ git diff > patchfile.patch
```

On the other side, We need to use this command to apply modifications:

```
$ git apply patchfile.patch
```

<div align="right">
<a href="#top">back to top</a>
</div>

## Part 4

In this case, we created a branch named `develope` and we needed to make three commits. After that we needed to just merge the second commit with the `master` branch. One way is using `git rebase` command. But I've found an **alternative** way to do this and it is this command:

```
$ git checkout master
$ git cherry-pick <commit hash code>
```

After this command, the graph is looked like this:

```
* ef4a14c (HEAD -> master) Commit 2
| * abc8383 (origin/develope, develope) Commit 3
| * 8cf51f8 Commit 2
| * 444f968 Commit 1
|/  
* 3a005ca (origin/master) Part 4 Begins here
```

Finally, I merged `master` and `develope` by this command:

```
$ git merge develop
```

The graph after merge looks like this:

```
*   a28d907 (HEAD -> master) Merge branch 'develope'
|\  
| * abc8383 (origin/develope, develope) Commit 3
| * 8cf51f8 Commit 2
| * 444f968 Commit 1
* | ef4a14c Commit 2
|/  
* 3a005ca (origin/master) Part 4 Begins here
```

<div align="right">
<a href="#top">back to top</a>
</div>
