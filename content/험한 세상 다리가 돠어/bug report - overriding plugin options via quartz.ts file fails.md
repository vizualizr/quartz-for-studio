---
date-created: "[[Journal/2026-09-11|2026-09-11]]"
date-updated: "[[Journal/2026-09-11|2026-09-11]]"
aliases:
tags:
  - quartz
ai-sourced:
  - ai-proofed
publish: true
---
See [[index]]

> [!NOTE] A draft for github issue comment.
> I added this comment to [the github issue](https://github.com/jackyzha0/quartz/issues/2382#issuecomment-5277667457) too.

I would like to share my case and the workaround I found, as my case regarding the quartz option overriding failure via `quartz.ts` brought me here too. In my case the plugin is `explorer` and the overridden option is `filterFn`.

I understand that the @Julian-M 's initial issue occurred in `recent-notes` plugin while mine popped up from `explorer`. But as I met this issue while searching for a solution using the keywords, `quartz.ts option overriding`. So there might be someone with the same keywords may need the solution I spotted on discord. 

And hopefully this would be a chance for the team to look into the official documentation and the code sample again to make them work under the circumstances we have faced.

**Describe the bug**

I tried the example code from the official document to filter the elements within explorer plugin but it failed. The code aims `explorer` to omit several folders in my obsidian vault based on its `displayName`. 

**To Reproduce**

1. install explorer community plugin to implement the code as the official document describes.

```bash
npm install github:quartz-community/explorer --legacy-peer-deps
```

2. I pasted code from [the documentation](https://quartz.jzhao.xyz/features/explorer#advanced-examples) on `quartz.ts` file to override filtering options.

```javascript
# quartz.ts

import { loadQuartzConfig, loadQuartzLayout } from "./quartz/plugins/loader/config-loader"
import * as Externals from "./.quartz/plugins"

Externals.Explorer({
    filterFn: (node) => {
        // set containing names of everything you want to filter out
        const omit = new Set(["assets"])

        // can also use node.slug or by anything on node.data
        // note that node.data is only present for files that exist on disk
        // (e.g. implicit folder nodes that have no associated index.md)
        console.log("omit: ", omit)
        return !omit.has(node.displayName.toLowerCase())
    },
})

const config = await loadQuartzConfig()
export default config
export const layout = await loadQuartzLayout()
```

3. build 

```bash
npx quartz build --serve
```

4. confirmed no changes. 
5. check again after I deleted quartz cache folder(quartz\.quartz-cache\), `quartz\public` folder  and browser cache. But the filter doesn't work.

**Expected behavior**

The code from official document is expected to filter the folder.

**Desktop**:

Quartz Version: 5.0.0
node Version: v22.17.1
npm version: v11.3.0
OS: Windows 11
Browser: chrome

**Workaround**

I found the [NeverMinds's workaround](https://discord.com/channels/927628110009098281/1539111521232363571/1539187360879739000) from discord. I tested so far it works. s/he wrote the code as below.

```javascript
import { Explorer, ExplorerOptions } from "@quartz-community/explorer";
import { componentRegistry } from "./quartz/components/registry"

componentRegistry.setOptionOverrides("@quartz-community/explorer", {
  mapFn: (node) => {
    if (node.isFolder) {
      node.displayName = "📁 " + node.displayName
    } else {
      node.displayName = "📄 " + node.displayName
    }
    return node
  },
} as Partial<ExplorerOptions>)
```

As well as this 

```yaml
  - source: "@quartz-community/explorer"
    enabled: true
    layout:
      position: left
      priority: 50
    options:
      mapFn: |
        (node) => {
          if (node.isFolder) {
            node.displayName = "📁 " + node.displayName;
          } else {
            node.displayName = "📄 " + node.displayName;
          }
          return node;
        }
```

And I tested as below, on my environment and it worked.

```yaml
- source: "@quartz-community/explorer"
    enabled: true
    options:
      title: notes
      folderDefaultState: collapsed
      folderClickBehavior: link
      useSavedState: true
      name: my-explorer
      mapFn: |
        (node) => {
          if (node.isFolder) {
            node.displayName = "📁 " + node.displayName;
          } else {
            node.displayName = "📄 " + node.displayName;
          }
          return node;
        }
      filterFn: |
        (node) => {
          const omit = new Set(["files", "attachment", "assets", "journal"])
          return !omit.has(node.displayName.toLowerCase())
        }
    layout:
      position: left
      priority: 50
```

I also tested on `quartz.ts` file and it worked.

```javascript
import { loadQuartzConfig, loadQuartzLayout } from "./quartz/plugins/loader/config-loader"
import { componentRegistry } from "./quartz/components/registry"


componentRegistry.setOptionOverrides("@quartz-community/explorer", {
    sortFn: (a, b) => {

    },
    mapFn: (node) => {
        if (node.isFolder) {
            node.displayName = "📁 " + node.displayName
        } else {
            node.displayName = "📄 " + node.displayName
        }
        return node
    },
    filterFn: (node) => {
        // implement your function here
        // set containing names of everything you want to filter out
        const omit = new Set(["files", "attachment", "assets"])

        // can also use node.slug or by anything on node.data
        // note that node.data is only present for files that exist on disk
        // (e.g. implicit folder nodes that have no associated index.md)
        console.log("omit: ", omit)
        return !omit.has(node.displayName.toLowerCase())
    }
} as Partial<ExplorerOptions>)

const config = await loadQuartzConfig()
export default config
export const layout = await loadQuartzLayout()
```

