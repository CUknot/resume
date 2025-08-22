<script lang="ts">
  export let name = "";
  export let jobTitle = "";
  export let phone = "";
  export let email = "";
  export let github = "";
  export let linkedin = "";
  export let location = "";
  export let website = "";
</script>

<div class="text-center border-b border-gray-300 pb-4 mb-6">
  <!-- Name + Job Title -->
  <h1
    class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold tracking-tight"
  >
    {name}
  </h1>
  <p class="text-base sm:text-lg md:text-xl text-gray-600 font-medium mb-2">
    {jobTitle}
  </p>

  <!-- Contact Info in one line -->
  <p class="contact-info text-sm sm:text-base text-gray-700 flex flex-wrap justify-center gap-x-2 gap-y-1">
    {#if phone}
      <a href="tel:{phone}" class="hover:text-green-600">{phone}</a>
    {/if}
    {#if email}
      • <a href="mailto:{email}" class="hover:text-green-600">{email}</a>
    {/if}
    {#if location}
      • {location}
    {/if}
    {#if github}
      • <a href="https://github.com/{github}" target="_blank" rel="noreferrer" class="hover:text-green-600">
        github.com/{github}
      </a>
    {/if}
    {#if website}
      • <a href="https://{website}" target="_blank" rel="noreferrer" class="hover:text-green-600">
        {website}
      </a>
    {/if}
    {#if linkedin}
      • <a href="https://linkedin.com/in/{linkedin}" target="_blank" rel="noreferrer" class="hover:text-green-600">
        linkedin.com/in/{linkedin}
      </a>
    {/if}
  </p>
</div>

<style>
  a {
    text-decoration: underline;
  }

  @media print {
    a {
      color: black !important;
      text-decoration: none;
    }
    .hover\:text-green-600 {
      color: black !important;
    }
    /* Make contact info more compact for print */
    .contact-info {
      font-size: 0.8rem !important; /* smaller than normal text */
      line-height: 1.2 !important;
      gap: 0.3rem !important; /* reduce spacing */
      flex-wrap: nowrap !important; /* keep in one line if possible */
    }
  }
</style>
