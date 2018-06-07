githook-clang-format
====================

Don't use this. Instead, look into integrating clang-format into your editor.
- Emacs: http://clang.llvm.org/docs/ClangFormat.html
- SublimeText: https://github.com/rosshemsley/SublimeClangFormat
- Vim: https://github.com/rhysd/vim-clang-format
- Visual Studio: http://llvm.org/builds/, or use the [integrated support in Visual Studio 2017](https://blogs.msdn.microsoft.com/vcblog/2018/03/13/clangformat-support-in-visual-studio-2017-15-7-preview-1/)
- Xcode: https://github.com/travisjeffery/ClangFormat-Xcode

This script will automatically run [`clang-format`](http://clang.llvm.org/docs/ClangFormat.html) on all changed files in a commit when set as a pre-commit hook. Proceed with caution.

## Warning
Do not use this on an existing codebase that isn't already in your desired style. Doing so will lead to a string a dirty commits where your code changes are intermixed with `clang-format`'s formatting changes.

Furthermore, every developer will need to install this hook. If they don't, you will again end up with commits with a mixture of code and formatting changes.

## Installation
First, verify that `clang-format` is installed. On Linux this should be included with the regular `clang` package. For MacOSX with Homebrew, `clang-format` is available via `brew install clang-format`.

Now install `clang-format.hook` from this repository into your repo's `.git/hooks`. If you don't already have a pre-commit hook, you can simply copy `clang-format.hook` to `.git/hooks/pre-commit`. For example:

`cp githook-clang-format/clang-format.hook myrepo/.git/hooks/pre-commit`

## Usage
Once the pre-commit hook is installed, `clang-format` will be run on each file included in the commit when you run `git commit`.

By default, `clang-format` uses the LLVM style. To change this, either create a `.clang-format` file with your desired format in the top level of your repo, or set the `hooks.clangformat.style` config option in your repo. The `.clang-format` file method is preferred if you will be working with a team or will be doing any major customizations to the style.

You can generate the `.clang-format` file from your desired style (here, llvm) using:

`clang-format -style=llvm -dump-config > .clang-format`

To use the `git config` method, inside your repo do:

`git config hooks.clangformat.style llvm`
