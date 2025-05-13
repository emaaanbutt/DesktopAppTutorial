🚀 How to Set Up a Basic Electron App and Push It to GitHub
1. Create a new repository on GitHub (give it a relevant name for your Electron app).

2. Open Visual Studio Code (VSCode).

3. Make a new folder for your app project on your computer.

4. Inside this folder, create two files: index.html and index.js.

5. Open a terminal in this folder and run the following command to initialize the project:

```bash
npm init
```
✅ Make sure your terminal is opened in the correct project directory.

6. Next, install Electron as a development dependency by running:

```bash
npm install --save-dev electron
```

✅ Again, make sure you’re still inside your project folder.

7. After installing, you’ll see a package.json file. In the "scripts" section of that file, add the following line:

```bash
"start": "electron ."
```

8. 🪟 Set Up the Electron Window
In your index.js, add the following code:

```bash
const path = require("path");
const { app, BrowserWindow, ipcMain } = require("electron");
const fs = require("fs");

let win;

function createWindow() {
  win = new BrowserWindow({
    width: 550,
    height: 600,
    webPreferences: {
      nodeIntegration: false,
      contextIsolation: true,
      preload: path.join(__dirname, "preload.js"),
    },
  });

  win.removeMenu();
  win.loadFile("index.html");
  
  ipcMain.on("load-page", (event, page) => {
    win.loadFile(page);
  });
}

app.whenReady().then(() => {
  createWindow();
  app.on("activate", () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow();
    }
  });
});

```

9. Now, create a new file named preload.js in the same folder and insert the following code:

```bash
const { contextBridge, ipcRenderer } = require("electron");

contextBridge.exposeInMainWorld("electronAPI", {
  loadPage: (page) => ipcRenderer.send("load-page", page),
});
```

10. 🗃️ Connect to GitHub
Initialize a new Git repository by running:

```bash
git init
```

✅ Again, confirm you're in the correct project folder.

11. Link your local project to your GitHub repository:

```bash
git remote add origin <your-repo-url>
```

12. To prevent uploading unnecessary or bulky files, create a .gitignore file and add this line:

```bash
node_modules/
```
(You can add more rules if needed to ignore additional files or folders.)

13. Finally, push your project to GitHub:

```bash
git add .
git commit -m "initialization"
git push -u origin main
```

14. ▶️ Run Your App
To launch your Electron app, use:

```bash
npm start
```
✅ Make sure you’re inside your project folder in the terminal.


Have fun building desktop apps ^~^🚀 

