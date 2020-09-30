---
layout: default
title: "Headcrab: September 2020 progress report"
---

## Headcrab: September 2020 progress report

We are working towards creating a modular, composable, and modern debugger library for Rust, and this month we want to highlight some of the exciting changes that were made possible thanks to our supporters and contributors.

<table>
<tr>
    <td>
        <figure>
            <a href="https://user-images.githubusercontent.com/17426603/94335626-20b7e780-ffdd-11ea-87c1-f806d42ce61f.png">
                <img src="https://user-images.githubusercontent.com/17426603/94335626-20b7e780-ffdd-11ea-87c1-f806d42ce61f.png" width="100%" />
            </a>
            <figcaption>Imgui-based GUI example for Headcrab by <a href="https://github.com/bjorn3">@bjorn3</a></figcaption>
        </figure>
    </td>
    <td>
        <figure>
            <a href="/static/september-update/inline-source-view.png">
                <img src="/static/september-update/inline-source-view.png" width="100%" />
            </a>
            <figcaption>Inline source view by <a href="https://github.com/blitzerr">@blitzerr</a></figcaption>
        </figure>
    </td>
</tr>
</table>

### GUI example

In [pull request #114](https://github.com/headcrab-rs/headcrab/pull/114), @bjorn3 has implemented a [Dear ImGui](https://github.com/Gekkio/imgui-rs)-based graphical interface for Headcrab. It demonstrates how Headcrab functionality can be used to visualize the state of a running program. The demo shows backtrace and a source view, and it can be expanded to display more contextual information.

One of the goals of Headcrab is providing tools for domain-specific debuggers and data visualization. The Headcrab core is not opinionated about how the user interface should be presented: it can be a native GUI (like in this case), a command line application, or a browser page that communicates with the debugger through its API.

### Code injection

[Pull request #114](https://github.com/headcrab-rs/headcrab/pull/114) demonstrates how [Cranelift](https://github.com/bytecodealliance/wasmtime/tree/main/cranelift) can be used for code injection. This allows to intercept and replace functions in runtime and it has many useful applications. For example, it can be used to run code snippets in the debugger command line, or for [dynamic tracing](<https://en.wikipedia.org/wiki/Tracing_(software)>) to record information about a debuggee process.

Currently, this implementation injects the [Cranelift IR](https://cranelift.readthedocs.io/en/stable/ir.html) code, but with the help of [rustc_codegen_cranelift](https://github.com/bjorn3/rustc_codegen_cranelift) it can be expanded to code written in Rust. However, this will require a lot more work.

```
Starting program: tests/testees/hello
Stopped(Pid(10787), SIGTRAP)

> inject examples/inject_hello_world.clif
run function: 0x00007ffff7fca030 stack: 0x00007ffff7fc8ff8
Hello World from injected code!
Stopped(Pid(10787), SIGTRAP) at 0x00007ffff7fca001

> injectlib libhello_dylib.so
run function: 0x00007ffff7fc7008 stack: 0x00007ffff7fc5ff8
orig rip: 0000555555559295
Hello World from dylib!
Stopped(Pid(10787), SIGTRAP) at 0x00007ffff7fc7001

> cont
Hello, world!

Exited(Pid(10787), 0)
Exit
```

### Command line improvements

In [pull request #106](https://github.com/headcrab-rs/headcrab/pull/106), @bjorn3 added highlighting and completion for the REPL example:

<figure>
    <img src="https://user-images.githubusercontent.com/17426603/92305939-0c5b6e80-ef8c-11ea-80c8-b4c94e690924.png" width="100%" />
</figure>

This was enhanced further by @blitzerr in [PR #107](https://github.com/headcrab-rs/headcrab/pull/107), which added inline source view for the code. Now it works similarly to LLDB:

```
(headcrab) exec tests/testees/hello
Starting program: tests/testees/hello
Stopped(Pid(75698), SIGTRAP)

(headcrab) cont
Stopped(Pid(75698), SIGTRAP)
0000555555559295 core::core_arch::x86::sse2::_mm_pause /rust/src/stdarch/crates/core_arch/src/x86/sse2.rs:25
/workspaces/headcrab/tests/testees/hello.rs:7:14
    4 #[inline(never)]
    5 fn breakpoint() {
    6     // This will be patched by the debugger to be a breakpoint
>   7     unsafe { core::arch::x86_64::_mm_pause(); }
    8 }
    9
   10 #[inline(never)]
```

### Breakpoint support on Linux

In [pull request #108](https://github.com/headcrab-rs/headcrab/pull/108), [@Arthamys](https://github.com/Arthamys) implemented functions that allow to set user breakpoints, which is a cornerstone feature of any debugger. This pull request also expands the command line example and allows setting breakpoints given a memory address or a function name.

## Contributing

We always need help, so if you'd like to join, we have a [Zulip chat](https://headcrab.zulipchat.com/) where we coordinate the development. You can help in a lot of ways: ideas, developer experience, design, documentation, and code. We also welcome first-time contributors and we would be [happy to mentor you](https://github.com/headcrab-rs/headcrab/blob/master/CONTRIBUTING.md#mentoring)!

You can also support our work financially by contributing to our [OpenCollective](https://opencollective.com/headcrab/).

## Contributors

This month's contributors were:

<!-- use `git shortlog --since="last month" -s --no-merges` to generate the list of contributors -->

- Arthamys
- bjorn3
- blitzerr
- Nikita Baksalyar

## Project sponsors

We thank our sponsors, [**Embark**](https://embark.games) and [**Khonsu Labs**](https://khonsulabs.com) for supporting our project.

<a href="https://embark.games"><img src="https://images.opencollective.com/embarkstudios/5256c29/logo/128.png" /></a>
<a href="https://khonsulabs.com"><img src="https://images.opencollective.com/ectondev/f7c3ce6/logo/128.png" /></a>

OpenCollective backers for this month:

<!--
async function getBackers() {
  const resp = await fetch('https://opencollective.com/headcrab/members/users.json');
  const body = await resp.json();
  body.sort((a, b) => b.totalAmountDonated - a.totalAmountDonated);
  const members = [];
  for (const member of body) {
    if (member.isActive == true && member.role == 'BACKER') {
      members.push(`- ${member.name}`);
    }
  }
  console.log(members.join('\n'));
}
await getBackers()
-->

- repi
- Max Filippov
- Giles Cope
- Sean Wilson
- Viktor Bakurin
- David Laban
- Daniil Ryzhkov
- Anton Izmailov
- Jeff Muizelaar
- Sergey Davidoff

Thank you for your support!

## Financial transparency

We have spent **€173.57** in August, which have been paid out to individual contributors (@bjorn3, @JJendryka, @nbaksalyar).

At the end of this month, our total remaining balance is **\$207.34**.

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
