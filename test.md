# This heading H1

## My Heading 2 with H2

~Lets check how it type text~
**Dont know**

+ Markdown
+ HTML
+ XML

## **Markdown Preview**

VS Code supports Markdown files out of the box. You just start writing Markdown text, save the file with the .md extension and then you can toggle the visualization of the editor between the code and the preview of the Markdown file; obviously, you can also open an existing Markdown file and start working with it. To switch between views, press ⇧⌘V in the editor. You can view the preview side-by-side (⌘K V) with the file you are editing and see changes reflected in real-time as you edit.

### **Dynamic previews and preview locking**

By default, Markdown previews automatically update to preview the currently active Markdown file:
You can lock a Markdown preview using the Markdown: Toggle Preview Locking command to keep it locked to its current Markdown document. Locked previews are indicated by [Preview] in the title:

### **Editor and preview synchronization**

VS Code automatically synchronizes the Markdown editor and the preview panes. Scroll the Markdown preview and the editor is scrolled to match the preview's viewport. Scroll the Markdown editor and the preview is scrolled to match its viewport:

You can disable scroll synchronization using the markdown.preview.scrollPreviewWithEditor and markdown.preview.scrollEditorWithPreview settings.

The currently selected line in the editor is indicated in the Markdown preview by a light gray bar in the left margin:

Additionally, double clicking an element in the Markdown preview will automatically open the editor for the file and scroll to the line nearest the clicked element.

### **Outline view**

The Outline view is a separate section in the bottom of the File Explorer. When expanded, it will show the symbol tree of the currently active editor. For Markdown files, the symbol tree is the Markdown file's header hierarchy.

The Outline view is a great way to review your document's header structure and outline.

### **Extending the Markdown preview**

Extensions can contribute custom styles and scripts to the Markdown preview to change its appearance and add new functionality. Here's a set of example extensions that customize the preview:

+ _Markdown Preview Github Styling_
+ _LaTeX Math for Markdown - Markdown+Math_
+ _Markdown Emoji_
+ _Markdown Preview with Bitbucket Styles_
  
### **Using your own CSS**

You can also use your own CSS in the Markdown preview with the "markdown.styles": [] [setting](https://code.visualstudio.com/docs/getstarted/settings).
This lists URLs for style sheets to load in the Markdown preview. These stylesheets can either be https URLs, or relative paths to local files in the current workspace.
For example, to load a stylesheet called Style.css at the root of your current workspace, use File > Preferences > Settings to bring up the workspace settings.json file and make this update:

// Place your settings in this file to overwrite default and user settings.
{
  "markdown.styles": ["style.css"]
}

### **Keep trailing whitespace in order to create line breaks**

To create [hard line breaks](https://spec.commonmark.org/0.29/#hard-line-breaks), Markdown requires two or more spaces at the end of a line. Depending on your user or workspace settings, VS Code may be configured to remove trailing whitespace. In order to keep trailing whitespace in Markdown files only, you can add these lines to your settings.json:

    { "[markdown]": {
    "files.trimTrailingWhitespace": false  }}

### **Markdown preview security**

For security reasons, VS Code restricts the content displayed in the Markdown preview. This includes disabling script execution and only allowing resources to be loaded over https.
When the Markdown preview blocks content on a page, an alert popup is shown in the top right corner of the preview window:
You can change what content is allowed in the Markdown preview by clicking on this popup or running the ___Markdown: Change preview security settings___ command in any Markdown file:
The Markdown preview security settings apply to all files in the workspace.

Here are the details about each of these security levels:

### **Strict**

This is the default setting. Only loads trusted content and disables script execution. Blocks http images.

It is strongly recommended that you keep Strict security enabled unless you have a very good reason to change it AND you trust all markdown files in the workspace.

### **Snippets for Markdown**

There are several built-in Markdown snippets included in VS Code - press ⌃Space (Trigger Suggest) and you get a context specific list of suggestions.

 ~ __Tip:__ You can add in your own User Defined Snippets for Markdown. Take a look at [User Defined Snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets) to find out how.

### **Compiling Markdown into HTML**

 VS Code integrates with Markdown compilers through the integrated [task runner](https://code.visualstudio.com/docs/editor/tasks). We can use this to compile .md files into .html files. Let's walk through compiling a simple Markdown document.

#### _Step 1: Install a Markdown compiler_

For this walkthrough, we use the popular Node.js module, markdown-it.
npm install -g markdown-it

~ __Note__: There are many Markdown compilers to choose from beyond markdown-it. Pick the one that best suits your needs and environment.

~ __Python__: using python to install markdown-it. pip install markdown-it-py

#### _Step 2: Create a simple MD file_

Open VS Code on an empty folder and create a sample.md file.

> **Note:** There are many Markdown compilers to choose from beyond markdown-it. Pick the one that best suits your needs and environment.

Place the following source code in that file:
>> Hello Markdown in VS Code!
This is a simple introduction to compiling Markdown in VS Code.
Things you'll need:
+ [Node.js](https://nodejs.org)
+ [markdown-it](https://www.npmjs.com/package/markdown-it)
+ [tasks.json](/docs/editor/tasks)

## Section Title

> This block quote is here for your information.

#### _Step 3: Create tasks.json_

The next step is to set up the task configuration file tasks.json. To do this, run Terminal > Configure Tasks and click Create tasks.json file from templates. VS Code then presents a list of possible tasks.json templates to choose from. Select Others since we want to run an external command.

This generates a tasks.json file in your workspace .vscode folder with the following content:
>> {
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "echo",
      "type": "shell",
      "command": "echo Hello"
    }
  ]
}

>>.... To use markdown-it to compile the Markdown file, change the contents as follows:

>>{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile Markdown",
      "type": "shell",
      "command": "markdown-it sample.md -o sample.html",
      "group": "build"
    }
  ]
}

> *Tip:* While the sample is there to help with common configuration settings, IntelliSense is available for the tasks.json file as well to help you along. Use ⌃Space to see the available settings.

#### _Step 4: Run the Build Task_
Since in more complex environments there can be more than one build task we prompt you to pick the task to execute after pressing ⇧⌘B (Run Build Task). In addition, we allow you to scan the output for compile problems. Since we only want to convert the Markdown file to HTML select Never scan the build output from the presented list.
At this point, you should see an additional file show up in the file list sample.html
If you want to make the Compile Markdown task the default build task to run execute Configure Default Build Task from the global Terminal menu and select Compile Markdown from the presented list. The final tasks.json file will then look like this:
>> {
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile Markdown",
      "type": "shell",
      "command": "markdown-it test.md -o test.html",
      "problemMatcher": [],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
