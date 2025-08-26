# Kontent.ai String List Custom Element

This is a custom element for Kentico Kontent that allows you to manage a list of strings in your content items.

## Usage

### Hosting the Custom Element

You can host the custom element files on your own server or use a static hosting service. The custom element consists of an HTML file and any associated JavaScript and CSS.

### Adding the Custom Element to a Content Type

1. In Kontent.ai, go to your project and open the Content model.
2. Add a new element to a content type.
3. Choose "Custom element".
4. Enter the URL where your custom element is hosted.
5. Configure any parameters as needed (see Configuration below).

### Configuration

The custom element supports the following configuration options via parameters:

- `maxItems`: The maximum number of strings allowed in the list (default is unlimited).
- `minItems`: The minimum number of strings required (default is 0).
- `unique`: Whether the list should enforce unique strings (default is true).

Example configuration JSON:

```json
{
  "maxItems": 10,
  "minItems": 1,
  "unique": true
}
```

### Example

Once added, the custom element will display an interface allowing content editors to add, remove, and reorder strings in the list.

## Development

To develop or customize the custom element:

1. Clone the repository.
2. Modify the HTML, JavaScript, and CSS files as needed.
3. Host the files on a web server.
4. Update the URL in your Kontent.ai project to point to your hosted files.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

# Kontent.ai Custom Element – String List

A lightweight [Kontent.ai](https://kontent.ai) custom element that lets editors manage a **list of strings** directly in the content editor.

## ✨ Features
- Add and remove list items.
- **Optional validation** with a configurable **regular expression**; shows a **modal warning** and blocks invalid entries.
- Respects **read‑only** state: when the field is disabled, the input/add and remove controls are hidden and the list is read‑only.
- Full‑width, minimal UI styled with **Tailwind CSS** (via CDN).
- Values are stored as a **JSON array of strings** (stringified) in the field.

---

## 🚀 Deploy / Host

This element is a single static HTML file at `src/index.htm`. Host it anywhere over HTTPS (GitHub Pages, Netlify, Vercel, your own server, etc.).  
Example:
```
https://your-domain.example/kontent-stringlist-custom-element/src/index.htm
```

---

## ➕ Add to a Content Type

1. In **Content model**, create or edit a content type.
2. **Add element → Custom element**.
3. Set **Hosted code URL** to the deployed URL of `src/index.htm`.
4. (Optional) Add **Parameters (JSON)** – see Configuration below.
5. Save the content type.

> Note: You do **not** register custom elements globally; you configure them per content type field.

---

## ⚙️ Configuration (Parameters JSON)

This custom element supports two optional parameters:

- `pattern` — a JavaScript **regular expression string** (no leading/trailing slashes). If present, the value must match this regex to be accepted.
- `warningMessage` — the message shown in a **modal dialog** when validation fails.

**Example: validate URL “stems” (paths only)**
```json
{
  "pattern": "^\\/[A-Za-z0-9._~!$&'()*+,;=:@%-]*(?:\\/[A-Za-z0-9._~!$&'()*+,;=:@%-]*)*$",
  "warningMessage": "Please enter a valid URL stem (e.g. /products/123)"
}
```

**Example: letters only**
```json
{
  "pattern": "^[A-Za-z]+$",
  "warningMessage": "Letters only"
}
```

**Behavior notes**
- If `pattern` is missing or invalid, validation is skipped.
- When validation fails, the value is **not added** and a modal warning is shown.

---

## 🧰 Data Shape

The field stores a **stringified JSON array**.  
Example value:
```json
["apples", "bananas", "cherries"]
```

When reading the value via the Management/Delivery APIs, parse it as JSON to get the array.

---


## 🛠 Local Development

You need to serve the files over **HTTPS** for the custom element to work properly (required by Kontent.ai).

The easiest way is to use [dotnet-serve](https://github.com/natemcmaster/dotnet-serve) with HTTPS enabled:

```bash
dotnet serve -S -p 5001
```

Then open:
```
https://localhost:5001/src/index.htm
```

---

## 🔒 Read‑only / Disabled State

If the custom element field is set to **disabled** (read‑only) by workflows/permissions, the component:
- hides the input and **Add** button,
- hides **Remove** buttons,
- renders the list as read‑only.

---

## 📦 Tech Notes

- Uses the official script:
  ```html
  <script src="https://app.kontent.ai/js-api/custom-element/v1/custom-element.min.js"></script>
  ```
  API surface used: `CustomElement.init`, `CustomElement.setValue`, `CustomElement.setHeight`.
- Tailwind is included via CDN.

---

## 📄 License

MIT