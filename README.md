# FormBuilder.js

A production-ready, reusable, plug-and-play Form Builder library (similar to PHPMailer, but for forms).

Create dynamic forms using a drag-and-drop or config-based interface, and embed them anywhere with a single line of JavaScript. Zero manual database setup required (uses JSON files by default) and works securely on any website.

## 🚀 Key Features

- **Web Builder UI**: Beautiful drag-and-drop builder to construct data collection forms.
- **9 Field Types**: Text, Email, Number, Password, Textarea, Select, Radio, Checkbox, File.
- **Validation**: Enforce required fields and formats.
- **Embed Anywhere**: Render the form on any website via a simple JavaScript tag.
- **Admin Dashboard**: Manage your generated forms and view incoming submissions safely.
- **Zero Database Setup**: Defaults to simple JSON flat-files (`forms.json` and `submissions.json`) for immediate portability.

---

## 📁 Project Structure

```text
/src
  /builder          # Form Builder UI core logic (form-builder.js, .css)
  /renderer         # Form Rendering engine (form-renderer.js, .css)
/dist               # Compiled & Minified assets for production
/api                # Node.js + Express backend handlers and JSON data storage
/examples           # Working HTML demos (dashboard, builder, and embed form)
```

---

## 🛠 Installation & Quick Start

### 1. Start the API Server

The library uses a Node.js API to process and save form configurations and submissions.

```bash
# Navigate to the API folder and start the server
npm install express cors
node api/server.js
```
*The server will run on `http://localhost:3000`.*

### 2. View the Examples

Open the `/examples/` folder in your browser:
- `builder-demo.html`: Create a new form.
- `embed-demo.html`: Paste the generated Form ID to see the form live.
- `dashboard.html`: View incoming submissions.

---

## 💻 Usage Guide

### 1. Implementing the Form Builder (Admin Side)

Include the builder CSS and JS, then initialize `FormBuilder`.

```html
<link rel="stylesheet" href="form-builder.css">
<div id="builder-container"></div>
<script src="form-builder.js"></script>

<script>
  const builder = new FormBuilder('builder-container', {
      apiEndpoint: 'http://localhost:3000/api/forms', // Your API endpoint
      onSave: (data) => {
          console.log('Form saved!', data.id);
      }
  });
</script>
```

### 2. Embedding a Form (Client Side)

To embed a generated form on an external website, add the renderer script and initialize it with your `formId`.

```html
<!-- Load the minimal CSS -->
<link rel="stylesheet" href="form-renderer.css">

<!-- The container where the form will magically appear -->
<div id="my-form-container"></div>

<!-- Load the renderer script -->
<script src="form-renderer.js"></script>
<script>
  FormRenderer.init({
      containerId: 'my-form-container',
      formId: '1711234567', // Replace with your actual form ID
      apiEndpoint: 'https://your-domain.com/api/forms'
  });
</script>
```

---

## 📡 API Reference

The Node.js server (`server.js`) natively exposes the following routes:

- `POST /api/forms`: Create a new form
- `GET /api/forms`: List all forms
- `GET /api/forms/:id`: Fetch form configuration
- `PUT /api/forms/:id`: Update existing form
- `DELETE /api/forms/:id`: Delete a form
- `POST /api/forms/:id/submissions`: Submit form data (used by renderer)
- `GET /api/forms/:id/submissions`: Retrieve submissions (used by dashboard)

---

## 🛠 Building for Production

If you modify the source code in `/src`, you can compile and minify the files into the `/dist` directory.

```bash
node build.js
```

## ⚖️ License
MIT License. Open-source and free to use.
