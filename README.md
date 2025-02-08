# SciPad Hover Answers Fix for PDF.js

A hacky bookmarklet for fixing mouse-hover previews of SciPad Answers in Firefox's in-built PDF Viewer, PDF.js. This fixes an incompatibility where push buttons without action dictionaries were not supported.

## Usage

1. Copy the code to your clipboard:

   ```javascript
   javascript:(function(){function getTargetId(e){var t=e.match(/pdfjs_internal_id_(\d+)([A-Za-z]+)/);if(t){var n=parseInt(t[1],10),a=t[2];return"pdfjs_internal_id_"+(n-1)+a}return null}function processButtons(){document.querySelectorAll("section.pushButton").forEach(function(e){if(!e.dataset.hoverEnabled){var t=getTargetId(e.id);if(t){var n=document.getElementById(t);n&&(e.dataset.hoverEnabled="true",e.dataset.actionDictionary||(e.dataset.actionDictionary=JSON.stringify({S:"URI",URI:"#"}),e.actionDictionary={S:"URI",URI:"#"}),e.addEventListener("mouseenter",function(){n.style.visibility="visible"}),e.addEventListener("mouseleave",function(){n.style.visibility="hidden"}))}}})}processButtons();new%20MutationObserver(processButtons).observe(document,{childList:!0,subtree:!0})})();
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

