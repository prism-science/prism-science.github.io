---
title: "Work With Us"
layout: single
permalink: /work-with-us/
---

<style>
/* Tab container */
.wwu-tabs { margin: 0 0 2em 0; }

/* Hide radio buttons */
.wwu-tabs input[type="radio"] { display: none; }

/* Tab labels */
.wwu-tabs label {
  display: inline-block;
  padding: 0.75em 1.5em;
  margin-right: 0.25em;
  cursor: pointer;
  font-weight: 600;
  border-bottom: 3px solid transparent;
  color: #555;
  transition: color 0.2s, border-color 0.2s;
}
.wwu-tabs label:hover { color: #000; }

/* Active tab label */
.wwu-tabs input#tab-careers:checked ~ .wwu-labels label[for="tab-careers"],
.wwu-tabs input#tab-engage:checked ~ .wwu-labels label[for="tab-engage"] {
  color: #000;
  border-bottom: 3px solid #D34F1D;
}

/* Tab content panels */
.wwu-panel { display: none; padding: 1.5em 0; }
.wwu-tabs input#tab-careers:checked ~ .wwu-panel-careers { display: block; }
.wwu-tabs input#tab-engage:checked ~ .wwu-panel-engage { display: block; }

/* Job cards */
.job-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 1.25em 1.5em;
  margin-bottom: 1em;
  transition: box-shadow 0.2s;
}
.job-card:hover { box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
.job-card h3 { margin: 0 0 0.5em 0; font-size: 1.1em; }
.job-card a {
  text-decoration: none;
  font-weight: 600;
  color: #1F395F;
}
.job-card a:hover { text-decoration: underline; }
.job-card p { margin: 0; color: #666; font-size: 0.9em; }
</style>

<div class="wwu-tabs">
  <!-- Radio inputs (default: Careers) -->
  <input type="radio" name="wwu" id="tab-careers" checked>
  <input type="radio" name="wwu" id="tab-engage">

  <!-- Tab labels -->
  <div class="wwu-labels">
    <label for="tab-careers"><i class="fas fa-briefcase"></i> Careers</label>
    <label for="tab-engage"><i class="fas fa-flask"></i> Scientifically Engage</label>
  </div>

  <!-- Panel: Careers -->
  <div class="wwu-panel wwu-panel-careers">
    <p>We're hiring! The DiffUSE Project is looking for scientists passionate about understanding protein dynamics. View the full descriptions and apply through the links below.</p>

    <div class="job-card">
      <h3><a href="https://jobs.ashbyhq.com/astera/c68cd9fd-59fb-4d0f-bf56-4b7d1b2e1e90" target="_blank" rel="noopener">Scientist — Ensemble Structural Informatics</a></h3>
      <p>Astera Institute</p>
    </div>


    <div class="job-card">
      <h3><a href="https://jobs.ashbyhq.com/astera/7c45ab2e-f341-4fef-a3f3-659abe852d71" target="_blank" rel="noopener">Scientist - Computational Biophysics</a></h3>
      <p>Astera Institute</p>
    </div>

    <div class="job-card">
      <h3><a href="https://jobs.ashbyhq.com/astera/cded582c-8965-4795-968c-c632a5112e82" target="_blank" rel="noopener">Research Assistant - Structural Bioinformatics</a></h3>
      <p>Astera Institute</p>
    </div>

    <div class="job-card">
      <h3><a href="https://jobs.ashbyhq.com/astera/bb7496f8-3342-4d8f-a5c6-e891fefa3b0e" target="_blank" rel="noopener">General DiffUSE Job Application</a></h3>
      <p>Astera Institute</p>
    </div>

     <p>Contact us at diffuse [at] radial [dot] org with questions.</p>

  </div>

  <!-- Panel: Scientifically Engage -->
  <div class="wwu-panel wwu-panel-engage">
    <p>Interested in collaborating with the DiffUSE Project? Fill out the form below to get in touch.</p>

    <iframe src="https://docs.google.com/forms/d/e/1FAIpQLSdaTvW3fGYx_53s7cTm7E63SAUdeweCA4KEja6HHSLj9J5WnQ/viewform?embedded=true" width="100%" height="800" frameborder="0" marginheight="0" marginwidth="0">Loading…</iframe>

    <p>Contact us at diffuse [at] radial [dot] org with questions. </p>

  </div>
</div>
