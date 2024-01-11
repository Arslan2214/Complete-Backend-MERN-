# Multer.js 
Multer is a Node.js middleware designed for managing multipart/form-data, commonly used for file uploads.\
Multer.js makes it easy to handel file uploads.
## Do I need Multer.js?
<div>
Multer enables you to manage both single and multiple files form HTML form. It's important to note that Multer should only be utilized when dealing with file uploads through forms, as it is specifically designed for multipart form data.
</div>

---
## Steps to use Multer.js:
####  1. Install Multer:
Install Multer using npm:

```cmd
npm install multer uuid
```

#### 2. Form Changes:
Add following attributes to form 
- `method`
- `action`
- `enctype="multipart/form-data"`\
\
Your form be like: 
```any .ejs file
<form method="post" action="/upload" enctype="multipart/form-data">
  <input type="file" name="fileToUpload" />
</form>
```
**`Note:`** **enctype="multipart/form-data"** is important, Otherwise It won't work.

#### 3. Multer.js Code
Create a file called `Multer.js` and paste following code.

```cmd
const multer = require("multer");
const { v4: uuidv4 } = require("uuid");
const path = require("path");

const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, "./public/images/uploads");    // Destination folder for Uploads
  },
  filename: function (req, file, cb) {
    const unique = uuidv4();            // Generate unique name using UUID
    cb(null, unique + path.extname(file.originalname));     // Using unique filename for Uploads
  },
});

module.exports = multer({ storage: storage });
```

#### 4. Implement to Server:
Create new route with following code. 
```any .ejs file
const upload = require("./multer");   // On top

router.post(
  "/fileUpload",
  upload.single("fileToUpload"),
  (req, res) => {
    if (req.file) {
        return res.send("File Uploaded");
    }
    res.send("No File found");
  }
);
```
**`Note:`** **upload.single("fileToUpload")** is important, Otherwise It won't work.\
In ("") we put name of input-field.

---
