# Pelican plugin for blogging with iPython Notebooks

This fork of the original [pelican-ipythonnb](https://github.com/danielfrg/pelican-ipythonnb/) has to small modifications to the output HTML

1. It hides all input code cells by default, and provides a toggle link on the interpreter to view them
   See http://andras.nemes.com.au/blog/ for an example.
2. Any code cells that begin with #HIDE are removed from the output all together. This allows the use of code blocks that won't be visible in the static website.

## Works with

This has been tested only on the default theme notmyidea and notmyidea-cms.

## Requirements

- `pelican==3.3`
- `ipython==1.1.0`
- `bs4==4.3.2`

Also some libraries are used by `IPython.nbconvert`:
- `Sphinx==1.1.3`
- [pandoc](http://johnmacfarlane.net/pandoc/)

I recommend Python 3 because all the libraries already support it and is the main target of this plugin, python 2.7 should work in any case.

## Installation

Put the plugin (`__init__.py` and `ipythonnb.py`) inside `pelican_project/other_plugins/ipythonnb` folder.

Then in the `pelicanconf.py`:
```
MARKUP = ('md', 'ipynb')

PLUGIN_PATH = './other_plugins'
PLUGINS = ['ipythonnb']
```

If you host your site on github pages (or just git) you could use it as a submodule:

```
git submodule add git://github.com/danielfrg/pelican-ipythonnb.git plugins/ipythonnb
```

The toggle requires a javascript toggle 
## How to use it

### Option 1 (recomended)

Write the post using the iPython notebook interface, using markdown, equations, etc.

Place the `.ipynb` file in the content folder and create a new file with the
same name as the ipython notebook with extention `.ipynb-meta`. So you should have:
`my_post.ipynb` and `my_post.ipynb-meta`

The `ipynb-meta` should have the regular markdown metadata:
```
Title:
Slug:
Date:
Category:
Tags:
Author:
Summary:

```

Note the empty line at the end, you need that.

### Option 2

Open the `.ipynb` file in a text editor and should see.

```
{
    "metadata": {
        "name": "Super iPython NB"
    },
{ A_LOT_OF_OTHER_STUFF }
```

Add the metadata in the `metadata` field like this:

```
{
 "metadata": {
        "name": "Super iPython NB",
        "Title": "Blogging with iPython notebooks in pelican",
        "Date": "2013-2-16",
        "Category": "Category",
        "Tags": "tag2, tag2",
        "slug": "slug-slug-slug",
        "Author": "Me"
    },
    { A_LOT_OF_OTHER_STUFF }
```
