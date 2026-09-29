# Steinbrenner Lab Website Handover

This repository is the source for <https://steinbrennerlab.org>, a GitHub Pages / Jekyll site using the So Simple theme.

## Architecture

- `_config.yml` contains site-wide Jekyll settings: title, URL, theme, plugins, Google fonts, collections, footer links, analytics ID, and custom domain assumptions.
- `Gemfile` and `Gemfile.lock` define the local Jekyll/GitHub Pages build environment. Use `bundle exec` when running Jekyll commands.
- Top-level Markdown files are the main pages:
  - `index.md` is the homepage.
  - `news.md` lists posts from `_posts`.
  - `people.md` is the main lab roster page.
  - `research.md`, `publications.md`, `mentorship.md`, `lab_notes.md`, `teaching.md`, `contact.md`, `internship.md`, and `cherry_tree_genomics.md` are standalone pages.
- `_posts/` contains news posts. File names follow `YYYY-MM-DD-title.md`, and each post has YAML front matter with `layout: post`, `title`, and `date`.
- `_data/navigation.yml` controls the main navigation menu.
- `images/` contains source images used by pages. Common subfolders are:
  - `images/people/` for grads, postdocs, staff, and PI photos.
  - `images/undergrads/` for undergraduate photos.
  - `images/publications/` for publication figures.
  - `images/posts/`, `images/research/`-style files, `images/teaching/`, and similar folders for page-specific assets.
- `assets/css/main.scss` and `assets/css/main_alt.scss` contain local Sass customizations layered on top of the So Simple theme.
- `_includes/` contains local include overrides such as `head.html` and `analytics.html`.
- `_layouts/` contains local layout overrides. Most pages use theme layouts through their front matter.
- `CNAME` contains the custom domain.
- `_site/` is generated Jekyll output. It is present in the repository, but it should not be edited by hand. Rebuild it with Jekyll when needed.

Most page content is plain Markdown with embedded HTML. The embedded HTML is intentional and is used for image alignment, line breaks, and manual formatting.

## Local Build and Preview

Install dependencies once if needed:

```sh
bundle install
```

Preview locally:

```sh
bundle exec jekyll serve
```

Build the site:

```sh
bundle exec jekyll build
```

The build writes generated HTML and assets to `_site/`.

## Updating Publications

Publications are maintained manually in `publications.md`.

1. Open `publications.md`.
2. Add the new publication near the top of the list, above the previous newest publication.
3. Keep the existing style:
   - Number the entry manually.
   - Bold Steinbrenner lab authors with `<strong>...</strong>`.
   - Include year, title, journal/preprint server, DOI if available, and links.
   - Use `<br/><br/>` between entries to match the current spacing.
4. If the publication has an image, add it under `images/publications/`.
5. Reference the image with the same pattern used by existing entries, for example:

```html
<p style="margin-left: 100px;"><img src="/images/publications/example.png" class="align-left" width="500" alt=""></p>
<br/><br/>
<BR CLEAR="left">
```

6. Rebuild and preview the site with `bundle exec jekyll serve` or `bundle exec jekyll build`.

The page also links to Google Scholar for the most up-to-date publication list. That link is currently hard-coded near the top of `publications.md`.

If the new paper belongs under one of the research topic summaries, also update the relevant `Our papers on this topic` list in `research.md`. Those lists are hand-written and do not pull automatically from `publications.md`.

## Updating Current Members

The visible roster is maintained manually in `people.md`.

For a new grad student, postdoc, staff member, or PI-style profile:

1. Add a photo to `images/people/`. Aim for a reasonably cropped portrait or landscape image that still looks good at `width="300"`.
2. Open `people.md`.
3. Add a new block under `Current grads, postdocs, and staff`, using the existing pattern:

```html
<img src="/images/people/name.jpg" class="align-left" alt="" width="300">
<strong>
Full Name <br>
Role <br>
email /at/ uw.edu <br>
</strong>
Short biography paragraph.
<BR CLEAR="left">
```

