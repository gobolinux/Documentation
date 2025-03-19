# GoboLinux Documentation

Here resides the official GoboLinux Documentation.

It has been build using [Hugo Static Site Generator](https://gohugo.io/), based
on the wonderful
[Hugo Relearn Theme](https://mcshelby.github.io/hugo-theme-relearn/).

## Project Structure

You will find the documentation under `contents/` in markdown format. The
projects main stylesheet lays under `assets/css/`.

The main configuration is stored in `config.toml`.

If you need more info consult the official
[Hugo](https://gohugo.io/documentation/) and
[Hugo Relearn Theme](https://mcshelby.github.io/hugo-theme-relearn/) docs.

## How to run Documentation locally

1. Install [Hugo](https://gohugo.io/). If you are on GoboLinux simply run
   `Compile Hugo`.

2. Clone this repository _including submodules_:

```shell
git clone --recurse-submodules https://github.com/gobolinux/Documentation.git
```

3. Enter the project directory and type `hugo serve`

4. Open http://localhost:1313/ (by default)

5. That's it! Any project changes will be automatically reflected on your local
   server.

## Note to Contributors

Contributions to the documentation (residing within `content/`) are licensed
under CC BY-SA 3.0.

The project source code is licensed under the MIT License.

So feel free and even encouraged to submit your contributions! ❤️
