# runt

Run a task.

## The Instructions

If all you want to do is immediately start using `runt`, grab the [runt](https://raw.githubusercontent.com/jpnance/runt/main/runt) file from this repository, make it executable with `chmod u+x runt`, and then put it in `~/bin` (or a different place that's in your `PATH`). Off you go!

If you'd like to try it out first and be lavished with a more curated tutorial-esque experience, do this stuff:

```bash
git clone https://github.com/jpnance/runt
cd runt
PATH="$PWD:$PATH" bash
```

This will set up a quasi-sandbox inside which `runt` will be executable. Try executing `runt hello`!

## The Past

Once upon a time, I got tired of typing `docker exec -it container sh -c "cd /app && whatever`, so I created a `Makefile` and made it so I could type `make whatever` instead. This was fine. One day, I needed a directory called `whatever/` so I created it. This was also fine. A few days later, though, I realized that `make whatever` didn't work the way I wanted it to anymore. Things were no longer fine. I was being mean to `make`, asking it to be a task runner when it really just wants to be a dependency manager.

The ecosystem being the way it is, the options seemed to be: a) sprinkle a bunch of `.PHONY`s in my `Makefile`; b) shoehorn my needs into `npm` scripts and enter a new circle of `package.json` hell; c) learn how to use a (very nice looking, to be honest) tool called [just](https://just.systems/); or d) just (as it were) make my own thing. Me being the way I am, I chose to just make my own thing. Here it is.

## The Present

`runt` is designed to be put into some directory in your `PATH`. I put it in `~/bin`. When you run it, it looks for a directory called `runts/` in your current working directory. Anything it sees inside that directory that's also executable is thereby deemed a "runt" that you can run with `runt <runt>`. Runts are just executable scripts; most of mine are Bash but they can be Python or Node.js or whatever else. Feel free to pass some arguments with `runt <runt> --arg -f` if you want, `runt`'s just the messenger.

No tool abuse, no awkward string escaping, no new syntax to learn.

## The Future

Here are some features that I think fit the scope of this project that I may implement at some point:

* Traverse up the directory tree to find the `runts/` directory so you can invoke runts from any subdirectory
* Support descriptions of runts to display on the "Available runts" screen
* Tab completion for available runts

## The Rules

I picked an MIT license because I don't care what you do with this. I don't really even know the differences between all of these licenses anymore, so go hog wild. Let me know if you use it, though!

## Frank Anticipated Questions

**Why not just use `make`?**

`make` wants to manage dependencies; it's willing to run tasks if that's what it takes to manage dependencies. The main quirk of this is that when you really only want `make`'s task-running capability, you can't have directories or files named the same thing as one of the task names because `make` thinks of that directory as a dependency under its purview. It's also tricky to pass arguments and some other little things but, for me, that was the main thing: I wanted my file structure to not have to care about my task names.

I know I could just drop `.PHONY` into my `Makefile` wherever I needed to disambiguate but that set off my hokeyometer, which is a definitely real device that I use to measure how hokey something is. If something's too hokey, I can't do it.

**Why not just use `npm run`?**

Tell me you've never actually tried to write a non-trivial `package.json` script without telling me you've never actually tried to write a non-trivial `package.json` script.

**Why not just use `just`?**

`just` looks like a great tool to me and it has a bunch of features I will definitely never bother to support in `runt`. You should probably [check it out](https://just.systems/) first. I just (sorry) didn't care to have to manage a new dependency across so many of my systems. `runt` is a dependency, yes, but it's one that I can just throw into my dotfiles that I already manage well with [chezmoi](https://www.chezmoi.io/). I also didn't want to learn a new syntax (eh, sort of, it at least looks like a `Makefile`) for what I felt were very simple needs. At the end of the day, we're just talking about little shell scripts.

**Why not just put your scripts in `bin/`?**

Yeah, this is what I did first. It works fine, I just don't really like the ergonomics of typing, say, `bin/seed-data`. I wanted the feel of `make seed-data`.

**Okay, but why this?**

I like bespoke stuff. I like code that I can understand within, say, ten minutes of reading it. I like feeling like a tool has a limited scope and that scope is clear to me. I think `runt` hits all of these things.

**Why do I have to use `runts/`?**

You don't. Change the script, I don't care. "Go hog wild", after all, is one of the rules listed above.

**Why aren't there any tests?**

For thirty-eight lines of Bash?
