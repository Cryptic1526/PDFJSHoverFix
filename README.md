# SciPad Hover Answers Fix for PDF.js

A hacky bookmarklet for fixing mouse-hover previews of SciPad Answers in Firefox's in-built PDF Viewer, PDF.js. This fixes an incompatibility where push buttons without action dictionaries were not supported.

## Usage

1. Copy the code to your clipboard:

   ```javascript
   javascript:(function(){function getTargetId(t){var e=t.match(/pdfjs_internal_id_(\d+)([A-Za-z]+)/);if(e){var n=parseInt(e[1],10),a=e[2];return"pdfjs_internal_id_"+(n-1)+a}return null}document.querySelectorAll("section.pushButton").forEach(function(t){var e=getTargetId(t.id);if(e){var n=document.getElementById(e);n&&(t.dataset.actionDictionary||(t.dataset.actionDictionary=JSON.stringify({S:"URI",URI:"#"}),t.actionDictionary={S:"URI",URI:"#"}),t.addEventListener("mouseenter",function(){n.style.visibility="visible"}),t.addEventListener("mouseleave",function(){n.style.visibility="hidden"}))}})})();
   ```

2. Create a new bookmark in your browser.
3. Paste the code into the URL field of the bookmark.
4. Save the bookmark.
5. Open a PDF in PDF.js and click the bookmarklet to turn on the fix.

## How It Works
- Finds push buttons in the PDF and checks if they have action dictionaries.
- If it's not there, it assigns a default dictionary.

If you don't trust the code, give it to chatgpt to explain what it does.

## Disclaimer
This is an extremely hacky workaround and will probably break with future PDF.js updates. Use at your own risk!

Feel free to contribute :)

## License
MIT License

