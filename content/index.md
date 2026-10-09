---
publish: true
permalink: /index.md
title: studio.o-m.kr
created: 2026-09-10T04:31:34.216Z
modified: 2026-09-18T08:14:51.443Z
---
<img class="workstat" src="https://wakatime.com/share/@2c977ef5-79a6-45cc-94ed-1ba3005f66dd/b7daf152-86c8-487b-ae7d-f2e684b50c85.png" />

A documentation of developing an independent data storytelling blog from scratch.

![[updates.base]]

### Updates

```dataviewjs
const LIMIT_COUNT = 5, PREVIEW_LENGTH = 200;
const omit = { folder: ["assets/", "backoffice/"], file: ["index", "start"] };
const IMG = /!\[\[([^\]|]+)(?:\|[^\]]*)?\]\]|!\[[^\]]*\]\((?!https?:)([^)]+)\)/g;
const isImg = n => /\.(png|jpe?g|gif|webp|svg|avif)$/i.test(n);

const pages = dv.pages()
  .where(p => p.file.path !== dv.current().file.path
    && !omit.file.includes(p.file.name)
    && !omit.folder.some(f => p.file.path.startsWith(f)))
  .sort(p => p.date || p.modified || p.file.cday, "desc")
  .slice(0, LIMIT_COUNT);

for (const p of pages) {
  let text = (await app.vault.readRaw(p.file.path)).replace(/^---[\s\S]*?\n---/, "");

  const names = [...text.matchAll(IMG)].map(m => decodeURI(m[1] || m[2]).split("/").pop());
  const img = names.find(isImg);

  text = text.replace(IMG, "").replace(/^#{1,6}\s+/gm, "").replace(/\s+/g, " ").trim();
  if (text.length > PREVIEW_LENGTH) text = text.slice(0, PREVIEW_LENGTH) + "…";

  const d = p.date || p.modified || p.file.cday;
  dv.header(4, dv.fileLink(p.file.path));
  dv.el("div", d?.toFormat("yyyy-MM-dd") ?? "", { attr: { style: "font-size:.85rem;color:gray" } });

  const f = img && app.metadataCache.getFirstLinkpathDest(img, p.file.path);
  if (f) dv.paragraph(dv.func.embed(dv.fileLink(f.path)));
  dv.paragraph(text);
}
```

