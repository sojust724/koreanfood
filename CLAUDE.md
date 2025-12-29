# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

이 프로젝트는 **한식(Korean Food) 전문 블로그**입니다. Astro 프레임워크를 사용하며, SEO 최적화와 수익화를 목표로 합니다.

## Development Commands

All commands should be run from the project root:

```bash
npm run dev       # Start dev server at localhost:4321
npm run build     # Build production site to ./dist/
npm run preview   # Preview production build locally
npm run astro ... # Run Astro CLI commands
```

## Architecture

### Content Collections

The blog uses Astro's Content Collections API for type-safe content management:

- **Collection Definition**: `src/content.config.ts` defines the `blog` collection
- **Content Location**: All blog posts live in `src/content/blog/` as `.md` or `.mdx` files
- **Schema Validation**: Frontmatter is validated using Zod schema with required fields:
  - `title` (string)
  - `description` (string)
  - `pubDate` (date)
  - `updatedDate` (optional date)
  - `heroImage` (optional image)

### Routing

- **Dynamic Routes**: `src/pages/blog/[...slug].astro` handles individual blog posts
  - Uses `getStaticPaths()` to generate routes from the blog collection
  - Retrieves posts via `getCollection('blog')`
  - Renders content using the `render()` function from `astro:content`
- **File-based Routing**: Pages in `src/pages/` are automatically exposed as routes

### Layouts and Components

- **BlogPost Layout**: `src/layouts/BlogPost.astro` provides the blog post template
  - Handles hero images, dates, and content rendering
  - Includes scoped styles for blog post presentation
- **Reusable Components**: Located in `src/components/`
  - `BaseHead.astro` - SEO and meta tags
  - `Header.astro`, `Footer.astro` - Site navigation and footer
  - `FormattedDate.astro` - Date formatting component

### Global Configuration

- **Site Constants**: `src/consts.ts` contains global site metadata (`SITE_TITLE`, `SITE_DESCRIPTION`)
- **Astro Config**: `astro.config.mjs` configures MDX and sitemap integrations
  - Update `site` property when deploying to production

### RSS Feed

- `src/pages/rss.xml.js` generates an RSS feed for blog posts

## Key Integration Points

When adding new blog posts:
1. Create `.md` or `.mdx` files in `src/content/blog/`
2. Ensure frontmatter matches the schema in `src/content.config.ts`
3. The post will automatically appear in the blog index and generate a route

When modifying blog functionality:
- Collection schema changes: Update `src/content.config.ts`
- Post rendering: Modify `src/layouts/BlogPost.astro`
- Dynamic route logic: Edit `src/pages/blog/[...slug].astro`

---

## 블로그 콘텐츠 작성 규칙

이 블로그는 **한식 전문 수익화 블로그**입니다. 사용자가 "새글 작성"이라고 명령하면, 아래 규칙에 따라 자동으로 블로그 포스트를 작성합니다.

### 작성 규칙

1. **주제**: 매번 새로운 한식 관련 주제 선정
   - 예: 특정 음식 소개, 레시피, 식재료, 한식 문화, 맛집 리뷰 등

2. **분량**: 최소 5,000자 이상
   - 블로그 글답게 충분한 정보와 깊이 있는 내용 제공

3. **말투**: 자연스러운 한국어
   - AI 느낌이 나지 않도록 편안하고 친근한 톤 사용
   - 실제 블로거가 쓴 것처럼 개인적인 경험, 생각, 팁 포함

4. **SEO 최적화**
   - 검색 엔진 최적화를 위한 키워드 자연스럽게 포함
   - 명확한 제목과 설명(description) 작성
   - 부제목(h2, h3)을 활용한 구조화된 글

5. **이미지**
   - 글 중간에 관련 한식 사진을 **최소 1개 이상** 삽입
   - Unsplash에서 검색하여 고품질 이미지 사용
   - 이미지는 `src/assets/` 폴더에 저장하고 frontmatter의 `heroImage`에 연결

6. **파일 형식**
   - `.md` (마크다운) 형식으로 작성
   - `src/content/blog/` 폴더에 저장
   - 파일명: `YYYY-MM-DD-주제.md` 형식 권장

### Frontmatter 템플릿

```markdown
---
title: "글 제목"
description: "검색 결과에 표시될 요약 설명 (150자 이내)"
pubDate: 2025-12-29
heroImage: "../../assets/이미지파일.jpg"
---
```

### 명령어

- **"새글 작성"**: 위 규칙에 따라 새로운 블로그 포스트를 자동 생성
