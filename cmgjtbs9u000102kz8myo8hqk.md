---
title: "Fixup commits"
datePublished: Thu Oct 09 2025 19:30:43 GMT+0000 (Coordinated Universal Time)
cuid: cmgjtbs9u000102kz8myo8hqk
slug: fixup-commits
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/__ZMnefoI3k/upload/221be1ddc501d2e1e8a3f6ec7382bb8e.jpeg
tags: git, advanced-git, fixup-commits

---

Ever wondered how you change a previous commit that’s all the way back in the commit history? You can use `git commit —amend` to update the very last commit, but what about something that happened three commits ago?

This is where “fixup” commits come in really handy. They’re a little weird to use initially, but once you get your head around them, they become a really useful tool and a way to really level up your Git skills.

> It is worth mentioning at this point that you should only work with fixup commits and perform interactive rebases on branches that you’re the only contributor to (i.e. feature branches). Rebasing can cause a lot of chaos if you’re working with others, so make sure you only do this on feature branches and definitely never on `main`!

# Syntax for fixup commits

I’m going to do things slightly differently in this post and put the syntax for fixup commits upfront - this is because every article I ever read about them explains what they are and why you’d want to use them and you have to scroll alllll the way down for the syntax, which is frustrating. It’s like those online recipes that talk about how the person’s grandma always used to make this particular apple pie and it’s special because it uses a particular variety of apple and it just goes on and on, when all you want to see is the dang recipe!

Anyway, here it comes:

```bash
git commit --fixup <insert commit hash here>
```

That’s it! You will have to find the commit hash of the commit you want to edit (or fixup if you will), of course, which you can do with:

```bash
git log --oneline
```

We’ll cover that in more detail in a bit.

Once you’ve got some fixup commits ready to go, you can merge them into their respective parent commits by running:

```bash
git rebase -i <commit hash of the commit before the parent commit> --autosquash
```

Again, you can use `git log` to get the git hash.

Right, if you just wanted a refresher of the commands, you can now go away, goodbye!

For those of you who want to know the ins and outs of fixup commits, keep reading.

# What on *earth* is a fixup commit?

You know when you’re working on something and you realise you’ve made a silly syntax error, or even, let’s say, a typo. Have you ever done this?

```bash
git commit -m "Fix typo"
```

Fixup commits are here to eliminate commits like this, where you are making small changes that really should have been incorporated into previous commits.

When you make a fixup commit, all you are really doing is telling Git “this commit is actually part of this other commit over here - I’ll give you the ID so you can match them up” and Git then flags the fixup commit as belonging to that other commit. You can then merge those commits together using an interactive rebase with the autosquash option. If that all sounds like gobbledygook, let’s dig in!

# Why would I want to use a fixup commit?

Say you’ve got the following git history:

```bash
ea085b2 (HEAD -> main) Stop basket from moving when items are added to it
f0fb73f Create ProductCard component
d5108bb Add padding to button component
```

> If this view of the git history is not familiar to you, you can get it by typing `git log —oneline` in your terminal. It just shows the hash (or ID) of the commit on the left and the message on the right and is a very quick way of seeing the commits on the current branch

You realise that in commit `f0fb73f`, the one where you created that `ProductCard` component, you made a typo. You accidentally wrote `PorductCard` instead of `ProductCard`:

```javascript
export const PorductCard = () => {
  return (
    <div className={styles.productCard}>
      <img src={imgUrl} alt='' />
      <h1>{name}</h1>
      <p>
        {quantity}
      </p>
    </div>
  );
}
```

You can’t easily update that commit as it’s not the last one in the git history, so you can’t use `git commit —amend`. You could do a separate commit and give it the message “Fix typo in ProductCard”, but it doesn’t feel nice, because that change should really go in commit `f0fb73f` so that all the relevant changes are together.

Fixup commits are Git’s solution to this problem. Let’s explore how we create one.

# The anatomy of a fixup commit

To fix the typo and create a fixup commit for commit `f0fb73f` or “Create ProductCard component”, you would make your code changes - i.e. change `PorductCard` to `ProductCard`, then do the following:

```bash
git add .
git commit --fixup f0fb73f
```

This stages all the changes you have made, then creates the fixup commit.

Once that’s done, if you type `git log —oneline` again, you’ll see the following:

```bash
ae9e5d1 (HEAD -> main) fixup! Create ProductCard component
ea085b2 Stop basket from moving when items are added to it
f0fb73f Create ProductCard component
d5108bb Add padding to button component
```

See how Git has labelled our most recent commit with “fixup! Create ProductCard component”? This is special Git lingo and just means that this commit actually belongs with commit `f0fb73f`.

To get these two commits to fuse, you’ll have to run another special Git command called an “interactive rebase”, which sounds really scary but it’s actually not. Let’s get into it.

