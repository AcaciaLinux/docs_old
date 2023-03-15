# Writing documentation for the AcaciaLinux Wiki

Writing docs for the AcaciaLinux Wiki requires some rules to be followed:

### References to other docs have to be absolute

If you want to reference another doc using the markdown reference, you have to prefix `/` and then supply the absolute path from the root of the wiki.
```
Home.md
installation.md
installation/article.md
installation/subcategory/subarticle.md
```
If you want to reference `subarticle.md` from `article.md`, you have to supply `/installation/subcategory/subarticle.md` to the URL. URLs that do not start with `/` get interpreted as external URLs and resolve normally.

### File naming

The docs **must** have filenames that are not separated by whitespaces because these names get converted to a URL. The style guidelines recommend to use underscores (`_`) to signal whitespaces.

Additionally file names should be lowercase, this ensures a consistent URL path.

### Subarticles

It is common to want to use subarticles when writing docs. This is possible, but it is recommended to name the subdirectory like the main article:
```
installation.md
installation/somesubarticle.md
```
This ensures a beatiful URL history: When you reference the subarticle, the URL is constructed as follows: `installation/somesubarticle` and the reference looks as follows: `[My Subarticle](/installation/somesubarticle.md)`.

### Title

The title should be of type h1, means in markdown:
```markdown
# This is a title
And this is the rest of the article...
```

### Language support

Currently, there is only limited support for language highlighting due to every language being an additional import. If you want to add an additional language highlighting, feel free to open up an issue on the [website](https://github.com/AcaciaLinux/website) repository.
