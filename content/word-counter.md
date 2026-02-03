---
title: Word Counter
description: Free online word counter for essays, documents, work, and study. Instantly count words, characters, and reading time.
eleventyNavigation:
  key: Word Counter
  order: 2
---
# Word Counter

Paste your text below to instantly count words, characters, and reading time.

**This tool also works as a character counter**, counting characters with and without spaces.



> The interactive word counter tool will appear here next.

<div id="wc-tool" style="margin: 1rem 0;">
  <label for="wc-text"><strong>Paste your text</strong></label>
  <textarea id="wc-text" rows="10" style="width:100%; padding:12px; font-size:16px;" placeholder="Paste or type here..."></textarea>

  <div style="display:flex; gap:12px; flex-wrap:wrap; margin-top:12px;">
    <div><strong>Words:</strong> <span id="wc-words">0</span></div>
    <div><strong>Characters (with spaces):</strong> <span id="wc-chars">0</span></div>
    <div><strong>Characters (no spaces):</strong> <span id="wc-chars-nospace">0</span></div>
    <div><strong>Reading time:</strong> <span id="wc-reading">0 min</span></div>
  </div>

  <button id="wc-clear" type="button" style="margin-top:12px; padding:10px 14px; cursor:pointer;">
    Clear
  </button>
</div>

<script>
(function () {
  const textEl = document.getElementById("wc-text");
  const wordsEl = document.getElementById("wc-words");
  const charsEl = document.getElementById("wc-chars");
  const charsNoSpaceEl = document.getElementById("wc-chars-nospace");
  const readingEl = document.getElementById("wc-reading");
  const clearBtn = document.getElementById("wc-clear");

  function updateCounts() {
    const text = textEl.value || "";

    const words = text.trim() ? text.trim().split(/\s+/).filter(Boolean).length : 0;
    const chars = text.length;
    const charsNoSpace = text.replace(/\s/g, "").length;

    const minutes = words === 0 ? 0 : Math.max(1, Math.ceil(words / 200));

    wordsEl.textContent = String(words);
    charsEl.textContent = String(chars);
    charsNoSpaceEl.textContent = String(charsNoSpace);
    readingEl.textContent = minutes + " min";
  }

  textEl.addEventListener("input", updateCounts);
  clearBtn.addEventListener("click", function () {
    textEl.value = "";
    updateCounts();
    textEl.focus();
  });

  updateCounts();
})();
</script>
