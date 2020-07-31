---
layout: default
title:  "Headcrab: July 2020 progress report"
---

## Headcrab: July 2020 progress report

About 3 weeks ago, we [started a new project](http://nbaksalyar.github.io/2020/07/12/soul-of-a-new-debugger.html) to create a new modular and composable debugger library for Rust, taking inspiration from projects such as [Delve](https://github.com/go-delve/delve) and [MDB](https://illumos.org/books/mdb/preface.html). In less than 4 weeks, we have already seen some exciting progress!

<figure>
    <img src="/static/july-update/repl.png" alt="Headcrab command line demonstration" style="width: 50%;" />
    <figcaption>Command line example: executing a debuggee and reading its registers. Example by <a href="https://github.com/bjorn3">@bjorn3</a></figcaption>
</figure>

We have started with the basics: launching debuggee processes, reading & writing memory, reading & writing CPU registers, and reading debug symbols -- doing these right is an essential prerequisite before progressing towards more complex features such as breakpoints. And there's a lot of hidden complexity in these functions, as every target platform has its own quirks and requires a separate implementation. Providing a unified, simple API to hide these quirks from a user is one of our goals for the phase 1.

Overall, there were 32 pull requests adding the following features:

- [#57](https://github.com/headcrab-rs/headcrab/pull/57) added a simple REPL/command line example (the one you see on the screen shot above!), and [#58](https://github.com/headcrab-rs/headcrab/pull/58) added some more commands.
- [#22](https://github.com/headcrab-rs/headcrab/pull/22), [#29](https://github.com/headcrab-rs/headcrab/pull/29), [#32](https://github.com/headcrab-rs/headcrab/pull/32), [#33](https://github.com/headcrab-rs/headcrab/pull/33), [#49](https://github.com/headcrab-rs/headcrab/pull/49) added new abstractions & tests for reading debuggee's memory.
- [#52](https://github.com/headcrab-rs/headcrab/pull/52) implemented a `ptrace` fallback for reading protected memory on Linux.
- [#40](https://github.com/headcrab-rs/headcrab/pull/40) added support for reading registers from a target process on Linux.
- [#62](https://github.com/headcrab-rs/headcrab/pull/62) implements a kill-on-exit function to make sure that processes started by the debugger don't linger on in the suspended state.
- [#59](https://github.com/headcrab-rs/headcrab/pull/59) added support for debugging [position-independent executables](https://en.wikipedia.org/wiki/Position-independent_code#Position-independent_executables).
- [#56](https://github.com/headcrab-rs/headcrab/pull/56) implemented helper functions to perform system calls in the context of a debuggee on Linux.
- [#47](https://github.com/headcrab-rs/headcrab/pull/47) added new functions to get a list of threads from a debuggee process.
- [#43](https://github.com/headcrab-rs/headcrab/pull/43) implemented the attach function to debug already running processes.
- [#6](https://github.com/headcrab-rs/headcrab/pull/6) implemented the basic debugger functions for the macOS target.
- [#12](https://github.com/headcrab-rs/headcrab/pull/12) started, and [#46](https://github.com/headcrab-rs/headcrab/pull/46) significantly improved implementation for reading DWARF debug symbols.
- [#15](https://github.com/headcrab-rs/headcrab/pull/15), [#19](https://github.com/headcrab-rs/headcrab/pull/19), [#25](https://github.com/headcrab-rs/headcrab/pull/25) added more documentation & guides for new contributors.
- [#2](https://github.com/headcrab-rs/headcrab/pull/2), [#5](https://github.com/headcrab-rs/headcrab/pull/5/files), [#14](https://github.com/headcrab-rs/headcrab/pull/14), [#24](https://github.com/headcrab-rs/headcrab/pull/24), [#23](https://github.com/headcrab-rs/headcrab/pull/23), [#27](https://github.com/headcrab-rs/headcrab/pull/27), [#45](https://github.com/headcrab-rs/headcrab/pull/45), and [#28](https://github.com/headcrab-rs/headcrab/pull/28) set up the build automation & continuous integration on Linux, macOS, and FreeBSD.
- [#3](https://github.com/headcrab-rs/headcrab/pull/3) implemented functions to launch a new debuggee process.

## What's next?

Here's a glimpse of what we'll be working on in the near term:

- Stack unwinding and backtraces. The implementation is already started with the pull request [#61](https://github.com/headcrab-rs/headcrab/pull/61).
- Disassembling code. This is already started by bjorn3 in [#54](https://github.com/headcrab-rs/headcrab/pull/54) and currently it's blocked by a dependency issue.
- Setting breakpoints and catching events, crashes, and signals occuring in a debuggee process.
- As not all of the functions listed above are implemented for macOS, there's a lot of catching up to do.
- Reading & writing thread-local variables.

If you want to help, you can join us in our [Zulip chat](https://headcrab.zulipchat.com/). We [welcome first-time contributors](https://github.com/headcrab-rs/headcrab/blob/master/CONTRIBUTING.md#mentoring)!  
You can also support our work on [OpenCollective](https://opencollective.com/headcrab/).

## Thank you

This month's contributors were:

<!-- use `git shortlog -s --no-merges` to generate the list of contributors -->

* Atul Bhosale
* DeltaManiac
* Egor Kovetskiy
* Fábio Botelho
* Harikrishnan Menon
* Jakub Jendryka
* Nikita Baksalyar
* bjorn3

OpenCollective backers and GitHub sponsors:

* Max Filippov
* Sean Wilson
* Serhiy Martynenko
* Viktor Bakurin

Thank you for your support!

## Newsletter

For future updates, please subscribe to the [RSS feed](/feed.xml) or to our email newsletter:

<!-- Begin Mailchimp Signup Form -->
<link href="//cdn-images.mailchimp.com/embedcode/slim-10_7.css" rel="stylesheet" type="text/css">
<style type="text/css">
 #mc_embed_signup{background:#fff; clear:left; text-align: center; }
 #mc_embed_signup input{margin: 10pt auto !important; }
 /* Add your own Mailchimp form style overrides in your site stylesheet or in this style block.
    We recommend moving this block and the preceding CSS link to the HEAD of your HTML file. */
</style>
<div id="mc_embed_signup">
<form action="https://github.us17.list-manage.com/subscribe/post?u=c178697256c455bad900e9215&amp;id=a27b5db6e6" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">
 
 <input type="email" value="" name="EMAIL" class="email" id="mce-EMAIL" placeholder="email address" required>
    <!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
    <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_c178697256c455bad900e9215_a27b5db6e6" tabindex="-1" value=""></div>
    <div class="clear"><input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
    </div>
</form>
</div>
<!--End mc_embed_signup-->
