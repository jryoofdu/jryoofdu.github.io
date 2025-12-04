---
layout: default
title: CV
cv_pdf: cv.pdf
permalink: /cv/
nav: true
nav_order: 3
---

<div class="cv-container" style="width: 100%; height: 100vh;">
  <embed src="{{ page.cv_pdf | prepend: 'assets/pdf/' | relative_url }}" type="application/pdf" width="100%" height="100%" />
</div>

<p style="margin-top: 1rem;">
  If the PDF doesn't display, you can <a href="{{ page.cv_pdf | prepend: 'assets/pdf/' | relative_url }}" target="_blank" rel="noopener noreferrer">download it here</a>.
</p>