4. Keep current members in the intended display order.
5. Add the person to `lab_timeline/lab_members.txt` so the lab timeline stays accurate.
6. Rebuild and preview the site.

For a new undergraduate:

1. Add the photo to `images/undergrads/`.
2. Add a compact block under `Undergraduate lab members` in `people.md`:

```html
<img src="/images/undergrads/name.jpg" class="align-left" alt="" width="200">
Full Name
<BR CLEAR="left">
```

3. Add the person to `lab_timeline/lab_members.txt`.
4. Rebuild and preview the site.

## Moving Members to Former Members

When someone leaves:

1. In `people.md`, remove them from the current-member section.
2. Add them to either `Former full-time lab members` or `Former undergraduates`.
3. In `lab_timeline/lab_members.txt`, replace `today` in their `End` column with the actual end date.
4. Set `keep` according to the timeline behavior:
   - `keep = 1` means the row appears in `lab_members.png`.
   - `keep = 0` means the row is excluded from `lab_members.png` and appears in the previous undergraduate/rotation timeline output.
5. Regenerate the timeline images and preview the site.

Older per-person pages exist in `former_members/` and `_undergrads/`. They are not the primary source for the current visible roster; use `people.md` first unless you intentionally want to maintain an individual profile page.

## Updating the Lab Timeline

The timeline at the bottom of `people.md` is the image `lab_timeline/lab_members.png`, generated from `lab_timeline/lab_members.txt`.

Important files (all in `lab_timeline/`):

- `lab_members.txt`: tab-delimited source table.
- `process_lab_members_txt.ipynb`: R notebook that reads `lab_members.txt` and writes the timeline outputs next to itself.
- `lab_members.png`: current lab timeline shown on the website.
- `previous_UG_rotations.png`: previous undergraduate/rotation timeline image.
- `previous_UG_rotations.csv`: generated data for previous undergraduate/rotation entries.
- `../_data/trainee_stats.yml`: generated trainee counts (undergraduates overall and in the past five years, postdocs, graduate students, etc.) shown in the "Mentorship by the numbers" section of `mentorship.md`. Do not edit by hand.

`lab_members.txt` columns:

- `Task`: person's name.
- `Project`: role, such as `postdoc`, `graduate student`, `technician`, `undergraduate`, or `rotation student`.
- `Start`: start date in `YYYY-MM-DD` format.
- `End`: end date in `YYYY-MM-DD` format, or `today` for current members.
- `keep`: `1` to keep in the main timeline, `0` to exclude from the main timeline.

Before regenerating the timeline, check `process_lab_members_txt.ipynb`: it has a hard-coded replacement date for rows where `End` is `today`. Update this line to the current date:

```r
date <- "YYYY-MM-DD"
```

Then run the notebook and confirm that `lab_members.png`, `previous_UG_rotations.png`, `previous_UG_rotations.csv`, and `_data/trainee_stats.yml` updated as expected. The same date is used as the "as of" date and the five-year cutoff on the Mentorship page.

## Updating News

Add a new Markdown file under `_posts/` named like:

```text
YYYY-MM-DD-short-title.md
```

Use this front matter:

```yaml
---
layout: post
title: "Post title"
date: YYYY-MM-DD 12:00:00 -0700
---
```

Write the post body below the front matter. The `news.md` page automatically lists posts using the `posts` layout, and the homepage shows the latest posts according to `posts_limit` in `index.md`.

## Deployment Notes

This is a GitHub Pages site. The usual update flow is:

1. Edit source files.
2. Run `bundle exec jekyll serve` or `bundle exec jekyll build`.
3. Check the changed pages locally.
4. Commit source changes, image assets, and any intentionally regenerated outputs.
5. Push to GitHub.

Do not hand-edit generated HTML in `_site/`; make the change in the source Markdown, Sass, data, image, or template file and rebuild.
