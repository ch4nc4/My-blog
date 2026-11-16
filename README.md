# My Blog

A personal Hugo blog using [Blank Magazine](https://github.com/codesign2020/blank-magazine).

## Requirements

- Git
- Hugo **0.158.0 or newer** (verified with 0.169.0). Standard Hugo works; Extended is optional.
- No Node.js or npm dependencies are needed.

On macOS, install Hugo with `brew install hugo`.

## Start locally

After cloning this repository, initialize its pinned theme submodule:

```sh
git submodule update --init --recursive
hugo server -D
```

Visit <http://localhost:1313/>. Hugo reloads the site when you edit content.
`-D` includes draft posts; stop the server with Ctrl+C.

When cloning a fresh checkout, `git clone --recurse-submodules <repository-url>`
also initializes the theme.

## Personalize

Edit `hugo.toml` to set the site title, author, bio, description, timezone, and
optional contact/social links. Replace the starter About page in
`content/about/_index.md` and the welcome post in `content/posts/welcome.md`.

Before publishing, set `baseURL` to your actual public URL, including its trailing
slash. It currently points to localhost for development. Hosting is not configured.
The upstream theme assumes root-relative navigation/search paths; use a domain
root for hosting unless you also adapt those paths for a subdirectory.

## Write a post

```sh
hugo new content posts/my-first-post.md
```

Edit the generated Markdown file and its front matter. New posts start with
`draft: true`; set it to `false` when ready. Use `description` for excerpts,
`categories` and `tags` for organization, and optionally `cover: "/images/photo.jpg"`
after adding the image to `static/images/`.

Set `featured: true` on one published post to choose the magazine cover story.
The starter welcome post is initially featured; clear its flag when featuring
your own post, or delete it.

## Add a photo gallery

```sh
hugo new content --kind gallery gallery/my-first-album/index.md
```

Put photos beside `index.md`:

```text
content/gallery/my-first-album/
  index.md
  01.jpg
  02.jpg
```

Edit the title and description, then set `draft: false`. The theme automatically
collects supported images in filename order and uses the first as the album cover.
The gallery is initially empty until you add your own photographs.

## Build

```sh
hugo --gc --minify
```

The static website is generated in `public/`, which is ignored by Git along with
generated resources and Hugo's lock file. RSS is available at `/index.xml`, and
the client-side search index is generated at `/index.json`.

## Theme maintenance

`themes/blank-magazine` is a Git submodule pinned to a specific upstream commit.
Keep site changes outside that directory. To deliberately update the theme:

```sh
git submodule update --remote themes/blank-magazine
hugo --gc --minify
```

Review the result and commit the changed submodule pointer with your site changes.
The theme's MIT license is retained in `themes/blank-magazine/LICENSE`.

Local Hugo template overrides in `layouts/` keep the theme's styling while:

- Providing English homepage labels and a working RSS subscription link.
- Rendering your About content without the theme's hardcoded demo biography.
- Using Hugo's current locale API in the base layout.

Some upstream gallery, taxonomy, search, and pagination labels remain in Chinese;
setting the content language alone does not translate those hardcoded labels.
They can be customized later through local template/static overrides.
