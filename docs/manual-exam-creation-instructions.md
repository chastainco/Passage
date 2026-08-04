# Creating .exam Files By Hand

If you prefer using your own text editor and command line rather than the app's built-in editor, you can create `.exam` files entirely by hand. They're just gzipped tar archives containing a Markdown file (and optionally images).

---

## Step 1: Create the exam content as `exam.md`

### Metadata headers

| Header | Required | Description |
|--------|----------|-------------|
| `# Version:` | Yes | Must be `1` |
| `# Name:` | Yes | The exam title |
| `# Description:` | Yes | One-line summary |
| `# Minutes:` | No | Time limit in minutes (omit for no timer) |
| `# Category:` | No | Name of a category for organization |
| `# CategoryDescription:` | No | One-line description of the category |
| `# GradientStart:` | No | 6-character hex color for category, e.g. `FF8B00` |
| `# GradientEnd:` | No | 6-character hex color for category, e.g. `6B2E00` |
| `# Banner:` | No | Filename of a wide banner image (~2:1 ratio) |
| `# Icon:` | No | Filename of a square icon image (1:1 ratio) |

> **Note:** Some exams you receive may be locked — they can't be edited, exported, or duplicated in the app. This is set by the author inside the app, not through the file format.

Example header block:

```
# Version: 1
# Name: World Geography
# Description: Test your knowledge of countries, capitals, and landmarks
# Minutes: 30
# Category: Geography
# CategoryDescription: Countries, capitals, and landmarks
# GradientStart: 3BB270
# GradientEnd: 003D0E
```

### Question format

Each question is separated by a blank line and follows this structure:

```
## Question: What is the capital of France?
## Topics: geography, europe
## Points: 1
## Options:
- () London
- (*) Paris
- () Berlin
- () Madrid
## Explanation: Paris has been the capital of France since the 10th century.
```

#### Multiple Choice (exactly one correct)

```
- () Wrong answer
- (*) Correct answer
- () Wrong answer
- () Wrong answer
```

You must have exactly one `(*)` option.

For True/False questions, just use two options: `True` and `False`.

#### Multiple Select (one or more correct)

```
- [] Wrong answer
- [*] Correct answer 1
- [*] Correct answer 2
- [] Wrong answer
```

You must have at least one `[*]` option.

#### Short Answer

```
## Options:
    ___ your answer text here
```

The `___` prefix marks the fill-in answer. The text that follows is the expected correct answer.

For fill-in-the-blank questions, put the sentence with a blank in the question text and the expected word as the answer.

**Important rules:**

- Do **not** mix `()` and `[]` markers in a single question — pick one type
- Each question must have at least one `## Options:` block
- `## Explanation:` is optional but recommended
- `## Topics:` is optional — comma-separated list of keywords (`## Keywords:` works as an alias)
- `## Points:` defaults to `1` if omitted

### Images inside questions

Reference images using standard Markdown syntax:

```
![alt text](filename.png)
```

The filename must match an image you'll include in the archive. Use bare filenames only — no `images/` prefix or directory paths.

Images can appear in question text, option text, and explanations.

---

## Step 2: Package into a `.exam` archive

From your terminal, create a gzipped tar archive:

```bash
# Just the exam — no images
tar -czf my-exam.exam exam.md

# Exam with images
tar -czf my-exam.exam exam.md paris.png eiffel-tower.jpg
```

The resulting `.exam` file can be shared via AirDrop, email, or any file transfer method. Open it on your iPhone/iPad and the app will import it.

---

## Validation checklist

Before sharing, verify your `.exam` file:

- [ ] `# Name:` is present and not empty
- [ ] At least one question exists
- [ ] Multiple Choice questions have exactly one `(*)` correct option
- [ ] Multiple Select questions have at least one `[*]` correct option
- [ ] Short Answer questions have `___` answer text
- [ ] No option text is empty
- [ ] All image references in markdown have a matching file in the archive
- [ ] File extension is `.exam` (not `.tar.gz`)
