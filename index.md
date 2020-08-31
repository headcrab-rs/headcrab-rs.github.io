---
layout: default
title: Headcrab, a modern Rust debugger library
---

<div class="banner"><a href="/2020/08/31/august-update.html">August 2020 progress report</a></div>

<img src="/static/headcrab.svg" style="width: 220pt; float: right; margin-left: 10pt;" />

This project's goal is to provide a modern debugger library for Rust so that you could build custom debuggers specific for your application. It will be developed with modern operating systems and platforms in mind.

Our goals for the Phase 1:

* Modular API and extensibility.
* Read & modify memory of other processes and control their execution (cross-platform: x86_64 for Linux & macOS).
* Basic symbolication for Rust (read DWARF debug information and translate symbols into addresses).
* Get information about process threads.
* Read & write variables in the thread-local storage.
* Setting breakpoints at given locations.

<div style="clear: both;"></div>