# What the heck is an “interactive rebase”?

Rebasing is kind of a whole other topic in itself, that I definitely want to write about one day, but for the purposes of fixup commits, all you need to know is that the interactive rebase is what will merge your two commits that have been marked as belonging together.

An interactive rebase command is run like this:

```bash
git rebase -i <commit hash of commit before the parent commit> --autosquash
```

In order for an interactive rebase to work, you have to find the git hash (or ID) of the commit *before* the commit you want to merge into. i.e. in our example:

```bash
ae9e5d1 (HEAD -> main) fixup! Create ProductCard component
ea085b2 Stop basket from moving when items are added to it
f0fb73f Create ProductCard component
--> d5108bb Add padding to button component
```

In this case, we have to use commit `d5108bb` “Add padding to button component”, as that is the commit just before `f0fb73f` “Create ProductCardComponent”, which is the commit we want to update with our typo fix.

So, in this case, we’ll run:

```bash
git rebase -i d5108bb --autosquash
```

Depending on the editor you’re using for Git, you’ll see some output at this point - you don’t need to worry about this too much, just accept whatever it’s telling you and exit out so that the rebase happens. Here’s a few editors and how you would deal with this:

| **Editor** | **What to do** |
| --- | --- |
| VS Code | Save and close the file |
| Vim | Type `:wq` |

Once the rebase is all done, your Git history will look like this:

```bash
9d8141f (HEAD -> main) Stop basket from moving when items are added to it
7e4ebcb Create ProductCard component
d5108bb Add padding to button component
```

The fixup commit has vanished!

If you look at the contents of the new commit, you should see that your `PorductCard` is now `ProductCard`:

```javascript
export const ProductCard = () => {
  return (
    <div className={styles.productCard}>
      <img src={imgUrl} alt='' />
      <h1>{name}</h1>
      <p>
        {quantity}
      </p>
    </div>
  );
}
```

And all is well with the world.

# Why does having a clean Git history matter?

You might say to yourself “nobody really looks at the Git history, do they?” or, if your particular project uses a “squash and merge” strategy where all the commits get merged into one giant commit into `main` you might think “all the commits will end up being merged anyway, who cares?”.

And you’re kind of right, this is an advanced thing that you might not need depending on your level of experience or your team’s use of Git. However, one day you will be debugging a Production issue and trying to figure out when a change was introduced, and that is when having an accurate and clean Git history is *incredibly* important.

This is where you’ll want to have all your commits neatly laid out and easily identifiable, so you can go through and find the commit that touches a particular component or area of the code you’re interested in, because you know that’s where the problem you’re looking at is located.

Having a clean Git history is also not just good for you, it’s also for your teammates. I feel like it’s part of being a responsible custodian of a codebase and a helpful teammate. If your Git history is clean and easy to read, it’ll make it that much easier for your team to understand what you are doing and why.

# A note about the dangers of rebasing

As you’ve seen in this article, rebasing is a really useful tool. However, it can also be very destructive and in fact, years ago, I was always told never to rebase upon pain of death because it “changes history”. I think a lot of people hear this and accept it as the law (I certainly did) because it’s easier not to think about it and just merge `main` into your feature branch when it becomes out of date.

if you’re wondering what “changing history” even means, then let me try to explain. Every time you rebase, Git will update all the hashes for the commits in the rebase, which effectively makes then totally new commits, just with the same contents. If you’ve ever rebased and noticed that on Github, you get the “we went looking for those commits and couldn’t find them anywhere” message, this is why. It makes doing a simple `git pull` impossible and you either have to reset the branch of delete it and start again.

If someone else commits to a branch and then you try and pull their commits down onto your rebased version, Git won’t be able to do it, because the commits on the server won’t be the same as the ones on your local machine - it doesn’t care that the contents of each commit is the same, it works on the basis that if the hashes don’t match, the commits are different.

So yes, if you are collaborating, stick to merging. I’d also advise not rebasing `main`, but more than that, I’d advise enabling branch protection on it so any changes have to be made by way of a pull request, because it’s just much safer all round. You do not want to be pushing commits straight to `main` in a work environment.

Public safety announcement finished, nothing more to see here!

# Tooling

If you are interested in fixup commits and use VS Code, I would highly recommend installing [the Git Lens extension](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) if you’re not already, because it makes the interactive rebase part so much nicer - it shows you a lovely graphical view of what’s going to happen and allows you to confirm with cmd+enter.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760038123521/64f559ab-fa49-4408-bb36-6dd7b3ad00c3.png align="center")

# Go forth and fixup!

I hope that was helpful - do have a go at using this very helpful technique, I think you’ll find it invaluable. Let me know if anything in this post is unclear, I really value honest feedback and I’ll be happy to try and make things clearer where I can.