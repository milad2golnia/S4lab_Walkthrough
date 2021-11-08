At short and simple words: **exposing .git file results in disclosuring source code**. If attacker can access source code, then he can read it completely and find a way to infiltrate our project or even more simple, he can find passwords and sensitive data which are hard coded when eveloping our application. Although **in security we shouldn't considering hiding source code as a mean to achieve security and it's recommended always to publish source code publicley**.

let's see how we can access to source code if we have .git files:

First of all we should download the .git directory:

`wget --mirror -I .git Website.com/.git/`

if we run `git status` we can see list of all lost files, and we can retrieve them simply as below:

`git checkout --`