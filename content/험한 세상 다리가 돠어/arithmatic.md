Quartz is a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites. Thousands of students, developers, and teachers are [already using Quartz](https://quartz.jzhao.xyz/showcase) to publish personal notes, websites, and [digital gardens](https://jzhao.xyz/posts/networked-thought) to the web.

## 🪴 Get Started

Quartz requires **at least [Node](https://nodejs.org/) v22** and `npm` v10.9.2 to function correctly. Ensure you have these installed on your machine before continuing. See the [prerequisites](https://quartz.jzhao.xyz/getting-started/#prerequisites) for help installing them.

> GitHub users
>
> You can also use the **[GitHub template](https://github.com/jackyzha0/quartz/generate)** to create your repository in one click, then clone that instead. See [Option A](https://quartz.jzhao.xyz/getting-started/installation#option-a-use-the-github-template-recommended) in the installation guide.

```sh
# 1. Clone the Quartz repository
git clone https://github.com/jackyzha0/quartz.git
cd quartz
 
# 2. Install dependencies
npm i
 
# 3. Initialize your site (choose a template, set your base URL, import content)
npx quartz create
 
# 4. Install plugins referenced by your chosen template
npx quartz plugin install --from-config
 
# 5. Preview your site locally
npx quartz build --serve
```

Your site is now running at `http://localhost:8080`. From here:

- **[Write content](https://quartz.jzhao.xyz/authoring-content)** in the `content/` folder
- **[Push to GitHub](https://quartz.jzhao.xyz/getting-started/installation)** with `npx quartz sync`
- **[Deploy](https://quartz.jzhao.xyz/hosting)** to GitHub Pages, Cloudflare, Netlify, or Vercel

For the full walkthrough, see the [Getting Started](https://quartz.jzhao.xyz/getting-started/) guide.

### Returning User?

Already have a Quartz repository and cloning it on a new machine?

`git clone https://github.com/<your-username>/<your-repo>.gitcd <your-repo>npm cinpx quartz plugin installnpx quartz build --serve`

> Tip
>
> If you hit build errors on a fresh clone, try `npx quartz plugin install --latest` to refresh plugins to their latest versions. See [troubleshooting > Plugins fail to build on a fresh clone](https://quartz.jzhao.xyz/troubleshooting#plugins-fail-to-build-on-a-fresh-clone) for details.

## 🔧 Features

- [Obsidian compatibility](https://quartz.jzhao.xyz/features/obsidian-compatibility), [full-text search](https://quartz.jzhao.xyz/features/full-text-search), [graph view](https://quartz.jzhao.xyz/features/graph-view), [wikilinks, transclusions](https://quartz.jzhao.xyz/features/wikilinks), [Backlinks](https://quartz.jzhao.xyz/plugins/backlinks), [Latex](https://quartz.jzhao.xyz/features/latex), [syntax highlighting](https://quartz.jzhao.xyz/features/syntax-highlighting), [popover previews](https://quartz.jzhao.xyz/features/popover-previews), [Docker Support](https://quartz.jzhao.xyz/features/docker-support), [internationalization](https://quartz.jzhao.xyz/features/i18n), [comments](https://quartz.jzhao.xyz/features/comments) and [many more](https://quartz.jzhao.xyz/features/) right out of the box
- Hot-reload on configuration edits and incremental rebuilds for content edits
- Simple JSX layouts and [page components](https://quartz.jzhao.xyz/advanced/creating-components)
- [Ridiculously fast page loads](https://quartz.jzhao.xyz/features/spa-routing) and tiny bundle sizes
- Fully-customizable parsing, filtering, and page generation through [plugins](https://quartz.jzhao.xyz/advanced/making-plugins)

For a comprehensive list of features, visit the [features page](https://quartz.jzhao.xyz/features/). You can read more about the _why_ behind these features on the [philosophy](https://quartz.jzhao.xyz/philosophy) page and a technical overview on the [architecture](https://quartz.jzhao.xyz/advanced/architecture) page.

### 🚧 Troubleshooting + Updating

Having trouble with Quartz? Try searching for your issue using the search feature or check the [troubleshooting](https://quartz.jzhao.xyz/troubleshooting) page. If you haven’t already, [upgrade](https://quartz.jzhao.xyz/upgrading) to the newest version of Quartz to see if this fixes your issue.

If you’re still having trouble, feel free to [submit an issue](https://github.com/jackyzha0/quartz/issues) if you feel you found a bug or ask for help in our [Discord Community](https://discord.gg/cRFFHYye7t). You can also browse the [community](https://quartz.jzhao.xyz/community) page for third-party plugins and resources.

### references

[[험한 세상 다리가 돠어/bug report - overriding plugin options via quartz.ts file fails|bug report - overriding plugin options via quartz.ts file fails]]
