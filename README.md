Download Link: https://assignmentchef.com/product/solved-cs107-lab9-using-git
<br>
After this lab, you will have

<ol>

 <li>investigated your assignment folders using git</li>

 <li>created a git repository with your partner, and worked on the repository together.</li>

 <li>practiced some git commands, and learned how to handle some typical git</li>

</ol>

Share a computer with somebody new. Discuss your favorite part of the guest lecture on Monday.

<h1>Get started</h1>

Clone the lab9 repo by using the command below.

<h1>Lab exercises</h1>

<h2>1) Investigate your assignment git directories</h2>

Both partners should take a turn at the keyboard for this exercise. For the entire quarter, your assignments have been stored in git repositories, although most of the interaction with the repositories was handled behind the scenes through the tools/sanitycheck and tools/submit scripts. Now, you are going to get a chance to investigate your previous

assignments using some of the functionality that git provides.

One partner should log into a myth machine, and change into the assign2 directory

(mywhich / scan_token / etc.), e.g.,

$ cd ~/cs107/assign2

Run the following commands, and answer the questions below on the checko form:

$ git log

(type `q` at the `:` prompt to stop the listing, or the spacebar to conti nue to scroll through the messages)

Based on the git log, what was the last date that you submitted your assignment?

$ git log –grep=”submit”

Notice that you have a list of all the commits which were generated when you submitted your assignment. If you want to just see a list of the commit messages that say “submit”, you can use the following:

The di erence between the two ways to run grep are that the rst is an internal git command, and the second simply uses the Linux grep program to nd only the lines that match the message.

Note that the log now has your latest commit. Does it also show your latest push?

Perform another git log and choose a commit that is a day or two before your nal submission. The long hex number after “commit” is the hash. Type the following, and replace the sample hash below with the commit hash you chose (use q to quit from the listing, or the spacebar to continue to scroll):

$ git diff b5d5335265b41614dfda5a7b02f0d2164bec4e42

The lines that begin with – are lines that were in the older version, and the lines that begin with + are lines that have been added since then.

Now type (again, replace the sample hash with your hash):

$ git checkout b5d5335265b41614dfda5a7b02f0d2164bec4e42

You have now “checked out” an older revision of your code. You can view the les in an editor, but you probably shouldn’t change them in this state. If you do want to use those changes, it is best to make a copy of the le, then revert back to the latest revision, as follows:

Now you are back to the latest state of your repository.

2) Create and work with a shared git repository.

In this part of the lab, you and your partner will both work on the same repository and you will both update les. You will investigate what happens when two users try to make changes to di erent les in a repository, and when they try to make changes to the same le. You should open two terminals on the lab computer (or one person can be on a laptop and the other on a lab computer, <strong>but they must be logged into the same myth machine, e.g., myth3</strong>), and each person should log in to a myth machine with their own usernames.

One of you should be student 1 below, and the other should be student 2 . You need to pick a team name (no spaces, but underscores are okay). Once you have picked a team name, replace team_name below with your team name.

Don’t worry about all of the details of the git commands — the more you use git , the more you will start to learn them (or you’ll just look them up online when you need the initialization ones, for instance).

student 1 should start in their terminal, and should type the following commands, which

create a shared repository and then pushes some initial les into it:

samples/create_repo  cd our_repo git init git add *

git commit -m “first commit” git remote add origin /tmp/team_name git push -u /tmp/team_name master chmod -R a+rwx /tmp/team_name




(note: if you accidentally forget to type the actual team name when you t ype the remote add origin command, fix it by typing: git remote set-url o rigin /tmp/the_actual_team_name)

student 2 should type the following to clone the repository:

at this point, student 2 should get an error! This happens when a user tries to push to a repository when another user has already pushed, so the changes aren’t synchronized between the two users. In this case, student 2 can simply pull and then push, and student2 will be required to add a “merge” message in an editor:

At this point, there is a “merge” error! This happens when two repository users make modi cations to the same le, and git cannot gure out how to non-destructively merge them into one le. Git modi es the le in question, and adds &lt;&lt;&lt;&lt;&lt;&lt; HEAD and &gt;&gt;&gt;&gt;&gt;&gt;&gt; hash comments to deliniate where the merge issues are. If there were a lot of changes, this can be ugly to manually merge, but you have to do the best you can. student 1 should clean things up, and then do the following:

git add README.md git commit -m “fixed up the readme in a merge”

Answer the following questions on the checko sheet:

Why is it always wise to git pull before a git push ?

Given the annoyance with the merge con ict, what do you imagine is a typical agreement between team members working on the same repository?

<h2>3) Learn the git bisect command, and how to get help</h2>

There are actually very few git commands that a typical user needs on a regular basis, and you have seen most of them today. However, git has many more features that are useful and powerful, and git has become a workhorse of the programming world.

If you need help when using git the rst place to go is simply to type

Sometimes, a bug is introduced into a repository that goes unnoticed, and it would be nice to be able to track down exactly when the bug occurred. If you can test your code, you should be able to determine if the code has the bug or not, but how do you nd the location in the repository where the bug rst occurred? One way to do it is to use the git bisect command. Type the following, and read the documentation on the command:

Next, perform another clone, as follows:

You should see that there is a problem! The correct answer should be Min first char of my arguments is b but it isn’t! The repository has hundreds of commit messages, and the error was introduced many revisions ago. Use the git bisect command to nd it.

What you do recall is that you know that the program was correct when you xed a pesky return value, so you should start with the following:

The rst commit was a good working version. Use what you learned by reading the man gitbisect page to nd the location when the bug was introduced, and then put the hash and the commit message from that commit into your lab checko form.

Hints:

To denote the farthest back good commit you know (what you found with the grep command above), you type git bisect good commit_hash and replace the commit hash withe one you found above. So, you would start as follows:

If you get the correct answer ( b ) then it is good, if you get an incorrect answer, it is bad.

Every time you type git bisect bad or git bisect good , you will get another version, which you can check as above. Eventually, you will get to the version that was the original place where the code broke.

What was the commit hash and commit message for the commit where the bug was introduced?

After you nish observing where you made the mistake, you probably want to type git bisect reset to go back to the newest version (where you could x the bug).

<h2>4) Review for Final Exam with your Lab TA</h2>

Since the midterm exam, we have covered three main topics:

Floating point numbers

Assembly Code

Heap allocation

Those three topics will comprise most of the nal exam, although you may see some questions from the beginning of the quarter, as well (suggestion: go re-do the midterm exam from scratch, and see how you do!). We will have an exam page online mid-week, but as always, studying your labs and previous assignments is the rst step.