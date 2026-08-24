# 18-740 website

Jekyll site for **https://cmu-ece18740.github.io/**. Push to `main` to deploy.

Most edits are in `_data/`.

## Which file to edit

| File | Controls |
|---|---|
| `_data/course.yml` | Term, links, meeting times, grading, policies |
| `_data/schedule.yml` | Schedule table on the home page |
| `_data/labs.yml` | Labs page |
| `_data/staff.yml` | Instructors and TAs on Course Info |
| `_data/prior_offerings.yml` | Prior Offerings page |
| `calendar.html` | Embedded Google Calendar (edit the iframe `src` for a new term) |

Each file lists its fields at the top.

## Adding a page

1. Create `foo.html` at the repo root with front matter `layout: default` and
   `title: Foo`. The layout prints the `<h1>`, so start the body with `<h2>`.
2. Add it to the menu. The nav is a single string on line 16 of
   `_layouts/default.html` -- append `|/foo.html,Foo` to it. Labels cannot
   contain commas; the loop splits items on `,`.

## YAML notes

- Quote any value containing `#`. `title: MIDTERM EXAM #1` truncates to `MIDTERM EXAM`. Use `title: "MIDTERM EXAM #1"`.
- Dates are written `2026-10-06`, not `10/6`.
- Assignment dates do not have to be class days.
- Grading weights add up to **100**. Course Info prints the total.
- `placeholder: true` on a link adds a **(placeholder)** tag and keeps the warning box on Course Info. A link with no `url:` shows **(link TBA)**.
- Indent with two spaces. Tabs break the build.

`jekyll build` prints YAML errors with line numbers.

## Archiving a semester

```
jekyll build
mkdir -p archive/fall2026
cp -R _site/* archive/fall2026/
```

Add the `url:` in `_data/prior_offerings.yml`:

```yaml
offerings:
  - term: Fall 2026
    url: /archive/fall2026/
```

Commit `archive/fall2026/`. Jekyll copies it through unchanged.

Archived pages load `/assets/style.css` from the live site, so restyling the site later also changes them. The `cp -R` above already puts a copy at `archive/fall2026/assets/style.css`. To pin the old styling, point the `<link>` in each archived page at that copy.

## Local preview

```
jekyll serve -l
```

Open **http://localhost:4000**. YAML and HTML edits reload on save. `_config.yml` changes need a restart.

Install with `gem install jekyll` if needed. The site uses no plugins or themes.

`_site/` is generated output and is gitignored. Do not edit or commit it.
