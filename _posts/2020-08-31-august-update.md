---
layout: default
title:  "Headcrab: August 2020 progress report"
---

## Headcrab: August 2020 progress report

We are working towards creating a modular, composable, and modern debugger library for Rust, and this month there has been a lot of exciting progress thanks to our supporters and contributors.

<figure>
    <script id="asciicast-356800" src="https://asciinema.org/a/356800.js" async></script>
    <noscript>
         <a href="https://asciinema.org/a/356800" target="_blank"><img src="https://asciinema.org/a/356800.svg" /></a>
    </noscript>
</figure>

We have extended core functionality, implementing important debugger features such as stack unwinding (which is necessary for displaying backtraces), reading of local variables, and disassembly view.

In total, this month there have been 20 pull requests:

- In [#54](https://github.com/headcrab-rs/headcrab/pull/54), @bjorn3 has added an API function to disassemble the source code. This pull request also added a new `disassemble` command for [the `repl` example](https://github.com/headcrab-rs/headcrab/blob/master/examples/repl.rs) (the one you see in the demo above).
- [#61](https://github.com/headcrab-rs/headcrab/pull/61): @bjorn3 has implemented stack unwinding functions which can be used to get backtraces. Corresponding command (`backtrace`) has been also added to the `repl` example.
- @Stupremee has implemented Rust symbols demangling in [#74](https://github.com/headcrab-rs/headcrab/pull/74).
- With [#76](https://github.com/headcrab-rs/headcrab/pull/76) and [#69](https://github.com/headcrab-rs/headcrab/pull/69), @DeltaManiac has started on implementing Headcrab functions for Windows.
- @DeltaManiac has also added a `help` command to the repl example in [#91](https://github.com/headcrab-rs/headcrab/pull/91).
- [#41](https://github.com/headcrab-rs/headcrab/pull/41): @nbaksalyar has added memory writing functions for Linux and macOS, including the protected memory overwriting for Linux (using `ptrace(2)`). [#75](https://github.com/headcrab-rs/headcrab/pull/75) added some more helper functions to read memory (e.g., `ReadMemory::read_slice` can be used for reading array values).
- [#84](https://github.com/headcrab-rs/headcrab/pull/84): @bjorn3 implemented reading of local variables (also expanding the command-line example app!).
- In [#73](https://github.com/headcrab-rs/headcrab/pull/73), @JJendryka implemented watchpoints for Linux with the use of x86_64 debug registers.
- With [#85](https://github.com/headcrab-rs/headcrab/pull/85), @fabiim has implemented a function to get a list of process threads on macOS, and [#81](https://github.com/headcrab-rs/headcrab/pull/81) made the tests more robuts on Linux.

## What's next?

Here's a glimpse of what we'll be working on next month:

- Release version 0.2.0 on crates.io.
- Better documentation and fewer barriers for new contributors.
- More example apps and use cases.
- Continue implementing target platforms support (Windows and macOS).
- Breakpoints and signals.
- Thread-local variables.

We always need help, so if you'd like to join, we have a [Zulip chat](https://headcrab.zulipchat.com/) where we coordinate the development. You can help in a lot of ways: ideas, developer experience, design, documentation, and code. We also welcome first-time contributors and we would be [happy to mentor you](https://github.com/headcrab-rs/headcrab/blob/master/CONTRIBUTING.md#mentoring)!

You can also support our work financially by contributing to our [OpenCollective](https://opencollective.com/headcrab/).

### Governance

Last but not least, we are planning to move towards more open & transparent governance model for our community.

For now, we have been following the "[Benevolent Dictator](https://communityrule.info/create/?r=1597183321596)" governance model, when the person who starts the project takes decisions and coordinate efforts, and it is natural to see in the begging when it also helps to minimize bureaucracy at a smaller scale. However, as our community grows, we have a goal of transitioning to a board-driven, inclusive decision-making framework.

## Contributors

This month's contributors were:

<!-- use `git shortlog -s --no-merges` to generate the list of contributors -->

* bjorn3
* DeltaManiac
* Fábio Botelho
* Jakub Jendryka
* Justus K
* Nikita Baksalyar
* Tobias Hunger

## Project sponsors

This month, [**Khonsu Labs**](https://khonsulabs.com) and [**Embark**](https://embark.games) have joined us as sponsors. Thank you!

<a href="https://embark.games"><img src="https://images.opencollective.com/embarkstudios/5256c29/logo/128.png" /></a>
<a href="https://khonsulabs.com"><img src="https://images.opencollective.com/ectondev/f7c3ce6/logo/128.png" /></a>

OpenCollective backers and GitHub sponsors:

* repi
* Max Filippov
* Giles Cope
* Anton Izmailov
* Sean Wilson
* Serhiy Martynenko
* Viktor Bakurin
* David Laban
* Daniil Ryzhkov
* Ivan Mir
* Jenan Wise
* Blitzerr
* Val Atamanchuk

Thank you for your support!

## Financial transparency

We have spent **€102** in July:

- **€68** have been paid out to individual contributors (@bjorn3, @JJendryka).
- **€34** were spent on the domain name registration fee (headcrab.rs).

At the end of this month, our total remaining balance is **$284**.

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
