# slim2erb

Get rid of that SLIM nonesense from a Rails application.

# Dependencies

- [gem install slim](https://github.com/slim-template/slim/blob/master/bin/slimrb)
- [gem install htmlbeautifier](https://github.com/threedaymonk/htmlbeautifier)

# Usage

This script is not perfect nor is it well-tested. I wrote it in times of need without any ambition for it to be production-ready.

If you're stuck with .html.slim files,
AND if you want to go back to good-old-erb,
AND if you didn't find any better tool,
AND if you absolutely understand what this script does (read it!)
AND if have a version control to back you up in case anything goes wrong,
THEN you can consider using this script.

Use it at your own risk.

```text
Usage: slim2erb [options]

    -h, --help          : Displays this message
    --remove-slim-files : Deletes .html.slim files after transpiling them to ERB.

This script recursively replaces all .html.slim files under your current directory by .html.erb files
Source: https://github.com/yoones/slim2erb
```

# How it works

I'm using the `slim` gem to transpile slim into erb. I don't use the `--pretty` option of `slimrb` because it produced erb outputs with a bunch of `<%= ::Temple::Utils.escape_html(...) %>` in them. To overcome this issue, I give the `disable_escape=true` option to `slimrb`, then I call `htmlbeautifier` to have a nicer output. It's not perfect (there are some newlines I don't know how to get rid of yet) but it's much better than the SLIM burden I had so far.

# Security warning

I strongly advice you make sure the transpiled code does not create any security issues in your app. For instance, make sure there are no unsafe string displayed without appropriate treatment (`html_escape` for instance).
