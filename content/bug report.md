---
cover: "[[assets/max richter now we can sing.png]]"
---

![[assets/max richter now we can sing.png]]

The image above exists in the following path in my vault. The path is vault-relative.

```text
assets/max richter now we can sing.png
```

Then try to load the image with dataviewjs code block as below.

![[assets/Pasted image 20261009085129.png]]

In Obsidian, the code successes to load the image.

```dataviewjs
   dv.paragraph("![[/assets/max richter now we can sing.png]]");
```

But after export to quartz syncer, the image above is replaced with the transclude error message as below.

> Transclude of app//0d16fee2d281ed9866880851deb7515ba011/d/yonggeun/now/makr/projects/o-m.kr/studio/quartz-for-studio/content/assets/max-richter-now-we-can-sing.png1791363249281

### appendix

vault setting

![[assets/Pasted image 20261009093055.png]]