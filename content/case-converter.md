---
title: Case Converter
description: Free case converter to instantly change text to UPPERCASE, lowercase, Title Case, Sentence case, or Alternating case.
eleventyNavigation:
  key: Case Converter
  order: 3
---

# Case Converter

Paste your text below and instantly convert it to UPPERCASE, lowercase, Title Case, Sentence case, or Alternating case.

<div id="case-tool" style="margin: 1rem 0;">
  <label for="case-text"><strong>Paste your text</strong></label>
  <textarea id="case-text" rows="10" style="width:100%; padding:12px; font-size:16px;" placeholder="Paste or type here..."></textarea>

  <div style="display:flex; gap:10px; flex-wrap:wrap; margin-top:12px;">
    <button type="button" data-action="upper" style="padding:10px 12px; cursor:pointer;">UPPERCASE</button>
    <button type="button" data-action="lower" style="padding:10px 12px; cursor:pointer;">lowercase</button>
    <button type="button" data-action="title" style="padding:10px 12px; cursor:pointer;">Title Case</button>
    <button type="button" data-action="sentence" style="padding:10px 12px; cursor:pointer;">Sentence case</button>
    <button type="button" data-action="alt" style="padding:10px 12px; cursor:pointer;">aLtErNaTiNg</button>
    <button type="button" data-action="copy" style="padding:10px 12px; cursor:pointer;">Copy</button>
    <button type="button" data-action="clear" style="padding:10px 12px; cursor:pointer;">Clear</button>
  </div>

  <p id="case-status" style="margin-top:10px;"></p>
</div>

<script>
(function () {
  const textEl = document.getElementById("case-text");
  const statusEl = document.getElementById("case-status");
  const tool = document.getElementById("case-tool");

  function setStatus(msg) {
    statusEl.textContent = msg || "";
    if (msg) setTimeout(() => (statusEl.textContent = ""), 1500);
  }

  function toTitleCase(str) {
    return str.toLowerCase().replace(/\b([a-z])([a-z']*)/g, (m, first, rest) => {
      return first.toUpperCase() + rest;
    });
  }

  function toSentenceCase(str) {
    const lower = str.toLowerCase();
    // Capitalise first letter after start or after . ! ?
    return lower.replace(/(^\s*[a-z])|([.!?]\s+[a-z])/g, (match) => match.toUpperCase());
  }

  function toAlternating(str) {
    let i = 0;
    return str.replace(/[a-z]/gi, (ch) => {
      const out = (i % 2 === 0) ? ch.toLowerCase() : ch.toUpperCase();
      i++;
      return out;
    });
  }

  async function copyToClipboard() {
    try {
      await navigator.clipboard.writeText(textEl.value || "");
      setStatus("Copied!");
    } catch (e) {
      // Fallback: select text
      textEl.focus();
      textEl.select();
      document.execCommand("copy");
      setStatus("Copied!");
    }
  }

  tool.addEventListener("click", async (e) => {
    const btn = e.target.closest("
