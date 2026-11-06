# News to HTML

A client-side DOCX to CMS HTML formatter that follows the `update-news` skill conventions.

## Use

Open the GitHub Pages tool at:

`https://thanakon-kn.github.io/skill-update-fs/news-html-tool/`

Select one or more `.docx` files, choose whether to skip detected headlines, and select **Convert to HTML**. Thai and English paragraphs are separated into language outputs. Each output starts with the standard figure placeholder. Use the copy or download action to take the generated HTML into the CMS.

## Preserved content

- Paragraph boundaries and hard line breaks
- Bold, italic, and underline formatting
- Basic numbered and bulleted lists
- External hyperlinks, with `target="_blank"`
- News text stored in a labeled `เนื้อข่าว` or `Body` table cell

The tool does not rewrite or summarize text. It reads DOCX files locally in the browser; the documents are not uploaded to a server. Legacy `.doc` files are not supported.

## Files

- `index.html` — interface and accessible controls
- `styles.css` — responsive layout
- `app.js` — DOCX ZIP/XML reader and HTML formatter

No build step or third-party runtime dependency is required. GitHub Pages serves the static files from this folder.
