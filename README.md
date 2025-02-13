# 📰 MuPDF.js 
This is a port of [MuPDF](https://mupdf.com/docs/) to javascript and webassembly, giving you the following:

- 🔥 **Blazing fast** rendering of PDFs to **PNG**, **SVG** and even **HTML**
- 💼 Run in the **web browser** or your **server**. Basically any platform that supports Webassembly!
- 🗺️ A super **simple** API that's also **completely flexible**, see below...

# 🏁 Getting Started

```bash
yarn add mupdf-js
# or
npm i mupdf-js
```

## Basic Usage

Before you do any processing, you'll need to initialise the MuPdf library:

```tsx
import createMuPdf from "mupdf-js";

async function handleSomePdf(file: File) {
  const mupdf = await createMuPdf();
  
  //...
}
```

In the *browser*, you'll most likely retrieve a [File](https://developer.mozilla.org/en-US/docs/Web/API/File) or [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) object from an html [`<input type="file">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file) tag, supplied by a user.

You'll need to convert the file firstly to an `ArrayBuffer`, then to a `Uint8Array`:

```js
import createMuPdf from "mupdf-js";

async function handleSomePdf(file) {
  const mupdf = await createMuPdf();
  const buf = await file.arrayBuffer();
  const arrayBuf = new Uint8Array(buf);
  
  //...
}
```

Once you have this, you can *load* the file into the MuPdf environment, creating a MuPdf *document*:

```js
import createMuPdf from "mupdf-js";

async function handleSomePdf(file) {
  const mupdf = await createMuPdf();
  const buf = await file.arrayBuffer();
  const arrayBuf = new Uint8Array(buf);
  const doc = pdf.load(arrayBuf);
}
```

You now have three different options to render the PDF document:

```js
import createMuPdf from "mupdf-js";

async function handleSomePdf(file) {
  const mupdf = await createMuPdf();
  const buf = await file.arrayBuffer();
  const arrayBuf = new Uint8Array(buf);
  const doc = pdf.load(arrayBuf);
  
  // Each of these returns a string:
  
  const png = mupdf.drawPageAsPNG(doc, 1, 300);
  const svg = mupdf.drawPageAsSVG(doc, 1);
  const html = mupdf.drawPageAsHTML(doc, 1);
}
```

## Conversion Options

### PNG

```js
mupdf.drawPageAsPNG(document, page, resolution);
```

Arguments:
- document: *a MuPdf document object*
- page: *the page number to be rendered, starting from 1*
- resolution: *the DPI to use for rendering the file*

Returns: *an uncompressed PNG image, encoded as a base64 data URI.*

### SVG

```js
mupdf.drawPageAsSVG(document, page);
```

Arguments:
- document: *a MuPdf document object*
- page: *the page number to be rendered, starting from 1*

Returns: *an SVG file with the PDF document rendered as image tiles.*

### HTML

```js
mupdf.drawPageAsHTML(document, page);
```

Arguments:
- document: *a MuPdf document object*
- page: *the page number to be rendered, starting from 1*

Returns: *an HTML file that uses absolute positioned elements for layout.*

# License

AGPL, subject to the [MuPDF license](https://www.mupdf.com/license.html).
