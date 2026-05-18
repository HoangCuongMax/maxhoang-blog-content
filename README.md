# Max Hoang Blog Content

Markdown content database for the Max Hoang website.

The Next.js website reads this repository through the GitHub API. Keep
published website records inside:

```text
09 Website Database/
|-- Blog/
|-- Awards/
|-- Events/
|-- Photos/
`-- Short Videos/
```

Set `published: true` in frontmatter to make a record live. Set
`published: false` or `status: draft` to hide it.

The website is configured to read:

```text
OBSIDIAN_VAULT_GITHUB_OWNER=HoangCuongMax
OBSIDIAN_VAULT_GITHUB_REPO=maxhoang-blog-content
OBSIDIAN_VAULT_GITHUB_BRANCH=main
OBSIDIAN_VAULT_CONTENT_PATH=09 Website Database
```
