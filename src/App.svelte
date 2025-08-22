<script lang="ts">
  import Intro from "./components/Intro.svelte";
  import Work from "./components/Work.svelte";
  import HideToggle from "./HideToggle.svelte";
  import {
    educations,
    fullVersionLink,
    introData,
    projects,
    activities,
    certs,
    sourceLink,
    technologies,
    workExperiences,
    interests
  } from "./data";

  let editMode = false;

  function toggleMode() {
    editMode = !editMode;
  }
</script>

<header
  class="web-only text-center p-6 bg-gradient-to-r from-green-600 to-emerald-500 text-white shadow-md"
>
  <h1 class="text-5xl font-bold mb-2 tracking-wide">Resumette</h1>
  <div class="flex justify-center gap-6 mb-4">
    <button on:click={toggleMode} class="hover:underline text-lg font-medium">
      {editMode ? "[View]" : "[Edit]"}
    </button>
    <button on:click={() => window.print()} class="hover:underline text-lg font-medium">
      [Print]
    </button>
  </div>
  <p class="max-w-2xl mx-auto text-sm opacity-90 leading-relaxed">
    Printer-friendly résumé template by
    <a href="https://github.com/narze/resume" class="underline">narze</a> · adapted from
    <a href="https://github.com/Leomotors/resumette" class="underline">Leomotor</a>.  
    Sections with <code>web-only</code> are hidden on print.
  </p>
  <p class="text-sm mt-2 opacity-90">
    You can toggle <button on:click={toggleMode} class="underline">[Edit Mode]</button> to hide sections before printing.  
    (<a href={sourceLink} target="_blank" rel="noopener" class="underline">Source</a>)
  </p>
</header>

<main
  class="p-4 m-0 md:m-8 xl:mx-auto max-w-screen-lg {editMode ? 'edit-mode' : 'display-mode'} text-gray-800"
>
  <Intro {...introData} />

  <!-- Skills -->
  <section>
    <HideToggle />
    <h2>Skills</h2>
    <hr />
    <table class="w-full text-left">
      {#each technologies as tech}
        <tr class="align-top">
          <td class="font-semibold pr-4 w-[10rem]">{tech.section}</td>
          <td class="flex flex-wrap gap-2">
            {#each tech.details as item}
              <span class="px-2 py-1 bg-gray-100 rounded-lg text-sm">{item}</span>
            {/each}
          </td>
        </tr>
      {/each}
    </table>
  </section>

  <!-- Work -->
  <section>
    <HideToggle />
    <h2>Work Experience</h2>
    <hr />
    {#each workExperiences as exp}
      <HideToggle />
      <Work {...exp} />
    {/each}
  </section>

  <!-- Education -->
  <section>
    <HideToggle />
    <h2>Education</h2>
    <hr />
    <ul>
      {#each educations as edu}
        <li>
          <HideToggle />
          <strong>{edu.head}</strong>, {edu.details}
        </li>
      {/each}
    </ul>
  </section>

  <!-- Projects -->
  <section>
    <HideToggle />
    <h2>Projects</h2>
    <hr />

    <ul>
      {#each projects as project}
        <li>
          <HideToggle />
          {#if project.url !== ""}
            <a
                href={`https://${project.url}`}
                target="_blank"
                rel="noreferrer"
                class="font-semibold text-green-600 hover:underline"
              >
                {project.name}
            </a>
          {:else}
            <span class="font-semibold">{project.name}</span>
          {/if}
          <span class="text-sm text-gray-500">({project.stack})</span>
          <p class="text-gray-700 text-sm">{project.details}</p>
          <a
            href={`https://${project.github}`}
            target="_blank"
            rel="noreferrer"
            class="text-xs text-blue-600 hover:underline"
          >
            {project.github}
          </a>
        </li>
      {/each}
    </ul>
  </section>

  <!-- Activities -->
  <section>
    <HideToggle />
    <h2>Activities</h2>
    <hr />
    <ul>
      {#each activities as act}
        <li class="mb-3">
          <HideToggle />
          <strong>{act.name}</strong>
          <p class="text-sm text-gray-700">{act.details}</p>
        </li>
      {/each}
    </ul>
  </section>

  <!-- Interests -->
  <section>
    <HideToggle />
    <h2>Interests</h2>
    <hr />
    <ul>
      {#each interests as interest}
        <li>
          <HideToggle />
          <strong>{interest.name}</strong> - <i>{interest.details}</i>
        </li>
      {/each}
    </ul>
  </section>
</main>

<style lang="postcss">
  main {
    overflow-x: hidden;
  }

  a {
    text-decoration: underline;
  }

  section {
    @apply my-6 p-4 text-left bg-white shadow-sm rounded-xl border-l-4 border-green-500;
  }

  section h2 {
    @apply text-2xl font-bold uppercase tracking-wide mb-3;
  }

  section hr {
    @apply mt-0 mb-3;
    border-color: #d1d5db;
  }

  section > ul {
    @apply list-disc pl-6;
  }

  li {
    margin: 6px 0;
  }

  :global(.print-only) {
    display: none;
  }

  :global(main.display-mode .hide-toggle) {
    display: none;
  }

  /* Print Styles */
  @media print {
    * {
      @apply text-xs;
      color: black !important;
    }

    :global(.print-only) {
      display: block;
    }

    :global(.web-only) {
      display: none;
    }

    section {
      @apply my-2 p-0 shadow-none border-l-0;
    }

    section h2 {
      @apply text-base mb-1;
    }

    section hr {
      border-bottom: 1px solid #aaa;
      margin-bottom: 4px;
    }

    ul {
      @apply pl-5;
    }

    main {
      margin: 0;
      padding: 10px;
    }

    @page {
      margin: 10mm;
    }
  }
</style>
