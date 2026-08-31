# Archived pages

Pages withdrawn from garemaplacesurgery.com.au but kept in the repo rather than
deleted.

| Folder | Was live at | Archived |
|---|---|---|
| `survey/` | garemaplacesurgery.com.au/survey/ | 31 August 2026 |

## Why this folder is named with an underscore

GitHub Pages builds this site with Jekyll, and Jekyll does not copy directories
whose name starts with `_` into the published site. That is what keeps these
pages off the live site while leaving them in the repo.

**Do not rename this folder to `archive/`** — that would republish everything in
it. Equally, if a `.nojekyll` file is ever added to the repo root, Jekyll stops
running and this folder becomes public again. Neither `.nojekyll` nor
`_config.yml` exists today, which is what makes the exclusion work.

Note the repository is public, so these files remain readable on github.com.
They are off the website, not off the internet.

## The survey form was live

`survey/index.html` posted to `https://formsubmit.co/reception@garemaplacesurgery.com.au`,
a third-party relay that emailed each submission to reception. Archiving the page
stops those emails. Nothing else on the site used that endpoint, and no submitted
data was ever stored in this repo.

The remaining feedback route for patients is the Contact Us page, which offers
`feedback@garemaplacesurgery.com.au` and (02) 6205 2222.

## Restoring a page

Unlike some of the other YourGP sites, **no path fix is needed**. Every page here
carries `<base href="/">`, so relative asset and page links resolve from the site
root whatever directory the file sits in.

```bash
git mv _archive/survey survey
```

Then put the references back — they were removed from ten pages and three
supporting files:

- The `<li>` in the **Contact Us flyout** on every page. It was the last item in
  that dropdown, so it carried `rounded-b-lg` and `pb-6 pt-3`; those classes were
  moved onto the "Feedback" item above it and need moving back.
- The `<li>` in the **footer navigation** on every page.
- The **"Take Our Survey"** button on `contact-us/index.html`, which pointed at
  `../survey/#survey-form`.
- The URL in `sitemap.xml`, the page entry in `llms.txt`, and the `## Survey`
  section plus its cross-reference in `llms-full.txt`.

`photos/survey.jpg` and `assets/data/survey/index.json` were deliberately left in
place. Both are referenced by the shared webpack bundle in `assets/js/`, and
moving them risks breaking pages that are still live.

The pre-archive state is commit `0ba2f26` plus this change.
