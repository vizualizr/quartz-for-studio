---
title: studio.o-m.kr
---
<img class="workstat" src="https://wakatime.com/share/@2c977ef5-79a6-45cc-94ed-1ba3005f66dd/b7daf152-86c8-487b-ae7d-f2e684b50c85.png" />

A documentation of developing an independent data storytelling blog from scratch.
## updated

```dataviewjs
// 1. 설정 항목
const LIMIT_COUNT = 5; // 화면에 표시할 최근 글 개수
const PREVIEW_LENGTH = 200; // 보여줄 본문 글자수 제한
const omittion = ["start"]; // 제외할 파일 이름 목록 (확장자 제외)

// 2. 최근 수정된 파일 가져오기 (현재 대시보드 파일 및 omittion 배열에 있는 파일 제외)
const recentPages = dv.pages()
    .where(p => 
        p.file.path !== dv.current().file.path && // 현재 대시보드 파일 제외
        !omittion.includes(p.file.name) // omittion 배열에 포함된 파일 이름 제외
    )
    .sort(p => p.file.mday, 'desc') // 수정일 기준 내림차순 정렬
    .slice(0, LIMIT_COUNT);

// 3. 각 파일의 내용을 읽어와 피드 스타일로 렌더링
for (let page of recentPages) {
    const content = await app.vault.readRaw(page.file.path);
    
    // 프론트매터(YAML 속성) 제거 처리
    let cleanContent = content;
    if (content.startsWith("---")) {
        const endFrontmatter = content.indexOf("---", 3);
        if (endFrontmatter !== -1) {
            cleanContent = content.slice(endFrontmatter + 3).trim();
        }
    }
    
    // 본문 미리보기 텍스트 자르기 및 말줄임표 처리
    const preview = cleanContent.length > PREVIEW_LENGTH 
        ? cleanContent.slice(0, PREVIEW_LENGTH) + "..." 
        : cleanContent;

    // HTML 구조로 로그 스타일 렌더링
    dv.header(3, dv.fileLink(page.file.path)); // 제목 링크
    dv.el("div", `📅 **수정일:** ${page.file.mday.toFormat("yyyy-MM-dd HH:mm")}`, { attr: { style: "font-size: 0.85em; color: gray; margin-bottom: 8px;" } }); // 날짜
    dv.el("div", preview, { attr: { style: "white-space: pre-wrap; line-height: 1.6; margin-bottom: 24px; padding-bottom: 16px; border-bottom: 1px solid var(--background-modifier-border);" } }); // 본문
}
```




