<template>
  
  <footer class="border-t border-gray-200 dark:border-gray-800
                 bg-white dark:bg-gray-950 py-8 px-6">
    <div class="max-w-5xl mx-auto flex flex-col md:flex-row 
                items-center justify-between gap-4">

      <!-- Logo -->
      <span class="font-mono text-emerald-600 dark:text-emerald-400 font-bold">
        &lt;MOUSSAIF SAAD  /&gt;
      </span>

      <!-- Copyright -->
      <span class="font-mono text-xs text-gray-400">
        © 2026 — {{ t.footer.copy }}
      </span>

      

    </div>
  </footer>
</template>

<script>
export default {
  name: 'FooterSection',

  props: {
    t: Object,
  },
}
</script>