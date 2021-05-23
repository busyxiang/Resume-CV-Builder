<script>
  import data from "./en";
  import html2pdf from "html2pdf.js";

  function exportToPDF() {
    document.body.classList.add("scale-cv");

    let areaCv = document.getElementById("area-cv");

    let exportOptions = {
      margin: 0,
      filename: "Resume.pdf",
      image: { type: "jpeg", quality: 0.98 },
      html2canvas: { scale: 4 },
      jsPDF: { format: "a4", orientation: "portrait" },
    };
    html2pdf(areaCv, exportOptions);

    setTimeout(() => {
      document.body.classList.remove("scale-cv");
    }, 5000);
  }

  function toggleDarkMode() {
    let themeButton = document.getElementById("theme-button");

    document.body.classList.toggle("dark-theme");
    themeButton.classList.toggle("bx-sun");
  }
</script>

<div class="l-main bd-container">
  <div class="resume" id="area-cv">
    <div class="resume_left">
      <section class="home">
        <div class="home_container section bd-grid">
          <div class="home_data bd-grid">
            <img src="profile.jpg" alt="profile_pic" class="home_img" />

            <h1 class="home_title">{data.name}</h1>
            <h3 class="home_profession">{data.job_title}</h3>

            <div>
              <a
                download=""
                href="output/ResumeCV.pdf"
                class="home_button-movil"
              >
                Download
              </a>
            </div>
          </div>

          <div class="home_address bd-grid">
            <span class="home_information">
              <i class="bx bx-map home_icon" />
              {data.location}
            </span>
            <span class="home_information">
              <i class="bx bx-envelope home_icon" />
              {data.email}
            </span>
            {#if data.contact_number?.length > 0}
              <span class="home_information">
                <i class="bx bx-phone home_icon" />
                {data.contact_number}
              </span>
            {/if}
          </div>
        </div>

        <i
          class="bx bx-moon change-theme"
          title="Theme"
          id="theme-button"
          on:click={toggleDarkMode}
        />

        <i
          class="bx bx-download generate-pdf"
          title="Generate PDF"
          id="resume-button"
          on:click={exportToPDF}
        />
      </section>

      <section class="links section">
        <h2 class="section-title">Links</h2>

        <div class="links_container bd-grid">
          {#each data.links as link}
            <a href={link.url} target="_blank" class="links_link">
              <i class="bx {link.icon_class} links_icon" />
              {link.url}
            </a>
          {/each}
        </div>
      </section>

      <section class="profile section">
        <h2 class="section-title">Profile</h2>

        <p class="profile_description">{data.profile_description}</p>
      </section>

      <section class="education section">
        <h2 class="section-title">Education</h2>

        <div class="education_container bd-grid">
          {#each data.educations as education, index}
            <div class="education_content">
              <div class="education_time">
                <span class="education_rounder" />
                {#if index !== data.educations.length - 1}
                  <span class="education_line" />
                {/if}
              </div>

              <div class="education_data bd-grid">
                <h3 class="education_title">{education.course}</h3>
                <span class="education_studies">{education.school}</span>
                <span class="education_year">{education.year}</span>
              </div>
            </div>
          {/each}
        </div>
      </section>

      <section class="skills section">
        <h2 class="section-title">Skills</h2>

        <div class="skills_content bd-grid">
          {#each data.skills as section}
            <ul class="skills_data">
              {#each section as skill}
                <li class="skills_name">
                  <span class="skills_circle" />
                  {skill}
                </li>
              {/each}
            </ul>
          {/each}
        </div>
      </section>
    </div>
    <div class="resume_right">
      <section class="experience section">
        <h2 class="section-title">Experience</h2>

        <div class="experience_container bd-grid">
          {#each data.work_experience as experience, i}
            <div class="experience_content">
              <div class="experience_time">
                <span class="experience_rounder" />
                {#if i !== data.work_experience.length - 1}
                  <span class="experience_line" />
                {/if}
              </div>

              <div class="experience_data bd-grid">
                <h3 class="experience_title">{experience.position}</h3>
                <span class="experience_company"
                  >{experience.year} | {experience.company}</span
                >
                <p class="experience_description">
                  <!-- {experience.description.join("\n")} -->
                  {experience.description.join("")}
                </p>
              </div>
            </div>
          {/each}
        </div>
      </section>

      {#if data.certificates && data.certificates.length > 0}
        <section class="certificate section">
          <h2 class="section-title">Certificates</h2>

          <div class="certificate_container bd-grid">
            {#each data.certificates as cert}
              <div class="certificate_content">
                <h3 class="certificate_title">{cert.title}</h3>
                <p class="certificate_description">{cert.description}</p>
              </div>
            {/each}
          </div>
        </section>
      {/if}

      {#if data.references}
        <section class="references section">
          <h2 class="section-title">References</h2>

          <div class="references_container bd-grid">
            {#each data.references as reference}
              <div class="references_content bd-grid">
                {#if reference.position.length > 0}
                  <span class="references_subtitle">{reference.position}</span>
                {/if}
                <h3 class="references_title">{reference.referee}</h3>
                <ul class="references_contact">
                  <li>{reference.contact_number}</li>
                  {#if reference.email.length > 0}
                    <li>{reference.email}</li>
                  {/if}
                </ul>
              </div>
            {/each}
          </div>
        </section>
      {/if}

      <section class="languages section">
        <h2 class="section-title">Languages</h2>

        <div class="languages_container">
          <ul class="languages_content bd-grid">
            {#each data.languages as language}
              <li class="languages_name">
                <span class="languages_circle" />
                {language}
              </li>
            {/each}
          </ul>
        </div>
      </section>
    </div>
  </div>
</div>

<style>
  .section {
    padding: 1.5rem 0;
  }

  .section-title {
    font-size: var(--h2-font-size);
    color: var(--title-color);
    font-weight: var(--font-semi-bold);
    text-transform: uppercase;
    letter-spacing: 0.35rem;
    text-align: center;
    margin-bottom: var(--mb-3);
  }

  .bd-container {
    max-width: 968px;
    width: calc(100% - 3rem);
    margin-left: var(--mb-3);
    margin-right: var(--mb-3);
  }

  .bd-grid {
    display: grid;
    gap: 1.5rem;
  }

  .home {
    position: relative;
  }

  .home_container {
    gap: 3rem;
  }

  .home_data {
    gap: 0.5rem;
    text-align: center;
  }

  .home_img {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    justify-self: center;
    margin-bottom: var(--mb-1);
  }

  .home_title {
    font-size: var(--h1-font-size);
  }

  .home_profession {
    font-size: var(--normal-font-size);
    margin-bottom: var(--mb-1);
  }

  .home_address {
    gap: 1rem;
  }

  .home_information {
    display: flex;
    align-items: center;
  }

  .home_icon {
    font-size: 1.2rem;
    margin-right: 0.25rem;
  }

  .home_button-movil {
    display: inline-block;
    border: 2px solid var(--text-color);
    color: var(--title-color);
    padding: 1rem 2rem;
    border-radius: 0.25rem;
    transition: 0.3s;
    font-weight: var(--font-medium);
    margin-top: var(--mb-3);
  }

  .home_button-movil:hover {
    background-color: var(--text-color);
    color: var(--container-color);
  }

  .links_container {
    grid-template-columns: max-content;
    gap: 1rem;
  }

  .links_link {
    display: inline-flex;
    align-items: center;
    font-size: var(--small-font-size);
    color: var(--text-color);
  }

  .links_link:hover {
    color: var(--title-color);
  }

  .links_icon {
    font-size: 1.2rem;
    margin-right: 0.25rem;
  }

  .profile_description {
    text-align: center;
  }

  .education_content,
  .experience_content {
    display: flex;
  }

  .education_time,
  .experience_time {
    padding-right: 1rem;
  }

  .education_rounder,
  .experience_rounder {
    position: relative;
    display: block;
    width: 16px;
    height: 16px;
    background-color: var(--text-color-light);
    border-radius: 50%;
    margin-top: 0.25rem;
  }

  .education_line,
  .experience_line {
    display: block;
    width: 2px;
    height: 110%;
    background-color: var(--text-color-light);
    transform: translate(7px, 0);
  }

  .education_data,
  .experience_data {
    gap: 0.5rem;
  }

  .education_title,
  .experience_title {
    font-size: var(--h3-font-size);
  }

  .education_studies,
  .experience_company {
    font-size: var(--small-font-size);
    color: var(--title-color);
  }

  .education_year {
    font-size: var(--smaller-font-size);
  }

  .skills_content,
  .languages_content {
    grid-template-columns: repeat(2, 1fr);
  }

  .languages_content {
    gap: 0;
  }

  .skills_name,
  .languages_name {
    display: flex;
    align-items: center;
    margin-bottom: var(--mb-3);
  }

  .skills_circle,
  .languages_circle {
    display: inline-block;
    width: 5px;
    height: 5px;
    background-color: var(--text-color);
    border-radius: 50%;
    margin-right: 0.75rem;
  }

  .certificate_title {
    font-size: var(--h3-font-size);
    margin-bottom: var(--mb-1);
  }

  .references_content {
    gap: 0.25rem;
  }

  .references_subtitle {
    color: var(--text-color-light);
  }

  .references_subtitle,
  .references_contact {
    font-size: var(--smaller-font-size);
  }

  .references_title {
    font-size: var(--h3-font-size);
  }

  .change-theme {
    position: absolute;
    right: 0;
    top: 2.2rem;
    display: flex;
    color: var(--text-color);
    font-size: 1.2rem;
    cursor: pointer;
  }

  .change-theme:hover {
    color: var(--title-color);
  }

  .generate-pdf {
    display: none;
    position: absolute;
    top: 2.2rem;
    left: 0;
    font-size: 1.2rem;
    color: var(--text-color);
    cursor: pointer;
  }

  .generate-pdf:hover {
    color: var(--title-color);
  }

  :global(.scale-cv .change-theme),
  :global(.scale-cv .generate-pdf) {
    display: none;
  }

  :global(.scale-cv .bd-container) {
    max-width: 595px;
  }

  :global(.scale-cv .section) {
    padding: 1.5rem 0 0.8rem;
  }

  :global(.scale-cv .section-title) {
    margin-bottom: 0.75rem;
  }

  :global(.scale-cv .resume_left),
  :global(.scale-cv .resume_right) {
    padding: 0 1rem;
  }

  :global(.scale-cv .home_img) {
    width: 90px;
    height: 90px;
  }

  :global(.scale-cv .home_container) {
    gap: 1.5rem;
  }

  :global(.scale-cv .home_data) {
    gap: 0.25rem;
  }

  :global(.scale-cv .home_address),
  :global(.scale-cv .links_container) {
    gap: 0.75rem;
  }

  :global(.scale-cv .home_icon),
  :global(.scale-cv .links_icon) {
    font-size: 1rem;
  }

  :global(.scale-cv .education_container),
  :global(.scale-cv .experience_container),
  :global(.scale-cv .certificate_container) {
    gap: 1rem;
  }

  :global(.scale-cv .education_time),
  :global(.scale-cv .experience_time) {
    padding-right: 0.5rem;
  }

  :global(.scale-cv .education_rounder),
  :global(.scale-cv .experience_rounder) {
    width: 11px;
    height: 11px;
    margin-top: 0.22rem;
  }

  :global(.scale-cv .education_line),
  :global(.scale-cv .experience_line) {
    width: 1px;
    height: 110%;
    transform: translate(5px, 0);
  }

  :global(.scale-cv .education_data),
  :global(.scale-cv .experience_data) {
    gap: 0.5rem;
  }

  :global(.scale-cv .skills_name) {
    margin-bottom: var(--mb-1);
  }

  @media screen and (min-width: 968px) {
    .bd-container {
      margin-left: auto;
      margin-right: auto;
    }

    .resume {
      display: grid;
      grid-template-columns: 0.5fr 1fr;
      background-color: var(--container-color);
      box-shadow: 0 0 8px rgba(13, 12, 12, 0.15);
    }

    .resume_left {
      background-color: var(--container-color-alt);
    }

    .resume_left,
    .resume_right {
      padding: 0 1.5rem;
    }

    .generate-pdf {
      display: inline-block;
    }

    :global(.scale-cv .generate-pdf) {
      display: none;
    }

    .section-title,
    .profile_description {
      text-align: initial;
    }

    .home_container {
      gap: 1.5rem;
    }

    .home_button-movil {
      display: none;
    }

    .references_container {
      grid-template-columns: repeat(2, 1fr);
    }

    .languages_content {
      grid-template-columns: repeat(3, max-content);
      column-gap: 3.5rem;
    }
  }
</style>
